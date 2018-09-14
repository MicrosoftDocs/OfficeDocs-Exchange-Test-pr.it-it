---
title: 'Rollback migraz. cart. pubbl. Exchange 2013-Exchange 2016: Exchange 2013 Help'
TOCTitle: Eseguire il rollback di una migrazione di cartella pubblica da Exchange 2013 a Exchange 2016
ms:assetid: bcd54aa0-aa45-4c68-b504-1475842d4b96
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt798259(v=EXCHG.150)
ms:contentKeyID: 74432712
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Eseguire il rollback di una migrazione di cartella pubblica da Exchange 2013 a Exchange 2016

 

_**Ultima modifica dell'argomento:** 2017-03-20_

**Riepilogo:**  Seguire questa procedura affinché l'infrastruttura di cartelle pubbliche torni allo stato precedente alla migrazione nell'organizzazione di Exchange 2013 in locale.

Se si riscontrano problemi con la migrazione delle cartelle pubbliche in Exchange Online o per qualsiasi altro motivo è necessario riattivare le cartelle pubbliche di Exchange 2013, seguire la procedura seguente.

## Ripristino della migrazione

Tenere presente che se si esegue il rollback della migrazione, si perderà qualsiasi contenuto che è stato aggiunto alle cartelle pubbliche in Exchange Online dopo la migrazione tramite client o tramite posta elettronica per le cartelle pubbliche abilitate alla posta elettronica. Per salvare il contenuto, è possibile esportare il contenuto delle cartelle pubbliche dopo la migrazione in un file con estensione pst, che può poi essere importato in tutte le cartelle pubbliche in locale, una volta completato il rollback.

1.  Nell'ambiente Exchange locale, eseguire il seguente comando per sbloccare le cartelle pubbliche di Exchange 2013 (tenere presente che lo sblocco può richiedere diverse ore):
    
        Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false -PublicFoldersEnabled Local 

2.  Nell'ambiente Exchange locale, ripristinare `ExternalEmailAddress` di tutte le cartelle pubbliche abilitate alla posta elettronica che sono state aggiornate da SetMailPublicFolderExternalAddress.ps1 (lo script utilizzato nel *Passaggio 8: Testare e sbloccare le cartelle pubbliche in Exchange Online* di [Utilizzare la migrazione batch per migrare le cartelle pubbliche di Exchange 2013 a Exchange Online](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/batch-migration-of-exchange-2013-public-folders)). È possibile vedere il file di riepilogo creato dallo script per individuare quelle che sono state modificate o usare il file con estensione OnPrem\_MEPF.xml generato in precedenza nello stesso processo di migrazione batch per ottenere le proprietà originali per tutte le cartelle pubbliche abilitate alla posta elettronica.

3.  In Exchange Online PowerShell, utilizzare i seguenti comandi per rimuovere tutte le cartelle pubbliche e le cassette postali di Exchange Online:
    
        Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
        Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true

4.  Per reindirizzare il traffico di cartelle pubbliche in locale (Exchange 2013) nell'ambiente Exchange Online, eseguire il seguente comando:
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote

5.  Vedere [Configurare le cartelle pubbliche di Exchange 2013 per una distribuzione ibrida](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md) per istruzioni su come riconfigurare l’accesso alle cartelle pubbliche in locale, affinché gli utenti di Exchange Online possano accedervi.


---
title: 'Configurare le cartelle pubbliche di Exchange 2013 per una distribuzione ibrida: Exchange 2013 Help'
TOCTitle: Configurare le cartelle pubbliche di Exchange 2013 per una distribuzione ibrida
ms:assetid: b828520f-022c-4fcb-ab68-e1c330e87c33
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn986544(v=EXCHG.150)
ms:contentKeyID: 65296580
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare le cartelle pubbliche di Exchange 2013 per una distribuzione ibrida

 

_<strong>Si applica a:</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2016-12-09_

**Riepilogo:** istruzioni per l'abilitazione degli utenti di Exchange Online per accedere alle cartelle pubbliche locali nel proprio ambiente di Exchange 2013.

In una distribuzione ibrida, gli utenti possono essere in Exchange Online, locale o entrambe e le cartelle pubbliche sono costituiti in Exchange Online o locale. In alcuni casi potrebbe essere necessario gli utenti in linea di accedere alle cartelle pubbliche nell'ambiente locale di Exchange Server 2013. Allo stesso modo, gli utenti di Exchange 2013 potrebbe essere necessario accedere alle cartelle pubbliche in Office 365 o Exchange Online.


> [!NOTE]
> Se si dispone di cartelle pubbliche di Exchange 2010 o Exchange 2007, vedere <A href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">Configurare cartelle pubbliche locali legacy per una distribuzione ibrida</A>.



In questo articolo viene descritto come consentire agli utenti di Exchange Online/Office 365 accedere a cartelle pubbliche di Exchange 2013. Per consentire agli utenti di Exchange 2013 locale accedere alle cartelle pubbliche di Exchange Online, vedere [Configurare le cartelle pubbliche di Exchange Online per una distribuzione ibrida](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md).

Un utente di Exchange Online/Office 365 deve essere rappresentato da un oggetto MailUser nell'ambiente locale di Exchange per accedere alle cartelle pubbliche di Exchange 2013. Questo oggetto MailUser deve inoltre essere locale da utilizzare come destinazione gerarchia di cartelle pubbliche di Exchange 2013. Se si dispone di Office 365 gli utenti che attualmente non sono rappresentati locale da oggetti MailUser, fare riferimento all'articolo della Microsoft Knowledge Base ["utenti di Exchange Online non possono accedere alle cartelle pubbliche locali legacy"](https://go.microsoft.com/fwlink/p/?linkid=699451) 3106618 per creare entità locali corrispondenti.

## Che cosa è necessario sapere prima di iniziare

1.  Per queste istruzioni si presume che sia stata utilizzata la procedura guidata di configurazione ibrida per configurare e sincronizzare gli ambienti locale e Exchange Online e che i record DNS utilizzati per il servizio di individuazione automatica della maggior parte degli utenti faccia riferimento a un endpoint locale. Per ulteriori informazioni, vedere [Procedura guidata di configurazione ibrida](hybrid-configuration-wizard-exchange-2013-help.md).

2.  Queste istruzioni si presuppone che Outlook via Internet è attivato e funzionalità nei server di Exchange locale. Per informazioni su come abilitare Outlook via Internet, vedere [Outlook via Internet](https://technet.microsoft.com/it-it/library/bb123741\(v=exchg.150\)).

3.  Implementazione della coesistenza della cartella pubblica per una distribuzione ibrida di Exchange con Office 365 potrebbe essere necessario risolvere i conflitti durante la procedura di importazione. Conflitti possono verificarsi a causa di indirizzo di posta elettronica non instradabili assegnato a posta elettronica di cartelle pubbliche abilitate, è in conflitto con altri utenti e gruppi in Office 365 e gli altri attributi.

4.  Per accedere alle cartelle pubbliche in più strutture locali, è necessario aggiornare i relativi client Outlook con l'aggiornamento pubblico di Outlook di novembre 2012 o successivo.
    
    1.  Per scaricare novembre 2012 aggiornamento di Outlook per Outlook 2010, vedere [aggiornamenti per Microsoft Outlook 2010 (KB2687623) a 32-Bit Edition](https://www.microsoft.com/en-us/download/details.aspx?id=35702).
    
    2.  Per scaricare novembre 2012 aggiornamento di Outlook per Outlook 2007, vedere [aggiornamento per Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/en-us/download/details.aspx?id=35718).

5.  Outlook 2011 per Mac e Microsoft Outlook per Mac per Office 365 non sono supportate per le cartelle pubbliche tra locali. Gli utenti devono essere nello stesso percorso le cartelle pubbliche per accedervi con Outlook 2011 per Mac o Outlook per Mac per Office 365. Inoltre, gli utenti le cui cassette postali si trovano in Exchange Online saranno in grado di accedere alle cartelle pubbliche locali utilizzando Outlook Web App.
    

    > [!NOTE]
    > 2016 Outlook per Mac è supportato per le cartelle pubbliche tra locali. Se i client nell'organizzazione utilizzano 2016 Outlook per Mac, assicurarsi di che aver installato l'aggiornamento di aprile 2016. In caso contrario, gli utenti non potranno accedere alle cartelle pubbliche in una topologia ibrida. Per ulteriori informazioni, vedere <A href="https://technet.microsoft.com/it-it/library/mt788631(v=exchg.150)">Accesso alle cartelle pubbliche con Outlook 2016 per Mac</A>.



## Passaggio 1: Download degli script

1.  Scaricare i file seguenti [dall'Abilitati alla posta elettronica le cartelle pubbliche - script di sincronizzazione directory](https://www.microsoft.com/en-us/download/details.aspx?id=46381):
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  Salvare i file nel computer locale da cui si eseguirà PowerShell. Ad esempio, C:\\PFScripts.

## Passaggio 2: Configurare la sincronizzazione delle directory

Il servizio di sincronizzazione della Directory non sincronizza le cartelle pubbliche abilitate alla posta. Eseguire lo script seguente verranno sincronizzate le cartelle pubbliche abilitate alla posta in locale e Office 365. Autorizzazioni speciali assegnate alle cartelle pubbliche abilitate alla posta saranno necessario ricreare nel cloud dopo cross-premise autorizzazione non sono supportate negli scenari di distribuzione ibrida. Per ulteriori informazioni, vedere [Exchange hybrid deployment documentation](exchange-server-hybrid-deployments-exchange-2013-help.md).


> [!NOTE]
> Verranno visualizzata sincronizzate le cartelle pubbliche abilitate alla posta ai fini del flusso di posta gli oggetti contatto di posta elettronica e non sarà visualizzato nel EInterfaccia di amministrazione di Exchange. Vedere il comando Get-MailPublicFolder. Per ricreare le autorizzazioni SendAs nel cloud, utilizzare il comando Add-RecipientPermission.



1.  Exchange 2013 server, eseguire il comando seguente per sincronizzare le cartelle pubbliche abilitate alla posta elettronica dal computer locale in locale di Active Directory per Office 365.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    `Credential` indica password e nome utente di Office 365 e `CsvSummaryFile` il percorso in cui si desidera registrare gli errori e le operazioni di sincronizzazione, in formato .csv.


> [!NOTE]
> Prima di eseguire lo script, si consiglia di simulare le operazioni che verrebbero effettuate dallo script nell'ambiente eseguendolo come descritto in precedenza con il parametro <CODE>-WhatIf</CODE>.<BR>Si consiglia inoltre di eseguire questo script ogni giorno per sincronizzare le cartelle pubbliche abilitate alla posta.



## Passaggio 3: Configurare gli utenti di Exchange Online per accedere alle cartelle pubbliche di Exchange 2013 locale

Il passaggio finale di questa procedura è possibile configurare l'organizzazione Exchange online e consentire l'accesso alle cartelle pubbliche di Exchange 2013.

Abilitare l'organizzazione exchange online accedere alle cartelle pubbliche locale. Farà riferimento a tutti i è nella cartella pubblica cassette postali locali.

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3


> [!NOTE]
> È necessario attendere fino a quando non ha completato la sincronizzazione di ActiveDirectory per visualizzare le modifiche. Questo processo può richiedere fino a 3 ore. Se non si desidera attendere la sincronizzazione ricorrente che si verificano ogni tre ore, è possibile forzare la sincronizzazione delle directory in qualsiasi momento. Per informazioni dettagliate sulla procedura per forzare la sincronizzazione delle directory, vedere <A href="http://technet.microsoft.com/en-us/library/jj151771.aspx">forzare la sincronizzazione delle directory</A>.



## Come verificare se l'operazione ha avuto esito positivo

1.  Accedere a Outlook per un utente in Exchange Online ed effettuare i seguenti test sulle cartelle pubbliche:
    
      - Visualizzare la gerarchia.
    
      - Controllare le autorizzazioni.
    
      - Creare ed eliminare cartelle pubbliche.
    
      - Pubblicare il contenuto ed eliminare il contenuto da una cartella pubblica.


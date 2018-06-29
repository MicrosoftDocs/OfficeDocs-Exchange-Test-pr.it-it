---
title: 'Destinatari di provisioning per i download della Rubrica offline: Exchange 2013 Help'
TOCTitle: Destinatari di provisioning per i download della Rubrica offline
ms:assetid: 141751ac-16d3-4e3c-b70c-004aeedcb5a0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996345(v=EXCHG.150)
ms:contentKeyID: 50480033
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Destinatari di provisioning per i download della Rubrica offline

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-02-15_

Se si utilizzano Rubriche offline (OAB) nella propria organizzazione, esistono diversi modi per specificare quali destinatari eseguiranno il download di rubriche offline e di quali rubriche, nell'ambito della propria organizzazione:

  - **Per database delle cassette postali**   È possibile utilizzare Interfaccia di amministrazione di Exchange o Shell per eseguire il provisioning dei destinatari per i download della Rubrica offline collegando un database delle cassette postali a una Rubrica offline predefinita per i client Office Outlook 2007, Outlook 2010 e Outlook 2013.

  - **Per destinatario**   È possibile utilizzare il cmdlet **Set-Mailbox** in Shell per specificare quale rubrica offline viene scaricata collegandola direttamente ad una cassetta postale del destinatario.

  - **Per più destinatari **  È possibile utilizzare un comando con pipeline in Shell per specificare la Rubrica offline che più destinatari scaricano sulla base di attributi comuni.

  - **Criteri a livello di rubrica**   È possibile assegnare criteri a livello di rubrica all'account utente associato a una cassetta postale per specificare la Rubrica fuori rete da scaricare nella cassetta postale del destinatario. Se si assegnano criteri a livello di rubrica a un account utente a cui è già assegnata una Rubrica offline, la Rubrica offline esplicitamente assegnata alla cassetta postale avrà la precedenza. Per ulteriori informazioni, vedere [Assegnare un criterio della Rubrica per gli utenti di posta](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md).

Per altre attività di gestione relative alle rubriche offline, vedere [Procedure della Rubrica fuori rete](offline-address-book-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per eseguire queste procedure. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo di Shell per il provisioning dei destinatari per i download della Rubrica offline tramite il collegamento del database delle relative cassette postali ad un database di cartelle pubbliche o a una Rubrica offline predefinita

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Database delle cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

In questo esempio, viene configurata la distribuzione basata su Web di Rubrica offline personale per il database della cassetta postale predefinita.

    Set-MailboxDatabase -Identity "Mailbox Database" -OfflineAddressBook "My OAB"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\)).

## Utilizzo di Shell per specificare quale Rubrica offline verrà scaricata collegandola direttamente ad una cassetta postale del destinatario

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

Per specificare quale Rubrica offline verrà scaricata collegandola direttamente ad una cassetta postale del destinatario, utilizzare la seguente sintassi.

    Set-Mailbox -Identity <MailboxIDParameter> -OfflineAddressBook <OfflineAddressBookIdParameter>


> [!NOTE]
> Il parametro <EM>Identity</EM> consente di identificare la cassetta postale e può assumere i seguenti valori: GUID, ADObjectID, nome distinto (DN), <EM>domain\account</EM>, nome dell'entità utente (UPN), LegacyExchangeDN, SmtpAddress e alias.



In questo esempio, viene specificato che l'utente Kim scaricherà la Rubrica offline di My OAB.

    Set-Mailbox -Identity Kim -OfflineAddressBook "My OAB"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Utilizzo di Shell per specificare la Rubrica offline che verrà scaricata da più destinatari

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

In questo esempio, viene specificato che tutte le cassette postali degli utenti negli Stati Uniti per l'azienda Contoso scaricheranno la Rubrica offline Contoso Stati Uniti.

    Get-User -ResultSize Unlimited -Filter { Company -eq "Contoso" -and RecipientType -eq "UserMailbox" } | Where { $_.CountryOrRegion -eq "United States"} | Set-Mailbox -OfflineAddressBook "Contoso United States"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-User](https://technet.microsoft.com/it-it/library/aa996896\(v=exchg.150\)) e [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).


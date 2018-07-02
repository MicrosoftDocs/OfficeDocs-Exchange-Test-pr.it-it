---
title: 'Disabilitare le funzionalità selezionate per gli utenti di Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Disabilitare le funzionalità selezionate per gli utenti di Outlook Voice Access
ms:assetid: 37421edf-af60-4ca9-9e8b-262b8b851607
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg602126(v=EXCHG.150)
ms:contentKeyID: 50555568
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disabilitare le funzionalità selezionate per gli utenti di Outlook Voice Access

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

Outlook Voice Access contiene due interfacce: l'interfaccia utente telefonica (TUI) e l'interfaccia utente vocale (VUI). Per impostazione predefinita, quando gli utenti si connettono a Outlook Voice Access, possono accedere al calendario, alla posta elettronica e ai contatti personali ed eseguire ricerche nella directory. È possibile utilizzare Shell per impedire agli utenti di accedere a una o più di queste funzioni quando utilizzano Outlook Voice Access per accedere alla cassetta postale. Quando vengono modificate le funzionalità di Outlook Voice Access nel criterio cassetta postale di messaggistica unificata, le modifiche vengono applicate a tutti gli utenti associati al criterio cassetta postale di messaggistica unificata.

È possibile disattivare l'accesso degli utenti alle seguenti funzionalità di Outlook Voice Access nel criterio cassetta postale di messaggistica unificata:

  - Calendario

  - Directory

  - Email

  - Contatti personali

Per altre attività di gestione relative ai criteri cassetta postale di messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

È inoltre possibile utilizzare Shell per disabilitare le funzionalità di Outlook Voice Access sulla cassetta postale di un singolo utente abilitato alla messaggistica unificata. Quando si effettua questa operazione, le funzionalità vengono disabilitate solo per quell'utente. Anche se non è possibile disattivare tutte le funzionalità di Outlook Voice Access trovate nel criterio di messaggistica unificata per un singolo utente, è possibile disattivare l'accesso al calendario e alla posta elettronica.

Per le altre attività di gestione relative alle cassette postali di messaggistica unificata, vedere [Segreteria telefonica per gli utenti](voice-mail-for-users-exchange-2013-help.md).


> [!NOTE]
> È possibile utilizzare Shell solo per modificare le funzionalità di Outlook&nbsp;Voice Access per gli utenti abilitati alla messaggistica unificata su un criterio cassetta postale di messaggistica unificata o sulla cassetta postale di un utente abilitato alla messaggistica unificata.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, confermare che un utente è stato abilitato per la messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Disabilitazione delle funzionalità di Outlook Voice Access selezionate per gli utenti abilitati alla messaggistica unificata su un criterio cassetta postale di messaggistica unificata tramite Shell

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

In questo esempio si impedisce agli utenti associati a un criterio di cassette postali di messaggistica unificata denominato `MyUMMailboxPolicy` di accedere al calendario quando si connettono a Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToCalendar $false

In questo esempio si impedisce agli utenti associati a un criterio di cassette postali di messaggistica unificata denominato `MyUMMailboxPolicy` di accedere alla directory quando si connettono a Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToDirectory $false

In questo esempio si impedisce agli utenti associati a un criterio di cassette postali di messaggistica unificata denominato `MyUMMailboxPolicy` di accedere alla posta elettronica quando si connettono a Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToEmail -$false

In questo esempio si impedisce agli utenti associati a un criterio di cassette postali di messaggistica unificata denominato `MyUMMailboxPolicy` di accedere ai contatti personali quando si connettono a Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToPersonalContacts $false

## Disabilitazione delle funzionalità di Outlook Voice Access selezionate sulla cassetta postale di un singolo utente abilitato alla messaggistica unificata tramite Shell

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

In questo esempio viene disabilitato l'accesso al calendario su un cassetta postale di messaggistica unificata denominata tony@contoso.com quando l'utente si connette a Outlook Voice Access.

    Set-UMMailbox -id tony@contoso.com -TUIAccessToCalendarEnabled $false

In questo esempio viene disabilitato l'accesso alla posta elettronica su una cassetta postale di messaggistica unificata denominata tony@contoso.com quando l'utente si connette a Outlook Voice Access.

    Set-UMMailbox -id tony@contoso.com -TUIAccessToEmailEnabled $false


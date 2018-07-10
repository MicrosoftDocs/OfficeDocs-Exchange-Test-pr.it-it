---
title: 'Set di funzionalità delle cassette postali per un utente di Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Set di funzionalità delle cassette postali per un utente di Outlook Voice Access
ms:assetid: a56bfd75-7bc5-49b9-b098-06855a720dcd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124030(v=EXCHG.150)
ms:contentKeyID: 50555650
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Set di funzionalità delle cassette postali per un utente di Outlook Voice Access

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

Le impostazioni dell'interfaccia telefonica di un utente (TUI, Telephone User Interface) vengono utilizzate quando l'utente accede al sistema di messaggistica unificata utilizzando Outlook Voice Access. Quando si modificano le impostazioni della configurazione dell'interfaccia telefonica di un utente abilitato alla messaggistica unificata, si modificano le proprietà e i relativi valori nella cassetta postale dell'utente abilitato alla messaggistica unificata.

È possibile modificare le seguenti impostazioni dell'interfaccia telefonica per un utente abilitato alla messaggistica unificata:

  - Consentire l'accesso al sottoscrittore

  - Consentire l'accesso al Calendario dall'interfaccia telefonica

  - Consentire l'accesso dell'interfaccia telefonica alla posta elettronica

  - Consentire il riconoscimento vocale automatico

Per le attività di gestione aggiuntive relative agli utenti di messaggistica unificata, vedere [Set di funzionalità delle cassette postali per un utente di Outlook Voice Access](set-mailbox-features-for-an-outlook-voice-access-user-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che il destinatario di Exchange esistente sia abilitato alla messaggistica unificata e al sistema di caselle vocali. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Modifica delle impostazioni dell'interfaccia telefonica di un singolo utente abilitato alla messaggistica unificata tramite Shell

Con questo esempio viene abilitato l'accesso al Calendario e alla posta elettronica tramite interfaccia telefonica per un utente abilitato alla messaggistica unificata denominato Tony Smith.

    Set-UMMailbox -Identity tony@contoso.com TUIAccessToCal True -TUIAccessToEmail True -OperatorNumber 111111 -DisableMissedCallNotification False -AnonCallBlock True


> [!NOTE]
> Le impostazioni dell'interfaccia telefonica sono disponibili anche nei criteri cassetta postale di messaggistica unificata. La modifica delle impostazioni dell'interfaccia telefonica su un criterio cassetta postale di messaggistica unificata incide su tutti gli utenti associati al criterio cassetta postale di messaggistica unificata. Per ulteriori informazioni su come modificare le impostazioni dell'interfaccia telefonica su un criterio cassetta postale di messaggistica unificata, vedere<A href="set-mailbox-features-for-outlook-voice-access-users-exchange-2013-help.md">Impostare funzionalità delle cassette postali per gli utenti di Outlook Voice Access</A>.



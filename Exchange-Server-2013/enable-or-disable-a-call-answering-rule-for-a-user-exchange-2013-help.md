---
title: 'Abilitare o disabilitare una regola di ricezione chiamata di un utente: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare una regola di ricezione chiamata di un utente
ms:assetid: f9e40ac3-117f-44f6-9ab1-dc9f4c72e8ac
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn140252(v=EXCHG.150)
ms:contentKeyID: 54652857
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare una regola di ricezione chiamata di un utente

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-04-08_

È possibile utilizzare Shell per abilitare o disabilitare una o più regole di ricezione chiamata per un utente. È possibile, inoltre, utilizzare i cmdlet **Enable-UMCallAnsweringRule** o **Disable-UMCallAnsweringRule** in uno script di Exchange Management Shell per abilitare o disabilitare una o più regole di ricezione chiamata per più utenti.

Le regole di ricezione chiamata vengono applicate alle chiamate in ingresso in modo simile a quello in cui le regole di Posta in arrivo vengono applicate ai messaggi di posta in arrivo. Per impostazione predefinita, quando un utente viene abilitato all'utilizzo della messaggistica unificata non viene configurata alcuna regola di ricezione chiamata. Ciononostante, il sistema di posta risponde alle chiamate e ai chiamanti viene chiesto di lasciare un messaggio vocale.

Per ulteriori attività di gestione relative alle regole di ricezione chiamata, vedere [Inoltro di chiamate di procedure](forwarding-calls-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Regole di ricezione chiamata di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che la cassetta postale dell'utente sia stata abilitata alla messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura. Per sapere come aprire Exchange Management Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)). Per informazioni su come usare Windows PowerShell per connettersi a Exchange Online, vedere [Connessione a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Abilitazione di una regola di ricezione chiamata tramite Shell

Quando viene creata, una regola ricezione chiamata è abilitata. È possibile utilizzare Shell per abilitare una regola di ricezione chiamata che era stata disabilitata. L'abilitazione di una regola di ricezione chiamata consente al cmdlet **Enable-UMCallAnsweringRule** di recuperare la regola di ricezione chiamata, incluse le condizioni e le azioni per una regola di ricezione chiamata specificata.

Con questo esempio viene creata la regola di ricezione chiamata `MyUMCallAnsweringRule` nella cassetta postale di Tony Smith.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

Con questo esempio viene utilizzata l'opzione *WhatIf* per verificare se la regola di ricezione chiamata `MyUMCallAnsweringRule` nella cassetta postale di Tony Smith è pronta per essere abilitata e se sono presenti errori nel comando.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

Con questo esempio viene abilitata la regola di ricezione chiamata `MyUMCallAnsweringRule` nella cassetta postale di Tony Smith e viene richiesto all'utente connesso di confermare che la regola di ricezione chiamata deve essere abilitata.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

## Disabilitazione di una regola di ricezione chiamata tramite Shell

La disabilitazione di una regola di ricezione chiamata consente di impedirne il recupero e l'elaborazione quando viene ricevuta una chiamata in ingresso. Quando si crea una regola di ricezione chiamata, per configurare condizioni e azioni è necessario disabilitarla. In questo modo è possibile impedire l'elaborazione della regola di ricezione chiamata alla ricezione di una chiamata in ingresso fin quando la regola non è stata configurata correttamente.

Con questo esempio viene disabilitata la regola di ricezione chiamata `MyUMCallAnsweringRule` nella cassetta postale di Tony Smith.

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

In questo esempio viene utilizzata l'opzione *WhatIf* per stabilire se la regola di ricezione chiamata `MyUMCallAnsweringRule` nella cassetta postale di Tony Smith è pronta per essere disabilitata e se vi sono errori all'interno del comando.

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

In questo esempio viene disabilitata la regola di ricezione chiamata `MyUMCallAnsweringRule` nella cassetta postale di Tony Smith e viene richiesto all'utente connesso di confermare la disabilitazione della regola di ricezione chiamata.

    Disable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm


---
title: 'Abilitare o disabilitare il riconoscimento vocale automatico per un utente di Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare il riconoscimento vocale automatico per un utente di Outlook Voice Access
ms:assetid: 58f41016-e725-432b-953e-415d61e0664c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232062(v=EXCHG.150)
ms:contentKeyID: 50555594
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare il riconoscimento vocale automatico per un utente di Outlook Voice Access

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-22_

È possibile configurare il riconoscimento vocale automatico per un utente abilitato alla messaggistica unificata e alla posta vocale. Quando il riconoscimento vocale automatico è abilitato sulla cassetta postale di un utente di Outlook Voice Access, l'utente può spostarsi all'interno dei menu della cassetta postale utilizzando i comandi vocali. Il riconoscimento vocale automatico è abilitato per impostazione predefinita. Se il riconoscimento vocale automatico è disabilitato, l'utente deve utilizzare gli input del segnale multifrequenza DTMF (Dual Tone Multi-Frequency), noti anche come input a toni, per spostarsi all'interno dei menu.


> [!NOTE]
> Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per configurare questa funzionalità. Per abilitare o disabilitare il riconoscimento vocale automatico per un utente di posta vocale è necessario utilizzare Shell.



Per altre attività di gestione relative agli utenti di posta vocale o di messaggistica unificata, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che la cassetta postale dell'utente sia stata abilitata alla messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Abilitazione o disabilitazione del riconoscimento vocale automatico per un utente abilitato alla messaggistica unificata tramite Shell

In questo esempio, l'utente `tonysmith` abilitato alla messaggistica unificata viene abilitato al riconoscimento vocale automatico.

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $true

In questo esempio, l'utente `tonysmith` abilitato alla messaggistica unificata viene disabilitato al riconoscimento vocale automatico.

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $false


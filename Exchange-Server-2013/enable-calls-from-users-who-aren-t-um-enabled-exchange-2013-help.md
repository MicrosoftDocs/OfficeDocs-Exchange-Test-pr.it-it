---
title: 'Abilitare le chiamate provenienti da utenti che non sono abilitati alla messaggistica unificata: Exchange 2013 Help'
TOCTitle: Abilitare le chiamate provenienti da utenti che non sono abilitati alla messaggistica unificata
ms:assetid: 3c39c6df-6d7a-469f-b92b-85b3f14bad31
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb267006(v=EXCHG.150)
ms:contentKeyID: 50480390
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare le chiamate provenienti da utenti che non sono abilitati alla messaggistica unificata

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-05_

È possibile abilitare o disabilitare le chiamate effettuate da utenti non abilitati alla messaggistica unificata. Per impostazione predefinita, tramite operatore automatico, la messaggistica unificata consente il trasferimento delle chiamate effettuate da chiamanti non autenticati a utenti abilitati alla messaggistica unificata. Se è stata abilitata questa opzione, gli utenti esterni all'organizzazione potranno trasferire chiamate a utenti abilitati alla messaggistica unificata.

Se questa impostazione viene disabilitata per un utente abilitato alla messaggistica unificata, la sua cassetta postale potrà comunque essere individuata tramite una ricerca nella directory. Tuttavia, se un chiamante esterno tenta di trasferire una chiamata a questo utente, il sistema notificherà l'impossibilità di farlo e la chiamata verrà quindi trasferita all'operatore configurato sull'operatore automatico. Se tale operatore non è stato configurato, la chiamata verrà trasferita all'operatore eventualmente configurato nel dial plan. Se non è stato configurato alcun interno sull'operatore automatico abilitato alla sintesi vocale, sull'operatore automatico del fallback del segnale multifrequenza o sul dial plan, il sistema notificherà che né l'operatore né il servizio a toni sono disponibili.

Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che la cassetta postale dell'utente sia stata abilitata alla messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo di Shell per l'abilitazione delle chiamate effettuate da utenti non abilitati per la messaggistica unificata

In questo esempio a Tony Smith viene concesso di ricevere chiamate vocali da utenti non abilitati per la messaggistica unificata.

    Set UMMailbox -Identity tony@contoso.com -AllowUMCallsFromNonUsers SearchEnabled


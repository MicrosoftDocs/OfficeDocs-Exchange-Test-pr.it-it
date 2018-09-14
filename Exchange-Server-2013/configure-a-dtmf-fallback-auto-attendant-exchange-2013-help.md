---
title: 'Configurare un operatore automatico di fallback DTMF: Exchange 2013 Help'
TOCTitle: Configurare un operatore automatico di fallback DTMF
ms:assetid: a82d85f7-de30-40db-8ee6-b091ac14da9d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232158(v=EXCHG.150)
ms:contentKeyID: 50481389
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare un operatore automatico di fallback DTMF

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-30_

È possibile configurare un operatore automatico di messaggistica unificata abilitato al servizio di sintesi vocale che dispone di un operatore automatico per il fallback del segnale multifrequenza (DTMF). Un operatore automatico per il fallback del segnale multifrequenza (DTMF) viene utilizzato quando un operatore automatico abilitato al servizio di sintesi vocale di messaggistica unificata non è in grado di comprendere o riconoscere gli input vocali del chiamante. Se è stato configurato un operatore automatico per il fallback del segnale multifrequenza, il chiamante deve utilizzare gli input DTMF, denominati anche input a toni, per spostarsi all'interno del sistema di menu dell'operatore automatico, pronunciare un nome utente sillaba per sillaba o utilizzare un'istruzione vocale personalizzata del menu. Se non è stato configurato alcun operatore automatico per il fallback del segnale multifrequenza ed è stato superato il numero massimo di input vocali perché le parole del chiamante non sono state comprese, verrà ricevuta un'istruzione che indica la necessità di riprovare in un momento successivo.

Per impostazione predefinita, un operatore automatico non è abilitato al servizio di sintesi vocale in fase di creazione. Dopo aver abilitato l'operatore automatico al servizio di sintesi vocale, i chiamanti possono utilizzare solo i comandi vocali per spostarsi all'interno del sistema di menu dell'operatore automatico e non è possibile utilizzare gli input a toni. Sebbene non sia obbligatorio, si consiglia di configurare un operatore automatico per il fallback del segnale multifrequenza per ciascun operatore automatico abilitato al servizio di sintesi vocale, in modo che i chiamanti possano utilizzare gli input a toni se l'operatore automatico abilitato al servizio di sintesi vocale non riconosce o comprende le parole pronunciate. Inoltre, si consiglia di non abilitare al servizio di sintesi vocale un operatore automatico per il fallback del segnale multifrequenza.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/create-a-um-auto-attendant).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Configurazione di un operatore automatico abilitato al servizio di sintesi vocale con un operatore automatico per il fallback del segnale multifrequenza tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata da modificare e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata per cui si desidera creare un operatore automatico di fallback DTMF. Sulla barra degli strumenti, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") nella barra degli strumenti.

3.  Nella pagina **Operatore automatico di messaggistica unificata** \> **Generali**, selezionare la casella di controllo **Utilizza questo operatore automatico se i comandi vocali non funzionano correttamente** e fare clic su **Sfoglia**.

4.  Nella pagina **Seleziona un operatore automatico di messaggistica unificata**, selezionare l'operatore automatico da utilizzare come operatore automatico per il fallback del segnale multifrequenza, quindi fare clic su **Salva**.


> [!IMPORTANT]
> È necessario per prima cosa abilitare l'operatore automatico alla sintesi vocale prima di cercare un operatore automatico per il fallback del segnale multifrequenza configurato.



## Configurazione di un operatore automatico abilitato al servizio di sintesi vocale con un operatore automatico per il fallback del segnale multifrequenza tramite Shell

Con questo esempio, un operatore automatico di messaggistica unificata denominato `MySpeechEnabledAA` viene configurato per utilizzare un operatore automatico per il fallback del segnale multifrequenza denominato `MyDTMFAA`.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA


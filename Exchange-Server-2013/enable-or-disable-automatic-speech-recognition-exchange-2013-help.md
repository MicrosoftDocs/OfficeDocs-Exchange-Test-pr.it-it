---
title: 'Abilitare o disabilitare il riconoscimento vocale automatico: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare il riconoscimento vocale automatico
ms:assetid: 92b3b679-b503-4068-8e88-25ec0f4537ab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232128(v=EXCHG.150)
ms:contentKeyID: 52057292
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare il riconoscimento vocale automatico

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-12-12_

È possibile abilitare l'operatore automatico di messaggistica unificata (UM) per il riconoscimento vocale automatico (ASR). Dopo che vocale abilitare un operatore automatico di messaggistica unificata, i chiamanti possono verbalmente risponde alle richieste di operatore automatico e spostarsi all'interno del sistema di menu dell'operatore automatico. Per impostazione predefinita, un operatore automatico non è abilitato quando si crea. Dopo che vocale abilitare l'operatore automatico, i chiamanti possono utilizzare solo i comandi vocali per passare il sistema di menu dell'operatore automatico e non è possibile utilizzare gli input di composizione a toni.

Anche se non è obbligatorio, è consigliabile configurare un operatore automatico di fallback multifrequenza (DTMF) bicolore per ogni operatore automatico abilitato in modo che i chiamanti possono utilizzare gli input di composizione a toni se l'operatore automatico abilitato non riconosce o acquisire familiarità con le parole che vengono di seguito. Se è configurato un operatore automatico di fallback DTMF, i chiamanti possono utilizzare gli input DTMF, noto anche come input di composizione a toni per passare il sistema di menu dell'operatore automatico, digitare il nome di un nome utente o utilizzare un prompt dei comandi di menu personalizzate. Non è consigliabile che si vocale abilitare un operatore automatico di fallback DTMF.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Utilizzo di EAC per abilitare alla sintesi vocale un operatore automatico di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata che si desidera abilitare al servizio di sintesi vocale, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina di **Operatore automatico** \> **Generale**, selezionare la casella di controllo accanto a **impostare l'operatore automatico di rispondere ai comandi vocali** per consentire il riconoscimento vocale. Per disabilitare il riconoscimento vocale automatico, deselezionare questa casella di controllo.

4.  Fare clic su **Salva**.

## Utilizzo di Shell per abilitare alla sintesi vocale un operatore automatico di messaggistica unificata

In questo esempio l'operatore automatico di messaggistica unificata `MySpeechEnabled AA` viene abilitato al riconoscimento vocale automatico.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -SpeechEnabled $true


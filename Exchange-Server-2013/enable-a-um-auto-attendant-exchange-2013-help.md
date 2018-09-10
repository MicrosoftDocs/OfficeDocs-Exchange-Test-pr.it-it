---
title: 'Abilita operatore automatico di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Abilitare un operatore automatico di messaggistica unificata
ms:assetid: 16667a8f-50ab-4bb8-9a05-0389511974b1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996379(v=EXCHG.150)
ms:contentKeyID: 50480107
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare un operatore automatico di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-05_

Per impostazione predefinita, al momento della creazione, lo stato di un operatore automatico di messaggistica unificata è disabilitato. Dopo aver creato l'operatore automatico di messaggistica unificata, è possibile modificarne lo stato affinché possa rispondere alle chiamate in ingresso.

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

## Utilizzo dell'interfaccia di amministrazione di Exchange per l'abilitazione di un operatore automatico di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata da modificare e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata in **Operatori automatici di messaggistica unificata**. Sulla barra degli strumenti, fare clic sulla **freccia su**![Icona Freccia in su](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "Icona Freccia in su").

3.  Nella pagina **Avviso** fare clic su **Sì**.

## Abilitazione di un operatore automatico di messaggistica unificata tramite Shell

In questo esempio viene abilitato l'operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant` per rispondere alle chiamate in arrivo.

    Enable-UMAutoAttendant -Identity MyUMAutoAttendant


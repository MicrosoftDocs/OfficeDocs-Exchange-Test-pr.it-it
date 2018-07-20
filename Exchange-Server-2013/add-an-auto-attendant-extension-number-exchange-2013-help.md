---
title: 'Aggiungere un numero di interno operatore automatico: Exchange 2013 Help'
TOCTitle: Aggiungere un numero di interno operatore automatico
ms:assetid: f2bd62ba-1e01-4cb7-862c-c750752e20e0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232200(v=EXCHG.150)
ms:contentKeyID: 50482003
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiungere un numero di interno operatore automatico

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-05_

È possibile configurare uno o più numeri di interno a un operatore automatico di messaggistica unificata (UM). Quando un numero di interno viene aggiunto a un operatore automatico di messaggistica unificata, il numero può essere utilizzato dai chiamanti per accedere all'operatore automatico. È anche possibile aggiungere numeri di interno nel caso in cui si desidera che più numeri di interno siano utilizzati dai chiamanti per accedere all'operatore automatico. Per impostazione predefinita, nessun numero di interno viene configurato quando si crea un operatore automatico.

È possibile creare un nuovo operatore automatico senza tuttavia impostare alcun numero di interno. È inoltre possibile associare più numeri telefonici o di interni a un unico operatore automatico. I numeri di interni possono essere aggiunti quando si crea un operatore automatico di messaggistica unificata o dopo aver configurato l'operatore automatico. Il numero di cifre del numero di interno configurato sull'operatore automatico di messaggistica unificata deve corrispondere al numero di cifre del numero di interno configurato nel dial plan di messaggistica unificata associato all'operatore automatico di messaggistica unificata.


> [!NOTE]
> Inoltre, in alternativa al numero di interno, è possibile aggiungere un indirizzo SIP. L'indirizzo SIP viene utilizzato da alcuni sistemi IP Private Branch eXchanges (PBXs) e Office Communications Server 2007 R2 o Microsoft Lync Server.



Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Aggiunta di un numero di telefono o di interno a un operatore automatico di messaggistica unificata tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata da modificare e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata** selezionare l'operatore automatico di messaggistica unificata a cui aggiungere i numeri di telefono o di interno.

3.  Sulla barra degli strumenti, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") nella barra degli strumenti.

4.  Nella pagina **Operatori automatici di messaggistica unificata** \> **Generale**, nella casella di testo di **Numeri di accesso** immettere il numero di telefono o di interno da utilizzare e fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

5.  Fare clic **Salva** per aggiungere il numero.

## Configurazione di un numero di interno su un operatore automatico di messaggistica unificata tramite Shell

In questo esempio viene configurato un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant` con più numeri di interni.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -PilotIdentifierList "12345, 72000, 75000"


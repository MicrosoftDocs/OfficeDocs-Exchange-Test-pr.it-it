---
title: 'Il servizio pubblicazione sul Web viene disattivato o missing_W3SVCDisabledOrNotInstalled: Exchange 2013 Help'
TOCTitle: Il servizio pubblicazione sul Web viene disattivato o missing_W3SVCDisabledOrNotInstalled
ms:assetid: 2d26d778-ddf1-4225-b5e2-f6b49d819c94
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.w3svcdisabledornotinstalled(v=EXCHG.150)
ms:contentKeyID: 50480315
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Il servizio pubblicazione sul Web viene disattivato o missing\_W3SVCDisabledOrNotInstalled

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Perché è stato trovato il tentativo di installare il ruolo del Server cassette postali o accesso Client che il servizio pubblicazione sul Web è disabilitato o non è installato nel computer, non continuare l'installazione di Microsoft® Exchange Server 2007.

Il computer in cui si installa Microsoft Exchange per il servizio pubblicazione sul Web installati e impostata su un valore diverso da disattivato richiede l'installazione di Exchange 2007.

Per risolvere questo problema, verificare che il servizio pubblicazione sul Web sia installato e non è stato disabilitato nel computer locale e quindi rieseguire il programma di installazione di Microsoft Exchange.

Per verificare che il servizio pubblicazione sul Web sia installato e non è disattivato

1.  Destro del mouse sul **Computer locale** sul desktop e quindi fare clic su **Gestisci**.

2.  Espandere il nodo **servizi e applicazioni** e quindi fare clic sul nodo **servizi**.

3.  Nel riquadro destro, individuare il **Servizio pubblicazione sul Web**.
    
    Se il **Servizio pubblicazione sul Web** non è visualizzato nell'elenco dei servizi installati, seguire i passaggi nella procedura seguente per installarlo.

4.  Se il **Servizio pubblicazione sul Web** viene visualizzata ma con uno stato diverso da **avviato**, continuare con la procedura seguente per avviarlo.

5.  Destro del mouse sul **Servizio pubblicazione sul Web** e quindi scegliere **proprietà**.

6.  Verificare il **Tipo di avvioautomatico** e lo **stato del servizio** è impostato su **avviato**.

7.  Fare clic su **Applica** e quindi su **OK**.

Per installare il servizio pubblicazione sul Web

1.  Nel menu **Start**, selezionare **Impostazioni**, **Pannello di controllo** e quindi fare clic su **Installazione applicazioni**

2.  Fare clic su **Installazione componenti di Windows**.

3.  Nella casella **componenti**, selezionare la casella di controllo **Server applicazioni** e quindi fare clic su **Dettagli**.

4.  Selezionare **Gestione Internet Information Services** e quindi fare clic su **Dettagli**.

5.  Selezionare **Servizio World Wide Web** e quindi selezionare la casella di controllo.

6.  Fare clic su **OK** due volte per tornare all'elenco dei **componenti** e quindi fare clic su **Avanti**.

7.  Quando viene installato il servizio IIS, fare clic su **Fine**.


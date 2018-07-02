---
title: 'Simple Mail Transport Protocol è attualmente installed_SMTPSvcInstalled: Exchange 2013 Help'
TOCTitle: Simple Mail Transport Protocol è attualmente installed_SMTPSvcInstalled
ms:assetid: f786a93c-876d-4f4e-adb6-4dfea3d820d1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.smtpsvcinstalled(v=EXCHG.150)
ms:contentKeyID: 50482053
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Simple Mail Transport Protocol è attualmente installed\_SMTPSvcInstalled

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Dal momento che il servizio Microsoft Windows Server™ 2003 SMTP Simple Mail Transfer Protocol () viene installato nel computer, non può continuare l'installazione di Microsoft® Exchange Server 2007.

Richiede l'installazione di Microsoft Exchange non installato il servizio SMTP nel server in cui vengono utilizzati per Exchange 2007.

Per risolvere questo problema, disinstallare il servizio SMTP e rieseguire il programma di installazione di Microsoft Exchange.

Per disinstallare il servizio SMTP mediante Aggiungi o Rimuovi un componente di Windows nel Pannello di controllo

1.  Nel menu **Start**, scegliere **Pannello di controllo**.

2.  Fare doppio clic su **Installazione applicazioni**.

3.  Fare clic su **Installazione componenti di Windows**.

4.  Nella casella **componenti**, selezionare la casella di controllo **Server applicazioni** e quindi fare clic su **Dettagli**.

5.  Selezionare **Gestione Internet Information Services** e quindi fare clic su **Dettagli**.

6.  Selezionare **Il servizio SMTP** e fare clic per deselezionare la casella di controllo.

7.  Fare due volte clic su **OK** per tornare all'elenco dei **componenti** e quindi fare clic su **Avanti**.

8.  Quando viene disinstallato il servizio SMTP, fare clic su **Fine**.


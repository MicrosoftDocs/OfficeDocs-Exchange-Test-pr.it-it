---
title: 'Il servizio Attivazione processo Windows - modello del processo componente è required_LonghornWASProcessModelInstalled: Exchange 2013 Help'
TOCTitle: Il servizio Attivazione processo Windows - modello del processo componente è required_LonghornWASProcessModelInstalled
ms:assetid: 8cc13dbb-4921-4c07-8602-d26613d7730a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.longhornwasprocessmodelinstalled(v=EXCHG.150)
ms:contentKeyID: 50481146
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Il servizio Attivazione processo Windows - modello del processo componente è required\_LonghornWASProcessModelInstalled

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2015-04-07_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

il programma di installazione Exchange Server 2010 non può continuare l'installazione su Windows Server 2008-computer basato su R2 Windows Server 2008 o perché il servizio Attivazione processo Windows - funzionalità di modello di processo non è installato nel server.

Il servizio Attivazione processo Windows generalizza il modello di processo di Internet Information Services (IIS), eliminando la dipendenza da HTTP. Tutte le caratteristiche di IIS in precedenza disponibili solo per le applicazioni HTTP sono ora disponibili per le applicazioni che ospitano servizi Windows Communication Foundation (WCF), tramite i protocolli HTTP non. IIS 7.0 utilizza anche servizio Attivazione processo Windows per l'attivazione basata su messaggi su HTTP.

Il modello di processo ospita i servizi WCF e Web. Introdotta in IIS 6.0, il modello di processo è una nuova architettura di tale funzionalità rapida protezione dagli errori e il riciclo del monitoraggio dello stato.

Per risolvere questo problema, installare il servizio Attivazione processo Windows - funzionalità di modello di processo nel server e quindi rieseguire il programma di installazione Exchange 2010.

Installare il servizio Attivazione processo Windows - modello di processo feature mediante lo strumento Server Manager

1.  Fare clic su **Start**, scegliere **Strumenti di amministrazione** e quindi **Server Manager**.

2.  Nel riquadro di spostamento sinistro, destro **caratteristiche** e quindi fare clic su **Aggiungi funzionalità**.

3.  Nel riquadro **Selezione funzionalità** scorrere verso il basso per **Il servizio Attivazione processo Windows**.

4.  Selezionare le caselle di controllo per il **Modello di processo**.

5.  Fare clic su **Avanti** nel riquadro **Selezione funzionalità** e quindi fare clic su **Installa** il riquadro **Conferma selezioni**.

6.  Fare clic su **Chiudi** per uscire dalla procedura guidata Aggiunta servizi ruolo.


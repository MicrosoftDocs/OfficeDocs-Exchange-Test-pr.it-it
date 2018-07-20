---
title: 'I messaggi attualmente esistono in uno o più queues_MessagesInQueue: Exchange 2013 Help'
TOCTitle: I messaggi attualmente esistono in uno o più queues_MessagesInQueue
ms:assetid: 3ffcdc7e-c1b7-49a7-8e5f-b30c0397908d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.messagesinqueue(v=EXCHG.150)
ms:contentKeyID: 50480453
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# I messaggi attualmente esistono in uno o più queues\_MessagesInQueue

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Il programma di installazione di Microsoft® Exchange Server 2007 viene visualizzato questo messaggio di avviso in quanto il tentativo di disinstallare un ruolo di trasporto può causare perdite di dati da una coda di trasporto.

Controlli per l'installazione di Exchange 2007 per assicurarsi che le code di trasporto sono vuote prima che consente di rimuovere i ruoli associati alla gestione delle code.

Se si rimuove i ruoli di trasporto prima del recapito dei messaggi ancora di code di trasposto, questi messaggi possono trovarsi per un tempo indefinito.

Per risolvere questo problema, esaminare le code di cui viene fatto riferimento per assicurarsi che siano vuote dei messaggi prima di continuare con l'installazione.

Per visualizzare il contenuto di una coda

1.  Aprire Exchange Management Console.

2.  Nell'albero della console, fare clic su **Casella degli strumenti**.

3.  Nel riquadro dei risultati fare clic su **Visualizzatore code di Exchange**.

4.  Nel riquadro azioni, fare clic su **Apri strumento**.

5.  Nel Visualizzatore code fare clic sulla scheda **code**. Viene visualizzato un elenco di tutte le code sul server in cui si è connessi.

6.  Fare clic sulla coda desiderata e scegliere **proprietà** per visualizzare le proprietà della coda.

Per visualizzare i messaggi in una coda

1.  Seguire i passaggi da 1 a 4.

2.  Nel Visualizzatore code fare clic sulla scheda **messaggi**. Viene visualizzato un elenco di tutti i messaggi nel server in cui si è connessi. Per regolare la visualizzazione di una singola coda, fare clic sulla scheda **code**, fare doppio clic sul nome della coda e quindi fare clic sulla scheda Server\\Queue visualizzata.

3.  Per visualizzare informazioni dettagliate su un messaggio, selezionare un messaggio e quindi fare clic su **proprietà** nel riquadro azioni.


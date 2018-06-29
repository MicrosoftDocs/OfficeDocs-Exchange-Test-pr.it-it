---
title: "Il servizio coordinatore di transazione distribuita deve essere avviato prima dell'installazione possono continue_MSDTCStopped: Exchange 2013 Help"
TOCTitle: Il servizio coordinatore di transazione distribuita deve essere avviato prima dell'installazione possono continue_MSDTCStopped
ms:assetid: 96e33c94-348e-4a0b-9585-9bee81be4355
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.msdtcstopped(v=EXCHG.150)
ms:contentKeyID: 50481226
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Il servizio coordinatore di transazione distribuita deve essere avviato prima dell'installazione possono continue\_MSDTCStopped

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Non può continuare l'installazione di Microsoft Exchange Server 2007 perché il tentativo di installare i ruoli del server Server accesso Client o la messaggistica unificata non riuscita perché il servizio DTC non è stato avviato nel computer di destinazione.

Installazione di Exchange 2007 richiede il computer che si sta installando Exchange Microsoft per avere lo stato del servizio DTC impostato su **avviato**.

Il servizio DTC fornisce servizi progettati per garantire il corretta completamento delle transazioni, anche con errori di sistema, processo e gli errori di comunicazione.

Ogni computer incluso in una transazione distribuita gestisce il proprio risorse e i dati e inoltre funziona in combinazione con altri computer della transazione. Per prima cosa, una transazione distribuita deve eseguire il commit o interrompere il proprio lavoro interamente in tutti i computer partecipanti. Il DTC riveste il ruolo di coordinamento delle transazioni per i componenti coinvolti e funge da un gestore delle transazioni per ogni computer che gestisce le transazioni.

Ruoli del Server accesso Client e messaggistica unificata con dipendenze nel servizio DTC.

Per risolvere questo problema, verificare che lo stato del servizio DTC sia impostato su **avviato** nel computer locale e quindi rieseguire il programma di installazione di Microsoft Exchange.

Per impostare lo stato del servizio DTC da 'Iniziato'

1.  **Risorse del** computer e quindi fare clic su **Gestisci**.

2.  Espandere il nodo **servizi e applicazioni** e quindi fare clic sul nodo **servizi**.

3.  Nel riquadro destro, individuare il **DTC**.

4.  Pulsante destro del mouse **DTC** e quindi scegliere **proprietà**.

5.  Impostare il **Tipo di avvio** su **automatico** e lo **stato del servizio** in **avviato**.

6.  Fare clic su **Applica** e quindi su **OK**.


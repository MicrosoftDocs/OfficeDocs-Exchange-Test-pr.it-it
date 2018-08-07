---
title: 'Avv. ev. sist. COM + pre-inst. continue_EventSystemStopped: Exchange 2013 Help'
TOCTitle: Deve essere avviato il servizio eventi di sistema COM + prima dell'installazione possono continue_EventSystemStopped
ms:assetid: 3b8d2ba3-87fb-4749-b4d1-5dfec97e1ca4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.eventsystemstopped(v=EXCHG.150)
ms:contentKeyID: 50480389
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deve essere avviato il servizio eventi di sistema COM + prima dell'installazione possono continue\_EventSystemStopped

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Dal momento che il tentativo di installare i ruoli del Server accesso Client o Trasporto Edge server non è riuscita perché il servizio di sistema non è stato avviato nel computer di destinazione, non può continuare l'installazione di Microsoft Exchange Server 2007.

Installazione di Exchange 2007 richiede il computer che si sta installando Exchange Microsoft per avere lo stato del servizio di sistema di eventi COM + impostato su **avviato**.

Il servizio di sistema di evento COM + supporta notifiche di eventi di sistema per tali componenti, che consentono la distribuzione automatica degli eventi ai componenti COM sottoscritti.

Ruoli del server il Server accesso Client e Trasporto Edge con dipendenze dalle COM + componenti di cui effettuare la sottoscrizione al servizio di sistema.

Per risolvere questo problema, verificare che lo stato del servizio di sistema è impostato su **avviato** nel computer locale e quindi rieseguire il programma di installazione di Microsoft Exchange.

Per impostare lo stato del servizio di sistema per 'Iniziato'

1.  **Risorse del** computer e quindi fare clic su **Gestisci**.

2.  Espandere il nodo **servizi e applicazioni** e quindi fare clic sul nodo **servizi**.

3.  Nel riquadro destro, individuare il **Sistema**.

4.  Destro del mouse sul **Sistema** e quindi scegliere **proprietà**.

5.  Impostare il **Tipo di avvio** su **automatico** e lo **stato del servizio** in **avviato**.

6.  Fare clic su **Applica** e quindi su **OK**.


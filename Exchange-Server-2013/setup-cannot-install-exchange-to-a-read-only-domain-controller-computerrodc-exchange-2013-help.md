---
title: 'Impossibile installare Exchange a un dominio di sola lettura controller_ComputerRODC: Exchange 2013 Help'
TOCTitle: Impossibile installare Exchange a un dominio di sola lettura controller_ComputerRODC
ms:assetid: 4934d755-65be-47e2-86b0-6ea1ab148a96
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.computerrodc(v=EXCHG.150)
ms:contentKeyID: 50480526
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impossibile installare Exchange a un dominio di sola lettura controller\_ComputerRODC

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Il programma di installazione di Microsoft Exchange Server 2007 non possono continuare l'installazione, dal momento che il computer di destinazione è un Controller di dominio di sola lettura (RODC).

I controller di dominio di sola lettura sono una funzionalità di Active Directory di Windows Server 2008. Quest'ultimo è un tipo di controller di dominio installare opzione che può essere installati nei siti remoti che possono avere livelli inferiori di protezione fisica.

Accesso in scrittura nel computer di destinazione installazione richiede l'installazione di Exchange.

Per risolvere questo problema, selezionare un computer install destinazione a cui non è progettato come un RODC e rieseguire il programma di installazione.


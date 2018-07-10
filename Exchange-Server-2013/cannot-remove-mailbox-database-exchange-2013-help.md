---
title: 'Impossibile rimuovere il database delle cassette postali: Exchange 2013 Help'
TOCTitle: Impossibile rimuovere il database delle cassette postali
ms:assetid: 5881e4c0-c2e2-48db-84b4-7f9ce3cf46a7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.unwillingtoremovemailboxdatabase(v=EXCHG.150)
ms:contentKeyID: 50480661
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impossibile rimuovere il database delle cassette postali

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2012-11-08_

L'installazione di Microsoft Exchange Server 2013 non può proseguire perché è impossibile rimuovere il database delle cassette postali di un utente dal server locale senza provocare una potenziale perdita di dati.

Il programma di installazione di Exchange 2013 verifica che tutti i database delle cassette postali siano stati rimossi dal server prima della rimozione del ruolo del server Cassette postali. Tuttavia, le cassette postali dell'utente potrebbero rimanere nel server.

Per risolvere il problema, spostare tutte le cassette postali sul server in un server Exchange diverso o, se le cassette postali con relativi dati non sono più necessari, disabilitare le cassette postali. Di seguito, eseguire nuovamente l'installazione di Exchange 2013.

  - Per ulteriori informazioni sull'identificazione di una cassetta postale nel database, vedere [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)).

  - Per ulteriori informazioni sullo spostamento di una cassetta postale, vedere [Spostamenti di cassette postali di Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

  - Per ulteriori informazioni sulla disabilitazione di una cassetta postale, vedere [Disable-Mailbox](https://technet.microsoft.com/it-it/library/aa997210\(v=exchg.150\)).

  - Per ulteriori informazioni sulla rimozione di un database delle cassette postali, vedere [Gestire il database delle cassette postali in Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.


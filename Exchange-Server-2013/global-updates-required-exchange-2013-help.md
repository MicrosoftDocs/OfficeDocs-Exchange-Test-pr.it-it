---
title: 'Aggiornamenti globali necessarie: Exchange 2013 Help'
TOCTitle: Aggiornamenti globali necessarie
ms:assetid: 0530f3c6-6fa6-456b-a33a-f3d2f7eaa2ef
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.globalupdaterequired(v=EXCHG.150)
ms:contentKeyID: 50479930
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiornamenti globali necessarie

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2014-12-02_

Microsoft Exchange Server 2013 non può proseguire con l'installazione perché l'utente connesso non dispone di autorizzazioni per gli account necessari per apportare aggiornamenti globali di Active Directory.

Il programma di installazione richiede che l'utente connesso quando viene installato Exchange 2013 disponga delle autorizzazioni per creare e modificare gli oggetti in Active Directory. Se si sta installando per la prima volta Exchange 2013 nell'organizzazione, l'account utilizzato deve essere membro dei gruppi Enterprise Admins e Schema Admins. Tali autorizzazioni sono necessarie perché Active Directory viene preparato per Exchange 2013 alla prima esecuzione del programma di installazione. Dopo aver preparato Active Directory, l'account utilizzato per installare i server Exchange 2013 aggiuntivi deve essere membro del gruppo di ruoli Gestione organizzazione.

Per risolvere questo problema, concedere all'utente connesso le autorizzazioni appropriate oppure accedere con un account che dispone di tali autorizzazioni, quindi eseguire nuovamente l'installazione di Exchange 2013.


> [!IMPORTANT]
> L'installazione tra foreste di Exchange 2013 non è supportata. Utilizzare l'account di un utente membro della foresta Active Directory in cui si installa Exchange 2013.



Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.


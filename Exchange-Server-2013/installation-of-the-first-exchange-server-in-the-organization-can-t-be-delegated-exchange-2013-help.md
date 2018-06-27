---
title: "Installazione di Exchange prima server nell'organizzazione non può essere delegata: Exchange 2013 Help"
TOCTitle: Installazione di Exchange prima server nell'organizzazione non può essere delegata
ms:assetid: bd1dbf09-5465-40fa-8668-ef99f753ba45
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.delegatedbridgeheadfirstinstall(v=EXCHG.150)
ms:contentKeyID: 50481578
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Installazione di Exchange prima server nell'organizzazione non può essere delegata

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2014-11-05_

Impossibile proseguire l'installazione di Microsoft Exchange Server 2013 perché l'utente collegato non dispone delle autorizzazioni account richieste per installare il primo server Exchange 2013 nell'organizzazione.

Anche se l'installazione di Exchange 2013 consente l'utilizzo delle delegazione per installare i ruoli server successivi, è necessario che l'utente collegato sia un membro del gruppo di protezione Enterprise Admins di Windows quando viene installato il primo server Exchange 2013 nell'organizzazione. Questo perché in fase di installazione di Exchange 2013 vengono creati e configurati oggetti nel contenitore Organizzazione Exchange in Active Directory.


> [!NOTE]
> Se non è stato preparato lo schema di Active Directory per Exchange 2013, l'utente collegato deve essere anche membro del gruppo di protezione Schema Admins di Windows. In alternativa, un altro utente membro del gruppo Schema Admins di Windows può preparare lo schema Active Directory prima dell'installazione di Exchange 2013.



Per risolvere questo problema, aggiungere l'utente collegato come membro del gruppo di protezione Enterprise Admins oppure accedere con un account membro del gruppo di protezione Enterprise Admins. Di seguito, eseguire nuovamente l'installazione di Exchange 2013.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.


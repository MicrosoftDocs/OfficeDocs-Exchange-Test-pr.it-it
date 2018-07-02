---
title: 'Deve essere updated_LocalDomainPrep il dominio locale: Exchange 2013 Help'
TOCTitle: Deve essere updated_LocalDomainPrep il dominio locale
ms:assetid: f33e6785-e85a-495e-a124-ebcb2b763e75
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.localdomainprep(v=EXCHG.150)
ms:contentKeyID: 50482010
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deve essere updated\_LocalDomainPrep il dominio locale

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Impossibile continuare l'installazione di Microsoft Exchange Server 2007 all'utente non dispone di account le autorizzazioni necessarie per la preparazione del dominio.

Installazione di Exchange è necessario che l'utente connesso durante l'esecuzione di **Setup /PrepareDomain** sia un membro dei gruppi Domain Admins ed Exchange Organization Administrators o del gruppo Enterprise Admins.

Per risolvere questo problema, concedere all'utente le autorizzazioni di amministratore dell'organizzazione di Exchange e Domain Admins, li effettuare la registrazione del gruppo Enterprise Admins o eseguire l'accesso con un account che disponga di tali autorizzazioni e rieseguire l'installazione di Exchange 2007.

Per ulteriori informazioni sulle autorizzazioni di Active Directory necessari a Microsoft Exchange, vedere "Utilizzo con Active Directory le autorizzazioni in Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).


---
title: 'Autorizzazioni sufficienti per eseguire /PrepareDomain_PrepareDomainNotAdmin: Exchange 2013 Help'
TOCTitle: Autorizzazioni sufficienti per eseguire /PrepareDomain_PrepareDomainNotAdmin
ms:assetid: c33a2bc0-5b07-49b8-a1c1-53baa4933d44
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.preparedomainnotadmin(v=EXCHG.150)
ms:contentKeyID: 50481604
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzazioni sufficienti per eseguire /PrepareDomain\_PrepareDomainNotAdmin

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Installazione di Microsoft Exchange Server 2007 non può continuare il tentativo di eseguire il processo di **/PrepareDomain**. L'utente dispone di autorizzazioni sufficienti per eseguire il processo di **/PrepareDomain**.

Installazione di Exchange 2007 è necessario che l'utente connesso durante l'esecuzione del processo di **/PrepareDomain** sia un membro del gruppo Domain Admins per il dominio da preparare e un membro del gruppo Enterprise Admins.

Per risolvere questo problema, concedere all'utente connesso Domain Admins gruppo le autorizzazioni per il dominio da preparare e registrare tali gruppi Enterprise Admins o eseguire l'accesso con un account che disponga di tali autorizzazioni e rieseguire l'installazione di Exchange 2007.

Per ulteriori informazioni sulle autorizzazioni di Active Directory necessari a Microsoft Exchange, vedere "Utilizzo con Active Directory le autorizzazioni in Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).


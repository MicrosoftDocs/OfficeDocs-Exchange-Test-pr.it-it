---
title: 'Autorizzazioni insufficienti per rimuovere tutti i server roles_CannotUninstallDelegatedServer: Exchange 2013 Help'
TOCTitle: Autorizzazioni insufficienti per rimuovere tutti i server roles_CannotUninstallDelegatedServer
ms:assetid: 214ae6f3-15e7-4337-99e8-40f9547c8e0c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.cannotuninstalldelegatedserver(v=EXCHG.150)
ms:contentKeyID: 50480151
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzazioni insufficienti per rimuovere tutti i server roles\_CannotUninstallDelegatedServer

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Installazione di Microsoft Exchange Server 2007 non può continuare il tentativo di disinstallare tutti i ruoli del server.

Installazione di Exchange 2007 è necessario che l'utente connesso durante la disinstallazione di tutti i ruoli del server sia un membro dei gruppi Exchange Organization Administrators o del gruppo Enterprise Admins.

Per risolvere questo problema, concedere all'utente connesso autorizzazioni di amministratore dell'organizzazione di Exchange o li effettuare la registrazione del gruppo Enterprise Admins o accedere con un account con le autorizzazioni e rieseguire il programma di installazione di Exchange 2007.

Per ulteriori informazioni sulle autorizzazioni di Active Directory necessari a Microsoft Exchange, vedere "Utilizzo con Active Directory le autorizzazioni di Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).


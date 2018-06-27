---
title: 'Autorizzazioni insufficienti per preparare Active Directory_ADUpdateRequired: Exchange 2013 Help'
TOCTitle: Autorizzazioni insufficienti per preparare Active Directory_ADUpdateRequired
ms:assetid: 1412d8a1-605a-4b1e-bee3-0c97f2cc9e65
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.adupdaterequired(v=EXCHG.150)
ms:contentKeyID: 50480031
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzazioni insufficienti per preparare Active Directory\_ADUpdateRequired

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Installazione di Microsoft Exchange Server 2007 non può continuare la preparazione del dominio tentativo.

Installazione di Exchange richiede che il servizio directory Active Directory da modificare per Exchange Server 2007 prima di preparare i domini in Active Directory.

L'account utilizzato per eseguire il comando **setup /PrepareAD** dispone di autorizzazioni sufficienti per eseguire questo comando, anche se è visualizzata appartenente al gruppo Enterprise Admins. L'account potrebbe essere scaduta.

Per risolvere questo problema, verificare che l'account utente connesso è valida e appartiene al gruppo Enterprise Admins o registro su con un account che disponga di tali autorizzazioni ed eseguire di nuovo **setup /PrepareAD**.

Per ulteriori informazioni su come eseguire il processo /PrepareAD, vedere "Come per preparare Active Directory e dei domini" ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453)).

Per ulteriori informazioni sulle autorizzazioni di Active Directory necessari a Microsoft Exchange, vedere "Utilizzo con Active Directory le autorizzazioni in Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).


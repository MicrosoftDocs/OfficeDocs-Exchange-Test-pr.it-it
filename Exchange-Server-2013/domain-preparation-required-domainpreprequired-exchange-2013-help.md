---
title: 'Dominio preparato required_DomainPrepRequired: Exchange 2013 Help'
TOCTitle: Dominio preparato required_DomainPrepRequired
ms:assetid: f6feae6f-7404-4b1f-887f-ed63c26a6bcd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.domainpreprequired(v=EXCHG.150)
ms:contentKeyID: 50482049
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Dominio preparato required\_DomainPrepRequired

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Installazione di Microsoft Exchange Server 2007 non può continuare il tentativo di installare il ruolo del server.

Preparare il dominio locale per Exchange Server 2007 prima di poter installare alcuni ruoli dei server richiede l'installazione di Microsoft Exchange.

Preparazione del dominio per Exchange Server 2007, è necessario eseguire le attività seguenti:

  - Impostazione delle autorizzazioni nel contenitore di dominio per il server di Exchange, Exchange Organization Administrators, gli utenti autenticati e gli amministratori delle cassette postali di Exchange.

  - La creazione del contenitore di oggetti di sistema di Microsoft Exchange se non esiste e impostazione delle autorizzazioni per il contenitore per il server di Exchange, Exchange Organization Administrators e gli utenti autenticati.

  - Creazione di un nuovo gruppo globale del dominio nel dominio corrente, viene chiamato Exchange Install Domain Servers.

  - Aggiunta al gruppo di Exchange Install Domain Servers per il gruppo di protezione Universale server di Exchange nel dominio radice.

Per risolvere questo problema, eseguire **setup /PrepareDomain** per preparare il dominio locale e riprovare server di installazione del ruolo.

Per ulteriori informazioni su come eseguire il processo PrepareDomain, vedere "Come per preparare Active Directory e dei domini" ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453)).


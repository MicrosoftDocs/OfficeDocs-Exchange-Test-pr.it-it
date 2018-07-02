---
title: "Tale Server sarà l'origine per un Connector_ServerIsSourceForSendConnector inviare: Exchange 2013 Help"
TOCTitle: Tale Server sarà l'origine per un Connector_ServerIsSourceForSendConnector inviare
ms:assetid: 151c0014-c90c-4c52-8e74-4b3f1bc7aaf1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.serverissourceforsendconnector(v=EXCHG.150)
ms:contentKeyID: 50480035
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Tale Server sarà l'origine per un Connector\_ServerIsSourceForSendConnector inviare

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Installazione di Microsoft Exchange Server 2007 non può continuare il tentativo di rimuovere il ruolo del server Trasporto Hub. Il computer locale è l'origine per uno o più connettori di invio nell'organizzazione di Exchange.

Un connettore di invio rappresenta un gateway logico attraverso il quale vengono inviati i messaggi in uscita.

Installazione di Exchange 2007 richiede che tutti i connettori di invio per un'organizzazione di Exchange deve essere spostati o eliminati dal computer server Trasporto Hub prima che il ruolo del server può essere eliminato.

Per risolvere questo problema, spostare o eliminare tutti i connettori di invio dal computer locale e quindi rieseguire il programma di installazione.

Per ulteriori informazioni sulla modifica o rimozione di connettori di invio, vedere gli argomenti seguenti nella documentazione del prodotto Exchange Server 2007:

  - "Come rimuovere un connettore di invio" ([https://go.microsoft.com/fwlink/?LinkId=86655](https://go.microsoft.com/fwlink/?linkid=86655)).

  - "Come modificare la configurazione di un connettore di invio" ([https://go.microsoft.com/fwlink/?LinkId=86656](https://go.microsoft.com/fwlink/?linkid=86656)).


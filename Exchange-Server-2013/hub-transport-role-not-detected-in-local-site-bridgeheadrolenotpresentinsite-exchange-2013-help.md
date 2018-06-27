---
title: 'Ruolo Trasporto hub non rilevato in site_BridgeheadRoleNotPresentInSite locale: Exchange 2013 Help'
TOCTitle: Ruolo Trasporto hub non rilevato in site_BridgeheadRoleNotPresentInSite locale
ms:assetid: f318c947-81a8-4c18-975a-0f1e7868042a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.bridgeheadrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 50482009
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ruolo Trasporto hub non rilevato in site\_BridgeheadRoleNotPresentInSite locale

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Il programma di installazione di Microsoft® Exchange Server 2007 viene visualizzato questo avviso perché un ruolo server Trasporto Hub esistente non è stato rilevato nel sito del servizio di directory Active Directory® locale.

Si è scelto di installare il Server cassette postali ruolo prima di un'istanza del ruolo Trasporto Hub è installato nel sito di Active Directory.

Servizi di Trasporto Hub di Exchange 2007 sono distribuiti all'interno Active Directory dell'organizzazione. Punto di manipolazione di servizi di trasporto hub tutta la posta flusso all'interno dell'organizzazione, si applica le regole di routing del flusso di posta dell'organizzazione e responsabili del recapito dei messaggi per cassetta postale del destinatario.

Gli utenti saranno in grado di eseguire l'accesso alle cassette postali, ma mail non può essere inviato o ricevuto da questa server cassette postali fino a quando non è installato un ruolo Trasporto Hub.


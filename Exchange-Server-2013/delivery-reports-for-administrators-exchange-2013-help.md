---
title: 'Rapporti di recapito per gli amministratori: Exchange 2013 Help'
TOCTitle: Rapporti di recapito per gli amministratori
ms:assetid: d98623d3-e0b7-4cb9-93fb-6351b4a06137
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ919241(v=EXCHG.150)
ms:contentKeyID: 51407430
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rapporti di recapito per gli amministratori

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

I rapporti di recapito per gli amministratori consentono di tenere traccia delle informazioni sul recapito dei messaggi inviati o ricevuti da una specifica cassetta postale dell'organizzazione. Nello specifico, i rapporti di recapito per gli amministratori utilizzano l'interfaccia di amministrazione di Exchange (EAC) per eseguire una ricerca mirata dei registri di verifica messaggi. L'ambito della ricerca è sempre una specifica cassetta postale. È possibile cercare i messaggi inviati dalla cassetta postale oppure inviati alla cassetta postale nonché filtrare i risultati della ricerca in base all'oggetto del messaggio.

In un rapporto di recapito non viene restituito il contenuto del corpo del messaggio, ma la riga dell'oggetto viene visualizzata nei risultati. Per cercare specifici messaggi di posta elettronica nelle cassette postali dell'organizzazione in base al contenuto dei messaggi, vedere [eDiscovery sul posto](https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery).

Le ricerche basate sui rapporti di recapito possono risultare utili nelle situazioni seguenti:

  - Un responsabile dà una valutazione scarsa a un apprendista perché questi non ha completato un compito nel tempo previsto. L'apprendista insiste nell'affermare di avere inviato un messaggio con il compito allegato. Il responsabile chiede di verificare lo stato del messaggio.

  - Agli utenti è stato inviato un bollettino sulla sicurezza con la richiesta di rispondere immediatamente, ma nessuno ha risposto. Il messaggio è stato ignorato oppure non è stato ricevuto?

  - Gli utenti lamentano la mancata ricezione dei messaggi inviati. Pur verificando lo stato di recapito della posta, non riescono a capire cosa avviene. Ciò potrebbe essere dovuto all'esistenza di una regola applicata ai messaggi a livello di organizzazione.

Dopo avere creato una ricerca dei rapporti di recapito, il rapporto di recapito risultante mostrerà le seguenti informazioni: mittente e destinatario del messaggio, riga dell'oggetto e data di invio del messaggio. Il rapporto di recapito mostra inoltre lo stato di recapito dei messaggi e i motivi per cui un recapito potrebbe essere in stato Ritardato o Non riuscito.

## Ulteriori informazioni sui rapporti di recapito

  - Di seguito è illustrato come creare un nuovo rapporto di recapito: [Tenere traccia dei messaggi con i rapporti di recapito](track-messages-with-delivery-reports-exchange-2013-help.md).

  - Le organizzazioni Exchange Online possono utilizzare Exchange Management Shell per eseguire la query direttamente nei registri di verifica messaggi. Per ulteriori informazioni, vedere [Registri di verifica messaggi di ricerca](search-message-tracking-logs-exchange-2013-help.md).

  - Gli utenti possono tenere traccia i propri messaggi. Per ulteriori informazioni, vedere [I rapporti di recapito per gli utenti](https://go.microsoft.com/fwlink/?linkid=279920).

  - Se l'organizzazione contiene una versione precedente di Exchange, è necessario considerare come funzionano i rapporti di recapito in Exchange 2013 tra le diverse versioni di Exchange.
    
      - I rapporti di recapito di Exchange 2013 possono verificare i messaggi tra i server Exchange 2010 nello stesso sito Active Directory.
    
      - I rapporti di recapito di Exchange 2013 possono verificare i messaggi tra i server Exchange 2007 nello stesso sito Active Directory. La funzionalità dei rapporti di recapito utilizza la chiamata a una procedura remota e un'interfaccia di servizio Web che non esiste in Exchange 2007.


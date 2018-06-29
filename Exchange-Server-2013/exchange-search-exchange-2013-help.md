---
title: 'Ricerca di Exchange: Exchange 2013 Help'
TOCTitle: Ricerca di Exchange
ms:assetid: 967e2a13-4e54-486a-ac22-08768674abbb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232132(v=EXCHG.150)
ms:contentKeyID: 52063129
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ricerca di Exchange

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-09-17_

Con l'aumento delle dimensioni delle cassette postali e della quantità dei dati archiviati sotto forma di messaggi e allegati, è importante per gli utenti essere in grado di cercare e individuare rapidamente i messaggi desiderati. [Archiviazione sul posto di Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md) consente di ridurre o di eliminare l'utilizzo di file .pst spostando in archivio gli elementi visitati precedentemente con scarsa frequenza. Ne consegue l'aumento del numero di dati delle cassette postali che possono essere archiviati dall'utente e l'utilizzo della ricerca tra le cassette postali dell'archivio principale dell'utente uno strumento importante per la produttività. [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md) consente agli utenti autorizzati di cercare contenuti nelle cassette postali tra le organizzazioni Exchange locali e basate su cloud, per essere conformi alle richieste di rilevamento elettronico (eDiscovery), alle verifiche normative o ai controlli interni. eDiscovery in locale utilizza inoltre gli indici di contenuto creati da Ricerca di Exchange.

Ricerca di Exchange differisce dall'indicizzazione di testo completo disponibile in Exchange Server 2003. Sono stati apportati miglioramenti alle prestazioni, all'indicizzazione del contenuto e alla ricerca. Ora gli elementi vengono indicizzati nella pipeline di trasporto quasi subito dopo essere stati creati o recapitati alla cassetta postale, consentendo all'utente di ricercare i dati nella cassetta postale in modo più semplice, veloce e affidabile. L'indicizzazione del contenuto è abilitata per impostazione predefinita e non è necessaria alcuna configurazione o installazione iniziale.

Per ulteriori informazioni su Exchange ricerca, vedere:

  - [Formati di file indicizzati da ricerca di Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [Proprietà messaggi indicizzati da ricerca di Exchange](message-properties-indexed-by-exchange-search-exchange-2013-help.md)

Per informazioni sulle altre attività relative a Ricerca Exchange, vedere [Exchange Search procedures](exchange-search-procedures-exchange-2013-help.md).

## Novità

Exchange 2013 introduce le seguenti modifiche a Ricerca Exchange:

  - Il modulo di indicizzazione del contenuto è stato sostituito con Microsoft Search Foundation, che offre miglioramenti delle prestazioni e delle funzionalità e funziona come il comune modulo di indicizzazione del contenuto in Exchange e SharePoint. L'interfaccia di gestione resta, tuttavia, la stessa.

  - Per impostazione predefinita, Search Foundation gestisce i formati file più comuni negli allegati di posta elettronica. Non è più necessario installare Microsoft Office Filter Pack per Ricerca Exchange. Per un elenco dei formati di file gestiti da Ricerca Exchange, vedere [Formati di file indicizzati da ricerca di Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md).
    
    È possibile aggiungere il supporto per le ulteriori formati di file da IFilter di installazione, come nelle versioni precedenti di Exchange.

  - L'indicizzazione del contenuto è più efficace poiché elabora i messaggi nella pipeline di trasporto. Di conseguenza, i messaggi indirizzati a più destinatari o gruppi di distribuzione vengono elaborati solo una volta. Un flusso di annotazioni viene allegato al messaggio, velocizzando in maniera significativa l'indicizzazione del contenuto, con un consumo minore delle risorse.


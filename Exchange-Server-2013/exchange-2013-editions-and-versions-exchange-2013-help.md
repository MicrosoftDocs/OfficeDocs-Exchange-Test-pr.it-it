---
title: 'Edizioni e versioni di Exchange 2013: Exchange 2013 Help'
TOCTitle: Edizioni e versioni di Exchange 2013
ms:assetid: b563b543-fb3f-4465-9a54-cbfd680aee1f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232170(v=EXCHG.150)
ms:contentKeyID: 50555670
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Edizioni e versioni di Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Microsoft Exchange Server 2013 è disponibile in due edizioni server: Standard Edition ed Enterprise Edition. È possibile scalare Enterprise Edition a 50 database montati per server nelle versioni RTM (Release to Manufacturing) e CU1 (Aggiornamento cumulativo 1) e a 100 database montati per server nelle versioni CU2 (Aggiornamento cumulativo 2) e successive. La Standard Edition è limitata a 5 database montati per server. Un database montato è un database in uso. Un database montato può essere un database delle cassette postali attivo montato per essere utilizzato dai client o un database delle cassette postali passivo montato durante il ripristino per la riproduzione e la replica del registro. Anche se è possibile creare più database dei limiti precedentemente indicati, è possibile montare il numero massimo sopra specificato. Il database di ripristino con conta rispetto a questo limite.

Queste edizioni in licenza sono definite da un codice "Product key". Quando viene immesso un codice "Product Key" valido e concesso in licenza, viene stabilita l'edizione supportata per il server. I codici "Product Key" possono essere utilizzati solo per gli scambi e gli aggiornamenti del codice della stessa edizione e non possono essere utilizzati per effettuare il downgrade. È possibile utilizzare un codice "Product Key" valido per passare dalla versione di valutazione (Trial Edition) di Exchange 2013 alla Standard o alla Enterprise Edition e per passare dalla Standard alla Enterprise Edition.

È inoltre possibile fornire nuovamente la licenza al server utilizzando lo stesso codice. Ad esempio, se si dispone di due server Standard Edition con due codici, ma è stato accidentalmente utilizzato lo stesso codice su entrambi i server, è possibile scambiare uno dei due codici con l'altro codice che è stato rilasciato. È possibile eseguire tali operazioni senza reinstallare o riconfigurare alcun elemento. Una volta immesso il codice e riavviato il servizio Archivio informazioni di Microsoft Exchange, verrà applicata l'edizione corrispondente al codice "Product Key".

Non si verifica alcuna perdita di funzionalità quando la versione di valutazione scade e pertanto è possibile mantenere gli ambienti di lavoro, di demo, di formazione e altri ambienti non di produzione per oltre 120 giorni senza dover reinstallare l'edizione di valutazione di Exchange 2013.

Come precedentemente indicato, non è possibile utilizzare i codici "Product Key" per effettuare il downgrade dalla Enterprise Edition alla Standard Edition, né per tornare all'edizione di prova. Questi tipi di downgrade possono essere effettuati solo disinstallando Exchange 2013, reinstallando Exchange 2013 e immettendo il codice "Product Key" corretto.

## Versioni di Exchange 2013

Per un elenco delle versioni di Exchange 2013 e informazioni su come aggiornare e scaricare la versione più recente di Exchange 2013, vedere i seguenti argomenti:

  - [Aggiornamenti di Exchange Server: numeri di build e date di rilascio](https://technet.microsoft.com/it-it/library/hh135098\(v=exchg.150\))

  - [Upgrade di Exchange 2013 all'aggiornamento cumulativo o Service Pack più recente](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)

Per visualizzare il numero di build per la versione di Exchange 2013 in esecuzione, utilizzare il seguente comando in Exchange Management Shell.

    Get-ExchangeServer | fl name,edition,admindisplayversion

## Tipi di licenze di Exchange 2013

Exchange 2013 viene concesso in licenza nel modello Server/Client Access License (CAL), modalità analoga alla concessione in licenza di Exchange 2010. Di seguito vengono riportati i tipi di licenze:

  - **Licenze server**   È necessario assegnare una licenza per ogni istanza del software server eseguito. La licenza server viene venduta in due edizioni server: Standard Edition ed Enterprise Edition.

  - **Licenze CAL (Client Access License)**   Exchange 2013 è inoltre disponibile in due edizioni con licenza CAL, denominate Standard CAL ed Enterprise CAL. È possibile combinare e associare le edizioni server con i tipi CAL. Ad esempio, è possibile utilizzare licenze CAL Enterprise con Exchange 2013 Standard Edition. Analogamente, è possibile utilizzare licenze CAL Standard con Exchange 2013 Enterprise Edition.

Per ulteriori informazioni sui tipi di licenze di Exchange, vedere [Licenze](https://go.microsoft.com/fwlink/p/?linkid=392675).


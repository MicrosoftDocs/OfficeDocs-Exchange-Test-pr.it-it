---
title: 'Archivio gestito: Exchange 2013 Help'
TOCTitle: Archivio gestito
ms:assetid: efdaf80b-335c-491c-8eb5-1fafd297e8a2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn792020(v=EXCHG.150)
ms:contentKeyID: 62606343
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Archivio gestito

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-07-14_

Tutte le versioni precedenti di Exchange Server, da Exchange Server 4.0 per Exchange Server 2010, sono supportati in esecuzione una sola istanza del processo di archivio informazioni (Store.exe) nel ruolo del server cassette postali. Questa istanza archivio unica ospita tutti i database nel server: attiva, passiva, ritardata e il ripristino. In architetture di Exchange precedente, è disponibile, gli interventi di isolamento tra i diversi database ospitati in un server cassette postali. Un problema con un database delle cassette postali singolo è in grado di avere effetti negativi sulla tutti gli altri database e arresti anomali risultante da un danneggiamento delle cassette postali possono influire sulle servizio per tutti gli utenti il cui database sono ospitati su tale server.

Un altro problema con una singola istanza di archiviazione nelle versioni precedenti di Exchange è che il motore di ESE (Extensible Storage) Ridimensiona anche a 12 8 core, ma oltre a quello, scala negativa causare problemi di sincronizzazione della cache e le comunicazioni tra più processori. Data odierna quantità server più grandi, con 16 + sistemi core disponibili, ciò significa impongono l'amministrazione difficoltà di gestione dell'affinità di 12 8 core per ESE e con altri core per i processi di archiviazione non (ad esempio, assistenti, Search Foundation, disponibilità gestita e così via). Inoltre, l'architettura precedente con restrizioni implementare la scalabilità verticale per il processo di archiviazione.

Il processo Store.exe evoluzione notevolmente nel corso degli anni come Server di Exchange stesso evoluzione, ma come un unico processo, in ultima analisi relativa scalabilità è limitata e rappresenta un singolo punto di errore. A causa di questi limiti Store.exe stati di Exchange 2013 e sostituito dall'archivio gestito.

## Archivio gestito

Archivio gestito è il nome per l'archivio informazioni (ovvero l'archivio) elabora di Exchange Server 2013. Archivio gestito utilizza un modello di processo controller/lavoro che fornisce l'isolamento dei processi di archiviazione e il failover del database più veloci. Archivio gestito include inoltre un nuovo database statico della memorizzazione nella cache meccanismo che sostituisce l'algoritmo dinamica del buffer nelle versioni precedenti di Exchange Server. Nel modello a più processo utilizzato dall'archivio gestito, non vi è un processo del controller singolo archivio service (in questo caso, ovvero MSExchangeIS Microsoft.Exchange.Store.Service.exe) e un processo di lavoro (in questo caso, Microsoft.Exchange.Store.Worker.exe) per ogni database installati. Quando viene installato un database, un nuovo processo di lavoro viene creata un'istanza che fornisce servizi solo tale database. Quando un database viene disinstallato, il processo di lavoro per il database viene terminato.

Ad esempio, se si dispone di 40 database installati in un server, ci sarà 41 processi in esecuzione per l'archivio gestito, uno per ogni database e uno per il controller di processo del servizio di archiviazione.

Il controller di processo del servizio di archiviazione è molto sottile e affidabile, ma se muore o viene terminata, tutti i processi di lavoro annullamento (verrà rilevano il processo di controller del servizio non sia più presente e uscire da). Il controller di processo archivio di monitoraggio dell'integrità di tutti i processi di lavoro di archiviazione nel server. La terminazione in Gigabit o imprevista il Microsoft.Exchange.Store.Service.exe provoca un failover immediata di tutte le copie del database attivo. Archivio gestito è inoltre strettamente integrato con il servizio replica di Microsoft Exchange (MSExchangeRepl.exe) e il Manager attivo. Il processo del controller, i processi di lavoro e il servizio di replica interagiscono per garantire una maggiore disponibilità e l'affidabilità:

  - Processo del servizio di replica di Microsoft Exchange (MSExchangeRepl.exe)
    
      - Responsabile per l'emissione di montare e smontare operazioni all'archivio
    
      - Avvia un'azione di ripristino nella archiviazione o database gli errori segnalati dallo risponditori archivio, il motore di ESE (Extensible Storage) e disponibilità gestita
    
      - Rileva un errore imprevisto del database
    
      - Fornisce l'interfaccia di amministrazione per attività di gestione

  - Servizio di archiviazione processo/controller (Microsoft.Exchange.Store.Service.exe)
    
      - Consente di gestire ogni durata del processo di lavoro in operazioni di montaggio e dismount fornite dal servizio replica di base
    
      - Gestisce le richieste in arrivo da Gestione controllo servizi Windows
    
      - Registra gli elementi quando rilevati problemi di processo di lavoro archivio (ad esempio, si blocchi o uscita imprevisto)
    
      - Termina l'archivio di processi di lavoro in caso di failover di risposta

  - Archiviare il processo di lavoro (Microsoft.Exchange.Store.Worker.exe)
    
      - Responsabile dell'esecuzione di operazioni RPC per le cassette postali in un database
    
      - Istanza di endpoint RPC all'interno di processo di lavoro è il GUID del database
    
      - Include cache del database per un database

## Algoritmo di memorizzazione nella cache Database statico

L'algoritmo di memorizzazione nella cache di database noto come allocazione dinamica del buffer che è stato introdotto in Exchange Server 5.5 e inoltre utilizzato per il servizio Archivio informazioni di Exchange 2000 Server, Exchange Server 2003, Exchange Server 2007 ed Exchange Server 2010, è inoltre più presente da Exchange 2013. Exchange 2013 utilizza un algoritmo molto semplice e rapido per la determinazione della cache di database. Archivio gestito riallocare non è più in modo dinamico cache tra database in caso di failover, semplificando notevolmente la gestione della cache interna. In realtà, la memoria allocata per ogni cache di database (ad esempio, ogni processo di lavoro store) dipende dal numero di copie del database locale e il valore di *MaximumActiveDatabases*, se configurata. Se il valore di *MaximumActiveDatabases* è maggiore del numero di copie del database corrente, il calcolo della cache si basa sul numero di copie del database.

L'algoritmo statico utilizzato da Exchange 2013 esegue l'allocazione di memoria della cache di ESE degli processo di lavoro ogni archivio basato su RAM fisica. Questa operazione viene definita del database *Max Cache di destinazione*. 25% della memoria totale del server viene assegnato alla cache di ESE. Questa operazione viene definita la *Destinazione di dimensioni della Cache di Server*.


> [!NOTE]
> L'obiettivo di dimensioni della Cache di Server e pertanto la quantità di memoria allocata per l'archivio della cache di ESE, può essere ignorati utilizzando <EM>msExchESEParamCacheSizeMax</EM> attributo dell'oggetto <EM>InformationStore</EM> in Active Directory (il valore configurato è il numero di pagine 32 ko di allocazione in tutti i processi di archiviazione).



Una quantità statica di tale cache viene allocata al copie attive e passive. Il processo di lavoro di archiviazione allocato sarà destinazione massima della Cache solo quando la manutenzione di una copia del database attivo. Copie passive del database vengono allocate al 20 percento della destinazione massima della Cache. Nella parte restante è riservata per l'archivio e allocata al processo di lavoro se il database passa da passivi a attivo.

Numero massimo Cache di destinazione viene calcolata solo all'avvio di archiviazione. Di conseguenza, se si aggiunge o rimuove i database o delle copie del database, è necessario riavviare il servizio controller di archiviazione (MSExchangeIS) in modo che la cache può essere regolata di conseguenza. Se il servizio non viene riavviato, quindi appena creato database è una destinazione di dimensioni della cache dimensioni inferiore rispetto ai database creato prima dell'avvio del servizio. In questo caso, la somma di destinazioni di dimensioni della cache di database probabilmente supera la destinazione di dimensioni della Cache di Server, è necessario riavviare MSExchangeIS.

## Calcoli della Cache di Database di esempio

Di seguito è database di esempio della memorizzazione nella cache i calcoli basati su un server di cassette postali della memoria e configurazione del database.

**Nell'esempio 1**

In questo esempio, il server cassette postali è 48 GB di memoria e ospita due database attivi e due database passivi. Inoltre, il parametro *MaximumActiveDatabases* non è configurato. In questa configurazione, la quantità di cache del database è 3 per ogni processo di lavoro Copia database attiva e 0,6 GB per ogni processo di lavoro copia passiva del database. Ecco come questi valori sono stati ottenuti.

Per ottenere la destinazione di dimensioni della Cache di Server, è necessario moltiplicare la quantità di memoria del 25%:

48 GB X 25% = 12 GB

Per ottenere la destinazione della Cache numero massimo di Database, dividere la destinazione di dimensioni della Cache di Server per il numero totale di database attivi e passivi:

12 GB / 4 database = 3 GB

Per determinare la quantità di memoria utilizzata per le copie passive del database, è necessario moltiplicare la destinazione della Cache numero massimo di Database per il 20%:

3 GB X 20% = 0,6 GB

Da 12 GB di memoria assegnato alla destinazione di dimensioni della Cache di Server, 7,2 GB sarà utilizzato da processi di lavoro di database e viene riservato 4,8 GB per l'archivio informazioni per le due copie passive del database in caso di diventano copie attive. In tal caso, si utilizzeranno i Target di Cache Max 3 GB.

**Nell'esempio 2**

In questo esempio, il server cassette postali dispone inoltre 48 GB di memoria e ospita due database attivi e due database passivi; Tuttavia, il parametro *MaximumActiveDatabases* viene configurato con un valore pari a 2. In questa configurazione, la quantità di cache del database è 5 GB per ogni processo di lavoro Copia database attiva e 0,2 GB per ogni processo di lavoro copia passiva del database. Ecco come questi valori sono stati ottenuti.

Per ottenere la destinazione di dimensioni della Cache di Server, è necessario moltiplicare la quantità di memoria del 25%:

48 GB X 25% = 12 GB

Per ottenere la destinazione della Cache numero massimo di Database, dividere la destinazione dimensioni della Cache di Server per il numero totale di database attiva e il numero totale di database passivi moltiplicato per il 20%:

12 GB / (2A + (2 P X 20 %)) = 5 GB

Per determinare la quantità di memoria utilizzata per le copie passive del database, è necessario moltiplicare la destinazione della Cache numero massimo di Database per il 20%:

5 GB X 20% = 1 GB

Da 12 GB di memoria assegnato alla destinazione di dimensioni della Cache di Server, 12 GB sarà utilizzato da processi di lavoro di database e memoria non verrà riservata per l'archivio informazioni per le due copie passive del database perché non è diventano di copie attive in questa configurazione, (perché *MaximumActiveDatabases* viene configurato con il valore 2 e sono presenti già 2 copie del database attive sul server).


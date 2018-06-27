---
title: 'Copie del database delle cassette postali: Exchange 2013 Help'
TOCTitle: Copie del database delle cassette postali
ms:assetid: ce748bca-3e24-493b-b9e6-153157bffd6a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd979802(v=EXCHG.150)
ms:contentKeyID: 50481686
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Copie del database delle cassette postali

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-07_

Microsoft Exchange Server 2013 sfrutta il concetto di mobilità del database, corrispondente ai failover a livello di database gestiti da Exchange. La mobilità del database consente di disconnettere i database dai server, di aggiungere il supporto per un massimo di 16 copie di un singolo database e di aggiungere copie di database a un database.

## Caratteristiche principali

Di seguito sono riportate le caratteristiche principali delle copie dei database delle cassette postali:

  - Fino a 16 copie di un Exchange 2013 database delle cassette postali possono essere creati in più server cassette postali, fornito che i server sono raggruppati in un gruppo di disponibilità del database (DAG), che corrisponde a un limite per la replica continua. database delle cassette postali Exchange 2013 possono essere replicati solo ad altri server di cassette postali Exchange 2013 all'interno di un DAG. Non è possibile replicare un database all'esterno di un DAG, né può replicare un database delle cassette postali Exchange 2013 a un server che esegue Exchange 2010 o versioni precedenti. Per informazioni dettagliate sui DAG, vedere [Gruppi di disponibilità dei database (DAG)](database-availability-groups-dags-exchange-2013-help.md).

  - Tutti i server di cassette postali in un gruppo di disponibilità del database devono trovarsi nello stesso dominio diActive Directory.

  - Le copie del database delle cassette postali supportano i concetti dell'intervallo di riesecuzione e del ritardo di troncamento. Prima di abilitare queste funzionalità, è necessario eseguire una pianificazione appropriata.

  - È possibile eseguire il backup di tutte le copie del database delle cassette postali utilizzando un'applicazione di backup basata sul Servizio Copia Shadow del volume e compatibile con Exchange.

  - Le copie del database possono essere create solo sui server di cassette postali che non ospitano la copia attiva di un database. Non è possibile creare due copie dello stesso database sullo stesso server.

  - Tutte le copie di un database utilizzano lo stesso percorso su ogni server contenente una copia. I percorsi del database e dei file di registro per una copia del database su ciascun server di cassette postali non devono essere in conflitto con qualsiasi altro percorso del database.

  - Le copie del database possono essere create negli stessi siti di Active Directory o in siti differenti, sulla stessa subnet di rete o su subnet diverse.

  - Le copie del database non sono supportate tra server di cassette postali con latenza di rete round trip superiore a 500 millisecondi.

## Copie del database delle cassette postali

È possibile creare una copia del database delle cassette postali in qualsiasi momento. Le copie del database delle cassette postali possono essere distribuite nei server di cassette postali in maniera flessibile e granulare.

È possibile creare una copia del database delle cassette postali utilizzando la procedura guidata **Aggiungi copia del database delle cassette postali** in Interfaccia di amministrazione di Exchange o utilizzando il cmdlet **Add-MailboxDatabaseCopy** in Exchange Management Shell.

Durante la creazione di una copia del database delle cassette postali è necessario specificare i seguenti parametri:

  - *Identity*    Questo parametro consente di specificare il nome del database da copiare. I nomi dei database devono essere univoci all'interno dell'organizzazione di Exchange.

  - *MailboxServer*   Questo parametro consente di specificare il nome del server che ospiterà la copia del database delle cassette postali. Il server deve essere un membro del DAG stesso e non deve già presente una copia del database.

Eventualmente, è possibile anche specificare quanto segue:

  - *ActivationPreference*    Questo parametro consente di specificare il numero della preferenza di attivazione, che viene utilizzato come parte del processo di selezione della copia migliore di Active Manager. Viene anche utilizzato per ridistribuire i database attivi delle cassette postali nell'ambito del DAG quando si utilizza lo script RedistributeActiveDatabases.ps1. Il valore della preferenza di attivazione è un numero uguale a o maggiore di 1, dove 1 si trova al vertice dell'ordine di preferenza. Il numero di posizione non può essere superiore al numero delle copie del database delle cassette postali.

  - *ReplayLagTime * Questo parametro consente di specificare il tempo di attesa del servizio Replica di Exchange prima della riproduzione dei file di log copiati nella copia del database. Il formato di questo parametro è giorni.ore:minuti:secondi. Il valore predefinito per questa impostazione è 0 secondi. L'impostazione massima consentita per questo valore è 14 giorni. L'impostazione minima consentita è 0 secondi. Se l'intervallo di riesecuzione è impostato su 0, il ritardo di riesecuzione del registro viene disattivato.

  - *TruncationLagTime* Questo parametro consente di specificare il tempo di attesa del servizio Replica di Exchange prima di troncare i file di log riprodotti in una copia del database. Il periodo di tempo ha inizio successivamente alla riesecuzione del registro nella copia del database. Il formato di questo parametro è giorni.ore:minuti:secondi. Il valore predefinito per questa impostazione è 0 secondi. L'impostazione massima consentita per questo valore è 14 giorni. L'impostazione minima consentita è 0 secondi. Se l'intervallo di troncamento è impostato su 0, il ritardo di troncamento del registro viene disattivato.

  - *SeedingPostponed*    Questo parametro consente di specificare che non è necessario eseguire automaticamente il seeding della copia del database sul server Cassette postali specificato. Questa opzione è in genere utilizzata quando si intende effettuare il seeding di una nuova copia del database delle cassette postali utilizzando una copia passiva esistente del database (ad esempio, aggiungendo una seconda copia di un determinato database in una posizione remota). Quando si utilizza tale parametro, è necessario effettuare manualmente il seeding della copia del database utilizzando il cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)).

Per ulteriori informazioni sulla creazione, sull'utilizzo e sulla gestione delle copie del database delle cassette postali, vedere [Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md).


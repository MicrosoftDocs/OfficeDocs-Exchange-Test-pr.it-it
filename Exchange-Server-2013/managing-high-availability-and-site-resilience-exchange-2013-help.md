---
title: 'Gestione di elevata disponibilità e resilienza del sito: Exchange 2013 Help'
TOCTitle: Gestione di elevata disponibilità e resilienza del sito
ms:assetid: f9677392-88d2-457f-a488-245771a8c1f2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638215(v=EXCHG.150)
ms:contentKeyID: 50482060
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione di elevata disponibilità e resilienza del sito

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-11-05_

Dopo aver creato, convalidato e distribuito una soluzione di disponibilità elevata o resilienza del sito di Microsoft Exchange Server 2013, avviene una transizione dalla fase di distribuzione alla fase operativa del ciclo di vita complessivo della soluzione. La fase operativa è costituita da diverse attività, tutte correlate a una delle seguenti aree: gruppi di disponibilità del database (DAG), copie del database delle cassette postali, esecuzione del monitoraggio proattivo e gestione di passaggi e failover.

**Sommario**

Database availability group management

Mailbox database copy management

Proactive monitoring

Switchovers and failovers

## Gestione del gruppo di disponibilità del database

Le attività di gestione operativa associate ai DAG includono:

  - **Creazione di uno o più gruppi di disponibilità del database**   La creazione di un gruppo di disponibilità del database è generalmente una procedura eseguita una sola volta durante la fase di distribuzione del ciclo di vita della soluzione. Tuttavia, possono esistere ragioni che richiedono la creazione dei gruppi di disponibilità del database durante la fase operativa, ad esempio:
    
      - Il gruppo di disponibilità del database è configurato per la modalità di replica di terze parti e si desidera ripristinare l'uso della replica continua. Non è possibile riconvertire un gruppo di disponibilità del database alla replica continua; è necessario creare un nuovo gruppo di disponibilità del database.
    
      - Si dispone di server in più domini. Tutti i membri dello stesso gruppo di disponibilità del database devono essere membri dello stesso dominio.

  - **Gestione dell'appartenenza al gruppo di disponibilità del database**   La gestione dei membri del gruppo di disponibilità del database è un'attività eseguita raramente, in genere durante la fase di distribuzione del ciclo di vita della soluzione. Tuttavia, a causa della flessibilità fornita dalla distribuzione incrementale, la gestione dell'appartenenza al gruppo di disponibilità del database può essere eseguita anche durante il ciclo di vita della soluzione.

  - **Configurazione delle proprietà del gruppo di disponibilità del database**   Ciascun gruppo di disponibilità del database dispone di diverse proprietà che possono essere configurate secondo necessità. Queste proprietà includono:
    
      - **Server e directory di controllo**   Il server di controllo è un server esterno al gruppo di disponibilità del database che agisce come voter di quorum quando il gruppo di disponibilità del database contiene un numero pari di membri. La directory di controllo viene creata e condivisa sul server di controllo per essere utilizzata dal sistema al fine di mantenere un quorum.
    
      - **Indirizzi IP**   Ciascun gruppo di disponibilità del database disporrà di uno o più indirizzi IPv4 e, facoltativamente, di uno o più indirizzi IPv6. Gli indirizzi IP assegnati al gruppo di disponibilità del database sono utilizzati dal cluster sottostante al gruppo di disponibilità del database. Il numero di indirizzi IPv4 assegnati al gruppo di disponibilità del database equivale al numero di subnet che compongono la rete MAPI utilizzata dal gruppo di disponibilità del database. È possibile configurare il gruppo di disponibilità del database affinché utilizzi indirizzi IP statici o in modo da ottenere automaticamente gli indirizzi per mezzo di DHCP (Dynamic Host Configuration Protocol).
    
      - **Modalità di coordinamento dell'attivazione del datacenter**   La modalità di coordinamento dell'attivazione del datacenter indica l'impostazione di una proprietà su un gruppo di disponibilità del database progettato per impedire le condizioni "split brain" a livello di database, in uno scenario in cui viene ripristinato il funzionamento di un datacenter primario dopo l'esecuzione del passaggio del datacenter. Per ulteriori informazioni sulla modalità di coordinamento dell'attivazione del datacenter, vedere [modalità di coordinamento dell'attivazione del centro dati](datacenter-activation-coordination-mode-exchange-2013-help.md).
    
      - **Server e directory di controllo alternativi**   Il server e la directory di controllo alternativi sono valori che è possibile preconfigurare come parte del processo di pianificazione del passaggio del datacenter. Indicano il server e la directory di controllo che saranno utilizzate nell'esecuzione di un passaggio del datacenter.
    
      - **Porta di replica**   Per impostazione predefinita, tutti i gruppi di disponibilità del database utilizzano la porta TCP 64327 per la replica continua. È possibile modificare il gruppo di disponibilità del database al fine di utilizzare una porta TCP diversa per la replica utilizzando il parametro *ReplicationPort* del cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\)).
    
      - **Individuazione della rete**   È possibile imporre al DAG di individuare nuovamente le reti e le interfacce di rete. Questa operazione viene eseguita quando si aggiungono o rimuovono reti o si introducono nuove subnet. La nuova individuazione di tutte le reti DAG può essere imposta utilizzando il parametro *DiscoverNetworks* del cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\)).
    
      - **Compressione di rete**   Per impostazione predefinita, i gruppi di disponibilità del database (DAG) utilizzano la compressione solo tra reti DAG in subnet diverse. È possibile abilitare la compressione per tutte le reti DAG o solo per le operazioni di seeding, oppure è possibile disabilitare la compressione per tutte le reti DAG.
    
      - **Crittografia di rete**   Per impostazione predefinita, i gruppi di disponibilità del database (DAG) utilizzano la crittografia solo tra reti DAG in subnet diverse. È possibile abilitare la crittografia per tutte le reti DAG o solo per le operazioni di seeding, oppure è possibile disabilitare la crittografia per tutte le reti DAG.

  - **Arresto dei membri del gruppo di disponibilità del database**   La soluzione di disponibilità elevata di Exchange 2013 è integrata con il processo di arresto di Windows. Se un amministratore o un'applicazione avvia la chiusura di un server Windows in un DAG che dispone di un database replicato in uno o più membri del DAG, il sistema cerca di attivare un'altra copia dei database installati prima di consentire il completamento della procedura di chiusura. Tuttavia, questo nuovo comportamento non garantisce un'attivazione senza perdita di dati per tutti i database sul server in chiusura. Di conseguenza, la procedura consigliata prevede di eseguire un passaggio di server prima di arrestare un server membro di un gruppo di disponibilità del database.

Per la procedura dettagliata relativa alla creazione di un DAG, vedere [Creare un gruppo di disponibilità del database](create-a-database-availability-group-exchange-2013-help.md). Per la procedura dettagliata sulla configurazione dei DAG e sulle proprietà relative, vedere [Configurazione delle proprietà del gruppo di disponibilità del database](configure-database-availability-group-properties-exchange-2013-help.md). Per ulteriori informazioni sulle precedenti attività di gestione e sulla gestione dei gruppi di disponibilità del database in generale, vedere [Gestione dei gruppi di disponibilità del database](managing-database-availability-groups-exchange-2013-help.md).

Inizio pagina

## Gestione della copia del database delle cassette postali

Le attività di gestione operativa associate alle copie del database delle cassette postali includono:

  - **Aggiunta di copie del database delle cassette postali**   Quando si aggiunge una copia di un database delle cassette postali, la replica continua tra il database esistente e la copia del database viene abilitata automaticamente.

  - **Configurazione delle proprietà della copia del database delle cassette postali**   È possibile configurare diverse proprietà, ad esempio i criteri di attivazione del database, la durata degli intervalli di riesecuzione e troncamento, e le preferenze di attivazione per la copia del database.

  - **Sospensione o ripresa di una copia del database delle cassette postali**   È possibile sospendere una copia del database delle cassette postali per prepararsi al seeding o ad altre forme di manutenzione. È inoltre possibile sospendere una copia del database delle cassette postali solo per l'attivazione. Questa configurazione impedisce al sistema di attivare automaticamente la copia a seguito di un errore, ma consente ancora al sistema di mantenere aggiornata la copia del database con il log shipping e la riesecuzione.

  - **Aggiornamento di una copia del database delle cassette postali**   L'aggiornamento, noto anche come *seeding*, è il processo tramite il quale una copia del database delle cassette postali viene aggiunta ad un altro server Cassette postali. Questo diventa il database di riferimento della copia. Dopo il primo seeding della copia del database di riferimento, solo in rari casi sarà necessario ripetere il seeding del database.

  - **Attivazione di una copia del database delle cassette postali**   L'attivazione è il processo con cui una specifica copia passiva viene designata come nuova copia attiva di un database delle cassette postali. Questo processo viene definito *passaggio*. Per ulteriori informazioni, vedere "Passaggi e failover" più avanti in questo argomento.

  - **Rimozione di una copia del database delle cassette postali**   È possibile rimuovere una copia del database delle cassette postali in qualsiasi momento. In alcuni casi, potrebbe essere necessario rimuovere una copia del database delle cassette postali. Ad esempio, non è possibile rimuovere un server Cassette postali da un gruppo di disponibilità del database fin quando dal server non sono state rimosse tutte le copie del database delle cassette postali. Inoltre, è necessario rimuovere tutte le copie di un database delle cassette postali prima di poter cambiare il percorso di un database delle cassette postali.

Per la procedura dettagliata su come aggiungere una copia del database delle cassette postali, vedere [Aggiungere una copia del database delle cassette postali](add-a-mailbox-database-copy-exchange-2013-help.md). Per la procedura dettagliata relativa alla configurazione delle copie del database delle cassette postali, vedere [Configurazione delle proprietà della copia del database delle cassette postali](configure-mailbox-database-copy-properties-exchange-2013-help.md). Per ulteriori informazioni sulle precedenti attività di gestione e sulla gestione delle copie del database delle cassette postali in generale, vedere [Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md). Per la procedura dettagliata su come rimuovere una copia del database delle cassette postali, vedere [Rimuovere una copia del database delle cassette postali](remove-a-mailbox-database-copy-exchange-2013-help.md).

Inizio pagina

## Monitoraggio proattivo

Per le operazioni quotidiane legate alle messaggistica è fondamentale assicurarsi che i server operino in modo affidabile e che le copie dei database siano integre. Exchange 2013 include numerose funzionalità utilizzabili per eseguire diverse attività di monitoraggio dello stato dei gruppi di disponibilità del database e delle copie del database delle cassette postali, tra cui:

  - [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/it-it/library/dd298044\(v=exchg.150\))

  - [Test-ReplicationHealth](https://technet.microsoft.com/it-it/library/bb691314\(v=exchg.150\))

  - Registrazione degli eventi del canale Crimson

Oltre a monitorare l'integrità e lo stato, è anche di importanza cruciale per monitorare le situazioni che rischiano di compromettere la disponibilità. Ad esempio, è consigliabile monitorare la ridondanza dei database replicati. È fondamentale evitare le situazioni in cui il sistema è inattivo con una singola copia di un database. Questo scenario deve essere affrontato con il più alto livello di priorità e risolto nel minor tempo possibile.

Per ulteriori informazioni sul monitoraggio dell'integrità e dello stato dei gruppi di disponibilità del database (DAG) e delle copie del database delle cassette postali, vedere [Gruppi di disponibilità del database di monitoraggio](monitoring-database-availability-groups-exchange-2013-help.md).

Inizio pagina

## Passaggi e failover

Un *passaggio* è un processo manuale in cui un amministratore attiva manualmente una o più copie del database delle cassette postali. I passaggi, che possono avvenire a livello di database o di server, vengono generalmente eseguiti come parte della preparazione alle attività di manutenzione. La gestione del passaggio richiede l'esecuzione di passaggi di database o server secondo le necessità. Ad esempio, per eseguire la manutenzione su un server Cassette postali in un gruppo di disponibilità del database, per prima cosa è necessario eseguire un passaggio di server in modo che il server non contenga copie del database delle cassette postali attive. Per ulteriori informazioni sull'esecuzione di uno switchover del database, vedere [Attivare una copia del database delle cassette postali](activate-a-mailbox-database-copy-exchange-2013-help.md). I passaggi possono essere eseguiti anche a livello di centro dati.

Un *failover* è l'attivazione automatica, da parte del sistema, di una o più copie del database a seguito di un errore. Ad esempio, la perdita di un'unità disco in un ambiente RAID provoca un failover del database. La perdita della rete MAPI o un'interruzione dell’energia elettrica provocano un failover del server.

Inizio pagina


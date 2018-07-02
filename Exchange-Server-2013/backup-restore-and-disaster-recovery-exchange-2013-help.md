---
title: 'Backup, ripristino e ripristino di emergenza: Exchange 2013 Help'
TOCTitle: Backup, ripristino e ripristino di emergenza
ms:assetid: 394fc4ed-fa02-41fa-9159-cc2754ff8875
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876874(v=EXCHG.150)
ms:contentKeyID: 50480362
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Backup, ripristino e ripristino di emergenza

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Per questo, è importante capire in che modo i dati possono essere protetti e determinare il metodo che meglio soddisfa le esigenze dell'organizzazione. La pianificazione della protezione dei dati è un processo complesso basato su molte decisioni prese durante la fase di pianificazione della distribuzione.

Tradizionalmente, i backup sono stati utilizzati per gli scenari seguenti:

  - **Ripristino di emergenza**   Nel caso in cui si verifichi un errore software o hardware, più copie del database in un gruppo di disponibilità del database garantiscono una disponibilità elevata con tempi di failover più brevi con perdita dei dati minima o nulla. Ciò elimina i tempi di inattività e la risultante perdita di produttività che rappresenta un costo notevole per l'organizzazione derivante dal ripristino da un backup temporizzato precedente su disco o nastro. I DAG possono essere estesi su più siti e possono offrire la resilienza contro errori del disco, del server, della rete e del datacenter.

  - **Ripristino di elementi eliminati accidentalmente**   Prima, quando un utente eliminava degli elementi che in seguito dovevano essere ripristinati, era necessario individuare il supporto di backup in cui erano archiviati i dati e in qualche modo recuperare gli elementi desiderati e fornirli all'utente. Grazie alla nuova cartella Elementi ripristinabili in Exchange 2013 e al criterio di blocco ad essa applicabile, è possibile mantenere tutti i dati eliminati e modificati per un determinato periodo di tempo. In questo modo, il ripristino di questi elementi è più semplice e più veloce. Ciò riduce il carico di lavoro degli amministratori e dell'assistenza tecnica di Exchange consentendo agli utenti finali di ripristinare da soli gli elementi eliminati accidentalmente, semplificando il processo e riducendo i costi associati al ripristino di un singolo elemento. Per ulteriori informazioni, vedere [Criteri di messaggistica e conformità](messaging-policy-and-compliance-exchange-2013-help.md) e [Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md).

  - **Archiviazione dei dati a lungo termine**   I backup vengono anche usati per archiviare i dati e di solito viene utilizzato il nastro per conservare istantanee temporizzate dei dati per lunghi periodi di tempo, come dettato dai requisiti di conformità. Le nuove funzionalità relative all'archiviazione, alla ricerca in più cassette postali e alla conservazione dei messaggi in Exchange 2013 consentono all'utente finale di conservare i dati in modo semplice per lunghi periodi di tempo. In questo modo vengono eliminati costosi ripristini da nastro e aumenta la produttività. Per ulteriori informazioni, vedere [Archiviazione sul posto di Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md), [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md) e [Archiviazione sul posto e conservazione per controversia legale](in-place-hold-and-litigation-hold-exchange-2013-help.md).

  - **Istantanea del database temporizzata**   Se per l'organizzazione è necessaria una copia precedente temporizzata dei dati della cassetta postale, Exchange offre la possibilità di creare una copia del database ritardata in un ambiente DAG. Ciò può essere utile nel caso remoto in cui un danneggiamento della partizione logica si ripeta in più database del DAG e quindi sia necessario tornare a uno stato precedente. Potrebbe anche essere utile se un amministratore elimina accidentalmente i dati dell'utente o delle cassette postali. È possibile che il ripristino da una copia ritardata sia più veloce rispetto al ripristino da un backup. Infatti le copie ritardate non richiedono il processo di copia (dispendioso in termini di tempo) dal server di backup al server Exchange. Questo può ridurre in modo significativo il costo totale di proprietà, riducendo i tempi di inattività.

Poiché esistono funzionalità native di Exchange 2013 che consentono di soddisfare ognuno di questi scenari in modo efficace, è possibile ridurre o eliminare l'uso dei backup tradizionali nell'ambiente.

Exchange Native Data Protection

Supported Backup Technologies

Exchange 2013 VSS Writer

Server Recovery

Unified Contact Store Recovery

Recovery Database

Database Portability

Dial Tone Portability

## Protezione dei dati nativi di Exchange

Microsoft [architettura preferito](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx) per Exchange Server 2013 utilizza il concetto di Exchange Native Data Protection. Exchange Protezione dei dati nativi basato sulle funzionalità incorporata Exchange per proteggere i dati delle cassette postali, senza l'utilizzo dei backup (sebbene sia possibile comunque utilizzare le caratteristiche e creare copie di backup). Exchange 2013 include numerose nuove funzionalità e componenti di base viene modificato, quando distribuito e configurato correttamente, è possibile fornire protezione dei dati nativi che elimina l'esigenza di rendere tradizionale backup dei dati. Grazie alle funzionalità di disponibilità elevata incorporata in Exchange 2013 per ridurre al minimo i tempi di inattività e la perdita di dati in caso di emergenza può inoltre ridurre il costo totale di proprietà del sistema di messaggistica. Tramite la combinazione di queste funzionalità con altre funzionalità incorporate, ad esempio giudiziari, è possibile ridurre o eliminare l'utilizzo dei backup tradizionale punto nel tempo e ridurre i costi associati.

Oltre a determinare se Exchange 2013 consente di non eseguire i backup tradizionali temporizzati, si consiglia di valutare il costo dell'infrastruttura di backup corrente. Considerare il costo dei tempi di inattività dell'utente finale e la perdita dei dati quando si cerca di eseguire il ripristino da un'infrastruttura di backup esistente. Inoltre, includere i costi relativi alla licenza, all'installazione e all'hardware, così come i costi di gestione associati al ripristino dei dati e al mantenimento dei backup. In base ai requisiti dell'organizzazione, è probabile che un ambiente Exchange 2013 puro con almeno tre copie del database delle cassette postali fornisca costi totali di proprietà inferiori rispetto a uno con backup.

È necessario considerare diversi motivi di natura tecnica e diversi problemi prima di utilizzare le funzionalità incorporate in Exchange 2013 in sostituzione ai tradizionali backup. Potrebbero esserci anche considerazioni specifiche per la propria organizzazione. Considerare i seguenti problemi e tenere presente che non si tratta di un elenco esaustivo:

  - È necessario determinare la quantità di copie di database da distribuire. Si consiglia di distribuire almeno tre copie (non ritardate) di un database delle cassette postali prima di eliminare i tradizionali sistemi di protezione del database, quali i backup tradizionali basati su VSS o le soluzioni RAID (Redundant Array of Independent Disks).

  - È necessario definire in modo chiaro l'obiettivo temporale di recupero e gli obiettivi per il punto di recupero e stabilire che l'utilizzo di un insieme combinato di funzionalità incorporate al posto di backup tradizionali consente di raggiungere questi obiettivi.

  - È necessario determinare il numero di copie del database necessarie a risolvere diversi scenari di errore.

  - È necessario determinare se l'eliminazione dell'uso di un gruppo di disponibilità del database o di alcuni dei suoi membri consenta un risparmio sufficiente a supportare una soluzione di backup tradizionale. In questo caso, è necessario determinare se quella soluzione migliora i contratti di servizio dell'obiettivo temporale di recupero o dell'obiettivo per il punto di recupero.

  - È necessario determinare se ci si possa permettere di perdere una copia temporizzata se nel membro del gruppo di disponibilità del database che ospita la copia si verifica un errore che influenza la copia o l'integrità della copia.

  - Exchange 2013 consente di distribuire cassette postali molto grandi, con una dimensione massima consigliata del database delle cassette postali di 2 terabyte (quando si utilizzano due o più copie di database delle cassette postali altamente disponibili). In base alle cassette postali di dimensioni maggiori che verranno probabilmente distribuite dalla maggior parte delle organizzazioni, è necessario determinare il proprio obietti per il punto di recupero qualora si dovessero riprodurre numerosi file di registro durante l'attivazione di una copia del database o di una copia del database ritardata.

  - È necessario determinare la modalità di rilevamento del danneggiamento della parte logica in una copia attiva del database e il modo per impedire che tale danneggiamento si ripeta nelle copie passive del database. Ciò include la definizione del piano di recupero per questa situazione e della quantità di volte in cui si è verificato questo scenario in passato. Se il danneggiamento della parte logica si verifica di frequente nell'organizzazione, si consiglia di calcolare questo scenario nel progetto utilizzando una o più copie ritardate con una finestra relativa all'intervallo di riesecuzione per consentire all'utente di rilevare e correggere il danneggiamento della parte logica quando si verifica, ma prima che tale danneggiamento viene replicato in altre copie del database.

Una delle funzioni eseguite al termine di un backup incrementale o di un backup completo è il troncamento dei file di registro non più necessari per il ripristino del database. Se i backup non vengono acquisiti, non si verifica il troncamento del registro. Per impedire che i file di registro aumentino, occorre abilitare la registrazione circolare per i database replicati. Quando si unisce la registrazione circolare con la replica continua, si forma un nuovo tipo di registrazione circolare denominata registrazione circolare a replica continua (CRCL), diversa dalla registrazione circolare ESE. Mentre la registrazione circolare ESE viene eseguita e gestita dal servizio Archivio informazioni di Microsoft Exchange, la registrazione circolare a replica continua viene eseguita e gestita dal servizio di replica di Microsoft Exchange. Quando abilitata, la registrazione circolare ESE non genera file di registro aggiuntivi ma, se necessario, sovrascrive il file di registro corrente. Tuttavia, in un ambiente di replica continua, i file di registro sono necessari per la distribuzione e la riproduzione dei registri. Di conseguenza, quando si abilita la registrazione circolare a replica continua, il file di registro corrente non viene sovrascritto e vengono generati file di registro chiusi per il processo di distribuzione e riproduzione dei registri.

In particolare, il servizio di replica di Microsoft Exchange gestisce la registrazione circolare a replica continua in modo da mantenere la continuità dei registri e i registri non vengono eliminati se sono ancora necessari per la replica. Il servizio di replica di Microsoft Exchange e il servizio Archivio informazioni di Microsoft Exchange comunicano utilizzando chiamate di procedura remote (RPC) relative ai quali file di registro possono essere eliminati.

Per eseguire il troncamento su copie di database delle cassette postali altamente disponibili (non ritardate), è necessario che sia vero quanto riportato di seguito:

  - È stato eseguito il backup del file di registro o è abilitata la registrazione circolare a replica continua.

  - Il file di registro è al di sotto del punto di arresto.

  - Le altre copie non ritardate del database accettano l'eliminazione.

  - Il file di registro è stato ispezionato da tutte le copie ritardate del database.

Per eseguire il troncamento su copie di database ritardate, è necessario che sia vero quanto riportato di seguito:

  - Il file di registro è al di sotto del punto di arresto.

  - Il file di registro è precedente a ReplayLagTime + TruncationLagTime.

  - Il file di registro viene eliminato sulla copia attiva del database.

Inizio pagina

## Tecnologie di backup supportate

Exchange 2013 supporta solo backup con un software che riconosca Exchange o basati su VSS. Exchange 2013 include un plug-in per il backup di Windows Server che consente di creare e ripristinare i backup basati su VSS dei dati di Exchange. Per eseguire il backup e il ripristino di Exchange 2013, è necessario utilizzare un'applicazione compatibile con Exchange che supporti VSS Writer per Exchange 2013; ad esempio, Windows Server Backup (con il plug-in VSS), Microsoft System Center 2012 - Data Protection Manager o un'applicazione di terze parti basata su VSS compatibile con Exchange.

Per la procedura dettagliata su come eseguire il backup e il ripristino dei dati di Exchange utilizzando Windows Server Backup, vedere [Utilizzo di Windows Server Backup per eseguire il backup e il recupero dei dati di Exchange](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md).

Inizio pagina

## Exchange 2013 VSS Writer

Exchange 2013 introduce una significativa modifica nell'architettura VSS utilizzata in Exchange 2010 e Exchange 2007. Queste versioni precedenti di Exchange includevano due writer VSS: uno interno al servizio Microsoft Exchange Information Store (store.exe) e uno interno al servizio Microsoft Exchange Replication (msexchangerepl.exe). In Exchange, la funzionalità VSS writer che precedentemente si trovava nel servizio Microsoft Exchange Information Store è stata spostata nel servizio Microsoft Exchange Replication. Il nuovo writer, denominato Microsoft Exchange Writer, viene ora utilizzato nelle applicazioni basate su VSS compatibili con Exchange per eseguire i backup di copie attive e passive del database e per ripristinare le copie del database salvate. Sebbene il nuovo writer venga eseguito nel servizio di replica di Microsoft Exchange, è necessario che sia in esecuzione anche il servizio Archivio informazioni di Exchange per consentire l'esecuzione del writer. Ciò implica che per eseguire un backup o un ripristino dei database di Exchange occorrono entrambi i servizi.

Inizio pagina

## Ripristino di Exchange Server

Quasi tutte le impostazioni di configurazione dei server cassette postali e Accesso client sono memorizzate in Active Directory. Come con le versioni precedenti di Exchange, Exchange 2013 include un parametro di configurazione per il ripristino dei server persi. Questo parametro, */m:RecoverServer*, viene utilizzato per creare nuovamente un server perso utilizzando le impostazioni e le informazioni di configurazione archiviate in Active Directory. Tenere comunque presente che esistono diverse impostazioni che non vengono ripristinate, come le modifiche ai file web.config locali e ad altri file di configurazione. Inoltre, le voci di registro personalizzate non vengono ripristinate. Si consiglia di utilizzare un processo di gestione delle modifiche affidabile per tenere traccia e ricreare tali modifiche.

Per la procedura dettagliata su come eseguire il ripristino di un server perso di Exchange 2013, vedere [Ripristino di un server Exchange](recover-an-exchange-server-exchange-2013-help.md). Per la procedura dettagliata su come ripristinare un server perso membro di un gruppo di disponibilità del database, vedere [Ripristinare un server membro di database availability group](recover-a-database-availability-group-member-server-exchange-2013-help.md).

Inizio pagina

## Ripristino dell'archivio unico dei contatti

Quando si utilizza Microsoft Lync Server 2013 in un ambiente Exchange 2013, le informazioni sui contatti Lync dell'utente vengono memorizzate in una determinata cartella dei contatti nella cassetta postale dell'utente. Questo viene definito archivio unico dei contatti (UCS). Se si ripristina una cassetta postale migrata da UCS, può essere influenzato l'elenco dei contatti di messaggistica istantanea dell'utente di destinazione. Se l'utente è stato migrato dopo l'ultimo backup, il ripristino della cassetta postale può provocare la perdita completa dell'elenco contatti dell'utente. In casi meno gravi, potrebbero essere perse le modifiche apportate all'elenco contatti dopo l'ultimo backup. Per mitigare queste potenziali perdite di dati, assicurarsi che l'utente venga riportato nel server di messaggistica istantanea prima di ripristinare la cassetta postale.

Inizio pagina

## Database di ripristino

Un database di ripristino è un tipo speciale di database delle cassette postali che consente di installare un database delle cassette postali ripristinato e di estrarre i dati dal database ripristinato durante un'operazione di ripristino. È possibile utilizzare il cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829875\(v=exchg.150\)) per estrarre i dati da un database di ripristino. Dopo l'estrazione, i dati possono essere esportati in una cartella o uniti in una cassetta postale esistente. I database di ripristino consentono di ripristinare i dati da un backup o dalla copia di un database senza interferire nell'accesso ai dati correnti dell'utente.

L'uso di un database di ripristino per un database delle cassette postali proveniente da qualsiasi versione precedente di Exchange non è supportato. Inoltre, la cassetta postale di destinazione utilizzata per l'unione e l'estrazione dei dati deve trovarsi nella stessa foresta di Active Directory del database installato nel database di ripristino.

Per ulteriori informazioni, vedere [Database di ripristino](recovery-databases-exchange-2013-help.md). Per la procedura dettagliata su come creare un database di ripristino, vedere [Creare un database di ripristino](create-a-recovery-database-exchange-2013-help.md). Per la procedura dettagliata su come utilizzare un database di ripristino, vedere [Recupero dei dati utilizzando un database di ripristino](restore-data-using-a-recovery-database-exchange-2013-help.md).

Inizio pagina

## Portabilità del database

La portabilità del database è una funzionalità che consente di spostare o installare un database cassette postali di Exchange 2013 su qualsiasi altro server Cassette postali di Exchange 2013 nella stessa organizzazione. Utilizzando la portabilità del database, è possibile migliorare l'affidabilità perché si eliminano dalle procedure di ripristino numerose operazioni manuali facilmente soggette a errore. Inoltre, la portabilità riduce i tempi totali di ripristino a fronte di diversi scenari di errore.

Per ulteriori informazioni, vedere [Portabilità del database](database-portability-exchange-2013-help.md). Per la procedura dettagliata relativa all'utilizzo della portabilità del database, vedere [Spostamento di un database delle cassette postali utilizzando la portabilità del database](move-a-mailbox-database-using-database-portability-exchange-2013-help.md).

Inizio pagina

## Portabilità temporanea

Portabilità temporanea è una funzionalità che fornisce una soluzione di continuità aziendale limitata in caso di errori relativi a un database delle cassette postali, a un server o a un intero sito. La portabilità temporanea consente agli utenti di disporre di una cassetta postale temporanea per l'invio e la ricezione di messaggi di posta elettronica durante il ripristino o la riparazione della cassetta postale originale. La cassetta postale temporanea può trovarsi sullo stesso server Cassette postali Exchange 2013 o su qualsiasi altro server Cassette postali Exchange 2013 nell'organizzazione. Ciò consente a un server alternativo di ospitare le cassette postali di utenti che si trovavano precedentemente su un server non più disponibile. I client che supportano l'individuazione automatica, ad esempio Microsoft Outlook, vengono automaticamente reindirizzati al nuovo server senza dover aggiornare manualmente il profilo desktop dell'utente. Una volta ripristinati i dati della cassetta postale originale dell'utente, un amministratore può unire la cassetta postale ripristinata e la cassetta postale temporanea dell'utente in una singola cassetta postale aggiornata.

Questo processo di utilizzo della portabilità temporanea è definito *ripristino temporaneo*. Un ripristino temporaneo presuppone la creazione di un database vuoto su un server Cassette postali per sostituire il database danneggiato. Il database vuoto, definito *database temporaneo*, consente agli utenti di inviare e ricevere messaggi di posta elettronica durante il ripristino del database danneggiato. Dopo aver ripristinato il database danneggiato, il database temporaneo e il database ripristinato vengono scambiati e i dati del database temporaneo vengono uniti nel database ripristinato.

Per ulteriori informazioni, vedere [Portabilità temporanea](dial-tone-portability-exchange-2013-help.md). Per la procedura dettagliata relativa all'esecuzione di un ripristino temporaneo, vedere [Esecuzione di un ripristino del segnale](perform-a-dial-tone-recovery-exchange-2013-help.md).

Inizio pagina


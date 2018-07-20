---
title: 'Gruppi di disponibilità dei database (DAG): Exchange 2013 Help'
TOCTitle: Gruppi di disponibilità dei database (DAG)
ms:assetid: ab9b88ce-2f44-4334-96ad-a666b95888a0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd979799(v=EXCHG.150)
ms:contentKeyID: 50481407
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gruppi di disponibilità dei database (DAG)

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-06-04_

Informazioni su Exchange DAG in Exchange Server 2013. In questo articolo viene descritto il ciclo di vita relativo al gruppo di disponibilità dei database (DAG) e l'utilizzo di un DAG per offrire disponibilità elevata e resilienza del sito.

Un gruppo di disponibilità del database (DAG, Database Availability Group) è il componente di base del server Cassette postali a disponibilità elevata e resilienza del sito integrata in Microsoft Exchange Server 2013. Un gruppo di disponibilità del database è un gruppo costituito da un massimo di 16 server Cassette postali che ospita un insieme di database e fornisce il ripristino automatico a livello del database da errori che hanno un impatto su singoli server o database.

Un gruppo di disponibilità del database è un confine per la replica del database delle cassette postali, i failover e gli switchover di database e server e un componente interno denominato *Active Manager*. Active Manager, che viene eseguito su tutti i server Cassette postali, gestisce switchover e failover all'interno dei gruppi di disponibilità del database. Per ulteriori informazioni su Active Manager, vedere [Active Manager](active-manager-exchange-2013-help.md).

Qualsiasi server in un gruppo di disponibilità del database è in grado di ospitare una copia del database delle cassette postali da qualsiasi altro server nel gruppo di disponibilità del database. Quando un server viene aggiunto al gruppo di disponibilità del database, funziona con altri server nel gruppo di disponibilità del database per fornire il ripristino automatico da errori che hanno un impatto sui database delle cassette postali, ad esempio un errore di rete, del server o del disco.

**Sommario**

Ciclo di vita del gruppo di disponibilità del database (DAG)

Utilizzo di un gruppo di disponibilità del database (DAG) per offrire disponibilità elevata

Utilizzo di un gruppo di disponibilità del database (DAG) per offrire resilienza del sito

## Ciclo di vita del gruppo di disponibilità del database (DAG)

I gruppi di disponibilità del database sfruttano il concetto di *distribuzione incrementale*, che consiste nella capacità di distribuire la disponibilità di servizi e dati per tutti i server Cassette postali e i database dopo l'installazione di Exchange. Dopo aver distribuito i server Cassette postali di Exchange 2013, è possibile creare un gruppo di disponibilità del database, aggiungere server Cassette postali al gruppo di disponibilità del database e quindi replicare i database delle cassette postali tra i membri del gruppo di disponibilità del database.


> [!NOTE]
> È possibile creare un gruppo di disponibilità del database che contiene una combinazione di server Cassette postali fisici e virtualizzati, purché tali server e la soluzione siano conformi a <A href="exchange-2013-system-requirements-exchange-2013-help.md">Requisiti di sistema di Exchange 2013</A> e ai requisiti specificati in <A href="exchange-2013-virtualization-exchange-2013-help.md">Virtualizzazione di Exchange 2013</A>. Come per tutte le configurazioni di Exchange ad alta disponibilità, è necessario verificare che tutti i server Cassette postali nel gruppo di disponibilità del database abbiano dimensioni appropriate per gestire il carico di lavoro necessario durante le interruzioni del servizio pianificate e non pianificate.



Un gruppo di disponibilità del database viene creato utilizzando il cmdlet [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd351107\(v=exchg.150\)). Un gruppo di disponibilità del database viene inizialmente creato come oggetto vuoto in Active Directory. Questo oggetto directory è utilizzato per archiviare informazioni relative al gruppo di disponibilità del database, come ad esempio le informazioni di appartenenza del server e alcune impostazioni di configurazione del gruppo. Quando si aggiunge il primo server a un DAG, per quel DAG viene creato automaticamente un cluster di failover. Il cluster di failover viene utilizzato esclusivamente dal gruppo di disponibilità del database e il cluster deve essere dedicato al DAG. L'utilizzo del cluster per altri scopi non è supportato.

Oltre alla creazione del cluster di failover, viene anche attivata l'infrastruttura che controlla i server per rilevare eventuali problemi della rete o dei server stessi. Il meccanismo heartbeat di cluster di failover e il database cluster sono poi utilizzati per tracciare e gestire le informazioni sul gruppo di disponibilità del database che possono cambiare rapidamente, come lo stato di installazione del database, lo stato di replica e l'ultimo percorso d'installazione.

Durante il processo di creazione, al gruppo di disponibilità del database viene assegnato un nome univoco e uno o più indirizzi IP statici oppure viene configurato per utilizzare il protocollo DHCP (Dynamic Host Configuration Protocol) o creato senza un punto di accesso amministrativo cluster. I DAG senza un punto di accesso amministrativo possono essere creati solo su server che eseguono Exchange 2013 Service Pack 1 o versione successiva su Windows Server 2012 R2 edizione Standard o Datacenter. I DAG senza punto di accesso amministrativo cluster hanno le seguenti caratteristiche:

  - Non è presente un indirizzo IP assegnato al cluster/DAG e, quindi, nessuna risorsa indirizzo IP nel gruppo risorsa principale del cluster.

  - Non è presente un nome di rete assegnata al cluster e, quindi, nessuna risorsa nome di rete nel gruppo risorsa principale del cluster

  - Il nome del cluster/DAG non è registrato nel DNS e non è risolvibile nella rete.

  - Non viene creato un oggetto di nome cluster (CNO) in Active Directory.

  - Il cluster non può essere gestito utilizzando lo strumento di gestione Cluster di Failover. Deve essere gestito utilizzando Windows PowerShell e i cmdlet PowerShell devono essere eseguiti sui membri del cluster individuale.

In questo esempio viene mostrato come utilizzare Shell per creare un gruppo di disponibilità del database con punto di accesso amministrativo cluster con tre server. Due server (EX1 e EX2) si trovano nella stessa subnet (10.0.0.0) e il terzo server (EX3) si trova in una subnet diversa (192.168.0.0).

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer EX4 -DatabaseAvailabilityGroupIPAddresses 10.0.0.5,192.168.0.5
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX1
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX2
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX3

I comandi per la creazione di un DAG senza un punto di accesso di amministrazione cluster sono molto simili:

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer EX4 -DatabaseAvailabilityGroupIPAddresses ([System.Net.IPAddress])::None
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX1
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX2
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX3

Il cluster per DAG1 viene creato quando EX1 viene aggiunto al gruppo di disponibilità del database. Durante la creazione del cluster, il cmdlet **Add-DatabaseAvailabilityGroupServer** recupera gli indirizzi IP configurati per il gruppo di disponibilità del database e ignora quelli che non corrispondono ad alcuna delle subnet individuate in EX1. Nel precedente esempio, il cluster per DAG1 viene creato con l'indirizzo IP 10.0.0.5 e 192.168.0.5 viene ignorato. Nel secondo esempio, il valore del parametro *DatabaseAvailabilityGroupIPAddresses* istruisce l'attività a creare un cluster di failover per il DAG che non dispone di un punto di accesso amministrativo. Per questo il cluster viene creato con un indirizzo IP o risorsa nome di rete nel gruppo di ricerca cluster principale.

Viene quindi aggiunto EX2 e il cmdlet **Add-DatabaseAvailabilityGroupServer** recupera nuovamente gli indirizzi IP configurati per il gruppo di disponibilità del database. Non viene apportata alcuna modifica agli indirizzi del cluster poiché EX2 si trova nella stessa subnet di EX1.

Viene quindi aggiunto EX3 e il cmdlet **Add-DatabaseAvailabilityGroupServer** recupera nuovamente gli indirizzi IP configurati per il gruppo di disponibilità del database. Poiché è presente una subnet corrispondente a 192.168.0.5 in EX3, l'indirizzo 192.168.0.5 viene aggiunto come risorsa indirizzo IP nel gruppo cluster. Inoltre, viene automaticamente configurata una dipendenza **OR** per la risorsa nome rete per ogni risorsa indirizzo IP. L'indirizzo 192.168.0.5 verrà utilizzato dal cluster quando il gruppo di risorsa cluster principale si sposta in EX3.

Per i DAG con punti di accesso amministrativo cluster, La funzionalità clustering di failover di Windows registra gli indirizzi IP per il cluster in Domain Name System (DNS) quando la risorsa nome rete viene portata online. Inoltre, quando EX1 viene aggiunto al cluster, viene creato un CNO (cluster name object) in Active Directory. Il nome di rete, gli indirizzi IP e il CNO per il cluster non vengono creati per le funzioni DAG. Amministratori e utenti finali non hanno necessità di interfacciarsi o connettersi al nome del gruppo di disponibilità del database/cluster o all'indirizzo IP per alcun motivo. Alcune applicazioni di terze parti si connettono al punto di accesso amministrativo cluster per eseguire attività di gestione, come il backup o monitoraggio. Se non si utilizza nessuna applicazione di terze parti che richiedono un punto di accesso amministrativo cluster e il DAG esegue Exchange 2013 SP1 o versione successiva su Windows Server 2012 R2, si consiglia di creare un DAG senza un punto di accesso amministrativo. Si semplifica così la configurazione DAG, si elimina la necessità per uno o più indirizzi IP e si riduce la superficie di attacco di un DAG.

I DAG vengono inoltre configurati per utilizzare un server e una directory di controllo. Il server e la directory di controllo sono configurati automaticamente dal sistema oppure possono essere configurati manualmente dall'amministratore. Nell'esempio precedente, EX4 (un server che non è e non sarà membro del DAG) viene configurato manualmente come server di controllo del DAG.

Per impostazione predefinita, il gruppo di disponibilità del database è progettato per utilizzare la funzionalità di replica continua incorporata per replicare i database delle cassette postali tra i server del gruppo di disponibilità del database. Se si utilizza un tipo di replica di dati di terza parte che supporta l'API di replica di terza parte in Exchange 2013, è necessario creare il gruppo di disponibilità del database in modalità di replica di terza parte utilizzando il cmdlet [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd351107\(v=exchg.150\)) con il parametro *ThirdPartyReplication*. Non è possibile disabilitare questa modalità, una volta abilitata.

Una volta creato il gruppo di disponibilità del database, è possibile aggiungere server Cassette postali a tale gruppo di disponibilità del database. Quando si aggiunge il primo server al gruppo di disponibilità del database, viene formato un cluster per l'utilizzo da parte del gruppo di disponibilità del database. I gruppi di disponibilità del database utilizzano la tecnologia clustering di failover di Windows, ad esempio heartbeat cluster, reti cluster e database cluster (per l'archiviazione di dati che vengono modificati, quali le modifiche di stato del database da attivo a passivo o viceversa, oppure da montato a smontato e viceversa). Con l'aggiunta di ogni server successivo al gruppo di disponibilità del database, il server viene aggiunto anche al cluster sottostante, il modello di quorum del cluster viene automaticamente regolato da Exchange e il server viene aggiunto all'oggetto gruppo di disponibilità del database in Active Directory.

Dopo l'aggiunta dei server Cassette postali a un gruppo di disponibilità del database, è possibile configurare una vasta gamma di proprietà del gruppo di disponibilità del database, ad esempio è possibile utilizzare o meno la crittografia di rete o la compressione di rete per la replica del database all'interno del DAG. È anche possibile configurare reti di gruppi di disponibilità del database e crearne altre.

Dopo aver aggiunto i membri a un gruppo di disponibilità del database e configurato tale gruppo, è possibile replicare i database delle cassette postali attivi in ogni server negli altri membri del gruppo di disponibilità del database. Dopo aver creato le copie del database delle cassette postali, è possibile monitorare l'integrità e lo stato delle copie utilizzano una vasta gamma di strumenti di monitoraggio incorporati. Inoltre, è possibile eseguire switchover di server e database.

Per ulteriori informazioni sulla creazione di gruppi di disponibilità del database, sulla gestione della loro appartenenza, sulla configurazione delle loro proprietà, su creazione e monitoraggio di copie del database delle cassette postali e sull'esecuzione di switchover, vedere [Gestione di elevata disponibilità e resilienza del sito](managing-high-availability-and-site-resilience-exchange-2013-help.md).

## Modelli di quorum del gruppo di disponibilità del database (DAG)

Alla base di ogni gruppo di disponibilità del database è presente un cluster di failover Windows. I cluster di failover utilizzano il concetto di quorum, che si basa sul consenso dei votanti per assicurare che, in un determinato momento, sia in funzione un solo sottoinsieme dei membri del cluster (che può includere tutti i membri o la maggioranza dei membri). Il quorum non è un concetto nuovo per Exchange 2013. Anche i server Cassette postali a elevata disponibilità nelle precedenti versioni di Exchange utilizzano il clustering di failover e il concetto di quorum. Il quorum rappresenta una vista condivisa di membri e risorse. Il termine quorum viene anche utilizzato per descrivere i dati fisici che rappresentano la configurazione del cluster condivisa da tutti i suoi membri. Di conseguenza, per tutti i gruppi di disponibilità del database è necessario che il cluster di failover sottostante raggiunga il quorum. Se il cluster perde il quorum, tutte le operazioni del gruppo di disponibilità del database vengono interrotte e tutti i database montati ospitati nel gruppo di disponibilità del database vengono smontati. In questo caso, è necessario l'intervento dell'amministratore per risolvere il problema del quorum e ripristinare le operazioni del gruppo di disponibilità del database.

Il quorum è importante per garantire la coerenza, per risolvere eventuali conflitti derivanti dal partizionamento e per garantire la velocità di risposta dei cluster:

  - **Garanzia di coerenza**   Il requisito principale per un cluster di failover Windows è che ogni membro deve disporre sempre di una vista del cluster coerente con gli altri membri. L'hive del cluster viene utilizzato come l'archivio definitivo in cui sono memorizzate tutte le informazioni di configurazione relative al cluster. Se non è possibile caricare localmente l'hive del cluster in un membro del gruppo di disponibilità del database, il servizio Cluster non viene avviato perché non è in grado di garantire che il membro soddisfa il requisito di disporre di una vista del cluster coerente con gli altri membri.

  - **Funzione di tie-breaker**   Nei gruppi di disponibilità del database viene utilizzata una risorsa di controllo del quorum con un numero pari di membri per evitare scenari di sindrome split brain e per garantire che solo una raccolta di membri nel gruppo di disponibilità del database è considerata ufficiale. Quando il server di controllo è necessario per il quorum, i membri del gruppo di disponibilità del database in grado di comunicare con il server di controllo possono impostare un blocco SMB (Server Message Block) sul file di log del server di controllo. Il membro del gruppo di disponibilità del database che blocca il server di controllo (definito *nodo di blocco*) mantiene un voto aggiuntivo ai fini del quorum. I membri del gruppo di disponibilità del database in contatto con il nodo di blocco sono in maggioranza e mantengono il quorum. I membri del gruppo di disponibilità del database in contatto con il nodo di blocco sono in minoranza e perdono il quorum.

  - **Garanzia di capacità di risposta**   Per garantire la velocità di risposta, il modello di quorum assicura che, ogniqualvolta il cluster è in esecuzione, un numero sufficiente di membri del sistema distribuito è operativo e in comunicazione ed è possibile garantire almeno una replica dello stato corrente del cluster. Non è richiesto tempo ulteriore per mettere i membri in comunicazione o per determinare se è garantita una replica specifica.

I gruppi di disponibilità del database con un numero pari di membri utilizzano la modalità quorum Maggioranza dei nodi e delle condivisioni file del cluster di failover, che impiega un server di controllo esterno che funge da tie-breaker. In questa modalità di quorum, ogni membro del gruppo di disponibilità del database ottiene un voto. Viene inoltre utilizzato il server di controllo per attribuire un voto pesato a un membro del gruppo di disponibilità del database (ad esempio, ottiene due voti anziché uno). Per impostazione predefinita, i dati relativi al quorum del cluster vengono archiviati nel disco di sistema di ogni membro del gruppo di disponibilità del database e ne viene garantita la coerenza tra tutti i dischi. Non viene tuttavia archiviata alcuna copia dei dati del quorum sul server di controllo. Nel server di controllo è presente un file che tiene traccia del membro con la copia più aggiornata dei dati, ma in tale server non è presente alcuna copia dei dati del quorum del cluster. In questo modo, la maggioranza dei voter (i membri del gruppo di disponibilità del database più il server di controllo) deve essere operativa e in grado di comunicare reciprocamente per mantenere il quorum. Se la maggior parte dei votanti non è in grado di comunicare con gli altri, il cluster sottostante del gruppo di disponibilità del database perde il quorum e sarà necessario un intervento amministrativo per ripristinare il funzionamento del gruppo di disponibilità del database.

I gruppi di disponibilità del database con un numero dispari di membri utilizzano la modalità quorum Maggioranza dei nodi del cluster di failover. In questa modalità, ogni membro ottiene un voto e il disco di sistema locale di ciascun membro viene utilizzato per archiviare i dati del quorum del cluster. Se la configurazione del gruppo di disponibilità del database viene modificata, le modifiche si rifletteranno su tutti i diversi dischi. La modifica viene considerata vincolante e permanente solo se viene apportata ai dischi della metà dei membri (con arrotondamento per difetto) più uno. Ad esempio, in un gruppo di disponibilità del database con cinque membri, la modifica deve essere apportata a due membri più uno o a un totale di tre membri.

Il quorum richiede che la maggioranza dei voter sia in grado di comunicare reciprocamente. Si consideri un gruppo di disponibilità del database con quattro membri. Poiché il gruppo di disponibilità del database include un numero pari di membri, viene utilizzato un server di controllo esterno per fornire a uno dei membri del cluster un quinto voto che consenta di risolvere i conflitti. Per mantenere una maggioranza di voter (e quindi il quorum), almeno tre voter devono essere in grado di comunicare reciprocamente. In qualsiasi momento, un numero massimo di due voter può trovarsi offline senza interrompere il servizio e l'accesso ai dati. Se tre o più voter sono offline, il gruppo di disponibilità del database perde il quorum e il servizo e l'accesso ai dati verranno interrotti fino alla risoluzione del problema.

Inizio pagina

## Utilizzo di un gruppo di disponibilità del database (DAG) per offrire disponibilità elevata

Per illustrare come un gruppo di disponibilità del database può fornire disponibilità elevata per i database delle cassette postali, considerare l'esempio seguente, in cui viene utilizzato un gruppo di disponibilità del database con cinque membri. Questo gruppo di disponibilità del database è illustrato nella figura seguente.

**Gruppo di disponibilità del database con cinque membri**

![Gruppo di disponibilità del database (DAG, Database Availability Group)](images/Dd979799.21fcbf7b-cb10-49c0-8e32-bdf3c03f825d(EXCHG.150).gif "Gruppo di disponibilità del database (DAG, Database Availability Group)")

Nella figura precedente, i database verdi sono copie del database delle cassette postali attive e i database blu sono copie del database delle cassette postali passive. In questo esempio, non viene eseguito il mirroring delle copie tra ogni server, le copie vengono viceversa ripartite tra più server. In questo modo si assicura che non vi siano due server nel gruppo di disponibilità del database con lo stesso insieme di copie del database e ciò fornisce al gruppo di disponibilità del database maggiore resilienza agli errori, inclusi gli errori che si verificano mentre altri componenti non sono disponibili a causa della normale manutenzione.

Considerare lo scenario seguente, utilizzando il gruppo di disponibilità del database dell'esempio precedente che illustra la resilienza a più errori di database e server.

Inizialmente, tutti i database e i server sono integri. È necessario installare alcuni aggiornamenti del sistema operativo su EX2, quindi il server deve essere portato nella modalità manutenzione. Questo provoca uno switchover del server mediante il quale viene attivata la copia di DB4 su un altro server Cassette postali. Lo switchover del server consente di spostare tutte le copie attive del database delle cassette postali dal server corrente in uso a uno più server Cassette postali nel gruppo di disponibilità del database, in previsione di un'interruzione pianificata del server corrente. In questo esempio, è presente un solo database delle cassette postali attivo in EX2 (DB4), pertanto viene spostata una sola copia del database delle cassette postali attiva.

**Gruppo di disponibilità del database con un server offline per manutenzione**

![Gruppo di disponibilità del database con server offline](images/Dd979799.f48f0e77-80e1-4f14-8c36-112393895bdc(EXCHG.150).gif "Gruppo di disponibilità del database con server offline")

Mentre viene eseguita la manutenzione su EX2, si verifica un errore hardware irreversibile in EX3 che si disconnette. Prima di disconnettersi, EX3 ospitava la copia attiva di DB2. Per ripristinare il sistema dall'errore, viene automaticamente attivata la copia di DB2 ospitata in EX1 entro 30 secondi. come illustrato nella figura seguente.

**Gruppo di disponibilità del database con un server offline per manutenzione e un server in errore**

![DAG con un server offline e con un server in errore](images/Dd979799.9bbfd9e7-3881-4957-ae8d-32318cbc208b(EXCHG.150).gif "DAG con un server offline e con un server in errore")

Dopo aver completato la manutenzione pianificata per EX2, il server viene riportato online ed esce dalla modalità manutenzione. Non appena EX2 è disponibile, gli altri membri del gruppo di disponibilità del database ne ricevono notifica e le copie di DB1, DB4 e DB5 ospitate su EX2 vengono automaticamente sincronizzate con la copia attiva di ogni database. come illustrato nella figura seguente.

**Gruppo di disponibilità del database con un server ripristinato che sincronizza le copie del database**

![DAG durante la risincronizzazione dei database in un server ripristinato](images/Dd979799.58601531-e078-41d3-9287-e8e470ef7f41(EXCHG.150).gif "DAG durante la risincronizzazione dei database in un server ripristinato")

Dopo che il componente hardware che ha causato l'errore in EX3 è stato sostituito, EX3 viene riportato online. Quando EX3 è di nuovo disponibile, gli altri membri del gruppo di disponibilità del database ne ricevono notifica e le copie di DB2, DB3 e DB4 ospitate su EX3 vengono automaticamente sincronizzate con la copia attiva di ogni database. come illustrato nella figura seguente.

**Gruppo di disponibilità del database con un server ripristinato che sincronizza le copie del database**

![DAG con membro durante la risincronizzazione delle copie del database](images/Dd979799.56259671-e840-4cf0-9ea2-3657dc36c035(EXCHG.150).gif "DAG con membro durante la risincronizzazione delle copie del database")

Inizio pagina

## Utilizzo di un gruppo di disponibilità del database (DAG) per offrire resilienza del sito

Oltre a fornire disponibilità elevata in un datacenter, un gruppo di disponibilità del database può essere esteso a uno o più altri datacenter in una configurazione che fornisce resilienza del sito per uno o più datacenter. Nelle figure dell'esempio precedente, il gruppo di disponibilità del database si trova in un unico datacenter e in un unico sito Active Directory. È possibile utilizzare la distribuzione incrementale per estendere questo gruppo di disponibilità del database a un secondo data center (e a un secondo sito di Active Directory) distribuendo un server Cassette postali e le risorse di supporto necessarie (uno o più server di Active Directory e i servizi DNS). Il server Cassette postali viene quindi aggiunto al gruppo di disponibilità del database, come illustrato nella figura seguente.

**Gruppo di disponibilità del database esteso tra due siti di Active Directory**

![DAG esteso tra due siti di Active Directory](images/Dd979799.28e96e9d-d7d6-451a-b7b8-c06122c81dc9(EXCHG.150).gif "DAG esteso tra due siti di Active Directory")

In questo esempio, una copia passiva di ogni database attivo nel datacenter di Redmond è configurata in EX6 nel datacenter di Dublino. Esistono tuttavia molti altri esempi di configurazioni del gruppo di disponibilità del database che forniscono resilenza del sito. Ad esempio:

  - Anziché ospitare solo le copie passive del database, EX6 potrebbe ospitare tutte le copie attive o un insieme di copie attive e passive.

  - Oltre a EX6, nel datacenter di Dublino potrebbero essere distribuiti più gruppi di disponibilità del database, offrendo protezione da ulteriori errori. Questo tipo di configurazione è anche in grado di fornire ulteriori capacità, in modo tale che, se si verifica un errore nel datacenter di Redmond, il datacenter di Dublino è in grado di supportare un numero di utenti molto più grande.

## Utilizzo di più gruppi di disponibilità del database (DAG) per offrire resilienza del sito

Nell'esempio precedente, un singolo gruppo di disponibilità del database si estende su più datacenter, fornendo resilienza del sito per uno o entrambi i datacenter. Quando si utilizza un singolo gruppo di disponibilità del database per fornire resilienza del sito in un ambiente in cui ogni datacenter a cui viene esteso il gruppo di disponibliità del database ha un gran numero di utenti attivi, esiste un singolo punto di errore nella connessione WAN (Wide Area Network). Ciò avviene perché il quorum richiede che la maggioranza dei voter sia attiva e in grado di comunicare reciprocamente.

Nell'esempio precedente, la maggioranza dei voter si trova nel datacenter di Redmond. Se il datacenter di Dublino ospita database attivi delle cassette postali e dispone di un gruppo di utenti locale, un'interruzione della connessione WAN determinerebbe un'interruzione del servizio di messaggistica per gli utenti di Dublino. Quando si verifica un'interruzione della connettività WAN, solo i membri del gruppo di disponibilità del database del datacenter di Redmond mantengono il quorum e continuano a fornire il servizio di messaggistica.

Per eliminare la rete WAN come singolo punto di errore quando è necessario fornire resilienza del sito per più datacenter che dispongono ciascuno di un gruppo di utenti attivo, è consigliabile distribuire più gruppi di disponibilità del database, in cui ogni DAG dispone della maggioranza dei voter in un datacenter separato. Quando si verifica un'interuzione della connettività WAN, la replica verrà bloccata fino al ripristino della connettività. Gli utenti potranno utilizzare il servizio di messaggistica, dal momento che ogni gruppo di disponibilità del database continua a servire il proprio gruppo di utenti locale.

Inizio pagina


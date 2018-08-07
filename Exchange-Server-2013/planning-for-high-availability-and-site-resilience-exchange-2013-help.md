---
title: 'Pianifica disponibilità elevata e resilienza del sito: Exchange 2013 Help'
TOCTitle: Pianificazione della disponibilità elevata e della resilienza del sito
ms:assetid: 29bb0358-fc8e-4437-8feb-d2959ed0f102
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638104(v=EXCHG.150)
ms:contentKeyID: 50480229
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pianificazione della disponibilità elevata e della resilienza del sito

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Durante la fase di pianificazione, gli architetti e gli amministratori di sistema, nonché le altre figure professionali coinvolte, devono identificare i requisiti aziendali e architetturali per la distribuzione e in particolare i requisiti di elevata disponibilità e resilienza del sito.

Per la distribuzione di queste funzionalità, devono essere soddisfatti sia i requisiti generali sia requisiti specifici relativi all'hardware, al software, alla rete.

**Sommario**

General requirements

Hardware requirements

Storage requirements

Software requirements

Network requirements

Witness server requirements

Planning for site resilience

## Requisiti generali

Prima di distribuire un gruppo di disponibilità del database e creare le copie dei database delle cassette postali, verificare che tutti i requisiti del sistema siano soddisfatti:

  - Domain Name System (DNS) deve essere in esecuzione. Il server DNS dovrebbe accettare gli aggiornamenti dinamici. Se il server DNS non accetta gli aggiornamenti automatici, occorre creare un record dell'host DNS (A) per ciascun server Exchange. In caso contrario, Exchange non funzionerà correttamente.

  - Ciascun server per cassette postali in un DAG deve essere un membro dello stesso dominio.

  - L'aggiunta di un server Cassette postali di Exchange 2013 che sia anche un server di directory in un gruppo di disponibilità del database non è supportata.

  - Il nome assegnato al gruppo di disponibilità del database deve essere un nome di computer valido, disponibile e univoco di massimo 15 caratteri.

Inizio pagina

## Requisiti hardware

In genere, non esistono requisiti hardware specifici per i gruppi di disponibilità del database o le copie dei database delle cassette postali. I server utilizzati devono soddisfare i requisiti definiti negli argomenti [Prerequisiti di Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md) e [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

Inizio pagina

## Requisiti di archiviazione

In genere, non esistono requisiti di archiviazione specifici per i gruppi di disponibilità del database o le copie dei database delle cassette postali. I gruppi DAG non richiedono o non utilizzano l'archiviazione condivisa gestita dal cluster. L'archiviazione condivisa gestita dal cluster è supportata per l'utilizzo in un gruppo DAG solo quando il gruppo è configurato per l'utilizzo di una soluzione che sfrutta il servizio API per la replica di terze parti incorporato in Exchange 2013.

Inizio pagina

## Requisiti software

I gruppi di disponibilità del database sono disponibili in Exchange 2013 Standard ed Exchange 2013 Enterprise. Inoltre, un gruppo di disponibilità del database può contenere un combinazione di server Exchange 2013 Standard e di server Exchange 2013 Enterprise.

Su ciascun membro del DAG deve anche essere in esecuzione lo stesso sistema operativo. Exchange 2013 è supportato sui sistemi operativi Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2. Tutti i membri di un determinato gruppo di disponibilità del database devono utilizzare lo stesso sistema operativo. Windows Server 2012 R2 è supportato soltanto per i membri DAG che eseguono Exchange 2013 Service Pack 1 o successivo.

Oltre ai requisiti per l'installazione di Exchange 2013, è necessario soddisfare anche i requisiti relativi al sistema operativo. I DAG utilizzando la la tecnologia Clustering di failover di Windows e, di conseguenza, richiedono la versione Enterprise o Datacenter di Windows Server 2008 R2 oppure la versione Standard o Datacenter dei sistemi operativi Windows Server 2012 o Windows Server 2012 R2.

Inizio pagina

## Requisiti di rete

Esistono specifici requisiti di rete che vanno soddisfatti per ciascun DAG e per ciascun membro di un DAG. Ciascun gruppo di disponibilità del database deve avere una singola *rete MAPI* che viene utilizzata da un membro del gruppo per comunicare con altri server (ad esempio, altri server Exchange 2013 o server di directory) e zero o più *reti di replica*, cioè reti dedicate al seeding e all'invio dei registri.

Nelle versioni precedenti di Exchange, si consiglia di almeno due reti (una rete MAPI e una rete di replica) per i DAG. In Exchange 2013, sono supportate più reti, ma il nostro Consiglio dipende dalla topologia di rete fisica. Se si dispone di più reti fisiche tra i membri del DAG fisicamente distinti rispetto a altro, quindi utilizza una rete MAPI e la replica separata fornisce ridondanza aggiuntiva. Se si dispone di più reti in cui sono parzialmente fisicamente distinti ma convergono in un'unica rete fisica (ad esempio, un singolo collegamento WAN), è consigliabile utilizzare quindi un'unica rete (preferibilmente 10 gigabit Ethernet) per il traffico di replica e MAPI. In tal modo semplicità per la rete e il percorso di rete.

Quando si progetta l'infrastruttura di rete per il DAG, considerare quanto segue:

  - Ogni membro del DAG deve avere almeno una scheda di rete che è in grado di comunicare con tutti gli altri membri del DAG. Se si utilizza un singolo percorso di rete, è consigliabile utilizzare almeno 1 gigabit Ethernet, ma è preferibile 10 gigabit Ethernet. Inoltre, quando si utilizza una singola scheda di rete in ciascun membro del DAG, si consiglia di progettazione della soluzione complessiva con la singola scheda di rete e il percorso presente.

  - L'utilizzo di due schede di rete in ciascun membro del DAG consente di avere una rete MAPI e una rete di replica, con la ridondanza per la rete di replica e le procedure di recupero indicate di seguito:
    
      - Nel caso di un errore della rete MAPI, si verifica il failover di un server (presupponendo che esistano delle copie integre dei database delle cassette postali che possono essere attivate).
    
      - In caso di errore della rete di replica, se la rete MAPI non è interessata dal problema per le operazioni di seeding e riproduzione dei registri verrà utilizzata la rete MAPI, anche se la relativa proprietà *ReplicationEnabled* è impostata su False. Quando la rete di replica è nuovamente in funzione e pronta per riprendere le operazioni di log shipping e seeding, è necessario passare manualmente alla rete di replica. Per passare da una rete MAPI a una rete di replica ripristinata, è necessario sospendere e riprendere la replica continua utilizzando i cmdlet **Suspend-MailboxDatabaseCopy** e **Resume-MailboxDatabaseCopy** o riavviare il servizio di replica di Microsoft Exchange. È consigliabile eseguire le operazioni di sospensione e ripresa per evitare la breve interruzione del servizio provocata dal riavvio del servizio di replica di Microsoft Exchange.

  - Ciascun membro del DAG deve avere lo stesso numero di reti. Ad esempio, se si pianifica l'utilizzo di una singola scheda di rete per un membro del gruppo di disponibilità del database, anche tutti gli altri membri del gruppo dovranno utilizzare una singola scheda di rete.

  - Ciascun DAG deve avere una sola rete MAPI. La rete MAPI deve fornire la connessione ad altri server Exchange e ad altri servizi, come Active Directory e DNS.

  - È possibile aggiungere ulteriori reti di replica, secondo necessità. È possibile evitare che una singola scheda di rete costituisca un singolo punto di errore utilizzando la tecnologia del teaming della scheda di rete o altra tecnologia simile. Tuttavia, anche utilizzando il gruppo, non si può impedire che la rete stessa costituisca un singolo punto di errore. Inoltre, il teaming complica inutilmente il DAG.

  - Ciascuna rete in ciascun server di un membro del DAG deve trovarsi sulla propria subnet. Ciascun server del DAG può trovarsi su una subnet differente, ma le reti MAPI e di replica devono essere instradabile e garantire la connessione, in modo tale che:
    
      - Ciascuna rete di ciascun server di un membro del DAG si trovi su una propria subnet che è diversa da quella utilizzata da ogni altra rete del server.
    
      - Ciascuna rete MAPI del server di un membro del DAG possa comunicare con la rete MAPI di ogni altro membro del DAG.
    
      - Ciascuna rete di replica del server di un membro del DAG possa comunicare con la rete di replica di ogni altro membro del DAG.
    
      - Non esiste un routing diretto che consenta il traffico heartbeat dalla rete di replica sul server di un membro del DAG alla rete MAPI sul server di un altro membro del DAG o viceversa oppure tra più reti di replica nell'ambito del DAG.

  - Indipendentemente dalla posizione geografica rispetto agli altri membri del gruppo di disponibilità del database, ciascun membro del gruppo deve avere una latenza di rete (tempo di andata e ritorno) inter-membro non superiore a 500 millisecondi (ms). Se aumenta la latenza di andata e ritorno tra due server Cassette postali che ospitano copie di database, aumenta anche il potenziale rischio che le repliche non siano aggiornate. Indipendentemente dalla latenza della soluzione, i clienti dovrebbero convalidare che la rete fra ciascun membro del gruppo di disponibilità del database è in grado di soddisfare gli obiettivi di sicurezza e disponibilità della distribuzione. Per raggiungere i requisiti desiderati, configurazioni con alti valori di latenza potrebbero richiedere una particolare regolazione del gruppo di disponibilità del database, della replica e dei parametri di rete, quali l'aumento del numero dei database o la riduzione del numero di cassette postali per database.

  - I requisiti della latenza di andata e ritorno potrebbero non essere i requisiti di larghezza di banda e latenza più rigidi per una configurazione multi-datacenter. Per determinare i requisiti di rete richiesti dall'ambiente è necessario valutare il carico complessivo della rete che include l'accesso dei client, Active Directory, i servizi di trasporto e di replica continua, nonché il traffico dovuto alle applicazioni.

  - Le reti del gruppo di disponibilità del database supportano Internet Protocol versione 4 (IPv4) e IPv6. IPv6 è supportato solo quando si utilizza anche IPv4; un ambiente IPv6 puro non è supportato. L'utilizzo degli indirizzi IPv6 e degli intervalli di indirizzi IP è supportato solo quando sul computer sono abilitati sia IPv6 che IPv4 e la rete supporta entrambe le versioni degli indirizzi IP. Se Exchange 2013 viene distribuito in questa configurazione, tutti i ruoli server potranno inviare e ricevere dati da dispositivi, server e client che utilizzano indirizzi IPv6.

  - Automatic Private IP Addressing (APIPA) è una funzionalità di Windows che assegna automaticamente gli indirizzi IP quando sulla rete non è disponibile alcun server DHCP (Dynamic Host Configuration Protocol). Gli indirizzi APIPA (inclusi gli indirizzi assegnati manualmente dall'intervallo di indirizzi APIPA) non sono supportati per i DAG o per Exchange 2013.

## Requisiti per indirizzi IP e nomi dei gruppi di disponibilità del database

Durante il processo di creazione, a ciascun DAG viene assegnato un nome univoco e uno o più indirizzi IP fissi oppure il DAG viene configurato per utilizzare il protocollo DHCP. Indipendentemente dall'utilizzo di indirizzi assegnati in modo statico o dinamico, ogni indirizzo IP assegnato al gruppo di disponibilità del database deve essere presente sulla rete MAPI.

Tutti i DAG in esecuzione su Windows Server 2008 R2 o Windows Server 2012 necessitano di almeno un indirizzo IP nella rete MAPI. Un DAG richiede degli indirizzi IP aggiuntivi quando la rete MAPI si estende su più subnet. I DAG eseguiti in Windows Server 2012 R2 creati senza un punto di accesso amministrativo del cluster non richiedono un indirizzo IP.

La figura che segue illustra un DAG in cui tutti i nodi hanno la rete MAPI sulla stessa subnet.

**Gruppo di disponibilità del database con rete MAPI sulla stessa subnet**

![DAG in una singola subnet](images/Dd638104.bcb7ef68-6d18-4516-a736-b936991c82cb(EXCHG.150).gif "DAG in una singola subnet")

In questo esempio, la rete MAPI di ciascun membro del DAG si trova sulla subnet 172.19.18.*x*. Di conseguenza, il DAG richiede un singolo indirizzo IP su quella subnet.

Nelle figura successiva, viene illustrato un gruppo di disponibilità del database con una rete MAPI che si estende su due subnet: 172.19.18.*x* e 172.19.19.*x*.

**Gruppo di disponibilità del database con rete MAPI su più subnet**

![DAG esteso tra più subnet](images/Dd638104.ffb57c64-3cb1-435c-8148-1b7154d1575c(EXCHG.150).gif "DAG esteso tra più subnet")

In questo esempio, la rete MAPI di ciascun membro del DAG si trova su una subnet separata. Di conseguenza, il DAG richiede due indirizzi IP, uno per ciascuna subnet sulla rete MAPI.

Ogni volta che la rete MAPI del DAG si estende su una subnet aggiuntiva, occorre configurare un ulteriore indirizzo IP per quella subnet. Ogni indirizzo IP configurato per il DAG viene assegnato e utilizzato dal cluster di failover che è il livello di base del DAG. Il nome del DAG viene utilizzato anche per il cluster di failover del DAG stesso.

In ogni specifico momento, il cluster del DAG utilizza uno solo degli indirizzi IP assegnati. La funzionalità clustering di failover di Windows registra questo indirizzo IP nel DNS quando le risorse Indirizzo IP e Nome di rete del cluster vengono richiamate online. Oltre all'indirizzo IP e al nome di rete, viene creato anche un oggetto nome cluster (o CNO) in Active Directory. Il nome, l'indirizzo IP e il CNO del cluster vengono utilizzati internamente dal sistema per proteggere il gruppo di disponibilità del database e per le comunicazioni interne. Amministratori e utenti finali non hanno bisogno di interfacciarsi o connettersi al nome del gruppo di disponibilità del database o all'indirizzo IP.


> [!NOTE]
> Sebbene l'indirizzo IP e il nome di rete del DAG siano utilizzati internamente dal sistema, non è assolutamente indispensabile per Exchange 2013&nbsp;che queste risorse siano disponibili. Anche nel caso in cui il punto di accesso del cluster sia offline, è ancora possibile comunicare internamente con il gruppo di disponibilità del database utilizzando i nomi server dei membri del gruppo di disponibilità del database. Tuttavia, si consiglia di monitorare periodicamente la disponibilità di queste risorse per verificare che non siano rimaste offline per più di trenta giorni. Se il cluster alla base del DAG rimane offline per oltre 30 giorni, l'account CNO del cluster potrebbe essere invalidato dal meccanismo di garbage collection in Active Directory.



## Configurazione della scheda di rete per i gruppi di disponibilità del database

Ogni scheda di rete deve essere configurato correttamente in base al relativo utilizzo previsto. Una scheda di rete utilizzato per una rete MAPI è configurata in modo diverso da una scheda di rete utilizzato per una rete di replica. Oltre a configurare correttamente ogni scheda di rete, è necessario configurare anche l'ordine della connessione di rete in Windows in modo che la rete MAPI sia nella parte superiore dell'ordine di connessione. Per ulteriori informazioni su come modificare l'ordine delle connessioni di rete, vedere [modificare il binding dei protocolli e l'ordine dei provider di rete](https://go.microsoft.com/fwlink/p/?linkid=179138).

## Configurazione della scheda di rete MAPI

Una scheda di rete da utilizzare per una rete MAPI deve essere configurata come descritto nella tabella che segue.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità di rete</th>
<th>Impostazioni</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client per reti Microsoft</p></td>
<td><p>Abilitato</p></td>
</tr>
<tr class="even">
<td><p>Utilità di pianificazione pacchetti QoS</p></td>
<td><p>Facoltativamente abilitato</p></td>
</tr>
<tr class="odd">
<td><p>Condivisione file e stampanti per reti Microsoft</p></td>
<td><p>Abilitato</p></td>
</tr>
<tr class="even">
<td><p>Internet Protocol versione 6 (TCP/IP v6)</p></td>
<td><p>Abilitato</p></td>
</tr>
<tr class="odd">
<td><p>Internet Protocol versione 4 (TCP/IP v4)</p></td>
<td><p>Abilitato</p></td>
</tr>
<tr class="even">
<td><p>Driver I/O mapper di individuazione topologia livelli di collegamento</p></td>
<td><p>Abilitato</p></td>
</tr>
<tr class="odd">
<td><p>Risponditore individuazione topologia livelli di collegamento</p></td>
<td><p>Abilitato</p></td>
</tr>
</tbody>
</table>


Le proprietà del TCP/IP v4 per una scheda di rete MAPI devono essere configurate come segue:

  - L'indirizzo IP della rete MAPI di un membro del gruppo di disponibilità del database può essere assegnato manualmente o configurato per l'utilizzo del protocollo DHCP. Se si utilizza il protocollo DHCP, si consiglia di utilizzare prenotazioni permanenti per l'indirizzo IP del server.

  - La rete MAPI utilizza in genere un gateway predefinito, anche se non è obbligatorio averne uno.

  - È necessario configurare almeno un indirizzo di server DNS. Si consiglia di utilizzare più server DNS per garantire la ridondanza.

  - La casella di controllo **Registra gli indirizzi della connessione in DNS** deve essere selezionata.

## Configurazione della scheda di rete di replica

Una scheda di rete da utilizzare per una rete di replica deve essere configurata come descritto nella tabella che segue.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità di rete</th>
<th>Impostazioni</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client per reti Microsoft</p></td>
<td><p>Disabilitato</p></td>
</tr>
<tr class="even">
<td><p>Utilità di pianificazione pacchetti QoS</p></td>
<td><p>Facoltativamente abilitato</p></td>
</tr>
<tr class="odd">
<td><p>Condivisione file e stampanti per reti Microsoft</p></td>
<td><p>Disabilitato</p></td>
</tr>
<tr class="even">
<td><p>Internet Protocol versione 6 (TCP/IP v6)</p></td>
<td><p>Abilitato</p></td>
</tr>
<tr class="odd">
<td><p>Internet Protocol versione 4 (TCP/IP v4)</p></td>
<td><p>Abilitato</p></td>
</tr>
<tr class="even">
<td><p>Driver I/O mapper di individuazione topologia livelli di collegamento</p></td>
<td><p>Abilitato</p></td>
</tr>
<tr class="odd">
<td><p>Risponditore individuazione topologia livelli di collegamento</p></td>
<td><p>Abilitato</p></td>
</tr>
</tbody>
</table>


Le proprietà del TCP/IP v4 per una scheda di rete di replica devono essere configurate come segue:

  - L'indirizzo IP della rete di replica di un membro del gruppo di disponibilità del database può essere assegnato manualmente o configurato per l'utilizzo del protocollo DHCP. Se si utilizza il protocollo DHCP, si consiglia di utilizzare prenotazioni permanenti per l'indirizzo IP del server.

  - Le reti di replica in genere non utilizzano gateway e, se la rete MAPI ha un gateway predefinito, nessun'altra rete deve avere gateway predefiniti. Il routing del traffico di rete su una rete di replica può essere configurato tramite route statiche permanenti che portano alla rete corrispondente su altri membri del DAG che utilizzano indirizzi gateway in grado di effettuare il routing tra le rete di replica. Tutto il traffico esterno a questa route verrà gestito dal gateway predefinito configurato sulla scheda della rete MAPI.

  - Gli indirizzi del server DNS non devono essere configurati.

  - La casella di controllo **Registra gli indirizzi della connessione in DNS** non deve essere selezionata.

Inizio pagina

## Requisiti per il server di controllo

Un *server di controllo* è un server che si trova all'esterno di un gruppo di disponibilità del database e che viene utilizzato per ottenere e mantenere il quorum quando il gruppo di disponibilità del database dispone di un numero pari di membri. I gruppi di disponibilità del database con un numero dispari di membri non utilizzano un server di controllo. Tutti i gruppi di disponibilità del database con un numero pari di membri devono utilizzare un server di controllo. Il server di controllo può essere qualsiasi computer con Windows Server. Non è necessario che la versione del sistema operativo Windows Server del server di controllo sia uguale a quella utilizzata dai membri del gruppo di disponibilità del database.

Il quorum viene mantenuto a livello di cluster, che è il livello di base del DAG. Un DAG ha il quorum quando la maggioranza dei suoi membri è online e può comunicare con gli altri membri online del DAG. Questa nozione di quorum è uno degli aspetti del concetto di quorum così come è inteso nel clustering di failover di Windows. Un aspetto correlato e necessario del quorum nei cluster di failover è la *risorsa quorum*. La risorsa quorum è una risorsa interna del cluster di failover che fornisce la funzionalità di arbitrato necessaria per le decisioni inerenti lo stato del cluster e il riconoscimento dell'appartenenza al cluster. La risorsa quorum fornisce inoltre un archivio permanente dove è possibile memorizzare le informazioni di configurazione. Alla risorsa quorum è abbinato il *registro quorum*, un database di configurazione per il cluster. che contiene informazioni quali l'elenco dei server che appartengono al cluster, l'elenco delle risorse installate nel cluster e lo stato di tali risorse (ad esempio, se sono online o meno).

È fondamentale che ogni membro del gruppo di disponibilità del database abbia un'idea chiara di come è configurato il cluster alla base del gruppo. Il quorum viene utilizzato come l'archivio in cui sono memorizzate tutte le informazioni di configurazione relative al cluster. Per evitare la sindrome *split-brain*, il quorum viene utilizzato anche per risolvere eventuali conflitti. La sindrome split brain si verifica quando i membri del gruppo di disponibilità del database non riescono a comunicare tra loro. È possibile evitare questa sindrome e mantenere il DAG operativo, facendo in modo che la maggioranza dei membri del DAG (e, nel caso dei DAG con un numero dispari di membri, il server di controllo) sia sempre disponibile e in grado di interagire.

Inizio pagina

## Pianificazione della resilienza del sito

Ogni giorno, un numero sempre crescente di aziende si rende conto di quanto l'accesso a un sistema di messaggistica affidabile e disponibile sia fondamentale per il proprio successo. Per molte organizzazioni, il sistema di messaggistica è parte integrante dei loro piani di continuità aziendale e la loro distribuzione del servizio di messaggistica viene progettata in un'ottica di resilienza del sito. Fondamentalmente, molte soluzioni con resilienza del sito prevedono la distribuzione dell'hardware in un secondo datacenter.

In ultima analisi, la struttura globale di un DAG, incluso il numero di membri del DAG e il numero di copie dei database delle cassette postali, dipende, per ciascuna organizzazione, dal contratto di servizio di recupero che copre le varie problematiche. In fase di pianificazione, gli architetti e amministratori della soluzione identificano i requisiti della distribuzione e in particolare i requisiti di resilienza del sito. Essi identificano i percorsi da utilizzare e gli opportuni obiettivi da definire nel contratto di servizio di recupero. Il contratto di servizio identifica due elementi specifici che devono costituire la base della progettazione di una soluzione in grado di garantire elevata disponibilità e resilienza del sito: l'obiettivo temporale di recupero e l'obiettivo per il punto di recupero. Entrambi questi valori sono misurati in minuti. L'obiettivo temporale di recupero corrisponde al periodo di tempo richiesto per il ripristino del servizio. L'obiettivo temporale di recupero fa riferimento al livello di aggiornamento in cui si troveranno i dati al termine dell'operazione di recupero. Un contratto di servizio può anche prevedere il pieno ripristino dell'operatività del datacenter principale dopo che tutti i suoi problemi sono stati risolti.

Gli architetti e amministratori della soluzione determinano altresì quali gruppi di utenti hanno bisogno della protezione da resilienza del sito e se la soluzione multi-sito avrà la configurazione attiva/passiva o attiva/attiva. Nella configurazione attiva/passiva, nessun utente utilizza di norma il datacenter di standby. Nella configurazione attiva/attiva, gli utenti utilizzano entrambi i datacenter e una parte dei database della soluzione ha un percorso attivo preferenziale in un secondo datacenter. Quando il servizio per gli utenti di un datacenter s'interrompe a causa di un problema, quegli stessi utenti vengono attivati nell'altro datacenter.

La creazione di contratti di servizio appropriati spesso richiede una risposta alle seguenti domande:

  - Qual è il livello di servizio richiesto dopo che si verifica un errore del datacenter principale?

  - Gli utenti necessitano dei propri dati o solo di servizi di messaggistica?

  - Con quale velocità sono richiesti i dati?

  - Quanti utenti è necessario supportare?

  - In quale modo gli utenti potranno accedere ai propri dati?

  - Che cos'è il contratto di servizio per l'attivazione del datacenter di standby?

  - In che modo il servizio viene trasferito di nuovo al datacenter principale?

  - Le risorse sono dedicate alla soluzione con resilienza del sito?

Rispondendo a queste domande è possibile iniziare a dare forma alla propria soluzione di messaggistica con resilienza del sito. Un requisito fondamentale per il recupero da errori del sito prevede la creazione di una soluzione che trasporti i dati di messaggistica necessari a un datacenter di backup che ospita il servizio di backup per la messaggistica.

## Pianificazione dei certificati

Per la distribuzione di un DAG in un singolo datacenter, non ci sono particolari considerazioni inerenti la progettazione dei certificati. Per contro, quando un DAG si estende su più datacenter in una configurazione con resilienza del sito, esistono specifiche considerazioni sui certificati che vanno tenute in debito conto. In genere, la progettazione dei certificati dipende dai client in uso e dai requisiti imposti da altre applicazioni che utilizzano quei certificati. Tuttavia, esistono specifiche raccomandazioni e procedure consigliate da seguire in merito al tipo e numero di certificati da utilizzare.

È consigliabile ridurre al minimo il numero di certificati utilizzati per i server Exchange e per i server proxy inversi. Si consiglia di utilizzare un solo certificato per tutti questi endpoint dei servizi in ciascun datacenter. Questo approccio consente di ridurre la minimo il numero di certificati necessari e ciò di conseguenza riduce il costo e la complessità della soluzione.

Per i client Outlook Anywhere, si consiglia di utilizzare un solo certificato del nome alternativo del soggetto (SAN) per ciascun datacenter e di includere più nomi host in quel certificato. Per garantire la connessione con Outlook Anywhere dopo il passaggio a un database, server o datacenter, occorre utilizzare lo stesso nome principale del certificato in ciascun certificato e configurare l'oggetto Configurazione provider di Outlook in Active Directory con lo stesso nome principale nel formato standard di Microsoft (msstd). Ad esempio, se si utilizza il nome principale del certificato mail.contoso.com, il relativo attributo va configurato come segue.

    Set-OutlookProvider EXPR -CertPrincipalName "msstd:mail.contoso.com"

Alcune applicazioni che si integrano con Exchange hanno specifici requisiti per i certificati, che potrebbero richiedere l'utilizzo di certificati aggiuntivi. Exchange 2013 può coesistere con Office Communications Server (OCS). L'OCS richiede certificati a 1024 bit o più che utilizzano il nome server OCS come Nome principale del certificato. Tuttavia, poiché l'utilizzo di un nome server OCS come Nome principale del certificato impedisce il corretto funzionamento di Outlook Anywhere, è necessario utilizzare un certificato aggiuntivo e separato per l'ambiente OCS.

## Pianificazione della rete

Oltre agli specifici requisiti di rete che devono essere soddisfatti per ciascun DAG e per ciascun server che è membro di un DAG, ci sono altri requisiti e consigli che sono specifici delle configurazioni con resilienza del sito. Come per tutti i gruppi di disponibilità del database, a prescindere dal fatto che i membri del gruppo siano distribuiti in un singolo sito o in più siti, la latenza di rete (tempo di andata e ritorno) inter-membro non deve essere superiore a 500 millisecondi (ms). Inoltre, ci sono specifiche impostazioni di configurazione consigliate per i DAG che si estendono su più siti:

  - **Le reti MAPI devono essere isolate dalle reti di replica**   È necessario utilizzare criteri di rete Windows, criteri di protezione tramite firewall Windows o elenchi di controllo di accesso al router per bloccare il traffico tra la rete MAPI e le reti di replica. Questa configurazione è necessaria per prevenire il problema dell'heartbeat cross-talk delle reti.

  - **I record DNS lato client devono avere una durata (TTL) di 5 minuti**   Il tempo di inattività dei client dipende non solo dalla rapidità del passaggio, ma anche dalla rapidità con cui avviene la replica DNS e con cui i client eseguono le query per ottenere le informazioni aggiornate sul DNS. I record DNS di tutti i servizi client Exchange, inclusi Microsoft Office Outlook Web App, Microsoft Exchange ActiveSync, servizi Web di Exchange, Outlook Anywhere, SMTP, POP3 e IMAP4, sia sui server DNS interni che su quelli esterni, devono essere impostati con un TTL di 5 minuti.

  - **Utilizzare le route statiche per configurare la connessione tra tutte le reti di replica** Per garantire la connessione tra tutte le schede di rete di replica, utilizzare le route statiche persistenti. Si tratta di una configurazione rapida e una tantum che va eseguita su ciascun membro del gruppo di disponibilità del database quando si utilizzano gli indirizzi IP statici. Se si utilizza il protocollo DHCP per ottenere gli indirizzi IP delle proprie reti di replica, è possibile utilizzarlo anche per assegnare route statiche alla replica, semplificando in questo modo la procedura di configurazione.

## Pianificazione generale della resilienza del sito

Oltre ai requisiti per l'elevata disponibilità elencati sopra, sono disponibili altre raccomandazioni sulla distribuzione di Exchange 2013 in una configurazione con resilienza del sito (ad esempio, l'estensione di un percorso di disponibilità del database su più datacenter). Ciò che si fa durante la fase di panificazione influenza direttamente il successo della soluzione con resilienza del sito. Ad esempio, un'inadeguata progettazione dello spazio dei nomi può causare problemi con i certificati e una configurazione errata dei certificati può impedire l'accesso degli utenti ai servizi.

Per ridurre al minimo il tempo di attivazione di un secondo datacenter e permettergli di ospitare gli endpoint dei servizi di un datacenter fuori uso, è necessario effettuare una pianificazione accurata. Di seguito sono riportati alcuni esempi:

  - Gli obiettivi del contratto di servizio per la soluzione con resilienza del sito devono essere ben compresi e documentati.

  - I server del secondo datacenter devono avere sufficiente capacità per ospitare l'intera popolazione di utenti di entrambi i datacenter.

  - Nel secondo datacenter, devono essere abilitati tutti i servizi forniti dal datacenter principale (a meno che un servizio non sia escluso dal contratto di servizio per la resilienza del sito). Questi servizi sono: Active Directory, infrastruttura di rete (ad esempio, DNS o TCP/IP), servizi di telefonia (se si utilizza la messaggistica unificata) e infrastruttura del sito (come alimentazione o raffreddamento).

  - Affinché gli utenti di un datacenter fuori uso possano avvalersi di questi servizi, è necessario che siano configurati i certificati server appropriati. Alcuni servizi non consentono la creazione di istanze (ad esempio, POP3 e IMAP4) e consentono solo l'utilizzo di un singolo certificato. In questi casi, il certificato deve essere un certificato del nome alternativo del soggetto comprendente più nomi oppure i nomi multipli devono essere così simili da permettere l'utilizzo di un certificato jolly (a condizione che i criteri di sicurezza dell'organizzazione ne consentano l'utilizzo).

  - I servizi necessari devono essere definiti nel datacenter secondario. Ad esempio, se il primo datacenter ha tre diversi URL SMTP su differenti server di trasporto, è necessario definire la configurazione appropriata nel secondo datacenter per abilitare almeno uno dei server di trasporto (se non tutti e tre) per gestire il carico di lavoro.

  - È necessario approntare la configurazione di rete appropriata per supportare lo switchover tra datacenter. Ciò potrebbe implicare la verifica delle opportune configurazioni di bilanciamento del carico, della configurazione del DNS globale e dell'abilitazione della connessione a Internet con l'appropriata configurazione del routing.

  - È necessario comprendere perfettamente la strategia per l'abilitazione delle modifiche apportate al DNS per supportare il passaggio tra datacenter. Le specifiche modifiche apportate al DNS, comprese le impostazioni per la durata (TTL), devono essere definite e documentate per supportare il contratto di servizio in vigore.

  - Va altresì definita un'adeguata strategia di test della soluzione e questa strategia va inserita nel contratto di servizio. La convalida periodica della distribuzione è uno dei modi per garantire che la qualità e adeguatezza della distribuzione non si deteriorino nel tempo. Una volta convalidata la distribuzione, si consiglia di documentare nel dettaglio quella parte di configurazione che influenza direttamente il successo della soluzione. Inoltre, si consiglia di lavorare al miglioramento dei processi di gestione delle modifiche che interessano quei specifici segmenti della distribuzione.

Inizio pagina


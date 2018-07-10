---
title: 'Disponibilità elevata e resilienza del sito: Exchange 2013 Help'
TOCTitle: Disponibilità elevata e resilienza del sito
ms:assetid: 6628285e-d07c-443d-866b-be784ad1ed1e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638137(v=EXCHG.150)
ms:contentKeyID: 50480792
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disponibilità elevata e resilienza del sito

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-15_

È possibile proteggere i database delle cassette postali di Exchange Server 2013 e i dati che contengono configurando i database e i server Cassette postali per la disponibilità elevata e la resilienza del sito. Exchange 2013 riduce il costo e la complessità della distribuzione di una soluzione di messaggistica a disponibilità elevata e resilienza del sito fornendo al contempo livelli di servizio e disponibilità dei dati e assistenza per cassette postali di grandi dimensioni.

Exchange 2013 consente ai clienti di tutte le dimensioni e in tutti i segmenti di distribuire economicamente un servizio di continuità di messaggistica nell'organizzazione, basandosi sulle capacità di replica nativa e sull'architettura di elevata disponibilità in Exchange 2010. Per un elenco delle modifiche in Exchange 2010 ed Exchange 2007, vedere [Modifiche alla disponibilità elevata e resilienza sul sito rispetto le versioni precedenti](changes-to-high-availability-and-site-resilience-over-previous-versions-exchange-2013-help.md).

**Sommario**

Key terminology

Database availability groups

Mailbox database copies

Active Manager

Site resilience

Third-party replication API

High availability and site resilience documentation

## Terminologia chiave

I seguenti termini chiave sono importanti per comprendere l'elevata disponibilità o la resilienza del sito:

  - *Active Manager*  
    Un componente interno di Exchange che viene eseguito all'interno del servizio di replica di Microsoft Exchange, responsabile del monitoraggio degli errori e di un'azione correttiva tramite failover all'interno di un gruppo di disponibilità del database.

<!-- end list -->

  - *AutoDatabaseMountDial*  
    Un'impostazione di una proprietà di un server Cassette postali che determina se una copia di database passivo si installerà automaticamente come nuova copia attiva sulla base del numero di file di registro che mancano nella copia in corso di installazione.

<!-- end list -->

  - *Replica continua - modalità di blocco*  
    Nella modalità di blocco, ogni singolo aggiornamento viene scritto nel buffer di registro attivo della copia di database attiva e viene anche inviato a un buffer di registro in ognuna delle copie passive delle cassette postali in modalità di blocco. Quando il buffer di registro è pieno, ogni copia del database compila, ispeziona e crea il file di log successivo nella sequenza di generazione.

<!-- end list -->

  - *Replica continua - modalità file*  
    Nella modalità file, i file di registro delle transazioni chiuse vengono spinti dalla copia del database attivo su una o più copie del database passivo.

<!-- end list -->

  - *Gruppo di disponibilità del database*  
    Gruppo di un massimo di 16 server Cassette postali Exchange 2013 che ospita un insieme di database replicati.

<!-- end list -->

  - *Mobilità del database*  
    La capacità di un singolo database Cassette postali di Exchange 2013 di essere replicato e installato su altri server Cassette postali Exchange 2013.

<!-- end list -->

  - *Datacenter*  
    In genere si riferisce a un sito di Active Directory; tuttavia, può anche riferirsi ad un luogo fisico. Nel contesto di questa documentazione, datacenter equivale al sito di Active Directory.

<!-- end list -->

  - *modalità di coordinamento dell'attivazione del centro dati*  
    Una proprietà dell'impostazione del gruppo di disponibilità del database che, quando abilitata, forza il servizio di replica di Microsoft Exchange ad ottenere l'autorizzazione per installare database all'avvio.

<!-- end list -->

  - *Ripristino d'emergenza*  
    Qualsiasi processo utilizzato per eseguire manualmente il ripristino da un errore. Può trattarsi di un errore che incide su un elemento singolo oppure di un errore che riguarda un'intera posizione fisica.

<!-- end list -->

  - *API di replica di terza parte Exchange*  
    API fornita da Exchange che consente l'utilizzo di una replica sincrona di terze parti per un gruppo di disponibilità del database invece della replica continua.

<!-- end list -->

  - *Disponibilità elevata*  
    Soluzione che fornisce la disponibilità del servizio, la disponibilità dei dati e il ripristino automatico dagli errori che incidono su servizio o dati (ad esempio errore di rete, archiviazione o server).

<!-- end list -->

  - *Distribuzione incrementale*  
    Possibilità di distribuire disponibilità elevata e resilienza del sito dopo l'installazione di Exchange 2013.

<!-- end list -->

  - *Copia del database delle cassette postali ritardata*  
    Copia passiva del database delle cassette postali che presenta un intervallo di riesecuzione registrazione superiore a zero.

<!-- end list -->

  - *Copia del database delle cassette postali*  
    Database delle cassette postali (file EDB e registri) attivo o passivo.

<!-- end list -->

  - *Resilienza delle cassette postali*  
    Nome di una soluzione unificata a disponibilità elevata e resilienza del sito in Exchange 2013.

<!-- end list -->

  - *Disponibilità gestita*  
    Un gruppo di processi interni costituito da probe, sistemi di monitoraggio e risponditori che incorpora il monitoraggio e l'elevata disponibilità in tutti i ruoli server e in tutti i protocolli.

<!-- end list -->

  - *\*over* (pronunciato "star over")  
    Abbreviazione di *switchover* e *failover*. Per switchover si intende l'attivazione manuale di una o più copie del database. Per failover si intende l'attivazione automatica di una o più copie del database dopo un errore.

<!-- end list -->

  - *Rete sicura*  
    Precedentemente conosciuta come dumpster di trasporto, si tratta di una funzionalità del servizio di trasporto che memorizza una copia di tutti i messaggi per *X* giorni. L'impostazione predefinita è 2 giorni.

<!-- end list -->

  - *Ridondanza shadow*  
    Una funzionalità del server di trasporto che fornisce ridondanza per i messaggi per l'intero periodo di transito.

<!-- end list -->

  - *Resilienza del sito*  
    Una configurazione che estende l'infrastruttura di messaggistica a più siti di Active Directory per fornire una continuità operativa per il sistema di messaggistica nel caso di un errore che incida su uno dei siti.

Inizio pagina

## Gruppi di disponibilità del database

Un gruppo di disponibilità del database è il componente di base del framework a disponibilità elevata e resilienza del sito integrata in Exchange 2013. Un DAG è un gruppo di un massimo di 16 server Cassette postali che ospita un insieme di database e fornisce il ripristino automatico a livello del database da errori che hanno un impatto su singoli database, reti o server. Qualsiasi server in un gruppo di disponibilità del database è in grado di ospitare una copia del database delle cassette postali da qualsiasi altro server nel gruppo di disponibilità del database. Quando un server viene aggiunto al gruppo di disponibilità del database, funziona con altri server nel gruppo di disponibilità del database per fornire il ripristino automatico da errori che hanno un impatto sui database delle cassette postali, ad esempio un errore nel server o nel disco. Per ulteriori informazioni sui gruppi di disponibilità del database, vedere [Gruppi di disponibilità dei database (DAG)](database-availability-groups-dags-exchange-2013-help.md).

Inizio pagina

## Copie del database delle cassette postali

Le funzionalità disponibilità elevata e resilienza del sito utilizzate introdotte inizialmente in Exchange 2010 vengono utilizzate in Exchange 2013 per creare e mantenere copie dei database. Exchange 2013 inoltre sfrutta il concetto di mobilità del database, cioè failover a livello di database gestiti da Exchange.

La mobilità dei database consente di disconnettere i database dai server e di supportare fino a 16 copie di un singolo database. Fornisce, inoltre, un'esperienza locale per la creazione di copie di un database.

L'impostazione di una copia del database come database delle cassette postali attivo è definita *switchover*. Quando si verifica un errore che incide su un database o sull'accesso ad un database e un nuovo database diventa la copia attiva, il processo è denominato *failover*. Questo processo si riferisce inoltre a un errore server in cui uno o più server portano in linea i database precedentemente in linea sul server che ha presentato l'errore. Quando si verifica uno switchover o un failover, gli altri server di Exchange 2013 vengono a conoscenza dello switchover pressoché immediatamente e reindirizzano il traffico di messaggistica e client al nuovo database attivo.

Ad esempio, se un database attivo in un gruppo di disponibilità del database presenta un problema a causa di un errore dell'archiviazione sottostante, Active Manager effettua immediatamente il ripristino mediante failover su una copia del database in un altro server Cassette postali del gruppo di disponibilità del database. In Exchange 2013, la disponibilità gestita aggiunge nuovi comportamenti da recuperare dalla perdita di accesso del protocollo a un database, inclusi il riciclaggio dei pool di lavoro delle applicazioni, il riavvio di servizi e server e l'avvio dei failover dei database.

Per ulteriori informazioni sulle copie del database delle cassette postali, vedere [Copie del database delle cassette postali](mailbox-database-copies-exchange-2013-help.md).

Inizio pagina

## Active Manager

Exchange 2013 sfrutta il componente di Active Manager introdotto in Exchange 2010 per gestire il database e l'integrità, lo stato, la replica continua della copia del database e altri aspetti dell'elevata disponibilità del server Cassette postali. Per ulteriori informazioni su Active Manager, vedere [Active Manager](active-manager-exchange-2013-help.md).

Inizio pagina

## Resilienza del sito

Anche se Exchange 2013 continua a utilizzare i gruppi di disponibilità del database e il servizio Clustering di failover di Windows per la disponibilità elevata del ruolo del server Cassette postali e la resilienza del sito, quest'ultima non è la stessa in Exchange 2013. La resilienza del sito è molto migliorata in Exchange 2013 perché è stata semplificata. Le modifiche architetturali sottostanti che erano state effettuate in Exchange 2013 hanno un impatto notevole sugli aspetti del ripristino di una configurazione della resilienza del sito.

In Exchange 2010, il ripristino della cassetta postale (gruppo di disponibilità del database) e dell'accesso client (array del server Accesso client) erano legati tra loro. Se andavano perduti tutti i server Accesso client, il VIP per l'array o una parte significativa del gruppo di disponibilità del database, ci si trovava nella situazione in cui era necessario effettuare un switchover del datacenter. Si tratta di un processo ben documentato e generalmente ben compreso, anche se occorre del tempo per eseguirlo ed è necessario l'intervento umano per avviarlo.

In Exchange 2013, se per qualche motivo va perduta l'array del server Accesso client (ad esempio, si verifica un errore del dispositivo di bilanciamento del carico), non è necessario eseguire un switchover del datacenter. Con la corretta configurazione, il failover si verifica a livello del client e i client vengono automaticamente reindirizzati a un secondo datacenter che dispone di server Accesso client operativi e questi server comunicano tramite proxy con il server Cassette postali dell'utente, che non subisce gli effetti dell'interruzione (poiché non si effettua uno switchover). Poiché il servizio viene ripristinato automaticamente, invece di effettuare le operazioni di recupero del servizio, l'utente può dedicarsi alla risoluzione del problema (ad esempio, la sostituzione del dispositivo di bilanciamento del carico).

Inoltre, con la semplificazione dello spazio dei nomi, il consolidamento dei ruoli del server, il disaccoppiamento dei requisiti dei ruoli server del sito di Active Directory, la separazione del ripristino dell'array del server Accesso client e del gruppo di disponibilità del database e le modifiche apportate al bilanciamento del carico, in Exchange 2013 sono presenti delle modifiche che ora consentono il ripristino automatico e separato del server Accesso client e del gruppo di disponibilità del database nei siti, fornendo in tal modo scenari di failover del datacenter, se si dispone di tre postazioni.

In Exchange 2010, era possibile distribuire un gruppo di disponibilità del database su due datacenter e ospitare il testimone su un terzo datacenter e abilitare il failover per il ruolo del server Cassette postali per uno dei datacenter. Tuttavia, il failover non si risolveva da solo, in quanto bisognava ancora modificare manualmente lo spazio dei nomi per i ruoli del server non di cassette postali.

In Exchange 2013, lo spazio dei nomi non ha bisogno di spostarsi con il gruppo di disponibilità del database. Exchange sfrutta la tolleranza di errore incorporata nello spazio dei nomi attraverso più indirizzi IP e il bilanciamento del carico (e, se necessario, la possibilità di attivare e disattivare i server). I client HTTP moderni lavorano automaticamente con questa ridondanza. Lo stack HTTP può accettare più indirizzi IP per un nome di dominio completo (FQDN) e, se si verifica un errore con il primo indirizzo IP (ovvero, non riesce a connettersi), passerà al successivo indirizzo IP dell'elenco. In caso di errore non grave (la connessione è andata perduta una volta stabilita la sessione, forse a causa di un errore saltuario nel servizio in cui, ad esempio, un dispositivo sta interrompendo i pacchetti e deve essere disattivato), l'utente potrebbe aver bisogno di riaggiornare il browser.

Ciò significa che lo spazio dei nomi non è più un singolo punto di errore come lo era in Exchange 2010. In Exchange 2010, forse il più grosso singolo punto di errore nel sistema di messaggistica è il nome di dominio completo che è stato dato agli utenti, poiché dice all'utente dove andare. Nel paradigma Exchange 2010, modificare il punto in cui va il nome di dominio completo non è facile, poiché è necessario modificare il DNS, quindi occuparsi della latenza del DNS, che in alcune parti del mondo è piuttosto scarsa. Inoltre, bisogna occuparsi anche delle cache dei nomi nei browser che normalmente hanno una durata di circa 30 minuti o più.

Una delle modifiche apportate in Exchange 2013 è l'abilitazione dei client a usufruire di più destinazioni. Presupponendo che il client abbia la possibilità di usufruire di più destinazioni (quasi tutti i protocolli di accesso client in Exchange 2013 si basano su HTTP (alcuni esempi includono Outlook, Outlook via Internet, EAS, EWS, OWA e l'interfaccia di amministrazione di Exchange) e tutti i client HTTP supportati hanno la possibilità di utilizzare più indirizzi IP fornendo, in tal modo, il failover sul lato client. È possibile configurare il DNS per gestire più indirizzi IP per un client durante la risoluzione dei nomi. Ad esempio, il client richiede mail.contoso.com e ottiene due indirizzi IP o quattro indirizzi IP. Tuttavia, il client utilizzerà in maniera affidabile molti degli indirizzi IP che ottiene. Ciò migliora notevolmente la condizione del client, poiché se si verifica un errore su uno degli indirizzi IP, il client può disporre di uno o più indirizzi aggiuntivi per tentare la connessione. Se un client ne prova uno e si verifica un errore, attende circa 20 secondi e, quindi, prova l'indirizzo successivo nell'elenco. Pertanto, se si perde il VIP per l'array del server Accesso client, il ripristino per i client avviene automaticamente e in circa 21 secondi.

I vantaggi sono i seguenti:

  - In Exchange 2010, se si perdeva il dispositivo di bilanciamento del carico nel datacenter principale e non si disponeva di un atro dispositivo su quel sito, bisognava eseguire uno switchover del datacenter. In Exchange 2013, se si perde il dispositivo di bilanciamento del carico nel sito principale, è sufficiente disattivarlo (o magari disattivare il VIP) e ripararlo o sostituirlo. I client che ancora non utilizzano il VIP nel datacenter secondario eseguiranno automaticamente un failover sul VIP secondario senza che vengano apportate modifiche allo spazio dei nomi e al DNS. Ciò non solo significa che non è più necessario eseguire uno switchover, ma anche che tutto il tempo generalmente associato al ripristino dello switchover di un datacenter viene risparmiato. In Exchange 2010, bisognava gestire la latenza DNS (di qui, la raccomandazione di impostare la durata TTL su 5 minuti e l'introduzione dell'URL di failback). In Exchange 2013, non è necessario effettuare tali operazioni, in quanto si dispone di un failover rapido (20 secondi) dello spazio dei nomi tra i VIP (datacenter).

  - Dal momento che è possibile eseguire il failover lo spazio dei nomi tra Data Center, sono necessarie per ottenere il failover di un centro dati è un meccanismo per il failover del ruolo del server cassette postali tra datacenter. Per ottenere il failover automatico per il DAG, semplicemente progettare una soluzione in DAG in modo uniforme è suddivisa tra due datacenter e quindi collocare il server di controllo in una posizione terza in modo che possono essere arbitrated dai membri del DAG in due datacenter, indipendentemente dallo stato della rete tra i Data Center che contengono i membri del DAG. Se si dispone solo due Data Center e un terzo località non è disponibile, è possibile effettuare il server di controllo in una macchina virtuale Microsoft Azure. [Utilizzo di una macchina virtuale Azure Microsoft come server di controllo del DAG](using-a-microsoft-azure-vm-as-a-dag-witness-server-exchange-2013-help.md) per ulteriori informazioni, vedere.

  - In questo scenario, gli sforzi dell'amministratore vengono velocizzati grazie a una soluzione semplice del problema e non spesi nel servizio di ripristino. È sufficiente risolvere il problema verificatosi, mentre il servizio rimane in esecuzione e l'integrità dei dati viene mantenuta. Il livello di urgenza e stress che si avverte durante la riparazione di un dispositivo rotto è nulla rispetto all'urgenza e allo stress che si avvertono durante il ripristino del servizio. È meglio per l'utente finale e meno stressante per l'amministratore.

È possibile consentire il failover senza dover eseguire dei switchback (alcune volte denominati per errore failback). Se si perdono i server Accesso client nel datacenter principale e si verifica un'interruzione di 20 secondi per i client, potrebbe anche non essere necessario occuparsi del failback. A questo punto, la preoccupazione primaria sarebbe di risolvere il problema principale (ad esempio, la sostituzione del dispositivo di bilanciamento del carico). Una volta che è di nuovo online e funzionante, alcuni client inizieranno ad utilizzarlo, mentre altri potrebbero rimanere operativi tramite l'uso del secondo datacenter.

Exchange 2013 fornisce anche la funzionalità che consente agli amministratori di occuparsi degli errori saltuari. Un errore saltuario si verifica quando, ad esempio, è possibile effettuare la connessione TCP iniziale, ma poi non accade più nulla. Per un errore saltuario è necessaria un' ulteriore azione amministrativa poiché potrebbe essere la conseguenza di un dispositivo di sostituzione messo in funzione. Mentre è in corso il processo di riparazione, il dispositivo potrebbe attivarsi e accettare alcune richieste, ma non essere realmente pronto a fornire servizi ai client fino a quando non viene eseguita la necessaria procedura di configurazione. In questo scenario, l'amministratore può eseguire un switchover dello spazio dei nomi semplicemente rimuovendo il VIP per il dispositivo in corso di sostituzione dal DNS. In tal modo, durante il periodo di manutenzione, nessun client cercherà di connettersi. Una volta completata la sostituzione, l'amministratore può aggiungere nuovamente il VIP al DNS e i client potranno iniziare ad utilizzarlo.

Per ulteriori informazioni sulla pianificazione e sulla distribuzione della resilienza del sito, vedere [Pianificazione della disponibilità elevata e della resilienza del sito](planning-for-high-availability-and-site-resilience-exchange-2013-help.md) e [Distribuzione di elevata disponibilità e resilienza del sito](deploying-high-availability-and-site-resilience-exchange-2013-help.md).

Inizio pagina

## API di replica di terze parti

Exchange 2013 include anche una API di replica di terze parti che consente alle organizzazioni di utilizzare le soluzioni di replica sincrone di terze parti invece della funzionalità di replica continua incorporata. Microsoft supporta soluzioni di terze parti che utilizzano l'API, purché la soluzione offra la funzionalità necessaria per sostituire tutte le funzionalità di replica continua native disabilitate in seguito all'utilizzo dell'API. Le soluzioni sono supportate solo quando l'API viene utilizzata in un DAG per gestire e attivare le copie del database delle cassette postali. L'uso dell'API al di fuori di questi confini non è supportato. Inoltre, la soluzione deve soddisfare i requisiti di supporto hardware Windows applicabili (non è richiesta una convalida di verifica per il supporto).

Quando si distribuisce una soluzione che utilizza l'API di replica di terze parti incorporato, tenere presente che il fornitore di soluzioni è responsabile per il supporto della soluzione. Microsoft supporta i dati di Exchange per le soluzioni replicate e non replicato. Soluzioni che utilizzano la replica dei dati devono essere conformi ai criteri di supporto Microsoft per la replica dei dati, come descritto nell'articolo della Microsoft Knowledge Base 895847, [supportano la replica dei dati di più siti per Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=895847). Inoltre, le soluzioni che utilizzano il modello di risorse di Cluster di Failover di Windows devono soddisfare requisiti di supporto di cluster di Windows come descritto nell'articolo della Microsoft Knowledge Base 943984, [The Microsoft il supporto dei criteri per Windows Server 2008 o cluster di Failover di Windows Server 2008 R2](https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=943984) o [The Microsoft il supporto dei criteri per Windows Server 2012 cluster di Failover](https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=2775067).

I criteri di supporto per il backup e il ripristino di Microsoft per le distribuzioni che utilizzano soluzioni basate su API per le repliche di terze parti sono analoghi ai criteri delle distribuzioni delle repliche continue native.

Se si è un partner alla ricerca di informazioni su API di terze parti, contattare il rappresentante Microsoft.

Inizio pagina

## Documentazione sulla resilienza del sito e l'elevata disponibilità

La tabella seguente contiene i collegamenti agli argomenti che guideranno l'utente attraverso l'apprendimento della gestione dei DAG, delle copie del database delle cassette postali e del backup e ripristino per Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Argomento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="database-availability-groups-dags-exchange-2013-help.md">Gruppi di disponibilità dei database (DAG)</a></p></td>
<td><p>Informazioni sui DAG, Active Manager, modalità di coordinamento dell'attivazione del datacenter (DAC) e copie del database delle cassette postali.</p></td>
</tr>
<tr class="even">
<td><p><a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">Pianificazione della disponibilità elevata e della resilienza del sito</a></p></td>
<td><p>Informazioni generali sull'hardware, la rete, il software, il server di controllo e altri requisiti e procedure consigliate per i gruppi di disponibilità del database.</p></td>
</tr>
<tr class="odd">
<td><p><a href="deploying-high-availability-and-site-resilience-exchange-2013-help.md">Distribuzione di elevata disponibilità e resilienza del sito</a></p></td>
<td><p>Illustrazione di uno scenario di distribuzione di esempio per la distribuzione e la configurazione dei DAG.</p></td>
</tr>
<tr class="even">
<td><p><a href="managing-high-availability-and-site-resilience-exchange-2013-help.md">Gestione di elevata disponibilità e resilienza del sito</a></p></td>
<td><p>Informazioni sulle attività di gestione dei DAG, sui switchover e failover e la modalità di manutenzione.</p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoring-database-availability-groups-exchange-2013-help.md">Gruppi di disponibilità del database di monitoraggio</a></p></td>
<td><p>Informazioni sui cmdlet e script incorporati per il monitoraggio dei DAG e copie dei database.</p></td>
</tr>
<tr class="even">
<td><p><a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">Backup, ripristino e ripristino di emergenza</a></p></td>
<td><p>Informazioni sul backup e il ripristino dei database di Exchange, i database di ripristino e il ripristino del server.</p></td>
</tr>
</tbody>
</table>


Inizio pagina


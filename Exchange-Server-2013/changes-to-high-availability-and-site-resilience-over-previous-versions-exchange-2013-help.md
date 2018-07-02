---
title: 'Modifiche alla disponibilità elevata e resilienza sul sito rispetto le versioni precedenti: Exchange 2013 Help'
TOCTitle: Modifiche alla disponibilità elevata e resilienza sul sito rispetto le versioni precedenti
ms:assetid: de53c00b-091c-4a31-aacc-1bd40c756ce2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn789066(v=EXCHG.150)
ms:contentKeyID: 62519730
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifiche alla disponibilità elevata e resilienza sul sito rispetto le versioni precedenti

 

_**Si applica a:** Exchange Server 2013 SP1_

_**Ultima modifica dell'argomento:** 2015-04-07_

Exchange 2013 utilizza i gruppi di disponibilità del database e le copie del database delle cassette postali, insieme ad altre funzionalità come il recupero di un singolo elemento, i criteri di conservazione e le copie del database ritardate, per fornire la disponibilità elevata, la resilienza del sito e la protezione dati nativa di Exchange. La piattaforma a disponibilità elevata, il servizio Archivio informazioni di Exchange ed Extensible Storage Engine (ESE) sono stati migliorati per fornire maggiore disponibilità, semplificare la gestione e ridurre i costi. Questi miglioramenti includono:

  - **Riduzione di operazioni di input/output su disco al secondo previste su Exchange 2010** Consente di sfruttare dischi di maggiori dimensioni in termini di capacità e di operazioni di input/output su disco al secondo previste, nel modo più efficace possibile.

  - **Disponibilità gestita** Con la disponibilità gestita, le funzionalità di monitoraggio interno e orientate al ripristino sono strettamente integrate per aiutare a prevenire gli errori, ripristinare i servizi in maniera proattiva e avviare automaticamente il failover dei server o avvisare gli amministratori affinché compiano un'azione. L'attenzione si concentra sul monitoraggio e sulla gestione dell'esperienza dell'utente finale piuttosto che sui tempi di attività del server e dei componenti per mantenere il servizio sempre disponibile.

  - **Archivio gestito** Archivio gestito è il nome dei processi di Archivio informazioni riscritti da zero in Exchange 2013. Il nuovo Managed Store è scritto in C\# ed è strettamente integrato con il Servizio di replica di Microsoft Exchange (MSExchangeRepl.exe) per fornire maggiore disponibilità grazie a una resilienza migliorata.

  - **Supporto di più database per disco** Exchange 2013 include miglioramenti che consentono di supportare più database (insiemi di copie attive e passive) sullo stesso disco, sfruttando dischi più grandi in termini di capacità e IOPS con la massima efficienza possibile.

  - **AutoReseed** Il reseeding automatico consente di ripristinare rapidamente la ridondanza dei database dopo un errore del disco. Se un disco è in errore, la copia del database archiviata su quel disco viene copiata dalla copia del database attiva a un disco di riserva sullo stesso server. Se nel disco danneggiato sono state archiviate più copie di database, queste possono essere sottoposte automaticamente a reseeding su un disco di riserva. In questo modo si accelera il reseeding poiché è probabile che i database attivi si trovino su più server e i dati vengano copiati in parallelo.

  - **Ripristino automatico dagli errori di archiviazione** Questa funzionalità prosegue le innovazioni introdotte in Exchange 2010 per consentire il ripristino del sistema in caso di errori che agiscono sulla resilienza o sulla ridondanza. Oltre ai comportamenti relativi al controllo dei bug in Exchange 2010, Exchange 2013 include comportamenti di ripristino aggiuntivi per tempi di I/O elevati, consumo di memoria eccessivo da parte di MSExchangeRepl.exe e casi gravi in cui il sistema è in uno stato tale da non consentire nemmeno la pianificazione dei thread.

  - **Miglioramenti delle copie ritardate** Le copie ritardate ora possono prendersi cura di sé stesse entro certi limiti grazie all'esecuzione automatica del log. Le copie ritardate ignoreranno automaticamente i file di registro in numerose situazioni, come negli scenari di applicazione patch alla pagina e con spazio su disco insufficiente. Se il sistema rileva che l'applicazione di patch alla pagina è necessaria per una copia ritardata, i registri verranno riprodotti automaticamente nella copia ritardata per eseguire l'applicazione di patch alla pagina. Le copie ritardate richiameranno inoltre la funzione di riproduzione automatica al raggiungimento della soglia di spazio insufficiente su disco e al rilevamento della copia ritardata come unica disponibile per un periodo di tempo specifico. Le copie ritardate possono anche sfruttare la rete sicura semplificando così il recupero o l'attivazione.

  - **Miglioramenti all'avviso per copia singola** L'avviso per copia singola introdotto in Exchange 2010 non è più uno script pianificato separato. Ora è integrato nei componenti di disponibilità gestita nel sistema ed è una funzione nativa di Exchange.

  - **Configurazione automatica della rete del gruppo di disponibilità del databasee** Le reti dei gruppi di disponibilità del database possono essere configurate automaticamente dal sistema in base alle impostazioni di configurazione. Oltre alle opzioni di configurazione manuale, i gruppi di disponibilità del database possono distinguere le reti della replica da quelle MAPI e configurare automaticamente le reti dei gruppi di disponibilità del database.

## Riduzione delle operazioni di input/output su disco al secondo previste su Exchange 2010

In Exchange 2010, le copie di database passive hanno una profondità del punto di arresto molto bassa, caratteristica necessaria per un rapido failover. Inoltre, la copia passiva esegue preletture aggressive dei dati per mantenere una profondità del punto di arresto di 5 MB. Come conseguenza dell'utilizzo di una profondità del punto di arresto bassa e dell'esecuzione di queste operazioni di prelettura aggressiva, le operazioni di input/output su disco al secondo previste per una copia passiva del database erano pari alle operazioni di input/output su disco al secondo previste per una copia attiva in Exchange 2010.

In Exchange 2013, il sistema è in grado di fornire un rapido failover mentre si utilizza una profondità del punto di arresto elevata sulla copia passiva (100 MB). Poiché hanno una profondità del punto di arresto di 100 MB, le copie passive sono state modificate in modo da non essere più così aggressive. Come conseguenza dell'aumento della profondità del punto di arresto e la modifica delle preletture aggressive, le operazioni di input/output su disco al secondo previste per una copia passiva sono circa il 50% delle operazioni di input/output su disco al secondo previste della copia attiva in Exchange 2013.

La profondità di arresto più elevata sulla copia passiva ha dato luogo anche ad altre modifiche. Al failover in Exchange 2010, la cache del database viene svuotata mentre il database viene convertito da una copia passiva a una copia attiva. In Exchange 2013, la registrazione di Extensible Storage Engine (ESE) è stata riscritta, quindi la cache è stata conservata attraverso la transizione da passiva a attiva. Poiché ESE non ha bisogno di svuotare la cache, si ottiene un failover veloce.

Un'altra modifica è stata apportata al processo di manutenzione in background del database (BDM). Adesso il processo di manutenzione in background del database elabora 1-2 MB al secondo per copia.

Come conseguenza di queste modifiche, Exchange 2013 fornisce una riduzione significativa delle operazioni di input/output su disco al secondo previste su Exchange 2010.

## Disponibilità gestita

La disponibilità gestita è l'integrazione del monitoraggio attivo incorporato con la piattaforma a disponibilità elevata di Exchange 2013. Con la disponibilità gestita, il sistema può determinare quando eseguire un failover su un database in base all'integrità dei servizi. La disponibilità gestita è un'infrastruttura interna che viene distribuita sui ruoli server Client access e Cassette postali in Exchange 2013. Disponibilità gestita include tre componenti asincroni che effettuano il lavoro con continuità. Il primo componente è il motore probe, responsabile delle misurazioni sul server e della raccolta dei dati. I risultati di tali misurazioni fluiscono nel secondo componente: lo strumento di monitoraggio. Lo strumento di monitoraggio contiene tutta la logica aziendale utilizzata dal sistema sulla base di ciò che è considerato integro nei dati raccolti. Simile al motore di riconoscimento dello schema, lo strumento di monitoraggio cerca vari schemi diversi in tutte le misurazioni raccolte, quindi stabilisce se un elemento debba considerarsi o meno integro. Infine, c'è il motore risponditore, responsabile delle azioni di recupero. Se qualche elemento non è integro, la prima azione da eseguire è tentare di recuperarlo. Tutto ciò potrebbe includere azioni di ripristino in più fasi; ad esempio, il primo tentativo potrebbe essere di riavviare il pool di applicazioni, il secondo di riavviare il servizio, il terzo di riavviare il server e il tentativo successivo potrebbe essere quello di mettere offline il server in modo che non accetti più il traffico. Se le azioni di recupero hanno esito negativo, il sistema inoltra il problema a una persona tramite notifiche del registro eventi.

Disponibilità gestita viene implementata sotto forma di due servizi:

  - **Exchange Health Manager Service (MSExchangeHMHost.exe)** Si tratta di un processo di controller utilizzato per gestire i processi di lavoro. Viene utilizzato per realizzare, eseguire, avviare e arrestare il processo di lavoro, in base alle esigenze. Viene, inoltre, utilizzato per recuperare il processo di lavoro in caso di arresti anomali, per impedire che questo diventi un singolo punto di errore.

  - **Processo Exchange Health Manager Poker (MSExchangeHMWorker.exe)** Si tratta del processo di lavoro responsabile dell'esecuzione delle attività di runtime.

Gestione disponibilità utilizza un'archiviazione persistente per svolgere le sue funzioni:

  - i file di configurazione XML vengono utilizzati per inizializzare le definizioni dell'elemento di lavoro durante l'avvio del processo di lavoro.

  - Il Registro di sistema viene utilizzato per memorizzare i dati di runtime, quali i segnalibri.

  - L'infrastruttura del registro eventi del canale Crimson viene utilizzata per memorizzare i risultati degli elementi di lavoro.

Per ulteriori informazioni sulla disponibilità gestita, vedere [Disponibilità gestita](managed-availability-exchange-2013-help.md).

## Archivio gestito

Tutte le versioni precedenti di Exchange Server, da Exchange Server 4.0 per Exchange Server 2010, sono supportati in esecuzione una sola istanza del processo di archivio informazioni (Store.exe) nel ruolo del server cassette postali. Questa istanza archivio unica ospita tutti i database nel server: attiva, passiva, ritardata e il ripristino. In architetture di Exchange precedente, è disponibile, gli interventi di isolamento tra i diversi database ospitati in un server cassette postali. Un problema con un database delle cassette postali singolo è in grado di avere effetti negativi sulla tutti gli altri database e arresti anomali risultante da un danneggiamento delle cassette postali possono influire sulle servizio per tutti gli utenti il cui database sono ospitati su tale server.

Un altro problema con una singola istanza di archiviazione nelle versioni precedenti di Exchange è che il motore di ESE (Extensible Storage) Ridimensiona anche a 12 8 core, ma oltre a quello, problemi di sincronizzazione della cache e le comunicazioni tra più processori causare negativo implementare la scalabilità. Dato molto grande server moderni, con 16 + sistemi core disponibili, ciò significa impongono l'obiettivo di amministrazione di gestione dell'affinità di 12 8 core per ESE e con altri core per i processi di archiviazione non (ad esempio assistenti, Search Foundation Disponibilità gestita e così via). Inoltre, l'architettura precedente con restrizioni implementare la scalabilità verticale per il processo di archiviazione.

Il processo Store.exe evoluzione notevolmente nel corso degli anni come Server di Exchange stesso evoluzione, ma come un unico processo, in ultima analisi relativa scalabilità è limitata e rappresenta un singolo punto di errore. A causa di questi limiti Store.exe stati di Exchange 2013 e sostituito dall'archivio gestito.

Per ulteriori informazioni, vedere [Archivio gestito](managed-store-exchange-2013-help.md).

## Più database per volume

Sebbene i miglioramenti relativi all'archiviazione in Exchange 2013 siano stati ideati principalmente per le configurazioni JBOD, sono disponibili per l'uso da parte di tutte le configurazioni di archiviazione supportate. Una di queste funzionalità è la capacità di ospitare più database sullo stesso volume. Questa funzionalità riguarda l'ottimizzazione di Exchange per dischi di grandi dimensioni. Queste ottimizzazioni danno luogo ad un uso molto più efficace dei dischi di grandi dimensioni in termini di capacità, operazioni di input/output su disco al secondo previste e tempi di reseeding e sono state ideate per affrontare le difficoltà dell'esecuzione in una configurazione di archiviazione JBOD:

  - Le dimensioni dei database devono essere gestibili.

  - Le operazioni di reseeding devono essere veloci e affidabili.

  - Sebbene la capacità di archiviazione sia in aumento, le operazioni di input/output su disco al secondo previste non lo sono.

  - I dischi che ospitano copie di database passive sono sottoutilizzati in termini di operazioni di input/output su disco al secondo previste.

  - Le copie ritardate hanno requisiti di archiviazione asimmetrica.

  - Si dispone di una capacità limitata di recupero in condizioni di spazio su disco insufficiente.

La tendenza ad aumentare la capacità di archiviazione continua e nel prossimo futuro saranno disponibili unità da 8 TB. Se si utilizzano unità da 8 TB insieme alle linee guida relative alle procedure consigliate sulle dimensioni massime del database di Exchange (2 TB), ci sarebbe uno spazio su disco inutilizzato di 5 TB. Una soluzione sarebbe quella di aumentare semplicemente le dimensioni dei database, ma questa inibirebbe la gestibilità in quanto comporta tempi di reseeding elevati, compresi, in alcuni casi, tempi di reseeding ingestibili a livello operativo e l'affidabilità nel copiare tale quantità di dati sulla rete sarebbe compromessa.

Inoltre, nel modello di Exchange 2010, il disco che memorizza una copia passiva è sottoutilizzato in termini di operazioni di input/output su disco al secondo previste. Nel caso di una copia passiva ritardata, non soltanto il disco è sottoutilizzato in termini di operazioni di input/output su disco al secondo previste, ma è anche asimmetrico in termini di dimensioni, rispetto ai dischi utilizzati per memorizzare le copie attive e passive non ritardate.

Continuando una pratica di lunga data, Exchange 2013 è stato ottimizzato in modo da utilizzare dischi di grandi dimensioni (8 TB) in una configurazione JBOD in maniera più efficace. In Exchange 2013, con più database per disco, è possibile disporre di dischi delle stesse dimensioni che archiviano più copie di database, incluse quelle ritardate. Lo scopo è guidare la distribuzione degli utenti attraverso il numero di volumi esistenti, fornendo una struttura simmetrica in cui durante le normali operazioni ciascun membro di un gruppo di disponibilità del database ospita un insieme di copie attive, passive e facoltative ritardate sugli stessi volumi.

Un esempio di una configurazione che utilizza più database per volume è illustrato qui di seguito.

**Configurazione che utilizza più database per ciascun volume**

![Più database per volume](images/Dn789066.c5e7d6c8-3e77-4f72-a873-5e9aaded9aa3(EXCHG.150).gif "Più database per volume")

La precedente configurazione offre una struttura simmetrica. Tutti e quattro i server hanno gli stessi quattro database, tutti ospitati su un singolo disco per server. L'aspetto più importante è che il numero di copie di ciascun database di cui si dispone deve essere uguale al numero di copie di database per disco. Nell'esempio sopra riportato ci sono quattro copie di ogni database: una copia attiva, due copie passive e una copia ritardata. Poiché esistono quattro copie di ciascun database, la configurazione appropriata è una con quattro copie per volume. Inoltre, è stata configurata la preferenza di attivazione in modo che ci sia un equilibrio nel gruppo di disponibilità del database e su ciascun server. Ad esempio, la copia attiva avrà un valore di preferenza di attivazione pari a 1, la prima copia passiva avrà un valore pari a 2, la seconda copia passiva avrà un valore pari a 3 e la copia ritardata avrà un valore pari a 4.

Oltre ad avere una miglior distribuzione degli utenti nei volumi esistenti, un altro vantaggio dell'uso di più database per disco è quello di ridurre il tempo necessario per il ripristino della protezione dei dati nel caso di un errore che necessiti di un reseeding (ad esempio, un errore del disco).

Aumentando le dimensioni del database, aumenterà anche il tempo richiesto per il reseeding del database. Ad esempio, un database da 2 TB potrebbe richiedere 23 ore per l'operazione di reseeding, mentre per un database da 8 TB potrebbero volercene 93 (quasi 4 giorni). Entrambi i seeding si verificherebbero a circa 20 MB al secondo. Generalmente, ciò significa che non è possibile eseguire il seeding di un database di dimensioni notevoli entro una quantità di tempo ragionevole a livello operativo.

Nel caso di uno scenario di una singola copia di database per disco, l'origine del seeding viene individuata facilmente, in quanto il seeding del disco viene sempre effettuato da una singola origine. Dividendo il volume in più copie di database e avendo la copia attiva dei database passivi su un determinato volume archiviata in membri del gruppo di disponibilità del database distinti, il sistema non è più in grado di individuare efficacemente l'origine nel contesto del reseeding del disco. Quando viene sostituito un disco danneggiato, il reseeding può essere effettuato da più origini. Ciò consente al sistema di effettuare il reseeding e ripristinare la protezione dei dati per questi database in tempi molto più brevi.

Quando si utilizzano più database per volume, si consiglia di attenersi alle procedure consigliate e ai requisiti riportati di seguito:

  - È necessario utilizzare una singola partizione del disco logico per ogni disco fisico. Evitare di creare più partizioni sul disco. Tutte le copie di database e i relativi file complementari (quali, i registri delle transazioni e l'indice del contenuto) devono essere ospitati in una directory univoca sulla singola partizione.

  - Il numero di copie del database configurato per volume deve essere uguale al numero di copie di ciascun database. Ad esempio, se si dispone di 4 copie dei database utilizzati, è necessario utilizzare 4 copie di database per volume.

  - Le copie di database devono avere gli stessi vicini. (ad esempio, devono condividere tutte lo stesso disco su ciascun server).

  - È necessario equilibrare la preferenza di attivazione nel gruppo di disponibilità del database, in modo che ciascuna copia del database su un determinato disco abbia un valore di preferenza di attivazione univoco.

## AutoReseed

Il reseeding automatico o AutoReseed è una funzionalità che sostituisce ciò che normalmente è un'azione guidata dall'amministratore in risposta ad un errore del disco, errore di danneggiamento del database o altri problemi che necessitano di un reseeding di una copia del database. L'AutoReseed è stato ideato per ripristinare automaticamente la ridondanza del database a seguito di un errore del disco utilizzando dischi di riserva forniti con il sistema.

Per ulteriori informazioni, vedere [AutoReseed](autoreseed-exchange-2013-help.md). Per la procedura dettagliata per configurare l'AutoReseed, vedere [Configurare il reseeding automatico per un gruppo di disponibilità del database](configure-autoreseed-for-a-database-availability-group-exchange-2013-help.md).

## Ripristino automatico degli errori di archiviazione

Ripristino automatico degli errori di archiviazione continua l'innovazione introdotta in Exchange 2010 per consentire il ripristino del sistema in seguito a errori che incidono sulla resilienza o la ridondanza. Oltre ai comportamenti relativi al controllo dei bug in Exchange 2010, Exchange 2013 include ulteriori comportamenti di ripristino per tempi di I/O elevati, consumo eccessivo della memoria da parte del servizio di replica di Microsoft Exchange (MSExchangeRepl.exe) e casi gravi in cui non è possibile programmare i thread.

Anche negli ambienti JBOD, i controller degli array di archiviazione possono riscontrare dei problemi, quali arresti anomali o blocchi. Exchange 2010 comprendeva funzionalità di rilevamento e ripristino degli I/O bloccati che fornivano una resilienza migliore. Queste funzionalità sono elencate nella tabella seguente.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Controllo</th>
<th>Azione</th>
<th>Soglia</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Rilevamento dell'interruzione di I/O del Database Extensible Storage Engine (ESE)</p></td>
<td><p>Controlli ESE per I/O eccezionali</p></td>
<td><p>Genera un errore nel canale Crimson per riavviare il server</p></td>
<td><p>240 secondi</p></td>
</tr>
<tr class="even">
<td><p>Heartbeat del canale con errore</p></td>
<td><p>Garantisce la possibilità di scrivere e leggere gli elementi errati sul canale Crimson</p></td>
<td><p>Il servizio di replica rileva gli heartbeat del canale Crimson e riavvia il server in errore</p></td>
<td><p>30 secondi</p></td>
</tr>
<tr class="odd">
<td><p>Heartbeat del disco di sistema</p></td>
<td><p>Verifica lo stato del disco di sistema del server</p></td>
<td><p>Invia periodicamente I/O senza buffer al disco di sistema; riavvia il server in caso di timeout dell'heartbeat</p></td>
<td><p>120 secondi</p></td>
</tr>
</tbody>
</table>


Exchange 2013 migliora la resilienza e l'archiviazione, includendo nuovi comportamenti per altre condizioni gravi. Queste condizioni e i relativi comportamenti sono descritti nella tabella seguente.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Controllo</th>
<th>Azione</th>
<th>Soglia</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Stato non valido del sistema</p></td>
<td><p>Nessun thread, tra cui i thread non gestiti, può essere programmato</p></td>
<td><p>Riavvio del server</p></td>
<td><p>302 secondi</p></td>
</tr>
<tr class="even">
<td><p>Tempi di I/O elevati</p></td>
<td><p>Misurazioni della latenza del funzionamento I/O</p></td>
<td><p>Riavvio del server</p></td>
<td><p>41 secondi</p></td>
</tr>
<tr class="odd">
<td><p>Utilizzo della memoria del servizio di replica</p></td>
<td><p>Misurazione del working set di MSExchangeRepl.exe</p></td>
<td><ol>
<li><p>Registrazione dell'evento 4395 nel canale Crimson con una richiesta di cessazione del servizio</p></li>
<li><p>Avviare la chiusura di MSExchangeRepl.exe</p></li>
<li><p>Se la cessazione del servizio non riesce, riavviare il server</p></li>
</ol></td>
<td><p>4 GB</p></td>
</tr>
<tr class="even">
<td><p>Evento di sistema 129 (reimpostazione del bus)</p></td>
<td><p>Verifica dell'evento 129 nel registro degli eventi di sistema</p></td>
<td><p>Riavvio del server</p></td>
<td><p>Quando si verifica un evento</p></td>
</tr>
<tr class="odd">
<td><p>Blocco del database di cluster</p></td>
<td><p>Vengono bloccati gli aggiornamenti di Update Manager globali</p></td>
<td><p>Riavvio del server</p></td>
<td><p>Quando si verifica un evento</p></td>
</tr>
</tbody>
</table>


## Miglioramenti della copia ritardata

I miglioramenti apportati alla copia ritardata includono l'integrazione con una rete sicura e la riproduzione automatica dei file di registro in determinati scenari. La rete sicura è una funzionalità di trasporto che sostituisce la funzionalità di Exchange 2010 conosciuta come dumpster di trasporto. La rete sicura è simile al dumpster di trasporto, in quanto è una coda di recapito associata al servizio Trasporto su un server Cassette postali. Questa coda archivia le copie dei messaggi che sono stati recapitati al database delle cassette postali attivo sul server Cassette postali. Ciascun database delle cassette postali attivo sul server Cassette postali dispone di una coda che archivia le copie dei messaggi recapitati. È possibile specificare per quanto tempo la Rete sicura conserva le copie dei messaggi recapitati prima che scadano e vengano eliminati automaticamente.

La rete sicura si assume alcune responsabilità della ridondanza shadow negli ambienti dei gruppi di disponibilità del database. Negli ambienti dei gruppi di disponibilità del database, non è necessario che la ridondanza shadow mantenga un'altra copia del messaggio recapitato in una coda shadow mentre attende che il messaggio recapitato venga replicato sulle copie passive del database delle cassette postali sugli altri server Cassette postali nel gruppo di disponibilità del database. La copia del messaggio recapitato è già archiviata nella rete sicura, quindi la ridondanza shadow può recapitare nuovamente il messaggio dalla rete sicura, se necessario.

Con l'introduzione della Rete sicura, attivare una copia ritardata del database diventa molto più semplice. Ad esempio, si supponga di disporre di una copia ritardata con un intervallo di riproduzione di 2 giorni. In questo caso, è necessario configurare la rete sicura per un periodo di 2 giorni. Se ci si dovesse trovare in una situazione in cui sarebbe necessario utilizzare la copia ritardata, è possibile sospenderne la replica e copiarla due volte (per mantenere la natura ritardata del database e creare un'ulteriore copia nel caso fosse necessaria). Quindi, prendere una copia e eliminare tutti i file di registro, eccetto quelli della serie richiesta. Installare la copia; in questo modo viene attivata una richiesta automatica alla rete sicura affinché recapiti nuovamente gli ultimi due giorni di posta. Con la rete sicura, non è necessario rispondere dove è stato introdotto il punto di danneggiamento. Si ricevono gli ultimi due giorni di posta, meno i dati andati normalmente persi per un failover.

Le copie ritardate si possono ora autoripristinare richiamando l'esecuzione automatica del registro per riprodurre i file di registro in certi scenari:

  - Raggiungimento di una soglia di spazio insufficiente su disco

  - Quando la copia ritardata ha un danneggiamento fisico è necessaria un'applicazione di patch alla pagina

  - Quando sono presenti meno di tre copie integre disponibili (solo attivo o passivo; copie del database ritardate non sono conteggiate) per più di 24 ore

In Exchange 2010, l'applicazione di patch alla pagina non era disponibile per le copie ritardate. In Exchange 2013, l'applicazione di patch alla pagina è disponibile per le copie ritardate tramite questa funzionalità di riproduzione automatica. Se il sistema rileva che l'applicazione di patch alla pagina è necessaria per una copia ritardata, i registri vengono automaticamente riprodotti nella copia ritardata per eseguire l'applicazione di patch alla pagina. Le copie ritardate richiamano inoltre la funzione di riproduzione automatica al raggiungimento della soglia di spazio insufficiente su disco e al rilevamento della copia ritardata come unica disponibile per un periodo di tempo specifico.

Il comportamento di riproduzione delle copie ritardate è disabilitato per impostazione predefinita e può essere abilitato utilizzando il comando seguente.

    Set-DatabaseAvailabilityGroup <DAGName> -ReplayLagManagerEnabled $true

Una volta abilitata, la riproduzione avviene quando ci sono meno di tre copie. È possibile modificare il valore predefinito di 3, modificando il seguente valore di registro DWORD.

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagManagerNumAvailableCopies**

Per abilitare la riproduzione per il raggiungimento della soglia di spazio insufficiente su disco, è necessario configurare la seguente voce di registro.

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagLowSpacePlaydownThresholdInMB**

Dopo aver configurato tutte le impostazioni di registro, riavviare il servizio Microsoft Exchange DAG Management per rendere effettive le modifiche.

Come esempio, considerare un ambiente dove un dato database dispone di 4 copie (3 copie ad elevata disponibilità ed 1 copia ritardata) e l'impostazione predefinita è utilizzata per *ReplayLagManagerNumAvailableCopies*. Se una copia non ritardata non è in grado di funzionare per qualsiasi motivo (ad esempio è sospeso) la copia ritardata riprodurrà automaticamente i rispettivi file di registro in 24 ore.

## Miglioramenti dell'avviso della presenza di una singola copia

Assicurarsi che i server stiano lavorando in maniera affidabile e che le copie del database delle cassette postali siano integre e siano gli obiettivi primari delle operazioni quotidiane di messaggistica di Exchange 2013. È necessario monitorare attivamente l'hardware, il sistema operativo Windows e i servizi di Exchange. Ma quando si lavora in un ambiente di resilienza delle cassette postali di Exchange 2013, è importante monitorare l'integrità e lo stato del gruppo di disponibilità del database e le copie del database delle cassette postali utilizzate. È particolarmente importante eseguire la gestione dei rischi della ridondanza dei dati ed eseguirne il monitoraggio per i periodi in cui un database replicato è sceso fino a una singola copia. Ciò è fondamentale soprattutto in ambienti che non utilizzano le soluzioni RAID (Redundant Array of Independent Disks) e distribuiscono, invece, configurazioni JBOD. In un ambiente RAID, l'errore di un singolo disco non influisce su una copia attiva del database delle cassette postali. Tuttavia, in un ambiente JBOD, l'errore di un singolo disco provoca un failover del database.

In Exchange 2010, è stato introdotto lo script CheckDatabaseRedundancy.ps1. Come indica il nome, l'obiettivo dello script era di monitorare la ridondanza dei database delle cassette postali replicati con la convalida di almeno due copie configurate, integre e aggiornate e inviare un avviso all'amministratore, tramite la generazione di una registrazione dell'evento, in presenza di una sola copia integra di un database replicato. In questo caso, vengono conteggiate entrambe le copie attiva e passiva per la determinazione della ridondanza.

Di seguito sono elencate alcune fra le condizioni di singola copia:

  - Replica su qualsiasi copia passiva non riuscita da parte di una copia attiva.

  - Errore di tutte le copie passive, inclusi lo stato FailedAndSuspended e Failed oltre agli stati di integrità in cui la copia è in ritardo nel copiare la registrazione o nella riproduzione. Si noti che le copie ritardate non sono considerate in ritardo se la riproduzione del registro avviene entro dieci minuti nell'ambito del periodo di ritardo.

  - Errore del sistema sull'informazione precisa riguardante l'attuale generazione del registro della copia attiva.

Poiché è altamente prioritario per gli amministratori sapere quando si trovano in presenza di una singola copia integra di un database, lo script CheckDatabaseRedundancy.ps1 è stato sostituito con una funzionalità nativa integrata che fa parte del set di integrità DataProtection di disponibilità gestita.

La funzionalità nativa avvisa ancora gli amministratori tramite notifica del registro eventi e per distinguere gli avvisi Exchange 2013 da Exchange 2010, Exchange 2013 utilizza i seguenti ID eventi:

  - Evento 4138 (Red Alert)

  - Evento 4139 (Green Alert)

In Exchange 2013, la funzionalità nativa è stata migliorata per ridurre il livello dei disturbi di avviso che possono presentarsi quando più database sullo stesso server entrano nella condizione di copia singola. In Exchange 2010, gli avvisi di singola copia sono stati generati a livello del singolo database. Di conseguenza, quando c'era un problema a livello di server che interessava più database e più copie di database, c'era la possibilità di una condizione di avvisi in soprannumero. Poiché diversi errori, quali problemi relativi ai controller o alla memoria, riguardano l'intero server, vi era una probabilità moderatamente elevata che potessero verificarsi numerosi avvisi per ogni incidente del server. In Exchange 2013, questi avvisi sono ora generati in base al singolo server. Quando un'interruzione incide su un intero server e la ridondanza dei dati diventa a rischio per più copie del database, viene ora generato un singolo avviso per server.

## Configurazione automatica della rete dei DAG

Una rete del DAG è un insieme di una o più subnet utilizzato sia per il traffico di replica che per il traffico MAPI. Ciascun DAG contiene al massimo una rete MAPI e zero o più reti di replica. In Exchange 2010, le reti dei DAG (ad esempio, DAGNetwork01 e DAGNetwork02) create dal sistema si basano sulle subnet enumerate dal servizio Cluster. Negli ambienti in cui vengono utilizzate più reti e le interfacce per una determinata rete (ad esempio, la rete MAPI) erano sulla stessa subnet, l'ulteriore configurazione che un amministratore doveva aggiungere era minima. Tuttavia, negli ambienti in cui le interfacce per una determinata rete erano su più subnet, l'amministratore doveva eseguire un'attività denominata compressione delle reti dei gruppi di disponibilità del database.

In Exchange 2013, la compressione delle reti dei gruppi di disponibilità del database non è più necessaria. Exchange 2013 utilizza ancora gli stessi meccanismi di rilevamento per distinguere tra le reti MAPI e di replica, ma ora comprime automaticamente le reti dei gruppi di disponibilità del database in base alle esigenze dell'utente.

Inoltre, per impostazione predefinita, le reti dei gruppi di disponibilità del database vengono ora gestite automaticamente dal sistema. Per visualizzare le proprietà delle reti dei gruppi di disponibilità del database utilizzando l'interfaccia di amministrazione di Exchange, è necessario configurare i gruppi di disponibilità del database per il controllo manuale della rete, modificando le proprietà del gruppo di disponibilità del database tramite l'interfaccia di amministrazione di Exchange o utilizzando il cmdlet **Set-DatabaseAvailabilityGroup** per impostare il parametro *ManualDagNetworkConfiguration* su `True`.

## Modifiche al processo di selezione della copia migliore

Il processo di selezione della copia migliore (BCS) è un processo di algoritmo interno per trovare la copia migliore di un singolo database da attivare in un elenco di potenziali copie per l'attivazione con relativi integrità e stato. Active Manager seleziona la migliore copia disponibile (e non bloccata) adatta a diventare la nuova copia attiva del database quando si verifica un errore della copia attiva del database esistente o quando l'amministratore esegue un passaggio generico. In Exchange 2010 il processo BCS valutava numerosi aspetti di ciascuna copia di database per determinare la copia migliore da attivare. Tra questi erano inclusi:

  - Lunghezza coda di copia

  - Lunghezza coda di riproduzione

  - Stato del database

  - Stato dell'indice del contenuto

In Exchange 2013, Active Manager esegue gli stessi controlli e fasi per il processo BCS per determinare l'integrità della replica, ma ora include anche l'uso di un limite dell'ordine decrescente degli stati di integrità. Come conseguenza di tali modifiche, il processo di selezione della copia migliore (BCS) viene ora denominato processo di selezione della copia e del server migliori (BCSS).

Il processo BCSS include diversi nuovi controlli di integrità che fanno parte dei componenti di monitoraggio della disponibilità gestita incorporati in Exchange 2013. Sono presenti quattro nuovi controlli eseguiti da Active Manager (elencati nell'ordine in cui vengono eseguiti):

1.  **All Healthy** Verifica la presenza di un server che ospita una copia del database interessato con tutti i componenti di monitoraggio in uno stato integro.

2.  **Up to Normal Healthy**   Verifica la presenza di un server che ospita una copia del database interessato con tutti i componenti di monitoraggio con priorità Normale in uno stato integro.

3.  **All Better than Source**   Verifica la presenza di un server che ospita una copia del database interessato con i componenti di monitoraggio in uno stato migliore del server corrente che ospita la copia interessata.

4.  **Same as Source** Verifica la presenza di un server che ospita una copia del database interessato con i componenti di monitoraggio in uno stato equivalente a quello del server corrente che ospita la copia interessata.

Se BCSS viene richiamato come conseguenza di un failover attivato dal componente di monitoraggio di disponibilità gestita (ad esempio, attraverso un risponditore di failover), viene applicato un ulteriore vincolo obbligatorio per cui l'integrità del componente del server di destinazione deve essere migliore del server sul quale si è verificato il failover. Ad esempio, se un errore di Microsoft Office Outlook Web App provoca un failover della disponibilità gestita tramite il risponditore Failover, BCSS deve selezionare un server che ospita una copia del database interessato in cui Outlook Web App risulta integro.

## Servizio di gestione del gruppo di disponibilità del database (DAG)

L'aggiornamento cumulativo (CU2) per la versione RTM (Release to Manufacturing ) di Exchange 2013 contiene un nuovo servizio sui server Cassette postali che sono membri di un gruppo di disponibilità del database. Questo servizio viene definito servizio di gestione del gruppo di disponibilità del database di Microsoft Exchange (MSExchangeDAGMgmt). Tale nuovo servizio contiene funzionalità di monitoraggio DAG interno che venivano precedentemente eseguite all'interno del servizio di replica di Microsoft Exchange (MSExchangeRepl).

## DAG senza un punto di accesso di amministrazione cluster

Tutti i DAG che eseguono Windows Server 2008 R2 o Windows Server 2012 richiedono almeno un indirizzo IP su ogni subnet inclusa nella rete MAPI. Gli indirizzi IP assegnati al DAG vengono utilizzati dal cluster del DAG con il punto di accesso amministrativo del cluster (denominato anche nome rete cluster) per abilitare la risoluzione del nome e la connettività sul cluster (o più esattamente, connettività sul membro del cluster che al momento include il gruppo risorsa principale del cluster) utilizzando il nome del cluster. Windows Server 2012 R2 abilita la creazione di un failover dei cluster senza un punto di accesso amministrativo. I cluster di failover di Windows senza punti di accesso amministrativo hanno le seguenti caratteristiche:

  - Non è presente un indirizzo IP assegnato al cluster e, quindi, nessuna risorsa indirizzo IP nel gruppo risorsa principale del cluster.

  - Non è presente un nome di rete assegnata al cluster e, quindi, nessuna risorsa nome di rete nel gruppo risorsa principale del cluster

  - Il nome del cluster non è registrato nel DNS e non è risolvibile nella rete.

  - Non viene creato un oggetto di nome cluster (CNO) in Active Directory.

  - Il cluster di failover di Windows non può essere gestito utilizzando lo strumento di gestione Cluster di Failover. Deve essere gestito utilizzando Windows PowerShell e i cmdlet PowerShell devono essere eseguiti sui membri del cluster individuale.

Quando si esegue Windows Server 2012 R2 o versione successiva, Service Pack 1 (SP1) per Exchange 2013 e versione successiva abilitano la creazione di un DAG senza un punto di accesso amministrativo cluster. È possibile creare un DAG senza un punto di accesso amministrativo utilizzando Exchange Admin Center o Shell. Per ulteriori informazioni, vedere [Creating DAGs](managing-database-availability-groups-exchange-2013-help.md) e [Creare un gruppo di disponibilità del database](create-a-database-availability-group-exchange-2013-help.md).


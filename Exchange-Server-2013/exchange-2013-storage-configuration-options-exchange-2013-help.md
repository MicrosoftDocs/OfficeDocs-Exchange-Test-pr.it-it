---
title: 'Opzioni di configurazione di archiviazione di Exchange 2013: Exchange 2013 Help'
TOCTitle: Opzioni di configurazione di archiviazione di Exchange 2013
ms:assetid: 37cdeacf-74f9-4399-9860-4d1dbec12bb1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee832792(v=EXCHG.150)
ms:contentKeyID: 50480343
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Opzioni di configurazione di archiviazione di Exchange 2013

 

_**Si applica a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Le informazioni sulle opzioni e i requisiti di archiviazione per il ruolo del server Cassette postali in Microsoft Exchange Server 2013 costituiscono un aspetto importante della soluzione di progettazione per l'archiviazione del server Cassette postali.

**Sommario**

Storage architectures

Physical disk types

Best practices for supported storage configurations

## Architetture di archiviazione

Nella tabella seguente vengono descritte le architetture di archiviazione supportate e vengono illustrate le procedure consigliate per ogni tipo di architettura.

### Architetture di archiviazione supportate

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Architettura di archiviazione</th>
<th>Descrizione</th>
<th>Procedura consigliata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DAS (Direct-Attached Storage)</p></td>
<td><p>DAS è un sistema di archiviazione digitale direttamente collegato al server o alla workstation, senza dover utilizzare una rete di archiviazione. Ad esempio, i trasporti DAS comprendono Serial Attached SCSI (Small Computer System Interface) e Serial Attached ATA (Advanced Technology Attachment).</p></td>
<td><p>Non disponibile.</p></td>
</tr>
<tr class="even">
<td><p>SAN (rete di archiviazione): iSCSI (Internet Small Computer System Interface)</p></td>
<td><p>La rete SAN è un'architettura che collega i dispositivi di archiviazione del computer remoto (ad esempio, array di dischi e librerie di nastri) ai server in modo tale da sembrare collegati in locale al sistema operativo (ad esempio, archiviazione di blocco). Le reti SAN iSCSI comprendono i comandi SCSI all'interno dei pacchetti IP e utilizzano l'infrastruttura di rete standard come trasporto di archiviazione (ad esempio, Ethernet).</p></td>
<td><p>Non condividere i dischi fisici che eseguono il backup dei dati di Exchange con altre applicazioni.</p>
<p>Utilizzare reti di archiviazione dedicate.</p>
<p>Utilizzare più percorsi di rete per le configurazioni autonome.</p></td>
</tr>
<tr class="odd">
<td><p>SAN: Fibre Channel</p></td>
<td><p>Le reti SAN di Fibre Channel comprendono i comandi SCSI all'interno dei pacchetti Fibre Channel e generalmente utilizzano le reti Fibre Channel specializzate come trasporto di archiviazione.</p></td>
<td><p>Non condividere i dischi fisici che eseguono il backup dei dati di Exchange con altre applicazioni.</p>
<p>Utilizzare più percorsi di rete Fibre Channel per le configurazioni standalone.</p>
<p>Seguire le procedure consigliate del fornitore di archiviazione per la regolazione delle schede bus host (HBA) di Fibre Channel, come la destinazione e la profondità della coda.</p></td>
</tr>
</tbody>
</table>


Un'unità NAS (Network Attached Storage) è un computer autonomo connesso ad una rete, con l'unico scopo di fornire servizi di archiviazione dei dati basati sui file ad altri dispositivi sulla rete. Il sistema operativo e il software sull'unità NAS offrono l'archiviazione dei dati, file system, l'accesso ai file e la gestione delle funzionalità (ad esempio, l'archiviazione dei file).

Tutti i sistemi utilizzati da Exchange per l'archiviazione dei dati Exchange devono essere sistemi di archiviazione a livello di blocco in quanto Exchange 2013 non supporta l'utilizzo di volumi NAS, diversi dallo scenario SMB 3.0 evidenziato più avanti nell'argomento [Virtualizzazione di Exchange 2013](exchange-2013-virtualization-exchange-2013-help.md). Inoltre, in un ambiente virtualizzato, l'archiviazione NAS presentata alla macchina guest come archiviazione a livello di blocco via hypervisor non è supportata.

Non è consigliabile utilizzare i livelli di archiviazione, come potrebbero influire negativamente sulle prestazioni del sistema. Per questo motivo, non consentire il controller di archiviazione spostare automaticamente gli file utilizzati per "superiore" spazio di archiviazione.

Inizio pagina

## Tipi di disco fisico

Nella tabella seguente viene fornito un elenco dei tipi di disco fisico supportati e vengono illustrate le procedure consigliate per ogni tipo di disco fisico.

### Tipi di disco fisico supportati

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di disco fisico</th>
<th>Descrizione</th>
<th>Procedura supportata o consigliata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SATA (Serial ATA)</p></td>
<td><p>SATA indica un'interfaccia seriale per ATA e i dischi IDE (Integrated Device Electronics). I dischi SATA sono disponibili con diversi form factor, velocità e capacità.</p>
<p>In generale, scegliere i dischi SATA per l'archiviazione delle cassette postali di Exchange 2013 quando si devono soddisfare i seguenti requisiti:</p>
<ul>
<li><p>Alta capacità</p></li>
<li><p>Prestazioni moderate</p></li>
<li><p>Consumo di energia moderato</p></li>
</ul></td>
<td><p>Supportati: dischi con settore da 512 byte per Windows Server 2008 e Windows Server 2008 R2. Sono inoltre supportati dischi 512e per Windows Server 2008 R2 con quanto indicato di seguito:</p>
<ul>
<li><p>Aggiornamento rapido descritto nell'<a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">articolo 982018 della Microsoft Knowledge Base</a> È disponibile un aggiornamento che migliora la compatibilità di Windows 7 e Windows Server 2008 R2 con i dischi di formato avanzato.</p></li>
<li><p>Windows Server 2008 R2 con Service Pack 1 (SP1) ed Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 e versioni successive supporta i dischi con settore da 4 kilobyte (KB) nativi e i dischi 512e. Il supporto richiede che tutte le copie di un database si trovino sullo stesso tipo di disco fisico. Ad esempio, non è supportata una configurazione che ospita una copia di un determinato database su un settore del disco da 512 byte e un'altra copia dello stesso database su un disco 512e o un disco 4K.</p>
<p>Procedura consigliata: Prendere in considerazione i dischi SATA classe Enterprise, che generalmente dispongono di migliori caratteristiche riguardo a calore, vibrazione e affidabilità.</p></td>
</tr>
<tr class="even">
<td><p>Serial Attached SCSI</p></td>
<td><p>Serial Attached SCSI indica un'interfaccia seriale per i dischi SCSI. I dischi Serial Attached SCSI sono disponibili in una vasta gamma di form factor, velocità e capacità.</p>
<p>In generale, scegliere i dischi Serial Attached SCSI per l'archiviazione delle cassette postali di Exchange 2013 quando si devono soddisfare i seguenti requisiti:</p>
<ul>
<li><p>Capacità moderata</p></li>
<li><p>Elevate prestazioni</p></li>
<li><p>Consumo di energia moderato</p></li>
</ul></td>
<td><p>Supportati: dischi con settore da 512 byte per Windows Server 2008 e Windows Server 2008 R2. Sono inoltre supportati dischi 512e per Windows Server 2008 R2 con quanto indicato di seguito:</p>
<ul>
<li><p>Aggiornamento rapido descritto nell'<a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">articolo 982018 della Microsoft Knowledge Base</a> È disponibile un aggiornamento che migliora la compatibilità di Windows 7 e Windows Server 2008 R2 con i dischi di formato avanzato.</p></li>
<li><p>Windows Server 2008 R2 con Service Pack 1 (SP1) ed Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 e versioni successive supporta i dischi con settore da 4 kilobyte (KB) nativi e i dischi 512e. Il supporto richiede che tutte le copie di un database si trovino sullo stesso tipo di disco fisico. Ad esempio, non è supportata una configurazione che ospita una copia di un determinato database su un settore del disco da 512 byte e un'altra copia dello stesso database su un disco 512e o un disco 4K.</p>
<p>Procedura consigliata: La cache in scrittura del disco dei dati fisici deve essere disabilitata quando viene utilizzata senza un gruppo di continuità.</p></td>
</tr>
<tr class="odd">
<td><p>Fibre Channel</p></td>
<td><p>Fibre Channel indica un'interfaccia elettrica utilizzata per collegare i dischi alle reti SAN basate su Fibre Channel. I dischi Fibre Channel sono disponibili in una vasta gamma di velocità e capacità.</p>
<p>In generale, scegliere i dischi Fibre Channel per l'archiviazione delle cassette postali di Exchange 2013 quando si devono soddisfare i seguenti requisiti:</p>
<ul>
<li><p>Capacità moderata</p></li>
<li><p>Elevate prestazioni</p></li>
<li><p>Connettività SAN</p></li>
</ul></td>
<td><p>Supportati: dischi con settore da 512 byte per Windows Server 2008 e Windows Server 2008 R2. Sono inoltre supportati dischi 512e per Windows Server 2008 R2 con quanto indicato di seguito:</p>
<ul>
<li><p>Aggiornamento rapido descritto nell'<a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">articolo 982018 della Microsoft Knowledge Base</a> È disponibile un aggiornamento che migliora la compatibilità di Windows 7 e Windows Server 2008 R2 con i dischi di formato avanzato.</p></li>
<li><p>Windows Server 2008 R2 con Service Pack 1 (SP1) ed Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 e versioni successive supporta i dischi con settore da 4 kilobyte (KB) nativi e i dischi 512e. Il supporto richiede che tutte le copie di un database si trovino sullo stesso tipo di disco fisico. Ad esempio, non è supportata una configurazione che ospita una copia di un determinato database su un settore del disco da 512 byte e un'altra copia dello stesso database su un disco 512e o un disco 4K.</p>
<p>Procedura consigliata: La cache in scrittura del disco dei dati fisici deve essere disabilitata quando viene utilizzata senza un gruppo di continuità.</p></td>
</tr>
<tr class="even">
<td><p>Unità SSD (disco flash)</p></td>
<td><p>Un'unità SSD è un dispositivo di archiviazione dei dati che utilizza la memoria a stato solido per archiviare i dati permanenti. Un'unità SSD emula un'interfaccia dell'unità disco rigido. I dischi SSD sono disponibili in una vasta gamma di velocità (diverse prestazioni I/O) e capacità.</p>
<p>In generale, scegliere i dischi SSD per l'archiviazione delle cassette postali di Exchange 2013 quando si devono soddisfare i seguenti requisiti:</p>
<ul>
<li><p>Capacità insufficiente</p></li>
<li><p>Prestazioni estremamente elevate</p></li>
</ul></td>
<td><p>Supportati: dischi con settore da 512 byte per Windows Server 2008 e Windows Server 2008 R2. Sono inoltre supportati dischi 512e per Windows Server 2008 R2 con quanto indicato di seguito:</p>
<ul>
<li><p>Aggiornamento rapido descritto nell'<a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">articolo 982018 della Microsoft Knowledge Base</a> È disponibile un aggiornamento che migliora la compatibilità di Windows 7 e Windows Server 2008 R2 con i dischi di formato avanzato.</p></li>
<li><p>Windows Server 2008 R2 con Service Pack 1 (SP1) ed Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 e versioni successive supporta i dischi con settore da 4 kilobyte (KB) nativi e i dischi 512e. Il supporto richiede che tutte le copie di un database si trovino sullo stesso tipo di disco fisico. Ad esempio, non è supportata una configurazione che ospita una copia di un determinato database su un settore del disco da 512 byte e un'altra copia dello stesso database su un disco 512e o un disco 4K.</p>
<p>Procedura consigliata: La cache in scrittura del disco dei dati fisici deve essere disabilitata quando viene utilizzata senza un gruppo di continuità.</p>
<p>Di solito, i server Cassette postali di Exchange 2013 non richiedono le caratteristiche relative alle prestazioni dell'unità di archiviazione SSD.</p></td>
</tr>
</tbody>
</table>


## Fattori da considerare quando si scelgono i tipi di disco

È necessario tenere in considerazione diversi fattori nella scelta dei dischi per l'archiviazione di Exchange 2013. Il disco corretto è quello che ha un giusto rapporto tra prestazioni (sia sequenziali che casuali), capacità, affidabilità, consumo di energia e costi. Nella tabella seguente relativa ai tipi di disco fisico supportati vengono fornite informazioni utili per la scelta del disco.

Da delle prestazioni prospettiva using dischi più lenti e di grandi dimensioni per archiviazione di Exchange è necessario, è necessario purché i dischi possono mantenere una media di lettura e scrittura latenza di 20 ms o meno sotto carico.

### Fattori nella scelta del tipo di disco

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Velocità disco (RPM)</th>
<th>Form factor disco</th>
<th>Interfaccia o trasporto</th>
<th>Capacità</th>
<th>Prestazioni I/O casuali</th>
<th>Prestazioni I/O sequenziali</th>
<th>Risparmio energetico</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5,400</p></td>
<td><p>2.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>Sufficiente</p></td>
<td><p>Scadente</p></td>
<td><p>Scadente</p></td>
<td><p>Eccellente</p></td>
</tr>
<tr class="even">
<td><p>5,400</p></td>
<td><p>3.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>Eccellente</p></td>
<td><p>Scadente</p></td>
<td><p>Scadente</p></td>
<td><p>Sopra la media</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>2.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>Sufficiente</p></td>
<td><p>Sufficiente</p></td>
<td><p>Sufficiente</p></td>
<td><p>Eccellente</p></td>
</tr>
<tr class="even">
<td><p>7,200</p></td>
<td><p>2.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Sufficiente</p></td>
<td><p>Sufficiente</p></td>
<td><p>Sopra la media</p></td>
<td><p>Eccellente</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>3.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>Eccellente</p></td>
<td><p>Sufficiente</p></td>
<td><p>Sopra la media</p></td>
<td><p>Sopra la media</p></td>
</tr>
<tr class="even">
<td><p>7,200</p></td>
<td><p>3.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Eccellente</p></td>
<td><p>Sufficiente</p></td>
<td><p>Sopra la media</p></td>
<td><p>Sopra la media</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>3.5-inch</p></td>
<td><p>Fibre Channel</p></td>
<td><p>Eccellente</p></td>
<td><p>Sufficiente</p></td>
<td><p>Sopra la media</p></td>
<td><p>Sufficiente</p></td>
</tr>
<tr class="even">
<td><p>10,000</p></td>
<td><p>2.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Sotto la media</p></td>
<td><p>Eccellente</p></td>
<td><p>Sopra la media</p></td>
<td><p>Sopra la media</p></td>
</tr>
<tr class="odd">
<td><p>10,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>Sufficiente</p></td>
<td><p>Sufficiente</p></td>
<td><p>Sopra la media</p></td>
<td><p>Sopra la media</p></td>
</tr>
<tr class="even">
<td><p>10,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Sufficiente</p></td>
<td><p>Sopra la media</p></td>
<td><p>Sopra la media</p></td>
<td><p>Sotto la media</p></td>
</tr>
<tr class="odd">
<td><p>10,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>Fibre Channel</p></td>
<td><p>Sufficiente</p></td>
<td><p>Sopra la media</p></td>
<td><p>Sopra la media</p></td>
<td><p>Sotto la media</p></td>
</tr>
<tr class="even">
<td><p>15,000</p></td>
<td><p>2.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Scadente</p></td>
<td><p>Eccellente</p></td>
<td><p>Eccellente</p></td>
<td><p>Sufficiente</p></td>
</tr>
<tr class="odd">
<td><p>15,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Sufficiente</p></td>
<td><p>Eccellente</p></td>
<td><p>Eccellente</p></td>
<td><p>Sotto la media</p></td>
</tr>
<tr class="even">
<td><p>15,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>Fibre Channel</p></td>
<td><p>Sufficiente</p></td>
<td><p>Eccellente</p></td>
<td><p>Eccellente</p></td>
<td><p>Scadente</p></td>
</tr>
<tr class="odd">
<td><p>SSD: classe Enterprise</p></td>
<td><p>Non applicabile</p></td>
<td><p>SATA, Serial Attached SCSI, Fibre Channel</p></td>
<td><p>Scadente</p></td>
<td><p>Eccellente</p></td>
<td><p>Eccellente</p></td>
<td><p>Eccellente</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Procedure consigliate per le configurazioni di archiviazione supportate

In questa sezione vengono illustrate le procedure consigliate per le configurazioni del controller dell'array e del disco supportate.

RAID (Redundant Array of Independent Disks) è spesso utilizzato sia per migliorare le prestazioni dei singoli dischi (striping dei dati in più dischi) che per fornire la protezione da errori del disco. Con le innovazioni nell'alta disponibilità di Exchange 2013, RAID non è più un componente necessario per l'archiviazione di Exchange 2013. Tuttavia, RAID è ancora un componente fondamentale dell'architettura di archiviazione di Exchange 2013 per i server autonomi così come per le soluzioni che necessitano di una tolleranza per gli errori di archiviazione.

**Sistema operativo, sistema o volume di paging**

La configurazione consigliata per un sistema operativo, sistema o volume di paging prevede l'uso della tecnologia RAID per proteggere questo tipo di dati. La configurazione RAID consigliata è RAID-1 o RAID-1/0, ma sono supportati tutti i tipi di RAID.

**Volumi separati per il registro e il database delle cassette postali**

Se si sta distribuendo un'architettura di ruolo server Cassette postali autonomo, la tecnologia RAID è necessaria per i volumi del database delle cassette postali e del registro. La configurazione RAID consigliata per i volumi delle cassette postali è RAID-1/0, soprattutto se si utilizzano dischi da 5,4K o 7,2K, ma sono supportati tutti i tipi di RAID. Per i volumi del registro, la configurazione RAID consigliata è RAID-1 o RAID-1/0.

Quando si utilizzano configurazioni RAID-5 o RAID-6 per il sistema operativo, il paging o i volumi di dati di Exchange, tenere presenti le seguenti considerazioni:

  - Le configurazioni RAID-5, incluse varianti come RAID-50 e RAID-51, devono includere massimo di 7 dischi per gruppo di array e lo scrubbing ad alta priorità e l'analisi della superficie del controller di array devono essere abilitati.

  - Nelle configurazioni RAID-6 lo scrubbing ad alta priorità e l'analisi della superficie del controller di array devono essere abilitati.

Anche se JBOD è supportato in architetture ad alta disponibilità con 3 o più copie di database altamente disponibili, dal momento che i volumi del database delle cassette postali e del registro sono separati, non è consigliato.

**Database delle cassette postali e registro nello stesso volume**

Questo tipo di collocazione non è consigliata nelle architetture autonome. Nelle architetture ad alta disponibilità, esistono due possibilità per questo scenario:

1.  Singolo database per volume

2.  Più database per volume

**Singolo database per volume**

Dalla prospettiva di Exchange, JBOD implica che il database e i registri associati sono archiviati in un unico disco. Per la distribuzione su JBOD, è necessario distribuire minimo di tre copie altamente disponibili del database. L'utilizzo di un unico disco costituisce un unico punto di errore perché, quando si verifica un errore del disco, si perde la copia del database che risiede nel disco. La presenza di almeno tre copie del database garantisce la tolleranza di errore perché implica la disponibilità di altre due copie nel caso in cui si verifichi un errore di una copia (o di un disco). Tuttavia, la presenza di tre copie altamente disponibili del database, così come l'utilizzo di copie ritardate del database, può influire sulla progettazione dell'archiviazione. Nella tabella seguente vengono visualizzate le linee guida per le considerazioni su RAID o JBOD.

### Considerazioni su RAID o JBOD

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Server di datacenter</th>
<th>Due copie altamente disponibili (totale)</th>
<th>Tre copie altamente disponibili (totale)</th>
<th>Due o più copie altamente disponibili per datacenter</th>
<th>Una copia ritardata</th>
<th>Due o più copie ritardate per datacenter</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Server di datacenter principale</p></td>
<td><p>RAID</p></td>
<td><p>RAID o JBOD (2 copie)</p></td>
<td><p>RAID o JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID o JBOD</p></td>
</tr>
<tr class="even">
<td><p>Server di datacenter secondario</p></td>
<td><p>RAID</p></td>
<td><p>RAID (1 copia)</p></td>
<td><p>RAID o JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID o JBOD</p></td>
</tr>
</tbody>
</table>


Per la distribuzione su JBOD con i server di datacenter principali, sono necessarie tre o più copie ad alta disponibilità del database all'interno del DAG. Se si mischiano le copie ritardate sullo stesso server che ospita le copie altamente disponibili del database (ad esempio, non utilizzando i server dedicati alle copie ritardate del database), sono necessarie almeno due copie ritardate del database.

Affinché i server di datacenter secondari utilizzino JBOD, è necessario disporre di almeno due copie altamente disponibili del database nel datacenter secondario. La perdita di una copia nel datacenter secondario non comporterà la richiesta di un reseeding attraverso la rete WAN o la presenza di un unico punto di errore nel caso in cui il datacenter secondario venga attivato. Se si mischiano le copie ritardate del database sullo stesso server che ospita le copie altamente disponibili del database (ad esempio, non utilizzando i server dedicati alle copie ritardate del database), sono necessarie almeno due copie ritardate del database.

Per i server dedicati alle copie ritardate del database, è necessario disporre di almeno due copie ritardate del database all'interno di un datacenter per utilizzare JBOD. In caso contrario, la perdita del disco comporta la perdita della copia ritardata del database, così come la perdita del meccanismo di protezione.

**Più database per volume**

Più database per volume è un nuovo scenario disponibile in Exchange 2013 che consente di mischiare copie attive e passive (incluse le copie ritardate) in un solo disco, permettendo un migliore utilizzo del disco. Tuttavia, per distribuire le copie in questo modo, è necessario abilitare la riproduzione automatica del file di registro della copia ritardata. Nella tabella seguente vengono mostrate le linee guida per le considerazioni su JBOD per più database per volume.

### Considerazioni su JBOD

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Server di datacenter</th>
<th>3 o più copie (totale)</th>
<th>Due o più copie per datacenter</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Server di datacenter principale</p></td>
<td><p>JBOD</p></td>
<td><p>JBOD</p></td>
</tr>
<tr class="even">
<td><p>Server di datacenter secondario</p></td>
<td><p>N/D</p></td>
<td><p>JBOD</p></td>
</tr>
</tbody>
</table>


Nella tabella seguente vengono fornite indicazioni sulle configurazioni dell'array di archiviazione per Exchange 2013.

### Tipi di RAID supportati per il ruolo del server Cassette postali di Exchange 2013

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di RAID</th>
<th>Descrizione</th>
<th>Procedura supportata o consigliata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dimensioni di striping RAID dell'array di dischi (KB)</p></td>
<td><p>Le dimensioni di striping rappresentano l'unità della distribuzione dei dati in un gruppo RAID per disco. Le dimensioni di striping sono definite anche <em>dimensioni del blocco</em>.</p></td>
<td><p>Procedura consigliata: un minimo di 256 KB. Seguire le procedure consigliate del fornitore di archiviazione.</p></td>
</tr>
<tr class="even">
<td><p>Impostazioni della cache per l'array di archiviazione</p></td>
<td><p>Le impostazioni della cache vengono fornite da un controller dell'array con cache supportato da batteria.</p></td>
<td><p>Procedura consigliata: il 100% cache in scrittura (batteria o cache a flash) per i controller di archiviazione DAS in uno una configurazione RAID o JBOD. il 75% cache in scrittura, al 25% lettura cache (batteria o cache sottoposti a flash) per altri tipi di soluzioni di archiviazione, ad esempio nome alternativo del SOGGETTO. Se al fornitore SAN include diverse procedure consigliate per la configurazione della cache della propria piattaforma, seguire le indicazioni del fornitore SAN.</p></td>
</tr>
<tr class="odd">
<td><p>Cache in scrittura del disco fisico</p></td>
<td><p>Le impostazioni per la cache sono su ciascun disco.</p></td>
<td><p>Procedura supportata: La cache in scrittura del disco dei dati fisici deve essere disabilitata quando viene utilizzata senza un gruppo di continuità.</p></td>
</tr>
</tbody>
</table>


Nella tabella seguente vengono fornite indicazioni sulla scelta dei file di database e di registro.

### Scelta del file di registro e di database per il ruolo del server Cassette postali di Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Opzioni del file di database e di registro</th>
<th>Descrizione</th>
<th>Autonomo: procedura supportata o consigliata</th>
<th>Alta disponibilità: procedura supportata o consigliata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Posizionamento del file: isolamento del database per registro</p></td>
<td><p>L'isolamento del database per registro si riferisce al posizionamento dei registri e del file di database dallo stesso database delle cassette postali a diversi volumi supportati da diversi dischi fisici.</p></td>
<td><p>Procedura consigliata: Per il ripristino, spostare i registri e il file (.edb) del database dallo stesso database a diversi volumi supportati da diversi dischi fisici.</p></td>
<td><p>Procedura supportata: Isolamento dei database e dei registri non necessario.</p></td>
</tr>
<tr class="even">
<td><p>Posizionamento del file: file di database per volume</p></td>
<td><p>I file di database per volume si riferiscono alla modalità di distribuzione dei file di database all'interno o tra i volumi del disco.</p></td>
<td><p>Procedura consigliata: in base alla metodologia di backup.</p></td>
<td><p>Procedura supportata: Utilizzando JBOD, si crea un volume singolo con directory separate per i database e per i file di registro.</p></td>
</tr>
<tr class="odd">
<td><p>Posizionamento del file: flussi di registrazione per volume</p></td>
<td><p>I flussi di registrazione per volume si riferiscono alla modalità di distribuzione dei file di registro del database all'interno o tra i volumi del disco.</p></td>
<td><p>Procedura consigliata: in base alla metodologia di backup.</p></td>
<td><p>Procedura supportata: Utilizzando JBOD, si crea un volume singolo con directory separate per i database e per i file di registro.</p>
<p>Procedura consigliata: Utilizzando JBOD, è possibile utilizzare più database per volume.</p></td>
</tr>
<tr class="even">
<td><p>Dimensione del database</p></td>
<td><p>Le dimensioni del database si riferiscono a quelle del file (.edb) di database dei dischi.</p></td>
<td><p>Procedura supportata: circa 16 terabyte.</p>
<p>Procedura consigliata:</p>
<ul>
<li><p>un massimo di 200 gigabyte (GB).</p></li>
<li><p>120% della dimensione massima del database calcolata.</p></li>
</ul></td>
<td><p>Procedura supportata: circa 16 terabyte.</p>
<p>Procedura consigliata:</p>
<ul>
<li><p>un massimo di 2 terabyte.</p></li>
<li><p>120% della dimensione massima del database calcolata.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Metodo di troncamento del registro</p></td>
<td><p>Il metodo di troncamento del registro indica il processo per il troncamento e l'eliminazione dei precedenti file di registro del database. Sono disponibili due metodi:</p>
<ul>
<li><p>La registrazione circolare, in cui Exchange elimina i registri.</p></li>
<li><p>Il troncamento del registro che si verifica dopo un backup completo o incrementale del Servizio Copia shadow del volume.</p></li>
</ul></td>
<td><p>Procedura consigliata:</p>
<ul>
<li><p>utilizzare i backup per il troncamento del registro (ad esempio, registrazione circolare disabilitata).</p></li>
<li><p>Tre giorni per la generazione dei registri.</p></li>
</ul></td>
<td><p>Procedura consigliata:</p>
<ul>
<li><p>abilitare la registrazione circolare per le distribuzioni che utilizzano le funzionalità di protezione dei dati nativi di Exchange.</p></li>
<li><p>Tre giorni in più per la generazione dei registri rispetto all'impostazione dell'intervallo di riesecuzione.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Nella tabella seguente vengono fornite informazioni sui tipi di disco di Windows.

### Tipi di disco di Windows per il ruolo del server Cassette postali di Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di disco di Windows</th>
<th>Descrizione</th>
<th>Autonomo: procedura supportata o consigliata</th>
<th>Alta disponibilità: procedura supportata o consigliata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Disco di base</p></td>
<td><p>Un disco inizializzato per l'archiviazione di base è definito disco di base. Un disco di base contiene volumi di base, quali partizioni primarie, partizioni estese e unità logiche.</p></td>
<td><p>Procedura supportata.</p>
<p>Procedura consigliata: utilizzare i dischi di base.</p></td>
<td><p>Procedura supportata.</p>
<p>Procedura consigliata: utilizzare i dischi di base.</p></td>
</tr>
<tr class="even">
<td><p>Disco dinamico</p></td>
<td><p>Un disco inizializzato per l'archiviazione dinamica è definito disco dinamico. Un disco dinamico contiene volumi dinamici, quali volumi semplici, volumi con spanning, volumi con striping, volumi con mirroring e volumi RAID-5.</p></td>
<td><p>Procedura supportata.</p></td>
<td><p>Procedura supportata.</p></td>
</tr>
</tbody>
</table>


Nella tabella seguente vengono fornite informazioni sulle configurazioni del volume.

### Configurazioni del volume per il ruolo del server Cassette postali di Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Configurazione del volume</th>
<th>Descrizione</th>
<th>Autonomo: procedura supportata o consigliata</th>
<th>Alta disponibilità: procedura supportata o consigliata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GPT (tabella di partizione GUID)</p></td>
<td><p>GPT è un'architettura del disco che si espande sullo schema di partizione precedente del record di avvio principale (MBR). Le dimensioni massime della partizione formattata NTFS è di 256 terabyte.</p></td>
<td><p>Procedura supportata.</p>
<p>Procedura consigliata: utilizzare le partizioni GPT.</p></td>
<td><p>Procedura supportata.</p>
<p>Procedura consigliata: utilizzare le partizioni GPT.</p></td>
</tr>
<tr class="even">
<td><p>MBR</p></td>
<td><p>MBR, o settore di partizione, indica il settore di avvio da 512 byte, cioè il primo settore (Settore 0 di LBA) di un dispositivo di archiviazione dei dati partizionati, come un disco rigido. Le dimensioni massime della partizione formattata NTFS è di 2 terabyte.</p></td>
<td><p>Procedura supportata.</p></td>
<td><p>Procedura supportata.</p></td>
</tr>
<tr class="odd">
<td><p>Allineamento tra le partizioni</p></td>
<td><p>Per allineamento tra le partizioni si intende l'allineamento delle partizioni nei limiti del settore per ottenere prestazioni ottimali.</p></td>
<td><p>Procedura supportata: Il valore predefinito in Windows Server 2008 R2 e Windows Server 2012 è 1 megabyte (MB).</p></td>
<td><p>Procedura supportata: Il valore predefinito in Windows Server 2008 R2 e Windows Server 2012 è 1 MB.</p></td>
</tr>
<tr class="even">
<td><p>Percorso volume</p></td>
<td><p>Percorso volume si riferisce alla modalità di accesso a un volume.</p></td>
<td><p>Procedura supportata: lettera di unità o punto di montaggio.</p>
<p>Procedura consigliata: il volume host del punto di montaggio deve disporre di RAID.</p></td>
<td><p>Procedura supportata: lettera di unità o punto di montaggio.</p>
<p>Procedura consigliata: il volume host del punto di montaggio deve essere abilitato a RAID.</p></td>
</tr>
<tr class="odd">
<td><p>File system</p></td>
<td><p>Il file system indica un metodo per l'archiviazione e l'organizzazione dei file del computer e dei dati contenuti per facilitarne l'individuazione e l'accesso.</p></td>
<td><p>Procedura supportata: NTFS e ReFS.</p></td>
<td><p>Supportato: NTFS e ReFS.</p></td>
</tr>
<tr class="even">
<td><p>Deframmentazione NTFS</p></td>
<td><p>Deframmentazione NTFS è un processo che riduce il livello di frammentazione nei file system di Windows. È in grado di organizzare il contenuto del disco in modo da archiviare parti di ciascun file in modo contiguo e ravvicinato.</p></td>
<td><p>Procedura supportata.</p>
<p>Procedura consigliata: Non necessario e non consigliato. Su Windows Server 2012, si consiglia anche di disabilitare l'ottimizzazione automatica del disco e la funzionalità di deframmentazione.</p></td>
<td><p>Procedura supportata.</p>
<p>Procedura consigliata: Non necessario e non consigliato. Su Windows Server 2012, si consiglia anche di disabilitare l'ottimizzazione automatica del disco e la funzionalità di deframmentazione.</p></td>
</tr>
<tr class="odd">
<td><p>Dimensione unità di allocazione NTFS</p></td>
<td><p>Dimensione unità di allocazione NTFS indica la quantità minima di spazio su disco che può essere allocata per memorizzare un file.</p></td>
<td><p>Procedura supportata: tutte le dimensioni delle unità di allocazione.</p>
<p>Procedura consigliata: 64 KB per i volumi dei file .edb e di registro.</p></td>
<td><p>Procedura supportata: tutte le dimensioni delle unità di allocazione.</p>
<p>Procedura consigliata: 64 KB per i volumi dei file .edb e di registro.</p></td>
</tr>
<tr class="even">
<td><p>Compressione NTFS</p></td>
<td><p>Compressione NTFS è il processo di riduzione delle dimensioni effettive di un file archiviato sul disco rigido.</p></td>
<td><p>Procedura supportata: non supportata per i file di registro o database di Exchange.</p></td>
<td><p>Procedura supportata: non supportata per i file di registro o database di Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>NTFS Encrypting File System (EFS)</p></td>
<td><p>EFS consente agli utenti di crittografare singoli file, cartelle o unità di dati. Dal momento che EFS fornisce un metodo di crittografia avanzata mediante algoritmi standard e crittografia a chiave pubblica, i file crittografati rimangono riservati anche nel caso in cui venga superato il sistema di sicurezza.</p></td>
<td><p>Procedura supportata: non supportata per i file di registro o database di Exchange.</p></td>
<td><p>non supportata per i file di registro o database di Exchange.</p></td>
</tr>
<tr class="even">
<td><p>Windows BitLocker (crittografia del volume)</p></td>
<td><p>Windows BitLocker indica una funzionalità di protezione dei dati in Windows Server 2008. BitLocker protegge dal furto dei dati o dall'esposizione su computer smarriti o rubati e offre una modalità più sicura di eliminazione dei dati quando i computer vengono rimossi.</p></td>
<td><p>Procedura supportata: tutti i file di registro e database di Exchange.</p></td>
<td><p>Procedura supportata: Tutti i file di registro e database di Exchange. I cluster di failover di Windows necessitano di Windows Server 2008 R2 o Windows Server 2008 R2 SP1 e della seguente hotfix: <a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=2446607">Impossibile abilitare BitLocker su un volume disco in Windows Server 2008 R2 se il computer è un nodo di cluster di failover</a>. I volumi di Exchange con BitLocker abilitato non sono supportati sui cluster di failover di Windows con versioni precedenti di Windows.</p>
<p>Per ulteriori informazioni sulla crittografia BitLocker Windows 7, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=220898">BitLocker Drive Encryption in Windows 7: domande frequenti</a>.</p></td>
</tr>
<tr class="odd">
<td><p>SMB (Server Message Block) 3.0</p></td>
<td><p>Il protocollo SMB (Server Message Block) è un protocollo per la condivisione dei file in rete (come TCP/IP o altri protocolli di rete) che consente alle applicazioni su un computer di accedere a file e risorse su un server remoto. Consente inoltre alle applicazioni di comunicare con qualsiasi programma server configurato per ricevere le richieste di client SMB. Windows Server 2012 introduce la nuova versione 3.0 del protocollo SMB con le seguenti funzionalità:</p>
<ul>
<li><p>Failover trasparente SMB</p></li>
<li><p>Scalabilità SMB</p></li>
<li><p>Multicanale SMB</p></li>
<li><p>Diretto SMB</p></li>
<li><p>Crittografia SMB</p></li>
<li><p>VSS per condivisioni di file SMB</p></li>
<li><p>Leasing directory SMB</p></li>
<li><p>PowerShell SMB</p></li>
</ul></td>
<td><p>Supporto limitato. Lo scenario supportato è una distribuzione hardware virtualizzata in cui i dischi si trovano su dischi rigidi virtuali in una condivisione SMB 3.0. Questi dischi rigidi virtuali comunicano con l'host tramite hypervisor. Per ulteriori informazioni, vedere <a href="exchange-2013-virtualization-exchange-2013-help.md">Virtualizzazione di Exchange 2013</a>.</p></td>
<td><p>Supporto limitato. Lo scenario supportato è una distribuzione hardware virtualizzata in cui i dischi si trovano su dischi rigidi virtuali in una condivisione SMB 3.0. Questi dischi rigidi virtuali comunicano con l'host tramite hypervisor. Per ulteriori informazioni, vedere <a href="exchange-2013-virtualization-exchange-2013-help.md">Virtualizzazione di Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Spazi di archiviazione</p></td>
<td><p>Spazi di archiviazione è una nuova soluzione di archiviazione che offre funzionalità di virtualizzazione per Windows Server 2012. Spazi di archiviazione consentono di organizzare i dischi fisici in un pool di archiviazione, che può essere facilmente espanse semplicemente aggiungendo dischi. Questi dischi possono essere connessi tramite USB, SATA o SAS. Utilizza anche dischi virtuali (spazi), si comportano come dischi fisici, con associato potenti funzionalità, ad esempio il provisioning di tipo sottile, nonché la resilienza a errori dei supporti fisici sottostanti. Per ulteriori informazioni su spazi di archiviazione, vedere <a href="https://technet.microsoft.com/en-us/library/hh831739.aspx">Cenni preliminari su spazi di archiviazione</a>.</p></td>
<td><p>Procedura supportata. In questo argomento vengono riportati alcuni limiti per i dischi fisici.</p></td>
<td><p>Procedura supportata. In questo argomento vengono riportati alcuni limiti per i dischi fisici.</p></td>
</tr>
<tr class="odd">
<td><p>Resilient File System (ReFS)</p></td>
<td><p>ReFS è un sistema di file appena reengineering per Windows Server 2012 basati su basi del file system NTFS. ReFS mantiene elevato grado di garantire la compatibilità con NTFS fornendo le tecniche di verifica e correzione automatica dei dati avanzata e su come un'integrati resilienza end-to-end di danneggiamenti soprattutto se utilizzato con la funzionalità di spazio di archiviazione. Per ulteriori informazioni su ReFS, vedere <a href="https://technet.microsoft.com/en-us/library/hh831724.aspx">Panoramica di sistema resiliente File</a>.</p></td>
<td><p>È supportata per i volumi che contiene i file di database di Exchange, i file di registro e file di indicizzazione del contenuto. Se la distribuzione in Windows Server 2012, verificare che i hotfix seguenti siano installati in Windows Server 2012:</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Windows 8 e Windows Server 2012 aggiornamento cumulativo: aprile 2013</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">Servizio disco virtuale o applicazioni che utilizzano l'arresto anomalo del servizio disco virtuale o si bloccano in Windows Server 2012</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">Computer basato su Windows Server 2012 o Windows 8 si blocca quando si esegue il comando 'directory' su un volume ReFS</a></p></li>
</ul>
<p>ReFS non è supportata per i volumi del sistema operativo.</p>
<p>Procedura consigliata: caratteristiche di integrità dei dati devono essere disabilitate per i file di database (. edb) di Exchange o volume che ospita i file.</p></td>
<td><p>È supportata per i volumi che contiene i file di database di Exchange, i file di registro e file di indicizzazione del contenuto. Se la distribuzione in Windows Server 2012, verificare che i hotfix seguenti siano installati in Windows Server 2012:</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Windows 8 e Windows Server 2012 aggiornamento cumulativo: aprile 2013</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">Servizio dischi virtuali o applicazioni che utilizzano l'arresto anomalo servizio dischi virtuali o si bloccano in Windows Server 2012</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">Computer basato su Windows Server 2012 o Windows 8 si blocca quando si esegue il comando 'directory' sur un volume ReFS</a></p></li>
</ul>
<p>ReFS non è supportata per i volumi del sistema operativo.</p>
<p>Procedura consigliata: caratteristiche di integrità dei dati devono essere disabilitate per i file del database (. edb) di Exchange o un volume che ospita i file.</p></td>
</tr>
<tr class="even">
<td><p>Deduplicazione dati</p></td>
<td><p>La deduplicazione dati è una nuova tecnica per l'ottimizzazione dell'utilizzo degli archivi in Windows Server 2012; è un metodo attraverso il quale viene trovata e rimossa la deduplicazione dei dati senza compromettere la loro affidabilità e integrità. L'obiettivo è quello di archiviare più dati in meno spazio tramite la segmentazione dei file in piccoli blocchi di dimensioni variabili, identificare i blocchi deduplicati e mantenere per ogni blocco una sola copia. Le copie ridondanti dei blocchi vengono sostituite da un riferimento alla singola copia, i blocchi vengono organizzati in file contenitore e i contenitori vengono compressi per una ulteriore ottimizzazione dello spazio.</p></td>
<td><p>La deduplicazione non è supportata per i file di database di Exchange. Nota: È possibile utilizzarla per i file di database di Exchange non in linea (utilizzati come backup o archivi).</p></td>
<td><p>La deduplicazione non è supportata per i file di database di Exchange. Nota: È possibile utilizzarla per i file di database di Exchange non in linea (utilizzati come backup o archivi).</p></td>
</tr>
</tbody>
</table>


Inizio pagina


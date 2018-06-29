---
title: 'Gruppi di disponibilità del database di monitoraggio: Exchange 2013 Help'
TOCTitle: Gruppi di disponibilità del database di monitoraggio
ms:assetid: f5bdfd6e-e93c-4d96-8bc2-548750d51930
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351258(v=EXCHG.150)
ms:contentKeyID: 50482071
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gruppi di disponibilità del database di monitoraggio

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

È possibile utilizzare i dettagli in questo argomento per monitorare l'integrità e lo stato delle copie del database delle cassette postali per gruppi di disponibilità del database (DAG) per la raccolta delle informazioni di diagnostica e per configurare lo spazio su disco insufficiente soglia di monitoraggio.

## Cmdlet MailboxDatabaseCopyStatus

È possibile utilizzare il cmdlet [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/it-it/library/dd298044\(v=exchg.150\)) per visualizzare le informazioni sullo stato delle copie del database delle cassette postali. Questo cmdlet consente di visualizzare informazioni su tutte le copie di un particolare database, informazioni su una specifica copia di un database su un server specifico, oppure informazioni su tutte le copie del database su un server. Nella seguente tabella sono descritti i possibili valori per lo stato di una copia del database delle cassette postali.

### Stato della copia del database

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Stato della copia del database</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Failed</p></td>
<td><p>La copia del database delle cassette postali è nello stato Failed quando non è stata sospesa e non è in grado di copiare o rieseguire i file di registro. Se lo stato è Failed e la copia non è sospesa, il sistema controlla periodicamente se il problema che ha causato l'impostazione dello stato Failed per la copia è stato risolto. Una volta rilevata la risoluzione del problema, a condizione che non vi siano altri problemi, lo stato della copia diventa automaticamente Healthy.</p></td>
</tr>
<tr class="even">
<td><p>Seeding</p></td>
<td><p>La copia del database delle cassette postali, l'indice del contenuto per la copia del database delle cassette postali o entrambi gli elementi sono sottoposti a seeding. Al completamento del seeding, lo stato della copia cambia in Initializing.</p></td>
</tr>
<tr class="odd">
<td><p>SeedingSource</p></td>
<td><p>La copia del database delle cassette postali è utilizzata come origine per l'operazione di seeding della copia del database.</p></td>
</tr>
<tr class="even">
<td><p>Suspended</p></td>
<td><p>La copia del database delle cassette postali è nello stato Suspended a seguito della sospensione manuale della copia del database da parte di un amministratore che ha eseguito il cmdlet <strong>Suspend-MailboxDatabaseCopy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Healthy</p></td>
<td><p>La copia del database delle cassette postali esegue correttamente la copia e la riesecuzione dei file di registro, oppure ha completato correttamente la copia e la riesecuzione di tutti i file di registro disponibili.</p></td>
</tr>
<tr class="even">
<td><p>ServiceDown</p></td>
<td><p>Il servizio Replica di Microsoft Exchange non è disponibile o è in esecuzione sul server che ospita la copia del database delle cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>Initializing</p></td>
<td><p>La copia del database delle cassette postali è nello stato Initializing quando è stata creata una copia del database, quando il servizio Replica di Microsoft Exchange è in fase di avvio o è stato appena avviato, e durante le transizioni dallo stato Suspended, ServiceDown, Failed, Seeding, SinglePageRestore, LostWrite o Disconnected a un altro stato. Quando la copia è in questo stato, il sistema verifica che il database e il flusso di registro abbiano uno stato coerente. Nella maggior parte dei casi, lo stato della copia rimane Initializing per circa 15 secondi, ma in ogni caso non deve rimanere tale per più di 30 secondi.</p></td>
</tr>
<tr class="even">
<td><p>Resynchronizing</p></td>
<td><p>La copia del database delle cassette postali e i suoi file di registro vengono confrontati con la copia attiva del database per verificare eventuali divergenze tra le due copie. La copia rimane in questo stato fino a quando non sono state rilevate e risolte tutte le divergenze.</p></td>
</tr>
<tr class="odd">
<td><p>Mounted</p></td>
<td><p>La copia attiva è online e sta accettando le connessioni dei client. Solo la copia attiva della copia del database delle cassette postali può assumere lo stato Mounted.</p></td>
</tr>
<tr class="even">
<td><p>Dismounted</p></td>
<td><p>La copia attiva è offline e non sta accettando le connessioni dei client. Solo la copia attiva della copia del database delle cassette postali può assumere lo stato Dismounted.</p></td>
</tr>
<tr class="odd">
<td><p>Mounting</p></td>
<td><p>La copia attiva sta per diventare online e non sta ancora accettando le connessioni dei client. Solo la copia attiva della copia del database delle cassette postali può assumere lo stato Mounting.</p></td>
</tr>
<tr class="even">
<td><p>Dismounting</p></td>
<td><p>La copia attiva sta per diventare offline e sta terminando le connessioni dei client. Solo la copia attiva della copia del database delle cassette postali può assumere lo stato Dismounting.</p></td>
</tr>
<tr class="odd">
<td><p>DisconnectedAndHealthy</p></td>
<td><p>La copia del database delle cassette postali non è più connessa alla copia del database attiva ed era nello stato Healthy quando si è verificata la perdita della connessione. Questo stato rappresenta la copia del database rispetto alla connettività alla copia del database di origine. Può essere segnalato durante gli errori di rete del gruppo di disponibilità del database tra la copia di origine e la copia del database di destinazione.</p></td>
</tr>
<tr class="even">
<td><p>DisconnectedAndResynchronizing</p></td>
<td><p>La copia del database delle cassette postali non è più connessa alla copia del database attiva ed era nello stato Resynchronizing quando si è verificata la perdita della connessione. Questo stato rappresenta la copia del database rispetto alla connettività alla copia del database di origine. Può essere segnalato durante gli errori di rete del gruppo di disponibilità del database tra la copia di origine e la copia del database di destinazione.</p></td>
</tr>
<tr class="odd">
<td><p>FailedAndSuspended</p></td>
<td><p>Gli stati Failed e Suspended sono stati impostati contemporaneamente dal sistema in quanto è stato rilevato un errore la cui risoluzione richiede esplicitamente l'intervento dell'amministratore. Un esempio è il caso in cui il sistema rileva una divergenza irreversibile tra il database delle cassette postali attivo e una copia del database. A differenza dello stato Failed, il sistema non controlla periodicamente se il problema è stato risolto e non esegue il ripristino automatico. Deve intervenire un amministratore per risolvere la causa dell'errore prima che la copia del database possa passare a uno stato di integrità.</p></td>
</tr>
<tr class="even">
<td><p>SinglePageRestore</p></td>
<td><p>Questo stato indica che sulla copia del database delle cassette postali si è verificata un'operazione di ripristino della singola pagina.</p></td>
</tr>
</tbody>
</table>


Il cmdlet **Get-MailboxDatabaseCopyStatus** restituisce, inoltre, i dettagli sulle reti di replica in uso, incluse *IncomingLogCopyingNetwork*, che viene restituita per le copie dei database passivi, e *OutgoingConnections*, che viene restituita per i database attivi che presentano più di una copia, nonché per eventuali copie di database utilizzate come origine per un'operazione di seeding del database. Le informazioni sulle connessioni in uscita vengono fornite per le copie di database che sono in replica modalità file. Le informazioni sulle connessioni in uscita non vengono fornite per le copie di database che sono in replica modalità blocco.

## Esempi di Get-MailboxDatabaseCopyStatus

Negli esempi riportati di seguito viene utilizzato il cmdlet **Get-MailboxDatabaseCopyStatus**. In ciascun esempio i risultati vengono inviati al cmdlet **Format-List** affinché siano visualizzati in formato elenco.

Con questo esempio vengono restituite le informazioni di stato per tutte le copie del database DB2.

    Get-MailboxDatabaseCopyStatus -Identity DB2 | Format-List

Con questo esempio viene restituito lo stato per tutte le copie del database sul server di cassette postali MBX2.

    Get-MailboxDatabaseCopyStatus -Server MBX2 | Format-List

Con questo esempio viene restituito lo stato per tutte le copie del database sul server di cassette postali locale.

    Get-MailboxDatabaseCopyStatus -Local | Format-List

Per ulteriori informazioni sull'uso del cmdlet **Get-MailboxDatabaseCopyStatus**, vedere [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/it-it/library/dd298044\(v=exchg.150\)).

## Cmdlet Test-ReplicationHealth

È possibile utilizzare il cmdlet [Test-ReplicationHealth](https://technet.microsoft.com/it-it/library/bb691314\(v=exchg.150\)) per visualizzare le informazioni sullo stato di replica continua delle copie del database delle cassette postali. Il cmdlet può essere utilizzato per controllare tutti gli aspetti dello stato di replica e riesecuzione per fornire una panoramica completa di uno specifico server di cassette postali in un gruppo di disponibilità del database.

Il cmdlet **Test-ReplicationHealth** è progettato per il monitoraggio preventivo della replica continua e della pipeline di replica continua, della disponibilità di Active Manager e dell'integrità e dello stato del Servizio cluster, del quorum e dei componenti di rete sottostanti. Può essere eseguito in locale o in modalità remota su qualsiasi server di cassette postali in un DAG. Il cmdlet **Test-ReplicationHealth** esegue i test elencati nella seguente tabella.

### Test del cmdlet Test-ReplicationHealth

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome del test</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ClusterService</p></td>
<td><p>Verifica che il Servizio cluster sia in esecuzione e raggiungibile sul membro del gruppo di disponibilità del database specificato, o sul server locale se non è specificato alcun membro del gruppo di disponibilità del database.</p></td>
</tr>
<tr class="even">
<td><p>ReplayService</p></td>
<td><p>Verifica che il servizio Replica di Microsoft Exchange sia in esecuzione e raggiungibile sul membro del gruppo di disponibilità del database specificato, o sul server locale se non è specificato alcun membro del gruppo di disponibilità del database.</p></td>
</tr>
<tr class="odd">
<td><p>ActiveManager</p></td>
<td><p>Verifica che l'istanza di Active Manager in esecuzione sul membro del gruppo di disponibilità del database specificato (o sul server locale se non è specificato alcun membro del gruppo di disponibilità del database) sia in un ruolo valido (primario, secondario o autonomo).</p></td>
</tr>
<tr class="even">
<td><p>TasksRpcListener</p></td>
<td><p>Verifica che la chiamata di procedura remota (RPC) delle attività sia in esecuzione e raggiungibile sul membro del gruppo di disponibilità del database specificato, o sul server locale se non è specificato alcun membro del gruppo di disponibilità del database.</p></td>
</tr>
<tr class="odd">
<td><p>TcpListener</p></td>
<td><p>Verifica che il listener della copia del registro TCP sia in esecuzione e raggiungibile sul membro del gruppo di disponibilità del database specificato, o sul server locale se non è specificato alcun membro del gruppo di disponibilità del database.</p></td>
</tr>
<tr class="even">
<td><p>ServerLocatorService</p></td>
<td><p>Verifica i processi client/server di Active Manager sui membri del gruppo di disponibilità del database e sul server Accesso client che esegue le ricerche in Active Directory e Active Manager per stabilire dove è attivo il database delle cassette postali di un utente.</p></td>
</tr>
<tr class="odd">
<td><p>DagMembersUp</p></td>
<td><p>Verifica che tutti i membri del gruppo di disponibilità del database siano disponibili, in esecuzione e raggiungibili.</p></td>
</tr>
<tr class="even">
<td><p>ClusterNetwork</p></td>
<td><p>Verifica che tutte le reti gestite dal cluster sul membro del gruppo di disponibilità del database specificato (o sul server locale se non è specificato alcun membro del gruppo di disponibilità del database) siano disponibili.</p></td>
</tr>
<tr class="odd">
<td><p>QuorumGroup</p></td>
<td><p>Verifica che il gruppo di cluster predefinito (gruppo di quorum) sia in uno stato integro e online.</p></td>
</tr>
<tr class="even">
<td><p>FileShareQuorum</p></td>
<td><p>Verifica che il server di controllo, la directory di controllo e la condivisione configurata per il gruppo di disponibilità del database siano raggiungibili.</p></td>
</tr>
<tr class="odd">
<td><p>DatabaseRedundancy</p></td>
<td><p>Verifica che sia disponibile almeno una copia integra dei database nel membro del gruppo di disponibilità del database specificato oppure, se non è stato specificato alcun membro del gruppo di disponibilità del database, sul server locale.</p></td>
</tr>
<tr class="even">
<td><p>DatabaseAvailability</p></td>
<td><p>Verifica che i database abbiano sufficiente disponibilità nel membro del gruppo di disponibilità del database specificato oppure, se non è stato specificato alcun membro del gruppo di disponibilità del database, sul server locale.</p></td>
</tr>
<tr class="odd">
<td><p>DBCopySuspended</p></td>
<td><p>Controlla se le copie del database delle cassette postali sono nello stato Suspended sul membro del gruppo di disponibilità del database specificato, o sul server locale se non è specificato alcun membro del gruppo di disponibilità del database.</p></td>
</tr>
<tr class="even">
<td><p>DBCopyFailed</p></td>
<td><p>Controlla se le copie del database delle cassette postali sono nello stato Failed sul membro del gruppo di disponibilità del database specificato, o sul server locale se non è specificato alcun membro del gruppo di disponibilità del database.</p></td>
</tr>
<tr class="odd">
<td><p>DBInitializing</p></td>
<td><p>Controlla se le copie del database delle cassette postali sono nello stato Initializing sul membro del gruppo di disponibilità del database specificato, o sul server locale se non è specificato alcun membro del gruppo di disponibilità del database.</p></td>
</tr>
<tr class="even">
<td><p>DBDisconnected</p></td>
<td><p>Controlla se le copie del database delle cassette postali sono nello stato Disconnected sul membro del gruppo di disponibilità del database specificato, o sul server locale se non è specificato alcun membro del gruppo di disponibilità del database.</p></td>
</tr>
<tr class="odd">
<td><p>DBLogCopyKeepingUp</p></td>
<td><p>Verifica che la copia del registro e l'ispezione da parte delle copie passive dei database sul membro del gruppo di disponibilità del database specificato (o sul server locale se non è specificato alcun membro del gruppo di disponibilità del database) siano in grado di tenere il passo dell'attività di generazione del registro sulla copia attiva.</p></td>
</tr>
<tr class="even">
<td><p>DBLogReplayKeepingUp</p></td>
<td><p>Verifica che l'attività di riesecuzione per le copie passive dei database sul membro del gruppo di disponibilità del database specificato (o sul server locale se non è specificato alcun membro del gruppo di disponibilità del database) sia in grado di tenere il passo dell'attività di ispezione e copia del registro.</p></td>
</tr>
</tbody>
</table>


## Esempio di Test-ReplicationHealth

Con questo esempio viene utilizzato il cmdlet **Test-ReplicationHealth** per verificare lo stato della replica per il server di cassette postali MBX1.

    Test-ReplicationHealth -Identity MBX1

## Registrazione degli eventi del canale Crimson

Windows include due categorie di registri eventi: i registri Windows e i registri applicazioni e servizi. La categoria dei registri di Windows include i registri eventi disponibili nelle versioni precedenti di Windows: applicazioni, protezione e sistema. Include inoltre due nuovi registri: il registro dell'installazione e il registro ForwardedEvents. I registri di Windows sono progettati per archiviare gli eventi delle applicazioni legacy e gli eventi relativi all'intero sistema.

I registri applicazioni e servizi sono una nuova categoria di registri eventi. Questi registri archiviano gli eventi di una singola applicazione o di un singolo componente, anziché gli eventi che possono avere un impatto sull'intero sistema. Questa nuova categoria di registri eventi è definita canale Crimson di un'applicazione.

La categoria dei registri applicazioni e servizi include quattro sottotipi: amministrazione, operativo, analitico e debug. Gli eventi nei registri di amministrazione sono di particolare interesse se si utilizzano i record del registro eventi per la risoluzione dei problemi. Gli eventi nel registro di amministrazione forniscono una guida sulla modalità di risposta agli eventi. Gli eventi nel registro operativo sono altrettanto utili, ma richiedono una maggiore interpretazione. I registri di amministrazione e di debug non sono di facile comprensione per gli utenti. I registri analitici (che per impostazione predefinita sono nascosti e disabilitati) archiviano gli eventi che analizzano un problema; al loro interno viene spesso registrato un elevato volume di eventi. I registri di debug sono utilizzati dagli sviluppatori durante il debug delle applicazioni.

Exchange 2013 registra gli eventi relativi ai canali Crimson nell'area dei registri applicazioni e servizi. È possibile visualizzare questi canali eseguendo la procedura descritta di seguito:

1.  Aprire Visualizzatore eventi.

2.  Nell'albero della console, accedere a **Registri applicazioni e servizi** \> **Microsoft** \> **Exchange**.

3.  In **Exchange**, selezionare un canale crimson, ad esempio **HighAvailability** o **MailboxDatabaseFailureItems** per visualizzare DAG e il database copia eventi correlati o **ActiveMontoring** o **ManagedAvailability** per visualizzare gli eventi relative alla disponibilità gestita.

Il canale HighAvailability contiene gli eventi relativi all'avvio e all'arresto del servizio Replica di Microsoft Exchange e ai diversi componenti eseguiti all'interno del servizio Replica di Microsoft Exchange, ad esempio Active Manager, l'API di replica sincrona di terze parti, il server RPC delle attività, il listener TCP e il writer del servizio Copia Shadow del volume (VSS). Il canale HighAvailability è utilizzato anche da Active Manager per registrare gli eventi relativi al monitoraggio del ruolo Active Manager e agli eventi di azione del database, ad esempio un'operazione di installazione del database e di troncamento del registro, e per la registrazione di eventi relativi al cluster sottostante a un gruppo di disponibilità del database.

Il canale MailboxDatabaseFailureItems è utilizzato per registrare eventi associati a qualsiasi errore che influisce su un database delle cassette postali replicato.

Il canale ActiveMonitoring contiene tutti gli eventi definizione e risultati di probe, monitor e risponditori Managed Availability.

Il canale ManagedAvailability contiene i registri delle azioni di ripristino e i risultati e gli eventi correlati.

## Monitor con spazio su disco insufficiente

Exchange 2013 Gestiti monitor disponibilità centinaia di metriche di sistema e i componenti ogni minuto, tra cui la quantità di spazio libero su disco per i volumi utilizzato dal ruolo del server cassette postali. Prima di Exchange 2013 Service Pack 1 (SP1), Exchange consente di monitorare lo spazio disponibile su tutti i volumi locali, inclusi i volumi che non contengono tutti i database o i file di registro. In SP1 e versioni successive, solo per i volumi che contengono database di Exchange e i file di registro vengono monitorati. In SP1, la soglia predefinita per il monitoraggio di spazio insufficiente volume è 200 GB. In Exchange 2013 aggiornamento cumulativo 6 e versioni successiva, la soglia predefinita è 180 GB. In SP1 e versioni successive, è possibile configurare la soglia aggiungendo il seguente valore DWORD (in MB) in ogni server della cassetta postale che si desidera personalizzare:

Percorso: **HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters**

Valore: *SpaceMonitorLowSpaceThresholdInMB*

Ad esempio per configurare la soglia a 100 GB, configurare il valore del Registro di sistema seguente:

**186a0 REG\_DWORD (100000)**

Dopo la configurazione o si modifica il valore del Registro di sistema sopra riportato, è necessario riavviare il servizio Microsoft Exchange DAG Management rendere effettive le modifiche.

## Script CollectOverMetrics.ps1

Exchange 2013 include nella cartella Scripts uno script chiamato CollectOverMetrics.ps1. CollectOverMetrics.ps1 legge i registri eventi dei membri del gruppo di disponibilità del database (DAG) per raccogliere informazioni sulle operazioni del database (ad esempio i montaggi, gli spostamenti e i failover del database) in un intervallo di tempo specifico. Per ogni operazione, lo script registra le informazioni seguenti:

  - Identità del database

  - Ora di inizio e di fine dell'operazione

  - Server su cui il database è stato montato all'inizio e alla fine dell'operazione

  - Motivo dell'operazione

  - Se l'operazione ha avuto esito positivo, inclusi i dettagli sull'errore se l'operazione non è riuscita

Lo script scrive queste informazioni nei file CSV con un'operazione per riga. Lo script scrive in un file CSV separato per ciascun gruppo di disponibilità del database (DAG).

Lo script supporta parametri che consentono di personalizzarne il comportamento e l'output. Ad esempio, è possibile limitare i risultati a un sottoinsieme specificato utilizzando i parametri *Database* o *ReportFilter*. Solo le operazioni che corrispondono a tali filtri saranno incluse nel rapporto HTML di riepilogo. I parametri disponibili sono elencati nella tabella seguente.

### Parametri dello script CollectOverMetrics.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DatabaseAvailabilityGroup</em></p></td>
<td><p>Specifica il nome del gruppo di disponibilità del database da cui si desidera raccogliere le metriche. Se questo parametro viene omesso, viene utilizzato il gruppo di disponibilità del database di cui è membro il server locale. I caratteri jolly possono essere utilizzati per raccogliere informazioni da più gruppi di disponibilità del database e creare i relativi rapporti.</p></td>
</tr>
<tr class="even">
<td><p><em>Database</em></p></td>
<td><p>Fornisce un elenco dei database per cui è necessario generare il report. Sono supportati i caratteri jolly, ad esempio <code>-Database:&quot;DB1&quot;,&quot;DB2&quot;</code> o <code>-Database:&quot;DB*&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>StartTime</em></p></td>
<td><p>Specifica la durata del periodo di tempo su cui creare il rapporto. Lo script raccoglie solo gli eventi registrati durante questo periodo. Di conseguenza, lo script può acquisire record di operazioni parziali (ad esempio, solo la fine di un'operazione all'inizio del periodo o viceversa). Se non viene specificato né <em>StartTime</em> né <em>EndTime</em>, lo script assumerà come valore predefinito le ultime 24 ore. Se viene specificato un solo parametro, il periodo sarà 24 ore, con inizio o fine all'ora specificata.</p></td>
</tr>
<tr class="even">
<td><p><em>EndTime</em></p></td>
<td><p>Specifica la durata del periodo di tempo su cui creare il rapporto. Lo script raccoglie solo gli eventi registrati durante questo periodo. Di conseguenza, lo script può acquisire record di operazioni parziali (ad esempio, solo la fine di un'operazione all'inizio del periodo o viceversa). Se non viene specificato né <em>StartTime</em> né <em>EndTime</em>, lo script assumerà come valore predefinito le ultime 24 ore. Se viene specificato un solo parametro, il periodo sarà 24 ore, con inizio o fine all'ora specificata.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>Specifica la cartella utilizzata per archiviare i risultati dell'elaborazione degli eventi. Se il parametro viene omesso, viene utilizzata la cartella Scripts. Quando è specificato, lo script prende un elenco di file CSV generati dallo stesso script e li utilizza come dati di origine per generare un rapporto HTML di riepilogo. Il rapporto è analogo a quello generato con l'opzione -GenerateHtmlReport. I file possono essere generati in più gruppi di disponibilità del database in molti orari diversi o anche in orari sovrapposti e lo script ne unirà tutti i dati.</p></td>
</tr>
<tr class="even">
<td><p><em>GenerateHtmlReport</em></p></td>
<td><p>Specifica che lo script raccoglie tutte le informazioni registrate, raggruppa i dati per tipo di operazione, quindi genera un file HTML che include le statistiche di ogni singolo gruppo. Il rapporto comprende il numero totale di operazioni in ogni gruppo, il numero di operazioni non riuscite e le statistiche del tempo impiegato in ciascun gruppo. Il rapporto contiene anche un'analisi dei tipi di errori che hanno causato le operazioni non riuscite.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowHtmlReport</em></p></td>
<td><p>Specifica che il report HTML generato deve essere visualizzato in un Web browser subito dopo la generazione.</p></td>
</tr>
<tr class="even">
<td><p><em>SummariseCsvFiles</em></p></td>
<td><p>Specifica che lo script legge i dati dai file CSV esistenti precedentemente generati dallo script stesso. I dati vengono quindi utilizzati per generare un rapporto di riepilogo simile a quello generato dal parametro <em>GenerateHtmlReport</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>ActionType</em></p></td>
<td><p>Specifica il tipo di azioni operative prese in considerazione dallo script. I valori validi per questo parametro sono <code>Move</code>, <code>Mount</code>, <code>Dismount</code> e <code>Remount</code>. Il valore <code>Move</code> si riferisce ai momenti in cui il database cambia il server attivo, a causa di spostamenti controllati o di failover. I valori <code>Mount</code>, <code>Dismount</code> e <code>Remount</code> si riferiscono ai momenti in cui il database cambia il proprio stato di montaggio senza spostamento in altro computer.</p></td>
</tr>
<tr class="even">
<td><p><em>ActionTrigger</em></p></td>
<td><p>Specifica quali operazioni amministrative devono essere prese in considerazione dallo script. I valori validi per questo parametro sono <code>Admin</code> o <code>Automatic</code>. Le azioni Automatico sono quelle eseguite automaticamente dal sistema (ad esempio, un failover quando un server passa alla modalità offline). Le azioni Admin sono le azioni eseguite da un amministratore utilizzando Exchange Management Shell o Exchange Administration Center.</p></td>
</tr>
<tr class="odd">
<td><p><em>RawOutput</em></p></td>
<td><p>Specifica che lo script scrive i risultati che avrebbero dovuto essere scritti nei file CSV direttamente con il flusso di output, come nel caso di write-output. Tali informazioni possono quindi essere reindirizzate ad altri comandi.</p></td>
</tr>
<tr class="even">
<td><p><em>IncludedExtendedEvents</em></p></td>
<td><p>Specifica che lo script raccoglie gli eventi che mostrano i dettagli di diagnostica del tempo impiegato per montare i database. L'operazione potrebbe richiedere molto tempo se il registro eventi dell'applicazione sui server è molto grande.</p></td>
</tr>
<tr class="odd">
<td><p><em>MergeCSVFiles</em></p></td>
<td><p>Specifica che lo script raccoglie tutti i file CSV contenenti i dati relativi a ciascuna operazione e li unisce un unico file CSV.</p></td>
</tr>
<tr class="even">
<td><p><em>ReportFilter</em></p></td>
<td><p>Specifica che deve essere applicato un filtro alle operazioni utilizzando i campi visualizzati nei file CSV. Questo parametro utilizza lo stesso formato dell'operazione <code>Where</code>, in cui ogni elemento è impostato su <code>$_</code> e restituisce un valore booleano. Ad esempio: <code>{$_DatabaseName -notlike &quot;Mailbox Database*&quot;}</code> può essere utilizzato per escludere i database predefiniti dal rapporto.</p></td>
</tr>
</tbody>
</table>


## Esempi di CollectOverMetrics.ps1

Con questo esempio vengono raccolte le metriche per tutti i database corrispondenti a DB\* (che include un carattere jolly) nel gruppo di disponibilità del database DAG1. Dopo la raccolta delle metriche, viene generato e visualizzato un report in formato HTML.

    CollectOverMetrics.ps1 -DatabaseAvailabilityGroup DAG1 -Database:"DB*" -GenerateHTMLReport -ShowHTMLReport

Negli esempi seguenti vengono dimostrate le modalità di filtraggio del rapporto HTML di riepilogo. Nel primo viene utilizzato il parametro *Database*, che prende un elenco di nomi dal database. Il rapporto di riepilogo contiene quindi solo i dati relativi a questi database. Nei due esempi successivi viene utilizzata l'opzione *ReportFilter*. Nell'ultimo esempio vengono filtrati tutti i database predefiniti.

    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -Database MailboxDatabase123,MailboxDatabase456
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { $_.DatabaseName -notlike "Mailbox Database*" }
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { ($_.ActiveOnStart -like "ServerXYZ*") -and ($_.ActiveOnEnd -notlike "ServerXYZ*") }

## Script CollectReplicationMetrics.ps1

CollectReplicationMetrics.ps1 è un altro script per le metriche di integrità incluso in Exchange 2013. Questo script fornisce una forma attiva di monitoraggio, in quanto raccoglie le metriche in tempo reale durante l'esecuzione dello script. CollectReplicationMetrics.ps1 raccoglie i dati dai contatori di prestazioni relativi alla replica del database. Lo script raccoglie i dati relativi ai contatori da più server Cassette postali, scrive tutti i dati del server in un file CSV e può riportare diverse statistiche per tutti i dati (ad esempio, il periodo di tempo in cui una copia non è riuscita o è stata sospesa, la lunghezza media della coda di riesecuzione o di copia o la quantità di tempo in cui le copie non soddisfacevano i criteri di failover).

I server possono essere specificati singolarmente o per interi gruppi di disponibilità del database. Lo script può essere eseguito per raccogliere i dati e creare il rapporto o può essere eseguito solo per raccogliere i dati o solo per creare il rapporto dei dati già raccolti. È possibile specificare la frequenza con cui i dati devono essere campionati e la durata complessiva di raccolta dei dati.

I dati raccolti da ogni server vengono salvati in un file denominato **CounterData.\<ServerName\>.\<TimeStamp\>.csv**. Se lo script non è stato eseguito con il parametro *DagName*, il rapporto di riepilogo verrà salvato in un file denominato **HaReplPerfReport.\<DAGName\>.\<TimeStamp\>.csv** o **HaReplPerfReport.\<TimeStamp\>.csv**.

Lo script avvia i processi Windows PowerShell per raccogliere i dati da ogni server. Questi processi vengono eseguiti per l'intera durata di raccolta dei dati. Se si specifica un gran numero di server, l'operazione può richiedere una notevole quantità di memoria. La fase finale del processo, in cui i dati vengono elaborati in un rapporto di riepilogo, può richiedere anche del tempo per l'elaborazione di grandi quantità di dati. È possibile eseguire la fase di raccolta su un computer, quindi copiare i dati altrove per l'elaborazione.

Lo script CollectReplicationMetrics.ps1 supporta parametri che consentono di personalizzarne il comportamento e l'output. I parametri disponibili sono elencati nella tabella seguente.

### Parametri dello script CollectReplicationMetrics.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>Specifica il nome del gruppo di disponibilità del database da cui si desidera raccogliere le metriche. Se questo parametro viene omesso, viene utilizzato il gruppo di disponibilità del database di cui è membro il server locale.</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseNames</em></p></td>
<td><p>Fornisce un elenco dei database per cui è necessario generare il report. Sono supportati i caratteri jolly, ad esempio <code>-DatabaseNames:&quot;DB1&quot;,&quot;DB2&quot;</code> o <code>-DatabaseNames:&quot;DB*&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>Specifica la cartella utilizzata per archiviare i risultati dell'elaborazione degli eventi. Se il parametro viene omesso, viene utilizzata la cartella Scripts.</p></td>
</tr>
<tr class="even">
<td><p><em>Duration</em></p></td>
<td><p>Specifica il tempo di esecuzione del processo di raccolta. I valori standard sono compresi tra una e tre ore. Le durate magggiori devono essere utilizzate solo con intervalli lunghi tra un campione e l'altro oppure come serie di processi più brevi eseguiti dalle attività pianificate.</p></td>
</tr>
<tr class="odd">
<td><p><em>Frequency</em></p></td>
<td><p>Specifica la frequenza di raccolta delle metriche dei dati. I valori standard sono 30 secondi, un minuto o cinque minuti. In circostanze normali, intervalli più brevi di questi non visualizzeranno modifiche significative tra ogni campione.</p></td>
</tr>
<tr class="even">
<td><p><em>Servers</em></p></td>
<td><p>Specifica l'identità dei server da cui raccogliere le statistiche. È possibile specificare qualsiasi valore, inclusi caratteri jolly o GUID.</p></td>
</tr>
<tr class="odd">
<td><p><em>SummariseFiles</em></p></td>
<td><p>Specifica un elenco di file CSV per generare un rapporto di riepilogo. Questi file sono denominati <strong>CounterData.&lt;CounterData&gt;*</strong> e sono generati dallo script CollectReplicationMetrics.ps1.</p></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p>Specifica le fasi di elaborazione eseguite dallo script. È possibile utilizzare i seguenti valori:</p>
<ul>
<li><p><code>CollectAndReport</code>   Questo è il valore predefinito. Questo valore indica che lo script deve sia raccogliere i dati dai server che elaborarli per creare il rapporto di riepilogo.</p></li>
<li><p><code>CollectOnly</code>   Questo valore indica che lo script deve solo raccogliere i dati e non creare il rapporto.</p></li>
<li><p><code>ProcessOnly</code>   Questo valore indica che lo script deve importare i dati da un insieme di file CSV ed elaborarli per creare il rapporto di riepilogo. Il parametro <em>SummariseFiles</em> viene utilizzato per fornire allo script l'elenco dei file da elaborare.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MoveFilestoArchive</em></p></td>
<td><p>Specifica che lo script deve spostare i file in una cartella compressa dopo l'elaborazione.</p></td>
</tr>
<tr class="even">
<td><p><em>LoadExchangeSnapin</em></p></td>
<td><p>Specifica che lo script deve caricare i comandi di Shell. Questo parametro è utile quando è necessario eseguire lo script dall'esterno di Shell, ad esempio in un'attività pianificata.</p></td>
</tr>
</tbody>
</table>


## Esempio di CollectReplicationMetrics.ps1

Nell'esempio seguente vengono raccolti i dati relativi a un'ora da tutti i server nel gruppo di disponibilità del database DAG1, campionati a intervalli di un minuto, e viene quindi generato un rapporto di riepilogo. Viene inoltre utilizzato il parametro *ReportPath*, a causa del quale lo script posiziona tutti i file nella directory corrente.

    CollectReplicationMetrics.ps1 -DagName DAG1 -Duration "01:00:00" -Frequency "00:01:00" -ReportPath

Nell'esempio seguente vengono letti i dati da tutti i file che corrispondono a CounterData\* e viene quindi generato il rapporto di riepilogo.

    CollectReplicationMetrics.ps1 -SummariseFiles (dir CounterData*) -Mode ProcessOnly -ReportPath


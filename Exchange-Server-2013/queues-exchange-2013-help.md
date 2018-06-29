---
title: 'Code: Exchange 2013 Help'
TOCTitle: Code
ms:assetid: e7ad0ba5-3789-4a2b-9825-6bb1b321609c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125022(v=EXCHG.150)
ms:contentKeyID: 51407440
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Code

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Una *coda* è una posizione di conservazione temporanea per i messaggi in attesa di passare alla fase successiva dell'elaborazione o di essere recapitati a una destinazione. Ogni coda rappresenta un insieme logico di messaggi elaborato da un server Exchange in base a un ordine specifico. In Microsoft Exchange Server 2013, nelle code i messaggi vengono conservati prima, durante e dopo il recapito. Le code esistono sui server Cassette postali e sui server Trasporto Edge. In questo argomento, i server Cassette postali e i server Trasporto Edge sono detti *server di trasporto*.

Come le versioni precedenti di Exchange, Exchange 2013 utilizza un solo database ESE (Extensible Storage Engine) per l'archiviazione della coda.

È possibile gestire le code e i messaggi contenuti utilizzando Exchange Management Shell e il Visualizzatore code nella Casella degli strumenti di Exchange. Queste interfacce possono essere utilizzate per visualizzare lo stato e il contenuto delle code e le proprietà dettagliate dei messaggi, nonché per eseguire azioni di modifica delle code o dei relativi messaggi.

**Sommario**

  - Types of queues

  - Queue database files

  - Queue properties
    
      - NextHopSolutionKey
    
      - IncomingRate, OutgoingRate, and Velocity
    
      - Queue status
    
      - Other queue properties

  - Message properties
    
      - Message status
    
      - Other message properties

  - Manage queues and messages in queues

## Tipi di code

In Exchange 2013 vengono utilizzati i seguenti tipi di code:

  - **Code permanenti**   Le *code permanenti* esistono su ogni server di trasporto di ogni organizzazione Exchange. Come nelle versioni precedenti di Exchange, esistono tre code permanenti in Exchange 2013:
    
      - **Coda Invio**   Una coda di invio viene utilizzata dal classificatore per raccogliere tutti i messaggi che sono stati risolti, instradati ed elaborati dagli agenti di trasporto sul server di trasporto. La fase di elaborazione di tutti i messaggi ricevuti da un server di trasporto ha inizio dalla coda di invio. Nei server Cassette postali, i messaggi vengono inviati tramite un connettore di ricezione, le directory di prelievo o riesecuzione oppure il servizio di invio del trasporto delle cassette postali. Nei server Trasporto Edge, i messaggi in genere vengono inviati tramite un connettore di ricezione, ma sono disponibili anche le directory di prelievo o riesecuzione.
        
        Il classificatore recupera i messaggi da questa coda e, tra le altre cose, determina la posizione del destinatario e la relativa route. Dopo la classificazione, il messaggio viene spostato in una coda di recapito o in una coda non raggiungibile. Ogni server di trasporto dispone di una sola coda di invio. I messaggi presenti nella coda di invio non possono trovarsi contemporaneamente in altre code. Per ulteriori informazioni sul classificatore e la pipeline di trasporto, vedere [Flusso di posta](mail-flow-exchange-2013-help.md).
    
      - **Coda non raggiungibile**   La coda non raggiungibile contiene messaggi che non possono essere instradati alle relative destinazioni. In genere, una destinazione diventa non raggiungibile quando viene modificato il percorso di routing configurato per il recapito dei messaggi. Tutti i messaggi con destinatari non raggiungibili sono situati in questa coda, indipendentemente dalle relative destinazioni. Ogni server di trasporto dispone di una sola coda non raggiungibile.
        
        I messaggi nella coda non raggiungibile vengono di nuovo inviati automaticamente quando viene rilevata una modifica del routing. Una volta risolta la condizione o l'errore di configurazione che ha causato l'inserimento dei messaggi nella coda non raggiungibile, non è necessario eseguire altre azioni per rimuovere i messaggi dalla coda e recapitarli.
        
        La coda non raggiungibile in genere è vuota. Se questa coda non contiene messaggi non viene visualizzata nel Visualizzatore code o nei risultati di **Get-Queue**.
    
      - **Coda di messaggi non elaborabili**   Una coda speciale utilizzata per isolare i messaggi che vengono rilevati come dannosi per il sistema Exchange 2013 dopo un errore del server o del servizio di trasporto. Il contenuto e il formato dei messaggi possono rivelarsi di fatto dannosi. In alternativa, è possibile che essi derivino da un agente scritto in modo inadeguato che ha causato l'errore nel server Exchange durante l'elaborazione dei presunti messaggi errati.
        
        La coda dei messaggi non elaborabili in genere è vuota. Se questa coda non contiene messaggi non viene visualizzata nel Visualizzatore code o nei risultati di **Get-Queue**. I messaggi nella coda di messaggi non elaborabili non vengono mai ripresi o fatti scadere automaticamente. I messaggi rimangono nella coda di messaggi non elaborabili fino a quando non vengono ripresi o rimossi manualmente da un amministratore.

  - **Code di recapito**   Le code di recapito contengono i messaggi che devono essere recapitati a destinazioni locali o remote tramite SMTP. Tutti i messaggi vengono trasmessi da un server Exchange all'altro tramite SMTP. Le destinazioni non SMTP utilizzano le code di recapito se la destinazione è servita da un connettore dell'agente di recapito. . Ogni coda contiene i messaggi instradati alla stessa destinazione. È praticamente inevitabile che esistano più code di recapito su un server di trasporto. Le code di recapito vengono create dinamicamente in base alla necessità e vengono eliminate automaticamente quando sono vuote e scadute. La scadenza di una coda è controllata dal parametro *QueueMaxIdleTime* nel cmdlet **Set-TransportService**. Il valore predefinito è tre minuti.

  - **Code shadow**   Contengono le copie ridondanti di un messaggio in transito. Per ulteriori informazioni, vedere [Ridondanza shadow](shadow-redundancy-exchange-2013-help.md).

  - **Rete sicura**   Conserva le copie dei messaggi correttamente recapitati dal server di trasporto. Anche se non è possibile accedervi dagli strumenti di gestione delle code, la Rete sicura è semplicemente un'altra coda del database delle code. Per ulteriori informazioni, vedere [Rete sicura](safety-net-exchange-2013-help.md).

Inizio pagina

## File di database delle code

Tutte le diverse code sono archiviate in un unico database ESE. Per impostazione predefinita, questo database delle code si trova su un server di trasporto in `%ExchangeInstallPath%TransportRoles\data\Queue`.

Come qualsiasi database ESE, il database delle code utilizza i file di registro per accettare, verificare e gestire i dati. Per migliorare le prestazioni, tutte le transazioni dei messaggi vengono scritte prima nei file di registro e in memoria, quindi nel file di database. Il file del checkpoint consente di tenere traccia delle voci del registro delle transazioni che sono state confermate nel database. Durante la normale chiusura del servizio di trasporto di Microsoft Exchange, le modifiche del database non salvate contenute nei registri delle transazioni vengono sempre salvate nel database.

Per il database delle code viene utilizzata la registrazione circolare. Significa che la cronologia delle transazioni confermate contenute nei registri delle transazioni non viene mantenuta. I registri delle transazioni antecedenti al checkpoint corrente vengono eliminati immediatamente e automaticamente. Pertanto, non è possibile rieseguire i registri delle transazioni per il ripristino da backup del database delle code.

Exchange 2013 utilizza *tabelle di generazione* per l'archiviazione e la pulitura dei messaggi nel database delle code. Anziché elaborare ed eliminare singoli record di messaggi da una tabella di grandi dimensioni, il database delle code archivia i messaggi nelle tabelle basate sul tempo ed elimina l'intera tabella solo quando tutti i messaggi presenti sono stati elaborati correttamente. Ad esempio, tutti i messaggi accodati dalle 13:00 alle 2:00, a prescindere dalla coda o dalla destinazione, vengono archiviati nella tabella `1p-2p_msgs`. Alle 2:00, nuovi messaggi vengono archiviati nella tabella `2p-3p_msgs`. Alle 4:00 PM, viene creata una nuova tabella denominata `4p-5p_msgs` e l'intera tabella `1p-2p_msgs` viene eliminata, ma solo se tutti i messaggi della tabella sono stati elaborati correttamente. Questo approccio tramite cui si elimina l'intera tabella dei messaggi anziché i singoli messaggi migliora le prestazioni dell'I/O dell'unità e conserva il database delle code.

Nella seguente tabella sono elencati i file che costituiscono il database delle code.

### File che costituiscono il database delle code

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>File</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.que</p></td>
<td><p>In questo file del database delle code sono archiviati tutti i messaggi in coda.</p></td>
</tr>
<tr class="even">
<td><p>Tmp.edb</p></td>
<td><p>Questo file di database temporaneo viene utilizzato per verificare lo schema del database delle code all'avvio.</p></td>
</tr>
<tr class="odd">
<td><p>Trn*.log</p></td>
<td><p>Questo registro delle transazioni consente di registrare tutte le modifiche apportate al database delle code. Le modifiche al database vengono prima scritte nel registro delle transazioni e quindi confermate nel database. Trn.log è il file di registro delle transazioni attivo. Trntmp.log è il successivo file delle transazioni di cui è stato effettuato il provisioning creato in anticipo. Se il file di registro delle transazioni Trn.log esistente raggiunge la dimensione massima, Trn.log viene rinominato in Trn<em>nnnn</em>.log, dove <em>nnnn</em> è un numero sequenziale. Trntmp.log viene quindi rinominato in Trn.log e diventa il file di registro delle transazioni attivo.</p></td>
</tr>
<tr class="even">
<td><p>Trn.chk</p></td>
<td><p>Questo file di checkpoint consente di tenere traccia delle voci del registro delle transazioni che sono state confermate nel database. Questo file si trova sempre nello stesso percorso del file mail.que.</p></td>
</tr>
<tr class="odd">
<td><p>Trnres00001.jrs</p>
<p>Trnres00002.jrs</p></td>
<td><p>Questi file di registro delle transazioni di riserva fungono da segnaposto. Vengono utilizzati solo nel caso in cui lo spazio sul disco rigido che contiene il registro delle transazioni è insufficiente per arrestare correttamente il database delle code.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Opzioni per la configurazione del database delle code

Configurare il database delle code aggiungendo o modificando le chiavi nel file di configurazione dell'applicazione XML `%ExchangeInstallPath%Bin\EdgeTransport.exe.config`. Tale file è associato al servizio di trasporto di Microsoft Exchange. Le modifiche apportate al file EdgeTransport.exe.config hanno effetto dopo il riavvio del servizio di trasporto Microsoft Exchange.

La sezione `<appSettings>` del file EdgeTransport.exe.config consente di aggiungere nuove chiavi o di modificare quelle esistenti. Se non esiste una specifica chiave, è possibile aggiungerla manualmente per modificarne il valore.

Le chiavi per il database delle code disponibili nel file EdgeTransport.exe.config sono descritte nella seguente tabella.

### Chiavi del database delle code dei messaggi disponibili nel file EdgeTransport.exe.config

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiave</th>
<th>Valore predefinito</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabaseBatchSize</em></p></td>
<td><p>40</p></td>
<td><p>Questa chiave consente di specificare il numero di operazioni di input/output del database che è possibile raggruppare prima dell'esecuzione. Per impostazione predefinita questa chiave non esiste nel file EdgeTransport.exe.config.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseBatchTimeout</em></p></td>
<td><p>100</p></td>
<td><p>Questa chiave consente di specificare il tempo massimo di attesa in millisecondi per il raggruppamento di più operazioni di input/output del database prima dell'esecuzione. Le operazioni di input/output del database vengono eseguite senza attendere oltre se sono soddisfatte le seguenti condizioni:</p>
<ul>
<li><p>Il numero di operazioni di input/output del database specificato dalla chiave <em>QueueDatabaseBatchSize</em> non è stato raggiunto.</p></li>
<li><p>È trascorso il tempo specificato dalla chiave <em>QueueDatabaseBatchTimeout</em>.</p></li>
</ul>
<p>Per impostazione predefinita questa chiave non esiste nel file EdgeTransport.exe.config.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxConnections</em></p></td>
<td><p>4</p></td>
<td><p>Questa chiave consente di specificare il numero di connessioni di database ESE che è possibile aprire.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingBufferSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>Questa chiave consente di specificare la memoria utilizzata per inserire nella cache i record delle transazioni prima che vengano scritti nel file di registro delle transazioni.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseLoggingFileSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>Questa chiave consente di specificare la dimensione massima di un file di registro delle transazioni. Quando viene raggiunta la dimensione massima, viene aperto un nuovo file di registro.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>Questa chiave consente di specificare la directory predefinita per i file di registro del database delle code. Per istruzioni sulla modifica della posizione del database delle code, vedere <a href="change-the-location-of-the-queue-database-exchange-2013-help.md">Modificare il percorso del database della coda</a>.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxBackgroundCleanupTasks</em></p></td>
<td><p>32</p></td>
<td><p>Questa chiave consente di specificare il numero massimo di elementi di lavoro per la pulizia in background che è possibile accodare in qualsiasi momento al pool di thread del motore di database.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragEnabled</em></p></td>
<td><p>True</p></td>
<td><p>La chiave consente di abilitare o disabilitare la deframmentazione in linea pianificata del database delle code di posta. Per impostazione predefinita questa chiave non esiste nel file EdgeTransport.exe.config.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseOnlineDefragSchedule</em></p></td>
<td><p><code>1:00:00</code> o 1:00 A.M.</p></td>
<td><p>Questa chiave consente di specificare l'ora, nel formato 24 ore, in cui avviare la deframmentazione in linea del database delle code di posta. Per specificare un valore, immettere un tempo nel formato <em>hh:mm:ss</em> dove <em>h</em> = ore, <em>m</em> = minuti e <em>s</em> = secondi.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragTimeToRun</em></p></td>
<td><p><code>3:00:00</code> o 3 ore</p></td>
<td><p>Questa chiave consente di specificare il periodo di tempo per cui può essere eseguita l'attività di deframmentazione in linea. Anche se l'attività di deframmentazione non termina entro l'ora specificata, il database delle code viene lasciato in uno stato coerente. Per specificare un valore, immettere un tempo nel formato <em>hh:mm:ss</em> dove <em>h</em> = ore, <em>m</em> = minuti e <em>s</em> = secondi.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>Questa chiave consente di specificare la directory predefinita per i file di database delle code. Per istruzioni sulla modifica della posizione del database delle code, vedere <a href="change-the-location-of-the-queue-database-exchange-2013-help.md">Modificare il percorso del database della coda</a>.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Qualsiasi impostazione personalizzata per singolo server apportata nei file di configurazione dell'applicazione XML di Exchange, ad esempio, i file web.config sui server Accesso client oppure il file EdgeTransport.exe.config sui server Cassette postali, verrà sovrascritta quando si installa un aggiornamento cumulativo di Exchange. Salvare queste informazioni in modo da poter facilmente riconfigurare il server dopo l'installazione. È necessario riconfigurare queste impostazioni dopo aver installato un aggiornamento cumulativo di Exchange.



Inizio pagina

## Proprietà coda

Una coda presenta molte proprietà che ne descrivono lo scopo e lo stato. Alcune proprietà delle code vengono applicate a una coda quando viene creata e non cambiano. Altre proprietà contengono lo stato, la dimensione, l'ora o altri indicatori che vengono aggiornati di frequente.

Inizio pagina

## NextHopSolutionKey

Il componente di routing del classificatore nel servizio di trasporto di Microsoft Exchange seleziona la destinazione per un messaggio e tale destinazione viene utilizzata per creare la coda di recapito. La destinazione viene indicata per ogni destinatario come attributo **NextHopSolutionKey**. Ogni valore univoco dell'attributo **NextHopSolutionKey** corrisponde a una coda di recapito separata.

L'attributo **NextHopSolutionKey** contiene i seguenti campi:

  - **DeliveryType**   Il valore di questo campo rappresenta i risultati della classificazione del messaggio e indica in che modo il servizio di trasporto trasmetterà il messaggio al successivo hop, che potrebbe rappresentare la destinazione finale del messaggio o un hop intermedio lungo il percorso. Il servizio di trasporto utilizza un elenco predefinito di valori per **DeliveryType** in base alla destinazione del routing di destinazione o al gruppo di recapito.

  - **NextHopDomain**   Questo campo utilizza valori specifici basati sul valore del campo **DeliveryType**. Per le code di recapito, il valore di questo campo è effettivamente il nome della coda. Il valore di **NextHopDomain** non è sempre un nome di dominio. Ad esempio, il valore potrebbe essere il nome del sito Active Directory di destinazione o del gruppo di disponibilità del database (DAG). Si può pensare a questo campo come il nome del successivo hop, dove il valore è il nome della destinazione di routing o del gruppo di recapito di destinazione.

  - **NextHopConnector**   Questo campo utilizza valori specifici basati sul valore del campo **DeliveryType**. Il valore è sempre espresso come GUID. Se questo campo non viene utilizzato, il valore è un GUID contenente solo zeri. Il valore di **NextHopConnector** non è sempre il GUID di un connettore. Ad esempio, il valore potrebbe essere il GUID del sito Active Directory di destinazione o del gruppo di disponibilità del database. Si può pensare a questo campo come il GUID del successivo hop, dove il valore è il GUID della destinazione di routing o del gruppo di recapito di destinazione.

Exchange 2013 aggiunge anche la proprietà **NextHopCategory** alla coda in base al valore di **DeliveryType**. Il valore di **NextHopCategory** è `External` o `Internal`. Il valore `External` indica l'hop successivo della coda esterno all'organizzazione Exchange. Il valore `Internal` indica l'hop successivo della coda interno all'organizzazione Exchange. Tenere presente che un messaggio per un destinatario esterno potrebbe richiedere uno o più hop interni prima che il messaggio venga recapitato esternamente.

I valori di **DeliveryType**, **NextHopCategory**, **NextHopDomain** e **NextHopConnector** sono descritti nella seguente tabella.


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
<th>Tipo di recapito nel Visualizzatore code</th>
<th>Tipo di recapito in Shell</th>
<th>Descrizione</th>
<th>NextHopCategory</th>
<th>NextHopDomain</th>
<th>NextHopConnector</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Agente di recapito</strong></p></td>
<td><p><strong>DeliveryAgent</strong></p></td>
<td><p>La coda contiene i messaggi per il recapito ai destinatari in uno spazio di indirizzi non SMTP. I messaggi vengono recapitati utilizzando un connettore dell'agente di recapito configurato sul server locale.</p></td>
<td><p>External</p></td>
<td><p>Il valore dello spazio di indirizzi di destinazione configurato nel connettore dell'agente di recapito.</p></td>
<td><p>Questo valore è il GUID del connettore dell'agente di recapito. Ad esempio, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p>La coda contiene i messaggi per il recapito ai destinatari in uno spazio di indirizzi SMTP. I messaggi vengono recapitati utilizzando un connettore di invio configurato sul server locale. Il connettore di invio è configurato per l'utilizzo del routing DNS.</p></td>
<td><p>External</p></td>
<td><p>Il valore è lo spazio di indirizzi di destinazione configurato nel connettore di invio. Ad esempio, <code>contoso.com</code>.</p></td>
<td><p>Questo valore è il GUID del connettore di invio. Ad esempio, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p>La coda contiene i messaggi per il recapito ai destinatari in uno spazio di indirizzi non SMTP. I messaggi vengono recapitati utilizzando un connettore esterno configurato sul server locale.</p></td>
<td><p>External</p></td>
<td><p>Questo valore è lo spazio di indirizzi di destinazione configurato nel connettore esterno.</p></td>
<td><p>Questo valore è il GUID del connettore esterno. Ad esempio, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p>La coda contiene i messaggi per il recapito ai destinatari in uno spazio di indirizzi SMTP. I messaggi vengono recapitati utilizzando un connettore di invio configurato sul server locale. Il connettore di invio è configurato per l'utilizzo del routing Smart Host.</p></td>
<td><p>External</p></td>
<td><p>Questo valore è l'elenco di smart host configurati nel connettore di invio. Gli smart host possono essere configurati come nomi di dominio completi, indirizzi IP o entrambi. I valori possono essere:</p>
<ul>
<li><p><strong>Nome di dominio completo</strong>   La sintassi è <code>&lt;FQDN1,FQDN2,...&gt;</code>. Ad esempio, <code>smarthost01.contoso.com</code> o <code>smarthost01.contoso.com,smarthost02.fabrikam.com</code>.</p></li>
<li><p><strong>Indirizzo IP</strong>   La sintassi è <code>&lt;[IPAddress1],[IPAddress2],...&gt;</code>. Ad esempio, <code>[10.10.10.100]</code> o <code>[10.10.10.100],[10.10.10.101]</code>.</p></li>
<li><p><strong>Nome di indirizzo completo e indirizzo IP</strong>   La sintassi è <code>&lt;[IPAddress1],FQDN1,...&gt;</code> e dipende da come gli smart host sono elencati nel connettore di invio. Ad esempio, <code>[172.17.17.7],relay.tailspintoys.com</code> o <code>mail.contoso.com,[192.168.1.50]</code>.</p></li>
</ul></td>
<td><p>Questo valore è il GUID del connettore di invio. Ad esempio, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Recapito SMTP alla cassetta postale</strong></p></td>
<td><p><strong>SmtpDeliveryToMailbox</strong></p></td>
<td><p>La coda contiene i messaggi per il recapito ai destinatari delle cassette postali di Exchange 2013. Il database delle cassette postali di destinazione si trova in una delle seguenti posizioni:</p>
<ul>
<li><p>Il server Cassette postali di Exchange 2013 locale.</p></li>
<li><p>Un server Cassette postali di Exchange 2013 nello stesso gruppo di disponibilità del database,</p></li>
<li><p>Un server Cassette postali di Exchange 2013 nel sito Active Directory in ambienti non DAG.</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>Questo valore è il nome del database di cassette postali di destinazione. Ad esempio, <code>Mailbox Database 0471695037</code>.</p></td>
<td><p>Questo valore è il GUID del database di cassette postali di destinazione. Ad esempio, <code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Inoltro SMTP ai server di origine del connettore di invio</strong></p></td>
<td><p><strong>SmtpRelayToConnectorSourceServers</strong></p></td>
<td><p>La coda contiene i messaggi per il recapito a SMTP o ai destinatari non SMTP. I messaggi vengono recapitati utilizzando un connettore di invio, un connettore dell'agente di recapito o un connettore esterno configurato su un server di trasporto remoto. Il server di trasporto remoto potrebbe essere un server Cassette postali di Exchange 2013 o un server Trasporto Hub di Exchange 2007 o Exchange 2010 di una versione precedente di Exchange. Il server remoto potrebbe risiedere nel sito Active Directory locale o in un sito Active Directory remoto.</p></td>
<td><p>Internal</p></td>
<td><p>Questo valore è in nome della destinazione del connettore di invio, del connettore dell'agente di recapito o del connettore esterno. Ad esempio, <code>Contoso.com Send Connector</code>.</p></td>
<td><p>Questo valore è il GUID della destinazione del connettore di invio, del connettore dell'agente di recapito o del connettore esterno. Ad esempio, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Inoltro SMTP al gruppo di disponibilità del database</strong></p></td>
<td><p><strong>SmtpRelayToDag</strong></p></td>
<td><p>La coda contiene messaggi per il recapito ai destinatari delle cassette postali di Exchange 2013, dove il database delle cassette postali di destinazione risiede in un gruppo di disponibilità del database remoto. Tale DAG remoto potrebbe risiedere nel sito Active Directory locale o in un sito Active Directory remoto.</p></td>
<td><p>Internal</p></td>
<td><p>Questo valore è il nome del gruppo di disponibilità del database di destinazione. Ad esempio, <code>DAG1</code>.</p></td>
<td><p>Questo valore è il GUID del gruppo di disponibilità del database di destinazione. Esempio: <code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Inoltro SMTP al gruppo di recapito delle cassette postali</strong></p></td>
<td><p><strong>SmtpRelayToMailboxDeliveryGroup</strong></p></td>
<td><p>La coda contiene i messaggi per il recapito ai destinatari delle cassette portali legacy, dove la cassetta postale di destinazione si trova su un server Cassette postali di Exchange 2007 o Exchange 2010. Il messaggio è correlato al server Trasporto Hub su cui è in esecuzione la stessa versione di Exchange della cassetta postale di destinazione. Il server Trasporto Hub di destinazione potrebbe risiedere nel sito Active Directory locale o in un sito Active Directory remoto.</p></td>
<td><p>Internal</p></td>
<td><p>Il nome della coda utilizza la seguente sintassi: <code>Site:&lt;ADSiteName&gt;;Version:&lt;ExchangeVersion&gt;</code>, dove <em>&lt;NomeSitoAD&gt;</em> è il nome del sito Active Directory di destinazione e <em>&lt;VersioneExchange&gt;</em> è la versione di Exchange sul server Cassette postali.</p></td>
<td><p>Questo valore è vuoto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Inoltro SMTP a un sito Active Directory remoto</strong></p></td>
<td><p><strong>SmtpRelayToRemoteActiveDirectorySite</strong></p></td>
<td><p>La coda contiene i messaggi per il recapito a una destinazione remota e la topologia di routing richiede che il messaggio venga instradato attraverso uno specifico sito Active Directory. Il sito è un hop intermedio nel percorso che conduce alla destinazione finale. Questa situazione si verifica nelle seguenti circostanze:</p>
<ul>
<li><p>Il messaggio deve essere instradato attraverso un sito hub.</p></li>
<li><p>Il messaggio richiede il recapito attraverso un connettore di invio configurato su un server Trasporto Edge con sottoscrizione a un sito Active Directory remoto.</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>Questo valore è il nome del sito Active Directory di destinazione. Ad esempio, <code>NorthAmericanSite</code>.</p></td>
<td><p>Questo valore è il GUID del sito Active Directory di destinazione. Ad esempio, <code>bfd6c3df-5b65-8bfb-53f1f2c0d55c</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Inoltro SMTP ai server Exchange specificati</strong></p></td>
<td><p><strong>SmtpRelayToServers</strong></p></td>
<td><p>La coda contiene i messaggi per il recapito a un gruppo di distribuzione configurato per uno specifico server di espansione. L'espansione potrebbe essere un server Cassette postali di Exchange 2013 o un server Trasporto Hub di Exchange 2007 o Exchange 2010. Il server potrebbe risiedere nel sito Active Directory locale o in un sito Active Directory remoto.</p></td>
<td><p>Internal</p></td>
<td><p>Questo valore è il nome di dominio completo del server di espansione di destinazione. Ad esempio, <code>mailbox01.contoso.com</code>.</p></td>
<td><p>Questo valore è <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Inoltro SMTP nel sito Active Directory al server Trasporto Edge</strong></p></td>
<td><p><strong>SmtpRelayWithinAdSiteToEdge</strong></p></td>
<td><p>La coda contiene i messaggi per il recapito a uno spazio di indirizzi SMTP. I messaggi vengono recapitati attraverso un connettore di invio configurato su un server Trasporto Edge con sottoscrizione a un sito Active Directory locale.</p></td>
<td><p>Internal</p></td>
<td><p>Questo valore è il nome del connettore di invio che invia la posta Internet in uscita dall'organizzazione a Internet. Tale connettore di invio viene creato automaticamente dalla sottoscrizione Edge ed è denominato <code>EdgeSync - &lt;ADSiteName&gt; to Internet</code>. <em>&lt;NomeSitoAD&gt;</em> è il nome del sito Active Directory locale sottoscritto dal server Trasporto Edge.</p></td>
<td><p>Questo valore è il GUID del connettore di invio. Ad esempio, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Heartbeat</strong></p></td>
<td><p><strong>Heartbeat</strong></p></td>
<td><p>Questo valore è riservato all'utilizzo interno da parte di Microsoft. Per ulteriori informazioni su heartbeat, vedere <a href="shadow-redundancy-exchange-2013-help.md">Ridondanza shadow</a>.</p></td>
<td><p>n/d</p></td>
<td><p>n/d</p></td>
<td><p>n/d</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ridondanza shadow</strong></p></td>
<td><p><strong>ShadowRedundancy</strong></p></td>
<td><p>La coda contiene i messaggi in una coda shadow. Una coda shadow contiene le copie ridondanti dei messaggi in transito nel caso i messaggi principali non vengano correttamente recapitati. Per ulteriori informazioni, vedere <a href="shadow-redundancy-exchange-2013-help.md">Ridondanza shadow</a>.</p></td>
<td><p>Internal</p></td>
<td><p>Questo valore è il dome di dominio completo del server primario per cui la coda shadow contiene copie ridondanti dei messaggi principali. Ad esempio, <code>mailbox01.contoso.com</code>.</p></td>
<td><p>Questo valore è <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Non definito</strong></p></td>
<td><p><strong>Non definito</strong></p></td>
<td><p>Questo valore viene utilizzato solo nella coda di invio e nella coda dei messaggi non elaborabili.</p></td>
<td><p>Internal</p></td>
<td><p>Per la coda di invio, questo valore è <code>Submisssion</code>. Per la coda dei messaggi non elaborabili, questo valore è <code>Poison Message</code>.</p></td>
<td><p>Questo valore è <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Undreachable</strong></p></td>
<td><p><strong>Non raggiungibile</strong></p></td>
<td><p>Questo valore viene utilizzato solo nella coda non raggiungibile.</p></td>
<td><p>Internal</p></td>
<td><p>Questo valore è <code>Unreachable Domain</code>.</p></td>
<td><p>Questo valore è <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
</tbody>
</table>


Tenere presente che Exchange 2013 supporta valori legacy di **DeliveryType** per la compatibilità con le versioni precedenti di Exchange. Questi valori sono disponibili nel Visualizzatore code e in Shell, ma non vengono utilizzati da Exchange 2013. I valori legacy di **DeliveryType** sono:

  - **MapiDelivery**   La coda contiene i messaggi per il recapito da parte di un server Trasporto Hub di Exchange 2007 o Exchange 2010 a una cassetta postale su un server Cassette postali di Exchange 2007 o Exchange 2010 nel sito Active Directory locale.

  - **SmtpRelayWithinAdSite**   La coda contiene i messaggi per il recapito da parte di un server Trasporto Edge di Exchange 2007 o Exchange 2010 a un altro server Trasporto Edge nello stesso sito Active Directory. Il server Trasporto Hub di destinazione può essere il server di origine per un connettore o un server di espansione del gruppo di distribuzione.

  - **SmtpRelaytoTiRg**   La coda contiene i messaggi per il recapito da parte di un server Trasporto Hub di Exchange 2007 o Exchange 2010 a un gruppo di routing di Exchange Server 2003. Il server di destinazione può essere il server di origine di un connettore, un server di espansione del gruppo di distribuzione o un server testa di ponte di Exchange 2003.

Inizio pagina

## IncomingRate, OutgoingRate e Velocity

Exchange 2013 misura la percentuale di messaggi che entrano ed escono da una coda e archivia i valori ottenuti nelle proprietà della coda. È possibile utilizzare questi valori come indicatore dell'integrità del server di trasporto e della coda. Le proprietà sono:

  - **IncomingRate**   Questa proprietà indica la percentuale di messaggi che entrano nella coda.
    
    Questo valore corrisponde alla media del numero di messaggi che entra nella coda ogni 5 secondi calcolata negli ultimi 60 secondi. La formula può essere espressa come `(i1+i2+i3+i4+i5+i6)/6`, dove i*n* = il numero di messaggi in arrivo in 5 secondi.

  - **OutgoingRate**   Questa proprietà indica la percentuale di messaggi che escono dalla coda.
    
    Questo valore corrisponde alla media del numero di messaggi che esce dalla coda ogni 5 secondi calcolata negli ultimi 60 secondi. La formula può essere espressa come `(o1+o2+o3+o4+o5+o6)/6`, dove i*n* = il numero di messaggi in uscita in 5 secondi.

  - **Velocity**   Questa proprietà indica la velocità di esaurimento della coda e viene calcolato sottraendo il valore di **IncomingRate** dal valore di **OutgoingRate**.
    
    Se il valore di **Velocity** è maggiore di 0, i messaggi lasciano la coda più velocemente di quanto entrano.
    
    Se il valore di **Velocity** è uguale a 0, la velocità con cui i messaggi lasciano e quella con cui entrano corrispondono. Questo è anche il valore visualizzato quando la coda è inattiva.
    
    Se il valore di **Velocity** è minore di 0, i messaggi entrano nella coda più velocemente di quanto escono.

A livello base, un valore positivo per **Velocity** indica una coda integra che si svuota correttamente mentre un valore negativo per **Velocity** indica una coda inefficiente. Tuttavia, è anche possibile considerare i valori delle proprietà **IncomingRate**, **OutgoingRate** e **MessageCount**, nonché la grandezza del valore **Velocity** per la coda. Ad esempio, un valore negativo elevato per **Velocity**, un valore elevato per **MessageCount**, un valore piccolo per **OutgoingRate** e un valore elevato per **IncominRate** sono indicatori accurati che la coda non si svuota in maniera efficiente. Tuttavia, una coda con un valore negativo per **Velocity** molto vicino a zero e con valori piccoli per **IncomingRate**, **OutgoingRate** e **MessageCount** non indica la presenza di un problema.

Inizio pagina

## Stato della coda

Lo stato corrente della coda è archiviato nella proprietà **Status** della coda. Una coda può assumere uno dei seguenti valori di stato:

  - **Attiva**   La coda sta attivamente trasmettendo messaggi.

  - **Connessione**   La coda è in fase di connessione al successivo hop.

  - **Pronta**   La coda ha recentemente trasmesso messaggi ma adesso è vuota.

  - **Retry**   L'ultimo tentativo di connessione automatica o manuale non è riuscito e la coda è in attesa di ritentare la connessione.

  - **Sospesa**   La coda è stata sospesa manualmente da un amministratore per evitare il recapito dei messaggi. Nuovi messaggi possono entrare nella coda e quelli che sono in fase di trasmissione al successivo hop verranno recapitati e lasceranno la coda. In caso contrario, i messaggi non lasceranno la coda finché essa non viene ripresa manualmente da un amministratore. Tener presente che la sospensione di una coda non cambia lo stato dei singoli messaggi nella coda.
    
    È possibile sospendere una coda il cui stato sia Attivo o Riprova. Inoltre, è possibile sospendere la coda dei messaggi con destinatari non raggiungibili e la coda di invio.
    
    Se si sospende la coda non raggiungibile, i messaggi non saranno automaticamente reinviati al classificatore quando vengono rilevati aggiornamenti della configurazione. Per reinviare automaticamente i messaggi, è necessario riprendere manualmente la coda non raggiungibile. Se si sospende la coda di invio, i messaggi non verranno recuperati dal classificatore finché la coda non verrà ripristinata.

Inizio pagina

## Altre proprietà della coda

Esistono altre proprietà della coda di chiara interpretazione. La maggior parte delle proprietà delle code vengono utilizzate come opzioni del filtro. Specificando i criteri del filtro, è possibile individuare rapidamente le code e agire su di esse. Per una descrizione completa delle proprietà delle code filtrabili, vedere [Filtri di coda](queue-filters-exchange-2013-help.md).

Una proprietà importante delle code che vale la pena di ricordare è la proprietà **MessageCount**, che mostra il numero di messaggi presenti in una coda. Questa proprietà è un indicatore importante dell'integrità della coda. Ad esempio, una coda di recapito che contiene un elevato numero di messaggi che continuano ad aumentare e non diminuiscono mai indica un problema con la pipeline di routing o trasporto che richiede attenzione.

Inizio pagina

## Proprietà del messaggio

Un messaggio in una coda presenta numerose proprietà Molte proprietà riflettono le informazioni utilizzate per creare il messaggio. Alcune proprietà informative e di stato dei messaggi sono pesantemente influenzate dalle proprietà corrispondenti nella coda. Tuttavia, un singolo messaggio può avere un valore diverso rispetto alla proprietà corrispondente della coda. Altre proprietà contengono lo stato, il tempo o altri indicatori che vengono aggiornati di frequente.

Inizio pagina

## Stato del messaggio

Lo stato corrente di un messaggio è archiviato nella proprietà **Status** della coda. Un messaggio può assumere uno dei seguenti valori di stato:

  - **Active**   Se il messaggio si trova in una coda di recapito, sarà recapitato alla destinazione indicata. Se il messaggio si trova nella coda di invio, sarà elaborato dal classificatore.

  - **Locked**   Questo valore è riservato per uso interno da parte di Microsoft e non viene utilizzato nelle organizzazioni Exchange locali.

  - **PendingRemove**   Il messaggio è stato eliminato dall'amministratore ma era già in fase di trasmissione al successivo hop. Il messaggio viene eliminato se l'operazione di recapito termina con un errore che determina la ricollocazione del messaggio nella coda. In caso contrario, il messaggio viene recapitato.

  - **PendingSuspend**   Il messaggio è stato sospeso dall'amministratore ma era già in fase di trasmissione al successivo hop. Il messaggio viene sospeso se l'operazione di recapito termina con un errore che determina la ricollocazione del messaggio nella coda. In caso contrario, il messaggio viene recapitato.

  - **Ready**   Il messaggio è in attesa nella coda ed è pronto per l'elaborazione.

  - **Retry**   L'ultimo tentativo di collegamento automatico o manuale per la coda in cui si trova il messaggio non ha avuto esito positivo. Il messaggio è in attesa del prossimo tentativo di connessione automatica alla coda.

  - **Suspended**   Il messaggio è stato manualmente sospeso dall'amministratore. Tutti i messaggi nella coda dei messaggi non elaborabili sono in uno stato di sospensione permanente.

Inizio pagina

## Altre proprietà dei messaggi

Esistono altre proprietà dei messaggi di chiara interpretazione. La maggior parte delle proprietà dei messaggi vengono utilizzate come opzioni del filtro. Specificando i criteri di filtro, è possibile individuare rapidamente i messaggi ed eseguire delle azioni. Per una descrizione completa delle proprietà dei messaggi filtrabili, vedere [Filtri per i messaggi](message-filters-exchange-2013-help.md).

Inizio pagina

## Gestione delle code e dei messaggi nelle code

Il Visualizzatore code e virtualmente tutti i tutti i cmdlet di gestione delle code e dei messaggi sono limitati a un singolo server Exchange. È possibile visualizzare o eseguire azioni su singole code o messaggi o su più code o messaggi, ma solo su uno specifico server.

Exchange 2013 introduce il cmdlet **Get-QueueDigest** che fornisce una visualizzazione aggregata di alto livello dello stato delle code su tutti i server in uno specifico ambito, ad esempio un gruppo di disponibilità del database, un sito Active Directory, un elenco di server o l'intera foresta Active Directory. Le code su un server Trasporto Edge sottoscritto nella rete perimetrale non sono incluse nei risultati. Inoltre, **Get-QueueDigest** è disponibile su un server Trasporto Edge, ma i risultati sono limitati alle code sul server Trasporto Edge.


> [!NOTE]
> Per impostazione predefinita, il cmdlet <STRONG>Get-QueueDigest</STRONG> visualizza le code di recapito contenenti dieci o più messaggi. I risultati restituiti risalgono da uno a due minuti prima. Per istruzioni su come modificare i valori predefiniti, vedere <A href="configure-get-queuedigest-exchange-2013-help.md">Configurazione di Get-QueueDigest</A>.



Nella tabella seguente vengono descritte le attività di gestione che è possibile eseguire sulle code o sui messaggi nelle code.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attività</th>
<th>Descrizione</th>
<th>Strumento da utilizzare</th>
<th>Istruzioni</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Visualizzazione e filtraggio delle code in un server</p></td>
<td><p>Questa azione visualizza una o più code in un server di trasporto. È possibile utilizzare i risultati per eseguire azioni sulle code.</p></td>
<td><p>Il Visualizzatore code o il cmdlet <strong>Get-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gestire le code</a></p></td>
</tr>
<tr class="even">
<td><p>Visualizzazione e filtraggio delle code su specifici server in specifici gruppi di disponibilità del database, specifici siti Active Directory o nell'intera foresta di Active Directory.</p></td>
<td><p>Questa azione mostra una visualizzazione sintetica delle code in un ambito definito (server, gruppi di disponibilità del database, sito Active Directory o l'intera foresta Active Directory).</p></td>
<td><p>Solo cmdlet <strong>Get-QueueDigest</strong></p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gestire le code</a></p></td>
</tr>
<tr class="odd">
<td><p>Sospensione delle code</p></td>
<td><p>Questa azione impedisce temporaneamente il recapito dei messaggi presenti nella coda. La coda continua ad accettare nuovi messaggi ma nessun messaggio lascia la coda.</p></td>
<td><p>Il Visualizzatore code o il cmdlet <strong>Suspend-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gestire le code</a></p></td>
</tr>
<tr class="even">
<td><p>Ripresa delle code</p></td>
<td><p>Questa azione inverte l'effetto dell'azione di sospensione della coda e consente di riprendere il recapito dei messaggi in coda.</p></td>
<td><p>Il Visualizzatore code o il cmdlet <strong>Resume-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gestire le code</a></p></td>
</tr>
<tr class="odd">
<td><p>Nuovo tentativo di elaborazione delle code</p></td>
<td><p>Questa azione tenta immediatamente la connessione al successivo hop. Senza intervento manuale, quando la connessione al successivo hop non riesce, la connessione viene tentata per un determinato numero di volte in base a uno specifico intervallo di tempo.</p>
<p>Quando il tentativo di connessione è manuale o automatico, eventuali tentativi di connessione reimpostano l'ora del successivo tentativo. Per ulteriori informazioni, vedere <a href="message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md">Intervalli di ripetizione, reinvio e scadenza messaggio</a>.</p></td>
<td><p>Il Visualizzatore code o il cmdlet <strong>Retry-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gestire le code</a></p></td>
</tr>
<tr class="even">
<td><p>Reinvio dei messaggi in coda</p></td>
<td><p>Questa azione causa il reinvio dei messaggi nella coda alla coda di invio e la riesecuzione del processo di categorizzazione.</p></td>
<td><p><strong>Retry-Queue</strong> con il parametro <em>Resubmit</em></p>
<p>Tenere presente che è possibile utilizzare il Visualizzatore code per reinviare i messaggi ma solo dalla coda dei messaggi non elaborabili. Per reinviare i messaggi nella coda dei messaggi non elaborabili, è necessario ripristinare il messaggio nel Visualizzatore code o utilizzare il cmdlet <strong>Resume-Message</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Gestire le code</a></p></td>
</tr>
<tr class="odd">
<td><p>Sospensione dei messaggi in coda</p></td>
<td><p>Questa azione impedisce temporaneamente il recapito di un messaggio. L'azione di sospensione dei messaggi può essere utilizzata per impedire il recapito di un messaggio a tutti i destinatari di una coda specifica o a tutti i destinatari di tutte le code.</p></td>
<td><p>Il Visualizzatore code o il cmdlet <strong>Suspend-Message</strong>.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Gestione dei messaggi nelle code</a></p></td>
</tr>
<tr class="even">
<td><p>Ripristino dei messaggi in coda</p></td>
<td><p>Questa azione inverte l'effetto dell'azione di sospensione dei messaggi e consente di riprendere il recapito dei messaggi in coda. L'azione di ripresa del recapito dei messaggi può essere utilizzata per riprendere il recapito di un messaggio a tutti i destinatari di una coda specifica o a tutti i destinatari di tutte le code.</p></td>
<td><p>Il Visualizzatore code o il cmdlet <strong>Resume-Message</strong>.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Gestione dei messaggi nelle code</a></p></td>
</tr>
<tr class="odd">
<td><p>Eliminazione dei messaggi dalle code</p></td>
<td><p>Questa azione impedisce permanentemente il recapito di un messaggio. L'azione di rimozione dei messaggi può essere utilizzata per impedire il recapito di un messaggio ai destinatari di una coda specifica o a tutti i destinatari di tutte le code. È inoltre possibile configurare l'azione di rimozione dei messaggi per inviare un rapporto di mancato recapito (NDR) al mittente quando il messaggio viene rimosso.</p></td>
<td><p>Il Visualizzatore code o il cmdlet <strong>Remove-Message</strong>.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Gestione dei messaggi nelle code</a></p></td>
</tr>
<tr class="even">
<td><p>Esportazione dei messaggi dalle code</p></td>
<td><p>Questa azione copia un messaggio nel percorso file specificato dall'utente. I messaggi non vengono eliminati dalla coda, ma ne viene salvata una copia nel percorso specificato. In questo modo amministratori e dirigenti di un'organizzazione possono esaminare i messaggi in un momento successivo. Prima di esportare un messaggio, è necessario sospenderlo nella coda in modo che la normale operazione di recapito non venga continuata durante il processo di esportazione.</p></td>
<td><p>Solo il cmdlet <strong>Export-Message</strong>.</p></td>
<td><p><a href="export-messages-from-queues-exchange-2013-help.md">Esportazione dei messaggi dalle code</a></p></td>
</tr>
</tbody>
</table>


Inizio pagina


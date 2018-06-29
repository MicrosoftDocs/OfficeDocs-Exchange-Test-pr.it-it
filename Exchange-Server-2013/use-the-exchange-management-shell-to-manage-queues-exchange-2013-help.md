---
title: 'Utilizzare Exchange Management Shell per gestire le code: Exchange 2013 Help'
TOCTitle: Utilizzare Exchange Management Shell per gestire le code
ms:assetid: 5433c1d3-ad2e-4f82-b50d-b67964b32f26
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998047(v=EXCHG.150)
ms:contentKeyID: 51407366
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzare Exchange Management Shell per gestire le code

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Come nelle versioni precedenti di Exchange, è possibile utilizzare Exchange Management Shell in Microsoft Exchange Server 2013 per visualizzare le informazioni sulle code e i messaggi in tali code e per eseguire azioni di gestione su code e messaggi. In Exchange 2013, le code si trovano nei server Cassette postali e Trasporto Edge. In questo argomento viene fatto riferimento ai *server di trasporto*.

Quando si utilizza Shell per visualizzare e gestire le code e i messaggi in coda sui server di trasporto, è importante capire come identificare le code o i messaggi che si intende gestire. In genere, i server di trasporto contengono un gran numero di code e messaggi da consegnare. Si utilizzano i parametri di filtro che sono disponibili sulla coda e sui cmdlet di gestione dei messaggi per identificare le code o i messaggi che si intendono visualizzare o gestire.

È anche possibile utilizzare il Visualizzatore code nella casella degli strumenti di Exchange per la gestione di code e messaggi in coda. Tuttavia, la coda e i cmdlet di visualizzazione messaggio supportano le proprietà valide per il filtro e le opzioni di filtro del Visualizzatore code. Per ulteriori informazioni sul Visualizzatore code, vedere [Visualizzatore code](queue-viewer-exchange-2013-help.md).

**Sommario**

  - Queue filtering parameters
    
      - Queue identity
    
      - Queue Filter parameter
    
      - Include and Exclude parameters

  - Get-QueueDigest

  - Message filtering parameters
    
      - Message identity
    
      - Message Filter parameter
    
      - Queue parameter

  - Comparison operators to use when filtering queues or messages

  - Advanced paging parameters

## Parametri filtro della coda

Nella tabella seguente vengono descritti i parametri di filtro disponibili sui cmdlet di gestione delle code.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Parametri di filtro</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Include</em></p>
<p><em>Exclude</em></p></td>
<td><p>Non è possibile utilizzare il parametro <em>Identity</em> nello stesso comando con i parametri <em>Filter</em>. È possibile utilizzare il parametro <em>Include</em> e i parametri <em>Exclude</em> con il parametro <em>Filter</em> nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><strong>Resume-Queue</strong></p>
<p><strong>Retry-Queue</strong></p>
<p><strong>Suspend-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p>È necessario utilizzare il parametro <em>Identity</em> oppure il parametro <em>Filter</em>, sebbene sia possibile utilizzarli entrambi nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get-QueueDigest</strong></p></td>
<td><p><em>Server</em></p>
<p><em>Dag</em></p>
<p><em>Site</em></p>
<p><em>Forest</em></p>
<p><em>Filter</em></p></td>
<td><p>È necessario utilizzare il parametro <em>Server</em>, <em>Dag</em>, <em>Site</em> oppure il parametro <em>Forest</em>, sebbene non sia possibile utilizzarli insieme nello stesso comando. È possibile utilizzare il parametro <em>Filter</em> con uno degli altri parametri di filtro.</p></td>
</tr>
</tbody>
</table>


Il parametro *Server* è disponibile su tutti i cmdlet di gestione delle code. Sul cmdlet **Get-QueueDigest**, il parametro *Server* è un parametro di ambito che specifica il server o i server in cui si intendono visualizzare le informazioni di riepilogo riguardo alle code. Su tutti gli altri cmdlet di gestione delle code, si utilizza il parametro *Server* per la connessione a un server specifico e l'esecuzione dei comandi di gestione delle code sul server. È possibile utilizzare il parametro *Server* con o senza il parametro *Filter*, ma è anche possibile utilizzare il parametro *Server* con il parametro *Identity*. Si utilizza il nome host o nome di dominio completo con il parametro *Server*.

Inizio pagina

## Identità delle code

Il parametro *Identity* sui cmdlet della code identifica una coda specifica. Quando si utilizza il parametro *Identity*, non è possibile specificare qualsiasi altro parametro filtro della coda, perché si è già identificato in modo univoco la coda. Il parametro *Identity* utilizza la sintassi di base *\<Server\>*\\*\<Coda\>*.

Il segnaposto *\<Server\>* corrisponde al nome host o al nome di dominio completo del server Exchange, ad esempio `mailbox01` oppure `mailbox01.contoso.com`. Se viene omesso il qualificatore *\<Server\>*, viene considerato il server locale.

Il segnaposto \<*Coda*\> accetta uno dei seguenti valori:

  - **Nome di coda persistente**   Le code persistenti dispongono di nomi unici e coerenti su tutti i server Cassette postali e Trasporto Edge. Di seguito i nomi delle code persistenti:
    
      - **Invio**   Questa coda contiene i messaggi in attesa di essere elaborati dal classificatore.
    
      - **Non raggiungibile**   Questa coda contiene messaggi che non possono essere instradati. Questa coda non esiste fino a quando i messaggi vengono inseriti in essa.
    
      - **Dannoso**   Questa coda contiene i messaggi definiti dannosi per il server di Exchange. Questa coda non esiste fino a quando i messaggi vengono inseriti in essa.

  - **Nome della coda di recapito**   Il nome di una coda di recapito è il valore della proprietà della coda **NextHopDomain**. Ad esempio, il nome della coda potrebbe essere lo spazio degli indirizzi di un connettore di invio, il nome di un sito di Active Directory oppure il nome di un DAG. Per ulteriori informazioni, vedere la sezione "NextHopSolutionKey" nell'argomento [Code](queues-exchange-2013-help.md).

  - **Coda intera**   Le code di recapito e le code ombra vengono assegnate a un valore intero univoco nel database delle code. Tuttavia, è necessario eseguire il cmdlet **Get-Queue** al fine di trovare il valore intero per la coda nelle proprietà **Identity** o **QueueIdentity**.

  - **Nome di coda ombra**   Una coda ombra utilizza la sintassi `Shadow\`*\<QueueInteger\>*

La tabella seguente riassume la sintassi che è possibile utilizzare con il parametro *Identity* sui cmdlet di gestione delle code. In tutti i valori, *\<Server\>* corrisponde al nome host o al nome di dominio completo del server.

### Formati di identità della coda

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valore del parametro di identità</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;PersistentQueueName&gt;</code> oppure <code>&lt;PersistentQueueName&gt;</code></p></td>
<td><p>Una coda persistente sul server specificato o il server locale.</p>
<p><em>&lt;PersistentQueueName&gt;</em> è <code>Submission</code>, <code>Unreachable</code> o <code>Poison</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\&lt;NextHopDomain&gt;</code> oppure <code>&lt;NextHopDomain&gt;</code></p></td>
<td><p>Una coda di recapito sul server specificato o il server locale.</p>
<p><em>&lt;NextHopDomain&gt;</em> è una destinazione di routing o di un gruppo di consegna per i messaggi in coda. Per ulteriori informazioni, vedere la sezione &quot;NextHopSolutionKey&quot; nell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;QueueInteger&gt;</code> oppure <code>&lt;QueueInteger&gt;</code></p></td>
<td><p>Una coda di recapito sul server specificato o il server locale.</p>
<p><em>&lt;QueueInteger&gt;</em> è il valore intero univoco della coda che viene visualizzato nella proprietà <strong>Identity</strong> del cmdlet <strong>Get-Queue</strong>.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\Shadow\&lt;QueueInteger&gt;</code> oppure <code>Shadow\&lt;QueueInteger&gt;</code></p></td>
<td><p>Una coda ombra sul server specificato o il server locale.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\*</code> oppure <code>*</code></p></td>
<td><p>Tutte le code sul server specificato o il server locale. È possibile utilizzare questi valori con il cmdlet <strong>Get-Queue</strong>.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Parametro del filtro coda

È possibile utilizzare il parametro *Filter* in tutti i cmdlet di gestione delle code per specificare le code che si intende visualizzare o gestire sulla base delle proprietà delle code. Il parametro *Filter* crea un'espressione con operatori di confronto che limita l'operazione di coda per le code che soddisfano i criteri di filtro. È possibile utilizzare l'operatore logico `-and` per specificare diverse condizioni cui è necessario che corrispondano i risultati.

Per un elenco completo delle proprietà della coda è possibile utilizzare il parametro *Filter*, vedere [Code](queues-exchange-2013-help.md).

Per un elenco di operatori di confronto è possibile utilizzare il *Filter* parametro, vedere la sezione in questo argomento Comparison operators to use when filtering queues or messages.

Per esempi di procedure che utilizzano il parametro *Filter* per visualizzare e gestire le code, vedere [Gestire le code](manage-queues-exchange-2013-help.md).

Inizio pagina

## Includere e escludere i parametri

Exchange 2013 dispone del *Include* e dei parametri *Exclude* disponibili sul cmdlet `Get-Queue`. È possibile utilizzare questi parametri singolarmente, insieme e con il parametro *Filter* per ritoccare i risultati della coda sul server di trasporto locale o specificato. Ad esempio, è possibile compiere queste operazioni:

  - Escludere code vuote dai risultati.

  - Escludere code per destinazioni esterne dai risultati.

  - Includere nei risultati le code che hanno un valore specifico di **DeliveryType**.

I parametri *Include* e *Exclude* utilizzano le seguenti proprietà della coda per filtrare le code:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Valore</th>
<th>Descrizione</th>
<th>Esempio di codice Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>DeliveryType</code></p></td>
<td><p>Questo valore include o esclude le code in base alla proprietà <strong>DeliveryType</strong>. È possibile specificare più valori separati da virgole. I valori validi per <strong>DeliveryType</strong> vengono descritti nella sezione &quot;NextHopSolutionKey&quot; sotto l'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
<td><p>In questo esempio vengono restituite tutte le code di recapito sul server locale dove l'hop successivo è un connettore di invio sul server locale configurato per il routing SmartHost:</p>
<p><code>Get-Queue -Include SmartHostConnectorDelivery</code></p></td>
</tr>
<tr class="even">
<td><p><code>Empty</code></p></td>
<td><p>Questo valore include o esclude le code vuote. Le code vuote hanno il valore <code>0</code> nella proprietà <strong>MessageCount</strong>.</p></td>
<td><p>In questo esempio vengono restituite tutte le code sul server locale che contiene i messaggi</p>
<p><code>Get-Queue -Exclude Empty</code></p></td>
</tr>
<tr class="odd">
<td><p><code>External</code></p></td>
<td><p>Questo valore include o esclude le code che hanno <code>External</code> nella proprietà <strong>NextHopCategory</strong>.</p>
<p>Le code esterni hanno sempre uno dei seguenti valori per <strong>DeliveryType</strong>:</p>
<ul>
<li><p><code>DeliveryAgent</code></p></li>
<li><p><code>DnsConnectorDelivery</code></p></li>
<li><p><code>NonSmtpGatewayDelivery</code></p></li>
<li><p><code>SmartHostConnectorDelivery</code></p></li>
</ul>
<p>Per ulteriori informazioni, vedere la sezione &quot;NextHopSolutionKey&quot; nell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
<td><p>In questo esempio vengono restituite tutte le code interne sul server locale.</p>
<p><code>Get-Queue -Exclude External</code></p></td>
</tr>
<tr class="even">
<td><p><code>Internal</code></p></td>
<td><p>Questo valore include o esclude le code che hanno il valore <code>Internal</code> nella proprietà <strong>NextHopCategory</strong>. Per ulteriori informazioni, vedere la sezione &quot;NextHopSolutionKey&quot; nell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
<td><p>In questo esempio vengono restituite tutte le code interne sul server locale.</p>
<p><code>Get-Queue -Include Internal</code></p></td>
</tr>
</tbody>
</table>


È possibile duplicare la funzionalità dei parametri *Include* e *Exclude* tramite il parametro *Filter*. Ad esempio,il comando `Get-Queue -Exclude Empty` produce lo stesso risultato di `Get-Queue -Filter {MessageCount -gt 0}`. Tuttavia, la sintassi dei parametri *Include* e *Exclude* è più semplice e più agevole da ricordare.

Inizio pagina

## Get-QueueDigest

Exchange 2013 aggiunge un nuovo cmdlet della coda denominato **Get-QueueDigest**. Questo cmdlet consente di visualizzare informazioni su alcune o tutte le code nell'organizzazione di Exchange utilizzando un unico comando. In particolare, il cmdlet **Get-QueueDigest** consente di visualizzare le informazioni sulle code in base alla loro percorso sui server, nel DAG, nei siti di Active Directory o in tutta la foresta di Active Directory. Considerare che le code su un server Trasporto Edge sottoscritto nella rete perimetrale non sono inclusi nei risultati. Inoltre, **Get-QueueDigest** è disponibile su server Trasporto Edge ma i risultati sono limitati alle code sul server Trasporto Edge.


> [!NOTE]
> Per impostazione predefinita, il cmdlet <STRONG>Get-QueueDigest</STRONG> visualizza le code di recapito contenenti dieci o più messaggi. I risultati restituiti risalgono da uno a due minuti prima. Per istruzioni su come modificare i valori predefiniti, vedere <A href="configure-get-queuedigest-exchange-2013-help.md">Configurazione di Get-QueueDigest</A>.



I parametri di filtro e ordinamento disponibili col cmdlet **Set-ContentFilterConfig** vengono descritti nella tabella seguente.


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
<td><p><em>Dag</em>, <em>Server</em> o <em>Site</em></p></td>
<td><p>Questi parametri si escludono a vicenda e impostano l'ambito per il cmdlet. È necessario specificare uno di questi parametri o il <em>Forest</em> opzionale. In genere, si utilizza il nome del server, DAG o di un sito di Active Directory, ma è possibile utilizzare qualsiasi valore che identifica in modo univoco il server, un DAG o un sito. È possibile specificare diversi server, DAG o siti separandoli con le virgole.</p></td>
</tr>
<tr class="even">
<td><p><em>Forest</em></p></td>
<td><p>Questa opzione è necessaria se non si utilizza <em>Dag</em>, <em>Server</em> o i parametri <em>Site</em>. Non è necessario specificare un valore per questa opzione. Utilizzando questa opzione, è possibile ottenere code da tutti i server Cassette postali di Exchange 2013 nella foresta di Active Directory. Non è possibile utilizzare il parametro <em>Forest</em> opzionale per visualizzare le code nelle foreste remote di Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><em>DetailsLevel</em></p></td>
<td><p>Questo parametro accetta i valori <code>None</code>, <code>Normal</code> e <code>Verbose</code>. Il valore predefinito è <code>Normal</code>. Quando si utilizza il valore <code>None</code>, il nome della coda viene omesso dalla colonna <strong>Dettagli</strong> nei risultati.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Questo parametro consente di filtrare le code in base alle proprietà della coda. È possibile utilizzare una qualsiasi delle proprietà della coda filtrabile come descritto nell'argomento <a href="queue-filters-exchange-2013-help.md">Filtri di coda</a>.</p></td>
</tr>
<tr class="odd">
<td><p><em>GroupBy</em></p></td>
<td><p>Questo parametro raggruppa i risultati della coda. È possibile raggruppare i risultati in base a una delle seguenti proprietà:</p>
<ul>
<li><p>DeliveryType</p></li>
<li><p>LastError</p></li>
<li><p>NextHopCategory</p></li>
<li><p>NextHopDomain</p></li>
<li><p>NextHopKey</p></li>
<li><p>Stato</p></li>
<li><p>NomeServer</p></li>
</ul>
<p>Per impostazione predefinita, i risultati sono raggruppati per <code>NextHopDomain</code>. Per ulteriori informazioni su queste proprietà delle code, vedere <a href="queue-filters-exchange-2013-help.md">Filtri di coda</a>.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Questo parametro limita i risultati delle code al valore specificato. Le code sono disposte in ordine decrescente in base al numero di messaggi nella coda e raggruppate in base al valore specificato dal parametro<em>GroupBy</em>. Il valore di default è 1000. Ciò significa che, per impostazione predefinita, il comando visualizza le prime 1000 code raggruppate per <strong>NextHopDomain</strong> e ordinate in base alle code che contengono più messaggi e alle code che ne contengono in minor quantità.</p></td>
</tr>
<tr class="odd">
<td><p><em>Timeout</em></p></td>
<td><p>Il parametro specifica il numero di secondi prima del timeout dell'operazione. Il valore predefinito è <code>00:00:10</code> o 10 secondi.</p></td>
</tr>
</tbody>
</table>


In questo esempio vengono restituite tutte le code esterni non vuote sui server Exchange 2013 Cassette postali denominati Mailbox01,Mailbox02 e Mailbox03.

    Get-QueueDigest -Server Mailbox01,Mailbox02,Mailbox03 -Include External -Exclude Empty

Inizio pagina

## Parametri di filtro messaggi

Nella tabella seguente vengono descritti i parametri di filtro disponibili sui cmdlet di gestione dei messaggi.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Parametri di filtro</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Queue</em></p></td>
<td><p>Tutti i parametri di filtro si escludono a vicenda e è possibile utilizzarli insieme nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><strong>Remove-Message</strong></p>
<p><strong>Resume-Message</strong></p>
<p><strong>Suspend-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p>È necessario utilizzare il parametro <em>Identity</em> o <em>Filter</em>, sebbene non sia possibile farlo nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Export-Message</strong></p></td>
<td><p><em>Identity</em></p></td>
<td><p>Il parametro <em>Identity</em> è obbligatorio.</p></td>
</tr>
</tbody>
</table>


Un parametro *Server* è disponibile in tutti i cmdlet di gestione dei messaggi ad eccezione del cmdlet **Export-Message**. Si utilizza il parametro *Server* per connettere un server specifico e eseguire i comandi di gestione dei messaggi sul server. È possibile utilizzare il parametro *Server* con o senza il parametro *Filter*, ma non è possibile utilizzare il parametro *Server* con il parametro *Identity*. Si utilizza il nome host o il nome di dominio completo del server di trasporto con il parametro *Server*.

Inizio pagina

## Identità del messaggio

Il parametro *Identity* sui cmdlet di gestione dei messaggi identifica uno specifico messaggio in una o più code. Quando si utilizza il parametro *Identity*, non è possibile specificare i parametri di filtro di qualsiasi altro messaggio perché si è già identificato in modo univoco il messaggio. Il parametro *Identity* utilizza la sintassi di base *\<Server\>*\\*\<Coda\>*\\*\<NumeroMessaggio\>*.

Il segnaposto *\<Server\>* è il nome host o nome di dominio completo del server di Exchange, ad esempio `mailbox01` o `mailbox01.contoso.com`. Se si omette il qualificatore *\<Server\>*, viene considerato il server locale.

Il segnaposto \<*Coda*\> accetta l'identità della coda come descritto nella sezione "Identità coda" in questo argomento. Ad esempio, è possibile utilizzare il nome della coda persistente, il valore **NextHopDomain** o il valore intero univoco della coda nel database delle code.

Il segnaposto *\<NumeroMessaggio\>* rappresenta il valore intero univoco assegnato al messaggio quando immette dapprima il database della coda sul server. Se il messaggio viene inviato a più destinatari che richiedono più code, tutte le copie del messaggio in tutte le code nel database della coda hanno lo stesso numero intero. Tuttavia, è necessario eseguire il cmdlet **Get-Message** per trovare il numero intero per il messaggio nelle proprietà **Identity** o **MessageIdentity**.

Nella seguente tabella viene riportata la sintassi che è possibile utilizzare con il parametro *Identity* sui cmdlet di gestione dei messaggi. In tutti i valori, *\<Server\>* rappresenta il nome host o il numero di dominio completo del server.

### Formati di identità del messaggio

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valore del parametro di identità</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</code> oppure <code>&lt;Queue&gt;\&lt;MessageInteger&gt;</code></p></td>
<td><p>Un messaggio in una coda specifica sul server specificato o il server locale.</p>
<p><em>&lt;MessageInteger&gt;</em> è il valore intero univoco della coda che viene visualizzato nella proprietà <strong>Identity</strong> del cmdlet <strong>Get-Message</strong>.</p>
<p><em>&lt;Coda&gt;</em> rappresenta uno dei seguenti valori:</p>
<ul>
<li><p><strong>Nome di coda persistente</strong>   Il valore <code>Submission</code>, <code>Unreachable</code> o <code>Poison</code>.</p></li>
<li><p><strong>Nome di coda di recapito</strong>   Il valore della proprietà <strong>NextHopDomain</strong> della coda (effettivamente il nome della coda). Questo valore può essere una destinazione di instradamento o un gruppo di recapito. Per ulteriori informazioni, vedere la sezione &quot;NextHopSolutionKey&quot; nell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></li>
<li><p><strong>Numero intero della coda</strong>   Il valore intero univoco della coda di recapito o della coda di ombra che viene visualizzato nella proprietà <strong>Identity</strong> dei cmdlet <strong>Get-Message</strong> o <strong>Get-Queue</strong>.</p></li>
<li><p><strong>Identità coda di ombra</strong>   L'identità della coda di ombra utilizza la sintassi <code>Shadow\&lt;QueueInteger&gt;</code>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\*\&lt;MessageInteger&gt;</code> o <code>*\&lt;MessageInteger&gt;</code> oppure <code>&lt;MessageInteger&gt;</code></p></td>
<td><p>Tutte le copie del messaggio in tutte le code del database della coda sul server specificato o il server locale.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Parametro di filtro messaggi

È possibile utilizzare il parametro *Filter* sui cmdlet **Get-Message**, **Remove-Message**, **Resume-Message** e **Suspend-Message** per specificare i messaggi che si intendono visualizzare o gestire in base alle proprietà dei messaggi. Il parametro *Filter* crea un'espressione con operatori di confronto che limita l'operazione messaggio ai messaggi che soddisfano i criteri di filtro. È possibile utilizzare l'operatore logico `-and` per specificare diverse condizioni cui è necessario corrispondano i risultati.

Per un elenco completo delle proprietà dei messaggi è possibile utilizzare il parametro *Filter*, vedere [Code](queues-exchange-2013-help.md).

Per un elenco di operatori di confronto è possibile utilizzare il parametro *Filter*, vedere la sezione in questo argomento Comparison operators to use when filtering queues or messages.

Per esempi di procedure che utilizzano il parametro *Filter* per visualizzare e gestire i messaggi, vedere [Gestire le code](manage-queues-exchange-2013-help.md).

Inizio pagina

## Parametro di coda

Il parametro *Queue* viene utilizzato esclusivamente col cmdlet **Get-Message**. È possibile utilizzare questo parametro per ottenere tutti i messaggi in una coda specifica o tutti i messaggi da più code utilizzando il carattere jolly (\*). Il parametro *Queue* utilizza il formato identità della coda *\<Server\>*\\*\<Coda\>* come descritto nella sezione "Identità coda" in questo argomento.

Inizio pagina

## Gli operatori di confronto da utilizzare durante le operazioni di filtro code o messaggi

Quando si crea una coda o un'espressione del filtro messaggi utilizzando il parametro *Filter*, è necessario includere un operatore di confronto per il valore della proprietà in modo che corrisponda. Nella seguente tabella vengono riportati gli operatori di confronto che è possibile utilizzare in un'espressione del filtro e il funzionamento di ciascun operatore. Per tutti gli operatori i valori confrontati non fanno distinzione tra maiuscole e minuscole.

### Operatori di confronto

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Operatore</th>
<th>Funzione</th>
<th>Esempio di codice Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>-eq</code></p></td>
<td><p>Questo operatore viene utilizzato per specificare che i risultati devono corrispondere esattamente al valore della proprietà fornito nell'espressione.</p></td>
<td><p>Per visualizzare un elenco di tutte le code il cui stato è Riprova:</p>
<p><code>Get-Queue -Filter {Status -eq &quot;Retry&quot;}</code></p>
<p>Per visualizzare un elenco di tutti i messaggi il cui stato è Riprova:</p>
<p><code>Get-Message -Filter {Status -eq &quot;Retry&quot;}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ne</code></p></td>
<td><p>Questo operatore viene utilizzato per specificare che i risultati non devono corrispondere al valore della proprietà fornito nell'espressione.</p></td>
<td><p>Per visualizzare un elenco di tutte le code il cui stato non è Attivo:</p>
<p><code>Get-Queue -Filter {Status -ne &quot;Active&quot;}</code></p>
<p>Per visualizzare un elenco di tutti i messaggi il cui stato non è Attivo:</p>
<p><code>Get-Message -Filter {Status -ne &quot;Active&quot;}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-gt</code></p></td>
<td><p>Questo operatore viene utilizzato con le proprietà in cui il valore viene espresso come numero intero o come data e ora. I risultati del filtro includono esclusivamente i messaggi o le code dove il valore della proprietà specificata è maggiore del valore fornito nell'espressione.</p></td>
<td><p>Per visualizzare un elenco delle code che contengono più di 1.000 messaggi:</p>
<p><code>Get-Queue -Filter {MessageCount -gt 1000}</code></p>
<p>Per visualizzare un elenco di messaggi il cui numero di tentativi è attualmente maggiore di 3:</p>
<p><code>Get-Message -Filter {RetryCount -gt 3}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ge</code></p></td>
<td><p>Questo operatore viene utilizzato con le proprietà in cui il valore viene espresso come numero intero o come data e ora. I risultati del filtro includono esclusivamente i messaggi e le code dove il valore della proprietà specificata è maggiore o uguale al valore fornito nell'espressione.</p></td>
<td><p>Per visualizzare un elenco delle code che contengono 1.000 o più messaggi:</p>
<p><code>Get-Queue -Filter {MessageCount -ge 1000}</code></p>
<p>Per visualizzare un elenco di messaggi il cui numero di tentativi è attualmente uguale o maggiore di 3:</p>
<p><code>Get-Message -Filter {RetryCount -ge 3}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-lt</code></p></td>
<td><p>Questo operatore viene utilizzato con proprietà dove il valore viene espresso come numero intero o come data e ora. I risultati del filtro includono esclusivamente i messaggi e le code nelle quali il valore della proprietà specificata è minore del valore fornito nell'espressione.</p></td>
<td><p>Per visualizzare un elenco delle code che contengono meno di 1.000 messaggi:</p>
<p><code>Get-Queue -Filter {MessageCount -lt 1000}</code></p>
<p>Per visualizzare un elenco di messaggi il cui valore SCL è inferiore a 6:</p>
<p><code>Get-Message -Filter {SCL -lt 6}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-le</code></p></td>
<td><p>Questo operatore viene utilizzato con proprietà dove il valore viene espresso come numero intero o come data e ora. I risultati del filtro includono esclusivamente i messaggi e le code nelle quali il valore della proprietà specificata è minore o uguale al valore fornito nell'espressione.</p></td>
<td><p>Per visualizzare un elenco delle code che contengono 1.000 o meno messaggi:</p>
<p><code>Get-Queue -Filter {MessageCount -le 1000}</code></p>
<p>Per visualizzare un elenco di messaggi il cui valore SCL è minore o uguale a 6:</p>
<p><code>Get-Message -Filter {SCL -le 6}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-like</code></p></td>
<td><p>Questo operatore viene utilizzato con le proprietà in cui il valore viene espresso come stringa di testo. I risultati del filtro includono esclusivamente i messaggi e le code nelle quali il valore della proprietà specificata contiene una stringa di testo fornita nell'espressione. È possibile includere il carattere jolly (*) in un'espressione <strong>-like</strong> applicata a un campo stringa di testo, ma non a un campo di tipo enumerazione.</p></td>
<td><p>Per visualizzare un elenco delle code di recapito con destinazioni all'interno di un qualsiasi dominio SMTP che termina con Contoso.com:</p>
<p><code>Get-Queue -Filter {Identity -like &quot;*contoso.com&quot;}</code></p>
<p>Per visualizzare un elenco di messaggi il cui oggetto contiene il testo &quot;payday loan&quot;:</p>
<p><code>Get-Messages -Filter {Subject -like &quot;*payday loan*&quot;}</code></p></td>
</tr>
</tbody>
</table>


È possibile specificare un filtro che valuti più espressioni utilizzando l'operatore di confronto **-and**. Per essere inclusi nei risultati, è necessario che le code e i messaggi soddisfino tutte le condizioni del filtro.

In questo esempio viene visualizzato un elenco di code con destinazioni all'interno di un qualsiasi nome di dominio SMTP che termina con Contoso.com e che contiene più di 500 messaggi.

    Get-Queue -Filter {Identity -like "*contoso.com*" -and MessageCount -gt 500}

In questo esempio viene visualizzato un elenco di messaggi inviati da un qualsiasi indirizzo di posta elettronica del dominio contoso.com il cui valore SCL è maggiore di 5.

    Get-Message -Filter {FromAddress -like "*Contoso.com*" -and SCL -gt 5}

Inizio pagina

## Parametri di paging avanzati

In base al flusso di posta corrente, le query relative a code e messaggi possono restituire un insieme di oggetti di notevoli dimensioni. È possibile utilizzare i parametri di paging avanzati per controllare come verranno recuperati e visualizzati i risultati delle query.

Quando si utilizza Shell per visualizzare le code e i relativi messaggi, viene recuperata una pagina di informazioni alla volta. I parametri di paging avanzati consentono di controllare la dimensione dell'insieme di risultati, ma anche di ordinarli. Tutti i parametri di paging avanzati sono facoltativi e possono essere combinati con qualsiasi insieme di parametri utilizzabile con i cmdlet **Get-Queue** e **Get-Message**. Se non viene specificato alcun parametro di paging avanzato, la query restituisce i risultati in ordine crescente in base all'identità.

Per impostazione predefinita, quando si specifica un ordinamento, la proprietà relativa all'identità del messaggio viene sempre inclusa e ordinata in ordine crescente. Questa è la relazione di ordinamento predefinita. Viene inclusa la proprietà dell'identità del messaggio poiché le altre proprietà che possono essere incluse in un ordinamento non sono univoche. Includendo esplicitamente nell'ordinamento la proprietà relativa all'identità del messaggio, è possibile specificare che nei risultati l'identità del messaggio venga ordinata in ordine decrescente.

I parametri *BookmarkIndex* e *BookmarkObject* consentono di segnare una posizione nell'insieme di risultati ordinato. Se l'oggetto segnalibro non esiste più quando viene recuperata la pagina successiva di risultati, la relazione di ordinamento predefinita garantisce che l'insieme di risultati inizi dall'oggetto più vicino al segnalibro. L'oggetto più vicino dipende dall'ordinamento specificato.

Nella tabella seguente vengono descritti i parametri di paging avanzati.

### Parametri di paging avanzati

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
<td><p><em>BookmarkIndex</em></p></td>
<td><p>Il parametro consente di specificare la posizione nell'insieme di risultati da cui iniziano i risultati visualizzati. Il valore del parametro è un indice in base 1 nell'insieme dei risultati totale. Se il valore è inferiore o uguale a zero, verrà restituita la prima pagina completa dei risultati. Se il valore è impostato su <code>Int.MaxValue</code>, verrà restituita l'ultima pagina completa dei risultati.</p></td>
</tr>
<tr class="even">
<td><p><em>BookmarkObject</em></p></td>
<td><p>Il parametro consente di specificare l'oggetto nell'insieme di risultati da cui iniziano i risultati visualizzati. Una volta specificato, l'oggetto segnalibro viene utilizzato come punto per iniziare la ricerca. Verranno recuperate le righe precedenti o successive all'oggetto, in base al valore del parametro <em>SearchForward</em>. Non è possibile combinare il parametro <em>BookmarkObject</em> e il parametro <em>BookmarkIndex</em> in una singola query.</p></td>
</tr>
<tr class="odd">
<td><p><em>IncludeBookmark</em></p></td>
<td><p>Il parametro consente di specificare se includere l'oggetto segnalibro nell'insieme di risultati. Per impostazione predefinita, il valore è impostato su <code>$true</code> e l'oggetto segnalibro è incluso. È possibile eseguire una query relativa a una dimensione dei risultati limitata e specificare l'ultimo elemento nell'insieme di risultati come segnalibro per la query successiva. In questo caso, è possibile impostare <em>IncludeBookmark</em> su <code>$false</code> in modo che l'oggetto non sia incluso in entrambi gli insiemi di risultati.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Il parametro consente di specificare il numero di risultati da visualizzare per pagina. Se non si specifica un valore, viene utilizzato il numero di risultati predefinito di 1000 oggetti. L'insieme di risultati di Exchange è limitato a 250.000 oggetti.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReturnPageInfo</em></p></td>
<td><p>È un parametro nascosto. che restituisce informazioni sul numero totale di risultati e sull'indice del primo oggetto della pagina corrente. Il valore predefinito è <code>$false</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>SearchForward</em></p></td>
<td><p>Il parametro consente di specificare se cercare in avanti o all'indietro nell'insieme di risultati. Questo parametro non influisce sull'ordine in cui viene restituito l'insieme di risultati. Consente di determinare la direzione della ricerca in relazione all'oggetto o all'indice del segnalibro. Se questi non vengono specificati, il parametro <em>SearchForward</em> consente di determinare se la ricerca inizia dal primo o dall'ultimo oggetto nell'insieme di risultati.</p>
<p>Il valore predefinito per questo parametro è <code>$true</code>. Se il parametro è impostato su <code>$true</code> e viene specificato un segnalibro, la query esegue una ricerca in avanti a partire dal segnalibro. Se si utilizza questa configurazione e non è presente alcun risultato oltre il segnalibro, la query restituisce l'ultima pagina completa di risultati.</p>
<p>Se il parametro <em>SearchForward</em> è impostato su <code>$false</code> e viene specificato un segnalibro, la query esegue una ricerca all'indietro a partire dal segnalibro. Se si utilizza questa configurazione ed è presente meno di una pagina completa di risultati oltre il segnalibro, la query restituisce la prima pagina completa di risultati.</p></td>
</tr>
<tr class="odd">
<td><p><em>SortOrder</em></p></td>
<td><p>Il parametro consente di specificare una matrice di proprietà dei messaggi utilizzate per controllare l'ordinamento dell'insieme di risultati. Le proprietà dell'ordinamento sono specificate in ordine decrescente in base alla priorità. Ogni proprietà è separata da una virgola e presenta il simbolo del segno più (+) per l'ordine crescente oppure il simbolo del segno meno (-) per l'ordine decrescente.</p>
<p>Se non viene specificato un ordinamento in modo esplicito tramite questo parametro, i record che soddisfano la query vengono visualizzati e ordinati in base al campo Identità del relativo tipo di oggetto. Quando l'ordinamento non viene specificato in modo esplicito, i risultati vengono sempre ordinati in base all'identità in ordine crescente.</p></td>
</tr>
</tbody>
</table>


Nel seguente esempio di codice viene illustrato come utilizzare i parametri di paging avanzati in una query. In questo esempio, il comando esegue la connessione al server specificato e recupera un insieme di risultati contenente 500 oggetti. I risultati vengono visualizzati in base a un ordinamento, prima in ordine crescente per indirizzo del mittente, quindi in ordine decrescente per dimensione del messaggio:

`Get-Message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size`

Per visualizzare le pagine successive, è possibile impostare un segnalibro per l'ultimo oggetto recuperato in un insieme di risultati ed eseguire un'ulteriore query. Per completare la procedura, è necessario utilizzare le funzionalità di scripting di Shell.

Nell'esempio riportato di seguito viene utilizzato lo scripting per recuperare la prima pagina di risultati, impostare l'oggetto segnalibro, escludere l'oggetto segnalibro dall'insieme di risultati e recuperare i 500 oggetti successivi sul server specificato.

1.  Aprire Shell e digitare il seguente comando per recuperare la prima pagina di risultati:
    
        $Results=Get-message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size

2.  Per impostare l'oggetto segnalibro, digitare il seguente comando per salvare l'ultimo elemento della prima pagina in una variabile:
    
        $temp=$results[$results.length-1]

3.  Per recuperare i 500 oggetti successivi sul server specificato e per escludere l'oggetto segnalibro, digitare il seguente comando:
    
        Get-message -Server mailbox01.contoso.com -BookmarkObject:$temp -IncludeBookmark $False -ResultSize 500 -SortOrder +FromAddress,-Size

Inizio pagina


---
title: 'Filtri per i messaggi: Exchange 2013 Help'
TOCTitle: Filtri per i messaggi
ms:assetid: 8e6187c1-76f0-49da-bc24-2ab57cfb3c2c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123714(v=EXCHG.150)
ms:contentKeyID: 50481156
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtri per i messaggi

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

L'operazione di filtro genera diverse visualizzazioni dei messaggi nelle code. Specificando i criteri di filtro, è possibile individuare rapidamente i messaggi ed eseguire delle azioni. Quando un messaggio di posta elettronica viene inviato a più destinatari, può essere collocato in più code. Quando si esegue il filtro in base alle proprietà dei messaggi, è possibile individuare i messaggi presenti in diverse code. Di seguito sono illustrati esempi di utilizzo del filtro dei messaggi per gestire il flusso di posta:

  - Nella coda di invio del server Cassette postali o Trasporto Edge che riceve posta elettronica da Internet, è presente una grande quantità di messaggi in attesa di essere recapitati. Molti dei messaggi utilizzano lo stesso oggetto. Si sospetta pertanto che siano messaggi di posta indesiderata indirizzati alla propria organizzazione. È possibile creare un filtro per visualizzare tutti i messaggi che soddisfano il criterio relativo all'oggetto. Se si stabilisce che i messaggi sono indesiderati, è possibile selezionarli ed eliminarli dalle code di recapito senza inviare un rapporto di mancato recapito.

  - Un utente comunica che il flusso di posta è lento. Si analizzano le code e si rileva che molti messaggi con oggetti diversi sembrano essere stati inviati da un solo dominio. È possibile creare un filtro per visualizzare tutti i messaggi in coda provenienti da quel dominio. Se si stabilisce che i messaggi sono indesiderati, è possibile selezionarli ed eliminarli dalle code senza inviare un rapporto di mancato recapito.

## Proprietà dei messaggi come filtri

Le proprietà dei messaggi possono essere utilizzate per creare un filtro e individuare i messaggi che soddisfano i criteri specificati. È possibile creare filtri nel Visualizzatore code oppure utilizzando il parametro *Filter* sui cmdlet di gestione dei messaggi. Tenere presente che i cmdlet di gestione dei messaggi supportano più proprietà valide per il filtro del Visualizzatore code. Nella seguente tabella sono elencate le proprietà dei messaggi in base alle quali è possibile applicare il filtro, nonché i valori associati a tali proprietà.

### Proprietà dei messaggi da utilizzare per il filtro dei messaggi

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Proprietà del messaggio nel Visualizzatore code</th>
<th>Proprietà del messaggio in Shell</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Data ricezione</strong></p></td>
<td><p><code>DateReceived</code></p></td>
<td><p>Data e ora quando il messaggio è stato inserito nella coda.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>DeferReason</code></p></td>
<td><p>Questa proprietà identifica il motivo per cui il messaggio è stato posticipato. Se il messaggio non è stato sospeso, il valore di questa proprietà è <code>None</code>. Un messaggio posticipato è stato restituito alla coda di invio a causa di errori temporanei riscontrati durante la risoluzione dei destinatari. Per ulteriori informazioni sui messaggi posticipati, vedere <a href="recipient-resolution-exchange-2013-help.md">Risoluzione dei destinatari</a>. I valori possibili sono i seguenti:</p>
<p><code>AD Transient Failure During Content Conversion</code></p>
<p><code>AD Transient Failure During Resolve</code></p>
<p><code>Agent</code></p>
<p><code>Ambiguous Recipient</code></p>
<p><code>Loop Detected</code></p>
<p><code>Marked As Retry Delivery If Rejected</code></p>
<p><code>Rerouted By Store Driver</code></p>
<p><code>Storage Transient Failure During Content Conversion</code></p>
<p><code>Transient Failure</code></p>
<p><code>Target Site Inbound Mail Disabled</code></p>
<p><code>Recipient Thread Limit Exceeded</code></p>
<p><code>Transient Attribution Failure</code></p>
<p><code>Transient Accepted Domains Load Failure</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Data scadenza</strong></p></td>
<td><p><code>ExpirationTime</code></p></td>
<td><p>Questa proprietà contiene la data/ora in cui il messaggio scade e viene eliminato dalla coda nel caso in cui non possa essere recapitato.</p></td>
</tr>
<tr class="even">
<td><p><strong>Indirizzo mittente</strong></p></td>
<td><p><code>FromAddress</code></p></td>
<td><p>Questa proprietà contiene gli indirizzi SMTP del mittente.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>Identity</code></p></td>
<td><p>Questa proprietà è l'identità del messaggio nel formato <em>&lt;Server&gt;\&lt;Coda&gt;\&lt;MessageInteger&gt;</em>. Per ulteriori informazioni, vedere la sezione relativa all'identità del messaggio nell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ID messaggio Internet</strong></p></td>
<td><p><code>InternetMessageId</code></p></td>
<td><p>Questa proprietà contiene il valore del campo di intestazione del messaggio <code>Message-ID:</code> che si trova nell'intestazione del messaggio. Il valore è espresso come un indirizzo di posta elettronica che contiene GUID e FQDN, il server mittente di SMTP. Ad esempio:</p>
<p><code>&lt;67D754D6103DC4FB3BA6BC7205DACABA61231@mailbox01.contoso.com&gt;</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ultimo errore</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>Questa proprietà contiene il testo dell'ultimo errore registrato per un messaggio. Ad esempio, <code>A matching connector cannot be found to route the external recipient</code>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>MessageLatency</code></p></td>
<td><p>Questa proprietà contiene il periodo di tempo trascorso tra quando il messaggio è entrato nella coda di invio sul server e quando è stato inserito nella coda. Il valore utilizza la sintassi <em>hh:mm:ss.ff</em>, dove <em>hh</em> = ore, <em>mm</em> = minuti, <em>ss</em> = secondi e <em>ff</em> = frazioni di secondo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Nome origine messaggio</strong></p></td>
<td><p><code>MessageSourceName</code></p></td>
<td><p>Questa proprietà contiene una stringa di testo che indica il nome del componente di trasporto che ha inviato il messaggio alla coda. Ad esempio, se il messaggio è entrato tramite un connettore di ricezione, il valore è: <code>SMTP:</code><em>&lt;ConnectorName&gt;</em>. Se il messaggio è una notifica sullo stato del recapito (DSN), il valore è <code>DSN</code>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>Priority</code></p></td>
<td><p>Questa proprietà contiene la priorità del messaggio che è stata assegnata dall'utente in Outlook o Outlook Web App. I valori possibili sono <code>Low</code>, <code>Normal</code> e <code>High</code>. Per ulteriori informazioni, vedere <a href="priority-queuing-exchange-2013-help.md">Accodamento prioritario</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ID coda</strong></p></td>
<td><p><code>Queue</code></p></td>
<td><p>Questa proprietà è l'identità della coda che include il messaggio. L'identità della coda utilizza la sintassi <em>&lt;Server&gt;\&lt;Coda&gt;</em>. Per ulteriori informazioni, vedere la sezione relativa all'identità della coda nell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>RetryCount</code></p></td>
<td><p>Questa proprietà identifica il numero di tentativi di recapito di un messaggio a una destinazione, manuali o automatici.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SCL</strong></p></td>
<td><p><code>SCL</code></p></td>
<td><p>Il valore della proprietà del livello di probabilità di posta indesiderata (SCL) specifica il valore SCL del messaggio. I valori SCL validi sono i numeri interi da 0 a 9. Una proprietà SCL vuota indica che il messaggio non è stato elaborato dall'agente filtro contenuto.</p>
<p>La proprietà contiene il livello di probabilità di posta indesiderata (SCL) del messaggio. Le voci SCL valide sono numeri interi da 0 a 9 e -1. Per ulteriori informazioni, vedere <a href="spam-confidence-level-threshold-exchange-2013-help.md">Soglia del livello di probabilità di posta indesiderata</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Dimensione (KB)</strong></p></td>
<td><p><code>Size</code></p></td>
<td><p>Questa proprietà indica la dimensione del messaggio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>IP di origine</strong></p></td>
<td><p><code>SourceIP</code></p></td>
<td><p>Questa proprietà contiene l'indirizzo IP del server cha ha inviato il messaggio al server Exchange che contiene il messaggio in coda. L'indirizzo potrebbe essere l'indirizzo IP di un server SMTP remoto oppure l'indirizzo IP del server Exchange locale.</p></td>
</tr>
<tr class="even">
<td><p><strong>Stato</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>Questa proprietà indica lo stato del messaggio corrente. Un messaggio può assumere uno dei seguenti valori di stato:</p>
<p><code>Active</code></p>
<p><code>Locked</code></p>
<p><code>None</code></p>
<p><code>Pending Remove</code></p>
<p><code>Pending Suspend</code></p>
<p><code>Ready</code></p>
<p><code>Retry</code></p>
<p><code>Suspended</code></p>
<p>Per ulteriori informazioni, vedere la sezione relativa alle proprietà del messaggio nell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Oggetto</strong></p></td>
<td><p><code>Subject</code></p></td>
<td><p>Questa proprietà indica l'oggetto di un messaggio disponibile nel campo dell'intestazione <code>Subject:</code> nell'intestazione del messaggio.</p></td>
</tr>
</tbody>
</table>


---
title: 'Filtri di coda: Exchange 2013 Help'
TOCTitle: Filtri di coda
ms:assetid: fbfbdcab-e0d2-4ed9-8f7f-e5fa2c87360d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125237(v=EXCHG.150)
ms:contentKeyID: 50482122
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtri di coda

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

L'operazione di filtro genera diverse visualizzazioni delle code. Le proprietà delle code vengono utilizzate come opzioni del filtro. Specificando i criteri del filtro, è possibile individuare rapidamente le code e agire su di esse. Di seguito sono illustrati esempi di utilizzo del filtro delle code per gestire il flusso di posta:

  - Si riceve un messaggio da Microsoft System Center Operations Manager che indica che la lunghezza di una coda ha superato la soglia stabilita. Si desidera verificare l'esistenza di un problema del flusso di posta a livello del server.
    
    È possibile creare un filtro per visualizzare tutte le code con un numero di messaggi superiore al numero ritenuto normale. Se viene indicato un problema del flusso di posta, è possibile selezionare tutte le code nei risultati del filtro e sospenderle mentre si continua la ricerca del problema.

  - Si sospendono diverse code per ricercare la causa dei problemi del flusso di posta. Viene accertato che la causa del problema risiede in una configurazione non corretta del connettore, problema che viene risolto.
    
    È possibile creare un filtro per visualizzare tutte le code con stato Sospeso, quindi selezionare le code nei risultati del filtro e riprenderle.

## Proprietà delle code da utilizzare per il filtro delle code

Le proprietà delle code possono essere utilizzate per creare un filtro e individuare le code che soddisfano i criteri specificati. È possibile creare filtri nel Visualizzatore code o tramite il parametro *Filter* dei cmdlet di gestione delle code. Tenere presente che i cmdlet di gestione delle code supportano più proprietà filtrabili del Visualizzatore code. Nella tabella seguente sono elencate le proprietà delle code in base alle quali è possibile eseguire il filtro, nonché i valori validi per tali proprietà.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Proprietà della coda nel Visualizzatore code</th>
<th>Proprietà della coda in Shell</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>DeferredMessageCount</code></p></td>
<td><p>Questa proprietà identifica il numero di messaggi restituiti alla coda di invio a causa di errori transitori rilevati durante la risoluzione del destinatario. Per ulteriori informazioni sui messaggi ritardati, vedere <a href="recipient-resolution-exchange-2013-help.md">Risoluzione dei destinatari</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tipo di recapito</strong></p></td>
<td><p><code>DeliveryType</code></p></td>
<td><p>I valori validi per <strong>DeliveryType</strong> sono illustrati nella sezione &quot;NextHopSolutionKey&quot; dell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>Identity</code></p></td>
<td><p>Questa proprietà è l'identità della coda in formato <em>&lt;Server&gt;\&lt;Coda&gt;</em> Per ulteriori informazioni, vedere la sezione &quot;Identità della coda&quot; dell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>IncomingRate</code></p></td>
<td><p>Questa proprietà è un numero calcolato che indica la rapidità con cui i messaggi entrano nella coda. Per ulteriori informazioni, vedere la sezione &quot;IncomingRate, OutgoingRate e Velocity&quot; nell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ultimo errore</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>Questa proprietà indica la stringa di testo dell'ultimo errore registrato per la coda.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ora ultimo tentativo</strong></p></td>
<td><p><code>LastRetryTime</code></p></td>
<td><p>Questa proprietà indica la data e l'ora dell'ultimo tentativo di connessione per una coda il cui stato è <code>Retry</code>.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>LockedMessageCount</code></p></td>
<td><p>Questa proprietà è riservata per uso interno da parte di Microsoft e non viene utilizzata nelle organizzazioni Exchange 2013 locali.</p></td>
</tr>
<tr class="even">
<td><p><strong>Numero messaggi</strong></p></td>
<td><p><code>MessageCount</code></p></td>
<td><p>Questa proprietà indica il numero di messaggi nella coda.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>NextHopCategory</code></p></td>
<td><p>Questa proprietà designa il successivo hop della code come <code>Internal</code> o <code>External</code> e si basa sul valore della proprietà <strong>DeliveryType</strong> della coda. Per ulteriori informazioni, vedere la sezione &quot;NextHopSolutionKey&quot; dell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>NextHopConnector</code></p></td>
<td><p>Questa proprietà è il GUID del successivo hop e si basa sul valore della proprietà <strong>DeliveryType</strong> della coda. Per ulteriori informazioni, vedere la sezione &quot;NextHopSolutionKey&quot; dell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Dominio hop successivo</strong></p></td>
<td><p><code>NextHopDomain</code></p></td>
<td><p>Questa proprietà è il nome del successivo hop e si basa sul valore della proprietà <strong>DeliveryType</strong> della coda. Per ulteriori informazioni, vedere la sezione &quot;NextHopSolutionKey&quot; dell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ora tentativo successivo</strong></p></td>
<td><p><code>NextRetryTime</code></p></td>
<td><p>Questa proprietà indica la data e l'ora del successivo tentativo di connessione per una coda il cui stato è <code>Retry</code>.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>OutgoingRate</code></p></td>
<td><p>Questa proprietà è un numero calcolato che indica la rapidità con cui i messaggi lasciano la coda. Per ulteriori informazioni, vedere la sezione &quot;IncomingRate, OutgoingRate e Velocity&quot; nell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>RiskLevel</code></p></td>
<td><p>Questa proprietà è riservata per uso interno da parte di Microsoft e non viene utilizzata nelle organizzazioni Exchange 2013 locali.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Stato</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>Questa proprietà indica lo stato corrente della coda. I valori possibili sono: Attivo, Connessione, Nessuno, Sospeso, Pronto o Riprova. Per ulteriori informazioni, vedere la sezione &quot;Stato della coda&quot; dell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>TlsDomain</code></p></td>
<td><p>Questa proprietà contiene il nome di dominio completo del dominio di destinazione, se è configurato per Protezione del dominio.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>Velocity</code></p></td>
<td><p>Questa proprietà contiene un numero calcolato che indica l'efficienza di svuotamento della coda. Per ulteriori informazioni, vedere la sezione &quot;IncomingRate, OutgoingRate e Velocity&quot; nell'argomento <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
</tbody>
</table>


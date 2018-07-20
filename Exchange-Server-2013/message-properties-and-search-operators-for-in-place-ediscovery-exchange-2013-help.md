---
title: 'Proprietà di messaggi e operatori di ricerca per eDiscovery In locale: Exchange 2013 Help'
TOCTitle: Proprietà di messaggi e operatori di ricerca per eDiscovery In locale
ms:assetid: 402b74e4-8853-4c51-9737-1a9c19f8e3dd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn774955(v=EXCHG.150)
ms:contentKeyID: 62617765
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Proprietà di messaggi e operatori di ricerca per eDiscovery In locale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In questo argomento vengono descritte le proprietà dei messaggi di posta elettronica Exchange che è possibile eseguire la ricerca con In-Place eDiscovery e conservazione in Exchange Server 2013 e Exchange Online. L'argomento descrive inoltre gli operatori di ricerca booleana e altre tecniche di query di ricerca che è possibile utilizzare per filtrare i risultati della ricerca eDiscovery.

In-Place eDiscovery utilizza Keyword Query Language (KQL). Per ulteriori informazioni, vedere [riferimento sintassi Keyword Query Language](https://go.microsoft.com/fwlink/?linkid=269603).

## Proprietà disponibili per le ricerche in Exchange

Nella tabella seguente sono elencati proprietà dei messaggi di posta elettronica che possono essere ricercate tramite una ricerca eDiscovery In locale oppure utilizzando i cmdlet **Set-MailboxSearch** o **New-MailboxSearch** . La tabella include un esempio di sintassi *property:value* per ogni proprietà e una descrizione dei risultati della ricerca restituiti per gli esempi.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Proprietà</th>
<th>Descrizione proprietà</th>
<th>Esempi</th>
<th>Risultati di ricerca restituiti dagli esempi</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Attachment</p></td>
<td><p>I nomi dei file allegati a un messaggio di posta elettronica.</p></td>
<td><p>attachment:annualreport.ppt</p>
<p>attachment:annual*</p></td>
<td><p>I messaggi che contengono un file allegato denominato annualreport.ppt.</p>
<p>Nel secondo esempio utilizzando il carattere jolly restituisce i messaggi con la parola &quot;annuale&quot; nel nome del file di un allegato.</p></td>
</tr>
<tr class="even">
<td><p>Bcc</p></td>
<td><p>Il campo BCC (Ccn) di un messaggio di posta elettronica.1</p></td>
<td><p>bcc:pilarp@contoso.com</p>
<p>bcc:pilarp</p>
<p>bcc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>Tutti gli esempi restituiscono messaggi contenenti Pilar Pinilla nel campo Bcc (Ccn).</p></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>Le categorie da cercare. Le categorie possono essere definite dagli utenti tramite Outlook o Outlook Web App. I valori possibili sono i seguenti:</p>
<ul>
<li><p>blue (blu)</p></li>
<li><p>green (verde)</p></li>
<li><p>orange (arancione)</p></li>
<li><p>purple (viola)</p></li>
<li><p>red (rosso)</p></li>
<li><p>yellow (giallo)</p></li>
</ul></td>
<td><p>category:&quot;Red Category&quot;</p></td>
<td><p>I messaggi ai quali è stata assegnata la categoria di colore rosso nelle cassette postali di origine.</p></td>
</tr>
<tr class="even">
<td><p>Cc</p></td>
<td><p>Il campo CC (Cc) di un messaggio di posta elettronica.1</p></td>
<td><p>cc:pilarp@contoso.com</p>
<p>cc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>In entrambi gli esempi, vengono restituiti i messaggi contenenti Pilar Pinilla specificati nel campo Cc.</p></td>
</tr>
<tr class="odd">
<td><p>From</p></td>
<td><p>Il mittente di un messaggio di posta elettronica.1</p></td>
<td><p>from:pilarp@contoso.com</p>
<p>from:contoso.com</p></td>
<td><p>I messaggi inviati dall'utente specificato o da un dominio specificato.</p></td>
</tr>
<tr class="even">
<td><p>Importance</p></td>
<td><p>La priorità di un messaggio di posta elettronica, che può essere specificata dall'utente al momento dell'invio di un messaggio. Per impostazione predefinita, i messaggi vengono inviati con una priorità normale, a meno che il mittente non imposti la priorità <strong>high</strong> (alta) o <strong>low</strong> (bassa).</p></td>
<td><p>importance:high</p>
<p>importance:medium</p>
<p>importance:low</p></td>
<td><p>I messaggi contrassegnati con priorità alta, media o bassa.</p></td>
</tr>
<tr class="odd">
<td><p>Kind</p></td>
<td><p>Il tipo di messaggio da cercare. Valori possibili:</p>
<ul>
<li><p>contacts (contatti)</p></li>
<li><p>docs (documenti)</p></li>
<li><p>email (posta elettronica)</p></li>
<li><p>faxes (fax)</p></li>
<li><p>im (IM)</p></li>
<li><p>journals (journal)</p></li>
<li><p>meetings (riunioni)</p></li>
<li><p>notes (note)</p></li>
<li><p>post (inserimenti)</p></li>
<li><p>rssfeeds (feed RSS)</p></li>
<li><p>tasks (attività)</p></li>
<li><p>voicemail (casella vocale)</p></li>
</ul></td>
<td><p>kind:email</p>
<p>kind:email OR kind:im OR kind:voicemail</p></td>
<td><p>Messaggi di posta elettronica che soddisfano i criteri di ricerca. Il secondo esempio restituisce i messaggi di posta elettronica, le chat e i messaggi vocali che soddisfano i criteri di ricerca.</p></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>Tutti i campi degli utenti in un messaggio di posta elettronica; questi campi sono From (Da), To (A), CC (Cc) e BCC (Ccn).1</p></td>
<td><p>participants:garthf@contoso.com</p>
<p>participants:contoso.com</p></td>
<td><p>I messaggi inviati da o inviati a garthf@contoso.com.</p>
<p>Nel secondo esempio restituisce tutti i messaggi inviati da o inviati a un utente nel dominio contoso.com.</p></td>
</tr>
<tr class="odd">
<td><p>Received</p></td>
<td><p>La data in cui un messaggio di posta elettronica viene ricevuto da un destinatario.</p></td>
<td><p>received:04/15/2014</p>
<p>received&gt;=01/01/2014 AND received&lt;=03/31/2014</p></td>
<td><p>I messaggi ricevuti il 15 aprile 2014. Il secondo esempio restituisce tutti i messaggi ricevuti tra il 1° gennaio 2014 e il 31 marzo 2014.</p></td>
</tr>
<tr class="even">
<td><p>Recipients</p></td>
<td><p>Tutti i campi dei destinatari in un messaggio di posta elettronica; questi campi sono To (A), CC (Cc) e BCC (Ccn).1</p></td>
<td><p>recipients:garthf@contoso.com</p>
<p>recipients:contoso.com</p></td>
<td><p>Messaggi inviati a garthf@contoso.com.</p>
<p>Nel secondo esempio restituisce i messaggi inviati a qualsiasi destinatario nel dominio contoso.com.</p></td>
</tr>
<tr class="odd">
<td><p>Sent</p></td>
<td><p>La data in cui un messaggio di posta elettronica viene inviato dal mittente.</p></td>
<td><p>sent:07/01/2014</p>
<p>sent&gt;=06/01/2014 AND sent&lt;=07/01/2014</p></td>
<td><p>I messaggi inviati in una data specifica o entro l'intervallo di date specificato.</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>Le dimensioni di un elemento, in byte.</p></td>
<td><p>size&gt;26214400</p>
<p>size:1..1048576</p></td>
<td><p>Messaggi di dimensioni superiori a 25 MB.</p>
<p>Nel secondo esempio restituisce i messaggi tra 1 e 1.048.576 byte (1 MB).</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>Il testo nella riga dell'oggetto di un messaggio di posta elettronica.</p></td>
<td><p>subject:&quot;Quarterly Financials&quot;</p>
<p>subject:northwind</p></td>
<td><p>I messaggi che contengono il valore esatto frase &quot;Quarterly Financials&quot; in un punto qualsiasi del testo della riga dell'oggetto.</p>
<p>Nel secondo esempio restituisce tutti i messaggi che contengono la parola northwind nella riga dell'oggetto.</p></td>
</tr>
<tr class="even">
<td><p>To</p></td>
<td><p>Il campo To (A) di un messaggio di posta elettronica.1</p></td>
<td><p>to:annb@contoso.com</p>
<p>to:annb</p>
<p>to:&quot;Ann Beebe&quot;</p></td>
<td><p>Tutti gli esempi restituiscono i messaggi in cui è specificato l'utente Ann Beebe nella riga To: (A:).</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1&nbsp;&nbsp;&nbsp;Per il valore della proprietà dei destinatari, è possibile utilizzare l'indirizzo SMTP, il nome visualizzato o l'alias per specificare un utente. Ad esempio, è possibile usare annb@contoso.com, annb o "Ann Beebe" per specificare l'utente Ann Beebe.



## Operatori di ricerca supportati

Operatori booleani ricerca, ad esempio **AND**, **OR**, consentono di definire ricerche nelle cassette postali più preciso, è necessario includere o escludere parole specifiche nella query di ricerca. Altre tecniche, quali l'utilizzo di operatori di proprietà (ad esempio \> = o..), racchiuso tra virgolette, parentesi e i caratteri jolly, consentono di ottimizzare le query di ricerca di eDiscovery. Nella tabella seguente sono elencati gli operatori che è possibile utilizzare per ridurre o ampliare risultati della ricerca.


> [!IMPORTANT]
> Utilizzare gli operatori booleani maiuscoli in una query di ricerca. Ad esempio, utilizzare <STRONG>AND</STRONG>; non utilizzare <STRONG>and</STRONG>. Utilizzo di operatori minuscoli nelle query di ricerca restituirà un errore.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Operatore</th>
<th>Utilizzo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AND</p></td>
<td><p>keyword1 AND keyword2</p></td>
<td><p>Restituisce i messaggi che includono tutte le parole chiave specificate o espressioni <code>property:value</code> .</p></td>
</tr>
<tr class="even">
<td><p>+</p></td>
<td><p>parola chiave1 + parola chiave2 + keyword3</p></td>
<td><p>Restituisce gli elementi contenenti <em><code>keyword2 </code>o <code>keyword3</code><em>e</em></em>contenenti <code>keyword1</code>. Di conseguenza, in questo esempio è l'equivalente per la query <code>(keyword2 OR keyword3) AND keyword1</code>.</p>
<p>Si noti che la query <code>keyword1 + keyword2</code> (con uno spazio dopo <strong>+</strong> simbolo) non equivale a utilizzare l'operatore <strong>AND</strong> . Questa query potrebbe essere equivale a <code>&quot;keyword1 + keyword2&quot;</code> e restituire gli elementi con il valore esatto fase <code>&quot;keyword1 + keyword2&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p>OR</p></td>
<td><p>keyword1 OR keyword2</p></td>
<td><p>Restituisce i messaggi che includono uno o più parole chiave specificate o espressioni <code>property:value</code> .</p></td>
</tr>
<tr class="even">
<td><p>NOT</p></td>
<td><p>keyword1 NOT keyword2</p>
<p>NOT from:&quot;Ann Beebe&quot;</p></td>
<td><p>Consente di escludere i messaggi specificati da una parola chiave o un'espressione <code>property:value</code> . Ad esempio <code>NOT from:&quot;Ann Beebe&quot;</code> esclude i messaggi inviati dalle Ann Beebe.</p></td>
</tr>
<tr class="odd">
<td><p>-</p></td>
<td><p>keyword1 -keyword2</p></td>
<td><p>Lo stesso come operatore <strong>NON</strong> . La query restituisce gli elementi che contengono <code>keyword1</code> ed esclude gli elementi che contengono <code>keyword2</code>.</p></td>
</tr>
<tr class="even">
<td><p>NEAR</p></td>
<td><p>keyword1 NEAR(n) keyword2</p></td>
<td><p>Restituisce i messaggi con le parole scritte vicini, dove n è uguale al numero di parole distinto. Ad esempio, <code>best NEAR(5) worst</code> restituisce i messaggi cui la parola &quot;peggiore&quot; è all'interno di cinque parole di &quot;best&quot;. Se viene specificato alcun numero, la distanza predefinita è otto parole.</p></td>
</tr>
<tr class="odd">
<td><p>:</p></td>
<td><p>property:value</p></td>
<td><p>I due punti (:) nella sintassi <code>property:value</code> specificano che il valore della proprietà da ricercare sia uguale al valore specificato. Ad esempio, <code>recipients:garthf@contoso.com</code> restituisce tutti i messaggi inviati a garthf@contoso.com.</p></td>
</tr>
<tr class="even">
<td><p>&lt;</p></td>
<td><p>property&lt;value</p></td>
<td><p>Indica che la proprietà da cercare è inferiore al valore specificato. 1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;</p></td>
<td><p>property&gt;value</p></td>
<td><p>Indica che la proprietà da cercare è superiore al valore specificato.1</p></td>
</tr>
<tr class="even">
<td><p>&lt;=</p></td>
<td><p>property&lt;=value</p></td>
<td><p>Indica che la proprietà da cercare è inferiore o uguale al valore specifico.1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;=</p></td>
<td><p>property&gt;=value</p></td>
<td><p>Indica che la proprietà da cercare è superiore o uguale al valore specifico.1</p></td>
</tr>
<tr class="even">
<td><p>..</p></td>
<td><p>property:value1..value2</p></td>
<td><p>Indica che la proprietà da cercare è superiore o uguale al valore 1 e inferiore o uguale al valore 2.1</p></td>
</tr>
<tr class="odd">
<td><p>&quot; &quot;</p></td>
<td><p>&quot;fair value&quot;</p>
<p>subject:&quot;Quarterly Financials&quot;</p></td>
<td><p>Utilizzare le virgolette (&quot; &quot;) per cercare una frase o un termine esatto nelle query di ricerca <code>property:value</code> e con parole chiave.</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>cat*</p>
<p>subject:set*</p></td>
<td><p>Ricerche con caratteri jolly prefisso (dove l'asterisco è posizionato alla fine di una parola) corrispondano per i caratteri zero o più parole chiave o le query <code>property:value</code> . Ad esempio, <code>subject:set*</code> restituisce i messaggi che contengono il set di word, il programma di installazione e impostazione (e altre parole che iniziano con&quot;&quot;) nella riga dell'oggetto.</p></td>
</tr>
<tr class="odd">
<td><p>( )</p></td>
<td><p>(accettabile discreto o libero) E from:contoso.com</p>
<p>(IPO OR initial) AND (stock OR shares)</p>
<p>(quarterly financials)</p></td>
<td><p>Le parentesi raggruppano le frasi booleane, gli elementi <code>property:value</code> e le parole chiave. Ad esempio, <code>(quarterly financials)</code> restituisce gli elementi che contengono le parole quarterly e financials.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1&nbsp;&nbsp;&nbsp;Utilizzare questo operatore per le proprietà che dispongono di valori numerici o di data.



## Caratteri non supportati nelle query di ricerca

Caratteri non supportati in una query di ricerca in genere causano un errore di ricerca o restituiscano risultati imprevisti. Caratteri non supportati sono spesso nascosti e in genere aggiunti a una query per copiare la query o la Web part della query da altre applicazioni (ad esempio Microsoft Word o Microsoft Excel) e copiarli nella finestra di parola chiave nella pagina query di ricerca di eDiscovery sul posto.

Ecco un elenco dei caratteri non supportati per una query di ricerca eDiscovery In locale.

  - **Le virgolette inglesi**   Single e double virgolette inglesi (denominate anche *inglesi*) non sono supportate. Solo le virgolette semplici può essere utilizzate in una query di ricerca.

  - **Caratteri non stampabili e il controllo**   Caratteri non stampabili e il controllo non rappresentano un simbolo scritto, ad esempio un carattere alfanumerico. Esempi di non stampabile e caratteri di controllo includono caratteri che in formato testo o righe separate del testo.

  - **Contrassegni da destra a sinistra e da sinistra a destra**   Si tratta di controllo di caratteri utilizzati per indicare l'orientamento del testo per le lingue da sinistra a destra (ad esempio inglese e italiano) e le relative lingue da destra a sinistra (ad esempio arabo ed ebraico).

  - **Operatori booleani minuscolo**   Precedente come descritto, è necessario utilizzare lettere maiuscole operatori booleani, ad esempio **AND** e **o**, in una query di ricerca. Si noti che la sintassi di query frequenza con cui viene indicato che un operatore booleano viene utilizzato anche se minuscoli operatori possono eventualmente essere utilizzati; ad esempio, `(WordA or WordB) and (WordC or WordD)`.

**Come evitare caratteri non supportati nella query di ricerca?** Il modo migliore per evitare che caratteri non supportati consiste nel digitare solo la query nella casella parole chiave. In alternativa, è possibile copiare una query da Word o Excel e incollarlo in un file in un editor di testo, ad esempio Microsoft Notepad. Quindi salvare il file di testo e selezionare nell'elenco a discesa **codificaANSI**. Questo comando rimuoverà tutti i caratteri non supportati e formattazione. È quindi possibile copiare e incollare la query dal file di testo nella casella query parola chiave.

## Suggerimenti pratici per la ricerca

  - Le ricerche per parole chiave non rilevano la distinzione tra maiuscole e minuscole. Ad esempio, **cat** e **CAT** restituiscono gli stessi risultati.

  - Spazio tra le due parole chiave o due espressioni `property:value` equivale utilizzando **AND**. Ad esempio, `from:"Sara Davis" subject:reorganization` restituisce tutti i messaggi inviati da Sara Davis che contengono la parola **riorganizzazione** nella riga dell'oggetto.

  - Utilizzare la sintassi che corrisponde al formato `property:value` . Valori non fanno distinzione maiuscole/minuscole e non può avere uno spazio dopo l'operatore. Se non vi sia uno spazio, il valore previsto sarà semplicemente ricercate full-text. Ad esempio **a: pilarp** le ricerche per "pilarp" come parola chiave, anziché per i messaggi inviati a pilarp.

  - Quando si cerca una proprietà relativa al destinatario, come To (A), From (Da), Cc (Cc) o Recipients (Destinatari), è possibile utilizzare un indirizzo SMTP, un alias o un nome visualizzato per denotare un destinatario. Ad esempio, è possibile utilizzare pilarp@contoso.com, pilarp o "Pilar Pinilla".

  - È possibile utilizzare solo prefisso ricerche con caratteri jolly, ad esempio **cat \*** o **set \***. Suffisso ricerche con caratteri jolly (\* cat) o una sottostringa ricerche con caratteri jolly (\* cat \*) non sono supportati.

  - Durante la ricerca di una proprietà, utilizzare le virgolette doppie ("") se il valore è costituita da più parole. Ad esempio **subject: preventivato T1** restituisce i messaggi che contengono **preventivato** nella riga dell'oggetto e che contengono **T1** in qualsiasi punto nel messaggio o in una delle proprietà dei messaggi. Utilizzo di **soggetto: "budget T1"** restituisce tutti i messaggi che contengono **preventivato T1** qualsiasi posizione nella riga dell'oggetto.


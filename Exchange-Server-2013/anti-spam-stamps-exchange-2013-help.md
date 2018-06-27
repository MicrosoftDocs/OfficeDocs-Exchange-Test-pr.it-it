---
title: 'Contrassegni filtro posta indesiderata: Exchange 2013 Help'
TOCTitle: Contrassegni filtro posta indesiderata
ms:assetid: 28d3a5c2-8509-4b25-9876-763536e77c27
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996878(v=EXCHG.150)
ms:contentKeyID: 50480296
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Contrassegni filtro posta indesiderata

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Gli indicatori di protezione da posta indesiderata permettono di effettuare una diagnosi dei problemi relativi alla posta indesiderata applicando i metadati diagnostici o gli indicatori, come le informazioni specifiche sul mittente, i risultati della convalida puzzle e di filtro contenuto, ai messaggi quando passano attraverso le funzionalità di protezione da posta indesiderata che filtrano i messaggi in ingresso da Internet. Ci sono tre contrassegni filtro posta indesiderata: indicatore del livello di probabilità di phishing, indicatore del livello di probabilità di posta indesiderata e indicatore ID mittente.

È possibile utilizzare gli indicatori protezione posta indesiderata come strumenti diagnostici per determinare le misure da adottare per i falsi positivi e per i messaggi presumibilmente di posta indesiderata che gli utenti ricevono nelle proprie cassette postali.

## Visualizzazione dei contrassegni filtro posta indesiderata

È possibile visualizzare gli indicatori posta indesiderata utilizzando Microsoft Outlook. Per ulteriori informazioni, vedere [Visualizzazione di indicatori di protezione da posta indesiderate in Outlook](view-anti-spam-stamps-in-outlook-exchange-2013-help.md).

## Informazioni sui rapporti di protezione da posta indesiderata

Il rapporto protezione posta indesiderata è un rapporto riepilogativo dei risultati del filtro protezione da posta indesiderata applicato a un messaggio di posta elettronica. L'agente Filtro contenuti applica questo indicatore alla busta del messaggio nel formato X-header nel modo seguente:

    X-MS-Exchange-Organization-Antispam-Report: DV:<DATVersion>;CW:CustomList;PCL:PhishingVerdict <verdict>;P100:PhishingBlock;PP:Presolve;SID:SenderIDStatus <status>;TIME:<SendReceiveDelta>;MIME:MimeCompliance 

La tabella seguente descrive le informazioni di filtro che possono apparire nel rapporto di protezione da posta indesiderata.


> [!NOTE]
> Nel rapporto protezione posta indesiderata vengono visualizzate solo le informazioni provenienti dai filtri applicati al messaggio specifico. Il rapporto di protezione da posta indesiderata di solito non contiene tutte le informazioni riportate nella tabella seguente. Ad esempio, è possibile ricevere il seguente messaggio di protezione da posta indesiderata: <CODE>DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures</CODE>.



### Informazioni di filtro in un rapporto di protezione da posta indesiderata

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Indicatore</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SID</p></td>
<td><p>L'indicatore ID mittente (SID, Sender ID) si basa su SPF (Sender Policy Framework) che autorizza l'uso dei dei domini nella posta elettronica. SPF viene visualizzato nella busta del messaggio come <code>Received-SPF</code>. Il processo di valutazione dell'ID mittente genera uno stato ID mittente per il messaggio. È possibile che lo stato venga restituito come uno dei seguenti valori:</p>
<ul>
<li><p><strong>Pass   </strong>Sia l'indirizzo IP che il PRA (Purported Responsible Address) hanno superato il controllo di verifica dell'ID mittente.</p></li>
<li><p><strong>Neutral   </strong>I dati relativi all'ID mittente pubblicato non consentono di arrivare a conclusioni esplicite.</p></li>
<li><p><strong>Soft fail</strong>   L'indirizzo IP del PRA potrebbe trovarsi nel set non consentito.</p></li>
<li><p><strong>Fail   </strong>L'indirizzo IP non è consentito; non viene trovato alcun indirizzo PRA nella posta in arrivo o il dominio di invio non esiste.</p></li>
<li><p><strong>None</strong>   Non esistono dati pubblicati sull'SFP nel DNS del mittente.</p></li>
<li><p><strong>TempError</strong>   Si è verificato un errore DNS temporaneo, ad esempio il server DNS non è disponibile.</p></li>
<li><p><strong>PermError</strong>   Il record DNS non è valido, ad esempio un errore nel formato del record.</p></li>
</ul>
<p>L'indicatore SID viene visualizzato come X-Header nella busta del messaggio nel modo seguente:</p>
<pre><code>X-MS-Exchange-Organization-SenderIdResult:&lt;status&gt;</code></pre>
<p>Per ulteriori informazioni sull'ID mittente, vedere <a href="sender-id-exchange-2013-help.md">ID mittente</a>.</p></td>
</tr>
<tr class="even">
<td><p>DV</p></td>
<td><p>L'indicatore DV (DAT Version) indica la versione del file di definizione della posta indesiderata utilizzato per l'analisi del messaggio.</p></td>
</tr>
<tr class="odd">
<td><p>SA</p></td>
<td><p>L'indicatore SA (Signature Action) indica che il messaggio è stato recuperato o eliminato a causa di una firma rilevata nel messaggio.</p></td>
</tr>
<tr class="even">
<td><p>SV</p></td>
<td><p>L'indicatore DV della firma (SV, Signature Version) indica la versione del file della firma utilizzato per l'analisi del messaggio.</p></td>
</tr>
<tr class="odd">
<td><p>PCL</p></td>
<td><p>L'indicatore del livello di probabilità di phishing (PCL) indica la classificazione del messaggio in base al contenuto e viene applicato quando il messaggio viene elaborato dall'agente Filtro contenuto. Lo stato restituito può avere i seguenti valori:</p>
<ul>
<li><p><strong>Neutral   </strong>È probabile che il contenuto del messaggio non sia phishing.</p></li>
<li><p><strong>Suspicious</strong>   È probabile che il contenuto del messaggio sia phishing.</p></li>
</ul>
<p>Il valore PCL può essere compreso tra 1 e 8. Il livello PCL compreso tra 1 e 3 restituisce lo stato <code>Neutral</code>. Ciò significa che è probabile che il contenuto del messaggio non sia phishing. Il livello PCL compreso tra 4 e 8 restituisce lo stato <code>Suspicious</code>. Ciò significa che è probabile che il contenuto del messaggio sia phishing.</p>
<p>I valori vengono utilizzati per determinare quale azione viene eseguita da Outlook sui messaggi. Outlook utilizza l'indicatore PCL per bloccare il contenuto dei messaggi sospetti.</p>
<p>L'indicatore PCL viene visualizzato come X-header nella busta del messaggio nel modo seguente:</p>
<pre><code>X-MS-Exchange-Organization-PCL:&lt;status&gt;</code></pre></td>
</tr>
<tr class="even">
<td><p>SCL</p></td>
<td><p>L'indicatore del livello di probabilità di posta indesiderata (SCL) del messaggio indica la classificazione del messaggio in base al contenuto. L'agente Filtro contenuto utilizza la tecnologia Microsoft SmartScreen per valutare il contenuto di un messaggio e per assegnare un livello SCL a ciascun messaggio. Il valore SCL è compreso tra 0 e 9, dove 0 rappresenta il numero minore di probabilità che il messaggio sia posta indesiderata e 9 il numero maggiore di probabilità che il messaggio sia posta indesiderata. Le azioni eseguite da Exchange e da Outlook dipendono dalle impostazioni della soglia SCL.</p>
<p>L'indicatore SCL viene visualizzato come X-header nella busta del messaggio nel modo seguente:</p>
<pre><code>X-MS-Exchange-Organization-SCL:&lt;status&gt;</code></pre>
<p>Per ulteriori informazioni sulle soglie SCL e sulle azioni, vedere <a href="spam-confidence-level-threshold-exchange-2013-help.md">Soglia del livello di probabilità di posta indesiderata</a>.</p></td>
</tr>
<tr class="odd">
<td><p>CW</p></td>
<td><p>L'indicatore CW (Custom Weight) di un messaggio indica che il messaggio contiene una parola o frase non approvata e che il valore SCL o peso di quella determinata parola o frase non approvata è stato applicato alla classificazione SCL finale:</p>
<ul>
<li><p>Le frasi non approvate, ovvero frasi bloccate, vengono considerate di massimo peso e il livello SCL assegnato a tali frasi è 9.</p></li>
<li><p>Le parole o frasi approvate, ovvero le frasi consentite, vengono considerate di minimo peso e la classificazione SCL finale assegnata è 0.</p></li>
</ul>
<p>Per ulteriori informazioni su come aggiungere parole o frasi approvate e non approvate all'agente Filtro contenuto, vedere <a href="manage-content-filtering-exchange-2013-help.md">Gestire il filtro contenuto</a>.</p></td>
</tr>
<tr class="even">
<td><p>PP</p></td>
<td><p>L'indicatore PP (Presolved Puzzle) indica che se il messaggio di un mittente contiene un timbro di calcolo valido e risolto, in base alla funzionalità di convalida del timbro posta elettronica di Outlook, è improbabile che si tratti di un mittente malintenzionato. In questo caso, l'agente Filtro contenuti ridurrà il livello di probabilità di posta indesiderata.</p>
<p>L'agente Filtro contenuto non cambia il livello SCL se la funzionalità di convalida del timbro posta elettronica è abilitata e se viene soddisfatta una delle seguenti condizioni:</p>
<ul>
<li><p>Il messaggio in ingresso non contiene l'intestazione di un timbro di calcolo.</p></li>
<li><p>L'intestazione del timbro di calcolo non è valida.</p></li>
</ul>
<p>Per ulteriori informazioni sulla funzionalità di convalida del timbro, vedere <a href="content-filtering-exchange-2013-help.md">Filtro contenuto</a>.</p></td>
</tr>
<tr class="odd">
<td><p>TIME:TimeBasedFeatures</p></td>
<td><p>L'indicatore TIME indica che si è verificato un ritardo significativo tra l'ora in cui il messaggio è stato inviato e l'ora in cui è stato ricevuto. L'indicatore TIME viene utilizzato per determinare il livello SCL finale del messaggio.</p></td>
</tr>
<tr class="even">
<td><p>MIME:MIMECompliance</p></td>
<td><p>L'indicatore MIME indica che il messaggio di posta elettronica non è conforme alla codifica MIME.</p></td>
</tr>
<tr class="odd">
<td><p>P100:PhishingBlock</p></td>
<td><p>L'indicatore P100 indica che il messaggio contiene un URL presente nel file di definizione phishing.</p></td>
</tr>
<tr class="even">
<td><p>IPOnAllowList</p></td>
<td><p>L'indicatore IPOnAllowList indica che l'indirizzo del mittente si trova nell'elenco degli indirizzi IP consentiti. Per ulteriori informazioni, vedere <a href="http://go.microsoft.com/fwlink/?linkid=268732">Informazioni sul filtro connessioni</a>.</p></td>
</tr>
<tr class="odd">
<td><p>MessageSecurityAntispamBypass</p></td>
<td><p>L'indicatore MessageSecurityAntispamBypass indica che al contenuto del messaggio non è stato applicato alcun filtro e che il mittente ha l'autorizzazione di ignorare i filtri di protezione da posta indesiderata.</p></td>
</tr>
<tr class="even">
<td><p>SenderBypassed</p></td>
<td><p>L'indicatore SenderBypassed indica che l'agente Filtro contenuto non applica alcun filtro al contenuto dei messaggi inviati da questo mittente. Per ulteriori informazioni, vedere <a href="manage-content-filtering-exchange-2013-help.md">Gestire il filtro contenuto</a>.</p></td>
</tr>
<tr class="odd">
<td><p>AllRecipientsBypassed</p></td>
<td><p>L'indicatore AllRecipientsBypassed indica che una delle seguenti condizioni è stata soddisfatta per tutti i destinatari elencati nel messaggio:</p>
<ul>
<li><p>Il parametro <em>AntispamBypassedEnabled</em> nella cassetta postale del destinatario è impostato su <code>$true</code>. Questa è una impostazione per singolo destinatario che può essere impostata solo da un amministratore utilizzando il cmdlet <strong>Set-Mailbox</strong>.</p></li>
<li><p>Il mittente del messaggio si trova nell'elenco Mittenti attendibili di Outlook del destinatario. Per ulteriori informazioni sull'elenco Mittenti attendibili, vedere <a href="manage-safelist-aggregation-exchange-2013-help.md">Gestisci aggregazione dell'elenco indirizzi attendibili</a>.</p></li>
<li><p>L'agente Filtro contenuto non applica alcun filtro al contenuto dei messaggi inviati a questo destinatario. Per ulteriori informazioni sulle eccezioni di destinatari, vedere <a href="manage-content-filtering-exchange-2013-help.md">Gestire il filtro contenuto</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>


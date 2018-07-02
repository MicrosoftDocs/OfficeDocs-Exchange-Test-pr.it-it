---
title: 'Proprietà filtrabili per il parametro - ContentFilter: Exchange 2013 Help'
TOCTitle: Proprietà filtrabili per il parametro - ContentFilter
ms:assetid: cf504a59-1938-489c-bb48-b27b2ac3234e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff601762(v=EXCHG.150)
ms:contentKeyID: 50555682
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Proprietà filtrabili per il parametro - ContentFilter

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-09-10_

In questo argomento vengono elencate le proprietà filtrabili del parametro *ContentFilter*. Il parametro *ContentFilter* viene utilizzato per esportare i messaggi in un file PST che corrisponde al filtro. Il parametro *ContentFilter* viene utilizzato nel cmdlet [New-MailboxExportRequest](https://technet.microsoft.com/it-it/library/ff607299\(v=exchg.150\)).

## Proprietà filtrabili

Molte proprietà del parametro *ContentFilter* accettano caratteri jolly. Se si utilizza un carattere jolly, utilizzare l'operatore **-like** invece dell'operatore **-eq**. L'operatore **-like** viene utilizzato per trovare le corrispondenze motivo nei tipi formattati, come le stringhe, mentre l'operatore **-eq** viene utilizzato per trovare una corrispondenza esatta.

La tabella seguente contiene un elenco delle proprietà filtrabili del parametro *ContentFilter*. Nella tabella sono elencati il nome della proprietà, la descrizione, i valori accettabili e un esempio di sintassi. Per ulteriori informazioni sui filtri OPath, vedere [Filtri destinatario comandi Shell](https://technet.microsoft.com/it-it/library/bb124268\(v=exchg.150\)).


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
<th>Descrizione</th>
<th>Valori</th>
<th>Esempio di sintassi</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>All</p></td>
<td><p>Questa proprietà restituisce tutti i messaggi con una stringa particolare in una delle proprietà indicizzate. Ad esempio, questa proprietà viene utilizzata per esportare tutti i messaggi con &quot;Ayla&quot; come destinatario, come mittente o con tale nome indicato nel corpo del messaggio.</p></td>
<td><p>String</p>
<p>Wildcard</p></td>
<td><pre><code>-ContentFilter {All -like &#39;*Ayla*&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Attachment</p></td>
<td><p>Questa proprietà restituisce i messaggi che contengono la stringa specificata nel contenuto di un allegato o nel nome file di un allegato.</p></td>
<td><p>Stringa</p>
<p>Wildcard</p></td>
<td><pre><code>-ContentFilter {Attachment -like &#39;*.jpg&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Ccn</p></td>
<td><p>Questa proprietà restituisce i messaggi che contengono il destinatario specificato nel campo Ccn.</p></td>
<td><p>Nome visualizzato</p>
<p>Alias</p>
<p>Indirizzo SMTP</p>
<p>LegacyDN</p>
<p>Wildcard</p></td>
<td><pre><code>-ContentFilter {(BCC -eq &#39;ayla@contoso.com&#39;) -or (BCC -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="even">
<td><p>Corpo</p></td>
<td><p>Questa proprietà restituisce i messaggi che contengono la stringa specificata nel corpo del messaggio.</p></td>
<td><p>Stringa</p>
<p>Wildcard</p></td>
<td><pre><code>-ContentFilter {Body -like &#39;*prospectus*&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>Questa proprietà restituisce i messaggi con una categoria corrispondente. Le categorie vengono impostate dagli utenti o dalle regole della Posta in arrivo.</p></td>
<td><p>Stringa</p>
<p>Wildcard</p></td>
<td><pre><code>-ContentFilter {Category -like &#39;*Blue*&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Cc</p></td>
<td><p>Questa proprietà restituisce i messaggi inviati che contengono il destinatario specificato nel campo Cc.</p></td>
<td><p>Nome visualizzato</p>
<p>Alias</p>
<p>Indirizzo SMTP</p>
<p>LegacyDN</p>
<p>Wildcard</p></td>
<td><pre><code>-ContentFilter {(CC -eq &#39;ayla@contoso.com&#39;) -or (CC -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Expires</p></td>
<td><p>Questa proprietà restituisce i messaggi che presentano un timestamp con la scadenza specificata.</p></td>
<td><p>Indicatore data e ora</p></td>
<td><pre><code>-ContentFilter {Expires -lt &#39;01/01/2013&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>HasAttachment</p></td>
<td><p>Questa proprietà restituisce messaggi con o senza allegati.</p></td>
<td><p>Booleano</p>
<p><code>$true</code> o <code>$false</code></p></td>
<td><pre><code>-ContentFilter {HasAttachment -eq $true}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>Questa proprietà restituisce i messaggi con un livello di priorità specificato.</p></td>
<td><p>0 o &quot;Bassa&quot;</p>
<p>1 o &quot;Normale&quot;</p>
<p>2 o &quot;Alta&quot;</p></td>
<td><pre><code>-ContentFilter {Importance -eq &#39;high&#39;}</code></pre>
<pre><code>-ContentFilter {Importance -eq 2}</code></pre></td>
</tr>
<tr class="even">
<td><p>IsFlagged</p></td>
<td><p>Questa proprietà restituisce i messaggi contrassegnati dall'utente o dalla regola della Posta in arrivo.</p></td>
<td><p>Booleano</p>
<p><code>$true</code> oppure <code>$false</code></p></td>
<td><pre><code>-ContentFilter {IsFlagged -eq $true}</code></pre></td>
</tr>
<tr class="odd">
<td><p>IsRead</p></td>
<td><p>Questa proprietà restituisce i messaggi letti o non letti dall'utente.</p></td>
<td><p>Booleano</p>
<p><code>$true</code> oppure <code>$false</code></p></td>
<td><pre><code>-ContentFilter {IsRead -eq $true}</code></pre></td>
</tr>
<tr class="even">
<td><p>MessageKind</p></td>
<td><p>Questa proprietà restituisce i messaggi del tipo specificato.</p></td>
<td><p>Calendario</p>
<p>Contact</p>
<p>Doc</p>
<p>Email</p>
<p>Fax</p>
<p>InstantMessage</p>
<p>Diario</p>
<p>Nota</p>
<p>Inserimento</p>
<p>RSSFeed</p>
<p>Attività</p>
<p>Segreteria telefonica</p></td>
<td><pre><code>-ContentFilter {MessageKind -eq &#39;Calendar&#39;}</code></pre>
<pre><code>-ContentFilter {MessageKind -ne &#39;Email&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>MessageLocalee</p></td>
<td><p>Questa proprietà restituisce i messaggi con le impostazioni locali specificate.</p></td>
<td><p>CultureInfo</p></td>
<td><pre><code>-ContentFilter {MessageLocale -ne &#39;en-US&#39;}</code></pre>
<pre><code>-ContentFilter {MessageLocale -eq &#39;tr-TR&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>Questa proprietà restituisce i messaggi che contengono il destinatario specificato nei campi A, Ccn o Cc.</p></td>
<td><p>Nome visualizzato</p>
<p>Alias</p>
<p>Indirizzo SMTP</p>
<p>LegacyDN</p>
<p>Wildcard</p></td>
<td><pre><code>-ContentFilter {(Participants -eq &#39;ayla@contoso.com&#39;) -or (Participants -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>PolicyTag</p></td>
<td><p>Questa proprietà restituisce i messaggi con un tag di criteri. L'archivio di Exchange mantiene i tag dei criteri come GUID. La stringa può quindi contenere un valore GUID esplicito, cercato con PR_POLICY_TAG, o una stringa con caratteri jolly.</p>
<p>Se il valore fornito non è un valore GUID, il comando utilizzerà le informazioni di Active Directory per risolvere i nomi nei GUID.</p></td>
<td><p>Stringa</p>
<p>Wildcard</p></td>
<td><pre><code>-ContentFilter {PolicyTag -ne &#39;00000000-0000-0000-0000-000000000000&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>Questa proprietà restituisce i messaggi ricevuti con il timestamp Received specificato.</p></td>
<td><p>Indicatore data e ora</p></td>
<td><pre><code>-ContentFilter {Received -lt &#39;01/01/2013 9:00&#39;}</code></pre>
<pre><code>-ContentFilter {(Received -lt &#39;01/01/2013&#39;) -and (Received -gt &#39;01/01/2012&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Mittente</p></td>
<td><p>Questa proprietà restituisce i messaggi ricevuti dal mittente specificato.</p></td>
<td><p>Nome visualizzato</p>
<p>Alias</p>
<p>Indirizzo SMTP</p>
<p>LegacyDN</p>
<p>Wildcard</p></td>
<td><pre><code>ContentFilter {Sender -eq &#39;tony&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>Questa proprietà restituisce i messaggi inviati con il timestamp Sent specificato.</p></td>
<td><p>Indicatore data e ora</p></td>
<td><pre><code>-ContentFilter {Sent -lt &#39;01/01/2013 9:00&#39;}</code></pre>
<pre><code>-ContentFilter {(Sent -lt &#39;01/01/2013&#39;) -and (Sent -gt &#39;01/01/2012&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>Questa proprietà restituisce i messaggi di una dimensione specifica.</p></td>
<td><p>B (byte)</p>
<p>KB (kilobyte)</p>
<p>MB (megabyte)</p></td>
<td><pre><code>-ContentFilter {Size -gt &#39;10KB&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Oggetto</p></td>
<td><p>Questa proprietà restituisce i messaggi che contengono la stringa specificata nell'oggetto del messaggio.</p></td>
<td><p>Stringa</p>
<p>Wildcard</p></td>
<td><pre><code>-ContentFilter {Subject -like &#39;*meeting*&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>To</p></td>
<td><p>Questa proprietà restituisce i messaggi che contengono il destinatario specificato nel campo A.</p></td>
<td><p>Nome visualizzato</p>
<p>Alias</p>
<p>Indirizzo SMTP</p>
<p>LegacyDN</p>
<p>Wildcard</p></td>
<td><pre><code>-ContentFilter {To -eq &#39;aylakol&#39;}</code></pre></td>
</tr>
</tbody>
</table>


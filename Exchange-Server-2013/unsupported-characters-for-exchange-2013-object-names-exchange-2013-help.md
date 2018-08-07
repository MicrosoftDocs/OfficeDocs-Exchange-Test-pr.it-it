---
title: 'Caratteri non supportati per oggetti Exchange 2013: Exchange 2013 Help'
TOCTitle: Caratteri non supportati per i nomi degli oggetti di Exchange 2013
ms:assetid: 76fa4e23-f0f6-473b-9227-70ded907578f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn169553(v=EXCHG.150)
ms:contentKeyID: 54652874
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Caratteri non supportati per i nomi degli oggetti di Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

In questo articolo sono descritti i caratteri che non è possibile utilizzare come nomi degli oggetti in Exchange 2013. Quando si creano nomi per oggetti o componenti in Exchange 2013, i nomi non possono contenere caratteri non supportati, anche se può essere possibile creare un oggetto utilizzando un carattere non supportato. Inoltre, se si cerca di importare o collegare oggetti i cui nomi contengono caratteri non supportati, potrebbe essere visualizzato un messaggio di errore oppure potrebbero verificarsi comportamenti imprevisti.

## Caratteri non supportati

Nella seguente tabella sono elencati i caratteri non supportati per l'utilizzo nei nomi di oggetti o componenti correlati a Exchange. Nella tabella sono inoltre elencati gli scenari in cui possono verificarsi problemi se vengono utilizzati caratteri non supportati. La lunghezza massima dei nomi è di 64 caratteri per ogni oggetto elencato nella tabella.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Oggetto o componente di Exchange</th>
<th>Scenario di Exchange</th>
<th>Caratteri non supportati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nome dominio di posta elettronica</p></td>
<td><p>Connettore Simple Mail Transfer Protocol (SMTP)</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>Spazio indirizzo del nome host del connettore</p></td>
<td><p>Flusso di posta</p></td>
<td><p><code>..</code> (due punti)</p></td>
</tr>
<tr class="odd">
<td><p>Nome host per i server Exchange</p></td>
<td><p>SMTP</p></td>
<td><p><code>_</code> (carattere di sottolineatura)</p></td>
</tr>
<tr class="even">
<td><p>Nome organizzazione o sito</p></td>
<td><p>Esecuzione del programma di installazione o spostamento di cassette postali</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>Nome della directory interna dell'organizzazione</p></td>
<td><p>Directory</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>Nome dell'albero di cartelle pubbliche</p></td>
<td><p>Visualizzazione e creazione delle cartelle pubbliche</p></td>
<td><p><code>: ;</code></p></td>
</tr>
<tr class="odd">
<td><p>Nome del destinatario</p></td>
<td><p>SMTP</p></td>
<td><p><code>' &quot;</code></p></td>
</tr>
<tr class="even">
<td><p>Indirizzo SMTP del criterio del destinatario</p></td>
<td><p>Visualizzazione della gerarchia delle cartelle pubbliche</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>Nome host indirizzo SMTP del criterio del destinatario</p></td>
<td><p>Flusso di posta</p></td>
<td><p><code>..</code> (due punti)</p></td>
</tr>
<tr class="even">
<td><p>Nome della directory del sito interno</p></td>
<td><p>Visualizzazione della gerarchia delle cartelle pubbliche</p></td>
<td><p><code>? ( ) *</code></p></td>
</tr>
<tr class="odd">
<td><p>Nome smart host</p></td>
<td><p>SMTP</p></td>
<td><p>Spazi iniziali o finali</p></td>
</tr>
</tbody>
</table>


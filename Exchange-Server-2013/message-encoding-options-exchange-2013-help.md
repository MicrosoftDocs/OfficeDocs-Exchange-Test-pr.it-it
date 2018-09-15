---
title: 'Opzioni di codifica dei messaggi: Exchange 2013 Help'
TOCTitle: Opzioni di codifica dei messaggi
ms:assetid: c1d9edbb-d87c-41e5-881b-cd612d83d7e4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb310794(v=EXCHG.150)
ms:contentKeyID: 50481590
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Opzioni di codifica dei messaggi

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Le opzioni di codifica dei messaggi disponibili in Exchange specificano le caratteristiche dei messaggi come i set di caratteri MIME e non MIME, la codifica binaria e i formati degli allegati. È possibile specificare le opzioni di codifica dei messaggi nei seguenti percorsi:

  - Impostazioni del dominio remoto

  - Impostazioni dell'utente di posta e del contatto di posta

  - Impostazioni di Microsoft Outlook
    
      - Formato messaggio
    
      - Formato dei messaggi Internet
    
      - Formato messaggi destinatari Internet
    
      - Opzioni di codifica dei set di caratteri dei messaggi

**Contenuto**

Message encoding options for messages sent to remote domains

Message encoding options for mail users and mail contacts

Message encoding options available in Outlook

Le opzioni disponibili in Outlook Web App di codifica dei messaggi

Order of precedence for message encoding options

Per ulteriori informazioni

## Opzioni di codifica per i messaggi inviati a domini remoti

Quando si configurano le opzioni di codifica dei messaggi per un dominio remoto, le impostazioni specifiche vengono applicate per tutti i messaggi inviati a quel dominio. Per i domini remoti dell'organizzazione, sono disponibili le seguenti opzioni di configurazione per la codifica dei messaggi.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Impostazione</strong></p></td>
<td><p><strong>Disponibile in EAC in Exchange Online Dedicated</strong></p></td>
<td><p><strong>Disponibile nella Shell</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Set di caratteri MIME</strong>   Il set di caratteri specificato verrà utilizzato solo per i messaggi MIME che non dispongono di un set di caratteri specificato. L'impostazione di questo parametro non implica la sovrascrittura dei set di caratteri già specificati nella posta in uscita.</p>
<p><strong>Set di caratteri non MIME</strong>   Questa impostazione viene utilizzata se si verifica una delle seguenti condizioni:</p>
<ul>
<li><p>Nei messaggi in arrivo provenienti da un dominio remoto manca il valore dell'impostazione <em>charset=</em> nel tipo di contenuto MIME: campo dell'intestazione.</p></li>
<li><p>Nei messaggi in uscita verso un dominio remoto manca il valore del set di caratteri MIME.</p></li>
</ul>
<p></p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p><strong>Tipo di contenuto</strong>   È possibile specificare il tipo di contenuto per i messaggi MIME inviati ai destinatari del dominio remoto. È possibile utilizzare le seguenti impostazioni:</p>
<ul>
<li><p><strong>MimeHtmlText</strong>   Tutti i messaggi vengono convertiti in messaggi MIME che utilizzano la formattazione HTML, a meno che il messaggio originale non sia un messaggio di testo. Se il messaggio originale è un messaggio di testo, il messaggio in uscita sarà un messaggio MIME che utilizza la formattazione di testo. Questa impostazione è quella predefinita.</p></li>
<li><p><strong>MimeText</strong>   Tutti i messaggi vengono convertiti in messaggi MIME che utilizzano la formattazione di testo.</p></li>
<li><p><strong>MimeHtml</strong>   Tutti i messaggi vengono convertiti in messaggi MIME che utilizzano la formattazione HTML.</p></li>
</ul></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p><strong>Lunghezza per il ritorno a capo</strong>   È possibile specificare il numero massimo di caratteri consentiti su una singola riga di testo nel corpo del messaggio di posta elettronica. Per le applicazioni client di posta elettronica meno recenti è preferibile un numero di 78 caratteri per riga. Questa opzione è disponibile solo se si utilizza la Shell.</p>
<p></p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Opzioni di codifica dei messaggi per gli utenti e i contatti di posta elettronica

Quando si configurano le opzioni di codifica dei messaggi per un contatto o un utente di posta, l'opzione viene applicata a tutti i messaggi inviati a quel destinatario. Per i contatti e gli utenti di posta dell'organizzazione, sono disponibili le seguenti opzioni di configurazione per la codifica dei messaggi:

  - **UsePreferMessageFormat**   Questo parametro consente di specificare se le impostazioni di formato dei messaggi configurate per il contatto di posta hanno la priorità sulle impostazioni globali per il dominio remoto. Se questa impostazione viene disabilitata, Exchange ignora le altre opzioni di codifica dei messaggi per questo destinatario e la codifica viene determinata dalla configurazione del dominio remoto o dalle impostazioni configurate dal mittente del messaggio.

  - **MessageFormat**   Questo parametro consente di specificare il formato dei messaggi. È possibile specificare Testo o Mime come formato dei messaggi. Il valore di questa impostazione dipende dal parametro *MessageBodyFormat*. Se il formato del corpo dei messaggi è Html o TextAndHtml, è necessario impostare questo parametro su Mime.

  - **MessageBodyFormat**   Questo parametro consente di specificare il formato del corpo dei messaggi. È possibile specificare Testo, Html o TextAndHtml. Il valore di questa impostazione dipende dal parametro *MessageFormat*. Se il formato dei messaggi è Testo, è necessario impostare anche questo parametro su Testo.

  - **MacAttachmentFormat**   Questo parametro consente di specificare il formato degli allegati per il sistema operativo Apple Macintosh per i messaggi. È possibile specificare BinHex, UuEncode, AppleSingle o AppleDouble. Il valore di questa impostazione dipende dal parametro *MessageFormat*. Se il formato dei messaggi è impostato su Testo, è necessario impostare questo parametro su BinHex o UuEncode. Se il formato dei messaggi è impostato su Mime, è necessario impostare questo parametro su BinHex, AppleSingle o AppleDouble.

È necessario utilizzare Exchange Management Shell per impostare le opzioni di codifica dei messaggi per gli utenti e i contatti di posta elettronica. Per ulteriori informazioni, vedere gli argomenti seguenti:

  - [Enable-MailContact](https://technet.microsoft.com/it-it/library/aa996001\(v=exchg.150\))

  - [New-MailContact](https://technet.microsoft.com/it-it/library/bb124519\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/it-it/library/aa995950\(v=exchg.150\))

  - [Enable-MailUser](https://technet.microsoft.com/it-it/library/aa996549\(v=exchg.150\))

  - [New-MailUser](https://technet.microsoft.com/it-it/library/aa996335\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/it-it/library/aa995971\(v=exchg.150\))

Inizio pagina

## Opzioni di codifica dei messaggi disponibili in Outlook

Come mittente, è possibile specificare le opzioni di codifica dei messaggi in Outlook in una delle seguenti fasi:

  - Durante le configurazione del formato predefinito dei messaggi su Testo normale o HTML.

  - Durante l'impostazione del formato del messaggio su Testo normale o HTML durante la composizione utilizzando l'area **Formato** nella scheda **Opzioni**.

  - Durante la configurazione delle opzioni di codifica per i messaggi inviati a tutti i destinatari esterni all'organizzazione di Exchange. Queste opzioni sono definite opzioni *Formato messaggi Internet*. Vengono applicate unicamente ai destinatari remoti, non ai destinatari nell'organizzazione di Exchange.

  - Durante la configurazione delle opzioni di codifica per i messaggi inviati a destinatari specifici esterni all'organizzazione di Exchange. Queste opzioni sono definite opzioni *Formato messaggi destinatari Internet*. Le opzioni vengono applicate solo ai destinatari remoti della cartella Contatti e non ai destinatari dell'organizzazione di Exchange.

Per impostazione predefinita, Outlook utilizza la codifica automatica dei set di caratteri dei messaggi analizzando tutto il testo del messaggio in uscita per determinare la codifica appropriata da utilizzare per il messaggio. Questa impostazione viene applicata ai messaggi inviati a destinatari Internet e a destinatari nell'organizzazione di Exchange. Tuttavia, è possibile ignorarla e specificare una codifica preferita per i messaggi in uscita.

Inizio pagina

## Opzioni di codifica dei messaggi disponibili in Outlook Web App

Come mittente, è possibile specificare le opzioni di codifica dei messaggi in Outlook Web App in una delle seguenti fasi:

  - Mediante la configurazione del formato di messaggio predefinito come testo normale o HTML nella sezione **Formato messaggio** della pagina **Impostazioni** \>**Opzioni** \> **Impostazioni**.

  - Mediante l'impostazione del formato di messaggio nel corso della composizione come testo normale o HTML tramite il menu **Altre opzioni** (…) e selezionando **Passa al testo normale** o **Passa a formato HTML**.

Inizio pagina

## Ordine di precedenza per le opzioni di codifica dei messaggi

Exchange utilizza l'ordine di precedenza descritto nel seguente elenco per determinare le opzioni di codifica per i messaggi in uscita inviati a destinatari esterni all'organizzazione di Exchange:

1.  Impostazioni del dominio remoto

2.  Impostazioni di Outlook o Outlook Web App

3.  Impostazioni dell'utente di posta o del contatto di posta

Nell'elenco viene specificato l'ordine di precedenza dal livello più basso a quello più alto. Un'impostazione creata a un livello più alto può avere la precedenza su un'impostazione creata a un livello più basso.

Nella seguente tabella viene descritto l'ordine di precedenza dalla priorità più bassa a quella più elevata per le opzioni di codifica dei set di caratteri dei messaggi.

### Ordine di precedenza dalla priorità più bassa a quella più elevata per le opzioni di codifica dei set di caratteri dei messaggi

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origine</th>
<th>Parametro</th>
<th>Valori</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Impostazione delle voci di dominio remoto tramite EAC o <strong>Set-RemoteDomain</strong></p></td>
<td><p><em>CharacterSet</em></p></td>
<td><p>Specificato</p></td>
</tr>
<tr class="even">
<td><p>Impostazione delle voci di dominio remoto tramite EAC o <strong>Set-RemoteDomain</strong></p></td>
<td><p><em>NonMimeCharacterSet</em></p></td>
<td><p>Specificato</p></td>
</tr>
<tr class="odd">
<td><p>Impostazioni di Outlook</p></td>
<td><p>Codifica dei set di caratteri dei messaggi</p></td>
<td><ul>
<li><p>Selezione automatica</p></li>
<li><p>Specificato</p></li>
</ul></td>
</tr>
</tbody>
</table>


Quando si imposta la serie di caratteri non MIME per un dominio remoto, questa viene assegnata ai seguenti tipi di messaggio:

  - Messaggi in uscita verso un dominio remoto configurato che non contengono un set di caratteri specificato.

  - Messaggi in arrivo provenienti da un dominio remoto configurato che non contengono un set di caratteri specificato.

Il valore della tabella codici ANSI di Windows per il server di trasporto viene utilizzato per assegnare un set di caratteri ai seguenti tipi di messaggi:

  - Messaggi interni che non contengono un set di caratteri specificato.

  - Messaggi interni che contengono un set di caratteri specificato, ma non una tabella codici per il server specificato.

Se il messaggio contiene un set di caratteri specificato ma non valido, il server di trasporto tenta di sostituire tale set non valido con un altro set valido.

Nella seguente tabella viene descritto l'ordine di precedenza dalla priorità più bassa a quella più elevata per le opzioni di codifica dei messaggi in testo normale.

### Ordine di precedenza dalla priorità più bassa a quella più elevata per le opzioni di codifica dei messaggi in testo normale

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origine</th>
<th>Parametro</th>
<th>Valori</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>LineWrapSize</em></p></td>
<td><ul>
<li><p>Da 0 a 132</p></li>
<li><p>illimitato</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Impostazioni di Outlook</p></td>
<td><p>Formato del messaggio</p></td>
<td><p>Testo normale</p></td>
</tr>
<tr class="odd">
<td><p>Impostazioni di Outlook</p></td>
<td><p>Formato del messaggio Internet</p></td>
<td><p>Opzioni testo normale:</p>
<ul>
<li><p>Codifica degli allegati in formato UUENCODE per l'invio di un messaggio di testo normale</p></li>
<li><p>A capo automatico dopo <em>nn</em> caratteri</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Impostazioni di Outlook</p></td>
<td><p>Formato del messaggio per destinatari Internet</p></td>
<td><p>Formato di testo normale:</p>
<ul>
<li><p>Codifica degli allegati in formato allegato UuEncode</p></li>
<li><p>Utilizzo del formato allegato Mac BinHex</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><ul>
<li><p><code>$true</code></p></li>
<li><p><code>$false</code></p></li>
</ul>
<p>Se il valore è <code>$false</code> o se il destinatario non è definito come utente o contatto di posta elettronica nell'organizzazione di Exchange, le impostazioni dell'utente o del contatto di posta vengono ignorate.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><p>Testo</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><p>Testo</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>UuEncode</p></li>
</ul></td>
</tr>
</tbody>
</table>


Nella seguente tabella viene descritto l'ordine di precedenza dalla priorità più bassa a quella più elevata per le opzioni di codifica dei messaggi MIME.

### Ordine di precedenza dalla priorità più bassa a quella più elevata per le opzioni di codifica dei messaggi MIME

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origine</th>
<th>Parametro</th>
<th>Valori</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>ContentType</em></p></td>
<td><ul>
<li><p><code>MimeHtmlText</code></p></li>
<li><p><code>MimeText</code></p></li>
<li><p><code>MimeHtml</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Impostazioni di Outlook o Outlook Web App</p></td>
<td><p>Formato del messaggio</p></td>
<td><ul>
<li><p>Testo normale</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Impostazioni di Outlook</p></td>
<td><p>Formato del messaggio per destinatari Internet</p></td>
<td><p>Formato messaggio MIME</p>
<ul>
<li><p>Testo normale</p></li>
<li><p>Includi testo normale e HTML</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><p><code>$true</code></p>
<p><code>$false</code></p>
<p>Se il valore è <code>$false</code> o se il destinatario non è definito come utente o contatto di posta elettronica nell'organizzazione di Exchange, le impostazioni dell'utente o del contatto di posta vengono ignorate.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><ul>
<li><p>Testo</p></li>
<li><p>Mime</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><ul>
<li><p><code>Text</code></p></li>
<li><p><code>Html</code></p></li>
<li><p><code>TextAndHtml</code></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>AppleSingle</p></li>
<li><p>AppleDouble</p></li>
</ul></td>
</tr>
</tbody>
</table>


Inizio pagina

## Ulteriori informazioni

[Opzioni di codifica dei messaggi](message-encoding-options-exchange-2013-help.md)

[Opzioni di conversione TNEF](tnef-conversion-options-exchange-2013-help.md)

[Domini remoti](remote-domains-exchange-2013-help.md)

[Domini remoti in Exchange Online](https://technet.microsoft.com/it-it/library/jj966211\(v=exchg.150\))

[Gestire gli utenti di posta](https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-mail-users)

[Gestire i contatti di posta](https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-mail-contacts)

[Modifica del formato dei messaggi in Outlook](https://go.microsoft.com/fwlink/p/?linkid=397890)


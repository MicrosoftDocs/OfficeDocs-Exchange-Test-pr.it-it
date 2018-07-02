---
title: 'Registrazione del protocollo POP3 e IMAP4: Exchange 2013 Help'
TOCTitle: Registrazione del protocollo POP3 e IMAP4
ms:assetid: 212ed3d5-0c98-4346-a860-1cfcac5d73c4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335141(v=EXCHG.150)
ms:contentKeyID: 50555555
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registrazione del protocollo POP3 e IMAP4

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile utilizzare la registrazione per esaminare le connessioni POP3 e IMAP4 Exchange nell'ambiente in uso del protocollo. Questo può essere utile se si sta risolvendo problemi relativi alle prestazioni POP3 o IMAP4.

## Abilitazione della registrazione del protocollo POP3 e IMAP4

È possibile abilitare, disabilitare o modificare la registrazione del protocollo utilizzando Exchange Management Shell. Se si abilita la registrazione del protocollo utilizzando la Shell, verranno utilizzate le impostazioni di registrazione del protocollo predefinito. Nella maggior parte dei casi, le impostazioni predefinite sono sufficienti.

In alternativa, è possibile abilitare, disabilitare e modificare opzioni di registrazione del protocollo modificando il Microsoft.Exchange.Pop3.exe.config e i file di configurazione Microsoft.Exchange.Imap4.exe.config presente nella MicrosoftExchange Server 2013 server Accesso Client. Per ulteriori informazioni su come gestire le impostazioni del protocollo POP3 e IMAP4, vedere [Configurare la registrazione del protocollo POP3 e IMAP4](configure-protocol-logging-for-pop3-and-imap4-exchange-2013-help.md).

## Esaminare il Registro di protocollo

I file di registro protocollo sono i file di testo che contengono dati nel formato di file delimitato da virgole (CSV). Il Registro di protocollo archivia ogni evento di protocollo in un'unica riga. Le informazioni archiviate su ogni riga sono organizzate in base ai campi. Questi campi sono separati da virgole. Nella tabella seguente vengono descritti i campi utilizzati per classificare ogni evento di protocollo.

### Campi utilizzati per classificare ogni evento protocollo

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome campo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Data-ora</p></td>
<td><p>Data e ora dell'evento protocollo. Il valore è formattato come <em>yyyy-mm-ddhh:mm:ss.fffZ</em>, dove <em>yyyy</em> = anno, <em>mm</em> = mese, <em>dd</em> = giorno, <em>hh</em> = ore, <em>mm</em> = minuti, <em>ss</em> = secondo, <em>fff</em> = frazioni di secondo, e <em>Z</em> indica Zulu. Zulu è un altro modo per indicare il formato UTC (Coordinated Universal Time).</p></td>
</tr>
<tr class="even">
<td><p>id connettore</p></td>
<td><p>In questo campo non viene utilizzato per la registrazione del protocollo POP3 e IMAP4.</p></td>
</tr>
<tr class="odd">
<td><p>id di sessione</p></td>
<td><p>GUID che identifica in modo univoco la sessione SMTP associato a un evento di protocollo.</p></td>
</tr>
<tr class="even">
<td><p>numero di sequenza</p></td>
<td><p>Contatore che inizia a 0 e viene incrementato per ogni evento nella stessa sessione.</p></td>
</tr>
<tr class="odd">
<td><p>endpoint locale</p></td>
<td><p>Endpoint locale di una sessione POP3 o IMAP4. Si tratta di un indirizzo IP e numero di porta TCP, il seguente formato: <em>&lt;IP address&gt;</em>:<em>&lt;port&gt;</em>.</p></td>
</tr>
<tr class="even">
<td><p>endpoint remoti</p></td>
<td><p>Endpoint remoti di una sessione POP3 o IMAP4. Si tratta di un indirizzo IP e numero di porta TCP, il seguente formato: <em>&lt;IP address&gt;</em>:<em>&lt;port&gt;</em>.</p></td>
</tr>
<tr class="odd">
<td><p>evento</p></td>
<td><p>Un singolo carattere che rappresenta l'evento protocollo. I valori possibili per l'evento sono i seguenti:</p>
<ul>
<li><p>+   Connessione</p></li>
<li><p>-   Disconnessione</p></li>
<li><p>&gt; Invia</p></li>
<li><p>&lt; Ricevere</p></li>
<li><p>*   Informazioni</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>dati</p></td>
<td><p>Informazioni di testo sono associata all'evento POP3 o IMAP4.</p></td>
</tr>
<tr class="odd">
<td><p>contesto</p></td>
<td><p>In questo campo non viene utilizzato per la registrazione del protocollo POP3 e IMAP4.</p></td>
</tr>
</tbody>
</table>


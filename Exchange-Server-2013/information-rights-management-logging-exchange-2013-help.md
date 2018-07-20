---
title: 'Registrazione di Information Rights Management: Exchange 2013 Help'
TOCTitle: Registrazione di Information Rights Management
ms:assetid: e06f57f9-a9e2-43a2-b88c-288b324d71f0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff461940(v=EXCHG.150)
ms:contentKeyID: 50481868
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registrazione di Information Rights Management

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

In Microsoft Exchange Server 2013, vengono registrate le operazioni di Information Rights Management (IRM) nei registri IRM. I registri IRM consentono di monitorare e risolvere i problemi interazioni tra il client Rights Management Services (RMS) su un server Exchange 2013 e il cluster di Rights Management Services (AD RMS) Active Directory all'interno dell'organizzazione.

Per informazioni relative a IRM, vedere [Information Rights Management](information-rights-management-exchange-2013-help.md).

**Sommario**

Struttura dei registri IRM

Processo di registrazione

Informazioni scritte i registri IRM

I registri di gestione di IRM

Per informazioni sulle attività di gestione relative a IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Struttura dei registri IRM

Per impostazione predefinita, i registri IRM si trovano in C:\\Programmi\\Microsoft\\Exchange Server\\V14\\Logging\\IRMLogs.

La convenzione di denominazione per i registri IRM è \<*Processo*\>\_\<*ID Processo* o *identificatore IIS AppPool*\>\_IRMLOG*aaaammgg*-*nnnn*.log, dove:

  - \<*Process*\>= processo che crea il file di registro. Nel servizio di trasporto, ad esempio, sarà EdgeTransport.

  - \<*ID Processo* o *identificatore IIS AppPool\>* =ID numerico del processo.

  - *aaaammgg* = la data UTC (Coordinated Universal Time) di creazione del file di registro.

  - *nnnn* = numero di istanza, inizia da 1 ogni giorno.

Un esempio di nome del file di registro è EdgeTransport\_1056\_IRMLOG20101201-1.log.

La tabella seguente mostra i registri generati da diversi ruoli del server.

### Registri sui ruoli del server

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo del server</th>
<th>Nome file di registro IRM</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servizio di trasporto</p></td>
<td><p>EdgeTransport_&lt;<em>ID Processo</em>&gt;_IRMLOG<em>aaaammgg</em>-<em>nnnn</em>.log</p></td>
<td><p>Questo registro viene utilizzato per registrare tutte le transazioni RMS effettuate da pipeline di trasporto nel servizio di trasporto (ad esempio, le regole di protezione di trasporto e decrittografia dei rapporti del journal). L'identificatore (PID) del processo di edgetransport.exe viene utilizzato per generare il nome del file di registro.</p></td>
</tr>
<tr class="even">
<td><p>Cassette postali</p></td>
<td><p>msftefd_&lt;<em>ID Processo</em>&gt;_IRMLOG<em>aaaammgg</em>-<em>nnnn</em>.log</p></td>
<td><p>Questo registro viene utilizzato per registrare tutte le transazioni RMS che si verificano durante le richieste di ricerca e indice. Exchange 2013 Server cassette postali tramite la procedura msftefd.exe per l'indicizzazione del contenuto. Il numero di serie del processo di msftefd.exe viene utilizzato per generare il nome del file di registro.</p></td>
</tr>
<tr class="odd">
<td><p>Accesso client</p></td>
<td><p>w3wp_MSExchangeOWAAppOol_IRMLOG<em>aaaammgg</em>-<em>nnnn</em>.log</p></td>
<td><p>Questo registro è utilizzato per registrare tutte le transazioni IRM in Microsoft OfficeOutlook Web App.</p></td>
</tr>
<tr class="even">
<td><p>Tutti i ruoli del server Exchange 2013</p></td>
<td><p>w3wp_MSExchangePowerShellAppPool_IRMLOG<em>aaaammgg</em>-<em>nnnn</em>.log</p></td>
<td><p>Questo registro è utilizzato per registrare tutte le transazioni IRM RMS effettuate da Windows PowerShell, ad esempio, quando si esegue il cmdlet <strong>Test-IRMConfiguration</strong>.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Processo di registrazione

Le informazioni vengono scritte sul file di registro fino a quando le dimensioni del file non raggiungono il valore massimo specificato. Quando viene raggiunto il valore massimo, viene creato un file di registro con un numero di istanza incrementato. Questo processo si ripete per tutta la giornata. La registrazione circolare rileva i file di registro più vecchi quando la directory del registro IRM raggiunge le dimensioni massime specificate oppure quando un file di registro raggiunge il limite di validità specificato nella configurazione di registrazione IRM su ciascun server.

Inizio pagina

## Informazioni scritte i registri IRM

I file di registro IRM sono file di testo che contengono dati nel formato CSV (Comma Separated Value). In ciascun file di registro IRM è presente un'intestazione in cui sono contenute le seguenti informazioni:

  - **\#Software**   Il nome del software con cui è stato creato il file di registro IRM. In genere, il valore è `Microsoft Exchange Server`.

  - **\#Version**   Numero della versione del software con cui è stato creato il file di registro IRM.

  - **\#Log-type**   Valore del tipo di registro, che è `Rms Client Manager Log`.

  - **\#Date:**    Data/ora UTC in cui il file di registro è stato creato. La data/ora UTC viene rappresentata nel formato data/ora ISO 8601: *aaaa*-*mm*-*gg*T*hh*:*mm*:*ss.fff*Z, dove:
    
      - aaaa = anno
    
      - *mm*  = mese
    
      - *gg*  = giorno
    
      - T = separatore utilizzato per indicare l'inizio della componente dell'orario
    
      - *hh* = ora
    
      - *mm*  = minuti
    
      - *ss* = secondi
    
      - *fff* = frazioni di secondo
    
      - Z = Zulu, che è un altro modo di indicare UTC

  - **\#Fields**   Nomi dei campi delimitati da virgole utilizzati nei file di registro IRM.
    
    I registri IRM memorizzano ciascun evento transazione RMS su una singola riga, organizzata in campi separati da virgole. La tabella seguente elenca i campi nei registri IRM per tutti i ruoli del server con la funzionalità IRM abilitata.
    
    ### Campi utilizzati nei registri IRM
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Campo</th>
    <th>Descrizione</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Date-time</strong></p></td>
    <td><p>Elenca il timestamp UTC.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Feature</strong></p></td>
    <td><p>Elenca le funzionalità client RMS utilizzate. Tra i valori validi sono inclusi:</p>
    <ul>
    <li><p><code>RacClc</code></p></li>
    <li><p><code>Template</code></p></li>
    <li><p><code>Prelicense</code></p></li>
    <li><p><code>UseLicense</code></p></li>
    <li><p>Verifica della firma</p></li>
    <li><p><code>ServerInfo</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Event-Type</strong></p></td>
    <td><p>Elenca il tipo di evento. Tra i valori validi sono inclusi:</p>
    <ul>
    <li><p><code>Acquire</code>   È richiesta una licenza o un modello RMS.</p></li>
    <li><p><code>Success</code>   È stata acquisita una licenza o un modello RMS.</p></li>
    <li><p><code>Exception</code>   Si è verificato un errore.</p></li>
    <li><p><code>Queued</code>   Una richiesta è sospesa.</p></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td><p><strong>Tenant-Id</strong></p></td>
    <td><p>Solo per uso interno Microsoft.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Server-url</strong></p></td>
    <td><p>Elenca gli URL dei server RMS a cui si è acceduto durante le operazioni.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Context</strong></p></td>
    <td><p>Utilizzato dal processo chiamante per unire tra loro più transazioni RMS. Tra i valori validi sono inclusi:</p>
    <ul>
    <li><p><code>MessageID: &lt;Actual message ID&gt;</code></p></li>
    <li><p><code>MailboxGuid: &lt;Mailbox GUID&gt;</code></p></li>
    <li><p><code>AttachmentFileName: &lt;File name&gt;</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Transaction-id</strong></p></td>
    <td><p>Identifica in modo univoco la transazione. Tutti gli eventi che accadono durante una transazione hanno lo stesso ID transazione.</p></td>
    </tr>
    </tbody>
    </table>


Inizio pagina

## I registri di gestione di IRM

Su ciascun ruolo del server per cui la funzionalità IRM è abilitata, per impostazione predefinita è abilitata la registrazione IRM. Per ciascun ruolo del server, è possibile modificare le seguenti impostazioni di registrazione IRM utilizzando il cmdlet **Set** relativo a ciascun ruolo del server. Per configurare, ad esempio, la registrazione IRM su un server Cassette postali, utilizzare il cmdlet **Set-MailboxServer**.

### Parametri di configurazione dei registri IRM

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
<td><p><em>IrmLogEnabled</em></p></td>
<td><p>Abilita la registrazione per le transazioni IRM. La registrazione IRM è abilitata per impostazione predefinita. Per disabilitare la registrazione IRM per il ruolo del server, impostare il parametro su <code>$false</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxAge</em></p></td>
<td><p>Specifica il limite massimo di validità dei file di registro IRM. I file precedenti al valore specificato vengono eliminati. Il valore predefinito è <code>30.00:00:00</code> (30 giorni).</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogMaxDirectorySize</em></p></td>
<td><p>Specifica la dimensione massima di tutti i registri IRM nella directory dei registri di connettività. Quando una directory raggiunge la dimensione massima dei file, il server elimina innanzitutto i file di log meno recenti. Il valore predefinito è <code>250 MB</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxFileSize</em></p></td>
<td><p>Specifica la dimensione massima di un singolo file di registro. Quando un file raggiunge la dimensione specificata, viene creato un file di registro e viene incrementato il numero di istanza. Il valore predefinito è <code>10 MB</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogPath</em></p></td>
<td><p>Specifica il percorso del registro IRM. Il percorso predefinito è % ExchangeInstallPath%Logging\IRMLogs.</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [Set-MailboxServer](https://technet.microsoft.com/it-it/library/aa998651\(v=exchg.150\))

  - [Set-ClientAccessServer](https://technet.microsoft.com/it-it/library/bb125157\(v=exchg.150\))

  - [Set-TransportService](https://technet.microsoft.com/it-it/library/jj215682\(v=exchg.150\))

Inizio pagina


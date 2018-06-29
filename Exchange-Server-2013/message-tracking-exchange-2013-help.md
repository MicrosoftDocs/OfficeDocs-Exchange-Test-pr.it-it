---
title: 'Verifica messaggi: Exchange 2013 Help'
TOCTitle: Verifica messaggi
ms:assetid: bada2ea7-6d7c-4630-b7f1-67f56818f0ff
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124375(v=EXCHG.150)
ms:contentKeyID: 51407404
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Verifica messaggi

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

In Microsoft Exchange Server 2013, il registro di verifica messaggi è un record dettagliato di tutta l'attività relativa ai messaggi trasferiti al/dal servizio di trasporto sui server Cassette postali, alle/dalle cassette postali sui server Cassette postali e ai/dai server Trasporto Edge. I registri di verifica messaggi possono essere utilizzati per le indagini sui messaggi, l'analisi del flusso di posta, le segnalazioni e la risoluzione dei problemi.

In Exchange 2013, è possibile utilizzare il cmdlet **Set-TransportService** o **Set-MailboxServer** per tutte le attività di configurazione della verifica dei messaggi perché il server Cassette postali di Exchange 2013 contiene il servizio di trasporto e le cassette postali. Questi cmdlet consentono di apportare le seguenti modifiche alla configurazione della verifica messaggi:

  - Abilitare o disabilitare la verifica messaggi. L'impostazione predefinita è abilitata.

  - Specificare la posizione dei file di registro della verifica messaggi.

  - Specificare una dimensione massima per i singoli file di registro della verifica messaggi. L'impostazione predefinita è 10 MB.

  - Specificare una dimensione massima per la directory contenente i file di registro della verifica dei messaggi: L'impostazione predefinita è 1.000 MB.

  - Specificare il limite di validità massimo per i file di registro della verifica messaggi: L'impostazione predefinita è 30 giorni.

  - Abilitare o disabilitare la registrazione degli oggetti nei registri della verifica messaggi. L'impostazione predefinita è abilitata.


> [!NOTE]
> È possibile, inoltre, utilizzare l'interfaccia di amministrazione di Exchange (EAC) per abilitare o disabilitare la verifica messaggi e per specificare il percorso dei file di registro della verifica messaggi.



Per impostazione predefinita, Exchange utilizza la registrazione circolare per limitare i registri di verifica messaggi in base alle dimensioni e al limite di validità dei file al fine di controllare lo spazio su disco rigido utilizzato dai file di registro di verifica messaggi.

**Sommario**

Ricerca nel registro di verifica messaggi

Struttura dei file di registro di verifica messaggi

Campi dei file di registro di verifica messaggi

Tipi di evento nel registro di verifica messaggi

Valori dell'origine del registro di verifica messaggi

Voci di esempio nel registro di verifica messaggi

Problemi relativi alla protezione per il registro di verifica messaggi

## Ricerca nel registro di verifica messaggi

I registri di verifica messaggi contengono grandi quantità di dati relativi allo spostamento dei messaggi attraverso un server Cassette postali di Exchange 2013. Per effettuare ricerche nei registri di verifica messaggi sono disponibili diverse opzioni.

  - **Get-MessageTrackingLog**   Gli amministratori possono utilizzare questo cmdlet per cercare nel registro di verifica messaggi informazioni sui messaggi con numerosi criteri di filtro. Per ulteriori informazioni, vedere [Registri di verifica messaggi di ricerca](search-message-tracking-logs-exchange-2013-help.md).

  - **Rapporti di recapito per gli amministratori**   Gli amministratori possono utilizzare la scheda **Rapporti di recapito** nell'interfaccia di amministrazione di Exchange (EAC) o i cmdlet **Search-MessageTrackingReport** e**Get-MesageTrackingReport** sottostanti per cercare nei registri di verifica messaggi informazioni sui messaggi inviati da una specifica cassetta postale dell'organizzazione. Per ulteriori informazioni, vedere [Rapporti di recapito per gli amministratori](delivery-reports-for-administrators-exchange-2013-help.md).

  - **Rapporti di recapito per gli utenti**   Gli utenti possono utilizzare la scheda **Rapporti di recapito** di Outlook Web App per cercare nei registri di verifica messaggi le informazioni sui messaggi inviati alla/dalla propria cassetta postale. Per ulteriori informazioni, vedere la pagina dei [rapporti di recapito per gli utenti](https://go.microsoft.com/fwlink/?linkid=279920).

Inizio pagina

## Struttura dei file di registro di verifica messaggi

Per impostazione predefinita, i file di registro di verifica messaggi si trovano in %ExchangeInstallPath%TransportRoles\\Logs\\MessageTracking.

La convenzione di denominazione per i file di registro nella directory dei registri della verifica messaggi è `MSGTRK`*aaaammgg-nnnn*`.log`, `MSGTRKMA`*aaaammgg-nnnn*`.log`, `MSGTRKMD`*aaaammgg-nnnn*`.log` e `MSGTRKMS`*aaaammgg-nnnn*`.log` . I diversi registri sono utilizzati dai seguenti servizi:

  - **MSGTRK**   Questi registri sono associati al servizio di trasporto.

  - **MSGTRKMA**   Questi registri sono associati alle approvazioni e ai rifiuti utilizzati dal trasporto moderato. Per ulteriori informazioni, vedere [Gestione approvazione del messaggio](manage-message-approval-exchange-2013-help.md).

  - **MSGTRKMD**   Questi registri sono associati ai messaggi recapitati alle cassette postali dal servizio Recapito alle cassette postali.

  - **MSGTRKMD**   Questi registri sono associati ai messaggi inviati dalle cassette postali dal servizio Recapito alle cassette postali.

I segnaposto nei nomi dei file di registro rappresentano le seguenti informazioni:

  - Il segnaposto *aaaammgg* è la data nel formato UTC (Coordinated Universal Time) in cui è stato creato il file di registro. *aaaa* = anno, *mm* = mese e *gg* = giorno.

  - Il segnaposto *nnnn* è un numero di istanza che inizia con il valore 1 ogni giorno per ciascun prefisso del nome dei file del registro di verifica dei messaggi.

Le informazioni vengono scritte su ciascun file di registro fino a quando le dimensioni del file non raggiungono il valore massimo specificato per ogni file di registro. Viene quindi aperto un nuovo file di registro con un numero di istanza maggiore. Questo processo si ripete per tutta la giornata. La funzionalità di rotazione dei file di registro elimina i file più vecchi quando si verifica una della seguenti condizioni:

  - Un file di registro raggiunge il limite di validità massimo specificato.

  - La directory dei registri di verifica messaggi raggiunge la dimensione massima specificata.
    

    > [!IMPORTANT]
    > La dimensione massima della directory dei registri di verifica dei messaggi viene calcolata come dimensione totale di tutti i file di registro con lo stesso prefisso del nome. Gli altri file che non seguono la convenzione del prefisso del nome non vengono conteggiati nel calcolo della dimensione totale della directory. Se si rinominano i file di registro meno recenti o si copiano gli altri file nella directory dei registri di verifica dei messaggi, la directory potrebbe superare la dimensione massima specificata.<BR>Nei server Cassette postali di Exchange 2013 la dimensione massima della directory del registro di verifica messaggi è tre volte superiore al valore specificato. Anche se i file di registro della verifica messaggi generati da quattro diversi servizi hanno quattro diversi prefissi dei nomi, la quantità e la frequenza dei dati scritti nei file di registro di <STRONG>MSGTRKMA</STRONG> sono trascurabili rispetto a quelle degli altri prefissi dei file di registro.



I file di registro di verifica messaggi sono file di testo che contengono dati in formato CSV (Comma Separated Value). In ciascun file di registro di verifica messaggi è presente un'intestazione in cui sono contenute le seguenti informazioni:

  - **\#Software:** il nome del software con cui è stato creato il file di registro di verifica messaggi. Generalmente, il valore è Microsoft Exchange Server.

  - **\#Version:** il numero della versione del software con cui è stato creato il file di registro di verifica messaggi. Il valore corrente è 15.0.0.0.

  - **\#Log-Type:**   il valore del tipo di registro, in questo caso Message Tracking Log.

  - **\#Date:**   Data/ora UTC in cui il file di registro è stato creato. La data/ora UTC viene rappresentata nel formato data/ora ISO 8601: *yyyy-mm-dd*T*hh:mm:ss.fff*Z, dove *yyyy* = anno, *mm* = mese, *dd* = giorno, T indica l'inizio della componente oraria, *hh* = ore, *mm* = minuti, *ss* = secondi, *fff* = frazioni di secondo e Z indica Zulu, un altro modo per denominare UTC.

  - **\#Fields:**   nomi dei campi delimitati da virgole utilizzati nei file di registro di verifica messaggi.

Inizio pagina

## Campi dei file di registro di verifica messaggi

Il registro di verifica messaggi archivia ciascun evento di messaggio su un'unica riga nel registro. Le informazioni sugli eventi dei messaggi sono organizzate in base ai campi e tali campi sono separati da virgole. Il nome del campo in genere è abbastanza descrittivo da consentire di determinare il tipo di informazione contenuta. Tuttavia, alcuni campi potrebbero essere vuoti oppure il tipo di informazioni archiviato nel campo potrebbe cambiare a seconda del tipo di evento del messaggio e al tipo di file di registro di verifica messaggi in cui è stato registrato l'evento. Le descrizioni generali dei campi utilizzati per classificare ogni evento di verifica messaggi sono fornite nella tabella seguente.


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
<td><p><strong>date-time</strong></p></td>
<td><p>Data/ora UTC dell'evento di verifica messaggi. La data/ora UTC viene rappresentata nel formato data/ora ISO 8601: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, dove <em>yyyy</em> = anno, <em>mm</em> = mese, <em>dd</em> = giorno, T indica l'inizio della componente oraria, <em>hh</em> = ore, <em>mm</em> = minuti, <em>ss</em> = secondi, <em>fff</em> = frazioni di secondo e Z indica Zulu, un altro modo per denominare UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>client-ip</strong></p></td>
<td><p>L'indirizzo IPv4 o IPv6 del server di messaggistica o del client di messaggistica che ha inviato il messaggio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>client-hostname</strong></p></td>
<td><p>Il nome host o il nome di dominio completo del server di messaggistica o del client di messaggistica che ha inviato il messaggio.</p></td>
</tr>
<tr class="even">
<td><p><strong>server-ip</strong></p></td>
<td><p>L'indirizzo IPv4 o IPv6 dell'origine o della destinazione del server Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>server-hostname</strong></p></td>
<td><p>Il nome host o il nome di dominio completo del server di destinazione.</p></td>
</tr>
<tr class="even">
<td><p><strong>source-context</strong></p></td>
<td><p>Informazioni aggiuntive associate al campo di <strong>origine</strong>. Ad esempio, informazioni sull'agente di trasporto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>connector-id</strong></p></td>
<td><p>Il nome del connettore di invio o del connettore di ricezione di origine o di destinazione. Ad esempio, <em>ServerName</em>\<em>ConnectorName</em> o <em>ConnectorName</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>source</strong></p></td>
<td><p>Il componente di trasporto di Exchange responsabile per l'evento di verifica messaggi. I valori che si trovano in questo campo sono descritti nella sezione Valori dell'origine del registro di verifica messaggi di questo argomento.</p></td>
</tr>
<tr class="odd">
<td><p><strong>event-id</strong></p></td>
<td><p>Il tipo di evento di messaggio. I tipi di evento sono descritti nella sezione Tipi di evento nel registro di verifica messaggi di questo messaggio.</p></td>
</tr>
<tr class="even">
<td><p><strong>internal-message-id</strong></p></td>
<td><p>Un identificativo del messaggio assegnato al server Exchange che sta elaborando il messaggio.</p>
<p>Il valore di <strong>internal-message-id</strong> di un messaggio specifico è diverso nel registro di verifica messaggi di ciascun server Exchange coinvolto nella trasmissione del messaggio. Un valore di esempio è <code>73014444033</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-id</strong></p></td>
<td><p>Il valore del campo di intestazione <strong>Message-Id:</strong> trovato nell'intestazione del messaggio. Se il campo di intestazione <strong>Message-Id:</strong> non esiste o è vuoto, viene assegnato un valore arbitrario. Questo valore rimane immutato per tutta la durata del messaggio. Per i messaggi creati in Exchange, il valore è nel formato <code>&lt;GUID@ServerFQDN&gt;</code>, incluse le parentesi angolari (<code>&lt; &gt;</code>). Ad esempio, <code>&lt;4867a3d78a50438bad95c0f6d072fca5@mailbox01.contoso.com&gt;</code>. Altri sistemi di messaggistica potrebbero utilizzare una sintassi o valori diversi.</p></td>
</tr>
<tr class="even">
<td><p><strong>network-message-id</strong></p></td>
<td><p>Un ID messaggio univoco che persiste tra le copie del messaggio che si possono creare a causa della biforcazione o dell'espansione del gruppo di distribuzione. Un valore di esempio è <code>1341ac7b13fb42ab4d4408cf7f55890f</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>recipient-address</strong></p></td>
<td><p>Gli indirizzi di posta elettronica dei destinatari del messaggio. Gli indirizzi di posta elettronica multipli sono separati dal carattere punto e virgola (;).</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-status</strong></p></td>
<td><p>Questo campo contiene lo stato del destinatario per ogni destinatario separato dal carattere di punto e virgola (;). I valori di stato sono presentati per i destinatari nello stesso ordine dei valori nel campo <strong>recipient-address</strong>. Valori di stato di esempio sono <code>250 2.1.5 Recipient OK</code> e <code>550 4.4.7 QUEUE.Expired;&lt;ErrorText&gt;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>total-bytes</strong></p></td>
<td><p>Le dimensioni massime del messaggio, compresi gli allegati, in byte.</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-count</strong></p></td>
<td><p>Il numero di destinatari per il messaggio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>related-recipient-address</strong></p></td>
<td><p>Questo campo viene utilizzato con gli eventi <strong>EXPAND</strong>, <strong>REDIRECT</strong> e <strong>RESOLVE</strong> per visualizzare gli altri indirizzi di posta elettronica dei destinatari associati al messaggio.</p></td>
</tr>
<tr class="even">
<td><p><strong>reference</strong></p></td>
<td><p>Questo campo contiene informazioni aggiuntive per i tipi specifici di eventi. Ad esempio:</p>
<p><strong>DSN</strong>   Contiene il collegamento al rapporto, ossia il valore <strong>Message-Id</strong> della notifica di stato di recapito (DSN) associato se un DSN viene generato dopo questo evento. Se si tratta di un messaggio di notifica di stato di recapito, il valore del campo <strong>Reference</strong> contiene il valore <strong>Message-Id</strong> del messaggio originale generato per cui è stato generato il DSN.</p>
<p><strong>EXPAND</strong>   Il campo Reference contiene il valore di <strong>related-recipient-address</strong> dei messaggi correlati.</p>
<p><strong>RECEIVE</strong>   Il campo Reference potrebbe contenere il valore di <strong>Message-Id</strong> del messaggio correlato se il messaggio è stato generato da altri processi, ad esempio journaling o regole di Posta in arrivo.</p>
<p><strong>SEND</strong>   Il campo Reference contiene il valore di <strong>Internal-Message-Id</strong> di eventuali messaggi DSN.</p>
<p><strong>THROTTLE</strong>   Il campo Reference contiene il motivo della limitazione del messaggio.</p>
<p><strong>TRANSFER</strong> Il campo Reference contiene il valore Internet-Message-Id del messaggio che è stato duplicato.</p>
<p>Per i messaggi generati dalle regole di Posta in arrivo, il campo <strong>Reference</strong> contiene il valore di <strong>Internal-Message-Id</strong> del messaggio di Posta in arrivo che ha causato la generazione del messaggio in uscita da parte della regola di Posta in arrivo.</p>
<p>Per altri tipo di eventi, il campo <strong>Reference</strong> potrebbe contenere il valore di <strong>Internal-Message-Id</strong> per i messaggi duplicati.</p>
<p>Per tutti gli altri tipi di evento, il campo <strong>Reference</strong> in genere è vuoto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-subject</strong></p></td>
<td><p>L'oggetto del messaggio che si trova nel campo di intestazione <code>Subject:</code>. La verifica degli oggetti dei messaggi viene controllata dal parametro <em>MessageTrackingLogSubjectLoggingEnabled</em> nei cmdlet <strong>Set-TransportService</strong> o <strong>Set-MailboxServer</strong>. Per impostazione predefinita, la verifica degli oggetti dei messaggi è attivata.</p></td>
</tr>
<tr class="even">
<td><p><strong>sender-address</strong></p></td>
<td><p>L'indirizzo di posta elettronica specificato nel campo di intestazione <code>Sender:</code> o nel campo di intestazione <code>From:</code> se <code>Sender:</code> non è presente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>return-path</strong></p></td>
<td><p>L'indirizzo di posta elettronica del mittente specificato dal campo <code>MAIL FROM:</code> nella busta del messaggio. Benché tale campo non sia mai vuoto, può avere il valore indirizzo mittente nullo rappresentato come <code>&lt;&gt;</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>message-info</strong></p></td>
<td><p>Ulteriori informazioni sul messaggio. Ad esempio:</p>
<ul>
<li><p>La data/ora UTC di origine del messaggio per gli eventi <strong>DELIVER</strong> e <strong>SEND</strong>. La data e l'ora di origine corrispondono alla data e all'ora in cui il messaggio entra per la prima volta nell'organizzazione Exchange. La data/ora UTC viene rappresentata nel formato data/ora ISO 8601: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, dove <em>yyyy</em> = anno, <em>mm</em> = mese, <em>dd</em> = giorno, T indica l'inizio della componente oraria, <em>hh</em> = ore, <em>mm</em> = minuti, <em>ss</em> = secondi, <em>fff</em> = frazioni di secondo e Z indica Zulu, un altro modo per denominare UTC.</p></li>
<li><p>Errori di autenticazione. Ad esempio, è possibile visualizzare il valore <code>11a</code> e il tipo di autenticazione utilizzato quando si verificano errori di autenticazione.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>directionality</strong></p></td>
<td><p>La direzione del messaggio. Valori di esempio sono <code>Incoming</code>, <code>Undefined</code> e <code>Originating</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>tenant-id</strong></p></td>
<td><p>Questo campo non è utilizzato dalle organizzazioni Exchange 2013 locali.</p></td>
</tr>
<tr class="odd">
<td><p><strong>original-client-ip</strong></p></td>
<td><p>L'indirizzo IPv4 o IPv6 del client originale.</p></td>
</tr>
<tr class="even">
<td><p><strong>original-server-ip</strong></p></td>
<td><p>L'indirizzo IPv4 o IPv6 del server originale.</p></td>
</tr>
<tr class="odd">
<td><p><strong>custom-data</strong></p></td>
<td><p>Questo campo contiene dati correlati a tipi di evento specifici. Ad esempio, l'agente regole di trasporto utilizza questo campo per registrare il GUID della regola di trasporto o il criterio DLP applicato al messaggio. Per ulteriori informazioni su questi valori dell'agente regole di trasporto, vedere la sezione sulla registrazione dei dati nell'argomento <a href="view-dlp-policy-detection-reports-exchange-2013-help.md">Visualizzare i report di rilevamento dei criteri DLP</a>,</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Tipi di evento nel registro di verifica messaggi

Diversi tipi di evento nel campo **event-id** sono utilizzati per classificare gli eventi dei messaggi nel registro di verifica messaggi. Alcuni eventi dei messaggi appaiono in un solo tipo di file di registro di verifica messaggi mentre altri eventi appaiono in tutti i tipi di file di registro di verifica messaggi. I tipi di evento utilizzati per classificare ciascun evento di messaggio sono illustrati nella tabella seguente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome evento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AGENTINFO</strong></p></td>
<td><p>Questo evento viene utilizzato dagli agenti di trasporto per registrare i dati personalizzati.</p></td>
</tr>
<tr class="even">
<td><p><strong>BADMAIL</strong></p></td>
<td><p>Dalla directory di prelievo o dalla directory di riesecuzione è stato inviato un messaggio che non può essere recapitato né restituito.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DEFER</strong></p></td>
<td><p>Il recapito del messaggio è stato ritardato.</p></td>
</tr>
<tr class="even">
<td><p><strong>DELIVER</strong></p></td>
<td><p>Un messaggio è stato recapitato a una cassetta postale locale.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DROP</strong></p></td>
<td><p>Un messaggio è stato rimosso senza notifica sullo stato del recapito (nota anche come DSN, notifica di mancato recapito, rapporto di mancato recapito o NDR). Ad esempio:</p>
<ul>
<li><p>Messaggi relativi alla richiesta di approvazione della moderazione completata.</p></li>
<li><p>I messaggi della posta indesiderata rimossi automaticamente senza NDR.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>È stata generata una notifica sullo stato del recapito (DSN, delivery status notification).</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEDELIVER</strong></p></td>
<td><p>Al destinatario è stato recapitato un messaggio duplicato. La duplicazione può avvenire se un destinatario è membro di più gruppi di distribuzione nidificati. I messaggi duplicati vengono rilevati e rimossi dall'archivio informazioni.</p></td>
</tr>
<tr class="even">
<td><p><strong>DUPLICATEEXPAND</strong></p></td>
<td><p>Durante l'espansione del gruppo di distribuzione è stato rilevato un destinatario duplicato.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEREDIRECT</strong></p></td>
<td><p>Un destinatario alternativo per il messaggio era già un destinatario.</p></td>
</tr>
<tr class="even">
<td><p><strong>EXPAND</strong></p></td>
<td><p>Un gruppo di distribuzione è stato espanso.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FAIL</strong></p></td>
<td><p>Recapito del messaggio non riuscito. Le origini sono <strong>SMTP</strong>, <strong>DNS</strong>, <strong>QUEUE</strong> e <strong>ROUTING</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>HADISCARD</strong></p></td>
<td><p>Un messaggio shadow è stato ignorato dopo il recapito della copia primaria al successivo hop. Per ulteriori informazioni, vedere <a href="shadow-redundancy-exchange-2013-help.md">Ridondanza shadow</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HARECEIVE</strong></p></td>
<td><p>Un messaggio shadow è stato ricevuto dal server nel gruppo di disponibilità del database (DAG) locale o nel sito Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><strong>HAREDIRECT</strong></p></td>
<td><p>È stato creato un messaggio shadow.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HAREDIRECTFAIL</strong></p></td>
<td><p>Non è stato possibile creare un messaggio shadow. I dettagli vengono archiviati nel campo <strong>source-context</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>INITMESSAGECREATED</strong></p></td>
<td><p>Un messaggio è stato inviato a un destinatario moderato, quindi il messaggio è stato inviato alla cassetta postale di arbitraggio per l'approvazione. Per ulteriori informazioni, vedere <a href="manage-message-approval-exchange-2013-help.md">Gestione approvazione del messaggio</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LOAD</strong></p></td>
<td><p>Un messaggio è stato correttamente caricato all'avvio.</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATIONEXPIRE</strong></p></td>
<td><p>Un moderatore per un destinatario moderato non ha mai approvato o rifiutato il messaggio, che è quindi scaduto. Per ulteriori informazioni sui destinatari moderati, vedere <a href="manage-message-approval-exchange-2013-help.md">Gestione approvazione del messaggio</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORAPPROVE</strong></p></td>
<td><p>Un moderatore per un destinatario moderato ha approvato il messaggio, che è stato quindi recapitato al destinatario moderato</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATORREJECT</strong></p></td>
<td><p>Un moderatore per un destinatario moderato ha rifiutato il messaggio, che non è stato quindi recapitato al destinatario moderato.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORSALLNDR</strong></p></td>
<td><p>Tutte le richieste di approvazione inviate a tutti i moderatori di un destinatario moderato non erano recapitabili e hanno generato rapporti di mancato recapito.</p></td>
</tr>
<tr class="even">
<td><p><strong>NOTIFYMAPI</strong></p></td>
<td><p>Un messaggio è stato rilevato nella cassetta di Posta in uscita di una cassetta posta sul server locale.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NOTIFYSHADOW</strong></p></td>
<td><p>Un messaggio è stato rilevato nella cassetta di Posta in uscita di una cassetta postale sul server locale ed è necessario creare una copia shadow del messaggio.</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>Un messaggio è stato collocato nella coda dei messaggi non elaborabili o è stato rimosso da tale coda.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PROCESS</strong></p></td>
<td><p>Il messaggio è stato elaborato correttamente.</p></td>
</tr>
<tr class="even">
<td><p><strong>PROCESSMEETINGMESSAGE</strong></p></td>
<td><p>Un messaggio di riunione è stato elaborato dal servizio Recapito alle cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RECEIVE</strong></p></td>
<td><p>Un messaggio è stato ricevuto dal componente di ricezione SMTP del servizio di trasporto o dalla directory di prelievo o di riesecuzione (origine: <code>SMTP</code>) oppure un messaggio è stato inviato da una cassetta postale al servizio Recapito alle cassette postali (origine: <code>STOREDRIVER</code>).</p></td>
</tr>
<tr class="even">
<td><p><strong>REDIRECT</strong></p></td>
<td><p>Un messaggio è stato reindirizzato a un destinatario alternativo dopo una ricerca in Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESOLVE</strong></p></td>
<td><p>I destinatari di un messaggio sono stati risolti in un indirizzo di posta elettronica diverso dopo una ricerca in Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMIT</strong></p></td>
<td><p>Un messaggio è stato reinviato automaticamente da Rete sicura. Per ulteriori informazioni, vedere <a href="safety-net-exchange-2013-help.md">Rete sicura</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESUBMITDEFER</strong></p></td>
<td><p>Un messaggio reinviato da Rete sicura è stato ritardato.</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMITFAIL</strong></p></td>
<td><p>Un messaggio reinviato da Rete sicura non è riuscito.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SEND</strong></p></td>
<td><p>Un messaggio è stato inviato tramite SMTP da un servizio di trasporto all'altro.</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMIT</strong></p></td>
<td><p>Il servizio Recapito alle cassette postali ha trasmesso correttamente il messaggio al servizio di trasporto. Per gli eventi <strong>SUBMIT</strong>, la proprietà <strong>source-context</strong> contiene i seguenti dettagli:</p>
<ul>
<li><p><strong>MDB</strong>   Il GUID del database delle cassette postali.</p></li>
<li><p><strong>Mailbox</strong>   Il GUID della cassetta postale.</p></li>
<li><p><strong>Event</strong>   Il numero di sequenza dell'evento.</p></li>
<li><p><strong>MessageClass</strong>   Il tipo di messaggio. Ad esempio, <code>IPM.Note</code>.</p></li>
<li><p><strong>CreationTime</strong>   La data e l'ora di creazione del messaggio.</p></li>
<li><p><strong>ClientType</strong>   Ad esempio <code>User</code>, <code>OWA</code> o <code>ActiveSync</code>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>SUBMITDEFER</strong></p></td>
<td><p>La trasmissione del messaggio dal servizio Recapito alle cassette postali al servizio di trasporto è stata ritardata.</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMITFAIL</strong></p></td>
<td><p>La trasmissione del messaggio dal servizio Recapito alle cassette postali al servizio di trasporto non è riuscita.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SUPPRESSED</strong></p></td>
<td><p>La trasmissione del messaggio è stata rimossa.</p></td>
</tr>
<tr class="even">
<td><p><strong>THROTTLE</strong></p></td>
<td><p>Il messaggio è stato limitato.</p></td>
</tr>
<tr class="odd">
<td><p><strong>TRANSFER</strong></p></td>
<td><p>I destinatari sono stati spostati su un messaggio duplicato in seguito a una conversione del contenuto, a limitazioni dei destinatari del messaggio o ad agenti. Le origini sono <strong>ROUTING</strong> e <strong>QUEUE</strong>.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Valori dell'origine del registro di verifica messaggi

I valori del campo **source** nel registro di verifica messaggi indicano il componente del trasporto responsabile dell'evento di verifica messaggi. Nella seguente tabella vengono descritti i valori del campo **source**.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valore di source</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ADMIN</strong></p></td>
<td><p>L'origine dell'evento era l'azione di un utente. Ad esempio, un amministratore ha utilizzato il Visualizzatore code per eliminare un messaggio o ha inviato i file dei messaggi utilizzando la directory di riesecuzione.</p></td>
</tr>
<tr class="even">
<td><p><strong>AGENT</strong></p></td>
<td><p>L'origine dell'evento era un agente di trasporto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>APPROVAL</strong></p></td>
<td><p>L'origine dell'evento è il framework di approvazione utilizzato con i destinatari moderati. Per ulteriori informazioni, vedere <a href="manage-message-approval-exchange-2013-help.md">Gestione approvazione del messaggio</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>BOOTLOADER</strong></p></td>
<td><p>L'origine evento sono messaggi non elaborati che esistono sul server in fase di avvio. Questo è correlato al tipo di evento <strong>LOAD</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DNS</strong></p></td>
<td><p>L'origine dell'evento era un DNS.</p></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>L'origine dell'evento era una notifica di stato di recapito (DSN). Ad esempio, un un rapporto di mancato recapito.</p></td>
</tr>
<tr class="odd">
<td><p><strong>GATEWAY</strong></p></td>
<td><p>L'origine dell'evento era un connettore esterno. Per ulteriori informazioni, vedere <a href="foreign-connectors-exchange-2013-help.md">Connettori esterni</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>MAILBOXRULE</strong></p></td>
<td><p>L'origine dell'evento era una regola di Posta in arrivo. Per ulteriori informazioni, vedere <a href="https://go.microsoft.com/fwlink/?linkid=285479">Regole di Posta in arrivo</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MEETINGMESSAGEPROCESSOR</strong></p></td>
<td><p>L'origine evento è il processore dei messaggi di riunione, che aggiorna i calendari in base agli aggiornamenti delle riunioni.</p></td>
</tr>
<tr class="even">
<td><p><strong>ORAR</strong></p></td>
<td><p>L'origine dell'evento era un ORAR (Originator Requested Alternate Recipient). È possibile abilitare o disabilitare il supporto di ORAR sui connettori di ricezione tramite il parametro <em>OrarEnabled</em> sui cmdlet <strong>New-ReceiveConnector</strong> o <strong>Set-ReceiveConnector</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PICKUP</strong></p></td>
<td><p>L'origine dell'evento era la directory di prelievo. Per ulteriori informazioni, vedere <a href="pickup-directory-and-replay-directory-exchange-2013-help.md">Directory di prelievo e directory di riesecuzione</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>L'origine dell'evento era l'identificativo messaggio non elaborabile. Per ulteriori informazioni sui messaggi non elaborabili e relativa coda, vedere <a href="queues-exchange-2013-help.md">Code</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PUBLICFOLDER</strong></p></td>
<td><p>L'origine dell'evento era la cartella pubblica abilitata alla posta.</p></td>
</tr>
<tr class="even">
<td><p><strong>QUEUE</strong></p></td>
<td><p>L'origine dell'evento era una coda.</p></td>
</tr>
<tr class="odd">
<td><p><strong>REDUNDANCY</strong></p></td>
<td><p>L'origine dell'evento era la ridondanza shadow. Per ulteriori informazioni, vedere <a href="shadow-redundancy-exchange-2013-help.md">Ridondanza shadow</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ROUTING</strong></p></td>
<td><p>L'origine dell'evento era il componente di risoluzione del routing del classificatore nel servizio di trasporto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SAFETYNET</strong></p></td>
<td><p>L'origine dell'evento era Rete sicura. Per ulteriori informazioni, vedere <a href="safety-net-exchange-2013-help.md">Rete sicura</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP</strong></p></td>
<td><p>Il messaggio è stato inviato dal componente di invio o ricezione SMTP del servizio di trasporto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>STOREDRIVER</strong></p></td>
<td><p>L'origine dell'evento era un invio MAPI da una cassetta postale sul server locale.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Voci di esempio nel registro di verifica messaggi

Un messaggio senza eventi inviato tra due utenti genera più voci nel registro di verifica messaggi. È possibile visualizzare i risultati utilizzando il cmdlet **Get-MessageTrackingLog**. Per ulteriori informazioni, vedere [Registri di verifica messaggi di ricerca](search-message-tracking-logs-exchange-2013-help.md).

Questo è un esempio limitato delle voci del registro di verifica messaggi creato quando l'utente chris@contoso.com invia un messaggio di prova all'utente michelle@contoso.com. Entrambi gli utenti hanno cassette postali sullo stesso server.

    EventId    Source      Sender            Recipients             MessageSubject
    -------    ------      ------            ----------             --------------
    NOTIFYMAPI STOREDRIVER                   {}
    RECEIVE    STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    SUBMIT     STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    HAREDIRECT SMTP        chris@contoso.com {michelle@contoso.com} test
    RECEIVE    SMTP        chris@contoso.com {michelle@contoso.com} test
    AGENTINFO  AGENT       chris@contoso.com {michelle@contoso.com} test
    SEND       SMTP        chris@contoso.com {michelle@contoso.com} test
    DELIVER    STOREDRIVER chris@contoso.com {michelle@contoso.com} test

Inizio pagina

## Problemi relativi alla protezione per il registro di verifica messaggi

Nel registro di verifica messaggi non viene archiviato alcun contenuto del messaggio. Per impostazione predefinita, la riga dell'oggetto di un messaggio di posta elettronica è archiviata nel registro di verifica messaggi. È possibile disabilitare la registrazione dell'oggetto dei messaggi per soddisfare requisiti di protezione o di privacy più rigidi. Prima di attivare o disattivvare la registrazione dell'oggetto dei messaggi, verificare i criteri dell'organizzazione relativi alla visualizzazione delle informazioni sull'oggetto Per ulteriori informazioni, vedere [Configurazione della verifica messaggi](configure-message-tracking-exchange-2013-help.md).

Inizio pagina


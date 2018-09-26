---
title: 'Registrazione agente di protezione da posta indesiderata: Exchange 2013 Help'
TOCTitle: Registrazione agente di protezione da posta indesiderata
ms:assetid: dbd478d2-7993-4931-80db-5b2f7d4269bd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124795(v=EXCHG.150)
ms:contentKeyID: 50481833
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registrazione agente di protezione da posta indesiderata

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Nei registri degli agenti vengono registrate le azioni eseguite su un messaggio da specifici agenti di protezione dalla posta indesiderata in Microsoft Exchange Server 2013. Solo i seguenti agenti possono scrivere informazioni nel registro dell'agente:

  - Agente filtro connessioni

  - Agente filtro contenuto

  - Agente regole Edge

  - Agente filtro destinatario

  - Agente filtro mittente

  - Agente ID mittente


> [!NOTE]
> L'agente filtro connessioni e l'agente regole Edge non sono disponibili nei server Cassette postali.



Le informazioni inserite nel registro dipendono dall'agente, dall'evento SMTP e dall'azione eseguita sul messaggio.

Utilizzare il cmdlet **Set-TransportService** in Exchange Management Shell per tutte le attività di configurazione del registro dell'agente. Sono disponibili le seguenti opzioni per i registri degli agenti:

  - Abilitazione o disabilitazione della registrazione degli agenti. L'impostazione predefinita è abilitata.

  - Indicazione del percorso dei file di registro degli agenti. Il valore predefinito è % ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog.

  - Indicazione della dimensione massima di ciascun file di registro dell'agente. Le dimensioni predefinite sono di 10 megabyte (MB).

  - Indicazione della dimensione massima della directory contenente i file di registro degli agenti. La dimensione predefinita è 250 MB.

  - Indicazione del limite massimo di validità dei file di registro degli agenti. La durata predefinita è 7 giorni.

Exchange utilizza la registrazione circolare per limitare i registri degli agenti in base alle dimensioni e al limite di validità dei file, al fine di controllare lo spazio su disco rigido utilizzato dai file di registro.

**Sommario**

Overview of transport agents

Structure of the agent log files

Information written to the agent log

Search the agent logs

## Informazioni generali sugli agenti di trasporto

Gli agenti possono agire sui messaggi solo in determinati punti della sequenza di comandi SMTP utilizzata per trasportare i messaggi attraverso un servizio di trasporto su un server Cassette postali o Trasporto Edge. Questi punti di accesso nella sequenza dei comandi SMTP sono denominati *eventi SMTP*. A ciascun agente può essere assegnato un valore relativo alla priorità. Tuttavia, gli eventi SMTP devono sempre verificarsi secondo un ordine specifico. Pertanto, la priorità di un agente dipende dall'evento SMTP. Difatti, se due agenti possono agire su un messaggio durante lo stesso evento SMTP, l'agente cui è stata assegnata la priorità più elevata agirà per primo.

Nella seguente tabella sono elencati gli eventi SMTP nell'ordine in cui si verificano. Per ciascun evento SMTP viene inoltre indicato quali agenti sono in grado di scrivere informazioni nel registro degli agenti in base alla priorità, dalla più alta alla più bassa.

### Eventi SMTP nell'ordine in cui si verificano e agenti in grado di scrivere informazioni nel registro degli agenti in base alla priorità per ciascun evento SMTP

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Evento SMTP</th>
<th>Agent</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>OnConnect</strong></p></td>
<td><p>Agente filtro connessioni</p></td>
</tr>
<tr class="even">
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>Agente filtro connessioni</p>
<p>Agente filtro mittente</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnRcptCommand</strong></p></td>
<td><p>Agente filtro connessioni</p>
<p>Agente Filtro destinatario</p></td>
</tr>
<tr class="even">
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>Agente filtro connessioni</p>
<p>Agente ID mittente</p>
<p>Agente filtro mittente</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>Agente regole Edge</p>
<p>Agente filtro contenuto</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> L'agente filtro connessioni e l'agente regole Edge non sono disponibili nei server Cassette postali.



Per ulteriori informazioni sugli agenti, sugli eventi SMTP e sulla priorità degli agenti, vedere [Agenti di trasporto](transport-agents-exchange-2013-help.md).

Inizio pagina

## Struttura dei file di registro degli agenti

Registri degli agenti presenti in % ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog.

La denominazione convenzionale per i file di registro degli agenti è AGENTLOG*aaaammgg-nnnn*.log. I segnaposto rappresentano le seguenti informazioni:

  - Il segnaposto *aaaammgg* rappresenta la data UTC (Coordinated Universal Time) di creazione del file di registro. *aaaa* = anno, *mm* = mese, *gg* = giorno.

  - Il segnaposto *nnnn* è un numero di istanza che inizia con il valore 1 per ciascun giorno.

Le informazioni vengono scritte nel file di registro finché le dimensioni del file raggiungono il valore massimo specificato, quindi viene aperto un nuovo file di registro con un numero di istanza maggiore. Questo processo si ripete per tutta la giornata. La registrazione circolare elimina i file di registro meno recenti quando la directory con i registri degli agenti raggiunge le dimensioni massime specificate oppure quando un file di registro raggiunge il limite massimo di validità specificato.

I file di registro degli agenti sono file di testo contenenti dati nel formato con valori delimitati da virgole (CSV). In ciascun file di registro degli agenti è presente un'intestazione in cui sono contenute le seguenti informazioni:

  - **\#Software**   Il nome del software con cui è stato creato il file di registro degli agenti. Generalmente, il valore è Microsoft Exchange Server.

  - **\#Versione**   Il numero di versione del software con cui è stato creato il file di registro degli agenti. Il valore corrente è 15.0.0.0.

  - **\#Log-Type**   Il valore del tipo di registro, in questo caso il registro degli agenti.

  - **\#Date**   Data/ora UTC in cui è stato creato il file di registro. La data/ora UTC viene rappresentata nel formato data/ora ISO 8601: *yyyy-mm-dd*T*hh:mm:ss.fff*Z, dove *yyyy* = anno, *mm* = mese, *dd* = giorno, T indica l'inizio della componente oraria, *hh* = ore, *mm* = minuti, *ss* = secondi, *fff* = frazioni di secondo e Z indica Zulu, un altro modo per denominare UTC.

  - **\#Fields**   I nomi dei campi, delimitati da virgole, utilizzati nei file di registro degli agenti.

Inizio pagina

## Informazioni scritte nel registro degli agenti

Nel registro degli agenti ciascuna transazione eseguita dall'agente viene archiviata su un'unica riga. Le informazioni archiviate su ciascuna riga sono organizzate per campi. Questi campi sono separati da virgole. Il nome del campo in genere è abbastanza descrittivo da consentire di determinare il tipo di informazione contenuta. Alcuni campi, tuttavia, potrebbero risultare vuoti, oppure il tipo di informazione archiviata nel campo può variare in base all'agente o all'azione eseguita dall'agente sul messaggio. Nella seguente tabella sono descritti i campi utilizzati per classificare ciascuna transazione degli agenti.

### Campi utilizzati per classificare ogni transazione degli agenti

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome del campo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Timestamp</strong></p></td>
<td><p>Data e ora UTC dell'evento dell'agente. La data/ora UTC viene rappresentata nel formato data/ora ISO 8601: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, dove <em>yyyy</em> = anno, <em>mm</em> = mese, <em>dd</em> = giorno, T indica l'inizio della componente oraria, <em>hh</em> = ore, <em>mm</em> = minuti, <em>ss</em> = secondi, <em>fff</em> = frazioni di secondo e Z indica Zulu, un altro modo per denominare UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionId</strong></p></td>
<td><p>Identificatore univoco della sessione SMTP. È rappresentato come numero esadecimale di 16 cifre.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalEndpoint</strong></p></td>
<td><p>Indirizzo IP locale e numero della porta che ha accettato il messaggio. Le sessioni SMTP utilizzano in genere la porta 25.</p></td>
</tr>
<tr class="even">
<td><p><strong>RemoteEndpoint</strong></p></td>
<td><p>Indirizzo IP e numero della porta del server SMTP precedente che ha eseguito la connessione al server corrente per il recapito del messaggio. Quando la posta Internet circola in un server Trasporto Edge nella rete perimetrale, il valore di <strong>RemoteEndpoint</strong> nel registro dell'agente sul server Cassette postali sarà l'indirizzo IP del server Trasporto Edge. Pertanto, anche se il messaggio viene trasmesso tramite SMTP, il numero della porta utilizzata dal server di invio sarà un numero casuale superiore a 1.024.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnteredOrgFromIP</strong></p></td>
<td><p>Indirizzo IP del server SMTP remoto che ha eseguito la connessione iniziale all'organizzazione di Exchange per il recapito del messaggio. Sul server Trasporto Edge i valori dei campi <strong>RemoteEndpoint</strong> ed <strong>EnteredOrgFromIP</strong> sono identici. Gli agenti di protezione dalla posta indesiderata utilizzano l'indirizzo IP del campo <strong>EnteredOrgFromIP</strong> per esaminare un messaggio.</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageId</strong></p></td>
<td><p>Valore del campo di intestazione <code>MessageID</code>. Se il campo viene lasciato vuoto e il messaggio viene accettato, il server di trasporto Exchange assegna un valore arbitrario. Una volta assegnato, il valore del campo <code>MessageID</code> rimane immutato per tutta la durata del messaggio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>P1FromAddress</strong></p></td>
<td><p>Indirizzo di posta elettronica del mittente specificato nel campo <code>MAIL FROM</code> nella busta del messaggio. Questo valore viene utilizzato per trasportare il messaggio tra i server di messaggistica SMTP. Viene inoltre confrontato con il valore del campo <strong>P2FromAddresses</strong> per determinare se l'indirizzo del mittente nell'intestazione del messaggio è stato contraffatto.</p></td>
</tr>
<tr class="even">
<td><p><strong>P2FromAddresses</strong></p></td>
<td><p>L'indirizzo di posta elettronica del mittente specificato nel campo di intestazione <code>From</code> o nel campo di intestazione <code>Sender</code> nell'intestazione del messaggio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Recipient</strong></p></td>
<td><p>Indirizzo di posta elettronica dei destinatari. Sebbene il messaggio originale possa contenere più destinatari, su ogni riga del registro degli agenti viene visualizzato un solo destinatario.</p></td>
</tr>
<tr class="even">
<td><p><strong>NumRecipients</strong></p></td>
<td><p>Numero totale di destinatari del messaggio originale.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agent</strong></p></td>
<td><p>Nome dell'agente che richiama l'azione. I valori possibili sono:</p>
<ul>
<li><p>Agente filtro contenuto</p></li>
<li><p>Agente Filtro destinatario</p></li>
<li><p>Agente filtro mittente</p></li>
<li><p>Agente ID mittente</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Event</strong></p></td>
<td><p>Evento SMTP in cui l'agente ha eseguito l'azione. Il valore del campo <strong>Event</strong> dipende dall'agente. Gli eventi SMTP disponibili per ciascun agente sono descritti nella prima tabella riportata in precedenza in questo argomento. I valori possibili del campo <strong>Event</strong> sono elencati di seguito:</p>
<ul>
<li><p>OnConnect</p></li>
<li><p>OnEndOfHeaders</p></li>
<li><p>OnEndOfData</p></li>
<li><p>OnMailCommand</p></li>
<li><p>OnRcptCommand</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Action</strong></p></td>
<td><p>Azione eseguita dall'agente sul messaggio. I valori possibili del campo <strong>Action</strong> sono riportati di seguito:</p>
<ul>
<li><p>AcceptMessage</p></li>
<li><p>DeleteMessage</p></li>
<li><p>DeleteRecipients</p></li>
<li><p>Disconnect</p></li>
<li><p>QuarantineMessage</p></li>
<li><p>QuarantineRecipients</p></li>
<li><p>RejectAuthentication</p></li>
<li><p>RejectCommand</p></li>
<li><p>RejectConnection</p></li>
<li><p>RejectMessage</p></li>
<li><p>RejectRecipients</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>SmtpResponse</strong></p></td>
<td><p>Risposta ESMTP (Enhanced SMTP) come definita in RFC 2034.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reason</strong></p></td>
<td><p>Motivo dell'azione fornita dall'agente.</p></td>
</tr>
<tr class="even">
<td><p><strong>ReasonData</strong></p></td>
<td><p>Dettagli descrittivi per l'azione fornita dall'agente.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Ricerca nei registri degli agenti

È possibile utilizzare il cmdlet **Get-AgentLog** e lo script **Get-AntiSpamFilteringReport.ps1** per eseguire ricerche nei registri dell'agente.

Lo script **Get-AntiSpamFilteringReport.ps1** si trova in `%ExchangeInstallPath%Scripts`. È necessario eseguire lo script in Shell dalla cartella Script. Per accedere alla cartella Script di Shell, utilizzare il seguente comando:

```powershell
Cd $env:ExchangeInstallPath\Scripts
```

Per eseguire lo script nella cartella Script, utilizzare la seguente sintassi:
```powershell
    .\Get-AntiSpamFilteringReport.ps1 -report <ReportValue> [<OptionalParameters>]
```

Per i dettagli sull'uso dello script, utilizzare il seguente comando:

```powershell
Get-Help -Detailed .\Get-AntiSpamFilteringReport.ps1
```

Inizio pagina


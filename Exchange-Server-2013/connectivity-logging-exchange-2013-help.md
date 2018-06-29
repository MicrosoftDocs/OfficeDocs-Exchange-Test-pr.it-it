---
title: 'Registrazione di integrazione applicativa: Exchange 2013 Help'
TOCTitle: Registrazione di integrazione applicativa
ms:assetid: c31fd710-4ae4-4d9a-8936-d056e7ca2748
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124500(v=EXCHG.150)
ms:contentKeyID: 50481598
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registrazione di integrazione applicativa

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

La registrazione della connettività registra l'attività di connessione in uscita utilizzata per trasmettere i messaggi da un servizio di trasporto sul server Exchange. Lo scopo del registro di connettività non è quello di verificare la trasmissione dei singoli messaggi di posta elettronica, bensì di verificare l'attività di connessione dall'origine alla destinazione indipendentemente dalla quantità di messaggi trasmessi. La registrazione della connettività è disponibile nel servizio di trasporto front-end dei server Accesso client, nel servizio di trasporto dei server Cassette postali e nel servizio di trasporto delle cassette postali nei server Cassette postali. Nel seguente elenco vengono descritti i tipi di informazioni registrati nel registro di connettività:

  - Origine

  - Destination

  - Informazioni sulla risoluzione DNS

  - Informazioni dettagliate sugli errori di connessione

  - Numero di messaggi e byte trasmessi

Utilizzare i cmdlet **Set-TransportService**, **Set-FrontEndTransportService** e **Set-MailboxTransportService** in Exchange Management Shell per eseguire tutte le attività di configurazione del registro di connettività. Per i registri di connettività sono disponibili le opzioni seguenti:

  - Abilitare o disabilitare la registrazione della connettività. L'impostazione predefinita è abilitata.

  - Specificare il percorso dei file di registro di connettività.

  - Specificare la dimensione massima di ciascun file di registro di connettività. La dimensione predefinita è 10 MB.

  - Specificare la dimensione massima della directory contenente i file di registro di connettività. La dimensione predefinita è 1.000 MB.

  - Specificare il limite massimo di validità dei file di registro di connettività. Il limite predefinito è 30 giorni.

Per impostazione predefinita, Exchange utilizza la registrazione circolare per limitare i registri di connettività in base alle dimensioni e al limite di validità dei file al fine di controllare lo spazio su disco rigido utilizzato dai file di registro di connettività.

**Sommario**

Structure of the connectivity log files

Information written to the connectivity log

## Struttura dei file di registro di connettività

Per impostazione predefinita, i file di registro di connettività si trovano nelle seguenti posizioni:

  - **Transport service** %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\Connectivity

  - **Front End Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\Connectivity

  - **Mailbox Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\Connectivity

La denominazione convenzionale per i file di registro di connettività è CONNECTLOG*aaaammgg-nnnn*.log. I segnaposto rappresentano le seguenti informazioni:

  - Il segnaposto *aaaammgg* rappresenta la data UTC (Coordinated Universal Time) di creazione del file di registro. *aaaa* = anno, *mm* = mese, *gg* = giorno.

  - Il segnaposto *nnnn* è un numero di istanza che inizia con il valore 1 per ciascun giorno.

Le informazioni vengono scritte nel file di registro finché le dimensioni del file non raggiungono il valore massimo specificato, quindi viene aperto un nuovo file di registro con un numero di istanza maggiore. Questo processo si ripete per tutta la giornata. La registrazione circolare rileva i file di registro più vecchi quando la directory del registro di connettività raggiunge le dimensioni massime specificate oppure quando un file di registro raggiunge il limite di validità specificato.

I file di registro di connettività sono file di testo contenenti dati nel formato con valori delimitati da virgole (CSV). In ciascun file di registro di connettività è presente un'intestazione contenente le seguenti informazioni:

  - **\#Software**   Il nome del software con cui è stato creato il file di registro di connettività. Generalmente, il valore è Microsoft Exchange Server.

  - **\#Versione**   Il numero di versione del software con cui è stato creato il file di registro di connettività. Il valore corrente è 15.0.0.0.

  - **\#Log-Type**   Il valore del tipo di registro, in questo caso il registro di connettività di trasporto.

  - **\#Date**   Data/ora UTC in cui è stato creato il file di registro. La data/ora UTC viene rappresentata nel formato data/ora ISO 8601: *yyyy-mm-dd*T*hh:mm:ss.fff*Z, dove *yyyy* = anno, *mm* = mese, *dd* = giorno, T indica l'inizio della componente oraria, *hh* = ore, *mm* = minuti, *ss* = secondi, *fff* = frazioni di secondo e Z indica Zulu, un altro modo per denominare UTC.

  - **\#Fields**   I nomi dei campi, delimitati da virgole, utilizzati nei file di registro di connettività.

Inizio pagina

## Informazioni scritte nel registro di connettività

Nel registro di connettività, i singoli eventi di connessione del servizio di trasporto in uscita vengono memorizzati su una singola riga del registro. Le informazioni archiviate su ciascuna riga sono organizzate per campi. Questi campi sono separati da virgole. Nella seguente tabella sono descritti i campi utilizzati per classificare ciascun evento di connettività in uscita.

### Campi utilizzati per classificare ogni evento di connessione

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
<td><p><strong>date-time</strong></p></td>
<td><p>Data e ora UTC dell'evento di connessione. La data/ora UTC viene rappresentata nel formato data/ora ISO 8601: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, dove <em>yyyy</em> = anno, <em>mm</em> = mese, <em>dd</em> = giorno, T indica l'inizio della componente oraria, <em>hh</em> = ore, <em>mm</em> = minuti, <em>ss</em> = secondi, <em>fff</em> = frazioni di secondo e Z indica Zulu, un altro modo per denominare UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>session</strong></p></td>
<td><p>Un GUID univoco per ciascuna sessione SMTP, ma identico per ciascun evento associato alla stessa sessione SMTP. Per le sessioni MAPI nel servizio Trasporto delle cassette postali il campo della sessione è vuoto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>source</strong></p></td>
<td><p><strong>SMTP</strong> per connessioni SMTP, <strong>MAPI</strong> per connessioni del servizio Trasporto delle cassette postali al database di cassette postali locale.</p></td>
</tr>
<tr class="even">
<td><p><strong>destination</strong></p></td>
<td><p>Nome della destinazione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>direction</strong></p></td>
<td><p>Un singolo carattere che rappresenta il momento iniziale, centrale e finale della connessione. Di seguito sono riportati i valori possibili per il campo direction:</p>
<ul>
<li><p><strong>+</strong>   Connessione</p></li>
<li><p><strong>-</strong>   Disconnessione</p></li>
<li><p><strong>&gt;</strong>   Invio</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>description</strong></p></td>
<td><p>Informazioni di testo associate all'evento di connessione. Di seguito sono riportati valori di esempio per il campo description:</p>
<ul>
<li><p>Il numero e la dimensione dei messaggi trasmessi</p></li>
<li><p>Informazioni sulla risoluzione del record della risorsa MX DNS per i domini di destinazione</p></li>
<li><p>Informazioni sulla risoluzione DNS per i server di cassette postali di destinazione</p></li>
<li><p>Messaggi di definizione della connessione</p></li>
<li><p>Messaggi di errore di connessione</p></li>
</ul></td>
</tr>
</tbody>
</table>


Quando il servizio di trasporto stabilisce una connessione a una destinazione, può essere preparato all'invio di uno o più messaggi. I processi di connessione e di trasmissione dei messaggi generano svariati eventi scritti su più righe nel registro di connettività. Connessioni simultanee a diverse destinazioni generano voci del registro di connettività correlate alle diverse destinazioni collegate. È tuttavia possibile utilizzare i campi date-time, session, source e direction per organizzare le voci del registro di connettività per ciascuna connessione distinta dall'inizio alla fine.

Inizio pagina


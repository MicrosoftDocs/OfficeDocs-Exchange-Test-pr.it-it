---
title: 'Registrazione del protocollo: Exchange 2013 Help'
TOCTitle: Registrazione del protocollo
ms:assetid: 40da446b-bcc3-4a97-ace7-a54f6ddebd79
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997624(v=EXCHG.150)
ms:contentKeyID: 50480457
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registrazione del protocollo

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

La registrazione protocollo registra le conversazioni SMTP tra i server di messaggistica come parte del recapito di un messaggio. Queste conversazioni SMTP avvengono sui connettori di invio e sui connettori di ricezione esistenti sul servizio di trasporto Front End sui server Accesso client e sul servizio Trasporto sui server Cassette postali. È possibile utilizzare la registrazione del protocollo per individuare eventuali problemi relativi al flusso di posta.

Per impostazione predefinita, la registrazione del protocollo è disabilitata su tutti i connettori di invio e di ricezione. La registrazione del protocollo viene abilitata o disabilitata su ciascun connettore. Le altre opzioni di registrazione protocollo sono impostate per tutti i connettori di ricezione e connettori di invio presenti in ciascun servizio trasporto individuale sul server. Tutti i connettori di ricezione in un servizio di trasporto condividono gli stessi file di registro del protocollo e opzioni di registro del protocollo. Tali file di registro del protocollo e opzioni di registro del protocollo sono diversi dai file di registro del protocollo e dalle opzioni di registro del protocollo dei connettori di invio nel servizio trasporto sullo stesso server.

Le seguenti opzioni sono disponibili per i registri del protocollo di tutti i connettori di invio o di tutti i connettori di ricezione in ciascun servizio trasporto o in un server Exchange:

  - Specificare la posizione dei file di registro del protocollo del connettore di invio o del connettore di ricezione.

  - Specificare la dimensione massima dei file di registro del protocollo del connettore di invio o del connettore di ricezione. Le dimensioni predefinite sono di 10 megabyte (MB).

  - Specificare la dimensione massima della directory che contiene i file di registro del protocollo del connettore di invio o del connettore di ricezione. La dimensione predefinita è 250 MB.

  - Specificare la durata massima dei file di registro del protocollo del connettore di invio o del connettore di ricezione. La durata predefinita è 30 giorni.

Per impostazione predefinita, Exchange utilizza la registrazione circolare per limitare i registri del protocollo in base alle dimensioni dei file e alla validità dei file in modo da controllare lo spazio su disco rigido utilizzato dai file di registro.

Uno speciale connettore di invio denominato connettore di invio tra organizzazioni è presente nel servizio di trasporto di tutti i server cassette postali e nel servizio trasporto front-end di ciascun server Accesso client. Tale connettore viene creato implicitamente, è invisibile e non richiede alcuna gestione. Il connettore di invio tra organizzazioni è utilizzato dai seguenti servizi di trasporto:

  - **Servizio Trasporto sui server Cassette postali**
    
      - Invio di messaggi al servizio di trasporto e il servizio trasporto cassette postali su altri server cassette postali Exchange 2013 nell'organizzazione.
    
      - Invio di messaggi ad altri server Trasporto Hub Exchange 2007 o Exchange 2010 nell'organizzazione.
    
      - Invio di messaggi ai server Trasporto Edge nella rete perimetrale.

  - **Servizio Trasporto front-end sui server Accesso client**   Invio di messaggi al servizio trasporto sui server cassette postali Exchange 2013 nell'organizzazione.

Un equivalente connettore di invio denominato connettore di invio per il recapito alle cassette postali è presente nel servizio Trasporto cassette postali su ciascun server cassette postali. Tale connettore viene creato implicitamente, è invisibile e non richiede alcuna gestione. Il connettore di invio per il recapito alle cassette postali viene utilizzato per l'invio di messaggi al servizio trasporto e al servizio trasporto cassetta postale su altri server cassette postali nell'organizzazione.

Per impostazione predefinita, la registrazione protocollo per il connettore di invio per il recapito alle cassette postali è disabilitata. È possibile abilitare o disabilitare la registrazione protocollo per il connettore di invio per il recapito alle cassette postali utilizzando il parametro *MailboxDeliveryConnectorProtocolLoggingLevel* del cmdlet **Set-MailboxTransportService**. Se si abilita la registrazione del protocollo per il connettore di invio per il recapito alle cassette postali, la registrazione avviene nei registri di protocollo del servizio Trasporto cassette postali sul server cassette postali.

**Sommario**

Structure of the protocol log files

Information written to the protocol log

## Struttura dei file di registro del protocollo

Per impostazione predefinita, i file di registro del protocollo si trovano nelle seguenti posizioni:

  - **File di registro del protocollo del connettore di ricezione per il servizio trasporto sui server cassette postali**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpReceive

  - **File di registro del protocollo del connettore di ricezione per il servizio trasporto cassette postali sui server cassette postali**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpReceive

  - **File di registro del protocollo del connettore di ricezione per il servizio trasporto front-end sui server Accesso client**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpReceive

  - **File di registro del protocollo del connettore di invio per il servizio trasporto sui server cassette postali**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpSend

  - **File di registro del protocollo del connettore di invio per il servizio trasporto cassette postali sui server cassette postali**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpSend

  - **File di registro del protocollo del connettore di ricezione per il servizio trasporto front-end sui server Accesso client**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpSend

La convenzione di denominazione per i file di registro in ciascuna directory del registro del protocollo è *prefissoaaaammgg-nnnn*.log. I segnaposto rappresentano le seguenti informazioni:

  - Il segnaposto *prefisso* è SEND per i connettori di invio o RECV per i connettori di ricezione.

  - Il segnaposto *aaaammgg* indica la data UTC (Coordinated Universal Time) in cui è stato creato il file di registro. Il segnaposto *aaaa* = anno, *mm* = mese e *gg* = giorno.

  - Il segnaposto *nnnn* è un numero di istanza che inizia con il valore 1 per ciascun giorno.

Le informazioni vengono scritte nel file di registro finché le dimensioni del file raggiungono il valore massimo specificato, quindi viene aperto un nuovo file di registro con un numero di istanza maggiore. Questo processo si ripete per tutta la giornata. La registrazione circolare rileva i file di registro più vecchi quando la directory del registro del protocollo raggiunge le dimensioni massime specificate oppure quando un file di registro raggiunge la durata massima specificata.

I file di registro protocollo sono file di testo contenenti dati nel formato file con valori delimitati da virgole (CSV). In ciascun file di registro del protocollo è presente un'intestazione in cui sono contenute le seguenti informazioni:

  - **\#Software:**   Nome del software con cui è stato creato il file di registro protocollo. Generalmente, il valore è Microsoft Exchange Server.

  - **\#Version**   Numero della versione del software con cui è stato creato il file di registro protocollo. Il valore corrente è 15.0.0.0.

  - **\#Log-Type**   Il valore di questo campo indica il registro protocollo di ricezione e di invio SMTP.

  - **\#Date**   Data/ora UTC in cui è stato creato il file di registro. La data/ora UTC viene rappresentata nel formato data/ora ISO 8601: *yyyy-mm-dd*T*hh:mm:ss.fff*Z, dove *yyyy* = anno, *mm* = mese, *dd* = giorno, T indica l'inizio della componente oraria, *hh* = ore, *mm* = minuti, *ss* = secondi, *fff* = frazioni di secondo e Z indica Zulu, un altro modo per denominare UTC.

  - **\#Fields**   Nomi dei campi delimitati da virgole utilizzati nei file di registro protocollo.

Inizio pagina

## Informazioni scritte nel registro del protocollo

Nel registro del protocollo vengono memorizzati i singoli eventi del protocollo SMTP in una sola riga. Le informazioni archiviate in ogni riga sono organizzate per campi. Questi campi sono separati da virgole. Nella seguente tabella vengono descritti i campi utilizzati per classificare ogni protocollo.

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
<td><p><strong>date-time</strong></p></td>
<td><p>Data e ora UTC dell'evento del protocollo. La data/ora UTC viene rappresentata nel formato data/ora ISO 8601: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, dove <em>yyyy</em> = anno, <em>mm</em> = mese, <em>dd</em> = giorno, T indica l'inizio della componente oraria, <em>hh</em> = ore, <em>mm</em> = minuti, <em>ss</em> = secondi, <em>fff</em> = frazioni di secondo e Z indica Zulu, un altro modo per denominare UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>connector-id</strong></p></td>
<td><p>Nome distinto del connettore associato all'evento SMTP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>session-id</strong></p></td>
<td><p>GUID univoco per ogni sessione SMTP, ma è lo stesso per ogni evento associato a quella sessione SMTP.</p></td>
</tr>
<tr class="even">
<td><p><strong>sequence-number</strong></p></td>
<td><p>Contatore che inizia da 0 e viene incrementato per ogni evento della stessa sessione SMTP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>local-endpoint</strong></p></td>
<td><p>Endpoint locale di una sessione SMTP. È composto da un indirizzo IP e un numero di porta TCP formattato come <em>&lt;indirizzo IP&gt;</em>:<em>&lt;porta&gt;</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>remote-endpoint</strong></p></td>
<td><p>Endpoint remoto di una sessione SMTP. È composto da un indirizzo IP e un numero di porta TCP formattato come <em>&lt;indirizzo IP&gt;</em>:<em>&lt;porta&gt;</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>event</strong></p></td>
<td><p>Carattere unico che rappresenta l'evento protocollo. Di seguito sono riportati i valori possibili per l'evento:</p>
<ul>
<li><p><strong>+</strong>   Connessione</p></li>
<li><p><strong>-</strong>   Disconnessione</p></li>
<li><p><strong>&gt;</strong>   Send</p></li>
<li><p><strong>&lt;</strong>   Receive</p></li>
<li><p><strong>*</strong>   Informazioni</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>data</strong></p></td>
<td><p>Informazioni di testo associate all'evento SMTP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>context</strong></p></td>
<td><p>Informazioni aggiuntive sul contesto che possono essere associate all'evento SMTP.</p></td>
</tr>
</tbody>
</table>


Una singola conversazione SMTP che rappresenta l'invio o la ricezione di un singolo messaggio di posta elettronica che genera più eventi SMTP. Questi eventi SMTP causano la scrittura di più righe nel registro del protocollo. Possono verificarsi più conversazioni SMTP che rappresentano l'invio o la ricezione di più messaggi di posta elettronica contemporaneamente. In tal modo vengono create voci del registro del protocollo da diverse conversazioni SMTP interconnesse. È possibile utilizzare i campi ID di sessione e numero di sequenza per ordinare le voci del registro protocollo in base alla conversazione SMTP.

Inizio pagina


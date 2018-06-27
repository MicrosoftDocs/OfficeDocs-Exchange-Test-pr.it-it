---
title: 'Agenti di trasporto: Exchange 2013 Help'
TOCTitle: Agenti di trasporto
ms:assetid: e7389d63-3172-40d5-bf53-0d7cd7e78340
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125012(v=EXCHG.150)
ms:contentKeyID: 50481959
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agenti di trasporto

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Gli agenti di trasporto è possibile installare il software personalizzato creati da Microsoft, fornitori di terze parti o dell'organizzazione, in un server Exchange. Questo software può elaborare i messaggi di posta elettronica che passano attraverso la pipeline di trasporto. In Microsoft Exchange Server 2013, la pipeline di trasporto comprende i processi seguenti:

  - Il servizio trasporto Front-End sui server Accesso Client

  - Il servizio di trasporto sui server cassette postali

  - Il servizio di trasporto delle cassette postali sui server cassette postali

  - Il servizio di trasporto nei server Trasporto Edge

Per ulteriori informazioni sulla pipeline di trasporto, vedere [Flusso di posta](mail-flow-exchange-2013-help.md)

Analogamente alla versione precedente di Exchange, trasporto Exchange 2013 fornisce estensibilità tramite Microsoft Exchange Server 2013 di SDK di agenti di trasporto. La versione Exchange 2013 del SDK è in base alla Microsoft.NET Framework versione 4.0 e consente a terze parti implementare le classi predefinite seguenti:

  - **SmtpReceiveAgent**

  - **RoutingAgent**

  - **DeliveryAgent**

Durante la conformità con le raccolte in SDK, vengono registrati gli assembly risultanti con Exchange 2013, che viene caricato gli agenti e richiama i gestori eventi durante le fasi specifiche del sessioni SMTP o elaborazione dei messaggi. Queste fasi o eventi, fanno parte delle definizioni di agenti. Le informazioni di registrazione agente viene archiviate in un file di configurazione XML.

Nell'elenco seguente sono descritti i requisiti per l'utilizzo di agenti di trasporto in Exchange 2013.

  - Servizio di trasporto sul server cassette postali e Trasporto Edge supporta completamente tutte le classi predefinite in SDK e pertanto le terze parti gli agenti di trasporto scritti per il server Trasporto Hub o Trasporto Edge ruoli in Microsoft Exchange Server 2010 dovrebbero funzionare nel servizio di trasporto in Exchange 2013.

  - Il servizio trasporto Front-End supporta solo la classe **SmtpReceiveAgent** in SDK e gli agenti di terze parti non è possibile utilizzare l'evento **OnEndOfData** SMTP.

  - Il servizio trasporto cassette postali non supporta il SDK, in modo che non è possibile utilizzare gli agenti di terze parti nel servizio trasporto cassette postali.

Supporto per gli agenti di trasporto legacy basato sulle versioni di .NET Framework precedenti alla versione 4.0 non è abilitato per impostazione predefinita, ma è possibile attivarlo. Per ulteriori informazioni, vedere [Attivare il supporto per gli agenti di trasporto legacy](enable-support-for-legacy-transport-agents-exchange-2013-help.md).

**Sommario**

Aggiornamenti per la gestione dell'agente di trasporto

Gli agenti di trasporto e gli eventi SMTP

Priorità di agenti di trasporto

Agenti di trasporto incorporati

Risoluzione dei problemi di agenti di trasporto

## Aggiornamenti per la gestione dell'agente di trasporto

Per gli aggiornamenti per la pipeline di trasporto Exchange 2013, il cmdlet dell'agente di trasporto devono poter distinguere tra il servizio di trasporto e il servizio trasporto Front-End, soprattutto se il server Accesso Client e il server cassette postali sono installati nello stesso computer. Per ulteriori informazioni, vedere [Gestire gli agenti di trasporto](manage-transport-agents-exchange-2013-help.md).

Cmdlet di gestione dell'agente di trasporto modificare un file di configurazione in `%ExchangeInstallPath%TransportRoles\Shared`. Per il servizio di trasporto sul server cassette postali e Trasporto Edge, il file è `agents.config`. Per il servizio trasporto Front-End sui server Accesso Client, il file è `fetagents.config`. Entrambi i file di utilizzano lo stesso formato di Exchange 2010. Per ulteriori informazioni sulla gestione degli agenti di trasporto, vedere [Gestire gli agenti di trasporto](manage-transport-agents-exchange-2013-help.md).

Inizio pagina

## Gli agenti di trasporto e gli eventi SMTP

Eventi SMTP utilizzata dagli agenti di trasporto. Questi eventi vengono attivati i messaggi lo spostamento attraverso la pipeline di trasporto. Eventi SMTP concedere gli agenti di trasporto di accesso ai messaggi in punti specifici durante la conversazione SMTP e il routing dei messaggi all'interno dell'organizzazione.

Si noti che non vi siano nuovi eventi di ricezione SMTP in Exchange 2013. Ricezione SMTP è presente nel servizio di trasporto Front-End sul server Accesso Client, il servizio di trasporto sul server cassette postali e Trasporto Edge e il servizio di recapito di trasporto delle cassette postali sui server cassette postali. Classificatore è presente solo nel servizio di trasporto sul server cassette postali e Trasporto Edge. Per ulteriori informazioni sui servizi di trasporto e classificatore, vedere [Routing della posta](mail-routing-exchange-2013-help.md).

Nelle tabelle seguenti sono elencano gli eventi SMTP che consentono di accedere ai messaggi nella pipeline di trasporto.

### Eventi di ricezione SMTP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Sequenza</th>
<th>Evento SMTP</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong></p></td>
<td><p>Questo evento viene attivato per la connessione di un host SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnHeloCommand</strong></p></td>
<td><p>Questo evento viene generato quando viene eseguito il comando <code>HELO</code> da parte dell'host SMTP remoto.</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnEhloCommand</strong></p></td>
<td><p>Questo evento viene generato quando viene eseguito il comando <code>EHLO</code> da parte dell'host SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnStartTlsCommand</strong></p></td>
<td><p>Questo evento viene generato quando viene eseguito il comando <code>STARTTLS</code> da parte dell'host SMTP remoto.</p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p><strong>OnAuthCommand</strong></p></td>
<td><p>Questo evento viene generato quando viene eseguito il comando <code>AUTH</code> da parte dell'host SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>6</p></td>
<td><p><strong>OnProcessAuthentication</strong></p></td>
<td><p>Questo evento viene generato quando viene elaborato l'autenticazione con l'host SMTP remoto.</p></td>
</tr>
<tr class="odd">
<td><p>7</p></td>
<td><p><strong>OnEndOfAuthentication</strong></p></td>
<td><p>Questo evento viene generato quando l'host SMTP remoto ha completato l'autenticazione.</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p><strong>OnXSessionParamsCommand</strong></p></td>
<td><p>Questo evento viene generato quando viene eseguito il comando <code>XSESSIONPARAMS</code> da parte dell'host SMTP remoto.</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>Questo evento viene generato quando viene eseguito il comando <code>MAIL FROM</code> da parte dell'host SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p><strong>OnRcptToCommand</strong></p></td>
<td><p>Questo evento viene generato quando viene eseguito il comando <code>RCPT TO</code> da parte dell'host SMTP remoto.</p></td>
</tr>
<tr class="odd">
<td><p>11</p></td>
<td><p><strong>OnDataCommand</strong></p></td>
<td><p>Questo evento viene generato quando la <code>DATA</code> (testo) o il comando <code>BDAT</code> (dati binari) emesso da parte dell'host SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>Questo evento viene generato quando l'host SMTP remoto ha completato l'invio di intestazioni dei messaggi di posta elettronica. Viene indicato da una riga vuota (<code>&lt;CRLF&gt;</code>) che separa le intestazioni dei messaggi e il corpo del messaggio.</p></td>
</tr>
<tr class="odd">
<td><p>13</p></td>
<td><p><strong>OnProxyInboundMessage</strong></p></td>
<td><p>Questo evento viene generato quando viene inoltrata una sessione SMTP in ingresso o <em>elaborati</em> dal servizio trasporto Front-End in un server Accesso Client al servizio di trasporto in un server cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>Questo evento viene generato quando l'host SMTP remoto emette una fine del comando dati. Per le sessioni di testo avviate dal comando <code>DATA</code> , la fine dell'indicatore di dati è <code>&lt;CRLF&gt;.&lt;CRLF&gt;</code>. Per le sessioni binarie avviate dal comando <code>BDAT</code> , la fine dell'indicatore di dati è <code>BDAT LAST</code>.</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnHelpCommand</strong></p></td>
<td><p>Questo evento viene generato se il comando <code>HELP</code> da parte dell'host SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnNoopCommand</strong></p></td>
<td><p>Questo evento viene generato se il comando <code>NOOP</code> da parte dell'host SMTP remoto.</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnReject</strong></p></td>
<td><p>Questo evento viene generato se l'host SMTP destinatario viene generato un codice di notifica (DSN) lo stato di recapito temporaneo o permanente all'host SMTP mittente.</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnRsetCommand</strong></p></td>
<td><p>Questo evento viene generato se il comando <code>RSET</code> per l'host SMTP mittente.</p></td>
</tr>
<tr class="odd">
<td><p>15</p></td>
<td><p><strong>OnDisconnectEvent</strong></p></td>
<td><p>Questo evento viene attivato per la disconnessione della conversazione SMTP per la ricezione o l'invio di host SMTP. In genere, ciò si verifica quando viene eseguito il comando <code>QUIT</code> da parte dell'host SMTP remoto.</p></td>
</tr>
</tbody>
</table>


\* \* Questi eventi possono verificarsi in qualsiasi momento dopo **OnConnectEvent** , ma prima **OnDisconnectEvent**.

### Eventi classificatore

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Sequenza</th>
<th>Evento classificatore</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
<td><p>Questo evento viene generato quando si riceve un messaggio nella coda di invio nel servizio di trasporto nel server cassette postali ricevente o nel server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
<td><p>Questo evento viene generato dopo che tutti i destinatari sono stati risolti, ma prima di quello successivo hop è stato determinato per ciascun destinatario. L'evento di routing <strong>OnResolvedMessage</strong> consente gli eventi successivi per ignorare il comportamento predefinito utilizzando il metodo per destinatario <strong>SetRoutingOverride</strong> .</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
<td><p>Questo evento viene generato dopo che i messaggi sono stati classificati, liste di distribuzione sono state estese e i destinatari sono stati risolti.</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
<td><p>Questo evento viene generato al termine dell'elaborazione del messaggio classificatore.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Priorità di agenti di trasporto

Esistono due fattori che determinano l'ordine in cui gli agenti di trasporto agiscono sui messaggi nella pipeline di trasporto:

1.  L'evento SMTP in cui è registrato l'agente di trasporto, e quando tale evento SMTP rileva i messaggi.

2.  Il valore della priorità assegnato all'agente di trasporto se sono presenti più agenti registrato per l'evento SMTP stesso. La priorità più alta è 1. Un valore intero maggiore indica una priorità più bassa agente.

Si supponga, ad esempio, che è stato configurato gli agenti di trasporto seguenti:

  - Agente di trasporto A con priorità 1 e C agente di trasporto con priorità 2 viene registrato per l'evento SMTP **OnEndOfHeaders** .

  - B agente di trasporto con priorità 4 viene registrato per l'evento SMTP **OnMailCommand** .

B agente di trasporto viene applicata ai messaggi prima perché l'evento **OnMailCommand** rileva i messaggi prima dell'evento **OnEndOfHeaders** . Quando i messaggi di raggiungano l'evento **OnEndOfHeaders** , dell'agente di trasporto A viene applicato prima C agente di trasporto in quanto l'agente di trasporto A ha priorità maggiore di (valore intero inferiore) C. agente di trasporto

## Agenti di trasporto incorporati

Exchange 2013 include molti agenti di trasporto incorporati che forniscono funzionalità di protezione da posta indesiderata, le regole di trasporto e l'inserimento nel journal. La maggior parte degli agenti di trasporto sul server Accesso Client e server di cassette postali Exchange 2013 sono invisibili e difficile da gestire per i cmdlet di gestione dell'agente di trasporto. Virtualmente tutti gli agenti di trasporto predefiniti che sono visibili e gestibile sono nel servizio di trasporto sui server cassette postali e nei server Trasporto Edge.

Nella tabella seguente sono descritti gli agenti di trasporto incorporati più interessanti sui server cassette postali. Si noti che questa tabella non include molti degli agenti di trasporto invisibili e difficile da gestire.

### Agenti di trasporto incorporati interessanti sui server cassette postali

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome agente</th>
<th>Gestibile?</th>
<th>Priorità</th>
<th>Eventi SMTP o classificatore</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agente della regola di trasporto</p></td>
<td><p>Sì</p></td>
<td><p>1</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente malware</p></td>
<td><p>Sì</p></td>
<td><p>2</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente di Routing della messaggistica di testo</p></td>
<td><p>Sì</p></td>
<td><p>3</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente di recapito di messaggistica di testo</p></td>
<td><p>Sì</p></td>
<td><p>4</p></td>
<td><p>n/d</p></td>
</tr>
<tr class="odd">
<td><p>Agente di Journal</p></td>
<td><p>No</p></td>
<td><p>Non è configurabile</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente di decrittografia rapporto del journal</p></td>
<td><p>No</p></td>
<td><p>Non è configurabile</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente di decrittografia RMS</p></td>
<td><p>No</p></td>
<td><p>Non è configurabile</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente di decrittografia RMS</p></td>
<td><p>No</p></td>
<td><p>Non è configurabile</p></td>
<td><p><strong>OnSubmittedMessage</strong>, <strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente di decrittografia RMS protocollo</p></td>
<td><p>No</p></td>
<td><p>Non è configurabile</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
</tbody>
</table>


Nei server Trasporto Edge, la maggior parte degli agenti di trasporto sono visibili e gestibili tramite i cmdlet di gestione dell'agente di trasporto o tramite i cmdlet di altri caratteristiche.

Nella tabella seguente sono descritti gli agenti di trasporto incorporati più interessanti nei server Trasporto Edge. Si noti che questa tabella non include gli agenti di trasporto invisibili o difficile da gestire.

### Agenti di trasporto incorporati interessanti su server Trasporto Edge

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome agente</th>
<th>Gestibile?</th>
<th>Priorità</th>
<th>Eventi SMTP o classificatore</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agente filtro connessioni</p></td>
<td><p>Sì</p></td>
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong>, <strong>OnMailCommand</strong>, <strong>OnRcptComand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente in ingresso riscrittura degli indirizzi</p></td>
<td><p>Sì</p></td>
<td><p>2</p></td>
<td><p><strong>OnRcptCommand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente della regola di Edge</p></td>
<td><p>Sì</p></td>
<td><p>3</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente filtro contenuto *</p></td>
<td><p>Sì</p></td>
<td><p>4</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente ID mittente *</p></td>
<td><p>Sì</p></td>
<td><p>5</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente filtro mittente *</p></td>
<td><p>Sì</p></td>
<td><p>6</p></td>
<td><p><strong>OnMailCommand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente filtro destinatario</p></td>
<td><p>Sì</p></td>
<td><p>7</p></td>
<td><p><strong>OnRcptCommand</strong></p></td>
</tr>
<tr class="even">
<td><p>Protocollo Analysis agente *</p></td>
<td><p>Sì</p></td>
<td><p>8</p></td>
<td><p><strong>OnConnectEvent</strong>, <strong>OnEndOfHeaders</strong>, <strong>OnEndOfData</strong>, <strong>OnReject</strong>, <strong>OnRsetCommand</strong>, <strong>OnDisconnectEvent</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente di filtro degli allegati</p></td>
<td><p>Sì</p></td>
<td><p>9</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente in uscita riscrittura degli indirizzi</p></td>
<td><p>Sì</p></td>
<td><p>10</p></td>
<td><p><strong>OnSubmittedMessage</strong>, <strong>OnRoutedMessage</strong></p></td>
</tr>
</tbody>
</table>


\* È anche possibile installare e configurare questi agenti protezione da posta indesiderati sui server cassette postali. Per ulteriori informazioni, vedere [Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

Inizio pagina

## Risoluzione dei problemi di agenti di trasporto

Per risolvere i problemi relativi agli agenti di trasporto, è possibile utilizzare le funzionalità seguenti:

  - **Get-TransportPipeline**   Questo cmdlet viene corrispondente gli agenti di trasporto che riscontrare i messaggi in Exchange server e gli eventi SMTP. Per ulteriori informazioni, vedere [Agenti di trasporto di visualizzazione nella pipeline di trasporto](view-transport-agents-in-the-transport-pipeline-exchange-2013-help.md).

  - **Analisi della pipeline**   Analisi della pipeline consente di creare uno snapshot esatto di un messaggio prima e dopo la rilevazione ciascun agente di trasporto. In questo modo è possibile trovare un agente di trasporto che ha provocato risultati imprevisti. Per ulteriori informazioni, vedere [Analisi della pipeline](pipeline-tracing-exchange-2013-help.md).

Inizio pagina


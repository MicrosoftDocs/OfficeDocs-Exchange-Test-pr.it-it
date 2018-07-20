---
title: 'Accodamento prioritario: Exchange 2013 Help'
TOCTitle: Accodamento prioritario
ms:assetid: 6edbd826-fe55-435b-9c63-48e6365c3d09
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb691107(v=EXCHG.150)
ms:contentKeyID: 51407376
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Accodamento prioritario

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

*Accodamento priorità* è una funzionalità di Microsoft Exchange Server 2013 che consente alla priorità di un messaggio definita dal mittente di influenzarne l'elaborazione tramite il servizio Trasporto sul server Cassette postali.

La priorità di un messaggio viene assegnata dal mittente in Microsoft Outlook in fase di creazione e invio del messaggio. Il mittente può impostare i seguenti valori relativi alla priorità dei messaggi in Outlook:

  - Priorità bassa

  - Priorità normale

  - Priorità alta

La priorità predefinita per un messaggio creato in Outlook o Outlook Web App è Priorità normale. La priorità dei messaggi è archiviata nel campo di intestazione di `X-Priority` nell'intestazione del messaggio.

Ogni messaggio inviato o ricevuto da un'organizzazione di Exchange 2013 deve essere classificato nel servizio Trasporto su un server Cassette postali prima di poter essere instradato e recapitato. Il classificatore nel servizio Trasporto su una cassetta postale preleva un messaggio alla volta dalla coda Invio ed esegue la risoluzione dei destinatari e del routing e la conversione del contenuto su un messaggio prima di inserirlo in una coda di recapito. Per ulteriori informazioni, vedere [Flusso di posta](mail-flow-exchange-2013-help.md).

Le code di recapito vengono create dinamicamente in base alla destinazione di un messaggio. Per ulteriori informazioni, vedere [Code](queues-exchange-2013-help.md).

Tutti i messaggi con la stessa destinazione vengono collocati nella stessa coda di recapito. L'accodamento priorità influenza la trasmissione dei messaggi da una coda di recapito al server di messaggistica di destinazione. Quando questa funzionalità è abilitata, i messaggi con Priorità alta vengono trasmessi alle destinazioni appropriate prima di quelli con Priorità normale. Questi ultimi vengono trasmessi alle destinazioni prima dei messaggi con Priorità bassa. Il recapito dei messaggi basato sulla priorità può consentire di definire specifici requisiti per il contratto di servizio (SLA, Service Level Agreement) per i tentativi di recapito dei messaggi.

## Opzioni per la configurazione dell'accodamento priorità

Il supporto per l'accodamento priorità è controllato da chiavi nel file di configurazione dell'applicazione XML `%ExchangeInstallPath%bin\EdgeTransport.exe.config`. Per istruzioni su come configurare l'accodamento priorità, vedere [Attivare e configurare Accodamento prioritario](enable-and-configure-priority-queuing-exchange-2013-help.md).

Nella seguente tabella viene illustrata dettagliatamente ciascuna chiave.

### Chiavi di accodamento priorità nel file EdgeTransport.exe.config

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiave</th>
<th>Valore predefinito</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>PriorityQueuingEnabled</em></p></td>
<td><p><code>false</code></p></td>
<td><p>Questa chiave abilita o disabilita l'accodamento priorità nel servizio Trasporto sul server Cassette postali. Il valore valido per questa chiave è <code>true</code> o <code>false</code>.</p>
<p>Quando la chiave è <code>false</code>, l'accodamento priorità è disabilitato e tutti i limiti dei messaggi di accodamento priorità esistenti nel file EdgeTransport.exe.config vengono ignorati.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxHighPriorityMessageSize</em></p></td>
<td><p><code>250KB</code></p></td>
<td><p>La chiave specifica la dimensione massima consentita di un messaggio con Priorità alta. Se la dimensione di un messaggio con Priorità alta supera il valore specificato dalla chiave, viene effettuato automaticamente il downgrade del messaggio da Priorità alta a Priorità normale.</p>
<p>Il valore della chiave deve essere notevolmente inferiore al valore del parametro <em>MaxSendMessageSize</em> sul cmdlet <strong>Set-TransportConfig</strong>. Il valore predefinito di questo parametro è <code>10 MB</code>. La differenza tra questi due valori consente di assicurarsi tentativi di recapito omogenei e prevedibili per i messaggi con Priorità alta.</p>
<p>Nel caso venga immesso un valore, qualificarlo con una delle seguenti unità:</p>
<ul>
<li><p>KB (kilobyte)</p></li>
<li><p>MB (megabyte)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>LowPriorityDelayNotificationTimeout</em></p>
<p><em>NormalPriorityDelayNotificationTimeout</em></p>
<p><em>HighPriorityDelayNotificationTimeout</em></p></td>
<td><p><strong>Bassa</strong>   <code>8:00:00</code> (8 ore)</p>
<p><strong>Normale</strong>   <code>4:00:00</code> (4 ore)</p>
<p><strong>Alta</strong>   <code>00:30:00</code> (30 minuti)</p></td>
<td><p>Queste chiavi specificano l'intervallo di timeout per i messaggi di notifica sullo stato del recapito in ritardo in base alla priorità del messaggio.</p>
<p>Dopo ogni tentativo fallito di recapito del messaggio, il servizio Trasporto genera un messaggio di notifica del ritardo nel recapito e lo accoda per inviarlo al mittente del messaggio non recapitato. Questo messaggio DSN viene inviato solo dopo un intervallo di timeout di notifica di ritardo specificato, e solo se il messaggio non riuscito non è stato recapitato in quell'arco di tempo. Questo intervallo di tempo evita l'invio di messaggi DSN non necessari che potrebbe essere causato da problemi di trasmissione del messaggio temporanei.</p>
<p>Per specificare un valore, immetterlo come intervallo di tempo: gg.hh:mm:ss dove g = giorni, h = ore, m = minuti e s = secondi.</p></td>
</tr>
<tr class="even">
<td><p><em>LowPriorityMessageExpirationTimeout</em></p>
<p><em>NormalPriorityMessageExpirationTimeout</em></p>
<p><em>HighPriorityMessageExpirationTimeout</em></p></td>
<td><p><strong>Bassa</strong>   <code>2.00:00:00</code> (2 ore)</p>
<p><strong>Normale</strong>   <code>2.00:00:00</code> (2 giorni)</p>
<p><strong>Alta</strong>   <code>8:00:00</code> (8 ore)</p></td>
<td><p>Queste chiavi specificano il periodo di tempo massimo in cui il servizio Trasporto tenta di consegnare un messaggio non inviato. Se il messaggio non può essere consegnato entro l'intervallo di time out di scadenza, viene recapitato al mittente un rapporto di mancato recapito (NDR) contenente il messaggio originale o le intestazioni del messaggio.</p>
<p>Per specificare un valore, immetterlo come intervallo di tempo: gg.hh:mm:ss dove g = giorni, h = ore, m = minuti e s = secondi.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxPerDomainLowPriorityConnections</em></p>
<p><em>MaxPerDomainNormalPriorityConnections</em></p>
<p><em>MaxPerDomainHighPriorityConnections</em></p></td>
<td><p><strong>Bassa</strong>   2</p>
<p><strong>Normale</strong>   15</p>
<p><strong>Alta</strong>   3</p></td>
<td><p>Queste chiavi specificano il numero massimo di connessioni a un unico dominio remoto che il servizio Trasporto è in grado di tenere aperte. Le connessioni in uscita ai domini remoti vengono effettuate tramite le code di recapito e i connettori di invio esistenti nel server Cassette postali.</p>
<p>la somma delle tre chiavi deve essere inferiore o uguale al valore del parametro <em>MaxPerDomainOutboundConnections</em> sul cmdlet <strong>Set-TransportService</strong>. Il valore predefinito di questo parametro è <code>20</code>.</p></td>
</tr>
</tbody>
</table>


## Influenza dell'accodamento priorità sugli altri limiti per i messaggi sui server Cassette postali

Tutti i messaggi che passano per il servizio Trasporto sono soggetti a vari limiti relativi all'invio, al reinvio e alla scadenza. Per ulteriori informazioni, vedere [Limiti di dimensione dei messaggi](message-size-limits-exchange-2013-help.md).

Ad alcuni limiti dei messaggi disponibili nel cmdlet **Set-TransportService** corrispondono limiti di messaggi di accodamento priorità disponibili nel file di configurazione dell'applicazione EdgeTransport.exe.config. Nella seguente tabella vengono illustrati questi limiti di messaggi corrispondenti.

### Limiti di messaggi nel cmdlet Set-TransportService che corrispondono ai limiti di messaggi dell'accodamento priorità nel file EdgeTransport.exe.config

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origine</th>
<th>Parametro o chiave</th>
<th>Valore predefinito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code> (4 ore)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityDelayNotificationTimeout</em></p></td>
<td><p><code>4:00:00</code> (4 ore)</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MessageExpirationTimeOut</em></p></td>
<td><p><code>2.00:00:00</code> (2 giorni)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityMessageExpirationTimeout</em></p></td>
<td><p><code>2.00:00:00</code> (2 giorni)</p></td>
</tr>
</tbody>
</table>


Quando la funzionalità accodamento priorità è disabilitata, vengono ignorati tutti i limiti di messaggi relativi presenti nel file di configurazione EdgeTransport.exe.config. Tutti i limiti di messaggi nel cmdlet **Set-TransportService** si applicano a tutti i messaggi che passano per il servizio Trasporto sul server Cassette postali.

Quando la funzionalità accodamento priorità è abilitata, i relativi limiti di messaggi nel file di configurazione EdgeTransport.exe.config sostituiscono i corrispondenti limiti di messaggi nel cmdlet **Set-TransportService**. Tutti gli altri limiti di messaggi nel cmdlet **Set-TransportService** vengono ancora applicati ai messaggi con Priorità bassa, Priorità normale e Priorità alta che passano per il servizio Trasporto sul server Cassette postali.

## Impostazioni utente per accodamento priorità

Cmdlet **Set-Mailbox** con il parametro *DowngradeHighPriorityMessagesEnabled* Il valore predefinito è `$false`. Quando questo parametro è impostato su `$true`, viene automaticamente effettuato il downgrade di tutti i messaggi inviati dalla cassetta postale con Priorità alta in Priorità normale.


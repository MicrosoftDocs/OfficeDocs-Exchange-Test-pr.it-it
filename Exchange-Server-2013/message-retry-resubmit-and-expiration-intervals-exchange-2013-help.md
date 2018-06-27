---
title: 'Intervalli di ripetizione, reinvio e scadenza messaggio: Exchange 2013 Help'
TOCTitle: Intervalli di ripetizione, reinvio e scadenza messaggio
ms:assetid: 03020e6f-4c01-4c6e-ae47-fd74d4c4f96a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ891103(v=EXCHG.150)
ms:contentKeyID: 51407332
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Intervalli di ripetizione, reinvio e scadenza messaggio

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

In Microsoft Exchange Server 2013, i messaggi che non possono essere recapitati correttamente sono soggetti a varie scadenze Riprova, reinvio e scadenza basate su origine e di destinazione del messaggio. *Tentativi* è un tentativo di connessione rinnovato con la destinazione. *Reinvio* è atto di inviare messaggi alla coda di invio classificatore di rielaborare. Il messaggio non *scade* dopo tutti gli sforzi di recapito non riusciti su un determinato periodo di tempo. Dopo la scadenza di un messaggio, il mittente riceve una notifica dell'errore di recapito. Il messaggio viene quindi eliminato dalla coda.

In tutti e tre Riprova rinviare o scade, è possibile intervenire manualmente prima di eseguire le azioni automatiche per i messaggi.

Per istruzioni su come configurare questi intervalli, vedere [Configurare gli intervalli di ripetizione, reinvio e scadenza messaggio](configure-message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md).

## Opzioni di configurazione per un nuovo tentativo messaggio

Quando un server di trasporto non può connettersi all'hop successivo, la coda viene messo in stato è Riprova. I tentativi di connessione continuano finché non scade la coda o viene eseguita la connessione.

## Opzioni di configurazione per un nuovo tentativo automatica dei messaggi

Nella tabella seguente sono descritte le opzioni di configurazione sono disponibili per gli intervalli messaggio.

### Opzioni di configurazione disponibili per messaggio intervalli tentativi

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome parametro o la chiave</th>
<th>Valore predefinito</th>
<th>Configurazione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueGlitchRetryCount</em></p></td>
<td><p>4</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Questa chiave consente di specificare il numero di tentativi di connessione vengono tentati immediatamente quando un server di trasporto con problemi di connessione al server di destinazione. Tali problemi di connessione vengono in genere causati da interruzioni della rete molto breve.</p>
<p>L'input valido per questa chiave è un numero intero compreso tra 0 e 15.</p>
<p>In genere, non è necessario modificare questa chiave, a meno che la rete non è affidabile e continua possano sfruttare al meglio molte connessioni accidentalmente interrotte.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueGlitchRetryInterval</em></p></td>
<td><p><code>00:01:00</code> o 1 minuto</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Questa chiave consente di controllare l'intervallo di connessione tra un tentativo di connessione specificato dalla chiave <em>QueueGlitchRetryCount</em> .</p>
<p>In genere, non è necessario modificare questo parametro solo se la rete non è affidabile e continua possano sfruttare al meglio molte connessioni accidentalmente interrotte.</p></td>
</tr>
<tr class="odd">
<td><p><em>TransientFailureRetryCount</em></p></td>
<td><p>6</p></td>
<td><p><strong>Set-TransportService</strong> proprietà nell'interfaccia di amministrazione di Exchange (EAC) cmdlet o del server</p></td>
<td><p>Questo parametro consente di specificare il numero di tentativi di connessione a cui si è tentato dopo i tentativi di connessione che vengono controllati per i tasti <em>QueueGlitchRetryCount</em> e <em>QueueGlitchRetryInterval</em> non riusciti. Problemi di connessione che le chiavi <em>QueueGlitchRetryCount</em> e <em>QueueGlitchRetryInterval</em> di scarico possono essere causati dal riavvio del server o memorizzati nella cache degli errori di ricerca DNS.</p>
<p>L'input valido per questo parametro è un numero intero compreso tra 0 e 15. Se questo parametro è impostato su 0, al successivo tentativo di connessione è controllato dal parametro <em>OutboundConnectionFailureRetryInterval</em> .</p></td>
</tr>
<tr class="even">
<td><p><em>TransientFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Servizio di trasporto nei server cassette postali: <code>00:05:00</code> o 5 minuti</p></li>
<li><p>Server Trasporto Edge: <code>00:01:00</code> o 10 minuti</p></li>
</ul></td>
<td><p>proprietà <strong>Set-TransportService</strong>cmdlet o del server in EAC</p></td>
<td><p>Questo parametro determina l'intervallo di connessione tra un tentativo di connessione specificata dal parametro <em>TransientFailureRetryCount</em> .</p>
<p>Per specificare un valore, immetterlo come intervallo di tempo: gg.hh:mm:ss dove g = giorni, h = ore, m = minuti e s = secondi.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundConnectionFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Servizio di trasporto nei server cassette postali: <code>00:10:00</code> o 10 minuti</p></li>
<li><p>Server Trasporto Edge: <code>00:30:00</code> o 30 minuti</p></li>
</ul></td>
<td><p>proprietà <strong>Set-TransportService</strong> cmdlet o del server in EAC</p></td>
<td><p>Questo parametro specifica l'intervallo per i tentativi di connessione in uscita non riuscite in precedenza. I tentativi di connessione non riuscita in precedenza sono controllati dai parametri <em>TransientFailureRetryCount</em> e <em>TransientFailureRetryInterval</em> .</p>
<p>Per specificare un valore, immetterlo come intervallo di tempo: gg.hh:mm:ss dove g = giorni, h = ore, m = minuti e s = secondi.</p></td>
</tr>
<tr class="even">
<td><p><em>MessageRetryInterval</em></p></td>
<td><p><code>00:15:00</code> or15 minuti</p></td>
<td><p>cmdlet <strong>Set-TransportService</strong></p></td>
<td><p>Questo parametro consente di specificare l'intervallo per singoli messaggi il cui stato è Riprova. È consigliabile non modificare il valore predefinito a meno che non Microsoft al servizio supporto tecnico notifiche per eseguire questa operazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>MailboxDeliveryQueueRetryInterval</em></p></td>
<td><p><code>00:05:00</code> o 5 minuti</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Questa chiave consente di specificare la frequenza con cui le code tentano di connettersi al servizio di recapito di trasporto delle cassette postali per un database delle cassette postali di destinazione non è raggiungibile correttamente.</p>
<p>Per specificare un valore, immetterlo come intervallo di tempo: gg.hh:mm:ss dove g = giorni, h = ore, m = minuti e s = secondi.</p>
<p>L'input valido per questa chiave è da 00:00:01 a 1.00:00:00.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Opzioni di configurazione per un nuovo tentativo messaggi manuale

Quando una coda di recapito è lo stato Riprova, è possibile forzare manualmente un tentativo di connessione immediata utilizzando il Visualizzatore code nella casella degli strumenti di Exchange o il cmdlet **Retry-Queue** in Shell. Il tentativo di tentativi manuale sostituisce la volta successiva che Riprova pianificata. Se la connessione non ha esito positivo, viene reimpostato il timer di intervallo tentativi query. Coda di recapito deve essere stato è Riprova per questa azione abbia effetto.

Per ulteriori informazioni, vedere la sezione "Code dei tentativi" in [Gestire le code](manage-queues-exchange-2013-help.md).

Inizio pagina

## Opzioni di configurazione per i messaggi DSN di ritardo

Dopo ogni errori di recapito dei messaggi, il server Trasporto Edge o il servizio di trasporto sul server cassette postali genererà un messaggio di notifica (DSN) lo stato di recapito ritardo e code per il recapito al mittente del messaggio non recapitabile. Questo messaggio di ritardo DSN viene inviato solo dopo un intervallo di timeout di notifica di ritardo specificato e solo se il messaggio di errore non è stato correttamente recapitato periodo di tempo. Per impostazione predefinita, l'intervallo di timeout di notifica di ritardo è 4 ore. Questo ritardo impedisce l'invio di messaggi DSN ritardo non necessari che possono dipendere da errori di trasmissione di messaggi temporaneo. L'invio di messaggi di notifica di ritardo DSN può essere in modo selettivo abilitato o disabilitato per i messaggi che hanno origine interni o esterni all'organizzazione di Exchange.

Nella tabella seguente vengono descritte le opzioni di configurazione disponibili per i messaggi di notifica di ritardo DSN.

### Opzioni di configurazione disponibili per i messaggi di notifica di ritardo DSN

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome del parametro</th>
<th>Valore predefinito</th>
<th>Percorso</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code>4 ore</p></td>
<td><p>proprietà <strong>Set-TransportService</strong> o del server in EAC</p></td>
<td><p>Questo parametro consente di specificare il tempo di attesa del server prima di inviare un messaggio DSN ritardo al mittente. Il valore di questo parametro deve essere sempre maggiore del valore del parametro <em>TransientFailureRetryCount</em> moltiplicato per il valore del parametro <em>TransientFailureRetryInterval</em> .</p>
<p>Per specificare un valore, immetterlo come intervallo di tempo: gg.hh:mm:ss dove g = giorni, h = ore, m = minuti e s = secondi.</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>Questo parametro consente di specificare se i messaggi DSN ritardo possono essere inviati ai mittenti dei messaggi che si trovano all'esterno dell'organizzazione di Exchange.</p>
<p>L'input valido per questo parametro è <code>$true</code> o <code>$false</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>Questo parametro consente di specificare se i messaggi DSN ritardo possono essere inviati ai mittenti dei messaggi che si trovano all'interno dell'organizzazione di Exchange.</p>
<p>L'input valido per questo parametro è <code>$true</code> o <code>$false</code>.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Nei server Trasporto Hub Exchange&nbsp;2007, tutti i parametri <EM>ExternalDSN*</EM> e <EM>InternalDSN*</EM> sono disponibili nel cmdlet <STRONG>Set-TransportServer</STRONG> , non il cmdlet <STRONG>Set-TransportConfig</STRONG> . Se si dispongono di tutti i server Trasporto Hub Exchange&nbsp;2007 all'interno dell'organizzazione, è necessario apportare modifiche a questi valori utilizzando il cmdlet <STRONG>Set-TransportServer</STRONG> in ogni server Trasporto Hub Exchange&nbsp;2007.



Inizio pagina

## Opzioni di configurazione per nuovo invio di messaggi

Nuovo invio di messaggi invia messaggi non recapitati a coda di invio per rielaborare dal classificatore.

## Nuovo invio automatica dei messaggi

Mancato recapito dei messaggi vengono ripetute automaticamente se la coda di recapito è lo stato Riprova ed è stato possibile recapitare correttamente i messaggi per un periodo di tempo specificato. Tale periodo di tempo è controllato dalla chiave *MaxIdleTimeBeforeResubmit* nel file di configurazione dell'applicazione EdgeTransport.exe.config. Solo i messaggi nelle code di recapito sono candidati per nuovo invio automatico.

Per specificare un valore, immetterlo come intervallo di tempo: gg.hh:mm:ss dove g = giorni, h = ore, m = minuti e s = secondi.

Il valore predefinito è `12:00:00` o 12 ore.

## Nuovo invio di messaggi manuale

È possibile manualmente reinvio dei messaggi il cui sono seguenti nel servizio di trasporto in un server cassette postali o un server Trasporto Edge:

  - Code di recapito con lo stato Riprova. I messaggi nelle code non devono essere stato sospeso.

  - Messaggi nella coda non raggiungibile e non sono in stato sospeso.

  - Messaggi nella coda di messaggi non elaborabili.

Per ulteriori informazioni sulla coda non raggiungibile e coda di messaggi non elaborabili, vedere "Su the non elaborabili messaggio coda e la coda non raggiungibile" nel argomento [Code](queues-exchange-2013-help.md).

Se si desidera inviare manualmente i messaggi che si trovano nella coda non raggiungibile o code di recapito senza dover attendere l'ora specificata dal parametro *MaxIdleTimeBeforeResubmit* da passare, è necessario utilizzare il cmdlet **Retry-Queue** con il parametro *Resubmit* . Per reinviare manualmente i messaggi che si trovano nella coda di messaggi non elaborabili, è possibile utilizzare il Visualizzatore code o il cmdlet **Resume-Message** per riprendere il messaggio. Per ulteriori informazioni, vedere la sezione "Reinvio dei messaggi nelle code" nel [Gestire le code](manage-queues-exchange-2013-help.md).

Un altro modo in cui è possibile manualmente reinvio dei messaggi è per sospendere i messaggi, esportare i messaggi per i file di testo con l'estensione di file eml e quindi copiare i file EML nella directory di riesecuzione in qualsiasi server cassette postali o Trasporto Edge. Questo metodo nuovo invio può essere utilizzato per i messaggi che si trovano nella coda non raggiungibile o code di recapito. I messaggi che si trovano nella coda di messaggi non elaborabili sono già nello stato Suspended. I messaggi che si trovano nella coda di invio non sono in sospeso o esportare.


> [!NOTE]
> Quando si esportano i messaggi da una coda, è non rimuovere i messaggi dalla coda. Dopo aver esportato i messaggi ed correttamente rinviarle utilizzando la directory di riesecuzione, è consigliabile rimuovere i messaggi sospesi per evitare il recapito dei messaggi duplicati.



Per ulteriori informazioni, vedere [Esportazione dei messaggi dalle code](export-messages-from-queues-exchange-2013-help.md).

Inizio pagina

## Opzioni di configurazione per la scadenza dei messaggi

L' *intervallo di timeout di scadenza messaggio* consente di specificare il periodo di tempo massimo che il servizio di trasporto in un server cassette postali o un server Trasporto Edge tenta di inviare un messaggio non riuscito. Se il messaggio non recapitato correttamente prima che ha passato l'intervallo di timeout di scadenza, un rapporto di mancato recapito che contiene il messaggio originale o le intestazioni del messaggio viene recapitato al mittente.

## Scadenza automatica dei messaggi

L'intervallo di timeout di scadenza dei messaggi è controllato dal parametro *MessageExpirationTimeOut* nel cmdlet **Set-TransportService** o nelle proprietà del server in EAC.

Per specificare un valore, immetterlo come intervallo di tempo: gg.hh:mm:ss dove g = giorni, h = ore, m = minuti e s = secondi.

Il valore predefinito è `2.00:00:00` o 2 giorni. L'intervallo di input valido per questo parametro è da `00:00:05` tramite `90.00:00:00`.

## Scadenza dei messaggi manuale

Anche se non è possibile forzare manualmente i messaggi per scadere, è possibile rimuovere manualmente i messaggi da qualsiasi coda, ad eccezione di coda di invio, con o senza un rapporto di mancato recapito.

Per ulteriori informazioni, vedere la sezione "Rimuovere i messaggi dalle code" nel [Gestione dei messaggi nelle code](manage-messages-in-queues-exchange-2013-help.md).

Inizio pagina


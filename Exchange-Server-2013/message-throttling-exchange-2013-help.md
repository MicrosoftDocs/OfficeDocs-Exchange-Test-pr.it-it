---
title: 'Limitazione per il messaggio: Exchange 2013 Help'
TOCTitle: Limitazione per il messaggio
ms:assetid: fba87902-2a79-42ac-b394-46a9016f667e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232205(v=EXCHG.150)
ms:contentKeyID: 50482123
ms.date: 01/08/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Limitazione per il messaggio

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

*Limitazione della larghezza di banda della rete per i messaggi* indica un gruppo di limiti impostati sul numero di messaggi e connessioni elaborabili da un computer Microsoft Exchange Server 2013. Tali limiti impediscono l'esaurimento, accidentale o intenzionale, delle risorse di sistema nel server Exchange.

**Sommario**

Ambito della limitazione della larghezza di banda della rete per i messaggi

Costo del messaggio e limitazione del flusso di posta

Limitazione della larghezza di banda della rete per i messaggi sui server

Limitazione della larghezza di banda della rete per i messaggi sui connettori di invio

Limitazione della larghezza di banda della rete per i messaggi su connettori di ricezione

Criteri di limitazione dei messaggi

## Ambito della limitazione della larghezza di banda della rete per i messaggi

La limitazione de i messaggi include una serie di limiti su messaggi, velocità di connessione SMTP e valori di timeout della sessione SMTP. Grazie all'interazione di tali limiti, è possibile proteggere un server Exchange da sovraccarichi dovuti all'accettazione e al recapito dei messaggi. Sebbene un ampio backlog di messaggi e connessioni possa restare in attesa di elaborazione, la limitazione della larghezza di banda della rete per i messaggi consente al server Exchange di elaborare i messaggi e le connessioni in modo ordinato.

Oltre alla limitazione della larghezza di banda della rete per i messaggi, è possibile anche imporre limiti di dimensione ai singoli componenti dei messaggi, quali il numero di destinatari, la dimensione dell'intestazione del messaggio o la dimensione dei singoli allegati. Per ulteriori informazioni sui limiti di dimensione del messaggio, vedere [Limiti di dimensione dei messaggi](message-size-limits-exchange-2013-help.md).

Per evitare il sovraccarico delle risorse di sistema di un server di trasporto Exchange è disponibile anche la funzionalità di *controllo dell'utilizzo delle risorse*. Lo stato di congestione è una funzionalità di monitoraggio delle risorse di sistema nel servizio di trasporto sui server Cassette postali e Trasporto Edge. Quando una risorsa di sistema monitorata, ad esempio l'utilizzo dell'unità disco rigido o della memoria, supera la soglia specificata, il server riduce la velocità di accettazione di nuovi messaggi e connessioni per dedicarsi al recapito dei messaggi esistenti. Quando l'utilizzo della risorsa di sistema monitorata ritorna a livelli normali, il server aumenta lentamente la velocità con cui accetta le nuove connessioni e quindi stabilisce un livello normale.

Torna su

## Costo del messaggio e limitazione del flusso di posta

Per garantire una velocità di trasmissione dei messaggi coerente e una latenza di recapito prevedibile, Exchange 2013 stabilisce un costo cumulativo per i messaggi, In Microsoft Exchange Server 2010 SP1 è stata aggiunta la funzionalità QoS (Quality of Service). Il costo è basato sui seguenti criteri:

  - Dimensione messaggio

  - Numero di destinatari

  - Frequenza di trasmissione

I server di trasporto Exchange 2013 tengono traccia del costo di recapito medio dei messaggi inviati da singoli utenti. Basandosi sul costo dei messaggi, Exchange 2013 fornisce un gruppo di impostazioni che consentono di controllare l'effetto di un utente o connessione su un'organizzazione Exchange. Tale gruppo di impostazioni è noto come *criterio di limitazione*. Se un utente invia ripetutamente messaggi ad alto costo, ad esempio messaggi con allegati di grandi dimensioni o messaggi inviati a numerosi destinatari, i server di trasporto basati su Exchange 2013 utilizzano un criterio di limitazione per assegnare una priorità inferiore ai messaggi con costo superiore inviati dall'utente, mentre continuano a recapitare i messaggi con costo inferiore. Questo nuovo comportamento aumenta la "qualità del servizio" offerta dalla funzionalità per la limitazione della larghezza di banda di rete dei messaggi in Exchange 2013.


> [!NOTE]
> La limitazione della larghezza di banda della rete per i messaggi non influisce sulla priorità dei messaggi dal punto di vista dell'utente. I messaggi mantengono la priorità originale impostata dall'utente, ad esempio Importante o Urgente.



Per supportare tale funzionalità, Exchange 2013 utilizza i meccanismi seguenti:

  - **Agente interno per la determinazione della priorità**   Questo agente è attivato dall'evento **OnResolvedMessage** e assegna una priorità inferiore ai messaggi dello stesso mittente con costo cumulativo elevato. Il costo viene misurato su un periodo di un minuto e interessa i messaggi con più di 500 destinatari o con dimensione superiore a 1 MB.

  - **Accodamento con priorità basata sulla quota per le code di tipo MapiDelivery**   Questo meccanismo consente a Exchange di recapitare i messaggi presenti nelle code con priorità normale con una frequenza superiore a quella dei messaggi nelle code a bassa priorità. Per impostazione predefinita, il rapporto tra messaggi con priorità normale e messaggi a bassa priorità è di 20:1. Tuttavia, i nuovi messaggi presenti nella coda con priorità inferiore non vengono ma recapitati prima di quelli nella coda con priorità superiore. Si consideri, ad esempio, lo scenario seguente:
    
    1.  Vengono recapitati venti messaggi con priorità normale. Per impostazione predefinita, il messaggio recapitato successivo ha priorità inferiore.
    
    2.  Il server di trasporto riceve due nuovi messaggi, uno dalla coda con priorità superiore e uno dalla coda con priorità inferiore.
    
    In questo scenario, il messaggio della coda con priorità superiore viene recapitato per primo, quindi viene recapitato quello della coda con priorità inferiore.

  - **Limitazione delle connessioni simultanee in base all'integrità del database di messaggistica**   Questo meccanismo consente di monitorare l'integrità del database di messaggistica (MDB) di Exchange e limitare le connessioni simultanee ai server di trasporto Exchange in base al valore assegnato per la misura dell'integrità. Il database di messaggistica è monitorato dall'API per il monitoraggio dell'integrità della risorsa nel servizio di trasporto sul server Cassette postali e gli viene assegnato un valore di integrità compreso tra -1 e 100. Questo valore si basa sulle statistiche delle prestazioni RPC incluse con ogni risposta RPC dal processo Store.exe nel servizio di trasporto alle cassette postali. Il framework di integrità delle risorse utilizza sia il contatore delle prestazioni **Richeste/Sec**, sia il contatore delle prestazioni **Latenza media RPC** per calcolare il valore dell'integrità del database. Per assicurare un'esperienza utente interattiva coerente, Exchange riduce il numero delle connessioni simultanee a mano a mano che diminuisce il valore dell'integrità. Sono disponibili i seguenti intervalli di valori di integrità:
    
      - **-1:** questo valore indica che lo stato di integrità del database di messaggistica è sconosciuto e viene assegnato all'avvio del database. In questo scenario, il database è considerato integro.
    
      - **0:** questo valore viene assegnato quando il database non è integro. Quando il database si trova in questo stato, non deve essere contattato.
    
      - **Da 1 a 99:** questi valori indicano che il database è abbastanza integro. I valori inferiori rappresentano un livello di integrità inferiore.
    
      - **100:** questo valore indica che il database è completamente integro.

Il servizio di limitazione di Microsoft Exchange fornisce il framework per la limitazione del flusso di posta. Il servizio di limitazione di Microsoft Exchange tiene traccia delle impostazioni relative al flusso di posta per un utente specifico e memorizza nella cache le informazioni relative alla limitazione. Le impostazioni di limitazione della larghezza di banda della rete sono note anche come *budget*. Al riavvio del servizio di limitazione di Microsoft Exchange i budget di limitazione del flusso di posta vengono reimpostati.

È possibile utilizzare i cmdlet dei criteri di limitazione disponibili in Exchange 2013 per configurare le singole impostazioni del budget per un criterio di limitazione. Un budget indica l'entità dell'accesso disponibile a un utente o applicazione per una specifica impostazione. Rappresenta il numero delle connessioni consentito per un utente o l'entità dell'attività consentita all'utente per ogni intervallo di un minuto. È ad esempio possibile configurare un budget per impostare la quantità di tempo per cui un utente può utilizzare una funzionalità specifica di Exchange, ad esempio ActiveSync, Outlook Web App o i servizi Web di Exchange. Questa soglia è archiviata in un criterio di limitazione e definisce il budget.

Le impostazioni di tempo del budget vengono specificate come percentuale di un minuto. Una soglia del 100% rappresenta pertanto un intervallo di 60 secondi. Si supponga ad esempio di voler specificare le impostazioni del criterio Outlook Web App che limitano la quantità di tempo per il quale un utente può eseguire il codice Outlook Web App su un server di accesso client e la quantità di tempo per cui l'utente può comunicare con il server di accesso client, fino a 600 millisecondi su un intervallo di un minuto. A tale scopo, è necessario impostare sull'1% di un minuto (600 millisecondi) entrambi i parametri seguenti:

  - **OWAPercentTimeInCAS:** 1

  - **OWAPercentTimeInMailboxRPC:** 1

Un utente a cui viene applicato questo criterio ha un budget di 600 millisecondi per OWAPercentTimeInCAS e di 600 millisecondi per OWAPercentageTimeInMailboxRPC. In tale scenario, quando l'utente è connesso a Outlook Web App può eseguire il codice di accesso client per un massimo di 600 millisecondi. Dopo 600 millisecondi la connessione supera il budget e il server Exchange non consente ulteriori operazioni di Outlook Web App per un minuto dopo il superamento del limite previsto dal budget. Dopo un minuto l'utente può eseguire il codice di accesso client di Outlook Web App per altri 600 millisecondi.

Torna su

## Limitazione della larghezza di banda della rete per i messaggi sui server

È possibile impostare le opzioni di limitazione della larghezza di banda della rete per i messaggi nelle seguenti posizioni:

  - Nel servizio di trasporto

  - Su un connettore di invio

  - Su un connettore di ricezione

È possibile impostare tutte le opzioni di limitazione della larghezza di banda della rete per i messaggi, disponibili nel servizio di trasporto sui server Cassette postali, nel servizio di trasporto alle cassette postali sui server Cassette postali o nel servizio di trasporto front-end sui server Accesso client utilizzando Exchange Management Shell. È inoltre possibile impostare alcune delle stesse opzioni configurando le proprietà del server di trasporto nell'interfaccia di amministrazione di Exchange.

Nella tabella seguente vengono mostrate le opzioni di limitazione della larghezza di banda della rete per i messaggi, disponibili sui server di trasporto.

### Opzioni di limitazione della larghezza di banda della rete per i messaggi sui server di trasporto

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Origine</th>
<th>Parametro</th>
<th>Valore predefinito</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxDeliveries</em></p></td>
<td><p>20</p></td>
<td><p>Questo parametro consente di specificare il numero massimo di thread di recapito che il servizio di trasporto può tenere aperti contemporaneamente per recapitare i messaggi alle cassette postali. L'intervallo di input valido per questo parametro è compreso tra 1 e 256. Si consiglia di non modificare il valore predefinito, a meno che il servizio clienti e supporto tecnico di Microsoft non richieda di effettuare questa operazione.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxSubmissions</em></p></td>
<td><p>20</p></td>
<td><p>Questo parametro consente di specificare il numero massimo di thread di invio che il servizio di trasporto può tenere aperti contemporaneamente per inviare i messaggi dalle cassette postali. L'intervallo di input valido per questo parametro è compreso tra 1 e 256.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MaxConnectionRatePerMinute</em></p></td>
<td><p>1200</p></td>
<td><p>Questo parametro consente di specificare la velocità massima consentita per l'apertura delle connessioni con il servizio di trasporto. Se si tentano più connessioni contemporaneamente con il servizio di trasporto, il parametro <em>MaxConnectionRatePerMinute</em> limita la velocità di apertura delle connessioni in modo da non sovraccaricare le risorse del server.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong> oppure</p>
<p>Proprietà del server di trasporto</p></td>
<td><p><em>MaxOutboundConnections</em></p></td>
<td><p>1000</p></td>
<td><p>Questo parametro indica il numero massimo di connessioni esterne che possono essere aperte contemporaneamente. Se si immette un valore di <code>unlimited</code>, non viene imposto alcun limite al numero di connessioni in uscita. Il valore di questo parametro deve essere uguale o superiore al valore del parametro <em>MaxPerDomainOutboundConnections</em>.</p>
<p>Questo valore può anche essere configurato tramite EAC in <strong>Server</strong> &gt; <strong>Server</strong> &gt; <strong>Proprietà</strong> &gt; <strong>Limiti di trasporto</strong> &gt; <strong>Restrizioni connessioni in uscita</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong> oppure</p>
<p>Proprietà del server di trasporto</p></td>
<td><p><em>MaxPerDomainOutboundConnections</em></p></td>
<td><p>20</p></td>
<td><p>Questo parametro indica il numero massimo di connessioni contemporanee a un singolo dominio. Se si immette un valore di <code>unlimited</code>, non viene imposto alcun limite al numero di connessioni in uscita per dominio. Il valore di questo parametro deve essere uguale o superiore al valore del parametro <em>MaxOutboundConnections</em>.</p>
<p>Questo valore può anche essere configurato tramite EAC in <strong>Server</strong> &gt; <strong>Server</strong> &gt; <strong>Proprietà</strong> &gt; <strong>Limiti di trasporto</strong> &gt; <strong>Restrizioni connessioni in uscita</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>PickupDirectoryMaxMessagesPerMinute</em></p></td>
<td><p>100</p></td>
<td><p>Questo parametro indica il numero massimo di messaggi elaborati al minuto dalla directory di prelievo e di riesecuzione. Ciascuna directory può elaborare separatamente i file dei messaggi alla velocità specificata da questo parametro.</p></td>
</tr>
</tbody>
</table>


Torna su

## Limitazione della larghezza di banda della rete per i messaggi sui connettori di invio

Nella tabella seguente vengono mostrate le opzioni di limitazione della larghezza di banda della rete per i messaggi, disponibili sui server di trasporto. Per configurare tale opzione è necessario utilizzare Exchange Management Shell.

### Opzione di limitazione della larghezza di banda della rete disponibile per i messaggi sui connettori di invio

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Origine</th>
<th>Parametro</th>
<th>Valore predefinito</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-SendConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>10 minuti</p></td>
<td><p>Questo parametro consente di specificare il tempo massimo per il quale una connessione SMTP aperta con un server di messaggistica di destinazione può restare inattiva prima che venga chiusa.</p></td>
</tr>
</tbody>
</table>


Torna su

## Limitazione della larghezza di banda della rete per i messaggi su connettori di ricezione

Nella seguente tabella sono mostrate le opzioni di limitazione della larghezza di banda della rete per i messaggi disponibili sui connettori di ricezione configurati nel servizio di trasporto su un server Cassette postali o Trasporto Edge. Per configurare tali opzioni è necessario utilizzare Exchange Management Shell.

### Opzione di limitazione della larghezza di banda della rete disponibile per i messaggi sui connettori di ricezione

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Origine</th>
<th>Parametro</th>
<th>Valore predefinito</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>5 minuti nel servizio di trasporto sui server Cassette postali</p>
<p>5 minuti nel servizio di trasporto front-end sui server Accesso client.</p>
<p>1 minuto sui server Trasporto Edge.</p></td>
<td><p>Questo parametro consente di specificare il tempo massimo per il quale una connessione SMTP aperta con un server di messaggistica di origine può restare inattiva prima che venga chiusa. Il valore del parametro deve essere inferiore al valore specificato dal parametro <em>ConnectionTimeout</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionTimeOut</em></p></td>
<td><p>10 minuti nel servizio di trasporto sui server Cassette postali</p>
<p>10 minuti nel servizio di trasporto front-end sui server Accesso client.</p>
<p>5 minuti sui server Trasporto Edge.</p></td>
<td><p>Questo parametro consente di specificare il tempo massimo per il quale una connessione SMTP con un server di messaggistica di origine può restare aperta anche se è in corso la trasmissione di dati dal server di messaggistica di origine. Il valore del parametro deve essere superiore al valore specificato dal parametro <em>ConnectionInactivityTimeout</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnection</em></p></td>
<td><p>5000</p></td>
<td><p>Questo parametro consente di specificare il numero massimo di connessioni SMTP in ingresso consentite contemporaneamente dal connettore di ricezione.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPercentagePerSource</em></p></td>
<td><p>100% sul connettore di ricezione predefinito nel servizio di trasporto su un server Cassette postali</p>
<p>2% sugli altri connettori di ricezione nel servizio di trasporto sui server Cassette postali e nel servizio di trasporto front-end sui server Accesso client.</p></td>
<td><p>Questo parametro consente di specificare il numero massimo di connessioni SMTP consentite contemporaneamente dal connettore di ricezione da un singolo server di messaggistica di origine. Il valore viene espresso come percentuale delle connessioni rimanenti disponibili in un connettore di ricezione. Il numero massimo di connessioni consentite dal connettore di ricezione è definito dal parametro <em>MaxInboundConnection</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPerSource</em></p></td>
<td><p>unlimited sul connettore di ricezione predefinito nel servizio di trasporto su un server Cassette postali</p>
<p>20% sugli altri connettori di ricezione nel servizio di trasporto sui server Cassette postali e nel servizio di trasporto front-end sui server Accesso client.</p></td>
<td><p>Questo parametro consente di specificare il numero massimo di connessioni SMTP consentite contemporaneamente dal connettore di ricezione da un singolo server di messaggistica di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxProtocolErrors</em></p></td>
<td><p>5</p></td>
<td><p>Questo parametro consente di specificare il numero massimo di errori del protocollo SMTP consentiti dal connettore di ricezione prima che chiuda la connessione con il server di messaggistica di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>TarpitInterval</em></p></td>
<td><p>5 secondi</p></td>
<td><p>Questo parametro consente di specificare il ritardo utilizzato durante il <em>tarpitting</em>. Il tarpitting consiste nel ritardare artificialmente le risposte SMTP per specifici modelli di comunicazione SMTP che indicano un attacco directory harvest o altri messaggi non graditi. Un <em>attacco directory harvest</em> è un tentativo di raccogliere indirizzi di posta elettronica validi da una determinata organizzazione in modo da poterli utilizzare come destinatari di messaggi commerciali indesiderati.</p>
<p>Il ritardo, che viene specificato dal parametro <em>TarpitInterval</em>, si applica solo alle connessioni anonime.</p></td>
</tr>
</tbody>
</table>


Torna su

## Criteri di limitazione dei messaggi

In Exchange 2013, ciascuna cassetta postale ha un'impostazione *ThrottlingPolicy*. Il valore predefinito per questa impostazione è vuoto (`$null`). È possibile utilizzare il parametro *ThrottlingPolicy* sul cmdlet **Set-Mailbox** per configurare un criterio di limitazione della larghezza di banda della rete per una cassetta postale.

È disponibile un criterio di limitazione predefinito che consente di specificare una configurazione di budget predefinita per gli utenti che si connettono a Exchange. Per configurare le impostazioni di budget personalizzate per uno o più utenti, creare un nuovo criterio di limitazione, quindi applicare il criterio all'utente o al gruppo appropriato.


> [!IMPORTANT]
> Si consiglia di non modificare il criterio di limitazione predefinito.



Tutte le opzioni di limitazione della larghezza di banda della rete per i messaggi disponibili nei server Cassette postali possono essere impostate in Exchange Management Shell. Per gestire i criteri di limitazione sono disponibili i cmdlet seguenti:

  - **Get-ThrottlingPolicy**

  - **Remove-ThrottlingPolicy**

  - **New-ThrottlingPolicy**

  - **Set-ThrottlingPolicy**

È possibile utilizzare i cmdlet **New-ThrottlingPolicy** e **Set-ThrottlingPolicy** per configurare la quantità di operazioni che un utente può eseguire in Exchange su una specifica connessione per un intervallo di tempo specifico. Tali impostazioni definiscono il budget di un utente. È possibile definire criteri di limitazione per controllare l'accesso alle seguenti funzionalità di Exchange:

  - Exchange ActiveSync

  - Servizi Web Exchange

  - Outlook Web App

  - Messaggistica unificata

  - IMAP4

  - POP3

  - Connessioni client Outlook (MAPI o RPC)

  - Impostazioni del flusso di posta

  - Comandi PowerShell

  - Utilizzi della CPU

Torna su


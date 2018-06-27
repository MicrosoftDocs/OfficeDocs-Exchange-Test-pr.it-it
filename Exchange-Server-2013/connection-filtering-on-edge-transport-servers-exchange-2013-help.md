---
title: 'Il filtro connessioni su server Trasporto Edge: Exchange 2013 Help'
TOCTitle: Il filtro connessioni su server Trasporto Edge
ms:assetid: b513755c-5d3e-44fa-a6cb-771d48b544ac
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124320(v=EXCHG.150)
ms:contentKeyID: 60829840
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Il filtro connessioni su server Trasporto Edge

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Il filtro delle connessioni è una funzionalità di protezione da posta indesiderata di Microsoft Exchange Server 2013 che consente o blocca la posta elettronica in base all'origine del messaggio. Il filtro delle connessioni è fornito dall'agente Filtro connessioni, disponibile solo nei server Trasporto Edge. L'agente Filtro Connessioni si basa sull'indirizzo IP del server di posta di connessione per determinare quale azione, se disponibile, deve essere eseguita su un messaggio in arrivo.

Per impostazione predefinita, l'agente Filtro connessioni è il primo agente di protezione da posta indesiderata a valutare un messaggio in arrivo su un server Trasporto Edge. L'indirizzo IP di origine della connessione SMTP viene verificato rispetto agli indirizzi IP consentiti e bloccati. Se l'indirizzo IP di origine viene consentito in modo specifico, il messaggio viene inviato ai destinatari dell'organizzazione senza ulteriore elaborazione da parte di altri agenti di protezione da posta indesiderata. Se l'indirizzo IP di origine è bloccato in modo specifico, la connessione SMTP viene interrotta. Se l'indirizzo IP di origine non viene consentito né bloccato in modo specifico, il messaggio passa attraverso gli altri agenti di protezione da posta indesiderata sul server Trasporto Edge.

Il filtro connessione confronta l'indirizzo IP del server di posta di origine con i valori dell'elenco indirizzi IP consentiti, dell'elenco indirizzi IP bloccati, dei provider elenco indirizzi IP consentiti e dei provider elenco indirizzi IP bloccati. Per consentire il funzionamento del filtro connessione, è necessario configurare almeno uno di questi quattro archivi dati di indirizzi IP. Se non vengono specificati dati per gli indirizzi IP, è necessario disabilitare l'agente Filtro connessioni. Per ulteriori informazioni, vedere [Gestire il filtro connessioni su server Trasporto Edge](manage-connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

**Sommario**

IP Block list

IP Allow list

IP Block List providers

IP Allow List providers

Test IP Block List providers and IP Allow List providers

Configure connection filtering on Edge Transport servers that aren't directly connected to the Internet

## Elenco Blocca indirizzi IP

L'elenco indirizzi IP bloccati contiene gli indirizzi IP dei server di posta elettronica che si desidera bloccare. È necessario effettuare la manutenzione manuale dell'elenco indirizzi IP bloccati. È possibile aggiungere singoli indirizzi IP o intervalli di indirizzi IP. È possibile specificare una data di scadenza che specifichi la durata del blocco di una voce di indirizzo IP. Quando viene raggiunta la data di scadenza, la voce di indirizzo IP bloccata viene disabilitata.

Se l'agente Filtro connessioni trova l'indirizzo IP di origine nell'elenco indirizzi IP bloccati, la connessione SMTP viene interrotta quando tutte le intestazioni **RCPT TO** (destinatari della busta) nel messaggio vengono elaborati.

Gli indirizzi IP possono inoltre essere aggiunti automaticamente all'elenco degli indirizzi IP bloccati mediante la funzionalità Reputazione mittente dell'Agente di analisi protocollo. Per ulteriori informazioni, vedere [Reputazione mittente e agente di analisi protocollo](sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md).

## Elenco indirizzi IP consentiti

L'elenco indirizzi IP consentiti contiene gli indirizzi IP dei server di posta elettronica che si desidera indicare come origini attendibili della posta elettronica. La posta elettronica proveniente dai server di posta specificati nell'elenco indirizzi IP consentiti non viene elaborata da altri agenti di protezione da posta indesiderata di Exchange.

È necessario effettuare la manutenzione manuale dell'elenco indirizzi IP consentiti. È possibile aggiungere singoli indirizzi IP o intervalli di indirizzi IP. È possibile specificare una data di scadenza che specifichi la durata del consenso a una voce di indirizzo IP. Quando viene raggiunta la data di scadenza, la voce nell'elenco indirizzi IP consentiti viene disabilitata.

Inizio pagina

## Provider dell'elenco indirizzi IP bloccati

I provider dell'elenco indirizzi IP bloccati vengono spesso denominati *elenchi indirizzi bloccati in tempo reale* o RBL. I provider dell'elenco indirizzi IP bloccati compilano elenchi degli indirizzi IP server di posta che inviano posta indesiderata. Molti provider elenchi indirizzi IP bloccati compilano anche elenchi degli indirizzi IP server di posta che potrebbero essere utilizzati per la posta indesiderata. Tra questi, i server di posta configurati per l'inoltro aperto, i provider di servizi Internet che assegnano indirizzi IP dinamici e quelli che consentono il traffico del server di posta SMTP dagli account di connessione remota.

Quando si configura il filtro delle connessioni in modo che utilizzi un provider dell'elenco indirizzi IP bloccati, l'agente Filtro connessioni confronta l'indirizzo IP del server di posta di connessione all'elenco indirizzi IP nel provider dell'elenco indirizzi IP bloccati. In caso di corrispondenza, il messaggio non viene consentito nell'organizzazione. È possibile configurare il filtro connessioni in modo che utilizzi più provider dell'elenco indirizzi IP bloccati, e assegnare valori di priorità diversi a ciascun provider.

L'agente Filtro connessioni verifica l'indirizzo IP di origine nell'elenco indirizzi IP consentiti e nell'elenco di indirizzi IP bloccati. Se l'indirizzo IP non esiste in nessuno degli elenchi, l'agente Filtro connessioni esegue una query al provider dell'elenco indirizzi IP bloccati in base al valore di priorità assegnato. Se l'indirizzo IP è definito in un provider dell'elenco indirizzi IP bloccati, il server Trasporto Edge attende l'intestazione **RCPT TO** e la elabora, risponde al server di posta di invio con un errore `SMTP 550` e chiude la connessione. La connessione non viene interrotta subito, in modo da consentire la registrazione del tentativo di connessione, e in quanto è possibile specificare i destinatari esentati dal blocco dei messaggi da parte di qualsiasi provider dell'elenco indirizzi IP bloccati.

Se l'indirizzo IP non è definito in nessuno dei provider dell'elenco indirizzi IP bloccati, l'agente Filtro contenuto passa il messaggio al successivo agente di trasporto del server Trasporto Edge.

Per ciascun provider dell'elenco indirizzi IP bloccati è possibile personalizzare l'errore `SMTP 550` che viene restituito al mittente quando un messaggio viene bloccato. È necessario identificare il provider dell'elenco indirizzi IP bloccati che ha individuato l'origine del messaggio come posta indesiderata. Se un server di posta di origine legittimo come origine di posta indesiderata, l'amministratore può quindi contattare il provider dell'elenco indirizzi IP bloccati e intraprendere i passaggi necessari a rimuovere il server di posta dal provider dell'elenco indirizzi IP bloccati.

I provider dell'elenco indirizzi IP bloccati possono restituire codici differenti per identificare il motivo per cui un indirizzo IP viene definito nei rispettivi elenchi. La maggior parte dei provider dell'elenco indirizzi IP bloccati restituisce dei tipi di dati maschera di bit o valore assoluto. All'interno di questi tipi di dati, il provider dell'elenco indirizzi IP bloccati può utilizzare più valori per classificare l'indirizzo IP in base al tipo di minaccia.

Quando si utilizzano i provider dell'elenco indirizzi IP bloccati è necessario considerare alcuni problemi:

  - Le interruzioni o i ritardi nel servizio provider dell'elenco indirizzi IP bloccati possono causare ritardi nell'elaborazione dei messaggi sul server Trasporto Edge. È necessario selezionare sempre dei provider dell'elenco indirizzi IP bloccati affidabili.

  - I server di origine noti come legittimi possono essere erroneamente identificati come origini di posta indesiderata. Ad esempio, il server di posta può essere configurato inavvertitamente per agire come inoltro aperto. È necessario selezionare sempre i provider dell'elenco indirizzi IP bloccati che forniscono procedura chiare per la valutazione e la rimozione dai relativi servizi.

Inizio pagina

## Esempi di maschere di bit e di valori assoluti

In questa sezione viene illustrato un esempio dei codici di stato restituiti dalla maggioranza dei provider degli elenchi di indirizzi bloccati. Per dettagli sui codici di stato restituiti dal provider, vedere la documentazione per il provider specifico.

Per i dati di tipo maschera di bit, il servizio provider dell'elenco indirizzi IP bloccati restituisce il codice di stato 127.0.0.*x*, dove il numero intero *x* indica uno dei valori elencati nella seguente tabella.

### Valori e codici di stato per i dati di tipo maschera di bit

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valore</th>
<th>Codice di stato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>L'indirizzo IP è contenuto in un elenco indirizzi IP bloccati.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>Il server SMTP è configurato per l'inoltro aperto.</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>L'indirizzo IP supporta un indirizzo IP di connessione remota.</p></td>
</tr>
</tbody>
</table>


Per i tipi di valore assoluto, il provider dell'elenco indirizzi IP bloccati restituisce risposte esplicite che definiscono il motivo per cui l'indirizzo IP viene definito nei relativi elenchi di blocco. Nella seguente tabella sono illustrati esempi di valori assoluti e risposte esplicite.

### Valori e codici di stato per i dati di tipo valore assoluto

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valore</th>
<th>Risposta esplicita</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>127.0.0.2</p></td>
<td><p>L'indirizzo IP è un'origine diretta di posta indesiderata.</p></td>
</tr>
<tr class="even">
<td><p>127.0.0.4</p></td>
<td><p>L'indirizzo IP è un mailer di posta inviata in blocco.</p></td>
</tr>
<tr class="odd">
<td><p>127.0.0.5</p></td>
<td><p>Il server remoto che invia il messaggio supporta gli inoltri aperti a più fasi.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Provider dell'elenco indirizzi IP consentiti

I provider dell'elenco indirizzi IP consentiti sono noti anche come *elenchi di indirizzi attendibili* o *white list*. I provider dell'elenco indirizzi IP consentiti sono configurati in modo identico ai provider dell'elenco indirizzi IP bloccati, tuttavia i risultati sono opposti: infatti, definiscono gli indirizzi IP dei server di posta che non sono associati in alcun modo ad attività di posta indesiderata. Se l'indirizzo IP del server di posta di connessione è definito in un provider dell'elenco indirizzi IP consentiti, il messaggio è esente dall'elaborazione da parte di altri agenti di protezione da posta indesiderata di Exchange. Per questa ragione, i provider dell'elenco indirizzi IP bloccati vengono utilizzati con maggiore frequenza rispetto ai provider dell'elenco indirizzi IP consentiti. Scegliere con attenzione i provider dell'elenco indirizzi IP consentiti.

Inizio pagina

## Test dei provider dell'elenco indirizzi IP bloccati e provider dell'elenco indirizzi IP consentiti

Dopo aver configurato il filtro connessioni in modo da utilizzare un provider dell'elenco indirizzi IP bloccati o un provider dell'elenco indirizzi IP consentiti, è possibile eseguire dei test per verificare che i provider funzionino correttamente. La maggior parte dei provider fornisce indirizzi IP di prova che è possibile utilizzare per eseguire il test dei loro servizi. Quando si esegue il test di un provider, l'agente Filtro connessioni esegue una query DNS che dovrebbe dare come risultato una risposta specifica dal provider. Per ulteriori informazioni sulla verifica degli indirizzi IP di un servizio provider dell'elenco indirizzi IP bloccati o dell'elenco indirizzi IP consentiti, vedere [Gestire il filtro connessioni su server Trasporto Edge](manage-connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

Inizio pagina

## Configurazione del filtro connessioni nei server Trasporto Edge che non sono connessi direttamente a Internet

È possibile utilizzare il filtro connessioni nei server Trasporto Edge che non ricevono direttamente la posta elettronica da Internet. In questo scenario, il computer su cui viene eseguito il ruolo del server Trasporto Edge si trova dietro un altro server di posta che riceve ed elabora i messaggi direttamente da Internet. Ad esempio, l'organizzazione potrebbe inviare traffico di posta tramite un server di protezione da posta indesiderata, un servizio o un dispositivo prima che il messaggio raggiunga il server Trasporto Edge. In questo scenario, l'agente Filtro connessioni deve estrarre l'indirizzo IP di origine corretto dal messaggio. A tale scopo, l'agente Filtro connessioni deve analizzare i valori del campo di intestazione **Ricevuto** nell'intestazione del messaggio e confrontarli con gli indirizzi IP noti del server di posta ubicato tra il server Trasporto Edge e Internet.

Ogni server di posta elettronica che accetta e inoltra un messaggio SMTP nel percorso di recapito, aggiunge il proprio campo intestazione **Ricevuto** nell'intestazione del messaggio. L'intestazione **Ricevuto** del messaggio in genere contiene il nome di dominio e l'indirizzo IP del server di posta che ha elaborato il messaggio.

Se il server Trasporto Edge non accetta il messaggio direttamente da Internet, è necessario utilizzare il parametro *InternalSMTPServers* nel cmdlet **Set-TransportConfig** di un server Exchange 2013 Cassette postali per identificare l'indirizzo IP del server di posta ubicato tra il server Trasporto Edge e Internet. I dati relativi agli indirizzi IP vengono replicati nei server Trasporto Edge da EdgeSync. Quando vengono ricevuti i messaggi dal server Trasporto Edge, l'agente Filtro connessioni presume che l'indirizzo IP di origine che deve essere verificato sia un indirizzo IP in un campo intestazione **Ricevuto** che non corrisponde a un valore specificato dal parametro *InternalSMTPServers*. Pertanto, per consentire il corretto funzionamento del filtro connessioni, è necessario specificare tutti i server SMTP interni.

Inizio pagina


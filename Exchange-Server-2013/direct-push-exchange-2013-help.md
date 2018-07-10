---
title: 'Direct Push: Exchange 2013 Help'
TOCTitle: Direct Push
ms:assetid: 373c1629-3d4b-4828-b014-9e103de4ef25
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997252(v=EXCHG.150)
ms:contentKeyID: 50480415
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Direct Push

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-07-11_

Direct Push è una funzionalità incorporata in Microsoft Exchange Server 2013. Direct Push consente di mantenere aggiornato un dispositivo mobile attraverso la connessione alla rete di telefonia cellulare o wireless. Informa il dispositivo mobile quando c'è un nuovo contenuto pronto per la sincronizzazione.

**Sommario**

Panoramica

Direct Push topology

Configuring Direct Push to work through your firewall

## Panoramica

Per utilizzare Direct Push, è necessario che il dispositivo mobile supporti questa funzionalità. Ad esempio:

  - Tutte le versioni di Windows Phone

  - Telefoni cellulari prodotti da licenziatari di Microsoft Exchange ActiveSync e progettati specificatamente per essere compatibili con Direct Push

Per impostazione predefinita, la funzionalità Direct Push è abilitata in Exchange 2013. I dispositivi mobili che supportano tale funzionalità inviano una richiesta HTTPS di lunga durata al server che esegue Microsoft Exchange. Il server Exchange monitora l'attività sulla cassetta postale dell'utente e invia una risposta al dispositivo mobile in caso di modifiche, quali messaggi di posta elettronica, attività ed elementi di calendario o di contatto nuovi o modificati. Se vengono apportate modifiche durante l'intervallo di tempo della richiesta HTTPS, il server Exchange invia una risposta al dispositivo in cui viene indicato che sono state apportate modifiche e che il dispositivo deve iniziare la sincronizzazione con il server Exchange. Il dispositivo invia quindi una richiesta al server. Al termine della sincronizzazione, viene generata una nuova richiesta HTTPS di lunga durata per avviare nuovamente il processo. Ciò garantisce un recapito rapido degli elementi disponibili nella posta elettronica, in Calendario, Contatti e Attività al dispositivo mobile e una sincronizzazione continua del dispositivo con il server Exchange.

## Topologia Direct Push

Direct Push funziona nel modo seguente:

1.  Un dispositivo mobile configurato per la sincronizzazione con un server Exchange 2013 invia una richiesta HTTPS al server. La richiesta è nota come PING. La richiesta indica al server di notificare al dispositivo eventuali modifiche avvenute nelle cartelle configurate per essere sincronizzate entro i successivi 15 minuti. Altrimenti, il server deve restituire il messaggio HTTP 200 OK. Il dispositivo mobile entrerà in modalità standby. L'intervallo di tempo di 15 minuti è noto come *intervallo di heartbeat*.

2.  Se durante i 15 minuti non viene modificato alcun elemento, il server restituisce la risposta HTTP 200 OK. Il dispositivo mobile riceve questa risposta, riprende l'attività (il cosiddetto *waking up*) e invia nuovamente la richiesta. Ciò consente di riavviare il processo.

3.  Se durante i 15 minuti dell'intervallo di heartbeat vengono modificati alcuni elementi o se ne ricevono di nuovi, il server invia una risposta che informa il dispositivo mobile della disponibilità di un elemento nuovo o modificato e comunica il nome della cartella in cui risiede tale elemento. Dopo aver ricevuto questa risposta, il dispositivo mobile invia una richiesta di sincronizzazione per la cartella in cui è presente l'elemento modificato o nuovo. Al termine della sincronizzazione, il dispositivo mobile invia una nuova richiesta PING e l'intero processo viene nuovamente avviato.

Direct Push dipende dalle condizioni della rete che supporta la richiesta HTTPS di lunga durata. Se la rete portante per il dispositivo mobile o il firewall non supporta richieste HTTPS di lunga durata, la richiesta HTTPS viene interrotta. I passi seguenti descrivono il funzionamento di Direct Push quando la rete portante per un dispositivo mobile ha un valore di timeout di 13 minuti.

1.  Un dispositivo mobile invia una richiesta HTTPS al server. La richiesta indica al server di notificare al dispositivo eventuali modifiche avvenute nelle cartelle configurate per essere sincronizzate entro i successivi 15 minuti. Altrimenti, il server deve restituire il messaggio HTTP 200 OK. Il dispositivo mobile entrerà in modalità standby.

2.  Se il server non risponde dopo 15 minuti, il dispositivo mobile esegue il waking up e deduce che la connessione è stata interrotta dalla rete. Il dispositivo invia nuovamente la richiesta HTTPS, ma questa volta viene utilizzato un intervallo di heartbeat di 8 minuti.

3.  Dopo 8 minuti il server invia il messaggio HTTP 200 OK. Il dispositivo tenterà di ottenere una connessione più lunga inviando una nuova richiesta HTTPS al server con un intervallo di heartbeat di 12 minuti.

4.  Dopo 4 minuti, viene ricevuto un nuovo messaggio di posta elettronica e il server risponde inviando una richiesta HTTPS che indica al dispositivo di eseguire la sincronizzazione. Il dispositivo esegue la sincronizzazione e invia nuovamente la richiesta HTTPS con un intervallo di heartbeat di 12 minuti.

5.  Dopo 12 minuti, se non sono disponibili elementi nuovi o modificati, il server risponde inviando il messaggio HTTP 200 OK. Il dispositivo esegue il waking up e deduce che le condizioni della rete supportano un intervallo di heartbeat di 12 minuti. Il dispositivo tenterà di ottenere una connessione più lunga inviando una nuova richiesta HTTPS con un intervallo di heartbeat di 16 minuti.

6.  Dopo 16 minuti, non viene ricevuta risposta dal server. Il dispositivo esegue il waking up e deduce che le condizioni di rete non sono in grado di supportare un intervallo di heartbeat di 16 minuti. Poiché questo errore si è verificato direttamente dopo il tentativo di aumentare l'intervallo di heartbeat, il dispositivo conclude che l'intervallo di heartbeat ha raggiunto il limite massimo. Il dispositivo invia quindi una richiesta HTTPS con un intervallo di 12 minuti poiché questo è stato l'ultimo intervallo di heartbeat corretto.

Il dispositivo mobile tenta di utilizzare l'intervallo di heartbeat più lungo supportato dalla rete. Questo consente di prolungare la durata della batteria del dispositivo e di ridurre la quantità di dati trasferiti in rete. Le portanti per i dispositivi mobili possono specificare un valore di heartbeat massimo, minimo e iniziale nelle impostazioni del Registro di sistema per il dispositivo mobile.

## Configurazione di Direct Push per il funzionamento con il firewall

Per utilizzare Direct Push con il firewall, è necessario aprire la porta TCP 443. Questa porta è necessaria per SSL (Secure Sockets Layer) e deve essere aperta tra Internet e il server Accesso client.

Oltre ad aprire le porte sul firewall, per un funzionamento corretto di Direct Push, è necessario aumentare il valore di timeout sul firewall, modificando il valore predefinito di 15 minuti su 30 minuti. La lunghezza massima della richiesta HTTPS è determinata dalle seguenti impostazioni:

  - Il valore di timeout massimo impostato sui firewall che controllano il traffico da Internet al server Accesso client

  - I valori di timeout del firewall impostati dall'operatore di telefonia mobile


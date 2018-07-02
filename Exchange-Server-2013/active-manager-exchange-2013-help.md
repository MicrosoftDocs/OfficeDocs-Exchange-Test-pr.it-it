---
title: 'Active Manager: Exchange 2013 Help'
TOCTitle: Active Manager
ms:assetid: f4be27b7-1d7c-47b4-87ac-bfdfcc046f00
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd776123(v=EXCHG.150)
ms:contentKeyID: 50482064
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Manager

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Microsoft Exchange Server 2013 include un componente denominato *Active Manager* che gestisce una piattaforma a disponibilità elevata che comprende il gruppo di disponibilità del database (DAG) e le copie del database delle cassette postali. Active Manager viene eseguito all'interno del servizio di replica di Microsoft Exchange (MSExchangeRepl.exe) su tutti i server Cassette postali. Nei server Cassette postali che non sono membri di un gruppo di disponibilità del database (DAG), è disponibile un unico ruolo di Active Manager: *Active Manager autonomo*. Nei server membri di un gruppo di disponibilità del database (DAG), sono disponibili due ruoli di Active Manager: *Active Manager principale* (PAM) e *Active Manager di standby* (SAM). PAM è il ruolo Active Manager in un gruppo di disponibilità del database che decide quali copie sono attive o passive. PAM è responsabile del recupero delle notifiche di cambiamento della tecnologia e della risposta agli errori del server. Il membro del gruppo di disponibilità del database che contiene il ruolo PAM è sempre il membro che possiede attualmente la risorsa quorum del cluster (gruppo di cluster predefinito). Se il server che possiede la risorsa quorum del cluster incontra un errore, il ruolo PAM passa automaticamente a un server ancora attivo, che assume la proprietà della risorsa quorum del cluster. Inoltre, se è necessario scollegare il server che ospita la risorsa quorum del cluster per ragioni di manutenzione o di aggiornamento, è necessario spostare prima il PAM in un altro server del gruppo di disponibilità del database. Il PAM controlla tutti gli spostamenti delle designazioni attive tra le copie di un database. (Può essere attiva una sola copia in un dato momento e può essere montata o smontata.) Il PAM esegue anche le funzioni del ruolo SAM sul sistema locale (rilevamento degli errori del database locale e dell'Archivio informazioni locale).

Il SAM fornisce informazioni sul server che ospita la copia attiva di un database delle cassette postali agli altri componenti di Exchange che eseguono un componente client Active Manager (ad esempio, i servizi Accesso client RPC o Trasporto). Il SAM rileva gli errori dei database locali e dell'Archivio informazioni locale. Per rispondere a tali errori richiede al PAM l'avvio di un failover (se il database è replicato). Un SAM non determina la destinazione del failover e non aggiorna lo stato della posizione del database nel PAM. Accede allo stato della posizione della copia attiva del database solo per rispondere alle query ricevute in relazione alla copia attiva del database.


> [!NOTE]
> Exchange 2013 non è un'applicazione in cluster. Utilizza invece le funzioni della libreria cluster implementata in clusapi.dll per le funzioni di cluster, gruppi, reti di cluster (heartbeat), gestione dei nodi, registri del cluster e alcune funzioni del codice di controllo. Inoltre, Active Manager archivia le informazioni del database delle cassette postali corrente (ad esempio i dati attivi e passivi e i dati installati) nel database cluster (noto anche come registro cluster). Anche se le informazioni sono archiviate direttamente nel database cluster, gli altri componenti non possono accedervi direttamente.



In Exchange 2013, il servizio di replica di Microsoft Exchange consente di controllare periodicamente l'integrità di tutti i database montati. Inoltre, controlla ESE (Extensible Storage Engine) alla ricerca di errori di I/O. Se il servizio rileva un errore, viene inviata una notifica ad Active Manager. che determina quale copia del database dovrebbe essere montato e quali sono i requisiti per il montaggio di tale database. Inoltre, tiene traccia della copia attiva di un database delle cassette postali (basandosi sull'ultima copia montata del database) e fornisce le informazioni sui risultati della verifica al server Accesso client a cui è connesso il client.

## Processo di selezione della copia migliore

Quando si verifica un errore che impedisce l'accesso alla copia attiva di un database delle cassette postali replicato, Active Manager esegue la procedura di risoluzione del problema selezionando per l'attivazione la miglior copia passiva del database in cui si è verificato l'errore. Questo processo era noto come Processo di selezione della copia migliore (BCS, Best Copy Selection) in Exchange 2010 e attualmente è denominato Copia e selezione server migliori (BCSS, Best Copy and Server Selection) in Exchange 2013. Il processo generale ha luogo nel seguente ordine:

1.  La disponibilità gestita o Active Manager rilevano un errore, oppure un amministratore avvia un passaggio senza destinazione.

2.  PAM esegue l'algoritmo interno BCSS.

3.  Viene eseguito un processo denominato *Tenta copia ultimi log* (Attempt Copy Last Logs, ACLL) che cerca di copiare i file di log mancanti dal server che ha ospitato la copia attiva del database prima dell'errore o del passaggio.

4.  Una volta completato il processo ACLL, il valore di *AutoDatabaseMountDial* per i server delle cassette postali che ospitano le copie del database viene confrontato con la lunghezza della coda di copia del database da attivare. A questo punto, è possibile uno dei due eventi indicati di seguito:
    
      - il numero di file di log mancanti è uguale o inferiore al valore di *AutoDatabaseMountDial*, nel qual caso procedere con il passaggio 5.
    
      - il numero di file di log mancanti è superiore al valore di *AutoDatabaseMountDial*, nel qual caso Active Manager tenterà di attivare la miglior copia disponibile successiva, se ne esiste una.

5.  PAM invia una richiesta di montaggio all'archivio informazioni di Microsoft Exchange tramite la chiamata di procedura remota (Remote Procedure Call, RPC). A questo punto, è possibile uno dei due eventi indicati di seguito:
    
      - Il database viene montato ed è disponibile per i client.
    
      - Il database non viene montato e il PAM esegue i passaggi 3 e 4 sulla migliore copia successiva (se disponibile).

In Exchange 2010, il processo di servizi di integrazione Applicativa valutati vari aspetti di ogni copia del database per determinare la migliore copia da attivare. Queste inclusi:

  - Lunghezza coda di copia

  - Lunghezza coda di riproduzione

  - Stato del database

  - Stato dell'indice del contenuto

In Exchange 2013, Active Manager viene eseguito per tutti gli stessi controlli e fasi BCS, ma ora include anche l'uso del vincolo di ordine decrescente degli stati di integrità. In particolare, BCSS include alcuni nuovi controlli di integrità che fanno parte dei componenti di monitoraggio incorporati nella disponibilità gestita in Exchange 2013. Sono presenti quattro nuovi controlli eseguiti da Gestione attiva (elencati nell'ordine in cui vengono eseguiti):

1.  **All Healthy**   Verifica la presenza di un server che ospita una copia del database interessato con tutti i componenti di monitoraggio in uno stato integro.

2.  **Up to Normal Healthy**   Verifica la presenza di un server che ospita una copia del database interessato con tutti i componenti di monitoraggio con priorità Normale in uno stato integro.

3.  **All Better than Source**   Verifica la presenza di un server che ospita una copia del database interessato con i componenti di monitoraggio in uno stato migliore del server corrente che ospita la copia interessata.

4.  **Same as Source**   Verifica la presenza di un server che ospita una copia del database interessato con i componenti di monitoraggio in uno stato equivalente a quello del server corrente che ospita la copia interessata.

Se BCSS viene richiamato come risultato di un failover attivato da un componente di monitoraggio (ad esempio, tramite un risponditore Failover), verrà imposto un vincolo obbligatorio aggiuntivo laddove l'integrità del componente del server di destinazione deve essere migliore di quella del server in cui si è verificato il failover. Ad esempio, se un errore di Microsoft Office Outlook Web App provoca un failover tramite il risponditore Failover, BCSS dovrà selezionare un server che ospita una copia del database interessato in cui Outlook Web App è integro.

## Processo di selezione della copia migliore

Per quanto riguarda gli errori di database (non gli errori di protocollo), Active Manager in Exchange 2013 esegue gli stessi controlli eseguiti in Exchange 2010. Active Manager inizia il processo di selezione della copia migliore creando un elenco di copie del database che sono potenziali candidati all'attivazione. Tutte le copie di database non raggiungibili o bloccate a livello amministrativo vengono ignorate e non utilizzate durante il processo di selezione. L'ordine dell'elenco dipende dal valore di *AutoDatabaseMountDial*:

  - Se il parametro *AutoDatabaseMountDial* è configurato con un valore diverso da `Lossless` su tutti i server che ospitano una copia del database, Active Manager ordinerà l'elenco risultante utilizzando la lunghezza della coda di copia come chiave primaria. Il calcolo è basato su LastLogInspected (dal punto di vista della copia), pertanto l'elenco di copie potenziali viene ordinato in base al valore più alto per LastLogInspected (che sarà la copia con la lunghezza di coda più bassa). Se necessario, Active Manager ordinerà l'elenco una seconda volta, utilizzando il valore di preferenza di attivazione come chiave secondaria per interrompere eventuali condizioni equivalenti laddove due o più copie passive presentino code di copia con la stessa lunghezza. La copia con il valore di preferenza di attivazione più basso avrà la priorità più alta nell'elenco.

  - Se il parametro *AutoDatabaseMountDial* è configurato con un valore diverso di `Lossless` su qualsiasi server che ospita una copia del database, Active Manager ordinerà l'elenco risultante in ordine crescente utilizzando il valore di preferenza di attivazione come chiave primaria. Inoltre, quando un amministratore esegue un passaggio di server o di database senza perdita di dati non specificando alcuna destinazione, Active Manager ordinerà anche l'elenco risultante in ordine crescente utilizzando il valore di preferenza di attivazione come chiave primaria.

Di seguito, Active Manager tenta di individuare nell'elenco una copia delle cassette postali del database con stato Healthy, DisconnectedAndHealthy, DisconnectedAndResynchronizing o SeedingSource, quindi valuta la potenziale attivazione di ogni copia dell'elenco utilizzando un ordine impostato di dieci criteri. Active Manager determina se uno dei candidati all'attivazione soddisfa il primo set di criteri:

  - Dispone di un indice del contenuto con stato Healthy.

  - Presenta una lunghezza della coda di copia inferiore a 10 file di registro.

  - Presenta una lunghezza della coda di riesecuzione inferiore a 50 file di log.

Se nessuna delle copie del database soddisfa il primo set di criteri, Active Manager cerca di individuare una copia del database in grado di soddisfare il set di criteri successivo:

  - Dispone di un indice del contenuto con stato Crawling.

  - Presenta una lunghezza della coda di copia inferiore a 10 file di registro.

  - Presenta una lunghezza della coda di riesecuzione inferiore a 50 file di log.

Se nessuna delle copie del database soddisfa il secondo set di criteri, Active Manager cerca di individuare una copia del database in grado di soddisfare il terzo set di criteri:

  - Dispone di un indice del contenuto con stato Healthy.

  - Presenta una lunghezza della coda di riesecuzione inferiore a 50 file di log.

Se nessuna delle copie del database soddisfa il terzo set di criteri, Active Manager cerca di individuare una copia del database in grado di soddisfare il quarto set di criteri:

  - Dispone di un indice del contenuto con stato Crawling.

  - Presenta una lunghezza della coda di riesecuzione inferiore a 50 file di log.

Se nessuna delle copie del database soddisfa il quarto set di criteri, Active Manager cerca di individuare una copia del database in grado di soddisfare il quinto set di criteri:

  - Presenta una lunghezza della coda di riesecuzione inferiore a 50 file di log.

Se nessuna delle copie del database soddisfa il quinto set di criteri, Active Manager cerca di individuare una copia del database in grado di soddisfare il sesto set di criteri:

  - Dispone di un indice del contenuto con stato Healthy.

  - Presenta una lunghezza della coda di copia inferiore a 10 file di registro.

Se nessuna delle copie del database soddisfa il sesto set di criteri, Active Manager cerca di individuare una copia del database in grado di soddisfare il settimo set di criteri:

  - Dispone di un indice del contenuto con stato Crawling.

  - Presenta una lunghezza della coda di copia inferiore a 10 file di registro.

Se nessuna delle copie del database soddisfa il settimo set di criteri, Active Manager cerca di individuare una copia del database in grado di soddisfare l'ottavo set di criteri:

  - Dispone di un indice del contenuto con stato Healthy.

Se nessuna delle copie del database soddisfa l'ottavo set di criteri, Active Manager cerca di individuare una copia del database in grado di soddisfare il nono set di criteri:

  - Dispone di un indice del contenuto con stato Crawling.

Se nessuna delle copie del database soddisfa il nono set di criteri, Active Manager cerca di attivare una qualsiasi copia del database con stato Healthy, DisconnectedAndHealthy, DisconnectedAndResynchronizing o SeedingSource (il decimo set di criteri). Se non sono disponibili copie del database in grado disoddisfare il decimo set di criteri. non viene attivata automaticamente alcuna copia del database.

Una volta individuate una o più copie in grado di soddisfare uno o più set di criteri, viene eseguito il processo ACLL per copiare i file di log dall'origine alla potenziale nuova copia attiva. Una volta completato il processo ACLL, il PAM invia una richiesta di montaggio e il database viene montato ed è di nuovo disponibile per i client, oppure non viene montato e il PAM cerca la copia migliore successiva (se disponibile).


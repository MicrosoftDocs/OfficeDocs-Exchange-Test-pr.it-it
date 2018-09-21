---
title: 'Passaggi centro dati: Exchange 2013 Help'
TOCTitle: Passaggi centro dati
ms:assetid: ac208c12-04d0-4809-bacd-72478ff14983
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351049(v=EXCHG.150)
ms:contentKeyID: 62523892
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Passaggi centro dati

 

_**Si applica a:** Exchange Server 2013 SP1_

_**Ultima modifica dell'argomento:** 2016-03-17_

In una configurazione con resilienza del sito, in caso di errore a livello di sito può verificarsi il ripristino automatico all'interno del gruppo di disponibilità del database, consentendo al sistema di messaggistica di rimanere in uno stato funzionale. Tale configurazione richiede almeno tre posizioni, dato che richiede la distribuzione dei membri del gruppo di disponibilità del database in due posizioni e del server di controllo del gruppo di disponibilità del database in una terza posizione.

Se non si dispone di tre posizioni, o anche nel caso in cui si disponga di tre posizioni, ma si desidera controllare le azioni di ripristino a livello di centro dati, è possibile configurare un gruppo di disponibilità del database per il ripristino manuale in caso di un errore del sito. In tal caso, sarà necessario effettuare un processo chiamato *switchover del datacenter*. Come per molti scenari di ripristino di emergenza, la pianificazione e preparazione anticipata di uno switchover del datacenter può semplificare il processo e ridurre la durata dell'interruzione.

Sono disponibili quattro passaggi di base da completare per eseguire lo switchover del centro dati, una volta deciso di attivare il secondo centro dati:

1.  **Terminare un datacenter in esecuzione parzialmente**   Questo passaggio implica la terminazione dei servizi di Exchange del datacenter principale, se ancora in esecuzione. Si tratta di un passaggio particolarmente importante per il ruolo del server Cassette postali, in quanto utilizza un modello attivo/passivo a disponibilità elevata. Se i servizi in un centro dati parzialmente danneggiato non vengono arrestati, è possibile che i problemi derivanti da tale centro dati influiscano negativamente sui servizi quando si ripete uno switchover sul centro dati principale.
    

    > [!IMPORTANT]
    > Se conseguentemente all'errore del centro dati principale è stata compromessa l'affidabilità dell'infrastruttura di Active Directory&nbsp;o della rete,&nbsp;si consiglia di disattivare tutti i servizi di messaggistica fino a quando non viene ripristinato il servizio di integrità delle dipendenze.



2.  **Convalidare e confermare i prerequisiti per il secondo centro dati**   Questo passaggio può essere eseguito parallelamente al passaggio 1 in quanto la convalida dell'integrità delle dipendenze dell'infrastruttura nel secondo centro dati dipende fortemente dai servizi del primo centro dati. Ogni organizzazione richiede, in genere, il proprio metodo per l'esecuzione di questo passaggio. Ad esempio, è possibile decidere di completare questo passaggio esaminando le informazioni sull'integrità raccolte e filtrate da un'applicazione di monitoraggio dell'infrastruttura oppure utilizzando uno strumento univoco per l'infrastruttura dell'organizzazione. Si tratta di un passaggio fondamentale, in quanto l'attivazione di un secondo centro dati con un'infrastruttura danneggiata e instabile è probabile che restituisca scarsi risultati.

3.  **Attivare i server Cassette postali**   Questo passaggio avvia il processo di attivazione del secondo centro dati e può essere eseguito parallelamente al passaggio 4 in quanto i servizi di Microsoft Exchange possono gestire le interruzioni del database ed eseguire il ripristino. L'attivazione dei server Cassette postali implica un processo atto a rendere non disponibili i server danneggiati del centro dati principale seguito dall'attivazione dei server nel secondo centro dati. Il processo di attivazione per i server Cassette postali dipende dal fatto che il gruppo di disponibilità del database sia o meno in modalità di coordinazione dell'attivazione del database (DAC, database activation coordination). Per ulteriori informazioni sulla modalità di coordinazione dell'attivazione del database, vedere [modalità di coordinamento dell'attivazione del centro dati](datacenter-activation-coordination-mode-exchange-2013-help.md).
    
    Se il gruppo di disponibilità del database è in modalità di coordinazione dell'attivazione del database è possibile utilizzare i cmdlet di resilienza del sito di Exchange per terminare un centro dati parzialmente danneggiato (se necessario) e attivare i server Cassette postali. Ad esempio, in modalità di coordinazione dell'attivazione del database, questo passaggio viene eseguito mediante il cmdlet [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd335133\(v=exchg.150\)). In alcuni casi, i server devono essere contrassegnati come non disponibili due volte (una in ogni centro dati). Quindi, viene eseguito il cmdlet [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd351169\(v=exchg.150\)) per ripristinare i rimanenti membri del gruppo di disponibilità del database nel secondo centro dati riducendo i membri del gruppo di disponibilità del database a quelli ancora operativi, ristabilendo, di conseguenza, il quorum. Se il gruppo di disponibilità del database non è in modalità di coordinazione dell'attivazione del database, è necessario utilizzare gli strumenti cluster di failover di Windows per attivare i server Cassette postali. Una volta completato uno di questi processi, le copie del database precedentemente passive nel secondo centro dati possono diventare attive ed essere montate. Viene completato il ripristino del server Cassette postali. A questo punto, il ripristino del server Cassette postali è completo.

4.  **Attivare i server Accesso client**   Ciò implica l'uso delle informazioni di mapping di URL e della metodologia di modifica del DNS per l'esecuzione di tutti gli aggiornamenti DNS richiesti. Le informazioni di mapping illustrano le modifiche del DNS da eseguire. La quantità di tempo richiesta per il completamento dell'aggiornamento dipende dalla metodologia utilizzata e dalle impostazioni TTL sul record DNS (e se l'infrastruttura di distribuzione rispetta il valore TTL).

Gli utenti dovrebbero iniziare ad avere accesso saltuario ai servizi di messaggistica unificata una volta completati i passaggi 3 e 4. I passaggi 3 e 4 vengono descritti dettagliatamente più avanti in questo argomento.

**Sommario**

Terminating a Partially Failed Datacenter

Activating Mailbox Servers

Activating Other Server Roles

Restoring Service to the Primary Datacenter

Reestablishing Site Resilience

## Interruzione di un centro dati parzialmente danneggiato

Se nel centro dati danneggiato sono ancora in esecuzione membri del gruppo di disponibilità del database, è necessario terminarli.

Quando il gruppo di disponibilità del database è in modalità di coordinazione dell'attivazione del database, per terminare i membri del gruppo di disponibilità del database ancora attivi nel centro dati principale, eseguire le operazioni specifiche riportate di seguito:

1.  I membri del gruppo di disponibilità del database nel centro dati principale devono essere contrassegnati come arrestati nel centro dati principale. *Arrestato* è uno stato di Active Manager che impedisce il montaggio dei database. Tale stato di Active Manager viene attivato utilizzando il cmdlet [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd335133\(v=exchg.150\)) in ogni server del datacenter danneggiato. È possibile utilizzare il parametro *ActiveDirectorySite* di questo cmdlet per contrassegnare tutti i server del centro dati principale come arrestati utilizzando un singolo comando. Tale passaggio potrebbe non essere consentito a seconda del tipo di errore e dovrebbe essere eseguito solo se consentito dallo stato del centro dati. Il cmdlet **Stop-DatabaseAvailabilityGroup** dovrebbe essere eseguito su tutti i server del centro dati principale. Se il server Cassette postali non è disponibile ma sul centro dati principale è in esecuzione Active Directory, il comando **Stop-DatabaseAvailabilityGroup** con il parametro *ConfigurationOnly* deve essere eseguito su tutti i server del centro dati principale che si trovano in questo stato oppure è necessario disattivare il server Cassette postali. Un errore durante la disattivazione dei server Cassette postali nel centro dati danneggiato o l'esecuzione del comando **Stop-DatabaseAvailabilityGroup** sui server può comportare la possibilità che si verifichi la sindrome split brain sui due centri dati. Potrebbe essere necessario disattivare singolarmente i computer tramite i dispositivi di risparmio energia per soddisfare questo requisito.

2.  È ora necessario aggiornare il secondo centro dati per indicare i server del centro dati principale che sono stati arrestati. Tale operazione viene effettuata eseguendo lo stesso comando **Stop-DatabaseAvailabilityGroup** con il parametro *ConfigurationOnly*, utilizzando lo stesso parametro *ActiveDirectorySite* e specificando il nome del sito Active Directory nel centro dati principale danneggiato. Lo scopo di questo passo è di informare i server del secondo centro dati su quali sono i server Cassette postali disponibili per l'uso durante il servizio di ripristino.

Quando il gruppo di disponibilità del database non è in modalità di coordinazione dell'attivazione del database, per terminare i membri del gruppo di disponibilità del database ancora attivi nel centro dati principale, eseguire le operazioni specifiche riportate di seguito:

1.  I membri del gruppo di disponibilità del database nel centro dati devono essere rimossi forzatamente dal cluster sottostante del gruppo di disponibilità del database eseguendo i comandi seguenti su ogni membro:
    
    ```powershell
net stop clussvc
```
        cluster <DAGName> node <DAGMemberName> /forcecleanup

2.  I membri del gruppo di disponibilità del database nel secondo centro dati devono essere riavviati e utilizzati per completare il processo di rimozione dal secondo centro dati. Arrestare il servizio Cluster su ogni membro del gruppo di disponibilità del database nel secondo centro dati eseguendo il comando seguente su ogni membro:
    
    ```powershell
net stop clussvc
```

3.  Su un membro del gruppo di disponibilità del database nel secondo centro dati, forzare un avvio del quorum sul servizio Cluster eseguendo il comando seguente:
    
    ```powershell
net start clussvc /forcequorum
```

4.  Aprire lo strumento Gestione cluster di failover e connettersi al cluster sottostante del gruppo di disponibilità del database. Espandere il cluster, quindi espandere **Nodi**. Fare clic con il pulsante destro del mouse su ogni nodo nel centro dati, selezionare **Altre azioni**, quindi **Rimuovi**. Dopo aver effettuato la rimozione dei membri del gruppo di disponibilità del database nel centro dati principale, chiudere lo strumento Gestione cluster di failover.

Inizio pagina

## Attivazione dei server Cassette postali

I passaggi richiesti per attivare i server Cassette postali durante lo switchover di un centro dati dipende anche dal fatto che il gruppo di disponibilità del database sia in modalità di coordinazione dell'attivazione del database. Prima di attivare i membri del gruppo di disponibilità del database nel secondo centro dati, è opportuno assicurarsi che i servizi di infrastruttura nel secondo centro dati siano pronti per l'attivazione del servizio di messaggistica.

Di seguito, è riportata la procedura per il completamento dell'attivazione dei server Cassette postali nel secondo centro dati, quando il gruppo di disponibilità del database è in modalità di coordinazione dell'attivazione del database:

1.  È necessario arrestare il servizio Cluster su ciascun membro del gruppo di disponibilità del database nel secondo centro dati. È possibile utilizzare il cmdlet **Stop-Service** per arrestare il servizio (ad esempio, `Stop-Service ClusSvc`) oppure utilizzare `net stop clussvc` da un prompt dei comandi elevato.

2.  I server Cassette postali nel datacenter di standby vengono quindi attivati utilizzando il cmdlet [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd351169\(v=exchg.150\)). Il sito Active Directory del centro dati di standby viene trasmesso al cmdlet **Restore-DatabaseAvailabilityGroup** per l'identificazione dei server da utilizzare per il ripristino del servizio e per configurare il DAG per l'utilizzo di un server di controllo alternativo. Se il server di controllo alternativo non è stato preconfigurato, può essere configurato utilizzando i parametri *AlternateWitnessServer* e *AlternateWitnessDirectory* del cmdlet [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd351169\(v=exchg.150\)). Se si utilizza tale comando, i criteri del quorum vengono compressi nei server del centro dati di standby. Se il numero di server in quel centro dati è un numero pari, verrà attivato il gruppo di disponibilità del database mediante l'uso del server di controllo alternativo come identificato dall'impostazione dell'oggetto gruppo di disponibilità del database.

3.  È ora possibile attivare il database. A seconda della configurazione specifica utilizzata dall'organizzazione, tale operazione potrebbe non avvenire automaticamente. Se i server nel centro dati di standby dispongono di un'impostazione di attivazione bloccata, il sistema non eseguirà un failover automatico dal centro dati principale a quello di standby di qualsiasi database. Se non vi sono restrizioni di failover per le copie del database nel centro dati di standby, il sistema attiverà le copie nel secondo centro dati presumendone l'integrità. Se i database sono configurati con un'impostazione di attivazione bloccata che richiede un'azione manuale esplicita, è possibile scegliere fra due opzioni:
    
    1.  Eliminare l'impostazione che blocca l'attivazione. In questo modo, verrà ripristinato il comportamento predefinito del sistema, ossia quello di attivare tutte le copie disponibili.
    
    2.  Lasciare invariata l'impostazione e utilizzare il cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/it-it/library/dd298068\(v=exchg.150\)) per completare l'attivazione del database nel secondo centro dati. Per completare tale passo utilizzando il cmdlet **Move-ActiveMailboxDatabase** quando è impostato il blocco dell'attivazione, è necessario identificare in modo esplicito la destinazione dello spostamento.

4.  L'ultimo passo è di esaminare tutti gli errori e i messaggi di avviso derivanti dalle attività. Tutti gli avvisi indicati devono essere esaminati e corretti. Il modello di progettazione dell'attività per questi comandi prevede una mancata riuscita solo se le attività non riescono a raggiungere lo scopo principale della propria progettazione. Ad esempio, il cmdlet **Restore-DatabaseAvailabilityGroup** avrà esito negativo se non può comprimere il quorum del gruppo di disponibilità del database per consentire il riavvio di un server nel secondo centro dati per l'elaborazione senza che venga interrotto il quorum. Tuttavia, l'output di ciascuna attività viene utilizzato anche per identificare i problemi che richiedono un completamento da parte dell'amministratore. Si consiglia di salvare l'output di tutte le attività e di riesaminarlo per le azioni successive.

Di seguito, è riportata la procedura per il completamento dell'attivazione dei server Cassette postali nel secondo centro dati, quando il gruppo di disponibilità del database non è in modalità di coordinazione dell'attivazione del database:

1.  Il quorum deve essere modificato in base al numero di membri del gruppo di disponibilità del database presenti nel secondo centro dati.
    
    1.  Se è presente un numero dispari di membri del gruppo di disponibilità del database, modificare il modello di quorum del gruppo di disponibilità del database da maggioranza dei nodi e delle condivisioni file a maggioranza dei nodi eseguendo il comando seguente:
        
        ```powershell
cluster <DAGName> /quorum /nodemajority
```
    
    2.  Se è presente un numero pari di membri del gruppo di disponibilità del database, riconfigurare il server e la directory di controllo eseguendo il comando seguente in Exchange Management Shell:
        
        ```powershell
Set-DatabaseAvailabilityGroup <DAGName> -WitnessServer <ServerName>
```

2.  Avviare il servizio Cluster su ogni membro del gruppo di disponibilità del database rimanente nel secondo centro dati eseguendo il comando seguente:
    
    ```powershell
net start clussvc
```

3.  Eseguire switchover del server per attivare i database delle cassette postali nel gruppo di disponibilità del database eseguendo il comando seguente per ogni membro del gruppo di disponibilità del database:
    
        Move-ActiveMailboxDatabase -Server <DAGMemberinPrimarySite> -ActivateOnServer <DAGMemberinSecondSite>

4.  Montare i database delle cassette postali in ogni membro del gruppo di disponibilità del database eseguendo il comando seguente:
    
    ```powershell
Get-MailboxDatabase <DAGMemberinSecondSite> | Mount-Database
```

Inizio pagina

## Attivazione dei server Accesso client

I client si connettono agli endpoint del servizio (ad esempio Outlook Web App, servizio di individuazione automatica, Exchange ActiveSync, Outlook via Internet, POP3, IMAP4 e l'array del server Accesso client per la chiamata di procedura remota) per accedere ai dati e ai servizi Exchange. Di conseguenza, l'attivazione dei server Accesso client comporta la modifica del mapping dei record DNS per gli endpoint del servizio, dagli indirizzi IP del centro dati principale agli indirizzi IP del secondo centro dati, configurati come nuovi endpoint del servizio. In base alla configurazione del DNS, i record DNS che è necessario modificare possono trovarsi o meno nella stessa zona DNS.

## Attivazione dei server Accesso client

I client si connetteranno automaticamente ai nuovi endpoint del servizio in uno dei due modi riportati di seguito:

  - I client continueranno a tentare la connessione e dovrebbero connettersi automaticamente una volta scaduto il valore TTL per la voce DNS originale e una volta che la voce risulta scaduta dalla cache DNS del client. Gli utenti possono anche eseguire il comando `ipconfig /flushdns` da un prompt dei comandi per eliminare manualmente la propria cache DNS.

  - L'avvio o riavvio dei client comporterà una ricerca DNS all'avvio e consentirà di ottenere il nuovo indirizzo IP per l'endpoint del servizio che sarà un server Accesso client o una matrice nel secondo centro dati.

Presumendo che siano state completate tutte le modifiche appropriate apportate alla configurazione per definire e configurare i servizi del secondo centro dati affinché questi ultimi funzionino nello stesso modo che se si trovassero nel centro dati principale e presumendo che la configurazione DNS stabilita sia corretta, non dovrebbe essere necessario apportare ulteriori modifiche per attivare i server Accesso client.

## Attivazione dei servizi Trasporto

Generalmente, i client e gli altri server che inoltrano messaggi identificano tali server mediante l'uso di DNS. L'attivazione dei servizi Trasporto nel secondo datacenter implica la modifica dei record DNS affinché puntino all'indirizzo IP dei server Cassette postali nel secondo datacenter. A questo punto, i client e i server mittente si connetteranno automaticamente ai server nel secondo datacenter in uno dei seguenti modi:

  - I client continueranno a tentare la connessione e dovrebbero connettersi automaticamente una volta scaduto il valore TTL per la voce DNS originale e una volta che la voce risulta scaduta dalla cache DNS del client. Gli utenti possono anche eseguire il comando `ipconfig /flushdns` da un prompt dei comandi per eliminare manualmente la propria cache DNS.

  - L'avvio o riavvio dei client comporterà una ricerca DNS all'avvio e consentirà di ottenere il nuovo indirizzo IP per l'endpoint SMTP che sarà un server Cassette postali nel secondo datacenter.

Presumendo che siano state completate tutte le modifiche appropriate apportate alla configurazione per definire e configurare i servizi del secondo centro dati affinché questi ultimi funzionino nello stesso modo che se si trovassero nel centro dati principale e presumendo che la configurazione DNS stabilita sia corretta, non dovrebbe essere necessario apportare ulteriori modifiche per attivare i server Trasporto.

## Attivazione dei servizi Messaggistica unificata

I servizi Messaggistica unificata si connettono alle linee telefoniche e al sistema PBX di un'organizzazione. La connessione logica tra il sistema PBX e il servizio Messaggistica unificata viene fornita da un gateway IP. I gateway IP includono una funzionalità ad elevata disponibilità e sono in grado di passare da un servizio Messaggistica unificata a un altro quando viene rilevato un errore.

Se, nel secondo datacenter, sono presenti servizi Messaggistica unificata che si trovavano in uno stato disabilitato in quanto dedicati alla soluzione di resilienza del sito, questi possono essere abilitati utilizzando il cmdlet [Enable-UMService](https://technet.microsoft.com/it-it/library/jj552411\(v=exchg.150\)) (ad esempio, `Enable-UMService EX4`).

Pertanto, presumendo che i gateway IP siano associati ai servizi Messaggistica unificata mediante l'uso dei server DNS, l'attivazione dei servizi Messaggistica unificata implica la modifica ai record DNS affinché questi puntino ai nuovi indirizzi IP che verranno configurati per il servizio Messaggistica unificata nel secondo centro dati. Presupponendo che siano state completate tutte le modifiche di configurazione appropriate necessarie per definire e configurare i servizi nel secondo datacenter, affinché funzionino come se si trovassero nel datacenter principale, e presupponendo che la configurazione DNS stabilita sia corretta, non dovrebbe essere necessario apportare ulteriori modifiche per attivare i servizi Messaggistica unificata.

Se il gateway IP utilizzato non supporta l'uso di nomi DNS per risolvere i servizi Messaggistica unificata, saranno necessari ulteriori passi di configurazione per direzionare manualmente il gateway IP verso gli indirizzi IP dei servizi Messaggistica unificata nel secondo datacenter.

## Attivazione dei server Trasporto Edge

I passi per l'attivazione del ruolo del server Trasporto Edge varieranno a seconda della configurazione specificata. I server Trasporto Edge in due centro dati possono essere configurati in una configurazione attiva/passiva o attiva/attiva. In una configurazione attiva/passiva, il server Trasporto Edge nel secondo centro dati risulta inattivo fino a quando non viene attivato il secondo centro dati. In una configurazione attiva/attiva, i server Trasporto Edge in entrambi i centro dati recapitano posta ininterrottamente.

In una configurazione attiva/attiva, non è richiesto alcun passo per l'attivazione dei server Trasporto Edge nel secondo centro dati, in quanto già in esecuzione. In una configurazione attiva/passiva, è necessario aggiornare il record di risorse DNS MX per ciascun dominio SMTP come parte dello switchover dal centro dati principale a quello di standby. Sebbene la configurazione attiva/attiva fornisca una soluzione semplice per lo switchover del centro dati, ha lo svantaggio che necessita di un monitoraggio accurato del carico per accertarsi che una volta eseguito lo switchover del centro dati i server Trasporto Edge nel secondo centro dati siano in grado di fornire capacità sufficiente per supportare il carico incrementato che scorre in esso; di conseguenza, i server Trasporto Edge nel centro dati principale risultano non disponibili.

Anche con una configurazione attiva/attiva, potrebbe essere appropriato aggiornare i record di risorse MX per i server Trasporto Edge durante lo switchover di un centro dati. Se si consente al record di risorse MX relativo al centro dati danneggiato di continuare a puntare al centro dati danneggiato, nel momento in cui viene avviato il ripristino del centro dati questo potrebbe tentare di connettersi ai relativi server Trasporto Edge. Ciò potrebbe accadere mentre i servizi Trasporto Edge sono in uno stato di instabilità (ad esempio, in quanto si stanno ripristinando servizi dipendenti nel centro dati).

Presumendo che i record DNS siano sotto il controllo dell'organizzazione, l'attivazione dei server Trasporto Edge implica l'aggiornamento del record di risorse MX per ciascun dominio SMTP ospitato dal server.


> [!NOTE]
> Se il record di risorse MX utilizzato dall'organizzazione non è ospitato da un server DNS sotto il controllo dell'organizzazione, si potrebbe prendere in considerazione l'idea di far riferimento a un record CNAME nel record di risorse MX e di utilizzare il record CNAME sotto il controllo dell'organizzazione per cui è quindi possibile eseguire l'aggiornamento.



Gli aggiornamenti del DNS abilitano il traffico in ingresso e il traffico in uscita viene gestito dall'attivazione dei database delle cassette postali in un sito che dispone di server Trasporto Edge funzionanti:

  - Quando le connessioni SMTP in ingresso vengono avviate utilizzando le informazioni sulla risoluzione dei nomi aggiornate, i client SMTP si connetteranno ai server Trasporto Edge nel secondo centro dati. Il traffico verrà instradato in modo appropriato dal server Trasporto Edge e non è necessario apportare ulteriori modifiche.

  - Quando vengono avviate le connessioni SMTP in uscita, queste proveranno a connettersi al server Trasporto Edge localmente disponibile e i messaggi verranno messi in coda o inviati immediatamente a seconda dello stato del server di ricezione.

Inizio pagina

## Ripristino del servizio per il centro dati principale

In genere, gli errori del centro dati sono temporanei o permanenti. Nel caso di un errore permanente, quale un evento che ha provocato la distruzione permanente di un centro dati principale, non vi è alcuna prospettiva che il centro dati principale venga attivato. Tuttavia, nel caso di un errore temporaneo (ad esempio, un'interruzione di alimentazione estesa o di dimensioni notevoli, ma con un danno reversibile), esiste una possibilità che venga ripristinato il servizio completo del centro dati principale.

Il processo di ripristino del servizio di un datacenter precedentemente danneggiato viene definito *switchback*. La procedura utilizzata per eseguire lo switchback del datacenter è analoga a quella utilizzata per eseguire lo switchover del datacenter, con l'importante differenza che gli switchback del datacenter sono programmati e la durata dell'interruzione è spesso molto breve.

È importante che lo switchback non venga eseguito finché le dipendenze dell'infrastruttura per Exchange non vengono riattivate, non risultano funzionanti e stabili e non sono state convalidate. Se tali dipendenze non sono disponibili o integre, il processo di switchback potrebbe determinare un'interruzione più lunga del necessario e potrebbe non essere completato correttamente.

## Switchback del ruolo server Cassette postali

Il ruolo server Cassette postali dovrebbe essere il primo di cui eseguire lo switchback al datacenter principale. La procedura seguente illustra in dettaglio il processo di switchback del ruolo server Cassette postali:

1.  Come parte del processo di switchover del centro dati, è stato attivato uno stato di arresto per i server Cassette postali nel centro dati principale. Quando l'ambiente (quali il centro dati principale, le dipendenze di Exchange e una connettività WAN) è pronto, il primo passaggio è di attivare lo stato avviato per i server Cassette postali del centro dati principale ripristinato e di incorporarli nel gruppo di disponibilità del database. La modalità con cui viene eseguita questa operazione dipende dal fatto che il gruppo di disponibilità del database sia o meno in modalità di coordinazione dell'attivazione del database.
    
    1.  Se il gruppo di disponibilità del database è in modalità di coordinazione dell'attivazione del database, è possibile incorporare i membri del gruppo di disponibilità del database nel sito principale utilizzando il cmdlet [Start-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd335076\(v=exchg.150\)). A questo punto, per assicurarsi che il DAG stia utilizzando il modello di quorum appropriato, eseguire il cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\)) sul DAG senza specificare alcun parametro.
    
    2.  Se il gruppo di disponibilità del database non è in modalità di coordinazione dell'attivazione del database, è possibile incorporare i membri del gruppo di disponibilità del database utilizzando il cmdlet [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/it-it/library/dd298049\(v=exchg.150\)).

2.  Una volta incorporati i server Cassette postali del centro dati principale nel gruppo di disponibilità del database, sarà necessario sincronizzarne saltuariamente le relative copie del database. A seconda del tipo di errore, della durata dell'interruzione e delle azioni intraprese da un amministratore durante l'interruzione, ciò potrebbe richiedere il reseeding delle copie del database. Ad esempio, se durante l'interruzione, si rimuovono le copie del database dal centro dati principale danneggiato per consentire il troncamento dei file di registro per le restanti copie attive nel secondo centro dati, sarà necessario eseguire il reseeding. Da questo punto in avanti, ciascun database può procedere individualmente. Una volta verificata l'integrità dei una copia del database replicata nel centro dati principale, è possibile passare al passo successivo.
    

    > [!NOTE]
    > Tale processo non richiede uno spostamento contemporaneo di tutti i database. Si consiglia di spostare la maggior parte dei database dell'organizzazione contemporaneamente; tuttavia, alcuni database potrebbero rimanere nel secondo centro dati qualora si verificassero problemi associati alle copie del database nel centro dati principale.



3.  Dopo aver verificato che la maggior parte dei database si trova in uno stato integro nel datacenter principale, è possibile programmare l'interruzione per lo switchback. Quando arriva il periodo pianificato, è necessario adottare la seguente procedura:
    
    1.  Durante il processo di switchover del centro dati, il gruppo di disponibilità del database era configurato per utilizzare un server di controllo alternativo. È necessario riconfigurare il gruppo di disponibilità del database affinché utilizzi un server di controllo nel centro dati principale. Se si utilizza lo stesso server di controllo e la directory di controllo utilizzata prima dell'interruzione del centro dati principale, è possibile eseguire il comando `Set-DatabaseAvailabilityGroup -Identity DAGName`. Se si intende utilizzare un server o una directory di controllo diversi dal server e dalla directory di controllo originali, utilizzare il comando [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\)) per configurare i parametri del server e della directory di controllo con i valori appropriati.
    
    2.  I database che si stanno riattivando nel centro dati principale devono essere smontati nel secondo centro dati. È possibile utilizzare il cmdlet [Dismount-Database](https://technet.microsoft.com/it-it/library/bb124936\(v=exchg.150\)) per smontare i database.
    
    3.  Una volta smontati i database, è necessario spostare gli URL del server Accesso client dal secondo centro dati nel centro dati principale. Tale operazione viene eseguita modificando il record DNS per gli URL in modo che puntino al server Accesso client o alla matrice nel centro dati principale. Così facendo, il sistema agirà come se si verificasse un failover del database per ciascun database spostato.
        

        > [!IMPORTANT]
        > Non passare al passo successivo fino allo spostamento degli URL del server Accesso client e alla scadenza delle voci della cache e del valore TTL del DNS. L'attivazione dei database nel centro dati principale prima dello spostamento degli URL del server Accesso client nel centro dati principale comporterà una configurazione errata (ad esempio, un database montato privo di server Accesso client nel relativo sito Active Directory).

    
    4.  Poiché ciascun database nel centro dati principale è in uno stato di integrità, è possibile attivarlo nel centro dati principale eseguendo gli switchover del database. Tale operazione viene eseguita utilizzando il cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/it-it/library/dd298068\(v=exchg.150\)) per ciascun database che verrà attivato.
    
    5.  Una volta spostati tutti i database nel centro dati principale, è possibile montarli utilizzando il cmdlet [Mount-Database](https://technet.microsoft.com/it-it/library/aa998871\(v=exchg.150\)).

Dopo avere attivato e montato uno o più database nel datacenter principale, è possibile eseguire le procedure di switchback per gli altri ruoli server.

## Switchback del server Accesso client

Come parte del processo di switchover, i record DNS interni ed esterni utilizzati dai client, da altri server e dai gateway IP per risolvere gli endpoint del servizio per i server Accesso client, Trasporto, Messaggistica unificata e Edge Transport sono stati modificati in modo da puntare agli endpoint corrispondenti nel secondo datacenter. Il processo di switchback per gli altri ruoli server implica la modifica di tali record in modo che puntino agli endpoint del servizio ripristinati nel datacenter principale.

Come nel caso delle modifiche apportate al DNS effettuate durante lo switchover al secondo centro dati, i client, i server e i gateway IP proseguiranno con i tentativi di connessione e dovrebbero connettersi automaticamente alla scadenza del valore TTL per la voce del DNS originale e alla scadenza della voce dalla relativa cache DNS.

Inizio pagina

## Ripristino della resilienza del sito

Terminato lo switchback al datacenter principale, è possibile ristabilire la resilienza del sito per il datacenter principale verificando l'integrità e lo stato di ogni copia del database delle cassette postali nel secondo datacenter. Inoltre, se ciascuna copia del database nel secondo centro dati risultava originariamente bloccata per l'attivazione, è possibile, a questo punto, riconfigurare tali impostazioni.

Inizio pagina


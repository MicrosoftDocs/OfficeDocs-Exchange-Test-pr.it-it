---
title: 'Spostamento del percorso del database delle cassette postali per una copia del database delle cassette postali: Exchange 2013 Help'
TOCTitle: Spostamento del percorso del database delle cassette postali per una copia del database delle cassette postali
ms:assetid: 324f255c-d95d-4a8a-a134-c8cee5c5b9cb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd979782(v=EXCHG.150)
ms:contentKeyID: 50480284
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Spostamento del percorso del database delle cassette postali per una copia del database delle cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-05-07_

Dopo aver creato un database delle cassette postali, è possibile spostarlo su un altro volume, in un'altra cartella o in un diverso percorso utilizzando l'interfaccia di amministrazione di Exchange o Shell. Per istruzioni dettagliate su come spostare il percorso di un database delle cassette postali non replicato, vedere [Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

Se il database di cassette postali è replicato in una o più copie, per modificarne il percorso è necessario eseguire la procedura in questo argomento. Tutte le copie del database di cassette postali devono trovarsi nello stesso percorso su ogni server in cui si trova una copia. Ad esempio, se il database DB1 si trova in C:\\mountpoints\\DB1 sul server EX1, le copie di DB1 sui server EX2, EX3 e così via dovranno anch'esse trovarsi in C:\\mountpoints\\DB1.

Per informazioni sulle altre attività di gestione correlate alle copie del database delle cassette postali? vedere [Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 2 minuti più il tempo necessario per spostare i dati; questo tempo dipende da un'ampia gamma di fattori quali la dimensione del database, la velocità, la larghezza di banda disponibile, la latenza della rete e la velocità di archiviazione.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Copie del database cassette postali" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Per eseguire l'operazione di spostamento, è necessario disinstallare temporaneamente il database, rendendolo inaccessibile agli utenti. Se al momento il database è disinstallato, non viene installato nuovamente al termine dell'operazione.

  - Per eseguire l'operazione di spostamento, la replica del database deve essere disabilitata per tutte le copie. Non è sufficiente sospendere la replica; è necessario disabilitarla utilizzando il cmdlet [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335119\(v=exchg.150\)) per rimuovere le copie del database.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Spostamento di un database di cassette postali replicato in un nuovo percorso tramite Shell


> [!NOTE]
> Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per spostare un database delle cassette postali replicato in un nuovo percorso.



1.  Notare eventuali impostazioni per l'intervallo di riesecuzione o troncamento per tutte le copie del database di cassette postali da spostare. È possibile ottenere queste informazioni utilizzando il cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb124924\(v=exchg.150\)), come mostrato in questo esempio.
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  Se per il database è abilitata la registrazione circolare, disabilitarla prima di procedere. Per disabilitare la registrazione circolare per un database di cassette postali, utilizzare il cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\)), come mostrato in questo esempio.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $false

3.  Rimuovere tutte le copie del database di cassette postali per il database da spostare. Per la procedura dettagliata, vedere [Rimuovere una copia del database delle cassette postali](remove-a-mailbox-database-copy-exchange-2013-help.md). Dopo aver rimosso tutte le copie, conservare i file di registro e database da ogni server da cui la copia del database viene rimossa e spostata in un altro percorso. Questi file sono conservati in modo che le copie del database non necessitino del reseeding dopo che sono state riaggiunte.

4.  Spostare il percorso del database di cassette postali nella nuova posizione. Per la procedura dettagliata, vedere [Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Durante l'operazione di spostamento, il database da spostare deve essere disinstallato. Fino a quando lo spostamento non è stato completato, questa procedura provocherà un'interruzione del servizio per tutti gli utenti le cui cassette postali si trovano sul database spostato. Al termine dell'operazione di spostamento, il database verrà installato automaticamente.



5.  Creare la struttura di cartelle appropriata su ogni server Cassette postali che in precedenza conteneva una copia passiva del database spostato. Ad esempio, se il database è stato spostato in C:\\mountpoints\\DB1, è necessario creare questo stesso percorso su ogni server Cassette postali che conterrà una copia del database di cassette postali.

6.  Dopo aver creato la struttura di cartelle, spostare la copia passiva del database e il relativo flusso di registrazione nel nuovo percorso. Si tratta dei file conservati dopo il passo 3. Ripetere questo procedura per ogni copia del database rimossa nel passo 3.

7.  Aggiungere tutte le copie del database rimosse nel passo 3. Per la procedura dettagliata, vedere [Aggiungere una copia del database delle cassette postali](add-a-mailbox-database-copy-exchange-2013-help.md).

8.  Su ogni server che contiene una copia del database di cassette postali da spostare, utilizzare i seguenti comandi per interrompere e riavviare i servizi di indicizzazione dei contenuti.
    
        Net stop MSExchangeFastSearch
        Net start MSExchangeFastSearch

9.  Facoltativamente, è possibile abilitare la registrazione circolare utilizzando il cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\)), come mostrato in questo esempio.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $true

10. Riconfigurare eventuali valori definiti in precedenza per l'intervallo di riesecuzione e e di troncamento usando il cmdlet [Set-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd298104\(v=exchg.150\)), come mostrato in questo esempio.
    
        Set-MailboxDatabaseCopy DB1\MBX2 -ReplayLagTime 00:15:00

11. Mentre le copie vengono aggiunte, si consiglia di verificare l'integrità e lo stato di ogni singola copia prima di procedere con la successiva. È possibile verificare l'integrità e lo stato nei seguenti modi:
    
    1.  Esaminando il registro eventi per individuare eventuali errori o avvisi relativi al database o alla copia.
    
    2.  Usando il cmdlet [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/it-it/library/dd298044\(v=exchg.150\)) per verificare l'integrità e lo stato della replica continua per la copia del database.
    
    3.  Usando il cmdlet [Test-ReplicationHealth](https://technet.microsoft.com/it-it/library/bb691314\(v=exchg.150\)) per verificare l'integrità e lo stato della replica continua e del gruppo di continuità del database.

Per ulteriori informazioni sulla sintassi e sui parametri, vedere gli argomenti seguenti:

  - [Get-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb124924\(v=exchg.150\))

  - [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\))

  - [Set-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd298104\(v=exchg.150\))

  - [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/it-it/library/dd298044\(v=exchg.150\))

  - [Test-ReplicationHealth](https://technet.microsoft.com/it-it/library/bb691314\(v=exchg.150\))

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che il percorso della copia del database delle cassette postali sia stato correttamente spostato, procedere in uno dei seguenti modi:

  - In EAC, individuare **Server** \> **Database**. Selezionare il database che è stato copiato. Nel riquadro dei dettagli vengono visualizzati lo stato della copia del database e del relativo indice di contenuto, insieme alla lunghezza della coda di copia corrente. Verificare lo stato sia integro.

  - In Shell eseguire il comando riportato di seguito per verificare che la copia del database delle cassette postali sia stata creata e che sia integra.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    I campi Stato e Stato indice contenuto devono essere entrambi integri.


---
title: 'Aggiornamento di una copia del database delle cassette postali: Exchange 2013 Help'
TOCTitle: Aggiornamento di una copia del database delle cassette postali
ms:assetid: bead3cc5-7d50-446f-95b7-e432bcb7968e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351100(v=EXCHG.150)
ms:contentKeyID: 50481585
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiornamento di una copia del database delle cassette postali

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-11-02_

L'aggiornamento, noto anche come *seeding*, è il processo tramite il quale una copia del database delle cassette postali viene aggiunta a un altro server Cassette postali in un gruppo di disponibilità del database (DAG). La copia aggiunta diventa il database di base per la copia passiva in cui i file di registro copiati dalla copia attiva vengono rieseguiti. Il seeding è necessario nei seguenti casi:

  - Quando viene creata una nuova copia passiva di un database. Il seeding può essere rimandato per una nuova copia di un database delle cassette postali, ma alla fine ogni copia passiva del database deve essere sottoposta a seeding per funzionare come copia del database ridondante.

  - Dopo che si è verificato un failover in cui vengono persi dati a seguito del fatto che la copia del database passiva è diventata divergente e irrecuperabile.

  - Quando il sistema rileva un file di registro danneggiato che non può essere riprodotto nella copia passiva del database.

  - Dopo che si è verificata una deframmentazione non in linea di qualsiasi copia del database.

  - Dopo che la sequenza di generazione del registro per il database è stata ripristinata a 1.

È possibile eseguire il seeding utilizzando i seguenti metodi:

  - **Seeding automatico**   Un seeding automatico consente di produrre una copia passiva del database attivo sul server Cassette postali di destinazione. Il seeding automatico avviene durante la creazione di un database.

  - **Seeding tramite il cmdlet Update-MailboxDatabaseCopy**   È possibile utilizzare il cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)) in Shell per eseguire il seeding di una copia del database in qualsiasi momento.

  - **Seeding tramite la procedura guidata di aggiornamento della copia database delle cassette postali**   È possibile utilizzare la procedura guidata di aggiornamento della copia database delle cassette postali in EAC per eseguire il seeding di una copia del database in qualsiasi momento.

  - **Copia manuale del database non in linea**   È possibile smontare la copia attiva del database e copiare il file di database nella stessa posizione su un altro server Cassette postali nello stesso gruppo di disponibilità del database. Se si utilizza questo metodo, si verificherà un'interruzione del servizio poiché il processo richiede lo smontaggio del database.

L'aggiornamento di una copia del database può richiedere molto tempo, soprattutto se il database che si sta copiando è di grandi dimensioni oppure se la rete ha una latenza elevata o una larghezza di banda limitata. Una volta avviato il processo di seeding, non chiudere EAC o Shell fino al termine del processo. Diversamente, l'operazione di seeding verrà terminata.

Una copia del database può essere sottoposta a seeding utilizzando la copia attiva o una copia passiva aggiornata come origine per il seeding. Se si esegue il seeding da una copia passiva, è importante ricordare che l'operazione di seeding terminerà con un errore di comunicazione di rete nelle seguenti circostanze:

  - Se lo stato della copia di origine del seeding cambia in Failed o FailedAndSuspended.

  - Se si verifica un failover del database su un'altra copia.

È possibile eseguire contemporaneamente il seeding di più copie del database. Tuttavia, se si esegue il seeding di più copie contemporaneamente, è necessario eseguire il seeding del solo file di database, omettendo il catalogo di indice del contenuto. È possibile eseguire questa operazione utilizzando il parametro *DatabaseOnly* con il cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)).


> [!NOTE]
> Se non si utilizza il parametro <EM>DatabaseOnly</EM> durante il seeding di più destinazioni dalla stessa origine, l'operazione termina con l'errore SeedInProgressException FE1C6491.



Per informazioni sulle altre attività di gestione che hanno per oggetto le copie del database delle cassette postali? vedere [Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 2 minuti più il tempo necessario per eseguire il seeding della copia del database, che dipende da un'ampia gamma di fattori quali la dimensione del database, la velocità, la larghezza di banda disponibile, la latenza della rete e la velocità di archiviazione.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Copie del database cassette postali" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - La copia del database delle cassette postali deve essere sospesa. Per la procedura dettagliata, vedere [Sospendere o riprendere una copia del database delle cassette postali](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md).

  - Il servizio Registro di sistema remoto deve essere in esecuzione sul server che ospita la copia del database passiva che si sta aggiornando.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Aggiornamento di una copia del database delle cassette postali tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Database**.

2.  Selezionare il database delle cassette postali di cui si desidera aggiornare la copia passiva.

3.  Nel riquadro Dettagli in **Copia di database** fare clic su **Sospendi** sotto la copia di database passiva di cui si desidera eseguire il seeding. Fornire qualsiasi commento facoltativo e scegliere **Salva**.

4.  Nel riquadro Dettagli in **Copia di database** fare clic su **Aggiorna** sotto la copia di database passiva di cui si desidera eseguire il seeding.

5.  
    
    Per impostazione predefinita, la copia attiva del database è utilizzata come database di origine per il seeding. Se si preferisce utilizzare una copia di database passiva per il seeding, fare clic su **Sfoglia…** per selezionare il server che contiene la copia di database passiva che si desidera utilizzare per l'origine.

6.  Fare clic su **OK** per aggiornare la copia di database passiva.

## Aggiornamento di una copia del database delle cassette postali tramite Shell

In questo esempio viene illustrato come eseguire il seeding della copia del database DB1 in MBX1.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1

In questo esempio viene illustrato come eseguire il seeding della copia del database DB1 in MBX1 utilizzando MBX2 come server Cassette postali di origine per il seeding.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2

In questo esempio viene illustrato come eseguire il seeding della copia del database DB1 in MBX1 senza eseguire il seeding del catalogo dell'indice di contenuto.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -DatabaseOnly

In questo esempio viene illustrato come eseguire il seeding del catalogo dell'indice di contenuto per la copia del database DB1 in MBX1 senza eseguire il seeding del file di database.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly

## Copia manuale di un database offline

1.  Se per il database è abilitata la registrazione circolare, disabilitarla prima di procedere. Per disabilitare la registrazione circolare per un database di cassette postali, utilizzare il cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\)), come mostrato in questo esempio.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $false

2.  Disinstallare il database. È possibile utilizzare il cmdlet [Dismount-Database](https://technet.microsoft.com/it-it/library/bb124936\(v=exchg.150\)), come illustrato in questo esempio.
    
        Dismount-Database DB1 -Confirm $false

3.  Copiare manualmente i file del database (il file del database e tutti i file di registro) in un'altra posizione, come ad esempio un'unità disco esterna o una condivisione di rete.

4.  installare il database. È possibile utilizzare il cmdlet [Mount-Database](https://technet.microsoft.com/it-it/library/aa998871\(v=exchg.150\)), come illustrato in questo esempio.
    
        Mount-Database DB1

5.  Sul server che ospiterà la copia, copiare i file del database dall'unità esterna o dalla condivisione di rete nello stesso percorso della copia del database attivo. Ad esempio, se il percorso del database della copia attiva è D:\\DB1\\DB1.edb e il percorso del file di registro è D:\\DB1, copiare i file del database in D:\\DB1 sul server che ospiterà la copia.

6.  Aggiungere la copia del database delle cassette postali utilizzando il cmlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd298105\(v=exchg.150\)) con il parametro *SeedingPostponed*, come mostrato nell'esempio.
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -SeedingPostponed

7.  Se la registrazione circolare è abilitata per il database, abilitarla nuovamente utilizzando il cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\)), come mostrato in questo esempio.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $true

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare il seeding corretto di una copia di database delle cassette postali, effettuare una delle seguenti operazioni:

  - In EAC, individuare **Server** \> **Database**. Selezionare il database di cui è stato eseguito il seeding. Nel riquadro dei dettagli vengono visualizzati lo stato della copia del database e del relativo indice di contenuto, insieme alla lunghezza della coda di copia corrente.

  - In Shell eseguire il comando riportato di seguito per verificare che il seeding della copia del database delle cassette postali sia stato eseguito correttamente e che la copia sia integra.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    I campi Stato e Stato indice contenuto devono essere entrambi integri.


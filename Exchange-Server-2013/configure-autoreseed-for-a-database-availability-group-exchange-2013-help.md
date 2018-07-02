---
title: 'Configurare il reseeding automatico per un gruppo di disponibilità del database: Exchange 2013 Help'
TOCTitle: Configurare il reseeding automatico per un gruppo di disponibilità del database
ms:assetid: 4a8bd779-b52a-40ed-8040-4d76eabeb41e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619303(v=EXCHG.150)
ms:contentKeyID: 50480541
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il reseeding automatico per un gruppo di disponibilità del database

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-04-15_

Il reseeding automatico è una funzionalità per il ripristino rapido della ridondanza del database dopo un errore del disco. In caso di errore di un disco, viene eseguito il reseeding automatico delle copie del database archiviate in esso su un disco di riserva preconfigurato del server Cassette postali. È possibile utilizzare la procedura illustrata in questo argomento per configurare il reseeding automatico di un gruppo di disponibilità del database (DAG).


> [!WARNING]
> La funzionalità Reseeding automatico non esegue tutte le attività di configurazione dei prerequisiti per l'utente. Le operazioni di corretta installazione dei dischi, aggiunta di dischi di riserva al sistema, sostituzione di dischi guasti e formattazione dei nuovi dischi devono essere eseguite manualmente da un amministratore.



Per altre attività di gestione relative ai gruppi di disponibilità del database, vedere [Gestione dei gruppi di disponibilità del database](managing-database-availability-groups-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di disponibilità del database" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - È necessario creare una singola partizione del disco logico per ogni disco fisico.

  - È necessario utilizzare il database specifico e la struttura della cartella di registro descritti nei passaggi riportati di seguito.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Come eseguire l'operazione

## Passaggio 1: Configurazione dei percorsi principali per database e volumi

Il primo passaggio implica la configurazione delle directory radice per i database (*AutoDagDatabasesRootFolderPath*) e i volumi (*AutoDagVolumesRootFolderPath*) utilizzati dal gruppo di disponibilità del database. I valori predefiniti sono rispettivamente C:\\ExchangeDatabases e C:\\ExchangeVolumes. Se si utilizzano i percorsi predefiniti, possibile saltare questo passaggio.

In questo esempio, viene illustrato come configurare il percorso principale per i database.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabasesRootFolderPath "C:\ExchDbs"

In questo esempio, viene illustrato come configurare il percorso principale per i volumi di archiviazione.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagVolumesRootFolderPath "C:\ExchVols"

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione dei percorsi principali per database e volumi, utilizzare il seguente comando.

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

L'output per *AutoDagDatabasesRootFolderPath* e *AutoDagVolumesRootFolderPath* deve corrispondere ai percorsi configurati.

## Passaggio 2: Configurazione del numero di database per volume

Successivamente, configurare il numero di database per ciascun volume (*AutoDagDatabaseCopiesPerVolume*) del gruppo di disponibilità del database.

In questo esempio, viene illustrato come configurare l'impostazione Reseeding automatico per un gruppo di disponibilità del database dotato di 4 database per volume.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabaseCopiesPerVolume 4

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione del numero di database per ciascun volume, utilizzare il seguente comando.

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

L'output per *AutoDagDatabaseCopiesPerVolume* deve corrispondere al valore configurato.

## Passaggio 3: Creazione delle directory radice per database e volumi

Quindi, creare le directory che corrispondono alle directory radice configurate nel passaggio 1. In questo esempio, viene illustrato come creare le directory predefinite utilizzando il prompt dei comandi.

    md C:\ExchangeDatabases
    md C:\ExchangeVolumes

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione delle directory radice per database e volumi, utilizzare il seguente comando.

    Dir C:\

Le directory create devono apparire nell'elenco di output.

## Passaggio 4: Montaggio delle cartelle di volume

Per ogni volume usato per i database (inclusi i volumi di riserva), utilizzare l'applicazione Gestione disco di Windows (diskmgmt.msc) per il montaggio di ciascun volume in una cartella installata in C:\\ExchangeVolumes\\. Ad esempio, se sono presenti 2 volumi con database e 1 volume di riserva, montare i volumi nelle seguenti cartelle installate:

  - C:\\ExchangeVolumes\\Volume1

  - C:\\ExchangeVolumes\\Volume2

  - C:\\ExchangeVolumes\\Volume3

I nomi delle cartelle installate possono essere il nome della cartella o delle cartelle installate nel percorso del volume della radice.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare il corretto montaggio delle cartelle di volume, utilizzare il seguente comando.

    Dir C:\

I volumi montati devono essere visualizzati nell'elenco di output.

## Passaggio 5: Creazione delle cartelle di database

Successivamente, creare le directory di database nel percorso radice C:\\ExchangeDatabases. In questo esempio viene illustrato come creare directory per la configurazione di archiviazione con 4 database su ogni volume.

    md c:\ExchangeDatabases\db001

    md c:\ExchangeDatabases\db002

    md c:\ExchangeDatabases\db003

    md c:\ExchangeDatabases\db004

## Come verificare se l'operazione ha avuto esito positivo

Per verificare il corretto montaggio delle cartelle di database, utilizzare il seguente comando.

    Dir C:\ExchangeDatabases

Le directory create devono apparire nell'elenco di output.

## Passaggio 6: Creazione di punti di montaggio per i database

Creare i punti di montaggio per ciascun database e collegare il punto di montaggio al volume corretto. Ad esempio, la cartella montata per db001 di deve trovare in C:\\ExchangeDatabases\\db001. Per eseguire questa operazione, è possibile utilizzare diskmgmt.msc o mountvol.exe. In questo esempio, viene illustrato come montare db001 in C:\\ExchangeDatabases\\db001 utilizzando mountvol.exe.

    Mountvol.exe c:\ExchangeDatabases\db001 \\?\Volume (GUID)

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione dei punti di montaggio per il database, utilizzare il seguente comando.

    Mountvol.exe C:\ExchangeDatabases\db001 /L

Il volume montato deve essere visualizzato nell'elenco dei punti di montaggio.

## Passaggio 7: Creazione della struttura di directory del database

In seguito, creare due directory sotto le cartelle create nel passaggio 5, una per ciascun database e una per ciascun flusso di registrazione del database che verrà archiviato sullo stesso volume. Per la propria struttura di directory, è necessario utilizzare il seguente formato:

C:\\\< *NomeCartellaDatabase*\>\\*NomeDatabase*\\\<*NomeDatabase*\>.db

C:\\\< *NomeCartellaDatabase*\>\\*NomeDatabase*\\\<*NomeDatabase*\>.log

In questo esempio, viene illustrato come creare le directory per 4 database che verranno archiviati sul volume 1:

    md c:\ExchangeDatabases\db001\db001.db

    md c:\ExchangeDatabases\db001\db001.log

    md c:\ExchangeDatabases\db002\db002.db

    md c:\ExchangeDatabases\db002\db002.log

    md c:\ExchangeDatabases\db003\db003.db

    md c:\ExchangeDatabases\db003\db003.log

    md c:\ExchangeDatabases\db004\db004.db

    md c:\ExchangeDatabases\db004\db004.log

Ripetere i comandi precedenti per i database su ogni volume.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione della struttura della directory del database, utilizzare il seguente comando.

    Dir C:\ExchangeDatabases /s

Le directory create devono apparire nell'elenco di output.

## Passaggio 8: Creazione dei database

Creazione di database con registro e percorsi del database configurati con le cartelle appropriate. In questo esempio, viene illustrato come creare un database archiviato nella directory e nella struttura dei punti di montaggio appena create.

    New-MailboxDatabase -Name db001 -Server MBX1 -LogFolderPath C:\ExchangeDatabases\db001\db001.log -EdbFilePath C:\ExchangeDatabases\db001\db001.db\db001.edb

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione dei database nella cartella appropriata, utilizzare il seguente comando.

    Get-MailboxDatabase db001 | Format List *path*

Le proprietà del database restituite devono indicare che il file del database e i file di registro sono archiviati nelle cartelle precedenti.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione del reseeding automatico per un gruppo di disponibilità del database, effettuare le seguenti operazioni:

1.  Utilizzare il seguente comando per verificare la corretta configurazione del gruppo di disponibilità del database.
    
        Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

2.  Utilizzare il seguente comando per verificare la corretta configurazione della struttura della directory (di seguito, sono riportati i percorsi predefiniti; se necessario, sostituirli con i percorsi utilizzati).
    
        Dir c:\ExchangeDatabases /s
    
        Dir c:\ExchangeVolumes /s


---
title: 'Recupero dei dati utilizzando un database di ripristino: Exchange 2013 Help'
TOCTitle: Recupero dei dati utilizzando un database di ripristino
ms:assetid: d64c18e7-16af-4bd8-a5c5-01206984d4d1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee332351(v=EXCHG.150)
ms:contentKeyID: 50481782
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recupero dei dati utilizzando un database di ripristino

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-10-01_

Un database di ripristino (RDB) è un tipo speciale di database delle cassette postali che consente di montare un database delle cassette postali ripristinato e di estrarre i dati dal database ripristinato durante un'operazione di ripristino. I database di ripristino consentono di ripristinare i dati da un backup o dalla copia di un database senza interferire con l'accesso dell'utente ai dati correnti.

Dopo aver creato un database di ripristino (RDB), è possibile ripristinare un database cassetta postale nell'RDB utilizzando un applicazione di backup o copiando un database e i rispettivi file di registro nella struttura delle cartelle RDB. Successivamente, è possibile utilizzare il cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829875\(v=exchg.150\)) per estrarre i dati dal database ripristinato. Una volta completata l'estrazione, i dati possono essere esportati in una cartella o uniti in una cassetta postale esistente.

Per altre attività di gestione relative ai database di ripristino, vedere [Database di ripristino](recovery-databases-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 1 minuto più il tempo impiegato per impostare il database su uno stato di chiusura normale e per l'estrazione dei dati.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ripristino delle cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Alcune applicazioni di backup hanno la possibilità di ripristinare i dati di Exchange direttamente in un database di ripristino. Windows Server Backup può ripristinare solo i backup a livello di file in un database di ripristino. Non può essere utilizzato per ripristinare i backup a livello di applicazione in un database di ripristino.

  - Il database e file di registro che contengono i dati ripristinati devono essere ripristinati o copiati nella struttura delle cartelle RDB.

  - Il database deve essere in uno stato di chiusura normale. Dal momento che un database RDB rappresenta un percorso di ripristino alternativo per tutti i database, tutti i database ripristinati saranno in uno stato di chiusura anomala. È necessario utilizzare **Eseutil /R** per portare il database ripristinato in uno stato di chiusura normale.

## Ripristino dei dati da un database di ripristino tramite Shell

1.  Copiare un database ripristinato e i rispettivi file di registro o ripristinare un database e i rispettivi file di registro nel percorso che si utilizzerà per il database di ripristino.

2.  Utilizzare Eseutil per portare il database in uno stato di chiusura normale. Nell'esempio seguente, EXX è il prefisso di generazione dei registri per il database (ad esempio, E00, E01, E02 e così via).
    
        Eseutil /R EXX /l <RDBLogFilePath> /d <RDBEdbFolder>
    
    L'esempio seguente mostra un prefisso di generazione dei registri di E01, un database di ripristino e un percorso di file di registro di E:\\Databases\\RDB1:
    
        Eseutil /R E01 /l E:\Databases\RDB1 /d E:\Databases\RDB1

3.  Creare un database di ripristino. Assegnare al database di ripristino un nome univoco, ma utilizzare il nome ed il percorso del file di database per il parametro EdbFilePath e il percorso dei file di registro ripristinati per il parametro LogFolderPath.
    
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath <RDBPathandFileName> -LogFolderPath <LogFilePath>
    
    L'esempio seguente mostra la creazione di un database di ripristino che verrà utilizzato per ripristinare DB1.edb e i rispettivi file di registro che si trovano nel percorso E:\\Databases\\RDB1.
    
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath "E:\Databases\RDB1\DB1.EDB" -LogFolderPath "E:\Databases\RDB1"

4.  Riavviare il servizio Archivio informazioni di Microsoft Exchange:
    
        Restart-Service MSExchangeIS

5.  Montare il database di ripristino:
    
        Mount-database <RDBName>

6.  Verificare che il database installato contenga le cassette postali che si desidera ripristinare:
    
        Get-MailboxStatistics -Database <RDBName> | ft -auto

7.  Utilizzare il cmdlet New-MailboxRestoreRequest per ripristinare una cassetta postale o gli elementi da un database di ripristino a una cassetta postale di produzione.
    
    Nell'esempio seguente viene ripristinata la cassetta postale di origine che ha MailboxGUID 1d20855f-fd54-4681-98e6-e249f7326ddd sul database delle cassette postali DB1 la cassetta postale di destinazione con l'alias Cavaglieri.
    
        New-MailboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox 1d20855f-fd54-4681-98e6-e249f7326ddd -TargetMailbox Morris
    
    Nell'esempio seguente consente di ripristinare il contenuto della cassetta postale di origine che è il nome visualizzato Morris Cornejo nel database delle cassette postali DB1 la cassetta postale di archiviazione per Morris@contoso.com.
    
        New-MaiboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox "Morris Cornejo" -TargetMailbox Morris@contoso.com -TargetIsArchive

8.  Controllare periodicamente lo stato della richiesta di ripristino delle cassette postali utilizzando [Get-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829907\(v=exchg.150\)).
    
    Una volta che lo stato di ripristino risulti "Completato", eliminare la richiesta di ripristino utilizzando [Remove-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829910\(v=exchg.150\)). Esempio:
    
        Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest

## Come verificare se l'operazione ha avuto esito positivo

Per verificare il ripristino corretto dei dati della cassetta postale, aprire la cassetta postale di destinazione utilizzando Outlook o Outlook Web App e verificare la presenza dei dati ripristinati.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



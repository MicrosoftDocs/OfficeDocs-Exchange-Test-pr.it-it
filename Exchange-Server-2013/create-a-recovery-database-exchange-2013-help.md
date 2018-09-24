---
title: 'Creare un database di ripristino: Exchange 2013 Help'
TOCTitle: Creare un database di ripristino
ms:assetid: 34d87491-b7b7-44a9-8d69-e1a9c1fe5852
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee332321(v=EXCHG.150)
ms:contentKeyID: 50480326
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un database di ripristino

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-01-21_

È possibile utilizzare Shell per creare un database di ripristino, cioè un particolare database delle cassette postali utilizzato per montare ed estrarre i dati dal database ripristinato nel corso di un'operazione di ripristino. Dopo aver creato un database di ripristino, è possibile spostare un database di cassette postali ripristinato nel database di ripristino e utilizzare il cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829875\(v=exchg.150\)) per estrarre i dati dal database ripristinato. Una volta completata l'estrazione, i dati possono essere esportati in una cartella o uniti in una cassetta postale esistente. Utilizzando i database di ripristino è possibile ripristinare i dati da un backup o dalla copia di un database senza interferire con l'accesso ai dati correnti da parte dell'utente.

Per informazioni sulle altre attività di gestione relative al recupero dei database? vedere [Database di ripristino](recovery-databases-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Ripristino delle cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md) .

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Creazione di un database di ripristino tramite Shell

In questo esempio, il database di ripristino RDB1 viene creato sul server Cassette postali MBX2.

```powershell
New-MailboxDatabase -Recovery -Name RDB1 -Server MBX2
```

In questo esempio, il database di ripristino RDB2 viene creato sul server Cassette postali MBX1 usando un percorso personalizzato per il file di database e la cartella registro.
```powershell
    New-MailboxDatabase -Recovery -Name RDB2 -Server MBX1 -EdbFilePath "C:\Recovery\RDB2\RDB2.EDB" -LogFolderPath "C:\Recovery\RDB2"
```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MailboxDatabase](https://technet.microsoft.com/it-it/library/aa997976\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver creato correttamente un database di ripristino, fare quanto segue:

  - In Shell, utilizzare il seguente comando per visualizzare le informazioni di configurazione per il database di ripristino.
    
    ```powershell
    Get-MailboxDatabase <RecoveryDatabaseName> | Format-List
    ```

## Altre attività

Dopo aver creato un database di ripristino, è anche possibile ripristinare i dati usando questo database. Per la procedura dettagliata, vedere [Recupero dei dati utilizzando un database di ripristino](restore-data-using-a-recovery-database-exchange-2013-help.md).


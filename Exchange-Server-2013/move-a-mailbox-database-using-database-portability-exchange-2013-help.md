---
title: 'Sposta database cassette postali con portabilità database: Exchange 2013 Help'
TOCTitle: Spostamento di un database delle cassette postali utilizzando la portabilità del database
ms:assetid: a765ead1-43bc-4786-ae93-1835cacfc8fc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876926(v=EXCHG.150)
ms:contentKeyID: 51407401
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Spostamento di un database delle cassette postali utilizzando la portabilità del database

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-06-16_

È possibile utilizzare la portabilità del database per spostare un database delle cassette postali di Microsoft Exchange Server 2013 tra i server Cassette postali di Exchange 2013 nella stessa organizzazione. Ciò consente di ridurre tempi di ripristino complessivo per alcuni scenari di errore. Per ulteriori informazioni, vedere [Portabilità del database](database-portability-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti più il tempo necessario per il ripristino dei dati, lo spostamento dei file di database e il completamento della replica di Active Directory.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ripristino delle cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare EAC per spostare le cassette postali utente in un database ripristinato o temporaneo utilizzando la portabilità del database.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Spostamento, tramite Shell, delle cassette postali utente in un database ripristinato o temporaneo mediante l'uso della portabilità del database

1.  Verificare che il database da spostare sia in stato di chiusura normale. Se il database non è in stato di chiusura normale, eseguire un ripristino software.
    

    > [!NOTE]
    > Quando si esegue un ripristino software, tutti i file di registro non salvati vengono salvati nel database. Se non si dispone di tutti i file di registro necessari, non sarà possibile completare il processo di ripristino software. Proseguire con il passo 2.

    
    Per salvare tutti i file di registro non salvati nel database, da un prompt dei comandi, utilizzare il seguente comando:
    
    ```powershell
    ESEUTIL /R <Enn>
    ```
    

    > [!NOTE]
    > &lt;E<EM>nn</EM>&gt; specifica il prefisso del file di registro per il database in cui si desidera riprodurre i file di registro. Il prefisso del file di registro specificato da &lt;E<EM>nn</EM>&gt; è un parametro obbligatorio per Eseutil /r.



2.  Creare un database su un server utilizzando la seguente sintassi:

    ```powershell
        New-MailboxDatabase -Name <DatabaseName> -Server <ServerName> -EdbFilePath <DatabaseFileNameandPath> -LogFolderPath <LogFilesPath>
    ```

3.  Impostare l'attributo *This database can be over written by restore* utilizzando la seguente sintassi:
    
    ```powershell
    Set-MailboxDatabase <DatabaseName> -AllowFileRestore $true
    ```

4.  Spostare i file del database originale (file EDB, file di registro e catalogo di ricerca di Exchange) nella cartella del database specificata al momento della creazione del nuovo database.

5.  Installare il database utilizzando la seguente sintassi:
    
    ```powershell
    Mount-Database <DatabaseName>
    ```

6.  Una volta installato il database, modificare le impostazioni dell'account utente con il cmdlet [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)) in modo che l'account faccia riferimento alla cassetta postale sul nuovo server delle cassette postali. Per spostare tutti gli utenti dal database precedente nel nuovo database, utilizzare la seguente sintassi. 

    ```powershell
        Get-Mailbox -Database <SourceDatabase> |where {$_.ObjectClass -NotMatch '(SystemAttendantMailbox|ExOleDbSystemMailbox)'}| Set-Mailbox -Database <TargetDatabase>
    ```
7.  Attivare il recapito dei messaggi che restano nelle code utilizzando la seguente sintassi.
    
    ```powershell
    Get-Queue <QueueName> | Retry-Queue -Resubmit $true
    ```

Una volta completata la replica di Active Directory, tutti gli utenti potranno accedere alle proprie cassette postali sul nuovo server Exchange. La maggior parte dei client viene reindirizzata tramite Individuazione automatica. Gli utenti di Microsoft Office Outlook Web App vengono reindirizzati automaticamente.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare il corretto spostamento di una cassetta postale, procedere come segue:

  - Aprire la cassetta postale utilizzando Outlook Web App.

  - Aprire la cassetta postale utilizzando Microsoft Outlook.


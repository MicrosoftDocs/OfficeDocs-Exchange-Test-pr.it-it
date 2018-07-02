---
title: 'Gestire spostamenti locali: Exchange 2013 Help'
TOCTitle: Gestire spostamenti locali
ms:assetid: 1691b658-f5af-49c6-9170-5c3cb66c7306
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150487(v=EXCHG.150)
ms:contentKeyID: 50480111
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire spostamenti locali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-02-25_

Una richiesta di spostamento rappresenta il processo di spostamento di una cassetta postale da un database delle cassette postali ad un altro. Una richiesta di spostamento locale è uno spostamento della cassetta postale all'interno di una singola foresta. In Microsoft Exchange Server 2013, le cassette postali e le cassette postali di archiviazione personale possono risiedere in database separati. Utilizzando la funzione di richiesta di spostamento, è possibile spostare la cassetta postale principale e l'archivio associato nello stesso database o in un database separato. Le procedure descritte in questo argomento consentono gli spostamenti delle cassette postali locali.

Utilizzare le procedure seguenti per spostare le cassette postali nell'organizzazione locale. Queste procedure utilizzano Exchange Management Shell e l'interfaccia di amministrazione di Exchange.

Quando si utilizza una richiesta di spostamento per spostare cassette postali, le richieste di spostamento vengono elaborate dai seguenti due servizi:

  - Servizio di replica delle cassette postali di Microsoft Exchange

  - Proxy di replica delle cassette postali di Microsoft Exchange

Per ulteriori informazioni su server e proxy di replica Cassette postali, vedere [Per ulteriori informazioni sul Proxy MRS](https://technet.microsoft.com/it-it/library/jj156451\(v=exchg.150\)).

Per ulteriori informazioni sullo spostamento di cassette postali, vedere [Spostamenti di cassette postali di Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 20 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di migrazione e spostamento delle cassette postali" in [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Per verificare se una cassetta postale è pronta allo spostamento

In questo esempio viene utilizzata l'opzione *WhatIf* per verificare se la cassetta postale di Tony Smith è pronta allo spostamento nel nuovo database DB01 e se vi sono errori all'interno del comando. Quando si utilizza l'opzione *WhatIf*, il sistema esegue dei controlli sulla cassetta postale. Se la cassetta postale non è pronta allo spostamento, si verifica un errore.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase DB01 -WhatIf

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219166\(v=exchg.150\)) e [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\)).

## Creazione di una richiesta di spostamento locale

## Utilizzo dell'interfaccia di amministrazione di Exchange per creare una richiesta di spostamento locale

Per creare una richiesta di spostamento locale, accedere all'interfaccia di amministrazione di Exchange e applicare la procedura seguente;

1.  In EAC accedere a **Destinatari** \> **Migrazione** e quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella procedura guidata per **Nuovo spostamento cassetta postale locale**, selezionare l'utente che si desidera spostare, fare clic su **OK**, quindi fare clic su **Avanti**.

3.  Nella pagina **Sposta configurazione** specificare un nome per il nuovo batch. Selezionare le opzioni desiderate per la cassetta postale di archiviazione e il percorso del database delle cassette postali, quindi fare clic su **Nuovo**.

## Creazione di una richiesta di spostamento locale con Shell

Per un esempio di creazione di una richiesta di spostamento locale, vedere Esempio 2 in [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la migrazione sia stata eseguita correttamente, procedere come segue:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Migrazione**.

  - Verificare che lo spostamento sia stato eseguito correttamente, facendo clic su **Stato per tutti i batch** in EAC.

  - Da Shell immettere il comando seguente per recuperare informazioni sullo spostamento delle cassette postali.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Per ulteriori informazioni, vedere [Get-MigrationUserStatistics](https://technet.microsoft.com/it-it/library/jj218695\(v=exchg.150\)).

## Creazione di una richiesta di spostamento batch

## Utilizzo dell'interfaccia di amministrazione di Exchange per creare una richiesta di spostamento batch

Accedere all'interfaccia di amministrazione di Exchange e attenersi alla procedura seguente:

1.  In EAC accedere a **Destinatari** \> **Migrazione** e quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella procedura guidata per **Nuovo spostamento cassetta postale locale**, selezionare gli utenti che si desidera spostare, fare clic su **OK**, quindi fare clic su **Avanti**.

3.  Nella pagina **Sposta configurazione** specificare un nome per il nuovo batch. Selezionare le opzioni desiderate per la cassetta postale di archiviazione e il percorso del database delle cassette postali, quindi fare clic su **Nuovo**.


> [!WARNING]
> Assicurarsi di non impostare il limite per gli elementi non validi su un valore superiore a 50 elementi. Se lo si fa, lo spostamento potrebbe non riuscire. Per impostare il limite per gli elementi non validi su un valore superiore a 50 elementi, è necessario utilizzare Exchange Management Shell e impostare il parametro <EM>AcceptLargeDataLoss</EM> su true.



## Utilizzo di Shell per creare una richiesta di spostamento batch

Con questo esempio viene creato un batch di migrazione per uno spostamento locale in cui le cassette postali presenti nel file .csv specificato vengono spostate in un altro database delle cassette postali. Nel file .csv è contenuta una singola colonna con l'indirizzo di posta elettronica per ciascuna delle cassette postali che verrà spostata. L'intestazione di questa colonna deve essere denominata **EmailAddress**. Il batch di migrazione dell'esempio deve essere avviato manualmente utilizzando il cmdlet **Start-MigrationBatch** oppure tramite l'interfaccia di amministrazione di Exchange. In alternativa è possibile utilizzare il parametro *AutoStart* per avviare automaticamente il batch di migrazione.

    New-MigrationBatch -Local -Name LocalMove1 -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\LocalMove1.csv")) -TargetDatabases MBXDB2 -TimeZone "Pacific Standard Time"

    Start-MigrationBatch -Identity LocalMove1

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219166\(v=exchg.150\)) e [Start-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219165\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la migrazione sia stata eseguita correttamente, procedere come segue:

  - Verificare che lo spostamento sia stato eseguito correttamente, facendo clic su **Stato per tutti i batch** in EAC.

  - Da Shell immettere il comando seguente per recuperare informazioni sullo spostamento delle cassette postali.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Per ulteriori informazioni, vedere [Get-MigrationUserStatistics](https://technet.microsoft.com/it-it/library/jj218695\(v=exchg.150\)).

## Visualizzazione dei batch di migrazione

Per un esempio dell'utilizzo di Shell per visualizzare un batch di migrazione, vedere Esempio 2 in [Get-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219164\(v=exchg.150\)).

## Spostamento della sola cassetta postale principale di un utente

## Utilizzo dell'interfaccia di amministrazione di Exchange per spostare solo la cassetta postale principale di un utente

1.  In EAC accedere a **Destinatari** \> **Migrazione** e quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella procedura guidata per **Nuovo spostamento cassetta postale locale**, selezionare l'utente per il quale si desidera spostare la cassetta postale principale, fare clic su **OK**, quindi fare clic su **Avanti**.

3.  Nella pagina **Sposta configurazione** specificare un nome per il nuovo batch. Selezionare **Sposta solo la cassetta postale principale**, selezionare le opzioni desiderate per il percorso del database della cassetta postale, quindi fare clic su **Nuovo**.

## Utilizzo di Shell per spostare solo la cassetta postale principale di un utente

Con questo esempio viene spostata in DB01 solo la cassetta postale principale di Tony Smith. L'archivio non viene spostato.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -PrimaryOnly -TargetDatabase "DB01"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la migrazione sia stata eseguita correttamente, procedere come segue:

  - Nell'interfaccia di amministrazione di Exchange, fare clic su **Stato per tutti i batch**.

  - Da Shell immettere il comando seguente per recuperare informazioni sullo spostamento delle cassette postali.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Per ulteriori informazioni, vedere [Get-MigrationUserStatistics](https://technet.microsoft.com/it-it/library/jj218695\(v=exchg.150\)).

## Creazione di uno spostamento tra foreste utilizzando un file batch. csv

Questo esempio configura l'endpoint di migrazione, quindi crea uno spostamento di batch tra foreste dalla foresta di origine alla foresta di destinazione utilizzando un file .csv.

    New-MigrationEndpoint -Name Fabrikam -ExchangeRemote -Autodiscover -EmailAddress tonysmith@fabrikam.com -Credentials (Get-Credential fabrikam\tonysmith) 
    
    $csvData=[System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\batch.csv")
    New-MigrationBatch -CSVData $csvData -Timezone "Pacific Standard Time" -Name FabrikamMerger -SourceEndpoint Fabrikam -TargetDeliveryDomain "mail.contoso.com"

Per ulteriori informazioni sulla preparazione della foresta per gli spostamenti tra foreste, vedere i seguenti argomenti:

  - [Preparare le cassette postali per le richieste di spostamento tra foreste](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Preparare le cassette postali per gli spostamenti tra foreste con codice di esempio](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

  - [Prepara le cassette postali per gli spostamenti tra foreste utilizzando lo script Prepare MoveRequest.ps1 in Shell](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219166\(v=exchg.150\)) e [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la migrazione sia stata eseguita correttamente, procedere come segue:

  - Da Shell immettere il comando seguente per recuperare informazioni sullo spostamento delle cassette postali.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Per ulteriori informazioni, vedere [Get-MigrationUserStatistics](https://technet.microsoft.com/it-it/library/jj218695\(v=exchg.150\)).

## Spostamento della sola cassetta postale di archivio

## Utilizzo dell' interfaccia di amministrazione di Exchange per spostare solo una cassetta postale di archiviazione

1.  In EAC accedere a **Destinatari** \> **Migrazione** e quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella procedura guidata per **Nuovo spostamento cassetta postale locale**, selezionare l'utente per il quale si desidera spostare la cassetta postale di archiviazione, fare clic su **OK**, quindi fare clic su **Avanti**.

3.  Nella pagina **Sposta configurazione** specificare un nome per il nuovo batch. Selezionare **Spostamento della sola cassetta postale di archivio**, selezionare le opzioni desiderate per il percorso del database della cassetta postale, quindi fare clic su **Nuovo**.

## Utilizzo di Shell per spostare la sola cassetta postale di archivio

Con questo esempio viene spostata in DB03 solo la cassetta postale di archivio di Tony Smith. La cassetta postale principale non viene spostata.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -ArchiveOnly -ArchiveTargetDatabase "DB03"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219166\(v=exchg.150\)) e [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la migrazione sia stata eseguita correttamente, procedere come segue:

  - Da Shell immettere il comando seguente per recuperare informazioni sullo spostamento delle cassette postali.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Per ulteriori informazioni, vedere [Get-MigrationUserStatistics](https://technet.microsoft.com/it-it/library/jj218695\(v=exchg.150\)).

## Spostamento di una cassetta postale principale dell'utente e di una cassetta postale di archivio in database separati

Con questo esempio la cassetta postale principale e la cassetta postale di archivio di Ayla vengono spostati in database separati. Il database principale viene spostato in DB01 e l'archivio viene spostato in DB03.

    New-MoveRequest -Identity 'ayla@humongousinsurance.com' -TargetDatabase DB01 -ArchiveTargetDatabase -DB03

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219166\(v=exchg.150\)) e [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la migrazione sia stata eseguita correttamente, procedere come segue:

  - Da Shell immettere il comando seguente per recuperare informazioni sullo spostamento delle cassette postali.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Per ulteriori informazioni, vedere [Get-MigrationUserStatistics](https://technet.microsoft.com/it-it/library/jj218695\(v=exchg.150\)).

## Spostamento di una cassetta postale principale dell'utente e limite di elementi non validi elevato

## Utilizzo dell'interfaccia di amministrazione di Exchange per spostare una cassetta postale principale dell'utente e consentire un limite di elementi non validi elevato

1.  In EAC accedere a **Destinatari** \> **Migrazione** e quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella procedura guidata per **Nuovo spostamento cassetta postale locale**, selezionare l'utente per il quale si desidera spostare la cassetta postale principale, fare clic su **OK**, quindi fare clic su **Avanti**.

3.  Nella pagina **Sposta configurazione** specificare un nome per il nuovo batch. Selezionare **Spostamento della sola cassetta postale principale**, quindi selezionare le opzioni desiderate per il percorso del database della cassetta postale.

4.  Fare clic su **Altre opzioni**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni"), immettere il limite di elementi non validi, quindi fare clic su **OK**.

## Utilizzo di Shell per spostare una cassetta postale principale dell'utente e consentire un limite di elementi non validi elevato

In questo esempio viene spostata la cassetta postale principale di Lisa nel database della cassetta postale DB01 e viene impostato il limite di elementi non validi su `100`. Per impostare un limite di elementi non validi elevato, è necessario utilizzare il parametro *AcceptLargeDataLoss*.

    New-MoveRequest -Identity 'Lisa' -PrimaryOnly -TargetDatabase "DB01" -BadItemLimit 100 -AcceptLargeDataLoss

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219166\(v=exchg.150\)) e [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la migrazione sia stata eseguita correttamente, procedere come segue:

  - Da Shell immettere il comando seguente per recuperare informazioni sullo spostamento delle cassette postali.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Per ulteriori informazioni, vedere [Get-MigrationUserStatistics](https://technet.microsoft.com/it-it/library/jj218695\(v=exchg.150\)).


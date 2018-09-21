---
title: 'Migr. batch cart. pub. in Exchange 2013 da versioni prec.: Exchange 2013 Help'
TOCTitle: Utilizzare la migrazione seriale per spostare le cartelle pubbliche in Exchange 2013 dalle versioni precedenti
ms:assetid: da808e27-d2b7-4fbd-915c-a600751f526c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn912663(v=EXCHG.150)
ms:contentKeyID: 64126832
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzare la migrazione seriale per spostare le cartelle pubbliche in Exchange 2013 dalle versioni precedenti

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2018-03-26_

**Riepilogo:**  in questo articolo viene illustrato come spostare cartelle pubbliche da Exchange 2007 o Exchange 2010 a Exchange 2013.

In questo articolo viene descritto come eseguire la migrazione delle cartelle pubbliche da Exchange Server 2010 SP3 RU8 o Exchange 2007 SP3 RU15 a Microsoft Exchange Server 2013 CU7 o versioni successive nella stessa foresta.

I server Exchange 2010 SP3 RU8 ed Exchange 2007 SP3 RU15 vengono definiti *server Exchange legacy*.


> [!NOTE]
> Il metodo della migrazione batch descritto in questo articolo è l'unico metodo supportato per la migrazione delle cartelle pubbliche legacy a Exchange 2013. Il vecchio metodo della migrazione seriale per le cartelle pubbliche è stato deprecato e non è più supportato da Microsoft.



La migrazione verrà eseguita mediante i cmdlet **\*MigrationBatch** e i cmdlet **\*PublicFolderMigrationRequest** per la risoluzione dei problemi. Inoltre, verranno utilizzati i seguenti script di PowerShell:

  - `Export-PublicFolderStatistics.ps1`   Questo script crea il file di mapping Nome cartella-Dimensione cartella.

  - ` Export-PublicFolderStatistics.psd1` Questo file di supporto è utilizzato dallo script Export-PublicFolderStatistics.ps1 e deve essere scaricato nello stesso percorso.

  - `PublicFolderToMailboxMapGenerator.ps1`   Questo script crea il file di mapping Cartella pubblica-Cassetta postale.

  - `PublicFolderToMailboxMapGenerator.strings.psd1` Questo file di supporto è utilizzato dallo script PublicFolderToMailboxMapGenerator.ps1 e deve essere scaricato nello stesso percorso.

  - `Create-PublicFolderMailboxesForMigration.ps1` Questo script crea le cassette postali delle cartelle pubbliche di destinazione per la migrazione. Inoltre, questo script calcola il numero di cassette postali necessarie per gestire il carico utente stimato, in base alle linee guida relative al numero di accessi utente per ogni cassetta postale delle cartelle pubbliche consigliato in [Limiti per le cartelle pubbliche](limits-for-public-folders-exchange-2013-help.md).

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` Questo file di supporto è utilizzato dallo script Create-PublicFolderMailboxesForMigration.ps1 e deve essere scaricato nello stesso percorso.

Passaggio 1: Download degli script di migrazione fornisce informazioni dettagliate sul percorso in cui scaricare questi script. Verificare che tutti gli script vengano scaricati nello stesso percorso.

Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

## Versioni di Exchange supportate per la migrazione delle cartelle pubbliche ad Exchange 2013

Exchange supporta lo spostamento delle cartelle pubbliche dalle seguenti versioni legacy di Exchange Server:

  - Exchange 2010 SP3 RU8 o versione successiva

  - Exchange 2007 SP3 RU15 o versione successiva

Se è necessario spostare le cartelle pubbliche in Exchange 2013 ma i server locali non eseguono le versioni minime supportate di Exchange 2010 o Exchange 2007, consultare [Utilizzo della migrazione seriale per spostare le cartelle pubbliche in Exchange 2013 dalle versioni precedenti](https://technet.microsoft.com/it-it/library/jj150486\(v=exchg.150\)). La migrazione seriale è un'opzione possibile, ma si consiglia di aggiornare i server locali e di utilizzare la migrazione batch. La migrazione batch è molto più rapida e affidabile.

Non è possibile eseguire la migrazione delle cartelle pubbliche direttamente da Exchange 2003. Se nell'organizzazione si esegue Exchange 2003, è necessario spostare tutti i database e le repliche delle cartelle pubbliche in Exchange 2010 SP3 RU8 o versione successiva oppure in Exchange 2007 SP3 RU15 o versione successiva. Nessuna replica di cartelle pubbliche può essere lasciata su Exchange 2003. Inoltre, la posta elettronica indirizzata a una cartella pubblica di Exchange 2013 non può essere instradata tramite un server Exchange 2003.

## Che cosa è necessario sapere prima di iniziare?

  - Prima di iniziare, è consigliabile leggere attentamente il presente argomento in quanto alcuni passaggi richiedono un tempo di inattività.

  - Il server Exchange 2010 deve eseguire Exchange 2010 SP3 RU8 o versione successiva.

  - Il server Exchange 2007 deve eseguire Exchange 2007 SP3 RU15 o versione successiva.

  - Il numero massimo di cartelle pubbliche che è possibile migrare a Exchange 2013 in una singola migrazione è di 500.000.

  - In Exchange 2013, è necessario essere un membro del gruppo di ruoli Gestione organizzazione. Per informazioni dettagliate su come attivare tale gruppo di ruoli, vedere [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - In Exchange 2010, è necessario essere un membro del gruppo di ruoli RBAC Gestione organizzazione o Gestione server. Per i dettagli, vedere [Aggiunta di membri a un gruppo di ruoli](https://go.microsoft.com/fwlink/?linkid=299212).

  - In Exchange 2007, è necessario essere assegnati al ruolo di amministratore dell'organizzazione Exchange o di amministratore server di Exchange. Inoltre, è necessario essere assegnati al ruolo Amministratore cartelle pubbliche e al gruppo Amministratori locale per il server di destinazione. Per i dettagli, vedere [Aggiunta di un utente o di un gruppo a un ruolo di amministratore](https://go.microsoft.com/fwlink/p/?linkid=81779).

  - Sul server Exchange 2007, eseguire l'aggiornamento a [Windows PowerShell 2.0 e WinRM 2.0 per Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Prima di eseguire la migrazione, è necessario considerare [Limiti per le cartelle pubbliche](limits-for-public-folders-exchange-2013-help.md).

  - Prima di eseguire la migrazione, spostare tutte le cassette postali utente in Exchange 2013, perché gli utenti con cassette postali di Exchange 2007 o Exchange 2010 non avranno accesso alle cartelle pubbliche in Exchange 2013. Per ulteriori dettagli, vedere [Spostamenti di cassette postali di Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

  - In un ambiente più domini, le cartelle pubbliche abilitate alla posta smetterà di funzionare dopo la migrazione a Exchange 2013, se Exchange è in esecuzione in un dominio figlio. Ciò avviene perché Exchange 2013, gli oggetti abilitati alla posta elettronica di cartelle pubbliche devono essere sotto il dominio radice. Per risolvere questo problema, è necessario disabilitare le cartelle pubbliche abilitate alla posta elettronica e quindi abilitare alla posta li, che consentirà di spostarli nella posizione di dominio corretto.

  - Al termine della migrazione, se si desidera che i mittenti esterni inviino posta elettronica alle cartelle pubbliche abilitate alla posta migrata, è necessario concedere all’utente **Anonimo** almeno l’autorizzazione a **creare elementi**. Se non si esegue questa operazione, i mittenti esterni riceveranno una notifica di errore di recapito e i messaggi non verranno recapitati alla cartella pubblica abilitata alla posta migrata. Per ulteriori informazioni su come impostare le autorizzazioni per l’utente anonimo, vedere [Posta elettronica attiva o Disattiva posta una cartella pubblica](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/enable-or-disable-mail-for-public-folder).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione?

## Passaggio 1: Download degli script di migrazione

1.  Scaricare tutti gli script e i file di supporto da [Script di migrazione delle cartelle pubbliche](https://go.microsoft.com/fwlink/?linkid=299838).

2.  Salvare gli script nel computer locale da cui si eseguirà PowerShell. Ad esempio, C:\\PFScripts. Verificare che tutti gli script vengano salvati nello stesso percorso.

## Passaggio 2: Preparazione della migrazione

Eseguire i passaggi prerequisiti di seguito riportati prima di iniziare la migrazione.

**Passaggi prerequisiti sul server Exchange legacy**

1.  Una volta completata la migrazione, a scopo di verifica si consiglia di eseguire prima i seguenti comandi sul server Exchange legacy per scattare istantanee dell'attuale distribuzione delle cartelle pubbliche.
    
      - Utilizzare il seguente comando per scattare un'istantanea della struttura delle cartelle di origine:
        
        ```powershell
Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
```
    
      - Utilizzare il seguente comando per scattare un'istantanea delle statistiche sulle cartelle pubbliche, quali proprietario, dimensioni e conteggio degli elementi:
        
        ```powershell
Get-PublicFolderStatistics | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
```
    
      - Utilizzare il seguente comando per scattare un'istantanea delle autorizzazioni:
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    Salvare le informazioni ottenute con i precedenti comandi per confrontarle al termine della migrazione.

2.  Se il nome di una cartella pubblica contiene una barra rovesciata **\\**, in fase di migrazione le cartelle pubbliche saranno create nella cartella pubblica padre. Prima della migrazione, si consiglia di rinominare tutte le cartelle pubbliche il cui nome contiene la barra rovesciata.
    
    1.  In Exchange 2010, per individuare le cartelle pubbliche il cui nome contiene una barra rovesciata, utilizzare il comando seguente:
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  In Exchange 2007, per individuare le cartelle pubbliche il cui nome contiene una barra rovesciata, utilizzare il comando seguente:
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  Se vengono restituite cartelle, è possibile rinominarle con il comando seguente:
        
        ```powershell
Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>
```

3.  Accertarsi che non vi sia un precedente record di una migrazione riuscita.
    
    1.  Nell'esempio seguente, viene controllato lo stato di migrazione delle cartelle pubbliche.
        
        ```powershell
Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
```
        
        Se è già stata completata una migrazione, il valore delle proprietà *PublicFoldersLockedforMigration* o *PublicFolderMigrationComplete* è `$true`. Utilizzare il comando indicato nel passaggio 3b per impostare il valore su `$false`. Se il valore è impostato su `$true`, la richiesta di migrazione avrà esito negativo.
    
    2.  Se lo stato della proprietà *PublicFoldersLockedforMigration* o *PublicFolderMigrationComplete* è impostato su `$true`, utilizzare il seguente comando per impostare il valore su `$false`.
        
        ```powershell
Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
```
    

    > [!WARNING]
    > Dopo la reimpostazione di queste proprietà, è necessario attendere che le nuove impostazioni vengano rilevate in Exchange. Potrebbero essere necessarie fino a due ore.



Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [Get-PublicFolder](https://technet.microsoft.com/it-it/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/it-it/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/it-it/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/it-it/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/it-it/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Passaggi preliminari sul server Exchange 2013**

1.  Assicurarsi che non siano presenti richieste di migrazione delle cartelle pubbliche esistenti. Se ve ne sono, annullarle affinché la richiesta di migrazione non abbia esito negativo. Questo passaggio non è necessario per tutti i casi; è obbligatorio solo se si pensa che possa esserci una richiesta di migrazione esistente nella pipeline.
    
    Una richiesta di migrazione esistente può essere di due tipi: migrazione batch o migrazione seriale. I comandi per il rilevamento e per la rimozione delle richieste di ciascun tipo sono riportati di seguito.
    

    > [!IMPORTANT]
    > Prima di rimuovere una richiesta di migrazione, è importante comprendere il motivo per cui ne esisteva una. Eseguire il seguente comando per stabilire quando è stata effettuata una richiesta precedente e per diagnosticare eventuali problemi che possono essersi verificati. Potrebbe essere necessario comunicare con altri amministratori dell'organizzazione per determinare il motivo della modifica.

    
    Nell'esempio seguente vengono rilevate le eventuali richieste di migrazione seriale esistenti.
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    
    Nell'esempio seguente vengono rimosse tutte le richieste di migrazione seriale di cartelle pubbliche esistenti.
    
    ```powershell
Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
```
    
    Nell'esempio seguente vengono rilevate le eventuali richieste di migrazione batch esistenti.
    
        $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    Nell'esempio seguente vengono rimosse tutte le richieste di migrazione batch di cartelle pubbliche esistenti.
    
    ```powershell
$batch | Remove-MigrationBatch -Confirm:$false
```

2.  Accertarsi che non esistano cartelle pubbliche o cassette postali di cartelle pubbliche nei server Exchange 2013.
    
    1.  Eseguire il seguente comando per controllare se esistono cassette postali di cartelle pubbliche.
        
            Get-Mailbox -PublicFolder 
    
    2.  Se il comando non restituisce cassette postali di cartelle pubbliche, procedere con Passaggio 3: Generazione di file CSV. Se il comando ha restituito cartelle pubbliche, utilizzare il seguente comando per controllare se esistono cartelle pubbliche:
        
        ```powershell
Get-PublicFolder
```
    
    3.  Se sono presenti cartelle pubbliche, eseguire i seguenti comandi di PowerShell per rimuoverle. Accertarsi di aver salvato tutte le informazioni contenute nelle cartelle pubbliche.
        

        > [!NOTE]
        > Quando vengono rimosse le cartelle pubbliche, tutte le informazioni in esse contenute verranno eliminate definitivamente.

        ```
        Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        ```
        ```
    ```powershell
Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false
```
        ```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere gli argomenti seguenti:

  - [Get-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219164\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/it-it/library/jj218718\(v=exchg.150\))

  - [Remove-PublicFolderMigrationRequest](https://technet.microsoft.com/it-it/library/jj218625\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/it-it/library/aa997615\(v=exchg.150\))

  - [Get-MailPublicFolder](https://technet.microsoft.com/it-it/library/bb124772\(v=exchg.150\))

  - [Disable-MailPublicFolder](https://technet.microsoft.com/it-it/library/bb123781\(v=exchg.150\))

  - [Remove-PublicFolder](https://technet.microsoft.com/it-it/library/bb124894\(v=exchg.150\))

  - [Remove-Mailbox](https://technet.microsoft.com/it-it/library/aa995948\(v=exchg.150\))

## Passaggio 3: Generazione di file csv

1.  Sul server Exchange legacy, eseguire lo script `Export-PublicFolderStatistics.ps1` per creare il file di mapping Nome cartella-Dimensione cartella. Questo script deve essere eseguito da un amministratore locale. Il file conterrà due colonne: **Nomecartella** e **Dimensionicartella**. I valori della colonna **Dimensionicartella** saranno visualizzati in byte. Ad esempio, **\\PublicFolder01,10000**.
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* corrisponde al nome di dominio completo del server Cassette postali che ospita la gerarchia delle cartelle pubbliche.
    
      - *Folder to size map path* corrisponde al nome file e al percorso su una cartella condivisa in rete in cui si desidera salvare il file CSV. Più avanti in questo argomento sarà necessario accedere a questo file mediante il server Exchange 2013. Se si specifica solo il nome del file, il file sarà creato nella directory PowerShell corrente sul computer locale.

2.  Eseguire lo script `PublicFolderToMailboxMapGenerator.ps1` per creare il file di mapping Cartella pubblica-Cassetta postale. Questo file viene utilizzato per calcolare il numero corretto di cassette postali di cartelle pubbliche sul server Cassette postali di Exchange 2013.
    

    > [!NOTE]
    > Se il nome di una cartella pubblica contiene una barra rovesciata \, in fase di migrazione le cartelle pubbliche saranno create nella cartella pubblica padre. Si consiglia di esaminare il file CSV e modificare i nomi che contengono una barra rovesciata.

    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    
      - *Maximum mailbox size in bytes* corrisponde alle dimensioni massime che si desidera impostare per le nuove cassette postali di cartelle pubbliche. Quando si specifica tale impostazione, è necessario consentire l'espansione in modo che la cassetta postale di cartelle pubbliche abbia lo spazio per crescere.
    
      - *Folder to size map path* corrisponde al percorso file del file CSV creato con lo script `Export-PublicFolderStatistics.ps1`.
    
      - *Folder to mailbox map path* corrisponde al nome file e al percorso del file csv Cartella-Cassetta postale che verrà creato con questo passaggio. Se si specifica solo il nome del file, il file sarà creato nella directory PowerShell corrente sul computer locale.

## Passaggio 4: Creazione delle cassette postali di cartelle pubbliche in Exchange 2013

1.  Eseguire il seguente comando per creare le nuove cassette postali delle cartelle pubbliche di destinazione. Lo script crea una cassetta postale di destinazione per ogni cassetta postale nel file CSV generata nel passaggio 3, eseguendo lo script PublicFoldertoMailboxMapGenerator.ps1.
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* è il file generato dallo script PublicFoldertoMailboxMapGenerator.ps1 nel passaggio 3. In genere, il numero stimato di connessioni utente simultanee per l'esplorazione di una gerarchia di cartelle pubbliche è inferiore al numero totale di utenti in un'organizzazione.

## Passaggio 5: avvio della richiesta di migrazione

I passaggi per la migrazione delle cartelle pubbliche di Exchange 2007 sono diversi da quelli relativi alla migrazione delle cartelle pubbliche di Exchange 2010.


> [!TIP]
> Che la migrazione venga eseguita da Exchange 2007 o Exchange 2010, una volta create le richieste di migrazione batch con il cmdlet appropriato, è possibile visualizzarle e gestirle nell'Interfaccia di amministrazione di Exchange.



**Migrazione delle cartelle pubbliche di Exchange 2007**

1.  Le cartelle pubbliche dei sistemi legacy come OWAScratchPad e la sottostruttura di cartelle schema-root in Exchange 2007 non saranno riconosciute da Exchange 2013 e saranno trattate come elementi "non validi", causando il fallimento della migrazione. Nell'ambito della richiesta di migrazione, è necessario specificare un valore per il parametro `BadItemLimit`. Questo valore varia a seconda del numero di database delle cartelle pubbliche presenti. I seguenti comandi consentono di stabilire il numero di database delle cartelle pubbliche e di calcolare il valore del parametro `BadItemLimit` per la richiesta di migrazione.

```        
$PublicFolderDatabasesInOrg = @(Get-PublicFolderDatabase)
```
```
$BadItemLimitCount = 5 + ($PublicFolderDatabasesInOrg.Count -1)
```

2.  Sul server Exchange 2013, eseguire il comando riportato di seguito:
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> -BadItemLimit $BadItemLimitCount 

3.  Avviare la migrazione utilizzando il comando seguente:
    
    ```powershell
Start-MigrationBatch PFMigration
```

**Migrazione delle cartelle pubbliche di Exchange 2010**

1.  Sul server Exchange 2013, eseguire il comando riportato di seguito.
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> 
    
    Il parametro `NotificationEmails` è facoltativo.

2.  Avviare la migrazione utilizzando il comando seguente:
    
    ```powershell
Start-MigrationBatch PFMigration
```
    
    Oppure:
    
    È possibile avviare la migrazione nell'Interfaccia di amministrazione di Exchange.
    
    1.  Accedere a Exchange Online e aprire l'Interfaccia di amministrazione di Exchange.
    
    2.  Accedere a **Destinatari** \> **Migrazione**.
    
    3.  Selezionare il batch di migrazione appena creato, quindi fare clic sul pulsante Start.

Nella colonna **Stato** viene visualizzato lo stato del batch iniziale come **Creato**. Durante la migrazione lo stato diventa **Sincronizzazione in corso**. Completata la richiesta di migrazione, lo stato diventa **Sincronizzato**. È possibile fare doppio clic su un batch per visualizzare lo stato di singole cassette postali all'interno del batch. I processi della cassetta postale iniziano con lo stato **In coda**. All'inizio del processo lo stato è **Sincronizzazione in corso** e, una volta che `InitialSync` è completo, lo stato è **Sincronizzato**.

È possibile visualizzare e gestire l'avanzamento e il completamento della migrazione nell'interfaccia di amministrazione di Exchange. Poiché il cmdlet **New-MigrationBatch** inizializza le richieste di migrazione delle cassette postali per ogni cassetta postale delle cartelle pubbliche, è possibile visualizzare lo stato di tali richieste dalla pagina di migrazione delle cassette postali. È possibile accedere a questa pagina e creare rapporti di migrazione che possono essere ricevuti tramite posta elettronica eseguendo le seguenti operazioni:

1.  Accedere a Exchange Online e aprire l'Interfaccia di amministrazione di Exchange.

2.  Andare a **Cassetta postale** \> **Migrazione**.

3.  Selezionare la richiesta di migrazione appena creata, quindi fare clic su **Visualizza dettagli** nel riquadro **Dettagli**.

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/it-it/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/it-it/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/it-it/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/it-it/library/jj218697\(v=exchg.150\))

## Passaggio 6: Blocco delle cartelle pubbliche sul server Exchange legacy per la migrazione finale (tempi di inattività richiesti)

Fino a questo punto della migrazione, gli utenti sono stati in grado di accedere alle cartelle pubbliche. Nei passaggi successivi, gli utenti verranno disconnessi dalle cartelle pubbliche legacy e durante la sincronizzazione finale della migrazione le cartelle verranno bloccate. Gli utenti non potranno accedere alle cartelle pubbliche durante questo processo. Inoltre, tutti i messaggi inviati alle cartelle pubbliche abilitate alla posta saranno accodati e non saranno recapitati fino al completamento della migrazione.

Prima di eseguire il comando `PublicFoldersLockedForMigration` come descritto di seguito, assicurarsi che tutti i processi sono nello stato **sincronizzati**. È possibile farlo eseguendo il comando `Get-PublicFolderMailboxMigrationRequest` . Continuare con questo passaggio solo dopo aver verificato che tutti i processi sono nello stato **sincronizzati**.

Sul server Exchange legacy, eseguire il comando di seguito riportato per bloccare le cartelle pubbliche legacy per la finalizzazione.

```powershell
Set-OrganizationConfig -PublicFoldersLockedForMigration:$true
```


> [!NOTE]
> Se per un motivo qualsiasi il file del batch di migrazione non viene finalizzato (il parametro <STRONG>PublicFolderMigrationComplete</STRONG> viene visualizzato come <STRONG>False</STRONG>), sul server legacy, riavviare l' Archivio Informazioni.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\)).

Se l'organizzazione dispone di più database delle cartelle pubbliche, sarà necessario attendere il completamento della replica delle cartelle pubbliche per confermare che tutti i database delle cartelle pubbliche abbiano estratto il flag `PublicFoldersLockedForMigration` e che eventuali modifiche in sospeso apportate dagli utenti alle cartelle siano confluite nell'organizzazione. L'operazione potrebbe richiedere diverse ore.

## Passaggio 7: finalizzazione della migrazione di cartelle pubbliche (tempi di inattività richiesti)

Per modificare il tipo di distribuzione di Exchange 2013 in **Remoto**, eseguire il comando riportato di seguito:

```powershell
Set-OrganizationConfig -PublicFoldersEnabled Remote
```

Al termine dell'operazione, è possibile completare la migrazione delle cartelle pubbliche eseguendo il comando riportato di seguito:

```powershell
Complete-MigrationBatch PublicFolderMigration
```

In alternativa, nell'Interfaccia di amministrazione di Exchange, è possibile completare la migrazione facendo clic su **Completa il batch di migrazione**.

Al termine della migrazione, Exchange eseguirà una sincronizzazione finale tra i server Exchange legacy ed Exchange 2013. Se la sincronizzazione finale ha esito positivo, le cartelle pubbliche sul server Exchange 2013 sarà sbloccate e lo stato del batch di migrazione verrà modificato al **completamento** e quindi viene **completata**. È usuale per il batch di migrazione richiedere alcune ore prima di modifiche apportate al relativo stato da **sincronizzati** al **completamento**, quindi verrà avviata la sincronizzazione finale.

## Passaggio 8: Verifica e sblocco della migrazione delle cartelle pubbliche

Dopo aver finalizzato la migrazione delle cartelle pubbliche, è necessario effettuare il test seguente per accertarsi che la migrazione sia avvenuta correttamente. In tal modo è possibile verificare la gerarchia delle cartelle pubbliche migrate prima di passare all'uso delle cartelle pubbliche di Exchange 2013.

1.  In PowerShell, eseguire il comando riportato di seguito per assegnare alcune cassette postali di prova per utilizzare una cassetta postale di cassette pubbliche migrata come cassetta postale di cartelle pubbliche predefinita.
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  Accedere a Outlook 2007 o versione successiva con l'utente di prova identificato nel passaggio precedente, quindi effettuare i seguenti test delle cartelle pubbliche:
    
      - Visualizzare la gerarchia.
    
      - Controllare le autorizzazioni.
    
      - Creare ed eliminare cartelle pubbliche.
    
      - Pubblicare il contenuto ed eliminare il contenuto da una cartella pubblica.

3.  In caso di problemi, vedere Roll back the migration più avanti in questo argomento. Se il contenuto e la gerarchia delle cartelle pubbliche sono accettabili e funzionano nel modo previsto, eseguire il comando di seguito riportato per sbloccare le cartelle pubbliche per tutti gli altri utenti.
    
    ```powershell
Get-Mailbox -PublicFolder | Set-Mailbox -PublicFolder -IsExcludedFromServingHierarchy $false
```
    

    > [!IMPORTANT]
    > Non utilizzare il parametro <EM>IsExcludedFromServingHierarchy</EM> dopo il completamento della convalida iniziale della migrazione perché questo parametro viene utilizzato dal servizio di gestione archiviazione automatica per Exchange Online.



4.  Sul server Exchange legacy, eseguire il comando di seguito riportato per indicare che la migrazione delle cartelle pubbliche è stata completata.
    
    ```powershell
Set-OrganizationConfig -PublicFolderMigrationComplete:$true
```

5.  Dopo aver verificato che è stata completata la migrazione, eseguire il seguente comando:
    
    ```powershell
Set-OrganizationConfig -PublicFoldersEnabled Local
```

6.  Infine, se si desidera che i mittenti esterni inviino posta elettronica alle cartelle pubbliche abilitate alla posta migrata, è necessario concedere all’utente **Anonimo** almeno l’autorizzazione a **creare elementi**. Se non si esegue questa operazione, i mittenti esterni riceveranno una notifica di errore di recapito e i messaggi non verranno recapitati alla cartella pubblica abilitata alla posta migrata.
    
    È possibile utilizzare Shell o Outlook per impostare le autorizzazioni per l’utente anonimo. Per ulteriori informazioni su come impostare le autorizzazioni per l’utente anonimo, vedere [Posta elettronica attiva o Disattiva posta una cartella pubblica](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/enable-or-disable-mail-for-public-folder).

## Come verificare se l'operazione ha avuto esito positivo?

In Step 2: Prepare for the migration era stato suggerito di scattare istantanee delle autorizzazioni, delle statistiche e della struttura delle cartelle pubbliche prima di iniziare la migrazione. La seguente procedura consentirà di verificare la corretta migrazione delle cartelle pubbliche tramite lo scatto delle stesse istantanee una volta completata la migrazione. È possibile, quindi, confrontare i dati in entrambi i file per verificare la riuscita dell'operazione.

1.  Eseguire il seguente comando per scattare un'istantanea della nuova struttura delle cartelle.
    
    ```powershell
Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml
```

2.  Utilizzare il seguente comando per scattare un'istantanea delle statistiche sulle cartelle pubbliche, quali proprietario, dimensioni e conteggio degli elementi.
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  Utilizzare il seguente comando per scattare un'istantanea delle autorizzazioni.
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## Rimozione dei database delle cartelle pubbliche dai server Exchange legacy

Al termine della migrazione, dopo aver verificato che le cartelle pubbliche di Exchange 2013 funzionano nel modo previsto, rimuovere i database delle cartelle pubbliche sui server Exchange legacy.

  - Per i dettagli sulla rimozione dei database delle cartelle pubbliche dai server Exchange 2007, vedere [Rimozione di database delle cartelle pubbliche](https://go.microsoft.com/fwlink/?linkid=123678).

  - Per i dettagli sulla rimozione dei database delle cartelle pubbliche dai server Exchange 2010, vedere [Rimozione di database delle cartelle pubbliche](https://go.microsoft.com/fwlink/?linkid=81409).

## Ripristino della migrazione

Se si riscontrano problemi con la migrazione e si ha la necessità di riattivare le proprie cartelle pubbliche di Exchange 2010, procedere come segue.


> [!WARNING]
> Se si annulla la migrazione e si torna ai server Exchange legacy, si perderanno eventuali messaggi di posta elettronica inviati alle cartelle pubbliche abilitate alla posta o eventuale contenuto pubblicato nelle cartelle pubbliche in Exchange 2013 dopo la migrazione. Per salvare il contenuto, è necessario esportarlo in un file PST e importarlo quindi nelle cartelle pubbliche legacy una volta completato il ripristino.



1.  Sul server Exchange legacy, eseguire il comando di seguito riportato per sbloccare le cartelle pubbliche legacy. Questo processo potrebbe richiedere diverse ore.
    
    ```powershell
Set-OrganizationConfig -PublicFoldersLockedForMigration:$False
```

2.  Sul server Exchange 2013, eseguire il comando riportato di seguito per rimuovere le cassette postali delle cartelle pubbliche.
    
        Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        
    ```powershell
Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false
```

3.  Sul server Exchange legacy, eseguire il comando di seguito riportato per impostare il flag `PublicFolderMigrationComplete` su `$false`.
    
    ```powershell
Set-OrganizationConfig -PublicFolderMigrationComplete:$False
```


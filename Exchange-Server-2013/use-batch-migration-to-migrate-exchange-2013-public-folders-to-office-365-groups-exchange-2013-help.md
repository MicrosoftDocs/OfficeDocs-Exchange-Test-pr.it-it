---
title: 'Utilizzare la migrazione batch per migrare le cartelle pubbliche di Exchange 2013 nei gruppi di Office 365: Exchange 2013 Help'
TOCTitle: Utilizzare la migrazione batch per migrare le cartelle pubbliche di Exchange 2013 nei gruppi di Office 365
ms:assetid: 1d800576-957d-4916-ae2a-55c08ca75be1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt843873(v=EXCHG.150)
ms:contentKeyID: 74468728
ms.date: 03/26/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utilizzare la migrazione batch per migrare le cartelle pubbliche di Exchange 2013 nei gruppi di Office 365

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2018-03-26_

**Sintesi:** come spostare le cartelle pubbliche di Exchange 2013 nei gruppi di Office 365.

Tramite un processo noto come *migrazione batch*, è possibile spostare alcune o tutte le cartelle pubbliche di Exchange 2013 nei gruppi di Office 365. I gruppi sono una nuova offerta di collaborazione di Microsoft che garantisce alcuni vantaggi rispetto alle cartelle pubbliche. Vedere [Eseguire la migrazione delle cartelle pubbliche nei gruppi di Office 365](migrate-your-public-folders-to-office-365-groups-exchange-2013-help.md) per una panoramica delle differenze tra le cartelle pubbliche e i gruppi e dei motivi per i quali l'organizzazione potrebbe o non potrebbe trarre vantaggio dal passaggio ai gruppi.

In questo articolo sono descritte procedure dettagliate per eseguire la migrazione batch effettiva delle cartelle pubbliche di Exchange 2013.

## Che cosa è necessario sapere prima di iniziare

Assicurarsi che tutte le condizioni seguenti siano soddisfatte prima di iniziare a preparare la migrazione.

  - Il server Exchange 2013 deve eseguire **Exchange 2013 CU15** o versione successiva.

  - In Exchange Online, è necessario essere un membro del gruppo di ruoli Gestione organizzazione. Questo gruppo di ruoli differisce dalle autorizzazioni assegnate in fase di sottoscrizione a Office 365 o Exchange Online. Per informazioni dettagliate sull'abilitazione del gruppo di ruoli Gestione organizzazione, vedere [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - In Exchange 2013, è necessario essere un membro del gruppo di ruoli RBAC Gestione organizzazione o Gestione server. Per i dettagli, vedere [Aggiunta di membri a un gruppo di ruoli](https://go.microsoft.com/fwlink/?linkid=299212).

  - Prima di eseguire la migrazione delle cartelle pubbliche ai gruppi di Office 365, è consigliabile spostare le cassette postali degli utenti in Office 365 per gli utenti che richiedono l'accesso ai gruppi di Office 365 dopo la migrazione. Per ulteriori informazioni, vedere [Modalità di migrazione della posta elettronica a Office 365](https://support.office.com/article/ways-to-migrate-multiple-email-accounts-to-office-365-0a4913fe-60fb-498f-9155-a86516418842).

  - Il proxy MRS deve essere abilitato su almeno un server di Exchange, e tale server deve ospitare anche cassette postali delle cartelle pubbliche. Per i dettagli, vedere [Abilitare l'endpoint del Proxy MRS per gli spostamenti remoti](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange (EAC) o Exchange Management Console (EMC) per eseguire questa procedura. Nei server Exchange 2013, è necessario utilizzare Exchange Management Shell. Per Exchange Online, è necessario utilizzare Exchange Online PowerShell. Per ulteriori informazioni, vedere [Connettersi a Exchange Online utilizzando una sessione PowerShell remota](https://technet.microsoft.com/library/jj984289\(v=exchg.150\).aspx).

  - Solo le cartelle pubbliche di tipo calendario e posta possono essere al momento migrate nei gruppi di Office 365; la migrazione di altri tipi di cartelle pubbliche non è supportata. Inoltre, i gruppi di destinazione in Office 365 dovrebbero essere creati prima della migrazione.

  - Il processo di migrazione batch copia solo i messaggi e gli elementi del calendario dalle cartelle pubbliche per la migrazione ai gruppi di Office 365. Non copia altri tipi di contenuto delle cartelle pubbliche come regole, criteri e autorizzazioni poiché non sono supportati nei gruppi di Office 365.

  - I gruppi di Office 365 includono una cassetta postale da 50 GB. Assicurarsi che la somma dei dati della cartella pubblica di cui eseguir la migrazione sia inferiore a 50 GB. Inoltre, lasciare spazio di archiviazione per contenuto aggiuntivo che gli utenti aggiungeranno in futuro, dopo la migrazione. Si consiglia di eseguire la migrazione di cartelle pubbliche di dimensioni totali inferiori a 25 GB.

  - Non si tratta di una migrazione "tutto o niente". È possibile individuare e selezionare cartelle pubbliche specifiche per cui eseguire la migrazione, e solo di queste cartelle pubbliche verrà eseguita la migrazione. Se la cartella pubblica migrata dispone di sottocartelle, le sottocartelle non verranno automaticamente incluse nella migrazione. Se è necessario eseguirne la migrazione, è necessario includerle in modo esplicito.

  - Le cartelle pubbliche non verranno interessate in alcun modo da questa migrazione. Tuttavia, una volta che si utilizza il nostro script lock-down per rendere le cartelle pubbliche migrate di sola lettura, gli utenti saranno obbligati a usare i gruppi di Office 365 invece delle cartelle pubbliche. 

  - Prima di iniziare, è consigliabile leggere attentamente il presente articolo in quanto alcuni passaggi richiedono un tempo di inattività.

## Passaggio 1: ottenere gli script

La migrazione batch ai gruppi di Office 365 richiede l'esecuzione di una serie di script in momenti diversi durante la migrazione, come descritto di seguito in questo articolo. Scaricare gli script e i relativi file di supporto [da questo percorso](https://www.microsoft.com/it-it/download/details.aspx?id=55985). Dopo che tutti gli script e i file vengono scaricati, salvarli nello stesso percorso, ad esempio `c:\PFtoGroups\Scripts`.

Prima di procedere, verificare di aver scaricato e salvato tutti i seguenti script e file:


> [!NOTE]
> Assicurarsi di salvare tutti gli script e file nello stesso percorso.



  - **AddMembersToGroups.ps1**. Questo script aggiunge membri e proprietari ai gruppi di Office 365 in base alle voci di autorizzazione nelle cartelle pubbliche di origine.

  - **AddMembersToGroups.strings.psd1**. Questo file di supporto viene utilizzato dallo script `AddMembersToGroups.ps1`.

  - **LockAndSavePublicFolderProperties.ps1**. Questo script rende le cartelle pubbliche di sola lettura per impedire le modifiche e trasferisce le proprietà delle cartelle pubbliche correlate alla posta (ammesso che nelle cartelle pubbliche siano abilitate per la posta) nei gruppi di destinazione, che reindirizzeranno i messaggi di posta elettronica dalle cartelle pubbliche ai gruppi di destinazione. Questo script inoltre esegue di nuovo il backup delle voci autorizzazione e delle proprietà della posta prima di modificarle.

  - **LockAndSavePublicFolderProperties.strings.psd1:** Questo file di supporto viene utilizzato dallo script `LockAndSavePublicFolderProperties.ps1`.

  - **UnlockAndRestorePublicFolderProperties.ps1**. Questo script ripristina i diritti di accesso e le proprietà della posta delle cartelle pubbliche utilizzando i file di backup creati da `LockandSavePublicFolderProperties.ps1`.

  - **UnlockAndRestorePublicFolderProperties.strings.psd1**. Questo file di supporto viene utilizzato dallo script `UnlockAndRestorePublicFolderProperties.ps1`.

  - **WriteLog.ps1**. Questo script consente ai tre script precedenti di scrivere log.

  - **RetryScriptBlock.ps1**. Questo script consente agli script `AddMembersToGroups`, `LockAndSavePublicFolderProperties` e `UnlockAndRestorePublicFolderProperties` di riprovare determinate azioni in caso di errori temporanei.

Per informazioni dettagliate su `AddMembersToGroups.ps1`, `LockAndSavePublicFolderProperties.ps1` e `UnlockAndRestorePublicFolderProperties.ps1` e sulle attività che eseguono nell'ambiente, vedere Script di migrazione più avanti in questo articolo.

## Passaggio 2: preparazione della migrazione

La seguente procedura è necessaria per preparare l'organizzazione per la migrazione:

1.  Compilare un elenco delle cartelle pubbliche (del tipo di posta elettronica e calendario) che si desidera migrare nei gruppi di Office 365.

2.  Avere un elenco di gruppi di destinazione corrispondenti per ogni cartella pubblica migrata. È possibile creare un nuovo gruppo in Office 365 per ogni cartella pubblica o utilizzare un gruppo esistente. Se si sta creando un nuovo gruppo, vedere [Informazioni sui gruppi di Office 365](https://go.microsoft.com/fwlink/p/?linkid=858521) per comprendere le impostazioni che un gruppo deve avere. Se una cartella pubblica di cui si esegue la migrazione ha l'autorizzazione predefinita impostata su **Autore** o sopra, è consigliabile creare il gruppo corrispondente in Office 365 con l'impostazione di privacy **Pubblico**. Tuttavia, affinché gli utenti possano visualizzare il gruppo pubblico nel nodo **Gruppi** in Outlook, dovranno comunque unirsi al gruppo.

3.  Rinominare le cartelle pubbliche che contengono una barra rovesciata (**\\**) nel nome. In caso contrario, le cartelle pubbliche potrebbero non venire migrate correttamente.

4.  È necessario abilitare la funzionalità di migrazione **PAW** per il tenant di Office 365. Per verificare questo, eseguire il seguente comando in Exchange Online PowerShell:
    
        Get-MigrationConfig
    
    Se in **Funzionalità** viene elencato **PAW**, allora la funzionalità è abilitata ed è possibile continuare con *Passaggio 3: creazione del file .csv*.
    
    Se la funzionalità PAW non è ancora abilitata per il tenant, potrebbe essere perché sono presenti dei batch di migrazione esistenti, o batch di cartelle pubbliche o batch di utenti. Tali batch potrebbero essere in uno stato qualsiasi, compreso Completato. In questo caso, completare e rimuovere i batch di migrazione esistenti finché non viene restituito nessun record quando si esegue `Get-MigrationBatch`. Dopo avere rimosso tutti i batch esistenti, la funzionalità PAW dovrebbe essere abilitata automaticamente. La modifica potrebbe non essere applicata immediatamente in `Get-MigrationConfig`, ma ciò è normale. Al termine dell'operazione, è possibile continuare a creare nuovi batch di migrazioni utente.

## Passaggio 3: creazione di un file .csv

Creare un file .csv, che fornisce input per uno degli script di migrazione.

Il file .csv contiene le seguenti colonne:

  - **FolderPath**. Percorso della cartella pubblica da migrare.

  - **TargetGroupMailbox**. Indirizzo SMTP del gruppo di destinazione in Office 365. È possibile eseguire il seguente comando per visualizzare l'indirizzo SMTP principale.
    
        Get-UnifiedGroup <alias of the group> | Format-Table PrimarySmtpAddress

File .csv di esempio:

    "FolderPath","TargetGroupMailbox"
    "\Sales","sales@contoso.onmicrosoft.com"
    "\Sales\EMEA","emeasales@contoso.onmicrosoft.com"

Tenere presente che una cartella di posta elettronica e una cartella di calendario possono essere unite in un solo gruppo in Office 365. Tuttavia, non è supportato nessun altro scenario di più cartelle pubbliche unite in un gruppo all'interno di un solo batch di migrazione. Se è necessario eseguire il mapping di più cartelle pubbliche nello stesso gruppo di Office 365, è possibile eseguire tale operazione eseguendo più batch di migrazione diversi, che dovrebbero essere eseguiti in modo consecutivo, uno dopo l'altro. È possibile includere fino a 500 voci in ogni batch di migrazione.

Una cartella pubblica deve essere migrata in un solo gruppo in un batch di migrazione.

## Passaggio 4: avvio della richiesta di migrazione

In questo passaggio, raccogliere informazioni dall'ambiente di Exchange, quindi utilizzare tali informazioni in Exchange Online PowerShell per creare un batch di migrazione. In seguito, avviare la migrazione.

1.  Nel server di Exchange 2013 individuare il server dell'endpoint del proxy MRS e annotarlo. Questa informazione servirà per eseguire la richiesta di migrazione.

2.  In Exchange Online PowerShell, utilizzare le informazioni restituite che sono state indicate in precedenza nel passaggio 1 per eseguire i comandi seguenti. Le variabili di questi comandi sono i valori del passaggio 1.
    
    1.  Passare le credenziali di un utente con autorizzazioni amministrative sull'ambiente locale di Exchange 2013 nella variabile `$Source_Credential`. Quando si esegue la richiesta di migrazione in Exchange Online, queste credenziali saranno utilizzate per ottenere l'accesso ai server di Exchange 2013 per copiare il contenuto in Exchange Online.
        
            $Source_Credential = Get-Credential
            <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  Utilizzare le informazioni sul server proxy MRS dall'ambiente di Exchange 2013 annotate nel passaggio 1 e passare tale valore nella variabile `$Source_RemoteServer`.
        
            $Source_RemoteServer = "<MRS proxy endpoint>"

3.  In Exchange Online PowerShell, per creare un endpoint di migrazione, eseguire il comando seguente:
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolderToUnifiedGroup -Name PFToGroupEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential

4.  Eseguire il seguente comando per creare un nuovo batch di migrazione delle cartelle pubbliche nel gruppo di Office 365. In questo comando:
    
      - **CSVData** è il file .csv creato durante il *Passaggio 3: creazione del file .csv*. Assicurarsi di fornire il percorso completo del file. Se il file è stato spostato per un motivo qualsiasi, accertarsi di verificare e usare il nuovo percorso.
    
      - **NotificationEmails** è un parametro opzionale che è possibile utilizzare per impostare gli indirizzi di posta elettronica che riceveranno le notifiche sullo stato e sull'avanzamento della migrazione.
    
      - **AutoStart** è un parametro facoltativo che, se utilizzato, inizia il batch di migrazione subito dopo la creazione.
    
      - **PublicFolderToUnifiedGroup** è il parametro per indicare che si tratta di un batch di migrazione di una cartella pubblica nei gruppi di Office 365.
    
    <!-- end list -->
    
        New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]

5.  Avviare la migrazione utilizzando il comando seguente in Exchange Online PowerShell. Tenere presente che questo passaggio è necessario solo se il parametro `-AutoStart` non è stato utilizzato durante la creazione del batch sopra nel passaggio 4.
    
        Start-MigrationBatch PublicFolderToGroupMigration

Se le migrazioni batch devono essere create utilizzando il cmdlet `New-MigrationBatch` in Exchange Online PowerShell, l'avanzamento e il completamento della migrazione possono essere visualizzate e gestite in Interfaccia di amministrazione di Exchange. È inoltre possibile visualizzare l'avanzamento della migrazione eseguendo i cmdlet [Get-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219164\(v=exchg.150\)) e [Get-MigrationUser](https://technet.microsoft.com/it-it/library/jj218702\(v=exchg.150\)). Il cmdlet `New-MigrationBatch` inizializza un utente di migrazione per ogni cassetta postale del gruppo di Office 365 ed è possibile visualizzare lo stato di queste richieste utilizzando la pagina di migrazione della cassetta postale.

Per visualizzare la pagina della migrazione della cassetta postale:

1.  In Exchange Online, aprire Interfaccia di amministrazione di Exchange.

2.  Andare a **Destinatari**, quindi selezionare **Migrazione**.

3.  Selezionare la richiesta di migrazione appena creata, quindi nel riquadro **Dettagli** fare clic su **Visualizza dettagli**.

Quando lo stato batch è **Completato**, è possibile passare al *Passaggio 5: aggiunta di membri a gruppi di Office 365 dalle cartelle pubbliche*.

## Passaggio 5: aggiunta di membri a gruppi di Office 365 dalle cartelle pubbliche

È possibile aggiungere membri al gruppo di destinazione in Office 365 manualmente in base alle esigenze. Tuttavia, se si desidera aggiungere membri al gruppo in base alle voci autorizzazione nelle cartelle pubbliche, è necessario farlo eseguendo lo script `AddMembersToGroups.ps1` nel server di Exchange 2013 come illustrato nel seguente comando. Le cassette postali degli utenti devono essere sincronizzate con Exchange Online per poter essere aggiunte come membri di un gruppo di Office 365. Per sapere quali autorizzazioni di cartelle pubbliche sono idonee per essere aggiunte come membri di un gruppo in Office 365, vedere Script di migrazione più avanti in questo articolo.

Nel comando seguente:

  - **MappingCsv** è il file .csv creato durante il *Passaggio 3: creazione del file .csv*. Assicurarsi di fornire il percorso completo del file. Se il file è stato spostato per un motivo qualsiasi, accertarsi di verificare e usare il nuovo percorso.

  - **BackupDir** è la directory in cui verranno archiviati i file di log di migrazione.

  - **ArePublicFoldersOnPremises** è un parametro per indicare se le cartelle pubbliche si trovano in locale o in Exchange Online.

  - **Credential** è il nome e la password dell'utente di Exchange Online.

<!-- end list -->

    .\AddMembersToGroups.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

Una volta che gli utenti sono stati aggiunti a un gruppo in Office 365, possono iniziare a utilizzarlo.

## Passaggio 6: blocco delle cartelle pubbliche (tempo di inattività delle cartelle pubbliche necessario)

Quando la maggior parte dei dati nelle cartelle pubbliche è stata migrata nei gruppi di Office 365, è possibile eseguire lo script `LockAndSavePublicFolderProperties.ps1` nel server di Exchange 2013 per rendere le cartelle pubbliche di sola lettura. Questo passaggio garantisce che non vengano aggiunti nuovi dati alle cartelle pubbliche prima che la migrazione sia completata.


> [!NOTE]
> Se sono presenti cartelle pubbliche abilitate alla posta elettronica (MEPF) tra le cartelle pubbliche migrate, in questo passaggio alcune proprietà delle MEPF (come gli indirizzi SMTP) vengono copiate nel gruppo di Office 365 corrispondente e quindi viene disabilitata la posta per la cartella pubblica. Poiché la posta per le MEPF verrà disabilitata dopo l'esecuzione di questo script, si inizia a visualizzare messaggi di posta elettronica inviati alle MEPF anziché essere ricevuti nei gruppi corrispondenti. Per ulteriori informazioni, vedere Script di migrazione più avanti in questo articolo.



Nel comando seguente:

  - **MappingCsv** è il file .csv creato durante il *Passaggio 3: creazione del file .csv*. Assicurarsi di fornire il percorso completo del file. Se il file è stato spostato per un motivo qualsiasi, accertarsi di verificare e usare il nuovo percorso.

  - **BackupDir** è la directory in cui vengono archiviati i file di cui viene eseguito il backup per le voci autorizzazione, le proprietà delle MEPF e i file di log della migrazione. Il backup sarà utile nel caso in cui sia necessario eseguire il rollback alle cartelle pubbliche.

  - **ArePublicFoldersOnPremises** è un parametro per indicare se le cartelle pubbliche si trovano in locale o in Exchange Online.

  - **Credential** è il nome e la password dell'utente di Exchange Online.

<!-- end list -->

    .\LockAndSavePublicFolderProperties.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

## Passaggio 7: finalizzazione della cartella pubblica per la migrazione nei gruppi di Office 365

Dopo aver reso le cartelle pubbliche di sola lettura, è necessario ripetere la migrazione. Questa operazione è necessaria per una copia incrementale finale dei dati. Prima di poter eseguire la migrazione, sarà necessario rimuovere il batch esistente eseguendo il seguente comando:

    Remove-MigrationBatch <name of migration batch>

Successivamente, creare un nuovo batch con lo stesso file .csv eseguendo il seguente comando. In questo comando:

  - **CsvData** è il file .csv creato durante il *Passaggio 3: creazione del file .csv*. Assicurarsi di fornire il percorso completo del file. Se il file è stato spostato per un motivo qualsiasi, accertarsi di verificare e usare il nuovo percorso.

  - **NotificationEmails** è un parametro opzionale che è possibile utilizzare per impostare gli indirizzi di posta elettronica che riceveranno le notifiche sullo stato e sull'avanzamento della migrazione.

  - **AutoStart** è un parametro facoltativo che, se utilizzato, inizia il batch di migrazione subito dopo la creazione.

<!-- end list -->

    New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]

Dopo aver creato il nuovo batch, avviare la migrazione utilizzando il comando seguente in Exchange Online PowerShell. Questo passaggio è necessario solo se il parametro `-AutoStart` non è stato utilizzato nel comando precedente.

    Start-MigrationBatch PublicFolderToGroupMigration

Dopo aver completato il passaggio (lo stato del batch è **Completato**), verificare che tutti i dati siano stati copiati nei gruppi di Office 365. A questo punto, se si è soddisfatti dell'esperienza con i gruppi, è possibile iniziare a eliminare le cartelle pubbliche migrate dall'ambiente di Exchange 2013.


> [!IMPORTANT]
> Sebbene esistano procedure supportate per eseguire il rollback della migrazione e tornare alle cartelle pubbliche, ciò non è possibile dopo aver eliminato le cartelle pubbliche di origine. Per ulteriori informazioni, vedere Come eseguire il rollback alle cartelle pubbliche dai gruppi di Office 365.



## Problemi noti

I seguenti problemi noti possono verificarsi durante una tipica migrazione delle cartelle pubbliche nei gruppi di Office 365.

  - Lo script che trasferisce l'indirizzo SMTP dalle cartelle pubbliche abilitate alla posta elettronica al gruppo di Office 365 aggiunge gli indirizzi solo come indirizzi di posta elettronica secondari in Exchange Online. Pertanto, se nell'ambiente in uso è stato configurato Exchange Online Protection (EOP) o il flusso della posta centralizzato, vengono riscontrati problemi nell'invio della posta ai gruppi (agli indirizzi e-mail secondari) dopo la migrazione.

  - Se il file di mapping .csv dispone di una voce con un percorso della cartella pubblica non valido, il batch di migrazione viene visualizzato come **Completato** senza generare un errore e non vengono copiati altri dati.

## Script di migrazione

Per riferimento, in questa sezione vengono fornite descrizioni dettagliate per tre script di migrazione e le attività che eseguono nell'ambiente di Exchange. Tutti gli script e i file di supporto [possono essere scaricati da questo percorso](https://www.microsoft.com/it-it/download/details.aspx?id=55985).

## AddMembersToGroups.ps1

Questo script legge le autorizzazioni delle cartelle pubbliche migrate e quindi aggiunge membri e proprietari ai gruppi di Office 365 nel modo seguente:

  - Gli utenti con i ruoli di autorizzazione seguenti vengono aggiunti come membri a un gruppo in Office 365. **Ruoli di autorizzazione:** Owner, PublishingEditor, Editor, PublishingAuthor, Author

  - Inoltre, anche gli utenti con i diritti di accesso minimi seguenti vengono aggiunti come membri a un gruppo in Office 365. **Diritti di accesso:** ReadItems, CreateItems, FolderVisible, EditOwnedItems, DeleteOwnedItems

  - Gli utenti con il diritto di accesso "Owner" vengono aggiunti come proprietari a un gruppo e gli utenti con altri diritti di accesso idonei vengono aggiunti come membri.

  - I gruppi di sicurezza non possono essere aggiunti come membri ai gruppi in Office 365. Pertanto, vengono espansi e quindi i singoli utenti vengono aggiunti come membri o proprietari ai gruppi in base ai diritti di accesso del gruppo di sicurezza.

  - Quando gli utenti nei gruppi di sicurezza dotati dei diritti di accesso per una cartella pubblica dispongono anche delle autorizzazioni esplicite per la stessa cartella pubblica, le autorizzazioni esplicite avranno la priorità. Si consideri, ad esempio, un caso in cui un gruppo di sicurezza denominato "SG1" include i membri User1 e User2. Le voci autorizzazione per la cartella pubblica "PF1" sono le seguenti:
    
    SG1: Author in PF1
    
    User1: Owner in PF1
    
    In questo caso, User1 viene aggiunto come proprietario al gruppo in Office 365.

  - Quando l'autorizzazione predefinita di una cartella pubblica migrata è "Author" o sopra, lo script suggerisce di configurare l'impostazione della privacy del gruppo corrispondente come "Public".

Questo script può essere eseguito anche dopo il blocco delle cartelle pubbliche, con il parametro di `ArePublicFoldersLocked` impostato su ` $true`. In questo scenario, lo script legge le autorizzazioni dal file di backup creato durante il blocco.

## LockAndSavePublicFolderProperties.ps1

Questo script rende le cartelle pubbliche migrate di sola lettura. Quando viene eseguita la migrazione di cartelle pubbliche abilitate alla posta elettronica, per tali cartelle viene innanzitutto disabilitata la posta e gli indirizzi SMTP vengono aggiunti ai rispettivi gruppi in Office 365. Successivamente, le voci autorizzazione vengono modificate per rendere tali cartelle di sola lettura. Un backup delle proprietà di posta delle cartelle pubbliche abilitate alla posta elettronica, oltre alle voci autorizzazione di tutte le cartelle pubbliche, vengono copiati prima di apportarvi eventuali modifiche.

Se sono presenti più batch di migrazione, è necessario utilizzare una directory di backup separata con ogni file di mapping .csv.

Oltre alle rispettive cartelle pubbliche abilitate alla posta elettronica e ai gruppi di Office 365, vengono archiviate le proprietà di posta seguenti:

  - PrimarySMTPAddress

  - EmailAddresses

  - ExternalEmailAddress

  - EmailAddressPolicyEnabled

  - GrantSendOnBehalfTo

  - Elenco Trustee SendAs

Le proprietà di posta di cui sopra vengono archiviate in un file .csv, che può essere utilizzato nel processo di rollback (se si desidera tornare alle cartelle pubbliche, vedere Come eseguire il rollback alle cartelle pubbliche dai gruppi di Office 365 per ulteriori informazioni). Uno snapshot delle proprietà delle cartelle pubbliche abilitate alla posta viene inoltre archiviato in un file denominato PfMailProperties.csv. Il file non è necessario per il processo di rollback, ma può essere usato come riferimento.

le seguenti proprietà di posta vengono migrate al gruppo di destinazione come parte del blocco:

  - PrimarySMTPAddress

  - EmailAddresses

  - Elenco Trustee SendAs

  - GrantSendOnBehalfTo

Lo script assicura che PrimarySMTPAddress e EmailAddresses delle cartelle pubbliche abilitate alla posta in fase di migrazione vengano aggiunti come indirizzi SMTP secondari dei gruppi corrispondenti in Office 365. Inoltre, alle autorizzazioni SendAs e SendOnBehalfTo di utenti nelle cartelle pubbliche abilitate alla posta viene attribuita un'autorizzazione equivalente nei gruppi di destinazione corrispondenti.

**Diritti di accesso consentiti**

Solo i diritti di accesso riportati di seguito sono concessi agli utenti per garantire che le cartelle pubbliche siano rese di sola lettura per tutti gli utenti. Sono archiviati in **ListOfAccessRightsAllowed**.

  - ReadItems

  - CreateSubfolders

  - FolderContact

  - FolderVisible

Le voci autorizzazione verranno modificate nel modo seguente:

1.  ###  
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Prima del blocco</th>
    <th>Dopo il blocco</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Nessuna</p></td>
    <td><p>Nessuna</p></td>
    </tr>
    <tr class="even">
    <td><p>AvailabilityOnly</p></td>
    <td><p>AvailabilityOnly</p></td>
    </tr>
    <tr class="odd">
    <td><p>LimitedDetails</p></td>
    <td><p>LimitedDetails</p></td>
    </tr>
    <tr class="even">
    <td><p>Collaboratore</p></td>
    <td><p>FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Reviewer</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>NonEditingAuthor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Author</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>Editor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>PublishingAuthor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>PublishingEditor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Proprietario</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderContact, FolderVisible</p></td>
    </tr>
    </tbody>
    </table>


2.  I diritti di accesso degli utenti senza autorizzazioni di lettura non vengono modificati e continueranno a essere bloccati dai diritti di lettura.

3.  Per gli utenti con ruoli personalizzati, tutti i diritti di accesso che non sono presenti in **ListOfAccessRightsAllowed** verranno rimossi. Nel caso in cui gli utenti non dispongano di alcun diritto di accesso dall'elenco di quelli consentiti dopo l'applicazione di filtri, i diritti di accesso di tali utenti vengono impostati su "None".

Potrebbe verificarsi un'interruzione nell'invio di messaggi di posta elettronica alle cartelle pubbliche abilitate alla posta tra il momento in cui viene disabilitata la posta per le cartelle e quello in cui i rispettivi indirizzi SMTP vengono aggiunti ai gruppi di Office 365.

## UnlockAndRestorePublicFolderProperties.ps1

Questo script assegna di nuovo le autorizzazioni alle cartelle pubbliche, in base al file di backup creato durante il blocco delle cartelle pubbliche. Questo script, inoltre, riabilita la posta per le cartelle pubbliche per le quali era stata disabilitata, dopo aver rimosso gli indirizzi SMTP delle cartelle pubbliche dai rispettivi gruppi in Office 365. Durante questo processo, potrebbe esserci un breve tempo di inattività.

## Come eseguire il rollback alle cartelle pubbliche dai gruppi di Office 365

Se si cambia idea e si desidera tornare a usare le cartelle pubbliche dopo aver utilizzato i gruppi di Office 365, il comando riportato di seguito consente di ripristinare l'ambiente allo stato precedente alla migrazione. È possibile eseguire un rollback finché i file di backup non vengono rimossi e finché le cartelle pubbliche di cui è stata eseguita la migrazione non vengono eliminate.

Sul server Exchange 2013, eseguire il comando riportato di seguito. In questo comando:

  - **BackupDir** è la directory in cui vengono archiviati i file di cui viene eseguito il backup per le voci autorizzazione, le proprietà delle MEPF e i file di log della migrazione. Assicurarsi di usare lo stesso percorso specificato in *Passaggio 6: blocco delle cartelle pubbliche (tempo di inattività delle cartelle pubbliche necessario)*.

  - **ArePublicFoldersOnPremises** è un parametro per indicare se le cartelle pubbliche si trovano in locale o in Exchange Online.

  - **Credential** è il nome e la password dell'utente di Exchange Online.

<!-- end list -->

    .\UnlockAndRestorePublicFolderProperties.ps1 -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

Tenere presente che gli elementi aggiunti al gruppo di Office 365, o qualsiasi operazione di modifica eseguita nei gruppi, non vengono copiati nelle cartelle pubbliche. Pertanto, presupponendo che siano stati aggiunti nuovi dati mentre la cartella pubblica era in un gruppo, alcuni di questi dati verranno persi.

Si noti, inoltre, che non è possibile ripristinare un subset di cartelle pubbliche, il che significa che devono essere ripristinate tutte le cartelle pubbliche migrate.

I gruppi corrispondenti in Office 365 non verranno eliminati durante il processo di rollback. È necessario eliminare manualmente tali gruppi.


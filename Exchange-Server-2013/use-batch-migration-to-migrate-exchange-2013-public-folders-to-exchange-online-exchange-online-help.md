---
title: 'Utilizzare la migrazione batch per migrare le cartelle pubbliche di Exchange 2013 a Exchange Online: Exchange 2013 Help'
TOCTitle: Utilizzare la migrazione batch per migrare le cartelle pubbliche di Exchange 2013 a Exchange Online
ms:assetid: 25a5234c-dd2c-487b-8541-3655fbeb030a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt798260(v=EXCHG.150)
ms:contentKeyID: 74432713
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzare la migrazione batch per migrare le cartelle pubbliche di Exchange 2013 a Exchange Online

 

_**Ultima modifica dell'argomento:**2018-03-26_

**Sintesi:** in questo articolo viene illustrato come spostare cartelle pubbliche da Exchange 2013 a Office 365.

La migrazione delle cartelle pubbliche di Exchange 2013 a Exchange Online richiede Exchange Server 2013 CU15 o versioni successive in esecuzione nell'ambiente locale.


> [!NOTE]
> Se si dispone di cartelle pubbliche di Exchange 2013 e Exchange 2016 nell'organizzazione e si desidera spostarle tutte in Exchange Online, utilizzare <A href="https://go.microsoft.com/fwlink/p/?linkid=845314">la versione Exchange 2016 di questo articolo</A> per pianificare ed eseguire la migrazione. Per i server di Exchange 2013 continua a essere necessario installare CU15 o versione successiva.



## Che cosa è necessario sapere prima di iniziare

  - Quando si esegue l'aggiornamento a Exchange Server 2013 CU15 o versione successiva, è inoltre necessario predisporre Active Directory o la migrazione delle cartelle pubbliche avrà esito negativo. La preparazione di Active Directory garantisce che tutti i parametri e i cmdlet di PowerShell rilevanti siano disponibili per predisporre ed eseguire la migrazione. Per ulteriori informazioni, vedere [Preparazione di Active Directory e dei domini](prepare-active-directory-and-domains-exchange-2013-help.md).

  - In Exchange Online, è necessario essere un membro del gruppo di ruoli Gestione organizzazione. Questo gruppo di ruoli differisce dalle autorizzazioni assegnate in fase di sottoscrizione a Office 365 o Exchange Online. Per informazioni dettagliate sull'abilitazione del gruppo di ruoli Gestione organizzazione, vedere [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - In Exchange Server 2013, è necessario essere un membro del gruppo di ruoli RBAC Gestione organizzazione o Gestione server. Per i dettagli, vedere [Aggiunta di membri a un gruppo di ruoli](https://go.microsoft.com/fwlink/?linkid=299212).

  - Prima di iniziare la migrazione delle cartelle pubbliche, se le dimensioni di una cartella pubblica dell'organizzazione superano i 25 GB, è consigliabile eliminare i contenuti da tale cartella per ridimensionarla oppure dividere i contenuti di tale cartella pubblica tra più cartelle di dimensioni inferiori. Il limite di 25 GB menzionato si applica solo alla cartella pubblica e non alle sue eventuali sottocartelle. Se nessuna delle due opzioni è eseguibile, si consiglia di non spostare le cartelle pubbliche su Exchange Online. Per ulteriori informazioni, vedere [Limiti di Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=391188).
    

    > [!NOTE]
    > Se le quote delle cartelle pubbliche correnti in Exchange Online sono inferiori a 25 GB, è possibile utilizzare il <A href="https://go.microsoft.com/fwlink/p/?linkid=844062">cmdlet Set-OrganizationConfig</A> per aumentarle con i parametri DefaultPublicFolderIssueWarningQuota e DefaultPublicFolderProhibitPostQuota.



  - In Office 365 ed Exchange Online, è possibile creare un massimo di 1.000 cassette postali delle cartelle pubbliche.

  - Se si prevede di migrare gli utenti a Office 365, è necessario completare la migrazione degli utenti prima della migrazione delle cartelle pubbliche. Per ulteriori informazioni, vedere [Modalità di migrazione di più account di posta elettronica a Office 365](https://go.microsoft.com/fwlink/p/?linkid=842798).

  - Il proxy MRS deve essere abilitato su almeno un server di Exchange, un server che ospita anche cassette postali delle cartelle pubbliche. Per i dettagli, vedere [Abilitare l'endpoint del Proxy MRS per gli spostamenti remoti](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md).

  - Per eseguire le procedure di migrazione illustrate in questo articolo, non è possibile utilizzare l'interfaccia di amministrazione di Exchange (EAC). È invece necessario utilizzare Exchange Management Shell sui server di Exchange 2013. In Exchange Online, è necessario utilizzare Exchange Online PowerShell. Per ulteriori informazioni, vedere [Connessione a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=842801).

  - La migrazione di elementi eliminati e cartelle eliminate da Exchange 2013 a Exchange Online è supportata. Prima di iniziare la migrazione, si consiglia di controllare tutte le cartelle e gli elementi eliminati e procedere all'eliminazione definitiva di ciò che non sarà necessario in Exchange Online. Tenere presente che gli elementi eliminati in modo permanente non potranno essere più recuperati.
    
    È possibile utilizzare i seguenti comandi per elencare le cartelle pubbliche eliminate presenti nel dumpster di Exchange (nell'ambiente locale di Exchange):
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null"} | ft name,foldersize
    
    Per eliminare una cartella specifica in modo permanente, utilizzare il seguente comando (in questo esempio viene usata una cartella denominata "Calendar2"):
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null" -and $_.Name -eq "Calendar2"} | Remove-PublicFolder

  - Prima di iniziare, leggere tutto l'articolo. Per alcuni passaggi sono previsti dei tempi di inattività. Durante tali periodi di inattività, le cartelle pubbliche non saranno accessibili per nessuno.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Passaggio 1: Download degli script di migrazione

1.  Scaricare tutti gli script e i file di supporto da [Script di migrazione delle cartelle pubbliche di Exchange 2013/2016](https://go.microsoft.com/fwlink/p/?linkid=844893).

2.  Salvare gli script nel computer locale da cui si eseguirà PowerShell. Ad esempio, C:\\PFScripts. Verificare che tutti gli script vengano salvati nello stesso percorso.

Gli script e i file che si stanno scaricando sono:

  - `Sync-ModernMailPublicFolders.ps1` Questo script sincronizza gli oggetti delle cartelle pubbliche abilitate alla posta elettronica dell'ambiente locale di Exchange con Office 365. Eseguire questo script in un server di Exchange 2013.

  - `SyncModernMailPublicFolders.strings.psd1` Questo file di supporto è utilizzato dallo script Sync-ModernMailPublicFolders.ps1 e deve essere scaricato nello stesso percorso.

  - `Export-ModernPublicFolderStatistics.ps1` Questo script crea il file di mapping Nome cartella-Dimensione cartella e Dimensione elementi eliminati. Eseguire questo script nel server di Exchange 2013.

  - `Export-ModernPublicFolderStatistics.strings.psd1` Questo file di supporto è utilizzato dallo script Export-ModernPublicFolderStatistics.ps1 e deve essere scaricato nello stesso percorso.

  - `ModernPublicFolderToMailboxMapGenerator.ps1` Questo script crea il file di mapping Cartella pubblica-Cassetta postale utilizzando l'output dello script Export-ModernPublicFolderStatistics.ps1. Eseguire lo script su un server Exchange 2013.

  - `ModernPublicFolderToMailboxMapGenerator.strings.psd1` Questo file di supporto è utilizzato dallo script ModernPublicFolderToMailboxMapGenerator.ps1 e deve essere scaricato nello stesso percorso.

  - `SetMailPublicFolderExternalAddress.ps1` Questo script esegue l'aggiornamento dell'`ExternalEmailAddress` delle cartelle pubbliche abilitate alla posta elettronica nell'ambiente locale in quello delle rispettive controparti di Exchange Online. In questo modo, dopo la migrazione i messaggi di posta elettronica indirizzati alle cartelle pubbliche abilitate alla posta elettronica vengono instradati correttamente a Exchange Online. È necessario eseguire questo script in un server di Exchange 2013.

  - `SetMailPublicFolderExternalAddress.strings.psd1` Questo file di supporto è utilizzato dallo script SetMailPublicFolderExternalAddress.ps1 e deve essere scaricato nello stesso percorso.

## Passaggio 2: Preparazione della migrazione

Prima di iniziare la migrazione delle cartelle pubbliche, eseguire tutti i passaggi preliminari descritti nelle sezioni seguenti.

**Passaggi preliminari generali**

Affinché la migrazione abbia esito positivo, è necessario:

  - Verificare che in Active Directory non siano presenti oggetti di posta elettronica delle cartelle pubbliche orfani, ovvero oggetti in Active Directory senza un oggetto corrispondente in Exchange.

  - Confermare che gli indirizzi di posta elettronica SMTP configurati per le cartelle pubbliche in Active Directory corrispondano agli indirizzi di posta elettronica SMTP negli oggetti di Exchange.

  - Verificare che in Active Directory non siano presenti oggetti delle cartelle pubbliche duplicati. Ciò è necessario per evitare una situazione in cui due o più oggetti di Active Directory puntino alla stessa cartella pubblica abilitata alla posta elettronica.

**Passaggi preliminari nell'ambiente del server di Exchange 2013 locale**

In Exchange Management Shell (locale) eseguire le operazioni seguenti:

1.  Dopo aver completato la migrazione, sarà necessario un po' di tempo affinché le cache DNS in Internet indirizzino messaggi alle cartelle pubbliche abilitate alla posta elettronica nella loro nuova posizione in Exchange Online. È possibile verificare che le cartelle pubbliche abilitate alla posta elettronica appena migrate ricevano messaggi in questa fase di transizione DNS creando un dominio accettato con un nome conosciuto. A tale scopo, eseguire il comando riportato di seguito nell'ambiente locale di Exchange. In questo esempio, `target domain` è il dominio di Office 365 o Exchange Online per il quale è già stato configurato un connettore di invio mediante la procedura guidata per la configurazione ibrida.
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName <target domain> -DomainType InternalRelay
    
    **Esempio**:
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName "contoso.mail.onmicrosoft.com" -DomainType InternalRelay
    
    Se il dominio accettato già esiste nell'ambiente locale, rinominarlo in `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99` e lasciare gli altri attributi inalterati.
    
    Per verificare se il dominio accettato è già presente nel proprio ambiente locale:
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" }
    
    Per rinominare il dominio accettato in `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99`, eseguire le operazioni seguenti:
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" } | Set-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99
    

    > [!NOTE]
    > Se si prevede che le cartelle pubbliche abilitate alla posta elettronica in Exchange Online ricevano e-mail esterne da Internet, è necessario disabilitare blocco Edge basato su directory in Exchange Online e Exchange Online Protection (EOP). Per ulteriori informazioni, vedere <A href="https://technet.microsoft.com/it-it/library/dn600322(v=exchg.150)">Utilizzare il blocco Edge basato su directory per rifiutare i messaggi inviati a destinatari non validi</A>.



2.  Se il nome di una cartella pubblica contiene una barra rovesciata **\\** o una barra **/**, potrebbe non essere migrata alla relativa cassetta postale designata durante il processo di migrazione. Prima di eseguire la migrazione, rinominare tali cartelle per rimuovere questi caratteri
    
    1.  Per individuare le cartelle pubbliche il cui nome contiene una barra rovesciata, eseguire il comando seguente:
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Where {$_.Name -like "*\*" -or $_.Name -like "*/*"} | Format-List Name, Identity, EntryId
    
    2.  Se vengono restituite cartelle, è possibile rinominarle con il comando seguente:
        
            Set-PublicFolder -Identity "<public folder EntryId>" -Name "<new public folder name>"

3.  Eseguire le operazioni seguenti per accertarsi che non vi sia un record di una migrazione effettuata in precedenza. Se così fosse, è necessario impostare quel valore su `$false`.
    
    Prima di modificare i valori, assicurarsi che il tentativo di migrazione precedente possa essere rimosso affinché non venga eseguita accidentalmente una seconda migrazione.
    
    1.  Eseguire il comando seguente per verificare la presenza di eventuali migrazioni precedenti e lo stato di tali migrazioni:
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete, PublicFolderMailboxesLockedForNewConnections, PublicFolderMailboxesMigrationComplete
        

        > [!NOTE]
        > Se i parametri <CODE>PublicFoldersLockedforMigration</CODE> o <CODE>PublicFolderMigrationComplete</CODE> sono <CODE>$true</CODE>, significa che è stata eseguita la migrazione di cartelle pubbliche legacy in un determinato momento. Verificare che i database delle cartelle pubbliche legacy non dispongano dell'autorizzazione prima di continuare con il passaggio 3b.

    
    2.  Se per uno degli elementi sopra indicati viene restituito un valore impostato su `$true`, renderlo `$false` eseguendo:
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false

4.  Per verificare l'esito positivo della migrazione, è consigliabile eseguire i comandi seguenti in tutti i server di Exchange 2013 appropriati. Verranno visualizzati degli snapshot della distribuzione corrente delle cartelle pubbliche che in seguito saranno utilizzati per fare un confronto con le cartelle pubbliche appena migrate.
    

    > [!NOTE]
    > A seconda della dimensione dell'organizzazione di Exchange, l'esecuzione di questi comandi potrebbe richiedere del tempo.

    
      - Utilizzare il seguente comando per scattare un'istantanea della struttura delle cartelle di origine.
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML OnPrem_PFStructure.xml
    
      - Utilizzare il seguente comando per scattare un'istantanea delle statistiche sulle cartelle pubbliche, quali proprietario, dimensioni e conteggio degli elementi.
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML OnPrem_PFStatistics.xml
    
      - Utilizzare il seguente comando per acquisire uno snapshot delle autorizzazioni delle cartelle pubbliche.
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML OnPrem_PFPerms.xml
    
      - Utilizzare il seguente comando per acquisire uno snapshot delle cartelle pubbliche abilitate alla posta elettronica:
        
            Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML OnPrem_MEPF.xml
    
      - Salvare i file generati dai comandi precedenti in una posizione sicura per fare un confronto al termine della migrazione.

5.  Se si utilizza Microsoft Azure Active Directory Connect (Connetti AD Azure) per sincronizzare le directory locale con Azure Active Directory, è necessario effettuare le seguenti operazioni (se non si utilizza Connetti AD Azure, è possibile ignorare questo passaggio):
    
    1.  In un computer locale, aprire Microsoft Azure Active Directory Connect e selezionare **Configura**.
    
    2.  Nella schermata **Attività aggiuntive** selezionare **Personalizza le opzioni di sincronizzazione**, quindi fare clic su **Avanti**.
    
    3.  Nella schermata **Connessione ad Azure AD** immettere le credenziali appropriate e quindi fare clic su **Avanti**. Una volta stabilita la connessione, continuare a fare clic su **Avanti** finché non viene visualizzata la schermata **Funzionalità facoltative**.
    
    4.  Verificare che **Cartelle pubbliche della posta di Exchange** non sia selezionata. Se non è selezionata, è possibile passare alla sezione successiva, *Passaggi preliminari in Exchange Online*. Se è selezionata, fare clic per deselezionare la casella di controllo e quindi fare clic su **OK**.
        

        > [!NOTE]
        > Se <STRONG>Cartelle pubbliche della posta di Exchange</STRONG> non viene visualizzata come opzione nella schermata <STRONG>Funzionalità facoltative</STRONG>, è possibile uscire da Microsoft Azure Active Directory Connect e passare alla sezione successiva, <EM>Passaggi preliminari in Exchange Online</EM>.

    
    5.  Dopo avere deselezionato **cartelle pubbliche della posta di Exchange**, continuare a fare clic su **Avanti** finché non viene visualizzata la schermata **Pronto per la configurazione**, quindi fare clic su **Configura**.

**Passaggi preliminari in Exchange Online**

In PowerShell di Exchange Online, eseguire le operazioni seguenti:

1.  Assicurarsi che non siano presenti richieste di migrazione delle cartelle pubbliche esistenti. Se ve ne sono, annullarle affinché la richiesta di migrazione non abbia esito negativo. Questo passaggio è obbligatorio solo se si pensa che possa esserci una richiesta di migrazione esistente nella pipeline (una che ha avuto esito negativo o che si desidera interrompere).
    
    Una richiesta di migrazione esistente può essere di due tipi: migrazione batch o migrazione seriale. I comandi per il rilevamento e per la rimozione di ciascun tipo di richiesta sono riportati di seguito.
    
    Nell'esempio seguente vengono rilevate le eventuali richieste di migrazione seriale esistenti:
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics 
    
    Nell'esempio seguente vengono rimosse tutte le richieste di migrazione seriale di cartelle pubbliche esistenti:
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    Nell'esempio seguente vengono rilevate le eventuali richieste di migrazione batch esistenti:
    
        Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    Nell'esempio seguente vengono rimosse tutte le richieste di migrazione batch di cartelle pubbliche esistenti:
    
        Remove-MigrationBatch <name of migration batch> -Confirm:$false

2.  È necessario che la funzionalità di migrazione **PAW** sia abilitata per il tenant di Office 365. È possibile verificarlo utilizzando il comando seguente in PowerShell di Exchange Online:
    
        Get-MigrationConfig
    
    Se in **Funzionalità** viene visualizzato **PAW**, la funzionalità è abilitata ed è possibile procedere con il passaggio successivo.
    
    Se la funzionalità PAW non è ancora abilitata per il tenant, potrebbe essere perché sono presenti dei batch di migrazione esistenti, o batch di cartelle pubbliche o batch di utenti. Tali batch potrebbero essere in uno stato qualsiasi, compreso Completato. In questo caso, completare e rimuovere i batch di migrazione finché non viene restituito nessun record quando si esegue `Get-MigrationBatch`. Dopo avere rimosso tutti i batch esistenti, la funzionalità PAW dovrebbe essere abilitata automaticamente. La modifica potrebbe non essere applicata immediatamente in `Get-MigrationConfig`, ma ciò è normale. In caso di migrazioni di utenti, è possibile continuare a creare nuovi batch dopo aver completato questo passaggio.

3.  Accertarsi che non siano presenti cartelle pubbliche o cassette postali di cartelle pubbliche esistenti in Exchange Online. Se sono presenti cartelle pubbliche in Exchange Online dopo aver eseguito le operazioni indicate di seguito, è importante stabilire perché ci sono e quale utente dell'organizzazione ha iniziato una gerarchia di cartelle pubbliche prima di iniziare a rimuovere cartelle pubbliche e cassette postali di cartelle pubbliche.
    
    1.  In Office 365 o Exchange Online PowerShell, utilizzare il seguente comando per controllare se esistono cassette postali di cartelle pubbliche.
        
            Get-Mailbox -PublicFolder
    
    2.  Se il comando non restituisce cassette postali di cartelle pubbliche, procedere con Passaggio 3: Generazione di file .csv. Se il comando restituisce cassette postali di cartelle pubbliche, utilizzare il seguente comando per controllare se esistono cartelle pubbliche:
        
            Get-PublicFolder -Recurse
    
    3.  Se in Office 365 o Exchange Online sono presenti cartelle pubbliche, utilizzare il seguente comando di PowerShell per rimuoverle (dopo aver verificato che non sono necessarie). Accertarsi di aver salvato le informazioni all'interno di queste cartelle pubbliche prima di eliminarle perché tutte le informazioni verranno eliminate in modo permanente quando si rimuovono le cartelle pubbliche.
        
            Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  Una volta rimosse le cartelle pubbliche, utilizzare i seguenti comandi per rimuovere tutte le cassette postali delle cartelle pubbliche:
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true 

## Passaggio 3: Generazione di file csv

Utilizzare gli script scaricati in precedenza per generare i file csv che verranno usati nella migrazione.

1.  Da Exchange Management Shell (locale), eseguire lo script `Export-ModernPublicFolderStatistics.ps1` per creare il file di mapping Nome cartella-Dimensione cartella. È necessario disporre delle autorizzazioni di amministratore locale per eseguire questo script. Il file risultante conterrà tre colonne: **FolderName**, **FolderSize** e **DeletedItemSize**. I valori delle colonne **FolderSize** e **DeletedItemSize** saranno visualizzati in byte. Ad esempio, **\\PublicFolder01,10240, 100** significa che la cartella pubblica nella radice della gerarchia denominata PublicFolder01 è di 10.240 byte o 10.240 MB, come dimensione, e che contiene 100 byte di elementi recuperabili.
    
        .\Export-ModernPublicFolderStatistics.ps1 <Folder-to-size map path>
    
    **Esempio**:
    
        .\Export-ModernPublicFolderStatistics.ps1 stats.csv

2.  Utilizzare lo script `ModernPublicFolderToMailboxMapGenerator.ps1` per creare un file csv che esegue il mapping delle cartelle pubbliche di origine alle cassette postali delle cartelle pubbliche nella destinazione di Exchange Online. Questo file viene utilizzato per calcolare il numero corretto di cassette postali di cartelle pubbliche in Exchange Online.
    

    > [!NOTE]
    > Il file generato da <CODE>ModernPublicFolderToMailboxMapGenerator.ps1</CODE> non conterrà il nome di ogni cartella pubblica dell'organizzazione. Contiene riferimenti alle cartelle padre di più grandi strutture di cartelle o i nomi delle cartelle il cui sono molto grandi. È possibile paragonare questo file come un file di "eccezione" utilizzato per assicurarsi che alcune strutture di cartelle e cartelle più grande ottenere inserite in posta specifica cartella pubblicafinestre. È normale per non visualizzare ciascuna delle cartelle pubbliche in questo file. Le sottocartelle di una cartella elencati in questo file di mapping verranno migrate anche alla stessa cassetta postale di cartelle pubbliche come cartella principale (a meno che non sia esplicitamente indicato in un'altra riga all'interno del file di mapping per invitarli a una cassetta postale diversa di cartelle pubbliche).

    
        .\ModernPublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes><Maximum mailbox recoverable item size in bytes><Folder-to-size map path><Folder-to-mailbox map path>
    
      - `Maximum mailbox size in bytes` è la quantità massima di dati da migrare in una singola cassetta postale delle cartelle pubbliche in Exchange Online. Le dimensioni massime di questo campo sono attualmente pari a 50 GB, ma si consiglia di utilizzare delle dimensioni inferiori (come il 50% di quelle massime) per consentire la crescita futura.
    
      - `Maximum mailbox recoverable items size in bytes` è la quota degli elementi recuperabili nelle cassette postali di Exchange Online. La dimensione massima delle cassette postali delle cartelle pubbliche in Exchange Online è pari a 50 GB. È consigliabile impostare ` RecoverableItemsQuota` su un massimo di 15 GB.
    
      - `Folder-to-size map path` è il percorso del file csv creato quando è stato eseguito lo script `Export-ModernPublicFolderStatistics.ps1`.
    
      - `Folder-to-mailbox map path` è il nome e il percorso del file csv Cartella-Cassetta postale che verrà creato in questo passaggio. Se si specifica solo il nome del file, il file sarà creato nella directory PowerShell corrente sul computer locale.

**Esempio**:

    .\ModernPublicFolderToMailboxMapGenerator.ps1 -MailboxSize 25GB -MailboxRecoverableItemSize 1GB -ImportFile .\stats.csv -ExportFile map.csv


> [!NOTE]
> Non Supportiamo di migrazione delle cartelle pubbliche di Exchange Online se il numero di cartelle pubbliche univoche le cassette postali di Exchange Online è maggiore di 100.



## Passaggio 4: Creazione delle cassette postali di cartelle pubbliche in Exchange Online

In seguito, in PowerShell di Exchange Online creare le cassette postali delle cartelle pubbliche di destinazione che conterranno le cartelle pubbliche migrate.

1.  Eseguire il seguente script per creare le nuove cassette postali delle cartelle pubbliche di destinazione. Lo script crea una cassetta postale di destinazione per ogni cassetta postale nel file CSV generata nel *Passaggio 3: Generazione di file csv* con lo script `ModernPublicFoldertoMailboxMapGenerator.ps1`.
    
        $mappings = Import-Csv <Folder-to-mailbox map path>
        $primaryMailboxName = ($mappings | Where-Object FolderPath -eq "\" ).TargetMailbox
        New-Mailbox -HoldForMigration:$true -PublicFolder -IsExcludedFromServingHierarchy:$false $primaryMailboxName 
        ($mappings | Where-Object TargetMailbox -ne $primaryMailboxName).TargetMailbox | Sort-Object -unique | ForEach-Object { New-Mailbox -PublicFolder -IsExcludedFromServingHierarchy:$false $_ }
    
      - `Folder-to-mailbox map path` è il percorso del file csv Cartella-Cassetta postale generato dallo script `ModernPublicFoldertoMailboxMapGenerator.ps1` nel *Passaggio 3: Generazione di file csv*.

## Passaggio 5: Avvio della richiesta di migrazione

A questo punto è necessario eseguire una serie di comandi nell'ambiente locale di Exchange 2013 e in Exchange Online.

1.  Da uno dei server di Exchange 2013 che ospita le cassette postali delle cartelle pubbliche, eseguire lo script seguente. Tale script consente di sincronizzare le cartelle pubbliche abilitate alla posta dalla versione locale di Active Directory a Exchange Online. Assicurarsi di avere scaricato la versione più recente di questo script e di eseguirlo da Exchange Management Shell.
    
        .\Sync-ModernMailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
      - `Credential` è il nome utente e la password dell'amministratore di Exchange Online.
    
      - `CsvSummaryFile` è il percorso del file in cui si desidera inserire il file di log degli errori e delle operazioni di sincronizzazione. Il log sarà in formato csv.

2.  Nel server di Exchange 2013 individuare il server dell'endpoint del proxy MRS e annotarlo. Questa informazione servirà per eseguire la richiesta di migrazione. Salvare questa informazione per il passaggio 3b riportato di seguito.

3.  In PowerShell di Exchange Online, utilizzare i seguenti comandi per trasmettere le informazioni sulle credenziali e su MRS ricevute nel passaggio precedente alle variabili del cmdlet che saranno poi utilizzate nella richiesta di migrazione.
    
    1.  Passare le credenziali di un utente con autorizzazioni amministrative sull'ambiente locale di Exchange 2013 nella variabile `$Source_Credential`. Nella richiesta di migrazione eseguita in Exchange Online queste credenziali saranno utilizzate per ottenere l'accesso ai server di Exchange 2013 locali per copiare il contenuto delle cartelle pubbliche in Exchange Online.
        
            $Source_Credential = Get-Credential <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  Annotare le informazioni sul server proxy MRS dall'ambiente di Exchange 2013 ottenute con il passaggio 2 e passarle nella variabile:
        
            $Source_RemoteServer = "<paste the value here>"

4.  In PowerShell di Exchange Online, eseguire i seguenti comandi per creare l'endpoint di migrazione delle cartelle pubbliche e la richiesta di migrazione delle cartelle pubbliche:
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential
         
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    

    > [!NOTE]
    > Separare più indirizzi di posta elettronica con virgole.

    
    `folder_mapping.csv` è il file di mapping generato durante il *passaggio 3: creazione di file csv*. Assicurarsi di fornire il percorso completo del file. Se il file di mapping è stato spostato per un motivo qualsiasi, accertarsi di usare la nuova posizione.

5.  Infine, in PowerShell di Exchange Online avviare la richiesta di migrazione utilizzando il seguente comando.
    
        Start-MigrationBatch PublicFolderMigration

Le migrazioni batch devono essere create utilizzando il cmdlet New-MigrationBatch in PowerShell di Exchange Online, mentre è possibile visualizzare e gestire l'avanzamento e il completamento della migrazione nell'interfaccia di amministrazione di Exchange o eseguendo il cmdlet Get-MigrationBatch. Il cmdlet New-MigrationBatch inizializza una richiesta di migrazione delle cassette postali per ogni cassetta postale delle cartelle pubbliche ed è possibile visualizzare lo stato di tali richieste dalla pagina di migrazione delle cassette postali.

Per passare alla pagina della migrazione della cassetta postale:

1.  Accedere a Exchange Online e aprire l'Interfaccia di amministrazione di Exchange.

2.  Andare a **Destinatari**, quindi selezionare **Migrazione**.

3.  Selezionare la richiesta di migrazione appena creata, quindi nel riquadro **Dettagli** fare clic su **Visualizza dettagli**.

Prima di passare al *Passaggio 6: Bloccare le cartelle pubbliche nel server di Exchange 2013*, verificare che tutti i dati siano stati copiati e che non vi siano errori nella migrazione. Dopo avere verificato che il batch è passato allo stato di **Sincronizzato**, eseguire i comandi indicati nel *Passaggio 2: Predisporre la migrazione*, nel passaggio finale in **Passaggi preliminari nell'ambiente del server di Exchange 2013 locale**, per acquisire uno snapshot delle cartelle pubbliche locali. Dopo avere eseguito questi comandi, è possibile procedere al passaggio successivo. Questi comandi potrebbero richiedere un po' di tempo a seconda del numero di cartelle di cui si dispone.

## Passaggio 6: Bloccare le cartelle pubbliche nell'ambiente di Exchange 2013 per la migrazione finale (tempo di inattività delle cartelle pubbliche obbligatorio)

Fino a questo punto della migrazione, gli utenti sono stati in grado di accedere alle cartelle pubbliche locali. Nei passaggi seguenti, gli utenti verranno disconnessi dalle cartelle pubbliche di Exchange 2013 e durante la sincronizzazione finale della migrazione le cartelle verranno bloccate. Gli utenti non potranno accedere alle cartelle pubbliche durante questo processo e tutti i messaggi inviati alle cartelle pubbliche abilitate alla posta elettronica saranno accodati e non saranno recapitati fino al completamento della migrazione.

Prima di eseguire il comando `PublicFolderMailboxesLockedForNewConnections`, come descritto in basso, verificare che tutti i processi abbiano lo stato **Sincronizzato**. È possibile eseguire questa operazione tramite il comando `Get-PublicFolderMailboxMigrationRequest`. Continuare con questo passaggio solo dopo aver verificato che tutti i processi abbiano lo stato **Sincronizzato**.

Nell'ambiente locale eseguire il comando di seguito riportato per bloccare le cartelle pubbliche di Exchange 2013 per la finalizzazione.

    Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections $true


> [!NOTE]
> Se non è possibile accedere al parametro <CODE>-PublicFolderMailboxesLockedForNewConnections</CODE>, potrebbe essere perché Active Directory non è stato predisposto durante l'aggiornamento dell'aggiornamento cumulativo, come indicato in precedenza in <EM>Che cosa è necessario sapere prima di iniziare?</EM> Per ulteriori informazioni, vedere <A href="prepare-active-directory-and-domains-exchange-2013-help.md">Preparazione di Active Directory e dei domini</A>.<BR>Inoltre, è necessario migrare prima gli utenti che devono accedere alle cartelle pubbliche, <STRONG>prima</STRONG> di migrare le cartelle pubbliche stesse.



Se l'organizzazione dispone di cassette postali delle cartelle pubbliche in più server di Exchange 2013, è necessario attendere fino al completamento della replica di AD. Una volta completato, è possibile verificare che tutte le cassette postali delle cartelle pubbliche abbiano prelevato il contrassegno `PublicFolderMailboxesLockedForNewConnections` e che eventuali modifiche in sospeso apportate di recente dagli utenti alle cartelle pubbliche siano state uniformate nell'organizzazione. Questa operazione può richiedere diverse ore.

## Passaggio 7: Finalizzazione della migrazione di cartelle pubbliche (tempo di inattività delle cartelle pubbliche obbligatorio)

Prima di poter completare la migrazione delle cartelle pubbliche, è necessario verificare che siano non sposta alcuna altra cassetta postale di cartelle pubbliche o cartelle pubbliche passerà corso nell'ambiente di Exchange locale. A tale scopo, utilizzare i cmdlet di `Get-MoveRequest` e `Get-PublicFolderMoveRequest` per visualizzare l'elenco delle cartelle pubbliche già esistenti si sposta. Se sono presenti gli eventuali spostamenti in corso o nello stato **completato**, è necessario rimuoverli.

Successivamente, per completare la migrazione delle cartelle pubbliche, eseguire il comando seguente in PowerShell in linea di Exchange:

    Complete-MigrationBatch PublicFolderMigration

Quando si esegue questo comando, Exchange esegue una sincronizzazione finale tra l'organizzazione di Exchange locale e in linea di Exchange. Durante questo periodo, lo stato del batch di migrazione cambierà da **sincronizzati** al **completamento** e infine su **completato**. Se ha esito positivo, la sincronizzazione finale le cartelle pubbliche in Exchange Online saranno sbloccate.

In genere, la modifica relativa allo stato del batch di migrazione da **Sincronizzato** a **Completato** richiede alcune ore. Solo a questo punto inizia la sincronizzazione finale.

## Passaggio 8: Testare e sbloccare le cartelle pubbliche in Exchange Online

Una volta completata la migrazione delle cartelle pubbliche, eseguire le operazioni seguenti per testare l'esito positivo della migrazione e verificarne ufficialmente il completamento. Queste attività finali consentono di testare la gerarchia delle cartelle pubbliche migrate prima di spostare l'organizzazione in modo permanente alle cartelle pubbliche di Exchange Online.

1.  In PowerShell di Exchange Online, assegnare ad alcune cassette postali utente di prova l'uso di una cassetta postale di cartelle pubbliche appena migrata come cassetta postale di cartelle pubbliche predefinita.
    
        Set-Mailbox -Identity <test user> -DefaultPublicFolderMailbox <public folder mailbox identity>
    
    Assicurarsi che gli utenti di prova dispongano delle autorizzazioni necessarie per creare cartelle pubbliche.

2.  Accedere a Outlook con l'utente di test è indicato nel passaggio precedente e quindi eseguire i seguenti test di cartelle pubbliche. Si noti che potrebbero essere necessari da 15 a 30 minuti rendere effettive le modifiche. Quando Outlook è in grado di riconoscere le modifiche, è possibile che venga richiesto di riavviare un paio di volte.
    
    1.  Visualizzare la gerarchia.
    
    2.  Controllare le autorizzazioni.
    
    3.  Creare alcune cartelle pubbliche ed eliminarle.
    
    4.  Pubblicare il contenuto ed eliminare il contenuto in una cartella pubblica.
    
    Se si verificano problemi e determinare che non si è pronti per passare a cartelle pubbliche dell'organizzazione interamente a Exchange Online, vedere [Eseguire il rollback di una migrazione di cartella pubblica da Exchange 2013 a Exchange 2016](roll-back-a-public-folder-migration-from-exchange-2013-to-exchange-online-exchange-2013-help.md).

3.  Eseguire il comando seguente Exchange Online PowerShell per sbloccare le cartelle pubbliche in Exchange Online. Dopo aver eseguito il comando, potrebbe richiedere circa 15-30 minuti rendere effettive le modifiche. Dopo che Outlook venga a conoscenza delle modifiche, esso venga richiesto agli utenti di riavviare il programma più volte.
    
        Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## Passaggio 9: Completare il migrazione sul posto

Per attivare i messaggi di posta elettronica in cartelle pubbliche abilitate alla posta locale, procedere come segue:

1.  Nell'ambiente locale, eseguire il seguente script per verificare che tutte le e-mail per le cartelle pubbliche abilitate alla posta elettronica siano indirizzate correttamente a Exchange Online. Lo script contrassegna le cartelle pubbliche abilitate alla posta elettronica con un `ExternalEmailAddress` che punta alle rispettive controparti in Exchange Online:
    
        .\SetMailPublicFolderExternalAddress.ps1 -ExecutionSummaryFile:mepf_summary.csv

2.  Se il test ha esito positivo, nell'ambiente locale utilizzare il seguente comando per indicare che è stata completata la migrazione delle cartelle pubbliche:
    
        Set-OrganizationConfig -PublicFolderMailboxesMigrationComplete:$true -PublicFoldersEnabled Remote

## Come verificare se l'operazione ha avuto esito positivo

Nel Passaggio 2: Preparazione della migrazione sono stati acquisiti degli snapshot delle autorizzazioni, delle statistiche e della struttura delle cartelle pubbliche. La seguente procedura consentirà di verificare la corretta migrazione delle cartelle pubbliche tramite l'acquisizione degli stessi snapshot in Exchange Online una volta completata la migrazione. Confrontare i dati in entrambi i file per verificare la riuscita dell'operazione.

1.  In PowerShell di Exchange Online, utilizzare il seguente comando per scattare un'istantanea della nuova struttura di cartelle:
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML Cloud_PFStructure.xml

2.  In PowerShell di Exchange Online, utilizzare il seguente comando per scattare un'istantanea delle statistiche sulle cartelle pubbliche, quali proprietario, dimensioni e conteggio degli elementi:
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderStatistics | Export-CliXML Cloud_PFStatistics.xml

3.  In PowerShell di Exchange Online, utilizzare il seguente comando per scattare un'istantanea delle autorizzazioni:
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User, AccessRights | Export-CliXML Cloud_PFPerms.xml

4.  In PowerShell di Exchange Online, utilizzare il seguente comando per acquisire uno snapshot delle cartelle pubbliche abilitate alla posta elettronica:
    
        Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML Cloud_MEPF.xml

## Problemi noti

Di seguito sono comuni problemi di migrazione di cartelle pubbliche che possono verificarsi all'interno dell'organizzazione.

  - Non Supportiamo di migrazione delle cartelle pubbliche di Exchange Online se il numero di cartelle pubbliche univoche le cassette postali di Exchange Online è maggiore di 100.

  - Le autorizzazioni per la cartella pubblica radice e la cartella EFORMS REGISTRY non vengono migrate a Exchange Online ed è necessario applicarle manualmente in Exchange Online. A tale scopo, eseguire il comando riportato di seguito in PowerShell di Exchange Online. Eseguire il comando una sola volta per ogni voce di autorizzazione presente in locale, ma non in Exchange Online:
    
        Add-PublicFolderClientPermission "\" -User <user> -AccessRights <access rights>
        Add-PublicFolderClientPermission "\NON_IPM_SUBTREE\EFORMS REGISTRY" -User <user> -AccessRights <access rights>

  - Le migrazioni di alcune cartelle pubbliche non riuscirà se alcune cassette postali di cartelle pubbliche non sono in uso la gerarchia di cartelle pubbliche. Ciò significa che il parametro `IsExcludedFromServingHierarchy` su uno o più cassette postali è impostato su `$true`. Per evitare questo problema, impostare tutte le cassette postali in Exchange Online per gestire la gerarchia.

  - Le autorizzazioni **Invia come** e **Invia per conto di** non vengono migrate a Exchange Online. Se ciò accade con la migrazione, utilizzare i comandi seguenti nell'ambiente locale per vedere chi dispone di queste autorizzazioni.
    
    Per visualizzare le cartelle pubbliche che dispongono delle autorizzazioni locali Invia come:
    
        Get-MailPublicFolder | Get-ADPermission | ?{$_.ExtendedRights -like "*Send-As*"}
    
    Per visualizzare le cartelle pubbliche che dispongono delle autorizzazioni locali Invia per conto di:
    
        Get-MailPublicFolder | ?{$_.GrantSendOnBehalfTo -ne "$null"} | ft name,GrantSendOnBehalfTo
    
    Per aggiungere l'autorizzazione Invia come a una cartella pubblica abilitata alla posta elettronica in Exchange Online, in PowerShell di Exchange Online digitare:
    
        Add-RecipientPermission -Identity <mail-enabled public folder primary SMTP address> -Trustee <name of user to be assigned permission> -AccessRights SendAs
    
    **Esempio**:
    
        Add-RecipientPermission -Identity send1 -Trustee Exo1 -AccessRights SendAs
    
    Per aggiungere l'autorizzazione Invia per conto di a una cartella pubblica abilitata alla posta elettronica in Exchange Online, in PowerShell di Exchange Online digitare:
    
        Set-MailPublicFolder -Identity <name of public folder> -GrantSendOnBehalfTo <user or comma-separated list of users>
    
    **Esempio**:
    
        Set-MailPublicFolder send2 -GrantSendOnBehalfTo exo1,exo2

  - Disporre di più di 10.000 cartelle nella cartella "\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT" può causare l'esito negativo della migrazione. Di conseguenza, controllare la cartella "\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT" per verificare se sono presenti più di 10.000 cartelle direttamente in essa (figli diretti). Per trovare il numero di cartelle pubbliche in questa posizione è possibile utilizzare il comando seguente:
    
        (Get-PublicFolder -GetChildren "\NON_IPM_SUBTREE\DUMPSTER_ROOT").Count 
    
    Exchange Online non supporta più di 10.000 sottocartelle, per cui le migrazioni di più di 10.000 cartelle hanno esito negativo. Stiamo sviluppando uno script per sbloccare tali configurazioni. Nel frattempo, è consigliabile attendere prima di eseguire la migrazione delle cartelle pubbliche.

  - I processi di migrazione non avanzano o sono bloccati. Questo problema può verificarsi se sono presenti troppi processi in esecuzione in parallelo, causando l'esito negativo dei processi con errori intermittenti. È possibile ridurre il numero di processi simultanei modificando `MaxConcurrentMigrations` e `MaxConcurrentIncrementalSyncs` in un numero inferiore. Usare l'esempio seguente per impostare questi valori:
    
        Set-MigrationEndpoint <PublicFolderEndpoint> -MaxConcurrentMigrations 30 -MaxConcurrentIncrementalSyncs 20  -SkipVerification 

  - I processi di migrazione hanno esito negativo con l'errore "Errore: dumpster della cartella Dumpster." Se viene visualizzato questo errore, dovrebbe essere risolto se si interrompe il batch e lo si riavvia.

  - Processi di migrazione non riuscire e generare una "richiesta è stato messo in quarantena a causa del seguente errore: la chiave specificata non è presente nel dizionario" messaggio di errore. Ciò si verifica quando un elemento danneggiato è presente in una cartella che non possono copiare processi di migrazione. Per risolvere questo problema:
    
    1.  Interrompere il batch di migrazione.
    
    2.  Identificare la cartella contenente l'elemento danneggiato. Il report della migrazione deve includere i riferimenti alla cartella di cui era in corso la copia quando si è verificato l'errore.
    
    3.  Nell'ambiente locale, spostare la cartella interessata nella cassetta postale delle cartelle pubbliche principale. È possibile utilizzare il cmdlet `New-PublicFolderMoveRequest` per lo spostamento di cartelle.
    
    4.  Attendere che lo spostamento della cartella per il completamento. Al termine, rimuovere la richiesta di spostamento. Quindi, riavviare il batch di migrazione.

## Rimuovere le cassette postali delle cartelle pubbliche dall'ambiente locale di Exchange

Al termine della migrazione e dopo aver verificato che le cartelle pubbliche in Exchange Online funzionano come previsto e contengono tutti i dati previsti, è possibile rimuovere le cassette postali delle cartelle pubbliche in locale.

Si tenga presente che questo passaggio è irreversibile, perché una volta eliminate le cassette postali di cartelle pubbliche, può essere annullate. Pertanto, è consigliabile che, oltre a verificare la riuscita della migrazione, è inoltre monitorare le cartelle pubbliche di Exchange Online per alcune settimane prima di rimuovere le cassette postali cartelle pubbliche locale.


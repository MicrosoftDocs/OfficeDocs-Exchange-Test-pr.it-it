---
title: 'Utilizzare la migrazione batch delle cartelle pubbliche legacy a Office 365 ed Exchange Online: Exchange 2013 Help'
TOCTitle: Utilizzare la migrazione batch delle cartelle pubbliche legacy a Office 365 ed Exchange Online
ms:assetid: e8ab9309-7d12-4f02-bfc4-14e61a373958
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn874017(v=EXCHG.150)
ms:contentKeyID: 63763714
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzare la migrazione batch delle cartelle pubbliche legacy a Office 365 ed Exchange Online

 

_**Si applica a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2018-03-26_

**Riepilogo:**  utilizzare queste procedure per spostare le cartelle pubbliche di Exchange 2007 ed Exchange 2010 in Office 365.

In questo argomento viene illustrato come effettuare la migrazione completa o la migrazione a fasi delle cartelle pubbliche dall'aggiornamento cumulativo 8 per Exchange Server 2010 Service Pack 3 (SP3) o dall'aggiornamento cumulativo 15 per Exchange 2007 SP3 a Office 365 o Exchange Online.

Nell'ambito di questo argomento i server Exchange 2010 SP3 RU8 ed Exchange 2007 SP3 RU15 vengono definiti *server Exchange legacy*. Inoltre, le procedure in questo argomento si applicano sia a Exchange Online che Office 365. I termini potrebbero essere utilizzati in maniera intercambiabile in questo argomento.


> [!NOTE]
> Il metodo della migrazione batch descritto in questo articolo è l'unico metodo supportato per la migrazione delle cartelle pubbliche legacy a Office 365 ed Exchange Online. Il vecchio metodo della migrazione seriale per le cartelle pubbliche è stato deprecato e non è più supportato da Microsoft.



Non utilizzare la funzionalità di esportazione PST di Outlook per migrare le cartelle pubbliche a Office 365 o Exchange Online. La crescita della cassetta postale di cartelle pubbliche di Office 365 e Exchange Online è gestita attraverso una funzionalità di divisione automatica che divide la cassetta postale di cartelle pubbliche quando supera le quote della dimensione prevista. La funzione di divisione automatica non è in grado di gestire la crescita improvvisa delle cassette postali di cartelle pubbliche quando si usa l'esportazione PST per la migrazione verso le cartelle pubbliche e potrebbe essere necessario attendere fino a due settimane finché la divisione automatica non sposti i dati dalla cassetta postale principale. Si consiglia di utilizzare le istruzioni basate sul cmdlet in questo documento per migrare le cartelle pubbliche a Office 365 e Exchange Online. Tuttavia, se si scegliere di migrare le cartelle pubbliche utilizzando l'esportazione PST, vedere la sezione Eseguire la migrazione di cartelle pubbliche a Office 365 tramite esportazione PST di Outlook più avanti in questo argomento.

Verrà eseguita la migrazione utilizzando i cmdlet **\*-MigrationBatch**, insieme ai seguenti script PowerShell:

  - `Export-PublicFolderStatistics.ps1`   Questo script crea il file di mapping Nome cartella-Dimensione cartella. Eseguire lo script sul server Exchange legacy.

  - `Export-PublicFolderStatistics.psd1`   Questo file di supporto è utilizzato dallo script `Export-PublicFolderStatistics.ps1` e deve essere scaricato nello stesso percorso.

  - `PublicFolderToMailboxMapGenerator.ps1`   Questo script crea il file di mapping Cartella-Cassetta postale utilizzando l'output dello script `Export-PublicFolderStatistics.ps1`. Eseguire lo script sul server Exchange legacy.

  - `PublicFolderToMailboxMapGenerator.strings.psd1`   Questo file di supporto è utilizzato dallo script `PublicFolderToMailboxMapGenerator.ps1` e deve essere scaricato nello stesso percorso.

  - `Create-PublicFolderMailboxesForMigration.ps1` Questo script crea le cassette postali delle cartelle pubbliche di destinazione per la migrazione. Inoltre, questo script calcola il numero di cassette postali necessarie per gestire il carico utente stimato, in base alle linee guida relative al numero di accessi utente per ogni cassetta postale delle cartelle pubbliche consigliato in [Limiti per le cartelle pubbliche](limits-for-public-folders-exchange-2013-help.md).

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` Questo file di supporto è utilizzato dallo script Create-PublicFolderMailboxesForMigration.ps1 e deve essere scaricato nello stesso percorso.

  - `Sync-MailPublicFolders.ps1`   Questo script sincronizza gli oggetti delle cartelle pubbliche abilitate alla posta elettronica della distribuzione locale di Exchange con Office 365. Eseguire lo script sul server Exchange legacy.

  - `SyncMailPublicFolders.strings.psd1`   File di supporto utilizzato dallo script `Sync-MailPublicFolders.ps1` che deve essere copiato nello stesso percorso degli script precedenti.

Passaggio 1: Download degli script di migrazione fornisce informazioni dettagliate sul percorso in cui scaricare questi script. Verificare che tutti gli script vengano scaricati nello stesso percorso.

Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

## Versioni di Exchange supportate per la migrazione delle cartelle pubbliche ad Office 365 ed Exchange Online

Exchange supporta lo spostamento delle cartelle pubbliche a Office 365 ed Exchange Online dalle seguenti versioni legacy di Exchange Server:

  - Exchange 2010 SP3 RU8 o versione successiva

  - Exchange 2007 SP3 RU15 o versione successiva

Se è necessario spostare le cartelle pubbliche in Exchange Online ma i server locali non eseguono le versioni supportate minime di Exchange 2010 o Exchange 2007, si consiglia vivamente di aggiornare i server locali e di utilizzare la migrazione batch, che è l'unico metodo di migrazione delle cartelle pubbliche supportato.

Non è possibile eseguire la migrazione delle cartelle pubbliche direttamente da Exchange 2003. Se nell'organizzazione si esegue Exchange 2003, è necessario spostare tutti i database e le repliche delle cartelle pubbliche in Exchange 2010 SP3 RU8 o versione successiva oppure in Exchange 2007 SP3 RU10 o versione successiva. Nessuna replica di cartelle pubbliche può essere lasciata su Exchange 2003. Inoltre, la posta elettronica indirizzata a una cartella pubblica di Exchange 2013 non può essere instradata tramite un server Exchange 2003.

## Che cosa è necessario sapere prima di iniziare

  - Il server Exchange 2010 deve eseguire Exchange 2010 SP3 RU8 o versione successiva.

  - Il server Exchange 2007 deve eseguire Exchange 2007 SP3 RU15 o versione successiva.

  - In Office 365 ed Exchange Online, è necessario essere un membro del gruppo di ruoli Gestione organizzazione. Questo gruppo di ruoli differisce dalle autorizzazioni assegnate in fase di sottoscrizione a Office 365 o Exchange Online. Per informazioni dettagliate sull'abilitazione del gruppo di ruoli Gestione organizzazione, vedere [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - In Exchange 2010, è necessario essere un membro del gruppo di ruoli RBAC Gestione organizzazione o Gestione server. Per i dettagli, vedere [Aggiunta di membri a un gruppo di ruoli](https://go.microsoft.com/fwlink/?linkid=299212).

  - In Exchange 2007, è necessario essere assegnati al ruolo di amministratore dell'organizzazione Exchange o di amministratore server di Exchange. Inoltre, è necessario essere assegnati al ruolo Amministratore cartelle pubbliche e al gruppo Amministratori locale per il server di destinazione. Per i dettagli, vedere [Aggiunta di un utente o di un gruppo a un ruolo di amministratore](https://go.microsoft.com/fwlink/p/?linkid=81779).

  - Sul server Exchange 2007, eseguire l'aggiornamento a [Windows PowerShell 2.0 e WinRM 2.0 per Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Prima della migrazione, se nell'organizzazione sono presenti cartelle pubbliche più grandi di 2 GB, si consiglia di eliminarne il contenuto o di dividerlo in più cartelle. Se nessuna delle due soluzioni è eseguibile, si consiglia di non spostare le cartelle pubbliche su Office 365 ed Exchange Online.

  - In Office 365 ed Exchange Online, è possibile creare un massimo di 1.000 cassette postali delle cartelle pubbliche.

  - Prima di eseguire la migrazione delle cartelle pubbliche, si consiglia di spostare tutte le cassette postali utente su Office 365 ed Exchange Online. Per informazioni dettagliate, vedere [Modalità di migrazione di più account di posta elettronica a Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).

  - Outlook via Internet deve essere abilitato sul server Exchange legacy. Per informazioni dettagliate sull'abilitazione di Outlook via Internet sui server Exchange 2010, vedere [Abilita Outlook via Internet](https://go.microsoft.com/fwlink/p/?linkid=187249). Per informazioni dettagliate sull'abilitazione di Outlook via Internet sui server Exchange 2007, vedere [Come abilitare Outlook via Internet](https://go.microsoft.com/fwlink/p/?linkid=167210).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange (EAC) o Exchange Management Console (EMC) per eseguire questa procedura. Nei server Exchange legacy, è necessario utilizzare Exchange Management Shell. Per Exchange Online, è necessario utilizzare Exchange Online PowerShell. Per ulteriori informazioni, vedere [Connessione a Exchange Online tramite Remote PowerShell](https://technet.microsoft.com/it-it/library/jj984289\(v=exchg.150\)).

  - Prima di iniziare, è consigliabile leggere attentamente il presente argomento in quanto alcuni passaggi richiedono un tempo di inattività.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione?

## Passaggio 1: Download degli script di migrazione

1.  Scaricare tutti gli script e i file di supporto da [Script di migrazione delle cartelle pubbliche](https://go.microsoft.com/fwlink/?linkid=299838).

2.  Salvare gli script nel computer locale da cui si eseguirà PowerShell. Ad esempio, C:\\PFScripts. Verificare che tutti gli script vengano salvati nello stesso percorso.

3.  Scaricare i seguenti file da [Cartelle pubbliche abilitate alla posta elettronica - script di sincronizzazione delle directory](https://go.microsoft.com/fwlink/p/?linkid=532376):
    
    1.  `Sync-MailPublicFolders.ps1`
    
    2.  `SyncMailPublicFolders.strings.psd1`

4.  Salvare gli script nello stesso percorso utilizzato nel passaggio 2, ad esempio C:\\PFScripts.

## Passaggio 2: Preparazione della migrazione

Eseguire i passaggi prerequisiti di seguito riportati prima di iniziare la migrazione.

**Passaggi preliminari generali**

  - Verificare che in Active Directory non siano presenti oggetti di posta elettronica delle cartelle pubbliche orfani, ovvero oggetti in Active Directory senza un oggetto corrispondente in Exchange.

  - Confermare che l'indirizzo di posta elettronica SMTP configurato per le cartelle pubbliche in Active Directory corrisponda agli indirizzi di posta elettronica SMTP negli oggetti di Exchange.

  - Assicurarsi che in Active Directory non siano presenti oggetti delle cartelle pubbliche duplicati per evitare una situazione in cui due o più oggetti di Active Directory puntino alla stessa cartella pubblica abilitata alla posta elettronica.

**Passaggi prerequisiti sul server Exchange legacy**

1.  Sul server Exchange legacy, accertarsi che il routing alle cartelle pubbliche abilitate alla posta che esisteranno in Office 365 o Exchange Online continui a funzionare finché tutte le cache DNS su Internet vengano aggiornate in modo da puntare al DNS di Exchange Online in cui al momento risiede l'organizzazione. A tale scopo, utilizzare il seguente comando per configurare un dominio accettato con un nome noto che eseguirà correttamente il routing dei messaggi di posta elettronica al dominio di Office 365 o Exchange Online.
    
        New-AcceptedDomain -Name "PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99" -DomainName contoso.onmicrosoft.com -DomainType InternalRelay 

2.  Se il nome di una cartella pubblica contiene una barra rovesciata **\\**, in fase di migrazione le cartelle pubbliche saranno create nella cartella pubblica padre. Prima della migrazione, si consiglia di rinominare tutte le cartelle pubbliche il cui nome contiene la barra rovesciata.
    
    1.  In Exchange 2010, per individuare le cartelle pubbliche il cui nome contiene una barra rovesciata, utilizzare il comando seguente:
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  In Exchange 2007, per individuare le cartelle pubbliche il cui nome contiene una barra rovesciata, utilizzare il comando seguente:
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  Se vengono restituite cartelle, è possibile rinominarle con il comando seguente:
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  Accertarsi che non vi sia un precedente record di una migrazione riuscita. Se così fosse, sarà necessario impostare quel valore su `$false`. Se il valore è impostato su `$true`, la richiesta di migrazione avrà esito negativo.
    
    1.  Nell'esempio seguente, viene controllato lo stato di migrazione delle cartelle pubbliche.
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
    
    2.  Se lo stato della proprietà *PublicFoldersLockedforMigration* o *PublicFolderMigrationComplete* è impostato su `$true`, utilizzare il seguente comando per impostare il valore su `$false`.
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    

    > [!WARNING]
    > Dopo la reimpostazione di queste proprietà, è necessario attendere che le nuove impostazioni vengano rilevate in Exchange. Potrebbero essere necessarie fino a due ore.



4.  Una volta completata la migrazione, a scopo di verifica si consiglia di eseguire prima i seguenti comandi Exchange Management Shell sul server Exchange legacy per scattare istantanee dell'attuale distribuzione delle cartelle pubbliche.
    
    1.  Utilizzare il seguente comando per scattare un'istantanea della struttura delle cartelle di origine.
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
    2.  Utilizzare il seguente comando per scattare un'istantanea delle statistiche sulle cartelle pubbliche, quali proprietario, dimensioni e conteggio degli elementi.
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
    3.  Utilizzare il seguente comando per scattare un'istantanea delle autorizzazioni.
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    Salvare le informazioni ottenute con i precedenti comandi per confrontarle al termine della migrazione.

5.  Se si utilizza Microsoft Azure Active Directory Connect (Azure AD Connect) per sincronizzare le directory locali con Azure Active Directory, è necessario eseguire le operazioni seguenti (se non è in uso Azure AD Connect, è possibile ignorare questo passaggio):
    
    1.  In un computer locale, aprire Microsoft Azure Active Directory Connect e selezionare **Configura**.
    
    2.  Nella schermata **Attività aggiuntive** selezionare **Personalizza le opzioni di sincronizzazione**, quindi fare clic su **Avanti**.
    
    3.  Nella schermata **Connessione ad Azure AD** immettere le credenziali appropriate e quindi fare clic su **Avanti**. Una volta stabilita la connessione, continuare a fare clic su **Avanti** finché non viene visualizzata la schermata **Funzionalità facoltative**.
    
    4.  Verificare che **Le cartelle pubbliche di posta elettronica di Exchange** non sia selezionata. Se non è selezionata, è possibile passare alla sezione successiva, *che operazioni preliminari in Office 365 o Exchange Online*. Se è selezionata, fare clic per deselezionare la casella di controllo e quindi fare clic su **Avanti**.
        

        > [!NOTE]
        > Se <STRONG>Le cartelle pubbliche di posta elettronica di Exchange</STRONG> non viene visualizzata come un'opzione nella schermata <STRONG>Funzionalità facoltative</STRONG>, è possibile chiudere Azure Active Directory connettersi e passare alla sezione successiva, <EM>che operazioni preliminari in Office 365 o Exchange Online</EM>.

    
    5.  Dopo avere deselezionato **cartelle pubbliche della posta di Exchange**, continuare a fare clic su **Avanti** finché non viene visualizzata la schermata **Pronto per la configurazione**, quindi fare clic su **Configura**.

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [New-AcceptedDomain](https://technet.microsoft.com/it-it/library/aa995975\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/it-it/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/it-it/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/it-it/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/it-it/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/it-it/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Operazioni preliminari in Office 365 o Exchange Online**

1.  Assicurarsi che non siano presenti richieste di migrazione delle cartelle pubbliche esistenti. Se ve ne sono, annullarle affinché la richiesta di migrazione non abbia esito negativo. Questo passaggio non è necessario per tutti i casi; è obbligatorio solo se si pensa che possa esserci una richiesta di migrazione esistente nella pipeline.
    
    Una richiesta di migrazione esistente può essere di due tipi: migrazione batch o migrazione seriale. I comandi per il rilevamento e per la rimozione delle richieste di ciascun tipo sono riportati di seguito.
    

    > [!IMPORTANT]
    > Prima di rimuovere una richiesta di migrazione, è importante comprendere il motivo per cui ne esisteva una. Eseguire il seguente comando per stabilire quando è stata effettuata una richiesta precedente e per diagnosticare eventuali problemi che possono essersi verificati. Potrebbe essere necessario comunicare con altri amministratori dell'organizzazione per determinare il motivo della modifica.

    
    Nell'esempio seguente vengono rilevate le eventuali richieste di migrazione seriale esistenti.
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    
    Nell'esempio seguente vengono rimosse tutte le richieste di migrazione seriale di cartelle pubbliche esistenti.
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    Nell'esempio seguente vengono rilevate le eventuali richieste di migrazione batch esistenti.
    
        $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    Nell'esempio seguente vengono rimosse tutte le richieste di migrazione batch di cartelle pubbliche esistenti.
    
        $batch | Remove-MigrationBatch -Confirm:$false

2.  Accertarsi che non esistano cartelle pubbliche o cassette postali di cartelle pubbliche in Office 365.
    

    > [!IMPORTANT]
    > Se vengono visualizzati le cartelle pubbliche in Office 365 o Exchange Online, è importante determinare il motivo per cui sono disponibili e all'interno dell'organizzazione avviato una gerarchia di cartelle pubbliche prima di rimuovere le cartelle pubbliche e cassette postali delle cartelle pubbliche.

    
    1.  In Office 365 o Exchange Online PowerShell, utilizzare il seguente comando per controllare se esistono cassette postali di cartelle pubbliche.
        
            Get-Mailbox -PublicFolder 
    
    2.  Se il comando non restituisce cassette postali di cartelle pubbliche, procedere con Passaggio 3: Generazione di file .csv. Se il comando ha restituito cassette postali di cartelle pubbliche, utilizzare il seguente comando per controllare se esistono cartelle pubbliche:
        
            Get-PublicFolder
    
    3.  Se in Office 365 o Exchange Online sono presenti cartelle pubbliche, utilizzare il seguente comando di PowerShell per rimuoverle. Accertarsi di aver salvato tutte le informazioni contenute nelle cartelle pubbliche in Office 365. Quando vengono rimosse le cartelle pubbliche, tutte le informazioni in esse contenute verranno eliminate definitivamente.
        
            Get-MailPublicFolder | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            
            
            Get-PublicFolder -GetChildren \ | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  Una volta rimosse le cartelle pubbliche, utilizzare i seguenti comandi per rimuovere tutte le cassette postali delle cartelle pubbliche.
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false

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

1.  Sul server Exchange legacy, eseguire lo script `Export-PublicFolderStatistics.ps1` per creare il file di mapping Nome cartella-Dimensione cartella. Questo script deve essere eseguito sempre da un amministratore locale. Il file conterrà due colonne: **Nomecartella** e **Dimensionicartella**. I valori della colonna **Dimensionicartella** saranno visualizzati in byte. Ad esempio, **\\PublicFolder01,10000**.
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* corrisponde al nome di dominio completo del server Cassette postali che ospita la gerarchia delle cartelle pubbliche.
    
      - *Folder to size map path* corrisponde al nome file e al percorso su una cartella condivisa in rete in cui si desidera salvare il file csv. Più avanti in questo argomento sarà necessario utilizzare Exchange Online PowerShell per accedere a questo file. Se si specifica solo il nome del file, il file sarà creato nella directory PowerShell corrente sul computer locale.
    
      - Se necessario, rimuovere le cartelle di sistema abilitate alla posta elettronica dall'output dello script prima di procedere.

2.  Eseguire lo script `PublicFolderToMailboxMapGenerator.ps1` per creare il file di mapping Cartella pubblica-Cassetta postale. Questo file viene utilizzato per calcolare il numero corretto di cassette postali di cartelle pubbliche in Exchange Online.
    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    

    > [!IMPORTANT]
    > Il file di mapping a-cassetta postale di cartelle pubbliche non deve superare 1000 righe. Se il file superiore a 1000 righe, la struttura di cartelle pubbliche deve essere semplificato. Procedere con un file di maggiore di 1000 righe non è consigliabile e può causare problemi di migrazione.

    
      - Prima di eseguire lo script, utilizzare il cmdlet seguente per verificare i limiti delle cartelle pubbliche corrente nel tenant di Exchange Online. Quindi, annotare i valori di quota corrente per le cartelle pubbliche. `Get-OrganizationConfig | fl *quota*`
        
        In Exchange Online, il valore predefinito è 2 GB per **DefaultPublicFolderProhibitPostQuota**e 1,7 GB per **DefaultPublicFolderIssueWarningQuota** .
    
      - *Maximum mailbox size in bytes* corrisponde alle dimensioni massime che si desidera impostare per le nuove cassette postali di cartelle pubbliche. In Exchange Online, la dimensione massima delle cassette postali di cartelle pubbliche è pari a 100 GB. È consigliabile utilizzare un'impostazione di 15 GB in modo che ciascuna cassetta postale di cartelle pubbliche abbia lo spazio per crescere. Exchange Online è il limite predefinito di cartelle pubbliche "Impedisci l'inserimento" di 2 GB. Se si dispone di singole cartelle pubbliche di dimensioni superiori a 2 GB, è possibile utilizzare una delle opzioni seguenti per risolvere questo problema:
        
          - Prima di avviare il batch di migrazione, aumentare la quota "Impedisci l'inserimento" cartelle pubbliche predefinita eseguendo il cmdlet seguente:
            
            `Set-OrganizationConfig -DefaultPublicFolderProhibitPostQuota <size value> -DefaultPublicFolderIssueWarningQuota <size value>`
        
          - Prima di avviare il batch di migrazione, eliminare cartelle pubbliche per ridurre le dimensioni del contenuto a 2 GB o meno.
        
          - Prima di avviare il batch di migrazione, dividere la cartella pubblica in più cartelle pubbliche di ogni 2 GB o meno.
        

        > [!NOTE]
        > Se la cartella pubblica è superiore a 30 GB e pertanto non è possibile eliminare il contenuto o suddiviso in più cartelle pubbliche, è consigliabile non vengono spostate le cartelle pubbliche a Exchange Online.

    
      - *Folder to size map path* corrisponde al percorso di file del file csv creato durante l'esecuzione dello script `Export-PublicFolderStatistics.ps1` .
    
      - *Folder to mailbox map path* è uguale a nome e percorso del file con estensione csv a-cassetta postale di cartelle creati in questo passaggio. Se si specifica solo il nome del file, viene generato il file nella directory corrente PowerShell nel computer locale.


> [!NOTE]
> Dopo che vengono eseguiti gli script e vengono generati file CSV, le nuove cartelle pubbliche o gli aggiornamenti alle cartelle pubbliche esistenti non verranno raccolti.



## Passaggio 4: Creazione delle cassette postali di cartelle pubbliche in Exchange Online

1.  Eseguire il seguente comando per creare le nuove cassette postali delle cartelle pubbliche di destinazione. Lo script crea una cassetta postale di destinazione per ogni cassetta postale nel file CSV generata nel passaggio 3, eseguendo lo script PublicFoldertoMailboxMapGenerator.ps1.
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* è il file generato dallo script PublicFoldertoMailboxMapGenerator.ps1 nel passaggio 3. In genere, il numero stimato di connessioni utente simultanee per l'esplorazione di una gerarchia di cartelle pubbliche è inferiore al numero totale di utenti in un'organizzazione.

## Passaggio 5: avvio della richiesta di migrazione

1.  Nel server Exchange legacy, eseguire il seguente comando per sincronizzare le cartelle pubbliche abilitate alla posta dalla versione locale di Active Directory a Exchange Online.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    `Credential` indica password e nome utente di Office 365. `CsvSummaryFile` indica il percorso del file in cui si desidera registrare gli errori e le operazioni di sincronizzazione, in formato .csv.
    

    > [!NOTE]
    > Prima di eseguire lo script, si consiglia di simulare le operazioni che verrebbero effettuate dallo script eseguendo quest'ultimo con un parametro <CODE>-WhatIf</CODE>.



2.  Nel server Exchange legacy, richiamare le seguenti informazioni necessarie per eseguire la richiesta di migrazione:
    
    1.  Individuare l'account dell'utente `LegacyExchangeDN` membro del ruolo Amministratore cartelle pubbliche. L'utente sarà quello di cui occorre fornire le credenziali nel passaggio 3 di questa procedura.
        
            Get-Mailbox <PublicFolder_Administrator_Account> | Select-Object LegacyExchangeDN
    
    2.  Individuare il `LegacyExchangeDN` di un server Cassette postali contenente un database delle cartelle pubbliche.
        
            Get-ExchangeServer <public folder server> | Select-Object -Expand ExchangeLegacyDN
    
    3.  Individuare il nome di dominio completo del nome host di Outlook Anywhere. Se si dispone di più istanze di Outlook Anywhere, si consiglia di selezionare quella più vicina all'endpoint di migrazione o alle repliche delle cartelle pubbliche nell'organizzazione Exchange legacy. Utilizzare il seguente comando per trovare tutte le istanze di Outlook Anywhere:
        
            Get-OutlookAnywhere | Format-Table Identity,ExternalHostName

3.  In Office 365 PowerShell, utilizzare i seguenti comandi per trasmettere le informazioni ricevute nel passaggio precedente alle variabili che saranno poi utilizzate nella richiesta di migrazione.
    
    1.  Passare le credenziali di un utente con autorizzazioni amministrative sul server Exchange legacy nella variabile `$Source_Credential`. Nella richiesta di migrazione eseguita in Exchange Online queste credenziali saranno utilizzate per ottenere l'accesso ai server Exchange legacy per copiare il contenuto.
        
            $Source_Credential = Get-Credential <source_domain\PublicFolder_Administrator_Account>
    
    2.  Utilizzare il `ExchangeLegacyDN` dell'utente di migrazione sul server Exchange legacy trovato nel passaggio 2a e passarlo alla variabile `$Source_RemoteMailboxLegacyDN`.
        
            $Source_RemoteMailboxLegacyDN = "<paste the value here>"
    
    3.  Utilizzare `ExchangeLegacyDN` del server di cartelle pubbliche individuato nel passaggio 2b precedente e passarlo alla variabile `$Source_RemotePublicFolderServerLegacyDN`.
        
            $Source_RemotePublicFolderServerLegacyDN = "<paste the value here>"
    
    4.  Utilizzare il nome host esterno di Outlook Anywhere individuato nel passaggio 2c precedente e passarlo nella variabile `$Source_OutlookAnywhereExternalHostName`.
        
            $Source_OutlookAnywhereExternalHostName = "<paste the value here>"

4.  Infine, in Exchange Online PowerShell, utilizzare i seguenti comandi per creare la richiesta di migrazione.
    

    > [!NOTE]
    > Il metodo di autenticazione riportato nel seguente esempio di Exchange Management Shell deve corrispondere alle impostazioni di Outlook via Internet dell'utente. In caso contrario, il comando ha esito negativo.

    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RPCProxyServer $Source_OutlookAnywhereExternalHostName -Credentials $Source_Credential -SourceMailboxLegacyDN $Source_RemoteMailboxLegacyDN -PublicFolderDatabaseServerLegacyDN $Source_RemotePublicFolderServerLegacyDN -Authentication Basic
        
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    
    Dove il file \<*folder\_mapping.csv*\> è il file generato in Step 3: Generate the .csv files.

5.  Avviare la migrazione utilizzando il comando seguente:
    
        Start-MigrationBatch PublicFolderMigration

Le migrazioni batch devono essere create utilizzando il cmdlet **New-MigrationBatch** nel Exchange Management Shell, mantre è possibile visualizzare e gestire l'avanzamento e il completamento della migrazione nell'interfaccia di amministrazione di Exchange. Poiché il cmdlet **New-MigrationBatch** inizializza le richieste di migrazione delle cassette postali per ogni cassetta postale delle cartelle pubbliche, è possibile visualizzare lo stato di tali richieste dalla pagina di migrazione delle cassette postali. È possibile accedere a questa pagina e creare rapporti di migrazione che possono essere ricevuti tramite posta elettronica eseguendo le seguenti operazioni:

1.  Accedere a Exchange Online e aprire l'Interfaccia di amministrazione di Exchange.

2.  Andare a **Cassetta postale** \> **Migrazione**.

3.  Selezionare la richiesta di migrazione appena creata, quindi fare clic su **Visualizza dettagli** nel riquadro **Dettagli**.

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\))

  - [Get-ExchangeServer](https://technet.microsoft.com/it-it/library/bb123873\(v=exchg.150\))

  - [Get-OutlookAnywhere](https://technet.microsoft.com/it-it/library/bb124263\(v=exchg.150\))

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/it-it/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/it-it/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/it-it/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/it-it/library/jj218697\(v=exchg.150\))

## Passaggio 6: Blocco delle cartelle pubbliche sul server Exchange legacy per la migrazione finale (tempi di inattività richiesti)

Fino a questo punto della migrazione, gli utenti sono stati in grado di accedere alle cartelle pubbliche. Nei passaggi successivi, gli utenti verranno disconnessi dalle cartelle pubbliche legacy e durante la sincronizzazione finale della migrazione le cartelle verranno bloccate. Gli utenti non potranno accedere alle cartelle pubbliche durante questo processo. Inoltre, tutti i messaggi inviati alle cartelle pubbliche abilitate alla posta saranno accodati e non saranno recapitati fino al completamento della migrazione.

Prima di eseguire il comando `PublicFoldersLockedForMigration` come descritto di seguito, assicurarsi che tutti i processi sono nello stato **sincronizzati**. È possibile farlo eseguendo il comando `Get-PublicFolderMailboxMigrationRequest` . Continuare con questo passaggio solo dopo aver verificato che tutti i processi sono nello stato **sincronizzati**.

Sul server Exchange legacy, eseguire il comando di seguito riportato per bloccare le cartelle pubbliche legacy per la finalizzazione.

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\)).

Se l'organizzazione dispone di più database delle cartelle pubbliche, sarà necessario attendere il completamento della replica delle cartelle pubbliche per confermare che tutti i database delle cartelle pubbliche abbiano estratto il flag `PublicFoldersLockedForMigration` e che eventuali modifiche in sospeso apportate dagli utenti alle cartelle siano confluite nell'organizzazione. L'operazione potrebbe richiedere diverse ore.

## Passaggio 7: finalizzazione della migrazione di cartelle pubbliche (tempi di inattività richiesti)

Per completare la migrazione delle cartelle pubbliche, eseguire il comando seguente:

    Complete-MigrationBatch PublicFolderMigration

Al termine della migrazione, Exchange eseguirà una sincronizzazione finale tra i server Exchange legacy ed Exchange Online. Se la sincronizzazione finale ha esito positivo, le cartelle pubbliche in Exchange Online saranno sbloccate e lo stato del batch di migrazione viene modificato in **completato**. È usuale per il batch di migrazione richiedere alcune ore prima di modifiche apportate al relativo stato da **sincronizzati** al **completamento**, quindi verrà avviata la sincronizzazione finale.

Se è stata configurata una distribuzione ibrida tra i server Exchange locali e Office 365, è necessario eseguire il comando seguente in Exchange Online PowerShell al termine della migrazione:

    Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## Passaggio 8: Verifica e sblocco della migrazione delle cartelle pubbliche

Dopo aver finalizzato la migrazione delle cartelle pubbliche, è necessario effettuare il test seguente per accertarsi che la migrazione sia avvenuta correttamente. In tal modo è possibile verificare la gerarchia delle cartelle pubbliche migrate prima di passare all'uso delle cartelle pubbliche di Office 365 o Exchange Online.

1.  In Office 365 o Exchange Online PowerShell, assegnare ad alcune alcune cassette postali di prova l'uso di una qualunque cassetta postale di cassette pubbliche appena migrata come cassetta postale di cartelle pubbliche predefinita.
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  Accedere a Outlook 2007 o versione successiva con l'utente di prova identificato nel passaggio precedente, quindi effettuare i seguenti test delle cartelle pubbliche:
    
      - Visualizzare la gerarchia.
    
      - Controllare le autorizzazioni.
    
      - Creare ed eliminare cartelle pubbliche.
    
      - Pubblicare il contenuto ed eliminare il contenuto da una cartella pubblica.

3.  In caso di eventuali problemi, vedere eseguire il rollback della migrazione più avanti in questo argomento. Se il contenuto delle cartelle pubbliche e delle gerarchie è accettabile e funzioni come previsto, continuare con il passaggio successivo.

4.  Sul server Exchange legacy, eseguire il comando di seguito riportato per indicare che la migrazione delle cartelle pubbliche è stata completata.
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  Dopo aver verificato che è stata completata la migrazione, eseguire il seguente comando in Exchange Online PowerShell per assicurarsi che il parametro *PublicFoldersEnabled* in **Set-OrganizationConfig** sia impostato su `Local`:
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

[Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\))

[Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\))

[Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\))

## Come verificare se l'operazione ha avuto esito positivo

In Step 2: Prepare for the migration era stato suggerito di scattare istantanee delle autorizzazioni, delle statistiche e della struttura delle cartelle pubbliche prima di iniziare la migrazione. La seguente procedura consentirà di verificare la corretta migrazione delle cartelle pubbliche tramite lo scatto delle stesse istantanee una volta completata la migrazione. È, quindi, possibile confrontare i dati in entrambi i file per verificare la riuscita dell'operazione.

1.  In Exchange Online PowerShell, utilizzare il seguente comando per scattare un'istantanea della nuova struttura di cartelle.
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  In Exchange Online PowerShell, utilizzare il seguente comando per scattare un'istantanea delle statistiche sulle cartelle pubbliche, quali proprietario, dimensioni e conteggio degli elementi.
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  In Exchange Online PowerShell, utilizzare il seguente comando per scattare un'istantanea delle autorizzazioni.
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## Rimozione dei database delle cartelle pubbliche dai server Exchange legacy

Al termine della migrazione, dopo aver verificato che le cartelle pubbliche di Exchange Online funzionano nel modo previsto, rimuovere i database delle cartelle pubbliche sui server Exchange legacy.


> [!IMPORTANT]
> Dal momento che tutte le cassette postali sono state migrate su Office 365 prima della migrazione della cartella pubblica, è opportuno instradare il traffico attraverso Office 365 (flusso di posta decentralizzato) al posto del flusso di posta centralizzato attraverso l'ambiente locale. Se si conserva il flusso di posta centralizzato, potrebbero verificarsi problemi di recapito alle cartelle pubbliche, dal momento che i database della cassetta postale relativi alla cartella pubblica sono stati rimossi dall'organizzazione locale.



  - Per i dettagli sulla rimozione dei database delle cartelle pubbliche dai server Exchange 2007, vedere [Rimozione di database delle cartelle pubbliche](https://go.microsoft.com/fwlink/?linkid=123678).

  - Per i dettagli sulla rimozione dei database delle cartelle pubbliche dai server Exchange 2010, vedere [Rimozione di database delle cartelle pubbliche](https://go.microsoft.com/fwlink/?linkid=81409).

## Ripristino della migrazione

Se si riscontrano problemi con la migrazione e si ha la necessità di riattivare le proprie cartelle pubbliche di Exchange 2010, procedere come segue.


> [!WARNING]
> Se si annulla la migrazione e si torna ai server Exchange legacy, si perderanno eventuali messaggi di posta elettronica inviati alle cartelle pubbliche abilitate alla posta o eventuale contenuto pubblicato nelle cartelle pubbliche dopo la migrazione. Per salvare il contenuto, è necessario esportarlo in un file PST e importarlo quindi nelle cartelle pubbliche legacy una volta completato il ripristino.



1.  Sul server Exchange legacy, eseguire il comando di seguito riportato per sbloccare le cartelle pubbliche legacy. Questo processo potrebbe richiedere diverse ore.
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  In Exchange Online PowerShell, utilizzare i seguenti comandi per rimuovere tutte le cartelle pubbliche di Exchange Online.
    
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force

3.  Sul server Exchange legacy, eseguire il comando di seguito riportato per impostare il flag `PublicFolderMigrationComplete` su `$false`.
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

## Eseguire la migrazione di cartelle pubbliche a Office 365 tramite esportazione PST di Outlook

Non utilizzare la funzionalità di esportazione PST di Outlook per migrare le cartelle pubbliche a Office 365 o Exchange Online se la gerarchia delle cartelle pubbliche locali è superiore a 30 GB. La crescita della cassetta postale di cartelle pubbliche di Office 365 è gestita attraverso una funzionalità di divisione automatica che divide la cassetta postale di cartelle pubbliche quando supera le quote della dimensione prevista. La funzione di divisione automatica non è in grado di gestire la crescita improvvisa delle cassette postali di cartelle pubbliche quando si usa l'esportazione PST per la migrazione verso le cartelle pubbliche e potrebbe essere necessario attendere fino a due settimane finché la divisione automatica non sposti i dati dalla cassetta postale principale. Inoltre, considerare quanto segue prima di utilizzare PST di Outlook per esportare le cartelle pubbliche a Office 365 o Exchange Online:

  - le autorizzazioni della cartella pubblica andranno perse durante questo processo. Acquisire le autorizzazioni corrente prima della migrazione e aggiungerle manualmente al termine della migrazione.

  - Se si utilizzano autorizzazioni complesse o si devono migrare molte cartelle, si consiglia di utilizzare il metodo cmdlet per la migrazione.

  - Tutte le modifiche di elementi o cartelle apportate alle cartelle pubbliche di origine durante la migrazione con esportazione PST andranno perse. Pertanto, si consiglia di utilizzare il metodo con cmdlet se il processo di esportazione e importazione dureranno molto.

Se si desidera comunque eseguire la migrazione delle cartelle pubbliche utilizzando i file PST, seguire la procedura per garantire la riuscita della migrazione.

1.  Utilizzare le istruzioni nel Step 1: Download the migration scripts per scaricare gli script di migrazione. È necessario solo scaricare il file `PublicFolderToMailboxMapGenerator.ps1`.

2.  Seguire il passaggio 2 di Step 3: Generate the .csv files per creare il file di mapping Cartella pubblica-Cassetta postale. Questo file viene utilizzato per calcolare il numero corretto di cassette postali di cartelle pubbliche in Exchange Online.

3.  Creare le cassette postali di cartelle pubbliche necessarie in base al file di mapping. Per ulteriori informazioni, vedere [Creazione di una cassetta postale di cartelle pubbliche](create-a-public-folder-mailbox-exchange-2013-help.md).

4.  Utilizzare il cmdlet New-PublicFolder per creare la cartella pubblica di livello più alto in ognuna delle cassette postali delle cartelle pubbliche utilizzando il parametro *Mailbox*.

5.  Esportare e importare i file PST con Outlook.

6.  Impostare le autorizzazioni per le cartelle pubbliche utilizzando EAC. Per ulteriori informazioni, seguire [Step 3: Assign permissions to the public folder](set-up-public-folders-in-a-new-organization-exchange-2013-help.md) nell'argomento [Configurare cartelle pubbliche in una nuova organizzazione](set-up-public-folders-in-a-new-organization-exchange-2013-help.md).


> [!WARNING]
> Se è già stata avviata una migrazione PST e la casella postale principale è piena, sono possibili due opzioni per recuperare la migrazione PST: 
> <OL>
> <LI>
> <P>Attendere che la divisione automatica sposti i dati dalla cassetta postale principale. Questa operazione può richiedere fino a due settimane. Tuttavia, tutte le cartelle pubbliche in una cassetta postale di cartelle pubbliche totalmente piena non potranno ricevere nuovi contenuti fino al termine della divisione automatica.</P>
> <LI>
> <P><A href="create-a-public-folder-mailbox-exchange-2013-help.md">Creazione di una cassetta postale di cartelle pubbliche</A> quindi utilizzare il cmdlet <STRONG>New-PublicFolder</STRONG> con il parametro <EM>Mailbox</EM> per creare le cartelle pubbliche rimanenti in una cassetta postale di cartelle pubbliche secondaria. Questo esempio crea una nuova cartella pubblica denominata PF201 nella cassetta postale secondaria di cartelle pubbliche.</P><PRE><CODE>New-PublicFolder -Name PF201 -Mailbox SecondaryPFMbx</CODE></PRE></LI></OL>



## Nuovo utente di Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Piccola icona per LinkedIn Learning" alt="Piccola icona per LinkedIn Learning" /> <strong>Nuovo utente di Office 365?</strong><br />
Sono disponibili esercitazioni video gratuite per <a href="https://support.office.com/it-it/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> grazie a LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>


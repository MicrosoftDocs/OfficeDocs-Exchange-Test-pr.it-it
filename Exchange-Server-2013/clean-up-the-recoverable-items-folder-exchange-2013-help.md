---
title: 'Pulire la cartella elementi ripristinabili: Exchange 2013 Help'
TOCTitle: Pulire la cartella elementi ripristinabili
ms:assetid: 82c310f8-de2f-46f2-8e1a-edb6055d6e69
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff678798(v=EXCHG.150)
ms:contentKeyID: 50555618
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pulire la cartella elementi ripristinabili

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-09-30_

(Questo argomento è destinato agli amministratori di Exchange.)

La cartella elementi ripristinabili (nelle versioni precedenti di Exchange come *il dumpster*) è presente per proteggere da eliminazioni accidentali o intenzionali e facilitare le azioni di individuazione comunemente eseguite prima o durante controversie o indagini. Per ulteriori informazioni sulla cartella elementi ripristinabili, vedere [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md).

Come pulire la cartella elementi ripristinabili in postale una cassetta dipende se la cassetta postale si trova in conservazione In locale o conservazione per controversia legale o fosse abilitato ripristino di singoli elementi:

  - Se una cassetta postale non viene inserita nella conservazione In locale o conservazione per controversia legale o non dispone di individuazione di singoli elementi, è sufficiente eliminare elementi dalla cartella elementi ripristinabili. Dopo l'eliminazione, è possibile utilizzare il ripristino di un singolo elemento per ripristinare gli elementi.

  - Se la cassetta postale si trova in conservazione In locale o conservazione per controversia legale o dispone di un singolo elemento abilitato il ripristino, è importante mantenere i dati della cassetta postale fino alla rimozione o ripristino di singoli elementi è disabilitato. In questo caso, è necessario eseguire ulteriori passaggi da pulire la cartella elementi ripristinabili.

Per ulteriori informazioni sull'archiviazione sul posto e conservazione per controversia legale, vedere [Archiviazione sul posto e conservazione per controversia legale](in-place-hold-and-litigation-hold-exchange-2013-help.md). Per ulteriori informazioni sul ripristino di un singolo elemento, vedere "Ripristino di un elemento singolo" in [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md).

Per ulteriori informazioni sulla cartella elementi ripristinabili, vedere [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per eseguire questa procedura: 30 minuti. Ciò può variare a seconda delle dimensioni della cartella elementi ripristinabili

  - È necessario ricoprire i seguenti ruoli di gestione per utilizzare il cmdlet **Search-Mailbox** per cercare ed eliminare i messaggi nella cassetta postale dell'utente.
    
      - **Ricerca cassetta postale**   Questo ruolo consente la ricerca dei messaggi in più cassette postali nell'organizzazione. Agli amministratori non viene assegnato questo ruolo per impostazione predefinita. Per assegnare a se stessi questo ruolo per poter effettuare ricerche nelle cassette postali, aggiungersi come membro del gruppo di ruoli Gestione individuazione. Vedere [Assegnare le autorizzazioni di eDiscovery di Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).
    
      - **Cassetta postale importazione/esportazione**   Questo ruolo consente di eliminare i messaggi dalla cassetta postale dell'utente. Per impostazione predefinita, questo ruolo non è assegnato ad alcun gruppo di ruolo. Per eliminare i messaggi dalle cassette postali degli utenti, è possibile aggiungere il ruolo cassette postali importazione/esportazione per il gruppo di ruoli Gestione organizzazione. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" in [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md) .

  - Poiché in modo non corretto pulizia della cartella elementi recuperabili può provocare la perdita di dati, è importante che si ha familiarità con la cartella elementi ripristinabili e dell'impatto di rimuovere il relativo contenuto. Prima di eseguire questa procedura, è consigliabile esaminare le informazioni contenute in [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md).

  - Per eseguire queste procedure, è possibile utilizzare il centro di amministrazione di Exchange (EAC). È necessario utilizzare la Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Utilizzo della Shell per eliminare gli elementi dalla cartella elementi recuperabili per le cassette postali che non sono messa in attesa o non è stato abilitato il ripristino di un singolo elemento

In questo esempio consente di eliminare definitivamente gli elementi dalla cartella elementi recuperabili di Gurinder Singh inoltre copiati gli elementi nella cartella GurinderSingh RecoverableItems la cassetta postale di individuazione (una cassetta postale di individuazione creata da Exchange il programma di installazione).

    Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent


> [!NOTE]
> Per eliminare gli elementi dalla cassetta postale senza vengono copiati in un'altra cassetta postale, utilizzare il comando precedente senza parametri <EM>TargetMailbox</EM> e <EM>TargetFolder</EM> .



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Search-Mailbox](https://technet.microsoft.com/it-it/library/dd298173\(v=exchg.150\)).

## Utilizzo della Shell per pulire la cartella elementi recuperabili per le cassette postali che restano in attesa o individuazione di singoli elementi

Se una cassetta postale raggiunge la quota degli elementi recuperabili, è consigliabile aumentare la quota di e non eliminare gli elementi dalla cartella. È inoltre possibile monitorare gli eventi nel registro dell'applicazione relative alla quota di avviso degli elementi recuperabili e intraprendere le azioni necessarie (ad esempio, che genera la quota o dell'analisi la crescita della cartella elementi recuperabili per le cassette postali che raggiungono la quota di avviso).

Vincoli di spazio di archiviazione o problemi simili impediscano è la generazione di quota degli elementi recuperabili, se è necessario eliminare i messaggi dalla cartella elementi recuperabili di una cassetta postale su conservazione In locale o conservazione per controversia legale o con un singolo elemento abilitato il ripristino, è consigliabile copiare dati dalla cartella elementi ripristinabili dell'utente di un'altra cassetta postale. Se si eliminano elementi a causa di vincoli di spazio di archiviazione su un volume, è possibile copiare gli elementi a una cassetta postale collocata su un volume che dispone di spazio di archiviazione adeguato.

Questa procedura consente di copiare gli elementi dalla cartella elementi recuperabili di Gurinder Singh nella cartella GurinderSingh RecoverableItems la cassetta postale di individuazione. Prima di copiare ed eliminare elementi dalla cartella elementi ripristinabili, è necessario eseguire diverse operazioni per verificare che gli elementi non vengono eliminati dalla cartella elementi recuperabili. Dopo aver copiare gli elementi in una cassetta postale di backup o l'individuazione e pulire la cartella, è possibile ripristinare le impostazioni precedenti della cassetta postale.

1.  Per recuperare le impostazioni di quote seguenti. Assicurarsi di prendere nota dei valori in modo che è possibile ripristinare le impostazioni dopo la pulizia della cartella elementi ripristinabili:
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    

    > [!NOTE]
    > Se il parametro <EM>UseDatabaseQuotaDefaults</EM> è impostato su <CODE>$true</CODE>, non vengono applicate le impostazioni relative alle quote precedente. Vengono applicate le impostazioni di quote corrispondenti configurate nel database delle cassette postali, anche se vengono specificate le impostazioni di singole cassette postali.

    
        Get-Mailbox "Gurinder Singh" | Format-List RecoverableItemsQuota, RecoverableItemsWarningQuota, ProhibitSendQuota, ProhibitSendReceiveQuota, UseDatabaseQuotaDefaults, RetainDeletedItemsFor, UseDatabaseRetentionDefaults

2.  Recuperare le impostazioni di accesso della cassetta postale per la cassetta postale. Prendere nota di queste impostazioni per utilizzi successivi.
    
        Get-CASMailbox "Gurinder Singh" | Format-List EwsEnabled, ActiveSyncEnabled, MAPIEnabled, OWAEnabled, ImapEnabled, PopEnabled

3.  Recuperare la dimensione corrente della cartella elementi recuperabili. Si noti la dimensione in modo che è possibile elevare le quote nel passaggio 6.
    
        Get-MailboxFolderStatistics "Gurinder Singh" -FolderScope RecoverableItems | Format-List Name,FolderAndSubfolderSize

4.  Recuperare la configurazione corrente del ciclo di lavoro Assistente cartelle gestite. Assicurarsi di prendere nota dell'impostazione per utilizzi successivi.
    
        Get-MailboxServer "My Mailbox Server" | Format-List Name,ManagedFolderWorkCycle

5.  Disabilitare l'accesso client per la cassetta postale per assicurarsi che nessun modifiche ai dati delle cassette postali per la durata di questa procedura.
    
        Set-CASMailbox "Gurinder Singh" -EwsEnabled $false -ActiveSyncEnabled $false -MAPIEnabled $false -OWAEnabled $false -ImapEnabled $false -PopEnabled $false

6.  Per assicurarsi che nessun elemento viene eliminato dalla cartella elementi ripristinabili, aumentare la quota degli elementi recuperabili, aumentare la quota di avviso relativo agli elementi ripristinabili e impostare il periodo di mantenimento elementi eliminati su un valore superiore a quella corrente della cartella elementi ripristinabili dell'utente. Ciò è particolarmente importante per conservare i messaggi per le cassette postali inserite nella conservazione In locale o conservazione per controversia legale. Si consiglia la generazione di queste impostazioni a due volte alle dimensioni correnti.
    
        Set-Mailbox "Gurinder Singh" -RecoverableItemsQuota 50Gb -RecoverableItemsWarningQuota 50Gb -RetainDeletedItemsFor 3650 -ProhibitSendQuota 50Gb -ProhibitSendRecieveQuota 50Gb -UseDatabaseQuotaDefaults $false -UseDatabaseRetentionDefaults $false

7.  Disattivare l'Assistente cartelle gestite sul server cassette postali.
    
        Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle $null
    

    > [!IMPORTANT]
    > Se la cassetta postale si trova in un database delle cassette postali in un gruppo di disponibilità del database (DAG), è necessario disabilitare l'Assistente cartelle gestite in ciascun membro del DAG che ospita una copia del database. Se il database di failover in un altro server, ciò impedisce l'Assistente cartelle gestite nel server di eliminazione dei dati delle cassette postali.



8.  Disabilitare il ripristino di singoli elementi e rimuovere la cassetta postale di conservazione per controversia legale.
    
        Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $false -LitigationHoldEnabled $false
    

    > [!IMPORTANT]
    > Dopo aver eseguito questo comando, potrebbe richiedere fino a un'ora per disabilitare il ripristino di singoli elementi o conservazione per controversia legale. È consigliabile eseguire il passaggio successivo solo una volta trascorso questo periodo.



9.  Copiare gli elementi dalla cartella elementi ripristinabili in una cartella nella cassetta postale di ricerca di individuazione ed eliminare il contenuto dalla cassetta postale di origine.
    
        Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    
    Se si desidera eliminare solo i messaggi che soddisfano le condizioni specificate, utilizzare il parametro *SearchQuery* per specificare le condizioni. In questo esempio consente di eliminare i messaggi che contengono la stringa "Your bank statement" nel campo **oggetto**.
    
        Search-Mailbox -Identity "Gurinder Singh" -SearchQuery "Subject:'Your bank statement'" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    

    > [!NOTE]
    > Non è necessario copiare gli elementi per la cassetta postale di individuazione. È possibile copiare i messaggi a qualsiasi cassetta postale. Tuttavia, per impedire l'accesso ai dati delle cassette postali riservate, è consigliabile copiare messaggi in una cassetta postale che dispone dell'accesso con restrizioni per i responsabili dei record autorizzato. Per impostazione predefinita, l'accesso per la cassetta postale di individuazione predefinita è limitato ai membri del gruppo di ruoli gestione individuazione. Per ulteriori informazioni, vedere <A href="in-place-ediscovery-exchange-2013-help.md">eDiscovery sul posto</A>.



10. Se la cassetta postale è stata inserita nella conservazione per controversia legale oppure non dispone di ripristino di singoli elementi è abilitato in precedenza, abilitare queste funzionalità nuovamente.
    
        Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $true -LitigationHoldEnabled $true
    

    > [!IMPORTANT]
    > Dopo aver eseguito questo comando, potrebbe richiedere fino a un'ora per consentire il ripristino di singoli elementi e conservazione per controversia legale. È consigliabile abilitare l'Assistente cartelle gestite e consentire l'accesso client (passaggi 11 e 12) solo dopo questo periodo di tempo.



11. Ripristinare le quote seguenti ai valori indicati nel passaggio 1:
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    
    In questo esempio la cassetta postale viene rimosso dal mantenimento, il periodo di mantenimento elementi eliminati viene reimpostato sul valore predefinito di 14 giorni e la quota degli elementi ripristinabili è configurata per utilizzare lo stesso valore del database delle cassette postali. Se i valori annotato al passaggio 1 sono diversi, è necessario utilizzare i parametri precedenti per specificare ogni valore e impostare il parametro *UseDatabaseQuotaDefaults* su `$false`. I parametri*and UseDatabaseRetentionDefaultsRetainDeletedItemsFor*precedentemente impostati su un valore diverso, deve inoltre ripristinare tali valori indicato nel passaggio 1.
    
        Set-Mailbox "Gurinder Singh" -RetentionHoldEnabled $false -RetainDeletedItemsFor 14 -RecoverableItemsQuota unlimited -UseDatabaseQuotaDefaults $true

12. Attivare l'Assistente cartelle gestite, impostando il ciclo di lavoro valore annotato al passaggio 4. In questo esempio viene impostato il ciclo di lavoro su un giorno.
    
        Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1

13. Attivare l'accesso client.
    
        Set-CASMailbox -ActiveSyncEnabled $true -EwsEnabled $true -MAPIEnabled $true -OWAEnabled $true -ImapEnabled $true -PopEnabled $true

Per ulteriori informazioni sulla sintassi e sui parametri, vedere gli argomenti seguenti:

  - [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\))

  - [Get-CASMailbox](https://technet.microsoft.com/it-it/library/bb124754\(v=exchg.150\))

  - [Get-MailboxFolderStatistics](https://technet.microsoft.com/it-it/library/aa996762\(v=exchg.150\))

  - [Get-MailboxServer](https://technet.microsoft.com/it-it/library/bb123539\(v=exchg.150\))

  - [Set-CASMailbox](https://technet.microsoft.com/it-it/library/bb125264\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\))

  - [Set-MailboxServer](https://technet.microsoft.com/it-it/library/aa998651\(v=exchg.150\))

  - [Search-Mailbox](https://technet.microsoft.com/it-it/library/dd298173\(v=exchg.150\))

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che sono correttamente pulire la cartella elementi recuperabili di una cassetta postale, utilizzare il cmdlet [Get-MailboxFolderStatistics](https://technet.microsoft.com/it-it/library/aa996762\(v=exchg.150\)) controllo le dimensioni della cartella elementi ripristinabili.

Questo esempio vengono recuperate le dimensioni della cartella elementi recuperabili e contare le sottocartelle e un elemento nella cartella e alle sottocartelle.

    Get-MailboxFolderStatistics -Identity "Gurinder Singh" -FolderScope RecoverableItems | Format-Table Name,FolderAndSubfolderSize,ItemsInFolderAndSubfolders -Auto


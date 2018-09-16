---
title: 'Cartelle pubbliche: Exchange 2013 Help'
TOCTitle: Cartelle pubbliche
ms:assetid: 94c4fb69-9234-4b34-8c1c-da2a0a11da65
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150538(v=EXCHG.150)
ms:contentKeyID: 50481235
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cartelle pubbliche

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-03-27_

Le cartelle pubbliche sono progettate per l'accesso condiviso e offrono un metodo semplice ed efficace per raccogliere, organizzare e condividere le informazioni con altre persone del gruppo di lavoro o dell'organizzazione. Le cartelle pubbliche facilitano l'organizzazione del contenuto in base a una gerarchia diretta facile da sfogliare. Gli utenti visualizzeranno la gerarchia completa in Outlook, che consente loro di sfogliare facilmente il contenuto cui sono interessati.


> [!NOTE]
> Le cartelle pubbliche sono disponibili nei seguenti client Outlook: Outlook Web App per Exchange 2013, Outlook 2007, Outlook 2010, Outlook 2013 e Outlook per Mac.



Le cartelle pubbliche possono anche essere utilizzate come metodo di archiviazione per i gruppi di distribuzione. Quando una cartella pubblica viene abilitata alla posta e aggiunta come membro di un gruppo di distribuzione, la posta elettronica inviata al gruppo di distribuzione sarà automaticamente aggiunta alla cartella pubblica per riferimenti futuri.


> [!NOTE]
> È necessario utilizzare Outlook 2007 o versione successiva per accedere alle cartelle pubbliche su server Exchange 2013.



Le cartelle pubbliche non sono destinate ai seguenti scopi:

  - **Archiviazione dati** Gli utenti che hanno limiti delle cassette postali talvolta utilizzano le cartelle pubbliche anziché le cassette postali per archiviare i dati. Questa pratica è sconsigliata perché influisce sulla quantità di dati archiviati nelle cartelle pubbliche e compromette l'obiettivo dei limiti delle cassette postali. In alternativa, si consiglia di utilizzare [Archiviazione sul posto di Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md) come soluzione di archiviazione.

  - **Condivisione dei documenti e collaborazione**. Le cartelle pubbliche non forniscono il controllo della versione o altre funzioni di gestione dei documenti, come la funzione di archiviazione ed estrazione controllata e la notifica automatica delle modifiche al contenuto. Al contrario, si consiglia di utilizzare [SharePoint](https://go.microsoft.com/fwlink/?linkid=282474) come soluzione di condivisione dei documenti.

Per ulteriori informazioni sulle cartelle pubbliche e altri metodi di collaborazione in Exchange 2013, vedere [Collaborazione](collaboration-exchange-2013-help.md).

Per consultare le domande frequenti sulle cartelle pubbliche in Exchange 2013, vedere [Domande frequenti: Cartelle pubbliche](faq-public-folders-exchange-2013-help.md).

Per ulteriori informazioni sui limiti e le quote per le cartelle pubbliche, vedere [Limiti per le cartelle pubbliche](limits-for-public-folders-exchange-2013-help.md).

Per un elenco delle attività di gestione di cartelle pubbliche, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

Per informazioni sulla versione di Exchange Online in questo argomento, vedere [Cartelle pubbliche in Office 365 ed Exchange Online](https://technet.microsoft.com/it-it/library/jj200758\(v=exchg.150\)).

**Sommario**

Architettura delle cartelle pubbliche

Migrare le cartelle pubbliche

Spostamenti delle cartelle pubbliche

Quote delle cartelle pubbliche

Ripristino d'emergenza

## Architettura delle cartelle pubbliche

In Exchange 2013 le cartelle pubbliche sono state riprogettate secondo l'architettura delle cassette postali per sfruttare l'elevata disponibilità esistente e le tecnologie di archiviazione del database delle cassette postali. L'architettura delle cartelle pubbliche utilizza cassette postali speciali per archiviare sia la gerarchia sia il contenuto della cartella pubblica. Questo significa anche che non è più disponibile un database delle cartelle pubbliche. La disponibilità elevata delle cassette postali delle cartelle pubbliche è fornita dal gruppo di disponibilità del database (DAG). Per ulteriori informazioni sui DAG, vedere [Gruppi di disponibilità dei database (DAG)](database-availability-groups-dags-exchange-2013-help.md).

I componenti architettonici principali delle cartelle pubbliche sono le cassette postali delle cartelle pubbliche, che possono essere presenti in uno o più database delle cassette postali.

## Cassette postali delle cartelle pubbliche

Esistono due tipi di cassette postali delle cartelle pubbliche: la *cassetta postale principale* e le *cassette postali secondarie*. Entrambi i tipi di cassette postali possono contenere contenuti:

  - **Cassetta postale principale della gerarchia**La cassetta postale principale della gerarchia è l'unica copia scrivibile della gerarchia di cartelle pubbliche. La gerarchia di cartelle pubbliche viene copiata in tutte le altre cassette postali delle cartelle pubbliche, ma queste saranno copie di sola lettura.

  - **Cassette postali secondarie della gerarchia**   Le cassette postali secondarie della gerarchia contengono elementi pubblici e una copia di sola lettura della gerarchia di cartelle pubbliche.


> [!NOTE]
> I criteri di conservazione non sono supportati per le cassette postali delle cartelle pubbliche.



Esistono due modi per gestire le cassette postali delle cartelle pubbliche:

  - In Interfaccia di amministrazione di Exchange accedere a **Cartelle pubbliche** \> **Cassette postali di cartelle pubbliche**.

  - In Exchange Management Shell, utilizzare l'insieme di cmdlet **\*-Mailbox**. I seguenti parametri sono stati aggiunti al cmdlet [New-Mailbox](https://technet.microsoft.com/it-it/library/aa997663\(v=exchg.150\)) per supportare le cassette postali di cartelle pubbliche:
    
      - *PublicFolder*   Questo parametro viene utilizzato con il cmdlet **New-Mailbox** per creare una cassetta postale di cartelle pubbliche. Quando si crea una cassetta postale di cartelle pubbliche, viene creata una nuova cassetta postale di tipo cassetta postale di `PublicFolder`. Per ulteriori informazioni, vedere [Creazione di una cassetta postale di cartelle pubbliche](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/create-public-folder-mailbox).
    
      - *HoldForMigration*   Questo parametro viene utilizzato solo quando si esegue la migrazione di cartelle pubbliche da una versione precedente a Exchange 2013. Per ulteriori informazioni, vedere Migrare le cartelle pubbliche riportato di seguito in questo argomento.
    
      - *IsHierarchyReady*   Questo parametro indica se la cassetta postale della cartella pubblica è pronta per offrire la gerarchia di cartelle pubbliche agli utenti. Viene impostato su `$True` solo dopo che l'intera gerarchia è stata sincronizzata con la cassetta postale della cartella pubblica. Se il parametro è impostato su $False, gli utenti non lo utilizzeranno per accedere alla gerarchia. Tuttavia, se l'utente ha impostato la proprietà *DefaultPublicFolderMailbox* in una cassetta postale utente per una determinata cassetta postale di cartelle pubbliche, potrà comunque accedere alla cassetta postale delle cartelle pubbliche specificata anche se il parametro *IsHierarchyReady* è impostato su `$False`.
    
      - *IsExcludedFromServingHierarchy*   Questo parametro impedisce agli utenti di accedere alla gerarchia di cartelle pubbliche nella cassetta postale delle cartelle pubbliche specificata. Ai fini del bilanciamento del carico, gli utenti vengono equamente distribuiti tra le cassette postali di cartelle pubbliche per impostazione predefinita. Quando il parametro viene impostato su una cassetta postale di cartelle pubbliche, la cassetta postale non viene inclusa nel bilanciamento del carico automatico e agli utenti non sarà consentito l'accesso per il recupero della gerarchia delle cartelle pubbliche. Tuttavia, se l'utente ha impostato la proprietà *DefaultPublicFolderMailbox* su una cassetta postale utente per una determinata cassetta postale di cartelle pubbliche, potrà comunque accedere alla cassetta postale delle cartelle pubbliche specificata anche se il parametro *IsExcludedFromServingHierarchy* è impostato per quella cassetta postale di cartelle pubbliche.

Una cassetta postale della gerarchia secondaria offre solo informazioni sulla gerarchia di cartelle pubbliche agli utenti se ciò viene specificato in modo esplicito nelle cassette postali dell'utente mediante la proprietà *DefaultPublicFolderMailbox* o se vengono soddisfatte le seguenti condizioni:

  - La proprietà *IsHierarchyReady* nella cassetta postale della cartella pubblica è impostata su `$True`.

  - La proprietà *IsExcludedFromServingHierarchy* nella cassetta postale della cartella pubblica è impostata su `$False`.

## Gerarchia delle cartelle pubbliche

La gerarchia delle cartelle pubbliche contiene le proprietà delle cartelle e informazioni sull'organizzazione, inclusa la struttura ad albero. Ogni cassetta postale delle cartelle pubbliche contiene una copia della gerarchia di cartelle pubbliche. Esiste una sola copia scrivibile della gerarchia, ossia la cassetta postale principale delle cartelle pubbliche. Per una specifica cartella, le informazioni sulla gerarchia vengono utilizzate per identificare i seguenti elementi:

  - Autorizzazioni per la cartella

  - Posizione della cartella nell'albero delle cartelle pubbliche, che include le relative cartelle padre e figlio


> [!NOTE]
> La gerarchia non memorizza le informazioni sugli indirizzi di posta elettronica per le cartelle pubbliche abilitate alla posta. Gli indirizzi di posta elettronica vengono archiviati nell'oggetto directory in Active Directory.



## Sincronizzazione della gerarchia

Il processo di sincronizzazione della gerarchia delle cartelle pubbliche utilizza la sincronizzazione incrementale (ICS), che fornisce un meccanismo di monitoraggio e sincronizzazione delle modifiche del contenuto o della gerarchia di archiviazione di Exchange. Le modifiche includono la creazione, la modifica e l'eliminazione di cartelle e messaggi. Quando gli utenti si connettono alle cassette postali del contenuto e le utilizzano, la sincronizzazione si verifica ogni 15 minuti. Se nessun utente è connesso a una cassetta postale del contenuto, la sincronizzazione viene attivata con minore frequenza (ogni 24 ore). Se un'operazione di scrittura, ad esempio la creazione di una cartella, viene eseguita nella gerarchia principale, viene immediatamente attivata la sincronizzazione alla cassetta postale del contenuto.


> [!IMPORTANT]
> Poiché esiste solamente una copia scrivibile della gerarchia, la creazione delle cartelle è inoltrata alla cassetta postale delle gerarchie dalle cassette postali cui sono collegati gli utenti.



Nelle organizzazioni grandi, quando si crea una nuova cassetta postale di cartelle pubbliche, la gerarchia deve eseguire la sincronizzazione a quella cartella pubblica prima che gli utenti vi si possano collegare. In caso contrario, gli utenti potrebbero visualizzare una struttura di cartelle pubbliche incompleta durante la connessione con Outlook. Per attendere il verificarsi della sincronizzazione senza che gli utenti eseguano tentativi per collegarsi alla nuova cassetta postale di cartelle pubbliche, impostare il parametro *IsExcludedFromServingHierarchy* sul cmdlet **New-Mailbox** durante la creazione della cassetta postale di cartelle pubbliche. Questo parametro impedisce agli utenti di collegarsi alla cassetta postale di cartelle pubbliche appena creata. Una volta completata la sincronizzazione, eseguire il cmdlet [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)) con il parametro *IsExcludedFromServingHierarchy* impostato su `false`, che indica che la cassetta postale di cartelle pubbliche è pronta per il collegamento. È inoltre possibile utilizzare il cmdlet [Get-PublicFolderMailboxDiagnostics](https://technet.microsoft.com/it-it/library/jj218720\(v=exchg.150\)) per visualizzare lo stato di sincronizzazione tramite le proprietà *SyncInfo* e *AssistantInfo*.

Per ulteriori informazioni, vedere [Creare una cartella pubblica](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/create-public-folder).

## Contenuto delle cartelle pubbliche

Le cartelle pubbliche possono contenere messaggi di posta elettronica, post, documenti e eForm. Il contenuto viene archiviato nella cassetta postale delle cartelle pubbliche ma non viene replicato in più cassette postali delle cartelle pubbliche. Tutti gli utenti accedono alla stessa cassetta postale delle cartelle pubbliche per lo stesso insieme di contenuti. Anche se è possibile eseguire una ricerca con testo completo del contenuto delle cartelle pubbliche, tale contenuto non può essere cercato in più cartelle pubbliche e non viene indicizzato da Ricerca di Exchange.


> [!NOTE]
> Outlook Web App è supportato, ma con limitazioni. È possibile aggiungere e rimuovere cartelle pubbliche preferite ed eseguire operazioni a livello di elemento, ad esempio la creazione e l'eliminazione di post, nonché la risposta ai post. Tuttavia, non è possibile creare o eliminare cartelle pubbliche da Outlook Web App. Inoltre, solo le cartelle pubbliche Posta, Post, Calendario e Contatti possono essere aggiunte all'elenco dei preferiti in Outlook Web App.



## Migrare le cartelle pubbliche

È possibile migrare le cartelle pubbliche dalla versione precedente di Exchange Server in Exchange 2013 o dalle versioni precedenti di Exchange Server in Exchange Online. È anche possibile migrare le cartelle pubbliche di Exchange 2013 in Exchange Online.

Se si dispone di cartelle pubbliche Exchange 2010 SP3 o Exchange 2007 SP3 RU10 nell'organizzazione prima di installare Exchange 2013, è necessario eseguirne la migrazione in Exchange 2013. A tal fine, utilizzare i cmdlet **PublicFolderMigrationRequst**. Per ulteriori informazioni, vedere [Utilizzare la migrazione seriale per spostare le cartelle pubbliche in Exchange 2013 dalle versioni precedenti](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md). Se l'organizzazione sta passando a Exchange Online, è possibile migrare le cartelle pubbliche nel cloud e aggiornarle contemporaneamente. Per dettagli, vedere [Utilizzare la migrazione batch delle cartelle pubbliche legacy a Office 365 ed Exchange Online](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/batch-migration-of-legacy-public-folders) e [Utilizzare la migrazione batch per migrare le cartelle pubbliche di Exchange 2013 a Exchange Online](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/batch-migration-of-exchange-2013-public-folders).

A causa delle modifiche al metodo di archiviazione delle cartelle pubbliche, le cassette postali di Exchange legacy non sono in grado di accedere alla gerarchia di cartelle pubbliche su server Exchange 2013 o Exchange Online. Tuttavia, le cassette postali degli utenti su server Exchange 2013 o Exchange Online possono collegarsi alle cartelle pubbliche legacy. Le cartelle pubbliche di Exchange 2013 e le cartelle pubbliche legacy non possono esistere contemporaneamente nell'organizzazione Exchange. Ciò significa che le due versioni non possono coesistere. La migrazione delle cartelle pubbliche in Exchange Server 2013 o Exchange Online attualmente è un processo completo singolo.

Per questo motivo si consiglia di eseguire la migrazione delle cassette postali legacy in Exchange 2013 o Exchange Online, prima di migrare le cartelle pubbliche. Per altre informazioni sulla migrazione delle cassette postali, vedere [Spostamenti di cassette postali di Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md), [Eseguire una migrazione completa della posta elettronica a Office 365](https://go.microsoft.com/fwlink/p/?linkid=536689) e [Eseguire una migrazione a fasi della posta elettronica a Office 365](https://go.microsoft.com/fwlink/p/?linkid=536687).

## Spostamenti delle cartelle pubbliche

È possibile spostare le cartelle pubbliche in una cassetta postale di cartelle pubbliche diversa ed è possibile spostare le cassette pubbliche in database di cassette postali diverse. Per spostare le cartelle pubbliche in cassette postali di cartelle pubbliche diverse, utilizzare l'insieme di cmdlet **PublicFolderMoveRequest**. Le sottocartelle nella cartella pubblica che è stata spostata non verranno spostate per impostazione predefinita. Se si desidera spostare un collegamento delle cartelle pubbliche, è possibile utilizzare lo script `Move-PublicFolderBranch.ps1` installato per impostazione predefinita con Exchange 2013. Per ulteriori informazioni, vedere [Spostare una cartella pubblica in una cassetta postale di cartelle pubbliche diversi](move-a-public-folder-to-a-different-public-folder-mailbox-exchange-2013-help.md).

Oltre a spostare le cartelle pubbliche, è possibile spostare le cassette postali delle cartelle pubbliche in database di cassette postali differenti, utilizzando l'insieme di cmdlet **MoveRequest**. Si tratta dello stesso insieme di cmdlet utilizzato per spostare le cassette postali standard. Per ulteriori informazioni, vedere [Spostare una cassetta postale di cartelle pubbliche a un database delle cassette postali diverse](move-a-public-folder-mailbox-to-a-different-mailbox-database-exchange-2013-help.md).

I cmdlet **PublicFolderMoveRequest** e **MoveRequest** utilizzano il servizio di replica delle cassette postali per spostare le cartelle pubbliche in modo asincrono. Ciò significa che il cmdlet non esegue il lavoro effettivo e durante gran parte dello spostamento la cartella pubblica e le cassette postali di cartelle pubbliche restano a disposizione degli utenti. Poiché il servizio di replica delle cassette postali esegue spostamenti della cassetta postale, richieste di importazione ed esportazione, è importante considerare la gestione del carico di lavoro e le limitazioni.

## Quote delle cartelle pubbliche

Una volta create, le cassette postali di cartelle pubbliche ereditano automaticamente i limiti delle dimensioni delle impostazioni predefinite del database delle cassette postali. Di conseguenza, per valutare in modo accurato lo stato della quota di archiviazione effettiva durante l'utilizzo del cmdlet [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)), è necessario rivedere la proprietà *UseDatabaseQuotaDefaults* oltre alle proprietà *ProhibitSendQuota*, *ProhibitSendReceiveQuota* e *IssueWarningQuota*. Se la proprietà *UseDatabaseQuotaDefaults* è impostata su `true`, le impostazioni per singola cassetta postale vengono ignorate e vengono utilizzati i limiti del database delle cassette postali. Se la proprietà è impostata su `true` e le proprietà *ProhibitSendQuota*, *ProhibitSendReceiveQuota* e *IssueWarningQuota* sono impostate su `unlimited`, la dimensione della cassetta postale non è realmente illimitata. È necessario utilizzare il cmdlet **Get-MailboxDatabase** ed esaminare i limiti di archiviazione del database delle cassette postali per individuare i limiti effettivi della cassetta postale. Se la proprietà *UseDatabaseQuotaDefaults* è impostata su `false`, vengono utilizzate le impostazioni per cassetta postale singola. In Exchange 2013, i limiti predefiniti della quota del database di cassette postali sono i seguenti:

  - *Quota di avviso problema*: 1,9 GB

  - *Quota Impedisci invio*: 2 GB

  - *Quota Impedisci ricezione*: 2,3 GB

Per individuare le quote del database delle cassette postali, eseguire il cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb124924\(v=exchg.150\)).

Per impostare le quote su una cassetta postale di cartelle pubbliche, utilizzare il cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\)).

## Ripristino d'emergenza

Le cartelle pubbliche Exchange 2013 sono create in base all'infrastruttura delle cassette postali e utilizzano gli stessi meccanismi per disponibilità e ridondanza. Ogni cassetta postale di cartelle pubbliche può avere più copie ridondanti con failover automatico, esattamente come le cassette postali standard. Per ulteriori informazioni, vedere [Disponibilità elevata e resilienza del sito](high-availability-and-site-resilience-exchange-2013-help.md).

Oltre allo scenario generale di ripristino di emergenza, è possibile ripristinare le cartelle pubbliche anche nei casi riportati:

  - **Ripristino di cartelle pubbliche con eliminazione reversibile**   La cartella pubblica è stata eliminata, ma è ancora nel periodo di conservazione.

  - **Ripristino di cassette postali cartelle pubbliche con eliminazione reversibile**   La cassetta postale di cartelle pubbliche è stata eliminata, ma è ancora nel periodo di conservazione della cassetta postale.

  - **Ripristino della cassetta postale di cartelle pubbliche da un database di ripristino**   È possibile ripristinare dal backup una singola cassetta postale di cartelle pubbliche una volta trascorso il periodo di conservazione della cassetta postale eliminata. Successivamente è possibile estrarre i dati dalla cassetta postale ripristinata e copiarli in una cartella di destinazione o unirli a un'altra cassetta postale.

In tutti questi casi, la cartella pubblica o la cassetta postale di cartelle pubbliche è ripristinabile tramite i cmdlet **MailboxRestoreRequest**.

Per ulteriori informazioni, vedere [Ripristinare le cartelle pubbliche e cassette postali delle cartelle pubbliche da spostamenti non riusciti](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).


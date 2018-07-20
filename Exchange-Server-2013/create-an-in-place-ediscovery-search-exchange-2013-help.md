---
title: 'Creazione di una ricerca eDiscovery sul posto: Exchange 2013 Help'
TOCTitle: Creazione di una ricerca eDiscovery sul posto
ms:assetid: feedc0c9-4a44-4bb2-8520-cc29d66d4fc3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd353189(v=EXCHG.150)
ms:contentKeyID: 50482135
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creazione di una ricerca eDiscovery sul posto

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-01-17_


> [!NOTE]
> La scadenza per la creazione di nuove ricerche eDiscovery sul posto in Exchange Online (nei piani autonomi di Office 365 e Exchange Online) è stata rimandata al 1° luglio 2017. Tuttavia, nell'ultima parte di quest'anno oppure all'inizio del prossimo, non sarà possibile creare nuove ricerche in Exchange Online. Per creare ricerche eDiscovery, iniziare a usare <A href="https://go.microsoft.com/fwlink/?linkid=847843">Ricerca contenuto</A> nel Centro sicurezza e conformità di Office 365. Una volta sospesa la creazione di nuove ricerche eDiscovery sul posto, sarà possibile modificare le ricerche eDiscovery sul posto esistenti e creare nuove ricerche eDiscovery sul posto nelle distribuzioni ibride di Exchange Server 2013 e Exchange.



Utilizzare [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md) per eseguire una ricerca nell'intero contenuto di una cassetta postale, inclusi gli elementi eliminati e le versioni originali degli elementi modificati per gli utenti con [Archiviazione sul posto e conservazione per controversia legale](in-place-hold-and-litigation-hold-exchange-2013-help.md) impostata.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "eDiscovery locale" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per creare ricerche eDiscovery, è necessario disporre di un indirizzo SMTP nell'organizzazione che si sta creando le ricerche in. Pertanto in Exchange Online, è necessario disporre di una cassetta postale di Exchange Online (piano 2) con licenza per creare ricerche eDiscovery. In un'organizzazione ibrida di Exchange, cassetta postale di Exchange locale deve disporre un account utente corrispondente di posta elettronica nell'organizzazione Office 365 in modo che è possibile cercare cassette postali Exchange Online. In alternativa, se si accede con un account che esiste solo in Office 365, ad esempio l'account di amministratore tenant, tale account deve essere assegnato una licenza di Exchange Online (piano 2).

  - Il programma di installazione di Exchange 2013 consente la creazione di una cassetta postale di individuazione denominata **Cassetta postale di individuazione** in cui copiare i risultati della ricerca. Per impostazione predefinita, la cassetta postale di individuazione viene creata anche in Exchange Online. È possibile creare ulteriori cassette postali di individuazione. Per ulteriori informazioni, vedere [Creazione di una cassetta postale di individuazione](create-a-discovery-mailbox-exchange-2013-help.md).

  - Quando si crea una ricerca eDiscovery in locale, i messaggi restituiti nei risultati della ricerca non vengono copiati automaticamente nella cassetta postale di individuazione. Una volta creata la ricerca, utilizzare l'interfaccia di amministrazione di Exchange (EAC) per la stima, l'anteprima o la copia dei risultati della ricerca in una cassetta postale di individuazione. Per dettagli, vedere:
    
      - Estimate or preview search results (più avanti in questo argomento)
    
      - [Copiare i risultati della ricerca eDiscovery in una cassetta postale di individuazione](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Creazione di una ricerca eDiscovery in locale tramite l'interfaccia di amministrazione di Exchange

Come indicato in precedenza, per creare ricerche eDiscovery è necessario accedere a un account utente che dispone di un indirizzo SMTP nell'organizzazione.

1.  Accedere a **Gestione conformità** \> **eDiscovery e archiviazione sul posto&**.

2.  Fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  In **eDiscovery** e conservazione in locale, nella pagina **Nome e descrizione** digitare un nome per la ricerca, aggiungere un'eventuale descrizione facoltativa, quindi fare clic su **Avanti**.

4.  Nella pagina **cassette postali**, selezionare le cassette postali per la ricerca. È possibile eseguire una ricerca tutte le cassette postali o selezionare quelle specifiche per la ricerca. In Exchange Online, è inoltre possibile selezionare gruppi Office 365 come origine di contenuto per la ricerca.
    

    > [!IMPORTANT]
    > Non è possibile utilizzare l'opzione <STRONG>Cerca in tutte le cassette postali</STRONG> per mettere in conservazione tutte le cassette postali. Per creare un'archiviazione sul posto, è necessario selezionare <STRONG>Specify mailboxes to search</STRONG>. Per ulteriori dettagli, vedere <A href="create-or-remove-an-in-place-hold-exchange-2013-help.md">Creare o rimuovere un'archiviazione sul posto</A>.



5.  Nella pagina **Query di ricerca** compilare i seguenti campi:
    
      - **Include all user mailbox content**   Selezionare questa opzione per mettere in conservazione tutto il contenuto nelle cassette postali selezionate. Se viene selezionata questa opzione, non è possibile specificare ulteriori criteri di ricerca.
    
      - **Filtro basato su criteri**   Selezionare questa opzione per specificare i criteri di ricerca, inclusi parole chiave, data di inizio e fine, indirizzo di mittente e destinatario e tipi di messaggi.
        
        ![Configurazione query ricerca di eDiscovery](images/Dd353189.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "Configurazione query ricerca di eDiscovery")  
    

    > [!NOTE]
    > Il <STRONG>da:</STRONG> e <STRONG>a/Cc/Ccn:</STRONG> campi sono connessi tramite un operatore <STRONG>o</STRONG> nella query di ricerca che viene creato quando si esegue la ricerca. Ciò significa che tutti i messaggi inviati o ricevuti da tutti gli utenti specificato (e gli altri criteri di ricerca corrispondenze) sono incluso nei risultati della ricerca.<BR>Le date sono connessi tramite un operatore <STRONG>AND</STRONG>.



6.  Nella pagina **Impostazioni di conservazione in locale**, selezionare la casella di controllo **Conserva il contenuto che corrisponde alla query di ricerca nelle cassette postali selezionate**, quindi selezionare una delle seguenti opzioni per impostare gli elementi su Archiviazione sul posto:
    
      - **In mantenimento illimitato**   Selezionare questa opzione per impostare gli elementi restituiti su un mantenimento illimitato. Gli elementi conservati verranno mantenuti fino a quando la cassetta postale non sarà stata rimossa dalla ricerca o non sarà stata eliminata la ricerca.
    
      - **Specifica numero di giorni di archiviazione degli elementi in relazione alla data di ricezione** Utilizzare questa opzione per conservare gli elementi per un periodo determinato. Ad esempio, è possibile utilizzare questa opzione se l'organizzazione richiede che tutti i messaggi vengano conservati per almeno sette anni. È possibile utilizzare una conservazione in locale *basata sul tempo* insieme al criterio di conservazione per essere certi che gli elementi vengano eliminati dopo sette anni.
        

        > [!IMPORTANT]
        > Quando le cassette postali o gli elementi vengono messi nell'archiviazione sul posto per motivi legali, si consiglia in genere di conservarli in modo illimitato e rimuovere la conservazione una volta terminati la causa o l'indagine.



7.  Selezionare **Fine** per salvare la ricerca e ottenere una stima delle dimensioni totali e del numeri di elementi che saranno restituiti dalla ricerca sulla base dei criteri specificati. Le stime vengono visualizzate nel riquadro dei dettagli. Fare clic su **Aggiorna**![Icona Aggiorna](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icona Aggiorna") per aggiornare le informazioni visualizzate nel riquadro dei dettagli.

Torna all'inizio

## Creazione di una ricerca eDiscovery in locale tramite Shell

In questo esempio viene creata la ricerca di eDiscovery In locale denominata Discovery-CaseId012 che consente di cercare gli elementi contenenti le parole chiave Contoso e ProjectA e che soddisfano anche i seguenti criteri:

  - Data di inizio: 1/1/2009

  - Data di fine: 12/31/2011

  - Cassetta postale di origine: DG-Finance

  - Cassetta postale di destinazione: Cassetta postale di individuazione

  - Tipi di messaggi: Email

  - Include gli elementi non ricercabili nelle statistiche ricerca

  - Livello di registrazione: Completa


> [!IMPORTANT]
> Se non si specificano ulteriori parametri di ricerca durante l'esecuzione della ricerca eDiscovery in locale, tutti gli elementi delle cassette postali di origine specificati vengono inclusi nei risultati. Se non si specificano le cassette postali in cui effettuare la ricerca, saranno incluse nella ricerca tutte le cassette postali dell'organizzazione di Exchange o Exchange Online.



    New-MailboxSearch "Discovery-CaseId012" -StartDate "01/01/2009" -EndDate "12/31/2011" -SourceMailboxes "DG-Finance" -TargetMailbox "Discovery Search Mailbox" -SearchQuery '"Contoso" AND "Project A"' -MessageTypes Email -IncludeUnsearchableItems -LogLevel Full


> [!NOTE]
> Quando si utilizzano i parametri <EM>StartDate</EM> e <EM>EndDate</EM>, è necessario utilizzare il formato di data mm/gg/aaaa, anche se le impostazioni del computer locale utilizzano un formato di data differente, ad esempio gg/mm/aaaa. Ad esempio, per cercare i messaggi inviati tra la data 1 aprile e 1 luglio 2013, verrà utilizzato il formato <STRONG>04/01/2013</STRONG> e <STRONG>07/01/2013</STRONG> per le date di inizio e di fine.



Questo esempio viene creata una ricerca eDiscovery In locale denominata HRCase090116 che esegue una ricerca per i messaggi di posta elettronica inviati da Alex Darrow in Sara Davis in 2015.

    New-MailboxSearch "HRCase090116" -StartDate "01/01/2015" -EndDate "12/31/2015" -SourceMailboxes  alexd,sarad -SearchQuery 'From:alexd@contoso.com AND To:sarad@contoso.com' -MessageTypes Email -TargetMailbox "Discovery Search Mailbox" -IncludeUnsearchableItems -LogLevel Full

Dopo aver utilizzato la shell per creare una ricerca eDiscovery locale, è necessario avviare la ricerca utilizzando il cmdlet **Start-MailboxSearch** per copiare i messaggi sulla cassetta postale di individuazione specificata nel parametro *TargetMailbox*. Per ulteriori informazioni, vedere [Copiare i risultati della ricerca eDiscovery in una cassetta postale di individuazione](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md).

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MailboxSearch](https://technet.microsoft.com/it-it/library/dd298064\(v=exchg.150\)).

Torna all'inizio

## Utilizzare l'interfaccia di amministrazione di Exchange per visualizzare una stima o un'anteprima dei risultati di ricerca

Dopo aver creato una ricerca eDiscovery in locale, è possibile utilizzare l'interfaccia di amministrazione di Exchange per visualizzare una stima o un'anteprima dei risultati di ricerca. Se è stata creata una nuova ricerca utilizzando il cmdlet **New-MailboxSearch**, è possibile utilizzare la shell per avviare la ricerca e visualizzare una stima dei risultati di ricerca. Non è possibile utilizzare Shell per visualizzare l'anteprima dei messaggi restituiti nei risultati della ricerca.

1.  Accedere a **Gestione conformità** \> **eDiscovery e conservazione in locale**.

2.  Nella visualizzazione elenco, selezionare la ricerca di eDiscovery In locale e quindi eseguire una delle operazioni seguenti:
    
      - Fare clic su **ricerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca") \> **stima dei risultati di ricerca** per restituire una stima delle dimensioni totali e numero di elementi che verranno restituiti dalla ricerca in base ai criteri specificati. Se si seleziona questa opzione Riavvia ricerca ed esegue una stima.
        
        Le stime della ricerca vengono visualizzate nel riquadro dei dettagli. Fare clic su **Aggiorna**![Icona Aggiorna](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icona Aggiorna") per aggiornare le informazioni visualizzate nel riquadro dei dettagli.
    
      - Fare clic su **Anteprima risultati di ricerca** nel riquadro dei dettagli per visualizzare in anteprima i risultati di una volta completata la stima di ricerca. Se si seleziona questa opzione apre la finestra di **anteprima della ricerca eDiscovery**. Vengono visualizzati tutti i messaggi restituiti dalle cassette postali in cui sono stati una ricerca.
        

        > [!NOTE]
        > Le cassette postali in cui è stata eseguita la ricerca vengono visualizzate nel riquadro a destra della finestra <STRONG>Anteprima di ricerca eDiscovery</STRONG>. Per ogni cassetta postale, viene visualizzato il numero degli elementi restituiti e la loro dimensione totale. Tutti gli elementi restituiti dalla ricerca vengono elencati nel riquadro a destra e possono essere ordinati in base alla data più o meno recente. Non è possibile visualizzare gli elementi di ogni cassetta postale nel riquadro a destra se si seleziona una cassetta postale nel riquadro a sinistra. Per visualizzare gli elementi restituiti da una cassetta postale specifica, è possibile copiare i risultati di ricerca e visualizzare gli elementi nella cassetta postale di individuazione.

    
    ![Stima o anteprima dei risultati di ricerca](images/Dd353189.57e0fc2d-71bf-42aa-aa4b-4a77148f2b43(EXCHG.150).gif "Stima o anteprima dei risultati di ricerca")  

Torna all'inizio

## Utilizzare la shell per eseguire una stima dei risultati di ricerca

È possibile utilizzare l'opzione *EstimateOnly* per ottenere soltanto una stima dei risultati di ricerca e non per copiare tali risultati in una cassetta postale di individuazione. È necessario avviare una ricerca di tipo solo stime con il cmdlet **Start-MailboxSearch**. In seguito, è possibile recuperare i risultati di ricerca stimati utilizzando il cmdlet **Get-MailboxSearch**.

Ad esempio, è necessario eseguire i comandi seguenti per creare una nuova ricerca eDiscovery e per visualizzare una stima dei risultati di ricerca.

```
New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeKeywordStatistics
```
```
Start-MailboxSearch "FY13 Q2 Financial Results"
```
```
Get-MailboxSearch "FY13 Q2 Financial Results"
```

Per visualizzare informazioni specifiche sui risultati di ricerca stimati nel precedente esempio, è possibile eseguire il comando seguente:

    Get-MailboxSearch "FY13 Q2 Financial Results" | FL Name,Status,LastRunBy,LastStartTime,LastEndTime,Sources,SearchQuery,ResultSizeEstimate,ResultNumberEstimate,Errors,KeywordHits

Torna all'inizio

## Ulteriori informazioni sulle ricerche eDiscovery

  - Dopo aver creato una nuova ricerca eDiscovery, è possibile copiare i risultati di ricerca nella cassetta postale di individuazione ed esportare tali risultati in un file PST. Per ulteriori informazioni, vedere:
    
      - [Copiare i risultati della ricerca eDiscovery in una cassetta postale di individuazione](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)
    
      - [Esportazione dei risultati della ricerca eDiscovery in un file PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)

  - Dopo aver eseguito una stima di ricerca di eDiscovery (che include le parole chiave nei criteri di ricerca), è possibile visualizzare statistiche sulle parole chiave fare clic su **statistiche sulle parole chiave visualizzazione** nel riquadro dei dettagli per la ricerca selezionata. Questi dati statistici Mostra dettagli sul numero di elementi restituiti per ogni parola chiave utilizzata nella query di ricerca. Se, tuttavia, la ricerca include più di 100 cassette postali di origine, è verrà restituito un errore se si tenta di visualizzare statistiche sulle parole chiave. Per visualizzare statistiche sulle parole chiave, è possono includere non più di 100 cassette postali di origine nella ricerca.

  - Se si utilizza **Get-MailboxSearch** in Exchange Online per recuperare informazioni su una ricerca eDiscovery, è necessario specificare il nome di una ricerca per restituire un elenco completo delle proprietà di ricerca. ad esempio, `Get-MailboxSearch "Contoso Legal Case"`. Se si esegue il cmdlet **Get-MailboxSearch** senza alcun parametro, non vengono restituite le proprietà seguenti:
    
      - SourceMailboxes
    
      - Sources
    
      - SearchQuery
    
      - ResultsLink
    
      - PreviewResultsLink
    
      - Errors
    
    Il motivo è che richiede molte risorse per restituire le proprietà per tutte le ricerche di eDiscovery nell'organizzazione.

Torna all'inizio


---
title: 'eDiscovery sul posto: Exchange 2013 Help'
TOCTitle: eDiscovery sul posto
ms:assetid: 6377cb7a-3416-4e15-8571-c45d2160fc6f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298021(v=EXCHG.150)
ms:contentKeyID: 50480811
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# eDiscovery sul posto

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-01-17_


> [!NOTE]
> La scadenza per la creazione di nuove ricerche eDiscovery sul posto in Exchange Online (nei piani autonomi di Office 365 e Exchange Online) è stata rimandata al 1° luglio 2017. Tuttavia, nell'ultima parte di quest'anno oppure all'inizio del prossimo, non sarà possibile creare nuove ricerche in Exchange Online. Per creare ricerche eDiscovery, iniziare a usare <A href="https://go.microsoft.com/fwlink/?linkid=847843">Ricerca contenuto</A> nel Centro sicurezza e conformità di Office 365. Una volta sospesa la creazione di nuove ricerche eDiscovery sul posto, sarà possibile modificare le ricerche eDiscovery sul posto esistenti e creare nuove ricerche eDiscovery sul posto nelle distribuzioni ibride di Exchange Server 2013 e Exchange.



Se l'organizzazione soddisfa i requisiti di presentazione del materiale probatorio (relativi alla politica dell'organizzazione, ai requisiti di conformità o ai processi), eDiscovery in locale in Microsoft Exchange Server 2013 e Exchange Online consente di eseguire ricerche per l'individuazione del contenuto all'interno delle cassette postali. Exchange 2013 e Exchange Online offrono, inoltre, funzionalità di ricerca federata e integrazione con Microsoft SharePoint 2013 e Microsoft SharePoint Online. Tramite Centro eDiscovery in SharePoint, è possibile cercare e conservare tutti i contenuti relativi a un caso, tra cui siti Web di SharePoint 2013 e SharePoint Online, documenti, condivisioni file indicizzate da SharePoint (soltanto SharePoint 2013), contenuto delle cassette postali in Exchange e il contenuto archiviato di Lync 2013. È anche possibile utilizzare eDiscovery in locale in un ambiente Exchange ibrido per cercare contemporaneamente nella cassette postali locali e e basate su cloud.

**Sommario**

How In-Place eDiscovery works

Exchange Search

Discovery Management role group and management roles

Custom management scopes for In-Place eDiscovery

Integration with SharePoint Server 2013 and SharePoint Online

eDiscovery in an Exchange hybrid deployment

Discovery mailboxes

Using In-Place eDiscovery

Estimate, preview, and copy search results

Export search results to a PST file

Different search results

Logging for In-Place eDiscovery searches

In-Place eDiscovery and In-Place Hold

Preserving mailboxes for In-Place eDiscovery

In-Place eDiscovery limits and throttling policies

In-Place eDiscovery documentation


> [!IMPORTANT]
> eDiscovery in locale è una funzionalità avanzata che consente a un utente con le autorizzazioni appropriate di avere accesso a tutti i record di messaggistica archiviati nell'organizzazione di Exchange 2013 o Exchange Online. È importante controllare e monitorare le attività di individuazione, compresa l'aggiunta di membri al gruppo di ruoli Gestione individuazione, l'assegnazione del ruolo di gestione Ricerca cassette postali e il permesso di accedere alla casella postale per l'individuazione di cassette postali.



## Funzionamento di eDiscovery in locale

eDiscovery in locale utilizza gli indici del contenuto creati da Ricerca di Exchange. Il controllo dell'accesso basato sui ruoli consente al gruppo di ruoli [Gestione individuazione](discovery-management-exchange-2013-help.md) di delegare le attività di individuazione a utenti non tecnici, senza la necessità di fornire privilegi elevati che potrebbero consentire all'utente di apportare modifiche operative alla configurazione di Exchange. L'interfaccia di amministrazione di Exchange offre un'interfaccia di ricerca semplice da utilizzare per gli utenti non tecnici, quali addetti al settore legale, responsabili della conformità, record manager e addetti alle risorse umane.

Gli utenti autorizzati possono eseguire una ricerca eDiscovery in locale selezionando le cassette postali e specificando quindi criteri come parole chiave, date di inizio e fine, indirizzi di mittenti e destinatari e tipo di messaggi. Una volta completata la ricerca, gli utenti autorizzati possono selezionare una delle azioni seguenti:

  - **Stima i risultati della ricerca**   Queste opzione consente di ottenere una stima delle dimensioni totali e del numero di elementi che saranno restituiti dalla ricerca sulla base dei criteri specificati.

  - **Visualizza in anteprima i risultati della ricerca** Questa opzione consente di visualizzare un'anteprima dei risultati. Vengono visualizzati i messaggi restituiti da ciascuna cassetta postale interessata dalla ricerca.

  - **Copia i risultati della ricerca**   Questa opzione consente di copiare i messaggi in una cassetta postale di individuazione.

  - **Esportazione risultati di ricerca**   Dopo aver copiato i risultati di una ricerca su una cassetta postale di individuazione, è possibile esportarli su file PST.

![Stima, anteprima, copia ed esportazioni risultati della ricerca](images/Dd298021.6356971a-34ed-4586-8229-030448d4fe2d(EXCHG.150).gif "Stima, anteprima, copia ed esportazioni risultati della ricerca")

## Ricerca di Exchange

eDiscovery in locale utilizza gli indici di contenuto creati da Ricerca di Exchange. Ricerca di Exchange è stata riorganizzato per l'utilizzo di Microsoft Search Foundation, una elaborata piattaforma di ricerca che viene fornita con l'indicizzazione, le prestazioni di query e la funzionalità di ricerca piuttosto migliorati. Poiché la funzionalità Microsoft Search Foundation viene utilizzata anche da altri prodotti Office, incluso SharePoint 2013, offre una maggiore interoperabilità e una sintassi di ricerca migliore per questi prodotti.

Con un unico motore di indicizzazione del contenuto, nessuna risorsa aggiuntiva viene utilizzata per eseguire la ricerca per indicizzazione e per indicizzare i database delle cassette postali per eDiscovery in locale quando i reparti IT ricevono richieste da eDiscovery.

eDiscovery in locale utilizza la sintassi KQL (Keyword Query Language), una sintassi per l'invio di query simile alla sintassi di ricerca avanzata utilizzata da Ricerca immediata in Microsoft Outlook e Outlook Web App. Gli utenti che hanno familiarità con la sintassi KQL possono creare facilmente query di ricerca potenti per cercare gli indici del contenuto.

Per ulteriori informazioni sui formati di file indicizzati da Ricerca Exchange, vedere [Formati di file indicizzati da ricerca di Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md).

## Gruppo di ruoli Gestione individuazione e ruoli di gestione

Per fare in modo che gli utenti autorizzati eseguano le ricerche eDiscovery in locale, è necessario aggiungerli al gruppo di ruoli [Gestione individuazione](discovery-management-exchange-2013-help.md). Questo gruppo contiene due ruoli di gestione: il [Ruolo di ricerca di cassette postali](mailbox-search-role-exchange-2013-help.md), che consente a un utente di eseguire una ricerca eDiscovery in locale e il [Ruolo di conservazione legale](legal-hold-role-exchange-2013-help.md), che consente a un utente di applicare a una cassetta postale Archiviazione sul posto o la conservazione per controversia legale.

Per impostazione predefinita, le autorizzazioni a eseguire attività associate a eDiscovery in locale non vengono assegnate a un qualsiasi utente o agli amministratori di Exchange. Gli amministratori di Exchange che sono membri del gruppo di ruoli Gestione organizzazione possono aggiungere utenti al gruppo di ruoli Gestione individuazione e creare gruppi di ruoli personalizzati per restringere l'ambito di un responsabile dell'individuazione a un sottoinsieme di utenti. Per ulteriori informazioni sull'aggiunta di utenti al gruppo di ruoli Gestione individuazione, vedere [Assegnare le autorizzazioni di eDiscovery di Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).


> [!IMPORTANT]
> Se un utente non è stato aggiunto al gruppo di ruoli Gestione individuazione o non è stato assegnato al ruolo Ricerca cassette postali, l'interfaccia utente di <STRONG>eDiscovery e conservazione in locale</STRONG> non viene visualizzato nell'interfaccia di amministrazione di Exchange e i cmdlet di eDiscovery in locale non saranno disponibili in Exchange Management Shell.



Il controllo delle modifiche al ruolo RBAC, abilitato per impostazione predefinita, consente di mantenere i record adeguati per verificare l'assegnazione del gruppo di ruoli Gestione individuazione. È possibile utilizzare il rapporto del gruppo di ruoli di amministratore per cercare le modifiche apportate ai gruppi di ruoli di amministratore. Per ulteriori informazioni, vedere [Ricerca delle modifiche al gruppo di ruoli o i registri di controllo dell'amministratore](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

Inizio pagina

## Ambiti di gestione personalizzata per eDiscovery in locale

È possibile utilizzare un ambito di gestione personalizzata per consentire a contatti o gruppi specifici l'utilizzo di eDiscovery in locale per ricercare un sottoinsieme di cassette postali nell'organizzazione Exchange 2013 o Exchange Online Per esempio, se si desidera eseguire una ricerca di gestione individuazione solo per le cassette postali di utenti in una determinata posizione o di un reparto specifico. È possibile farlo attraverso la creazione di un ambito di gestione personalizzata che utilizza un filtro destinatario personalizzato per controllare quali cassette postali si possono ricercare. Gli ambiti di filtro dei destinatari utilizzano filtri da applicare a specifici destinatari in base al tipo di destinatario o altre proprietà del destinatario.

Per eDiscovery in locale, l'unica proprietà su una cassetta postale utente che è possibile utilizzare per creare un filtro destinatario per un ambito personalizzato è l'appartenenza a gruppi di distribuzione. Se si utilizzano altre proprietà, come *CustomAttributeN*, *Department* o *PostalCode*, è impossibile eseguire la ricerca quando viene eseguita da un membro del gruppo di ruoli assegnato all'ambito personalizzato. Per ulteriori informazioni, vedi [Creazione di un ambito di gestione personalizzato per le ricerche di eDiscovery sul posto](create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md).

## Integrazione con SharePoint Server 2013 e SharePoint Online

Exchange 2013 e Exchange Online offrono l'integrazione con SharePoint 2013 e SharePoint Online, consentendo a un responsabile dell'individuazione di utilizzare Centro eDiscovery in SharePoint per eseguire le seguenti attività:

  - **Ricerca e conserva il contenuto da una singola posizione** Un responsabile dell'individuazione autorizzato può ricercare e conservare il contenuto in SharePoint ed Exchange, inclusi i contenuti Lync, quali conversazioni di messaggistica immediata e documenti di riunione condivisi archiviati nelle cassette postali di Exchange.

  - **Gestione casi** Centro eDiscovery utilizza un approccio alla gestione dei casi su eDiscovery, consentendo di creare casi e di ricercare e conservare il contenuto in archivi di contenuto differenti per ciascun caso.

  - **Esporta risultati ricerca** Un responsabile dell'individuazione può utilizzare Centro eDiscovery per esportare i risultati di ricerca. Il contenuto della cassetta postale incluso nei risultati di ricerca viene esportato in un file PST.

SharePoint utilizza anche Microsoft Search Foundation per l'invio di query e l'indicizzazione del contenuto. Indipendentemente dal fatto che un responsabile dell'individuazione utilizzi l'interfaccia di amministrazione di Exchange o il Centro eDiscovery per ricercare il contenuto Exchange, viene restituito lo stesso contenuto della cassetta postale.

Nelle distribuzioni locali, prima di poter utilizzare Centro eDiscovery in SharePoint per ricercare cassette postali di Exchange, è necessario stabilire attendibilità tra le due applicazioni. In Exchange 2013 e SharePoint 2013, questo viene fatto utilizzando l'autenticazione OAuth. Per informazioni dettagliate, vedere [Configurare Exchange per SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md). Le ricerche eDiscovery eseguite da SharePoint sono autorizzate da Exchange tramite RBAC. Affinché un utente SharePoint possa eseguire una ricerca eDiscovery di cassette postali di Exchange, queste devono godere dell'autorizzazione di Gestione individuazione delegata in Exchange. Per poter visualizzare un'anteprima del contenuto delle cassette postali restituito durante una ricerca eDiscovery eseguita utilizzando un Centro eDiscovery SharePoint, il responsabile dell'individuazione deve disporre di una cassetta postale nella stessa organizzazione di Exchange.

Per passaggio istruzioni dettagliate per la configurazione di un eDiscovery Center in un'organizzazione Office 365, vedere [configurare un centro eDiscovery di SharePoint Online](https://go.microsoft.com/fwlink/p/?linkid=331600).

## eDiscovery in una distribuzione ibrida di Exchange

Per eseguire correttamente delle ricerche eDiscovery estese in un'organizzazione Exchange 2013 ibrida, è necessario configurare l'autenticazione OAuth (Open Authorization) tra organizzazioni Exchange in locale e Exchange Online in modo che sia possibile utilizzare eDiscovery in locale per ricercare cassette postali in locale e basate sul cloud. L'autenticazione OAuth è un protocollo di autenticazione S2S che consente alle applicazioni di eseguire l'autenticazione reciproca.

L'autenticazione OAuth supporta i seguenti scenari di eDiscovery in un'implementazione ibrida di Exchange:

  - Cassette postali di ricerca locali che utilizzano il Archiviazione Exchange Online per le cassette postali basate su cloud.

  - Ricerca locale e cassette postali basate su cloud nella ricerca di eDiscovery stesso.

  - Ricerca cassette postali locali tramite eDiscovery Center in SharePoint Online.

Per ulteriori informazioni su scenari eDiscovery che richiedono la configurazione dell'autenticazione OAuth in una distribuzione ibrida di Exchange, vedere [Utilizzo dell'autenticazione OAuth per supportare eDiscovery in un'implementazione ibrida di Exchange](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md). Per istruzioni dettagliate sulla configurazione dell'autenticazione OAuth per supportare eDiscovery, vedere [Configurazione dell'autenticazione OAuth tra organizzazioni di Exchange ed Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md).

## Cassette postali di individuazione

Una volta creata una ricerca eDiscovery in locale, è possibile copiare i risultati della ricerca in una cassetta postale di destinazione. L'interfaccia di amministrazione di Exchange consente di selezionare una cassetta postale di individuazione come cassetta postale di destinazione. Una cassetta postale di individuazione è un tipo speciale di cassetta postale che offre le seguenti funzionalità:

  - **Selezione sicura e più semplice della cassetta postale di destinazione**   Quando si utilizza l'interfaccia di amministrazione di Exchange per copiare i risultati di una ricerca eDiscovery in locale, sarà possibile archiviare i risultati della ricerca solo nelle cassette postali di individuazione. Non è necessario esaminare un elenco lungo di cassette postali disponibili nell'organizzazione. In questo modo, un responsabile dell'individuazione non selezionerà accidentalmente un'altra cassetta postale o una cassetta postale non protetta in cui archiviare il contenuto riservato dei messaggi.

  - **Quota superiore di archiviazione della cassetta postale**   La cassetta postale di destinazione deve essere in grado di archiviare grandi quantità di dati relativi ai messaggi che possono essere restituiti da una ricerca eDiscovery in locale. Per impostazione predefinita, le cassette postali di individuazione dispongono di una quota di archiviazione delle cassette postali di 50 gigabyte (GB). Questo limite di archiviazione può essere aumentato.

  - **Maggiore sicurezza per impostazione predefinita**   Come tutti i tipi di cassette postali, una cassetta postale di individuazione ha un account utente di Active Directory associato. Tuttavia, questo account è disabilitato per impostazione predefinita. Solo gli utenti autorizzati ad accedere alla cassetta postale di individuazione, potranno utilizzarlo. Ai membri del gruppo di ruoli Gestione individuazione vengono assegnate le autorizzazioni di accesso completo per la cassetta postale di individuazione predefinita. Le autorizzazioni di accesso alla cassetta postale non verranno assegnate a qualsiasi utente di altre cassette postali di individuazione create.

  - **Recapito messaggi di posta elettronica disabilitato**   Anche se visibili negli elenchi indirizzi di Exchange, gli utenti non possono inviare messaggi di posta elettronica a una cassetta postale di individuazione. Il recapito di messaggi di posta elettronica alle cassette postali di individuazione è proibito utilizzando le restrizioni di recapito. Ciò preserva l'integrità dei risultati di ricerca copiati in una cassetta postale di individuazione.

Il programma di installazione di Exchange 2013 crea una cassetta postale di individuazione con il nome **Cassetta postale di individuazione**. È possibile utilizzare Shell per creare altre cassette postali di individuazione. Per impostazione predefinita, alle altre cassette postali di individuazione create non verranno assegnate le autorizzazioni di accesso alle cassette postali. È possibile assegnare autorizzazioni di accesso completo per consentire a un responsabile dell'individuazione di accedere ai messaggi copiati in una cassetta postale di individuazione. Per ulteriori informazioni, vedere [Creazione di una cassetta postale di individuazione](create-a-discovery-mailbox-exchange-2013-help.md).

eDiscovery in locale utilizza anche una cassetta postale di sistema con il nome visualizzato **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}** per conservare i metadati di eDiscovery in locale. Le cassette postali di sistema non sono visibili nell'interfaccia di amministrazione di Exchange o negli elenchi di indirizzi di Exchange. Nelle organizzazioni locali, prima di rimuovere un database delle cassette postali in cui si trova la cassetta postale di sistema eDiscovery in locale, è necessario spostare la cassetta postale in un altro database di cassette postali. Se la cassetta postale viene rimossa o danneggiata, i responsabili dell'individuazione non sono in grado di eseguire ricerche eDiscovery fino a quando non viene ricreata la cassetta postale. Per ulteriori informazioni, vedere [Re-create the Discovery system mailbox](re-create-the-discovery-system-mailbox-exchange-2013-help.md).

Inizio pagina

## Utilizzo di eDiscovery in locale

Gli utenti che sono stati aggiunti al gruppo di ruoli Gestione individuazione possono eseguire ricerche eDiscovery in locale. È possibile eseguire una ricerca utilizzando l'interfaccia basata sul Web nell'interfaccia di amministrazione di Exchange. Ciò facilita l'utilizzo di eDiscovery in locale da parte di utenti non tecnici, ad esempio responsabili di record, responsabili della conformità o addetti al settore legale e delle risorse umane. È anche possibile utilizzare Shell per eseguire una ricerca. Per ulteriori informazioni, vedere [Creazione di una ricerca eDiscovery sul posto](create-an-in-place-ediscovery-search-exchange-2013-help.md)


> [!NOTE]
> Nelle organizzazioni locali, è possibile utilizzare eDiscovery in locale per ricercare cassette postali sui server Cassette postali di Exchange 2013. Per ricercare cassette postali situate sui server Cassette postali di Exchange&nbsp;2010, utilizzare Ricerca in più cassette postali su un server di Exchange&nbsp;2010.<BR>In una distribuzione ibrida, costituita da un ambiente in cui alcune cassette postali si trovano nei server Cassette postali locale e altre si trovano nell'organizzazione basata su cloud, è possibile eseguire ricerche eDiscovery in locale nelle cassette postali basate su cloud utilizzando l'interfaccia di amministrazione di Exchange nell'organizzazione locale. Se si desidera copiare messaggi in una cassetta postale di individuazione, è necessario selezionare una cassetta postale di individuazione locale. I messaggi delle cassette postali basate su cloud restituiti nei risultati delle ricerche vengono copiati nella cassetta postale di individuazione specificata. Per ulteriori informazioni sulle distribuzioni ibride, vedere <A href="https://technet.microsoft.com/it-it/library/jj200581(v=exchg.150)">Distribuzioni ibride di Exchange Server</A>.



La procedura guidata **eDiscovery e Archiviazione sul posto** nell'interfaccia di amministrazione di Exchange consente di creare una ricerca eDiscovery in locale e anche di utilizzare Conservazione in locale per conservare i risultati di ricerca. Quando si crea una ricerca eDiscovery in locale, viene creato un oggetto di ricerca nella cassetta postale di sistema eDiscovery in locale. È possibile manipolare questo oggetto per avviare, interrompere, modificare e rimuovere la ricerca. Una volta creata la ricerca, è possibile scegliere di ottenere una stima dei risultati di ricerca comprendente le statistiche sulle parole chiave che consentono di determinare l'efficacia delle query. È anche possibile creare un'anteprima dinamica degli elementi restituiti nella ricerca, consentendo di visualizzare il contenuto dei messaggi, il numero di messaggi restituiti da ciascuna cassetta postale di origine e il numero totale di messaggi. È possibile utilizzare queste informazioni per ottimizzare ulteriormente la query se necessario.

Una volta soddisfatti dei risultati di ricerca, è possibile copiarli in una cassetta postale di individuazione. È anche possibile utilizzare l'interfaccia di amministrazione di Exchange o Outlook per esportare una cassetta postale di individuazione o parte del relativo contenuto in un file PST.

Quando si crea una ricerca eDiscovery in locale, è necessario specificare i seguenti parametri:

  - **Nome** Il nome di ricerca viene utilizzato per identificare la ricerca. Quando si copiano i risultati della ricerca in una cassetta postale di individuazione, viene creata una cartella nella cassetta postale di individuazione utilizzando il nome di ricerca e il timestamp per identificare in modo univoco i risultati della ricerca in una cassetta postale di individuazione.

  - **Cassette postali**   È possibile scegliere di ricerca tutte le cassette postali nell'organizzazione Exchange 2013 o Exchange Online o specificare le cassette postali per la ricerca. Un utente del principale e cassette postali di archiviazione sono incluse nella ricerca. Se inoltre si desidera utilizzare la stessa ricerca inserire gli elementi in attesa, è necessario specificare le cassette postali. È possibile specificare un gruppo di distribuzione per includere gli utenti delle cassette postali che sono membri del gruppo. L'appartenenza del gruppo viene calcolato una volta durante la creazione di ricerca e successivi all'appartenenza al gruppo non vengono automaticamente riflesse nella ricerca.
    
    In Exchange Online, è inoltre possibile specificare gruppi Office 365 come origine di contenuto in modo che la cassetta postale gruppo viene eseguita la ricerca (o messa in attesa). Quando si aggiunge un gruppo di Office 365 a una ricerca eDiscovery In locale, viene eseguita solo la cassetta postale di gruppo; non vengono effettuate le cassette postali dei membri del gruppo.

  - **Query di ricerca** È possibile includere tutto il contenuto della cassetta postale ricavato da determinate cassette postali oppure utilizzare una query di ricerca per restituire elementi che riguardano più da vicino il caso o l'indagine. In una query di ricerca, è possibile specificare i seguenti parametri:
    
      - **Parole chiave**   È possibile specificare parole chiave e frasi per cercare contenuto dei messaggi. È anche possibile utilizzare gli operatori logici **AND**, **OR** e **NOT**. Inoltre, Exchange 2013 supporta anche l'operatore **NEAR** che consente di effettuare una ricerca in base per una parola o frase posizionata vicino a un'altra parola o frase.
        
        Per cercare la corrispondenza esatta di una frase, è necessario racchiudere la frase fra virgolette. Ad esempio, la ricerca della frase "piano e competizione" restituirà i messaggi contenenti la corrispondenza esatta della frase, mentre se si specifica **piano E competizione** verranno restituiti i messaggi contenenti le parole **piano** e **competizione** presenti in qualsiasi punto del messaggio.
        
        Exchange 2013 supporta anche la sintassi KQL (Keyword Query Language) per le ricerche eDiscovery in locale.
        

        > [!NOTE]
        > La funzionalità eDiscovery in locale non supporta le espressioni regolari.

        
        È necessario scrivere in lettere maiuscole gli operatori logici quali **AND** e **OR** affinché vengano trattati come operatori invece che come parole chiave. Si consiglia di utilizzare le parentesi esplicite per tutte le query che combinano più operatori logici per evitare errori o interpretazioni non corrette. Ad esempio, per cercare i messaggi che contengono "ParolaA" o "ParolaB" AND "ParolaC" o "ParolaD", è necessario specificare **(ParolaA OR ParolaB) AND (ParolaC OR ParolaD)**.
    
      - **Date di inizio e di fine**   Per impostazione predefinita, eDiscovery in locale non limita le ricerche in base a un intervallo di date. Per cercare i messaggi inviati entro un intervallo di date specifico, è possibile restringere la ricerca specificando le date di inizio e di fine. Se non si specifica una data di fine, la ricerca restituirà i risultati più recenti ogni volta che viene riavviata.
    
      - **Mittenti e destinatari**Per restringere la ricerca, è possibile specificare i mittenti o i destinatari dei messaggi. È possibile utilizzare indirizzi di posta elettronica, nomi visualizzati o il nome di un dominio per cercare elementi inviati da o verso qualsiasi utente del dominio. Ad esempio, per trovare un messaggio di posta elettronica inviato da o a un utente qualsiasi alla Contoso, Ltd, specificare **@contoso.com** nel campo **Da** o **A/cc** nell'interfaccia di amministrazione di Exchange. È anche possibile specificare **@contoso.com** nel parametro *Senders* o *Recipients* in Shell.
    
      - **Tipi di messaggio** Per impostazione predefinita, vengono cercati tutti i tipi di messaggio. È possibile restringere la ricerca selezionando tipi di messaggio specifici, quali posta elettronica, contatti, documenti, journal, riunioni, note e contenuto Lync.

La schermata seguente mostra un esempio di query di ricerca in EAC.

![Configurazione query ricerca di eDiscovery](images/Dd353189.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "Configurazione query ricerca di eDiscovery")

Quando si utilizza eDiscovery in locale, tenere in considerazione anche quanto segue:

  - **Allegati** eDiscovery sul posto cerca gli allegati supportati da Ricerca di Exchange. Per ulteriori informazioni, vedere [Formati di file indicizzati da ricerca di Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md). Nelle distribuzioni locali, è possibile aggiungere il supporto per ulteriori tipi di file installando i filtri di ricerca (conosciuti come iFilter) per il tipo di file sui server Cassette postali.

  - **Elementi non ricercabili**   Gli elementi non ricercabili sono elementi della cassetta postale che non possono essere indicizzati da Ricerca di Exchange. Le cause che non possono essere indicizzate includono la mancanza di un filtro di ricerca installato per un file allegato, un errore di filtro e la presenza di messaggi crittografati. Affinché la ricerca eDiscovery abbia esito positivo, è possibile che l'organizzazione debba inserire alcuni elementi per la revisione. Quando si copiano i risultati della ricerca in una cassetta postale di individuazione o si esportano in un file PST, è possibile includere elementi non ricercabili. Per ulteriori informazioni, vedere [Elementi non ricercabili in Exchange eDiscovery](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

  - **Elementi crittografati**   Dal momento che i messaggi crittografati con S/MIME non vengono indicizzati da Ricerca di Exchange, eDiscovery sul posto non cerca questi messaggi. Se si decide di includere nei risultati della ricerca gli elementi non ricercabili, i messaggi crittografati con S/MIME vengono copiati nella cassetta postale di individuazione.

  - **Elementi protetti con IRM** I messaggi protetti con la funzionalità IRM (Information Rights Management) vengono indicizzati da Ricerca di Exchange e, pertanto, vengono inclusi nei risultati della ricerca se corrispondono ai parametri di query. I messaggi devono essere protetti utilizzando un cluster AD RMS (Rights Management Services) di Active Directory nella stessa foresta di Active Directory del server Cassette postali. Per ulteriori informazioni, vedere [Information Rights Management](information-rights-management-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Quando Ricerca di Exchange non riesce a eseguire l'indicizzazione di un messaggio protetto con IRM, a causa di un errore di decrittografia o perché IRM è disabilitato, il messaggio protetto non viene aggiunto all'elenco degli elementi con errore. Se si decide di includere nei risultati della ricerca gli elementi non ricercabili, i risultati potrebbero non includere i messaggi protetti con IRM che non è stato possibile decrittografare.<BR>Per includere i messaggi protetti con IRM in una ricerca, è possibile creare un'altra ricerca per includere i messaggi con allegati .rpmsg. È possibile utilizzare la stringa di query <CODE>attachment:rpmsg</CODE> per cercare tutti i messaggi protetti con IRM nelle cassette postali specificate, indipendentemente dalla riuscita o meno dell'indicizzazione. Ciò potrebbe causare la copia dei risultati della ricerca in scenari in cui una ricerca restituisce i messaggi che corrispondono ai criteri di ricerca, compresi i messaggi protetti con IRM non indicizzati correttamente. La ricerca non restituisce i messaggi protetti con IRM che non è stato possibile indicizzare.<BR>Durante l'esecuzione di una seconda ricerca di tutti i messaggi protetti con IRM, vengono inclusi anche i messaggi protetti con IRM correttamente indicizzati e restituiti dalla prima ricerca. Inoltre, è possibile che i messaggi protetti con IRM restituiti dalla seconda ricerca non corrispondano ai criteri di ricerca, quali parole chiave utilizzate per la prima ricerca.



  - **Deduplicazione** Quando si copiano i risultati della ricerca in una cassetta postale di individuazione, è possibile abilitare la *deduplicazione* dei risultati della ricerca per copiare solo un'istanza di un messaggio univoco nella cassetta postale di individuazione. La deduplicazione offre i seguenti vantaggi:
    
      - Requisiti di archiviazione inferiori e dimensioni minori della cassetta postale di individuazione a causa del numero ridotto di messaggi copiati.
    
      - Riduzione del carico di lavoro per i responsabili delle individuazioni, i consulenti legali o altre persone coinvolte nell'analisi dei risultati della ricerca.
    
      - Riduzione dei costi di individuazione, in base al numero di elementi duplicati esclusi dai risultati della ricerca.

Inizio pagina

## Stima, anteprima e copia dei risultati della ricerca

Una volta completata una ricerca eDiscovery sul posto, è possibile visualizzare le stime dei risultati della ricerca nel riquadro Dettagli dell'interfaccia di amministrazione di Exchange. La stima comprende il numero di elementi restituiti e le dimensioni totali di tali elementi. È anche possibile visualizzare le statistiche sulle parole chiave che restituiscono i dettagli sul numero di elementi restituiti per ciascuna parola chiave utilizzata nella query di ricerca. Queste informazioni sono utili nel determinare l'efficacia delle query. Se la query è troppo ampia, potrebbe restituire una serie di dati molto più grandi che potrebbero richiedere più risorse per l'esame e aumentare i costi per eDiscovery. Se la query è troppo ristretta, potrebbe ridurre in modo significativo il numero di record restituiti o non restituirne affatto. È possibile utilizzare le stime e le statistiche sulle parole chiave per ottimizzare la query affinché soddisfi i requisiti.


> [!NOTE]
> In Exchange 2013, le statistiche sulle parole chiave includono anche le statistiche per le proprietà che non sono parole chiave, quali date, tipi di messaggio e mittenti/destinatari specificati in una query di ricerca.



È anche possibile visualizzare un'anteprima dei risultati della ricerca per garantire ulteriormente che i messaggi restituiti contengano il contenuto che si sta cercando e ottimizzare la query, se necessario. Anteprima della ricerca eDiscovery visualizza il numero di messaggi restituiti da ciascuna cassetta postale ricercata e il numero totale di messaggi restituiti dalla ricerca. L'anteprima viene generata rapidamente senza che venga richiesto di copiare i messaggi in una cassetta postale di individuazione.

Una volta soddisfatti della quantità e qualità dei risultati della ricerca, è possibile copiarli in una cassetta postale di individuazione. Quando si copiano i messaggi, sono disponibili le seguenti opzioni:

  - **Includi elementi senza funzioni di ricerca** Per informazioni dettagliate sui tipi di elemento considerati non ricercabili, vedere le considerazioni sulla ricerca eDiscovery nella sezione precedente.

  - **Abilita deduplicazione** La deduplicazione riduce il set di dati includendo semplicemente una singola istanza di un record univoco se vengono trovate più istanze in una o più cassette postali ricercate.

  - **Abilita registrazione completa** Per impostazione predefinita, viene abilitata solo la registrazione base durante la copia degli elementi. È possibile selezionare la registrazione completa per includere informazioni su tutti i record restituiti dalla ricerca.

  - **Invia un messaggio di posta elettronica quando la copia è stata completata** Una ricerca eDiscovery sul posto potrebbe restituire un elevato numero di record. La copia dei messaggi restituiti a una cassetta postale di individuazione può richiedere parecchio tempo. Utilizzare questa opzione per ottenere una notifica tramite posta elettronica una volta completato il processo di copia. Per un accesso semplificato tramite Outlook Web App, la notifica include un collegamento alla posizione della cassetta postale di individuazione in cui vengono copiati i messaggi.

Per ulteriori informazioni, vedere [Copiare i risultati della ricerca eDiscovery in una cassetta postale di individuazione](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md).

Inizio pagina

## Esportare i risultati della ricerca in un file PST

Dopo aver copiato i risultati di una ricerca su una cassetta postale di individuazione, è possibile esportarli su file PST.

![Esportazione dei risultati della ricerca eDiscovery in un file PST](images/Dd298021.4ddca8af-1af5-4cb2-852c-e3a292099a58(EXCHG.150).gif "Esportazione dei risultati della ricerca eDiscovery in un file PST")

Dopo aver esportato i risultati di una ricerca in un file PST, l'utente o altri possono aprirli in Outlook per visualizzare o stampare i messaggi restituiti in tali risultati. Per ulteriori informazioni, vedere [Esportazione dei risultati della ricerca eDiscovery in un file PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md).

## Risultati di ricerca diversi

Poiché eDiscovery sul posto esegue ricerche su dati dinamici, è possibile che due ricerche delle stesse origini del contenuto, eseguite utilizzando la stessa query di ricerca, restituiscano risultati diversi. È inoltre possibile che i risultati della ricerca stimati siano diversi dai risultati effettivi copiati in una cassetta postale di individuazione. Questo può verificarsi anche quando si esegue nuovamente la stessa ricerca nell'arco di un breve periodo di tempo. Esistono diversi fattori in grado di influenzare la coerenza dei risultati della ricerca:

  - Indicizzazione continua della posta in arrivo, poiché la ricerca di Exchange effettua continuamente una ricerca per indicizzazione e indicizza i database delle cassette postali e la pipeline di trasporto dell'organizzazione.

  - Eliminazione di messaggi di posta elettronica da parte di utenti o processi automatizzati.

  - Importazione di grandi quantità di posta elettronica, con lunghi tempi di indicizzazione.

Se si ricevono risultati diversi per la stessa ricerca, si consiglia di adottare i seguenti provvedimenti: archiviare le cassette postali per conservarne il contenuto, eseguire le ricerche nelle ore di minor traffico e concedere il tempo necessario per l'indicizzazione dopo l'importazione di grandi quantità di messaggi di posta.

## Registrazione per le ricerche eDiscovery sul posto

Esistono due tipi di registrazione per le ricerche eDiscovery sul posto:

  - **Registrazione di base** La registrazione di base viene abilitata per impostazione predefinita per tutte le ricerche eDiscovery sul posto. Include informazioni sulla ricerca e sull'utente che l'ha eseguita. Le informazioni acquisite sulla registrazione di base vengono visualizzate nel corpo del messaggio di posta elettronica inviato alla cassetta postale in cui vengono archiviati i risultati della ricerca. Il messaggio si trova nella cartella creata per l'archiviazione dei risultati della ricerca.

  - **Registrazione completa**   La registrazione completa include informazioni relative a tutti i messaggi restituiti dalla ricerca. Tali informazioni sono contenute in un file con valori delimitati da virgole (.csv) allegato al messaggio di posta elettronica contenente le informazioni sulla registrazione di base. Il nome della ricerca viene utilizzato per denominare il file .csv. Queste informazioni potrebbero essere necessarie per la conformità o per il mantenimento dei record. Per abilitare la registrazione completa, è necessario selezionare l'opzione **Abilita registrazione completa** quando si copiano i risultati della ricerca in una cassetta postale di individuazione nell'interfaccia di amministrazione di Exchange. Se si utilizza Shell, specificare l'opzione di registrazione completa utilizzando il parametro *LogLevel*.


> [!NOTE]
> Quando si utilizza Shell per creare o modificare una ricerca eDiscovery sul posto, è anche possibile disabilitare la registrazione.



Oltre al registro della ricerca incluso durante la copia dei risultati della ricerca in una cassetta postale di individuazione, Exchange registra anche i cmdlet utilizzati dall'interfaccia di amministrazione di Exchange o da Shell per creare, modificare o rimuovere le ricerche eDiscovery sul posto. Queste informazioni vengono registrate nelle voci del registro di controllo admin. Per ulteriori informazioni, vedere [Registrazione controlli dell'amministratore](administrator-audit-logging-exchange-2013-help.md).

Inizio pagina

## eDiscovery e Archiviazione sul posto

Come parte delle richieste eDiscovery, all'utente potrebbe essere richiesto di conservare il contenuto della cassetta postale fino al termine di una causa legale. È necessario conservare anche i messaggi eliminati o alterati dall'utente di una cassetta postale o tutti i processi. In Exchange 2013, tale operazione viene eseguita utilizzando Archiviazione sul posto. Per ulteriori informazioni, vedere [Archiviazione sul posto e conservazione per controversia legale](in-place-hold-and-litigation-hold-exchange-2013-help.md).

In Exchange 2013, è possibile utilizzare la nuova procedura guidata **eDiscovery e archiviazione sul posto** per cercare gli elementi e conservarli per tutto il tempo in cui sono necessari per la ricerca eDiscovery o per soddisfare altri requisiti aziendali. Quando si utilizza la stessa ricerca sia per eDiscovery sia per Archiviazione sul posto, prestare attenzione a quanto segue:

  - Non è possibile utilizzare l'opzione per ricercare tutte le cassette postali. È necessario selezionare le cassette postali o i gruppi di distribuzione.

  - Non è possibile rimuovere una ricerca eDiscovery sul posto se la ricerca viene utilizzata anche per Archiviazione sul posto. Prima di tutto, è necessario disabilitare l'opzione Archiviazione sul posto in una ricerca e, poi, rimuovere la ricerca.

## Conservazione delle cassette postali per eDiscovery sul posto

Quando un dipendente lascia un'organizzazione, la relativa cassetta postale viene in genere disabilitata o rimossa. Una volta disabilitata una cassetta postale, questa viene disconnessa dall'account utente ma rimane nella cassetta postale per un determinato periodo di tempo, che per impostazione predefinita è di 30 giorni. Durante tale periodo di tempo, le cassette postali disconnesse non vengono elaborate dall'Assistente cartelle gestite e non sono soggette ai criteri di conservazione. Non è possibile eseguire ricerche nel contenuto di una cassetta postale disconnessa. Al termine del periodo di mantenimento configurato per il database delle cassette postali, la cassetta postale eliminata viene rimossa dal database delle cassette postali.


> [!IMPORTANT]
> In Exchange Online, eDiscovery sul posto è in grado di ricercare contenuti nelle cassette postali inattive. Le casette postali inattive sono cassette postali che vengono disposte in Archiviazione sul posto o in conservazione per controversia legale e poi rimosse. Le casette postali inattive vengono conservate fintanto che sono disposte in conservazione. Una cassetta postale inattiva viene eliminata in modo permanente se rimossa da Archiviazione sul posto oppure quando una conservazione per controversia legale viene disabilitata. Per ulteriori informazioni, vedere <A href="https://technet.microsoft.com/it-it/library/dn144876(v=exchg.150)">Gestione delle cassette postali inattive in Exchange Online</A>.



Nelle distribuzioni locali, qualora l'organizzazione richiedesse l'applicazione delle impostazioni di conservazione ai messaggi dei dipendenti che non fanno più parte dell'organizzazione o fosse necessario conservare la cassetta postale di un ex-dipendente per eseguire ricerche eDiscovery, al momento o in futuro, non è possibile disabilitare o rimuovere la cassetta postale. Per impedire l'accesso alla cassetta postale ed evitare che vi vengano recapitati messaggi, attenersi alla seguente procedura.

1.  Disabilitare l'account utente di Active Directory tramite **Utenti di Active Directory & Computer** o altri strumenti o script di Active Directory per il provisioning degli account. per impedire l'accesso alla cassetta postale tramite l'account utente associato.
    

    > [!IMPORTANT]
    > Gli utenti con l'autorizzazione di accesso completo per la cassetta postale saranno ancora in grado di accedere alla cassetta postale. Per evitare l'accesso ad altri utenti, è necessario rimuovere l'autorizzazione di accesso completo dalla cassetta postale. Per informazioni sul come rimuovere per un utente le autorizzazioni di accesso completo alla cassetta postale, vedere <A href="manage-permissions-for-recipients-exchange-online-help.md">Gestione delle autorizzazioni per i destinatari</A>.



2.  Impostare su un valore molto basso, ad esempio 1 KB, le dimensioni massime dei messaggi che possono essere inviati o ricevuti dall'utente della cassetta postale. Questo impedisce il recapito di nuovi messaggio in entrata e in uscita dalla cassetta postale. Per ulteriori informazioni, vedere [Configurazione dei limiti nelle dimensioni dei messaggi per una cassetta postale](configure-message-size-limits-for-a-mailbox-exchange-2013-help.md).

3.  Configurare restrizioni di recapito per la cassetta postale, affinché nessuno possa inviarvi messaggi. Per ulteriori informazioni, vedere [Configurazione di restrizioni di recapito messaggi per una cassetta postale](configure-message-delivery-restrictions-for-a-mailbox-exchange-2013-help.md).


> [!IMPORTANT]
> È necessario eseguire questa procedura insieme a qualsiasi altro processo di gestione degli account richiesto dall'organizzazione, ma senza disabilitare o rimuovere la cassetta postale o rimuovere l'account utente associato.



Quando si pianifica l'implementazione della conservazione delle cassette postali per la gestione della conservazione dei messaggi (MRM) o eDiscovery sul posto, è necessario tenere conto dell'avvicendamento dei dipendenti. La conservazione a lungo termine delle cassette postali degli ex-dipendenti richiede spazio di archiviazione aggiuntivo nei server Cassette postali e comporta un aumento delle dimensioni del database di Active Directory, perché è necessario mantenere l'account utente associato per lo stesso periodo di tempo. Potrebbe essere inoltre necessario modificare i processi di gestione e provisioning degli account dell'organizzazione.

Inizio pagina

## Limiti e criteri di limitazione di eDiscovery sul posto

In Exchange 2013 e Exchange Online, le risorse che la funzionalità eDiscovery sul posto può consumare su un server Cassette postali sono controllate tramite criteri di limitazione.

Il criterio di limitazione predefinito contiene i seguenti parametri di limitazione.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Descrizione</th>
<th>Valore predefinito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DiscoveryMaxConcurrency</p></td>
<td><p>Il numero massimo di ricerche eDiscovery sul posto che può essere eseguito contemporaneamente nella propria organizzazione.</p></td>
<td><p>2</p>

> [!NOTE]
> Una ricerca eDiscovery che viene avviata mentre sono in esecuzione altre due ricerche, non sarà accodata ma avrà esito negativo. Sarà necessario attendere che una delle due ricerche termini, prima di avviare una nuova ricerca.


</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxMailboxes</p></td>
<td><p>Numero massimo di cassette postali ricercabili con una singola ricerca eDiscovery sul posto.</p></td>
<td><p>Exchange Online: 10,0001</p>
<p>Exchange 2013: 5,000</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxStatsSearchMailboxes</p></td>
<td><p>Il numero massimo di cassette postali ricercabili in una singola ricerca eDiscovery sul posto che ancora consentono all'utente di consultare le statistiche sulle parole chiave.</p></td>
<td><p>100</p>

> [!NOTE]
> Dopo aver eseguito una stima sulla ricerca eDiscovery, è possibile visualizzare le statistiche sulle parole chiave. Queste statistiche sulle parole chiave consentono di consultare i dettagli sul numero di elementi restituiti per ciascuna parola chiave utilizzata nella query di ricerca. Se la ricerca include oltre 100 cassette postali di origine, viene visualizzato un errore quando si prova a consultare le statistiche sulle parole chiave.


</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxKeywords</p></td>
<td><p>Numero massimo di parole chiave specificabili in una singola ricerca eDiscovery sul posto.</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxSearchResultsPageSize</p></td>
<td><p>Numero massimo di elementi visualizzati su una singola pagina di anteprima della ricerca eDiscovery sul posto.</p></td>
<td><p>200</p></td>
</tr>
<tr class="even">
<td><p>DiscoverySearchTimeoutPeriod</p></td>
<td><p>Numero di minuti per cui sarà eseguita la ricerca ricerca eDiscovery sul posto prima che venga raggiunto il timeout.</p></td>
<td><p>10 minuti</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1 se si avvia una ricerca eDiscovery da eDiscovery Center in SharePoint Online in un'organizzazione Office 365, è possibile cercare un massimo di 1500 cassette postali in una singola ricerca.



In Exchange Server 2013 è possibile modificare i valori predefiniti di questi parametri per adattarli ai propri requisiti o per creare criteri di limitazione aggiuntivi e assegnarli agli utenti in possesso dell'autorizzazione di Gestione individuazione delegata. In Exchange Online i valori predefiniti di questi parametri di limitazione non possono essere modificati.

## Documentazione di eDiscovery sul posto

Nella seguente tabella sono riportati i collegamenti agli argomenti che offrono maggiori informazioni su eDiscovery sul posto e relative modalità di gestione.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Argomento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="assign-ediscovery-permissions-in-exchange-exchange-2013-help.md">Assegnare le autorizzazioni di eDiscovery di Exchange</a></p></td>
<td><p>Informazioni su come fornire a un utente l'accesso all'uso di eDiscovery sul posto in EAC per effettuare ricerche nelle cassette postali di Exchange. Aggiungendo un utente al gruppo di ruoli Gestione individuazione si consente all'utente di utilizzare il centro eDiscovery in SharePoint 2013 e SharePoint Online per effettuare ricerche nelle cassette postali di Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-discovery-mailbox-exchange-2013-help.md">Creazione di una cassetta postale di individuazione</a></p></td>
<td><p>Informazioni su come utilizzare Shell per creare cassette postali di individuazione e assegnare le autorizzazioni di accesso.</p></td>
</tr>
<tr class="odd">
<td><p><a href="create-an-in-place-ediscovery-search-exchange-2013-help.md">Creazione di una ricerca eDiscovery sul posto</a></p></td>
<td><p>Informazioni su come creare una ricerca eDiscovery sul posto e come stimare e visualizzare in anteprima i risultati della ricerca eDiscovery.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=506799">Proprietà del messaggio e gli operatori di ricerca per eDiscovery In locale</a></p></td>
<td><p>Scopi come è possibile cercare le proprietà del messaggio di posta elettronica utilizzando eDiscovery sul posto. In questo argomento vengono offerti esempi di sintassi per ogni proprietà, informazioni sugli operatori di ricerca come <strong>AND</strong> e <strong>OR</strong>, quindi informazioni su altre tecniche di query di ricerca come l'utilizzo del doppio punto interrogativo (&quot; &quot;) e i caratteri jolly.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/dn798915(v=exchg.150)">Limiti relativi alla ricerca di eDiscovery In locale in Exchange Online</a></p></td>
<td><p>Informazioni sui limiti eDiscovery sul posto in Exchange Online che consentono di preservare l'integrità e la qualità dei servizi eDiscovery per le organizzazioni di Office 365.</p></td>
</tr>
<tr class="even">
<td><p><a href="start-or-stop-an-in-place-ediscovery-search-exchange-2013-help.md">Avviare o interrompere una ricerca eDiscovery In locale</a></p></td>
<td><p>Informazioni su come avviare, arrestare e riavviare le ricerche eDiscovery.</p></td>
</tr>
<tr class="odd">
<td><p><a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">Modificare una ricerca eDiscovery In locale</a></p></td>
<td><p>Informazioni su come modificare una ricerca eDiscovery esistente.</p></td>
</tr>
<tr class="even">
<td><p><a href="copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md">Copiare i risultati della ricerca eDiscovery in una cassetta postale di individuazione</a></p></td>
<td><p>Informazioni su come copiare i risultati di una ricerca eDiscovery in una cassetta postale di individuazione.</p></td>
</tr>
<tr class="odd">
<td><p><a href="export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md">Esportazione dei risultati della ricerca eDiscovery in un file PST</a></p></td>
<td><p>Informazioni su come esportare i risultati di una ricerca eDiscovery in un file PST.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md">Creazione di un ambito di gestione personalizzato per le ricerche di eDiscovery sul posto</a></p></td>
<td><p>Come utilizzare gli ambiti di gestione personalizzata per limitare le cassette postali che un responsabile dell'individuazione può ricercare.</p></td>
</tr>
<tr class="odd">
<td><p><a href="remove-an-in-place-ediscovery-search-exchange-2013-help.md">Rimuovere una ricerca eDiscovery In locale</a></p></td>
<td><p>Informazioni su come eliminare una ricerca eDiscovery.</p></td>
</tr>
<tr class="even">
<td><p><a href="search-for-and-delete-messages-admin-help-exchange-2013-help.md">Ricerca ed eliminazione di messaggi - Guida di Amministrazione</a></p></td>
<td><p>Informazioni su come usare il cmdlet <strong>Search-Mailbox</strong> per cercare ed eliminare i messaggi di posta elettronica.</p></td>
</tr>
<tr class="odd">
<td><p><a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">Ridurre le dimensioni di una cassetta postale di individuazione in Exchange</a></p></td>
<td><p>Usa questa procedura per ridurre le dimensioni di una cassetta postale di individuazione che supera i 50 GB.</p></td>
</tr>
<tr class="even">
<td><p><a href="delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md">Elimina e ricrea la cassetta postale di individuazione predefinita in Exchange</a></p></td>
<td><p>Scopri come eliminare la cassetta postale di individuazione predefinita, ricrearla, quindi riassegnarle autorizzazioni. Usa questa procedura se la cassetta postale ha superato la soglia dei 50 GB e non hai bisogno dei risultati della ricerca.</p></td>
</tr>
<tr class="odd">
<td><p><a href="re-create-the-discovery-system-mailbox-exchange-2013-help.md">Re-create the Discovery system mailbox</a></p></td>
<td><p>Informazioni su come ricreare la cassetta postale di sistema di individuazione. Questa attività si applica solo alle organizzazioni Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md">Utilizzo dell'autenticazione OAuth per supportare eDiscovery in un'implementazione ibrida di Exchange</a></p></td>
<td><p>Informazioni sugli scenari di eDiscovery in un ambiente ibrido Exchange che richiede la configurazione dell'autenticazione OAuth.</p></td>
</tr>
<tr class="odd">
<td><p><a href="configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md">Configurare Exchange per SharePoint eDiscovery Center</a></p></td>
<td><p>Informazioni su come configurare Exchange 2013 per poter utilizzare il centro eDiscovery in SharePoint 2013 per effettuare ricerche nelle cassette postali di Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Elementi non ricercabili in Exchange eDiscovery</a></p></td>
<td><p>Informazioni sugli elementi delle cassette postali che non possono essere indicizzati da Ricerca Exchange e vengono restituiti nei risultati della ricerca di eDiscovery come elementi non ricercabili.</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su eDiscovery in Office 365, Exchange 2013, SharePoint 2013 e Lync 2013, vedere [domande frequenti su eDiscovery](https://go.microsoft.com/fwlink/p/?linkid=386633).

Inizio pagina


---
title: 'Controllo di accesso basato sui ruoli: Exchange 2013 Help'
TOCTitle: Controllo di accesso basato sui ruoli
ms:assetid: fd268867-2ae5-441b-8103-7a7583eb2bbe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298183(v=EXCHG.150)
ms:contentKeyID: 50482093
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Controllo di accesso basato sui ruoli

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2018-01-31_

*Role Based Access Control* (RBAC) è il nuovo modello di autorizzazioni utilizzato in Microsoft Exchange Server 2013. Con RBAC non è necessario modificare e gestire gli elenchi di controllo di accesso come in Exchange Server 2007. Gli elenchi di controllo di accesso ponevano diverse sfide in Exchange 2007, ad esempio la modifica degli elenchi senza provocare conseguenze impreviste, la conservazione delle modifiche agli elenchi dopo un aggiornamento e la risoluzione dei problemi che si verificavano a causa dell'utilizzo degli elenchi di controllo di accesso con modalità non standard.

RBAC consente di controllare, a livello ampio o granulare, le operazioni consentite agli amministratori e agli utenti finali. Consente inoltre di allineare con maggiore precisione i ruoli assegnati a utenti e amministratori con i ruoli effettivi che svolgono nell'organizzazione. In Exchange 2007, il modello delle autorizzazioni del server si applica solo agli amministratori che gestiscono l'infrastruttura di Exchange 2007. In Exchange 2013, RBAC ora controlla sia le attività amministrative che possono essere eseguite sia i limiti dell'utente per la gestione delle proprie cassette postali e gruppi di distribuzione.

RBAC include due modi principali con cui vengono assegnate le autorizzazioni agli utenti dell'organizzazione, a seconda del fatto che l'utente sia un amministratore, un utente esperto o un utente finale: i gruppi di ruoli di gestione e i criteri di assegnazione del ruolo di gestione. Ogni metodo associa gli utenti alle autorizzazioni di cui necessitano per eseguire le attività. È disponibile anche un terzo metodo avanzato, l'assegnazione diretta del ruolo all'utente. Nelle seguenti sezioni di questo argomento viene descritto RBAC e vengono forniti esempi di utilizzo.


> [!NOTE]
> Questo argomento è incentrato sulla funzionalità RBAC avanzata. Se si desidera gestire le autorizzazioni di base di Exchange 2013, quale l'utilizzo dell'interfaccia di amministrazione di Exchange (EAC) per aggiungere membri ai gruppi di ruoli oppure per rimuoverli da tali gruppi, per creare e modificare gruppi di ruoli oppure per creare e modificare i criteri di assegnazione dei ruoli, vedere <A href="permissions-exchange-2013-help.md">Autorizzazioni</A>.



**Sommario**

Management role groups

Management role assignment policies

Direct user role assignment

Summary and examples

For more information

## Gruppi di ruoli di gestione

I *gruppi di ruoli di gestione* associano i ruoli di gestione a un gruppo di amministratori o utenti esperti. Gli amministratori gestiscono una configurazione del destinatario o dell'organizzazione di Exchange su vasta scala. Gli utenti esperti gestiscono le funzionalità specifiche di Exchange, ad esempio la conformità. In alternativa, possono disporre di capacità di gestione limitate, come nel caso dei membri dell'assistenza, ma non ottengono diritti amministrativi estesi. I gruppi di ruoli in genere associano ruoli di gestione amministrativi che consentono agli amministratori e agli utenti esperti di gestire la configurazione dell'organizzazione e i destinatari. Ad esempio, la possibilità per gli amministratori di gestire i destinatari o di utilizzare le funzionalità di individuazione delle cassette postali viene controllata per mezzo dei gruppi di ruoli.

L'aggiunta o la rimozione degli utenti nei gruppi di ruoli è il metodo utilizzato più spesso per assegnare autorizzazioni agli amministratori o agli utenti esperti. Per ulteriori informazioni, vedere [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md).

I gruppi di ruoli sono costituiti dai seguenti componenti, che definiscono le operazioni consentite ad amministratori e utenti esperti:

  - **Gruppo di ruoli di gestione**   Il *gruppo di ruoli di gestione* è uno speciale gruppo di protezione universale contenente cassette postali, utenti, gruppi di protezione universali e altri gruppi di ruoli che sono membri del gruppo di ruoli. Qui è possibile aggiungere e rimuovere membri e individuare i ruoli di gestione assegnati. La combinazione di tutti i ruoli di un gruppo consente di definire ogni elemento gestibile dagli utenti aggiunti a un gruppo nell'organizzazione di Exchange.

  - **Ruolo di gestione**   Un *ruolo di gestione* è un contenitore per un raggruppamento di voci del ruolo di gestione. I ruoli vengono utilizzati per definire le specifiche attività che possono essere eseguite dai membri di un gruppo assegnato al ruolo. Una *voce del ruolo di gestione* è un cmdlet, uno script o una determinata autorizzazione che consente di eseguire ogni specifica attività di un ruolo. Per ulteriori informazioni, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

  - **Assegnazione del ruolo di gestione**   Un'*assegnazione del ruolo di gestione* consente di collegare un ruolo a un gruppo di ruoli. L'assegnazione di un ruolo a un gruppo di ruoli consente ai membri del gruppo di utilizzare i cmdlet e i parametri definiti nel ruolo. Le assegnazioni di ruolo possono utilizzare gli ambiti di gestione per controllare dove può essere utilizzata l'assegnazione. Per ulteriori informazioni, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

  - **Ambito del ruolo di gestione**   Un *ambito del ruolo di gestione* è l'ambito di influenza o di impatto di un'assegnazione di ruolo. Quando un ruolo viene assegnato a un gruppo con un ambito, l'ambito di gestione indica in modo specifico quali oggetti possono essere gestiti dall'assegnazione. L'assegnazione e il suo ambito vengono quindi forniti ai membri del gruppo di ruoli e limitano gli elementi che i membri possono gestire. Un ambito può essere costituito da un elenco di server o di database, unità organizzative o filtri degli oggetti server, di database o destinatari. Per ulteriori informazioni, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

Con l'aggiunta a un gruppo di ruoli, l'utente riceve tutti i ruoli assegnati al gruppo di ruoli. Se sono applicati ambiti alle assegnazioni di ruolo tra il gruppo di ruoli e i ruoli, tali ambiti controllano la configurazione del server o i destinatari che l'utente può gestire.

Se si desidera modificare i ruoli assegnati ai gruppi di ruoli, è necessario modificare le assegnazioni di ruolo che collegano i gruppi di ruoli ai ruoli. Ad ogni modo, a meno che le assegnazioni predefinite di Exchange 2013 non siano adatte alle proprie esigenze, non è necessario modificare tali assegnazioni. Per ulteriori informazioni, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Per ulteriori informazioni sui gruppi di ruoli, vedere [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md).

## Criteri di assegnazione del ruolo di gestione

I criteri di assegnazione del ruolo di gestione consentono di associare i ruoli di gestione degli utenti finali agli utenti. I criteri di assegnazione di ruolo sono costituiti da ruoli che controllano le operazioni consentite a un utente sulla sua cassetta postale o sui suoi gruppi di distribuzione. Questi ruoli non consentono la gestione delle funzionalità che non sono direttamente associate all'utente. Quando si crea un criterio di assegnazione del ruolo, è necessario definire tutte le operazioni che un utente può eseguire sulla sua cassetta postale. Ad esempio, un criterio di assegnazione di ruolo può consentire a un utente di impostare il nome visualizzato, predisporre il sistema di caselle vocali e configurare le regole di Posta in arrivo. Un altro criterio di assegnazione di ruolo potrebbe consentire a un utente di cambiare l'indirizzo, utilizzare l'invio di SMS e configurare gruppi di distribuzioni. A ciascun utente con una cassetta postale Exchange 2013, inclusi gli amministratori, viene dato un criterio di assegnazione dei ruoli per impostazione predefinita. Si può decidere quale criterio di assegnazione dei ruoli venga assegnato per impostazione predefinita, scegliere cosa un criterio di assegnazione dei ruoli predefinito deve includere, sovrascrivere l'impostazione predefinita di alcune cassette postali o non assegnare nessun criterio di assegnazione dei ruoli.

L'assegnazione di un utente a un criterio di assegnazione è il metodo utilizzato più spesso per gestire le autorizzazioni che consentono agli utenti di gestire la propria cassetta postale e le opzioni del gruppo di distribuzione. Per ulteriori informazioni, vedere [Informazioni sui criteri di assegnazione di ruolo di gestione](understanding-management-role-assignment-policies-exchange-2013-help.md).

I criteri di assegnazione di ruolo sono costituiti dai seguenti componenti, che stabiliscono le operazioni consentite agli utenti sulle loro cassette postali. Alcuni degli stessi componenti sono applicabili anche ai gruppi di ruoli. Se vengono utilizzati con i criteri di assegnazione di ruolo, questi componenti si limitano a consentire agli utenti di gestire la propria cassetta postale:

  - **Criterio di assegnazione del ruolo di gestione**   Il *criterio di assegnazione del ruolo di gestione* è uno speciale oggetto di Exchange 2013. Gli utenti vengono associati al criterio di assegnazione di ruolo quando vengono create le loro cassette postali o se si modifica il criterio di assegnazione di ruolo su una cassetta postale. È anche l'elemento a cui si assegnano anche i ruoli di gestione degli utenti finali. La combinazione di tutti i ruoli per un criterio di assegnazione di ruolo consente di definire gli elementi che l'utente può gestire nella sua cassetta postale o nei gruppi di distribuzione.

  - **Ruolo di gestione**   Un *ruolo di gestione* è un contenitore per un raggruppamento di voci del ruolo di gestione. I ruoli vengono utilizzati per definire le specifiche attività che un utente può eseguire sulla sua cassetta postale o sui gruppi di distribuzione. Una *voce del ruolo di gestione* è un cmdlet, uno script o una determinata autorizzazione che consente di eseguire ogni specifica attività di un ruolo di gestione. È possibile utilizzare solo i ruoli degli utenti finali con i criteri di assegnazione di ruolo. Per ulteriori informazioni, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

  - **Assegnazione del ruolo di gestione**   Un'*assegnazione del ruolo di gestione* indica il collegamento tra un ruolo e un criterio di assegnazione di ruolo. L'assegnazione di un ruolo a un criterio di assegnazione di ruolo consente di utilizzare i cmdlet e i parametri definiti nel ruolo. Quando si crea un'assegnazione di ruolo tra un criterio di assegnazione di ruolo e un ruolo, non è possibile specificare alcun ambito. L'ambito applicato dall'assegnazione è `Self` o `MyGAL`. L'ambito tutte le assegnazioni di ruolo è la cassetta postale dell'utente o i gruppi di distribuzione. Per ulteriori informazioni, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Se si desidera modificare i ruoli assegnati ai criteri di assegnazione di ruolo, è necessario modificare le assegnazioni di ruolo che collegano i criteri di assegnazione di ruolo ai ruoli. Ad ogni modo, a meno che le assegnazioni predefinite di Exchange 2013 non siano adatte alle proprie esigenze, non è necessario modificare tali assegnazioni. Per ulteriori informazioni, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Per ulteriori informazioni, vedere [Informazioni sui criteri di assegnazione di ruolo di gestione](understanding-management-role-assignment-policies-exchange-2013-help.md).

## Assegnazione diretta del ruolo dell'utente

L'*assegnazione diretta del ruolo* è un metodo avanzato per l'assegnazione diretta dei ruoli di gestione a un utente o a un gruppo di protezione universale, senza l'uso di un gruppo di ruoli o di un criterio di assegnazione di ruolo. Le assegnazioni dirette dei ruoli possono essere utilizzate per fornire un insieme granulare di autorizzazioni solo a un utente specifico e non agli altri. Tuttavia, l'uso delle assegnazioni dirette dei ruoli può aumentare notevolmente la complessità del modello delle autorizzazioni. Se un utente cambia lavoro o lascia l'azienda, è necessario rimuovere manualmente le assegnazioni e aggiungerle al nuovo dipendente. Si consiglia di utilizzare i gruppi di ruoli per assegnare le autorizzazioni agli amministratori e agli utenti esperti e i criteri di assegnazione di ruolo per assegnare le autorizzazioni agli utenti.

Per ulteriori informazioni sull'assegnazione diretta del ruolo, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

## Riepilogo ed esempi

Nella seguente figura sono mostrati i componenti di RBAC e le loro modalità di interazione:

  - Gruppi di ruoli:
    
      - Uno o più amministratori possono essere membri di un gruppo di ruoli. Possono inoltre essere membri di più gruppi di ruoli.
    
      - Al gruppo di ruolo sono assegnate una o più assegnazioni di ruolo. Queste collegano il gruppo di ruoli a uno o più ruoli di amministrazione che definiscono le attività che possono essere eseguite.
    
      - Le assegnazioni di ruolo possono contenere ambiti di gestione che definiscono la posizione in cui gli utenti del gruppo di ruoli possono eseguire le azioni. Gli ambiti determinano la posizione in cui gli utenti del gruppo di ruoli possono modificare la configurazione.

  - Criteri di assegnazione di ruolo:
    
      - Uno o più utenti possono essere associati a un criterio di assegnazione di ruolo.
    
      - Al criterio di assegnazione di ruolo sono assegnate una o più assegnazioni di ruolo. Queste collegano il criterio di assegnazione di ruolo a uno o più ruoli degli utenti finali. I ruoli degli utenti finali definiscono gli elementi che l'utente può configurare sulla sua cassetta postale.
    
      - Le assegnazioni di ruolo tra i criteri di assegnazione di ruolo e i ruoli presentano ambiti predefiniti che limitano l'ambito delle assegnazioni alla cassetta postale dell'utente o ai gruppi di distribuzione.

  - Assegnazione diretta del ruolo (metodo avanzato):
    
      - Un'assegnazione di ruolo può essere creata direttamente tra un utente o un gruppo di protezione universale e uno o più ruoli. Il ruolo definisce le attività che l'utente o il gruppo di protezione universale può eseguire.
    
      - Le assegnazioni di ruolo possono contenere ambiti di gestione che definiscono la posizione in cui l'utente o il gruppo di protezione universale può eseguire le azioni. Gli ambiti determinano la posizione in cui l'utente o il gruppo di protezione universale può modificare la configurazione.

**Informazioni generali su RBAC**

![Relazioni tra componenti RBAC](images/Dd298183.1dee60cc-1d58-4d36-b34e-639f091e7a56(EXCHG.150).jpg "Relazioni tra componenti RBAC")

Come mostrato nella figura precedente, molti componenti di RBAC sono in relazione tra loro. È l'integrazione di ciascun componente a definire le autorizzazioni applicate a ciascun amministratore o utente. Nei seguenti esempi vengono fornite alcune informazioni aggiuntive sull'utilizzo dei gruppi di ruoli e dei criteri di assegnazione di ruolo in un'organizzazione.

## Jane, l'amministratore

Jane è un amministratore della società di medie dimensioni Contoso. È responsabile della gestione dei destinatari della società nella sede di Vancouver. Quando è stato creato il modello di autorizzazioni per Contoso, Jane è stata configurata come membro del gruppo di ruoli personalizzato Gestione destinatari - Vancouver. Il gruppo di ruoli Gestione destinatari - Vancouver è quello che rispecchia più fedelmente i suoi compiti, che comprendono la creazione e la rimozione di destinatari, cassette postali e contatti, la gestione delle appartenenze ai gruppi di distribuzione e delle proprietà delle cassette postali, e altre attività simili.

Oltre al gruppo di ruoli personalizzato Gestione destinatari - Vancouver, Jane necessita anche di un criterio di assegnazione di ruolo per gestire le impostazioni di configurazione della propria cassetta postale. Gli amministratori dell'organizzazione hanno stabilito che tutti gli utenti, fatta eccezione per la direzione aziendale, ricevono le stesse autorizzazioni per la gestione delle proprie cassette postali. Possono configurare la propria segreteria telefonica, impostare criteri di conservazione e cambiare le informazioni relative all'indirizzo. Il criterio di assegnazione di ruolo predefinito fornito con Exchange 2013 riflette tali requisiti.


> [!NOTE]
> Essendo membro del gruppo di ruoli personalizzato Gestione destinatari - Vancouver, Jane dovrebbe già disporre delle autorizzazioni di gestione della sua cassetta postale. È vero, ma il gruppo di ruoli non le assegna tutte le autorizzazioni necessarie per gestire tutti gli aspetti della sua cassetta postale. Le autorizzazioni necessarie per gestire la segreteria telefonica e le impostazioni dei criteri di conservazione non sono incluse nel suo gruppo di ruoli. Le sono assegnate solo quelle fornite dal criterio di assegnazione di ruolo predefinito.



Per ottenere questo risultato, è necessario prendere in considerazione il gruppo di ruoli, che fornisce le autorizzazioni amministrative di Jane per i destinatari nella sede di Vancouver:

1.  È stato creato un gruppo di ruoli personalizzato denominato Gestione destinatari - Vancouver. In fase di creazione, sono state eseguite le seguenti operazioni:
    
    1.  Al gruppo di ruoli sono stati assegnati tutti gli stessi ruoli di gestione assegnati anche al gruppo di ruoli predefinito Gestione destinatari. In questo modo gli utenti aggiunti al gruppo di ruoli personalizzato Gestione destinatari - Vancouver ottengono le stesse autorizzazioni degli utenti aggiunti al gruppo di ruoli Gestione destinatari. Tuttavia, i seguenti passaggi limitano le posizioni in cui è possibile utilizzare tali autorizzazioni.
    
    2.  È stato creato l'ambito di gestione personalizzato Vancouver Recipients, che corrisponde esclusivamente ai destinatari della sede di Vancouver. L'operazione è stata eseguita creando un ambito di filtro in base alla città dell'utente o ad altre informazioni univoche.
    
    3.  Il gruppo di ruoli è stato creato con l'ambito di gestione personalizzato Vancouver Recipients. Significa che, nonostante gli amministratori aggiunto al gruppo di ruoli personalizzato Gestione destinatari - Vancouver dispongano delle autorizzazioni di gestione dei destinatari complete, tali autorizzazioni possono essere utilizzate solo sui destinatari con sede a Vancouver.
    
    Per ulteriori informazioni sulla creazione dei gruppi di ruoli personalizzati, vedere [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

2.  Jane viene quindi aggiunta come membro del gruppo di ruoli personalizzato Gestione destinatari - Vancouver.
    
    Per ulteriori informazioni sull'aggiunta di membri a un gruppo di ruoli, vedere [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).

Per consentire a Jane di gestire le impostazioni della sua cassetta postale, è necessario configurare un criterio di assegnazione di ruolo con le autorizzazioni necessarie. Il criterio di assegnazione di ruolo predefinito consente di fornire agli utenti le autorizzazioni necessarie per la configurazione della propria cassetta postale. Tutti i ruoli dell'utente finale vengono rimossi dal criterio di assegnazione di ruolo predefinito, fatta eccezione per: `MyBaseOptions`, `MyContactInformation`, `MyVoicemail` e `MyRetentionPolicies`. `MyBaseOptions` è incluso in quanto ruolo di gestione che fornisce le funzionalità utente di base in Microsoft Outlook Web App, ad esempio le regole di Posta in arrivo, la configurazione del calendario e altre attività.

Non è necessario eseguire altre operazioni, perché a Jane è già assegnato il criterio di assegnazione di ruolo predefinito. In pratica, le modifiche apportate al criterio di assegnazione di ruolo vengono immediatamente applicate alla sua cassetta postale e a tutte le altre cassette postali assegnate al criterio di assegnazione di ruolo predefinito.

Per ulteriori informazioni sulla personalizzazione del critero di assegnazione di ruolo predefinito, vedere [Gestire i criteri di assegnazione dei ruoli](manage-role-assignment-policies-exchange-2013-help.md).

## Joe, l'esperto

Joe lavora per Contoso, la stessa società per cui lavora Jane. È responsabile dell'esibizione, dell'impostazione dei criteri di conservazione e della configurazione delle regole di trasporto e dell'inserimento nel journal per l'intera organizzazione. Come nel caso di Jane, quando è stato creato il modello di autorizzazioni per Contoso Joe è stato aggiunto ai gruppi di ruoli corrispondenti alle sue mansioni. Il gruppo di ruoli Gestione record consente a Joe di configurare i criteri di conservazione, l'inserimento nel journal e le regole di trasporto. Il gruppo di ruoli Gestione individuazione consente di eseguire le ricerche nelle cassette postali.

Come nel caso di Jane, Joe necessita delle autorizzazioni per gestire la sua cassetta postale. Gli sono state assegnate le stesse autorizzazioni di Jane: può configurare la segreteria telefonica, i criteri di conservazione e cambiare le informazioni relative all'indirizzo.

Per assegnare a Joe le autorizzazioni per svolgere i suoi incarichi, Joe viene aggiunto ai gruppi di ruoli Gestione record e Gestione individuazione. I gruppi di ruoli non devono essere modificati, perché mettono già a disposizione le autorizzazioni necessarie e gli ambiti di gestione applicati ad essi comprendono l'intera organizzazione.

Per ulteriori informazioni sull'aggiunta di un utente di un gruppo di ruoli, vedere [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).

Alla cassetta postale di Joe è assegnato lo stesso criterio di assegnazione di ruolo predefinito applicato alla cassetta postale di Jane. In questo modo egli ottiene tutte le autorizzazioni necessarie per gestire le caratteristiche della sua cassetta postale che è autorizzato a gestire.

## Isabel, il vicepresidente

Isabel è il vicepresidente marketing di Contoso. Isabel, che fa parte della direzione di Contoso, riceve un numero di autorizzazioni superiore a quello dell'utente medio. Sono incluse le autorizzazioni per gestire la sua cassetta postale, con una sola eccezione: a Isabel non è permesso gestire i suoi criteri di conservazione per ragioni legate alla conformità alle leggi. Isabel può configurare la sua segreteria telefonica, modificare le informazioni dei contatti, le informazioni del profilo, creare e gestire gruppi di distribuzione e unirsi o lasciare gruppi di distribuzione esistenti di proprietà di altre persone.

Pertanto, Isabel riceve autorizzazioni diverse per la propria cassetta postale. La maggior parte degli utenti di Contoso è assegnata al criterio di assegnazione di ruolo predefinito. La direzione, invece, viene assegnata al criterio di assegnazione di ruolo Senior Leadership. Per creare il criterio di assegnazione di ruolo personalizzato vengono eseguite le seguenti operazioni:

1.  Viene creato un criterio di assegnazione di ruolo personalizzato denominato Senior Leadership. Al criterio di assegnazione di ruolo sono assegnati i ruoli `MyBaseOptions`, `MyContactInformation`, `MyVoicemail`, `MyProfileInformation`, `MyDistributionGroupMembership` e ` MyDistributionGroups`. `MyBaseOptions` è incluso in quanto questo ruolo di gestione fornisce le funzionalità utente di base in Outlook Web App, ad esempio le regole di Posta in arrivo, la configurazione del calendario e altre attività.

2.  Isabel viene quindi assegnata manualmente al criterio di assegnazione di ruolo Senior Leadership.

La cassetta postale di Isabel ora dispone delle autorizzazioni fornite dal criterio di assegnazione di ruolo Senior Leadership. Le modifiche apportate a questo criterio di assegnazione di ruolo vengono applicate automaticamente alla sua cassetta postale e a tutte le altre cassette postali assegnate allo stesso criterio di assegnazione di ruolo.

## Ulteriori informazioni

[Gestire i criteri di assegnazione dei ruoli](manage-role-assignment-policies-exchange-2013-help.md)

[Modificare il criterio di assegnazione di una cassetta postale](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)


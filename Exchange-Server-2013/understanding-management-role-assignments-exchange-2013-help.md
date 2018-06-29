---
title: 'Informazioni sulle assegnazioni dei ruoli di gestione: Exchange 2013 Help'
TOCTitle: Informazioni sulle assegnazioni dei ruoli di gestione
ms:assetid: 1dc33dd6-52fb-4852-a5ce-027bc73e1d8f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335131(v=EXCHG.150)
ms:contentKeyID: 50480123
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Informazioni sulle assegnazioni dei ruoli di gestione

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-04_

Un'*assegnazione del ruolo di gestione*, che fa parte del modello di autorizzazioni Controllo di accesso basato sui ruoli (RBAC) in Microsoft Exchange Server 2013, indica il collegamento tra un ruolo di gestione e un assegnatario di ruolo. Un *assegnatario di ruolo* indica un gruppo di ruolo, un criterio di assegnazione dei ruoli, un utente o un gruppo di protezione universale. Un ruolo deve essere associato a un assegnatario per essere applicato. Per ulteriori informazioni su RBAC, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).


> [!NOTE]
> Questo argomento è incentrato sulla funzionalità RBAC avanzata. Se si desidera gestire le autorizzazioni di base di Exchange 2013, quale l'utilizzo dell'interfaccia di amministrazione di Exchange (EAC) per aggiungere membri ai gruppi di ruoli oppure per rimuoverli da tali gruppi, per creare e modificare gruppi di ruoli oppure per creare e modificare i criteri di assegnazione dei ruoli, vedere <A href="permissions-exchange-2013-help.md">Autorizzazioni</A>.



In questo argomento viene descritta l'assegnazione dei ruoli a gruppi di ruolo e a criteri di assegnazione dei ruoli e l'assegnazione diretta dei ruoli a utenti e a gruppi di protezione universale. Non viene descritta l'assegnazione dei gruppi di ruolo o dei criteri di assegnazione dei ruoli agli utenti. Per ulteriori informazioni sui gruppi di ruolo e i criteri di assegnazione dei ruoli, che costituiscono il metodo consigliato per assegnare le autorizzazioni agli utenti, vedere i seguenti argomenti:

  - [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md)

  - [Informazioni sui criteri di assegnazione di ruolo di gestione](understanding-management-role-assignment-policies-exchange-2013-help.md)

È possibile creare i seguenti tipi di assegnazioni di ruolo, che vengono descritti in dettaglio più avanti in questo argomento:

  - Regular and delegating role assignments

  - Exclusive role assignments

## Assegnazioni di ruoli di gestione

Quando le assegnazioni di ruolo vengono modificate, le modifiche apportate riguarderanno probabilmente i gruppi di ruolo e i criteri di assegnazione dei ruoli. Aggiungendo, rimuovendo o modificando le assegnazioni di ruolo di questi assegnatari, è possibile controllare le autorizzazioni fornite agli amministratori e agli utenti, in pratica attivando o disattivando la gestione delle relative funzionalità.

È inoltre possibile assegnare i ruoli direttamente agli utenti o ai gruppi di protezione universale. Si tratta di un'attività più avanzata che consente di definire più precisamente le autorizzazioni fornite agli utenti. Sebbene fornisca flessibilità, aumenta anche la complessità del modello di autorizzazioni. Ad esempio, se l'utente modifica i processi, potrebbe essere necessario assegnare di nuovo manualmente a un altro utente i ruoli associati a tale utente. Per questo motivo si consiglia di utilizzare i gruppi di ruolo e i criteri di assegnazione dei ruoli per fornire le autorizzazioni agli utenti. È possibile assegnare i ruoli a un gruppo di ruolo o a un criterio di assegnazione dei ruoli, quindi aggiungere o rimuovere semplicemente i membri del gruppo di ruolo o modificare i criteri di assegnazione dei ruoli in base alle esigenze.

È possibile aggiungere, rimuovere e abilitare le assegnazioni di ruolo, modificare l'ambito di gestione per un'assegnazione di ruolo esistente e spostare le assegnazioni di ruolo ad altri assegnatari di ruolo. Il processo di assegnazione dei ruoli a gruppi di ruolo, criteri di assegnazione dei ruoli, utenti e gruppi di protezione universale è in gran parte lo stesso per ogni assegnatario di ruolo. Le uniche eccezioni sono:

  - Ai criteri di assegnazione dei ruoli possono essere assegnati solo ruoli di gestione di utenti finali.

  - Ai criteri di assegnazione dei ruoli non possono essere associate assegnazioni del ruolo di delega.

  - Durante la creazione di un'assegnazione di ruolo ai criteri di assegnazione dei ruoli, non è possibile specificare un ambito di gestione.

Per ulteriori informazioni sulla gestione delle assegnazioni di ruolo, vedere i seguenti argomenti:

  - Gruppi di ruolo:
    
      - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - Criteri di assegnazione del ruolo:
    
      - [Gestire i criteri di assegnazione dei ruoli](manage-role-assignment-policies-exchange-2013-help.md)
    
      - [Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md)

  - Utenti e gruppi di protezione universale:
    
      - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
    
      - [Rimozione di un ruolo da un utente o gruppo di protezione universale](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)
    
      - [Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md)
    
      - [Modificare un ambito di ruolo](change-a-role-scope-exchange-2013-help.md)
    
      - [Delegare le assegnazioni di ruolo](delegate-role-assignments-exchange-2013-help.md)

## Assegnazioni di ruolo regolare e di delega

Le assegnazioni di ruolo regolari consentono all'assegnatario di accedere alle voci del ruolo di gestione rese disponibili dal ruolo di gestione associato. Se più ruoli di gestione vengono associati a un assegnatario, le voci del ruolo di gestione per ogni ruolo vengono aggregate e applicate. Ciò significa che, se a un assegnatario di ruolo vengono associati i ruoli Regole di trasporto e Inserimento nel journal, i ruoli vengono combinati e tutte le voci associate del ruolo di gestione vengono fornite all'assegnatario. Se l'assegnatario è un gruppo di ruolo o un criterio di assegnazione dei ruoli, le autorizzazioni previste dai ruoli vengono poi fornite agli utenti assegnati al gruppo di ruolo o al criterio di assegnazione dei ruoli. Per ulteriori informazioni sui ruoli di gestione e sulle voci di ruolo, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

Le assegnazioni del ruolo di delega non consentono la gestione delle funzionalità. Le assegnazioni del ruolo di delega consentono a un assegnatario di associare il ruolo specificato ad altri assegnatari. Se l'assegnatario è un gruppo di ruolo, tutti i membri del gruppo possono associare il ruolo a un altro assegnatario. Per impostazione predefinita, solo il gruppo di ruolo Gestione organizzazione può associare i ruoli ad altri assegnatari. Solo gli utenti che hanno installato Exchange 2013 sono membri del gruppo di ruolo Gestione organizzazione per impostazione predefinita. È comunque possibile aggiungere altri utenti a questo gruppo di ruolo o crearne altri con assegnazioni del ruolo di delega.


> [!NOTE]
> Le assegnazioni del ruolo di delega consentono agli assegnatari di delegare i ruoli di gestione ad altri assegnatari. Ciò non consente agli utenti di delegare i gruppi di ruolo. Per ulteriori informazioni sulla delega dei gruppi di ruolo, vedere <A href="understanding-management-role-groups-exchange-2013-help.md">Informazioni sui gruppi di ruoli di gestione</A>.



Se si desidera consentire a un utente di gestire una funzionalità e di assegnare ad altri utenti il ruolo che fornisce le autorizzazioni per l'utilizzo della funzionalità, assegnare:

1.  Un'assegnazione di ruolo regolare per ogni ruolo di gestione che garantisce l'accesso alle funzionalità da gestire.

2.  Un'assegnazione del ruolo di delega per ogni ruolo di gestione che si possono associare ad altri assegnatari.

Le assegnazioni del ruolo regolari e di delega per un assegnatario non devono essere identiche. Ad esempio, un utente è membro di un gruppo di ruolo assegnato al ruolo Regole di trasporto utilizzando un'assegnazione di ruolo regolare. In questo modo l'utente può gestire la funzionalità Regole di trasporto. Tuttavia, all'utente non è stata associata un'assegnazione del ruolo di delega per il ruolo Regole di trasporto, pertanto non può associare questo ruolo ad altri utenti. Comunque, l'utente è membro di un gruppo di ruolo assegnato al ruolo di gestione Inserimento nel journal utilizzando un'assegnazione del ruolo di delega. Il gruppo di ruolo di cui è membro l'utente non dispone di un'assegnazione di ruolo regolare per il ruolo Inserimento nel journal, ma, siccome dispone invece di un'assegnazione del ruolo di delega, l'utente può associare il ruolo ad altri assegnatari.

## Ambiti di gestione

Quando si crea un'assegnazione del ruolo di gestione regolare o di delega, è possibile creare l'assegnazione con un ambito di gestione per limitare gli oggetti manipolabili dall'utente. È possibile creare ambiti destinatari o ambiti di configurazione. Gli ambiti destinatari consentono di controllare chi può gestire cassette postali, utenti di posta, gruppi di distribuzione e così via. Gli ambiti di configurazione consentono di controllare chi può gestire database e server.

Gli ambiti destinatari e di configurazione consentono di segmentare la gestione del server, database o oggetti destinatario nell'organizzazione. Ad esempio, un ambito destinatario può essere aggiunto all'assegnazione di ruolo in modo che amministratori a Vancouver possano gestire solo destinatari di quell'ufficio. Un ambito di configurazione server può essere aggiunto ad una diversa assegnazione ruolo in modo che amministratori a Sydney possano gestire solo server nel loro sito Active Directory.

Gli ambiti consentono di assegnare le autorizzazioni ai gruppi di utenti per individuare dove questi amministratori possono eseguire le loro attività. Ciò consente di creare un modello di autorizzazioni associato ai limiti geografici o dell'organizzazione.

È possibile creare un'assegnazione con un ambito predefinito o aggiungere un ambito personalizzato. Gli ambiti predefiniti, come limitare un utente solo alla propria cassetta postale o ai gruppi di distribuzione, possono essere applicati utilizzando le opzioni disponibili sull'assegnazione stessa. In alternativa, è possibile creare un ambito destinatario o di configurazione personalizzato e aggiungerlo all'assegnazione di ruolo. Gli ambiti personalizzati consentono una scelta più dettagliata degli oggetti da inserire nell'ambito stesso.

Non è possibile specificare gli ambiti predefiniti e personalizzati nella stessa assegnazione. Non è inoltre possibile combinare gli ambiti esclusivi e regolari nella stessa assegnazione.

Ciascuna assegnazione di ruolo può avere un solo ambito destinatario ed un solo ambito di configurazione. Se si vogliono specificare più di un ambito destinatario o di configurazione ad una assegnazione di ruolo per lo stesso ruolo di gestione, è necessario creare più assegnazioni di ruolo.

In assenza di un ambito personalizzato o predefinito l'assegnazione di ruolo è limitata agli ambiti destinatario o di configurazione definiti nel ruolo stesso. Questi ambiti sono definiti ambiti impliciti. Qualunque assegnazione di ruolo priva di un ambito predefinito o personalizzato eredita gli ambiti impliciti del ruolo al quale viene associata.

Per ulteriori informazioni sugli ambiti, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

## Assegnazioni di ruoli regolari

Le assegnazioni di ruolo esclusive vengono create quando si associa un ambito esclusivo a un'assegnazione di ruolo. Gli ambiti esclusivi agiscono come gli ambiti regolari e consentono agli assegnatari di ruolo di gestire i destinatari corrispondenti all'ambito esclusivo. Tuttavia, diversamente dagli ambiti regolari, a tutti gli altri assegnatari viene negata la possibilità di gestire i destinatari, anche se corrispondono agli ambiti applicati alle assegnazioni di ruolo. Ciò può risultare utile quando si desidera consentire la gestione di un destinatario solo a pochi amministratori. Solo questi specifici amministratori possono gestire il destinatario: a tutti gli altri amministratori viene negato l'accesso.

Ad esempio, si consideri quanto segue:

  - John è un dirigente di Contoso. La sua cassetta postale corrisponde all'ambito esclusivo denominato VIP Users, associato all'assegnazione esclusiva VIP Restricted.

  - La cassetta postale di John viene inclusa anche nell'ambito regolare denominato Redmond Users, associato all'assegnazione regolare Redmond Administration.

  - Bill è un amministratore associato all'assegnazione esclusiva VIP Restricted.

  - Chris è un amministratore associato all'assegnazione regolare Redmond Administration.

Dato che la cassetta postale di John corrisponde all'ambito esclusivo VIP Users, solo Bill può gestire la sua cassetta postale. Anche se la cassetta postale di John corrisponde anche all'ambito regolare Redmond Users, Chris non è associato all'assegnazione esclusiva VIP Restricted. Di conseguenza, Exchange nega a Chris la possibilità di gestire la cassetta postale di John. Per gestire la cassetta postale di John, Chris deve essere associato a un'assegnazione esclusiva con un ambito esclusivo corrispondente alla cassetta postale di John.

Per ulteriori informazioni, vedere [Informazioni sui ambiti esclusivi](understanding-exclusive-scopes-exchange-2013-help.md).


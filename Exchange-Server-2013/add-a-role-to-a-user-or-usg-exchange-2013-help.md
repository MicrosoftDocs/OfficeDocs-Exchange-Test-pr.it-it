---
title: 'Aggiungere un ruolo di un utente o gruppo di protezione universale: Exchange 2013 Help'
TOCTitle: Aggiungere un ruolo di un utente o gruppo di protezione universale
ms:assetid: ae5608de-a141-4714-8876-bce7d2a22cb5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351056(v=EXCHG.150)
ms:contentKeyID: 50481415
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiungere un ruolo di un utente o gruppo di protezione universale

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

Le assegnazioni del ruolo di gestione consentono di assegnare un ruolo di gestione a un utente o a un gruppo di protezione universale (USG, Universal Security Group). Assegnando un ruolo a un utente o a un gruppo di protezione universale, gli utenti possono eseguire attività dipendenti dai cmdlet o dagli script e dai relativi parametri definiti nel ruolo di gestione.

Per assegnare ruoli a un gruppo di ruoli di gestione o a un criterio di assegnazione del ruolo di gestione, vedere i seguenti argomenti:

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Gestire i criteri di assegnazione dei ruoli](manage-role-assignment-policies-exchange-2013-help.md)

Per aggiungere membri a un gruppo di ruolo o assegnare un criterio di assegnazione del ruolo a un utente finale, vedere i seguenti argomenti:

  - [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md)

  - [Modificare il criterio di assegnazione di una cassetta postale](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

Per ulteriori informazioni, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative ai ruoli, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Assegnazioni ruolo" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Anche se è possibile assegnare direttamente i ruoli agli utenti e ai gruppi di protezione universali, per concedere le autorizzazioni agli amministratori e agli utenti finali è consigliabile utilizzare i gruppi di ruoli di gestione e i criteri di assegnazione dei ruoli di gestione. Se si utilizzano i gruppi di ruolo e i criteri di assegnazione, il modello di autorizzazioni risulterà semplificato.

  - Le assegnazioni dei ruoli si possono sommare. In pratica, tutti i ruoli vengono aggiunti in fase di valutazione. Se a un utente sono assegnati due ruoli e uno di questi contiene un cmdlet, a differenza dell'altro, il cmdlet è tuttora a disposizione dell'utente.
    
    Per impostazione predefinita, le assegnazioni di ruolo non concedono la capacità di assegnare ruoli ad altri utenti. Per consentire a un utente di assegnare ruoli ad altri utenti o gruppi di protezione universali, vedere [Delegare le assegnazioni di ruolo](delegate-role-assignments-exchange-2013-help.md).

  - Se si crea un'assegnazione con un ambito, questo sostituisce l'ambito di scrittura implicito del ruolo. L'ambito di lettura implicito del ruolo viene comunque applicato. Il nuovo ambito non è in grado di restituire oggetti esterni all'ambito di lettura implicito del ruolo. Per ulteriori informazioni, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

  - Tutte le procedure in questo argomento utilizzano il parametro *SecurityGroup* per assegnare i ruoli a un gruppo di protezione universale. Se si desidera assegnare il ruolo a un utente specifico, utilizzare il parametro *User* anziché il parametro *SecurityGroup*. La sintassi per ciascun comando è la stessa.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Creazione di un'assegnazione di ruolo priva di ambito

È possibile creare un'assegnazione di ruolo senza alcun ambito. Quando si esegue questa operazione, vengono applicati gli ambiti di scrittura e di lettura impliciti del ruolo.

Utilizzare la seguente sintassi per assegnare un ruolo a un gruppo di protezione universale senza alcun ambito.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name>

In questo esempio viene assegnato il ruolo dei server Exchange al gruppo di protezione universale SeattleAdmins.

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Creazione di un'assegnazione di ruolo con un ambito relativo predefinito

Se un ambito relativo predefinito consente di soddisfare i requisiti aziendali, è possibile applicare tale ambito all'assegnazione di ruolo anziché creare un ambito personalizzato. Per un elenco degli ambiti predefiniti e le relative descrizioni, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

Utilizzare la seguente sintassi per assegnare un ruolo a un gruppo di protezione universale con un ambito predefinito:

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

In questo esempio viene assegnato il ruolo dei server Exchange al gruppo di protezione universale SeattleAdmins e viene applicato l'ambito predefinito Organization.

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers" -RecipientRelativeWriteScope Organization

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Creazione di un'assegnazione di ruolo con un ambito basato su un filtro destinatari

Se è stato creato un ambito basato su un filtro destinatari e si desidera utilizzarlo con un'assegnazione di ruolo, è necessario includere l'ambito nel comando utilizzato per assegnare il ruolo a un gruppo di protezione universale utilizzando il parametro *CustomRecipientWriteScope*. Se si utilizza il parametro *CustomRecipientWriteScope*, non è possibile utilizzare il parametro *RecipientOrganizationalUnitScope*.

Prima di poter aggiungere un ambito ad un'assegnazione del ruolo, è necessario crearne uno. Per ulteriori informazioni, vedere [Creare un ambito normale o esclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

Utilizzare la seguente sintassi per assegnare un ruolo a un gruppo di protezione universale con un ambito basato su un filtro destinatari.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -CustomRecipientWriteScope <role scope name>

In questo esempio viene assegnato il ruolo Mail Recipients al gruppo di protezione universale Seattle Recipient Admins e viene applicato l'ambito Seattle Recipients.

    New-ManagementRoleAssignment -Name "Mail Recipients_Seattle Recipient Admins" -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -CustomRecipientWriteScope "Seattle Recipients"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Creazione di un'assegnazione di ruolo con un ambito di configurazione basato su un elenco o su un filtro server o database

Se è stato creato un ambito basato su un elenco o su un filtro server o database e si desidera utilizzarlo con un'assegnazione di ruolo, è necessario includere l'ambito nel comando utilizzato per assegnare il ruolo a un gruppo di protezione universale utilizzando il parametro *CustomConfigWriteScope*.

Prima di poter aggiungere un ambito ad un'assegnazione del ruolo, è necessario crearne uno. Per ulteriori informazioni, vedere [Creare un ambito normale o esclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

Utilizzare la seguente sintassi per assegnare un ruolo a un gruppo di protezione universale con un ambito di configurazione.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -CustomConfigWriteScope <role scope name>

In questo esempio viene assegnato il ruolo dei server Exchange al gruppo di protezione universale MailboxAdmins e viene applicato l'ambito Mailbox Servers.

    New-ManagementRoleAssignment -Name "Exchange Servers_MailboxAdmins" -SecurityGroup MailboxAdmins -Role "Exchange Servers" -CustomConfigWriteScope "Mailbox Servers"

Nell'esempio precedente viene descritto come aggiungere un'assegnazione di ruolo con un ambito di configurazione server. La sintassi per aggiungere un ambito di configurazione di database è identica. Viene specificato il nome di un ambito di database anziché di un ambito server.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Creazione di un'assegnazione di ruolo con un ambito OU

Se si desidera applicare l'ambito di scrittura di un ruolo a un'unità organizzativa (OU), è possibile specificare l'unità organizzativa direttamente nel parametro *RecipientOrganizationalUnitScope*. Se si utilizza il parametro *RecipientOrganizationalUnitScope*, non è possibile utilizzare il parametro *CustomRecipientWriteScope*.

Utilizzare la sintassi seguente per assegnare un ruolo a un gruppo di protezione universale e limitare l'ambito di scrittura di un ruolo a un'unità organizzativa specifica.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -RecipientOrganizationalUnitScope <OU>

In questo esempio viene assegnato il ruolo Mail Recipients al gruppo di protezione universale SalesRecipientAdmins e viene esaminata l'assegnazione all'unità organizzativa sales/users OU del dominio contoso.com.

    New-ManagementRoleAssignment -Name "Mail Recipients_SalesRecipientAdmins" -SecurityGroup SalesRecipientAdmins -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Creazione di un'assegnazione di ruolo con un ambito di configurazione o destinatario esclusivo

Per creare un'assegnazione di ruolo esclusiva con un ambito di configurazione o destinatario esclusivo, è possibile utilizzare le procedure descritte nelle sezioni Create a role assignment with a recipient filter-based scope e Create a role assignment with a server or database filter or list-based configuration scope. L'unica differenza nella creazione di un'assegnazione di ruolo con un ambito esclusivo riguarda la necessità di specificare i seguenti parametri esclusivi, valutando se si utilizza un ambito destinatario esclusivo o un ambito di configurazione esclusivo:

  - **Ambiti esclusivi dei destinatari**   Utilizzare il parametro *ExclusiveRecipientWriteScope*, invece del parametro *CustomRecipientWriteScope*.

  - **Ambiti esclusivi della configurazione**   Utilizzare il parametro *ExclusiveConfigWriteScope*, invece del parametro *CustomConfigWriteScope*.

Quando si esegue questa procedura, gli utenti a cui è assegnato il ruolo possono eseguire operazioni sugli oggetti inclusi nell'ambito esclusivo. Per ulteriori informazioni sugli ambiti esclusivi, vedere [Informazioni sui ambiti esclusivi](understanding-exclusive-scopes-exchange-2013-help.md).

Non è possibile creare un'assegnazione di ruolo utilizzando sia ambiti esclusivi sia ambiti regolari.

In questo esempio viene assegnato il ruolo Mail Recipients al gruppo di protezione universale Protected User Admins e viene applicato l'ambito esclusivo Protected Users.

    New-ManagementRoleAssignment -Name "Mail Recipients_Protected User Admins" -SecurityGroup "Protected User Admins" -Role "Mail Recipients" -ExclusiveRecipientWriteScope "Protected Users"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).


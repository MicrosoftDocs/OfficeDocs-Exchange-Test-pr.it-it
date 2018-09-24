---
title: 'Configurare Exchange 2013 per le autorizzazioni diviso: Exchange 2013 Help'
TOCTitle: Configurare Exchange 2013 per le autorizzazioni diviso
ms:assetid: 8c74f893-a6f3-4869-8571-3bc0f662cc87
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638155(v=EXCHG.150)
ms:contentKeyID: 50481145
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare Exchange 2013 per le autorizzazioni diviso

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Le autorizzazioni suddivise consentono a due gruppi separati, ad esempio gli amministratori di Active Directory e di Microsoft Exchange Server 2013, di gestire i relativi servizi, oggetti e attributi. Gli amministratori di Active Directory gestiscono le entità di sicurezza, ad esempio gli utenti, che forniscono le autorizzazioni per accedere a una foresta di Active Directory. Gli amministratori di Exchange gestiscono gli attributi relativi a Exchange per gli oggetti Active Directory e la creazione e la gestione degli oggetti specifici di Exchange.

Microsoft Exchange Server 2013 offre i seguenti tipi di modelli di autorizzazioni divisi:

  - **Autorizzazioni suddivise RBAC**   Le autorizzazioni per creare le entità di sicurezza nella partizione di dominio di Active Directory vengono verificate dal controllo di accesso basato sui ruoli (RBAC). Le entità di sicurezza possono essere create solo dai membri dei gruppi di ruoli appropriati.

  - **Autorizzazioni suddivise Active Directory**   Le autorizzazioni per la creazione delle entità di sicurezza nella partizione di dominio di Active Directory vengono completamente rimosse da qualsiasi utente, servizio o server Exchange. Per creare le entità di sicurezza, non viene fornita alcuna opzione in RBAC. La creazione delle entità di sicurezza in Active Directory deve essere eseguita utilizzando gli strumenti di gestione di Active Directory.
    

    > [!NOTE]
    > Le autorizzazioni divise di Active Directory sono disponibili nelle organizzazioni che utilizzano Exchange Server 2010 Service Pack 1 (SP1) o versioni successive, Exchange 2013 oppure entrambe le versioni di Exchange.



La scelta del modello dipende dalla struttura e dalle esigenze dell'organizzazione. Selezionare la procedura seguente, applicabile al modello che si desidera configurare. Si consiglia di utilizzare il modello delle autorizzazioni suddivise RBAC. Il modello delle autorizzazioni suddivise RBAC fornisce una maggiore flessibilità, mantenendo la stessa separazione amministrativa delle autorizzazioni suddivise di Active Directory.

Per ulteriori informazioni sulle autorizzazioni condivise e suddivise, vedere [Informazioni sulle autorizzazioni diviso](understanding-split-permissions-exchange-2013-help.md).

Per ulteriori informazioni sui gruppi del ruolo di gestione, i ruoli di gestione e le assegnazioni del ruolo di gestione regolari e di delega, vedere i seguenti argomenti:

  - [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md)

  - [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md)

  - [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md)

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

Per informazioni sulle altre attività di gestione relative alle autorizzazioni, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni suddivise Active Directory" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - È necessario utilizzare Windows PowerShell, la shell comandi Windows o entrambe le funzionalità per eseguire queste procedure. Per ulteriori informazioni, vedere la specifica procedura.

  - Se sono presenti server Exchange 2010 all'interno dell'organizzazione, il modello di autorizzazioni che selezionare inoltre possibile applicare a tali server.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Passaggio alle autorizzazioni suddivise RBAC

L'organizzazione di Exchange 2013 può essere configurata per le autorizzazioni suddivise RBAC. Al termine dell'operazione, solo gli amministratori di Active Directory saranno in grado di creare le entità di protezione di Active Directory. Ciò significa che gli amministratori di Exchange non potranno utilizzare i cmdlet seguenti:

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Gli amministratori di Exchange potranno gestire solo gli attributi di Exchange sulle entità di protezione esistenti di Active Directory. Tuttavia, potranno creare e gestire oggetti specifici di Exchange, ad esempio le regole di trasporto e i gruppi di distribuzione. Per ulteriori informazioni, vedere la sezione "Autorizzazioni suddivise RBAC" in [Informazioni sulle autorizzazioni diviso](understanding-split-permissions-exchange-2013-help.md).

Per configurare le autorizzazioni suddivise su Exchange 2013, è necessario assegnare il ruolo Creazione destinatario di posta elettronica e il ruolo Creazione e appartenenza a un gruppo di sicurezza al gruppo di ruoli contenente gli amministratori di Active Directory. Quindi, è necessario rimuovere le assegnazioni tra questi ruoli e qualsiasi gruppo di ruoli o gruppo di protezione universale contenente gli amministratori di Exchange.

Per configurare le autorizzazioni suddivise RBAC, effettuare le seguenti operazioni:

1.  Se l'organizzazione è attualmente configurata per le autorizzazioni divise di Active Directory, effettuare le seguenti operazioni da un prompt della shell comandi di Windows.
    
    1.  Disabilitare le autorizzazioni divise di Active Directory eseguendo il comando riportato di seguito dal supporto di installazione di Exchange 2013.
        
        ```powershell
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false
        ```
    
    2.  Riavviare i server Exchange 2013 dell'organizzazione o attendere il token di accesso di Active Directory per la replica su tutti i server Exchange 2013.
        

        > [!NOTE]
        > Se sono presenti server Exchange&nbsp;2010 all'interno dell'organizzazione, è inoltre necessario riavviare i server.



2.  Eseguire le seguenti operazioni da Exchange Management Shell:
    
    1.  Creare un gruppo di ruoli per gli amministratori di Active Directory. Oltre a creare il gruppo di ruoli, il comando crea assegnazioni di ruolo regolari tra il nuovo gruppo di ruoli e il ruolo Creazione destinatario di posta elettronica e Creazione e appartenenza a un gruppo di sicurezza.
        ```powershell
            New-RoleGroup "Active Directory Administrators" -Roles "Mail Recipient Creation", "Security Group Creation and Membership"
        ```

        > [!NOTE]
        > Se si desidera consentire la creazione delle assegnazioni di ruolo da parte dei membri di questo gruppo di ruoli, includere il ruolo Gestione ruoli. Non è necessario aggiungere il ruolo in questa fase. Tuttavia, se si desidera assegnare il ruolo Creazione destinatario di posta elettronica o il ruolo Creazione e appartenenza a un gruppo di sicurezza ad altri assegnatari, il ruolo Gestione ruoli deve essere assegnato a questo nuovo gruppo di ruoli. La procedura seguente consente di configurare il gruppo di ruoli Administrators di Active Directory come l'unico gruppo di ruoli che può delegare questi ruoli.

    
    2.  Creare le assegnazioni del ruolo di delega tra il nuovo gruppo di ruoli e il ruolo Creazione destinatario di posta elettronica e il ruolo Creazione e appartenenza a un gruppo di sicurezza utilizzando i comandi seguenti.
        ```powershell
            New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Active Directory Administrators" -Delegating
            New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Active Directory Administrators" -Delegating
        ```
    3.  Aggiungere membri al nuovo gruppo di ruoli utilizzando il comando seguente.
        
        ```powershell
        Add-RoleGroupMember "Active Directory Administrators" -Member <user to add>
        ```
    
    4.  Sostituire l'elenco di delegati sul nuovo gruppo di ruoli in modo che solo i membri del gruppo possono aggiungere o rimuovere i membri.
        
        ```powershell
        Set-RoleGroup "Active Directory Administrators" -ManagedBy "Active Directory Administrators"
        ```
        

        > [!IMPORTANT]
        > I membri del gruppo di ruoli Gestione organizzazione o quelli assegnati al ruolo Gestione ruolo direttamente o mediante un altro gruppo di ruoli o gruppo di sicurezza universale, possono ignorare questo controllo di sicurezza delegato. Se si desidera impedire a qualsiasi amministratore di Exchange di aggiungersi al nuovo gruppo di ruoli, è necessario rimuovere l'assegnazione di ruolo tra il ruolo Gestione ruoli e qualsiasi amministratore di Exchange e attribuirla a un altro gruppo di ruoli.

    
    5.  Individuare tutte le assegnazione di ruolo di delega e regolari per il ruolo Creazione destinatario di posta elettronica utilizzando il comando seguente. Il comando visualizza solo le proprietà **NameRole** e **RoleAssigneeName**.
        
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Format-Table Name, Role, RoleAssigneeName -Auto
    
    6.  Rimuovere tutte le assegnazioni di ruolo di delega e regolari per il ruolo Creazione destinatario di posta elettronica non associate al nuovo gruppo di ruoli o a qualsiasi altro gruppo di ruoli o gruppo di protezione universale o le assegnazioni dirette che si desidera mantenere utilizzando il comando seguente.
        
        ```powershell
        Remove-ManagementRoleAssignment <Mail Recipient Creation role assignment to remove>
        ```
        

        > [!NOTE]
        > Se si desidera rimuovere tutte le assegnazioni di ruolo regolari e di delega al ruolo Creazione destinatario di posta elettronica per ogni assegnatario diverso dal gruppo di ruoli Administrators di Active Directory, utilizzare il comando seguente. L'opzione <EM>WhatIf</EM> consente di visualizzare le assegnazioni di ruolo che verranno rimosse. Rimuovere l'opzione <EM>WhatIf</EM> ed eseguire di nuovo il comando per rimuovere le assegnazioni di ruolo.

        ```powershell
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
        ```
    7.  Individuare tutte le assegnazioni di ruolo regolari e di delega al ruolo Creazione e appartenenza a un gruppo di sicurezza utilizzando il comando seguente. Il comando visualizza solo le proprietà **NameRole** e **RoleAssigneeName**.
        ```powershell
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Format-Table Name, Role, RoleAssigneeName -Auto
        ```
    8.  Rimuovere tutte le assegnazioni di ruolo regolari e di delega al ruolo Creazione e appartenenza a un gruppo di sicurezza non associate al nuovo gruppo di ruoli o a qualsiasi altro gruppo di ruoli, gruppo di sicurezza universale o assegnazione diretta che si desidera mantenere utilizzando il comando seguente.
        ```powershell
            Remove-ManagementRoleAssignment <Security Group Creation and Membership role assignment to remove>
        ```

        > [!NOTE]
        > È possibile utilizzare lo stesso comando della nota precedente per rimuovere tutte le assegnazioni di ruolo regolari e di delega al ruolo Creazione e appartenenza a un gruppo di sicurezza per qualsiasi assegnatario diverso dal gruppo di ruoli Administrators di Active Directory, come illustrato in questo esempio.

        ```powershell
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
        ```
Per ulteriori informazioni sulla sintassi e sui parametri, vedere gli argomenti seguenti:

  - [New-RoleGroup](https://technet.microsoft.com/it-it/library/dd638181\(v=exchg.150\))

  - [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\))

  - [Add-RoleGroupMember](https://technet.microsoft.com/it-it/library/dd638207\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/it-it/library/dd638182\(v=exchg.150\))

  - [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\))

  - [Remove-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351205\(v=exchg.150\))

## Passaggio alle autorizzazioni suddivise di Active Directory

È possibile configurare l'organizzazione di Exchange 2013 per le autorizzazioni suddivise di Active Directory. Le autorizzazioni suddivise di Active Directory rimuovono completamente le autorizzazioni che consentono agli amministratori e ai server Exchange di creare le entità di sicurezza in Active Directory o di modificare gli attributi non Exchange per tali oggetti. Al termine dell'operazione, solo gli amministratori di Active Directory saranno in grado di creare le entità di sicurezza di Active Directory. Ciò significa che gli amministratori di Exchange non potranno utilizzare i cmdlet seguenti:

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

  - **Update-DistributionGroupMember**

Gli amministratori e i server Exchange potranno gestire solo gli attributi di Exchange per le entità di sicurezza esistenti di Active Directory. Tuttavia, potranno creare e gestire gli oggetti specifici di Exchange, ad esempio le regole di trasporto e i dial plan di messaggistica unificata.


> [!WARNING]
> Una volta abilitate le autorizzazioni suddivise di Active Directory, gli amministratori e i server Exchange non potranno più creare le entità di sicurezza in Active Directory, né potranno gestire l'appartenenza ai gruppi di distribuzione. Queste attività devono essere eseguite utilizzando gli strumenti di gestione di Active Directory con le autorizzazioni di Active Directory necessarie. Prima di apportare questa modifica, è necessario valutare l'effetto che avrà sui processi amministrativi e sulle applicazioni di terze parti integrate con Exchange 2013 e il modello di autorizzazioni RBAC.<BR>Per ulteriori informazioni, vedere la sezione "Autorizzazioni divise di Active Directory" in <A href="understanding-split-permissions-exchange-2013-help.md">Informazioni sulle autorizzazioni diviso</A>.



Per passare dalle autorizzazioni suddivise RBAC o condivise alle autorizzazioni suddivise di Active Directory, effettuare le seguenti operazioni:

1.  Da una shell comandi di Windows, eseguire il comando riportato di seguito dal supporto di installazione di Exchange 2013 per abilitare le autorizzazioni divise di Active Directory.
    
    ```powershell
    setup.exe /PrepareAD /ActiveDirectorySplitPermissions:true
    ```

2.  Se l'organizzazione dispone di più domini di Active Directory, è necessario eseguire `setup.exe /PrepareDomain` in ciascun dominio figlio che contiene oggetti o server di Exchange oppure eseguire `setup.exe /PrepareAllDomains` da un sito che dispone di un server Active Directory da ogni dominio.

3.  Riavviare i server Exchange 2013 dell'organizzazione o attendere il token di accesso di Active Directory per la replica su tutti i server Exchange 2013.
    

    > [!NOTE]
    > Se sono presenti server Exchange&nbsp;2010 all'interno dell'organizzazione, è inoltre necessario riavviare i server.



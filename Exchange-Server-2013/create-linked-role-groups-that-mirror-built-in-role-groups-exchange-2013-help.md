---
title: 'Creare gruppi di ruoli collegato il mirroring di gruppi di ruoli incorporati: Exchange 2013 Help'
TOCTitle: Creare gruppi di ruoli collegato il mirroring di gruppi di ruoli incorporati
ms:assetid: 89dfcbb3-0568-4bbf-a885-746b91ba307e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876918(v=EXCHG.150)
ms:contentKeyID: 50481105
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare gruppi di ruoli collegato il mirroring di gruppi di ruoli incorporati

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

Utilizzo di gruppi di ruoli gestione collegato in Microsoft Exchange Server 2013, è possibile collegare un gruppo di ruoli in una foresta di risorse Exchange 2013 con un gruppo di protezione universale (USG) in una foresta utente esterno. Ciò è utile quando si desidera che gli amministratori di account nella foresta degli utenti per gestire i server che eseguono Exchange nella foresta di risorse. Per ulteriori informazioni sui gruppi di ruoli collegato, vedere [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md).

Per impostazione predefinita, Exchange 2013 include un numero di gruppi di ruoli incorporati che offrono le autorizzazioni per gestire un'ampia gamma di caratteristiche e funzioni di processo. Ogni gruppo di ruoli è personalizzato per fornire le autorizzazioni necessarie per ogni caratteristica e un processo della funzione. Tuttavia, non sono collegati questi gruppi di ruoli gruppi di protezione universale di una foresta esterna. Può contenere solo gli utenti e gruppi di protezione universale dalla foresta risorsa locale. Fortunatamente, è possibile replicare i gruppi di ruoli incorporati utilizzando gruppi di ruoli collegato.

È possibile creare ogni gruppo di ruoli incorporati nuovo gruppo di ruoli collegato. Tutti i ruoli di gestione e gli ambiti di gestione assegnati a ogni gruppo di ruolo vengono aggiunti al nuovo gruppo di ruoli collegato. Per ulteriori informazioni sui ruoli di gestione e sugli ambiti, vedere gli argomenti seguenti:

  - [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md)

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

Cerchi altre attività di gestione relative a gruppi di ruoli? Estrarre [Autorizzazioni](permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di ruoli" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Configurazione di un gruppo di ruoli collegato, è necessario un trust unidirezionale tra le risorse Active Directory di strutture in cui risiederà il gruppo di ruoli collegato ed esterna Active Directory in cui risiedono gli utenti o gruppi di protezione universale. La foresta risorsa deve ritenere attendibile la foresta esterna.

  - È necessario disporre delle seguenti informazioni sulla foresta esterna di Active Directory:
    
      - **Credenziali**   È necessario disporre di un nome utente e password che può accedere foresta esterna Active Directory. Queste informazioni vengono utilizzate con il parametro *LinkedCredential* nel cmdlet **New-RoleGroup** . Queste informazioni vengono ottenute eseguendo il cmdlet **Get-Credential** . Il formato del nome utente è *domain*\\*username*.
    
      - **Controller di dominio**   È necessario disporre del nome di dominio completo (FQDN) di un controller di dominio di Active Directory nella foresta esterna di Active Directory. Queste informazioni vengono utilizzate con il parametro *LinkedDomainController* sul cmdlet **New-RoleGroup**.
    
      - **Gruppo di protezione universale esterno**   È necessario disporre del nome completo di un gruppo di protezione universale nella foresta esterna di Active Directory che contiene i membri che si desidera associare al gruppo di ruoli collegato. Queste informazioni vengono utilizzate con il parametro *LinkedForeignGroup* sul cmdlet **New-RoleGroup**.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo della Shell per creare gruppi di ruoli collegato replicano i gruppi di ruoli incorporati

Ognuna delle sezioni seguenti viene illustrato come ricreare ogni gruppo di ruoli come un gruppo di ruoli collegato. Completare le procedure descritte in ogni sezione per creare tutti i gruppi di ruoli incorporati come gruppi di ruoli collegato.

## Creare il gruppo di ruoli collegato Gestione organizzazione

Per creare nuovamente il gruppo di ruoli Gestione organizzazione gruppo di ruoli collegato, eseguire una routine differente rispetto alla procedura utilizzata per ricreare altri gruppi di ruoli incorporati. Ciò avviene perché il gruppo di ruoli Gestione organizzazione con delega le assegnazioni di ruolo tra di esso e tutti i ruoli di gestione. Ricreare le assegnazioni di ruolo delegate richiede un passaggio aggiuntivo.

1.  Creare un gruppo di protezione universale nella foresta esterna che verrà collegata al gruppo di ruoli Gestione organizzazione.

2.  Archiviare le credenziali della foresta esterna di Active Directory in una variabile.
    
        $ForeignCredential = Get-Credential

3.  Archiviare tutti i ruoli assegnati al gruppo di ruoli Gestione organizzazione in una variabile.
    
        $OrgMgmt  = Get-RoleGroup "Organization Management"

4.  Creare il gruppo di ruoli collegato Gestione organizzazione e aggiungere i ruoli assegnati al gruppo di ruoli incorporati Gestione organizzazione.
    
        New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles

5.  Rimuovere tutte le assegnazioni regolari tra il nuovo gruppo di ruoli collegato Gestione organizzazione e il personale \* ruoli dell'utente finale.
    
        Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment

6.  Aggiungere la delega le assegnazioni di ruolo tra il nuovo gruppo di ruoli collegato Gestione organizzazione e tutti i ruoli di gestione.
    
        Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

In questo esempio si presuppone che per ogni parametro vengono utilizzati i valori seguenti:

  - **LinkedForeignGroup**   `Organization Management Administrators`

  - **LinkedDomainController**   `DC01.users.contoso.com`

Utilizza valori precedenti, in questo esempio viene creato nuovamente il gruppo di ruolo Gestione organizzazione un gruppo di ruoli collegato.

    $ForeignCredential = Get-Credential
    $OrgMgmt  = Get-RoleGroup "Organization Management"
    New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup "Organization Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles
    Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment
    Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

## Creare tutti gli altri gruppi di ruoli collegato

Per ricreare i gruppi di ruoli incorporati (escluso il gruppo di ruoli Gestione organizzazione ) come gruppi di ruoli collegato, utilizzare la procedura seguente per ogni gruppo.

1.  Creare un gruppo di protezione universale nella foresta esterna per ogni gruppo di ruoli collegato a ogni nuovo gruppo di ruoli.

2.  Archiviare le credenziali di foresta esterna Active Directory in una variabile. È sufficiente eseguire questa operazione una sola volta.
    
        $ForeignCredential = Get-Credential

3.  Recuperare un elenco dei gruppi di ruolo utilizzando il cmdlet seguente.
    
        Get-RoleGroup

4.  Per ogni gruppo di ruoli, oltre al gruppo di ruolo Gestione organizzazione, eseguire le operazioni seguenti.
    
        $RoleGroup = Get-RoleGroup <name of role group to re-create>
        New-RoleGroup "<role group name> - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles

5.  Ripetere il passaggio precedente per ogni gruppo di ruoli incorporati che si desidera creare di nuovo gruppo di ruoli collegato.

In questo esempio si presuppone che per ogni parametro vengono utilizzati i valori seguenti:

  - **LinkedDomainController**   `DC01.users.contoso.com`

  - **Gruppi di ruoli incorporati per essere ricreata come gruppi di ruoli collegato** `Recipient Management, Server Management`   

  - **Gruppo esterna per il gruppo di ruoli collegato Recipient Management** `Recipient Management Administrators`   

  - **Gruppo esterna per il gruppo di ruoli collegato Gestione Server** `Server Management Administrators`   

Utilizza valori precedenti, in questo esempio viene ricreato il Gestione destinatari e i gruppi di ruoli di gestione dei Server come gruppi di ruoli collegato.

    $ForeignCredential = Get-Credential
    Get-RoleGroup
    $RoleGroup = Get-RoleGroup "Recipient Management"
    New-RoleGroup "Recipient Management - Linked" -LinkedForeignGroup "Recipient Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles
    $RoleGroup = Get-RoleGroup "Server Management"
    New-RoleGroup "Server Management - Linked" -LinkedForeignGroup "Server Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles

## Altre attività

Dopo aver creato i gruppi di ruoli collegato, è inoltre possibile:

Aggiungere membri a USG esterno utilizzando Active Directory utenti e computer nella foresta esterna.

Rimuovere i membri dei gruppi di ruoli incorporati. Per ulteriori informazioni, vedere [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).

Aggiungere, rimuovere o modificare l'ambito dei ruoli per i nuovi gruppi di ruoli collegato. Per ulteriori informazioni, vedere [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

Creare gruppi di ruoli collegato aggiuntive. Per ulteriori informazioni, vedere [Gestire i gruppi di ruoli collegato](manage-linked-role-groups-exchange-2013-help.md).


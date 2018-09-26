---
title: 'Configurare Exchange 2013 per autorizzazioni condivise: Exchange 2013 Help'
TOCTitle: Configurare Exchange 2013 per autorizzazioni condivise
ms:assetid: 7d119977-b420-4b66-acf0-0a978b188cdd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638146(v=EXCHG.150)
ms:contentKeyID: 50481017
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare Exchange 2013 per autorizzazioni condivise

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Le autorizzazioni condivise consentono all'utente, in qualità di amministratore di Microsoft Exchange Server 2013, di creare le entità di sicurezza di Active Directory, come gli utenti, quindi di configurarle come destinatari di Exchange. A differenza delle autorizzazioni suddivise, che separano le attività di gestione tra i gruppi di amministratori di Exchange e di amministratori di Active Directory, le autorizzazioni condivise non separano alcuna attività.

Per ulteriori informazioni sulle autorizzazioni condivise e suddivise, vedere [Informazioni sulle autorizzazioni diviso](understanding-split-permissions-exchange-2013-help.md).

È possibile configurare l'organizzazione di Exchange 2013 per le autorizzazioni condivise se è stata già configurata per le autorizzazioni suddivise. La procedura per passare alle autorizzazioni condivise varia in base alla divisione delle autorizzazioni utilizzata: controllo di accesso basato sui ruoli (RBAC) o Active Directory. Selezionare la seguente procedura applicabile alla configurazione corrente. L'organizzazione utilizza la divisione delle autorizzazioni Active Directory se le seguenti condizioni sono vere:

  - L'unità organizzativa Gruppi di protezione di Microsoft Exchange esiste già.

  - Il gruppo di sicurezza Autorizzazioni di Exchange Windows si trova nell'unità organizzativa Gruppi protetti di Microsoft Exchange.

  - Il gruppo di sicurezza Sottosistema attendibile di Exchange è un membro del gruppo di sicurezza Autorizzazioni di Exchange Windows.

  - Non esistono assegnazioni dei ruoli di gestione regolari al ruolo Creazione destinatario di posta elettronica o al ruolo Creazione e appartenenza a un gruppo di sicurezza.

Se l'organizzazione non è stata mai configurata per le autorizzazioni suddivise, non è necessario eseguire questa procedura. Per impostazione predefinita, Exchange 2013 viene configurato per le autorizzazioni di condivisione.

Per ulteriori informazioni sui gruppi del ruolo di gestione, i ruoli di gestione e le assegnazioni del ruolo di gestione regolari e di delega, vedere i seguenti argomenti:

  - [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md)

  - [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md)

  - [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md)

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

Per informazioni sulle altre attività di gestione relative alle autorizzazioni, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - Per eseguire queste procedure, è necessario utilizzare Windows PowerShell, Windows Command Shell o entrambi. Per ulteriori informazioni, vedere la specifica procedura.

  - L'organizzazione di Exchange 2013 deve essere attualmente configurata per la divisione delle autorizzazioni Active Directory o RBAC.

  - Se l'organizzazione dispone di server Microsoft Exchange Server 2010, il modello delle autorizzazioni selezionato verrà applicato anche a quei server.

  - È necessario disporre delle autorizzazioni per delegare il ruolo di gestione Creazione destinatario di posta elettronica e il ruolo di gestione Creazione e appartenenza a un gruppo di sicurezza al gruppo del ruolo di gestione Gestione organizzazione o a un altro gruppo di ruoli assegnato al ruolo Destinatari di posta.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Passaggio dalle autorizzazioni suddivise RBAC alle autorizzazioni condivise

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di ruoli" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

Per passare dalle autorizzazioni suddivise RBAC alle autorizzazioni condivise di Exchange 2013, è necessario assegnare il ruolo Creazione destinatario di posta elettronica e il ruolo Creazione e appartenenza a un gruppo di sicurezza a un gruppo di ruoli a cui viene assegnato anche il ruolo Destinatari di posta e che ha come membri gli amministratori di Exchange 2013. Nella configurazione predefinita delle autorizzazioni condivise, il gruppo di ruoli Gestione organizzazione contiene entrambi i ruoli. Per questo motivo, il gruppo di ruoli Gestione organizzazione si trova in questa procedura.

## Configurazione delle autorizzazioni condivise

Per configurare le autorizzazioni condivise sul gruppo di ruoli Gestione organizzazione, effettuare l'operazione seguente utilizzando un account con le autorizzazioni per delegare le assegnazioni di ruolo per il ruolo Creazione destinatario di posta elettronica e il ruolo Creazione e appartenenza a un gruppo di sicurezza:

1.  Aggiungere le assegnazioni del ruolo di delega per il ruolo Creazione destinatario di posta elettronica e il ruolo Creazione e appartenenza a un gruppo di sicurezza al gruppo di ruoli Gestione organizzazione utilizzando i comandi seguenti.
    ```powershell
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management" -Delegating
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management" -Delegating
    ```

    > [!NOTE]
    > Al gruppo di ruoli (in questa procedura, il gruppo di ruoli Administrators di Active Directory), che dispone delle assegnazioni del ruolo di delega per il ruolo Creazione destinatario di posta elettronica e il ruolo Creazione e appartenenza a un gruppo di sicurezza, deve essere assegnato il ruolo Gestione ruoli per eseguire il cmdlet <STRONG>New-ManagementRoleAssignment</STRONG>. L'assegnatario del ruolo che può delegare il ruolo Gestione ruoli deve assegnare tale ruolo al gruppo di ruoli Administrators di Active Directory.



2.  Aggiungere assegnazioni di ruolo regolari per il ruolo Creazione destinatario di posta elettronica ai gruppi di ruoli Gestione organizzazione e Gestione destinatari utilizzando i comandi seguenti.
    ```powershell
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Recipient Management"
    ```
3.  Aggiungere un'assegnazione del ruolo regolare per il ruolo Creazione e appartenenza a un gruppo di sicurezza al gruppo di ruoli Gestione organizzazione utilizzando il comando seguente.
    ```powershell
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"
    ```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Eliminazione delle autorizzazioni dagli amministratori di Active Directory (facoltativo)

Facoltativamente, è possibile rimuovere le autorizzazioni concesse agli amministratori di Active Directory se non si desidera più che creino o gestiscano gli oggetti di Active Directory utilizzando gli strumenti di gestione di Exchange. Se si desidera rimuovere le autorizzazioni dagli amministratori di Active Directory, eseguire questa procedura.


> [!NOTE]
> Anche se è possibile rimuovere le autorizzazioni per gli amministratori di Active Directory in modo che non siano più in grado di gestire gli oggetti di Active Directory utilizzando gli strumenti di gestione di Exchange, gli amministratori di Active Directory possono continuare a gestire gli oggetti di Active Directory con gli strumenti di gestione di Active Directory, se le autorizzazioni di Active Directory lo consentono. Tuttavia, non saranno in grado di gestire attributi specifici di Exchange sugli oggetti di Active Directory. Per ulteriori informazioni, vedere <A href="understanding-split-permissions-exchange-2013-help.md">Informazioni sulle autorizzazioni diviso</A>.



Per rimuovere le autorizzazioni suddivise relative a Exchange dagli amministratori di Active Directory, fare quanto segue:

1.  Rimuovere le assegnazioni di ruolo regolari e di delega che associano il ruolo Creazione destinatario di posta elettronica al gruppo di ruoli o al gruppo di sicurezza universale (USG) contenente gli amministratori di Active Directory come membri utilizzando il comando seguente. Questo comando utilizza come esempio il gruppo di ruoli Administrators di Active Directory. L'opzione *WhatIf* consente di visualizzare le assegnazioni di ruolo che verranno rimosse. Rimuovere l'opzione *WhatIf* ed eseguire di nuovo il comando per rimuovere le assegnazioni di ruolo.
    ```powershell
        Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
    ```
2.  Rimuovere le assegnazioni del ruolo di delega e regolare che applicano il ruolo Creazione e appartenenza a un gruppo di sicurezza al gruppo di ruoli o al gruppo di protezione universale che contiene gli amministratori di Active Directory come membri utilizzando il comando seguente. Questo comando utilizza come esempio il gruppo di ruoli Administrators di Active Directory. L'opzione *WhatIf* consente di visualizzare le assegnazioni di ruolo che verranno rimosse. Rimuovere l'opzione *WhatIf* ed eseguire di nuovo il comando per rimuovere le assegnazioni di ruolo.
    ```powershell
        Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
    ```
3.  Facoltativo. Se si desidera rimuovere tutte le autorizzazioni di Exchange dagli amministratori di Active Directory, è possibile rimuovere il gruppo di ruoli o il gruppo di protezione universale in cui sono membri. Per ulteriori informazioni sulla rimozione di un gruppo di ruoli, vedere [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)) o [Remove-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351205\(v=exchg.150\)).

## Passaggio dalle autorizzazioni suddivise Active Directory alle autorizzazioni condivise

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni suddivise Active Directory" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

Per passare dalle autorizzazioni suddivise Active Directory alle autorizzazioni condivise di Exchange 2013, è necessario eseguire di nuovo il programma di installazione di Exchange per disabilitare le autorizzazioni suddivise Active Directory nell'organizzazione di Exchange, quindi creare le assegnazioni di ruolo tra un gruppo di ruoli e il ruolo Creazione destinatario di posta elettronica e il ruolo Creazione e appartenenza a un gruppo di sicurezza. Nella configurazione predefinita delle autorizzazioni condivise, il gruppo di ruoli Gestione organizzazione contiene entrambi i ruoli. Per questo motivo, il gruppo di ruoli Gestione organizzazione si trova in questa procedura.


> [!IMPORTANT]
> Il comando setup.com di questa procedura apporta modifiche a Active Directory. È necessario utilizzare un account che dispone delle autorizzazioni necessarie per apportare queste modifiche. Questo account non può corrispondere a quello che dispone delle autorizzazioni per creare le assegnazioni di ruolo utilizzando il cmdlet <STRONG>New-ManagementRoleAssignment</STRONG>. Utilizzare l'account, o gli account, con le autorizzazioni necessarie per completare correttamente ogni passo della procedura.



Per passare dalle autorizzazioni suddivise Active Directory alle autorizzazioni condivise, effettuare le seguenti operazioni:

1.  Da una shell dei comandi di Windows, eseguire il comando seguente dal supporto di installazione di Exchange 2013 per disabilitare le autorizzazioni suddivise di Active Directory.
    
    ```powershell
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false
    ```

2.  Da Exchange Management Shell, eseguire i comandi seguenti per aggiungere le assegnazioni di ruolo regolari tra il ruolo Creazione destinatario di posta elettronica e il ruolo Creazione e gestione del gruppo di sicurezza e i gruppi di ruoli Gestione organizzazione e Gestione destinatari.
    ```powershell
        New-ManagementRoleAssignment "Mail Recipient Creation_Organization Management" -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Security Group Creation and Membership_Org Management" -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Mail Recipient Creation_Recipient Management" -Role "Mail Recipient Creation" -SecurityGroup "Recipient Management"
    ```
3.  Riavviare i server Exchange 2013 dell'organizzazione.
    

    > [!NOTE]
    > Se sono presenti server Exchange&nbsp;2010 all'interno dell'organizzazione, è inoltre necessario riavviare i server.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).


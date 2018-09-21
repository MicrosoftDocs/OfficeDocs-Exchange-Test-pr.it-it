---
title: 'Gestire i gruppi di ruoli collegato: Exchange 2013 Help'
TOCTitle: Gestire i gruppi di ruoli collegato
ms:assetid: e2a07395-90c2-4d62-b15d-ac3ff28fe786
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657502(v=EXCHG.150)
ms:contentKeyID: 50481884
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire i gruppi di ruoli collegato

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-09_

Un gruppo legato al ruolo di gestione può essere utilizzato per abilitare i membri di un gruppo di protezione universale in una foresta Active Directory esterna al fine di gestire un'organizzazione Microsoft Exchange Server 2013 in una foresta di risorse Active Directory. Associando un gruppo di protezione universale in una foresta esterna con un gruppo legato al ruolo, ai membri del gruppo di protezione universale sono concesse le autorizzazioni fornite dai ruoli di gestione assegnati al gruppo legato al ruolo. Per ulteriori informazioni sui gruppi di ruoli collegati, vedere [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md).

Per creare e configurare gruppi legati al ruolo, è necessario utilizzare i cmdlet **New-RoleGroup** e **Set-RoleGroup**. Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [New-RoleGroup](https://technet.microsoft.com/it-it/library/dd638181\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/it-it/library/dd638182\(v=exchg.150\))

Per le attività di gestione aggiuntive relative a gruppi di ruoli, vedere [Autorizzazioni](permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: Da 5 a 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di ruoli" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per creare o configurare gruppi legati al ruolo. È necessario utilizzare Exchange Management Shell.

  - Per configurare un gruppo legato al ruolo è necessario che vi sia almeno un trust unidirezionale tra la foresta di risorse Active Directory in cui il gruppo sarà ubicato e la foresta Active Directory esterna a cui appartengono gli utenti o i gruppi di protezione universale. La foresta di risorse deve considerare attendibile la foresta esterna.

  - È necessario disporre delle seguenti informazioni sulla foresta esterna di Active Directory:
    
      - **Credenziali**   È necessario disporre di un nome utente e di una password per poter accedere alla foresta esterna di Active Directory. Queste informazioni vengono utilizzate con il parametro *LinkedCredential* nei cmdlet **New-RoleGroup** e **Set-RoleGroup**.
    
      - **Controller di dominio**   È necessario disporre del nome di dominio completo (FQDN) di un controller di dominio di Active Directory nella foresta esterna di Active Directory. Queste informazioni vengono utilizzate con il parametro *LinkedDomainController* nei cmdlet **New-RoleGroup** e **Set-RoleGroup**.
    
      - **Gruppo di protezione universale esterno**   È necessario disporre del nome completo di un gruppo di protezione universale nella foresta esterna di Active Directory che contiene i membri che si desidera associare al gruppo di ruoli collegato. Queste informazioni vengono utilizzate con il parametro *LinkedForeignGroup* nei cmdlet **New-RoleGroup** e **Set-RoleGroup**.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Creazione di un gruppo legato al ruolo

## Utilizzo di Shell per creare un gruppo legato al ruolo senza ambito

Per creare un gruppo legato al ruolo e assegnare ruoli di gestione per il gruppo legato al ruolo, fare quanto segue:

1.  Archiviare le credenziali della foresta esterna di Active Directory in una variabile.
    
    ```powershell
$ForeignCredential = Get-Credential
```

2.  Creare il gruppo di ruoli collegato utilizzando la sintassi seguente.
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>

3.  Aggiungere o rimuovere i membri dal gruppo di protezione universale esterno utilizzando Utenti e computer di Active Directory su un computer nella foresta esterna di Active Directory.

Con questo esempio viene effettuato quanto segue:

  - Vengono recuperate le credenziali per la foresta esterna di Active Directory users.contoso.com. Queste credenziali vengono utilizzate per collegarsi al controller di dominio DC01.users.contoso.com nella foresta esterna.

  - Crea un gruppo legato al ruolo chiamato Gruppo di ruoli conformi nella foresta risorse in cui Exchange 2013 è installato.

  - Collega il nuovo gruppo di ruolo al gruppo di protezione universale degli amministratori conformi nella foresta Active Directory esterna di users.contoso.com.

  - Assegnare le Regole di trasporto e le regole per la gestione dell'inserimento del Journal al nuovo gruppo legato al ruolo.

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
    New-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles "Transport Rules", "Journaling"

## Utilizzo di Shell per creare un gruppo legato al ruolo con ambito di gestione personalizzato

È possibile creare gruppi legati al ruolo con ambiti di gestione del destinatario personalizzato, ambiti di gestione di configurazione personalizzata o entrambi. Per creare un gruppo legato al ruolo e assegnare ad esso ruoli di gestione con ambiti personalizzati, fare quanto segue:

1.  Archiviare le credenziali della foresta esterna di Active Directory in una variabile.
    
    ```powershell
$ForeignCredential = Get-Credential
```

2.  Creare il gruppo di ruoli collegato utilizzando la sintassi seguente.
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -CustomConfigWriteScope <name of configuration scope> -CustomRecipientWriteScope <name of recipient scope> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>

3.  Aggiungere o rimuovere i membri dal gruppo di protezione universale esterno utilizzando Utenti e computer di Active Directory su un computer nella foresta esterna di Active Directory.

Con questo esempio viene effettuato quanto segue:

  - Vengono recuperate le credenziali per la foresta esterna di Active Directory users.contoso.com. Queste credenziali vengono utilizzate per collegarsi al controller di dominio DC01.users.contoso.com nella foresta esterna.

  - Crea un gruppo legato al ruolo chiamato Gruppo di ruoli conformi di Seattle nella foresta risorse in cui Exchange 2013 è installato.

  - Collega il nuovo gruppo di ruolo al gruppo di protezione universale degli amministratori conformi di Seattle nella foresta Active Directory esterna di users.contoso.com.

  - Assegnare le Regole di trasporto e le regole per la gestione dell'inserimento del Journal al nuovo gruppo legato al ruolo con ambiti di gestione dei destinatari personalizzati di Seattle.

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
    New-RoleGroup "Seattle Compliance Role Group" -LinkedForeignGroup "Seattle Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -CustomRecipientWriteScope "Seattle Recipients" -Roles "Transport Rules", "Journaling"

Per ulteriori informazioni sugli ambiti di gestione, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

## Utilizzo di Shell per creare un gruppo legato al ruolo con ambito di unità organizzativa

È possibile creare gruppi legati al ruolo che utilizzano un ambito destinatario dell'unità organizzativa. Per creare un gruppo legato al ruolo e assegnare ad esso ruoli di gestione con ambito di unità organizzativa, fare quanto segue:

1.  Archiviare le credenziali della foresta esterna di Active Directory in una variabile.
    
    ```powershell
$ForeignCredential = Get-Credential
```

2.  Creare il gruppo di ruoli collegato utilizzando la sintassi seguente.
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope <OU name> -Roles <role1, role2, role3...>

3.  Aggiungere o rimuovere i membri dal gruppo di protezione universale esterno utilizzando Utenti e computer di Active Directory su un computer nella foresta esterna di Active Directory.

Con questo esempio viene effettuato quanto segue:

  - Vengono recuperate le credenziali per la foresta esterna di Active Directory users.contoso.com. Queste credenziali vengono utilizzate per collegarsi al controller di dominio DC01.users.contoso.com nella foresta esterna.

  - Crea un gruppo legato al ruolo chiamato Gruppo di ruoli conformi Executives nella foresta risorse in cui Exchange 2013 è installato.

  - Collega il nuovo gruppo di ruolo al gruppo di protezione universale degli amministratori conformi Executives nella foresta Active Directory esterna di users.contoso.com.

  - Assegnare le Regole di trasporto e le regole per la gestione dell'inserimento del Journal al nuovo gruppo legato al ruolo con ambito destinatario dell'unità organizzativa Executives.

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
    New-RoleGroup "Executives Compliance Role Group" -LinkedForeignGroup "Executives Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope "Executives OU" -Roles "Transport Rules", "Journaling"

Per ulteriori informazioni sugli ambiti di gestione, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

## Modifica del gruppo di protezione universale in un gruppo legato al ruolo

## Modifica del gruppo di protezione universale esterno in un gruppo di ruolo collegato tramite Shell

Per modificare il gruppo di protezione universale esterno associato a un gruppo di ruolo collegato, procedere come segue:

1.  Archiviare le credenziali della foresta esterna di Active Directory in una variabile.
    
    ```powershell
$ForeignCredential = Get-Credential
```

2.  Modificare il gruppo di protezione universale nel gruppo legato al ruolo esistente utilizzando la seguente sintassi.
    
        Set-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential 

Con questo esempio viene effettuato quanto segue:

  - Vengono recuperate le credenziali per la foresta esterna di Active Directory users.contoso.com. Queste credenziali vengono utilizzate per collegarsi al controller di dominio DC01.users.contoso.com nella foresta esterna.

  - Consente di cambiare il gruppo di protezione universale esterno del gruppo di ruolo Compliance Role Group in Regulatory Compliance Officers.

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
    Set-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Regulatory Compliance Officers" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential


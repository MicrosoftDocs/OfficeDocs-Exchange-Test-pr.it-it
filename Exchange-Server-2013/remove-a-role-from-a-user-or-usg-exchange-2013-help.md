---
title: 'Rimozione ruolo da utente/gruppo protezione universale: Exchange 2013 Help'
TOCTitle: Rimozione di un ruolo da un utente o gruppo di protezione universale
ms:assetid: df3510ef-e0c2-4d3c-81b0-7dc3e70c01a0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351196(v=EXCHG.150)
ms:contentKeyID: 50481864
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimozione di un ruolo da un utente o gruppo di protezione universale

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-02_

Le assegnazioni del ruolo di gestione consentono di assegnare un ruolo di gestione a un utente o a un gruppo di protezione universale (USG, Universal Security Group). Se si elimina un'assegnazione di ruolo, gli utenti assegnati al ruolo non avranno più accesso ai cmdlet disponibili per quel ruolo. Per ulteriori informazioni sulle assegnazioni del ruolo di gestione in Microsoft Exchange Server 2013, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative ai ruoli, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Assegnazioni ruolo" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Eliminazione di un'assegnazione del ruolo di gestione

Se si conosce il nome dell'assegnazione di ruolo da rimuovere, utilizzare la sintassi seguente:

```powershell
Remove-ManagementRoleAssignment <assignment name>
```

Ad esempio, per rimuovere l'assegnazione del ruolo "Tier 2 Help Desk Assignment", eseguire il comando riportato di seguito:

```powershell
Remove-ManagementRoleAssignment "Tier 2 Help Desk Assignment"
```

Se non si conosce il nome dell'assegnazione di ruolo da rimuovere, utilizzare la sintassi seguente:

```powershell
    Get-ManagementRoleAssignment -RoleAssignee <user or USG> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment 
```

Se ad esempio si desidera rimuovere dall'utente Davids l'assegnazione del ruolo regolare per Mail Recipients, utilizzare il comando seguente:

```powershell
    Get-ManagementRoleAssignment -RoleAssignee davids -Role "Mail Recipients" -Delegating $false | Remove-ManagementRoleAssignment
```

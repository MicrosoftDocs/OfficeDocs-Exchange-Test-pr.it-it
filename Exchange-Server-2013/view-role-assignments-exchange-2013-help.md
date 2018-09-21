---
title: 'Visualizzare le assegnazioni di ruolo: Exchange 2013 Help'
TOCTitle: Visualizzare le assegnazioni di ruolo
ms:assetid: 0be4def9-af6d-476a-9c97-7155ae11b587
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335086(v=EXCHG.150)
ms:contentKeyID: 50479978
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizzare le assegnazioni di ruolo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

Le assegnazioni del ruolo di gestione consentono di assegnare un ruolo di gestione a un assegnatario di ruolo. Per ulteriori informazioni sulle assegnazioni del ruolo di gestione in Microsoft Exchange Server 2013, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative ai ruoli, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Assegnazioni ruolo" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Questo argomento utilizza il pipelining e il cmdlet **Format-List**. Per ulteriori informazioni su questi concetti, vedere i seguenti argomenti:
    
      - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))
    
      - [Utilizzo dell'output del comando](working-with-command-output-exchange-2013-help.md)

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Visualizzazione di un elenco di tutte le assegnazioni di ruolo

È possibile visualizzare un elenco di tutte le assegnazioni di ruolo configurate per l'organizzazione eseguendo il cmdlet **Get-ManagementRoleAssignment**. Se si desidera recuperare un elenco delle assegnazioni di ruolo corrispondenti a una stringa parziale specificata, utilizzare i caratteri jolly (\*). In questo esempio viene recuperato un elenco di tutte le assegnazioni di ruolo che iniziano con la stringa "Tier 1".

    Get-ManagementRoleAssignment "Tier 1*"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Visualizzazione dei dettagli di una specifica assegnazione di ruolo

È possibile visualizzare i dettagli di un'assegnazione di ruolo eseguendo il piping dei risultati del cmdlet **Get-ManagementRoleAssignment** al cmdlet **Format-List**. Utilizzare la seguente sintassi.

```powershell
Get-ManagementRoleAssignment <assignment name> | Format-List
```

In questo esempio vengono recuperati i dettagli dell'assegnazione di ruolo Help Desk Assignment.

```powershell
Get-ManagementRoleAssignment "Help Desk Assignment" | Format-List
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Visualizzazione dell'elenco delle assegnazioni di ruolo associate a uno specifico assegnatario di ruolo

Per visualizzare un elenco delle assegnazioni di ruolo associate a un gruppo del ruolo di gestione, un ruolo o un criterio di assegnazione dei ruoli o associate a un utente o un gruppo di protezione universale, utilizzare la seguente sintassi.

```powershell
Get-ManagementRoleAssignment -RoleAssignee <role assignee name>
```

In questo esempio vengono recuperate tutte le assegnazioni di ruolo associate al gruppo di ruolo Server Management.

```powershell
Get-ManagementRoleAssignment -RoleAssignee "Server Management"
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Visualizzazione delle assegnazioni di ruolo associate a uno specifico ruolo

Per ogni ruolo possono esistere più assegnazioni di ruolo. È possibile utilizzare il cmdlet **Get-ManagementRoleAssigment** per visualizzare un elenco delle assegnazioni di ruolo associate a uno specifico ruolo.

Per visualizzare un elenco delle assegnazioni di ruolo associate a uno specifico ruolo, utilizzare la seguente sintassi.

```powershell
Get-ManagementRoleAssignment -Role <role name>
```

In questo esempio vengono recuperate tutte le assegnazioni di ruolo associate al ruolo Mail Recipients.

```powershell
Get-ManagementRoleAssignment -Role "Mail Recipients"
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Visualizzazione di un elenco delle assegnazioni di ruolo che utilizzano uno specifico ambito predefinito

Per visualizzare un elenco delle assegnazioni di ruolo che utilizzano uno specifico ambito predefinito, utilizzare la seguente sintassi.

    Get-ManagementRoleAssignment -RecipientWriteScope < MyGAL | MyDistributionGroups | Organization | Self | CustomRecipientScope | ExecutiveRecipientScope >

In questo esempio vengono recuperate tutte le assegnazioni di ruolo che utilizzano l'ambito predefinito Organization.

```powershell
Get-ManagementRoleAssignment -RecipientWriteScope Organization
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Visualizzazione di un elenco delle assegnazioni di ruolo inserite nell'ambito di una specifica unità organizzativa

Per visualizzare un elenco delle assegnazioni di ruolo inserite nell'ambito di una specifica unità organizzativa, utilizzare la seguente sintassi.

```powershell
Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope <OU>
```

In questo esempio vengono recuperate tutte le assegnazioni di ruolo inserite nell'ambito dell'unità organizzativa North America\\Engineering\\Users nel dominio contoso.com.

    Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope "contoso.com/North America/Engineering/Users"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Visualizzazione di un elenco delle assegnazioni che utilizzano uno specifico ambito personalizzato

Per visualizzare un elenco delle assegnazioni di ruolo che utilizzano uno specifico ambito personalizzato, è necessario innanzitutto determinare se l'ambito indica un ambito dei destinatari, un ambito della configurazione, un ambito esclusivo dei destinatari o un ambito esclusivo della configurazione. Ogni tipo di ambito utilizza un parametro diverso per il cmdlet **Get-ManagementRoleAssignment**. Di seguito viene elencato ogni ambito e il relativo parametro associato:

  - **Ambiti destinatari**   *CustomRecipientWriteScope*

  - **Ambiti di configurazione**   *CustomConfigWriteScope*

  - **Ambiti esclusivi dei destinatari**   *ExclusiveRecipientWriteScope*

  - **Ambiti esclusivi di configurazione**   *ExclusiveConfigWriteScope*

La sintassi per ogni parametro è lo stessa. Specificare il nome dell'ambito con il parametro corrispondente al tipo di ambito.

In questo esempio vengono recuperate tutte le assegnazioni di ruolo che utilizzano l'ambito dei destinatari Vancouver Recipients.

```powershell
Get-ManagementRoleAssignment -CustomRecipientWriteScope "Vancouver Recipients"
```

In questo esempio vengono recuperate tutte le assegnazioni di ruolo che utilizzano l'ambito esclusivo di configurazione Seattle AD Site.

```powershell
Get-ManagementRoleAssignment -ExclusiveConfigWriteScope "Seattle AD Site"
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Visualizzazione di un elenco degli ambiti esclusivi o regolari

Per visualizzare un elenco delle assegnazioni di ruolo esclusive o regolari, utilizzare la seguente sintassi.

```powershell
Get-ManagementRoleAssignment -Exclusive < $True | $False >
```

Ad esempio, per visualizzare un elenco degli ambiti esclusivi, eseguire il seguente comando:

```powershell
Get-ManagementRoleAssignment -Exclusive $True
```

In questo esempio viene recuperato un elenco di ambiti regolari senza alcun ambito esclusivo.

```powershell
Get-ManagementRoleAssignment -Exclusive $False
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Visualizzazione degli utenti che possono modificare un destinatario o un server specifico

Per visualizzare un elenco delle assegnazioni di ruolo che possono modificare un destinatario o un server specifico, utilizzare i parametri *WritableRecipient* e *WritableServer*. Specificare il nome del destinatario con il parametro *WritableRecipient* e il nome del server con il parametro *WritableServer*.

In questo esempio viene recuperato un elenco delle assegnazioni di ruolo che possono modificare il destinatario Brian.

```powershell
Get-ManagementRoleAssignment -WritableRecipient "Brian"
```

I parametri *WritableRecipient* e *WritableServer* possono essere combinati con altri parametri, come il parametro *RoleAssignee* e l'opzione *GetEffectiveUsers* per rifinire la query ed espandere i gruppi di ruolo o i gruppi di protezione universale. In questo esempio vengono recuperati tutti gli utenti che possono modificare il server EX02 e a cui viene assegnato il gruppo di ruolo Server Management.

    Get-ManagementRoleAssignment -WritableServer EX02 -RoleAssignee "Server Management" -GetEffectiveUsers

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Visualizzazione degli utenti che ricevono le autorizzazioni da un'assegnazione tramite un gruppo di ruolo o un gruppo di protezione universale

Per visualizzare un elenco degli utenti che ricevono le autorizzazioni da un'assegnazione di ruolo, utilizzare la seguente sintassi.

```powershell
Get-ManagementRoleAssignment <assignment name> -GetEffectiveUsers
```

In questo esempio, viene recuperato un elenco degli utenti per l'assegnazione di ruolo Help Desk Assignment.

```powershell
Get-ManagementRoleAssignment "Help Desk Assignment" -GetEffectiveUsers
```

Anche l'opzione *GetEffectiveUsers* può essere combinata con altri parametri del cmdlet **Get-ManagementRoleAssignment** per espandere i gruppi di ruolo e i gruppi di protezione universale a cui vengono associate le assegnazioni di ruolo. Per un esempio di come l'opzione *GetEffectiveUsers* venga utilizzata con altri parametri, vedere "Visualizzazione degli utenti che possono modificare un destinatario o un server specifico" di questo argomento.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Visualizzazione di un elenco delle assegnazioni di ruolo abilitate o disabilitate

Per visualizzare un elenco delle assegnazioni di ruolo abilitate o disabilitate, utilizzare la seguente sintassi.

```powershell
Get-ManagementRoleAssignment -Enabled < $True | $False >
```

In questo esempio viene recuperato un elenco delle assegnazioni di ruolo disabilitate.

```powershell
Get-ManagementRoleAssignment -Enabled $False
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).


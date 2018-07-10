---
title: "Modificare un'assegnazione di ruolo: Exchange 2013 Help"
TOCTitle: Modificare un'assegnazione di ruolo
ms:assetid: 0fa77efc-e393-461f-b3c0-232cc56cee85
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335096(v=EXCHG.150)
ms:contentKeyID: 50480052
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare un'assegnazione di ruolo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

Le assegnazioni del ruolo di gestione consentono di assegnare un ruolo di gestione a un assegnatario di ruolo. Modificando l'assegnazione di ruolo, è possibile controllare gli oggetti modificabili dagli assegnatari associati a un ruolo. Gli ambiti del ruolo di gestione, applicati alle assegnazioni di ruolo, sostituiscono l'ambito di scrittura implicito del ruolo. L'ambito di lettura implicito del ruolo viene comunque applicato. Gli ambiti applicati non possono restituire oggetti esterni all'ambito di lettura implicito del ruolo.

Per ulteriori informazioni sugli ambiti e le assegnazioni del ruolo di gestione in Microsoft Exchange Server 2013, vedere i seguenti argomenti:

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

Per informazioni sulle altre attività di gestione relative alle assegnazioni di ruolo, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Assegnazioni ruolo" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Abilitazione o disabilitazione di un'assegnazione di ruolo tramite Shell

Le assegnazioni di ruolo vengono abilitate per impostazione predefinita: il ruolo viene applicato all'assegnatario a cui viene associato il ruolo. Se un'assegnazione di ruolo viene disabilitata, il ruolo associato non viene applicato all'assegnatario del ruolo.

Per abilitare un'assegnazione di ruolo, utilizzare la seguente sintassi.

    Set-ManagementRoleAssignment <role assignment> -Enabled $true

Per disabilitare un'assegnazione di ruolo, utilizzare la seguente sintassi.

    Set-ManagementRoleAssignment <role assignment> -Enabled $false

In questo esempio viene disabilitata l'assegnazione di ruolo Help Desk Assignment.

    Set-ManagementRoleAssignment "Help Desk Assignment" -Enabled $false

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335173\(v=exchg.150\)).

## Modifica di un ruolo di gestione o di un assegnatario per un'assegnazione di ruolo tramite Shell

Non è possibile modificare il ruolo di gestione o l'assegnatario del ruolo specificato per un'assegnazione di ruolo. Se si desidera associare un'assegnazione di ruolo a un altro ruolo o assegnatario, è necessario creare una nuova assegnazione di ruolo ed eliminare l'assegnazione precedente. Per ulteriori informazioni su come aggiungere e rimuovere le assegnazione di ruolo, vedere i seguenti argomenti:

  - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [Rimozione di un ruolo da un utente o gruppo di protezione universale](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

Se le assegnazioni vengono create direttamente per un utente o un gruppo di protezione universale, si consiglia di utilizzare i gruppi del ruolo di gestione e i criteri di assegnazione del ruolo di gestione. I gruppi di ruolo e i criteri di assegnazione consentono di semplificare il modello delle autorizzazioni e di ridurre il numero delle assegnazioni di ruolo da gestire. Per ulteriori informazioni, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

## Modifica di un ambito relativo predefinito di un'assegnazione di ruolo tramite Shell

È possibile modificare o aggiungere un ambito relativo predefinito di un assegnazione di ruolo. Se si aggiunge o si modifica un ambito predefinito, tutti gli ambiti dei destinatari precedentemente specificati vengono rimossi dall'assegnazione di ruolo. Per un elenco degli ambiti predefiniti e le relative descrizioni, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

Per modificare o aggiungere un ambito predefinito di un'assegnazione di ruolo, utilizzare la seguente sintassi.

    Set-ManagementRoleAssignment <assignment name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

In questo esempio viene modificato l'ambito predefinito dell'assegnazione di ruolo John's Assignment in MyDistributionGroups.

    Set-ManagementRoleAssignment "John's Assignment" - RecipientRelativeWriteScope MyDistributionGroups

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335173\(v=exchg.150\)).

## Modifica di un ambito di filtro dei destinatari per un'assegnazione di ruolo tramite Shell

È possibile specificare un nuovo ambito basato sul filtro dei destinatari o modificare l'ambito basato sul filtro dei destinatari applicato all'assegnazione di ruolo. Se si aggiunge un ambito di filtro dei destinatari, tutti gli ambiti dei destinatari precedentemente definiti vengono rimossi dall'assegnazione di ruolo.

Per specificare un nuovo ambito basato sul filtro dei destinatari o sostituirne uno esistente, utilizzare la seguente sintassi.

    Set-ManagementRoleAssignment <assignment name> -CustomRecipientWriteScope <role scope name>

In questo esempio viene aggiunto o modificato l'ambito basato sul filtro dei destinatari in Redmond Recipients.

    Set-ManagementRoleAssignment "Redmond Recipient Administrators Assignment" -CustomRecipientWriteScope "Redmond Recipients"

Se si desidera mantenere lo stesso ambito basato sul filtro dei destinatari applicato all'assegnazione di ruolo, modificando il filtro dei destinatari utilizzato per trovare una corrispondenza tra gli oggetti destinatario, è necessario modificare il filtro dei destinatari nell'ambito stesso. Per ulteriori informazioni sulla modifica degli ambiti, vedere [Modificare un ambito di ruolo](change-a-role-scope-exchange-2013-help.md).

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335173\(v=exchg.150\)).

## Modifica del filtro server o dell'ambito di configurazione basato su elenco per un'assegnazione di ruolo tramite Shell

È possibile specificare un nuovo filtro server o un nuovo ambito di configurazione basato su elenco o modificare l'ambito applicato all'assegnazione di ruolo. Se si aggiunge o si modifica un ambito di configurazione, tutti gli ambiti di configurazione precedentemente specificati vengono rimossi dall'assegnazione di ruolo.

Per specificare un nuovo ambito di configurazione o sostituirne uno esistente, utilizzare la seguente sintassi.

    Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>

In questo esempio viene aggiunto o modificato l'ambito di configurazione in Redmond Servers.

    Set-ManagementRoleAssignment "Redmond Administrators Assignment" -CustomConfigWriteScope "Redmond Servers"

Se si desidera mantenere lo stesso ambito di configurazione applicato all'assegnazione di ruolo, modificando il filtro server o l'elenco server dell'ambito, è necessario modificare l'ambito di configurazione stesso. Per ulteriori informazioni sulla modifica degli ambiti, vedere [Modificare un ambito di ruolo](change-a-role-scope-exchange-2013-help.md).

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335173\(v=exchg.150\)).

## Modifica del filtro database o dell'ambito di configurazione basato su elenco in un'assegnazione di ruolo tramite Shell

È possibile specificare un nuovo filtro database o un nuovo ambito di configurazione basato su elenco oppure modificare l'ambito già applicato all'assegnazione di ruolo. Se si aggiunge o si modifica un ambito di configurazione, tutti gli ambiti di configurazione precedentemente specificati verranno rimossi dall'assegnazione di ruolo.

Per specificare un nuovo ambito di configurazione o sostituirne uno esistente, utilizzare la seguente sintassi.

    Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>

In questo esempio viene aggiunto o modificato l'ambito di configurazione in Redmond Databases.

    Set-ManagementRoleAssignment "Redmond Database Admins" -CustomConfigWriteScope "Redmond Databases"

Se si desidera mantenere l'ambito di configurazione già applicato all'assegnazione di ruolo modificandone però il filtro database o l'elenco database, è necessario modificare l'ambito di configurazione stesso. Per ulteriori informazioni su come modificare un ambito, vedere [Modificare un ambito di ruolo](change-a-role-scope-exchange-2013-help.md).

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335173\(v=exchg.150\)).

## Modifica dell'unità organizzativa per un'assegnazione di ruolo tramite Shell

È possibile aggiungere una nuova unità organizzativa o modificarne una già applicata all'assegnazione di ruolo. Se si specifica una nuova unità organizzativa, tutti gli ambiti dei destinatari precedentemente specificati vengono rimossi dall'assegnazione di ruolo.

Per modificare o aggiungere una nuova unità organizzativa per un'assegnazione di ruolo, utilizzare la seguente sintassi.

    Set-ManagementRoleAssignment <assignment name> -RecipientOrganizationalUnitScope <OU>

In questo esempio viene aggiunta l'unità organizzativa Engineering\\Users nel domino contoso.com per l'assegnazione di ruolo Engineering Help Desk.

    Set-ManagementRoleAssignment "Engineering Help Desk" -RecipientOrganizationalUnitScope contoso.com/Engineering/Users

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335173\(v=exchg.150\)).

## Modifica di un ambito esclusivo dei destinatari o di configurazione tramite Shell

Per modificare ambiti di configurazione o destinatari esclusivi, eseguire le procedure descritte nelle sezioni precedenti di questo argomento, ossia "Modifica di un ambito di filtro dei destinatari per un'assegnazione di ruolo tramite Shell", "Modifica del filtro server o dell'ambito di configurazione basato su elenco per un'assegnazione di ruolo tramite Shell" e "Modifica del filtro database o dell'ambito di configurazione basato su elenco in un'assegnazione di ruolo trmiate Shell". L'unica differenza è che quando si modifica un ambito esclusivo, è necessario specificare i seguenti parametri esclusivi relativi a un ambito esclusivo dei destinatari o a un ambito esclusivo di configurazione:

  - **Ambiti esclusivi dei destinatari**   Utilizzare il parametro *ExclusiveRecipientWriteScope*, invece del parametro *CustomRecipientWriteScope*.

  - **Ambiti di configurazione server e database esclusivi**   Utilizzare il parametro *ExclusiveConfigWriteScope* invece del parametro *CustomConfigWriteScope*.

Come per gli ambiti regolari dei destinatari e di configurazione, se si aggiunge o si modifica un ambito esclusivo, tutti gli ambiti dei destinatari o di configurazione precedentemente definiti vengono sostituiti.

In questo esempio viene modificato un ambito esclusivo di scrittura dei destinatari.

    Set-ManagementRoleAssignment "Exclusive Executive Users" -ExclusiveRecipientWriteScope "Exclusive Executives"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335173\(v=exchg.150\)).


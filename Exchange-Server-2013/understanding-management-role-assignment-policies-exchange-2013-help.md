---
title: 'Info. su criteri di assegnazione di ruolo di gestione: Exchange 2013 Help'
TOCTitle: Informazioni sui criteri di assegnazione di ruolo di gestione
ms:assetid: 25913e43-326a-4371-90b5-021a35f100fe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638100(v=EXCHG.150)
ms:contentKeyID: 50480268
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Informazioni sui criteri di assegnazione di ruolo di gestione

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Un *criterio di assegnazione del ruolo di gestione* indica un insieme di uno o più ruoli di gestione che consente agli utenti finali di gestire la configurazione della cassetta postale e del gruppo di distribuzione di Microsoft Exchange Server 2013. I criteri di assegnazione dei ruoli, che fanno parte del modello di autorizzazioni Controllo di accesso basato sui ruoli (RBAC) in Exchange 2013, consentono di controllare le specifiche impostazioni della cassetta postale e del gruppo di distribuzione che gli utenti finali possono modificare. Gruppi diversi di utenti possono disporre di criteri di assegnazione dei ruoli specializzati.


> [!NOTE]
> Questo argomento è incentrato sulla funzionalità RBAC avanzata. Se si desidera gestire le autorizzazioni di base di Exchange 2013, quale l'utilizzo dell'interfaccia di amministrazione di Exchange (EAC) per aggiungere membri ai gruppi di ruoli oppure per rimuoverli da tali gruppi, per creare e modificare gruppi di ruoli oppure per creare e modificare i criteri di assegnazione dei ruoli, vedere <A href="permissions-exchange-2013-help.md">Autorizzazioni</A>.



Per ulteriori informazioni su RBAC, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

**Sommario**

Role assignment policy layers

Default and explicit role assignment policies

Using role assignment policies

Role assignment policy management

## Livelli di criteri di assegnazione dei ruoli

Nell'elenco seguente, sono riportati i livelli che costituiscono il modello del criterio di assegnazione dei ruoli:

  - **Cassetta postale**   Alle cassette postali viene assegnato un singolo criterio di assegnazione dei ruoli. Quando a una cassetta postale viene assegnato un criterio di assegnazione dei ruoli, alla cassetta postale vengono applicate le assegnazioni tra i ruoli di gestione e un criterio di assegnazione. Alla cassetta postale vengono concesse tutte le autorizzazioni fornite dai ruoli di gestione.

  - **Criterio di assegnazione del ruolo di gestione**   Il *criterio di assegnazione del ruolo di gestione* è uno speciale oggetto di Exchange 2013. Gli utenti vengono associati a un criterio di assegnazione dei ruoli quando le cassette postali vengono create o se si modifica il criterio per una cassetta postale. A ciò si assegnano anche i ruoli di gestione degli utenti finali. La combinazione di tutti i ruoli per un criterio di assegnazione dei ruoli consente di definire cosa può gestire l'utente nella cassetta postale o nel gruppo di distribuzione.

  - **Assegnazione del ruolo di gestione**   Un'*assegnazione del ruolo di gestione* indica il collegamento tra un ruolo di gestione e un criterio di assegnazione dei ruoli. L'assegnazione di un ruolo di gestione a un criterio di assegnazione dei ruoli consente di utilizzare i cmdlet e i parametri definiti nel ruolo di gestione. Quando si crea un'assegnazione di ruolo tra un criterio di assegnazione dei ruoli e un ruolo di gestione, non è possibile specificare alcun ambito. L'ambito applicato dall'assegnazione si basa sul ruolo di gestione ed è `Self` o `MyGAL`. Per ulteriori informazioni, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

  - **Ruolo di gestione**   Un *ruolo di gestione* è un contenitore per un raggruppamento di voci del ruolo di gestione. I ruoli vengono utilizzati per definire le specifiche attività che un utente può eseguire sulla cassetta postale o sui gruppi di distribuzione. Una *voce del ruolo di gestione* indica un cmdlet, uno script o una determinata autorizzazione che consente a ogni specifica attività di un ruolo di gestione di essere eseguita. È possibile utilizzare solo i ruoli di gestione degli utenti finali con i criteri di assegnazione dei ruoli. Per ulteriori informazioni, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

  - **Voce del ruolo di gestione**   Le voci del ruolo di gestione indicano le singole voci di un ruolo di gestione che determinano i cmdlet e i parametri disponibili per il ruolo o per il gruppo di ruolo. Ogni voce di ruolo è costituita da un unico cmdlet e dai parametri accessibili dal ruolo di gestione.

Nella seguente figura vengono illustrati tutti i livelli dei criteri di assegnazione dei ruoli dell'elenco precedente e come ogni livello si riferisca agli altri.

**Modello dei criteri di assegnazione del ruolo di gestione**

![Relazioni del modello di assegnazione ruolo](images/Dd638100.7f7c11ca-0d61-464d-98a3-a9991ec811b5(EXCHG.150).jpg "Relazioni del modello di assegnazione ruolo")

Per ulteriori informazioni sui ruoli di gestione, sulle assegnazioni dei ruoli e sugli ambiti, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

## Criteri di assegnazione dei ruoli predefiniti ed espliciti

Nelle seguenti sezioni vengono descritti i due tipi di criteri di assegnazione dei ruoli in Exchange 2013.

## Criterio di assegnazione dei ruoli predefinito

Un criterio predefinito di assegnazione dei ruoli indica un unico criterio assegnato alla cassetta postale quando questa viene creata o spostata in un server che esegue Exchange 2013 e non è stato fornito un criterio di assegnazione dei ruoli utilizzando il parametro *RoleAssignmentPolicy* sui cmdlet **New-Mailbox** o **Enable-Mailbox**.

Exchange 2013 include un criterio predefinito di assegnazione dei ruoli che fornisce agli utenti finali le autorizzazioni più comunemente utilizzate. È possibile modificare le autorizzazioni predefinite per il criterio predefinito di assegnazione dei ruoli aggiungendo o rimuovendo i ruoli di gestione da esso.

Se si desidera sostituire il criterio predefinito di assegnazione dei ruoli incorporato con un altro criterio, è possibile utilizzare il cmdlet **Set-RoleAssignmentPolicy** per selezionarne uno nuovo. Quando si esegue questa operazione, a tutte le nuove cassette postali viene assegnato il criterio di assegnazione dei ruoli specificato per impostazione predefinita, se non si specifica esplicitamente un criterio.

Quando si modifica il criterio predefinito di assegnazione dei ruoli, alle cassette postali a cui è stato assegnato il criterio non viene assegnato automaticamente il nuovo criterio. Se si desidera aggiornare le cassette postali create precedentemente per utilizzare il criterio di assegnazione dei ruoli impostato come predefinito, è necessario utilizzare il cmdlet **Set-Mailbox** per eseguire questa operazione.

## Criterio esplicito di assegnazione dei ruoli

Un criterio esplicito di assegnazione dei ruoli indica un criterio assegnato manualmente a una cassetta postale utilizzando il parametro *RoleAssignmentPolicy* sui cmdlet **New-Mailbox**, **Set-Mailbox** o **Enable-Mailbox**. Quando si associa un criterio esplicito di assegnazione dei ruoli, il nuovo criterio diventa immediatamente effettivo e sostituisce il criterio assegnato precedentemente.

## Utilizzo dei criteri di assegnazione dei ruoli

I criteri di assegnazione dei ruoli consentono di adattare le autorizzazioni in base alle esigenze aziendali che gli utenti sono in grado di configurare. Se il criterio predefinito di assegnazione dei ruoli soddisfa le esigenze, la personalizzazione non è necessaria. Tuttavia, se si dispone di molti gruppi utenti diversi, è possibile creare i criteri di assegnazione dei ruoli per ciascuno di essi.

Il criterio predefinito di assegnazione dei ruoli in uso deve contenere le autorizzazioni applicate all'amplissima gamma di utenti. Quindi, creare i criteri di assegnazione dei ruoli per ogni gruppo utenti specializzato e adattare questi criteri per concedere loro autorizzazioni più o meno restrittive. Quando si organizzano in questo modo i criteri di assegnazione dei ruoli, si riduce la complessità solo assegnando esplicitamente i criteri agli utenti specializzati, mentre la maggior parte degli utenti riceve le autorizzazioni più comuni fornite dal criterio predefinito.

Una cassetta postale può disporre di un solo criterio di assegnazione dei ruoli. A tutti gli utenti, inclusi gli amministratori e gli utenti esperti, viene assegnato un unico criterio di assegnazione dei ruoli. Se si desidera che un utente disponga di un insieme diverso di autorizzazioni, è necessario assegnare alla cassetta postale di tale utente un altro criterio di assegnazione dei ruoli con le autorizzazioni necessarie.

## Gestione dei criteri di assegnazione dei ruoli

Per aggiungere un nuovo criterio di assegnazione dei ruoli, crearne prima uno e decidere se sarà il criterio predefinito. Una volta creato il criterio di assegnazione dei ruoli, si assegnano i ruoli di gestione al criterio e poi si assegna il criterio alle cassette postali. In seguito, è possibile scegliere di aggiungere o rimuovere i ruoli di gestione o scegliere un diverso criterio di assegnazione dei ruoli come predefinito.

Nella seguente tabella vengono elencati il livello dei criteri di assegnazione dei ruoli e gli argomenti relativi alle procedure utilizzabili per la gestione di ogni livello.

### Argomenti relativi alla gestione dei criteri di assegnazione dei ruoli

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Livello del modello dei criteri di assegnazione dei ruoli</th>
<th>Argomenti relativi alla gestione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cassetta postale</p></td>
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">Gestire le cassette postali degli utenti</a></p>
<p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Modificare il criterio di assegnazione di una cassetta postale</a></p></td>
</tr>
<tr class="even">
<td><p>Criterio di assegnazione dei ruoli</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Gestire i criteri di assegnazione dei ruoli</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Ruoli di gestione e assegnazioni</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Gestire i criteri di assegnazione dei ruoli</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Voci del ruolo di gestione</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">Aggiungere una voce di ruolo a un ruolo</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">Modificare una voce di ruolo</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">Rimuovere una voce di ruolo da un ruolo</a></p>

> [!NOTE]
> La modifica delle voci del ruolo di gestione nei ruoli di gestione di un criterio di assegnazione dei ruoli è un'attività avanzata e in genere non è necessaria. È possibile, invece, utilizzare un ruolo di gestione preesistente che si adatta alle esigenze. Per ulteriori informazioni, vedere <A href="built-in-role-groups-exchange-2013-help.md">Gruppi di ruoli incorporati</A>.


</td>
</tr>
</tbody>
</table>


---
title: 'Installazione delegata: Exchange 2013 Help'
TOCTitle: Installazione delegata
ms:assetid: 49362059-e53f-4135-ad2b-9edfbfff9a1e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876881(v=EXCHG.150)
ms:contentKeyID: 50480527
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Installazione delegata

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Configurazione delegata Il gruppo dei ruoli di gestione è uno dei numerosi gruppi incorporati che costituiscono il modello delle autorizzazioni del controllo degli accessi in base al ruolo in Microsoft Exchange Server 2013. Ai gruppi di ruoli vengono assegnati uno o più ruoli di gestione che includono le autorizzazioni necessarie per eseguire un determinato gruppo di attività. I membri di un gruppo di ruoli possono accedere ai ruoli di gestione assegnati a tale gruppo. Per altre informazioni sui gruppi di ruoli, vedere [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md).

Gli amministratori membri del gruppo di ruolo Configurazione delegata possono distribuire i server Exchange 2013 precedentemente sottoposti a provisioning da un membro del gruppo di ruolo Gestione organizzazione.

I membri del gruppo di ruolo Configurazione delegata possono solamente distribuire i server Exchange 2013. Non possono gestire il server dopo la distribuzione. Per gestire un server dopo la distribuzione, l'utente deve essere membro del gruppo di ruolo [Server Management](server-management-exchange-2013-help.md).

Per ulteriori informazioni su RBAC, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

## Appartenenza ai gruppi di ruolo

Se si desidera aggiungere o rimuovere membri in questo gruppo di ruoli, vedere [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).

Per impostazione predefinita, solo i membri del gruppo di ruoli Gestione organizzazione possono aggiungere o rimuovere membri da questo gruppo di ruoli. Per altre informazioni sull'aggiunta di ulteriori delegati al gruppo di ruoli, vedere la sezione "Aggiungere o rimuovere un delegato in un gruppo di ruoli" in [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

È possibile utilizzare il seguente comando per visualizzare un elenco degli utenti o dei gruppi di protezione universali membri di questo gruppo di ruolo.

    Get-RoleGroupMember "Delegated Setup"

Per ulteriori informazioni sui membri di un gruppo di ruolo, vedere [View the members of a role group](manage-role-group-members-exchange-2013-help.md) in [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).

## Personalizzazione dei gruppi di ruolo

Questo gruppo di ruoli viene assegnato ai ruoli di gestione per impostazione predefinita. I ruoli inclusi sono elencati nella sezione "Ruoli di gestione assegnati a questo gruppo di ruoli". È possibile aggiungere o rimuovere le assegnazioni dei ruoli da questo gruppo in base alle esigenze della propria organizzazione.

I gruppi di ruoli forniti con Exchange 2013 sono stati ideati per poter svolgere attività più dettagliate. Quando si assegnano i ruoli ad un gruppo di ruoli, i membri di quel gruppo sono abilitati ad eseguire le attività associate al ruolo. Ad esempio, il ruolo di inserimento nel journal consente la gestione dell'agente di inserimento nel journal e delle relative regole. Per altre informazioni sull'assegnazione dei ruoli ai gruppi di ruoli, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

I ruoli assegnati a questo gruppo di ruoli vengono assegnati agli ambiti di gestione predefiniti. Gli ambiti di gestione determinano quali oggetti di Exchange possono essere visualizzati o modificati dai membri di un gruppo di ruoli. È possibile modificare gli ambiti associati alle assegnazioni tra i ruoli e i gruppi di ruoli. Questo può essere necessario, ad esempio, se si desidera che solo i membri di un gruppo di ruoli siano in grado di modificare i destinatari che sono in un'unità organizzativa specifica o in una posizione specifica. Per altre informazioni sugli ambiti di gestione, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

Per altre informazioni su come personalizzare questo gruppo di ruoli, vedere gli argomenti seguenti:

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md)

Se si desidera creare un gruppo di ruoli e assegnare al nuovo gruppo alcuni dei ruoli assegnati a questo gruppo di ruoli, vedere la sezione "Creare un gruppo di ruoli" in [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

## Autorizzazioni aggiuntive

Le autorizzazioni concesse ai membri del gruppo di ruolo Configurazione delegata sono determinate principalmente dai ruoli di gestione assegnati al gruppo di ruolo. Tuttavia, non tutte le attività che devono essere eseguite sono coperte dai ruoli di gestione. Ciò accade perché alcune attività si verificano all'esterno degli strumenti di gestione di Exchange e quindi non viene applicato il modello di autorizzazioni RBAC. Per queste attività, le autorizzazioni sono fornite per mezzo dell'aggiunta del gruppo di ruolo Configurazione delegata agli elenchi di controllo di accesso (ACL) di alcuni oggetti di Active Directory.

Per la seguente attività le autorizzazioni vengono concesse per mezzo degli elenchi ACL degli oggetti Active Directory e non per mezzo dei ruoli di gestione assegnati al gruppo di ruolo Configurazione delegata:

  - Distribuzione dei server precedentemente sottoposti a provisioning da un membro del gruppo di ruolo Gestione organizzazione.

## Ruoli di gestione assegnati a questo gruppo di ruolo

La tabella seguente elenca tutti i ruoli di gestione assegnati a questo gruppo di ruoli e gli attributi di ciascuna assegnazione di ruolo:

  - **Assegnazione regolare**   Consente ai membri del gruppo di ruoli di accedere alle voci del ruolo di gestione rese disponibili dal ruolo di gestione associato.

  - **Assegnazione di delega**   Consente ai membri del gruppo di ruoli di assegnare il ruolo specificato ad altri gruppi di ruoli, altri criteri per l'assegnazione dei ruoli, altri utenti e altri gruppi di protezione universale.

  - **Ambito di lettura del destinatario**   Determina a quali membri oggetti destinatario del gruppo di ruoli è consentito leggere Active Directory.

  - **Ambito di scrittura del destinatario**   Determina a quali membri oggetti destinatario del gruppo di ruoli è consentito modificare Active Directory.

  - **Ambito di lettura della configurazione**   Determina a quali membri oggetti della configurazione e del server del gruppo di ruoli è consentito leggere Active Directory.

  - **Ambito di scrittura di configurazione**   Determina a quali membri oggetti dell'organizzazione e del server del gruppo di ruoli è consentito modificare Active Directory.

Per altre informazioni sulle assegnazioni dei ruoli e sugli ambiti di gestione, vedere gli argomenti seguenti:

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

### Ruoli di gestione assegnati a questo gruppo di ruolo

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo di gestione</th>
<th>Assegnazione regolare</th>
<th>Assegnazione di delega</th>
<th>Ambito di lettura del destinatario</th>
<th>Ambito di scrittura del destinatario</th>
<th>Ambito di lettura della configurazione</th>
<th>Ambito di scrittura della configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">Ruolo di configurazione di sola visualizzazione</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
</tbody>
</table>


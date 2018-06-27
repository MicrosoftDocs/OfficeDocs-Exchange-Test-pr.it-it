---
title: 'Assistenza: Exchange 2013 Help'
TOCTitle: Assistenza
ms:assetid: e7958752-22e4-4155-a2fc-948099dec6f7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876949(v=EXCHG.150)
ms:contentKeyID: 50481902
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Assistenza

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Il gruppo dei ruoli di gestione è uno dei numerosi gruppi incorporati che costituiscono il modello delle autorizzazioni del controllo degli accessi in base al ruolo in Microsoft Exchange Server 2013. Ai gruppi di ruoli vengono assegnati uno o più ruoli di gestione che includono le autorizzazioni necessarie per eseguire un determinato gruppo di attività. I membri di un gruppo di ruoli possono accedere ai ruoli di gestione assegnati a tale gruppo. Per altre informazioni sui gruppi di ruoli, vedere [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md). di Help Desk

Gli utenti membri del gruppo di ruolo Assistenza possono eseguire una gestione limitata dei destinatari di Exchange 2013.

Il gruppo di ruolo Help Desk consente ai membri, per impostazione predefinita, di visualizzare e modificare le opzioni di Outlook Web App per qualsiasi utente nell'organizzazione. Queste opzioni potrebbero includere la modifica del nome visualizzato, dell'indirizzo, del numero telefonico e di altre informazioni sull'utente. Non comprendono le opzioni che non sono disponibili in Outlook Web App, ad esempio la modifica delle dimensioni di una cassetta postale o la configurazione del database delle cassette postali in cui si trova una cassetta postale.

I membri di questo gruppo di ruolo possono solamente modificare le opzioni di Outlook Web App che anche l'utente è in grado di modificare. In pratica, se un utente può modificare il suo nome visualizzato, anche un membro del gruppo di ruolo Help Desk può modificare il nome visualizzato dell'utente. Tuttavia, se un altro utente non può modificare il suo nome visualizzato, anche il membro del gruppo di ruolo Help Desk non può modificare il nome visualizzato dell'utente.


> [!WARNING]
> I limiti alle opzioni di Outlook Web App che un membro del gruppo di ruolo Help Desk può modificare vengono applicati tramite l'interfaccia di amministrazione di Exchange. Se un membro del gruppo di ruolo Help Desk ha accesso a Exchange&nbsp;Management Shell, egli potrà modificare qualsiasi opzione di Outlook Web App per tale utente. È opportuno valutare attentamente gli utenti da rendere membri del gruppo di ruolo Help Desk e stabilire se devono avere accesso anche a Shell.



Il gruppo di ruolo Help Desk non consente altre attività, in quanto esistono molti tipi diversi di organizzazioni. In effetti è possibile aggiungere ruoli di gestione a questo gruppo di ruolo per creare un gruppo di ruolo Help Desk in grado di rispondere alle esigenze della propria organizzazione. Ad esempio, se si desidera che i membri del gruppo di ruolo Help Desk siano in grado di gestire le cassette postali, i contatti di posta e gli utenti abilitati alla posta, è possibile assegnare il ruolo di gestione Destinatari posta a questo gruppo di ruolo. Per ulteriori informazioni sull'aggiunta di ruoli di gestione a questo gruppo di ruolo, vedere la sezione "Personalizzazione dei gruppi di ruolo" in questo argomento.

Per ulteriori informazioni su RBAC, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

## Appartenenza ai gruppi di ruolo

Se si desidera aggiungere o rimuovere membri in questo gruppo di ruoli, vedere [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).

Per impostazione predefinita, solo i membri del gruppo di ruoli Gestione organizzazione possono aggiungere o rimuovere membri da questo gruppo di ruoli. Per altre informazioni sull'aggiunta di ulteriori delegati al gruppo di ruoli, vedere la sezione "Aggiungere o rimuovere un delegato in un gruppo di ruoli" in [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

È possibile utilizzare il seguente comando per visualizzare un elenco degli utenti o dei gruppi di protezione universali membri di questo gruppo di ruolo.

    Get-RoleGroupMember "Help Desk"

Per ulteriori informazioni sui membri di un gruppo di ruolo, vedere [View the members of a role group](manage-role-group-members-exchange-2013-help.md) in [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).

## Personalizzazione dei gruppi di ruolo

Questo gruppo di ruoli viene assegnato ai ruoli di gestione per impostazione predefinita. I ruoli inclusi sono elencati nella sezione "Ruoli di gestione assegnati a questo gruppo di ruoli". È possibile aggiungere o rimuovere le assegnazioni dei ruoli da questo gruppo in base alle esigenze della propria organizzazione.

I gruppi di ruoli forniti con Exchange 2013 sono stati ideati per poter svolgere attività più dettagliate. Quando si assegnano i ruoli ad un gruppo di ruoli, i membri di quel gruppo sono abilitati ad eseguire le attività associate al ruolo. Ad esempio, il ruolo di inserimento nel journal consente la gestione dell'agente di inserimento nel journal e delle relative regole. Per altre informazioni sull'assegnazione dei ruoli ai gruppi di ruoli, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

I ruoli assegnati a questo gruppo di ruoli vengono assegnati agli ambiti di gestione predefiniti. Gli ambiti di gestione determinano quali oggetti di Exchange possono essere visualizzati o modificati dai membri di un gruppo di ruoli. È possibile modificare gli ambiti associati alle assegnazioni tra i ruoli e i gruppi di ruoli. Questo può essere necessario, ad esempio, se si desidera che solo i membri di un gruppo di ruoli siano in grado di modificare i destinatari che sono in un'unità organizzativa specifica o in una posizione specifica. Per altre informazioni sugli ambiti di gestione, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

Per altre informazioni su come personalizzare questo gruppo di ruoli, vedere gli argomenti seguenti:

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md)

Se si desidera creare un gruppo di ruoli e assegnare al nuovo gruppo alcuni dei ruoli assegnati a questo gruppo di ruoli, vedere la sezione "Creare un gruppo di ruoli" in [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

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
<td><p><a href="user-options-role-exchange-2013-help.md">Ruolo di opzioni utente</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">Ruolo destinatari di sola visualizzazione</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
</tbody>
</table>


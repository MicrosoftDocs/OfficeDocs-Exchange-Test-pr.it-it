﻿---
title: 'Ruolo MyContactInformation: Exchange 2013 Help'
TOCTitle: Ruolo MyContactInformation
ms:assetid: 0df7fc20-d9b3-40db-bb14-ba8b903df201
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876850(v=EXCHG.150)
ms:contentKeyID: 50479988
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ruolo MyContactInformation

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Il ruolo di gestione `MyContactInformation` consente ai singoli utenti di modificare le informazioni di contatto, compresi l'indirizzo e i numeri di telefono.

Questo ruolo di gestione è uno dei numerosi ruoli incorporati nel modello delle autorizzazioni Controllo degli accessi in base al ruolo di Microsoft Exchange Server 2013. I ruoli di gestione che vengono assegnati a uno o più gruppi, i criteri di assegnazione dei ruoli di gestione, gli utenti o i gruppi di protezione universale (USG) agiscono in qualità di raggruppamento logico di cmdlet o script che vengono combinati per consentire la visualizzazione o la modifica della configurazione dei componenti di Exchange 2013, come i database delle cassette postali, le regole di trasporto e i destinatari. Un cmdlet o uno script e i relativi parametri, denominati collettivamente voce del ruolo di gestione, inclusi in un ruolo possono essere eseguiti dagli utenti assegnati a quel ruolo. Per altre informazioni sui ruoli di gestione e sulle voci di tali ruoli, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

Per altre informazioni sui ruoli di gestione, sui gruppi di ruoli di gestione e sugli altri componenti di Controllo degli accessi in base al ruolo, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

## Assegnazioni del ruolo di gestione

Per consentire a questo ruolo di concedere autorizzazioni, è necessario assegnarlo a un assegnatario di ruolo, ad esempio un criterio di assegnazione dei ruoli. Questa assegnazione viene eseguita con le assegnazioni del ruolo di gestione. Le assegnazioni dei ruoli collegano gli assegnatari e i ruoli tra loro. Un assegnatario di ruolo a cui è assegnato più di un ruolo dispone di tutte le autorizzazioni concesse a tutti i ruoli a lui assegnati.


> [!NOTE]
> È inoltre possibile assegnare questo ruolo di gestione a un gruppo di ruoli, a un gruppo di protezione universale o direttamente a un utente. Tuttavia, i ruoli incentrati sull'utente sono più efficaci se vengono usati con i criteri di assegnazione dei ruoli.



Questo ruolo incentrato sull'utente ha ambiti impliciti che non possono essere modificati. Di conseguenza, non è opportuno aggiungere ambiti personalizzati alle assegnazioni di ruolo che assegnano questo ruolo ai criteri di assegnazione dei ruoli, ai gruppi di ruoli, ai gruppi di protezione universali o agli utenti.

Per altre informazioni sulle assegnazioni dei ruoli e sugli ambiti, vedere gli argomenti seguenti:

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

Questo ruolo può essere assegnato a uno o più criteri di assegnazione dei ruoli per impostazione predefinita. Per altre informazioni, vedere la sezione "Assegnazioni del ruolo di gestione predefinite".

Se si desidera visualizzare un elenco di gruppi di ruoli, utenti o gruppi di protezione universale assegnati a questo ruolo, usare il comando seguente.

```powershell
Get-ManagementRoleAssignment -Role "<role name>"
```

## Assegnazioni di ruolo regolare e di delega

È possibile assegnare questo ruolo agli assegnatari dei ruoli usando le assegnazioni regolari o le assegnazioni del ruolo di delega. Le assegnazioni regolari concedono all'assegnatario del ruolo le autorizzazioni fornite dal ruolo. L'assegnazione del ruolo di delega consente a un assegnatario di assegnare il ruolo ad altri utenti. Per altre informazioni sulle assegnazioni dei ruoli regolari e tramite assegnazione del ruolo di delega, vedere Informazioni sulle assegnazioni del ruolo di gestione[Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

## Aggiunta o eliminazione delle assegnazioni di ruolo

È possibile cambiare gli assegnatari a cui è associato questo ruolo. Cambiando l'assegnatario a cui è associato questo ruolo, è possibile cambiare gli utenti a cui vengono concesse le autorizzazioni. È possibile assegnare questo ruolo ad altri criteri di assegnazione dei ruoli predefiniti oppure creare criteri di assegnazione dei ruoli e assegnare loro questo ruolo.

Per assegnare questo ruolo agli assegnatari di ruolo, assegnarlo a un gruppo di ruoli di cui si è membri, direttamente a se stessi oppure a un gruppo di protezione universale di cui si è membri, con un'assegnazione del ruolo di delega. Per altre informazioni sulle assegnazioni del ruolo di delega, vedere la sezione "Assegnazioni di ruoli regolari e di delega".

È inoltre possibile rimuovere questo ruolo dal criterio di assegnazione dei ruoli predefinito, dai criteri di assegnazione dei ruoli e dai gruppi di ruoli creati, nonché dagli utenti e dai gruppi di protezione universale. Tuttavia, deve esistere sempre almeno un'assegnazione del ruolo di delega tra questo ruolo e un gruppo di ruoli o un gruppo di protezione universale. Non è possibile eliminare l'ultima assegnazione del ruolo di delega.

Per altre informazioni su come aggiungere o rimuovere le assegnazioni tra questo ruolo e gruppi di ruoli, utenti e gruppi di protezione universali, vedere gli argomenti seguenti:

  - "Aggiunta o rimozione di un ruolo da un gruppo" in [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [Rimozione di un ruolo da un utente o gruppo di protezione universale](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

## Abilitazione o disabilitazione delle assegnazioni di ruolo

Abilitando o disabilitando un'assegnazione di ruolo, si può controllare l'applicazione di tale assegnazione. Se un'assegnazione di ruolo è disabilitata, le autorizzazioni fornite dal ruolo associato non vengono applicate all'assegnatario del ruolo. Questo risulta utile se si desidera rimuovere temporaneamente le autorizzazioni senza eliminare un'assegnazione di ruolo. Per altre informazioni, vedere Modifica di un'assegnazione di ruolo[Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md).

## Assegnazioni predefinite del ruolo di gestione

Questo ruolo ha assegnazioni di ruolo a uno o più assegnatari di ruolo. La tabella seguente indica se l'assegnazione di ruolo è regolare o se c'è una delega e indica anche gli ambiti di gestione applicati a ciascuna assegnazione. Nell'elenco seguente viene descritta ciascuna colonna:

  - **Assegnazione regolare**   Le assegnazioni regolari di ruolo consentono all'assegnatario di ruolo di accedere alle autorizzazioni fornite dalle voci di ruolo di gestione per questo ruolo.

  - **Assegnazione di delega**   Le assegnazioni del ruolo di delega conferiscono all'assegnatario di ruolo la possibilità di assegnare questo ruolo ai gruppi di ruoli, agli utenti o ai gruppi di protezione universali (USG).

  - **Ambito di lettura del destinatario**   L'ambito di lettura del destinatario determina quali oggetti destinatario possono essere letti dall'assegnatario di ruolo da Active Directory.

  - **Ambito di scrittura del destinatario**   L'ambito di scrittura del destinatario determina quali oggetti destinatario possono essere modificati dall'assegnatario di ruolo in Active Directory.

  - **Ambito di lettura della configurazione**   L'ambito di lettura della configurazione determina quali oggetti configurazione e server possono essere letti dall'assegnatario di ruolo da Active Directory.

  - **Ambito di scrittura della configurazione**   L'ambito di scrittura della configurazione determina quali oggetti organizzativi e server possono essere modificati dall'assegnatario di ruolo in Active Directory.

### Assegnazioni del ruolo di gestione predefinite per questo ruolo

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
<th>Gruppo di ruolo o criterio di assegnazione</th>
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
<td><p>Criterio di assegnazione dei ruoli predefinito.</p>
<p>Per ulteriori informazioni, vedere <a href="understanding-management-role-assignment-policies-exchange-2013-help.md">Informazioni sui criteri di assegnazione di ruolo di gestione</a>.</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## Personalizzazione del ruolo di gestione

Questo ruolo è stato configurato per fornire all'assegnatario di un ruolo tutti i cmdlet necessari e i parametri per gestire le funzionalità e i componenti elencati all'inizio di questo argomento. Sono stati forniti anche altri ruoli per consentire la gestione di altre funzionalità. Mediante l'aggiunta e la rimozione di ruoli nei gruppi di ruoli, è possibile creare un modello di autorizzazioni personalizzate senza che sia necessario personalizzare i singoli ruoli di gestione. Per un elenco completo dei ruoli, vedere [Ruoli di gestione predefiniti](built-in-management-roles-exchange-2013-help.md). Per altre informazioni sulla personalizzazione dei gruppi di ruoli, vedere [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

Se si desidera creare una versione personalizzata di questo ruolo, è necessario creare un ruolo figlio e personalizzare il nuovo ruolo.


> [!WARNING]
> Le informazioni riportate di seguito consentono di eseguire la gestione avanzata delle autorizzazioni. La personalizzazione dei ruoli di gestione può aumentare notevolmente la complessità del modello delle autorizzazioni. Se si sostituisce un ruolo di gestione incorporato con un ruolo personalizzato non configurato correttamente, alcune funzionalità potrebbero smettere di funzionare.



Qui di seguito sono riportati i passaggi più comuni per creare un ruolo personalizzato e assegnarlo a un assegnatario di ruolo:

1.  Creare una copia di questo ruolo. Per ulteriori informazioni, vedere [Creare un ruolo](create-a-role-exchange-2013-help.md).

2.  Modificare o rimuovere le voci del ruolo sul nuovo ruolo utilizzando i cmdlet **Set-ManagementRoleEntry** e **Remove-ManagementRoleEntry**. Non è possibile aggiungere altre voci di ruolo al nuovo ruolo poiché questo può contenere solo le voci di ruolo del ruolo padre incorporato. Per altre informazioni, vedere gli argomenti seguenti:
    
      - [Modificare una voce di ruolo](change-a-role-entry-exchange-2013-help.md)
    
      - [Rimuovere una voce di ruolo da un ruolo](remove-a-role-entry-from-a-role-exchange-2013-help.md)

3.  Se si desidera sostituire il ruolo incorporato con questo nuovo ruolo personalizzato, eliminare qualsiasi assegnazione di ruolo associata al ruolo incorporato. Per ulteriori informazioni, vedere gli argomenti seguenti:
    
      - "Aggiunta o rimozione di un ruolo da un gruppo" in [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)
    
      - [Rimozione di un ruolo da un utente o gruppo di protezione universale](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

4.  Aggiungere il nuovo ruolo personalizzato agli assegnatari di ruolo richiesti. Per ulteriori informazioni, vedere gli argomenti seguenti:
    
      - "Aggiunta o rimozione di un ruolo da un gruppo" in [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)
    
      - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
        

        > [!IMPORTANT]
        > Se si desidera che oltre all'utente che ha creato il ruolo, altri utenti siano in grado di assegnare il nuovo ruolo personalizzato, aggiungere un'assegnazione del ruolo di delega ad almeno un assegnatario di ruolo. Per altre informazioni, vedere <A href="delegate-role-assignments-exchange-2013-help.md">Delegare le assegnazioni di ruolo</A>.



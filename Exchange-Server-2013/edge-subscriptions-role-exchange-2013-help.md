---
title: 'Ruolo di sottoscrizioni Edge: Exchange 2013 Help'
TOCTitle: Ruolo di sottoscrizioni Edge
ms:assetid: 7de1a663-96fb-4fb5-898a-effa82653597
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876912(v=EXCHG.150)
ms:contentKeyID: 50481044
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ruolo di sottoscrizioni Edge

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Il ruolo di gestione `Edge Subscriptions` consente agli amministratori di gestire la sincronizzazione Edge e la configurazione delle sottoscrizioni tra i server Trasporto Edge di Microsoft Exchange Server 2010 e i server Cassette postali di Microsoft Exchange Server 2013 in un'organizzazione.

Questo ruolo di gestione è uno dei numerosi ruoli incorporati nel modello delle autorizzazioni Controllo degli accessi in base al ruolo di Microsoft Exchange Server 2013. I ruoli di gestione che vengono assegnati a uno o più gruppi, i criteri di assegnazione dei ruoli di gestione, gli utenti o i gruppi di protezione universale (USG) agiscono in qualità di raggruppamento logico di cmdlet o script che vengono combinati per consentire la visualizzazione o la modifica della configurazione dei componenti di Exchange 2013, come i database delle cassette postali, le regole di trasporto e i destinatari. Un cmdlet o uno script e i relativi parametri, denominati collettivamente voce del ruolo di gestione, inclusi in un ruolo possono essere eseguiti dagli utenti assegnati a quel ruolo. Per altre informazioni sui ruoli di gestione e sulle voci di tali ruoli, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

Per altre informazioni sui ruoli di gestione, sui gruppi di ruoli di gestione e sugli altri componenti di Controllo degli accessi in base al ruolo, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

## Assegnazioni del ruolo di gestione

Per consentire a questo ruolo di concedere autorizzazioni, occorre assegnarlo ad un assegnatario di ruolo, che può essere un gruppo di ruoli, un utente o un gruppo di protezione universale (USG). Questa assegnazione viene eseguita con le assegnazioni del ruolo di gestione. Le assegnazioni dei ruoli collegano gli assegnatari e i ruoli tra loro. Un assegnatario di ruolo a cui è assegnato più di un ruolo dispone di tutte le autorizzazioni concesse a tutti i ruoli a lui assegnati.

Oltre a collegare gli assegnatari dei ruoli ai ruoli, le assegnazioni dei ruoli possono essere applicate anche agli ambiti di gestione personalizzati o incorporati. Gli ambiti di gestione controllano quali oggetti destinatario, server e database possono essere modificati dagli assegnatari dei ruoli. Se questo ruolo viene assegnato ad un assegnatario di ruolo, ma un ambito di gestione consente all'assegnatario del ruolo di gestire soltanto alcuni oggetti in base a un ambito definito, l'assegnatario del ruolo può utilizzare solo le autorizzazioni concesse da questo ruolo per quegli oggetti specifici. Le autorizzazioni concesse da questo ruolo non possono essere infatti applicate agli oggetti al di fuori dell'ambito definito dall'assegnazione del ruolo. Per altre informazioni sulle assegnazioni dei ruoli e sugli ambiti, vedere gli argomenti seguenti:

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

Questo ruolo viene assegnato a uno o più gruppi di ruoli per impostazione predefinita. Per altre informazioni, vedere la sezione "Assegnazioni predefinite del ruolo di gestione" più avanti in questo argomento.

Se si desidera visualizzare un elenco di gruppi di ruoli, utenti o gruppi di protezione universale assegnati a questo ruolo, usare il comando seguente.

    Get-ManagementRoleAssignment -Role "<role name>"

## Assegnazioni di ruolo regolare e di delega

È possibile assegnare questo ruolo agli assegnatari dei ruoli usando le assegnazioni regolari o le assegnazioni del ruolo di delega. Le assegnazioni regolari concedono all'assegnatario del ruolo le autorizzazioni fornite dal ruolo. L'assegnazione del ruolo di delega consente a un assegnatario di assegnare il ruolo ad altri utenti. Per altre informazioni sulle assegnazioni dei ruoli regolari e tramite assegnazione del ruolo di delega, vedere Informazioni sulle assegnazioni del ruolo di gestione[Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

## Aggiunta o eliminazione delle assegnazioni di ruolo

È possibile cambiare gli assegnatari a cui è associato questo ruolo. Cambiando l'assegnatario a cui è associato questo ruolo, è possibile cambiare gli utenti a cui vengono concesse le autorizzazioni. È possibile assegnare questo ruolo ad altri gruppi di ruoli incorporati oppure è possibile creare gruppi di ruoli e assegnare loro questo ruolo. È inoltre possibile assegnare questo ruolo a utenti o gruppi di protezione universali (USG). Tuttavia, si consiglia di limitare l'assegnazione dei ruoli agli utenti e ai gruppi di protezione universali (USG) perché queste assegnazioni possono aumentare notevolmente la complessità del modello delle autorizzazioni.

Per assegnare questo ruolo agli assegnatari di ruolo, assegnarlo a un gruppo di ruoli di cui si è membri, direttamente a se stessi oppure a un gruppo di protezione universale di cui si è membri, con un'assegnazione del ruolo di delega. Per altre informazioni sulle assegnazioni del ruolo di delega, vedere la sezione "Assegnazioni di ruoli regolari e di delega".

È inoltre possibile rimuovere questo ruolo da gruppi di ruoli incorporati, da gruppi di ruoli creati, dagli utenti e dai gruppi di protezione universali (USG). Tuttavia, deve esistere sempre almeno un'assegnazione del ruolo di delega tra questo ruolo e un gruppo di ruoli o un gruppo di protezione universale. Non è possibile eliminare l'ultima assegnazione del ruolo di delega. Questa limitazione serve a evitare che l'utente rimanga bloccato fuori dal sistema.


> [!IMPORTANT]
> Ci deve essere sempre almeno una delega di assegnazione di ruolo tra questo ruolo e un gruppo di ruoli o gruppo di protezione universale (USG). Non è possibile rimuovere l'ultima delega di assegnazione di ruolo associata a questo ruolo se l'ultima assegnazione era stata fatta a un utente.



Per altre informazioni su come aggiungere o rimuovere le assegnazioni tra questo ruolo e gruppi di ruoli, utenti e gruppi di protezione universali, vedere gli argomenti seguenti:

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [Rimozione di un ruolo da un utente o gruppo di protezione universale](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

## Modifica degli ambiti di gestione per le assegnazioni di ruolo

È inoltre possibile modificare gli ambiti di gestione sulle assegnazioni dei ruoli esistenti tra questo ruolo e gli assegnatari di ruolo. Modificando gli ambiti sulle assegnazioni dei ruoli, è possibile controllare quali oggetti possono essere gestiti mediante le autorizzazioni fornite da questo ruolo. Quando si modifica l'ambito di un'assegnazione di ruolo, sono disponibili varie opzioni. È possibile eseguire una delle operazioni seguenti:

  - Aggiungere un nuovo ambito personalizzato utilizzando il cmdlet **Set-ManagementRoleAssignment**. Per altre informazioni, vedere gli argomenti seguenti:
    
      - [Creare un ambito normale o esclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md)
    
      - [Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md)

  - Aggiungere o modificare l'ambito di un'unità organizzativa utilizzando il cmdlet **Set-ManagementRoleAssignment**. Per altre informazioni, vedere [Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md).

  - Aggiungere o modificare un ambito predefinito utilizzando il cmdlet **Set-ManagementRoleAssignment**. Per altre informazioni, vedere [Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md).

  - Modificare l'ambito del destinatario, del server o del database in un ambito personalizzato associato ad un'assegnazione di ruolo utilizzando il cmdlet **Set-ManagementScope**. Per altre informazioni, vedere [Modificare un ambito di ruolo](change-a-role-scope-exchange-2013-help.md).

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
<th>Gruppo di ruolo</th>
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
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
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



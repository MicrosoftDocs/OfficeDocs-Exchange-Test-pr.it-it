---
title: 'Gestire gruppi di ruoli: Exchange 2013 Help'
TOCTitle: Gestire gruppi di ruoli
ms:assetid: ab9b7a3b-bf67-4ba1-bde5-8e6ac174b82c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657480(v=EXCHG.150)
ms:contentKeyID: 50481405
ms.date: 04/05/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestire gruppi di ruoli

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-08_

In questo argomento è spiegato come aggiungere, rimuovere, copiare e visualizzare i gruppi di ruoli di gestione in Microsoft Exchange Server 2013. Viene inoltre mostrato come aggiungere, rimuovere e gestire i ruoli di gestione nei gruppi di ruoli e come cambiare gli ambiti di gestione e i delegati nei gruppi di ruoli. Per ulteriori informazioni sui gruppi di ruoli in Exchange 2013, vedere [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md).

Per le attività di gestione aggiuntive relative a gruppi di ruoli, vedere [Autorizzazioni](permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: Da 5 a 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di ruoli" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Creare un gruppo di ruoli

Se si desidera personalizzare le autorizzazioni che è possibile assegnare a un gruppo di utenti finali, è possibile creare un nuovo gruppo di ruoli di gestione personalizzato.

## Utilizzare EAC per creare un gruppo di ruoli

1.  In Interfaccia di amministrazione di Exchange (EAC), accedere ad **Autorizzazioni** \> **Ruoli amministratore** e fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  **Nuovo gruppo di ruoli** specificare un nome per il nuovo gruppo di ruoli.

3.  È possibile selezionare i ruoli da assegnare al gruppo di ruoli e i membri da aggiungere al gruppo di ruoli; le stesse operazioni possono essere eseguite in un secondo momento.

4.  Selezionare l'ambito di scrittura da applicare al nuovo gruppo di ruoli.

5.  Fare clic su **Salva** per creare il gruppo di ruoli.

## Utilizzare Shell per creare un gruppo di ruoli

Per creare un gruppo di ruoli, vedere la sezione [Examples](https://technet.microsoft.com/it-it/dd638181\(exchg.150\)#examples) in [New-RoleGroup](https://technet.microsoft.com/it-it/library/dd638181\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione di un gruppo di ruoli, procedere come segue:

1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Verificare che il nuovo gruppo di ruoli compaia nell'elenco dei gruppi di ruoli e selezionarlo.

3.  Verificare che i membri, i ruoli assegnati e l'ambito specificato nel nuovo gruppo di ruoli siano elencati nel riquadro dei dettagli del gruppo di ruoli.

## Copiare un gruppo di ruoli

## Utilizzare EAC per copiare un gruppo di ruoli

Se si dispone di un gruppo di ruoli contenente le autorizzazioni che si desidera concedere agli utenti, ma si desidera applicare un ambito di gestione differente o rimuovere o aggiungere uno o due ruoli di gestione senza dover aggiungere tutti gli altri ruoli manualmente, è possibile copiare il gruppo di ruoli esistenti.


> [!IMPORTANT]
> Non è possibile utilizzare EAC per copiare un gruppo di ruoli se è stata utilizzata Exchange Management Shell per configurare più ambiti di ruoli di gestione o ambiti esclusivi nel gruppo di ruoli. Se si sono configurati più ambiti o ambiti esclusivi nel gruppo di ruoli, è necessario utilizzare le procedure Shell descritte più avanti in questo argomento per copiare il gruppo di ruoli. Per ulteriori informazioni sugli ambiti dei ruoli di gestione, vedere <A href="understanding-management-role-scopes-exchange-2013-help.md">Comprensione degli ambiti di gestione dei ruoli</A>.



1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Selezionare il gruppo di ruoli che si desidera copiare e fare clic su **Copia**![Icona Copia](images/JJ657505.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "Icona Copia").

3.  **Nuovo gruppo di ruoli** specificare un nome per il nuovo gruppo di ruoli.

4.  Riesaminare i ruoli copiati nel nuovo gruppo di ruoli. Aggiungere o rimuovere i ruoli necessari.

5.  Riesaminare l'ambito di scrittura e cambiarlo, se necessario.

6.  Riesaminare i membri copiati nel nuovo gruppo di ruoli. Aggiungere o rimuovere membri come necessario.

7.  Fare clic su **Salva** per creare il gruppo di ruoli.

## Copia di un gruppo di ruoli senza ambito tramite Shell

1.  Archiviare il gruppo di ruoli che si desidera copiare in una variabile utilizzando la sintassi seguente.
    
        $RoleGroup = Get-RoleGroup <name of role group to copy>

2.  Utilizzare la seguente sintassi per creare il nuovo gruppo di ruoli, aggiungere membri al gruppo di ruoli e specificare gli utenti che possono delegare il gruppo di ruoli ad altri utenti.
    
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -Members <member1, member2, member3...> -ManagedBy <user1, user2, user3...>

Ad esempio, i seguenti comandi copiano il gruppo di ruoli Gestione organizzazione e denominano il nuovo gruppo di ruoli "Gestione organizzazione limitata". Vengono aggiunti i membri Isabelle, Carter e Lukas che possono essere delegati da Jenny e Katie.

    $RoleGroup = Get-RoleGroup "Organization Management"
    New-RoleGroup "Limited Organization Management" -Roles $RoleGroup.Roles -Members Isabelle, Carter, Lukas -ManagedBy Jenny, Katie

Una volta creato il nuovo gruppo di ruoli, è possibile aggiungere o rimuovere ruoli, modificare l'ambito delle assegnazioni dei ruoli per il ruolo e altro ancora.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-RoleGroup](https://technet.microsoft.com/it-it/library/dd638115\(v=exchg.150\)) e [New-RoleGroup](https://technet.microsoft.com/it-it/library/dd638181\(v=exchg.150\)).

## Copia di un gruppo di ruoli senza un ambito personalizzato tramite Shell

1.  Archiviare il gruppo di ruoli che si desidera copiare in una variabile utilizzando la sintassi seguente.
    
        $RoleGroup = Get-RoleGroup <name of role group to copy>

2.  Creare il nuovo gruppo di ruoli con un ambito personalizzato utilizzando la sintassi seguente.
    
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuraiton scope name>

Ad esempio, i seguenti comandi copiano il gruppo di ruoli Gestione organizzazione e creano un nuovo gruppo di ruoli denominato Gestione organizzazione di Vancouver con l'ambito del destinatario Utenti di Vancouver e l'ambito di configurazione Server di Vancouver.

    $RoleGroup = Get-RoleGroup "Organization Management"
    New-RoleGroup "Vancouver Organization Management" -Roles $RoleGroup.Roles -CustomRecipientWriteScope "Vancouver Users" -CustomConfigWriteScope "Vancouver Servers"

È possibile anche aggiungere membri al gruppo di ruoli quando ne viene creato uno utilizzando il parametro *Members* come illustrato nella sezione Copia di un gruppo di ruoli senza ambito tramite Shell descritta in precedenza in questo argomento. Per ulteriori informazioni sugli ambiti di gestione, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

Una volta creato il nuovo gruppo di ruoli, è possibile aggiungere o rimuovere ruoli, modificare l'ambito delle assegnazioni dei ruoli per il ruolo ed eseguire altre attività.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-RoleGroup](https://technet.microsoft.com/it-it/library/dd638115\(v=exchg.150\)) e [New-RoleGroup](https://technet.microsoft.com/it-it/library/dd638181\(v=exchg.150\)).

## Copia di un gruppo di ruoli con un ambito di unità organizzativa tramite Shell

1.  Archiviare il gruppo di ruoli che si desidera copiare in una variabile utilizzando la sintassi seguente.
    
        $RoleGroup = Get-RoleGroup <name of role group to copy>

2.  Creare il nuovo gruppo di ruoli con un ambito personalizzato utilizzando la sintassi seguente.
    
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope <OU name>

Ad esempio, i seguenti comandi copiano il gruppo di ruoli Gestione destinatari e creare un nuovo gruppo di ruoli denominato Gestione organizzazione di Toronto che consente di gestire solo gli utenti nell'unità organizzativa Utenti di Toronto.

    $RoleGroup = Get-RoleGroup "Recipient Management"
    New-RoleGroup "Toronto Recipient Management" -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope "contoso.com/Toronto Users"

È possibile anche aggiungere membri al gruppo di ruoli quando ne viene creato uno utilizzando il parametro *Members* come illustrato nella sezione Copia di un gruppo di ruoli senza ambito tramite Shell descritta in precedenza in questo argomento. Per ulteriori informazioni sugli ambiti di gestione, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

Una volta creato il nuovo gruppo di ruoli, è possibile aggiungere o rimuovere ruoli, modificare l'ambito delle assegnazioni dei ruoli per il ruolo e altro ancora.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-RoleGroup](https://technet.microsoft.com/it-it/library/dd638115\(v=exchg.150\)) e [New-RoleGroup](https://technet.microsoft.com/it-it/library/dd638181\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta copia di un gruppo di ruoli, procedere come segue:

1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Verificare che il gruppo di ruoli copiato compaia nell'elenco dei gruppi di ruoli e selezionarlo.

3.  Verificare che i membri, i ruoli assegnati e l'ambito specificato nel gruppo di ruoli copiato siano elencati nel riquadro dei dettagli del gruppo di ruoli.

## Rimuovere un gruppo di ruoli

Se un gruppo di ruoli precedentemente creato non è più necessario, è possibile rimuoverlo. Quando questo viene rimosso, verranno eliminate anche le assegnazioni di ruolo di gestione esistenti tra il gruppo di ruoli e i ruoli di gestione. I ruoli di gestione non vengono rimossi. Se il gruppo di ruoli da rimuovere consente a un utente di accedere a una particolare funzionalità, una volta che il gruppo è stato eliminato, questa funzionalità non sarà più accessibile per l'utente. Non è possibile rimuovere i gruppi di ruolo incorporati.

## Utilizzare EAC per rimuovere un gruppo di ruoli

1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Selezionare il gruppo di ruoli che si desidera rimuovere e fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

3.  Assicurarsi di voler rimuovere il gruppo di ruoli selezionato e rispondere **Sì** al messaggio di avviso.

## Utilizzo di Shell per rimuovere un gruppo di ruoli

Per rimuovere un gruppo di ruoli, vedere la sezione [Examples](https://technet.microsoft.com/it-it/dd638141\(exchg.150\)#examples) in [Remove-RoleGroup](https://technet.microsoft.com/it-it/library/dd638141\(v=exchg.150\)).

## Visualizzare i gruppi di ruoli

È possibile visualizzare un elenco dei gruppi di ruoli o le informazioni dettagliate su uno specifico gruppo di ruoli esistente nell'organizzazione.

## Utilizzare EAC per visualizzare un elenco dei gruppi di ruoli e dei dettagli dei gruppi di ruoli

1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**. Qui sono elencati tutti i gruppi di ruoli nell'organizzazione.

2.  Selezionare un gruppo di ruoli per visualizzarne i membri, i ruoli assegnati e l'ambito configurati nel gruppo di ruoli.

## Utilizzare Shell per visualizzare un elenco dei gruppi di ruoli e dei dettagli dei gruppi di ruoli

Per visualizzare un elenco di gruppi di ruoli, vedere la sezione [Examples](https://technet.microsoft.com/it-it/dd638115\(exchg.150\)#examples) in [Get-RoleGroup](https://technet.microsoft.com/it-it/library/dd638115\(v=exchg.150\)).

## Aggiungere un ruolo a un gruppo di ruoli

L'aggiunta di un ruolo a un gruppo di ruoli costituisce il metodo più semplice ed efficiente per concedere autorizzazioni a un gruppo di amministratori o utenti esperti. Se si desidera che i membri di un gruppo di ruoli siano in grado di gestire una determinata funzionalità, è necessario aggiungere il ruolo di gestione per tale funzionalità al gruppo di ruoli. Dopo l'aggiunta del ruolo, ai membri del gruppo di ruoli vengono concesse le autorizzazioni fornite dal ruolo.

## Utilizzare EAC per aggiungere un ruolo di gestione a un gruppo di ruoli


> [!IMPORTANT]
> Non è possibile utilizzare EAC per aggiungere ruoli a un gruppo di ruoli se è stata utilizzata Shell per configurare più ambiti di ruoli di gestione o ambiti esclusivi nel gruppo di ruoli. Se per il gruppo di ruoli sono stati configurati più ambiti o ambiti esclusivi, per aggiungere ruoli a un gruppo di ruoli è necessario utilizzare le procedure per la shell illustrate più avanti in questo argomento. Per ulteriori informazioni sugli ambiti dei ruoli di gestione, vedere <A href="understanding-management-role-scopes-exchange-2013-help.md">Comprensione degli ambiti di gestione dei ruoli</A>.



1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Selezionare il gruppo di ruoli a cui aggiungere un ruolo e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella sezione **Ruoli**, selezionare i ruoli che si desidera aggiungere al gruppo di ruoli.

4.  Una volta terminata l'aggiunta di ruoli al gruppo di ruoli, fare clic su **Salva**.

## Creazione di un'assegnazione di ruolo senza ambito tramite Shell

È possibile creare un'assegnazione di ruolo priva di ambito tra un ruolo e un gruppo di ruolo. Quando si esegue questa operazione, vengono applicati gli ambiti di scrittura e di lettura impliciti del ruolo.

Utilizzare la seguente sintassi per assegnare un ruolo privo di ambito a un gruppo di ruolo. Se non si specifica un nome per l'assegnazione di ruolo, ne verrà creato uno automaticamente.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name>

Con questo esempio viene assegnato il ruolo di gestione Transport Rules al gruppo di ruolo Seattle Compliance.

    New-ManagementRoleAssignment -SecurityGroup "Seattle Compliance" -Role "Transport Rules"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Creazione di un'assegnazione di ruolo con un ambito predefinito tramite Shell

Se un ambito predefinito consente di soddisfare i requisiti aziendali, è possibile applicare tale ambito all'assegnazione di ruolo, senza crearne uno nuovo. Per un elenco degli ambiti predefiniti e le relative descrizioni, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

Per ulteriori informazioni sulle assegnazioni di ruolo, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Utilizzare la seguente sintassi per assegnare un ruolo a un gruppo di ruolo con un ambito predefinito. Se non si specifica un nome per l'assegnazione di ruolo, ne verrà creato uno automaticamente.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientRelativeWriteScope < MyGAL | MyDistributionGroups | Organization | Self >

Con questo esempio viene assegnato il ruolo Message Tracking al gruppo di ruolo Enterprise Support e viene applicato l'ambito predefinito Organization.

    New-ManagementRoleAssignment -SecurityGroup "Enterprise Support" -Role "Message Tracking" -RecipientRelativeWriteScope Organization

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Creazione di un'assegnazione di ruolo con un ambito basato su un filtro destinatari tramite Shell

Se è stato creato un ambito basato su un filtro destinatari, è necessario includere l'ambito nel comando utilizzato per assegnare il ruolo a un gruppo di ruolo utilizzando il parametro *CustomRecipientWriteScope*.

È inoltre possibile includere un ambito di scrittura della configurazione durante la creazione di un'assegnazione di ruolo con un ambito di scrittura dei destinatari.

Per ulteriori informazioni sulle assegnazioni dei ruoli e sugli ambiti, vedere i seguenti argomenti:

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

Utilizzare la seguente sintassi per assegnare un ruolo a un gruppo di ruolo con un ambito basato su un filtro destinatari. Se non si specifica un nome per l'assegnazione di ruolo, ne verrà creato uno automaticamente.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomRecipientWriteScope <role scope name>

Con questo esempio viene assegnato il ruolo Message Tracking al gruppo di ruolo Seattle Recipient Admins e viene applicato l'ambito Seattle Recipients.

    New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Message Tracking" -CustomRecipientWriteScope "Seattle Recipients"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Creazione di un'assegnazione di ruolo con un ambito di configurazione tramite Shell

Se è stato creato un filtro configurazione del database o del server oppure un ambito basato su un elenco, è necessario utilizzare il parametro *CustomConfigWriteScope* per includere tale ambito nel comando utilizzato per assegnare il ruolo a un gruppo di ruoli.

È inoltre possibile includere un ambito di scrittura dei destinatari durante la creazione di un'assegnazione di ruolo con un ambito di scrittura della configurazione.

Per ulteriori informazioni sulle assegnazioni dei ruoli e sugli ambiti di gestione, vedere i seguenti argomenti:

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

Per assegnare un ruolo a un gruppo di ruoli con un ambito di configurazione, utilizzare la sintassi seguente. Se non si specifica un nome per l'assegnazione di ruolo, ne verrà creato uno automaticamente.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <role scope name>

Con questo esempio viene assegnato il ruolo Databases al gruppo di ruolo Seattle Server Admins e viene applicato l'ambito Seattle Servers.

    New-ManagementRoleAssignment -SecurityGroup "Seattle Server Admins" -Role "Databases" -CustomConfigWriteScope "Seattle Servers"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Creazione di un'assegnazione di ruolo con un ambito OU tramite Shell

Se si desidera applicare l'ambito di scrittura di un ruolo a un'unità organizzativa, è possibile specificare l'unità organizzativa direttamente nel parametro *RecipientOrganizationalUnitScope*.

Per ulteriori informazioni sulle assegnazioni dei ruoli e sugli ambiti di gestione, vedere i seguenti argomenti:

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

Utilizzare il seguente comando per assegnare un ruolo a un gruppo di ruolo e limitare l'ambito di scrittura del ruolo a un'unità organizzativa specifica. Se non si specifica un nome per l'assegnazione di ruolo, ne verrà creato uno automaticamente.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientOrganizationalUnitScope <OU>

Con questo esempio viene assegnato il ruolo Mail Recipients al gruppo di ruolo Seattle Recipient Admins e viene applicato l'ambito all'assegnazione Sales\\Users OU nel dominio Contoso.com.

    New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta aggiunta di ruoli a un gruppo di ruoli, procedere come segue:

1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Selezionare il gruppo di ruoli a cui sono stati aggiunti i ruoli. Nel riquadro dei dettagli del gruppo di ruoli, verificare che siano elencati i ruoli che sono stati aggiunti.

## Rimuovere un ruolo da un gruppo di ruoli

La rimozione di un ruolo da un gruppo di ruoli di gestione è il metodo migliore e più semplice per revocare le autorizzazioni concesse a un gruppo di amministratori o di utenti esperti. Per non concedere ad amministratori o utenti esperti le autorizzazioni per la gestione di una funzionalità, rimuovere il ruolo di gestione dal gruppo di ruoli di gestione che gestisce le autorizzazioni. Una volta rimosso il ruolo, i membri del gruppo di ruoli non disporranno più delle autorizzazioni necessarie per la gestione della funzionalità.


> [!NOTE]
> Alcuni gruppi di ruolo, ad esempio il gruppo di ruolo Gestione organizzazione, pongono limiti sui ruoli che possono essere rimossi dal gruppo di ruolo. Per ulteriori informazioni, vedere <A href="understanding-management-role-groups-exchange-2013-help.md">Informazioni sui gruppi di ruoli di gestione</A>.<BR>Se un amministratore è membro di un altro gruppo di ruoli che contiene ruoli di gestione che consentono la gestione della funzionalità, è necessario rimuovere l'amministratore dagli altri gruppi di ruoli oppure rimuovere il ruolo che concede le autorizzazioni per la gestione della funzionalità dagli altri gruppi di ruoli.



## Utilizzare EAC per rimuovere un ruolo di gestione da un gruppo di ruoli


> [!IMPORTANT]
> Non è possibile utilizzare EAC per rimuovere ruoli da un gruppo di ruoli se è stata utilizzata Shell per configurare più ambiti o ambiti esclusivi nel gruppo di ruoli. Se sono stati configurati più ambiti o ambiti esclusivi nel gruppo di ruoli, è necessario utilizzare le procedure della shell illustrate più avanti in questo argomento per rimuovere i ruoli dal gruppo di ruoli. Per ulteriori informazioni sugli ambiti dei ruoli di gestione, vedere <A href="understanding-management-role-scopes-exchange-2013-help.md">Comprensione degli ambiti di gestione dei ruoli</A>.



1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Selezionare il gruppo di ruoli da cui rimuovere un ruolo e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella sezione **Ruoli**, selezionare i ruoli che si desidera rimuovere dal gruppo di ruoli.

4.  Una volta terminata la rimozione di ruoli dal gruppo di ruoli, fare clic su **Salva**.

## Rimozione di un ruolo da un gruppo di ruolo tramite Shell

Per rimuovere i ruoli dai gruppi di ruoli, recuperare l'assegnazione del ruolo di gestione associato utilizzando il cmdlet **Get-ManagementRoleAssignment** ed eseguire il piping dell'assegnazione del ruolo restituita al cmdlet **Remove-ManagementRoleAssignment**. A meno che non si desideri rimuovere contemporaneamente le assegnazioni del ruolo di delega e del ruolo regolare, specificare con il parametro *Delegating* se si desidera rimuovere le assegnazioni del ruolo regolare o di delega.

Per ulteriori informazioni sulle assegnazioni del ruolo di delega, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Questa procedura utilizza il pipelining. Per ulteriori informazioni sull'esecuzione del piping, vedere [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\)).

Per rimuovere un ruolo da un gruppo di ruoli, utilizzare la seguente sintassi.

    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment

In questo esempio viene rimosso il ruolo Distribution Groups, che consente agli amministratori di gestire i gruppi di distribuzione, dal gruppo di ruoli Seattle Recipient Administrators. Dal momento che si desidera rimuovere l'assegnazione del ruolo che concede le autorizzazioni necessarie per la gestione dei gruppi di distribuzione, il parametro *Delegating* è impostato su `$False`, in modo da restituire solo le assegnazioni dei ruoli regolari.

    Get-ManagementRoleAssignment -RoleAssignee "Seattle Recipient Administrators" -Role "Distribution Groups" -Delegating $false | Remove-ManagementRoleAssignment

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351205\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta rimozione dei ruoli da un gruppo di ruoli, procedere come segue:

1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Selezionare il gruppo di ruoli da cui sono stati rimossi i ruoli. Nel riquadro dei dettagli del gruppo di ruoli, verificare che non siano più elencati i ruoli che sono stati rimossi.

## Modificare l'ambito di un gruppo di ruoli

Le assegnazioni dei ruoli di gestione tra un gruppo di ruoli e un ruolo contengono ambiti di gestione che determinano gli oggetti disponibili per i membri di tale gruppo di ruoli. Modificando un ambito di scrittura in un gruppo di ruoli, è possibile modificare gli oggetti disponibili per i membri del gruppo di ruoli da creare, modificare o rimuovere. Non è possibile modificare l'ambito di lettura su un gruppo di ruoli.

Exchange 2013 include ambiti applicati per impostazione predefinita alle assegnazioni di ruolo quando non vengono creati ambiti personalizzati. Se si desidera utilizzare un ambito personalizzato con un'assegnazione dei ruoli su un gruppo di ruoli, è necessario crearne prima uno. Per ulteriori informazioni sulla creazione degli ambiti personalizzati, che è un'attività avanzata, vedere [Creare un ambito normale o esclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

Per ulteriori informazioni sugli ambiti e le assegnazioni dei ruoli di gestione in Exchange 2013, vedere i seguenti argomenti:

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

## Utilizzare EAC per modificare l'ambito in un gruppo di ruoli

Quando si utilizza EAC per modificare l'ambito in un gruppo di ruoli, si sta effettivamente modificando l'ambito in tutte le assegnazioni dei ruoli tra il gruppo di ruoli e tutti i ruoli di gestione assegnati al gruppo di ruoli. Se si desidera modificare l'ambito in determinate assegnazioni dei ruoli, è necessario utilizzare le procedure di Shell descritte più avanti in questo argomento.


> [!IMPORTANT]
> Non è possibile utilizzare EAC per gestire gli ambiti nelle assegnazioni dei ruoli tra i ruoli e un gruppo di ruoli se si sono configurati più ambiti o ambiti esclusivi in tali assegnazioni dei ruoli tramite Shell. Se si sono configurati più ambiti o ambiti esclusivi in tali assegnazioni dei ruoli, è necessario utilizzare le procedure Shell descritte più avanti in questo argomento per gestire gli ambiti. Per ulteriori informazioni sugli ambiti dei ruoli di gestione, vedere <A href="understanding-management-role-scopes-exchange-2013-help.md">Comprensione degli ambiti di gestione dei ruoli</A>.



1.  In Stima al completamento (EAC, Estimate at Completion) passare ad **Autorizzazioni** \> **Ruoli di amministratore**.

2.  Selezionare il gruppo di ruoli per cui si desidera modificare l'ambito, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Selezionare una delle due opzioni **Ambito di scrittura** riportate di seguito:
    
      - Un ambito di scrittura dalla casella di riepilogo a discesa, dove è possibile selezionare sia l'ambito di scrittura predefinito sia un ambito di scrittura personalizzato.
    
      - **Unità organizzativa**   Selezionare questa opzione e fornire un'unità organizzativa se si desidera assegnare un ambito a questo gruppo di ruoli in un'unità organizzativa.

4.  Fare clic su **Salva** per salvare le modifiche al gruppo di ruoli.

## Modifica contemporanea dell'ambito di tutte le assegnazioni di ruolo su un gruppo di ruoli tramite Shell

Le assegnazioni dei ruoli tra il gruppo di ruoli e i ruoli assegnati ad esso possono utilizzare l'ambito implicito ottenuto dai ruoli stessi, lo stesso ambito personalizzato o diversi ambiti personalizzati. Per ulteriori informazioni sulle assegnazioni di ruolo, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Gli ambiti delle assegnazioni dei ruoli vengono gestiti mediante il cmdlet **Set-ManagementRoleAssignment**. Non è possibile gestire gli ambiti utilizzando il cmdlet **Set-RoleGroup**.

Per modificare contemporaneamente l'ambito di tutte le assegnazioni di ruolo tra un gruppo di ruoli e un gruppo di ruoli di gestione, è necessario prima recuperare le assegnazioni di ruolo sul gruppo di ruoli, quindi impostare il nuovo ambito su ciascuna assegnazione. È possibile eseguire l'operazione utilizzando il cmdlet **Get-ManagementRoleAssignment** per recuperare le assegnazioni di ruolo, quindi eseguire il pipelining al cmdlet **Set-ManagementRoleAssignment**.

Questa procedura utilizza i concetti di pipeline e l'opzione *WhatIf*. Per ulteriori informazioni, vedere i seguenti argomenti:

  - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))

  - [Opzioni WhatIf, Confirm e ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

Per configurare contemporaneamente l'ambito su tutte le assegnazioni di ruolo su un gruppo di ruoli, utilizzare la sintassi seguente.

    Get-ManagementRoleAssignment -RoleAssignee <name of role group> | Set-ManagementRoleAssignment -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>

Utilizzare solo i parametri necessari per la configurazione dell'ambito desiderato. Ad esempio, se si desidera modificare l'ambito destinatari per tutte le assegnazioni di ruolo sul gruppo di ruoli Sales Recipient Management in Direct Sales Employees, utilizzare il comando seguente.

    Get-ManagementRoleAssignment -RoleAssignee "Sales Recipient Management" | Set-ManagementRoleAssignment -CustomRecipientWriteScope "Direct Sales Employees"


> [!NOTE]
> È possibile utilizzare l'opzione <EM>WhatIf</EM> per verificare di aver modificato solo le assegnazioni di ruolo desiderate. Eseguire il comando precedente con l'opzione <EM>WhatIf</EM> per verificare i risultati, quindi rimuovere l'opzione <EM>WhatIf</EM> per applicare le modifiche.



Per ulteriori informazioni sulla modifica delle assegnazioni del ruolo di gestione, vedere [Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md).

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Modifica dell'ambito delle singole assegnazioni di ruolo su un gruppo di ruoli tramite Shell

Le assegnazioni dei ruoli tra il gruppo di ruoli e i ruoli assegnati ad esso possono utilizzare l'ambito implicito ottenuto dai ruoli stessi, lo stesso ambito personalizzato o diversi ambiti personalizzati. Per ulteriori informazioni sulle assegnazioni di ruolo, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Gli ambiti delle assegnazioni dei ruoli vengono gestiti mediante il cmdlet **Set-ManagementRoleAssignment**. Non è possibile gestire gli ambiti utilizzando il cmdlet **Set-RoleGroup**.

In questa procedura, vengono utilizzati i concetti di pipeline e il cmdlet **Format-List**. Per ulteriori informazioni, vedere i seguenti argomenti:

  - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))

  - [Utilizzo dell'output del comando](working-with-command-output-exchange-2013-help.md)

Per modificare l'ambito su un'assegnazione di ruolo tra un gruppo di ruoli e un ruolo di gestione, è necessario prima individuare il nome dell'assegnazione di ruolo, quindi configurare l'ambito sull'assegnazione di ruolo.

1.  Per individuare i nomi di tutte le assegnazioni di ruolo su un gruppo di ruoli, utilizzare il comando seguente. Eseguendo il pipelining delle assegnazioni del ruolo di gestione al cmdlet **Format-List**, è possibile visualizzare il nome completo dell'assegnazione.
    
        Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-List Name

2.  Trovare il nome dell'assegnazione di ruolo che si desidera modificare. Utilizzare il nome dell'assegnazione di ruolo nel passo successivo.

3.  Per configurare l'ambito su una singola assegnazione, utilizzare la sintassi seguente.
    
        Set-ManagementRoleAssignment <role assignment name> -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>

Utilizzare solo i parametri necessari per la configurazione dell'ambito desiderato. Ad esempio, se si desidera modificare l'ambito destinatari per l'assegnazione di ruolo Mail Recipients\_Sales Recipient Management in All Sales Employees, utilizzare il comando seguente.

    Set-ManagementRoleAssignment "Mail Recipients_Sales Recipient Management" -CustomRecipientWriteScope "All Sales Employees"

Per ulteriori informazioni sulla modifica delle assegnazioni del ruolo di gestione, vedere [Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md).

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335173\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta modifica dell'ambito di un'assegnazione di ruolo in un gruppo di ruoli, procedere come segue:

  - Se è stata utilizzata EAC per configurare l'ambito nel gruppo di ruoli, procedere come segue:
    
    1.  In EAC selezionare **Autorizzazioni** \> **Ruoli amministratore**. Qui sono elencati i gruppi di ruoli nell'organizzazione.
    
    2.  Selezionare un gruppo di ruoli per visualizzare l'ambito configurato nel gruppo di ruoli.

  - Se è stata utilizzata Shell per configurare l'ambito nel gruppo di ruoli, procedere come segue:
    
    1.  Eseguire il seguente comando in Shell.
        
            Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-Table *WriteScope
    
    2.  Verificare che l'ambito di scrittura nelle assegnazioni di ruolo sia stato cambiato nell'ambito specificato.

## Aggiungere o rimuovere un delegato del gruppo di ruoli

I delegati del gruppo di ruoli sono utenti o gruppi di protezione universali (USG), che possono aggiungere o rimuovere i membri da un gruppo di ruolo o modificare le proprietà di un gruppo di ruolo. Con l'aggiunta o la rimozione di delegati del gruppo di ruolo, è possibile controllare chi è autorizzato a gestire un gruppo di ruolo.


> [!IMPORTANT]
> Dopo aver aggiunto un delegato a un gruppo di ruolo, il gruppo di ruolo può essere gestito solo dai delegati del gruppo o dagli utenti a cui viene assegnato, direttamente o indirettamente, il ruolo di gestione.<BR>Se ad un utente è assegnato, direttamente o indirettamente, il ruolo di gestione e non è aggiunto come un delegato del gruppo, l'utente deve utilizzare l'opzione <EM>BypassSecurityGroupManagerCheck</EM> sui cmdlet <STRONG>Add-RoleGroupMember</STRONG>, <STRONG>Remove-RoleGroupMember</STRONG>, <STRONG>Update-RoleGroupMember</STRONG> e <STRONG>Set-RoleGroup</STRONG> per gestire un gruppo di ruolo.




> [!NOTE]
> Non è possibile utilizzare EAC per aggiungere un delegato a un gruppo di ruoli.



## Utilizzare Shell per aggiungere un delegato a un gruppo di ruolo

Per modificare l'elenco dei delegati su un gruppo di ruoli, utilizzare il parametro *ManagedBy* sul cmdlet **Set-RoleGroup**. Il parametro *ManagedBy* sovrascrive l'intero elenco dei delegati sul gruppo di ruoli. Se si desidera aggiungere delegati al gruppo di ruolo piuttosto che sostituire l'intero elenco dei delegati, utilizzare i seguenti passi:

1.  Archiviare il gruppo di ruoli in una variabile utilizzando il comando seguente.
    
        $RoleGroup = Get-RoleGroup <role group name>

2.  Aggiungere il delegato al gruppo di ruolo memorizzato nella variabile utilizzando il seguente comando.
    
        $RoleGroup.ManagedBy += (Get-User <user to add>).Identity
    

    > [!NOTE]
    > Utilizzare il cmdlet di <STRONG>Get-Group</STRONG> se si desidera aggiungere un gruppo di protezione universale.



3.  Ripetere il passo 2 per ogni delegato che si desidera aggiungere.

4.  Applicare il nuovo elenco di delegati al gruppo di ruoli attuale utilizzando il comando seguente.
    
        Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy

In questo esempio viene aggiunto l'utente David Strome come delegato al gruppo di ruolo Gestione organizzazione.

    $RoleGroup = Get-RoleGroup "Organization Management"
    $RoleGroup.ManagedBy += (Get-User "David Strome").Identity
    Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-RoleGroup](https://technet.microsoft.com/it-it/library/dd638182\(v=exchg.150\)).

## Utilizzo di Shell per rimuovere un delegato da un gruppo di ruolo

Per modificare l'elenco dei delegati su un gruppo di ruoli, utilizzare il parametro *ManagedBy* sul cmdlet **Set-RoleGroup**. Il parametro *ManagedBy* sovrascrive l'intero elenco dei delegati sul gruppo di ruoli. Se si desidera rimuovere delegati dal gruppo di ruolo piuttosto che sostituire l'intero elenco dei delegati, utilizzare i seguenti passi:

1.  Archiviare il gruppo di ruoli in una variabile utilizzando il comando seguente.
    
        $RoleGroup = Get-RoleGroup <role group name>

2.  Rimuovere il delegato dal gruppo di ruolo memorizzato nella variabile utilizzando il seguente comando.
    
        $RoleGroup.ManagedBy -= (Get-User <user to remove>).Identity
    

    > [!NOTE]
    > Utilizzare il cmdlet di <STRONG>Get-Group</STRONG> se si desidera rimuovere un gruppo di protezione universale.



3.  Ripetere il passo 2 per ogni delegato che si desidera rimuovere.

4.  Applicare il nuovo elenco di delegati al gruppo di ruoli attuale utilizzando il comando seguente.
    
        Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy

In questo esempio viene rimosso l'utente David Strome come delegato al gruppo di ruolo Gestione organizzazione.

    $RoleGroup = Get-RoleGroup "Organization Management"
    $RoleGroup.ManagedBy -= (Get-User "David Strome").Identity
    Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-RoleGroup](https://technet.microsoft.com/it-it/library/dd638182\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta modifica dell'elenco dei delegati in un gruppo di ruoli, procedere come segue:

1.  In Shell, utilizzare il seguente comando.
    
        Get-RoleGroup <role group name> | Format-List ManagedBy

2.  Verificare che i delegati elencati nella proprietà *ManagedBy* includano solo i delegati che dovrebbero essere in grado di gestire il gruppo di ruoli.


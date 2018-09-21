---
title: 'Controlla distr. autom. cassette postali ambiti database: Exchange 2013 Help'
TOCTitle: Controllare la distribuzione automatica delle cassette postali tramite gli ambiti dei database
ms:assetid: 8eaff177-2251-4c8b-8570-c91a77d0a6fc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff628332(v=EXCHG.150)
ms:contentKeyID: 50481159
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Controllare la distribuzione automatica delle cassette postali tramite gli ambiti dei database

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Distribuzione automatica delle cassette postali è una funzione di Microsoft Exchange Server 2013 che effettua una selezione casuale del database delle cassette postali per memorizzare una cassetta postale nuova o trasferita quando non viene specificato esplicitamente un database. Questa funzionalità può essere utile quando si desidera consentire agli amministratori junior o al personale del servizio di assistenza di creare delle cassette postali senza che sia necessario sapere su quale database devono essere create.

È possibile utilizzare gli ambiti di gestione del database per controllare quali database di cassette postali possono essere selezionati dalla distribuzione automatica delle cassette postali. Quando si applicano gli ambiti del database ad un amministratore, per quest'ultimo sono disponibili solo i database che corrispondono all'ambito del database definito. Poiché la distribuzione automatica delle cassette postali utilizza il contesto dell'utente corrente, questa viene vincolata anche dagli ambiti del database applicati all'amministratore.

Per ulteriori informazioni sulla distribuzione automatica delle cassette postali, e sugli ambiti del database, vedere i seguenti argomenti:

  - [Distribuzione automatica delle cassette postali](automatic-mailbox-distribution-exchange-2013-help.md)

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

Per informazioni sulle altre attività di gestione relative agli ambiti, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa procedura: 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ambiti di gestione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passo 1: Creazione di un ambito di database

In questo passo, decidere quali database si desidera includere nell'ambito del database. Inoltre, decidere se si desidera specificare un elenco statico di database o se si desidera creare un filtro di database che includa solo i database che corrispondono ai criteri che si specificano.


> [!IMPORTANT]
> Le assegnazioni di ruolo associate agli ambiti dei database sono valide solo per gli utenti che si connettono al server che eseguono Microsoft Exchange Server 2010 Service Pack 1 (SP1) o versione successiva o Exchange 2013. Se un utente assegnato un'assegnazione di ruolo associata a un ambito di database si connette a un server di pre-Exchange&nbsp;2010 SP1, l'assegnazione di ruolo non viene applicata all'utente e all'utente non verrà concesse le autorizzazioni disponibili per l'assegnazione di ruolo.



## Utilizzo di un ambito degli elenchi di database

Utilizzare un elenco di database se si desidera definire un elenco statico dei database delle cassette postali che devono essere incluse in questo ambito. Utilizzare la sintassi seguente per creare un ambito basato su un elenco di database.

```powershell
New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>
```

In questo esempio viene creato un ambito che si applica unicamente ai database Database 1, Database 2 e Database 3.

    New-ManagementScope -Name "Accounting databases" -DatabaseList "Database 1", "Database 2", "Database 3"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementScope](https://technet.microsoft.com/it-it/library/dd335137\(v=exchg.150\)).

## Utilizzo di un ambito del filtro dei database

Se si desidera creare un ambito di un database dinamico che includa solo i database che corrispondono ai criteri specificati, utilizzare un filtro di database. Ciò può essere utile se non si desidera gestire l'ambito dei database dopo che sarà stato creato e dopo che saranno stati definiti dei valori standard per la propria organizzazione che possono identificare gruppi specifici di database delle cassette postali.

Per ottenere un elenco delle proprietà filtrabili del database, vedere [Informazioni sui filtri di ambito di gestione dei ruoli](understanding-management-role-scope-filters-exchange-2013-help.md).

Utilizzare la sintassi seguente per creare un ambito basato su un filtro dei database.

```powershell
New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>
```

In questo esempio viene creato un ambito che include tutti i database contenenti la stringa "ACCT" nella proprietà **Name** del database.

    New-ManagementScope -Name "Accounting Databases" -DatabaseRestrictionFilter { Name -Like '*ACCT*' }

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementScope](https://technet.microsoft.com/it-it/library/dd335137\(v=exchg.150\)).

## Passo 2: Aggiungere l'ambito del database ad un'assegnazione dei ruoli di gestione

Dopo aver creato l'ambito è necessario aggiungerlo a un'assegnazione del ruolo di gestione nuova o esistente. Si raccomanda di utilizzare i gruppi dei ruoli di gestione per controllare le autorizzazione amministrative, quindi, gli esempi in questo passo utilizzano un gruppo di ruolo esemplificativo denominato amministratori contabili. Per ulteriori informazioni sulla rimozione di un gruppo di ruoli, vedere [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

Dopo aver assegnato il ruolo ad un gruppo di ruoli con l'ambito del database, i membri del gruppo di ruolo saranno in grado di creare solo cassette postali e spostarle sui database inclusi nell'ambito.

Per un elenco dei ruoli incorporati che è possibile assegnare a gruppi di ruoli, vedere [Ruoli di gestione predefiniti](built-in-management-roles-exchange-2013-help.md).

## Aggiunta di un'assegnazione di un nuovo ruolo

Utilizzare questa procedura se si è appena creato un gruppo di ruoli ed è necessario aggiungervi dei ruoli.

Utilizzare la seguente sintassi per creare un'assegnazione di ruolo tra il ruolo di gestione che si desidera assegnare e il nuovo gruppo di ruolo, con il nuovo ambito di database.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <database scope name>

Questo esempio crea un'assegnazione di ruolo tra i ruoli dei destinari dei messaggi di posta elettronica e della creazione dei destinatari e il gruppo dei ruoli di amministratori contabili, utilizzando l'ambito dei database contabili.

    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipients" -CustomConfigWriteScope "Accounting Databases"
    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipient Creation" -CustomConfigWriteScope "Accounting Databases"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Modificare un'assegnazione di ruolo esistente

Utilizzare questa procedura se si ha un gruppo di ruoli esistente che già ha delle assegnazioni di ruolo tra di esso e i ruoli a cui si desidera applicare il nuovo ambito di database.

Questa procedura utilizza il pipelining. Per ulteriori informazioni, vedere [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\)).

Utilizzare la seguente sintassi per modificare un'assegnazione di ruolo tra il ruolo di gestione al quale si desidera applicare l'ambito del database e un gruppo di ruoli esistente.

    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> | Set-ManagementRoleAssignment -CustomConfigWriteScope <database scope name>

Questo esempio aggiunge l'ambito di database dei database contabili ai ruoli dei destinatari dei messaggi e di creazione dei destinatari dei messaggi assegnati al gruppo dei ruoli degli amministratori contabili.

    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipients" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"
    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipient Creation" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)) o [Set-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335173\(v=exchg.150\)).

## Passo 3: Aggiungere i membri ad un gruppo di ruoli (se applicabile)

Se si desidera aggiungere dei membri ad un gruppo di ruoli, vedere [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).


> [!IMPORTANT]
> Se si aggiungono membri a questo gruppo di ruoli per limitare il numero di database sui quali gli utenti possono creare o spostare cassette postali, accertarsi che non siano membri di altri gruppi di ruoli che potrebbero concedere ulteriori permessi.



## Passo 4: Aggiungere i membri da un gruppo di ruoli (se applicabile)

Se sono stati aggiunti dei membri ad un nuovo gruppo di ruoli che limita i database su cui possono creare delle cassette postali o su cui possono spostarle e sono membri di un altro gruppo di ruoli che ha ulteriori permessi, rimuoverli dal vecchio gruppo di ruoli. Per ulteriori informazioni, vedere [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).


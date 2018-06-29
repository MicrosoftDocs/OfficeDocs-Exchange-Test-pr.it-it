---
title: 'Modificare una voce di ruolo in un ruolo di primo livello senza ambito: Exchange 2013 Help'
TOCTitle: Modificare una voce di ruolo in un ruolo di primo livello senza ambito
ms:assetid: 65c0bfb3-aafd-4c64-8429-7616c57adf1c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876896(v=EXCHG.150)
ms:contentKeyID: 50480831
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare una voce di ruolo in un ruolo di primo livello senza ambito

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-03_

Le voci di ruolo di gestione nei ruoli di gestione di primo livello senza ambito si riferiscono agli script e ai cmdlet non Exchange, nonché ai relativi parametri, che si desidera rendere disponibili a chi è assegnato al ruolo. Modificando i parametri disponibili in una voce di ruolo, è possibile controllare le attività che gli utenti assegnati al ruolo possono eseguire con lo script o il cmdlet non Exchange. Per ulteriori informazioni sulle voci di ruolo senza ambito, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).


> [!NOTE]
> Se si desidera modificare una voce per un ruolo di gestione contenente i cmdlet Exchange, vedere <A href="change-a-role-entry-exchange-2013-help.md">Modificare una voce di ruolo</A>.



Per informazioni sulle altre attività di gestione relative ai ruoli, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ruoli di gestione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - La modifica di una voce di ruolo di primo livello senza ambito non è una funzionalità predefinita dei gruppi di ruoli di gestione. Affinché per un utente sia possibile aggiungere o modificare una voce di ruolo di primo livello senza ambito, è necessario assegnare il ruolo Gestione ruoli senza ambito all'utente oppure a un gruppo di protezione universale o a un gruppo di ruoli di cui l'utente sia membro. Per ulteriori informazioni sull'aggiunta di un ruolo a un utente, a un gruppo di protezione universale o a un gruppo di ruolo, vedere i seguenti argomenti:
    
      - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)
    
      - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo di Shell per aggiungere uno o più parametri a una voce di ruolo

Per aggiungere parametri a una voce di ruolo di primo livello senza ambito, effettuare quanto segue:

  - Specificare i parametri che si desidera aggiungere utilizzando il parametro *Parameters*.

  - Impostare il parametro *AddParameter* per specificare che si desidera eseguire un'operazione di aggiunta.

  - Specificare il parametro *UnscopedTopLevel* per indicare che si sta modificando una voce in un ruolo di primo livello senza ambito. Se questo parametro non viene specificato quando si modifica una voce di un ruolo senza ambito, si verifica un errore.

Per aggiungere parametri a una voce di ruolo, utilizzare la seguente sintassi.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter -UnscopedTopLevel

In questo esempio viene mostrato come aggiungere i parametri *EmailAddress* e *City* allo script **CreateUsers.ps1** nel ruolo senza ambito Recipient Administrators.

    Set-ManagementRoleEntry "Recipient Administrators\CreateUsers.ps1" -Parameters EmailAddress, City -AddParameter -UnscopedTopLevel

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351162\(v=exchg.150\)).

## Utilizzo di Shell per rimuovere uno o più parametri da una voce di ruolo

Per rimuovere un parametro da una voce di ruolo, effettuare quanto segue:

  - Specificare i parametri che si desidera rimuovere utilizzando il parametro *Parameters*.

  - Impostare il parametro *RemoveParameter* per specificare che si desidera eseguire un'operazione di rimozione.

  - Specificare il parametro *UnscopedTopLevel* per indicare che si sta modificando una voce in un ruolo di primo livello senza ambito. Se questo parametro non viene specificato quando si modifica una voce di un ruolo senza ambito, si verifica un errore.


> [!WARNING]
> Non è possibile annullare le operazioni di rimozione. Se si rimuove un parametro da una voce di ruolo per errore, è necessario aggiungerlo di nuovo manualmente.



Per rimuovere parametri da una voce di ruolo, utilizzare la seguente sintassi.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter -UnscopedTopLevel

In questo esempio viene mostrato come rimuovere i parametri *Delay*, *Force* e *Credential* dal cmdlet **Start-Widget** non Exchange contenuto nel ruolo Tier 1 Server Administrators.

    Set-ManagementRoleEntry "Tier 1 Server Administrators\Start-Widget" -Parameters Delay, Force, Credential -RemoveParameter -UnscopedTopLevel

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351162\(v=exchg.150\)).

## Utilizzo di Shell per rimuovere tutti i parametri da una voce di ruolo

Per rimuovere tutti i parametri da una voce di ruolo, effettuare quanto segue:

  - Specificare il valore `$Null` nel parametro *Parameters*. Non è necessario includere il parametro *RemoveParameter*.

  - Specificare il parametro *UnscopedTopLevel* per indicare che si sta modificando una voce in un ruolo di primo livello senza ambito. Se questo parametro non viene specificato quando si modifica una voce di un ruolo senza ambito, si verifica un errore.

La rimozione di tutti i parametri da una voce di ruolo è particolarmente utile quando in uno script o in un cmdlet non Exchange si desidera rendere disponibili solo alcuni parametri, escludendo tutti gli altri.

Se non si desidera che un ruolo abbia accesso a uno script o un cmdlet non Exchange, anziché rimuovere i parametri, rimuovere completamente dal ruolo la voce di ruolo associata. Per ulteriori informazioni sulla rimozione di una voce da un ruolo, vedere [Rimuovere una voce di ruolo da un ruolo](remove-a-role-entry-from-a-role-exchange-2013-help.md).


> [!WARNING]
> Non è possibile annullare le operazioni di rimozione. Se si rimuovono erroneamente tutti i parametri da una voce di ruolo, è necessario aggiungerli di nuovo manualmente.



Per rimuovere tutti i parametri da una voce di ruolo, utilizzare la seguente sintassi.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters $Null -UnscopedTopLevel

In questo esempio viene mostrato come rimuovere tutti i parametri dallo script FindMailboxesOverQuota.ps1, nel ruolo Recipient Administrators.

    Set-ManagementRoleEntry "Recipient Administrators\FindMailboxesOverQuota.ps1" -Parameters $Null -UnscopedTopLevel

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351162\(v=exchg.150\)).

## Utilizzo di Shell per applicare un determinato insieme di parametri

Se si desidera che in una voce di ruolo sia incluso solo un gruppo specifico di parametri, effettuare quanto segue:

  - Specificare solo il parametro *Parameters*. Non includere i parametri *AddParameter* o *RemoveParameter*.

  - Impostare il parametro *UnscopedTopLevel* per specificare che si sta modificando una voce di ruolo senza ambito. Se questo parametro non viene specificato quando si modifica una voce di ruolo di primo livello senza ambito, si verifica un errore.


> [!WARNING]
> Quando si specifica solo il parametro <EM>Parameters</EM>, vengono inclusi nella voce di ruolo solo i parametri specificati nel comando. Tutti gli altri parametri vengono rimossi.



Per specificare un determinato insieme di parametri, utilizzare la seguente sintassi.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -UnscopedTopLevel

In questo esempio viene mostrato come includere soltanto i parametri *Alias*, *DisplayName*, *WidgetConfig* e *Enabled* nel cmdlet **Set-Widget** del ruolo Seattle Mail Recipient Admins.

    Set-ManagementRoleEntry "Seattle Mail Recipient Admins\Set-UMMailbox" -Parameters Alias, DisplayName, WidgetConfig, Enabled -UnscopedTopLevel

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351162\(v=exchg.150\)).

## Altre attività

Una volta modificata una voce di ruolo di primo livello senza ambito, è possibile anche effettuare le seguenti operazioni:

[Aggiungere una voce di ruolo a un ruolo](add-a-role-entry-to-a-role-exchange-2013-help.md)

[Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

[Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md)

[Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[Rimozione di un ruolo da un utente o gruppo di protezione universale](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)


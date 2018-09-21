---
title: 'Creare un ambito normale o esclusivo: Exchange 2013 Help'
TOCTitle: Creare un ambito normale o esclusivo
ms:assetid: b97a5be3-15cc-4954-ba30-a824a95e21be
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351083(v=EXCHG.150)
ms:contentKeyID: 50481533
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un ambito normale o esclusivo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Gli ambiti del ruolo di gestione consentono di determinare gli oggetti disponibili, in modo che l'utente possa modificarli utilizzando i cmdlet e i parametri relativi. Aggiungendo un ambito di gestione, è possibile configurare le assegnazioni dei ruoli di gestione, in modo che gli utenti possano amministrare specifici server, database, destinatari e altri oggetti nell'organizzazione pur rimanendo soggetti a restrizioni per la modifica di altri oggetti.


> [!IMPORTANT]
> Quando si crea un ambito normale o esclusivo, viene sostituito l'ambito di scrittura definito nel ruolo di gestione che si sta assegnando. Non è possibile sostituire l'ambito di lettura configurato per il ruolo di gestione.



È possibile creare un ambito di gestione personalizzato e aggiungere o modificare un'assegnazione di ruolo di gestione. Se si desidera creare un'assegnazione del ruolo di gestione con un ambito di gestione definito in precedenza o relativo a un'unità organizzativa, vedere [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

Per ulteriori informazioni sugli ambiti e le assegnazioni del ruolo di gestione in Microsoft Exchange Server 2013, vedere i seguenti argomenti:

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

Per informazioni sulle altre attività di gestione relative agli ambiti, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ambiti di gestione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passaggio 1: Creazione di un ambito personalizzato

Per creare un ambito personalizzato, scegliere uno dei seguenti tipi di ambito.

## Ambito del filtro destinatario

Gli ambiti basati sui filtri destinatari vengono creati utilizzando il parametro *RecipientRestrictionFilter* nel cmdlet **New-ManagementScope**. Quando si crea un filtro destinatario, è possibile specificare l'unità organizzativa in cui viene eseguita la query del filtro, oltre alle proprietà del destinatario da filtrare. Quando si specifica un'unità organizzativa di base, è possibile limitare ulteriormente l'ambito di scrittura del ruolo.

Per ulteriori informazioni sui filtri dell'ambito di gestione, vedere [Informazioni sui filtri di ambito di gestione dei ruoli](understanding-management-role-scope-filters-exchange-2013-help.md).

Utilizzare la seguente sintassi per creare un ambito con filtro di limitazione dei domini utilizzando un'unità organizzativa di base.

    New-ManagementScope -Name <scope name> -RecipientRestrictionFilter <filter query> [-RecipientRoot <OU>]

Con questo esempio viene creato un ambito che include tutte le cassette postali nell'unità organizzativa contoso.com/Sales OU.

    New-ManagementScope -Name "Mailboxes in Sales OU" -RecipientRestrictionFilter { RecipientType -eq 'UserMailbox' } -RecipientRoot "contoso.com/Sales OU"


> [!NOTE]
> È possibile omettere il parametro <EM>RecipientRoot</EM> se si desidera applicare il filtro all'intero ambito di lettura implicito del ruolo di gestione e non all'interno di un'unità organizzativa specifica.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementScope](https://technet.microsoft.com/it-it/library/dd335137\(v=exchg.150\)).

## Ambito di configurazione del filtro server

Gli ambiti di configurazione basati sui filtri server vengono creati utilizzando il parametro *ServerRestrictionFilter* nel cmdlet **New-ManagementScope**. Un filtro server consente di creare un ambito che si applica unicamente ai server corrispondenti al filtro specificato.

Per ulteriori informazioni sui filtri dell'ambito di gestione e per un elenco delle proprietà filtrabili del server, vedere [Informazioni sui filtri di ambito di gestione dei ruoli](understanding-management-role-scope-filters-exchange-2013-help.md).

Utilizzare la sintassi seguente per creare un ambito del filtro server.

```powershell
New-ManagementScope -Name <scope name> -ServerRestrictionFilter <filter query>
```

In questo esempio viene creato un ambito che include tutti i server all'interno del sito AD 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' (Active Directory).

    New-ManagementScope -Name "Servers in Seattle AD site" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementScope](https://technet.microsoft.com/it-it/library/dd335137\(v=exchg.150\)).

## Ambito di configurazione dell'elenco di server

Gli ambiti di configurazione basati sugli elenchi di server vengono creati utilizzando il parametro *ServerList* nel cmdlet **New-ManagementScope**. Un ambito basato su un elenco di server consente di creare un ambito che si applica unicamente ai server specificati nell'elenco.

Utilizzare la sintassi seguente per creare un ambito basato su un elenco di server.

```powershell
New-ManagementScope -Name <scope name> -ServerList <server 1>, <server 2...>
```

Con questo esempio viene creato un ambito applicato solo a MBX1, MBX3 e MBX5.

```powershell
New-ManagementScope -Name "Mailbox servers" -ServerList MBX1,MBX3,MBX5
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementScope](https://technet.microsoft.com/it-it/library/dd335137\(v=exchg.150\)).

## Ambito di configurazione del filtro di database

Gli ambiti di configurazione basati sui filtri di database vengono creati utilizzando il parametro *DatabaseRestrictionFilter* nel cmdlet **New-ManagementScope**. Un filtro di database consente di creare un ambito che si applica unicamente ai database corrispondenti al filtro specificato.


> [!IMPORTANT]
> Le assegnazioni di ruolo associate agli ambiti dei database sono valide solo per gli utenti che si connettono al server che eseguono Microsoft Exchange Server 2010 Service Pack 1 (SP1) o versione successiva o Exchange 2013. Se un utente assegnato un'assegnazione di ruolo associata a un ambito di database si connette a un server di pre-Exchange&nbsp;2010 SP1, l'assegnazione di ruolo non viene applicata all'utente e all'utente non verrà concesse le autorizzazioni disponibili per l'assegnazione di ruolo.



Per ulteriori informazioni sui filtri dell'ambito di gestione e per ottenere un elenco delle proprietà filtrabili del database, vedere [Informazioni sui filtri di ambito di gestione dei ruoli](understanding-management-role-scope-filters-exchange-2013-help.md).

Utilizzare la sintassi seguente per creare un filtro delle restrizioni del database.

```powershell
New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>
```

In questo esempio viene creato un ambito che include tutti i database contenenti la stringa "Executive" nella proprietà **Name** del database.

    New-ManagementScope -Name "Executive Databases" -DatabaseRestrictionFilter { Name -Like '*Executive*' }

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementScope](https://technet.microsoft.com/it-it/library/dd335137\(v=exchg.150\)).

## Ambito di configurazione dell'elenco di database

Gli ambiti di configurazione basati su elenchi di database vengono creati utilizzando il parametro *DatabaseList* nel cmdlet **New-ManagementScope**. Un ambito basato su un elenco di database consente di creare un ambito che si applica unicamente ai database specificati nell'elenco.


> [!IMPORTANT]
> Le assegnazioni di ruolo associate agli ambiti dei database sono valide solo per gli utenti che si connettono al server che eseguono Microsoft Exchange Server 2010 Service Pack 1 (SP1) o versione successiva o Exchange 2013. Se un utente assegnato un'assegnazione di ruolo associata a un ambito di database si connette a un server di pre-Exchange&nbsp;2010 SP1, l'assegnazione di ruolo non viene applicata all'utente e all'utente non verrà concesse le autorizzazioni disponibili per l'assegnazione di ruolo.



Utilizzare la sintassi seguente per creare un ambito basato su un elenco di database.

```powershell
New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>
```

In questo esempio viene creato un ambito che si applica unicamente ai database Database 1, Database 2 e Database 3.

```powershell
New-ManagementScope -Name "Primary databases" -DatabaseList "Database 1", "Database 2", "Database 3"
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementScope](https://technet.microsoft.com/it-it/library/dd335137\(v=exchg.150\)).

## Ambito esclusivo

Qualsiasi ambito creato con il cmdlet **New-ManagementScope** può essere designato come ambito esclusivo. Per creare un ambito esclusivo si utilizzano gli stessi comandi di una delle precedenti sezioni allo scopo di creare un ambito basato su un filtro destinatari, su un filtro server, su un elenco di server, su un filtro di database o su un elenco di database aggiungendo l'opzione *Exclusive* al comando.


> [!WARNING]
> Quando si creano ambiti di gestione esclusivi, solo gli utenti assegnati ad ambiti esclusivi che contengono oggetti da modificare possono accedere a tali oggetti. Agli oggetti esclusivi, o protetti, possono accedere solo gli amministratori assegnati a un ruolo che dispone dell'ambito esclusivo.



Con questo esempio viene creato un ambito esclusivo basato su un filtro destinatari che corrisponde a qualsiasi utente appartenente al reparto Executives.

    New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive

Per impostazione predefinita, quando viene creato un ambito esclusivo è necessario confermarne la creazione ed essere consapevoli dell'impatto dell'ambito esclusivo sulle assegnazioni di ruolo non esclusive esistenti. Se si desidera eliminare l'avviso, è possibile utilizzare l'opzione *Force*. Con questo esempio viene creato lo stesso ambito dell'esempio precedente, ma senza visualizzare l'avviso.

    New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive -Force

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementScope](https://technet.microsoft.com/it-it/library/dd335137\(v=exchg.150\)).

## Passaggio 2: Aggiunta o modifica di un'assegnazione del ruolo di gestione

Dopo aver creato l'ambito è necessario aggiungerlo a un'assegnazione del ruolo di gestione nuova o esistente.

Se si crea un ambito di gestione e si desidera aggiungerlo a una nuova assegnazione del ruolo di gestione in fase di creazione, vedere i seguenti argomenti:

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

Se si crea un ambito del ruolo di gestione e si desidera aggiungerlo a un'assegnazione del ruolo di gestione esistente, vedere i seguenti argomenti:

  - [Gestire i criteri di assegnazione dei ruoli](manage-role-assignment-policies-exchange-2013-help.md)

  - [Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md)


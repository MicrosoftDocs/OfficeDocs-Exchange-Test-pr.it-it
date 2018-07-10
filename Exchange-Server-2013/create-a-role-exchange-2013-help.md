---
title: 'Creare un ruolo: Exchange 2013 Help'
TOCTitle: Creare un ruolo
ms:assetid: e614ad8f-5946-4135-b130-89ea626afcd4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351214(v=EXCHG.150)
ms:contentKeyID: 50481955
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un ruolo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-17_

È possibile creare un ruolo di gestione, cambiare le voci del ruolo di gestione, aggiungere un ambito (se necessario) e poi assegnare il ruolo agli utenti. È raramente necessario eseguire questa procedura. Si consiglia di controllare se è possibile utilizzare un ruolo di gestione incorporato, invece di creare un ruolo di gestione. Per un elenco dei ruoli di gestione incorporati, vedere [Ruoli di gestione predefiniti](built-in-management-roles-exchange-2013-help.md).

Per ulteriori informazioni sui ruoli di gestione in Microsoft Exchange Server 2013, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).


> [!NOTE]
> In questo argomento non è spiegato come creare un ruolo di gestione privo di ambito. Per informazioni su come creare un ruolo di gestione privo di ambito, vedere <A href="create-an-unscoped-role-exchange-2013-help.md">Creazione di un ruolo senza ambito</A>.



Per informazioni sulle altre attività di gestione relative ai ruoli, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa procedura: 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ruoli di gestione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passaggio 1: Creare il ruolo di gestione

I nuovi ruoli di gestione sono basati sui ruoli esistenti. Quando si crea un ruolo, un ruolo esistente e le relative voci del ruolo di gestione vengono copiati nel nuovo ruolo. Il ruolo esistente diventa l'elemento padre del nuovo ruolo figlio. È sempre necessario scegliere un ruolo contenente tutti i cmdlet e i parametri da utilizzare, rimuovendo quelli non necessari. I ruoli figli non possono contenere voci del ruolo di gestione inesistenti nel ruolo padre.

Per creare un nuovo ruolo, utilizzare la seguente sintassi.

    New-ManagementRole -Parent <existing role to copy> -Name <name of new role>

Con questo esempio viene copiato il ruolo Mail Recipients e le relative voci del ruolo di gestione nel ruolo Seattle Mail Recipients.

    New-ManagementRole -Parent "Mail Recipients" -Name "Seattle Mail Recipients"

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-ManagementRole](https://technet.microsoft.com/it-it/library/dd298073\(v=exchg.150\)).

## Passaggio 2: Modificare le voci del ruolo di gestione del nuovo ruolo

Una volta creato il ruolo, è necessario modificare le voci del ruolo. È possibile rimuovere un'intera voce di ruolo, disabilitando così completamente l'accesso al cmdlet associato. In alternativa, è possibile rimuovere i parametri da una voce di ruolo per disabilitare l'accesso a quegli specifici parametri sul cmdlet associato.

Non è possibile aggiungere nuove voci di ruolo o parametri delle voci di ruolo se non esistono nel ruolo padre. Dato che il nuovo ruolo è stato creato da un ruolo padre nel Passo 1, non è possibile aggiungere altre voci di ruolo o altri parametri alle voci di ruolo, in quanto non esistenti nel ruolo padre.

Quando si modifica la voce di un ruolo, è possibile effettuare una delle seguenti operazioni:

  - Rimuovere una singola voce di ruolo.

  - Rimuovere più voci di ruolo.

  - Rimuovere parametri da una voce di ruolo.

Per rimuovere voci dal nuovo ruolo, vedere [Rimuovere una voce di ruolo da un ruolo](remove-a-role-entry-from-a-role-exchange-2013-help.md).

## Passaggio 3: Creare un ambito del ruolo di gestione personalizzato, se necessario

Gli ambiti del ruolo di gestione determinano gli oggetti disponibili che un utente può visualizzare o modificare utilizzando le voci di ruolo configurate nel passaggio 2. I nuovi ruoli di gestione ereditano gli ambiti del ruolo di gestione di lettura e scrittura del ruolo padre. Sono definiti *ambiti impliciti*. Tuttavia, a volte può essere utile modificare l'ambito di scrittura del nuovo ruolo in conformità alle esigenze aziendali. Quando si crea un ambito personalizzato, viene sostituito l'ambito di scrittura implicito del ruolo. L'ambito di lettura implicito del ruolo non cambia. Per ulteriori informazioni sugli ambiti del ruolo di gestione, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

È possibile creare un ambito personalizzato o un ambito esclusivo, oppure un ambito predefinito o un'ambito di assegnazione a un'unità organizzativa (OU). Il nuovo ambito deve essere contenuto nell'ambito di lettura implicito del ruolo. Per utilizzare un ambito predefinito o per specificare un'unità organizzativa, procedere al passaggio 4.

Per aggiungere un ambito personalizzato al nuovo ruolo, vedere [Creare un ambito normale o esclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

## Passaggio 4: Assegnare il nuovo ruolo di gestione

L'ultima operazione per la creazione e la configurazione di un ruolo è l'assegnazione a un assegnatario di ruolo.

Quando si crea un'assegnazione di ruolo, è possibile utilizzare una delle strategie seguenti:

  - Creare un'assegnazione di ruolo priva di ambito.

  - Creare un'assegnazione di ruolo con un ambito predefinito.

  - Creare un'assegnazione di ruolo con un'unità organizzativa priva di filtro di limitazione del dominio.

  - Creare l'assegnazione di ruolo con l'ambito personalizzato o esclusivo creato nel passaggio 3.
    

    > [!NOTE]
    > Non è possibile specificare un ambito quando si crea un'assegnazione tra un ruolo e un criterio di assegnazione del ruolo di gestione.



È possibile assegnare il nuovo ruolo a un gruppo di ruolo, a un criterio di assegnazione del ruolo, a un utente o a un gruppo di protezione universale (USG). Per ulteriori informazioni, vedere gli argomenti seguenti:

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Gestire i criteri di assegnazione dei ruoli](manage-role-assignment-policies-exchange-2013-help.md)

  - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)


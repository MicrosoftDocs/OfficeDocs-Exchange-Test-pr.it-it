---
title: 'Assegnare le autorizzazioni di eDiscovery di Exchange: Exchange 2013 Help'
TOCTitle: Assegnare le autorizzazioni di eDiscovery di Exchange
ms:assetid: 729e09d8-614b-431f-ae04-ae41fb4c628e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298059(v=EXCHG.150)
ms:contentKeyID: 50480878
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Assegnare le autorizzazioni di eDiscovery di Exchange

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-10-02_

Se si desidera che gli utenti siano in grado di utilizzare Microsoft Exchange Server 2013 In-Place eDiscovery, è innanzitutto necessario autorizzare li aggiungendoli al gruppo di ruoli gestione individuazione. Membri del gruppo di ruoli Gestione individuazione dispongono delle autorizzazioni di accesso completo della cassetta postale per la cassetta postale di individuazione che viene creato da Exchange il programma di installazione.


> [!WARNING]
> Membri del gruppo di ruoli gestione individuazione possono accedere al contenuto di messaggi sensibili. In particolare, i membri possono utilizzare <A href="in-place-ediscovery-exchange-2013-help.md">eDiscovery sul posto</A> di ricerca tutte le cassette postali dell'organizzazione di Exchange, anteprima messaggi (e altri elementi delle cassette postali), copiarli in una cassetta postale di individuazione ed esportare i messaggi copiati in un file pst. Nella maggior parte delle organizzazioni, questa autorizzazione viene concessa a legali, conformità o reparto risorse umane personale.<BR>



Per ulteriori informazioni sul gruppo di ruoli gestione individuazione, vedere [Gestione individuazione](discovery-management-exchange-2013-help.md). Per ulteriori informazioni sui ruoli basati su Access controllo (RBAC), vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

Ulteriori informazioni sugli scenari in cui si utilizza questa procedura Vedere i seguenti argomenti:

  - [Creazione di una ricerca eDiscovery sul posto](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [Creare o rimuovere un'archiviazione sul posto](create-or-remove-an-in-place-hold-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Gruppi di ruoli" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md) .

  - Per impostazione predefinita, il gruppo di ruoli Gestione individuazione non contiene alcun membro. Gli amministratori con il ruolo Gestione organizzazione sono inoltre non è possibile creare o gestire ricerche individuazione senza viene aggiunto al gruppo di ruoli Gestione individuazione.

  - In Exchange 2013, i membri del gruppo di ruoli Gestione organizzazione possono creare un [Archiviazione sul posto e conservazione per controversia legale](in-place-hold-and-litigation-hold-exchange-2013-help.md) per tutto il contenuto delle cassette postali di mettere in attesa. Per creare un'archiviazione sul posto basata su query, tuttavia, l'utente deve essere un membro del gruppo di ruoli gestione individuazione o assegnato il ruolo cassetta postale di ricerca.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Utilizzare EAC per aggiungere un utente al gruppo di ruoli gestione individuazione

1.  Accedere ad **autorizzazioni** \> **ruoli amministratore**.

2.  Nella visualizzazione elenco, selezionare **Gestione individuazione** e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica")

3.  Nel **Gruppo di ruoli** in **membri**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  In **Seleziona membri**, selezionare uno o più utenti, fare clic su **Aggiungi** e quindi fare clic su **OK**.

5.  Nel **Gruppo di ruoli**, fare clic su **Salva**.

## Utilizzo della Shell per aggiungere un utente al gruppo di ruoli gestione individuazione

In questo esempio aggiunge l'utente Bsuneja al gruppo di ruoli gestione individuazione.

    Add-RoleGroupMember -Identity "Discovery Management" -Member Bsuneja

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Add-RoleGroupMember](https://technet.microsoft.com/it-it/library/dd638207\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'utente si è aggiunti al gruppo di ruoli gestione individuazione, eseguire le operazioni seguenti:

1.  In EAC, andare a **autorizzazioni** \> **ruoli amministratore**.

2.  Nella visualizzazione elenco, selezionare **Gestione individuazione**.

3.  Nel riquadro dei dettagli verificare che l'utente è elencato nella sezione **membri**.

È inoltre possibile eseguire questo comando per elencare i membri del gruppo di ruoli gestione individuazione.

    Get-RoleGroupMember -Identity "Discovery Management"


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



---
title: "Installare o rimuovere applicazioni per Outlook per l'organizzazione: Exchange 2013 Help"
TOCTitle: Installare o rimuovere applicazioni per Outlook per l'organizzazione
ms:assetid: 112f3ef7-9943-4a1e-8a42-e08e8e9f67f4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ943752(v=EXCHG.150)
ms:contentKeyID: 52063045
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Installare o rimuovere applicazioni per Outlook per l'organizzazione

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2017-02-03_

È possibile installare o rimuovere componenti aggiuntivi per Outlook per l'organizzazione tramite EAC o Shell.


> [!NOTE]
> Per impostazione predefinita, dopo aver installato un componente aggiuntivo per la propria organizzazione, il componente aggiuntivo è disponibile per tutti gli utenti nell'organizzazione. Dopo l'installazione, è possibile utilizzare EAC o Shell per verificare il componente aggiuntivo facoltativo o obbligatorio per gli utenti e specificare se si desidera che il componente aggiuntivo per attivare o disattivare. Per informazioni su come modificare le impostazioni predefinite per un componente aggiuntivo, vedere <A href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Gestione dell'accesso degli utenti alle app per Outlook</A>. Per limitare la disponibilità dei componenti aggiuntivi a specifici utenti all'interno dell'organizzazione, è necessario utilizzare la Shell. Per ulteriori informazioni, vedere <A href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Gestione dell'accesso degli utenti alle app per Outlook</A>.



Per altre attività di gestione, vedere [App per Outlook](add-ins-for-outlook-exchange-2013-help.md).

## Informazioni necessarie prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "App per Outlook" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md) .

  - È possibile assegnare amministratori le autorizzazioni per installare e gestire i componenti aggiuntivi per l'organizzazione. È inoltre possibile assegnare agli utenti l'autorizzazione per installare e gestire i componenti aggiuntivi per uso personale. Per ulteriori informazioni, vedere [Specificare gli amministratori e gli utenti in grado di installare e gestire componenti aggiuntivi per Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

  - Accesso all'archivio di Office non è supportato per le cassette postali o organizzazioni in aree specifiche. Se non viene visualizzata **Add da Office Store** come un'opzione nell' **interfaccia di amministrazione di Exchange** in **organizzazione** \> **aggiunte** \> ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), è possibile installare un componente aggiuntivo per Outlook da un percorso URL o il file. Per ulteriori informazioni, contattare il provider di servizi.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Installare un componente aggiuntivo per Outlook

## Utilizzare EAC per aggiungere un componente aggiuntivo

1.  Amministrazione di Exchange, andare a **organizzazione** \> **componenti aggiuntivi**.

2.  Fare clic su **New**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi")e quindi scegliere il percorso che si desidera installare il componente aggiuntivo da.
    
      - **Aggiungere da Office Store**. In Office Store, selezionare l'applicazione che si desidera installare e quindi fare clic su **Aggiungi**. Applicazioni che interagiscono con Outlook Web App sono elencate in **componenti aggiuntivi per Office e SharePoint** \> **Outlook**.
        

        > [!NOTE]
        > Accesso all'archivio di Office non è supportato per le cassette postali o organizzazioni in aree specifiche. Se non viene visualizzata <STRONG>Aggiungi da Office Store</STRONG> come un'opzione nell' <STRONG>interfaccia di amministrazione di Exchange</STRONG> in <STRONG>organizzazione</STRONG> &gt; <STRONG>Add-ins</STRONG> &gt; <IMG title="Icona Aggiungi" alt="Icona Aggiungi" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif">, è possibile installare un componente aggiuntivo per Outlook da un percorso URL o il file. Per ulteriori informazioni, contattare il provider di servizi.

    
      - **Aggiungere dall'URL**. In **URL** immettere l'URL completo per il componente aggiuntivo per file manifesto che si desidera installare.
    
      - **Aggiungi file**. Selezionare **Sfoglia** e quindi passare alla posizione del componente aggiuntivo file manifesto che si desidera installare.

3.  Fare clic su **Salva**.

## Utilizzo della Shell per aggiungere un componente aggiuntivo

Questo esempio viene illustrato come aggiungere un componente aggiuntivo da un URL.

    New-App -OrganizationApp -Url <URL location for add-in manifest file>

Questo esempio viene illustrato come aggiungere un componente aggiuntivo da un file.

    New-App -OrganizationApp -FileData <File location for add-in manifest file>


> [!TIP]
> Quando si utilizza Shell per installare un componente aggiuntivo per l'organizzazione, è possibile installare il componente aggiuntivo e configurare le relative impostazioni contemporaneamente.



Per informazioni sulla sintassi e sui parametri, vedere [New-App](https://technet.microsoft.com/it-it/library/jj218722\(v=exchg.150\)).

## Rimuovere un componente aggiuntivo per Outlook

## Utilizzare EAC per rimuovere un componente aggiuntivo

1.  In EAC, andare a **organizzazione** \> **componenti aggiuntivi**.

2.  In questo elenco, selezionare l'app che si desidera rimuovere, quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

## Utilizzo della Shell per rimuovere un componente aggiuntivo

È possibile utilizzare la Shell per rimuovere un componente aggiuntivo dall'organizzazione.


> [!NOTE]
> Eseguire il comando seguente per cercare i nomi visualizzati e gli ID applicazione per tutti i componenti aggiuntivi per Outlook per l'organizzazione.



    Get-App -OrganizationApp |FL DisplayName,AppID

Eseguire il comando seguente per rimuovere il personalizzato aggiuntivo Finance Test componente aggiuntivo dall'organizzazione.

    Remove-App -OrganizationApp -Identity <GUID for Finance Test Add-in>

Per informazioni sulla sintassi e sui parametri, vedere [Remove-App](https://technet.microsoft.com/it-it/library/jj218709\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per visualizzare i componenti aggiuntivi installati nella propria organizzazione, effettuare una delle operazioni seguenti:

  - In EAC, andare a **organizzazione** \> **componenti aggiuntivi** e quindi esaminare l'elenco dei componenti aggiuntivi installati.

  - Nella shell, eseguire `Get-App`e quindi rivedere l'elenco dei componenti aggiuntivi installati.


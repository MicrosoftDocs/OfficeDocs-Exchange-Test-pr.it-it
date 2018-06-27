---
title: 'Specificare gli amministratori e gli utenti in grado di installare e gestire componenti aggiuntivi per Outlook: Exchange 2013 Help'
TOCTitle: Specificare gli amministratori e gli utenti in grado di installare e gestire componenti aggiuntivi per Outlook
ms:assetid: 7ee4302d-b8bb-40a0-9810-10d3a0271bcb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ943754(v=EXCHG.150)
ms:contentKeyID: 52063114
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Specificare gli amministratori e gli utenti in grado di installare e gestire componenti aggiuntivi per Outlook

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2017-02-08_

È possibile specificare quali amministratori nell'organizzazione abbiano le autorizzazioni per installare e gestire i componenti aggiuntivi per Outlook. Inoltre è possibile specificare quali utenti nell'organizzazione abbiano le autorizzazioni per installare e gestire i componenti aggiuntivi per il proprio utilizzo.

È possibile eseguire questa operazione assegnando oppure rimuovendo ruoli di gestione specifici ai componenti aggiuntivi. Sono disponibili 5 ruoli integrati da usare.

Ruoli amministrativi

  - **App Marketplace per l'org**   Consente all'amministratore di installare e gestire i componenti aggiuntivi disponibili da Office Store per l'organizzazione.

  - **App personalizzate per l'org**   Consente all'amministratore di installare e gestire i componenti aggiuntivi personalizzati per l'organizzazione.

Ruoli utente

  - **App Marketplace**   Consente all'utente di installare e gestire i componenti aggiuntivi dell'Office Store per il proprio utilizzo.

  - **App personalizzate**   Consente all'utente di installare e gestire i componenti aggiuntivi personalizzati per il proprio utilizzo.

  - **App ReadWriteMailbox personali**   Consentono a un utente di installare e gestire i componenti aggiuntivi che necessitano del livello di autorizzazione ReadWriteMailbox nel proprio file manifesto.

Per impostazione predefinita, tutti gli amministratori con ruolo **Gestione organizzazione** dispongono di entrambi i ruoli amministrativi. Per impostazione predefinita, gli utenti finali dispongono dei ruoli precedentemente citati.

Per informazioni su ognuno di questi ruoli, vedere [Ruolo App Marketplace dell'organizzazione](org-marketplace-apps-role-exchange-2013-help.md), [Ruolo dell'organizzazione personalizzato App](org-custom-apps-role-exchange-2013-help.md), [Il ruolo App Marketplace](my-marketplace-apps-role-exchange-2013-help.md), [Il ruolo personalizzato App](my-custom-apps-role-exchange-2013-help.md) e [Il ruolo ReadWriteMailbox App](my-readwritemailbox-apps-role-exchange-2013-help.md).

Per informazioni sui componenti aggiuntivi, vedere [App per Outlook](add-ins-for-outlook-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per poter eseguire questo cmdlet, è necessario disporre delle autorizzazioni appropriate. Sebbene in questo argomento vengano elencati tutti i parametri relativi al cmdlet, è possibile che alcuni di essi non siano accessibili se non sono inclusi nelle autorizzazioni di cui si dispone. Per sapere quali autorizzazioni sono necessarie, vedere "Assegnazioni ruolo" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - L'accesso all'Office Store non è supportato per le cassette postali o per le organizzazioni di specifiche aree geografiche. Se non si visualizza l'opzione **Aggiungi da Office Store** nell'**interfaccia di amministrazione di Exchange** in **Organizzazione** \> **Componenti aggiuntivi** \> ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), è possibile installare un componente aggiuntivo per Outlook tramite URL o percorso file. Per ulteriori informazioni, contattare il provider di servizi.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Assegnazione agli amministratori delle autorizzazioni necessarie per installare e gestire i componenti aggiuntivi per l'organizzazione

## Utilizzare EAC per assegnare autorizzazioni agli amministratori

È possibile utilizzare EAC per assegnare agli amministratori le autorizzazioni necessarie per installare e gestire i componenti aggiuntivi disponibili dall'Office Store per l'organizzazione. Per informazioni dettagliate su tale operazione, vedere [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

## Assegnare agli utenti le autorizzazioni necessarie per installare e gestire i componenti aggiuntivi per il proprio utilizzo

## Utilizzare EAC per assegnare autorizzazioni agli utenti

È possibile utilizzare EAC per assegnare agli utenti le autorizzazioni necessarie per visualizzare e modificare i componenti aggiuntivi personalizzati per il proprio utilizzo. Per informazioni dettagliate su tale operazione, vedere [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta assegnazione delle autorizzazione a un utente, eseguire un comando Shell utilizzando il formato `Get-ManagementRoleAssignment -Role <Role Name> -GetEffectiveUsers`, in cui `Role Name` è il ruolo per il quale si desidera verificare le autorizzazioni assegnate.

In questo esempio viene mostrato come verificare a quale persona sono state assegnate le autorizzazioni per installare i componenti aggiuntivi dall'Office Store per l'organizzazione.

1.  Eseguire `Get-ManagementRoleAssignment -Role "Org Marketplace Apps" -GetEffectiveUsers`.

2.  Nei risultati, esaminare le voci nella colonna **Utenti interessati**.

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).


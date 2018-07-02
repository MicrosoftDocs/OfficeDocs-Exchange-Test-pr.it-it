---
title: 'App per Outlook: Exchange 2013 Help'
TOCTitle: App per Outlook
ms:assetid: 28b6f2a1-a235-4023-b561-6fd304962775
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ943753(v=EXCHG.150)
ms:contentKeyID: 52063038
ms.date: 05/05/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# App per Outlook

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2017-03-13_

**Riepilogo:**  Viene fornita una panoramica dei componenti aggiuntivi per Outlook, compatibili con Outlook su computer Windows e MacIntosh, su dispositivi mobili, in Outlook Web App e in Outlook sul web.

I componenti aggiuntivi per Outlook sono applicazioni che estendono l'utilità dei client di Outlook aggiungendo informazioni o strumenti che gli utenti possono utilizzare senza dover uscire da Outlook. I componenti aggiuntivi vengono integrati dagli sviluppatori di terze parti e possono essere installati da un file, da un URL o da Office Store. Per impostazione predefinita, tutti gli utenti possono installare componenti aggiuntivi. Gli amministratori di Exchange possono utilizzare i ruoli per controllare l'installazione di componenti aggiuntivi eseguita dagli utenti.


> [!TIP]
> Per informazioni su componenti aggiuntivi per Outlook dalla prospettiva di un utente finale, leggere l'argomento della guida relativo ai <A href="https://go.microsoft.com/fwlink/p/?linkid=282387">componenti aggiuntivi installati</A> su Office.com. Tale argomento offre una panoramica di dei componenti aggiuntivi e mostra alcuni componenti aggiuntivi per Outlook che potrebbero essere installati per impostazione predefinita.



## Componenti aggiuntivi di Office Store e componenti aggiuntivi personalizzati

Il client di Outlook supporta diversi componenti aggiuntivi disponibili in Office Store. Outlook supporta inoltre componenti aggiuntivi personalizzati che possono essere creati e distribuiti agli utenti dell'organizzazione.


> [!NOTE]
> L'accesso all'Office Store non è supportato per le cassette postali o per le organizzazioni di specifiche aree geografiche. Se non si visualizza l'opzione <STRONG>Aggiungi da Office Store</STRONG> nell'<STRONG>interfaccia di amministrazione di Exchange</STRONG> in <STRONG>Organizzazione</STRONG> &gt; <STRONG>Componenti aggiuntivi</STRONG> &gt; <IMG title="Icona Aggiungi" alt="Icona Aggiungi" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif">, è possibile installare un componente aggiuntivo per Outlook tramite URL o percorso file. Per ulteriori informazioni, contattare il provider di servizi.




> [!NOTE]
> Alcuni componenti aggiuntivi per Outlook vengono installati per impostazione predefinita. I componenti aggiuntivi predefiniti di Outlook funzionano solo con contenuti in lingua inglese. Ad esempio, gli indirizzi postali tedeschi nel corpo del messaggio non attiveranno il componente aggiuntivo Mappe di Bing.



## Accesso e installazione dei componenti aggiuntivi

Per impostazione predefinita, tutti gli utenti possono installare e rimuovere componenti aggiuntivi. Gli amministratori di Exchange hanno una serie di controlli disponibili per la gestione dei componenti aggiuntivi e del loro utilizzo da parte degli utenti. Gli amministratori possono impedire agli utenti di installare i componenti aggiuntivi che non vengono scaricati dall'Office Store (invece sono trasferiti tramite sideload da un file o URL). Gli amministratori possono impedire agli utenti di installare i componenti aggiuntivi dell'Office Store e di installare i componenti aggiuntivi per conto di altri utenti. È anche possibile assegnare agli utenti un ruolo che consenta loro di installare componenti aggiuntivi per l'organizzazione o per un sottoinsieme di utenti dell'organizzazione.

Per impedire agli utenti di installare un componente aggiuntivo che non proviene dall'Office Store, rimuovere il ruolo **App personalizzate** di tali utenti. Per impedire agli utenti di installare un componente aggiuntivo che proviene dall'Office Store, rimuovere il ruolo **App del Marketplace** di tali utenti. Per ulteriori dettagli, vedere [Specificare gli amministratori e gli utenti in grado di installare e gestire componenti aggiuntivi per Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

Per installare componenti aggiuntivi per alcuni o tutti gli utenti dell'organizzazione, vedere [Installare o rimuovere applicazioni per Outlook per l'organizzazione](install-or-remove-add-ins-for-outlook-for-your-organization-exchange-2013-help.md).

Se necessario, è possibile limitare la disponibilità di un componente aggiuntivo a utenti specifici nell'organizzazione. Per ulteriori informazioni, vedere [Gestione dell'accesso degli utenti alle app per Outlook](manage-user-access-to-add-ins-for-outlook-exchange-online-help.md).

## Operazioni amministrative comuni con componenti aggiuntivi per Outlook

Esistono due scenari comuni che gli amministratori di Exchange possono gestire nella propria organizzazione.

**Se si desidera impedire agli utenti finali di installare i componenti aggiuntivi per Outlook su tutti i client di Outlook, apportare le modifiche seguenti ai ruoli nell'interfaccia di amministrazione di Exchange**:

  - Per impedire agli utenti di installare un componente aggiuntivo dell'Office Store, rimuovere il ruolo **Marketplace** di tali utenti.

  - Per impedire agli utenti di caricare un componente aggiuntivo da origini diverse dall'Office Store, rimuovere il ruolo **App personalizzate** di tali utenti.

  - Per impedire agli utenti di installare tutti i componenti aggiuntivi, rimuovere entrambi i ruoli di tali utenti indicati in precedenza.

Per ulteriori informazioni, vedere [Specificare gli amministratori e gli utenti in grado di installare e gestire componenti aggiuntivi per Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

**Se gli utenti finali al momento sono in grado di accedere ai componenti aggiuntivi e si desidera rimuovere tale accesso, usare il cmdlet `Get-App` per visualizzare quali componenti aggiuntivi ha installato ogni utente.**

Successivamente, utilizzare il cmdlet `Remove-App` per rimuovere i componenti aggiuntivi da uno o più utenti. 

Per ulteriori informazioni, vedere [Get-App](https://technet.microsoft.com/it-it/library/jj218673\(v=exchg.150\)) e [Remove-App](https://technet.microsoft.com/it-it/library/jj218709\(v=exchg.150\)) per Exchange 2013. Per Exchange Online o Exchange 2016, andare [qui](https://go.microsoft.com/fwlink/p/?linkid=844721).

## Consentire ad amministratori e utenti di installare componenti aggiuntivi

È possibile specificare quali amministratori nell'organizzazione abbiano l'autorizzazione necessaria per installare e gestire i componenti aggiuntivi per Outlook. Inoltre è possibile specificare quali utenti nell'organizzazione abbiano le autorizzazioni per installare e gestire i componenti aggiuntivi per il proprio utilizzo. Per ulteriori informazioni, vedere [Specificare gli amministratori e gli utenti in grado di installare e gestire componenti aggiuntivi per Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).


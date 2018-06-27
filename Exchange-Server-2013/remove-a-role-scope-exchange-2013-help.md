---
title: 'Rimuovere un ambito di ruolo: Exchange 2013 Help'
TOCTitle: Rimuovere un ambito di ruolo
ms:assetid: ad17cba0-a8d3-4f40-b3c9-c37e6e5c3f36
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351051(v=EXCHG.150)
ms:contentKeyID: 50481413
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere un ambito di ruolo

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-02_

Gli ambiti del ruolo di gestione determinano gli oggetti messi a disposizione di un utente, che può così modificare gli oggetti utilizzando i cmdlet e i parametri assegnati all'utente. Se un ambito non è più in uso, è possibile eliminarlo. Per ulteriori informazioni sugli ambiti del ruolo di gestione in Microsoft Exchange Server 2013, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ambiti di gestione" nell'argomento[Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Prima di eliminare un ambito è necessario rimuoverlo da qualsiasi assegnazione del ruolo di gestione che lo utilizza. Per ulteriori informazioni sull'eliminazione di un ambito da un'assegnazione di ruolo, vedere [Modificare un'assegnazione di ruolo](change-a-role-assignment-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Eliminazione di un ambito tramite Shell

Per eliminare un ambito, utilizzare la seguente sintassi:

    Remove-ManagementScope <scope name>

Ad esempio, per eliminare l'ambito "Dublin Servers", utilizzare il comando riportato di seguito.

    Remove-ManagementScope "Dublin Servers"


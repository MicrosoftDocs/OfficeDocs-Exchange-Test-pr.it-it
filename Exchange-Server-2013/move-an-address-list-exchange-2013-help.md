---
title: 'Spostamento di un elenco di indirizzi: Exchange 2013 Help'
TOCTitle: Spostamento di un elenco di indirizzi
ms:assetid: c843bbd5-6c0e-41e1-b749-7ae87c1beb25
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124534(v=EXCHG.150)
ms:contentKeyID: 50481651
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Spostamento di un elenco di indirizzi

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-14_

In questo argomento viene descritto come spostare un elenco di indirizzi esistente in un nuovo contenitore nell'elenco di indirizzi radice.

Per altre attività di gestione relative agli elenchi di indirizzi, vedere [Procedure dell'elenco indirizzi](address-list-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Elenchi indirizzi" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Spostamento di un elenco indirizzi tramite Shell

In questo esempio viene utilizzato il GUID di un elenco indirizzi per spostare l'elenco indirizzi nel contenitore Building4, situato all'interno del contenitore All Users\\Sales.

    Move-AddressList -Identity c3fffd8e-026b-41b9-88c4-8c21697ac8ac -Target "\All Users\Sales\Building4"

Digitare **S** per confermare lo spostamento dell'elenco di indirizzi, quindi premere INVIO.

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Move-AddressList](https://technet.microsoft.com/it-it/library/bb124520\(v=exchg.150\)).


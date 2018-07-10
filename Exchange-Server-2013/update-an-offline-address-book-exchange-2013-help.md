---
title: 'Aggiornare una Rubrica fuori rete: Exchange 2013 Help'
TOCTitle: Aggiornare una Rubrica fuori rete
ms:assetid: 448a207e-41b4-4cef-9fe9-a68b81e2ec4e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997684(v=EXCHG.150)
ms:contentKeyID: 50480486
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiornare una Rubrica fuori rete

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-11-15_

Dopo aver creato una Rubrica offline o averne modificato le impostazioni, le modifiche saranno visualizzabili solo al completamento del processo di generazione della Rubrica stessa (OABGen).

Per altre attività di gestione relative alle rubriche offline, vedere [Procedure della Rubrica fuori rete](offline-address-book-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Rubriche offline" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo di Shell per l'aggiornamento di una Rubrica offline

In questo esempio, viene aggiornata la Rubrica offline denominata My OAB.

    Update-OfflineAddressBook -Identity "My OAB"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Update-OfflineAddressBook](https://technet.microsoft.com/it-it/library/aa995979\(v=exchg.150\)).


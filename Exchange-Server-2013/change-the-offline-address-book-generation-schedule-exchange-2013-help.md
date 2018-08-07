---
title: 'Modifica pianificazione generazione Rubrica offline: Exchange 2013 Help'
TOCTitle: Modificare la pianificazione di generazione della Rubrica offline
ms:assetid: d2b4d527-311e-442d-9f1f-54fac8371b80
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124719(v=EXCHG.150)
ms:contentKeyID: 50481729
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.OfflineAddressBookGeneralPage
ms.translationtype: MT
---

# Modificare la pianificazione di generazione della Rubrica offline

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-12-05_

Una Rubrica offline è una copia di una rubrica scaricata in modo tale da consentire a un utente di Outlook di accedere alle informazioni contenute quando è disconnesso dal server. È possibile configurare la frequenza di generazione della rubrica offline utilizzando i parametri *OABGeneratorWorkCycle* e *OABGeneratorWorkCycleCheckpoint* sul cmdlet Set-MailboxServer.

Per altre attività di gestione relative alle rubriche offline, vedere [Procedure della Rubrica fuori rete](offline-address-book-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Rubriche offline" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare la shell per configurare le proprietà della Rubrica offline

Con questo esempio viene generata la rubrica offline ogni sei ore ogni giorno sul server Cassette postali, MBXServer01.

    Set-MailboxServer -Identity MBXServer01 -OABGeneratorWorkCycle 01.00:00:00 -OABGeneratorWorkCycleCheckpoint 06:00:00 

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OfflineAddressBook](https://technet.microsoft.com/it-it/library/aa996330\(v=exchg.150\)).


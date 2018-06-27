---
title: 'Configurazione delle proprietà di distribuzione della Rubrica offline: Exchange 2013 Help'
TOCTitle: Configurazione delle proprietà di distribuzione della Rubrica offline
ms:assetid: 8df985e9-75ba-47ea-9cc3-aa98a5d8acf4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123710(v=EXCHG.150)
ms:contentKeyID: 50481150
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.ClientAccess.OabDistributionGeneralPage
ms.translationtype: MT
---

# Configurazione delle proprietà di distribuzione della Rubrica offline

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-14_

Per ogni punto di distribuzione della rubrica offline (OAB) in Exchange, è possibile configurare due URL: un URL interno a cui è possibile accedere solo dalla rete aziendale interna e un URL esterno a cui si può accedere da Internet.

Per altre attività di gestione relative alle rubriche offline, vedere [Procedure della Rubrica fuori rete](offline-address-book-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Rubriche offline" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurazione delle proprietà di distribuzione della Rubrica offline tramite Shell

In questo esempio, viene impostato l'intervallo di polling per la distribuzione della Rubrica Offline sulla directory virtuale della Rubrica offline (Sito Web predefinito) su sei ore.

    Set-OABVirtualDirectory "OAB (Default Web Site)" -PollInterval 360

In questo esempio, viene impostato il punto di distribuzione esterno su https://contoso.com/OAB per la l'intervallo di polling per la directory virtuale della Rubrica offline (Sito Web predefinito).

    Set-OABVirtualDirectory "OAB (Default Web Site)" -ExternalUrl https://contoso.com/OAB

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OabVirtualDirectory](https://technet.microsoft.com/it-it/library/bb124707\(v=exchg.150\)).

## Per ulteriori informazioni

[Rubriche offline](offline-address-books-exchange-2013-help.md)


---
title: 'Trovare gli URL interni ed esterni per il centro di amministrazione di Exchange: Exchange 2013 Help'
TOCTitle: Trovare gli URL interni ed esterni per il centro di amministrazione di Exchange
ms:assetid: 3ddb30ff-a405-4b9d-8d77-2d7a3a5ab8fa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ680108(v=EXCHG.150)
ms:contentKeyID: 50480423
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Trovare gli URL interni ed esterni per il centro di amministrazione di Exchange

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-02-04_

Dal momento che l'interfaccia di amministrazione di Exchange è una console di gestione basata sul Web in Exchange Server 2013, è possibile accedervi utilizzando l'URL della directory virtuale del Pannello di controllo di Exchange (ECP) in un browser. In questo argomento è spiegato come trovare l'URL della directory virtuale del Pannello di controllo di Exchange.


> [!NOTE]
> Il Pannello di controllo di Exchange è l'interfaccia utente basata sul Web sviluppata per Exchange Server 2010. I cmdlet dell'interfaccia di amministrazione di Exchange per le directory virtuali utilizzano ancora la dicitura "ECP" nel nome e questi cmdlet possono essere utilizzati per gestire le directory virtuali del Pannello di controllo di Exchange in Exchange&nbsp;2010 ed Exchange 2013.



Per ulteriori informazioni sull'interfaccia di amministrazione di Exchange, vedere [Interfaccia di amministrazione di Exchange in Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettività di Interfaccia di amministrazione di Exchange" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo di Shell per l'individuazione degli URL interni ed esterni per la directory virtuale del Pannello di controllo di Exchange

In questo esempio, il nome della directory virtuale del Pannello di controllo di Exchange, l'URL interno e l'URL esterno vengono visualizzati in un elenco formattato.

    Get-ECPVirtualDirectory | Format-List Name,InternalURL,ExternalURL

Una volta completato il comando, utilizzare il valore *InternalURL* o *ExternalURL* nel browser per avviare l'interfaccia di amministrazione di Exchange.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-EcpVirtualDirectory](https://technet.microsoft.com/it-it/library/dd351058\(v=exchg.150\)).


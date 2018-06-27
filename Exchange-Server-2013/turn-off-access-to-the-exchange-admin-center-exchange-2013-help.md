---
title: "Disattivare l'accesso all'interfaccia di amministrazione di Exchange: Exchange 2013 Help"
TOCTitle: Disattivare l'accesso all'interfaccia di amministrazione di Exchange
ms:assetid: 49f4fa77-1722-4703-81c9-8724ae0334fb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ218639(v=EXCHG.150)
ms:contentKeyID: 50480534
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disattivare l'accesso all'interfaccia di amministrazione di Exchange

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-05-20_

Per motivi di sicurezza, alcune organizzazioni potrebbero voler limitare l'accesso all'interfaccia di amministrazione di Exchange da parte di utenti da Internet. Questa procedura illustra come disattivare l'accesso all'interfaccia di amministrazione di Exchange. Questa procedura non impedisce agli utenti di accedere a Opzioni in Outlook Web App.


> [!NOTE]
> Questa procedura disattiva l'accesso all'interfaccia di amministrazione di Exchange sul server CAS, sul quale viene applicata la procedura. Per abilitare l'interfaccia di amministrazione di Exchange agli utenti interni, è necessario installare un server CAS separato e configurarlo solo per gestire le richieste interne utilizzando il seguente comando:<BR><CODE>Set-ECPVirtualDirectory -Identity "InternalCAS\ecp (default web site)" -AdminEnabled $True</CODE>




> [!WARNING]
> La procedura si applica solo alle distribuzioni locali di Exchange Server 2013.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettività di Interfaccia di amministrazione di Exchange" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo di Shell per la disattivazione dell'accesso tramite Internet all'interfaccia di amministrazione di Exchange

In questo esempio viene disattivato l'accesso a EAC sul server CAS01.

    Set-ECPVirtualDirectory -Identity "CAS01\ecp (default web site)" -AdminEnabled $false

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-EcpVirtualDirectory](https://technet.microsoft.com/it-it/library/dd297991\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente disattivato l'accesso all'interfaccia di amministrazione di Exchange, attenersi alla seguente procedura:

1.  Utilizzando il browser Internet, digitare l'URL esterno o interno dell'organizzazione per l'accesso a Outlook Web App sostituendo l'identificatore **/owa** con **/ecp**. Ad esempio, se l'URL esterno per accedere a Outlook Web App è https://primary.tailspintoys.com/owa, utilizzare https://primary.tailspintoys.com/ecp.

2.  Se l'accesso è disattivato, verrà visualizzato un errore **404 – sito Web non trovato**.


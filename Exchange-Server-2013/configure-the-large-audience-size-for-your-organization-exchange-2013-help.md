---
title: "Configura gruppo destinatari grande per l'organizzazione: Exchange 2013 Help"
TOCTitle: Configurare le dimensioni di grandi dimensioni gruppo di destinatari per l'organizzazione
ms:assetid: 8a37911c-4339-4921-b5d3-0a5a774d4517
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ659068(v=EXCHG.150)
ms:contentKeyID: 50481107
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare le dimensioni di grandi dimensioni gruppo di destinatari per l'organizzazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

È possibile utilizzare Exchange Management Shell per configurare numerose impostazioni che definiscono il modo in cui vengono utilizzati gli avvisi relativi ai messaggi all'interno dell'organizzazione.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Suggerimenti messaggio" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurazione delle dimensioni relative al pubblico esteso per l'organizzazione tramite Shell

Non è possibile utilizzare il cmdlet **Set-OrganizationConfig** per configurare le dimensioni relative al pubblico esteso per l'organizzazione. Quando i mittenti indirizzano i messaggi a un numero di destinatari maggiore rispetto alle dimensioni configurate, viene loro visualizzato un suggerimento messaggio per il pubblico esteso. Per impostazione predefinita, le dimensioni relative al pubblico esteso sono impostate su 25. In questo esempio, vengono configurate le dimensioni relative al pubblico esteso su 50 all'interno dell'organizzazione.

    Set-OrganizationConfig -MailTipsLargeAudienceThreshold 50

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\)).


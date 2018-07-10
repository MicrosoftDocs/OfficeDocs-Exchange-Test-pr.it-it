---
title: 'Configurare un dominio remoto risposte fuori sede: Exchange 2013 Help'
TOCTitle: Configurare un dominio remoto risposte fuori sede
ms:assetid: 0c1e56be-7a29-4294-9762-600f9f788741
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657713(v=EXCHG.150)
ms:contentKeyID: 50480011
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare un dominio remoto risposte fuori sede

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

È possibile utilizzare Exchange Management Shell per configurare il modo in cui i messaggi di posta elettronica vengono inviati e ricevuti tramite i domini remoti. Di seguito è spiegato come utilizzare Exchange Management Shell per configurare il modo in cui Exchange gestisce le risposte di fuori sede.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere°"Domini remoti" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo di Shell per la configurazione delle risposte di fuori sede

Il cmdlet **Set-RemoteDomain** consente di configurare le proprietà di un dominio remoto.

In questo esempio vengono disabilitati i messaggi di fuori sede per il dominio remoto Contoso.

    Set-RemoteDomain Contoso -AllowedOOFType None

In questo esempio sono consentiti solo i messaggi fuori sede esterni.

    Set-RemoteDomain Contoso -AllowedOOFType External


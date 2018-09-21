---
title: 'Configurare le risposte automatiche dominio remoto: Exchange 2013 Help'
TOCTitle: Configurare le risposte automatiche dominio remoto
ms:assetid: 3d88a1fb-4b62-419a-a50d-ffd868e229d0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657720(v=EXCHG.150)
ms:contentKeyID: 50480412
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare le risposte automatiche dominio remoto

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

È possibile utilizzare Exchange Management Shell per configurare il modo in cui i messaggi di posta elettronica vengono inviati e ricevuti tramite i domini remoti. Di seguito è spiegato come utilizzare Exchange Management Shell per configurare il modo in cui Exchange gestisce le risposte automatiche.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere°"Dominio remoto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo di Shell per la configurazione delle risposte automatiche

Il cmdlet **Set-RemoteDomain** consente di configurare le proprietà di un dominio remoto.

In questo esempio sono consentite le risposte automatiche al dominio remoto Contoso. Questa impostazione è disabilitata per impostazione predefinita.

```powershell
Set-RemoteDomain Contoso -AutoReplyEnabled $true
```

In questo esempio sono consentiti gli inoltri automatici al dominio remoto. Questa impostazione è disabilitata per impostazione predefinita.

```powershell
Set-RemoteDomain Contoso -AutoForwardEnabled $true
```


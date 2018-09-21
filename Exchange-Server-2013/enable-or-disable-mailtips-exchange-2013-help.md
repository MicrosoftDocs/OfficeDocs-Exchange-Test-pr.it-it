---
title: 'Abilitare o disabilitare i suggerimenti messaggio: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare i suggerimenti messaggio
ms:assetid: 11ad3848-f303-4ad5-a21d-9b0883db4bda
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ649321(v=EXCHG.150)
ms:contentKeyID: 50480022
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare i suggerimenti messaggio

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

È possibile utilizzare Exchange Management Shell per configurare numerose impostazioni che definiscono il modo in cui vengono utilizzati gli avvisi relativi ai messaggi all'interno dell'organizzazione.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Suggerimenti messaggio" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Abilitazione o disabilitazione dei suggerimenti messaggio tramite Shell

È possibile utilizzare il cmdlet **Set-OrganizationConfig** per abilitare o disabilitare i suggerimenti messaggio all'interno dell'organizzazione. Quando si installa una nuova organizzazione Exchange, gli avvisi messaggio sono abilitati per impostazione predefinita. In questo esempio, viene illustrato come abilitare i suggerimenti messaggio all'interno dell'organizzazione.

```powershell
Set-OrganizationConfig -MailTipsAllTipsEnabled $true
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\)).


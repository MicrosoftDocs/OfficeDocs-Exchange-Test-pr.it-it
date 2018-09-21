---
title: 'Gestire imp. mess. unificata su server cassette postali: Exchange 2013 Help'
TOCTitle: Gestire le impostazioni di messaggistica unificata su un server cassette postali
ms:assetid: 6df4853d-21d2-473f-b0ca-ebc996d8794a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998815(v=EXCHG.150)
ms:contentKeyID: 50555612
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMServerPropertiesPropertyPage
ms.translationtype: MT
---

# Gestire le impostazioni di messaggistica unificata su un server cassette postali

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-11_

Dopo aver installato un server Cassette postali su cui è in esecuzione il servizio di messaggistica unificata di Microsoft Exchange, è possibile configurare diverse opzioni tra cui il numero di chiamate contemporanee, le porte di ascolto TCP e TLS, lo stato e la modalità di avvio per Messaggistica unificata.


> [!IMPORTANT]
> Non è necessario che i server Cassette postali vengano aggiunti a un dial plan di messaggistica unificata prima di poter elaborare le chiamate per la messaggistica unificata, a meno che non si stia integrando la messaggistica unificata e Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server. Per impostazione predefinita, tutti i server Cassette postali nell'organizzazione sono disponibili per rispondere alle chiamate.



Per informazioni sulle altre attività di gestione relative ai server Cassette postali e Messaggistica unificata, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Server Cassette postali (servizio Messaggistica unificata)" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Verificare che il server Cassette postali sia installato nello stesso computer del server Accesso client o in un altro computer.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Configurazione delle proprietà della messaggistica unificata su un server Messaggistica unificata tramite Shell

In questo esempio, il server Cassette postali `MyMailboxServer` viene rimosso da tutti i dial plan SIP.

```powershell
Set-UMService -Identity MyMailboxServer -DialPlans $null
```

In questo esempio, il server Messaggistica unificata `MyMailboxServer` viene aggiunto al dial plan SIP di messaggistica unificata `MySIPDialPlanName` e viene impostato il numero massimo di chiamate vocali in ingresso.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -MaxCalls 150 

In questo esempio, la modalità di avvio viene impostata su Doppio sul server Cassette postali `MyUMServer`.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -UMStartUpMode -Dual 

## Visualizzazione delle proprietà del server Cassette postali tramite Shell

In questo esempio viene visualizzato un elenco di tutti i server Cassette postali.

```powershell
Get-UMService
```

In questo esempio viene visualizzato un elenco formattato delle proprietà per il server Cassette postali `MyMailboxServer`.

```powershell
Get-UMService -Identity MyMailboxServer | Format-List
```


---
title: "Installare e configurare l'agente di Address Book Policy Routing: Exchange 2013 Help"
TOCTitle: Installare e configurare l'agente di Address Book Policy Routing
ms:assetid: 20e8a43d-4508-4388-a2c9-aa3073593cc2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ907308(v=EXCHG.150)
ms:contentKeyID: 51407348
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Installare e configurare l'agente di Address Book Policy Routing

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-01-09_

L'agente di routing del criterio della rubrica è un agente di trasporto eseguito sul server Cassette postali che controlla il modo in cui i destinatari vengono risolti nell'organizzazione. Quando l'agente di routing ABP viene installato e configurato, gli utenti assegnati a diversi GAL vengono visualizzati come destinatari esterni in quanto non possono visualizzare le schede contatto dei destinatari esterni.

Per ulteriori attività di gestione relative ai criteri della rubrica, consultare [Procedure relative al criterio della Rubrica indirizzi](address-book-policy-procedures-exchange-2013-help.md).

Ulteriori informazioni su una versione per Exchange Online di questo argomento Vedere [Attivare il criterio della Rubrica routing](https://technet.microsoft.com/it-it/library/jj891095\(v=exchg.150\)).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 15 minuti.

  - Dopo che l'agente di routing viene installato e configurato, l'agente potrebbe impiegare fino a 30 minuti per valutare la posta elettronica nell'organizzazione.

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passaggio 1: Installare l'agente di routing ABP

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Agenti di trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

Installare l'agente di routing ABP eseguendo il comando seguente: Questi sono il comando e la sintassi esatti da utilizzare.

    Install-TransportAgent -Name "ABP Routing Agent" -TransportAgentFactory "Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.AddressBookPolicyRoutingAgentFactory" -AssemblyPath $env:ExchangeInstallPath\TransportRoles\agents\AddressBookPolicyRoutingAgent\Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.dll

Verrà inviato un avviso che informa che il servizio di trasporto deve essere avviato affinché le modifiche vengano apportate. Effettuare il passaggio 2 prima per dover riavviare il servizio di trasporto solo una volta.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Install-TransportAgent](https://technet.microsoft.com/it-it/library/aa997998\(v=exchg.150\)).

## Passaggio 2: Abilitare l'agente di routing di trasporto

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Agenti di trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

Dopo che l'agente di routing viene installato, è necessario abilitarlo eseguendo il seguente comando:

    Enable-TransportAgent "ABP Routing Agent"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Enable-TransportAgent](https://technet.microsoft.com/it-it/library/bb124921\(v=exchg.150\)).

## Passaggio 3: riavviare il servizio di trasporto e verificare che l'agente di routing ABP venga installato e abilitato

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Agenti di trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

1.  Riavviare il servizio di trasporto eseguendo il comando riportato di seguito:
    
        Restart-Service MSExchangeTransport

2.  Dopo che il servizio è stato riavviato, verificare che l'agente di routing ABP sia installato e abilitato eseguendo il seguente cmdlet.
    
        Get-TransportAgent
    
    Se l'agente di routing ABP è presente nell'elenco, l'agente è stato installato correttamente.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-TransportAgent](https://technet.microsoft.com/it-it/library/bb123536\(v=exchg.150\)).

## Passaggio 4: Abilitare l'agente di routing ABP

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Configurazione di trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

Il passaggio finale di questa procedura consente nell'abilitare il routing ABP per l'organizzazione. Eseguire il comando riportato di seguito.

    Set-TransportConfig -AddressBookPolicyRoutingEnabled $true

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-TransportConfig](https://technet.microsoft.com/it-it/library/bb124151\(v=exchg.150\)).


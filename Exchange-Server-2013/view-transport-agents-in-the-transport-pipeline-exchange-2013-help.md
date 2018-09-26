---
title: 'Agenti trasporto visualizzaz. pipeline trasporto: Exchange 2013 Help'
TOCTitle: Agenti di trasporto di visualizzazione nella pipeline di trasporto
ms:assetid: bd715d8e-7b21-48de-8f68-d425d8506e4c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124395(v=EXCHG.150)
ms:contentKeyID: 51407405
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agenti di trasporto di visualizzazione nella pipeline di trasporto

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

È possibile utilizzare Exchange Management Shell per visualizzare un elenco di agenti di trasporto nella pipeline di trasporto sui server Cassette postali e Accesso client di Microsoft Exchange Server 2013. Nello specifico, il cmdlet **Get-TransportPipeline** mostra le informazioni sui seguenti tipi di agenti di trasporto nella pipeline di trasporto:

  - Gli agenti basati sulle classi **SmtpReceiveAgent**, **RoutingAgent**, **DeliveryAgent** e **StorageAgent** nel servizio di trasporto sui server Cassette postali.

  - Gli agenti basati su **SmtpReceiveAgentClass** nel servizio Recapito alle cassette postali sui server Cassette postali.

  - Gli agenti basati su **SmtpReceiveAgentClass** nel servizio di trasporto di front-end sui server Accesso client.

È possibile visualizzare un elenco di tutti gli agenti di trasporto abilitati che hanno individuato messaggi nella pipeline di trasporto e gli eventi SMTP su cui sono registrati. Per ulteriori informazioni sugli agenti di trasporto, vedere [Agenti di trasporto](transport-agents-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Agenti di trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Visualizzazione di un elenco degli agenti di trasporto nella pipeline di trasporto tramite Shell

Per utilizzare Shell per visualizzare un elenco di agenti di trasporto nella pipeline di trasporto su un server Exchange, utilizzare il seguente comando:

```powershell
Get-TransportPipeline | Format-List
```

Per esportare i risultati in un file di testo denominato C:\\Documenti\\Transport Agents.txt, utilizzare il seguente comando:

```powershell
Get-TransportPipeline | Format-List > "C:\My Documents\Transport Agents.txt"
```

## Come verificare se l'operazione ha avuto esito positivo

Con il cmdlet vengono visualizzati solo gli agenti di trasporto che hanno individuato messaggi nella pipeline di trasporto tra l'avvio del servizio di trasporto e l'esecuzione del cmdlet **Get-TransportPipeline**. Un agente di trasporto che non ha individuato alcun messaggio nella pipeline di trasporto non verrà visualizzato nei risultati del cmdlet **Get-TransportPipeline**, anche se tale agente di trasporto è abilitato.


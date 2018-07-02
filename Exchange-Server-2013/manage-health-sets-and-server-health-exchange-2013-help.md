---
title: 'Gestire i set di integrità e lo stato dei server: Exchange 2013 Help'
TOCTitle: Gestire i set di integrità e lo stato dei server
ms:assetid: a4f84312-6cfa-4f17-9707-676aadab1143
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn482054(v=EXCHG.150)
ms:contentKeyID: 59890030
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire i set di integrità e lo stato dei server

 

_**Si applica a:** Exchange Online, Exchange Server 2013 SP1_

_**Ultima modifica dell'argomento:** 2013-12-02_

È possibile utilizzare i cmdlet integrati per creare report sull'integrità per eseguire un'ampia serie di attività correlate alla disponibilità gestita, tra cui:

  - Visualizzazione dell'integrià di un server o di un gruppo di server

  - Visualizzazione di un elenco di set di integrità

  - Visualizzazione di un elenco di probe, strumenti di monitoraggio e risponditori associati a un set di integrità specifico

  - Visualizzare un elenco di strumenti di monitoraggio e la relativa integrità

## Informazioni preliminari

  - Tempo stimato per il completamento di ciascuna procedura: 2 minuti

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Per saperne di più

## Visualizzare l'integrità del server

È possibile utilizzare Shell per ottenere un riepilogo dell'integrità di un server che esegue Exchange 2013.

## Utilizzare Shell per visualizzare l'integrità dei server

Eseguire uno dei seguenti comandi per visualizzare le informazioni sui set di integrità e sull'integrità in un server che esegue Exchange 2013.

    Get-HealthReport -Identity <ServerName>

    Get-ServerHealth -Identity <ServerName> | Format-Table Server,CurrentHealthSetState,Name,HealthSetName,AlertValue,HealthGroupName -Auto

Eseguire uno dei seguenti comandi per visualizzare i set di integrità in un server o gruppo di disponibilità del database che esegue Exchange 2013.

    Get-ExchangeServer | Get-HealthReport -RollupGroup

    Get-ExchangeServer | Get-HealthReport -RollupGroup -HealthSetName <HealthSet>

    (Get-DatabaseAvailabiltyGroup <DAGName>).Servers | Get-HealthReport -RollupGroup

## Visualizzare un elenco dei set di integrità

Un set di integrità è un gruppo di strumenti di monitoraggio, probe e risponditori di un componente che consentono di determinare se il componente è integro o meno. È possibile utilizzare Shell per visualizzare un elenco di set di integrità in un server che esegue Exchange 2013.

## Utilizzare Shell per visualizzare un elenco di set di integrità

Esegui il comando seguente per visualizzare i set di integrità in un server che esegue Exchange 2013.

    Get-HealthReport -Server <ServerName>

## Visualizzare probe, strumenti di monitoraggio e risponditori per un set di integrità

Un set di integrità è un gruppo di strumenti di monitoraggio, probe e risponditori di un componente che consentono di determinare se il componente è integro o meno. È possibile utilizzare Shell per visualizzare un elenco di probe, strumenti di monitoraggio e risponditori associati a un set di integrità in un server che esegue Exchange 2013.

## Utilizzare Shell per visualizzare probe, strumenti di monitoraggio e risponditori per un set di integrità

Eseguire il seguente comando per visualizzare probe, strumenti di monitoraggio e risponditori associati a un set di integrità in un server che esegue Exchange 2013.

    Get-MonitoringItemIdentity -Server <ServerName> -Identity <HealthSetName> | Format-Table Identity,ItemType,Name -Auto

## Visualizzare un elenco di strumenti di monitoraggio e la relativa integrità corrente

L'integrità di uno strumento di monitoraggio viene determinata mediante l'utilizzo dei "peggiori" strumenti di monitoraggio nel set di integrità. È possibile visualizzare i dettagli di un set di integrità per vedere quali strumenti di monitoraggio sono integri e quali non lo sono.

## Utilizzare Shell per visualizzare un elenco di strumenti di monitoraggio e la relativa integrità corrente

Eseguire il seguente comando per visualizzare un elenco di strumenti di monitoraggio e la relativa integrità in un server che esegue Exchange 2013.

    Get-ServerHealth -HealthSet <HealthSetName> -Server <ServerName> | Format-Table Name, AlertValue -Auto


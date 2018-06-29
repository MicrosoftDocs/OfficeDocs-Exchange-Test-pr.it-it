---
title: "Configurazione dell'analisi della pipeline: Exchange 2013 Help"
TOCTitle: Configurazione dell'analisi della pipeline
ms:assetid: 10293c83-2157-474e-840d-942e064a4672
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ916678(v=EXCHG.150)
ms:contentKeyID: 52063044
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione dell'analisi della pipeline

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-08_

L'analisi della pipeline acquisisce copie dei messaggi di posta elettronica quando si spostano attraverso la pipeline di trasporto nel servizio di trasporto o nel servizio di trasporto di cassette postali sul server Cassette postali e sui server Trasporto Edge.

## Informazioni necessarie prima di iniziare

  - Tempo stimato per il completamento di questa procedura: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Servizio Trasporto" e "Server trasporto di cassette postali" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - L'analisi della pipeline copia l'intero contenuto dei messaggi di posta elettronica che vengono inviati dall'indirizzo di posta elettronica del mittente. Per evitare un'inutile esposizione delle informazioni riservate, è necessario impostare apposite autorizzazioni di protezione sul percorso della cartella relativa all'analisi della pipeline.

  - Non abilitare l'analisi della pipeline per periodi di tempo prolungati. L'analisi della pipeline crea più file snapshot dei messaggi che si accumulano rapidamente. Controllare sempre lo spazio disponibile sul disco quando l'analisi della pipeline è abilitata.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Abilitare e configurare l'analisi della pipeline

## Passaggio 1: configurazione dell'indirizzo mittente dell'analisi della pipeline tramite Shell

Utilizzare la sintassi seguente per configurare l'indirizzo mittente dell'analisi della pipeline.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingSenderAddress <SMTPAddress | "<>">

In questo esempio viene configurata l'analisi della pipeline per acquisire snapshot di tutti i messaggi inviati dal mittente chris@contoso.com nel servizio di trasporto sul server Cassette postali denominato Mailbox01.

    Set-TransportService Mailbox01 -PipelineTracingSenderAddress chris@contoso.com

In questo esempio viene configurata l'analisi della pipeline per acquisire snapshot di tutti i messaggi generati dal sistema e ricevuti dal servizio di trasporto sul server Cassette postali denominato Mailbox02.

    Set-TransportService Mailbox02 -PipelineTracingSenderAddress "<>"


> [!WARNING]
> La configurazione dell'analisi della pipeline per acquisire tutti i messaggi generati dal server in un servizio di trasporto potrebbe comportare un carico notevole sul server ed esaurire rapidamente lo spazio disponibile sul disco. Controllare sempre lo spazio disponibile sul disco quando l'analisi della pipeline è abilitata.



## Passaggio 2: utilizzo di Shell per specificare una cartella personalizzata per l'analisi della pipeline (facoltativo)

La cartella predefinita dell'analisi della pipeline non viene creata finché non si abilita l'analisi della pipeline e finché i messaggi che corrispondono ai criteri specificati utilizzando il parametro *PipelineTracingSenderAddress* attraversano il servizio di trasporto sul server. Il percorso predefinito per il servizio di trasporto sul server Cassette postali è `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`. Il percorso predefinito per il servizio di trasporto di cassette postali su un server Cassette postali è `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`. Se viene specificato un percorso personalizzato, è necessario che tale percorso si trovi sul server Exchange locale.

Utilizzare la sintassi seguente per configurare la cartella relativa all'analisi della pipeline.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingPath <LocalFilePath>

In questo esempio viene impostata la cartella relativa all'analisi della pipeline per il servizio di trasporto sul server Cassette postali denominato Mailbox01 su D:\\Hub\\Pipeline Tracing.

    Set-TransportService Mailbox01 -PipelineTracingPath "D:\Hub\Pipeline Tracing"

## Passaggio 3: abilitazione dell'analisi della pipeline tramite Shell

Per impostazione predefinita, l'analisi della pipeline è disabilitata su tutti i server Exchange. Quando si abilita l'analisi della pipeline, questa viene abilitata nel servizio di trasporto specifico e soltanto sul server Exchange indicato. Prima di abilitare l'analisi della pipeline, è necessario indicare l'indirizzo del mittente, come illustrato nel passaggio 1.

Utilizzare la sintassi seguente per abilitare l'analisi della pipeline.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $true

In questo esempio viene abilitata l'analisi della pipeline nel servizio di trasporto sul server Cassette postali denominato Mailbox01.

    Set-TransportService Mailbox01 -PipelineTracingEnabled $true

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione dell'analisi della pipeline, effettuare le seguenti operazioni:

1.  Eseguire il comando indicato di seguito:
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracing*

2.  Verificare che i valori visualizzati siano quelli configurati.

3.  Verificare la cartella relativa all'analisi della pipeline per il servizio di trasporto o per il servizio di trasporto di cassette postali e verificare che i file snapshot dei messaggi siano stati creati nella cartella.

## Disabilitazione dell'analisi della pipeline

A causa dello spazio sul disco e di problemi relativi alla sicurezza collegati all'analisi della pipeline, quest'ultima rappresenta un'azione temporanea a scopo di diagnostica e di risoluzione dei problemi. Quando si abilita l'analisi della pipeline, ricordarsi di disabilitarla al termine della procedura.

Utilizzare la sintassi seguente per disabilitare l'analisi della pipeline.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $false

In questo esempio viene disabilitata l'analisi della pipeline nel servizio di trasporto sul server Cassette postali denominato Mailbox01.

    Set-TransportService Mailbox01 -PipelineTracingEnabled $false

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta disabilitazione dell'analisi della pipeline, effettuare le seguenti operazioni:

1.  Eseguire il comando indicato di seguito:
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracingEnabled

2.  Verificare che il valore del parametro *PipelineTracingEnabled* sia $false.

3.  Controllare la cartella relativa all'analisi della pipeline e assicurarsi che i file snapshot dei messaggi non vengano più creati nella cartella.


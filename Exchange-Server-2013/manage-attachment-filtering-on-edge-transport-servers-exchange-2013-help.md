---
title: 'Gestione di filtro degli allegati nei server Trasporto Edge: Exchange 2013 Help'
TOCTitle: Gestione di filtro degli allegati nei server Trasporto Edge
ms:assetid: 2ec91cc6-6ade-48ee-88bb-66153874393d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997139(v=EXCHG.150)
ms:contentKeyID: 60829831
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione di filtro degli allegati nei server Trasporto Edge

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

Il filtro degli allegati è fornito dall'agente filtro allegati disponibile solo nei server Trasporto Edge. Il filtro degli allegati consente di impedire ai file allegati ai messaggi di posta elettronica di entrare nell'organizzazione. È possibile configurare più voci del filtro degli allegati per filtrare gli allegati per tipo di contenuto o per nome file.

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Funzionalità di protezione dalla posta indesiderata" nell'argomento [Autorizzazioni di protezione da posta indesiderata e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) e "Agenti di trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Le modifiche di configurazione apportate al filtro degli allegati in un server Trasporto Edge vengono applicate solo al computer locale. Se nella rete perimetrale sono presenti più server Trasporto Edge, è necessario configurare il filtro degli allegati separatamente in ogni server Trasporto Edge.

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Quando si disattiva il filtro degli allegati e si riavvia il servizio di trasporto di Microsoft Exchange, tutte le funzionalità di filtro degli allegati smettono di funzionare.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Abilitazione o disabilitazione del filtro degli allegati tramite Shell

Quando si attiva o disattiva l'agente filtro allegati, la modifica viene applicata quando si riavvia il servizio di trasporto di Microsoft Exchange. Quando si riavvia il servizio in un server Trasporto Edge, il flusso di posta sul server viene interrotto temporaneamente.

Per disabilitare il filtro degli allegati, eseguire il seguente comando:

    Disable-TransportAgent "Attachment Filtering Agent"

Per abilitare il filtro degli allegati, eseguire questo comando:

    Enable-TransportAgent "Attachment Filtering Agent"

Dopo aver attivato o disattivato il filtro degli allegati, riavviare il servizio di trasporto di Microsoft Exchange eseguendo il seguente comando:

    Restart-Service MSExchangeTransport

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione del filtro degli allegati, effettuare le seguenti operazioni:

1.  Eseguire il comando indicato di seguito:
    
        Get-TransportAgent "Attachment Filtering Agent"

2.  Se il valore **Enabled** è `True`, il filtro degli allegati è attivato. Se il valore è `False`, il filtro degli allegati è disattivato.

## Visualizzazione delle voci del filtro degli allegati tramite Shell

Le voci del filtro degli allegati definiscono gli allegati dei messaggi da tenere fuori dall'organizzazione. Per visualizzare le voci del filtro degli allegati utilizzate dall'agente filtro allegati, eseguire il comando seguente:

    Get-AttachmentFilterEntry | Format-Table

Per visualizzare una voce specifica del tipo di contenuto MIME, è possibile utilizzare la sintassi seguente:

    Get-AttachmentFilteringEntry ContentType:<MIMEContentType>

Ad esempio, per visualizzare la voce del tipo di contenuto per le immagini JPEG, è possibile eseguire il comando riportato di seguito:

    Get-AttachmentFilteringEntry ContentType:image/jpeg

Per visualizzare un nome di file specifico o la voce di estensione del nome di file, utilizzare la sintassi seguente:

    Get-AttachmentFilteringEntry FileName:<FileName or FileNameExtension>

Ad esempio, per visualizzare la voce dell'estensione del nome file per gli allegati JPEG, è possibile eseguire il comando riportato di seguito:

    Get-AttachmentFilteringEntry FileName:*.jpg

## Aggiunta delle voci del filtro degli allegati tramite Shell

Per aggiungere una voce del filtro degli allegati che filtra gli allegati per tipo di contenuto MIME, utilizzare la sintassi seguente:

    Add-AttachmentFilterEntry -Name <MIMEContentType> -Type ContentType

Nell'esempio seguente viene aggiunta una voce del tipo di contenuto MIME che filtra le immagini JPEG.

    Add-AttachmentFilterEntry -Name image/jpeg -Type ContentType

Per aggiungere una voce del filtro degli allegati che filtra gli allegati per nome file o estensione del nome file, utilizzare la sintassi seguente:

    Add-AttachmentFilterEntry -Name <FileName or FileNameExtension> -Type FileName

Nell'esempio riportato di seguito vengono filtrati gli allegati con estensione del nome file .jpg.

    Add-AttachmentFilterEntry -Name *.jpg -Type FileName

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la voce del filtro degli allegati sia stata aggiunta correttamente, attenersi alla seguente procedura:

1.  Eseguire il comando seguente per verificare che sia presente la voce del filtro.
    
        Get-AttachmentFilterEntry | Format-Table

2.  Inviar un messaggio di prova contenente un allegato proibito da una cassetta postale esterna a un destinatario interno e verificare che il messaggio venga rifiutato, rimosso o eliminato.

## Rimozione delle voci del filtro degli allegati tramite Shell

Per rimuovere una voce del filtro degli allegati che filtra gli allegati per tipo di contenuto MIME, utilizzare la sintassi seguente:

    Remove-AttachmentFilterEntry ContentType:<ContentType>

Nell'esempio riportato di seguito viene rimossa la voce del tipo di contenuto MIME per le immagini JPEG.

    Remove-AttachmentFilterEntry ContentType:image/jpeg

Per rimuovere una voce del filtro degli allegati che filtra gli allegati per nome file o estensione del nome file, utilizzare la sintassi seguente:

    Remove-AttachmentFilterEntry FileName:<FileName or FileNameExtension>

Nell'esempio riportato di seguito viene rimossa la voce del nome file per l'estensione. jpg.

    Remove-AttachmentFilterEntry FileName:*.jpg

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la voce del filtro degli allegati sia stata rimossa correttamente, attenersi alla seguente procedura:

1.  Eseguire il comando seguente per verificare che la voce del filtro sia stata rimossa.
    
        Get-AttachmentFilterEntry | Format-Table

2.  Inviar un messaggio di prova contenente un allegato consentito da una cassetta postale esterna a un destinatario interno e verificare che il messaggio venga recapitato correttamente con l'allegato.

## Utilizzare Shell per visualizzare l'azione del filtro degli allegati

Per visualizzare l'azione del filtro degli allegati utilizzata quando viene individuato un allegato proibito in un messaggio, eseguire il seguente comando:

    Get-AttachmentFilterListConfig

## Utilizzare Shell per configurare l'azione del filtro degli allegati

Per configurare l'azione del filtro degli allegati utilizzata quando viene individuato un allegato proibito in un messaggio, utilizzare la seguente sintassi:

    Set-AttachmentFilterListConfig [-Action <Reject | Strip | SilentDelete>] [-RejectResponse "<Message text>"] [-AdminMessage "<Replacement file text>"] [-ExceptionConnectors <ConnectorGUID>]

In questo esempio vengono apportate le seguenti modifiche alla configurazione dell'agente filtro allegati:

  - Rifiutare (bloccare) i messaggi con allegati vietati.

  - Utilizzare una risposta personalizzata per i messaggi rifiutati.

<!-- end list -->

    Set-AttachmentFilterListConfig -Action Reject -RejectResponse "This message contains a prohibited attachment. Your message can't be delivered. Please resend the message without the attachment."

Per ulteriori informazioni, vedere [Set-AttachmentFilterListConfig](https://technet.microsoft.com/it-it/library/bb123483\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver configurato correttamente l'azione del filtro degli allegati, inviare un messaggio di testo contenente un allegato proibito da una cassetta postale esterna a un destinatario interno e verificare che il messaggio e l'allegato vengano elaborati come previsto.


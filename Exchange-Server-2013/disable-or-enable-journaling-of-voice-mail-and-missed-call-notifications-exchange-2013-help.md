---
title: 'Dis./abilita ins. journal mess. voc./notifiche chiamata: Exchange 2013 Help'
TOCTitle: Disabilitare o abilitare l'inserimento nel journal dei messaggi vocali e delle notifiche di chiamata
ms:assetid: 5164a92e-69e6-4339-b80c-0cfbf0dc0198
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201690(v=EXCHG.150)
ms:contentKeyID: 50480591
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disabilitare o abilitare l'inserimento nel journal dei messaggi vocali e delle notifiche di chiamata

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

In Microsoft Exchange Server 2013, quando si crea una regola del journal per l'inserimento nel journal dei messaggi di posta elettronica inviati o ricevuti da utenti in un'organizzazione Exchange, vengono inclusi i messaggi vocali e i messaggi di notifica di chiamata senza risposta generati dal servizio di messaggistica unificata. Utilizzare la procedura illustrata in questo argomento per attivare e disattivare questa funzionalità per l'intera organizzazione.

Per informazioni sulle altre attività di gestione relative all'inserimento nel journal, vedere [Gestire l'inserimento nel journal](https://docs.microsoft.com/it-it/exchange/security-and-compliance/journaling/manage-journaling).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Inserimento nel journal" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo di Shell per la disabilitazione o l'abilitazione dell'inserimento nel journal dei messaggi vocali e dei messaggi di notifica di chiamata senza risposta

In questo esempio viene disabilitato l'inserimento nel journal dei messaggi vocali e dei messaggi di notifica di chiamata senza risposta impostando il parametro*VoicemailJournalingEnabled* su `$false`.

    Set-TransportConfig -VoicemailJournalingEnabled $false

In questo esempio viene abilitato l'inserimento nel journal dei messaggi vocali e dei messaggi di notifica di chiamata senza risposta impostando lo stesso parametro su `$true`.

    Set-TransportConfig -VoicemailJournalingEnabled $true

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-TransportConfig](https://technet.microsoft.com/it-it/library/bb124151\(v=exchg.150\)).

## Per ulteriori informazioni

[Inserimento nel journal](journaling-exchange-2013-help.md)

[Gestire l'inserimento nel journal](https://docs.microsoft.com/it-it/exchange/security-and-compliance/journaling/manage-journaling)


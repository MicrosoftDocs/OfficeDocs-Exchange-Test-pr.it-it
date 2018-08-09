---
title: 'Versione messaggi della posta indesiderata in quarantena: Exchange 2013 Help'
TOCTitle: Versione messaggi dalla cassetta postale di quarantena della posta indesiderata in quarantena
ms:assetid: 7a86bfde-f868-4689-bdec-5f01e52b510d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998920(v=EXCHG.150)
ms:contentKeyID: 50481012
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Versione messaggi dalla cassetta postale di quarantena della posta indesiderata in quarantena

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile utilizzare Microsoft Outlook per recuperare un messaggio in quarantena dalla cassetta postale della posta indesiderata.

Quarantena della posta indesiderata è una funzionalità dell'agente Filtro contenuti che riduce il rischio di perdita di messaggi legittimi. Se un messaggio raggiunge la soglia di quarantena della posta indesiderata, viene racchiuso in un rapporto di mancato recapito (NDR) e recapitato alla cassetta postale di quarantena della posta indesiderata. Per ulteriori informazioni sulla funzionalità per la quarantena della posta indesiderata, vedere [Quarantena posta indesiderata](spam-quarantine-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Accesso alle cassette postali" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Questa procedura richiede la configurazione della cassetta postale della quarantena antispam. Per ulteriori informazioni, vedere [Configurare una cassetta postale di quarantena della posta indesiderata](configure-a-spam-quarantine-mailbox-exchange-2013-help.md).

  - Per accedere alla cassetta postale di quarantena, è necessario configurare un profilo di Outlook per tale cassetta postale e quindi aprire la cassetta postale utilizzando Outlook. Per ulteriori informazioni sulla configurazione e utilizzo di più profili di Outlook, vedere [Panoramica di Outlook profili di posta elettronica](https://go.microsoft.com/fwlink/p/?linkid=178975).

  - Per facilitare l'individuazione del messaggio da recuperare, è possibile creare un modulo Outlook personalizzato e modificare la visualizzazione predefinita dell'indirizzo mittente originale nell'elenco dei messaggi. Per la procedura dettagliata, vedere [Configurare Outlook per visualizzare il mittente originale nella cassetta postale di quarantena](configure-outlook-to-show-the-original-sender-in-the-quarantine-mailbox-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Rilascio di un messaggio dalla cassetta postale per la quarantena della posta indesiderata tramite Outlook 2010 o Outlook 2013

1.  Aprire la cassetta postale della quarantena utilizzando Outlook 2010 o Outlook 2013 su un computer client.

2.  Nella vista **Posta**, trovare il messaggio che si vuole recuperare in **Posta in arrivo**, quindi fare doppio clic sul messaggio per aprirlo.

3.  Nella sezione **Sposta** della barra multifunzione, fare clic su **Azioni** \> **Reinvia il messaggio**.

4.  Quando viene aperto il messaggio di posta elettronica, fare clic su **Invia** per inviare nuovamente il messaggio di posta elettronica al destinatario desiderato.

## Rilascio di un messaggio dalla cassetta postale per la quarantena della posta indesiderata tramite Outlook 2007

1.  Aprire la cassetta postale della quarantena utilizzando Outlook 2007 su un computer client.

2.  Nella vista **Posta**, trovare il messaggio che si vuole recuperare in **Posta in arrivo**, quindi fare doppio clic sul messaggio per aprirlo.

3.  Nel gruppo **Rispondi** della scheda **Rapporto**, fare clic su **Rinvia**.

4.  Quando viene aperto il messaggio di posta elettronica, fare clic su **Invia** per inviare nuovamente il messaggio di posta elettronica al destinatario desiderato.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il messaggio sia stato correttamente rilasciato dalla cassetta postale per la quarantena della posta indesiderata, mettersi in contatto con il destinatario e verificare che abbia ricevuto il messaggio.


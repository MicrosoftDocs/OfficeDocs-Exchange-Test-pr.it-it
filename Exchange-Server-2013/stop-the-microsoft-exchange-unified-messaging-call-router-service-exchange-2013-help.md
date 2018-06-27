---
title: 'Arrestare il servizio Microsoft Exchange Unified Messaging routing delle chiamate: Exchange 2013 Help'
TOCTitle: Arrestare il servizio Microsoft Exchange Unified Messaging routing delle chiamate
ms:assetid: 79935528-1a8c-4f22-826c-8f9a60f4f6f4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673535(v=EXCHG.150)
ms:contentKeyID: 50555614
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Arrestare il servizio Microsoft Exchange Unified Messaging routing delle chiamate

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-16_

Per arrestare il servizio di routing delle chiamate di messaggistica unificata di MicrosoftExchange su un server Accesso client, è possibile utilizzare lo snap-in Servizi in Microsoft Management Console (MMC) o cmd.exe al prompt dei comandi. In alcune situazioni può essere necessario arrestare questo servizio, ad esempio, quando è indispensabile disconnettere il server Accesso client. Una volta arrestato il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange, il server Accesso client non sarà più in grado di accettare ed elaborare le chiamate in arrivo.

Per le attività di gestione aggiuntive relative ai server Accesso client, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire le procedure riportate di seguito, è necessario accedere al server Accesso client utilizzando un account membro del gruppo Administrators locale.

  - Verificare che il server Accesso client sia installato nello stesso computer del server Cassette postali o in un computer diverso.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Arresto del servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange tramite lo snap-in Servizi MMC

1.  Fare clic sul pulsante **Start**, quindi su **Pannello di controllo**.

2.  Nel Pannello di controllo fare doppio clic su **Strumenti di amministrazione**.

3.  In **Strumenti di amministrazione** fare doppio clic su **Servizi**.

4.  Nel riquadro dei dettagli **Servizi**, fare clic con il pulsante destro del mouse su **Router delle chiamate di messaggistica unificata di Microsoft Exchange**, quindi scegliere **Arresta**.

## Arresto del servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange tramite prompt dei comandi

1.  Scegliere **Esegui** dal menu **Start**.

2.  Nella casella **Apri** digitare il seguente comando e premere INVIO.
    
        net stop MSExchangeUMCR


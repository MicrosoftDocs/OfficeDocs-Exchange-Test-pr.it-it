---
title: 'Arrestare il servizio di messaggistica unificata di Exchange: Exchange 2013 Help'
TOCTitle: Arrestare il servizio di messaggistica unificata di Exchange
ms:assetid: 64fa5535-8150-45c6-82e6-d2346892a031
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998595(v=EXCHG.150)
ms:contentKeyID: 50555605
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Arrestare il servizio di messaggistica unificata di Exchange

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-16_

È possibile utilizzare lo snap-in Servizi in Microsoft Management Console (MMC) o cmd.exe nel prompt dei comandi per arrestare il servizio di messaggistica unificata di MicrosoftExchange su un server Cassette postali. In alcune situazioni è necessario arrestare il servizio. Ad esempio, quando è indispensabile disconnettere il server Cassette postali. Una volta arrestato il servizio di messaggistica unificata di MicrosoftExchange, il server Cassette postali non è più in grado di accettare ed elaborare le chiamate in arrivo.

Per le altre attività di gestione relative ai server Cassette postali, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Informazioni necessarie per iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per completare le seguenti procedure, è necessario accedere al server Cassette postali utilizzando un account membro del gruppo Amministratori locale.

  - Verificare che il server Cassette postali sia installato sullo stesso computer del server Accesso client o su un altro computer.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dello snap-in Servizi di MMC per arrestare il servizio Messaggistica unificata di Microsoft Exchange

1.  Fare clic sul pulsante **Start**, quindi su **Pannello di controllo**.

2.  Nel Pannello di controllo fare doppio clic su **Strumenti di amministrazione**.

3.  In **Strumenti di amministrazione**, fare doppio clic su **Servizi**.

4.  Nel riquadro dei dettagli **Servizi**, fare clic con il pulsante destro del mouse su **Messaggistica unificata di Microsoft Exchange**, quindi scegliere **Interrompi**.

## Utilizzo di un prompt dei comandi per arrestare il servizio Messaggistica unificata di Microsoft Exchange

1.  Fare clic su **Start**, quindi su **Esegui**.

2.  Nella casella **Apri** digitare il seguente comando e premere Invio.
    
        net stop MSExchangeUM


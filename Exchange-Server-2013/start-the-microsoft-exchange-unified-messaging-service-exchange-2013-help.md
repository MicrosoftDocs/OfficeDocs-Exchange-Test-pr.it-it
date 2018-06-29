---
title: 'Avviare il servizio di messaggistica unificata di Exchange: Exchange 2013 Help'
TOCTitle: Avviare il servizio di messaggistica unificata di Exchange
ms:assetid: b54008e6-172e-4435-8516-57cff740e89c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124330(v=EXCHG.150)
ms:contentKeyID: 50555669
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Avviare il servizio di messaggistica unificata di Exchange

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-16_

È possibile utilizzare lo snap-in Servizi in Microsoft Management Console (MMC) o cmd.exe al prompt dei comandi per avviare il servizio Messaggistica unificata di MicrosoftExchange su un server Cassette postali. Per impostazione predefinita, il servizio Messaggistica unificata di MicrosoftExchange viene avviato dopo l'installazione di un server Cassette postali. Tuttavia, può verificarsi la necessità di riavviare il servizio Messaggistica unificata di MicrosoftExchange manualmente quando, ad esempio, si deve riportare in linea il server Cassette postali per cui era stata attivata la modalità non in linea.

Quando il servizio Messaggistica unificata di MicrosoftExchange viene avviato su un server Cassette postali, tale server può elaborare le chiamate di messaggistica unificata in arrivo.

Per ulteriori attività di gestione relative ai server Cassette postali, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire le seguenti procedure, è necessario accedere al server Cassette postali utilizzando un account membro del gruppo Administrators locale.

  - Verificare che il server Cassette postali sia installato nello stesso computer del server Accesso client o in un altro computer.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dello snap-in Servizi MMC per avviare il servizio Messaggistica unificata di Microsoft Exchange

1.  Fare clic sul pulsante **Start**, quindi su **Pannello di controllo**.

2.  Nel Pannello di controllo fare doppio clic su **Strumenti di amministrazione**.

3.  In **Strumenti di amministrazione** fare doppio clic su **Servizi**.

4.  Nel riquadro dei dettagli **Servizi**, fare clic con il pulsante destro del mouse su **Messaggistica unificata di Microsoft Exchange**, quindi scegliere **Avvio**.

## Utilizzo di un prompt dei comandi per avviare il servizio Messaggistica unificata di Microsoft Exchange

1.  Scegliere **Esegui** dal menu **Start**.

2.  Nella casella **Apri** digitare il seguente comando e premere Invio.
    
        net start MSExchangeUM


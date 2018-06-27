---
title: 'Avviare il servizio Microsoft Exchange Unified Messaging routing delle chiamate: Exchange 2013 Help'
TOCTitle: Avviare il servizio Microsoft Exchange Unified Messaging routing delle chiamate
ms:assetid: 8b7e1a4c-87b3-4477-a95f-6b41cf2d38f0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673542(v=EXCHG.150)
ms:contentKeyID: 50555622
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Avviare il servizio Microsoft Exchange Unified Messaging routing delle chiamate

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-16_

È possibile utilizzare lo snap-in Servizi in Microsoft Management Console (MMC) o cmd.exe al prompt dei comandi per avviare il servizio di routing delle chiamate di messaggistica unificata di MicrosoftExchange su un server Accesso client. Per impostazione predefinita, il servizio di routing delle chiamate di messaggistica unificata di MicrosoftExchange viene avviato dopo l'installazione del server Accesso client. Tuttavia, può verificarsi la necessità di riavviare manualmente il servizio di routing delle chiamate di messaggistica unificata di MicrosoftExchange quando, ad esempio, è necessario riportare in linea il server Accesso client per cui era stata attivata la modalità non in linea.

Quando il servizio di routing delle chiamate di messaggistica unificata di MicrosoftExchange viene avviato su un server Accesso client, tale server può rispondere ed elaborare le chiamate di messaggistica unificata in arrivo.

Per le attività di gestione aggiuntive relative ai server Accesso client, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire le procedure riportate di seguito, è necessario accedere al server Accesso client utilizzando un account membro del gruppo Administrators locale.

  - Verificare che il server Accesso client sia installato nello stesso computer del server Cassette postali o in un computer diverso.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Avvio del servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange tramite lo snap-in Servizi MMC

1.  Fare clic sul pulsante **Start**, quindi su **Pannello di controllo**.

2.  Nel Pannello di controllo fare doppio clic su **Strumenti di amministrazione**.

3.  In **Strumenti di amministrazione** fare doppio clic su **Servizi**.

4.  Nel riquadro dei dettagli **Servizi**, fare clic con il pulsante destro del mouse su **Router delle chiamate di messaggistica unificata di Microsoft Exchange**, quindi scegliere **Start**.

## Avvio del servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange tramite prompt dei comandi

1.  Scegliere **Esegui** dal menu **Start**.

2.  Nella casella **Apri** digitare il seguente comando e premere INVIO.
    
        net start MSExchangeUMCR


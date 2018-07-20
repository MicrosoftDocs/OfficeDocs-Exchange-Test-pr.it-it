---
title: 'Avviare e arrestare i servizi POP3: Exchange 2013 Help'
TOCTitle: Avviare e arrestare i servizi POP3
ms:assetid: 3d543921-d8c9-4d4b-99a1-82446b585ceb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997475(v=EXCHG.150)
ms:contentKeyID: 50480403
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Avviare e arrestare i servizi POP3

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-03-13_

Per impostazione predefinita, i due servizi POP3, il servizio Microsoft Exchange POP3 e il servizio back-end POP3 di Microsoft Exchange, non vengono avviati sui computer in cui è in esecuzione MicrosoftExchange Server 2013. È necessario avviare questi due servizi per consentire ai client della posta elettronica di connettersi a Exchange utilizzando POP3. Quando questi servizi sono in esecuzione, Exchange 2013 accetta le comunicazioni client POP3 non protette sulla porta 110 e sulla porta 995 utilizzando SSL (Secure Sockets Layer).

Il servizio Microsoft Exchange POP3 viene eseguito sui computer Exchange 2013 che eseguono il ruolo del server Accesso client. Il servizio back-end POP3 di Microsoft Exchange viene eseguito sul computer Exchange 2013 che esegue il ruolo del server Cassette postali. Negli ambienti in cui i ruoli Accesso client e Cassette postali sono attivi sullo stesso computer, entrambi i servizi vengono gestiti sullo stesso computer.

Per ulteriori informazioni su POP3 e IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni POP3 e IMAP4" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dello snap-in dei servizi Microsoft Management Console per avviare o arrestare i servizi POP3

Per avviare i servizi POP3:

1.  Su un computer su cui è attivo il ruolo del server Accesso client, fare clic su **Start**, selezionare **Programmi**, **Strumenti di amministrazione**, quindi fare clic su **Servizi**. Fare clic con il pulsante destro del mouse su **Microsoft Exchange POP3**, quindi fare clic su **Avvio**.

2.  Su un computer su cui è attivo il ruolo del server Cassette postali, fare clic su **Start**, selezionare **Programmi**, **Strumenti di amministrazione**, quindi fare clic su **Servizi**. Nel riquadro dei risultati, fare clic con il pulsante destro del mouse su **Back-end POP3 di Microsoft Exchange** , quindi scegliere **Start**.

Per interrompere i servizi POP3:

1.  Su un computer su cui è attivo il ruolo del server Accesso client, fare clic su **Start**, selezionare **Programmi**, **Strumenti di amministrazione**, quindi fare clic su **Servizi**. Fare clic con il pulsante destro del mouse su **Microsoft Exchange POP3**, quindi fare clic su **Arresto**.

2.  Su un computer su cui è attivo il ruolo del server Cassette postali, fare clic su **Start**, selezionare **Programmi**, **Strumenti di amministrazione**, quindi fare clic su **Servizi**. Fare clic con il pulsante destro del mouse su **Back-end POP3 di Microsoft Exchange** , quindi fare clic **Arresto**.

## Utilizzare Shell per avviare o arrestare i servizi POP3

Per avviare i servizi POP3:

1.  Sul computer che esegue il ruolo del server Accesso client, da Shell, utilizzare il seguente comando per avviare il servizio Microsoft Exchange POP3.
    
        Start-service MSExchangePOP3

2.  Sul computer che esegue il ruolo del server Cassette postali, da Shell, utilizzare il seguente comando per avviare il servizio back-end POP3 di Microsoft Exchange.
    
        Start-service MSExchangePOP3BE

Per interrompere i servizi POP3:

1.  Sul computer che esegue il ruolo del server Accesso client, da Shell, utilizzare il seguente comando per arrestare il servizio Microsoft Exchange POP3.
    
        Stop-service MSExchangePOP3

2.  Sul computer che esegue il ruolo del server Cassette postali, da Shell, utilizzare il seguente comando per arrestare il servizio back-end POP3 di Microsoft Exchange.
    
        Stop-service MSExchangePOP3BE

## Utilizzo del comando net start per avviare o arrestare i servizi POP3

Per avviare i servizi POP3:

1.  Sul computer che esegue il ruolo del server Accesso client, al prompt dei comandi, utilizzare il seguente comando per avviare il servizio Microsoft Exchange POP3.
    
        Net Start msExchangePOP3

2.  Sul computer che esegue il ruolo del server Cassette postali, al prompt dei comandi, utilizzare il seguente comando per avviare il servizio back-end POP3 di Microsoft Exchange.
    
        Net Start msExchangePOP3BE

Per interrompere i servizi POP3:

1.  Sul computer che esegue il ruolo del server Accesso client, al prompt dei comandi, utilizzare il seguente comando per arrestare il servizio Microsoft Exchange POP3.
    
        Net Stop MSExchangePOP3

2.  Sul computer che esegue il ruolo del server Cassette postali, al prompt dei comandi, utilizzare il seguente comando per arrestare il servizio back-end POP3 di Microsoft Exchange.
    
        Net Stop MSExchangePOP3BE

## Come verificare se l'operazione ha avuto esito positivo

1.  Sul server Accesso client di Exchange, aprire Task Manager Windows. Nella scheda **Servizi**, lo stato per **MSExchangePOP3** verrà visualizzato come **In esecuzione** se il servizio Microsoft Exchange POP3 è in esecuzione.

2.  Sul server cassette postali di Exchange, aprire Task Manager Windows. Nella scheda **Servizi**, lo stato per **MSExchangePOP3** verrà visualizzato come **In esecuzione** se il servizio back-end POP3 di Microsoft Exchange è in esecuzione.


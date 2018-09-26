---
title: 'Avviare e arrestare i servizi IMAP4: Exchange 2013 Help'
TOCTitle: Avviare e arrestare i servizi IMAP4
ms:assetid: a52db4bd-69a6-47b2-acf3-d9d8571c7a87
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124022(v=EXCHG.150)
ms:contentKeyID: 50481318
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Avviare e arrestare i servizi IMAP4

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-05_

Per impostazione predefinita, i due servizi IMAP4, il servizio IMAP4 di Microsoft Exchange IMAP4 e il servizio Back-end IMAP4 di Microsoft Exchange, non vengono avviati sui computer su cui è installato MicrosoftExchange Server 2013. È necessario avviare questi due servizi per consentire ai client di posta elettronica di connettersi a Exchange utilizzando IMAP4. Quando questi servizi sono in esecuzione, Exchange 2013 accetta le comunicazioni client IMAP4 non protette sulla porta 143 e sulla porta 993 utilizzando SSL (Secure Sockets Layer).

Il servizio IMAP4 di Microsoft Exchange viene eseguito sui computer Exchange 2013 che eseguono il ruolo del server Accesso client. Il servizio back-end IMAP4 di Microsoft Exchange viene eseguito sul computer Exchange 2013 che esegue il ruolo del server Cassette postali. Negli ambienti in cui i ruoli del server Accesso client e Cassette postali sono attivi sullo stesso computer, entrambi i servizi vengono gestiti sullo stesso computer.

Per ulteriori informazioni su POP3 e IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni POP3 e IMAP4" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare lo snap-in Servizi di Microsoft Management Console per avviare o arrestare i servizi IMAP4

Per avviare i servizi IMAP4:

1.  Su un computer su cui è attivo il ruolo del server Accesso client, fare clic su **Start**, selezionare **Programmi**, **Strumenti di amministrazione**, quindi fare clic su **Servizi**. Fare clic con il pulsante destro del mouse su **Microsoft Exchange - IMAP4** e scegliere **Avvia**.

2.  Su un computer su cui è attivo il ruolo del server Cassette postali, fare clic su **Start**, selezionare **Programmi**, **Strumenti di amministrazione**, quindi fare clic su **Servizi**. Fare clic con il pulsante destro del mouse su **Microsoft Exchange - Back-end IMAP4** e scegliere **Avvia**.

Per interrompere i servizi IMAP4:

1.  Su un computer su cui è attivo il ruolo del server Accesso client, fare clic su **Start**, selezionare **Programmi**, **Strumenti di amministrazione**, quindi fare clic su **Servizi**. Fare clic con il pulsante destro del mouse su **Microsoft Exchange - IMAP4** e scegliere **Interrompi**.

2.  Su un computer su cui è attivo il ruolo del server Cassette postali, fare clic su **Start**, selezionare **Programmi**, **Strumenti di amministrazione**, quindi fare clic su **Servizi**. Fare clic con il pulsante destro del mouse su **Microsoft Exchange - Back-end IMAP4** e scegliere **Interrompi**.

## Utilizzare Shell per avviare o arrestare i servizi IMAP4

Per avviare i servizi IMAP4:

1.  Sul computer su cui è attivo il ruolo del server Accesso client, eseguire il comando riportato di seguito in Shell per avviare il servizio IMAP4 di Microsoft Exchange.
    
    ```powershell
    Start-service msExchangeIMAP4
    ```

2.  Sul computer su cui è attivo il ruolo del server Cassette postali, eseguire il comando riportato di seguito in Shell per avviare il servizio Back-end IMAP4 di Microsoft Exchange.
    
    ```powershell
    Start-service msExchangeIMAP4BE
    ```

Per interrompere i servizi IMAP4:

1.  Sul computer su cui è attivo il ruolo del server Accesso client, eseguire il comando riportato di seguito in Shell per interrompere il servizio IMAP4 di Microsoft Exchange.
    
    ```powershell
    Stop-service msExchangeIMAP4
    ```

2.  Sul computer su cui è attivo il ruolo del server Cassette postali, eseguire il comando riportato di seguito in Shell per interrompere il servizio Back-end IMAP4 di Microsoft Exchange.
    
    ```powershell
    Stop-service msExchangeIMAP4BE
    ```

## Utilizzare net start per avviare o arrestare i servizi IMAP4

Per avviare i servizi IMAP4:

1.  Sul computer su cui è attivo il ruolo del server Accesso client, eseguire il comando riportato di seguito nel prompt dei comandi per avviare il servizio IMAP4 di Microsoft Exchange.
    
    ```powershell
    net start msExchangeIMAP4
    ```

2.  Sul computer su cui è attivo il ruolo del server Cassette postali, eseguire il comando riportato di seguito nel prompt dei comandi per avviare il servizio Back-end IMAP4 di Microsoft Exchange.
    
    ```powershell
    net start msExchangeIMAP4BE
    ```

Per interrompere i servizi IMAP4:

1.  Sul computer su cui è attivo il ruolo del server Accesso client, eseguire il comando riportato di seguito nel prompt dei comandi per interrompere il servizio IMAP4 di Microsoft Exchange.
    
    ```powershell
    Net Stop MSExchangeIMAP4
    ```

2.  Sul computer su cui è attivo il ruolo del server Cassette postali, eseguire il comando riportato di seguito nel prompt dei comandi per interrompere il servizio Back-end IMAP4 di Microsoft Exchange.
    
    ```powershell
    Net Stop MSExchangeIMAP4BE
    ```

## Come verificare se l'operazione ha avuto esito positivo

1.  Sul server Accesso client di Exchange, aprire Task Manager Windows. Nella scheda **Servizi**, lo stato di **MSExchangeIMAP4** è **In esecuzione** se il servizio IMAP4 di Microsoft Exchange è in esecuzione.

2.  Sul server cassette postali di Exchange, aprire Task Manager Windows. Nella scheda **Servizi**, lo stato di **MSExchangeIMAP4BE** è **In esecuzione** se il servizio Back-end IMAP4 di Microsoft Exchange è in esecuzione.


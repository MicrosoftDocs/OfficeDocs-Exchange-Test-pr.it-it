---
title: 'Configurare gli intervalli di ripetizione, reinvio e scadenza messaggio: Exchange 2013 Help'
TOCTitle: Configurare gli intervalli di ripetizione, reinvio e scadenza messaggio
ms:assetid: 5420124f-aa4c-4702-b493-40a9a7edb786
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998043(v=EXCHG.150)
ms:contentKeyID: 51407365
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare gli intervalli di ripetizione, reinvio e scadenza messaggio

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-12-16_

In Microsoft Exchange Server 2013, è possibile configurare gli intervalli di tentativi, reinvio e scadenza messaggio nel servizio di trasporto sui server cassette postali e nei server Trasporto Edge. Per una descrizione di queste impostazioni, vedere [Intervalli di ripetizione, reinvio e scadenza messaggio](message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Servizio trasporto" e "Server Trasporto Edge" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md) .

  - Qualsiasi impostazione personalizzata per singolo server apportata nei file di configurazione dell'applicazione XML di Exchange, ad esempio, i file web.config sui server Accesso client oppure il file EdgeTransport.exe.config sui server Cassette postali, verrà sovrascritta quando si installa un aggiornamento cumulativo di Exchange. Salvare queste informazioni in modo da poter facilmente riconfigurare il server dopo l'installazione. È necessario riconfigurare queste impostazioni dopo aver installato un aggiornamento cumulativo di Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzare EdgeTransport.exe.config per configurare il numero di tentativi glitch coda, l'intervallo di tentativi glitch coda, l'intervallo di tentativi coda di recapito delle cassette postali e il tempo di inattività massimo prima di inviare di nuovo intervallo.

Per configurare il numero di tentativi glitch coda, l'intervallo di tentativi glitch coda, l'intervallo di tentativi coda di recapito delle cassette postali e il tempo di inattività massimo prima di inviare nuovamente intervallo è modificare chiavi nel file di configurazione dell'applicazione XML %ExchangeInstallPath%Bin\\EdgeTransport.exe.config nel server cassette postali o nel server Trasporto Edge. Dopo aver riavviato il servizio di trasporto di Microsoft Exchange, vengono applicate le modifiche salvate a questo file. Quando viene riavviato il servizio, il flusso della posta nel server è temporaneamente interrotto.

1.  In una finestra del prompt dei comandi nel server cassette postali o nel server Trasporto Edge aprire il file EdgeTransport.exe.config in blocco note eseguendo il comando seguente:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Individuare le chiavi seguenti nella sezione `<appSettings>` .
    
        <add key="QueueGlitchRetryCount" value="<Integer>" />
        <add key="QueueGlitchRetryInterval" value="<hh:mm:ss>" />
        <add key="MailboxDeliveryQueueRetryInterval" value="<hh:mm:ss>" />
        <add key="MaxIdleTimeBeforeResubmit" value="<hh:mm:ss>" />
    
    Questo esempio vengono modificate glitch coda tentativi numero 6, l'intervallo tentativi glitch coda 30 secondi, l'intervallo di tentativi coda recapito delle cassette postali su 3 minuti e tempo di inattività massimo prima di inviare nuovamente intervallo su 6 ore.
    
        <add key="QueueGlitchRetryCount" value="6" />
        <add key="QueueGlitchRetryInterval" value="00:00:30" />
        <add key="MailboxDeliveryQueueRetryInterval" value="00:03:00" />
        <add key="MaxIdleTimeBeforeResubmit" value="6:00:00" />

3.  Se non si desidera salvare e chiudere il file EdgeTransport.exe.config.

4.  Riavviare il servizio di trasporto di Microsoft Exchange utilizzando il seguente comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## Configurare il numero di tentativi di errore temporaneo, l'intervallo di errore temporaneo tentativi e l'intervallo di tentativi di errore di connessione in uscita

Il numero di tentativi di errore temporaneo specifica il numero di tentativi di connessione a cui si è tentato dopo i tentativi di connessione controllati per i tasti `QueueGlitchRetryCount` e `QueueGlitchRetryInterval` non riusciti. Il numero predefinito di tentativi di errore temporaneo è 6. L'intervallo di input valido per questo parametro è compreso tra 0 e 15. Se si imposta il numero di errore temporaneo tentativi su 0, al successivo tentativo di connessione è controllato dall' *intervallo tentativi di connessione in uscita*.

L'intervallo di errore temporaneo tentativi specifica l'intervallo tra un tentativo di connessione specificata del numero di tentativi di errore temporaneo. Nel servizio trasporto su un server cassette postali, l'intervallo di tentativi di errore temporaneo predefinito è 5 minuti. In un server Trasporto Edge, l'intervallo di tentativi di errore temporaneo predefinito è 10 minuti.

L'intervallo di tentativi di connessione in uscita errore specifica l'intervallo tentativi dei tentativi di connessione in uscita che non sono state precedentemente. I tentativi di connessione non riuscita in precedenza sono controllati dal numero di tentativi di errore temporaneo e l'intervallo di tentativi di errore temporaneo. Il valore predefinito per un errore di connessione in uscita tentativi per il trasporto servizio su un server cassette postali è 10 minuti. Il valore predefinito in un server Trasporto Edge è 30 minuti.

## Utilizzare EAC per configurare il numero di tentativi di errore temporaneo, l'intervallo di tentativi di errore temporaneo o l'intervallo di tentativi di errore di connessione in uscita

1.  Nell'interfaccia di amministrazione di Exchange (EAC), fare clic su **server** \> **server**, selezionare il server, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica")e quindi fare clic su **limiti di trasporto**.

2.  Nella sezione **tentativi** immettere un valore per **errore di connessione in uscita intervallo tentativi (secondi)**, l' **intervallo (minuti) di tentativi di errore temporaneo** o **tentativi di errore temporaneo**.

3.  Al termine, fare clic su **Save**.

## Utilizzo della Shell per configurare il numero di tentativi di errore temporaneo, l'intervallo di errore temporaneo tentativi e l'intervallo di tentativi di errore di connessione in uscita

Utilizzare la sintassi seguente per configurare il numero di tentativi di errore temporaneo, l'intervallo di errore temporaneo tentativi e l'intervallo di tentativi di connessione in uscita errore nel servizio di trasporto in un server cassette postali o in un server Trasporto Edge.

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

In questo esempio vengono modificati i valori seguenti nel server cassette postali denominato Mailbox01: nel server Trasporto Edge Exchange01.

  - Il numero di tentativi di errore temporaneo viene impostato su 8.

  - L'intervallo di errore temporaneo tentativi è impostato su 1 minuto.

  - L'intervallo di tentativi di errore di connessione in uscita è impostato su 45 minuti.

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00


> [!NOTE]
> I parametri <EM>TransientFailureRetryCount</EM> e <EM>TransientFailureRetryInterval</EM> sono anche disponibili nel cmdlet <STRONG>Set-FrontEndTransportService</STRONG> per il servizio trasporto Front-End sui server Accesso Client.



## Configurare il numero di tentativi di errore temporaneo, l'intervallo di errore temporaneo tentativi e l'intervallo di tentativi di errore di connessione in uscita

## Utilizzare EAC per configurare il numero di tentativi di errore temporaneo, l'intervallo di errore temporaneo tentativi e l'intervallo di tentativi di errore di connessione in uscita

1.  In EAC, fare clic su **server** \> **server**, selezionare il server, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica")e quindi fare clic su **limiti di trasporto**.

2.  Nella sezione **tentativi** immettere un valore per **errore di connessione in uscita intervallo tentativi (secondi)**, l' **intervallo (minuti) di tentativi di errore temporaneo** o **tentativi di errore temporaneo**.

3.  Al termine, fare clic su **Save**.

## Utilizzo della Shell per configurare il numero di tentativi di errore temporaneo, l'intervallo di errore temporaneo tentativi e l'intervallo di tentativi di errore di connessione in uscita

Utilizzare la sintassi seguente per configurare il numero di tentativi di errore temporaneo, l'intervallo di errore temporaneo tentativi e l'intervallo di tentativi di connessione in uscita errore nel servizio di trasporto in un server cassette postali o in un server Trasporto Edge.

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

In questo esempio vengono modificati i valori seguenti nel server cassette postali denominato Mailbox01: nel server Trasporto Edge Exchange01.

  - Il numero di tentativi di errore temporaneo viene impostato su 8.

  - L'intervallo di errore temporaneo tentativi è impostato su 1 minuto.

  - L'intervallo di tentativi di errore di connessione in uscita è impostato su 45 minuti.

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00


> [!NOTE]
> I parametri <EM>TransientFailureRetryCount</EM> e <EM>TransientFailureRetryInterval</EM> sono anche disponibili nel cmdlet <STRONG>Set-FrontEndTransportService</STRONG> per il servizio trasporto Front-End sui server Accesso Client.



## Utilizzo della Shell per configurare l'intervallo di tentativi di messaggio

Per impostazione predefinita, l'intervallo di tentativi di messaggio è `00:15:00` o 15 minuti. È consigliabile non modificare il valore predefinito a meno che non Microsoft al servizio supporto tecnico notifiche per eseguire questa operazione.

Utilizzare la sintassi seguente per impostare l'intervallo di tentativi di messaggio.

    Set-TransportService <ServerIdentity> -MessageRetryInterval <dd.hh:mm:ss>

In questo esempio viene impostato l'intervallo tentativi messaggio 20 minuti sul server cassette postali denominato Mailbox01.

    Set-TransportService Mailbox01 -MessageRetryInterval 00:20:00

## Configurare le impostazioni di timeout DSN di ritardo

È possibile utilizzare EAC o Shell per configurare l'intervallo di timeout di ritardo DSN notifica. Questa impostazione viene applicata solo nel server di trasporto locale. È possibile utilizzare solo la Shell per abilitare o disabilitare l'invio di messaggi DSN ritardo ai mittenti interni ed esterni. Queste impostazioni vengono applicate a tutti i server di trasporto nell'organizzazione.


> [!NOTE]
> Nei server Trasporto Hub Exchange&nbsp;2007, tutti i parametri <EM>ExternalDSN*</EM> e <EM>InternalDSN*</EM> sono disponibili nel cmdlet <STRONG>Set-TransportServer</STRONG> , non il cmdlet <STRONG>Set-TransportConfig</STRONG> . Se si dispongono di tutti i server Trasporto Hub Exchange&nbsp;2007 all'interno dell'organizzazione, è necessario apportare modifiche a questi valori utilizzando il cmdlet <STRONG>Set-TransportServer</STRONG> in ogni server Trasporto Hub Exchange&nbsp;2007.



## Utilizzare EAC per configurare l'intervallo di timeout notifica di messaggio di ritardo DSN

1.  In EAC, fare clic su **server** \> **server**, selezionare il server, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica")e quindi fare clic su **limiti di trasporto**.

2.  Nella sezione **notifiche**, immettere un valore per **il mittente di notifica quando il messaggio è ritardato dopo (ore)**.

3.  Al termine, fare clic su **Save**.

## Utilizzo della Shell per configurare l'intervallo di timeout notifica di messaggio di ritardo DSN

Utilizzare la sintassi seguente per impostare l'intervallo di tentativi di messaggio.

    Set-TransportService <ServerIdentity> -DelayNotificationTimeout <dd.hh:mm:ss>

In questo esempio viene impostato l'intervallo di timeout notifica di messaggio di ritardo DSN 6 ore sul server cassette postali denominato Mailbox01.

    Set-TransportService Mailbox01 -DelayNotificationTimeout 06:00:00

## Utilizzare la Shell per abilitare o disabilitare l'invio di notifiche di ritardo DSN ai mittenti interni o esterni

Utilizzare la sintassi seguente per configurare le impostazioni di notifica DSN ritardo.

    Set-TransportConfig -ExternalDelayDSNEnabled <$true | $false> -InternalDelayDSNEnabled <$true |$false>

Questo esempio viene disattivato l'invio di messaggi di notifica di ritardo DSN ai mittenti esterni.

    Set-TransportConfig -ExternalDelayDSNEnabled $false

Questo esempio viene disattivato l'invio di messaggi di notifica di ritardo DSN ai mittenti interni.

    Set-TransportConfig -InternalDelayDSNEnabled $false

## Configurare l'intervallo di timeout di scadenza messaggio

## Utilizzare EAC per configurare l'intervallo di timeout di scadenza messaggio

1.  In EAC, fare clic su **server** \> **server**, selezionare il server, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica")e quindi fare clic su **limiti di trasporto**.

2.  Nella sezione **la scadenza dei messaggi**, immettere un valore per **tempo massimo dall'invio (giorni)**.

3.  Al termine, fare clic su **Save**.

## Utilizzo della Shell per configurare l'intervallo di timeout di scadenza messaggio

Per configurare l'intervallo di timeout di scadenza dei messaggi, utilizzare la sintassi seguente.

    Set-TransportService <ServerIdentity> -MessageExpirationTimeout <dd.hh:mm:ss>

In questo esempio viene impostato l'intervallo di timeout di scadenza messaggio 4 giorni in Exchange server denominato Mailbox01.

    Set-TransportService Mailbox01 -MessageExpirationTimeout 4.00:00:00


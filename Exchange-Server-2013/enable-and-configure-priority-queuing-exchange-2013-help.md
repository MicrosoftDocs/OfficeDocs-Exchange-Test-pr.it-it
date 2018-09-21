---
title: 'Attivare e configurare Accodamento prioritario: Exchange 2013 Help'
TOCTitle: Attivare e configurare Accodamento prioritario
ms:assetid: 1975d85d-2f1d-4852-8d19-e74ba4ba3853
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ891104(v=EXCHG.150)
ms:contentKeyID: 51407344
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Attivare e configurare Accodamento prioritario

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-12-16_

*Accodamento priorità* è una funzionalità di Microsoft Exchange Server 2013 che consente alla priorità del messaggio configurata dal mittente in Microsoft Outlook o Outlook Web Access di influenzare l'elaborazione del messaggio dal servizio di trasporto nel server Cassette postali. Quando questa funzionalità è abilitata, i messaggi con Priorità alta vengono trasmessi alle destinazioni appropriate prima di quelli con Priorità normale. Questi ultimi vengono trasmessi alle destinazioni prima dei messaggi con Priorità bassa. Per ulteriori informazioni, vedere [Accodamento prioritario](priority-queuing-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 15 minuti

  - Le autorizzazioni di Exchange non sono applicabili alle procedure descritte in questo argomento. Queste procedure vengono eseguite nel sistema operativo del server di Exchange.

  - Le modifiche salvate nel file di configurazione dell'applicazione EdgeTransport.exe.config vengono applicate dopo aver avviato il servizio di trasporto di Microsoft Exchange.

  - Quando si riavvia il servizio, il flusso di posta sul server viene interrotto temporaneamente.

  - Qualsiasi impostazione personalizzata per singolo server apportata nei file di configurazione dell'applicazione XML di Exchange, ad esempio, i file web.config sui server Accesso client oppure il file EdgeTransport.exe.config sui server Cassette postali, verrà sovrascritta quando si installa un aggiornamento cumulativo di Exchange. Salvare queste informazioni in modo da poter facilmente riconfigurare il server dopo l'installazione. È necessario riconfigurare queste impostazioni dopo aver installato un aggiornamento cumulativo di Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare il prompt dei comandi per abilitare e configurare l'accodamento priorità nel file EdgeTransport.exe.config.

1.  In una finestra del prompt dei comandi, utilizzare il seguente comando per aprire il file di configurazione dell'applicazione EdgeTransport.exe.config in Blocco note:
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

2.  Trovare le seguenti chiavi nella sezione `<appSettings>`.
    
        <add key="PriorityQueuingEnabled" value="false" />
        <add key="MaxPerDomainHighPriorityConnections" value="3" />
        <add key="MaxPerDomainNormalPriorityConnections" value="15" />
        <add key="MaxPerDomainLowPriorityConnections" value="2" />
        <add key="HighPriorityMessageExpirationTimeout" value="8:00:00" />
        <add key="NormalPriorityMessageExpirationTimeout" value="2.00:00:00" />
        <add key="LowPriorityMessageExpirationTimeout" value="2.00:00:00" />
        <add key="HighPriorityDelayNotificationTimeout" value="00:30:00" />
        <add key="NormalPriorityDelayNotificationTimeout" value="4:00:00" />
        <add key="LowPriorityDelayNotificationTimeout" value="8:00:00" />
        <add key="MaxHighPriorityMessageSize" value="250KB" />
    
    Per abilitare l'accodamento priorità nel servizio di trasporto nel server Cassette postali, utilizzare il seguente valore:
    
    ```command line
<add key="PriorityQueuingEnabled" value="true" />
```
    
    Configurare i rimanenti valori dell'accodamento prorità o lasciarli con i valori predefiniti.

3.  Al termine, salvare e chiudere il file EdgeTransport.exe.config.

4.  Riavviare il servizio di trasporto di Microsoft Exchange utilizzando il seguente comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta abilitazione e configurazione dell'accodamento priorità, effettuare le seguenti operazioni:

1.  Verificare che la chiave **PriorityQueueinEnabled** nel file EdgeTransport.exe.config abbia il valore `"true"`.

2.  Utilizzare Outlook per creare un messaggio di prova con priorità elevata più grande del valore specificato dalla chiave **MaxHighPriorityMessageSize**, quindi verificare se il messaggio arriva come un messaggio di priorità normale.

3.  Provare a verificare che i messaggi con priorità maggiore arrivino prima di quelli con priorità inferiore inviati allo stesso destinatario o stessa destinazione. È possibile provare a utilizzare più cassette postali per inviare contemporaneamente più messaggi di prova simili con diversi valori di priorità allo stesso destinatario.


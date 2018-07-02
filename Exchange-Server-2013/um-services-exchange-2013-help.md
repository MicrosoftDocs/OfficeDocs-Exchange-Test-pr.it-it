---
title: 'Servizi di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Servizi di messaggistica unificata
ms:assetid: f36835f2-1e5f-4e5a-88bc-0672af1e3498
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125191(v=EXCHG.150)
ms:contentKeyID: 50555712
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Servizi di messaggistica unificata

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-18_

I server Accesso client su cui è in esecuzione il servizio di routing di chiamate di messaggistica unificata di Microsoft Exchange e i server Cassette postali con il servizio Messaggistica unificata di Microsoft Exchange consentono di distribuire la messaggistica unificata e le funzionalità di segreteria telefonica agli utenti dell'organizzazione.

Per informazioni sulle attività di gestione relative ai servizi di messaggistica unificata? vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

**Sommario**

Client Access and Mailbox servers

Server configuration settings

Server operation

## Server Accesso client e Cassette postali

In Exchange 2013 i ruoli server presenti in Exchange 2007 ed Exchange 2010 sono combinati in due tipi di server e tutti i componenti o servizi di questi ruoli server vengono eseguiti sullo stesso server fisico o su due server separati denominati Accesso client e Cassette postali.

In questo nuovo modello, il server Accesso client è responsabile dell'individuazione automatica, di SSL (Secure Sockets Layer), dell'autenticazione, del reindirizzamento e del proxy. Il server Accesso client è il punto di ingresso per qualsiasi chiamata in arrivo o richiesta SIP di messaggistica unificata. La logica di instradamento e il comando SIP REDIRECT vengono implementati come un servizio incluso automaticamente in un server Accesso client. Questo servizio è noto come servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange. Viene eseguito su ogni server Accesso client dell'organizzazione.

Quando un server Accesso client riceve un SIP INVITE per una chiamata in entrata, il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange reindirizza la chiamata al server Cassette postali. Viene quindi creato un canale di supporto (RTP o SRTP) tra il gateway VoIP, PBX IP o SBC (Session Border Controller) e il server Cassette postali che ospita la cassetta postale dell'utente. Sebbene il server Accesso client agisca come un reindirizzatore SIP, gestisce solo le richieste provenienti da gateway VoIP, PBX IP o SBC. Non riceve alcun traffico multimediale. Il traffico multimediale che utilizza RTP o SRTP viene passato solo tra server Cassette postali e peer SIP quali gateway VoIP, PBX IP o SBC. Quando si distribuisce Exchange 2013 e messaggistica unificata, è necessari configurare i propri gateway VoIP, PBX IP o SBC per puntare ai server Accesso client installati in modo che le chiamate in entrata vengano correttamente instradate per la messaggistica unificata.

In Exchange 2013, il server Cassette postali dispone degli stessi processi del ruolo server Messaggistica unificata gestito in Exchange 2007 e Exchange 2010. Il server Cassette postali esegue sia il servizio Messaggistica unificata di Microsoft Exchange che il processo di lavoro di messaggistica unificata.

Quando si installano i server Accesso client e Cassette postali e si distribuisce la messaggistica unificata, non è necessario associare o aggiungere tali server ai dial plan di messaggistica unificata. I server Accesso client e Cassette postali rispondono a tutte le chiamate in arrivo e utilizzano i dial plan di messaggistica unificata per individuare gli utenti.

Tuttavia, se si sta eseguendo l'integrazione della messaggistica unificata con Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server, entrambi i canali multimediali SIP e RTP o SRTP per le chiamate in arrivo sono gestiti dai server Lync e dai server Cassette postali. In un ambiente integrato Lync, non sono disponibili gateway VoIP, PBX IP PBX o SBC. Lync considera il server Cassette postali su cui è in esecuzione il servizio Messaggistica unificata di Microsoft Exchange come un server di messaggistica unificata di Exchange 2010. I server Cassette postale e Accesso client sono considerati peer attendibili in quanto entrambi devono essere aggiunti a un dial plan SIP. Lync instrada la chiamata in entrata utilizzando il componente Inbound Routing che utilizza SIP per comunicare con il server Accesso client quindi instrada la chiamata al server Cassette postali.

Inizio pagina

## Impostazioni di configurazione del server

In Exchange 2013, tutte le impostazioni di configurazione e dei componenti di messaggistica unificata che venivano applicate a un singolo computer su cui era in esecuzione il ruolo server Messaggistica unificata in Exchange 2010 sono ancora disponibili. Alcuni componenti e impostazioni di configurazioni sono tuttavia presenti nei server Accesso client mentre altri sono disponibili nei server Cassette postali. In alcuni casi, la stessa impostazione è disponibile su entrambi. L'elenco seguente mostra i parametri e le impostazioni disponibili sul server Accesso client e sul server Cassette postali.

  - \[-DialPlans \<MultiValuedProperty\>\]

  - \[-MaxCallsAllowed \<Int32\>\]

  - \[-SipTcpListeningPort \<Int32\>\]

  - \[-SipTlsListeningPort \<Int32\>\]

  - \[-Status \<Enabled | Disabled | NoNewCalls\>\]

  - \[-UMStartupMode \<TCP | TLS | Dual\>\]

Per il server Cassette postali si utilizzeranno i cmdlet **Set-UMService**, **Get-UMService**, **Enable-UMService** e **Disable-UMService** per visualizzare o configurare le proprietà di messaggistica unificata per il servizio Messaggistica unificata di Microsoft Exchange. Un diverso gruppo di cmdlet, **Set-UMCallRouterSettings** e **Get-UMCallRouterSettings**, viene utilizzato per visualizzare o configurare le proprietà del servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange su un server Accesso client. Questo assicura che i cmdlet esistenti **Get-UMServer**, **Set-UMServer**, **Enable-UMServer** e **Disable-UMServer** provenienti da Exchange 2007 e Exchange 2010 possano funzionare in una distribuzione in cui coesistono server Cassette postali di Exchange 2013. Questo assicura che i cmdlet possano funzionare anche se i server Accesso client e i server Cassette postali sono installati o nello stesso computer o in computer diversi.

Inizio pagina

## Funzionamento del server

Quando i server Accesso client e Cassette postali vengono installati, vengono automaticamente abilitati alla funzione di risposta alle chiamate vocali in arrivo e in uscita e di instradamento dei messaggi di posta vocale ai destinatari appropriati nell'organizzazione di Exchange.

È possibile consentire al servizio Messaggistica unificata di Microsoft Exchange su un server Cassette postali o al servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange su un server Accesso client di rispondere alle nuove chiamate oppure impedire questa funzionalità. Per impostazione predefinita, un server Cassette postali o Accesso client si trova nello stato abilitato dopo che è stato installato. Quando si imposta un server Cassette postali o Accesso client per l'accettazione delle chiamate vocali, fax, dell'operatore automatico e di Outlook Voice Access in arrivo, si utilizza il cmdlet **Set-ServerComponentState**.

La configurazione della modalità di mantenimento per un server Cassette postali o Accesso client di Exchange 2013 consente di scollegare il server dal servizio. Scollegare un server Cassette postali dal servizio significa che il server non ospiterà database attivi, tutte le code di trasporto saranno vuote e il server non accetterà chiamate in arrivo dai server Accesso client, dai gateway VoIP, IP PBX, PBX abilitati a SIP o SBC. Scollegare un server Accesso client dal servizio significa che il server non accetterà chiamate in arrivo da gateway VoIP, IP PBX, PBX abilitati a SIP o SBC.

In Exchange 2007 ed Exchange 2010 era presente un parametro di stato che poteva essere utilizzato per controllare lo stato funzionale di un server Messaggistica unificata. In Exchange 2013 non è disponibile alcun parametro di stato per questo scopo nel cmdlet **Set-UMService** per un server Cassette postali o nel cmdlet **Set-UMCallRouterSettings** su un server Accesso client.

Sebbene i server Accesso client e Cassette postali siano impostati sullo stato abilitato quando vengono installati, nessuno dei due server può elaborare e instradare correttamente le chiamate in arrivo agli utenti abilitati alla messaggistica unificata fino a quando non viene collegato un dial plan di messaggistica unificata ad almeno un gateway IP di messaggistica unificata.

Una volta che il dial plan è stato collegato a un gateway IP di messaggistica unificata, i server Accesso client e Cassette postali individuano tutti i gateway IP di messaggistica unificata associati al dial plan di messaggistica unificata e ai gateway VoIP, IP PBX e SBC. Per rilevare e identificare le modifiche di configurazione sui dial plan di messaggistica unificata o sui gateway IP di messaggistica unificata, il server Accesso client o Cassette postali eseguirà una verifica sulla configurazione ogni 10 minuti.

Se vengono identificate modifiche di configurazione mediante il gateway IP di messaggistica unificata, il server Accesso client o Cassette postali si comporterà di conseguenza, vale a dire che inizierà a utilizzare o smetterà di utilizzare i gateway VoIP, gli IP PBX o gli SBC appropriati. Una volta che i server Accesso client e Cassette postali rispondono alle chiamate in arrivo per gli utenti collegati a un dial plan di messaggistica unificata e comunicano correttamente con i gateway VoIP, IP PBX ed SBC, è possibile eseguire un insieme di operazioni diagnostiche per verificare che non ci siano problemi e che la connettività tra i server Exchange e i gateway VoIP, IP PBX o SBC funzioni correttamente.

Inizio pagina


---
title: 'Supporto IPv6 in messaggistica unificata: Exchange 2013 Help'
TOCTitle: Supporto IPv6 in messaggistica unificata
ms:assetid: 91242c85-ce4e-422a-954e-ab623d3d6939
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150536(v=EXCHG.150)
ms:contentKeyID: 50481176
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supporto IPv6 in messaggistica unificata

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-04-07_

Internet Protocol versione 6 (IPv6) è la versione più recente del protocollo IP. IPv6 ha lo scopo di colmare molte lacune di IPv4, cioè la precedente versione del protocollo. In Microsoft Exchange Server 2010, IPv6 è supportato solo quando è in uso anche IPv4. L'ambiente di Exchange IPv6 puro non è supportato. L'utilizzo degli indirizzi IPv6 e degli intervalli di indirizzi IP è supportato solo quando sul computer con Exchange 2010 sono abilitati sia IPv6 che IPv4 e se la rete supporta entrambe le versioni degli indirizzi IP. Tuttavia, dal momento che IPv4 e IPv6 sono protocolli completamente diversi, una rete IPv4 non è in grado di comunicare direttamente con una rete IPv6 e viceversa. Per gestire questa mancanza, gli amministratori di rete devono distribuire dispositivi, ad esempio router, che possano instradare le informazioni tra reti IPv4 e reti IPv6. Se Exchange 2010 viene distribuito utilizzando sia IPv4 sia IPv6, tutti i ruoli dei server, fatta eccezione per la messaggistica unificata, potranno inviare e ricevere dati da dispositivi, server e client che utilizzano indirizzi IPv6. In Exchange 2013, la messaggistica unificata non è più un ruolo del server separato come Trasporto, Accesso client e Cassette postali in Exchange 2007 e in Exchange 2010. I componenti relativi alla messaggistica unificata e i servizi di sintesi vocali vengono eseguiti solo sui server Accesso client e Cassette postali.

In Exchange 2013, poiché l'architettura di messaggistica unificata è cambiata e ora richiede Unified Communications Managed API (UCMA) v4.0 per supportare sia IPv4 sia IPv6, nonché altre funzionalità di Exchange, entrambi i server Accesso client e Cassette postali che dispongono di componenti e servizi di messaggistica unificata supporteranno pienamente le reti IPv6.

## Supporto di IPv6

A partire da Exchange 2010 Service Pack 1 (SP1), il ruolo del server Messaggistica unificata affidabile UCMA 2.0 per la segnalazione sottostante protocollo SIP (Session Initiation) e la sintesi vocale elaborazione. UCMA 2.0 è il componente principale per la funzionalità di riconoscimento vocale di messaggistica unificata. UCMA 2.0 include uno stack SIP, uno stack multimediale e motori di riconoscimento vocale per riconoscimento vocale automatico (ASR), oltre alla sintesi vocale che viene generata dalla funzionalità di sintesi vocale (TTS).

In Exchange 2010, esegue un doppio stack (IPv4 e IPv6) è stato necessario per tutti i ruoli del server ad eccezione di messaggistica unificata perché alla messaggistica unificata necessari UCMA 2.0, ma solo IPv4, IPv6 non è supportato. Per Exchange 2013 UCMA 4.0 utilizzati dalla messaggistica unificata ed è necessaria per l'installazione Exchange 2013 sul server cassette postali e accesso Client. UCMA 4.0 è necessaria per supportare le funzionalità nuove e per il supporto di IPv6.

Di seguito sono riportati alcuni dei motivi per cui la messaggistica unificata ora utilizza UCMA 4.0 per supportare le nuove funzionalità di Exchange 2013, tra cui IPv6:

  - Alcune agenzie governative richiedono il supporto IPv6 per i prodotti utilizzati.

  - La messaggistica unificata ora richiede la compatibilità con i dispositivi hardware quali router, gateway IP, IP-PBX e session border controller (SBC) che utilizzano un dual stack (IPv4 e IPv6) o solo IPv6.

  - In Exchange 2013, il servizio Messaggistica unificata di Microsoft Exchange viene eseguito sul server Cassette postali, mentre il servizio Router chiamate di messaggistica unificata di Microsoft Exchange viene eseguito sul server Accesso client. I ruoli del server Accesso client e Cassette postali in Exchange 2013 richiedono sia IPv4 sia IPv6.

  - I servizi online consentono ai client di connettersi al proprio servizio utilizzando IPv4 o IPv6.

  - Lo spazio degli indirizzi IPv4 pubblico è in esaurimento. In Exchange Server 2013 Enterprise, questo non rappresenta un vero problema per la messaggistica unificata, che comunica sempre con peer SIP interni che possono essere distribuiti con uno spazio degli indirizzi IPv4 privato. Tuttavia, per la messaggistica unificata di Exchange ospitata, le attrezzature del cliente devono supportare la messaggistica unificata ospitata utilizzando IPv4 e IPv6.

Fatta eccezione per la messaggistica unificata e per una piccola parte del trasporto, Exchange 2013 può connettersi ai server di Exchange 2010 in un'organizzazione quando un server Accesso client o Cassette postali è in esecuzione nella modalità dual stack con IPv4 e IPv6 abilitati. In pratica, i clienti possono installare Exchange 2013 su computer per cui sono configurati entrambi gli indirizzi degli stack IPv4 e IPv6. In questo modo i client IPv6 e altri server Exchange, tra cui Exchange Server 2010, possono connettersi direttamente a Exchange 2013.

La messaggistica unificata è utilizzabile sui server Windows in esecuzione nella modalità dual stack, perché i protocolli come HTTP ignorano il tipo di trasporto e la messaggistica unificata utilizza i protocolli Voice over IP (VoIP, tra cui SIP/RTP/STUN/TURN/ICE), che non dipendono l'uno dall'altro. Sono inclusi la negoziazione dei supporti (RTP/SRTP), in cui la messaggistica unificata annuncia e comunica un elenco di indirizzi IP ai peer SIP, quali gateway IP, IP-PBX o SBC.

## Implicazioni del supporto IPv6 per la messaggistica unificata

Per abilitare la messaggistica unificata di Exchange 2013 al supporto di IPv6, gli amministratori della messaggistica unificata online e dell'organizzazione devono poter sfruttare IPv6 durante la connessione della messaggistica unificata a dispositivi IPv6, compresi router, gateway IP, IP-PBX e server Office Communications Server 2007 R2 e Microsoft Lync. Tuttavia, se IPv6 non è disponibile per l'interoperabilità e la compatibilità con le versioni precedenti di Exchange, gli amministratori non devono apportare altre modifiche alla configurazione e potrà essere utilizzato IPv4.

In Exchange 2013 Enterprise, la messaggistica unificata deve comunicare direttamente con i peer SIP (gateway IP, IP-PBX e SBC) che potrebbero non supportare IPv6 nel relativo software o firmware. Di conseguenza, la messaggistica unificata deve essere in grado di comunicare direttamente con peer SIP che supportano IPv4 e soprattutto IPv6. Per Exchange 2013 ospitato, la messaggistica unificata comunica con le attrezzature del cliente tramite SBC, Lync Server 2010 o Lync Server 15. Negli ambienti Exchange 2013 ospitati, i client abilitati per SIP IPv6 come SBC e server Lync possono essere distribuiti e di conseguenza possono gestire il processo di conversione da IPv6 a IPv4.

## Supporto dei dispositivi di messaggistica unificata per IPv6

Visto che i server Accesso client e Cassette postali di Exchange 2013 che eseguono componenti e servizi di messaggistica unificata supportano IPv6, anche i fornitori di gateway IP, IP-PBX e SBC devono essere in grado di supportare IPv6. Esistono diversi problemi che interessano il supporto dei dispositivi per IPv6:

  - Esistono gateway IP, IP-PBX e SBC che sono in grado di supportare IPv6 ma che non sono stati testati con IPv6 e la messaggistica unificata. Questo supporto potrà essere aggiunto in futuro, ma la scelta spetta al fornitore dell'hardware.

  - Alcuni gateway IP attualmente non supportano IPv6.

  - Alcuni SBC dispongono di funzionalità IPv4-IPv6, ma attualmente non funzionano con la messaggistica unificata perché non supportano SRTP (Secure Real-time Transport Protocol)/SDES (Session Description Protocol Security).

  - Esistono IP-PBX che non supportano il dual stack e IPv6 puro, ma questi dispositivi non sono stati testati per l'utilizzo con Exchange 2013.

Attualmente UCMA 4.0 è abilitato per IPv6, quindi può accettare connessioni IPv6 ma anche IPv4 quando opera nella modalità doppia o quando effettua connessioni in uscita. L'esecuzione nella modalità doppia consente di effettuare connessioni IPv4 quando necessario per connettersi a versioni precedenti della messaggistica unificata di Exchange. Per le installazioni Lync, questa operazione viene eseguita da Lync Server, che ottiene da Active Directory le informazioni sulla versione più recente di Exchange Server. Affinché i dispositivi di telefonia tradizionali (tra cui gateway IP, IP-PBX e SBC) supportino connessioni IPv6 insieme a IPv4, è necessario che siano in ascolto di entrambi i tipi di connessioni. Questo perché ogni peer SIP deve essere in grado di accettare entrambi i tipi di connessioni per la compatibilità con le versioni precedenti della messaggistica unificata di Exchange. È necessario anche per supportare l'effettuazione di una chiamata esterna per entrambi i tipi di connessioni.

## Configurazione della messaggistica unificata per il supporto di IPv6

Dopo aver installato i server Accesso client e Cassette postali, è necessario creare dial plan, operatori automatici, gateway IP e gruppi di risposta di messaggistica unificata. Per consentire alla messaggistica unificata di supportare IPv6 è necessario:

  - Creare un nuovo gateway IP di messaggistica unificata o configurarne uno esistente con un indirizzo IPv6 per ogni gateway IP, PBX IP o SBC della rete. Durante la creazione e la configurazione dei gateway IP di messaggistica unificata richiesti, è necessario aggiungere l'indirizzo IPv6 o il nome di dominio completo (FQDN) del gateway IP di messaggistica unificata. Se si aggiunge un FQDN al gateway IP di messaggistica unificata, è prima necessario creare i record DNS richiesti per risolvere l'FQDN del gateway IP di messaggistica unificata nell'indirizzo IPv6. Se è già disponibile un gateway IP di messaggistica unificata, per configurare l'indirizzo IPv6 o l'FQDN è possibile utilizzare il cmdlet **Set-UMIPgateway**. Dopo aver creato o configurato i gateway IP di messaggistica unificata, è possibile utilizzare il cmdlet **Get-UMIPgateway** per visualizzare le proprietà del gateway IP di messaggistica unificata e garantire che le impostazioni di IPv6 siano corrette.

  - Configurare il parametro *IPAddressFamily* in ogni gateway IP di messaggistica unificata. Per abilitare il gateway IP affinché accetti pacchetti IPv6, è necessario impostare il gateway IP di messaggistica unificata per accettare connessioni IPv4 e IPv6, o per accettare solo connessioni IPv6, utilizzando il cmdlet **Set-UMIPgateway** e impostando il parametro *IPAddressFamily* su uno dei seguenti valori:
    
      - *IPv4* - È il valore predefinito e viene utilizzato quando non sono configurati altri valori.
    
      - *IPv6* - Consente di utilizzare IPv6. IPv4 non viene utilizzato.
    
      - *Any* - Consente di utilizzare IPv6, ma se il dispositivo non lo supporta viene utilizzato IPv4.

  - Dopo aver configurato i gateway IP di messaggistica unificata, è necessario configurare anche i gateway IP, gli IP-PBX e gli SBC sulla rete per il supporto di IPv6. Per ulteriori dettagli, contattare il fornitore dell'hardware per ottenere un elenco dei dispositivi che supportano IPv6 e informazioni su come configurarli correttamente.

  - Facoltativamente, potrebbe essere necessario impostare i server Accesso client e Cassette postali per accettare il traffico IPv6 se uno dei server è impostato per ricevere solo traffico IPv4. Tuttavia, l'impostazione predefinita per i server Accesso client con il servizio Router chiamate di messaggistica unificata di Microsoft Exchange e i server Cassette postali con il servizio Messaggistica unificata di Microsoft Exchange prevede l'accettazione del traffico IPv4 e IPv6. Per i dettagli sulla configurazione delle impostazioni IPv6 sui server Accesso client e Cassette postali, vedere [Set-UMCallRouterSettings](https://technet.microsoft.com/it-it/library/jj215758\(v=exchg.150\)) e [Set-UMService](https://technet.microsoft.com/it-it/library/jj552412\(v=exchg.150\)).
    
    Potrebbe essere necessario configurare due parametri sui server Accesso client e Cassette postali per supportare IPv6: *IPAddressFamily* e *IPAddressFamilyConfigurable*. Per abilitare un server Accesso client e un server Cassette postali affinché accetti pacchetti IPv6, è necessario impostare il server Accesso client e Cassette postali per accettare connessioni IPv4 e IPv6, o per accettare solo connessioni IPv6: Per configurare il parametro *IPAddressFamily*, il parametro *IPAddressFamilyConfigurable* deve essere impostato su `$true`.

## Logica di indirizzamento IP della messaggistica unificata

La logica alla base del supporto IPv6 per la messaggistica unificata in Exchange 2013 è la seguente:

  - I server Accesso client e Cassette postali restano in ascolto sulle interfacce IPv4 e IPv6 quando viene abilitato il dual stack e i server Accesso client e Cassette postali sono impostati su *IPv6* o *Any*. In caso contrario, viene utilizzato solo IPv4.

  - Per le chiamate in uscita, la messaggistica unificata utilizza la modalità doppia se il parametro *IPAddressFamily* per i gateway IP di messaggistica unificata, i server Accesso client e i server Cassette postali è impostato su *IPv6* o *Any*. In caso contrario, viene utilizzato solo IPv4.

Quando si effettuano chiamate in uscita nella modalità doppia, se il parametro *IPAddressFamily* è impostato su *IPv6* o *Any*:

  - UCMA otterrà un elenco di indirizzi nel nome di dominio completo (FQDN) per un peer SIP che sta tentando di raggiungere.

  - UCMA proverà tutti gli indirizzi IPv6, se presenti.

  - Se UCMA determina che un indirizzo non è disponibile, l'indirizzo sarà incluso in un elenco e non sarà riprovato per un tempo specificato. In questo modo si impedisce che la messaggistica unificata riprovi inutilmente indirizzi notoriamente errati.

  - Se non sono disponibili indirizzi IPv6, UCMA eseguirà il fallback agli indirizzi IPv4 nell'elenco degli indirizzi per i peer SIP.


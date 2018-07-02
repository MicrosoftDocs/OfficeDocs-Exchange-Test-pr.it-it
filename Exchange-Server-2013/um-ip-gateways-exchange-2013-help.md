---
title: 'Gateway IP di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Gateway IP di messaggistica unificata
ms:assetid: 991d77e0-3995-44ab-bedf-52ff7a0301ab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123890(v=EXCHG.150)
ms:contentKeyID: 50481260
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gateway IP di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2014-06-24_

Un gateway IP di messaggistica unificata rappresenta un gateway Voice over IP (VoIP) fisico, un IP Private Branch eXchange (PBX) o un dispositivo hardware Session Border Controller (SBC). Prima che un gateway VoIP, un IP-PBX o un SBC possa essere utilizzato per rispondere alle chiamate in arrivo e inviare chiamate in uscita per gli utenti della segreteria telefonica, è necessario creare un gateway IP di messaggistica unificata per il servizio directory.

**Sommario**

Overview of UM IP gateways

UM IP gateways

IPv6 support for UM IP gateways

Enabling and disabling a UM IP gateway

## Informazioni generali sui sui gateway IP di messaggistica unificata

Solitamente, *gateway* è un termine utilizzato per descrivere un dispositivo fisico che collega due reti incompatibili. Nella messaggistica unificata di Exchange e in altre soluzioni di messaggistica unificata, il gateway VoIP viene utilizzato come traduttore tra la rete PSTN (Public Switched Telephone Network)/TDM (Time Division Multiplex) o rete di telefonia a commutazione di circuito e una rete basata su IP o rete dati a commutazione di pacchetto. Anche un IP-PBX effettua la conversione tra la rete PSTN e una rete a commutazione di pacchetto, pertanto il gateway VoIP non è richiesto se viene utilizzato un IP-PBX. Un gateway VoIP è richiesto solo se si connette a un dispositivo hardware PBX legacy alla distribuzione della messaggistica unificata.


> [!NOTE]
> Una rete a commutazione di pacchetto è una rete in cui i pacchetti (messaggi o frammenti di messaggi) vengono instradati singolarmente tra dispositivi quali router, switch, gateway VoIP, IP-PBX e SBC. Si tratta del contrario di quanto accade in una rete a commutazione di circuito, in cui viene impostata una singola connessione tra due nodi così da poterli utilizzare in modo esclusivo per l'intera durata della comunicazione.



La messaggistica unificata di Exchange si basa sull'abilità del gateway VoIP di tradurre i TDM o protocolli a commutazione di circuito, quali ISDN (Integrated Services Digital Network) o QSIG, da un sistema PBX ai protocolli basati su VoIP or IP, quali SIP (Session Initiation Protocol), RTP (Realtime Transport Protocol) o T.38 per trasmissioni via fax in tempo reale.

Gli IP-PBX sono utilizzati anche per la connessione di una rete di telefonia a commutazione di circuito a una rete a commutazione di pacchetti o dati. Sono inoltre utilizzati per convertire i protocolli a commutazione di circuito in protocolli basati su VoIP o IP, ad esempio SIP, RTP e Secure RTPC (SRTP).

I Session Border Controller (SBC) sono diversi dai gateway VoIP e dagli IP-PBX. Invece di connettere una rete a commutazione di circuito a una rete a commutazione di pacchetti, sono utilizzati per connettere due reti dati su una rete pubblica, come Internet, o su una connessione WAN privata. Nella messaggistica unificata, gli SBC sono utilizzati in una distribuzione ibrida della messaggistica unificata, in cui quest'ultima utilizza alcuni componenti locali e altri, come le cassette postali, situati nel cloud.

## Configurazioni del dispositivo VoIP

Sebbene esistano numerosi tipi e produttori di sistemi PBX, gateway VoIP, IP-PBX e SBC, esistono essenzialmente tre tipi di configurazioni dei dispositivi VoIP:

  - **IP-PBX**   Un singolo dispositivo che converte la rete di telefonia PSTN/TDM o a commutazione di circuito in una rete dati a commutazione di pacchetto o IP

  - **PBX (legacy) e gateway VoIP**   Due componenti separati che insieme eseguono la conversione tra una rete di telefonia PSTN/TDM o a commutazione di circuito in una rete dati a commutazione di pacchetto o IP

  - **SBC**   Uno o più dispositivi che connettono due tipi di reti basate su IP, come una LAN e un centro dati.

Per supportare la messaggistica unificata, vengono utilizzati uno o più tipi di configurazione dei dispositivi IP/VoIP per la connessione di un'infrastruttura di rete di telefonia a un'infrastruttura di rete dati o per la connessione di una distribuzione locale con una distribuzione di messaggistica unificata nel cloud.

## Gateway IP di messaggistica unificata

Il gateway IP di messaggistica unificata contiene uno o più gruppi di risposta di messaggistica unificata e impostazioni di configurazione. I gruppi di risposta di messaggistica unificata sono utilizzati per collegare un gateway IP di messaggistica unificata a un dial plan di messaggistica unificata. La combinazione di gateway IP di messaggistica unificata e gruppo di risposta di messaggistica unificata stabilisce un collegamento tra gateway IP, IP PBX o SBC e un dial plan di messaggistica unificata. Se si creano più gruppi di risposta di messaggistica unificata è possibile associare un singolo gateway IP di messaggistica unificata a più dial plan di messaggistica unificata.

Dopo aver creato un gateway IP di messaggistica unificata, i server Exchange collegati al gateway IP di messaggistica unificata invieranno una richiesta SIP OPTIONS al gateway VoIP, all'IP-PBX o all'SBC per garantire che il dispositivo risponda. Se il gateway VoIP, l'IP-PBX o l'SBC non risponde alla richiesta, il server Exchange registrerà un evento con ID 1400 che segnala che la richiesta ha avuto esito negativo. In questo caso, assicurarsi che il gateway VoIP, l'IP-PBX o l'SBC sia disponibile e online e che la configurazione di messaggistica unificata sia corretta.

Un server Cassette postali comunica solo con gateway VoIP, IP-PBX e SBC elencati come peer SIP attendibili. In alcuni casi, se due gateway VoIP, IP-PBX o SBC sono configurati per l'utilizzo dello stesso indirizzo IP, verrà registrato un evento con ID 1175. La messaggistica unificata protegge da richieste non autorizzate recuperando l'URL interno della directory virtuale dei servizi Web di messaggistica unificata e utilizza questo URL per compilare l'elenco di FQDN relativo ai peer SIP attendibili. Se due nomi di dominio completi vengono risolti nello stesso indirizzo IP, viene registrato questo evento.

## Supporto di IPv6 per i gateway IP di messaggistica unificata

Internet Protocol versione 6 (IPv6) è la versione più recente del protocollo IP. IPv6 ha lo scopo di colmare molte lacune di IPv4, cioè la precedente versione del protocollo. Nelle distribuzioni ibride e locali di Microsoft Exchange Server 2010, IPv6 era supportato solo quando era in uso anche IPv4.

Nelle distribuzioni ibride e locali di Exchange 2013, i componenti relativi alla messaggistica unificata e i servizi di sintesi vocali vengono eseguiti solo sui server Accesso client e Cassette postali. Poiché l'architettura di messaggistica unificata è cambiata e ora richiede Unified Communications Managed API (UCMA) v4.0 per supportare sia IPv4 sia IPv6, nonché altre funzionalità di Exchange, i server Accesso client e Cassette postali che dispongono di componenti e servizi di messaggistica unificata supporteranno pienamente le reti IPv6 e non richiederanno IPv4.

Nelle distribuzioni ibride e locali di Exchange Online, gli amministratori della messaggistica unificata Exchange Online e dell'organizzazione possono utilizzare IPv6 durante la connessione della messaggistica unificata a dispositivi IPv6, compresi router, gateway IP, IP-PBX e server Microsoft Office Communications Server 2007 R2 e Microsoft Lync. Tuttavia, per l'interoperabilità e la compatibilità, è possibile utilizzare IPv4 senza modifiche aggiuntive alla configurazione se il parametro *IPAddressFamily* è impostato su `Any` sui gateway IP di messaggistica unificata.

La messaggistica unificata di Exchange deve ancora comunicare direttamente con i peer SIP (gateway VoIP, IP-PBX e SBC) che potrebbero non supportare IPv6 nel relativo software o firmware. Se non supportano IPv6, la messaggistica unificata deve poter comunicare direttamente con i peer SIP che utilizzano IPv4. Per il servizio di segreteria telefonica ospitata, la messaggistica unificata comunica con le attrezzature del cliente tramite SBC, Lync Server 2010 o Lync Server 2013. Negli ambienti ospitati, i client abilitati per SIP IPv6 come SBC e server Lync possono essere distribuiti per gestire il processo di conversione da IPv6 a IPv4.

Per le distribuzioni ibride e locali, dopo aver installato i server Accesso client e Cassette postali, e per le distribuzioni di messaggistica unificata Exchange Online, è necessario creare gateway IP di messaggistica unificata. Affinché i gateway IP di messaggistica unificata supportino IPv6, è inoltre necessario:

1.  Creare un nuovo gateway IP di messaggistica unificata o configurarne uno esistente con un indirizzo IPv6 per ogni gateway IP, PBX IP o SBC della rete. Durante la creazione e la configurazione dei gateway IP di messaggistica unificata richiesti, è necessario aggiungere l'indirizzo IPv6 o il nome di dominio completo (FQDN) del gateway IP di messaggistica unificata. Se si aggiunge un FQDN al gateway IP di messaggistica unificata, è prima necessario creare i record DNS richiesti per risolvere l'FQDN del gateway IP di messaggistica unificata nell'indirizzo IPv6. Se è già disponibile un gateway IP di messaggistica unificata, per configurare l'indirizzo IPv6 o l'FQDN è possibile utilizzare il cmdlet **Set-UMIPgateway**.

2.  Configurare il parametro *IPAddressFamily* in ogni gateway IP di messaggistica unificata. Per abilitare il gateway VoIP affinché accetti pacchetti IPv6, è necessario impostare il gateway IP di messaggistica unificata per accettare connessioni IPv4 e IPv6, o per accettare solo connessioni IPv6, utilizzando il cmdlet **Set-UMIPgateway**.

3.  Dopo aver configurato i gateway IP di messaggistica unificata, è necessario configurare anche i gateway VoIP, gli IP-PBX e gli SBC sulla rete per il supporto di IPv6. Per ulteriori dettagli, contattare il fornitore dell'hardware per ottenere un elenco dei dispositivi che supportano IPv6 e informazioni su come configurarli correttamente.


> [!NOTE]
> Il numero massimo di un gateway IP di messaggistica unificata per dial plan è 200. Se se ne creano più di 200, il servizio di di messaggistica unificata non si avvierà.



## Abilitazione e disabilitazione di un gateway IP di messaggistica unificata

Per impostazione predefinita, dopo la creazione un gateway IP di messaggistica unificata rimane in uno stato abilitato. Tuttavia il gateway IP di messaggistica unificata può essere abilitato o disabilitato. Se si disabilita un gateway IP di messaggistica unificata, è possibile impostarlo per forzare tutti i server Exchange alla conclusione delle chiamate esistenti. In alternativa, è possibile impostarlo per forzare i server Exchange associati al gateway IP di messaggistica unificata ad interrompere la gestione delle nuove chiamate presentate dal gateway VoIP, dall'IP-PBX o dall'SBC.

Se si sta integrando la messaggistica unificata con Office Communications Server R2 o con Microsoft Lync Server, è necessario consentire un solo gateway IP di messaggistica unificata per effettuare chiamate in uscita per gli utenti e disabilitare le chiamate in uscita su tutti gli altri gateway IP di messaggistica unificata associati ai dial plan URI SIP. Utilizzare Shell o EAC per disabilitare le chiamate in uscita.

Quando si seleziona il gateway IP di messaggistica unificata attraverso il quale consentire le chiamate in uscita per le distribuzioni ibride e locali, è consigliabile scegliere quello che probabilmente gestirà la maggior parte del traffico. Non consentire il traffico in uscita attraverso un gateway IP di messaggistica unificata che si connette a un pool di Lync Server Director. Questa scelta è necessaria per garantire che le chiamate in uscita agli utenti esterni effettuate da un server Cassette postali con il servizio Messaggistica unificata di Microsoft Exchange (ad esempio negli scenari Ascolta al telefono) attraversino in maniera affidabile il firewall aziendale.


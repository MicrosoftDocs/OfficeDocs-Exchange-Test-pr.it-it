---
title: 'Integrazione telefono con messaggistica unificata: Exchange 2013 Help'
TOCTitle: Integrazione del telefono sistema con la messaggistica UNIFICATA
ms:assetid: b8790117-b040-4c84-9d34-005c75088e76
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673558(v=EXCHG.150)
ms:contentKeyID: 50555671
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Integrazione del telefono sistema con la messaggistica UNIFICATA

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Per distribuire in modo corretto la messaggistica unificata, è necessario avere una buona conoscenza delle nozioni fondamentali e dei componenti della telefonia. Una volta compresi i concetti fondamentali, è possibile integrare la messaggistica unificata in un'organizzazione di Exchange. I concetti e i componenti di base comprendono:

  - Reti a commutazione di circuito e a commutazione di pacchetto

  - Centralino (PBX, Private Branch eXchange)

  - IP PBX

  - Voice over Internet Protocol (VoIP)

  - Gateway VoIP

In un ambiente locale, ibrido o Office 365, la connessione e configurazione dei componenti di telefonia necessari rappresentano il passaggio più complesso e importante per la corretta distribuzione della messaggistica unificata, con o senza Lync Server Enterprise Voice. Sarà necessario connettere e configurare i gateway VoIP, i gateway VoIP avanzati, i PBX, gli IP PBX e gli SBC per una rete di telefonia tradizionale ed eseguire la connessione a una rete di telefonia se verranno utilizzati Microsoft Lync Server e la messaggistica unificata.

La pianificazione e l'implementazione di una nuova distribuzione della messaggistica unificata o l'aggiornamento di un sistema di caselle vocali legacy possono comportare alcune sfide per le organizzazioni. È necessaria una conoscenza approfondita dei gateway VoIP, dei PBX, degli IP PBX, di Microsoft Lync Server e della messaggistica unificata. A seconda dell'esperienza tecnica con Exchange e i sistemi di segreteria telefonica, è possibile voler ottenere l'assistenza di uno specialista nella messaggistica unificata. Uno specialista nella messaggistica unificata di Exchange garantisce la transizione agevole da un sistema di segreteria telefonica legacy o di terze parti alla messaggistica unificata di Exchange. Per ulteriori informazioni su come contattare uno specialista della messaggistica unificata, vedere [Specialisti della messaggistica unificata di Microsoft Exchange Server 2013](http://go.microsoft.com/fwlink/p/?linkid=262708).

## Integrazione della rete di telefonia

La messaggistica unificata richiede di integrare la distribuzione di Exchange Server con la rete di telefonia esistente o la messaggistica unificata con Microsoft Lync Server per l'organizzazione. Per una gestione e una distribuzione corrette del sistema di caselle vocali di messaggistica unificata è necessario eseguire un'analisi accurata dell'infrastruttura di telefonia esistente o della distribuzione di Microsoft Lync Server Enterprise Voice e completare i passaggi di pianificazione opportuni.

## Gateway VoIP

Quando si distribuisce la messaggistica unificata in un'organizzazione di Exchange, è necessario installare, distribuire e configurare uno o più gateway VoIP per la connessione a PBX nella rete di telefonia oppure installare, distribuire e configurare i PBX abilitati a SIP o gli IP PBX.

Un gateway VoIP è un dispositivo hardware di terze parti che connette un PBX legacy alla rete LAN. Il gateway VoIP consente al sistema PBX di comunicare con i server Exchange dell'organizzazione.

La messaggistica unificata si basa sulle capacità del gateway VoIP di tradurre o convertire i TDM o i protocolli basati sulla commutazione dei circuiti come ISDN e QSIG da un sistema PBX ai protocolli basati su VoIP o IP, quali SIP (Session Initiated Protocol), RTP (Realtime Transport Protocol) o T.38 per trasmissioni fax in tempo reale. Il gateway VoIP è parte integrante della funzionalità e dell'operatività della messaggistica unificata. Il gateway VoIP può inoltre connettersi ai sistemi PBX che utilizzano il VoIP anziché i protocolli a commutazione di circuiti PSTN.

La scelta del gateway VoIP, dell'IP-PBX, del PBX abilitato a SIP o dell'SBC corretto è solo il primo passo nell'integrazione della rete di telefonia con la messaggistica unificata. È necessario configurare tali dispositivi per il funzionamento con la messaggistica unificata. Sia nelle distribuzioni locali che in quelle ibride è necessario distribuire i server Accesso client e Cassette postali richiesti e creare e configurare tutti i componenti necessari di messaggistica unificata. Per Office 365 con posta vocale ospitata, non è necessario installare e configurare alcun server. I componenti consentono di stabilire la connessione tra la propria rete di telefonia a commutazione di circuito e la rete dati IP nonché di abilitare la posta vocale per gli utenti dell'organizzazione. Per informazioni dettagliate e per conoscere i dispositivi di telefonia supportati, vedere le seguenti risorse:

  - [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

  - [Note di configurazione per i gateway VoIP, IP PBX e PBX supportati](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Note di configurazione per session border controller supportati](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

## Microsoft Lync Server

La messaggistica unificata può utilizzare Microsoft Lync Server per combinare funzionalità di messaggistica vocale, messaggistica immediata, presenza avanzata, conferenza audio/video e posta elettronica in un ambiente di comunicazione integrato e intuitivo. Offrire agli utenti dell'organizzazione le funzionalità Enterprise Voice integrando la messaggistica unificata e Microsoft Lync Server comporta i vantaggi seguenti:

  - Notifiche di presenza avanzate, disponibili per numerose applicazioni, che consentono di informare gli utenti sulla disponibilità dei contatti.

  - Integrazione di messaggistica immediata, messaggistica vocale, conferenze, posta elettronica e altri metodi di comunicazione che consentono agli utenti di selezionare la modalità più appropriata alle loro attività. Gli utenti hanno inoltre la possibilità di passare da una modalità all'altra.

  - Disponibilità di metodi di comunicazione alternativi da qualsiasi postazione dotata di una connessione Internet.

  - Un client intelligente (Microsoft Lync) per telefonia, messaggistica istantanea e conferenze.

  - Modalità di utilizzo coerenti tra dispositivi diversi.

Il componente di routing della messaggistica unificata di Exchange gestisce il routing della posta vocale tra Lync Server e i server Exchange ai fini dell'integrazione tra Lync Server con le funzionalità di messaggistica unificata. Il componente di routing di messaggistica unificata di Exchange presente in Lync Server gestisce inoltre il reindirizzamento della posta vocale sulla rete PSTN se i server Exchange non sono disponibili. Se Enterprise Voice è distribuito nei siti delle filiali e tali siti non dispongono di un collegamento WAN resiliente a un sito centrale, un Survivable Branch Appliance che si distribuisce nel sito della filiale fornisce la posta vocale agli utenti della filiale in caso di interruzione di un collegamento WAN. Quando il collegamento WAN non è disponibile, Survivable Branch Appliance effettua le operazioni seguenti:

  - Reindirizza le chiamate senza risposta sulla rete PSTN a un server Cassette postali di Exchange nel sito centrale.

  - Fornisce all'utente la possibilità di recuperare i messaggi vocali sulla rete PSTN.

  - Mette in coda le notifiche delle chiamate perse, quindi le carica nel server Exchange quando viene ripristinato il collegamento WAN.

Per ulteriori informazioni su Microsoft Lync Server, vedere [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).


> [!WARNING]
> Durante l'integrazione della messaggistica unificata con Lync Server in una distribuzione locale o ibrida, le notifiche di chiamata senza risposta non sono disponibili per gli utenti la cui cassetta postale si trova su un server Cassette postali di Exchange 2007 o Exchange 2010. Una notifica di chiamata senza risposta viene generata quando un utente effettua la disconnessione prima che la chiamata sia inviata a un server Cassette postali.



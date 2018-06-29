---
title: 'Configurazioni PBX e IP-PBX: Exchange 2013 Help'
TOCTitle: Configurazioni PBX e IP-PBX
ms:assetid: fb086680-6e3e-477a-a5d8-e24ca30196ee
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb430797(v=EXCHG.150)
ms:contentKeyID: 54652894
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazioni PBX e IP-PBX

 

_**Si applica a:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

Sempre più spesso, le organizzazioni effettuano l'acquisto, l'installazione e la manutenzione di componenti hardware quali PBX (Private Branch eXchange) o IP PBX, necessari per il supporto dei propri sistemi di telefonia. Molte organizzazioni acquistano apparecchiature telefoniche e formano il personale internamente per ridurre le spese associate alla manutenzione dei sistemi di telefonia e per esercitare un più stretto controllo sulle funzionalità di telefonia disponibili all'interno di tali sistemi.

Affinché un'organizzazione sia in grado di possedere ed eseguire la manutenzione della propria rete telefonica, è necessario che vengano acquistati i componenti hardware di telefonia adeguati. È altresì necessario tenere presente l'esigenza di una manutenzione quotidiana delle apparecchiature telefoniche e di una formazione adeguata del personale di supporto del sistema di telefonia. In questo argomento vengono illustrati i diversi tipi di telefonia aziendale o di sistemi organizzativi e i componenti hardware di telefonia richiesti. L'argomento offre inoltre esempi di diversi tipi di configurazioni di telefonia.


> [!IMPORTANT]
> È consigliabile che tutti i clienti che prevedono di distribuire Microsoft Exchange 2013 la messaggistica unificata ottenere l'aiuto di un esperto di messaggistica UNIFICATA. In modo da garantire un aggiornamento senza problemi da un sistema di caselle vocali legacy. Distribuzione una nuova distribuzione di messaggistica UNIFICATA o l'esecuzione di un aggiornamento di un sistema di posta vocale richiede la conoscenza significativo su PBX, IP PBX e la messaggistica unificata. Per ulteriori informazioni su chi contattare, vedere il sito Web <A href="https://go.microsoft.com/fwlink/p/?linkid=261951">Microsoft individuare</A>.



**Sommario**

Overview of Telephony Systems

Legacy and Traditional PBX Configurations

IP PBX Configurations

Calling or Called Party Identification

## Informazioni generali sui sistemi di telefonia

Nelle reti a commutazioni di circuiti, ad esempio la rete PSTN (Public Switched Telephone Network), vengono trasmesse più chiamate attraverso lo stesso supporto di trasmissione. Nella rete PSTN il supporto utilizzato è spesso il rame. Tuttavia, è possibile utilizzare anche cavi in fibra ottica.

Una rete a commutazione di circuiti è una rete in cui esiste una connessione dedicata, ovvero un circuito o canale che viene impostato tra due nodi in modo che possano comunicare. Una volta stabilita una chiamata tra due nodi, la connessione può essere utilizzata solo da questi due nodi. Quando la chiamata viene terminata da uno dei nodi, la connessione viene annullata.

Esistono diversi tipi e categorie di sistemi di telefonia utilizzati all'interno di aziende e organizzazioni che sono in grado di ospitare una rete basata su circuito o su IP, o entrambe. Ciascuna tipologia presenta vantaggi e svantaggi che vanno tenuti in considerazione durante la pianificazione e l'implementazione di un sistema di telefonia.

  - **Centrex:**Centrex appartiene a una tipologia di servizi di telefonia che le compagnie telefoniche concedono in locazione alle aziende e alle organizzazioni. Un sistema di telefonia Centrex tradizionale elimina la necessità, per aziende e organizzazioni, di acquistare i componenti hardware di telefonia da utilizzare in sede per il supporto del sistema di telefonia dell'organizzazione. Generalmente i sistemi Centrex vengono utilizzati da piccole aziende che prendono a nolo i servizi Centrex da una compagnia telefonica su base mensile e per ciascuna linea. I sistemi di telefonia Centrex sono utilizzati, talvolta, anche da organizzazioni più grandi, ma sono presenti più di frequente in organizzazioni governative, pubbliche e private. Nei sistemi Centrex vengono spesso utilizzate linee telefoniche analogiche per il collegamento con l'azienda o l'organizzazione. Talvolta vengono utilizzati, tuttavia, anche circuiti T1 con un demultiplexer in sede per il supporto di telefoni analogici o digitali o di linee ISDN.
    
    In un sistema di telefonia basato su Centrex, la sede centrale della compagnia telefonica agisce da luogo di interscambio telefonico. Tale sistema è progettato specificamente per supportare i bisogni di una determinata organizzazione. L'ufficio telefonico centrale esegue l'instradamento delle chiamate originate all'interno dell'azienda verso il relativo numero di telefono interno o esterno. Nei sistemi Centrex, la sede centrale della compagnia telefonica viene utilizzata come luogo di interscambio per l'instradamento delle chiamate interne verso un determinato numero di interno. Con Centrex, ad esempio, il sistema di interscambio telefonico o la sede centrale della compagnia telefonica è in grado di distinguere le chiamate interne. I dipendenti appartenenti alla rete telefonica dell'organizzazione, pertanto, possono chiamare un altro dipendente all'interno della stessa rete o dello stesso dial plan digitando un numero di interno di quattro cifre. Quando viene composto un numero di telefono interno, la chiamata viene inoltrata alla sede centrale della compagnia telefonica e quindi instradata nuovamente verso il numero di interno che ha avviato la chiamata.

Una variante del sistema di telefonia Centrex tradizionale è denominata *IP Centrex*. In un sistema di telefonia IP Centrex, la chiamata viene inviata attraverso un gateway VoIP (Voice over IP) situato presso la sede centrale della compagnia telefonica o presso la sede di un provider di servizi. In questo tipo di sistemi di telefonia, il gateway VoIP converte la chiamata in pacchetti di dati basati su IP da inviare attraverso Internet o attraverso una rete basata su un sistema VoIP. Tuttavia, se la chiamata viene inviata attraverso Internet, generalmente è presente un altro gateway VoIP che riceve la chiamata convertendola poi nuovamente in una tradizionale chiamata a commutazione di circuito.

Le organizzazioni che dispongono attualmente di un sistema di telefonia Centrex tradizionale devono installare, distribuire e mantenere uno o più gateway VoIP per consentire il corretto funzionamento della messaggistica unificata. Nei sistemi IP Centrex, la messaggistica unificata potrebbe richiedere l'installazione, la distribuzione e la manutenzione di gateway VoIP. Diverse variabili sono da tenere in considerazione nel determinare la necessità di disporre di un gateway VoIP. Tali variabili includono la tipologia di telefoni utilizzati all'interno dell'organizzazione (analogici, digitali o IP) e i protocolli supportati dal sistema IP Centrex.

  - **Key telephone:** in un sistema Key telephone, la sede centrale della compagnia telefonica è collegata all'organizzazione mediante linee telefoniche standard, analogiche o digitali. Un unico numero di interno è collegato a più telefoni in modo tale che, quando si utilizza tale numero per effettuare una chiamata verso l'organizzazione, tutti i telefoni associati a quella linea o interno squillino contemporaneamente.

Con i sistemi Key telephone, le linee telefoniche vengono condivise da più utenti. I chiamanti, pertanto, non ascolteranno spesso segnali di occupato nei tentativi di chiamata all'organizzazione. I sistemi di telefonia Key telephone vengono utilizzati nelle piccole aziende, dove il volume di chiamate interne è consistente, mentre quello delle chiamate esterne è ridotto.

I sistemi di telefonia Key telephone hanno raggiunto un discreto livello di ricercatezza nel tempo e possono essere utilizzati con la messaggistica unificata se viene aggiunto un gateway VoIP. Alcuni sistemi meno sofisticati, tuttavia, potrebbero non funzionare correttamente anche se viene utilizzato un gateway VoIP supportato.

  - **PBX:** un sistema PBX legacy è un dispositivo telefonico in grado di passare chiamate all'interno di una rete di telefonia o a commutazione di circuito. Un sistema PBX legacy è un PBX che non dispone di un adattatore di rete e che non è in grado di trasmettere i pacchetti IP. Poiché tali sistemi non sono in grado di trasmettere pacchetti IP, alcune aziende e organizzazioni hanno scelto di sostituire i sistemi PBX legacy con sistemi IP PBX. Per un elenco di PBX supportati dalla messaggistica unificata, vedere [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).
    
    I sistemi PBX vengono utilizzati dalla maggior parte delle aziende di grandi e medie dimensioni. Il sistema PBX consente agli utenti o ai sottoscrittori di condividere un determinato numero di linee esterne per effettuare chiamate telefoniche considerate esterne al sistema PBX. È una soluzione che risulta molto meno dispendiosa che fornire a ciascun utente dell'azienda una linea telefonica esterna dedicata. È possibile collegare al sistema PBX sia gli apparecchi telefonici sia fax, modem e molti altri dispositivi di comunicazione.
    
    L'apparecchiatura PBX viene in genere installata nelle sedi dell'organizzazione e consente di collegare le chiamate tra i telefoni situati all'interno dell'azienda e la compagnia telefonica. È in genere disponibile un numero limitato di linee esterne, note anche come linee a lunga distanza, per effettuare e ricevere chiamate esterne all'azienda da un'origine esterna, ad esempio la rete PSTN.
    
    Per poter utilizzare un sistema PBX legacy con la messaggistica unificata, è necessario distribuire un gateway VoIP supportato. Per un elenco dei gateway VoIP supportati, vedere [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

  - **IP PBX:** Un sistema IP PBX è un sistema PBX che dispone di una scheda di rete che supporta il protocollo IP. È un dispositivo di commutazione telefonica generalmente collocato all'interno di un'organizzazione o di un'azienda, anziché presso la sede della compagnia telefonica. Esistono due tipi di sistemi IP PBX: i sistemi IP PBX tradizionali e i sistemi IP PBX ibridi. Sia la versione tradizionale che quella ibrida dei sistemi IP PBX supportano il protocollo IP per l'invio di conversazioni vocali in pacchetti ai telefoni basati sul sistema VoIP. I sistemi IP PBX ibridi, tuttavia, sono in grado di collegare anche i telefoni analogici tradizionali e quelli digitali.
    
    I sistemi IP PBX sono spesso più semplici da amministrare dei PBX legacy, poiché gli amministratori possono configurare facilmente i servizi IP PBX utilizzando un browser Internet o un altro strumento basato su IP. Inoltre, non è necessario installare ulteriori cavi o pannelli. I sistemi IP PBX consentono di spostare un apparecchio telefonico basato su IP scollegando semplicemente il telefono e collegandolo nuovamente in un'altra postazione, evitando così le dispendiose chiamate necessarie a disdire il contratto con la compagnia telefonica fornitrice del sistema PBX legacy. Le organizzazioni che utilizzano sistemi IP PBX, inoltre, non sono costrette a sostenere ulteriori spese per l'infrastruttura, necessarie per la manutenzione e la gestione di reti a commutazione di circuito e commutazione di pacchetto separate. Per un elenco di IP PBX supportati per la messaggistica unificata, vedere [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).
    
    Inizio pagina

## Configurazioni di un sistema PBX legacy e tradizionale

Nelle reti di telefonia con sistema PBX legacy o tradizionale, il PBX consente di eseguire le operazioni seguenti:

  - Creazione delle connessioni o dei circuiti tra apparecchi telefonici di utenti diversi.

  - Mantenimento della connessione per il tempo necessario agli utenti.

  - Erogazione di informazioni di carattere amministrativo (ad esempio, il numero di scatti per ciascuna chiamata).

Oltre alle tre funzioni riportate nell'elenco, i sistemi PBX sono in grado di offrire ulteriori funzionalità di chiamata, ad esempio:

  - Operatori automatici

  - Dettagli chiamata

  - Accettazione chiamata

  - Trasferimento di chiamata

  - Avviso di chiamata

  - Chiamata in conferenza

  - Composizione diretta interni (DID, Direct Inward Dialing)

  - Blocco chiamate in arrivo (DND, Do Not Disturb)

Benché esistano diverse aziende produttrici di sistemi PBX, è possibile distinguere tra due categorie principali: analogico e digitale. Questi sistemi PBX sono noti anche come PBX *legacy* o *tradizionali*.

Generalmente i sistemi PBX sono collegati alla sede centrale della compagnia telefonica mediante linee telefoniche speciali, denominate linee T1 ed E1. Le linee T1 ed E1 dispongono di più canali. Tali linee telefoniche sono note anche come *linee a lunga distanza*. Consentono alla sede centrale o al sistema PBX di inviare più chiamate sulla stessa linea per una maggiore efficienza, grazie all'utilizzo di un layout dei cavi semplificato. I sistemi PBX possono essere utilizzati con linee analogiche o ISDN.

Configurando adeguatamente il sistema PBX, è possibile stabilire la quantità di canali o di linee da configurare per la ricezione di chiamate esterne e la quantità di canali o linee da dedicare alle chiamate provenienti dall'interno dell'organizzazione. La configurazione di un numero di canali o di linee appropriato consente di prevenire frequenti segnali di occupato e di determinare la quantità di canali o di linee da dedicare ad applicazioni come i call center. La corretta configurazione del sistema PBX rappresenta un metodo efficace per la gestione dei canali o delle linee all'interno dell'organizzazione, poiché consente di ridurre il numero delle linee dedicate.

I sistemi PBX sono in grado di instradare il numero di telefono composto verso un apparecchio telefonico specifico, in modo che gli utenti possano disporre di un proprio numero di telefono o di interno. Tale funzionalità è denominata numero di Composizione diretta interni (DID). Quando viene composto il numero di telefono di un utente, la compagnia telefonica invia il numero DID al sistema PBX mediante il servizio di identificazione del numero composto (DNIS, Dialed Number Identification Service). Grazie al servizio DNIS utilizzato dalla compagnia telefonica per inviare il numero, non è necessario l'intervento di un operatore per instradare la chiamata. Il sistema PBX dispone delle informazioni sulla chiamata necessarie per il corretto invio al numero composto dal chiamante. Per un elenco di PBX supportati dalla messaggistica unificata, vedere [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

Inizio pagina

## PBX analogici e digitali

I sistemi PBX analogici inviano informazioni vocali e di segnalazione chiamata, come le composizioni a toni del numero di telefono composto, sotto forma di suono analogico. Il suono, pertanto, non viene mai digitalizzato. Per indirizzare correttamente una chiamata, è necessario che il PBX o la sede centrale della compagnia telefonica dispongano delle informazioni di segnalazione necessarie.


> [!NOTE]
> La composizione a toni è nota agli esperti come segnale multifrequenza (DTMF). Quando il chiamante preme un tasto sul tastierino numerico del telefono, l'apparecchio produce due segnali acustici distinti: un segnale ad alta frequenza e uno a bassa frequenza. Durante una conversazione telefonica, viene emesso un tono di frequenza singolo. L'invio contemporaneo di due segnali acustici con frequenze diverse riduce l'eventualità che i segnali acustici vengano interpretati come voce umana o che la voce umana venga interpretata come segnale acustico.



I sistemi PBX digitali codificano il suono analogico in formato digitale, ovvero lo digitalizzano. Generalmente, i sistemi digitali PBX codificano i suoni vocali utilizzando un codec audio secondo gli standard di settore, come G.711 o G.729. Una volta codificato in formato digitale, il segnale vocale viene inviato attraverso un canale mediante la commutazione di circuito. Viene così impostata una connessione aperta end-to-end che lascia aperto il canale ad uso esclusivo dell'utente per l'intera durata della chiamata. Il metodo di segnalazione utilizzato dal PBX dipende, tuttavia, dal produttore. Il metodo di segnalazione per l'impostazione delle chiamate può avere caratteristiche diverse a seconda del produttore.


> [!NOTE]
> I sistemi digitali PBX supportano linee a lunga distanza sia analogiche che digitali.



Nelle organizzazioni più grandi, i sistemi PBX consentono ai dipendenti di comunicare tra loro da posizioni fisiche diverse componendo semplicemente il numero di interno dell'utente corrispondente. A tale scopo, è possibile utilizzare un singolo sistema PBX o più sistemi PBX collegati in rete. È possibile collegare i sistemi PBX dislocati in postazioni diverse a un'unica rete a commutazione di circuito trasparente utilizzando linee T1 o E1. Quando tali linee eseguono il collegamento tra più sistemi PBX, vengono spesso denominate *linee connodali*. I sistemi PBX comunicano tra loro attraverso le linee connodali utilizzando un protocollo da PBX a PBX, come QSIG. Il protocollo QSIG fa sì che una serie di sistemi PBX si comportino come un singolo sistema PBX.

Questo tipo di ambiente PBX può comprendere anche funzionalità avanzate, come il trasferimento delle chiamate e la conferenza telefonica. Oltre a consentire l'utilizzo di funzionalità avanzate, il collegamento di due sistemi PBX comporta una riduzione dei costi per l'organizzazione, eliminando le spese per le chiamate a lunga distanza tra dipendenti dislocati in sedi diverse. Questo perché una chiamata tra dipendenti rimane su una linea connodale che collega più sistemi PBX e all'utente viene richiesto soltanto di comporre il numero di interno di un altro utente, anziché effettuare una chiamata a lunga distanza.

In un ambiente di telefonia che comprende uno o più sistemi PBX analogici, la presenza di un gateway VoIP tra il sistema PBX e i server Accesso client e Cassette postali di Exchange 2013 è necessaria per convertire i protocolli basati su circuito presenti in una rete di telefonia in protocolli basati su IP presenti in una rete di dati. Per ulteriori informazioni sui gateway VoIP, vedere i seguenti argomenti:

  - [Gateway IP di messaggistica unificata](um-ip-gateways-exchange-2013-help.md)

  - [Connettere un gateway VoIP per comunicare con un PBX](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md)

Per un elenco di gateway VoIP supportati per la messaggistica unificata, vedere [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

Inizio pagina

## Configurazione degli IP PBX

Un sistema IP PBX è un PBX che supporta il protocollo IP per connettere i telefoni mediante una rete LAN Ethernet o a commutazione di pacchetto e invia conversazioni vocali in pacchetti IP o di dati. Un sistema IP PBX può avere più interfacce, tra cui interfacce per una rete di dati e altre che consentono la connessione a una rete di telefonia o a commutazione di circuito.

Lo sviluppo di protocolli Internet in tempo reale ha reso possibile l'invio di messaggi fax e vocali attraverso una rete di dati. Tali protocolli Internet comprendono i protocolli VoIP utilizzati nella messaggistica unificata: SIP (Session Initiation Protocol) su TCP (Transmission Control Protocol) per la messaggistica vocale. Tali protocolli hanno reso possibile l'invio di messaggi fax e vocali attraverso una rete di dati. I protocolli VoIP in tempo reale sono necessari per inviare messaggi vocali attraverso una rete di dati o a commutazione di pacchetto mantenendo e controllando l'ordine temporale e di recapito dei pacchetti di dati. Se tali protocolli per il controllo e il mantenimento dell'ordine temporale e di recapito di pacchetti di dati non venissero utilizzati, la voce di una persona risulterebbe interrotta e poco comprensibile e le immagini non verrebbero visualizzate correttamente. Per un elenco di IP PBX supportati per la messaggistica unificata, vedere [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).


> [!NOTE]
> La messaggistica unificata supporta solo il protocollo SIP su TCP.



## Configurazioni di un sistema IP PBX tradizionale

Un sistema IP PBX standard o tradizionale contiene almeno un'interfaccia di rete collegata a una rete di dati mediante protocolli VoIP. Può contenere anche ulteriori interfacce di rete o altre interfacce di telefonia che abilitano il collegamento con una rete di telefonia esistente, come la rete PSTN. Il collegamento alla rete di dati consente la comunicazione con altri host VoIP collocati sulla rete di dati mediante l'utilizzo di pacchetti di dati IP. Tali host VoIP includono altri IP PBX, telefoni basati su VoIP, gateway VoIP e server Accesso client e Cassette postali in cui sono in esecuzione servizi di messaggistica unificata. I sistemi IP PBX tradizionali non supportano telefoni analogici o digitali, ma soltanto telefoni VoIP.

Poiché i sistemi IP PBX sono già in grado di effettuare il collegamento con una rete di dati e di convertire i protocolli basati su circuito della rete PSTN in protocolli VoIP a commutazione di pacchetto, l'utilizzo di un gateway VoIP potrebbe non essere necessario per abilitare la comunicazione con i server Accesso client e Cassette postali sulla rete di dati.

## Configurazioni IP PBX ibride

I sistemi IP PBX ibridi dispongono di funzionalità analogiche, digitali e basate su VoIP. Un sistema IP PBX in cui sono installate determinate interfacce e un software che supporta diversi tipi di interfacce viene considerato un sistema IP PBX ibrido. In un sistema IP PBX ibrido è possibile utilizzare diversi tipi di telefoni: analogici, digitali o basati su IP.

La maggior parte dei sistemi IP PBX supporta e fornisce tutti e tre i tipi di comunicazione vocale ed è possibile aggiornare un sistema IP PBX tradizionale a un sistema IP PBX ibrido installando le interfacce e gli aggiornamenti del software o del firmware necessari.

L'utilizzo congiunto di telefoni analogici, digitali e basati su IP consente agli utenti dell'organizzazione di accedere a nuove funzionalità e garantisce la massima flessibilità in un ambiente di telefonia. I sistemi IP PBX ibridi consentono inoltre una transizione graduale verso un ambiente di telefonia e un sistema di messaggi vocali interamente basati su VoIP per l'organizzazione.

Diversi fattori determinano se un gateway VoIP sarà necessario in caso di connessione ai server Accesso client e Cassette postali. Uno di questi è la compatibilità dei protocolli VoIP utilizzati dal sistema IP PBX o IP PBX ibrido e dalla messaggistica unificata. La mancata necessità di un gateway VoIP comporta una semplificazione dell'infrastruttura di telefonia e una riduzione del supporto necessario per la messaggistica unificata.

Inizio pagina

## Identificazione della parte chiamante o chiamata

L'identificazione della parte chiamante o chiamata è un servizio offerto dalle compagnie telefoniche che consente a chi riceve una chiamata di visualizzare il numero di telefono e talvolta il nome del chiamante, nonché altre informazioni sulla chiamata. Queste informazioni vengono inviate attraverso un cavo seriale utilizzando la segnalazione della chiamata. Quando un sistema PBX o IP PBX riceve una chiamata da una compagnia telefonica, la chiamata è accompagnata dalle seguenti informazioni identificative:

  - Numero della parte chiamante

  - Numero della parte chiamata

  - Codici di stato (ad esempio chiamata senza risposta), lo stato e condizione della linea (ad esempio linea occupata) e inoltro delle chiamate attivato

  - Numero della linea o della porta utilizzata per la chiamata

  - In telefonia, le informazioni di segnalazione vengono utilizzate per lo scambio di informazioni tra gli endpoint di una rete per configurare, controllare e terminare le chiamate. Diversi metodi di segnalazione utilizzati dai gateway VoIP e dai sistemi IP PBX sono supportati nella messaggistica unificata. Il metodo di segnalazione utilizzato dipende dal tipo di dispositivo e dal metodo di segnalazione in uso nella compagnia telefonica. La condizione più importante è che il dispositivo che consente il collegamento con la compagnia telefonica e con il gateway VoIP o IP PBX supporti almeno uno dei metodi di segnalazione che permettono agli utenti di inviare e ricevere informazioni relative alla parte chiamante o chiamata. Per ulteriori informazioni sulle informazioni di configurazione della segnalazione per un gateway VoIP supportato, vedere [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

Benché sia possibile utilizzare altri metodi di segnalazione, i due metodi più comuni sono i seguenti:

  - **Simplified Message Desk Interface (SMDI):** Il protocollo SMDI viene utilizzato per lo scambio di informazioni di segnalazione, di controllo e di identificazione della chiamata in un'interfaccia tra un sistema di telefonia e un sistema di caselle vocali e consente la trasmissione delle informazioni necessarie per l'elaborazione delle chiamate in ingresso nel sistema di caselle vocali. Ogni volta che una chiamata in arrivo viene inviata attraverso un'interfaccia seriale o RS-232 mediante il protocollo SMDI, le informazioni trasmesse identificano la linea o porta, il tipo di chiamata e i numeri di telefono della parte chiamante o chiamata. Il cavo SMDI consente il collegamento tra un dispositivo come un sistema PBX e una connessione seriale sul gateway VoIP. Il protocollo SMDI è utilizzato, tuttavia, anche con i sistemi IP PBX. Il protocollo SMDI consente un massimo di 10 cifre per ciascun numero chiamante o chiamato. Questa limitazione è propria del protocollo e non può essere modificata.

  - **In-Band:**   la segnalazione In-Band consente la trasmissione di informazioni relative a segnalazione, controllo chiamata e identificazione chiamata da parte della compagnia telefonica. Tali informazioni vengono inviate sullo stesso canale e sulla stessa banda (da 300 Hz a 3,4 kHz) della voce e di altri suoni prodotti durante la chiamata. Ad esempio, quando un utente effettua una chiamata utilizzando DTMF o la composizione a toni e inizia una conversazione con la parte chiamata, il segnale a toni e quello vocale utilizzano lo stesso canale e la stessa banda. La segnalazione In-Band è meno sicura poiché i segnali di controllo sono esposti all'utente; questo metodo di segnalazione è meno diffuso rispetto a SMDI. La segnalazione In-Band si applica solo alla segnalazione associata al canale (CAS, Channel Associated Signaling).

Inizio pagina


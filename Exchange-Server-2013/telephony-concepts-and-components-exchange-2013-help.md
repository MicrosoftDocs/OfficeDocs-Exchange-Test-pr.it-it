---
title: 'Componenti e concetti di telefonia: Exchange 2013 Help'
TOCTitle: Componenti e concetti di telefonia
ms:assetid: ce70bf6a-db85-411b-8b93-2987703963a9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124606(v=EXCHG.150)
ms:contentKeyID: 54652884
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Componenti e concetti di telefonia

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-04-25_

Se si sta pianificazione e distribuzione MicrosoftExchange 2013 della messaggistica unificata (UM) in rete, è necessario comprendere le reti di messaggistica unificata e telefonia. In questo argomento viene fornita una panoramica della telefonia concetti dell'infrastruttura e i componenti che consentono di piano e distribuire server che eseguono Exchange 2013 la messaggistica unificata.

**Sommario**

Panoramica

Concetti e componenti

Reti a commutazione di circuito

Reti a commutazione di pacchetto

PBX

IP PBX

PBX abilitato SIP

VoIP

Gateway IP

## Panoramica

Nelle versioni di Microsoft Exchange prima Exchange Server 2007, responsabilità principale dell'amministratore Exchange è stato gestione dei messaggi di posta elettronica e, in alcuni casi, gestione di un'infrastruttura di rete. Le versioni precedenti di Exchange non dispongono delle funzionalità di messaggistica unificata. gli amministratori di Exchange Server versione 5.5, Exchange 2000 Server e Exchange Server 2003 sono disponibili per l'ambiente Exchange e l'infrastruttura di rete e fortemente utilizzavano consulenti di telefonia per gestire l'ambiente di telefonia e dell'infrastruttura.

## Concetti e componenti

Per distribuire correttamente la messaggistica unificata in Exchange 2013, è necessario disporre di una buona conoscenza dei concetti di base di telefonia e componenti di telefonia. Una volta ottenuto una buona conoscenza generale di telefonia, è possibile integrare correttamente Exchange 2013 la messaggistica unificata nell'organizzazione di Exchange 2013. Concetti di base e i componenti includono quanto segue:

  - Reti a commutazione di circuito e a commutazione di pacchetto

  - Centralino (PBX, Private Branch eXchange)

  - IP PBX

  - Voice over Internet Protocol (VoIP)

  - Gateway VoIP

## Reti a commutazione di circuito

Nelle reti a commutazione di circuito, ad esempio il telefono rete PSTN (Public Switched), più chiamate vengono trasmessi mezzo di trasmissione stesso. Di solito, il supporto utilizzato nella rete PSTN è rame. Tuttavia, cavo in fibra ottica inoltre può essere utilizzato.

Una rete a commutazione di circuito è una rete in cui è disponibile una connessione dedicata. Una connessione dedicata è un canale impostare tra due nodi in modo che possano comunicare o a commutazione di circuito. Dopo avere stabilita una chiamata tra due nodi, la connessione può essere utilizzata solo per questi due nodi. Quando la chiamata viene terminata da uno dei nodi, la connessione è stata annullata.


> [!NOTE]
> La rete PSTN è il raggruppamento delle reti telefoniche a commutazione di circuiti pubbliche nel mondo, allo stesso modo in cui Internet è il raggruppamento delle reti pubbliche nel mondo a commutazione di pacchetti basati su IP.



Esistono due tipi di reti a commutazione di base: analogici e digitali. Analogico è stato progettato per la trasmissione vocale. Da molti anni, la rete PSTN era solo analogiche, ma oggi sono diventate reti a commutazione di circuito, ad esempio la rete PSTN da analogico a digitale. Per supportare una voce analogica trasmissione del segnale in una rete digitale il segnale analogico trasmissione deve essere codificato o convertito in formato digitale prima di telefonia WAN. Sul lato ricevente della connessione, è necessario decodificato segnale digitale o riconvertito in un formato segnale analogico.

Esistono vantaggi e svantaggi per reti a commutazione di circuito. Reti a commutazione di circuito sono diversi svantaggi. Reti a commutazione di circuito possono essere relativamente efficace, in quanto può essere utilizzato inutilmente della larghezza di banda. Quando si utilizza una rete a commutazione di pacchetto VoIP, non è il caso. VoIP condivide larghezza di banda disponibile con tutte le altre applicazioni di rete e utilizzo più efficiente della larghezza di banda disponibile. Un altro svantaggio alle reti a commutazione di circuito è necessario prevedere il numero massimo di chiamate telefoniche che saranno necessari per periodi di utilizzo e quindi il pagamento per l'utilizzo a commutazione di circuito o circuiti per supportare il numero massimo di chiamate.

Il passaggio a commutazione di circuito ha un importante vantaggio in reti a commutazione di pacchetto. In una rete a commutazione di circuito, quando si utilizza un circuito, è necessario a commutazione di circuito completo per il periodo di tempo che si sta utilizzando a commutazione di circuito senza concorrenza da altri utenti. Questo non è il caso con reti a commutazione di pacchetto.


> [!NOTE]
> Gerarchia digitale sincrono (SDH) è diventato il protocollo di trasmissione primario per la maggior parte delle reti PSTN. SDH viene eseguita tramite reti in fibra ottica.



Inizio pagina

## Reti a commutazione di pacchetto

Commutazione di pacchetto è una tecnica che divide un messaggio di dati in unità di misura più piccole chiamato pacchetti. I pacchetti inviati alle rispettive destinazioni, la route ottimale disponibile e quindi vengono riassemblati destinatario.

Nelle reti a commutazione di pacchetto, ad esempio Internet pacchetti vengono instradati al propria destinazione attraverso la route più vantaggioso, ma non tutti i pacchetti in uscita tra due host viaggiano la stessa route, persino quelle provenienti da un singolo messaggio. In questo modo quasi che i pacchetti arriveranno in momenti diversi e ordine. In una rete a commutazione di pacchetto, i pacchetti (messaggi o frammenti dei messaggi) vengono instradati singolarmente tra i nodi attraverso collegamenti di dati che possono essere condivise da altri nodi. A commutazione di pacchetto, a differenza di commutazione di circuito, più le connessioni ai nodi della rete condividono la larghezza di banda disponibile.


> [!NOTE]
> A commutazione di circuito, tutti i pacchetti di accedere al destinatario nell'ordine indicato e su un singolo percorso.



Reti a commutazione di pacchetto sono disponibili per consentire le comunicazioni di dati su Internet in tutto il mondo. Una rete pubblica dati o commutazione di pacchetto è l'equivalente di dati alla rete PSTN.

Reti a commutazione di pacchetto sono disponibili anche in quali ambienti di rete come LAN e WAN. Un ambiente WAN commutazione di pacchetto si basa su circuiti telefono, ma parte del circuito vengono disposte in modo da mantenere una connessione permanente con i rispettivi endpoint. In un ambiente di commutazione di pacchetto LAN, ad esempio con una rete Ethernet la trasmissione di pacchetti di dati si basa su pacchetti switch, router e cavi di rete LAN. In una rete LAN, l'opzione stabilisce una connessione tra due segmenti solo tempo sufficiente per inviare il pacchetto corrente. I pacchetti in ingresso vengono salvati in un'area di memoria temporanea o buffer di memoria. In una LAN Ethernet-based un frame Ethernet contiene la parte del payload o i dati di un'intestazione speciale che include le informazioni di indirizzo media access controllo (MAC) per la destinazione del pacchetto di origine e il pacchetto. Quando i pacchetti giungano a destinazione, vengono inseriti nuovamente nell'ordine indicato dall'assembler pacchetto. È necessario un assembler pacchetti a causa della route diverse che potrebbero richiedere i pacchetti.

Reti a commutazione di pacchetto è stato possibile per Internet sia disponibile e, al contempo, ha reso reti di dati, ovvero reti IP particolarmente Local, ovvero più diffusi e disponibili.

Inizio pagina

## PBX

Un PBX legacy è un dispositivo di telefonia che funge da un'opzione per il passaggio tra le chiamate in reti a commutazione di circuito o telefonia.


> [!NOTE]
> Un PBX legacy è un PBX che non è possibile passare dei pacchetti IP. In molte aziende, sistemi PBX legacy sono state sostituite da IP PBX.



Un sistema PBX è un dispositivo di telefonia utilizzato dalle società più medie dimensioni e dimensioni maggiori. Un sistema PBX consente agli utenti o i sottoscrittori del PBX per condividere un determinato numero di linee esterne per le telefonate considerate esterne al PBX. Un sistema PBX è una soluzione molto meno costosa rispetto agli ogni utente in un'azienda di una linea telefonica esterno dedicato. Set di telefono, inoltre per fax macchine, i modem e molti altri dispositivi di comunicazione, possono essere connessi a un sistema PBX.

Le apparecchiature di PBX viene in genere installata in locale di un'azienda e si connette per le chiamate tra i telefoni Trova e installato nel sito di business. Un numero limitato di linee esterne, noto anche come righe trunk, è in genere disponibile per l'esecuzione e ricezione di chiamate esterne all'azienda da un'origine esterna, ad esempio la rete PSTN.

Chiamate aziendali interne effettuate ai numeri di telefono esterno tramite un PBX vengono eseguite per la composizione di 9 o 0 in alcuni sistemi seguiti dal numero esterno. Per completare la chiamata viene selezionata automaticamente una linea trunk in uscita. Al contrario, le chiamate effettuate tra utenti all'interno dell'azienda non richiedono in genere telefono speciale cifre o per l'utilizzo di una linea esterna di trunk. Ciò avviene perché le chiamate interne vengono instradate o a commutazione dal PBX tra telefoni fisicamente connesso al PBX.

Per le aziende di dimensioni più grandi e medie dimensioni, sono possibili configurazioni PBX seguenti:

  - Un singolo PBX che supporta l'intera azienda.

  - Raggruppamento di due o più sistemi PBX non in rete o connessi tra loro.

  - Un raggruppamento di due o più sistemi PBX connessi contemporaneamente o in rete.


> [!NOTE]
> Un dial plan di messaggistica unificata Exchange 2013 possono estendersi su più di un sistema PBX o IP PBX.



Inizio pagina

## IP PBX

Un PBX IP è un PBX che supporta il protocollo IP per la connessione mediante una LAN Ethernet o commutazione di pacchetto telefoni e invia le conversazioni vocali in pacchetti IP. Una IP PBX ibrida supporta il protocollo IP per inviare le conversazioni vocali nei pacchetti, ma anche si connette analogici e digitali a commutazione di circuito Time Division Multiplex TDM () telefoni tradizionali. Un IP PBX è commutazione apparecchiatura si trova in un'azienda privata anziché compagnia telefonica telefonica.

IP PBX sono spesso più semplice per l'amministrazione di sistemi PBX legacy, in quanto gli amministratori possono configurare facilmente i servizi di PBX IP utilizzando un browser Internet o un'altra utilità basato su IP. Inoltre, non devono essere installati alcun cablaggio aggiuntiva, nel cablaggio o pannelli patch. Con un PBX IP, lo spostamento di un telefono basato su IP è semplice come se si scollega un telefono e collegarlo in una nuova posizione, anziché le chiamate al servizio costose per spostare un telefono da numerosi fornitori PBX legacy. Inoltre, le aziende che possiedono un IP PBX privi i costi di infrastruttura aggiuntiva necessari per mantenere e gestire due separate a commutazione di circuito e reti a commutazione di pacchetto.

## PBX abilitati al SIP

Il PBX abilitato SIP è un dispositivo telefonico che agisce come un commutatore di rete per il passaggio delle chiamate in una rete telefonica o a commutazione di circuiti. Tuttavia, la differenza tra un PBX abilitato SIP e un PBX tradizionale, è che il PBX abilitato SIP può connettersi a Internet utilizzando il protocollo SIP per effettuare chiamate tramite Internet.

PBX abilitati al SIP utilizzare un formato per le chiamate che include un URI SIP contenente un numero e. 164 globale e il "utente = telefono" parametro. Ad esempio: sip:+14255551234@contoso.com;user=phone

Il numero di E164 inizia con l'indicazione "+" e non contiene un parametro di contesto telefonico o qualsiasi separatori. PBX abilitati al SIP supporta sia TCP e UDP. UDP è ancora ampiamente utilizzata con sistemi legacy. PBX abilitati al SIP supportano inoltre Mutual Transport Layer Security (mutual TLS) e le ricerche DNS.

## VoIP

Voice over Internet Protocol (VoIP) è una tecnologia che contiene l'hardware e software che consente agli utenti di utilizzare una rete basata su IP come mezzo di trasmissione per le chiamate telefoniche. In VoIP, voice dati vengono inviati nei pacchetti utilizzando le linee telefoniche a commutazione di circuito della rete PSTN o IP anziché le trasmissioni a commutazione di circuito tradizionale. Un gateway VoIP che si connette alla rete IP utilizza VoIP protocolli per inviare i pacchetti di dati tra i server Accesso Client e cassette postali Exchange 2013 e un sistema PBX vocale.

## Gateway VoIP

Un gateway VoIP è un dispositivo hardware di terze parti o prodotto che si connette un PBX legacy per le connessioni LAN. Il gateway VoIP consente il sistema PBX a comunicare con Exchange 2013 cassette postali e server Accesso Client che eseguono la messaggistica unificata di Exchange e servizi Call Router di messaggistica unificata.


> [!NOTE]
> Il gateway VoIP inoltre possibile connettere ai sistemi PBX che utilizzano VoIP invece di protocolli PSTN a commutazione di circuito.



Exchange 2013 La messaggistica unificata si basa sulle capacità del gateway VoIP per tradurre o convertire TDM o a commutazione di circuito telefonia basati su protocolli come ISDN e QSIG da un sistema PBX per protocolli basata su IP o VoIP come avviate protocollo SIP (Session), in tempo reale RTP (Transport Protocol) o t. 38 per il trasporto fax in tempo reale. Il gateway VoIP è fondamentale per la funzionalità e il funzionamento della messaggistica unificata.


> [!IMPORTANT]
> Dopo aver installato il gateway VoIP, IP PBX o PBX abilitato al SIP, è necessario creare un gateway IP di messaggistica unificata per rappresentare il dispositivo fisico. Dopo aver creato un gateway IP di messaggistica unificata, il server Accesso Client e cassette postali collegate con il gateway IP di messaggistica unificata invierà una richiesta SIP opzioni per il gateway VoIP, IP PBX o PBX abilitato al SIP per assicurarsi che il dispositivo si risponde. Se il gateway VoIP non risponde alla richiesta SIP OPTIONS dal server cassette postali, il server cassette postali verrà registrato un evento con ID 1088 che indica che la richiesta non riuscita. Per risolvere questo problema, verificare che il gateway VoIP, IP PBX o è in linea e disponibile e che la configurazione di messaggistica unificata sui server Accesso Client e cassette postali sia corretta.



Per ulteriori informazioni sulle configurazioni PBX e IP PBX, vedere [Configurazioni PBX e IP-PBX](pbx-and-ip-pbx-configurations-exchange-2013-help.md).

Inizio pagina

## Ulteriori informazioni

[Servizi, porte e protocolli di messaggistica unificata](um-protocols-ports-and-services-exchange-2013-help.md)

[Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)


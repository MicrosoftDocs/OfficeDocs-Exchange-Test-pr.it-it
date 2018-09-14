---
title: 'Consentire agli utenti di posta vocale di ricevere fax: Exchange 2013 Help'
TOCTitle: Consentire agli utenti di posta vocale di ricevere fax
ms:assetid: 451ab0ea-21e1-4c1f-ae62-4ba7cdfd1e4d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232022(v=EXCHG.150)
ms:contentKeyID: 52063064
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consentire agli utenti di posta vocale di ricevere fax

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2015-04-07_

Microsoft Exchange messaggistica unificata (UM) consente di messaggi vocali per essere recapitato alla cassetta postale dell'utente e anche consente agli utenti di ricevere fax nella propria cassetta postale. Nella messaggistica unificata, viene inviato un fax cassetta postale dell'utente come messaggio di posta elettronica con un file di immagine con estensione tif collegata. L'utente può aprire il file allegato utilizzando un'applicazione software in grado di aprire e visualizzare i file di immagine con estensione tif. In questo argomento vengono illustrati i fax e del relativo funzionamento nella messaggistica unificata.


> [!NOTE]
> Benché la messaggistica unificata non consentire agli utenti di inviare i fax in uscita, molte soluzioni di terze parti, ad esempio un servizio fax Internet, un messaggio di posta elettronica fax servizio o un'applicazione server fax di terze parti, è possibile utilizzare per l'invio di fax in uscita.



**Sommario**

Panoramica di fax

Metodi di fax

T.38

Panoramica di fax con la messaggistica unificata

La ricezione dei fax in arrivo

Fax metodi di chiamata di riferimento

Configurazione di fax

Numeri di telefono e fax

Messaggi fax di messaggistica unificata l'inserimento nel journal

## Panoramica di fax

Fax è l'abbreviazione di fax word. È una tecnologia che consente di trasferire elettronicamente documenti. In generale, fax vengono inviati e ricevuti da apparecchi fax o modem fax computer utilizzando il telefono rete PSTN (Public Switched), una rete basata su a commutazione di circuito o telefonia. Tuttavia, possono utilizzare altre opzioni per inviare e ricevere fax.

La maggior parte delle organizzazioni desidera oggi agli utenti siano in grado di inviare e ricevere fax. Le organizzazioni utilizzano uno o più dei metodi descritti di seguito per inviare o ricevere fax sulla rete PSTN o su Internet. Esistono vantaggi e svantaggi per ognuno di questi metodi.

  - Fax tradizionale e basati su computer fax

  - Fax con server fax o gateway fax

  - Fax con un vocali tramite rete IP (VoIP)

  - Fax con un'applicazione client di posta elettronica

Per inviare un messaggio fax, gli utenti in un'organizzazione potrebbero essere necessario eseguire le operazioni seguenti:

  - Stampare la copia del documento da inviare e utilizzare un apparecchio fax fisica per inviarlo.

  - Salvare il documento nel proprio computer e il modem fax per inviare i fax, ma questo richiede una linea telefonica connessa al computer in uso.

  - Utilizzare un servizio fax Internet che consente di inviare un documento da un'applicazione software specifico del fornitore.

  - Inviare un fax in uscita a un server fax utilizzando un'applicazione software che è configurata per l'utilizzo del server fax.

Per ricevere fax, gli utenti in un'organizzazione potrebbero essere necessario eseguire le operazioni seguenti:

  - Ricevere fax in un computer fisico fax all'interno dell'organizzazione.

  - Ricevere fax con modem fax installata nel proprio computer.

  - Ricezione fax da un Internet servizio fax.

  - Ricevere fax da un server fax configurata una rete.

  - Ricevere fax dal server dei partner fax che utilizza la messaggistica unificata per fornire i fax, utilizzare una rete VoIP.

Inizio pagina

## Metodi di fax

Sono disponibili diverse opzioni per l'invio e la ricezione dei fax, incluse le seguenti:

**Fax tradizionale e basati su computer fax**   Scanner, modem fax in un computer, una stampante con funzionalità fax incorporata o un apparecchio fax dedicato consente di inviare e ricevere fax. Tutti questi utilizzabile per trasmettere dati sotto forma di impulsi utilizzando una linea telefonica a un'altra fax periferica, solitamente un apparecchio fax o computer con modem fax. Gli impulsi sono quindi trasformati in immagini o utilizzati per stampare l'immagine nel documento.

Il metodo fax tradizionale richiede almeno una linea telefonica singolo del dispositivo di invio e ricezione e fax solo uno può essere inviato o ricevuto alla volta. Svantaggi dell'invio e ricezione dei fax con modem fax sono che il computer deve essere attivato e in esecuzione il software fax o un servizio fax. Questo tipo di basati su computer fax non utilizza Internet per inviare o ricevere fax.

**Fax tradizionale e basati su computer**

![Fax tradizionale](images/Bb232022.7bdc1cab-9504-4314-a6e0-eccdfe2a9cd6(EXCHG.150).gif "Fax tradizionale")

**Server fax o gateway e i servizi fax Internet**   Esistono diversi modi per inviare e ricevere fax via Internet. Queste proprietà includono utilizzando un'applicazione software in un computer o tramite un client di posta elettronica di ricevere fax. Nella maggior parte dei casi questo tipo di fax prevede l'utilizzo di un server fax o un gateway fax per eseguire la conversione tra posta elettronica e fax. Questo metodo è diventato sempre più popolari in quanto consente alle organizzazioni di rimuovere o evitare l'acquisto di apparecchi fax aggiuntive. Inoltre elimina la necessità di installare linee telefoniche aggiuntive. Questo tipo di fax comporta la creazione di un documento, inclusi pagina copertina fax con le informazioni di identificazione corrette e quindi il documento viene inviato a un apparecchio fax tradizionale. Ad esempio, l'utente utilizza un'applicazione software, ad esempio Microsoft Word o Microsoft Outlook per creare e inviare i fax al server fax o al gateway. Il server fax o il gateway riceve fax e quindi invia tramite una linea telefonica tradizionale a un apparecchio fax o modem fax che viene installato in un computer.

**Fax con server fax o gateway**

![Fax con server/gateway fax](images/Bb232022.d6fa2402-b4ca-4313-956c-62e5fe7731ad(EXCHG.150).gif "Fax con server/gateway fax")

Servizi fax via Internet consentono agli utenti di inviare fax da un computer tramite Internet. Un'applicazione software, ad esempio Word o Outlook può essere utilizzata per creare e inviare i fax a un servizio fax Internet. Molte aziende sono disponibili i servizi fax Internet sottoscrizione o tramite l'addebito per ogni messaggio fax inviato. Servizi fax via Internet offrono i vantaggi seguenti:

  - Non è necessario alcun apparecchio fax.

  - Non deve essere installato alcun software o hardware.

  - Nessun linee telefoniche dedicate sono necessari.

  - Riservatezza.

  - Fax più possono essere inviati alla stessa ora.

  - Quando il computer è disattivato, è possibile ricevere fax.

Nella figura seguente viene illustrato come utilizzare i servizi fax Internet per inviare e ricevere fax.

**Servizi fax via Internet**

![Servizi fax via Internet](images/Bb232022.5d0fb3d6-95f4-4fbf-80e5-64f5de553e65(EXCHG.150).gif "Servizi fax via Internet")

**Fax con un'applicazione client di posta elettronica**   Fax possono essere inviati e ricevuti da un apparecchio fax via Internet e quindi ricevuto da un client di posta elettronica, ad esempio Outlook.

Il protocollo T.37 è stato progettato per consentire un apparecchio fax inviare messaggi fax via Internet a un client di posta elettronica. I fax vengono inviati tramite Internet come allegati di posta elettronica, in genere come file tif o PDF. In questo tipo di fax, un apparecchio fax che supporta iFax o T.37 è necessario, oltre a un indirizzo di posta elettronica per i computer di invio e ricezione fax. Per interagire con modem fax e apparecchi fax tradizionale, tutti i computer fax T.37 supportano fax standard con una linea telefonica. Tuttavia, in alcuni casi, apparecchi fax T.37 essere utilizzati quando viene utilizzato anche un gateway fax. Nella figura seguente viene illustrato come base T.37 apparecchi fax e client di posta elettronica consente di inviare e ricevere fax.

**Fax tramite posta elettronica**

![Fax tramite posta elettronica](images/Bb232022.086f086b-dc39-4439-a694-7a98e03e65d1(EXCHG.150).gif "Fax tramite posta elettronica")

**Fax tramite una rete VoIP**   È una tecnologia che consente l'hardware e software che consente agli utenti di utilizzare una rete basata su IP come mezzo di trasmissione per le chiamate telefoniche VoIP. In una rete VoIP, fax e vocali dati vengono inviati nei pacchetti utilizzando IP anziché a commutazione di circuito tradizionale trasmissioni o le linee telefoniche a commutazione di circuito della rete PSTN. Un gateway VoIP che si connette alla rete IP utilizza VoIP per inviare i pacchetti di dati tra un server Accesso Client che eseguono il servizio Microsoft Exchange Unified Messaging routing delle chiamate e un server cassette postali in esecuzione il servizio messaggistica unificata di Exchange e un sistema di eXchange (PBX) Private Branch vocale. È inoltre possibile utilizzare un IP PBX per eseguire le funzioni di un gateway VoIP e un PBX.

Esistono due tipi di reti di base: a commutazione di circuito e commutazione di pacchetto. Una rete a commutazione di circuito è una rete in cui è disponibile una connessione dedicata. Una connessione dedicata è un canale configurato tra due nodi in modo che possano comunicare o a commutazione di circuito. Dopo avere stabilita una chiamata tra due nodi, la connessione è utilizzabile solo da questi due nodi. Quando la chiamata viene terminata da uno dei nodi, la connessione è stata annullata. Nelle reti a commutazione di circuito, ad esempio la rete PSTN, più chiamate vengono trasmessi mezzo di trasmissione stesso. Di solito, il supporto utilizzato nella rete PSTN è rame. Tuttavia, cavo in fibra ottica inoltre può essere utilizzato.

Nelle reti a commutazione di pacchetto, ad esempio Internet o una rete locale (LAN) pacchetti vengono instradati al propria destinazione attraverso la route più vantaggioso, ma non tutti i pacchetti in uscita tra due host viaggiano la stessa route, persino quelle provenienti da un singolo messaggio. In questo modo quasi che i pacchetti arriveranno in momenti diversi e ordine. In una rete a commutazione di pacchetto, i pacchetti (messaggi o frammenti dei messaggi) vengono instradati singolarmente tra i nodi attraverso collegamenti di dati che possono essere condivise da altri nodi. A commutazione di pacchetto, a differenza di commutazione di circuito, più le connessioni ai nodi della rete condividono la larghezza di banda disponibile. Reti a commutazione di pacchetto è stato possibile per Internet sia disponibile e, al contempo, ha reso reti di dati, ovvero reti IP e VoIP particolarmente Local, ovvero più diffusi e disponibili.

Inizio pagina

## T.38

T. 38 è un protocollo che consente l'invio di fax su una rete basato su IP e standard fax. Una rete basata su IP che utilizza il protocollo t. 38 utilizza Simple Mail Transfer Protocol (SMTP) e (MULTIPURPOSE Internet Mail Extension) per inviare un messaggio alla cassetta postale del destinatario. Consente di t. 38 per le trasmissioni fax IP per i dispositivi fax basate su IP e gateway fax. I dispositivi possono includere host basato su rete IP, ad esempio i computer client e stampanti. In messaggistica unificata di Exchange, le immagini fax sono documenti separati codificati come file tif e collegato a un messaggio di posta elettronica. Messaggio di posta elettronica sia l'allegato del file tif vengono inviati alla cassetta postale abilitata alla messaggistica unificata dell'utente.

La messaggistica unificata si basa sulle capacità del gateway per tradurre o convertire ora divisione Multiplex TDM () o protocolli di telefonia a commutazione di circuito basata come ISDN Integrated Services Digital Network () e QSIG da un sistema PBX protocolli basato su VoIP o IP come protocollo SIP (Session Initiation), Real-time Transport Protocol (RTP) o t. 38 per la ricezione dei messaggi fax. Il gateway VoIP è fondamentale per la funzionalità e il funzionamento della messaggistica unificata. Il gateway VoIP è responsabile del rilevamento del fax toni. Server accesso client e cassette postali si basano sul gateway VoIP per inviare una notifica che è stato rilevato un fax. Il server Accesso Client e cassette postali verrà quindi discutere del fattore sessione multimediale e utilizzano il protocollo t. 38.

Inizio pagina

## Panoramica di fax con la messaggistica unificata

In messaggistica unificata, l'utente riceve fax immagini come documenti separati codificati nel file di immagine TIF associati a un messaggio di posta elettronica. Messaggio di posta elettronica sia l'allegato tif vengono inviati alla cassetta postale abilitata alla messaggistica unificata dell'utente.

Esistono numerosi vantaggi per l'invio di un messaggio fax cassetta postale dell'utente. I vantaggi sono i seguenti:

  - È possibile ridurre il numero di computer fisico o tradizionale fax.

  - Il numero di linee telefoniche utilizzate per fax in un'organizzazione può essere ridotto, in quanto il server cassette postali può coda dei fax e inviare ogni fax quando una delle linee telefoniche diventa disponibile.

  - Fax ricevuti come file di immagine TIF sono migliore rispetto al fax tradizionale. Fax in arrivo possono essere stampate dalla stampante locale o condivisa.

  - Fax inviati alla cassetta postale dell'utente sono più sicuro perché è meno probabilità di fax stampato per essere prelevati da un utente diverso dal destinatario.

  - Gli utenti possono ricevere fax senza lasciare propria scrivania.

  - Messaggi fax ricevuti possono essere monitorati per assicurarsi che siano conformi ai criteri di protezione dell'organizzazione.

Un messaggio fax singolo è possibile inviare solo a un singolo utente abilitato alla messaggistica unificata. La messaggistica unificata non può inoltrare messaggi a una lista di distribuzione fax. Se è necessario disporre di questa funzionalità, è necessario eseguire la procedura seguente:

1.  Creare una cassetta postale per rispondere alla chiamata fax. Questo valore sarà la cassetta postale per la lista di distribuzione.

2.  Abilitare alla messaggistica unificata la cassetta postale elenco di distribuzione.

3.  Creare una regola per la cassetta postale abilitata alla messaggistica unificata. La regola verrà configurata per inoltrare tutti i messaggi della lista di distribuzione selezionati.

Inizio pagina

## La ricezione dei fax in arrivo

Ricezione di un fax su una rete VoIP differisce ricezione dei fax in un apparecchio fax standard o tramite un server fax che si trova in una rete IP. Per abilitare i fax inviati e ricevuti tramite una rete VoIP, è necessario disporre di un gateway VoIP o IP PBX che supporta il protocollo t. 38 e un server che supporta anche t. 38. T. 38 consente per le trasmissioni fax basato su IP per gli host basato su rete IP, ad esempio, computer client, stampanti a fax incorporato e server, ad esempio un server cassette postali.


> [!IMPORTANT]
> Invio e ricezione dei fax utilizzando t. 38 o g. 711 non è supportato in un ambiente in cui vengono integrati Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server e la messaggistica unificata.



Quando un PBX riceve una chiamata, la inoltra la chiamata all'estensione appropriata. Se non esiste alcuna risposta al numero di interno dell'utente, il PBX inoltra la chiamata a un gateway VoIP e il gateway inoltra la chiamata al server cassette postali appropriato. Il server cassette postali determina se la chiamata è una chiamata vocale o una chiamata fax, in base al protocollo utilizzato per la chiamata. Quando si utilizza il protocollo SIP, il server cassette postali elabora la chiamata come un messaggio vocale. Tuttavia, se viene utilizzato il protocollo t. 38 dal gateway VoIP, il server cassette postali riconosce che la chiamata è per fax e viene elaborato come descritto nel paragrafo seguente. Un server cassette postali inoltra le chiamate fax in arrivo a un server partner fax dedicato, che quindi consente di stabilire la chiamata fax con il mittente riceve fax per conto dell'utente abilitato alla messaggistica unificata. Il server partner fax invia quindi fax incluso come allegato tif in un messaggio SMTP alla cassetta postale del destinatario.

Quando un server cassette postali riceve un segnale di fax in ingresso di t. 38 da un gateway VoIP, il server cassette postali esegue una query utilizzando Lightweight Directory Access Protocol (LDAP) per determinare se il destinatario della chiamata fax in ingresso è consentito ricevere messaggi fax in arrivo e per determinare l'indirizzo SIP del server partner fax. Dopo che è archiviato questa informazione, il server cassette postali invia una richiesta di rinvio chiamata fax al gateway VoIP o peer SIP, che quindi inoltra la richiesta di fax al server partner fax. Dopo il fax chiamata è stata stabilita, il mittente riceve il supporto di fax e i dati al server partner fax. Dopo che il server partner fax riceve i dati e il supporto di fax, utilizza SMTP per inviare un messaggio di posta elettronica a un server cassette postali. Il messaggio contiene un'immagine TIF del messaggio fax e X-Header speciali per il destinatario previsto.

Dopo il fax messaggio viene autenticato e viene inviato da un server partner fax valido, l'Assistente cassette postali di messaggistica unificata sul server cassette postali emette una chiamata RPC al servizio di messaggistica unificata di Exchange. In questo modo che le proprietà dei messaggi fax corrispondano a quelle dei messaggi fax creati da un server cassette postali. Infine, il server cassette postali invia nuovamente il messaggio finale fax, che include l'allegato di tif e messaggi di posta elettronica per i fax in arrivo. Quindi, tramite MAPI RPC, viene recapitata versione completata e formattata del messaggio fax al server cassette postali che contiene cassetta postale del destinatario previsto.

Inizio pagina

## Fax metodi di chiamata di riferimento

La segnalazione chiamate fax in ingresso alla cassetta postale di una server tramite SIP re-INVITE dal gateway VoIP o peer SIP (gateway multimediali), la notifica CNG (chiamata segnale fax) tramite peer SIP o il rilevamento CNG dal server cassette postali. Nelle sottosezioni seguenti in dettaglio il riferimento di chiamate fax in ogni caso.

## Re-INVITE dal peer SIP

Una chiamata in arrivo a un numero pilota alla messaggistica unificata viene indirizzata alla messaggistica unificata come un invito a voice profilo SDP (RTP/audio)

1.  Messaggistica unificata accetta l'invito e i flussi multimediali vengono stabiliti. Quando la chiamata è stata stabilita, la trasmissione di fax viene avviata dal chiamante.

2.  Il peer SIP rileva il tono di fax chiamante (CNG). Peer SIP problemi un INVITARE di nuovo al server cassette postali, questa volta se si specifica un profilo di fax (t. 38 o g. 711) il SDP.

3.  Messaggistica unificata risponde all'invito a una 200 OK che inserisce il peer SIP "in attesa?.

4.  Messaggistica unificata problemi si riferiscono, che fa riferimento il peer SIP (CNG) a un fax partner soluzione punto finale, ottenuto dal relativi dati di configurazione.

5.  Peer SIP invia la sessione di fax invita la soluzione di partner fax.

6.  La soluzione di partner fax accetta l'invito e una sessione multimediale viene stabilita con il peer SIP.

## Notifica CNG tramite peer SIP

Una chiamata in arrivo a un numero pilota alla messaggistica unificata viene indirizzata alla messaggistica unificata come un invito a voice profilo SDP (RTP/audio).

1.  Messaggistica unificata accetta l'invito e i flussi multimediali vengono stabiliti. Quando la chiamata è stata stabilita, la trasmissione di fax viene avviata dal chiamante.

2.  Il peer SIP rileva il tono di fax chiamante (CNG). Il peer SIP notifica al server di messaggistica unificata del fax inviando una notifica CNG nel flusso RTP conforme a RFC 4733.

3.  Messaggistica unificata risponde alla notifica inviando immediatamente si riferiscono e fa riferimento il peer SIP a un endpoint soluzioni partner fax ottenuto dal relativi dati di configurazione.

4.  Peer SIP invia la sessione di fax invita la soluzione di partner fax.

5.  La soluzione di partner fax accetta l'invito.

6.  Una sessione multimediale viene stabilita con il peer SIP.

## Rilevamento CNG tramite un server cassette postali

Una chiamata in arrivo a un numero pilota alla messaggistica unificata viene indirizzata alla messaggistica unificata come un invito a voice profilo SDP (RTP/audio). Messaggistica unificata accetta l'invito e i flussi multimediali vengono stabiliti.

1.  Quando la chiamata è stata stabilita, la trasmissione di fax viene avviata dal chiamante.

2.  Il server cassette postali rileva il tono di fax (CNG) nel flusso audio RTP.

3.  Messaggistica unificata risponde alla notifica inviando immediatamente si riferiscono e fa riferimento il peer SIP a un endpoint soluzioni partner fax ottenuto dal relativi dati di configurazione.

4.  Peer SIP invia la sessione di fax invita la soluzione di partner fax.

5.  La soluzione di partner fax accetta l'invito.

6.  Una sessione multimediale viene stabilita con il peer SIP.

Inizio pagina

## Configurazione di fax

Per impostazione predefinita, quando si installa il server cassette postali, il server non è configurato per consentire le chiamate fax in arrivo devono essere elaborati o inviati a un utente abilitato alla messaggistica unificata. Per configurare la messaggistica unificata con un server partner fax, è necessario configurare il criterio cassetta postale di messaggistica unificata e configurare l'autenticazione tra server cassette postali e il server partner fax. Per ulteriori informazioni, vedere [Impostazione di fax in arrivo](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/set-up-incoming-faxing).

Inizio pagina

## Numeri di telefono e fax

Se si sta configurando gli utenti abilitati alla messaggistica unificata per ricevere messaggi fax, la messaggistica unificata di Exchange offre le seguenti opzioni:

  - Un numero di telefono di accesso esterno DID (Direct Inward) per un singolo utente utilizzato per fax e segreteria telefonica.

  - Numero di telefono DID distinto per un singolo utente utilizzato per la ricezione dei fax.

  - Un numero di telefono fax centrale per tutti gli utenti che riceve tutti i fax.

## Un singolo numero di telefono DID

Quando si attiva un utente per la messaggistica unificata utilizzando la pagina **attiva della messaggistica unificata delle cassette postali** o il cmdlet **Enable-UMMailbox** , è necessario specificare almeno un numero di interno singolo utente. Questo numero di interno è stato attivato per ogni utente e deve essere univoco all'interno di un determinato dial plan. L'estensione viene utilizzato dalla messaggistica unificata per individuare l'utente corretto e a recapitare i messaggi vocali e fax cassetta postale dell'utente. Per ulteriori informazioni, vedere [Enable-UMMailbox](https://technet.microsoft.com/it-it/library/aa998033\(v=exchg.150\)).

Utilizzo di un singolo numero DID, è possibile configurare Fax in modo che un utente utilizza un singolo numero DID per fax e vocali. Questa configurazione è facile da gestire e non rifiuti numeri DID aggiuntivi. Se l'utente non al computer o sul telefono quando si riceve una chiamata fax, alla messaggistica unificata risponde alla chiamata, viene rilevato il tono di fax, crea il messaggio fax e viene inviato all'utente.

Se è stato di un utente la cui fax è configurato con un singolo numero di telefono riceve una chiamata da un apparecchio fax quando non è al computer o sul telefono, è possibile:

  - Non rispondere al telefono quando che squilli in modo che la chiamata fax verrà inoltrata e ha risposto per un server cassette postali e il messaggio verrà creato e inoltrato alla cassetta postale dell'utente.

  - Rispondere alla chiamata fax e trasferirla a se stesso in modo che la chiamata viene inoltrata e ha risposto per un server cassette postali e il messaggio verrà creato e inoltrato alla cassetta postale dell'utente.

  - Attendere il chiamante a inviare nuovamente il fax e consentire le chiamate fax trasferita a un server cassette postali.

In breve, con un singolo numero DID richiede all'utente di eseguire azioni aggiuntive per poter ricevere i messaggi fax.

Inizio pagina

## Più numeri di telefono DID

Quando si attiva un utente per la messaggistica unificata, è necessario immettere almeno un numero di interno singolo per tale utente. È possibile aggiungere più numeri di interno di un utente abilitato alla messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange (EAC). Per ulteriori informazioni, vedere [Aggiungere un numero interno](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-voice-mail/add-extension-number).

Aggiunta di più numeri di interno è utile quando un utente abilitato alla messaggistica unificata:

  - Riceve fax molti.

  - Non si desidera essere disturbato con risponde al telefono per ricevere fax.

  - Non desidera ascoltare un tono di fax quando si risponde al telefono.

Aggiungere più estensioni è più complessa rispetto all'utilizzo di una singola estensione e potrebbe essere necessario configurare alcune impostazioni aggiuntive in un sistema PBX o IP PBX. Per configurare più numeri di interno di un utente abilitato alla messaggistica unificata, è necessario disporre estensione numeri DID disponibili non vengono utilizzati nell'organizzazione. Non è consigliabile utilizzare più numeri per un utente abilitato alla messaggistica unificata, se l'organizzazione dispone di un numero limitato di numeri di interno DID disponibili.

I vantaggi dell'utilizzo di più numeri di interno DID sono che un utente abilitato alla messaggistica unificata per ricevere le chiamate vocali in un numero di interno DID e fax viene chiamato su un altro numero di estensione DID. Utilizzando separata non ha numeri per la segreteria telefonica e le chiamate fax è più semplice per l'utente.

Se si configurano due numeri di interno DID per un utente specifico, i numeri DID possono provenire da separato dial plan di messaggistica unificata. Per l'utilizzo di due numeri DID, è possibile creare un dial plan e utilizzare un server cassette postali come un server dedicato che riceverà le chiamate fax e messaggi fax in avanti per gli utenti. Per ulteriori informazioni, vedere [Creazione di un dial plan di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

Quando si sta configurando più numeri di interno DID per gli utenti abilitati alla messaggistica unificata sono disponibili le opzioni seguenti:

  - **Un'estensione di fax senza la messaggistica unificata e uno per VoIP**   Questo tipo di configurazione è stato attivato per ogni utente e viene utilizzato quando è necessario inutilizzati o in più numeri di interno DID disponibili. Un numero di interno DID deve essere pubblicato come numero di posta vocale dell'utente e numero di interno altri DID deve essere pubblicato come numero di fax dell'utente. Segreteria telefonica chiamate che risponde perché l'utente non rispondere al telefono o un segnale di occupato viene rilevato vengono inoltrate a un server cassette postali e un messaggio vocale viene creato e inviato alla cassetta postale dell'utente abilitato alla messaggistica unificata. Numero di interno può essere collegato a un apparecchio fax o a un altro computer con modem fax. Con questa configurazione, un server cassette postali non elaborazione le chiamate fax e i messaggi fax non vengono inviati alla cassetta postale dell'utente abilitato alla messaggistica unificata.

  - **Un'estensione per fax e una per VoIP**   Questo tipo di configurazione è stato attivato per ogni utente e può essere utilizzato quando l'organizzazione dispone di molti numeri di interno DID disponibili. In questa configurazione, entrambi estensione DID numeri che risponde perché l'utente non risponde al telefono o un segnale di occupato viene rilevato vengono inoltrate a un server cassette postali, che consente di creare un messaggio fax o vocali in base al numero di interno DID che viene chiamato. Anche se l'utente pubblica un numero di Enterprise voice e una per fax, il server cassette postali rileva il tipo di chiamata viene ricevuto il numero di estensione DID e può creare un messaggio fax o vocali da chiamate a uno dei numeri di interno DID. Ciò è molto utile quando un utente non dispone di un fax separato o un computer dedicato con modem fax per rispondere alle chiamate fax in ingresso.

  - **Una "fantasma? estensione per fax e una per voice** questo tipo di configurazione è stato attivato per ogni utente. È sostanzialmente uguale come la configurazione che utilizza due numeri, uno per fax e quello di Enterprise voice. Tuttavia, questa configurazione, il numero che viene pubblicato per le chiamate fax per l'utente abilitato alla messaggistica unificata sia configurato su PBX come "fantasma? estensione. Le chiamate in arrivo ricevuti in questo numero di interno DID "fantasma" vengono sempre inoltrate a un server cassette postali.
    
    Il vantaggio di questo tipo di configurazione è che le chiamate fax in arrivo sono ha risposto per un server cassette postali. Quando il telefono squilla ma non si risponde, fax viene creato e inoltrato dal server cassette postali alla cassetta postale dell'utente abilitato alla messaggistica unificata senza interferire con l'utente. Infatti, automaticamente alcun dispositivo fax o telefono non è posizionato all'incirca l'utente e l'utente non riceve l'opzione chiama della chiamata in arrivo.
    
    Gli svantaggi di questo tipo di configurazione sono che sono necessari ulteriori estensioni DID disponibile e che è necessario configurare il sistema PBX o IP PBX per inoltrare la chiamata a un server cassette postali.

## Numero di fax centrale

Quando si attiva un utente per la messaggistica unificata utilizzando la pagina **Attiva della messaggistica unificata delle cassette postali** o il cmdlet **Enable-UMMailbox** , è necessario specificare almeno un numero di interno singolo utente. Tuttavia, se è necessario configurare un solo numero di fax per i fax in arrivo, è necessario configurare una cassetta abilitata alla messaggistica unificata che consente di ricevere tutti i fax.

In alcune organizzazioni, in particolare quelli che ricezione dei fax ogni giorno, è possibile pubblicare un numero di fax dell'intera organizzazione. Questo numero di fax viene utilizzato da tutti i chiamanti quando si inviano fax per gli utenti nell'organizzazione.

Pubblicare un numero di fax dell'intera organizzazione consente all'organizzazione di controllare i tipi di fax ricevuti da parte di utenti. Il vantaggio di questa configurazione è che richiede solo un singolo numero di estensione DID o di un numero di telefono esterno. Inoltre, non richieda un numero DID separato per fax per ogni utente abilitato alla messaggistica unificata. Tuttavia, necessario "segretaria di fax" o altra persona per distribuire i fax in arrivo per gli utenti all'interno dell'organizzazione in base alle informazioni che sono incluso nella pagina copertina fax o del messaggio di fax.


> [!NOTE]
> Utilizzo di un solo numero di fax con il riconoscimento ottico caratteri (OCR) non è disponibile in Exchange messaggistica unificata. Questo tipo di configurazione può utilizzare un solo numero di fax. Tuttavia, invece di essere inviato al destinatario da una persona, il software fax riceve fax, esegue OCR e quindi cerca di individuare il destinatario in base alle informazioni sul messaggio copertina fax o pagina.



Utilizzo di un numero di fax singolo per tutta l'organizzazione è utile nelle situazioni seguenti:

  - Un utente all'interno dell'organizzazione riceve fax troppi nella propria cassetta postale per una gestione ottimale.

  - L'utente riceve fax un numero eccessivo di posta indesiderata nella propria cassetta postale.

  - Le esigenze aziendali sono troppo complesse da permettono l'utilizzo di creazione di una regola di trasporto per accettare i fax in ingresso e li indirizzano alla cassetta postale desiderata. Può non essere possibile, ad esempio, se l'organizzazione richiede instradare determinati fax a un gruppo e altre attività fax in un altro gruppo. Per ulteriori informazioni, vedere [Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

  - Filtro messaggi fax tramite Outlook non efficace.

Inizio pagina

## Messaggi fax di messaggistica unificata l'inserimento nel journal

Molte organizzazioni che implementano l'inserimento nel journal possono inoltre utilizzare la messaggistica unificata per consolidare i loro posta elettronica, segreteria telefonica e dell'infrastruttura di fax. Tuttavia, è possibile non al processo di inserimento nel journal di generare rapporti del journal per i messaggi generati dalla messaggistica unificata. In questo caso, è possibile decidere se alla posta vocale del journal i messaggi e messaggi di notifica di chiamata senza risposta vengono gestite da un server cassette postali o per ignorare tali messaggi. Se l'organizzazione non richiede l'inserimento nel journal dei messaggi vocali e delle notifiche di chiamata, è possibile ridurre lo spazio su disco che è necessario per archiviare i rapporti del journal saltando tali messaggi. Quando si abilita o disabilita l'inserimento nel journal dei messaggi della segreteria telefonica e messaggi di notifica di chiamata senza risposta, la modifica viene applicata a tutti i servizi di trasporto nell'organizzazione. Per ulteriori informazioni, vedere [Inserimento nel journal](journaling-exchange-2013-help.md).


> [!NOTE]
> I messaggi che contengono fax generate da un server cassette postali sono sempre inseriti nel journal, anche se si configura una regola del journal che specifica i messaggi di notifica non di posta vocale di messaggistica unificata del journal e chiamata senza risposta.



Inizio pagina


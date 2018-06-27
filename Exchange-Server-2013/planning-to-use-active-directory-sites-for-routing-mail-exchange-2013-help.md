---
title: "Pianificazione dell'utilizzo di siti di Active Directory per il routing della posta: Exchange 2013 Help"
TOCTitle: Pianificazione dell'utilizzo di siti di Active Directory per il routing della posta
ms:assetid: 0f697cee-bcaa-4c69-b80c-7a2afd1817d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996299(v=EXCHG.150)
ms:contentKeyID: 52063043
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pianificazione dell'utilizzo di siti di Active Directory per il routing della posta

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-05-21_

In Microsoft Exchange Server 2013, i siti Active Directory e i gruppi di disponibilità dei database (DAG, Database Availability Group) vengono riconosciuti come confini di routing. Tuttavia, Exchange 2013 utilizza comunque la topologia dei siti di Active Directory per stabilire la modalità di trasporto dei messaggi dai server di Exchange a diversi gruppi di disponibilità dei database o siti interni all'azienda. Per ulteriori informazioni, vedere [Routing della posta](mail-routing-exchange-2013-help.md).

Il servizio di trasporto sul server Cassette postali consente di trasportare i messaggi all'interno dell'organizzazione di Exchange. Quando si distribuisce un'organizzazione Exchange 2013 pura o si distribuisce Exchange 2013 in un'organizzazione Exchange Server 2010 pura, non è necessaria una configurazione aggiuntiva per stabilire il routing nella foresta.

**Sommario**

How Exchange 2013 uses Active Directory site membership

Determine Active Directory site membership

Overview of IP site links

Exchange 2013 server placement in Active Directory sites

## Modalità di utilizzo dell'appartenenza al sito di Active Directory da parte di Exchange 2013

Exchange 2013 è un'applicazione che dispone del supporto per i siti. Le applicazioni con supporto per i siti possono determinare la propria appartenenza al sito di Active Directory e l'appartenenza al sito di altri server interrogando Active Directory. Exchange 2013 utilizza l'appartenenza al sito per determinare i controller di dominio e i server di catalogo globale da utilizzare per l'elaborazione delle query di Active Directory. Inoltre, quando un server che esegue Exchange deve stabilire l'appartenenza al sito Active Directory di un altro server Exchange, è possibile eseguire una query in Active Directory per recuperare il nome del sito.

In Exchange 2013, il servizio Topologia di Microsoft Exchange Active Directory è responsabile dell'aggiornamento dell'attributo sito dell'oggetto server Exchange. Poiché l'appartenenza al sito di Active Directory è un attributo dell'oggetto server, non è necessario che Exchange esegua una query DNS per risolvere l'indirizzo di un server in una subnet associata a un sito di Active Directory. Contrassegnare l'attributo del sito di Active Directory in un oggetto server di Exchange consente l'assegnazione dell'appartenenza al sito di Active Directory a un server che non è un membro del dominio, ad esempio un server Trasporto Edge sottoscritto.

I server Exchange 2013 utilizzano le informazioni sull'appartenenza al sito di Active Directory nel modo riportato di seguito:

  - **Invio di posta**   Il servizio di invio del trasporto alla cassetta postale su un server Cassette postali di Exchange 2013 utilizza le informazioni relative all'appartenenza al sito di Active Directory per determinare gli altri server Cassette postali di Exchange 2013 che si trovano nello stesso sito di Active Directory. Se il server Cassette postali non appartiene a un gruppo di disponibilità del database o se quest'ultimo non si estende su più siti di Active Directory, il servizio di invio del trasporto alla cassetta postale sul server Cassette postali di origine invia messaggi per il routing e il trasporto al servizio di trasporto su un server Cassette postali di Exchange 2013, nello stesso sito di Active Directory.

  - **Recapito posta**   Il servizio di trasporto su un server Cassette postali di Exchange 2013 esegue la risoluzione dei destinatari e la query di Active Directory per stabilire una corrispondenza tra un indirizzo di posta elettronica e l'account del destinatario. Le informazioni sull'account del destinatario includono il nome di dominio completo (FQDN, Fully Qualified Domain Name) del database di cassette postali dell'utente. Il servizio di trasporto esegue una query di Active Directory per determinare il sito di Active Directory relativo al database di cassette postali dell'utente. Se il database di cassette postali non appartiene a un gruppo di disponibilità del database, il messaggio verrà inviato a quel server Cassette postali. Altrimenti, il messaggio verrà inoltrato a un altro server Cassette postali nello stesso sito del server Cassette postali di destinazione per il recapito.

  - **Routing dei messaggi**   Il servizio di trasporto sui server Cassette postali di Exchange 2013 recupera informazioni da Active Directory per determinare come eseguire il routing della posta all'interno dell'organizzazione. In Exchange 2013 viene utilizzato il concetto di *gruppi di recapito* al fine di stabilire dove e come eseguire il routing dei messaggi. A seconda della destinazione, è possibile eseguire il routing del messaggio nel servizio di trasporto o nel servizio di recapito del trasporto alla cassetta postale su un server Cassette postali di Exchange 2013 o su un server Trasporto Hub che esegue una versione precedente di Exchange. Per ulteriori informazioni, vedere [Routing della posta](mail-routing-exchange-2013-help.md).

  - **Invio messaggi di messaggistica unificata**   Il servizio di messaggistica unificata nei server Cassette postali di Exchange 2013 utilizza le informazioni relative all'appartenenza al sito di Active Directory per individuare gli altri server Cassette postali presenti nello stesso sito di Active Directory. Il servizio di messaggistica unificata invia messaggi per eseguire il routing al servizio di trasporto nel server Cassette postali presente all'interno del medesimo sito di Active Directory. Il server del servizio di trasporto esegue la risoluzione dei destinatari e interroga Active Directory per stabilire la corrispondenza tra un numero di telefono (numero E.164) o un indirizzo SIP e l'account del destinatario. Al termine della risoluzione dei destinatari, il servizio di trasporto recapita il messaggio alla cassetta postale di destinazione in modo analogo a un normale messaggio di posta elettronica.

  - **Connessioni client al server Accesso client**   Quando il server Accesso client riceve una richiesta di connessione dall'utente, interroga Active Directory per determinare quale server Cassette postali ospita la cassetta postale dell'utente. In seguito, il server Accesso client recupera l'appartenenza al sito di Active Directory del server Cassette postali e inoltra la connessione al server Cassette postali.

## Determinare l'appartenenza al sito di Active Directory

I client di Active Directory presuppongono l'appartenenza al sito associando l'indirizzo IP assegnato a una subnet definita in Siti e servizi di Active Directory e associata a un sito di Active Directory. Il client utilizza quindi tali informazioni per determinare i controller di dominio e i server di catalogo globale che si trovano in quel sito e comunica con i server di directory per ottenere l'autenticazione e le autorizzazioni. Exchange 2013 utilizza questa relazione preferendo inoltre recuperare le informazioni sui destinatari dai server di directory che si trovano nello stesso sito del server Exchange 2013.

Tutti i computer che appartengono allo stesso sito di Active Directory vengono considerati ben collegati, con una connessione di rete affidabile e ad alta velocità. Per impostazione predefinita, quando una foresta di Active Directory viene distribuita per prima, esiste un unico sito denominato `Default-First-Site-Name`. Se nessun altro sito è stato configurato manualmente dall'amministratore, tutti i server e i computer client nella foresta vengono considerati membri di `Default-First-Site-Name`.

Quando viene definito più di un sito, l'amministratore di Active Directory deve definire le subnet presenti nell'organizzazione e associarle ai siti di Active Directory.

Il servizio Topologia di Microsoft Exchange Active Directory verifica l'attributo di appartenenza al sito nell'oggetto server Exchange all'avvio del server. Se è necessario aggiornare l'attributo del sito, il servizio Topologia di Active Directory di Microsoft Exchange contrassegna l'attributo con il nuovo valore. Il servizio Topologia di Active Directory di Microsoft Exchange verifica il valore dell'attributo del sito ogni 15 minuti e aggiorna il valore se l'appartenenza al sito è cambiata. Il servizio Topologia di Active Directory di Microsoft Exchange utilizza il servizio Accesso rete per ottenere l'appartenenza corrente al sito. Il servizio Accesso rete aggiorna l'appartenenza al sito ogni cinque minuti. Ciò significa che il periodo di latenza tra il momento in cui cambia l'appartenenza al sito e il momento in cui il nuovo valore viene indicato sull'attributo del sito non supera i 20 minuti.

## Cenni preliminari sui collegamenti al sito IP

Le relazioni tra i siti di Active Directory vengono definite dai collegamenti al sito IP. Il collegamento al sito IP è costituito da due o più siti di Active Directory. Tutti i siti di Active Directory che fanno parte del collegamento comunicano allo stesso costo. Le proprietà del collegamento al sito IP includono l'assegnazione di un costo, una pianificazione e un intervallo. Le proprietà della pianificazione e dell'intervallo vengono utilizzate solo per determinare la frequenza di replica di Active Directory. Exchange 2013 utilizza l'assegnazione del costo per determinare la route con il costo di traffico più basso quando esistono più percorsi di destinazione. Il costo della route è determinato dall'aggregazione del costo di tutti i collegamenti al sito in un percorso di trasmissione. L'amministratore di Active Directory assegna il costo a un collegamento in base alla relativa velocità della rete e alla larghezza di banda disponibile a confronto con altre connessioni disponibili.

Per impostazione predefinita, il servizio di trasporto su un server Cassette postali tenta sempre di stabilire una connessione diretta con il servizio di trasporto o di recapito del trasporto alla cassetta postale sul server Cassette postali di un sito Active Directory diverso. I messaggi in transito non vengono inoltrati attraverso il servizio di trasporto su ogni server Cassette postali in un percorso di collegamento al sito. Tuttavia, i server Cassette postali nei siti intermedi di Active Directory lungo il percorso di routing possono effettuare l'inoltro del messaggio nei seguenti scenari:

  - L'inoltro diretto tra i server Cassette postali non si verifica se esiste un sito hub lungo il percorso di routing più conveniente. È possibile configurare un sito di Active Directory come sito hub in modo che i messaggi vengano instradati attraverso il sito hub prima di essere inoltrati al server di destinazione. I siti hub saranno illustrati più avanti in questo argomento.

  - Exchange 2013 utilizza il percorso di routing derivato dalle informazioni sul collegamento al sito IP quando si verifica un errore durante la comunicazione al sito di Active Directory di destinazione. Se nessun server Cassette postali risponde nel sito di Active Directory di destinazione, il recapito dei messaggi viene rinviato lungo il percorso di routing più conveniente fino a quando non viene stabilita una connessione a un server Cassette postali in un sito di Active Directory lungo il percorso di routing. I messaggi vengono accodati nel sito di Active Directory e lo stato della coda sarà Riprova. Questo comportamento viene denominato *coda nel punto di errore*.

  - Nelle organizzazioni Exchange 2013 prive di gruppi di disponibilità dei database, il servizio di trasporto sul server Cassette postali utilizza le informazioni sul collegamento al sito IP per ottimizzare il routing dei messaggi inviati a più destinatari. Il server Cassette postali ritarda la moltiplicazione dei messaggi fino al raggiungimento di una duplicazione nei percorsi di routing dei destinatari. Il messaggio moltiplicato viene inoltrato a ciascuna destinazione da un server Cassette postali nel sito di Active Directory che rappresenta la duplicazione nei singoli percorsi di routing. Questa funzionalità è denominata *fanout ritardato*.

## Designazione dei siti hub

È possibile utilizzare il cmdlet **Set-AdSite** per configurare un sito di Active Directory come sito hub. Se esiste un sito hub lungo il percorso di routing dal costo più conveniente tra due server di trasporto, i messaggi vengono indirizzati verso il sito hub per l'elaborazione prima di essere inoltrati al server di destinazione. Affinché si verifichi questo comportamento di routing, è necessario che il sito hub si trovi lungo il percorso di routing più conveniente tra due server di trasporto. Questa configurazione deve essere utilizzata solo quando viene richiesta dalla topologia di rete, ad esempio quando esistono dei firewall tra i siti di Active Directory che non consentono l'inoltro diretto delle comunicazioni SMTP. Per ulteriori informazioni, vedere [Configurare impostazioni di routing della posta di Exchange in Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

## Impostazione di un costo specifico di Exchange per un collegamento al sito IP

È possibile utilizzare il cmdlet **Set-AdSiteLink** in Exchange Management Shell per configurare un costo specifico di Exchange per un collegamento al sito IP di Active Directory. Il costo specifico di Exchange è un attributo distinto utilizzato in luogo del costo assegnato ad Active Directory per determinare il percorso di routing di Exchange. Questa configurazione è utile quando i costi del collegamento al sito IP di Active Directory non producono una topologia di routing ottimale dei messaggi in Exchange. Per ulteriori informazioni, vedere [Configurare impostazioni di routing della posta di Exchange in Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

## Impostazione dei limiti relativi ai messaggi nei collegamenti ai siti IP

Per impostazione predefinita, Exchange 2013 non impone un limite per la dimensione massima dei messaggi inoltrati mediante server Cassette postali in diversi siti di Active Directory. Se si utilizza il cmdlet **Set-AdSiteLink** per configurare la dimensione massima dei messaggi su un collegamento al sito IP di Active Directory, il routing genera un rapporto di mancato recapito (NDR) per tutti i messaggi di dimensioni superiori rispetto al limite massimo configurato su uno qualsiasi dei collegamenti al sito di Active Directory nel percorso di routing con il costo minore. Questa configurazione è utile per limitare la dimensione dei messaggi inviati ai siti remoti di Active Directory che devono comunicare mediante connessioni con larghezza di banda ridotta.

## Posizionamento del server Exchange 2013 nei siti di Active Directory

Affinché venga eseguito correttamente il routing dei messaggi tra i server di Exchange 2013, tutti i server Exchange che vengono distribuiti nella foresta devono appartenere a un sito di Active Directory. Assicurarsi che gli indirizzi IP che sono stati assegnati si trovino nelle subnet associate correttamente ai siti di Active Directory.

Il primo passo nella pianificazione del posizionamento dei server Exchange 2013 nella topologia del sito di Active Directory consiste nel documentare la topologia corrente. La documentazione deve includere quanto segue:

  - Siti

  - Subnet e relative associazioni al sito

  - Collegamenti al sito IP e relativi siti membri

  - Costi di collegamento al sito IP

  - Server di elenchi in linea in ciascun sito

  - Connessioni fisiche alla rete

  - Posizione dei firewall

Una volta creato uno schema per questi oggetti, pianificare il posizionamento dei server di Exchange. Per determinare il posizionamento dei server è necessario tenere presente quanto segue:

  - È necessario che un server Cassette postali comunichi direttamente con un server di catalogo globale per effettuare le ricerche in Active Directory.

  - È consigliabile distribuire più server Cassette postali in ciascun sito di Active Directory per il bilanciamento del carico e la tolleranza di errore.

  - Gruppi di disponibilità del database e resilienza del sito

  - Il servizio di messaggistica unificata sui server Cassette postali invia messaggi di posta vocale al servizio di trasporto sui server Cassette postali al fine di recapitarli alle cassette postali. Il server Accesso client in esecuzione nel servizio router di chiamata di messaggistica unificata può trovarsi in un sito hub o nei pressi di un gateway IP o VoIP, IP PBX (IP Private Branch eXchange), PBX abilitato al SIP o SBC (Session Border Controller). Il servizio di trasporto su un server Cassette postali che dispone della stessa appartenenza al sito del server Accesso client riceverà messaggi di posta vocale per il trasporto e indirizzerà i messaggi al servizio di trasporto su altri server Cassette postali all'interno dell'organizzazione.

  - I server Accesso client forniscono un punto di connettività all'organizzazione di Exchange per gli utenti che accedono a Exchange in modalità remota. Il server Accesso client deve essere distribuito in ogni sito di Active Directory che contiene i server Cassette postali.

Una volta pianificato il posizionamento di Exchange 2013, è possibile identificare le aree in cui modificare la topologia del sito Active Directory per migliorare il flusso delle comunicazioni. Per ottimizzare il recapito della posta, è possibile regolare i collegamenti al sito IP e i costi al collegamento del sito. In una topologia di Active Directory efficiente non è necessaria alcuna modifica per supportare Exchange 2013.


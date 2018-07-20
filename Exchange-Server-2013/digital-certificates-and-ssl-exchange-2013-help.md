---
title: 'Certificati digitali e SSL: Exchange 2013 Help'
TOCTitle: Certificati digitali e SSL
ms:assetid: a9e2e08c-d46a-4135-a387-eb653212b676
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351044(v=EXCHG.150)
ms:contentKeyID: 51407394
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Certificati digitali e SSL

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-08-26_

SSL (Secure Sockets Layer) è un metodo di protezione delle comunicazioni tra un client e un server. Per Exchange Server 2013, SSL viene utilizzato per assicurare comunicazioni protette tra il server e i client. I client consistono nei telefoni cellulari e nei computer interni o esterni alla rete di un'organizzazione.

Per impostazione predefinita, quando si installa Exchange 2013, le comunicazioni client vengono crittografate mediante SSL quando si utilizza Outlook Web App, Exchange ActiveSync e Outlook Anywhere.

SSL prevede l'utilizzo di certificati digitali. In questo argomento vengono riepilogati i diversi tipi di certificati digitali e le informazioni su come configurare Exchange 2013 per l'utilizzo di questi tipi di certificati digitali.

**Sommario**

Overview of digital certificates

Digital certificates and proxying

Digital certificates best practices

## Panoramica sui certificati digitali

I certificati digitali sono file elettronici che funzionano come password in linea in grado di verificare l'identità di un utente o di un computer. Vengono utilizzati per creare il canale SSL crittografato necessario per le comunicazioni client. Un certificato è una dichiarazione digitale emessa da un'Autorità di certificazione che si fa garante dell'identità del titolare del certificato e consente a terzi di comunicare in modo sicuro utilizzando la crittografia.

I certificati digitali eseguono le seguenti operazioni:

  - Garantiscono che i titolari, ossia persone, siti Web e anche risorse di rete come i router, siano effettivamente chi o cosa dichiarano di essere.

  - Proteggono i dati scambiati in linea da furti o alterazioni.

I certificati digitali possono essere rilasciati da una CA di terze parti attendibile o da un'infrastruttura a chiave pubblica (PKI, Public Key Infrastructure) di Windows mediante Servizi certificati, oppure possono essere autofirmati. Ogni tipo di certificato ha i suoi vantaggi e svantaggi. I certificati sono inalterabili e non possono essere contraffatti.

I certificati possono essere rilasciati per diversi usi. Tra questi sono compresi l'autenticazione utente Web, l'autenticazione server Web, S/MIME (Secure/Multipurpose Internet Mail Extensions), IPsec (Internet Protocol security), TLS (Transport Layer Security) e firma dei codici.

Un certificato contiene una chiave pubblica e la associa all'identità della persona, del computer o del servizio che possiede la chiave privata corrispondente. La chiave pubblica e quella privata sono utilizzate dal client e dal server per crittografare i dati prima di trasmetterli. Per utenti, computer e servizi basati su Windows, l'attendibilità di una CA viene stabilita quando c'è una copia del certificato radice nell'archivio certificati radice attendibili e il certificato contiene un percorso di certificazione valido. Perchè il certificato sia valido non deve essere stato revocato e il periodo di validità non deve essere scaduto.

## Tipi di certificati

Esistono tre tipi principali di certificati digitali: certificati autofirmati, certificati generati mediante PKI di Windows e certificati di terze parti.

## Certificati autofirmati

Quando si installa Exchange 2013, viene automaticamente configurato un certificato autofirmato sui server Cassette postali. Un certificato autofirmato viene firmato dall'applicazione che lo ha creato. L'oggetto e il nome del certificato corrispondono. L'autore e l'oggetto sono definiti nel certificato. Il certificato autofirmato viene utilizzato per crittografare le comunicazioni tra il server Accesso client e il server Cassette postali. Il server Accesso client ritiene attendibile il certificato autofirmato sul server Cassette postali automaticamente, per cui non è necessario alcun certificato di terze parti su tale server. Quando si installa Exchange 2013, viene creato un certificato autofirmato anche sul server Accesso client. Il certificato autofirmato consentirà ad alcuni protocolli client di utilizzare SSL per le comunicazioni. Exchange ActiveSync e Outlook Web App sono in grado di stabilire una connessione SSL utilizzando un certificato autofirmato. Outlook Anywhere non funzionerà con un certificato autofirmato sul server Accesso client. I certificati autofirmati devono essere copiati manualmente nell'archivio certificati radice attendibili sul dispositivo mobile o sul computer client. Quando un client si collega ad un server mediante SSL e il server presenta un certificato autofirmato, il client viene avvertito di verificare che il certificato sia stato rilasciato da un'autorità di certificazione attendibile. Il client deve ritenere attendibile l'autorità di certificazione. Se il client conferma l'attendibilità, le comunicazioni SSL possono continuare.


> [!NOTE]
> Per impostazione predefinita, il certificato originale installato sui server Cassette postali è un certificato autofirmato. Non è necessario sostituire il certificato autofirmato sui server Cassette postali dell'organizzazione con un certificato di terze parti attendibile. Il server Accesso client ritiene attendibile il certificato autofirmato sul server Cassette postali automaticamente e non è necessaria alcuna ulteriore configurazione per i certificati su tale server.



Frequentemente, le organizzazione di piccole di dimensioni decidono di non utilizzare un certificato di terza parte o di non installare la loro infrastruttura a chiave pubblica per emettere i propri certificati. Questa decisione è dovuta al fatto che tali soluzioni sono troppo costose, che i loro amministratori non dispongono dell'esperienza e delle conoscenze necessarie per creare una propria gerarchia di certificati o per entrambi i motivi. Quando si utilizzano certificati autofirmati, il costo è minimo e la configurazione è semplice. Tuttavia, stabilire un'infrastruttura per la gestione del ciclo di vita, il rinnovo, la gestione attendibile e la revoca dei certificati è molto più difficile con i certificati autofirmati.

## Certificati di infrastruttura a chiave pubblica di Windows

Il secondo tipo di certificato è un certificato generato da un'infrastruttura a chiave pubblica di Windows. Un'infrastruttura a chiave pubblica (PKI) è un sistema di certificati digitali, di Autorità di certificazione (CA) e di autorità di registrazione (RA) che verificano e autenticano la validità di ciascuna parte coinvolta in una transazione elettronica, utilizzando la crittografia a chiave pubblica. Quando si implementa una infrastruttura a chiave pubblica in un'organizzazione che utilizza Active Directory, si fornisce un'infrastruttura per la gestione del ciclo di vita, il rinnovo, la gestione attendibile e la revoca dei certificati. Tuttavia, la distribuzione di server e infrastrutture per creare e gestire certificati generati da un'infrastruttura a chiave pubblica di Windows, implica dei costi aggiuntivi.

I Servizi certificati sono necessari per distribuire un'infrastruttura a chiave pubblica di Windows e possono essere installati mediante l'opzione **Installazione applicazioni** del Pannello di controllo. È possibile installare Servizi certificati su qualsiasi server nel dominio.

Se si ottengono certificati da una CA di dominio basata su Windows, è possibile utilizzarla per richiedere o firmare certificati da emettere sui propri server o computer in rete. Ciò consente di utilizzare una PKI, simile all'utilizzo di un fornitore di certificati di terze parti ma meno costosa. Questi certificati PKI non possono essere distribuiti pubblicamente come altri tipi di certificati. Tuttavia, quando una CA di un PKI firma il certificato del richiedente utilizzando la chiave privata, il richiedente viene verificato. La chiave pubblica di questa CA è parte del certificato. Un server che ha questo certificato nell'archivio certificati radice attendibili può utilizzare la chiave pubblica per decrittografare il certificato del richiedente e autenticarlo.

I passaggi per distribuire un certificato generato dall'infrastruttura a chiave pubblica (PKI) sono simili ai passaggi necessari per la distribuzione di un certificato autofirmato. È sempre necessario installare una copia del certificato radice attendibile dalla PKI nell'archivio certificati radice attendibili dei computer o dei dispositivi mobili che si desidera predisporre per una connessione SSL a Microsoft Exchange.

Una PKI di Windows consente alle organizzazioni di pubblicare i propri certificati. I client possono richiedere e ricevere i certificati da una PKI di Windows sulla rete interna. La PKI di Windows può rinnovare o revocare certificati.

## Certificati di terze parti

I certificati di terze parti o commerciali sono certificati generati da una CA di terze parti o commerciale e acquistati dall'utente per l'utilizzo sui propri server di rete. Poiché i certificati autofirmati e quelli basati su PKI non sono automaticamente ritenuti attendibili dal dispositivo mobile o dal computer client, occorre accertarsi di importare il certificato nell'archivio certificati radice attendibili su computer e dispositivi client. I certificati di terze parti o commerciali non presentano questo problema. La maggior parte dei certificati CA commerciali sono già attendibili perché il certificato risiede già nell'archivio certificati radice attendibili. Poiché l'emittente è attendibile, lo sarà anche il certificato. L'utilizzo di certificati di terze parti semplifica molto la distribuzione.

Per organizzazioni più grandi o per organizzazione che devono distribuire i certificati pubblicamente, l'utilizzo di un certificato di terze parti o commerciale è la soluzione migliore, anche se esistono dei costi associati al certificato. I certificati commerciali potrebbero non essere la soluzione migliore per organizzazioni più piccole e di medie dimensioni e si può decidere di utilizzare le altre opzioni di certificato disponibili.

Inizio pagina

## Scelta del tipo di certificato

Al momento di scegliere il tipo di certificato da installare ci sono diversi fattori da prendere in considerazione. Per essere valido un certificato deve essere firmato. Può essere autofirmato o firmato da una CA. Un certificato autofirmato presenta delle limitazioni. Ad esempio, non tutti i dispositivi mobili permettono ad un utente di installare un certificato digitale nell'archivio certificati radice attendibili. La possibilità di installare certificati su dispositivi mobili dipende dal produttore del dispositivo o dal provider del servizio mobile. Alcuni produttori e provider di servizi mobili disabilitano l'accesso all'archivio certificati radice attendibili. In questo caso, né un certificato autofirmato né un un certificato proveniente da una CA di una PKI di Windows può essere installato sul dispositivo mobile.

## Certificati di Exchange predefiniti

Per impostazione predefinita, Exchange installa un certificato autofirmato sia sul server Accesso client che sul server Cassette postali in modo che tutte le comunicazioni di rete siano crittografate. La crittografia di tutta la comunicazione di rete richiede che ogni server Exchange abbia un certificato X.509 che possa utilizzare. È necessario sostituire questo certificato autofirmato sul server Accesso client con uno automaticamente considerato attendibile dai client.

Per certificato "autofirmato" si intende un certificato creato e firmato solo dal server Exchange stesso. Poiché non è stato creato e formato da una CA generalmente considerata attendibile, il certificato autofirmato predefinito non verrà considerato attendibile da alcun software ad eccezione di altri server Exchange della stessa organizzazione. Il certificato predefinito è abilitato per tutti i servizi di Exchange. Presenta un nome alternativo del soggetto (SAN, Subject Alternative Name) che corrisponde al nome del server Exchange su cui è installato. Presenta inoltre un elenco di SAN che includono sia il nome che server che il nome di dominio completo del server.

Sebbene altri server Exchange dell'organizzazione Exchange considerino attendibile questo certificato automaticamente, client quali Web browser, client Outlook, telefoni cellulari e altri client di posta elettronica oltre ai server di posta elettronica esterni non lo considerano attendibile automaticamente. Di conseguenza, valutare la sostituzione del certificato con un certificato di terze parti attendibile sui server Accesso client di Exchange. Se è presente una PKI interna e tutti i client considerano attendibile tale entità, è anche possibile utilizzare certificati emessi personalmente.

## Requisiti dei certificati in base al servizio

I certificati vengono utilizzati per diverse operazioni in Exchange. La maggior parte dei clienti, inoltre, utilizza i certificati su più server Exchange. In generale, minore è il numero di certificati, più semplice è la loro gestione.

## IIS

Tutti i servizi di Exchange seguenti utilizzano lo stesso certificato su un dato server Accesso client di Exchange:

  - Outlook Web App

  - Interfaccia di amministrazione di Exchange (EAC)

  - Servizi Web di Exchange

  - Exchange ActiveSync

  - Outlook via Internet

  - Individuazione automatica

  - Distribuzione Rubrica di Outlook

Poiché è possibile associare un solo certificato a un sito Web e poiché tutti questi servizi sono offerti per impostazione predefinita in un unico sito Web, tutti i nomi utilizzati dai client di questi servizi devono essere inclusi nel certificato (o rientrare in un nome con caratteri jolly nel certificato).

## POP/IMAP

I certificati utilizzati per POP o IMAP possono essere specificati separatamente dal certificato utilizzato per IIS. Tuttavia, per semplificare l'amministrazione, è consigliabile includere il nome del servizio POP o IMAP nel certificato IIS e utilizzare un unico certificato per tutti questi servizi.

## SMTP

È possibile utilizzare un certificato separato per ogni connettore di ricezione configurato. Il certificato deve includere il nome utilizzato dai client SMTP, o da altri server SMTP, per raggiungere tale connettore. Per semplificare la gestione dei certificati, valutare l'inclusione di tutti i nomi per i quali è necessario supportare il traffico TLS in un unico certificato.

## Certificati digitali e inoltro tramite proxy

L'inoltro tramite proxy è il metodo con cui un server invia le connessioni client a un altro server. Nel caso di Exchange 2013, ciò accade quando il server Accesso client inoltra tramite proxy una richiesta client in ingresso al server Cassette postali che contiene la copia attiva della cassetta postale del client.

Quando i server Accesso client inoltrano le richieste, SSL viene utilizzato per la crittografia ma non per l'autenticazione. Il certificato autofirmato sul server Cassette postali crittografa il traffico tra il server Accesso client e il server Cassette postali.

## Proxy inversi e certificati

Molte distribuzioni di Exchange utilizzano proxy inversi per pubblicare servizi Exchange su Internet. Tali proxy inversi possono essere configurati per terminare la crittografia SSL, esaminare il traffico in chiaro sul server e quindi aprire un nuovo canale di crittografia SSL dai server proxy inversi ai server Exchange dietro di essi. Questa procedura è nota come bridging SSL. Un altro modo per configurare i server proxy inverso è di consentire che le connessioni SSL passino attraverso i server Exchange dietro i server proxy inverso. Con entrambi i modelli di distribuzione, i client in Internet si connettono al server proxy inverso utilizzando un nome host per l'accesso a Exchange, ad esempio mail.contoso.com. Quindi il server proxy inverso si connette a Exchange utilizzando un nome host diverso, ad esempio il nome computer del server Accesso client Exchange. Non è necessario includere il nome computer del server Accesso client Exchange nel certificato poiché i server proxy inverso più comuni sono in grado di associare il nome host originale utilizzato dal client server al nome host interno del server Accesso client Exchange.

## SSL e DNS diviso

DNS diviso è una tecnologia che consente di configurare diversi indirizzi IP per lo stesso nome host, a seconda della provenienza della richiesta DNS di origine. È anche noto come "split-horizon DNS", "split-view DNS" o "split-brain DNS". DNS diviso consente di ridurre il numero di nomi host che è necessario gestire per Exchange consentendo ai client di connettersi a Exchange tramite lo stesso nome host, a prescindere che si connettano da Internet o dalla rete Intranet. DNS diviso consente alle richieste provenienti dalla rete Intranet di ricevere un indirizzo IP diverso rispetto alle richieste provenienti da Internet.

DNS diviso in genere non è necessario in distribuzioni di Exchange di piccole dimensioni poiché gli utenti possono accedere allo stesso endpoint DNS sia che provengano dalla rete Intranet che da Internet. Tuttavia, nelle distribuzioni più grandi, questa configurazione in un carico troppo elevato sul server proxy Internet in uscita e sul server proxy inverso. Per le distribuzioni più grandi, configurare il DNS diviso in modo che, ad esempio, gli utenti esterni accedano a mail.contoso.com e gli utenti interni accedano a internal.contoso.com. L'utilizzo di DNS diviso per questa configurazione assicura che gli utenti non debbano ricordare di utilizzare nomi host diversi a seconda della loro posizione.

## Windows PowerShell remoto

L'autenticazione Kerberos e la crittografia Kerberos sono utilizzate per l'accesso a Windows PowerShell remoto, sia dall'interfaccia di amministrazione di Exchange (EAC) che da Exchange Management Shell. Pertanto, non è necessario configurare i certificati SSL per l'uso con Windows Remote PowerShell remoto.

Inizio pagina

## Procedure consigliate per i certificati digitali

Sebbene la configurazione dei certificati digitali dell'organizzazione varia in base alle esigenze specifiche, sono state illustrate procedure consigliate per consentire di scegliere la configurazione dei certificati digitali migliore.

## Procedura consigliata: utilizzare un certificato di terza parte attendibile

Per impedire che i client ricevano errori relativi a certificati non attendibili, il certificato utilizzato dal server Exchange deve essere emesso da un'origine ritenuta attendibile dal client. Sebbene la maggior parte dei client possa essere configurata per ritenere attendibile qualsiasi certificato o emittente di certificato, è più semplice utilizzare un certificato di terza parte attendibile sul server Exchange. Infatti la maggior parte dei client ritiene già attendibili i rispettivi certificati radice. Vi sono diversi emittenti di certificati di terza parte che offrono certificati configurati in modo specifico per Exchange. È possibile utilizzare EAC per generare richieste di certificati che funzionino con la maggior parte degli emittenti di certificati.

## Come selezionare un'autorità di certificazione

Un'autorità di certificazione (CA) è una società che emette e assicura la validità dei certificati. Il software client (ad esempio, browser quali Microsoft Internet Explorer o sistemi operativi quali Windows o Mac OS) include un elenco incorporato di CA che ritiene attendibile. Questo elenco può essere in genere configurato per l'aggiunta e la rimozione di CA, ma tale configurazione è spesso difficoltosa. Adottare i criteri seguenti quando si seleziona una CA da cui acquistare certificati:

  - Assicurarsi che la CA sia ritenuta attendibile dal software client (sistemi operativi, browser e telefoni cellulari) che si connetterà ai server Exchange.

  - Scegliere una CA che dichiari di supportare "certificati per comunicazioni unificate" per l'utilizzo con il server Exchange.

  - Assicurarsi che la CA supporti il tipo di certificati che verranno utilizzati. Considerare l'utilizzo di certificati SAN (Subject Alternative Name). Non tutte le CA supportano i certificati SAN e altre CA non supportano molti nomi host che possono essere necessari.

  - Assicurarsi che la licenza che si acquista per i certificati consente di inserire il certificato nel numero di server che si intende utilizzare. Alcune CA consentono di inserire un solo certificato in un unico server.

  - Confrontare i prezzi dei certificati tra le CA.

## Procedura consigliata: utilizzare certificati SAN

A seconda di come si configurano i nomi dei servizi nell'implementazione di Exchange, il server Exchange potrebbe richiedere un certificato che rappresenta più nomi di dominio. Anche se è possibile risolvere il problema utilizzando un certificato con caratteri jolly come \*.contoso.com, molti clienti sono preoccupati per le implicazioni di sicurezza correlate all'utilizzo di un certificato che può essere utilizzato per qualunque sottodominio. Un'alternativa più sicura consiste nell'elencare ciascuno dei dominio richiesti come SAN nel certificato. Per impostazione predefinita, questo approccio viene utilizzato quando le richieste dei certificati vengono generate da Exchange.

## Procedura consigliata: utilizzare Gestione guidata certificati di Exchange per richiedere certificati

In Exchange sono presenti molti servizi che utilizzano certificati. Quando si richiede un certificati si commette spesso l'errore di non includere l'insieme di nomi di servizi corretto. Gestione guidata certificati nell'interfaccia di amministrazione di Exchange consente di includere l'elenco corretto di nomi nella richiesta del certificato. Questa procedura guidata consente di specificare con quali servizi il certificato deve funzionare e, in base ai servizi selezionati, include i nomi che è necessario siano presenti nel certificato affinché possa essere utilizzato con tali servizi. Eseguire Gestione guidata dei certificati dopo aver distribuito l'insieme iniziale di server Exchange 2013 e determinato quali nomi host utilizzare per i diversi servizi per la distribuzione. Teoricamente, sarebbe necessario eseguire la gestione guidata dei certificati una sola volta per ogni sito Active Directory in cui si distribuisce Exchange.

Anziché preoccuparsi di non dimenticare un nome host nell'elenco di SAN del certificato che si acquista, è possibile utilizzare un'autorità di certificazione che offra, gratuitamente, un periodo di tolleranza durante il quale è possibile restituire un certificato e richiedere lo stesso nuovo certificato con alcuni nomi host aggiuntivi.

## Procedura consigliata: utilizzare il minor numero di nomi host possibile

Oltre a utilizzare il minor numero di certificati possibile, è opportuno utilizzare il minor numero di nomi host possibile. In questo modo è possibile risparmiare sui costi. Molti provider di certificati addebitano una tariffa in base al numero di nomi host che si aggiungono al certificato.

L'operazione più importante che è possibile effettuare per ridurre il numero di nomi host necessari e, pertanto, la complessità della gestione dei certificati, consiste nel non includere singoli nomi host di server nei nomi alternativi del soggetto del certificato.

I nomi host che è necessario includere nei certificati Exchange sono i nomi host utilizzati dalle applicazioni client per connettersi a Exchange. Di seguito è riportato un elenco di nomi host tipici che sarebbero richiesti per una società denominata Contoso:

  - **Mail.contoso.com**   Questo nome host copre la maggior parte delle connessioni a Exchange, incluse MicrosoftOutlook, Outlook Web App, Outlook Anywhere, Rubrica offline, Servizi Web di Exchange, POP3, IMAP4, SMTP, Pannello di controllo di Exchange e ActiveSync.

  - **Autodiscover.contoso.com**   Questo nome host è utilizzato per i client che supportano l'individuazione automatica, inclusi i client Microsoft Office Outlook 2007 e versioni successive, Exchange ActiveSync e Servizi Web di Exchange.

  - **Legacy.contoso.com**   Questo nome host è richiesto in uno scenario di coesistenza con Exchange 2007 e Exchange 2013. Se saranno presenti client con cassette postali su Exchange 2007 e Exchange 2013, la configurazione di un nome host legacy evita agli utenti di dover apprendere un secondo URL durante il processo di aggiornamento.

## Informazioni sui certificati con caratteri jolly

Un certificato con caratteri jolly è progettato per supportare un dominio e più sottodomini. Ad esempio, la configurazione di un certificato con carattere jolly per \*.contoso.com ha come risultato un certificato utile per mail.contoso.com, web.contoso.com e autodiscover.contoso.com.

Inizio pagina


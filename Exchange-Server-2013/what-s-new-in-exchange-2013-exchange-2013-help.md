---
title: 'Novità di Exchange 2013: Exchange 2013 Help'
TOCTitle: Novità di Exchange 2013
ms:assetid: 97501135-2149-4590-8373-98e638ac8eb1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150540(v=EXCHG.150)
ms:contentKeyID: 50481229
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Novità di Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile scoprire tutte le nuove funzionalità in Exchange 2013.

Microsoft Exchange Server 2013 aggiunge una ricca serie di tecnologie, funzionalità e servizi alla linea di prodotti Exchange Server. Il suo obiettivo è sostenere persone e organizzazioni mentre le relative abitudini lavorative si evolvono dalla comunicazione alla collaborazione. Nello stesso tempo, Exchange Server 2013 aiuta a ridurre il costo totale di proprietà se Exchange 2013 viene distribuito in locale o se le cassette postali vengono sottoposte a provisioning nel cloud. Le nuove funzionalità di Exchange 2013 sono progettate per:

  - **Supportare una forza lavoro multigenerazionale**   L'integrazione sociale e la semplificazione della ricerca dei contatti sono importanti per gli utenti. La *ricerca avanzata* apprende dal comportamento di comunicazione e collaborazione degli utenti per migliorare e definire la priorità dei risultati della ricerca in Exchange. Inoltre, con Exchange 2013, gli utenti possono unire i contatti da più origini per ottenere una singola visualizzazione di una persona, collegando le informazioni sul contatto estratte da molteplici posizioni.

  - **Fornire un'esperienza coinvolgente**   Microsoft Outlook 2013 e Microsoft Outlook Web App hanno un aspetto totalmente nuovo. Outlook Web App pone l'accento su un'interfaccia utente semplificata che supporta anche l'uso del tocco, migliorando l'esperienza dei dispositivi mobili con Exchange.

  - **Integrare con SharePoint e Lync**   Exchange 2013 offre un'integrazione superiore con Microsoft SharePoint 2013 e Microsoft Lync 2013 attraverso le cassette postali del sito e In-Place eDiscovery. Insieme, questi prodotti offrono un ventaglio di funzionalità che supportano l'eDiscovery aziendale e la collaborazione tramite l'utilizzo delle cassette postali del sito.

  - **Soddisfare requisiti di conformità in continua evoluzione** Conformità ed eDiscovery rappresentano una sfida per molte organizzazioni. Exchange 2013 consente di cercare e trovare dati non solo in Exchange ma nell'intera organizzazione. Grazie alla ricerca e all'indicizzazione migliorate, è possibile eseguire ricerche in Exchange 2013, Lync 2013, SharePoint 2013 e nei file server Windows. Inoltre, la prevenzione della perdita di dati (DLP) può aiutare a proteggere l'organizzazione da utenti che, per errore, inviano informazioni riservate a persone non autorizzate. DLP aiuta a identificare, monitorare e proteggere i dati sensibili attraverso un'analisi approfondita del contenuto.

  - **Offrire una soluzione resiliente**   Exchange 2013 si basa sull'architettura di Exchange Server 2010 ed è stato riprogettato per facilitare il ridimensionamento, l'utilizzo dell'hardware e l'isolamento degli errori.

Per informazioni sulle modifiche apportate alla versione RTM (Release To Manufacturing) di Exchange Server 2013, vedere [Aggiornamenti per Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

Consultare le sezioni di seguito per ulteriori informazioni sulle novità in Exchange 2013:

Interfaccia di amministrazione di Exchange

Architettura di Exchange 2013

Installazione

Criteri di messaggistica e conformità

Protezione anti-malware

Flusso di posta

Destinatari

Condivisione e collaborazione

Integrazione con SharePoint e Lync

Client e dispositivi mobili

Messaggistica unificata

Spostamenti in batch delle cassette postali

[Disponibilità elevata e resilienza del sito](high-availability-and-site-resilience-exchange-2013-help.md)

Gestione del carico di lavoro di Exchange


> [!NOTE]
> Per informazioni sulle funzionalità delle precedenti versioni di Exchange che sono state rimosse, interrotte o sostituite in Exchange Server 2013, vedere <A href="what-s-discontinued-in-exchange-2013-exchange-2013-help.md">Funzionalità sospese in Exchange 2013</A>. Si potrebbe essere interessati anche a <A href="release-notes-for-exchange-2013-exchange-2013-help.md">Note sulla versione di Exchange 2013</A>.



## Interfaccia di amministrazione di Exchange

Exchange 2013 offre una singola console di gestione unificata pensata per la facilità di utilizzo e ottimizzata per la gestione di distribuzioni ibride locali, online o ibride. *Interfaccia di amministrazione di Exchange* (EAC) in Exchange 2013 sostituisce Exchange Management Console (EMC) e il Pannello di controllo di Exchange (ECP) di Exchange 2010. "ECP" è comunque ancora utilizzato come nome della directory virtuale impiegata da EAC. Di seguito sono presentate alcune funzionalità di EAC:

  - **Visualizzazione elenco**   La visualizzazione elenco in EAC è stata progettata per rimuovere le limitazioni esistenti in ECP. ECP limitava la visualizzazione a 500 oggetti e, se si desiderava visualizzare gli oggetti non riportati nel riquadro dei dettagli, si doveva ricorrere alla ricerca e al filtraggio per trovare quegli oggetti specifici. In Exchange 2013, il limite visualizzabile nell'elenco EAC è di circa 20.000 oggetti. Dopo la restituzione dei risultati, il client EAC esegue la ricerca e l'ordinamento, migliorando notevolmente le prestazioni rispetto a ECP in Exchange 2010. Inoltre, è stato aggiunto il paging per poter sfogliare i risultati. È inoltre possibile configurare la dimensione della pagina ed eseguire l'esportazione in un file CSV.

  - **Aggiungere/rimuovere colonne nella visualizzazione Elenco destinatari**   È possibile scegliere quali colonne visualizzare e, grazie ai cookie locali, salvare le visualizzazioni elenco personalizzate sul computer utilizzato per accedere a EAC.

  - **Proteggere la directory virtuale ECP**   È possibile partizionare l'accesso da Internet e intranet dall'interno della directory virtuale IIS di ECP per consentire o negare le funzionalità di gestione. Con questa funzionalità è possibile concedere o negare l'accesso agli utenti che tentano di accedere a EAC da Internet esternamente all'ambiente dell'organizzazione, pur consentendo l'accesso alle opzioni di Outlook Web App di un utente finale.

  - **Gestione di cartelle pubbliche**   In Exchange 2010 e Exchange 2007, le cartelle pubbliche erano gestite tramite la console di amministrazione delle cartelle pubbliche. Le cartelle pubbliche ora sono in Interfaccia di amministrazione di Exchange e non serve uno strumento a parte per gestirle.

  - **Notifiche**   In Exchange 2013, l'interfaccia di amministrazione di Exchange ora comprende un visualizzatore di notifiche per visualizzare lo stato dei processi di lunga durata e, se lo si desidera, è possibile ricevere la notifica con un messaggio di posta elettronica al completamento del processo.

  - **Editor utente controllo di accesso basato sui ruoli (RBAC)**   In Exchange 2010, è possibile utilizzare Editor utente controllo di accesso basato sui ruoli (RBAC) nella Casella degli strumenti di Exchange per aggiungere utenti ai gruppi di ruoli di gestione. In Exchange 2013, la funzionalità Editor utente controllo di accesso basato sui ruoli (RBAC) è ora presente in EAC e non necessita di uno strumento separato per la gestione di RBAC.

  - **Strumenti di messaggistica unificata**   In Exchange 2010, è possibile utilizzare gli strumenti Statistiche chiamate e Registri chiamate utente per fornire statistiche e informazioni di messaggistica unificata sulle specifiche chiamate per un utente abilitato alla messaggistica unificata. In Exchange 2013, gli strumenti Statistiche chiamate e Registri chiamate utente sono ora presenti in EAC e non necessitano di uno strumento separato per la gestione.

  - **Miglioramenti relativi ai gruppi**   L'interfaccia di amministrazione di Exchange (EAC) è ora in grado di visualizzare fino a 10.000 destinatari nella finestra **GruppiSeleziona membri**. Per impostazione predefinita, fino a 500 destinatari vengono restituiti quando si apre la finestra **Seleziona membri**. Tuttavia, l'utente può scegliere di visualizzare fino a 10.000 destinatari facendo clic su **Visualizza tutti i risultat** sotto l'elenco dei destinatari. È ora supportata la ricerca di oltre 500 destinatari tramite la barra di scorrimento e sono state aggiunte funzionalità di ricerca migliorate per consentire all'utente di filtrare i destinatari visualizzati nell'elenco. È possibile filtrare in base a:
    
      - città
    
      - azienda
    
      - paese
    
      - reparto
    
      - ufficio
    
      - ruolo

Per ulteriori informazioni, vedere [Interfaccia di amministrazione di Exchange in Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md).

## Architettura di Exchange 2013

Le versioni precedenti di Exchange erano ottimizzate e architettate con i vincoli tecnologici esistenti all'epoca. Ad esempio, durante lo sviluppo di Exchange 2007, uno dei vincoli principali riguardava le prestazioni della CPU. Per mitigare tale vincolo, Exchange 2007 era diviso in diversi ruoli del server che consentivano la scalabilità attraverso la separazione dei server. Tuttavia, i ruoli del server in Exchange 2007 ed Exchange 2010 erano strettamente collegati. Il collegamento dei ruoli presentava diversi svantaggi, quali la dipendenza dalla versione, la geoaffinità (che richiedeva la presenza di tutti i ruoli in un sito specifico), l'affinità di sessione (che richiedeva un costoso bilanciamento del carico hardware sullo strato 7) e la complessità degli spazi dei nomi.

Oggi, la potenza delle CPU è notevolmente meno costosa e non rappresenta più un fattore vincolante. Una volta rimosso tale vincolo, gli obiettivi di progettazione principali di Exchange 2013 sono divenuti la facilità del ridimensionamento, l'utilizzo dell'hardware e l'isolamento degli errori. In Exchange 2013 il numero di ruoli del server è stato ridotto a tre: i ruoli dei server Accesso client, Cassette postali e Trasporto Edge.

Il server Cassette postali include tutti i componenti server tradizionali presenti in Exchange 2010: protocolli di Accesso client, servizi di trasporto, database delle cassette postali e messaggistica unificata. Il server Cassette postali gestisce tutta l'attività per le cassette postali attive su quel server. Il server Accesso client fornisce l'autenticazione, il reindirizzamento limitato e i servizi proxy. Il server Accesso Client non esegue alcun rendering dei dati. Il server Accesso Client è un thin server senza stato. Non vi sono mai oggetti in coda o archiviati sul server Accesso client. Il server Accesso client include tutti i protocolli di accesso client normalmente disponibili: HTTP, POP e IMAP, SMTP.

Con questa nuova architettura, il server Accesso client e il server Cassette postali sono divenuti "liberamente collegati". L'elaborazione e l'attività di una specifica cassetta postale avvengono sul server Cassette postali che ospita la copia attiva del database in cui risiede la cassetta postale. Tutto il rendering e la trasformazione dei dati vengono eseguiti in locale sulla copia attiva del database, eliminando i problemi di compatibilità tra le versioni dei server Accesso client e Cassette postali.

Con Exchange 2013 Service Pack 1, è stato introdotto nuovamente il ruolo del server Trasporto Edge. In genere, il ruolo Trasporto Edge viene distribuito nella propria rete perimetrale, all'esterno della foresta Active Directory interna e ha lo scopo di ridurre al minimo la superficie di attacco della distribuzione di Exchange. Grazie alla gestione di tutto il flusso di posta per Internet, aggiunge anche ulteriori strati di protezione dei messaggi da virus e spam. Inoltre, può applicare le regole di trasporto al controllo del flusso dei messaggi. Per ulteriori informazioni sul ruolo del server Edge Transport, vedere [Server Trasporto Edge](edge-transport-servers-exchange-2013-help.md).

L'architettura di Exchange 2013 garantisce i seguenti vantaggi:

  - **Flessibilità di aggiornamento della versione**   Non esistono più requisiti di aggiornamento rigorosi. Un server Accesso client può essere aggiornato in maniera indipendente rispetto a un server Cassette postali.

  - **Indifferenza di sessione**   In Exchange 2010, era richiesta l'affinità di sessione al ruolo del server Accesso client per diversi protocolli. In Exchange 2013, i componenti Accesso client e Cassette postali sono installati sullo stesso server Cassette postali. Visto che il server Accesso client esegue il proxy di tutte le connessioni per un utente a un server Cassette postali specifico, non è richiesta l'affinità di sessione nei server Accesso client. Questo consente di bilanciare le connessioni in ingresso ai server Accesso client utilizzando tecniche fornite dalla tecnologia di bilanciamento del carico, come la connessione minima o il round robin.

  - **Semplicità di distribuzione**   Con una progettazione con resilienza del sito di Exchange 2010 erano necessari otto spazi dei nomi diversi: due spazi dei nomi Internet Protocol, due per il fallback di Outlook Web App, uno per l'individuazione automatica, due per Accesso client RPC e uno per SMTP. Era inoltre richiesto uno spazio dei nomi legacy se si eseguiva l'aggiornamento da Exchange 2003 o Exchange 2007. In Exchange 2013 il numero minimo di spazi dei nomi è stato ridotto a due. Se è in atto la coesistenza con Exchange 2007, è ancora necessario creare un nome host legacy, mentre per la coesistenza con Exchange 2010 o se si installa una nuova organizzazione di Exchange 2013, il numero minimo di spazi dei nomi necessari è due: uno per i protocolli client e uno per l'individuazione automatica. Potrebbe anche essere necessario uno spazio dei nomi SMTP.

Queste modifiche all'architettura hanno comportato dei cambiamenti nella connettività client. In primo luogo, RPC non è più un protocollo di accesso diretto supportato. Significa che la connettività di Outlook deve avvenire tramite RPC su HTTP (detto anche Outlook via Internet). A prima vista questa potrebbe sembrare una limitazione, ma in realtà fornisce alcuni vantaggi aggiuntivi. Il vantaggio più ovvio è che non è necessario avere il servizio Accesso client RPC sul server Accesso client. Si riduce così a due il numero di spazi dei nomi normalmente richiesti per una soluzione con resilienza del sito. Inoltre, non esiste più il requisito di fornire l'affinità per il servizio Accesso client RPC.

In secondo luogo, i client Outlook non si connettono più a un nome di dominio completo (FQDN) di server come facevano nelle precedenti versioni di Exchange. Outlook utilizza l'individuazione automatica per creare un nuovo punto di connessione costituito dal GUID della cassetta postale, dal simbolo @ e dalla parte del dominio dell'indirizzo SMTP primario dell'utente. Questa semplice modifica rende meno probabile la visualizzazione agli utenti del temuto messaggio "L'amministratore ha apportato una modifica alla cassetta postale dell'utente. Si prega di riavviare." In Exchange 2013 sono supportati solo Outlook 2007 e versioni successive.

Il modello di disponibilità elevata del componente cassetta postale non è cambiato significativamente da Exchange 2010. L'unità della disponibilità elevata è ancora il gruppo di disponibilità del database. Il gruppo di disponibilità del database utilizza ancora il clustering di failover di Windows Server. La replica continua supporta ancora la replica sia in modalità file sia in modalità blocco. Tuttavia, sono stati apportati alcuni miglioramenti. I tempi di failover sono stati ridotti grazie ai miglioramenti al codice di log delle transazioni e a un punto di controllo più approfondito sui database passivi. Il servizio Archivio di Exchange è stato riscritto in codice gestito (vedere la sezione "Archivio gestito" più avanti in questo argomento). Ora ogni database viene eseguito con il proprio processo, consentendo l'isolamento dei problemi dell'archivio in un singolo database.

## Archivio gestito

In Exchange 2013, *Archivio gestito* è il nuovo nome dei processi di Archivio informazioni riscritti da zero, Microsoft.Exchange.Store.Service.exe e Microsoft.Exchange.Store.Worker.exe. Il nuovo Archivio gestito è scritto in C\# ed è strettamente integrato con il servizio di replica di Microsoft Exchange (MSExchangeRepl.exe) per fornire maggiore disponibilità grazie a una resilienza migliorata. Inoltre, l'Archivio gestito è stato architettato per consentire una gestione più precisa del consumo delle risorse e un'analisi delle cause più rapida attraverso una diagnostica migliorata.

L'Archivio gestito collabora con il servizio di replica di Microsoft Exchange per gestire i database delle cassette postali, continuando a utilizzare Extensible Storage Engine (ESE) come motore di database. Exchange 2013 include importanti cambiamenti allo schema del database delle cassette postali, garantendo diverse ottimizzazioni rispetto alle precedenti versioni di Exchange. Oltre a queste modifiche, il servizio Replica di Microsoft Exchange è responsabile di tutta la disponibilità dei servizi relativi ai server Cassette postali. Le modifiche architettoniche permettono un failover del database più rapido e una migliore gestione degli errori sul disco fisico.

L'Archivio gestito è inoltre integrato con il motore di ricerca Search Foundation (lo stesso utilizzato da SharePoint 2013) per offrire indicizzazioni e ricerche più solide rispetto al motore di ricerca Microsoft nelle versioni precedenti di Exchange.

Per ulteriori informazioni, vedere [Disponibilità elevata e resilienza del sito](high-availability-and-site-resilience-exchange-2013-help.md).

## Gestione dei certificati

La gestione dei certificati digitali è una delle attività di sicurezza più importanti per l'organizzazione di Exchange. Configurare correttamente i certificati è fondamentale per offrire un'infrastruttura di messaggistica sicura all'organizzazione. In Exchange 2010, Exchange Management Console era il mezzo primario per la gestione dei certificati. In Exchange 2013, la funzionalità di gestione dei certificati è fornita in Interfaccia di amministrazione di Exchange, la nuova interfaccia utente dell'amministratore di Exchange 2013.

Il lavoro in Exchange 2013 relativo ai certificati è incentrato sulla riduzione del numero dei certificati che un amministratore deve gestire, sulla riduzione delle interazioni dell'amministratore con i certificati e sulla possibilità di gestire i certificati da una posizione centrale. I vantaggi derivanti dai cambiamenti nella gestione dei certificati sono i seguenti:

  - La gestione dei certificati può essere eseguita sul server Accesso client e sul server Cassette postali. Sul server Cassette postali è installato per impostazione predefinita un certificato autofirmato. Il server Accesso client ritiene automaticamente attendibile il certificato autofirmato sul server Cassette postali di Exchange 2013, in modo che i client non ricevano l'avviso su un certificato autofirmato non considerato attendibile, purché il server Accesso client di Exchange 2013 disponga di un certificato non autofirmato di un'Autorità di certificazione di Windows o di terze parti ritenute attendibili.

  - Nelle versioni precedenti di Exchange era difficile vedere quando un certificato digitale era prossimo alla scadenza. In Exchange 2013, il centro Notifiche visualizza avvisi quando un certificato archiviato su un server di Exchange 2013 sta per scadere. Gli amministratori possono anche scegliere di ricevere queste notifiche tramite posta elettronica.

Per ulteriori informazioni, vedere [Certificati digitali e SSL](digital-certificates-and-ssl-exchange-2013-help.md).

## Installazione

L'installazione è stata completamente riscritta, in modo da facilitare più che mai l'installazione di Exchange 2013 e la verifica della disponibilità di tutti gli aggiornamenti cumulativi e della protezione più recenti. Ecco alcuni dei miglioramenti apportati:

  - **Installazione sempre aggiornata**   Durante l'esecuzione dell'installazione guidata, viene offerta la possibilità di scaricare e utilizzare gli ultimi aggiornamenti cumulativi dei prodotti, gli aggiornamenti della protezione e i Language Pack. Questa opzione non aggiorna solamente i file utilizzati per eseguire Exchange, ma anche l'installazione stessa. Questa modalità consente di migliorare continuamente l'installazione anche dopo il rilascio e di includere e aggiornare i controlli di conformità quando i requisiti cambiano o vengono aggiornati.
    
    Se si sta utilizzando la modalità di installazione automatica, non è possibile scaricare automaticamente gli aggiornamenti. Tuttavia, è ancora possibile eseguire l'ultima versione dell'installazione scaricando preventivamente gli aggiornamenti e utilizzando il parametro `/UpdatesDir: <path>` per consentire all'installazione di aggiornarsi prima dell'inizio del processo.

  - **Controlli di conformità migliorati**   I controlli di conformità assicurano che il computer e l'organizzazione siano pronti per Exchange 2013. Dopo aver fornito le informazioni necessarie sull'installazione, prima dell'inizio dell'installazione stessa vengono eseguiti i controlli di conformità. Il nuovo motore di controllo della conformità ora esegue tutti i controlli prima di segnalare le azioni da eseguire per consentire il proseguimento dell'installazione; questa operazione viene inoltre eseguita più velocemente che in passato. Come per le precedenti versioni di Exchange, è possibile comunicare all'installazione di installare le funzionalità di Windows richieste, in modo che non sia necessario installarle manualmente.

  - **Procedura guidata moderna e semplificata**   Sono stati rimossi tutti i passaggi dell'installazione guidata che non sono assolutamente richiesti per installare Exchange. Ciò che resta è una procedura guidata facile da seguire, che consente di svolgere il processo di installazione un passo alla volta.

Per ulteriori informazioni, vedere [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md).

## Criteri di messaggistica e conformità

In Exchange 2013 sono disponibili due nuove funzionalità relative ai criteri dei messaggi e alla conformità: Data loss prevention e il connettore Microsoft Rights Management.

Le funzionalità *Data loss prevention* (DLP) consentono di proteggere i dati sensibili e informare gli utenti sui criteri di conformità interni. DLP contribuisce inoltre a proteggere l'organizzazione dall'invio involontario di informazioni riservate a persone non autorizzate. DLP aiuta a identificare, monitorare e proteggere i dati sensibili attraverso un'analisi approfondita del contenuto. Exchange 2013 offre criteri DLP integrati basati su standard di regolamentazione quali informazioni personali (PII) e standard di protezione dei dati dell'industria delle carte di pagamento (PCI); è inoltre estendibile per supportare altri criteri importanti per il business. Inoltre, i nuovi Suggerimenti criteri in Outlook 2013 informano gli utenti sulle violazioni dei criteri prima dell'invio dei dati sensibili.

Il connettore Microsoft Rights Management (RMS) è un'applicazione facoltativa che aumenta la protezione dei dati del server Exchange 2013 eseguendo la connessione ai servizi Microsoft Rights Management basati su cloud. Una volta installato, il connettore RMS assicura una protezione costante per l'intero ciclo di vita dei dati. I servizi sono personalizzabili, in modo da consentire agli utenti di definire il livello di protezione più adatto alle specifiche necessità. È possibile, ad esempio, limitare a specifici utenti l'accesso ai messaggi di posta elettronica o impostare i diritti di sola lettura per particolari messaggi.

Per ulteriori informazioni su queste funzionalità, vedere:

[Prevenzione della perdita di dati](https://docs.microsoft.com/it-it/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[Connettore Rights Management](https://go.microsoft.com/fwlink/p/?linkid=330432)

## Archiviazione sul posto, conservazione ed eDiscovery

Exchange 2013 include i seguenti miglioramenti all'archiviazione sul posto, alla conservazione e all'eDiscovery per aiutare l'organizzazione a rispettare i requisiti di conformità:

  - **Archiviazione sul posto**   Archiviazione sul posto è un nuovo modello di conservazione unificato che aiuta a rispettare i requisiti di conservazione a fini giudiziari negli scenari riportati di seguito:
    
      - Mantenere i risultati della query (conservazione basata su query), che consente l'immutabilità a livello di ambito tra le cassette postali.
    
      - Inserire una conservazione basata sul tempo per soddisfare i requisiti di mantenimento (ad esempio, mantenere tutti gli elementi in una cassetta postale per sette anni, uno scenario che richiedeva l'utilizzo del ripristino di un singolo elemento/mantenimento degli elementi eliminati in Exchange 2010).
    
      - Inserire una cassetta postale per l'archiviazione illimitata (analogamente alla conservazione per controversia legale in Exchange 2010).
    
      - Inserire un utente in più archiviazioni per gestire requisiti diversi.

  - **In-Place eDiscovery**   In-Place eDiscovery consente agli utenti autorizzati di cercare i dati delle cassette postali in tutte le cassette postali e negli archivi sul posto in un'organizzazione di Exchange 2013 e di copiare i messaggi in una cassetta postale di individuazione per la revisione. In Exchange 2013, In-Place eDiscovery è stato migliorato per consentire ai manager dell'individuazione di eseguire le ricerche e la conservazione con maggiore efficienza. Questi miglioramenti includono:
    
      - La **ricerca federata** consente di cercare e conservare i dati in più repository. In Exchange 2013, è possibile eseguire ricerche eDiscovery sul posto in Exchange, SharePoint 2013 e Lync 2013. È possibile utilizzare Centro eDiscovery in SharePoint 2013 per eseguire la ricerca e la conservazione In-Place eDiscovery.
    
      - L'**archiviazione sul posto basata su query** consente di salvare i risultati della query, consentendo l'immutabilità a livello di ambito tra le cassette postali.
    
      - **Esportazione dei risultati della ricerca**   I manager dell'individuazione possono esportare il contenuto delle cassette postali in un file PST da SharePoint 2013 eDiscovery Console. I cmdlet di richiesta di esportazione delle cassette postali non sono più necessari per esportare una cassetta postale in un file PST.
    
      - **Statistiche delle parole chiave**   Le statistiche di ricerca sono proposte in base ai termini di ricerca. In questo modo un manager dell'individuazione può prendere rapidamente decisioni intelligenti sul perfezionamento della query di ricerca per ottenere risultati migliori. I risultati della ricerca eDiscovery sono ordinati per pertinenza.
    
      - **Sintassi KQL**   I responsabili dell'individuazione possono utilizzare la sintassi KQL (Keyword Query Language) nelle query di ricerca. KQL è simile a Sintassi di ricerca avanzata, utilizzato per le ricerche di individuazione in Exchange 2010.
    
      - **Procedura guidata In-Place eDiscovery and Hold**   I manager dell'individuazione possono utilizzare la nuova procedura guidata In-Place eDiscovery and Hold per eseguire le operazioni di eDiscovery e conservazione.
        

        > [!NOTE]
        > Se SharePoint 2013 non è disponibile, un sottoinsieme delle funzionalità eDiscovery è disponibile in Interfaccia di amministrazione di Exchange.



  - **Ricerca tra cassette postali principali e di archiviazione in Outlook Web App**   Gli utenti possono cercare nelle loro cassette postali principali e di archiviazione in Outlook Web App. Non sono più necessarie due ricerche separate.

  - **Archiviazione del contenuto Lync**   Exchange 2013 supporta l'archiviazione del contenuto Lync 2013 nella cassetta postale di un utente. È possibile inserire il contenuto Lync nell'archiviazione utilizzando Archiviazione sul posto, per poi utilizzare In-Place eDiscovery per cercare il contenuto Lync archiviato in Exchange.

  - **Criteri di conservazione**   I criteri di conservazione aiutano l'organizzazione a ridurre i rischi associati alla posta elettronica e ad altre comunicazioni; soddisfano inoltre i requisiti di conservazione della posta elettronica. I criteri di conservazione includono i seguenti miglioramenti:
    
      - **Supporto per i tag di conservazione Calendario e Attività**   È possibile creare tag dei criteri di conservazione per le cartelle predefinite Calendario e Attività in modo da far scadere gli elementi in queste cartelle. Gli elementi nelle cartelle vengono spostati nell'archivio dell'utente in base alle impostazioni dei criteri di archiviazione applicati alla cassetta postale.
    
      - **Capacità migliorata di conservare gli elementi per un periodo specificato**   È possibile utilizzare i tag di conservazione e un'archiviazione sul posto basata sul tempo per imporre la conservazione degli elementi per un periodo stabilito.

Per ulteriori informazioni, vedere [Criteri di messaggistica e conformità](messaging-policy-and-compliance-exchange-2013-help.md).

## Regole di trasporto

Le regole di trasporto in Exchange Server 2013 sono una prosecuzione delle funzionalità disponibili in Exchange Server 2010. Tuttavia, sono stati apportati diversi miglioramenti alle regole di trasporto in Exchange 2013. Il cambiamento più importante è il supporto per la prevenzione della perdita di dati (DLP). Esistono inoltre nuovi predicati e azioni, il monitoraggio avanzato e alcune modifiche architettoniche.

Per ulteriori informazioni, vedere [Novità delle regole di trasporto](what-s-new-for-transport-rules-exchange-2013-help.md).

## Information Rights Management

Information Rights Management (IRM) è compatibile con Cryptographic Mode 2, una modalità di crittografia di Active Directory Rights Management Services (AD RMS) che supporta una crittografia avanzata consentendo l'utilizzo di chiavi a 2048 bit per RSA e chiavi a 256 bit per SHA-1. Inoltre, la modalità 2 consente di utilizzare l'algoritmo di hashing SHA-2. Per ulteriori informazioni sulle modalità di crittografia in AD RMS, vedere [Modalità di crittografia di AD RMS](https://go.microsoft.com/fwlink/p/?linkid=263219).

## Controllo

Exchange 2013 include i seguenti miglioramenti del controllo:

  - **Rapporti di controllo**   EAC include funzionalità di controllo che consentono di eseguire rapporti o di esportare voci dal log di controllo della cassetta postale e da quello dell'amministratore. Nel registro di controllo della cassetta postale viene registrato ogni accesso a una cassetta postale da parte di un utente diverso dal proprietario della cassetta stessa. In questo modo è possibile determinare chi ha effettuato l'accesso a una casetta postale e quali operazioni ha eseguito. Il log di controllo dell'amministratore registra qualsiasi azione, in base a un cmdlet di Exchange Management Shell, eseguita da un amministratore. In questo modo è possibile risolvere problemi di configurazione o individuare la causa di problemi relativi alla sicurezza o alla conformità. Per ulteriori informazioni, vedere [Rapporti di controllo di Exchange](exchange-auditing-reports-exchange-2013-help.md).

  - **Visualizzazione del registro di controllo dell'amministratore**   Invece di esportare il registro di controllo dell'amministratore, in meno di 24 ore è possibile riceverlo in un messaggio di posta elettronica e visualizzarne le voci nell'interfaccia di amministrazione di Exchange. A tale scopo, andare a **Gestione della conformità** \> **Controllo**, quindi fare clic su **Visualizza il registro di controllo dell'amministratore**. Saranno visualizzate fino a 1000 voci, su più pagine. Per restringere la ricerca è possibile specificare un intervallo di date. Per ulteriori informazioni, vedere [Visualizzare il registro di controllo dell'amministratore](https://docs.microsoft.com/it-it/exchange/security-and-compliance/exchange-auditing-reports/view-administrator-audit-log).

## Protezione anti-malware

Le capacità di filtraggio anti-malware predefinite di Exchange 2013 aiutano a proteggere la rete dal software dannoso trasferito tramite i messaggi di posta elettronica. Tutti i messaggi inviati o ricevuti dal server di Exchange vengono analizzati alla ricerca di malware (virus e spyware). Se viene rilevato del malware, il messaggio viene eliminato. Quando un messaggio infetto viene eliminato e non recapitato, è possibile inviare notifiche ai mittenti o agli amministratori. È inoltre possibile scegliere di sostituire gli allegati infetti con messaggi predefiniti o personalizzati che avvisano i destinatari del rilevamento del malware.

Per ulteriori informazioni sulla protezione anti-malware, vedere [Protezione antimalware](anti-malware-protection-exchange-2013-help.md).

## Flusso di posta

Il flusso di posta dei messaggi in un'organizzazione e le azioni eseguite su tali messaggi sono notevolmente cambiati in Exchange 2013. Di seguito è riportata una breve descrizione delle modifiche:

  - **Pipeline di trasporto**   La pipeline di trasporto in Exchange 2013 è ora costituita da diversi servizi: il servizio Trasporto front-end sui server Accesso client, il servizio Trasporto sui server Cassette postali e il servizio Trasporto cassette postali sui server Cassette postali. Per ulteriori informazioni, vedere [Flusso di posta](mail-flow-exchange-2013-help.md).

  - **Routing**   Il routing della posta elettronica in Exchange 2013 riconosce i limiti dei gruppi di disponibilità del database e i limiti del sito Active Directory. Inoltre, il routing della posta elettronica è stato migliorato per accodare più direttamente i messaggi per i destinatari interni. Per ulteriori informazioni, vedere [Routing della posta](mail-routing-exchange-2013-help.md).

  - **Connettori**   La dimensione massima dei messaggi predefinita per un connettore di invio o di ricezione, specificata dal parametro *MaxMessageSize*, è stata elevata da 10 MB a 25 MB. Per ulteriori informazioni sull'impostazione dei parametri su un connettore, vedere [Set-SendConnector](https://technet.microsoft.com/it-it/library/aa998294\(v=exchg.150\)) e [Set-ReceiveConnector](https://technet.microsoft.com/it-it/library/bb125140\(v=exchg.150\)).
    
    È possibile impostare un connettore di invio nel servizio Trasporto di un server Cassette postali per instradare la posta in uscita attraverso un server Trasporto front-end nel sito Active Directory locale, per mezzo del parametro *FrontEndProxyEnabled* del cmdlet **Set-SendConnector**, consolidando la modalità di routing della posta elettronica applicata dal servizio Trasporto.

  - **Trasporto Edge**   È possibile installare (in modo facoltativo) un server Trasporto Edge nella propria rete perimetrale per ridurre la superficie di attacco e fornire protezione e sicurezza ai messaggi. Per altre informazioni, vedere [Server Trasporto Edge](edge-transport-servers-exchange-2013-help.md).

## Destinatari

In questa sezione sono descritti i miglioramenti alla gestione dei destinatari in Exchange 2013:

  - **Criteri di denominazione dei gruppi**   Gli amministratori ora possono utilizzare EAC per creare un *criterio di denominazione dei gruppi*, che consente di standardizzare e gestire i nomi dei gruppi di distribuzione creati dagli utenti nell'organizzazione. È possibile richiedere un prefisso e un suffisso specifici da aggiungere al nome per il gruppo di distribuzione al momento della creazione e bloccare l'utilizzo di parole specifiche. Questa funzionalità aiuta a ridurre l'utilizzo di parole inadatte nei nomi di gruppo.
    
    Per ulteriori informazioni, vedere [Creare un gruppo di distribuzione dei criteri di denominazione](https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy).

  - **Verifica dei messaggi**   Gli amministratori possono utilizzare EAC per verificare le informazioni sul recapito dei messaggi di posta elettronica inviati o ricevuti dagli utenti nell'organizzazione. È sufficiente selezionare una cassetta postale e cercare i messaggi inviati o ricevuti da un altro utente. È possibile limitare la ricerca cercando parole specifiche nella riga dell'oggetto. Con il rapporto di recapito risultante è possibile tenere traccia di un messaggio durante il processo di recapito e specificare se il messaggio è stato recapitato correttamente, è in sospeso o non è stato recapitato.
    
    Per ulteriori informazioni, vedere [Tenere traccia dei messaggi con i rapporti di recapito](track-messages-with-delivery-reports-exchange-2013-help.md).

## Condivisione e collaborazione

In questa sezione sono descritti i miglioramenti alla condivisione e alla collaborazione in Exchange 2013:

  - **Cartelle pubbliche**   Le cartelle pubbliche ora sfruttano la disponibilità elevata esistente e le tecnologie dell'archivio cassette postali. L'architettura delle cartelle pubbliche utilizza cassette postali speciali per archiviare sia la gerarchia sia il contenuto della cartella pubblica. Il nuovo design implica anche che non è più disponibile un database delle cartelle pubbliche. La replica delle cartelle pubbliche ora utilizza il modello di replica continua. La disponibilità elevata della gerarchia e le cassette postali del contenuto sono fornite dal gruppo di disponibilità del database (DAG). Con questo design si passa da un modello di replica multimaster a un modello di replica a master singolo.
    
    Gli utenti di Outlook Web App dell'organizzazione ora hanno la possibilità di aggiungere le cartelle pubbliche ai Preferiti oppure di rimuoverle. In precedenza, questa operazione era possibile solo in Outlook.
    
    Per ulteriori informazioni, vedere [Cartelle pubbliche](public-folders-exchange-2013-help.md).

  - **Cassette postali del sito**   La posta elettronica e i documenti sono per tradizione conservati in due repository dati univoci e separati. La maggior parte dei team collabora generalmente utilizzando entrambi i supporti. La difficoltà è dovuta al fatto che alla posta elettronica e ai documenti si accede utilizzando due client diversi, che solitamente causano una riduzione della produttività degli utenti e un'esperienza utente peggiore.
    
    La *cassetta postale del sito* è un nuovo concetto di Exchange 2013 che tenta di risolvere questi problemi. Le cassette postali del sito migliorano la collaborazione e la produttività degli utenti consentendo l'accesso sia ai documenti in un sito SharePoint sia ai messaggio di posta elettronica in Outlook 2013 utilizzando la stessa interfaccia client. Una cassetta postale del sito è una funzionalità composta dall'appartenenza a un sito SharePoint (proprietari e membri), dall'archiviazione condivisa tramite una cassetta postale Exchange per i messaggi di posta elettronica e da un sito SharePoint per i documenti, e da un'interfaccia di gestione che si occupa delle esigenze del provisioning e del ciclo di vita.
    
    Per ulteriori informazioni, vedere [Cassette postali del sito](site-mailboxes-exchange-2013-help.md).

  - **Cassette postali condivise**   Nelle precedenti versioni di Exchange, la creazione di una cassetta postale condivisa era un processo in più passaggi in cui occorreva utilizzare Exchange Management Shell per impostare le autorizzazioni di delega. In Exchange 2013, è possibile creare una cassetta postale condivisa in un passaggio utilizzando Interfaccia di amministrazione di Exchange. In EAC, selezionare **Destinatari** \> **Cassette postali condivise** per creare una cassetta postale condivisa. La cassetta postale condivisa è ora un tipo di destinatario, quindi è possibile cercare facilmente le cassette postali condivise sia nell'interfaccia utente sia utilizzando Shell.
    
    Per ulteriori informazioni, vedere [Cassette postali condivise](shared-mailboxes-exchange-2013-help.md).

## Integrazione con SharePoint e Lync

Exchange 2013 offre una maggiore integrazione con SharePoint 2013 e Lync 2013. I vantaggi di questa integrazione avanzata includono:

  - Exchange 2013 si integra con SharePoint 2013 per consentire agli utenti di collaborare in maniera più efficace utilizzando le cassette postali del sito.

  - Lync Server 2013 può archiviare il contenuto in Exchange 2013 e utilizzare Exchange 2013 come archivio dei contatti.

  - I manager dell'individuazione possono eseguire ricerche In-Place eDiscovery e di archiviazione sul posto in SharePoint 2013, Exchange 2013 e Lync 2013.

  - L'autenticazione Oauth consente alle applicazioni partner di autenticarsi come un servizio o di rappresentare gli utenti quando necessario.

Per ulteriori informazioni, vedere [Integrazione con SharePoint e Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md).

## Client e dispositivi mobili

L'interfaccia utente di Outlook Web App è nuova e ottimizzata per tablet e smartphone, oltre che per computer desktop e portatili. Le nuove funzionalità includono le app per Outlook, che permettono a utenti e amministratori di estendere le capacità di Outlook Web App; il collegamento dei contatti, vale a dire la possibilità per gli utenti di aggiungere contatti dai loro account LinkedIn; gli aggiornamenti all'aspetto e alle funzionalità del Calendario.

Per ulteriori informazioni, vedere [Novità per Outlook Web App in Exchange 2013](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md).

## Messaggistica unificata

La messaggistica unificata in Exchange 2013 contiene essenzialmente le stesse funzionalità di segreteria telefonica incluse in Exchange 2010. Tuttavia, sono state aggiunge funzionalità e caratteristiche nuove e migliorate. In particolare, le modifiche architettoniche alla messaggistica unificata di Exchange 2013 hanno portato alla divisione tra i ruoli del server Accesso client e Messaggistica unificata di Exchange 2013 i componenti, i servizi e le funzionalità che erano inclusi nel ruolo del server Messaggistica unificata in Exchange 2010.

Per ulteriori dettagli, vedere [Novità per la messaggistica unificata di Exchange 2013](what-s-new-for-unified-messaging-in-exchange-2013-exchange-2013-help.md).

## Spostamenti in batch delle cassette postali

Exchange 2013 introduce il concetto di spostamenti in batch. La nuova architettura di spostamento è creata sulla base degli spostamenti del servizio di replica delle cassette postali (MRS) con capacità di gestione avanzate. La nuova architettura di spostamento in batch dispone dei seguenti miglioramenti:

  - Capacità di spostare più cassette postali in grandi batch.

  - Notifica di posta elettronica durante lo spostamento con creazione di un rapporto.

  - Ripetizione e prioritizzazione automatiche degli spostamenti.

  - Le cassette postali di archiviazione principali e personali possono essere spostate insieme o separatamente.

  - Opzione per la finalizzazione della richiesta di spostamento manuale, che consente di rivedere lo spostamento prima di completarlo.

  - Sincronizzazioni incrementali periodiche per eseguire la migrazione delle modifiche.

Per ulteriori informazioni, vedere [Gestire spostamenti locali](manage-on-premises-moves-exchange-2013-help.md).

## Disponibilità elevata e resilienza del sito

Exchange 2013 utilizza i gruppi di disponibilità del database e le copie del database delle cassette postali, insieme ad altre funzionalità come il recupero di un singolo elemento, i criteri di conservazione e le copie del database isolate, per fornire la disponibilità elevata, la resilienza del sito e la protezione dati nativa di Exchange. La piattaforma a disponibilità elevata, l'Archivio informazioni di Exchange ed Extensible Storage Engine (ESE) sono stati migliorati per fornire maggiore disponibilità, una gestione più semplice e ridurre i costi. Questi miglioramenti includono:

  - **Disponibilità gestita**   Con la disponibilità gestita, le funzionalità di monitoraggio interno e orientate al ripristino sono strettamente integrate per aiutare a prevenire gli errori, ripristinare i servizi in maniera proattiva e avviare automaticamente il failover dei server o avvisare gli amministratori affinché compiano un'azione. Il focus si concentra sul monitoraggio e sulla gestione dell'esperienza dell'utente finale piuttosto che sui tempi di attività del server e dei componenti per mantenere il servizio sempre disponibile.

  - **Archivio gestito**   Archivio gestito è il nome dei processi di Archivio informazioni riscritti da zero in Exchange 2013. Il nuovo Managed Store è scritto in C\# ed è strettamente integrato con il Servizio di replica di Microsoft Exchange (MSExchangeRepl.exe) per fornire maggiore disponibilità grazie a una resilienza migliorata.

  - **Supporto di più database per disco**   Exchange 2013 include miglioramenti che consentono di supportare più database (insiemi di copie attive e passive) sullo stesso disco, sfruttando dischi più grandi in termini di capacità e IOPS con la massima efficienza possibile.

  - **Reseeding automatico**   Consente di ripristinare rapidamente la ridondanza dei database dopo un errore del disco. Se un disco è in errore, la copia del database archiviata su quel disco viene copiata dalla copia del database attiva a un disco di riserva sullo stesso server. Se nel disco danneggiato sono state archiviate più copie di database, possono essere sottoposte automaticamente a reseeding su un disco di riserva. In questo modo si accelera il reseeding poiché è probabile che i database attivi si trovino su più server e i dati vengano copiati in parallelo.

  - **Ripristino automatico dagli errori di archiviazione**   Questa funzionalità prosegue le innovazioni introdotte in Exchange 2010 per consentire il ripristino del sistema in caso di errori che agiscono sulla resilienza o sulla ridondanza. Oltre ai comportamenti di controllo dei bug in Exchange 2010, Exchange 2013 include comportamenti di ripristino aggiuntivi per tempi di I/O elevati, consumo di memoria eccessivo da parte di MSExchangeRepl.exe e casi gravi in cui il sistema è in uno stato che non consente nemmeno di pianificare i thread.

  - **Miglioramenti delle copie isolate**   Le copie isolate ora possono prendersi cura di se stesse entro certi limiti grazie all'esecuzione automatica del log. Le copie isolate ignoreranno automaticamente i file di registro in numerose situazioni, come negli scenari di ripristino della pagina singola e con spazio su disco insufficiente. Se il sistema rileva che l'applicazione di patch alla pagina è necessaria per una copia isolata, i registri verranno riprodotti automaticamente nella copia isolata per eseguire l'applicazione di patch alla pagina. Le copie isolate richiameranno inoltre la funzione di riproduzione automatica al raggiungimento della soglia di spazio insufficiente su disco e al rilevamento della copia isolata come unica disponibile per un periodo di tempo specifico. Le copie isolate possono anche sfruttare la rete sicura semplificando così il recupero o l'attivazione. *Safety Net* è una funzionalità migliorata di Exchange 2013 che si basa sul dumpster di trasporto di Exchange 2010.

  - **Miglioramenti all'avviso per copia singola**   L'avviso per copia singola introdotto in Exchange 2010 non è più uno script pianificato separato. Ora è integrato nei componenti di disponibilità gestita nel sistema ed è una funzione nativa di Exchange.

  - **Configurazione automatica della rete del gruppo di disponibilità del database**   Le reti dei gruppi di disponibilità del database possono essere configurate automaticamente dal sistema in base alle impostazioni di configurazione. Oltre alle opzioni di configurazione manuale, i DAG possono distinguere le reti della replica da quelle MAPI e configurare automaticamente le reti DAG.

Per ulteriori informazioni su queste funzionalità, vedere [Disponibilità elevata e resilienza del sito](high-availability-and-site-resilience-exchange-2013-help.md) e [Modifiche alla disponibilità elevata e resilienza sul sito rispetto le versioni precedenti](changes-to-high-availability-and-site-resilience-over-previous-versions-exchange-2013-help.md).

## Gestione del carico di lavoro di Exchange

Un carico di lavoro di Exchange è una funzionalità, un protocollo o un servizio di Exchange Server esplicitamente definito allo scopo di gestire le risorse di sistema di Exchange. Ciascun carico di lavoro di Exchange consuma risorse di sistema quali CPU, operazioni del database delle cassette postali o richieste di Active Directory per eseguire le richieste utente o operazioni in background. Alcuni esempi di carico di lavoro di Exchange sono Outlook Web App, Exchange ActiveSync, la migrazione delle cassette postali e gli assistenti cassette postali.

Esistono due modi per gestire i carichi di lavoro di Exchange in Exchange 2013:

  - **Monitorare l'integrità delle risorse di sistema**   La gestione dei carichi di lavoro in base all'integrità delle risorse di sistema è una novità di Exchange 2013.

  - **Controllare come vengono consumate le risorse dai singoli utenti**   Il controllo del consumo delle risorse da parte dei singoli utenti era già possibile in Exchange 2010 (dove era chiamato limitazione delle richieste utente); questa capacità è stata migliorata in Exchange 2013.

Per ulteriori informazioni su tali funzionalità, vedere [Gestione del carico di lavoro di Exchange](exchange-workload-management-exchange-2013-help.md).


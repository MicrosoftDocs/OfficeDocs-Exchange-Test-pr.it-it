---
title: 'Inserimento nel journal: Exchange 2013 Help'
TOCTitle: Inserimento nel journal
ms:assetid: 6a20f207-4485-44ef-b010-ec760eb5165b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998649(v=EXCHG.150)
ms:contentKeyID: 50480898
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Inserimento nel journal

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

La creazione del journal consente alle organizzazioni di soddisfare i requisiti di conformità legale, normativa e organizzativa registrando le comunicazioni di posta elettronica in entrata e in uscita. Quando si pianifica un sistema per garantire la conservazione e la conformità dei messaggi, è fondamentale avere ben chiaro il concetto di creazione di un journal e capire come adattarlo ai criteri di conformità dell'organizzazione e in che modo Microsoft Exchange Server 2013 può essere utile per proteggere i messaggi inseriti nel journal.

**Sommario**

Why journaling is important

Journaling agent

Journal rules

Journal rule replication

Journal reports

Interoperability with Exchange 2010 and Exchange 2007

Troubleshooting

## Importanza dell'inserimento nel journal

Per prima cosa è importante comprendere la differenza tra l'inserimento nel journal e una strategia di archiviazione dei dati:

  - L'*inserimento nel journal* consente di registrare tutte le comunicazioni di un'organizzazione, incluse le comunicazioni di posta elettronica, per utilizzarle nella strategia di mantenimento o archiviazione della posta elettronica dell'organizzazione stessa. Per soddisfare il numero sempre crescente di requisiti normativi e di conformità, numerose organizzazioni devono tenere traccia delle comunicazioni effettuate dai dipendenti durante le normali attività aziendali.

  - L'*archiviazione dei dati* esegue il backup dei dati, li rimuove dall'ambiente nativo e li memorizza in un altro percorso, riducendo così il sovraccarico causato dalla conservazione dei dati. L'inserimento nel journal di Exchange può quindi essere utilizzato come uno strumento della strategia di conservazione o archiviazione della posta elettronica.

Sebbene l'inserimento nel journal possa non essere richiesto da alcuna normativa specifica, questa operazione potrebbe consentire di conformarsi ai termini di alcune normative. Ad esempio, in alcuni settori finanziari i dirigenti aziendali potrebbero essere ritenuti responsabili delle richieste effettuate ai clienti dai propri dipendenti. Per verificare che le dichiarazioni siano accurate, un funzionario aziendale può impostare un sistema in cui i dirigenti possono regolarmente controllare una parte delle comunicazioni tra i dipendenti e i clienti. Ogni trimestre i dirigenti verificano e approvano la condotta dei propri dipendenti. Dopo che tutti i dirigenti hanno segnalato tale approvazione al funzionario aziendale, quest'ultimo segnala la conformità, per conto dell'azienda, all'organo di controllo. In questo esempio, i messaggi di posta elettronica potrebbero rappresentare un tipo di comunicazione tra i dipendenti e i clienti che il dirigente deve controllare; pertanto, è possibile decidere di inserire nel journal tutti i messaggi di posta elettronica inviati dai dipendenti che gestiscono le comunicazioni con i clienti. Altri meccanismi di comunicazione con i clienti potrebbero includere i fax e le conversazioni telefoniche, a loro volta essere soggetti a specifiche normative. La capacità di inserire nel journal tutte le classi di dati di un'azienda è una parte importante dell'architettura IT.

Il seguente elenco contiene alcune tra le più importanti normative statunitensi e internazioni che vedono nell'inserimento dei dati nel journal un utile strumento nell'ambito della strategia di conformità:

  - Sarbanes-Oxley Act del 2002 (SOX)

  - Security Exchange Commission Rule 17a-4 (SEC Rule 17 A-4)

  - National Association of Securities Dealers 3010 & 3110 (NASD 3010 & 3110)

  - Gramm-Leach-Bliley Act (Financial Modernization Act)

  - Financial Institution Privacy Protection Act del 2001

  - Financial Institution Privacy Protection Act del 2003

  - Health Insurance Portability and Accountability Act del 1996 (HIPAA)

  - Uniting and Strengthening America by Providing Appropriate Tools Required to Intercept and Obstruct Terrorism Act del 2001 (Patriot Act)

  - European Union Data Protection Directive (EUDPD)

  - Japan's Personal Information Protection Act

Inizio pagina

## agente di journaling

In un'organizzazione Exchange 2013, tutto il traffico di posta elettronica viene instradato dai server Cassette postali. Tutti i messaggi attraversano almeno un server che utilizza il servizio di Trasporto nel loro percorso. L'*agente di journaling* è un agente di trasporto che, avendo come principale obiettivo la conformità, elabora i messaggi sui server Cassette postali. Si attiva in concomitanza con gli eventi di trasporto **OnSubmittedMessage** e **OnRoutedMessage**.


> [!NOTE]
> In Exchange 2013, l'agente di journaling è incorporato. Gli agenti integrati non sono inclusi nell'elenco degli agenti restituiti dal cmdlet <STRONG>Get-TransportAgent</STRONG>. Per ulteriori dettagli, vedere <A href="transport-agents-exchange-2013-help.md">Agenti di trasporto</A>.



Exchange 2013 fornisce le seguenti opzioni di inserimento nel journal:

  - **Inserimento standard nel journal**   L'inserimento standard è configurato su un database delle cassette postali. Consente all'agente di journaling di inserire nel journal tutti i messaggi inviati da e a cassette postali che si trovano in uno specifico database. Per poter inserire nel journal tutti i messaggi inviati e ricevuti, è necessario configurare l'inserimento su tutti i database delle cassette postali su tutti i server Cassette postali nell'organizzazione.

  - **Inserimento avanzato nel journal**   L'inserimento avanzata consente all'agente di journaling di eseguire un'operazione più granulare utilizzando le regole del journal. Invece di inserire nel journal tutte le cassette postali presenti su un database, è possibile configurare delle regole del journal in base alle esigenze della propria organizzazione, così da inserire, ad esempio, singoli destinatari o membri dei gruppi di distribuzione. Per utilizzare l'inserimento avanzato, è necessario disporre della licenza CAL (Client Access License) di Exchange Enterprise.

Quando si abilita l'inserimento standard su un database delle cassette postali, queste informazioni vengono salvate in Active Directory e lette dall'agente di journaling. Analogamente, anche le regole del journal configurate con l'inserimento nel journal avanzato vengono salvate in Active Directory e applicate dall'agente di journaling. Per ulteriori informazioni su come configurare l'inserimento nel journal standard e l'inserimento nel journal avanzato, vedere [Gestire l'inserimento nel journal](https://docs.microsoft.com/it-it/exchange/security-and-compliance/journaling/manage-journaling).

Inizio pagina

## Regole del journal

Di seguito sono riportati gli aspetti chiave delle regole del journal:

  - **Ambito delle regole del journal**   Definisce quali messaggi vengono inseriti nel journal dall'agente di journaling.

  - **Destinatario journal**   Specifica l'indirizzo SMTP del destinatario da inserire nel journal.

  - **Cassetta del journaling**   Specifica una o più cassette postali utilizzate per la raccolta dei rapporti del journal.

## Ambito delle regole del journal

È possibile utilizzare una regola del journal per inserire nel journal solo messaggi interni, solo messaggi esterni o entrambi. Di seguito vengono descritti questi ambiti:

  - **Solo messaggi interni**   Le regole del journal il cui ambito è impostato sull'inserimento nel journal dei messaggi interni inviati tra destinatari all'interno dell'organizzazione Exchange.

  - **Solo messaggi esterni**   Le regole del journal il cui ambito è impostato sull'inserimento nel journal dei messaggi esterni inviati a destinatari o ricevuti da mittenti esterni all'organizzazione Exchange.

  - **Tutti i messaggi**   Le regole del journal il cui ambito è impostato sull'inserimento nel journal di tutti i messaggi che passano all'interno dell'organizzazione indipendentemente dall'origine o dalla destinazione. In questo ambito sono inclusi i messaggi che possono essere già stati elaborati dalle regole del journal negli ambiti interno ed esterno.

## Destinatario journal

È possibile implementare le regole di inserimento nel journal specificando l'indirizzo SMTP del destinatario journal. Il destinatario può essere una cassetta postale, un gruppo di distribuzione, un utente di posta elettronica o un contatto di Exchange. Questi destinatari potrebbero essere soggetti a requisiti normativi oppure coinvolti in procedimenti legali in cui i messaggi di posta elettronica o altre comunicazioni vengono raccolti come prove. Scegliendo destinatari o gruppi di destinatari specifici, è possibile configurare facilmente un ambiente di inserimento nel journal che soddisfi i processi e i requisiti legali e normativi dell'organizzazione. Scegliendo solo i destinatari specifici che devono essere inseriti nel journal è inoltre possibile ridurre i costi di archiviazione e gli altri costi associati alla conservazione di grandi volumi di dati.

Tutti i messaggi inviati agli o dagli utenti specificati in una regola del journal vengono inseriti nel journal. Se si specifica un gruppo di distribuzione come destinatario del journal, tutti i messaggi inviati a e provenienti da membri del gruppo di distribuzione vengono inseriti nel journal. Se non si specifica un destinatario da inserire nel journal, tutti i messaggi inviati o ricevuti dai destinatari che corrispondono all'ambito della regola verranno inseriti nel journal.

**Destinatari del journal abilitati alla messaggistica unificata**

Molte organizzazioni che implementano l'inserimento nel journal possono inoltre utilizzare la messaggistica unificata per consolidare l'infrastruttura di posta elettronica, posta vocale e fax. Tuttavia, si potrebbe preferire che il processo di inserimento nel journal non generi rapporti del journal per i messaggi generati dalla messaggistica unificata. In questo caso, è possibile scegliere se inserire nel journal i messaggi vocali e i messaggi di notifica di chiamata senza risposta gestiti da un server di Exchange che utilizza il servizio di messaggistica unificata oppure scegliere di ignorare tali messaggi. Se l'organizzazione non richiede l'inserimento nel journal di questi messaggi, è possibile ridurre la quantità di spazio su disco rigido necessario per l'archiviazione dei rapporti del journal ignorando questi messaggi.


> [!NOTE]
> I messaggi contenenti fax generati da un servizio di messaggistica unificata vengono sempre inseriti nel journal, anche se si disabilita l'inserimento nel journal dei messaggi di notifica di chiamata senza risposta e dei messaggi vocali della messaggistica unificata.



Per ulteriori informazioni su come abilitare o disabilitare i messaggi vocali e i messaggi di notifica delle chiamate senza risposta, vedere [Disabilitare o abilitare l'inserimento nel journal dei messaggi vocali e delle notifiche di chiamata](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md).

## Cassetta del journaling

La cassetta del journaling viene utilizzata per raccogliere i report del journal. La modalità di configurazione della cassetta del journaling dipende dai criteri e dai requisiti legali e normativi dell'organizzazione. È possibile specificare una cassetta del journaling in cui raccogliere i messaggi per tutte le regole del journal configurate nell'organizzazione oppure utilizzare diverse cassette del journaling per regole o gruppi di regole del journal differenti.


> [!IMPORTANT]
> Non è possibile designare una cassetta postale di Office 365 come cassetta del journaling. È possibile recapitare i report del journal al sistema di archiviazione locale o a un servizio di archiviazione di terze parti. Se si esegue una distribuzione ibrida con cassette postali suddivise tra server locali e Office 365, è possibile scegliere una cassetta postale locale come cassetta del journaling per le cassette postali locali e di Office 365.




> [!IMPORTANT]
> Le cassette postali per l'inserimento nel journal contengono informazioni molto riservate. È necessario proteggere le cassette postali di inserimento nel journal poiché raccolgono messaggi inviati a e da destinatari nell'organizzazione. Questi messaggi possono fare parte di procedimenti legali o possono essere soggetti a requisiti normativi. Numerose leggi richiedono che i messaggi non vengano alterati prima di essere inviati all'autorità investigativa. Si consiglia di creare all'interno dell'organizzazione dei criteri per la determinazione degli utenti autorizzati ad accedere alle cassette postali per l'inserimento nel journal, limitando l'accesso solo agli utenti che ne abbiano effettiva necessità. Inoltre, si consiglia di rivolgersi ai propri rappresentanti legali per assicurarsi che la soluzione di inserimento nel journal adottata sia conforme alle leggi e alle normative applicabili all'organizzazione.




> [!IMPORTANT]
> Le cassette postali dell'inserimento nel journal devono accettare i messaggi fino a una dimensione uguale o maggiore rispetto alla dimensione massima dei messaggi che è configurato nell'organizzazione. Se è stato configurato eccezioni ai MaxSendSize e MaxReceiveSize sulla cassetta postale di un singolo utente di dimensioni maggiori delle impostazioni generali di TransportConfig, è necessario impostare MaxSendSize cassetta del journaling e MaxReceiveSize conseguenza per garantire che i messaggi inviati all'inserimento nel journal vengono accettati e non viene inserito in coda o rifiutati. Messaggi rifiutati dal cassetta del journaling verranno ritentati periodicamente, causando spreco di risorse e la crescita del database non necessari. Inoltre, è consigliabile impostare una cassetta del journaling alternativa per evitare che altri casi non recapitabile non si verificherà.



## Cassetta del journaling alternativa

Quando la cassetta del journaling non è disponibile, è possibile impedire che i rapporti del journal non recapitati vengano raccolti in code di posta elettronica nei server Cassette postali. configurare una cassetta postale per l'inserimento nel journal alternativa per la memorizzazione di tali rapporti. La cassetta postale alternativa per l'inserimento nel journal riceve i rapporti del journal come allegati ai rapporti di mancato recapito generati quando la cassetta postale per l'inserimento nel journal, o il server che la contiene, rifiuta di recapitare il rapporto o non è più disponibile.

Quando la cassetta del journaling diventa nuovamente disponibile, è possibile utilizzare la funzionalità **Rinvia** di Office Outlook per inviare nuovamente i rapporti del journal da recapitare alla cassetta postale.

Se si configura una cassetta del journaling alternativa, tutti i rapporti del journal rifiutati o non recapitati nell'intera organizzazione Exchange vengono recapitati alla cassetta del journaling alternativa. Di conseguenza, è importante assicurarsi che la cassetta postale per l'inserimento nel journal alternativa e il server Cassette postali che la contiene possano supportare molti rapporti del journal.


> [!WARNING]
> Una volta configurata una cassetta del journaling alternativa, è necessario monitorare la cassetta postale per assicurarsi che sia sempre disponibile contemporaneamente alle cassette del journaling. Se la cassetta postale per l'inserimento nel journal alternativa diventa non disponibile o nello stesso tempo rifiuta i rapporti del journal, tali rapporti andranno persi e non potranno essere recuperati.



Poiché la cassetta del journaling alternativa raccoglie tutti i rapporti del journal rifiutati per l'intera organizzazione Exchange, è necessario assicurarsi che l'operazione sia conforme alle leggi e alle normative applicabili all'organizzazione. Se determinate legge o normative vietano all'organizzazione di archiviare rapporti del journal inviati a cassette postali per l'inserimento nel journal diverse nella stessa cassetta postale alternativa, la configurazione di una cassetta postale per l'inserimento nel journal alternativa potrebbe non essere consentita. Rivolgersi ai propri rappresentanti legali per sapere se è possibile utilizzare una cassetta postale per l'inserimento nel journal alternativa.

Quando si configura una cassetta postale per l'inserimento nel journal alternativa, è opportuno utilizzare gli stessi criteri utilizzati per configurare la cassetta postale per l'inserimento nel journal.


> [!IMPORTANT]
> La cassetta del journaling alternativa deve essere trattata come una speciale cassetta postale dedicata. Eventuali messaggi indirizzati direttamente a questa cassetta non vengono inseriti nel journal.



Inizio pagina

## Replica delle regole del journal

Le regole del journal vengono archiviate in Active Directory e applicate da tutti i server Cassette postali dell'organizzazione Exchange 2013. Quando si crea, si modifica o si elimina una regola del journal, la modifica viene replicata su tutti i server Active Directory dell'organizzazione. Tutti i server Cassette postali dell'organizzazione recuperano la configurazione aggiornata delle regole del journal dai server di Active Directory e applicano le regole nuove o modificate.

Replicando tutte le regole del journal all'interno dell'organizzazione, Exchange 2013 consente di fornire all'organizzazione una serie coerente di regole del journal. Tutti i messaggi che passano attraverso l'organizzazione Exchange 2013 sono soggetti alle stesse regole del journal.


> [!IMPORTANT]
> Dipende dalla replica Active Directory è la replica delle regole del journal in un'organizzazione. Tempo di replica tra i controller di dominio Active Directory varia a seconda del numero di siti all'interno dell'organizzazione e la velocità dei collegamenti e altri fattori all'esterno del controllo di Microsoft Exchange. Prendere in considerazione dei ritardi di replica quando si implementano le regole del journal nell'organizzazione. Per ulteriori informazioni sulla replica Active Directory, vedere <A href="https://go.microsoft.com/fwlink/?linkid=274904">Introduzione alla replica di Active Directory e alla topologia di gestione utilizzando Windows PowerShell</A>.




> [!IMPORTANT]
> Ogni server Cassette postali inserisce nella cache l'appartenenza a gruppi di distribuzione per evitare tempi di andata e ritorno ripetuti per Active Directory. La cache dei gruppi espansi riduce il numero di richieste che ogni server Cassette postali deve eseguire su un controller di dominio di Active Directory. Per impostazione predefinita, le voci nella cache dei gruppi espansi scadono dopo quattro ore. Pertanto, se si specifica un gruppo di distribuzione come destinatario journal, le modifiche apportate all'appartenenza a gruppi di distribuzione potrebbero non essere applicate alle regole del journal fino a quando la cache dei gruppi espansi non viene aggiornata. Per forzare un aggiornamento immediato della cache del destinatario, è necessario arrestare e avviare il servizio di trasporto di Microsoft Exchange. È necessario fare questo per ciascun server Cassette postali su cui si desidera forzare l'aggiornamento della cache del destinatario.



Inizio pagina

## Rapporti del journal

Il *rapporto del journal* è il messaggio generato dall'agente di journaling quando un messaggio è conforme a una regola del journal e deve essere inviato alla cassetta del journal. Il messaggio originale conforme alla regola del journal viene incluso inalterato come allegato al rapporto del journal. Il corpo del rapporto del journal contiene le informazioni ricavate dal messaggio originale, quali l'indirizzo di posta elettronica del mittente, l'oggetto, l'ID messaggio e gli indirizzi di posta elettronica dei destinatari. Questo sistema è anche detto "inserimento nel journal degli allegati" ed è l'unico metodo di inserimento nel journal supportato da Exchange 2013.

## Rapporti del journal e messaggi protetti da IRM

Quando si implementa l'inserimento nel journal in un ambiente Exchange 2013, è necessario tenere conto dei rapporti del journal e i messaggi protetti da IRM. I messaggi protetti da IRM influenzano le funzionalità di ricerca e individuazione dei sistemi di archiviazione di terze parti in cui non è incorporato il supporto per RMS. In Exchange 2013, è possibile configurare la decrittografia dei rapporti del journal per salvare in un rapporto del journal una copia con testo non crittografato del messaggio.

Inizio pagina

## Interoperabilità con Exchange 2007

Non esiste alcun molta differenza tra l'inserimento nel journal funzionalità Exchange 2013, Exchange 2010 e Exchange 2007. Tuttavia, in Exchange 2010 e versioni successive, il programma di installazione consente di creare un contenitore separato in Active Directory per archiviare le regole del journal. Quando si imposta il primo Exchange 2010 server o versione successiva in un'organizzazione Exchange 2007, il programma di installazione crea una copia delle regole del journal esistente in Exchange 2007 e li archivia nel nuovo contenitore. Al termine dell'installazione, le regole del journal in entrambe le versioni di Exchange sono coerenti.

Al termine dell'installazione, se si modifica la configurazione delle regole del journal in Exchange 2010 (o versioni successive), è necessario apportare la stessa modifica nei server Exchange 2007 per verificare che la coerenza. Analogamente, le modifiche apportate alle registrazioni regole su Exchange 2007 devono essere inoltre prevedere in Exchange 2010 o versioni successive. È inoltre possibile esportare le regole del journal da Exchange 2007 e importarli Exchange 2013.

Inizio pagina

## Risoluzione dei problemi

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).. Se si riscontrano problemi con la cassetta postale **JournalingReportDNRTo**, vedere [regole delle cassette postali in Exchange Online e trasporto non funziona come previsto](https://go.microsoft.com/fwlink/p/?linkid=331674).


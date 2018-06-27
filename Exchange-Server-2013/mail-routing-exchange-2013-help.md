---
title: 'Routing della posta: Exchange 2013 Help'
TOCTitle: Routing della posta
ms:assetid: 6fd39079-9655-4fd9-9269-c7462c76e0a7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998825(v=EXCHG.150)
ms:contentKeyID: 50480848
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Routing della posta

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Il compito principale del servizio di trasporto disponibile su tutti i server Cassette postali in un'organizzazione Microsoft Exchange Server 2013 è l'instradamento dei messaggi ricevuti da utenti e fonti esterne alla destinazione finale. Le decisioni relative al routing vengono effettuate durante la classificazione dei messaggi. Il classificatore è un componente del servizio di trasporto su un server Cassette postali che elabora tutti i messaggi in arrivo e stabilisce come gestirli in base alle informazioni sulle loro destinazioni.

Ora l'instradamento in Exchange 2013 tiene conto dei gruppi di disponibilità del database e utilizza l'appartenenza a questi gruppi come limite per l'instradamento. Ciò è necessario in quanto In Exchange 2013, tutti i server Cassette postali ospitano il servizio di trasporto. Di conseguenza, quando un server Cassette postali appartiene a un gruppo di disponibilità del database, il meccanismo utilizzato per l'instradamento dei messaggi segue quello applicato dal gruppo di disponibilità del database. Quando un gruppo di disponibilità del database si estende su più siti Active Directory, l'utilizzo del sito Active Directory come limite principale per l'instradamento non è una buona scelta. Exchange 2013 utilizza l'appartenenza a un sito Active Directory come limite per l'instradamento per i server Cassette postali che non appartengono ai gruppi di disponibilità del database e per l'interoperabilità dell'instradamento con le precedenti versioni di Exchange. Altre importanti modifiche apportate all'instradamento in Exchange 2013:

  - Il servizio di trasporto su un server Cassette postali non comunica mai direttamente con un database delle cassette postali. Infatti, il servizio di trasporto comunica con il servizio di trasporto alle cassette postali sul server Cassette postali. Solo il servizio di trasporto alle cassette postali comunica con il database delle cassette postali sul server Cassette postali locale. Quando il server Cassette postali è membro di un gruppo di disponibilità del database, solo il servizio di trasporto alle cassette postali sul server Cassette postali che ospita la copia attiva del database accetta il messaggio per il destinatario.

  - Le RPC (Remote Procedure Call) vengono utilizzate dal servizio di trasporto alle cassette postali solo per l'invio e la ricezione dei messaggi dal database delle cassette postali locale. Quando il server Cassette postali è un membro del gruppo di disponibilità del database, il servizio di trasporto alle cassette postali utilizza le RPC solamente per comunicare in locale con le copie attive dei database delle cassette postali. In altre parole, le RPC non vengono mai utilizzate per le comunicazioni tra i server. Il servizio di trasporto alle cassette postali e il servizio di trasporto su diversi server Cassette postali comunicano sempre tramite SMTP.

  - Exchange 2013 utilizza un accodamento dei messaggi più accurato per le destinazioni remote. Invece di utilizzare una coda per tutte le destinazioni in un sito Active Directory remoto, Exchange 2013 accoda i messaggi per specifiche destinazioni nel sito Active Directory, come ad esempio i singoli connettori di invio.

  - I connettori collegati sono stati deprecati. Un connettore collegato era un connettore di ricezione collegato a un connettore di invio. Tutti i messaggi ricevuti dal connettore di ricezione veniva automaticamente inoltrati al connettore di invio.

**Sommario**

Routing components

  - Routing destinations

  - Delivery groups

  - Queues

Routing messages

  - Routing messages between Active Directory sites

  - Routing in the Front End Transport service

  - Routing in the Mailbox Transport service

  - Routing in the Transport service on Edge Transport servers

## Componenti di instradamento

Quando viene ricevuto dal servizio di trasporto su un server Cassette postali Exchange 2013, il messaggio deve essere classificato. La prima fase della classificazione consiste nella risoluzione del destinatario. Dopo che è stato risolto il destinatario, sarà possibile determinare la destinazione finale. La fase successiva, ovvero il routing, determina il percorso ottimale per raggiungere la destinazione specifica. In Exchange 2013 l'instradamento è stato generalizzato per garantire una maggiore flessibilità e una minore complessità grazie all'introduzione di concetti quali "destinazioni di instradamento" e "gruppi di recapito".

## Destinazioni di instradamento

In Exchange 2013, la destinazione finale di un messaggio è chiamata *destinazione di instradamento*. In Exchange 2013 sono presenti le seguenti destinazioni di instradamento:

  - **Database delle cassette postali**   È la destinazione di instradamento per qualsiasi destinatario con una cassetta postale su un server Cassette postali nell'organizzazione di Exchange. In Exchange 2013, le cartelle pubbliche sono un tipo di cassetta postale e quindi l'instradamento dei messaggi alle cartelle pubbliche corrisponde all'instradamento dei messaggi alle cassette postali.

  - **Connettore**   È un connettore di invio per i messaggi SMTP utilizzato come destinazione di instradamento. Per i messaggi non SMTP, si utilizza un connettore agente di recapito o un connettore esterno come destinazione di instradamento.

  - **Server di espansione del gruppo di distribuzione**   È la destinazione di instradamento quando un gruppo di distribuzione dispone di uno specifico server di espansione responsabile per l'espansione dell'elenco dei membri del gruppo. Un server di espansione del gruppo di distribuzione è sempre un server Trasporto Hub o Cassette postali Exchange 2013.

Notare che queste stesse destinazioni di instradamento erano presenti anche nelle versioni precedenti di Exchange.

Inizio pagina

## Gruppi di recapito

Ciascuna destinazione di instradamento in Exchange 2013 dispone di uno o più server di trasporto responsabili per il recapito dei messaggi a quella destinazione. Questo insieme di server di trasporto è chiamato *gruppo di recapito*. Un server di trasporto può essere un server Cassette postali Exchange 2013, un server Exchange 2010 o un server Exchange 2007 su cui è installato il ruolo Trasporto Hub. Quando la destinazione di instradamento è un database delle cassette postali, i server di trasporto nel gruppo di recapito utilizzano la stessa versione di Exchange del database delle cassette postali. Quando la destinazione di instradamento è un connettore o un server di espansione del gruppo di distribuzione, il gruppo di recapito potrebbe contenere una combinazione di server Cassette postali Exchange 2013 e Exchange 2010 o server Trasporto Hub Exchange 2007. La modalità di instradamento del messaggio dipende dalla relazione tra il server di trasporto di origine e il gruppo di recapito di destinazione:

  - Se il server di trasporto di origine è il gruppo di recapito di destinazione, la destinazione di instradamento è il successivo hop per il messaggio. Il messaggio viene recapitato dal server di trasporto locale al database delle cassette postali o al connettore sul server di trasporto nel gruppo di recapito. Se la destinazione di instradamento è un server di espansione del gruppo di distribuzione, il gruppo di distribuzione risulta già espanso quando i messaggi raggiungono la fase di instradamento della categorizzazione sul server di espansione del gruppo di distribuzione. Di conseguenza, la destinazione di instradamento dal server di espansione del gruppo di distribuzione è sempre un database delle cassette postali o un connettore.

  - Se il server di trasporto di origine non fa parte del gruppo di recapito di destinazione, il messaggio viene inoltrato al gruppo di recapito di destinazione tramite il percorso di instradamento più conveniente. In base alla dimensione e alla complessità della topologia di Exchange, il messaggio può essere inoltrato ad altri server di trasporto tramite il percorso di instradamento più conveniente oppure essere inoltrato direttamente a un server di trasporto nel gruppo di recapito di destinazione.

In Exchange 2013 sono disponibili i seguenti tipi di gruppi di destinazione:

  - **Gruppo di disponibilità del database instradabile**   È un insieme di server Cassette postali Exchange 2013 che appartengono a un unico gruppo di disponibilità del database. I database delle cassette postali nel gruppo di disponibilità del database sono le destinazioni di instradamento servite da questo gruppo di recapito. Una volta arrivato al servizio di trasporto su un server Cassette postali che appartiene al gruppo di disponibilità del database, il messaggio viene instradato al servizio di trasporto alle cassette postali sul server Cassette postali nel gruppo di disponibilità del database su cui è presente la copia attiva del database delle cassette postali di destinazione. Il servizio di trasporto alle cassette postali sul server Cassette postali di destinazione recapita poi il messaggio al database delle cassette postali locale. Sebbene un gruppo di disponibilità del database possa contenere server Cassette postali che si trovano in diversi siti Active Directory, il gruppo di disponibilità del database rappresenta il limite per il gruppo di recapito.

  - **Gruppo di recapito cassette postali**   È un insieme di server Exchange con la stessa versione che si trovano in un sito Active Directory. Il sito Active Directory rappresenta il limite per il gruppo di recapito. Le destinazioni di instradamento e i gruppi di recapito che il servono dipendono dalle versioni di Exchange utilizzate nel sito Active Directory. I database delle cassette postali che si trovano sui server Cassette postali Exchange 2010 sono serviti dai server Trasporto Hub Exchange 2010 che si trovano nel sito Active Directory. I database delle cassette postali che si trovano sui server Cassette postali Exchange 2007 sono serviti dai server Trasporto Hub Exchange 2007 che si trovano nel sito Active Directory. I database delle cassette postali che si trovano sui server Cassette postali Exchange 2013 nel sito Active Directory che non appartiene a un gruppo di disponibilità del database sono serviti dal servizio di trasporto sui server Cassette postali Exchange 2013 nel sito Active Directory. La modalità di recapito del messaggio al database delle cassette postali dipende dalla versione di Exchange:
    
      - **Exchange 2013**    Dopo l'arrivo del messaggio nel server Cassette postali di destinazione nel sito Active Directory di destinazione, il servizio di trasporto lo trasferisce al servizio di trasporto alle cassette postali tramite SMTP. Il servizio di trasporto alle cassette postali recapita poi il messaggio al database delle cassette postali locale tramite RPC.
    
      - **Exchange 2010 o Exchange 2007**   Dopo l'arrivo del messaggio in un server Trasporto Hub casuale della stessa versione nel sito Active Directory di destinazione, il driver di archiviazione presente sul server Trasporto Hub utilizza RPC per scrivere il messaggio nel database delle cassette postali.

  - **Server di origine per il connettore**   È un insieme di server Trasporto Hub Exchange 2010, Exchange 2007 o Cassette postali Exchange 2013 che vengono utilizzati come server di origine per un connettore di invio, un connettore agente di recapito o un connettore esterno. Il connettore è la destinazione di instradamento servita da questo gruppo di instradamento. Quando un connettore ha come ambito uno specifico server, solo quel server può instradare i messaggi alla destinazione definita dal connettore. Questo gruppo di recapito può contenere server Trasporto Hub Exchange 2010, Exchange 2007 o Cassette postali Exchange 2013 che si trovano in diversi siti Active Directory.

  - **Sito AD**   In alcuni casi, un sito Active Directory non è la destinazione finale di un messaggio, ma il messaggio deve passare attraverso un server Trasporto Hub Exchange 2010, Exchange 2007 o Cassette postali Exchange 2013 in quel sito Active Directory. Ciò si verifica nei seguenti casi:
    
      - Quando il sito Active Directory è configurato come sito hub. In presenza di un sito hub nel percorso di instradamento più conveniente per il recapito dei messaggi, prima di essere inoltrati alla destinazione finale, i messaggi vengono accodati ed elaborati da un server di trasporto nel sito hub.
    
      - Quando un server Trasporto Edge è sottoscritto al sito Active Directory. Non è possibile accedere a questi server Trasporto Edge sottoscritti direttamente da altri siti Active Directory. Considerare che il server Trasporto Edge potrebbe essere Exchange 2013, Exchange 2010 o Exchange 2007.
    

    > [!NOTE]
    > Il fan-out posticipato viene utilizzato solamente quando il gruppo di recapito è un sito Active Directory. Quando più destinatari condividono una qualsiasi parte del percorso di instradamento più conveniente, il fan-out posticipato tenta di ridurre il numero di trasmissioni di messaggi.



  - **Elenco server**   i tratta di uno o più server Trasporto Hub Exchange 2010, Exchange 2007 o Cassette postali Exchange 2013 configurati come server di espansione dei gruppi di distribuzione. Il server di espansione del gruppo di distribuzione è la destinazione di instradamento servita da questo gruppo di recapito.

L'appartenenza a un gruppo di recapito non è esclusiva. Ad esempio, un server Cassette postali Exchange 2013 che è membro di un gruppo di disponibilità del database può anche essere il server di origine di un connettore di invio con ambito. Questo server Cassette postali apparterrà al gruppo di recapito del gruppo di disponibilità del database instradabile per i database delle cassette postali nel gruppo di disponibilità del database, ma anche a un gruppo di recapito del server di origine per il connettore di invio con ambito.

Nella seguente tabella le destinazioni di instradamento sono abbinate al gruppo di recapito in base alla versione di Exchange utilizzata:


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>Server Cassette postali di Exchange 2013</th>
<th>Server Trasporto Hub di Exchange 2010 o Exchange 2007</th>
<th>Server Trasporto Edge nella rete perimetrale</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Database delle cassette postali in un gruppo di disponibilità del database</p></td>
<td><p>Gruppo di disponibilità del database instradabile</p></td>
<td><p>Gruppo di recapito cassette postali</p></td>
<td><p>n/d</p></td>
</tr>
<tr class="even">
<td><p>Database delle cassette postali non in un gruppo di disponibilità del database</p></td>
<td><p>Gruppo di recapito cassette postali</p></td>
<td><p>Gruppo di recapito cassette postali</p></td>
<td><p>n/d</p></td>
</tr>
<tr class="odd">
<td><p>Connettore</p></td>
<td><p>Server di origine del connettore</p></td>
<td><p>Server di origine del connettore</p></td>
<td><p>Sito AD</p></td>
</tr>
<tr class="even">
<td><p>Server di espansione del gruppo di distribuzione</p></td>
<td><p>Lista server</p></td>
<td><p>Lista server</p></td>
<td><p>n/d</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Code

Dal punto di vista del server mittente, ogni coda di recapito rappresenta la destinazione di un messaggio specifico. Quando nel servizio di trasporto sul server Cassette postali Exchange 2013 viene selezionata la destinazione di un messaggio, i dati relativi alla destinazione vengono aggiunti al destinatario come attributo **NextHopSolutionKey**. Se viene inviato un singolo messaggio a più destinatari, ciascun destinatario disporrà dell'attributo **NextHopSolutionKey**. Anche nel server ricevente vengono eseguiti la classificazione e l'accodamento del messaggio per il recapito. Dopo che il messaggio è stato accodato, sarà possibile esaminare il tipo di recapito di una coda specifica per determinare se il messaggio verrà nuovamente inoltrato una volta raggiunta la destinazione dell'hop successivo. Ogni valore univoco dell'attributo **NextHopSolutionKey** corrisponde a una coda di recapito separata.

Per ulteriori informazioni, vedere la sezione "NextHopSolutionKey" nell'argomento [Code](queues-exchange-2013-help.md).

Inizio pagina

## Instradamento dei messaggi

Quando è necessario recapitare un messaggio a un gruppo di recapito remoto, è necessario stabilire un percorso di instradamento per il messaggio. Exchange 2013 utilizza la seguente logica per selezionare il percorso di instradamento per un messaggio. Questa logica è rimasta sostanzialmente invariata da Exchange 2010:

1.  Calcolare il percorso di instradamento più conveniente aggiungendo il costo dei collegamenti al sito IP utilizzati per raggiungere la destinazione. Se la destinazione è un connettore, il costo assegnato allo spazio indirizzo verrà aggiunto al costo per raggiungere il connettore selezionato. Se sono possibili più percorsi di instradamento, verrà utilizzato il percorso con il costo complessivo minore.

2.  In presenza di più percorsi di routing con lo stesso costo complessivo, verrà valutato il numero di hop di ogni percorso e verrà scelto il percorso di routing con il numero minore.

3.  Se sono ancora disponibili più percorsi di instradamento, viene preso in considerazione il nome assegnato ai siti Active Directory prima della destinazione. Viene utilizzato il percorso di instradamento il cui sito Active Directory più vicino alla destinazione presenta il valore minore in ordine alfanumerico. Se il sito più vicino alla destinazione è identico per tutti i percorsi di routing valutati, verrà considerato il nome di un sito precedente.

In Exchange 2010, ciascun destinatario è sempre associato a un solo sito Active Directory e c'è un unico percorso di instradamento più conveniente tra i siti Active Directory di origine e di destinazione. In Exchange 2013, un gruppo di recapito può estendersi su più siti Active Directory e ci possono essere più percorsi di instradamento più convenienti a questi siti Active Directory. Exchange 2013 sceglie un singolo sito Active Directory nel gruppo di recapito di destinazione come *sito primario*. Il sito primario è il sito Active Directory più vicino in base alla logica di instradamento illustrata in precedenza. Per instradare correttamente i messaggi tra i gruppi di recapito, Exchange 2013 tiene conto delle seguenti questioni:

  - **La presenza di uno o più siti hub lungo il percorso di instradamento più conveniente**   Se il percorso più conveniente al sito primario contiene dei siti hub, è necessario instradare il messaggio tramite questi siti hub. Il sito hub più vicino lungo il percorso di instradamento più conveniente viene selezionato come nuovo gruppo di recapito di tipo **AD site** che include tutti i server di trasporto nel sito hub. Dopo che il messaggio ha attraversato il sito hub, l'instradamento del messaggio lungo il percorso più conveniente prosegue. Se il sito primario è un sito hub, continua a essere considerato tale per i seguenti motivi:
    
      - Se il gruppo di recapito di destinazione si espande su più siti Active Directory, il server di origine deve tentare di connettersi solo ai server nel sito hub.
    
      - Sono preferiti i server nel sito hub che appartengono al gruppo di recapito di destinazione.
    
    Come nelle precedenti versioni di Exchange, vengono ignorati i siti hub che non si trovano lungo il percorso di instradamento più conveniente verso il sito primario.

  - **Il server Exchange di destinazione da selezionare nel gruppo di instradamento di destinazione**   Quando il gruppo di recapito di destinazione si estende su più siti Active Directory, il percorso di instradamento verso specifici server del gruppo di recapito potrebbe avere costi diversi. Sulla base del percorso di instradamento più conveniente, i server che si trovano nel sito Active Directory più vicino vengono selezionati come server di destinazione per il gruppo di recapito e il sito Active Directory di cui fanno parte quei server viene selezionato come sito primario.

  - **Opzioni di fallback in caso di errore dei tentativi di connessione a tutti i server del gruppo di instradamento di destinazione**   Se il gruppo di recapito di destinazione si estende su più siti Active Directory, la prima opzione di fallback è rappresentata da tutti gli altri server del gruppo di recapito di destinazione che si trovano in altri siti Active Directory e che non sono selezionati come server di destinazione. La selezione dei server viene eseguita sulla base del costo del percorso di instradamento a quegli altri siti Active Directory. Se il gruppo di recapito di destinazione ha dei server nel sito Active Directory locale, non ci sono altre opzioni di fallback perché il messaggio è già il più vicino possibile alla destinazione di instradamento di destinazione. Se il gruppo di recapito di destinazione ha dei server nel sito Active Directory remoto, l'opzione prevede il tentativo di connettersi a tutti i server nel sito primario. In caso di errore, viene utilizzato un percorso di backoff nel percorso di instradamento più conveniente verso il sito primario. Exchange 2013 tenta di recapitare il messaggio il più vicino possibile alla destinazione eseguendo il backoff, hop per hop, lungo il percorso di instradamento più conveniente fino a quando non stabilisce una connessione.

Inizio pagina

## Instradamento dei messaggi tra siti Active Directory

La modalità di instradamento dei messaggi tra siti Active Directory in Exchange 2013 è praticamente uguale a quella utilizzata in Exchange 2010. Per ulteriori informazioni, vedere [Instradamento della posta tra siti Active Directory](route-mail-between-active-directory-sites-exchange-2013-help.md).

Inizio pagina

## Routing nel servizio Trasporto Front End sui server Accesso client

Questa procedura agisce da proxy senza stato per tutto il traffico SMTP esterno in ingresso e (facoltativamente) in uscita per l'organizzazione Exchange 2013. Per i messaggi in uscita, il servizio di trasporto utilizza i connettori di invio per comunicare con il servizio di trasporto Front End su un server Accesso client. Nello specifico, il servizio di trasporto Front End invia tramite proxy i messaggi in uscita quando il parametro *FrontEndProxyEnabled* su un connettore di invio adatto è impostato su `$true` o quando nelle proprietà del connettore di invio nell'interfaccia di amministrazione di Exchange è selezionata l'opzione **Proxy tramite server Accesso client**. Verrà selezionato qualsiasi server Accesso client nel sito Active Directory locale. Considerare che il servizio di trasporto Front End non dispone di connettori di invio.

Per i messaggi in arrivo, il servizio di trasporto Front End deve trovare velocemente un singolo servizio di trasporto integro su un server Cassette postali che possa ricevere la trasmissione dei messaggi, indipendentemente dal numero o tipo di destinatari. Se non ci riesce, il servizio di posta elettronica verrà percepito come non disponibile dai mittenti esterni. Come nel caso del servizio di trasporto, anche il servizio di trasporto Front End carica le tabelle di instradamento sulla base delle informazioni ricevute da Active Directory e utilizza i gruppi di recapito per stabilire come instradare i messaggi. Le tabelle utilizzate dal servizio di trasporto Front End presentano però le seguenti caratteristiche univoche:

  - Il servizio di trasporto Front End non viene mai considerato come membro di un gruppo di recapito, anche quando i ruoli Cassette postali e Accesso client sono installati sullo stesso server fisico. Di conseguenza, il servizio di trasporto Front End può comunicare solo con il servizio di trasporto.

  - Le tabelle di instradamento non contengono alcun instradamento al connettore di invio.

  - Le tabelle di instradamento contengono un elenco speciale di server Cassette postali nel sito Active Directory locale per poter gestire velocemente eventuali failover.

L'instradamento nel servizio di trasporto Front End risolve i destinatari dei messaggi nei database delle cassette postali. L'elenco dei server Cassette postali utilizzato dal servizio di trasporto Front End si basa sui database delle cassette postali dei destinatari dei messaggi. Notare che è possibile che nessuno dei destinatari abbia una cassetta postale, ad esempio, nel caso in cui un destinatario sia un gruppo di distribuzione o un utente di posta elettronica. Per ciascun database delle cassette postali, il servizio di trasporto Front End esamina il gruppo di recapito e le informazioni di instradamento ad esso associate. I gruppi di recapito utilizzati dal servizio di trasporto Front End sono:

  - Gruppo di disponibilità del database instradabile

  - Gruppo di recapito cassette postali

  - Sito AD

A seconda del numero e tipo di destinatari, il servizio di trasporto Front End esegue una delle seguenti azioni:

  - Per i messaggi con un singolo destinatario, selezionare un server Cassette postali nel gruppo di recapito di destinazione e dare la preferenza al server Cassette postali basato sulla prossimità del sito Active Directory. Il routing del messaggio al destinatario potrebbe implicare il routing del messaggio stesso attraverso un sito hub.

  - Per i messaggi con più destinatari, utilizzare i primi 20 destinatari per selezionare un server Cassette postali nel gruppo di recapito più vicino, in base alla prossimità del sito Active Directory. Notare che nel trasporto Front-End non può verificarsi la biforcazione dei messaggi e di conseguenza viene selezionato solo un server Cassette postali, indipendentemente dal numero di destinatari del messaggio.

  - Se un messaggio non ha alcuna cassetta postale come destinatario, selezionare un qualsiasi server Cassette postali nel sito Active Directory locale.

Inizio pagina

## Routing del servizio di trasporto della cassetta postale sul server cassette postali

Tale procedura è costituita da due servizi separati: il servizio Invio Trasporto cassette postali il servizio Recapito Trasporto cassette postali. Per i messaggi in arrivo, il servizio di recapito del trasporto alle cassette postali riceve i messaggi SMTP dal servizio di trasporto e si collega al database delle cassette postali locale utilizzando RPC per recapitare il messaggio. Per i messaggi in uscita, il servizio di invio del trasporto alle cassette postali si collega al database delle cassette postali locale utilizzando RPC per recuperare i messaggi e li invia al servizio di trasporto tramite SMTP. Il servizio di trasporto alle cassette postali è privo di stato e non accoda i messaggi in locale.

Come nel caso del servizio di trasporto, anche il servizio di trasporto alle cassette postali carica le tabelle di instradamento sulla base delle informazioni ricevute da Active Directory e utilizza i gruppi di recapito per stabilire come instradare i messaggi. Tuttavia, ci sono degli aspetti dell'instradamento che sono univoci del servizio di trasporto alle cassette postali:

  - Dal momento che il servizio di trasporto e il servizio di trasporto alle cassette postali sono presenti sullo stesso server Cassette postali Exchange 2013, il servizio di trasporto alle cassette postali appartiene sempre allo stesso gruppo di recapito del server Cassette postali. Questo gruppo di recapito è chiamato *gruppo di recapito locale*.

  - Il servizio di invio del trasporto alle cassette postali non invia automaticamente i messaggi al servizio di trasporto sul server Cassette postali locale o su altri server Cassette postali nel suo gruppo di recapito locale. Il servizio di invio del trasporto alle cassette postali ha accesso alle stesse informazioni sulla topologia di instradamento del servizio di trasporto e di conseguenza il servizio di invio del trasporto alle cassette postali può inviare i messaggi al servizio di trasporto sui server Cassette postali esterni al gruppo di recapito. I server Cassette postali nel gruppo di recapito locale vengono utilizzati come opzioni di fallback e per il recapito ai destinatari che non sono cassette postali.

  - Il servizio di trasporto alle cassette postali comunica esclusivamente con il servizio di trasporto sui server Cassette postali Exchange 2013.

  - Il servizio di trasporto alle cassette postali comunica esclusivamente con il servizio di trasporto sui server Cassette postali Exchange 2013. Il servizio di trasporto alle cassette postali non comunica mai con i database delle cassette postali sugli altri server Cassette postali.

Quando un utente invia un messaggio dalla sua cassetta postale, il servizio di invio del trasporto alle cassette postali risolve i destinatari del messaggio nei database delle cassette postali. L'elenco dei server Cassette postali utilizzato dal servizio di invio del trasporto alle cassette postali si basa sui database delle cassette postali dei destinatari dei messaggi. Notare che è possibile che nessuno dei destinatari abbia una cassetta postale, ad esempio, nel caso in cui un destinatario sia un gruppo di distribuzione o un utente di posta elettronica. Per ciascun database delle cassette postali, il servizio di invio di trasporto alle cassette postali esamina il gruppo di recapito e le informazioni di instradamento ad esso associate. I gruppi di recapito utilizzati dal servizio di invio di trasporto alle cassette postali sono:

  - Gruppo di disponibilità del database instradabile

  - Gruppo di recapito cassette postali

  - Sito AD

A seconda del numero e tipo di destinatari, il servizio di invio di trasporto alle cassette postali esegue una delle seguenti azioni:

  - Per i messaggi con un singolo destinatario, selezionare un server Cassette postali nel gruppo di recapito di destinazione e dare la preferenza al server Cassette postali basato sulla prossimità del sito Active Directory. Il routing del messaggio al destinatario potrebbe implicare il routing del messaggio stesso attraverso un sito hub.

  - Per i messaggi con più destinatari, utilizzare i primi 20 destinatari per selezionare un server Cassette postali nel gruppo di recapito più vicino, in base alla prossimità del sito Active Directory.

  - Se un messaggio non ha alcuna cassetta postale come destinatario, selezionare un server Cassette postali nel gruppo di recapito locale.

Quando il servizio di recapito del trasporto alle cassette postali riceve un messaggio dal servizio di trasporto, accetta o rifiuta il messaggio per il recapito in un database delle cassette postali locale. Il servizio di recapito del trasporto alle cassette postali può recapitare il messaggio se il destinatario si trova in una copia attiva di un database delle cassette postali locale. Se però il destinatario non si trova in una copia attiva di un database delle cassette postali locale, il servizio di recapito del trasporto alle cassette postali non può recapitare il messaggio e deve fornire una risposta di mancato recapito al servizio di trasporto. Ad esempio, se la copia attiva del database delle cassette postali è stata spostata di recente su un altro server, il servizio di trasporto potrebbe erroneamente trasmettere un messaggio a un server Cassette postali che ora contiene una copia non attiva del database delle cassette postali. Le risposte di mancato recapito restituite al servizio di trasporto dal servizio di trasporto alle cassette postali sono:

  - Ritenta il recapito

  - Genera un rapporto di mancato recapito

  - Reinstrada il messaggio

Inizio pagina

## Routing del servizio di trasporto sui server Trasporto Edge

Se si dispone di un server Trasporto Edge installato nella rete perimetrale, il servizio di trasporto su server di trasporto Edge fornisce l'inoltro SMTP e servizi smarthost per tutti i flussi di posta connessi a Internet. I messaggi in entrata e in uscita da Internet vengono accodati localmente sul server Trasporto Edge. Le code corrispondono ai domini esterni o ai connettori di invio. Per ulteriori informazioni, vedere la sezione "NextHopSolutionKey" nell'argomento [Code](queues-exchange-2013-help.md).

Solitamente, quando si installata un server Trasporto Edge nella rete perimetrale, si sottoscrive il server Trasporto Edge a un sito di Active Directory. Il sito di Active Directory contiene i server cassette postali che inoltrano i messaggi a e dal server Trasporto Edge. Il processo di sottoscrizione Edge consente di creare un'affiliazione di appartenenza al sito di Active Directory per il server Trasporto Edge. L'affiliazione al sito consente ai server cassette postali nel sito di Active Directory di inoltrare messaggi al server Trasporto Edge per il recapito su Internet senza dover configurare connettori di invio espliciti.

Nelle configurazioni con più siti, la posta in uscita da destinatari interni a esterni è la prima instradata al sito di Active Directory sottoscritto. Il sito Active Directory di destinazione rappresenta il gruppo di recapito. La destinazione di routing è il connettore di invio all'interno dell'organizzazione nel servizio di trasporto su ciascun server cassette postali nel sito Active Directory sottoscritto. Il *connettore di invio all'interno dell'organizzazione* è uno speciale connettore di invio esistente nel servizio di trasporto su ciascun server cassette postali. Il connettore di invio viene implicitamente creato, è invisibile, non richiede gestione ed è utilizzato per inoltrare messaggi tra server di Exchange.

La posta in uscita per destinatari esterni è instradata dal server cassette postali al server trasporto Edge. Il server Accesso client non è coinvolto nella posta di routing su un server di trasporto Edge. La posta viene trasmessa dal connettore di invio all'interno dell'organizzazione nel servizio di trasporto nel server cassette postali su un connettore di ricezione nel servizio di trasporto sul server di trasporto Edge. Su un server Trasporto Edge, il connettore di ricezione predefinito è configurato per l'ascolto delle connessioni dai server cassette postali interni nel sito di Active Directory sottoscritto e le connessioni anonime da Internet. Dopo la categorizzazione del messaggio da parte del servizio di trasporto sul server Trasporto Edge, il messaggio viene accodato localmente per il recapito su Internet utilizzando il connettore di invio dedicato creato durante la sottoscrizione Edge.

La posta in ingresso da parte di destinatari esterni arriva sul Trasporto Edge tramite il connettore di ricezione predefinito e i messaggi vengono categorizzati e accodati per la consegna. I messaggi vengono inoltrati tramite connettore di invio dedicato creato dalla sottoscrizione Edge per inviare la posta all'organizzazione Exchange. La destinazione dei messaggi dipende dalla configurazione del server di Exchange interni.

  - **I server cassette postali e Accesso client installati sullo stesso computer**   In questa configurazione, il server Accesso client viene utilizzato per il flusso di posta in ingresso. I flussi di posta dal connettore di invio nel servizio trasporto sul server Trasporto Edge al connettore di ricezione predefinito nel servizio di trasporto Front End sul server Accesso client e poi sul connettore di ricezione predefinito nel servizio di trasporto nel server cassette postali.

  - **I server cassette postali e Accesso client installati su diversi computer**   In questa configurazione, il server Accesso client viene ignorato per il flusso di posta in ingresso. I flussi di posta dal connettore di invio nel servizio di trasporto nel server di trasporto Edge al connettore di ricezione predefinito nel servizio di trasporto sul server cassette postali.

Se si dispone di un server di trasporto Edge Exchange 2007 o Exchange 2010 installato nella rete perimetrale, il flusso di posta in ingresso e in uscita si verifica sempre direttamente tra il server di trasporto Edge e il server cassette postali. Non viene utilizzato il server Accesso client.

Inizio pagina


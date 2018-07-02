---
title: 'Instradamento della posta tra siti Active Directory: Exchange 2013 Help'
TOCTitle: Instradamento della posta tra siti Active Directory
ms:assetid: 86b423e3-7bec-4430-9a5a-4f84ce9d82ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ916681(v=EXCHG.150)
ms:contentKeyID: 52063120
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Instradamento della posta tra siti Active Directory

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Un sito di Active Directory è un componente logico di configurazione basato sugli elementi fisici della rete. L'obiettivo principale alla base della creazione di un sito di Active Directory è la definizione delle subnet della rete da connettere in modo da ottimizzare il controllo del traffico di replica di Active Directory. Microsoft Exchange Server 2013 riconosce i gruppi di disponibilità del database (DAG) e i siti di Active Directory come limiti per il routing e i server Exchange 2013 effettuano decisioni di routing in base alla topologia del sito Active Directory.

Per impostazione predefinita, una foresta Active Directory contiene solo un sito Active Directory. Il nome predefinito per questo sito di Active Directory è `Default-First-Site-Name`. Se non vengono creati altri siti di Active Directory, tutti i computer della foresta appartenenti al dominio saranno membri di `Default-First-Site-Name`. Non sarà necessario configurare un'associazione tra siti e subnet. Se vengono creati altri siti di Active Directory, sarà necessario specificare le subnet assegnate ai nuovi siti di Active Directory.

**Sommario**

Determining site membership

IP site links

Controlling IP site link costs

Implementing hub sites

Topology discovery

## Determinazione dell'appartenenza al sito

Un sito di Active Directory può essere associato a una o più subnet IP. L'appartenenza al sito di Active Directory viene assegnata dagli amministratori ai computer configurati come controller di dominio e server di catalogo globale. Inoltre, viene assegnata automaticamente ad altri computer appartenenti al dominio, come, ad esempio, i server Exchange, configurati per utilizzare l'indirizzo IP di una subnet IP associata a un sito di Active Directory. Si presume che nei computer che appartengono allo stesso sito di Active Directory sia presente un'ottima connettività di rete. Un server è sempre membro di un unico sito di Active Directory.

Un'applicazione dispone del supporto per i siti se è in grado di determinare l'appartenenza al sito di Active Directory del computer in cui è installata e di altri computer della foresta e quindi di utilizzare tali informazioni per controllare il flusso di comunicazione. Se l'applicazione deve utilizzare i servizi di altri server, ad esempio un controller di dominio o un server di catalogo globale, la priorità viene assegnata ai server che appartengono allo stesso sito di Active Directory del computer che richiede tali servizi.

Exchange 2013 è un'applicazione che dispone del supporto per i siti e utilizza la topologia di Active Directory per il routing dei messaggi e per comunicare con i servizi eseguiti su altri computer Exchange 2013. Il sito di Active Directory non rappresenta solo il limite di routing, ma anche il limite di individuazione dei servizi.

La determinazione dell'appartenenza al sito per un computer appartenente al dominio dipende da una serie di query DNS effettuate per confrontare l'indirizzo IP locale con le subnet definite e determinare quindi l'associazione appropriata di appartenenza al sito. Per limitare il sovraccarico associato alle query DNS, è necessario integrare allo schema di Active Directory in Exchange 2013 l'attributo **msExchServerSite** dell'oggetto server Exchange. Il valore dell'attributo è il nome distinto del sito di Active Directory di un server Exchange. Questo attributo è una proprietà di ogni oggetto server Exchange. Se l'affinità di appartenenza al sito viene archiviata come attributo dell'oggetto server, sarà possibile leggere la topologia corrente direttamente da Active Directory anziché tramite query DNS e l'associazione di appartenenza al sito verrà abilitata per un computer non appartenente al dominio, ad esempio un server Trasporto Edge sottoscritto.

Il valore dell'attributo **msExchServerSite** viene compilato e mantenuto aggiornato dal servizio Topologia di Active Directory di Microsoft Exchange. Quando viene avviato un computer basato su Windows, il servizio Accesso rete ne determina l'appartenenza al sito, utilizza tali informazioni per individuare i controller di dominio presenti nello stesso sito di Active Directory del computer locale e invia richieste di autorizzazione e autenticazione a tali server. Il servizio Topologia di Active Directory di Microsoft Exchange utilizza la chiamata API **DsGetSiteName** per recuperare il valore dell'appartenenza al sito dal servizio Accesso rete e scrive il nome distinto del sito di Active Directory nell'attributo **msExchServerSite** dell'oggetto server Exchange in Active Directory.

Nella tabella seguente viene illustrato come possono essere definiti i siti di Active Directory in un'organizzazione. Nel seguente esempio vengono definiti tre siti di Active Directory e ciascuno di essi viene associato a più subnet IP.

**Esempio di un'associazione tra subnet e siti di Active Directory**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome del sito di Active Directory</th>
<th>Subnet IP associate</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sito A</p></td>
<td><p>192.168.1.0/24</p>
<p>192.168.2.0/24</p></td>
</tr>
<tr class="even">
<td><p>Sito B</p></td>
<td><p>192.168.3.0/24</p>
<p>192.168.4.0/24</p></td>
</tr>
<tr class="odd">
<td><p>Sito C</p></td>
<td><p>192.168.5.0/24</p>
<p>192.168.6.0/24</p></td>
</tr>
</tbody>
</table>


Se l'indirizzo IP di un server denominato Mailbox01 è 192.168.1.1, il server sarà membro del sito A. La modifica dell'indirizzo IP di un server consente di modificarne l'appartenenza al sito. Se si modifica l'indirizzo IP del server Mailbox01 impostandolo su 192.168.2.1, l'appartenenza del server al sito di Active Directory non verrà modificata poiché la subnet è associata anche al sito A. Tuttavia, se il server viene spostato e l'indirizzo IP viene modificato in 192.168.3.1, il server verrà considerato un membro del sito B.

La modifica dell'appartenenza al sito può verificarsi anche se viene modificata l'associazione delle subnet ai siti di Active Directory. Ad esempio, se viene rimossa la subnet 192.168.3.0 dall'associazione con il sito B e viene associata al sito A, l'appartenenza al sito di un server con indirizzo IP 192.168.3.1 verrà impostata sul sito A. Quando viene modificata l'appartenenza al sito, Exchange deve aggiornare i dati di configurazione in modo che la modifica venga considerata quando vengono prese le decisioni di routing. Tra la modifica dell'appartenenza al sito di Active Directory e la propagazione completa della modifica della topologia, si verifica una determinata latenza.

Inizio pagina

## Collegamenti al sito IP

I collegamenti di sito sono percorsi logici tra i siti di Active Directory. Un oggetto collegamento di sito rappresenta un insieme di siti in grado di comunicare allo stesso costo. I collegamenti di sito non corrispondono al percorso corrente utilizzato dai pacchetti di rete sulla rete fisica. Tuttavia, il costo assegnato dall'amministratore al collegamento di sito in genere è correlato all'affidabilità, alla velocità e alla larghezza di banda disponibile della rete sottostante. Ad esempio, l'amministratore di Active Directory assegnerebbe un costo minore a una connessione di rete con una velocità di 100 megabit al secondo (Mbps) rispetto a una connessione con una velocità di 10 Mbps.

Per impostazione predefinita, tutti i collegamenti di sito sono transitivi. Ciò significa che se il sito A dispone di una connessione al sito B e il sito B dispone di una connessione al sito C, il sito A sarà connesso in modo transitivo al sito C. Il collegamento transitivo tra il sito A e il sito C viene anche denominato *ponte di collegamenti di sito*.

In Exchange vengono utilizzati solo collegamenti di sito IP per determinare la topologia di routing del sito di Active Directory. Il costo assegnato al collegamento di sito IP verrà considerato dal componente di routing di Exchange quando viene calcolata la tabella di routing. Questi costi vengono utilizzati per calcolare il percorso di routing più conveniente fino alla destinazione finale di un messaggio.

Ogni sito Active Directory deve essere associato ad almeno un collegamento di sito IP. Vi è un solo collegamento di sito IP predefinito il cui nome è `DEFAULTIPSITELINK`. Quando viene creato un sito di Active Directory, è necessario associarlo a un collegamento di sito IP. Per implementare la topologia desiderata, è possibile creare ulteriori collegamenti di sito IP oppure associare ogni sito di Active Directory al collegamento `DEFAULTIPSITELINK`. Ogni sito di Active Directory che appartiene a un collegamento di sito IP è in grado di comunicare direttamente con ogni altro sito del collegamento allo stesso costo.

Nella figura seguente viene illustrata una foresta in cui sono configurati quattro siti di Active Directory. A ogni sito è stato associato il collegamento `DEFAULTIPSITELINK`. Pertanto, ciascun sito di Active Directory è in grado di comunicare direttamente con gli altri siti utilizzando la stessa metrica di costo. Sono indicati più percorsi di comunicazione, tuttavia viene definito un unico collegamento di sito IP.

**Topologia a maglia completa con una singola connessione al sito IP**

![Topologia a maglia completa con una singola connessione al sito IP](images/JJ916681.af38d41d-e768-4221-ab4b-b782aa388b73(EXCHG.150).gif "Topologia a maglia completa con una singola connessione al sito IP")

Nella figura seguente viene illustrata una foresta in cui sono configurati quattro siti di Active Directory. In questa topologia, l'amministratore ha configurato collegamenti di sito IP per creare una *topologia hub e spoke* di siti di Active Directory. Ogni sito spoke è in grado di comunicare direttamente con il sito centrale e con gli altri siti spoke utilizzando collegamenti di sito IP transitivi.

**Topologia hub e spoke dei collegamenti di sito IP di Active Directory**

![Topologia hub e spoke dei collegamenti al sito IP](images/JJ916681.eca6cd51-8c2e-4996-81ea-070cd9766ef8(EXCHG.150).gif "Topologia hub e spoke dei collegamenti al sito IP")

È importante notare che Exchange utilizza i collegamenti di sito per determinare il percorso più conveniente, ma cercherà sempre di recapitare i messaggi direttamente al server Exchange di destinazione. Ad esempio, se un utente nel sito B nella topologia mostrata nella figura precedente invia un messaggio a un altro utente del sito C, il server Cassette postali nel sito B si connette direttamente al server Cassette postali nel sito C. Se si vuole che i messaggi passino attraverso il sito A, è necessario attivare tale sito come sito hub. Per ulteriori informazioni sui siti hub, vedere "Implementazione di siti hub" più avanti in questo argomento.

L'amministratore di Active Directory implementa la topologia che rappresenta al meglio i requisiti di connettività e comunicazione della foresta. Poiché la stessa topologia viene utilizzata da Exchange, è necessario assicurarsi che la topologia corrente supporti una comunicazione di messaggistica efficiente.

Il costo predefinito per un collegamento di sito è pari a 100. Un costo valido può essere qualsiasi numero compreso tra 1 e 99.999. Se vengono specificati collegamenti ridondanti, verrà utilizzato sempre il collegamento a cui è assegnato il costo minore. L'amministratore di un'organizzazione Exchange può assegnare un costo specifico di Exchange a un collegamento di sito IP. In tal caso, il costo specificato verrà utilizzato da Exchange. In caso contrario, verrà utilizzato il costo di Active Directory. Per informazioni su come impostare un costo Exchange su un collegamento di sito IP, vedere "Controllo dei costi del collegamento di sito IP" più avanti in questo argomento. Un amministratore che appartiene al gruppo Enterprise Administrators può creare ulteriori collegamenti di sito IP.

Per ulteriori informazioni sulla configurazione del sito di Active Directory, vedere [Progettazione della topologia del sito](https://go.microsoft.com/fwlink/p/?linkid=33551).

Inizio pagina

## Controllo dei costi di collegamento al sito IP

I costi di collegamento di sito IP Active Directory si basano sulla velocità di rete relativa rispetto a tutte le connessioni di rete WAN e sono progettati per produrre una topologia affidabile ed efficiente di replica. Pertanto, nella maggior parte dei casi, i costi del collegamento di sito IP esistente dovrebbero funzionare bene per il routing dei messaggi di Exchange. Tuttavia, se dopo aver documentato il sito esistente di Active Directory e la topologia del collegamento di sito IP, si rileva che i costi del collegamento di sito IP di Active Directory e gli schemi di flusso del traffico non sono ottimali per Exchange, è possibile modificare i costi valutati da Exchange. Modifica del costo assegnato al collegamento di sito IP utilizzando gli strumenti di Active Directory che possono influire sull'intero ambiente. Dovrebbe invece utilizzare il cmdlet **Set-AdSiteLink** in Exchange Management Shell per assegnare un costo specifico di Exchange per un collegamento di sito IP. Ad esempio, per configurare un costo specifico di Exchange pari a 25 per il collegamento del sito IP denominato SITELINKAB, è possibile utilizzare il seguente comando in Shell: `Set-AdSiteLink SITELINKAB -ExchangeCost 25`.

Quando viene assegnato un costo specifico di Exchange a un collegamento al sito IP, il costo di Exchange sostituisce il costo di Active Directory a scopo di routing dei messaggi e per il routing viene preso in considerazione il costo di Exchange solo quando si valuta il percorso di routing meno costoso.

La modifica dei costi del collegamento di sito IP può risultare utile quando la topologia di routing dei messaggi deve essere differenziata dalla topologia di replica di Active Directory. I costi di Exchange consentono di imporre a tutte le route dei messaggi l'utilizzo di un sito hub, nonché di controllare la posizione in cui vengono accodati i messaggi quando si verifica un errore di comunicazione con un sito di Active Directory. Di seguito è illustrata una topologia Active Directory con quattro siti.

**Topologia con costi di Exchange configurati per i collegamenti di sito IP**

![Topologia con costi di Exchange per i collegamenti al sito IP](images/JJ916681.56ac2bab-99de-4ddf-b968-80cd34ab8c21(EXCHG.150).gif "Topologia con costi di Exchange per i collegamenti al sito IP")

Nella figura precedente, la connessione di rete tra il sito C e il sito D è una connessione a larghezza di banda ridotta che deve essere utilizzata solo per la replica di Active Directory e non per il routing dei messaggi. Tuttavia, i costi del collegamento di sito IP di Active Directory determinano l'inclusione del collegamento nel percorso di routing più conveniente dagli altri siti di Active Directory al sito D. Pertanto, i messaggi vengono recapitati alla coda del sito D nel sito C. Per l'amministratore di Exchange è preferibile che il percorso di routing più conveniente includa il sito B, in modo tale che, se il sito D non è disponibile, i messaggi vengano accodati nel sito B. La configurazione di un costo elevato di Exchange su un collegamento di sito IP tra il sito C e il sito D impedisce l'inclusione del collegamento nel percorso di routing più conveniente al sito D.

Exchange fornisce il supporto per la configurazione di un limite delle dimensioni massime del messaggio su un collegamento di sito IP di Active Directory. Per impostazione predefinita, Exchange non impone un limite di dimensione massima dei messaggi ai messaggi inoltrati mediante server Exchange in diversi siti di Active Directory. Se si utilizza il cmdlet **Set-AdSiteLink** per configurare la dimensione massima dei messaggi su un collegamento di sito IP di Active Directory, il routing genera un rapporto di mancato recapito (NDR) per tutti i messaggi di dimensioni superiori rispetto al limite massimo per la dimensione dei messaggi configurato su un qualunque collegamento di sito di Active Directory nel percorso di routing con il costo minore. Questa configurazione è utile per limitare la dimensione dei messaggi inviati ai siti remoti di Active Directory che devono comunicare mediante connessioni con larghezza di banda ridotta. Per ulteriori informazioni, vedere [Limiti di dimensione dei messaggi](message-size-limits-exchange-2013-help.md).

Inizio pagina

## Implementazione di siti hub

Nell'organizzazione di Exchange, potrebbe essere opportuno imporre l'inoltro di tutti i messaggi tramite un sito di Active Directory specifico. È possibile utilizzare Shell per designare un sito di Active Directory come sito hub. Quando si effettua questa operazione, si può verificare un sovraccarico generale aggiuntivo in quanto sono coinvolti più server nel recapito dei messaggi. Ad esempio, si supponga di inviare un messaggio dal sito A al sito E. Se il percorso di routing più conveniente è sito A-sito B-sito C-sito D-sito E e viene designato il sito C come sito hub, il messaggio verrà inoltrato dal sito A al sito C e quindi dal sito C al sito E.

Il cmdlet **Set-AdSite** consente di specificare un sito di Active Directory come sito hub. In presenza di un sito hub nel percorso di routing più conveniente per il recapito dei messaggi, prima che vengano inoltrati alla destinazione finale, i messaggi verranno accodati ed elaborati dal servizio di trasporto sui server Cassette postali nel sito hub.

Una volta scelto il percorso di routing più conveniente, il routing determina se nel percorso esiste un sito hub. Se è configurato un sito hub, i messaggi si fermano in un server cassette postali nel sito hub prima di essere inoltrati alla destinazione. Se nel percorso di routing più conveniente sono presenti più siti hub, i messaggi si fermano in ciascun sito hub del percorso.

Tale variazione del routing per l'inoltro diretto si verifica solo quando il sito hub è posizionato lungo il percorso di routing più conveniente. Nella figura seguente viene illustrato l'utilizzo corretto di un sito hub. In questo diagramma il sito B è configurato come sito hub. Prima di essere recapitati al sito D, i messaggi inviati dal sito A al sito D vengono inoltrati al sito B.

**Recapito dei messaggi con un sito hub**

![Recapito dei messaggi con un sito hub](images/JJ916681.93238bcb-6bbc-4a48-aeb0-09342a421b5b(EXCHG.150).gif "Recapito dei messaggi con un sito hub")

Nella figura seguente viene illustrata l'influenza dei costi dei collegamenti di sito IP sul routing a un sito hub. In questo scenario il sito B è stato designato come sito hub. Tuttavia, poiché non è incluso nel percorso di routing più conveniente tra gli altri siti, prima di essere recapitati al sito D, i messaggi inviati dal sito A al sito D non vengono mai inoltrati al sito B. Un sito di Active Directory non viene mai utilizzato come sito hub se non è incluso nel percorso di routing più conveniente tra altri due siti.

**Sito hub non correttamente configurato**

![Sito hub non correttamente configurato](images/JJ916681.c010d4d8-5cd3-4b79-b7db-0367ba3cc287(EXCHG.150).gif "Sito hub non correttamente configurato")

È possibile configurare qualsiasi sito di Active Directory come sito hub. Tuttavia, per eseguire correttamente la configurazione, è necessario che nel sito hub sia stato distribuito almeno un server Cassette postali.

Inizio pagina

## Individuazione della topologia

La topologia di Active Directory viene fornita a Exchange tramite i seguenti elementi:

  - Il servizio Topologia di Active Directory di Microsoft Exchange.

  - Il modulo di individuazione della topologia all'interno del servizio di trasporto di Microsoft Exchange.

Il servizio Topologia di Active Directory di Microsoft Exchange viene eseguito sui server Accesso client Exchange 2013. Questi server utilizzano il servizio Topologia di Active Directory di Microsoft Exchange per individuare i controller di dominio e i server di catalogo globale utilizzabili dai server Exchange per le operazioni di lettura e scrittura dei dati Active Directory. Exchange 2013 effettua il binding ai server di directory individuati ogni volta che Exchange esegue operazioni di scrittura o lettura in Active Directory.

Il modulo di individuazione della topologia è un componente del servizio di trasporto di Microsoft Exchange e fornisce informazioni sulla topologia di Active Directory ai server Exchange. L'API consente di individuare i ruoli e i server Exchange presenti nell'organizzazione e di determinarne la relazione con gli oggetti di configurazione di Active Directory. I dati di configurazione vengono recuperati da Active Directory e memorizzati nella cache in modo da garantirne l'accessibilità da parte dei servizi di Exchange in esecuzione sul computer specifico.

Per generare una topologia di routing di Exchange, nel modulo di individuazione della topologia vengono eseguiti i passaggi riportati di seguito:

1.  I dati vengono letti da Active Directory. Vengono recuperati i seguenti oggetti:
    
      - Siti di Active Directory.
    
      - Collegamenti di sito IP.
    
      - Tutti i server Exchange.

2.  I dati recuperati nel passaggio 1 vengono utilizzati per creare la topologia iniziale e per iniziare il collegamento e il mapping degli oggetti di configurazione correlati.

3.  I server Exchange vengono associati ai siti di Active Directory recuperando il valore dell'attributo del sito dall'oggetto server Exchange archiviato in Active Directory.

4.  Le tabelle di routing vengono aggiornate con la raccolta di informazioni recuperate.

Questo processo fornisce a ogni server Exchange 2013 informazioni sulla presenza e sulla prossimità di altri server Exchange nell'organizzazione.

Inizio pagina


---
title: 'Bilanciamento del carico: Exchange 2013 Help'
TOCTitle: Bilanciamento del carico
ms:assetid: f572c193-6f3a-400e-9085-a9d3e5e18c59
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ898588(v=EXCHG.150)
ms:contentKeyID: 51407441
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Bilanciamento del carico

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Il bilanciamento del carico consente di stabilire e gestire i server che devono ricevere traffico. Il bilanciamento del carico consente di distribuire le connessioni client in ingresso tra una varietà di endpoint, ad esempio server Cassette postali, per garantire che nessun endpoint assuma una quota sproporzionata del carico. Il bilanciamento del carico fornisce, inoltre, la ridondanza del failover in caso di errore di uno o più endpoint. Grazie al bilanciamento del carico di Exchange Server 2013, è possibile accertarsi che gli utenti continuino a ricevere il servizio Exchange in caso di guasto di un computer. Il bilanciamento del carico, inoltre, consente all'ambiente di distribuzione di gestire più traffico di quello che potrebbe elaborare un solo server fornendo, allo stesso tempo, un solo nome host per tutti i client.

Il bilanciamento del carico ha due funzioni principali: Riduce l'impatto dei guasti del server Accesso client in uno o più siti Active Directory. Garantisce, inoltre, che il carico su ciascun server Accesso client sia equamente distribuito.

Exchange 2013 include anche le seguenti soluzioni di switchover e ridondanza di failover:

  - **Disponibilità elevata** Exchange 2013 utilizza gruppo di disponibilità del database (DAG) per conservare più copie delle cassette postali su diversi server sincronizzati. In tal modo, in caso di errore di un database delle cassette postali su un server, gli utenti possono collegarsi a una copia sincronizzata del database su un altro server.

  - **Resilienza del sito** È possibile distribuire due siti Active Directory in posizioni geografiche separate, mantenere la sincronizzazione dei dati tra le due posizioni e far sì che uno dei siti assuma tutto il carico in caso di errore dell'altro.

  - **Spostamento delle cassette postali in linea** Durante lo spostamento delle cassette postali in linea, gli utenti finali possono comunque accedere agli account di posta elettronica. L'account diventa inaccessibile solo per un breve periodo di tempo alla fine del processo (quando si verifica la sincronizzazione finale). È possibile eseguire spostamenti delle cassette postali in linea tra foreste o nell'ambito di una stessa foresta.

  - **Ridondanza shadow**   La ridondanza shadow protegge la disponibilità e il ripristino dei messaggi durante il transito degli stessi. Con la ridondanza shadow, l'eliminazione di un messaggio dai database di trasporto viene ritardata finché il server di trasporto non verifica il completamento di tutti gli hop successivi relativi a quel messaggio. Se in uno degli hop successivi si verifica un errore prima della segnalazione del recapito del messaggio, il messaggio viene inviato nuovamente all'hop in questione.

## Modifiche architettoniche nel bilanciamento del carico per Exchange Server 2013

In Exchange Server 2010, le connessioni client e l'elaborazione vengono gestite dal ruolo server Accesso client. Questo richiede che il carico delle connessioni Outlook esterne ed interne, nonché delle connessioni di dispositivi mobili e di terze parti, sia bilanciato tra i diversi server Accesso client della distribuzione in modo da ottenere la tolleranza di errore e un utilizzo efficiente dei server. Molti protocolli di Accesso client di Exchange 2010 richiedevano l'affinità, una relazione tra il client e un particolare server Accesso client. In particolare, Outlook Web App, il pannello di controllo di Exchange, i Servizi Web di Exchange, Outlook Anywhere, le connessioni MAPI TCP/IP di Outlook, Exchange ActiveSync, il servizio Rubrica di Exchange e Remote PowerShell richiedevano o sfruttavano l'affinità client-server Accesso client. Le opzioni di bilanciamento del carico di Exchange 2010 erano:

  - Bilanciamento carico di rete di Microsoft Windows con affinità basata sull'IP di origine

  - Bilanciamento del carico hardware

A causa delle diverse esigenze di Exchange 2010 i protocolli client, si consiglia utilizzando un soluzione di bilanciamento carico di livello 7. Livello 7, noto anche come a livello di applicazione il bilanciamento del carico, consentiti il soluzione per utilizzare le regole complesse per determinare la modalità di bilanciare ogni richiesta in ingresso nel sistema considerato che l'intera conversazione tra client e server è disponibile per la logica di servizio di bilanciamento del carico di bilanciamento del carico. Queste regole complesse verificato che indica la presenza di tutte le richieste da un client specifica per lo stesso endpoint server Accesso Client. In Exchange 2010, se tutte le richieste da un client specifico non è stato passa allo stesso endpoint per i protocolli necessari affinità, l'esperienza utente sarebbe influenzato negativamente. Per ulteriori informazioni sulle opzioni di bilanciamento del carico di Exchange 2010, vedere [Understanding bilanciamento del carico in Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=196447).

In Exchange Server 2013, esistono due tipi di server primari: il server Accesso client e il server Cassette postali. I server Accesso client in Exchange 2013 servono da server proxy leggeri, senza stato, che consentono la connessione dei client ai server Cassette postali di Exchange 2013. I server Accesso client di Exchange 2013 forniscono autenticazione e spazio dei nomi unificati. Inoltre, i server Accesso client di Exchange 2013:

  - Supportano la logica di reindirizzamento e proxy per i protocolli client,

  - Supportano l'uso del bilanciamento del carico di Livello 4.

Con l'affinità della sessione e il bilanciamento del carico di Livello 7, tutte le richieste tra il client e il server vengono inviate allo stesso endpoint, come richiesto da diversi protocolli. Le richieste vengono distribuite a livello dell'applicazione. Con il bilanciamento del carico di Livello 4, le richieste vengono distribuite a livello del trasporto. La soluzione di bilanciamento del carico distribuisce le richieste dal client, che riconosce un singolo indirizzo IP (talvolta detto indirizzo IP virtuale o VoIP), a un insieme di server che eseguono il lavoro. La connessione tra il client e il server deve essere stabilita prima che venga determinato il contenuto della richiesta, pertanto il sistema di bilanciamento del carico seleziona un server per la ricezione della richiesta prima di esaminarne il contenuto. La selezione del server di destinazione può essere effettuata in diversi modi, ad esempio \&quot;round-robin,\&quot; in cui ogni connessione in ingresso passa al successivo server di destinazione in un elenco circolare, o "meno connessioni", in cui il sistema di bilanciamento del carico invia ogni nuova connessione al server per cui è definito il minor numero di connessioni. Ora che l'affinità della sessione non è necessaria, l'architettura di bilanciamento del carico distribuita è più flessibile, semplice e presenta maggiore disponibilità di scelta. Il bilanciamento del carico senza affinità di sessione consente di aumentare la capacità e l'utilizzo dei sistema di bilanciamento del carico perché l'elaborazione non viene utilizzata per gestire altre opzioni di affinità coinvolte quali il bilanciamento del carico basato su cookie o l'ID sessione SSL (Secure Sockets Layer).

## Array di server Accesso client e Exchange 2013

In Exchange 2010, è stato introdotto il concetto di array di Accesso client. Una volta configurato un array di Accesso client per un sito Active Directory attivo, tutti i server Accesso client del sito diventano automaticamente membri dell'array. Nella build correnti di Exchange 2013, non è necessaria alcuna configurazione di array Accesso client perché la distribuzione di un servizio a carico bilanciato e altamente disponibile è molto più semplice.

## Soluzioni di bilanciamento del carico

L'utilizzo di servizi di bilanciamento del carico hardware è ancora supportato per Exchange 2013. Per informazioni sulle soluzioni di bilanciamento del carico hardware che hanno completato soluzione testando Exchange 2010 e verrà lavoro probabilmente analoghe a quelle con Exchange 2013, vedere [distribuzione del servizio di bilanciamento del carico di Exchange Server 2010](https://go.microsoft.com/fwlink/p/?linkid=261834). Tenere presente che questa pagina è illustrata la configurazione di livello 7 più complessa di servizi di bilanciamento del carico hardware con Exchange 2010. Bilanciamento del carico del traffico Exchange 2013 può essere molto più semplice, le modifiche dell'architettura illustrate in precedenza in questo argomento. Anziché configurando l'affinità di sessione per ognuno dei protocolli di Exchange, le connessioni in ingresso a Exchange 2013 server Accesso Client possono indirizzate a un server disponibile dal servizio di bilanciamento del carico senza ulteriori affinità elaborazione necessarie. Servizio di bilanciamento del carico hardware è ancora un ruolo importante per ottenere una disponibilità elevata del servizio di Exchange poiché può rilevare quando un server Accesso Client specifico non è più disponibile e rimuovere dall'insieme dei server che consente di gestire le connessioni in ingresso.

## Bilanciamento carico di rete di Microsoft Windows (WNLB)

Bilanciamento carico di rete di Microsoft Windows (WNLB) è un software di bilanciamento del carico comunemente usato con i server Exchange. Per poter utilizzare questo software con Microsoft Exchange è necessario considerare una serie di limitazioni.

  - Il software non può essere utilizzato su server Exchange ove sono in uso anche gruppi di disponibilità del database (DAG) dal momento che è incompatibile con il clustering di failover di Windows. Se è in uso un gruppo di disponibilità del database di Exchange 2013 e si desidera utilizzare Bilanciamento carico di rete di Microsoft Windows, occorrerà che il ruolo server Accesso client e il ruolo server Cassette postali siano eseguiti da server distinti.

  - Il software Bilanciamento carico di rete di Microsoft Windows non rileva le interruzioni di servizio, ma solo le interruzioni del server tramite l'indirizzo IP. Ciò significa che nel caso di errore di un particolare servizio Web, ad esempio Outlook Web App, con il server ancora in funzione, il software WNLB non rileverà l'errore e continuerà a instradare le richieste al server Accesso client. Pertanto, occorrerà intervenire manualmente per rimuovere dal pool di bilanciamento del carico il server Accesso client su cui si è verificato l'errore.

  - L'uso di Bilanciamento carico di rete di Microsoft Windows può causare un traffico eccessivo sulle porte con conseguente sovraccarico sulle reti.

  - Dal momento che esegue l'affinità dei client utilizzando l'indirizzo IP di origine, Bilanciamento carico di rete di Microsoft Windows non è una soluzione efficace se il pool IP di origine è ridotto, come, ad esempio, quando questo proviene da una subnet di una rete remota o quando l'organizzazione utilizza la conversione degli indirizzi di rete.


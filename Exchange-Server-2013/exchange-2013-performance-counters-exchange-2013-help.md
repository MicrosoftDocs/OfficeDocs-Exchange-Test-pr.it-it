---
title: 'Contatori delle prestazioni di Exchange 2013: Exchange 2013 Help'
TOCTitle: Contatori delle prestazioni di Exchange 2013
ms:assetid: 9143dd77-7c30-4769-8de1-28c717cfa9e9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn904093(v=EXCHG.150)
ms:contentKeyID: 63910903
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Contatori delle prestazioni di Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-02-06_

## Contatori delle prestazioni di Exchange 2013

Nelle sezioni seguenti vengono elencati i contatori delle prestazioni più utili da usare quando si risolvono i problemi di Exchange 2013.

## Contatori della connettività dei controller di dominio di Exchange

Nelle tabella seguente sono riportate soglie accettabili e informazioni sui contatori della connettività dei controller di dominio di Exchange.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Contatore</th>
<th>Descrizione</th>
<th>Soglia</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Controller di dominio MSExchange ADAccess(*)\Durata lettura LDAP</p></td>
<td><p>Indica il tempo, in millisecondi (ms), per l'invio di una richiesta di lettura LDAP al controller di dominio specificato e la ricezione di una risposta.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 50 ms. I picchi (valori massimi) non devono essere superiori a 100 ms.</p></td>
</tr>
<tr class="even">
<td><p>Controller di dominio MSExchange ADAccess(*)\Durata ricerca LDAP</p></td>
<td><p>Indica il tempo, in millisecondi, per l'invio di una richiesta di ricerca LDAP e la ricezione di una risposta.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 50 ms. I picchi (valori massimi) non devono essere superiori a 100 ms.</p></td>
</tr>
<tr class="odd">
<td><p>Processi MSExchange ADAccess(*)\Durata lettura LDAP</p></td>
<td><p>Indica il tempo, in millisecondi (ms), per l'invio di una richiesta di lettura LDAP al controller di dominio specificato e la ricezione di una risposta.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 50 ms. I picchi (valori massimi) non devono essere superiori a 100 ms.</p></td>
</tr>
<tr class="even">
<td><p>Processi MSExchange ADAccess(*)\Durata ricerca LDAP</p></td>
<td><p>Indica il tempo, in millisecondi, per l'invio di una richiesta di ricerca LDAP e la ricezione di una risposta.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 50 ms. I picchi (valori massimi) non devono essere superiori a 100 ms.</p></td>
</tr>
</tbody>
</table>


## Contatori di processori e processi

Nelle tabella seguente sono riportate soglie accettabili e informazioni sui processori e contatori di processo.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Contatore</th>
<th>Descrizione</th>
<th>Soglia</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Processore(_Totale)\% tempo processore</p></td>
<td><p>Indica la percentuale del tempo utilizzato dal processore per l'esecuzione di processi di applicazioni o del sistema operativo. Si tratta del periodo di tempo durante il quale il processore non è inattivo.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 75%.</p></td>
</tr>
<tr class="even">
<td><p>Processore(_Totale)\% tempo utente</p></td>
<td><p>Indica la percentuale del tempo di processore utilizzata in modalità utente. La modalità utente è una modalità di elaborazione limitata, progettata per applicazioni, sottosistemi di ambiente e sottosistemi integrali.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 75%.</p></td>
</tr>
<tr class="odd">
<td><p>Processore(_Totale)\% tempo privilegiato</p></td>
<td><p>Indica la percentuale del tempo di processore utilizzata in modalità privilegiata. La modalità privilegiata è una modalità di elaborazione progettata per i componenti del sistema operativo e per i driver che gestiscono l'hardware e consente l'accesso diretto all'hardware e all'intera memoria.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 75%.</p></td>
</tr>
<tr class="even">
<td><p>Sistema\Lunghezza coda processore (tutte le istanze)</p></td>
<td><p>Indica il numero di thread serviti da ciascun processore. Il contatore Lunghezza coda processore può essere utilizzato per identificare se eventuali conflitti di processore o un utilizzo elevato della CPU sono dovuti a una capacità insufficiente del processore per gestire i carichi di lavoro assegnati. Il contatore Lunghezza coda processore indica il numero di thread ritardati nella coda Processore pronto e in attesa di essere programmati per l'esecuzione. Il valore elencato è l'ultimo valore rilevato al momento in cui è stata effettuata la misurazione.</p></td>
<td><p>Il valore non deve essere superiore a 5 per processore.</p></td>
</tr>
<tr class="odd">
<td><p>Processo(*)\% tempo processore</p></td>
<td><p>Può essere usato per identificare specifici processi che consumano CPU.</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


## Contatori di memoria

Nelle tabella seguente sono riportate soglie accettabili e informazioni sui processori e contatori di memoria.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contatore</p></td>
<td><p>Descrizione</p></td>
<td><p>Soglia</p></td>
</tr>
<tr class="even">
<td><p>Memoria\Mbyte disponibili</p></td>
<td><p>Indica la quantità di memoria fisica, in megabyte (MB), immediatamente disponibile per l'allocazione in un processore o per l'utilizzo da parte del sistema. È uguale alla somma della memoria assegnata agli elenchi di pagine di memoria standby (cache), di memoria libera e di azzeramento. Per una spiegazione completa della gestione della memoria, fare riferimento a Microsoft Developer Network (MSDN) o alla &quot;Guida alle prestazioni del sistema e alla risoluzione dei problemi&quot; in Windows Server 2003 Resource Kit.</p></td>
<td><p>Deve rimanere al di sopra del 5% di RAM totale.</p></td>
</tr>
<tr class="odd">
<td><p>Memoria\% byte salvati in uso</p></td>
<td><p>Indica il rapporto tra Memoria\Byte salvati e Memoria\Limite memoria salvata. La memoria salvata è la memoria fisica in uso per la quale è stato riservato uno spazio nel file di paging nel caso in cui debba essere scritta su disco. Il limite della memoria salvata viene determinato dalla dimensione del file di paging. Se la dimensione del file di paging aumenta, aumenta anche il limite della memoria salvata e il rapporto si riduce. Il contatore visualizza solo la percentuale corrente, non si tratta di una media.</p></td>
<td><p>Se il valore è superiore all'80%, è un'indicazione che probabilmente il sistema è sottoposto a carico per fornire più memoria.</p></td>
</tr>
</tbody>
</table>


## Contatori .NET Framework

Nelle tabella seguente sono riportate soglie accettabili e informazioni sui processori e contatori di .NET Framework.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contatore</p></td>
<td><p>Descrizione</p></td>
<td><p>Soglia</p></td>
</tr>
<tr class="even">
<td><p>Memoria CLR .NET(*)\% tempo in GC</p></td>
<td><p>Indica il momento in cui si è verificato il processo GC (Garbage Collection). Se il contatore supera il limite, ciò è indice del fatto che la CPU sta eseguendo la pulitura e che non viene utilizzata in modo efficiente per il carico. La situazione può essere migliorata aggiungendo memoria al server.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 10%.</p></td>
</tr>
<tr class="odd">
<td><p>Eccezioni CLR .NET(*)\N. di eccezioni generate/sec</p></td>
<td><p>Indica il numero di eccezioni generate al secondo. Queste includono sia le eccezioni .NET Framework che le eccezioni non gestite e convertite in eccezioni .NET Framework. Ad esempio, l'eccezione riferimento puntatore null in codice non gestito verrebbe generata nuovamente in codice gestito come .NET Framework System.NullReferenceException. Questo contatore include sia le eccezioni gestite che quelle non gestite.</p></td>
<td><p>Il valore deve essere inferiore al 5% delle richieste al secondo totali (Server Web(_Totale)\Tentativi di connessione/sec * 0,05).</p></td>
</tr>
<tr class="even">
<td><p>Memoria CLR .NET(*)\Byte in tutti gli heap</p></td>
<td><p>Indica la somma di altri quattro contatori: Dimensione heap di generazione 0, Dimensione heap di generazione 1, Dimensione heap di generazione 2 e Dimensione heap oggetti grandi. Questo contatore indica la memoria corrente, in byte, allocata negli heap GC.</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


## Contatori di rete

Nelle tabella seguente sono riportate soglie accettabili e informazioni sui processori e contatori di rete comuni.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contatore</p></td>
<td><p>Descrizione</p></td>
<td><p>Soglia</p></td>
</tr>
<tr class="even">
<td><p>Interfaccia di rete(*)\Errori su pacchetti in uscita</p></td>
<td><p>Indica il numero di pacchetti in uscita che non è stato possibile trasmettere a causa di errori.</p></td>
<td><p>Il valore deve essere sempre 0.</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Errori di connessione</p></td>
<td><p>Indica il numero di connessioni TCP per le quali lo stato corrente è ESTABLISHED o CLOSE-WAIT. Il numero di connessioni TCP che possono essere stabilite è limitato dalla dimensione del pool non di paging. Quando il pool non di paging è esaurito, non è possibile stabilire nuove connessioni.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>TCPv4\Connessioni ripristinate</p></td>
<td><p>Indica il numero di volte che le connessioni TCP hanno effettuato una transizione diretta allo stato CLOSED dallo stato ESTABLISHED o dallo stato CLOSE-WAIT.</p></td>
<td><p>Un aumento del numero di ripristini o un aumento continuo del tasso di ripristini potrebbe indicare una mancanza di larghezza di banda.</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Connessioni ripristinate</p></td>
<td><p>Indica il numero di volte che le connessioni TCP hanno effettuato una transizione diretta allo stato CLOSED dallo stato ESTABLISHED o dallo stato CLOSE-WAIT.</p></td>
<td><p>Un aumento del numero di ripristini o un aumento continuo del tasso di ripristini potrebbe indicare una mancanza di larghezza di banda.</p></td>
</tr>
</tbody>
</table>


## Contatori di Netlogon

La tabella seguente riporta soglie accettabili e informazioni sui contatori più comuni per monitorare i problemi di autenticazione NTLM e per gli errori di MaxConcurrentAPI. Per maggiori informazioni, vedere l'articolo della Microsoft Knowledge Base numero 2688798 [Come eseguire l'ottimizzazione delle prestazioni per l'autenticazione NTLM tramite l'impostazione di MaxConcurrentApi](https://go.microsoft.com/fwlink/p/?linkid=38972).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contatore</p></td>
<td><p>Descrizione</p></td>
<td><p>Soglia</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\oggetti waiter Semaforo</p></td>
<td><p>Il numero di thread che sono in attesa di ottenere il semaforo.</p></td>
<td><p>Vedere l'articolo della Microsoft Knowledge Base numero 2688798 <a href="https://go.microsoft.com/fwlink/p/?linkid=38972">Come eseguire l'ottimizzazione delle prestazioni per l'autenticazione NTLM tramite l'impostazione di MaxConcurrentApi</a></p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Detentori semaforo</p></td>
<td><p>Il numero di thread che detiene il semaforo.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Acquisizioni semaforo</p></td>
<td><p>Il numero totale di volte in cui il semaforo è stato acquisito durante il tempo operativo della connessione relativa al canale di sicurezza o dall'avvio del sistema per _Total.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Timeout semaforo</p></td>
<td><p>Il numero totale di volte in cui il thread ha raggiunto il timeout mentre attendeva il semaforo durante il tempo operativo della connessione relativa al canale di sicurezza o dall'avvio del sistema per _Total.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Durata media detenzione semaforo</p></td>
<td><p>La durata media (in secondi) di detenzione del semaforo rispetto all'ultimo esempio.</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


## Contatori dei database

Nella seguente tabella, sono riportati i contatori dei requisiti di latenza I/O dei registri attivi e delle loro soglie accettabili. Quando si superano questi valori, le prestazioni del client si riducono. Ad esempio, gli utenti potrebbero riscontrare ritardi nel recapito dei messaggi oppure un rallentamento delle prestazioni.


> [!NOTE]
> La guida relativa alla latenza di archiviazione normale in Exchange 2013 è molto simile a quella di Exchange 2010. Altri contatori dei database sono disponibili in <A href="https://go.microsoft.com/fwlink/p/?linkid=52562">Contatori del server Cassette postali</A>.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contatore</p></td>
<td><p>Descrizione</p></td>
<td><p>Soglia</p></td>
</tr>
<tr class="even">
<td><p>Database di MSExchange ==&gt; Istanze(*)\Latenza media I/O letture database (allegato)</p></td>
<td><p>Indica l'intervallo di tempo medio in millisecondi (ms) per l'operazione di lettura database.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 20 ms.</p></td>
</tr>
<tr class="odd">
<td><p>Database di MSExchange ==&gt; Istanze(*)\Latenza media scrittura database I/O (Collegamento)</p></td>
<td><p>Indica l'intervallo di tempo medio, in ms, per l'operazione di scrittura nel database.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 50 ms.</p></td>
</tr>
<tr class="even">
<td><p>Database di MSExchange ==&gt; Istanze(*)\Latenza media I/O scritture log</p></td>
<td><p>Indica l'intervallo di tempo medio, in ms, per l'operazione di scrittura nel log.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 10 ms.</p></td>
</tr>
<tr class="odd">
<td><p>Database di MSExchange ==&gt; Istanze(*)\Latenza media I/O letture database (recupero)</p></td>
<td><p>Indica l'intervallo di tempo medio, in ms, per l'operazione di lettura del database passive.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 200 ms.</p></td>
</tr>
<tr class="even">
<td><p>Database di MSExchange ==&gt; Istanze(*)\Latenza media I/O scritture database (recupero)</p></td>
<td><p>Indica l'intervallo di tempo medio, in ms, per l'operazione di scrittura del database passive.</p></td>
<td><p>Deve essere inferiore alla latenza di lettura per la stessa istanza, così come misurata da Database di MSExchange ==&gt;Istanze(*)\Contatore latenza media I/O scritture database (recupero).</p></td>
</tr>
<tr class="odd">
<td><p>Database di MSExchange ==&gt; Istanze(*)\Lettura database I/O (Collegamento)/sec</p></td>
<td><p>Mostra il numero delle operazioni di lettura del database al secondo per ogni istanza del database collegato.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>Database di MSExchange ==&gt; Istanze(*)\Scrittura database I/O (Collegamento)/sec</p></td>
<td><p>Mostra il numero delle operazioni di scrittura del database al secondo per ogni istanza del database collegato.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>Database di MSExchange ==&gt; Istanze(*)\Scritture log/sec</p></td>
<td><p>Mostra il numero di log di scrittura al secondo per ogni istanza del database.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>Gestione attiva di MSExchange (_total)\Database montato</p></td>
<td><p>Mostra il numero di copie di database attivi sul server.</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


## ASP.NET

Nelle tabella seguente sono riportate soglie accettabili e informazioni sui contatori ASP.NET.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contatore</p></td>
<td><p>Descrizione</p></td>
<td><p>Soglia</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Riavvii applicazione</p></td>
<td><p>Indica il numero di volte in cui l'applicazione è stata riavviata durante il ciclo di vita del server Web.</p></td>
<td><p>Il valore deve essere sempre 0.</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET\Riavvii processo di lavoro</p></td>
<td><p>Indica il numero di volte in cui un processo di lavoro è stato riavviato sul computer.</p></td>
<td><p>Il valore deve essere sempre 0.</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Tempo di attesa richiesta</p></td>
<td><p>Indica l'intervallo di tempo, in millisecondi, di attesa in coda della richiesta più recente.</p></td>
<td><p>Il valore deve essere sempre 0.</p></td>
</tr>
<tr class="odd">
<td><p>Applicazioni ASP.NET(*)\Richieste nella coda dell'applicazione</p></td>
<td><p>Indica il numero di richieste presenti nella coda di richieste dell'applicazione.</p></td>
<td><p>Il valore deve essere sempre 0.</p></td>
</tr>
<tr class="even">
<td><p>Applicazioni ASP.NET ASP.NET(*)\Richieste in esecuzione</p></td>
<td><p>Mostra il numero di richieste attualmente in esecuzione.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>Applicazioni ASP.NET ASP.NET(*)\Richieste/sec</p></td>
<td><p>Indica il numero medio di richieste eseguite al secondo.</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


## Contatori Accesso client RPC

Nelle tabella seguente sono riportate soglie accettabili e informazioni sui contatori Accesso client RPC.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contatore</p></td>
<td><p>Descrizione</p></td>
<td><p>Soglia</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Latenza media RPC</p></td>
<td><p>Mostra la latenza RPC espressa in millisecondi (ms) calcolata sulla media degli ultimi pacchetti 1.024.</p></td>
<td><p>Deve essere inferiore a 250 ms.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Richieste RPC</p></td>
<td><p>Indica il numero di richieste client attualmente elaborate dal servizio Accesso client RPC.</p></td>
<td><p>Non deve essere superiore a 40.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Numero di utenti attivi</p></td>
<td><p>Indica il numero di utenti univoci che hanno rilevato alcune attività negli ultimi 2 minuti.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Numero di connessioni</p></td>
<td><p>Indica il numero totale di connessioni client mantenute.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Operazioni RPC al secondo</p></td>
<td><p>Indica la velocità a cui si verificano le operazioni RPC al secondo.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Numero di utenti</p></td>
<td><p>Indica il numero di utenti connessi al servizio.</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


## Contatori proxy HTTP

Nella tabella seguente sono riportate informazioni sui contatori proxy HTTP.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contatore</p></td>
<td><p>Descrizione</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Latenza media MailboxServerLocator</p></td>
<td><p>Mostra la latenza media (ms) delle chiamate relative al servizio Web MailboxServerLocator.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Latenza autenticazione media</p></td>
<td><p>Mostra la durata media relativa all'autenticazione delle richieste CAS su più di 200 campioni.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Latenza media di elaborazione del server ClientAccess</p></td>
<td><p>Mostra la latenza media (ms) relativa alla durata di elaborazione CAS (non include la durata dell'applicazione proxy) su più di 200 richieste.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Tasso di errore proxy server Cassette postali</p></td>
<td><p>Mostra la percentuale di connettività correlata agli errori tra il server Accesso client e i server MBX su oltre 200 campioni.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Richieste proxy in attesa</p></td>
<td><p>Mostra il numero di richieste proxy simultanee in attesa.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Richieste proxy/sec</p></td>
<td><p>Indica il numero medio di richieste proxy elaborate al secondo.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Richieste/sec</p></td>
<td><p>Indica il numero medio di richieste elaborate al secondo.</p></td>
</tr>
</tbody>
</table>


## Contatori Archivio informazioni

Nelle tabella seguente sono riportate soglie accettabili e informazioni sui contatori Archivio contatori.


> [!NOTE]
> La guida relativa alla latenza di archiviazione normale in Exchange 2013 è molto simile a quella di Exchange 2010. Altri contatori dei contatori Archivio informazioni sono disponibili in <A href="https://go.microsoft.com/fwlink/p/?linkid=52562">Contatori del server Cassette postali</A>.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contatore</p></td>
<td><p>Descrizione</p></td>
<td><p>Soglia</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS Store(*)\Richieste RPC</p></td>
<td><p>Indica le richieste RPC complessive attualmente in esecuzione all'interno del processo Archivio informazioni.</p></td>
<td><p>Il valore deve essere sempre inferiore a 70.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeIS Client Type(*)\Latenza media RPC</p></td>
<td><p>Indica una latenza RPC media del server, in ms, per gli ultimi 1.024 pacchetti per un determinato protocollo client.</p></td>
<td><p>Mediamente, il valore deve essere inferiore a 50 ms per ogni client.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS Store(*)\Latenza media RPC</p></td>
<td><p>La latenza media RPC (msec) è il valore medio in millisecondi delle richieste RPC per database. La media viene calcolata su tutte le RPC a partire dal momento in cui è stato caricato exrpc32.</p></td>
<td><p>Deve essere sempre inferiore a 50 ms, con punte inferiori a 100 ms.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeIS Store(*)\Operazioni RPC al secondo</p></td>
<td><p>Mostra il numero di operazioni RPC al secondo per ogni istanza del database.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS Client Type(*)\Operazioni RPC/sec</p></td>
<td><p>Mostra il numero di operazioni RPC al secondo per ogni connessione di tipo client.</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


## Contatori relativi ai server Accesso client

Nella tabella seguente vengono visualizzate informazioni sui contatori di connessione client e sui contatori IIS (Internet Information Services).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contatore</p></td>
<td><p>Descrizione</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Richieste al secondo</p></td>
<td><p>Indica il numero di richieste HTTP ricevute dal client tramite ASP.NET al secondo. Determina la frequenza delle richieste Exchange ActiveSync correnti. Viene utilizzato solo per determinare il carico utente corrente.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange ActiveSync\Comandi ping in sospeso</p></td>
<td><p>Indica il numero di comandi Ping attualmente in sospeso nella coda.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Comandi di sincronizzazione al secondo</p></td>
<td><p>Indica il numero di comandi di sincronizzazione elaborati al secondo. I client utilizzano questo comando per sincronizzare gli elementi in una cartella.</p></td>
</tr>
<tr class="odd">
<td><p>Servizio Disponibilità di Microsoft Exchange\Richieste di disponibilità al secondo</p></td>
<td><p>Indica il numero medio di richieste servite al secondo. La richiesta può essere soltanto relative alle informazioni sulla disponibilità o può includere proposte. Una richiesta può contenere più cassette postali. Determina la frequenza con cui si verificano richieste al servizio Disponibilità.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange OWA\Utenti univoci correnti</p></td>
<td><p>Indica il numero di utenti univoci attualmente connessi a Outlook Web App. Questo valore consente di monitorare il numero di sessioni utente univoche attive, in modo che gli utenti vengano rimossi dal contatore solo dopo il timeout della rispettiva sessione. Consente di determinare il carico utente corrente.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange OWA\Richieste al secondo</p></td>
<td><p>Indica il numero di richieste gestite da Outlook Web App al secondo. Consente di determinare il carico utente corrente.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeAutodiscover\Requests/sec</p></td>
<td><p>Indica il numero medio di richieste del servizio di individuazione automatica elaborate al secondo. Consente di determinare il carico utente corrente.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeWS\Requests/sec</p></td>
<td><p>Indica il numero medio di richieste elaborate al secondo. Consente di determinare il carico utente corrente.</p></td>
</tr>
<tr class="even">
<td><p>Servizio Web(_Total)\Connessioni correnti</p></td>
<td><p>Indica il numero corrente di connessioni stabilite con il servizio Web. Consente di determinare il carico utente corrente.</p></td>
</tr>
<tr class="odd">
<td><p>Servizio Web (sito Web predefinito)\Connessioni correnti</p></td>
<td><p>Mostra il numero di connessioni correnti stabilite con il sito Web predefinito che corrisponde al numero di connessioni che accedono al ruolo server CAS front-end. Consente di determinare il carico utente corrente.</p></td>
</tr>
<tr class="even">
<td><p>Servizio Web(_Total)\Tentativi di connessione/sec</p></td>
<td><p>Indica la frequenza con cui vengono effettuati i tentativi di connessione al servizio Web. Consente di determinare il carico utente corrente.</p></td>
</tr>
<tr class="odd">
<td><p>Servizio Web(_Total)\Richieste altri metodi/sec</p></td>
<td><p>Indica la frequenza delle richieste HTTP eseguite che non utilizzano i metodi OPTIONS, GET, HEAD, POST, PUT, DELETE, TRACE, MOVE, COPY, MKCOL, PROPFIND, PROPPATCH, SEARCH, LOCK o UNLOCK. Consente di determinare il carico utente corrente.</p></td>
</tr>
</tbody>
</table>


## Contatori di gestione del carico di lavoro

Nella tabella seguente sono riportate informazioni sui contatori di gestione del carico di lavoro di Exchange. Questi contatori sono importanti da monitorare perché la gestione del carico di lavoro potrebbe eseguire attività in background durante i periodi non di punta.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contatore</p></td>
<td><p>Descrizione</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement Workloads(*)\ActiveTasks</p></td>
<td><p>Mostra il numero di attività attive al momento in background per la gestione del carico di lavoro.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange WorkloadManagement Workloads(*)\CompletedTasks</p></td>
<td><p>Mostra il numero delle attività di gestione del carico di lavoro che sono state completate.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement Workloads(*)\QueuedTasks</p></td>
<td><p>Mostra il numero il numero di attività di gestione che sono attualmente in coda di elaborazione.</p></td>
</tr>
</tbody>
</table>


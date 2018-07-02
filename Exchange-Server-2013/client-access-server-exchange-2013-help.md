---
title: 'Server Accesso client: Exchange 2013 Help'
TOCTitle: Server Accesso client
ms:assetid: 87e206ab-7a7b-4b4f-be1a-5035713c74d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298114(v=EXCHG.150)
ms:contentKeyID: 50481114
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Server Accesso client

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-07-02_

In Microsoft Exchange 2013 sono state apportate importanti modifiche architettoniche ai ruoli del server di Exchange. Al posto dei cinque ruoli del server presenti in Exchange 2010 ed Exchange 2007, in Exchange 2013 sono disponibili solo tre ruoli del server: il server Accesso client e il server Cassette postali, e con Service Pack 1, il ruolo del server Trasporto Edge.


> [!NOTE]
> Exchange 2013 può anche lavorare con il ruolo del server Trasporto Edge di Exchange 2010.



Il server Cassette postali di Exchange 2013 include tutti i componenti server tradizionali presenti in Exchange 2010: i protocolli di accesso client, i servizi di trasporto, i database delle cassette postali e la messaggistica unificata (il server Accesso client reindirizza il traffico SIP generato dalle chiamate in ingresso al server Cassette postali). Per ulteriori informazioni sul server Cassette postali di Exchange 2013, vedere [Server Cassette postali](mailbox-server-exchange-2013-help.md).

Il server Accesso client fornisce l'autenticazione, il proxy e i servizi di reindirizzamento limitato e offre tutti i protocolli di accesso client normalmente disponibili: HTTP, POP, IMAP e SMTP. Il server Accesso Client è un server thin e senza stato che non esegue alcun rendering dei dati. Non vi sono mai oggetti in coda o archiviati sul server Accesso client. Per ulteriori informazioni sulla nuova architettura di Exchange 2013, vedere [Novità di Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).


> [!WARNING]
> I server Accesso client non sono supportati in reti perimetrali e devono essere distribuiti nell'ambiente Active Directory interno. Ogni sito di Active Directory che contiene un server Cassette postali deve contenere anche un server Accesso client.



Queste modifiche all'architettura hanno comportato dei cambiamenti nella connettività client. In primo luogo, RPC/TCP non è più un protocollo di accesso diretto supportato. Significa che la connettività di Outlook deve avvenire tramite RPC su HTTPS (detto anche Outlook via Internet) oppure con Exchange 2013 SP1 e Outlook 2013 SP1, MAPI tramite HTTP. Come conseguenza di queste modifiche, non è necessario avere il servizio Accesso client RPC sul server Accesso client. Inoltre, è richiesto un numero minore di spazi dei nomi per una soluzione con resilienza del sito rispetto a quanto imposto da Exchange 2010 e non è più necessario fornire l'affinità per il servizio Accesso client RPC. Inoltre, i client Outlook non si connettono più a un nome di dominio completo (FQDN) di server come facevano nelle precedenti versioni di Exchange. Utilizzando l'individuazione automatica, Outlook individua un nuovo punto di connessione costituito dal GUID della cassetta postale dell'utente + @ + la parte del dominio dell'indirizzo SMTP primario dell'utente. Questa modifica rende meno probabile la visualizzazione agli utenti del temuto messaggio "L'amministratore ha apportato una modifica alla cassetta postale dell'utente". Solo Outlook 2007 e versioni successive sono supportati con Exchange 2013.

## Funzionalità del server Accesso client

Il server Accesso client in Exchange 2013 funziona come una porta di ingresso, che accoglie tutte le richieste dei client e le instrada al database delle cassette postali attivo corretto. Il server Accesso client fornisce funzionalità di sicurezza della rete quali Secure Sockets Layer (SSL) e l'autenticazione client; inoltre, gestisce le connessioni client attraverso il reindirizzamento e la funzionalità proxy. Il server Accesso client autentica le connessioni client e, nella maggior parte dei casi, usa un proxy per una richiesta al server Cassette postali che ospita la copia attualmente attiva del database contenente la cassetta postale dell'utente. In alcuni casi, il server Accesso client potrebbe reindirizzare la richiesta a un server Accesso client più adatto, sia in una posizione diversa sia su cui è in esecuzione una versione più recente di Exchange Server.

Il server Accesso Client presenta le seguenti caratteristiche:

  - **Server senza stato**   Nelle precedenti versioni di Exchange, molti protocolli di accesso client richiedevano l'affinità di sessione. Ad esempio, Outlook Web App richiedeva che tutte le richieste provenienti da un client specifico fossero gestite da un determinato server Accesso client all'interno di un array con bilanciamento del carico di server Accesso client. In Exchange 2013, il server Accesso Client è senza stato. In altre parole, visto che tutta l'elaborazione per la cassetta postale avviene sul server Cassette postali, non è importante quale server Accesso client in un array di server Accesso client riceve ogni singola richiesta dei client. Questo cambiamento di funzionalità implica che l'affinità di sessione non è più richiesta a livello del bilanciamento del carico. Questo consente di bilanciare le connessioni in ingresso ai server Accesso client utilizzando semplici tecniche fornite dalla tecnologia di bilanciamento del carico, come il round robin DNS. Consente inoltre ai dispositivi di bilanciamento del carico hardware di supportare in maniera significativa più connessioni simultanee.

  - **Pool di connessioni**   I server Accesso client gestiscono l'autenticazione client e inviano i dati AuthN al server Cassette postali. L'account utilizzato da tutti i server Accesso client per connettersi ai server Cassette postali è un account con privilegi membro del gruppo Exchange Servers. Questo consente ai server Accesso client di creare pool di connessioni ai server Cassette postali in maniera efficace. Un array di server Accesso client può gestire milioni di connessioni client da Internet, ma viene utilizzato un numero di molto inferiore di connessioni per il proxy delle richieste ai server Cassette postali rispetto alle versioni precedenti di Exchange. Questa scelta migliora l'efficienza di elaborazione e la latenza end-to-end.

## Attività di gestione sul server Accesso Client

In Exchange 2013, esistono diverse attività cruciali che possono essere eseguite sul server Accesso client. La gestione dei certificati digitali viene eseguita principalmente sul server Accesso client; anche parte della gestione dei protocolli client per Exchange ActiveSync, POP3 e IMAP4 viene gestita sul server Accesso client.


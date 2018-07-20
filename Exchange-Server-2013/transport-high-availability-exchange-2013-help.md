---
title: 'Disponibilità elevata di trasporto: Exchange 2013 Help'
TOCTitle: Disponibilità elevata di trasporto
ms:assetid: e9ec6d05-f441-4cca-8592-8f7469948299
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657506(v=EXCHG.150)
ms:contentKeyID: 50481969
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disponibilità elevata di trasporto

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-15_

In Microsoft Exchange Server 2013 l'elevata disponibilità del trasporto è responsabile della conservazione delle copie ridondanti dei messaggi prima e dopo l'avvenuto recapito. Le prestazioni di Exchange 2013 risultano migliorate dopo l'introduzione delle funzionalità ad alta disponibilità in Exchange Server 2010, ad esempio, la ridondanza shadow e il dumpster di trasporto, che garantiscono che i messaggi non vadano persi nel transito.

Di seguito viene riportato un riepilogo dei principali miglioramenti dovuti all'elevata disponibilità del trasporto in Exchange 2013:

  - La ridondanza shadow crea una copia ridondante del messaggio su un server diverso prima che il messaggio venga accettato o riconosciuto. Il supporto del server di invio o la mancanza di supporto per la ridondanza shadow è irrilevante.

  - La ridondanza shadow riconosce sia i gruppi di disponibilità del database (DAG) che i siti Active Directory come limiti all'elevata disponibilità del trasporto. In questo modo viene ridotto il numero di server in grado di mantenere copie ridondanti dei messaggi e viene eliminato il traffico di manutenzione dei messaggi ridondanti non necessari nei gruppi di disponibilità del database o nei siti Active Directory.
    
    Per ulteriori informazioni, vedere [Ridondanza shadow](shadow-redundancy-exchange-2013-help.md).

  - Il dumpster di trasporto è stato migliorato e attualmente viene denominato *Rete sicura*. La rete sicura archivia i messaggi correttamente elaborati dal servizio di trasporto sui server Cassette postali. L'attività della rete sicura è ottimale per i server Cassette postali in un gruppo di disponibilità del database, ma è funzionale anche per più server Cassette postali dello stesso sito Active Directory non appartenenti ad alcun gruppo di disponibilità del database.

  - La stessa rete sicura è stata resa ridondante su un altro server. È importante evitare un singolo punto di errore in Exchange 2013, dal momento che il servizio di trasporto e i database delle cassette postali si trovano entrambi sul server Cassette postali.
    
    Per ulteriori informazioni, vedere [Rete sicura](safety-net-exchange-2013-help.md).

Il diagramma riportato di seguito fornisce un riepilogo generale del funzionamento dell'elevata disponibilità del trasporto in Exchange 2013.

![Panoramica dell'alta disponibilità di trasporto](images/JJ657506.88f2284d-8afe-4c8f-94a6-cd4c097a55d8(EXCHG.150).gif "Panoramica dell'alta disponibilità di trasporto")

1.  Un server Cassette postali di Exchange 2013 denominato Mailbox01 riceve un messaggio da un server SMTP che non si trova nell'ambito dell'elevata disponibilità del trasporto. L' *ambito dell'elevata disponibilità del trasporto* è un gruppo di disponibilità del database (DAG) o un sito Active Directory in ambienti non DAG. Il messaggio potrebbe provenire da un server SMTP di terze parti, da un server SMTP Internet proxy tramite un server Accesso client o da un altro server Exchange 2013.

2.  Prima di confermare la ricezione del messaggio, Mailbox01 avvia una nuova sessione SMTP per un altro server Cassette postali di Exchange 2013 denominato Mailbox03 che non si trova nell'ambito dell'elevata disponibilità del trasporto e che creerà una copia ridondante del messaggio. In ambienti DAG, è preferibile un server shadow in un sito Active Directory remoto. Mailbox01 è il server primario che custodisce il messaggio principale e Mailbox03 è il server shadow che custodisce il messaggio shadow.

3.  Il servizio di trasporto su Mailbox01 elabora il messaggio principale.
    
    1.  In questo esempio, la cassetta postale del destinatario si trova su Mailbox01 e il servizio di trasporto trasmette il messaggio al servizio Trasporto cassette postali locale.
    
    2.  Il servizio Trasporto cassette postali recapita il messaggio al database delle cassette postali locale.
    
    3.  Mailbox01 mette in coda lo stato di eliminazione per Mailbox03, a indicare che il messaggio principale è stato elaborato correttamente e Mailbox01 sposta una copia del messaggio principale nella rete sicura principale locale. Si noti che il messaggio viene spostato tra le code all'interno dello stesso database delle code.

4.  Mailbox03 interroga periodicamente Mailbox01 sullo stato di eliminazione del messaggio principale.

5.  Quando Mailbox03 stabilisce che Mailbox01 ha completato l'elaborazione del messaggio principale, Mailbox03 sposta il messaggio shadow nella rete sicura shadow locale. Si noti che il messaggio viene spostato tra le code all'interno dello stesso database delle code.

Il messaggio viene conservato nella rete sicura principale e nella rete sicura shadow fino alla scadenza determinata da un valore di timeout configurabile. Se si verifica un failover nel database delle cassette postali prima della scadenza del messaggio, la rete sicura principale di Mailbox01 invierà nuovamente il messaggio. Se Mailbox01 non è disponibile, la rete sicura shadow su Mailbox03 subentrerà e invierà nuovamente il messaggio.

## Ridondanza dei messaggi nel servizio di trasporto front-end sui server Accesso client

Un server Accesso client non ha code di messaggi. È il server proxy senza stato che utilizza il servizio di trasporto front-end per accettare connessioni SMTP in ingresso e a inoltrarle al servizio di trasporto su un server Cassette postali. Il servizio di trasporto front-end mantiene aperta la sessione SMTP con il server di invio mentre il messaggio principale viene trasmesso al servizio di trasporto su un server Cassette postali e viene creata una copia shadow del messaggio dal servizio di trasporto su un server Cassette postali diverso nell'ambito dell'elevata disponibilità del trasporto. Solo dopo aver completato la creazione del messaggio principale e del messaggio shadow, il comando fine dei dati SMTP viene reinviato al server SMTP di invio tramite il server Accesso client.


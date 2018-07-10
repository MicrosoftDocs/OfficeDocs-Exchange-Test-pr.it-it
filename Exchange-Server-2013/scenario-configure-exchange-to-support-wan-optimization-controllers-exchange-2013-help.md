---
title: 'Scenario: Configurare Exchange per supportare i controller di ottimizzazione della WAN: Exchange 2013 Help'
TOCTitle: 'Scenario: Configurare Exchange per supportare i controller di ottimizzazione della WAN'
ms:assetid: 1f407698-0b71-45a3-867a-640ccf7351da
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633456(v=EXCHG.150)
ms:contentKeyID: 52063052
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Scenario: Configurare Exchange per supportare i controller di ottimizzazione della WAN

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-09-28_

In Microsoft Exchange Server 2013, la crittografia Transport Layer Security (TLS) è obbligatoria per tutta la comunicazione SMTP nel servizio di trasporto tra i server Cassette postali. Ciò aumenta la sicurezza complessiva delle comunicazioni del servizio di trasporto tra i server Cassette postali. Tuttavia, in alcune topologie in cui vengono utilizzati dispositivi WAN Optimization Controller (WOC), è consigliabile evitare la crittografia TLS del traffico SMTP. È possibile disabilitare TLS per le comunicazioni tra il servizio di trasporto tra i server Cassette postali per questi scenari specifici.

Considerare la topologia illustrata nella figura seguente. Questa topologia a quattro siti parte dal presupposto che i due siti centrali e Branch Office 2 siano ben collegati e che la connessione tra Central Office Site 1 e Branch Office 1 si trovi su un collegamento WAN. L'azienda ha installato due dispositivi WOC su questo collegamento per comprimere e ottimizzare il traffico sul collegamento WAN.

**Topologia di rete di esempio con dispositivi WOC**

![Topologia di esempio con ottimizzatori WAN](images/Ee633456.52876869-52f1-4c0f-85b2-7a850643e8a1(EXCHG.150).gif "Topologia di esempio con ottimizzatori WAN")

In questa topologia, poiché Exchange 2013 utilizza la crittografia TLS per la comunicazione tra i server Cassette postali, il traffico SMTP che attraversa il collegamento WAN non può essere compresso. In teoria, tutto il traffico SMTP che attraversa il collegamento WAN non dovrebbe essere crittografato, conservando la protezione TLS nei siti collegati correttamente. Exchange 2013 offre l'opzione di disabilitare la crittografia TLS per il traffico tra i siti configurando i connettori di ricezione. Utilizzando questa capacità in Exchange 2013, è possibile configurare un'eccezione nel traffico SMTP tra Central Office Site 1 e Branch Office 1, come mostrato nella seguente figura.

**Flusso di un messaggio logico preferito**

![Flusso di un messaggio logico preferito](images/Ee633456.e0fe62fa-1bad-4d43-9eaf-205a9b8d07e1(EXCHG.150).gif "Flusso di un messaggio logico preferito")

La configurazione consigliata è quella di limitare il traffico SMTP non crittografato solo a quei messaggi che passano sul collegamento WAN. Pertanto, le comunicazioni del servizio di trasporto all'interno del sito tra i server Cassette postali in tutti i siti e le comunicazioni del servizio di trasposto tra i siti tra i server Cassette postali che non comprendono Branch Office 1 devono essere tutte crittografate tramite TLS.

Per raggiungere questo risultato finale, è necessario effettuare le seguente azioni, nell'ordine specificato, in ogni server Cassette postali nei siti che contengono dispositivi WOC (Central Office Site 1 e Branch Office 1 nella topologia di esempio):

1.  Abilitare l'autenticazione a Exchange Server downgrade.

2.  Creare un connettore di ricezione dedicato per gestire il traffico attraverso la connessione che contiene dispositivi WOC.
    
    1.  Configurare la proprietà dell'intervallo di indirizzi IP remoti del connettore di ricezione dedicato per gli intervalli di indirizzi IP dei server Cassette postali nel sito remoto di Active Directory.
    
    2.  Disabilitare TLS nel connettore di ricezione dedicato.

Inoltre, è necessario effettuare le seguente azioni per garantire che tutto il traffico SMTP sulla WAN venga gestito dai connettori di ricezione dedicati creati:

  - Configurare i siti di Active Directory che parteciperanno alle comunicazioni non TLS come siti hub per forzare tutto il flusso di messaggi attraverso i connettori di ricezione dedicati (Central Office Site 1 e Branch Office Site 1 nella topologia di esempio).

  - Verificare che i costi di collegamento al sito IP di Active Directory sono configurati in modo da garantire che il percorso di routing più conveniente verso il sito remoto (Branch Office 1 nella topologia di esempio) attraversi il collegamento di rete che presenta dispositivi WOC. Assegnare un costo specifico di Exchange ai collegamenti del sito di Active Directory in base alle esigenze.

Nelle seguenti sezioni viene fornita una panoramica su questa procedura. Per istruzioni dettagliate su come configurare l'organizzazione per questo scenario. vedere [Disabilitare TLS tra siti Active Directory](disable-tls-between-active-directory-sites-exchange-2013-help.md).

**Sommario**

Downgrade authentication over TLS-disabled connections

Create and configure dedicated Receive connectors

Configure Hub sites

Configure Exchange-specific Active Directory site link costs

## Eseguire il downgrade dell'autenticazione su connessioni dove Transport Layer Security (TLS) è disabilitato

L'autenticazione Kerberos viene utilizzata con la crittografia TLS in Exchange. Quando TLS viene disabilitato nelle comunicazioni del servizio di trasporto tra i server Cassette postali, è necessario eseguire un'altra forma di autenticazione. Quando Exchange 2013 comunica con altri server che eseguono Exchange e che non supportano **X-ANONYMOUSTLS**, ripiega sull'autenticazione Generic Security Services Application Programming Interface (GSSAPI). Tutte le comunicazione del servizio di trasporto tra i server Cassette postali di Exchange 2013 utilizzano **X-ANONYMOUSTLS**. Quando il servizio di trasporto viene configurato nel server Cassette postali affinché utilizzi l'autenticazione a Exchange Server downgrade, si sta effettivamente abilitando l'autenticazione GSSAPI per le comunicazioni del servizio di trasporto con altri server Cassette postali di Exchange 2013.

Inizio pagina

## Creare e configurare connettori di ricezione dedicati

È necessario creare i connettori di ricezione che saranno gli unici responsabili della gestione del traffico crittografato non da TLS. L'utilizzo di connettori di ricezione separati per questo scopo garantisce che tutto il traffico che non passa attraverso il collegamento WAN resti protetto dalla crittografia TLS.

Per limitare i connettori di ricezione dedicati solo al traffico sulla WAN, è necessario configurare la proprietà dell'intervallo di indirizzi IP remoti. Exchange usa sempre il connettore con l'intervallo di indirizzi IP remoti più specifico. Quindi, questi nuovi connettori saranno scelti come connettori preferiti rispetto al connettore di ricezione predefinito configurato per ricevere i messaggi.

Tornando alla topologia di esempio, partire dal presupposto che la subnet di classe C 10.0.1.0/24 viene utilizzata per Central Office Site 1 e che 10.0.2.0/24 viene utilizzata per Branch Office 1. Per prepararsi alla disabilitazione di TLS tra questi due siti, è necessario fare quanto segue:

1.  Creare un connettore di ricezione denominato WAN in ogni server Cassette postali in Central Office Site 1 e Branch Office 1.

2.  Configurare l'intervallo di indirizzi IP remoti di 10.0.2.0/24 su ogni connettore di ricezione dedicato in Central Office Site 1.

3.  Configurare l'intervallo di indirizzi IP remoti di 10.0.1.0/24 su ogni connettore di ricezione dedicato in Branch Office 1.

4.  Disabilitare TLS in tutti i connettori di ricezione dedicati.

Il risultato finale viene visualizzato nella seguente figura (la proprietà dell'intervallo di indirizzi IP remoti dei connettori di ricezioni denominati WAN è indicata tra parentesi). Solo un unico server Cassette postali viene visualizzato in Branch Office 1 e Branch Office 2 viene omesso per maggiore chiarezza.

**Configurazione del connettore di ricezione**

![Configurazione del connettore di ricezione](images/Ee633456.1821b3db-1f7a-4ae7-afbc-5c99e117f976(EXCHG.150).gif "Configurazione del connettore di ricezione")

Inizio pagina

## Configurare i siti hub

Per impostazione predefinita, un server Cassette postali di Exchange 2013 tenterà una connessione diretta al server Cassette postali più vicino alla destinazione finale del messaggio specifico. Nella topologia di esempio, se un utente in Branch Office 2 invia un messaggio a un utente in Branch Office 1, il server Cassette postali in Branch Office 2 si connetterà direttamente al server Cassette postali in Branch Office 1 per recapitare il messaggio. La connessione verrà crittografata, quindi non è consigliabile nella topologia specifica. Per far passare tali messaggi attraverso i server Cassette postali in Central Office Site 1, garantendo in questo modo che non vengano crittografati mentre transitano sul collegamento WAN, Central Office Site 1 e Branch Office 1 devono essere configurati come siti hub. In breve, qualsiasi sito dove è presente un server Cassette postali con un connettore di ricezione in cui TLS è disabilitato deve essere configurato come sito hub per poter forzare i server in altri siti a instradare il traffico attraverso tale sito. Per ulteriori informazioni, vedere [Configurare impostazioni di routing della posta di Exchange in Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

Inizio pagina

## Configurare costi di collegamento al sito di Active Directory specifici per Exchange

Configurare i siti hub non è sufficiente a garantire che tutto il traffico venga decrittografato sul collegamento WAN. Questo perché Exchange instraderà i messaggi attraverso i siti hub solo se il sito hub si trova all'interno di un percorso di instradamento con il costo più basso. Ad esempio, si supponga che i costi del collegamento al sito IP per la nostra topologia di esempio siano configurati in Active Directory come configurato nella seguente figura (Central Office Site 2 viene omesso per maggiore chiarezza).

**Costi del collegamento al sito IP per la topologia di esempio**

![Costi di collegamento al sito IP per topologia di esempio](images/Ee633456.099deb15-795a-417a-b6aa-925b3bedf8b4(EXCHG.150).gif "Costi di collegamento al sito IP per topologia di esempio")

In questo caso, il percorso da Branch Office 2 a Branch Office 1 che passa attraverso il sito hub ha un costo totale pari a 12 (6+6), mentre il costo del percorso diretto è 10. Quindi, nessun messaggio da Branch Office 2 a Branch Office 1 passerà tramite Central Office Site 1 e perciò tutto il traffico utilizzerà ancora la crittografia TLS.

Per evitare questo problema, è necessario determinare un costo specifico per Exchange superiore a 12 per il collegamento al sito IP tra Branch Office 2 e Branch Office 1, come mostrato nella seguente figura. Ciò garantirà che tutti i messaggi passino attraverso il canale non crittografato tra Central Office Site 1 e Branch Office 1.

**Topologia di esempio configurata con i costi del collegamento al sito IP specifici di Exchange**

![Topologia di esempio con costi di Exchange](images/Ee633456.cd036fe0-c37d-479e-a4c1-235e17e90ca7(EXCHG.150).gif "Topologia di esempio con costi di Exchange")

Per ulteriori informazioni, vedere [Configurare impostazioni di routing della posta di Exchange in Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

Inizio pagina


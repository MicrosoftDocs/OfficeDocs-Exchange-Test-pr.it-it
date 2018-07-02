---
title: 'Reputazione mittente e agente di analisi protocollo: Exchange 2013 Help'
TOCTitle: Reputazione mittente e agente di analisi protocollo
ms:assetid: c4c34235-d545-41e7-ac2f-1dd43aaa3708
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124512(v=EXCHG.150)
ms:contentKeyID: 50481637
ms.date: 01/08/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Reputazione mittente e agente di analisi protocollo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-16_

La reputazione mittente è una funzionalità di protezione dalla posta indesiderata di Exchange che blocca i messaggi in base alle caratteristiche del mittente. La reputazione mittente si basa su dati permanenti relativi al mittente per determinare l'eventuale azione da eseguire su un messaggio in arrivo. L'agente di analisi del protocollo è l'agente che si occupa della funzionalità di reputazione mittente.

Quando vengono configurati su un server Exchange, gli agenti di protezione dalla posta indesiderata agiscono sui messaggi in modo cumulativo per ridurre il numero di messaggi indesiderati ricevuti dall'organizzazione.

**Sommario**

Calcolo del livello di reputazione mittente

Utilizzo del livello di reputazione mittente

Abilitazione e configurazione del rilevamento di server proxy aperti

Impostazione della soglia di blocco del livello reputazione mittente

## Calcolo del livello di reputazione mittente

Il livello di reputazione mittente (SRL, Sender Reputation Level) viene calcolato in base alle seguenti statistiche:

  - **Analisi HELO/EHLO**   I comandi HELO e EHLO SMTP consentono di fornire il nome di dominio, ad esempio Contoso.com o l'indirizzo IP, del server mittente SMTP al server ricevente SMTP. Gli utenti malintenzionati o gli *spammer* spesso falsificano l'istruzione HELO/EHLO in vari modi. Ad esempio, digitano un indirizzo IP che non corrisponde all'indirizzo IP da cui ha origine la connessione. Gli spammer, inoltre, inseriscono nell'istruzione HELO domini supportati in locale sul server di destinazione, nel tentativo di far risultare i domini come appartenenti all'organizzazione. In altri casi, gli spammer modificano il dominio trasmesso nell'istruzione HELO. Il comportamento tipico di un utente autorizzato può essere quello di utilizzare un insieme di domini diversi, ma relativamente costanti, nelle istruzioni HELO.
    
    Pertanto, l'analisi dell'istruzione HELO/EHLO in base al mittente può indicare che il mittente è probabilmente uno spammer. Ad esempio, è molto più probabile che un mittente che fornisce numerose istruzioni univoche HELO/EHLO diverse in un intervallo di tempo specifico sia uno spammer. I mittenti che forniscono costantemente un indirizzo IP nell'istruzione HELO che non corrisponde all'indirizzo IP di origine determinato dall'agente filtro connessioni sono con molta probabilità spammer. I mittenti remoti che forniscono costantemente un nome di dominio locale nell'istruzione HELO che si trova nella stessa organizzazione del server Exchange sono con molta probabilità spammer.

  - **Ricerca DNS inversa**   La reputazione mittente verifica inoltre che l'indirizzo IP di origine da cui il mittente ha trasmesso il messaggio corrisponda al nome di dominio registrato che il mittente invia nel comando SMTP HELO o EHLO.
    
    La reputazione mittente esegue una query DNS inversa inviando l'indirizzo IP di origine a DNS. Il risultato restituito da DNS è il nome di dominio registrato utilizzando l'autorità dei nomi di dominio per l'indirizzo IP. La reputazione mittente confronta il nome di dominio restituito da DNS con il nome di dominio che il mittente ha inviato nel comando SMTP HELO/EHLO. Se i nomi di dominio non corrispondono, è probabile che il mittente sia uno spammer e il valore di classificazione SRL globale per il mittente sia aumentato.
    
    L'agente ID mittente esegue un'attività simile, ma il cui esito è positivo se i mittenti autorizzati possono aggiornare l'infrastruttura DNS per identificare tutti i server SMTP di invio della posta elettronica nell'organizzazione. L'esecuzione di una ricerca DNS inversa consente di identificare i potenziali spammer.

  - **Analisi dei valori di classificazione SCL nei messaggi provenienti da un determinato mittente**   Quando l'agente Filtro contenuto elabora un messaggio, assegna un livello di probabilità di posta indesiderata (SCL) al messaggio. Il livello di probabilità di posta indesiderata è un numero compreso tra 0 e 9. Più alto è il livello, più alta è la probabilità che si tratti di un messaggio di posta indesiderata. I dati di ciascun mittente e le classificazioni del livello di probabilità di posta indesiderata restituiti dai messaggi vengono mantenuti per l'analisi eseguita dalla reputazione mittente. La reputazione mittente calcola le statistiche sul mittente in base al rapporto fra tutti i messaggi provenienti da quel mittente che in passato avevano una classificazione bassa del livello di probabilità di posta indesiderata e tutti i messaggi dello stesso mittente che in passato avevano una classificazione alta del livello di probabilità di posta indesiderata. Inoltre, al livello di reputazione mittente globale viene applicato il numero di messaggi con una classificazione alta del livello di probabilità di posta indesiderata che il mittente ha inviato nell'ultimo giorno.

  - **Test di proxy aperto del mittente**   Un *proxy aperto* è un server proxy che accetta le richieste di connessione provenienti da chiunque e da qualsiasi luogo e inoltra il traffico come se avesse origine dagli host locali. I server proxy inoltrano il traffico TCP tramite gli host firewall per fornire alle applicazioni utente un accesso trasparente attraverso il firewall. Poiché i protocolli proxy sono leggeri e indipendenti dai protocolli delle applicazioni utente, i proxy possono essere utilizzati da molti servizi diversi. I proxy possono anche essere utilizzati per condividere un'unica connessione Internet tra più host. In genere la configurazione dei proxy consente solo agli host considerati attendibili all'interno del firewall di attraversare i proxy. Un mittente legittimo può essere un proxy aperto a causa di una configurazione errata non intenzionale o malware.
    
    I proxy aperti rappresentano per gli utenti malintenzionati l'occasione ideale per nascondere la loro vera identità e avviare attacchi Denial of Service (DoS) o inviare posta indesiderata. Dal momento che sempre più server proxy vengono configurati per essere aperti per impostazione predefinita, i proxy aperti sono diventati sempre più comuni. Gli utenti malintenzionati possono inoltre utilizzare più proxy aperti per mascherare l'indirizzo IP di origine del mittente.
    
    La reputazione mittente esegue il test del proxy aperto formattando una richiesta SMTP nel tentativo di connettersi al server Exchange dal proxy aperto. Se una richiesta SMTP viene ricevuta dal proxy, la reputazione mittente si accerta che il proxy sia un proxy aperto e aggiorna la statistica del test dei proxy aperti per il mittente.

La reputazione mittente valuta ognuna di tali statistiche e calcola un SRL per ogni mittente. Il livello reputazione mittente è un numero compreso tra 0 e 9 che indica la probabilità che uno specifico mittente sia uno spammer o un utente malintenzionato. Il valore 0 indica che il mittente probabilmente non è uno spammer, mentre il valore 9 indica che il mittente probabilmente è uno spammer.

È possibile configurare una soglia di blocco tra 0 e 9 in corrispondenza della quale la reputazione mittente invia una richiesta all'agente Filtro mittente per impedire al mittente di inviare messaggi nell'organizzazione. Quando un mittente è bloccato viene aggiunto all'elenco dei mittenti bloccati per un periodo di tempo configurabile. La gestione dei messaggi bloccati dipende dalla configurazione dell'agente Filtro mittente. Le seguenti azioni rappresentano le opzioni di gestione per i messaggi bloccati:

  - Rifiuta

  - Elimina e archivia

  - Accetta e segna come mittente bloccato

Se un mittente viene incluso nell'elenco degli indirizzi IP bloccati o nel servizio reputazione IP di Microsoft, Reputazione mittente invia una richiesta immediata all'agente Filtro mittente per bloccarlo. Per sfruttare al meglio questa funzionalità, è necessario abilitare e configurare il servizio di aggiornamento della protezione da posta indesiderata di Microsoft Exchange.

Per impostazione predefinita, Reputazione mittente imposta un valore di classificazione 0 per i mittenti che non sono stati analizzati. Appena il mittente ha inviato 20 o più messaggi, la reputazione mittente calcola un livello di reputazione mittente in base alle statistiche elencate in precedenza in questo argomento.

Torna su

## Utilizzo del livello di reputazione mittente

La reputazione mittente agisce sui messaggi durante due fasi della sessione SMTP:

  - **Al comando MAIL FROM: di SMTP**   La reputazione mittente agisce su un messaggio solo se il messaggio è stato bloccato o altrimenti elaborato dall'agente Filtro connessioni, Filtro mittente, Filtro destinatario o ID mittente. In questo caso, la reputazione mittente recupera la valutazione del livello attuale di reputazione mittente dal profilo mantenuto per quel mittente nel database di Exchange. Una volta recuperata e valutata la classificazione, la configurazione del server Exchange determina il comportamento da tenere a seguito di una determinata connessione in base alla soglia di blocco.

  - **Dopo il comando "fine dei dati" di SMTP**   Il comando SMTP che segnala la fine del trasferimento dati (**EOD**) viene eseguito quando tutti i dati del messaggio sono stati inviati. A questo punto della sessione SMTP, molti agenti di protezione dalla posta indesiderata hanno già elaborato il messaggio. A seguito dell'elaborazione della posta indesiderata, le statistiche su cui si basa la reputazione mittente vengono aggiornate. Pertanto, la reputazione mittente dispone dei dati per calcolare o ricalcolare la classificazione del livello di reputazione per il mittente.

Per ulteriori informazioni, vedere [Gestione di reputazione mittente](manage-sender-reputation-exchange-2013-help.md).

Torna su

## Abilitazione e configurazione del rilevamento di server proxy aperti

La reputazione mittente valuta diverse caratteristiche del mittente per calcolare il livello di reputazione mittente. Una delle caratteristiche valutate dalla reputazione mittente è il risultato di un test relativo ai server proxy aperti. Spesso gli spammer inviano messaggi attraverso i server proxy aperti su Internet. Inviando messaggi di posta indesiderata attraverso i server proxy aperti, gli spammer possono inviare messaggi che sembrano essere originati da un server diverso dal proprio.

Quando la reputazione mittente calcola un livello di reputazione mittente, tenta di connettersi all'indirizzo IP di origine del mittente utilizzando molti protocolli proxy comuni, ad esempio SOCKS4, SOCKS5, HTTP, Telnet, Cisco e Wingate. La reputazione mittente formatta una richiesta specifica del protocollo nel tentativo di connettersi di nuovo al server Trasporto Edge dal server proxy aperto utilizzando una richiesta SMTP. Se una richiesta SMTP viene ricevuta dal server proxy, la reputazione mittente si accerta che il server proxy sia un server proxy aperto e regola il valore del livello di reputazione mittente in base a questo risultato. Per impostazione predefinita, il rilevamento di server proxy aperti è abilitato nella reputazione mittente.

Per ulteriori informazioni sull'abilitazione e sulla configurazione del rilevamento di server proxy aperti, vedere [Gestione di reputazione mittente](manage-sender-reputation-exchange-2013-help.md).

Torna su

## Impostazione della soglia di blocco del livello reputazione mittente

Il livello reputazione mittente è un numero compreso tra 0 e 9 che indica la probabilità che uno specifico mittente sia uno spammer o un utente malintenzionato. È necessario impostare una soglia di blocco del mittente in base al livello di reputazione mittente. La soglia di blocco del livello di reputazione mittente definisce il valore SRL raggiunto il quale un mittente viene bloccato. Per impostazione predefinita, il livello di reputazione mittente è impostato su 7. È consigliabile controllare l'efficacia dell'agente al livello predefinito. In seguito, è possibile eseguire un'eventuale correzione del valore per soddisfare le esigenze dell'organizzazione. Se si impostano altri agenti di protezione dalla posta indesiderata su valori elevati, è possibile impostare una soglia di SRL per la reputazione mittente più elevata rispetto a quella che verrebbe impostata nel caso in cui gli altri agenti di protezione dalla posta indesiderata fossero impostati su valori più bassi. Per ulteriori informazioni su come regolare le configurazioni di protezione dalla posta indesiderata in modo che tutte contribuiscano alla riduzione della posta indesiderata, vedere [Protezione anti-spam](anti-spam-protection-exchange-2013-help.md).

Se in un server Trasporto Edge la soglia di blocco del livello di reputazione mittente viene superata per un determinato mittente, la reputazione mittente lo aggiunge all'elenco indirizzi IP bloccati presente nell'agente filtro connessioni. Talvolta, gli spammer inviano gruppi di messaggi di posta indesiderata da un solo mittente. In questo scenario, se la reputazione mittente calcola un livello di reputazione mittente superiore alla soglia di blocco, il mittente viene aggiunto all'elenco di contatti bloccati per una durata configurabile. La durata predefinita è 24 ore. Trascorse le 24 ore, il mittente viene rimosso dall'elenco di contatti bloccati e può di nuovo inviare messaggi.

Quando un mittente viene aggiunto all'elenco indirizzi IP bloccati, la reputazione mittente ne elimina il profilo. La reputazione mittente elimina il profilo perché il rispettivo mittente bloccato indica che il valore del livello di reputazione mittente ha superato la soglia di blocco. In tal caso, è possibile che il mittente bloccato sia aggiunto nuovamente all'elenco indirizzi IP bloccati subito dopo il termine del periodo di blocco del mittente.

Per ulteriori informazioni, vedere [Gestione di reputazione mittente](manage-sender-reputation-exchange-2013-help.md).

Inizio pagina


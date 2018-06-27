---
title: 'Directory di prelievo e directory di riesecuzione: Exchange 2013 Help'
TOCTitle: Directory di prelievo e directory di riesecuzione
ms:assetid: ae191700-953f-411c-906f-dc90feec3d5a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124230(v=EXCHG.150)
ms:contentKeyID: 50481443
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Directory di prelievo e directory di riesecuzione

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Per impostazione predefinita, le directory di prelievo e di riesecuzione sono presenti in tutti i server Cassette postali o Trasporto Edge di Microsoft Exchange Server 2013. I file dei messaggi di posta elettronica formattati correttamente e copiati nella directory di prelievo o riesecuzione vengono inviati per il recapito. La directory di prelievo viene utilizzata dagli amministratori per la verifica del flusso di posta o dalle applicazioni che devono creare e inviare i propri messaggi. La directory di riesecuzione riceve i messaggi da server gateway esterni e può anche essere utilizzata per inviare nuovamente i messaggi esportati dagli amministratori dalle code dei server Exchange.

**Sommario**

Anatomy of an email message file

How the Pickup and Replay directories process messages

Pickup directory message file requirements

Pickup directory message header modifications

Replay directory message file requirements

Replay directory message header modifications

Failures in Pickup and Replay directory message processing

Security considerations for the Pickup and Replay directories

Permissions for the Pickup and Replay directories

## Struttura di un file dei messaggi di posta elettronica

Un messaggio di posta elettronica SMTP standard è costituito da una *busta del messaggio* e dal contenuto del messaggio. La busta del messaggio contiene le informazioni necessarie per la trasmissione e il recapito del messaggio. Il contenuto del messaggio include i campi di intestazione del messaggio (denominati collettivamente *intestazione del messaggio*) e il corpo del messaggio. La busta del messaggio è descritta in RFC 2821, mentre l'intestazione del messaggio è descritta in RFC 2822.

Quando il mittente crea un messaggio di posta elettronica e lo invia per il recapito, il messaggio contiene le informazioni di base necessarie per la conformità agli standard SMTP, quali mittente, destinatario, data e ora di creazione del messaggio, campo oggetto facoltativo e corpo del messaggio facoltativo. Queste informazioni sono contenute nel messaggio stesso e, per definizione, sono contenute nell'intestazione del messaggio.

Il server Messaggistica del mittente genera una busta per il messaggio utilizzando le informazioni su mittente e destinatario presenti nell'intestazione del messaggio, per poi trasmetterlo ad Internet per il recapito al server Messaggistica del destinatario. I destinatari non vedono mai la busta del messaggio, perché viene generata dal processo di trasmissione del messaggio e non è parte integrante di questo.

Ogni server coinvolto nella trasmissione del messaggio può inserire campi d'intestazione del messaggio relativi al ruolo del server nel recapito del messaggio, oppure altri campi d'intestazione del messaggio specifici per la sua applicazione. Quando il destinatario apre il messaggio utilizzando un client di posta elettronica, il client visualizza alcune delle informazioni più importanti dall'intestazione del messaggio, quali mittente, destinatari e oggetto insieme al corpo del messaggio.

Inizio pagina

## Modalità di elaborazione dei messaggi delle directory di prelievo e riesecuzione

In Exchange 2013 il percorso predefinito della directory di prelievo è `%ExchangeInstallPath%TransportRoles\Pickup`. Il percorso predefinito della directory di riesecuzione è `%ExchangeInstallPath%TransportRoles\Replay`. Un file dei messaggi con estensione EML, formattato correttamente e copiato nella directory di prelievo o riesecuzione, viene elaborato per l'invio come descritto di seguito:

1.  Ogni cinque secondi viene verificata l'eventuale presenza di nuovi file dei messaggi nelle directory di prelievo e riesecuzione. Non è possibile modificare questo intervallo di polling. È possibile impostare la velocità di elaborazione dei file dei messaggi utilizzando il parametro *PickupDirectoryMaxMessagesPerMinute* sul cmdlet **Set-TransportService**. Questo parametro influisce sulle directory di prelievo e di riesecuzione. Il valore predefinito è 100 messaggi al minuto. I file che non possono essere aperti rimangono nella directory di prelievo e vengono verificati al polling successivo.

2.  I limiti applicati ai file dei messaggi nella directory di prelievo, come la dimensione massima dell'intestazione e il numero massimo di destinatari, vengono controllati. Per impostazione predefinita, la dimensione massima dell'intestazione è 64 KB e il numero massimo di destinatari è pari a 100. Questi limiti possono essere modificati utilizzando il cmdlet **Set-TransportService**. Le impostazioni influiscono direttamente solo sulla directory di prelievo.

3.  Il file viene rinominato da *\<nomefile\>*.eml a *\<nomefile\>*.tmp. Se il file *\<nomefile\>*.tmp esiste già, il file viene rinominato *\<nomefile\>\<dataora\>*.tmp. Se la ridenominazione del file non riesce, viene generato un errore nel registro eventi e il processo di prelievo viene eseguito sul file successivo.

4.  Una volta convertito correttamente il file TMP in un messaggio di posta elettronica, viene inviato un comando di **delete on close** al file TMP. Il file con estensione .tmp rimane visualizzato nella directory di prelievo, ma non può essere aperto.

5.  Dopo che il messaggio è accodato in attesa di essere recapitato, viene inviato un comando **close** e il file con estensione .tmp viene eliminato dalla directory di prelievo. Se l'eliminazione non riesce, viene generato un errore nel registro eventi. Se il servizio di trasporto di Microsoft Exchange viene riavviato quando i file con estensione TMP si trovano nella directory di prelievo, tutti i file con estensione TMP vengono rinominati come file con estensione EML e vengono rielaborati. Ciò potrebbe causare una trasmissione di messaggi duplicata.

Inizio pagina

## Requisiti relativi ai file dei messaggi della directory di prelievo

Un file dei messaggi copiato nella directory di prelievo deve soddisfare i seguenti requisiti per il recapito corretto:

  - Il file dei messaggi deve essere un file di testo conforme al formato di base dei messaggi SMTP. Il contenuto e i campi di intestazione del messaggio MIME sono supportati.

  - Il file dei messaggi deve avere estensione del nome del file eml.

  - Almeno un indirizzo di posta elettronica deve essere presente nei campi di intestazione del messaggio `Sender` o `From` contenuti nell'intestazione. Se è presente un solo indirizzo di posta elettronica in entrambi i campi `Sender` e `From`, l'indirizzo di posta elettronica nel campo `From` viene utilizzato come mittente del messaggio nella relativa busta.

  - Il campo `Sender` può contenere un solo indirizzo di posta elettronica. Non sono consentiti più indirizzi di posta elettronica. Il campo `Sender` è facoltativo se è presente un solo indirizzo di posta elettronica nel campo `From`.

  - Il campo `From` consente di immettere più indirizzi di posta elettronica ma allo stesso tempo deve esistere un unico indirizzo di posta elettronica nel campo `Sender`. L'indirizzo nel campo `Sender` viene quindi utilizzato come mittente del messaggio nella relativa busta.

  - Almeno un indirizzo di posta elettronica deve essere presente nel campo `To`, `Cc` o `Bcc`.

  - Tra l'intestazione e il corpo del messaggio deve essere presente una riga vuota.

Con questo esempio viene mostrato un messaggio di testo normale che utilizza una formattazione accettabile per la directory di prelievo.

    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    
    This is the body of the message.

Il contenuto MIME è supportato anche nei file dei messaggi della directory di prelievo. MIME definisce un'ampia gamma di contenuti di messaggi comprendenti lingue che non possono essere rappresentate in testo ASCII a 7 bit, HTML e altro contenuto multimediale. Una descrizione completa e i requisiti di MIME esulano dall'ambito di questo argomento. Con questo esempio viene mostrato un messaggio MIME semplice che utilizza una formattazione accettabile per la directory di prelievo.

    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>

Inizio pagina

## Modifiche all'intestazione del messaggio nella directory di prelievo

La directory di prelievo rimuove uno dei seguenti campi di intestazione del messaggio dall'intestazione:

  - `Received`

  - `Resent-*`

  - `Bcc`
    

    > [!NOTE]
    > Tutti gli indirizzi di posta elettronica che si trovano nei campi di intestazione del messaggio <CODE>Bcc</CODE> facoltativi sono elaborati correttamente. Una volta elaborati i destinatari <CODE>Bcc</CODE> come destinatari invisibili nella busta del messaggio, questi vengono rimossi dall'intestazione del messaggio per proteggerne l'identità. Se un messaggio contiene solamente destinatari <CODE>Bcc</CODE>, il valore <STRONG>Undisclosed Recipients</STRONG> è aggiunto al campo <CODE>To</CODE> nell'intestazione del messaggio.



La directory di prelievo aggiunge il proprio campo di intestazione `Received` al messaggio come parte del processo di inoltro del messaggio. Il campo di intestazione `Received` viene applicato nel seguente formato.

    Received: from localhost by Pickup with Microsoft SMTP Server id <ExchangeServerVersion><datetime>

La directory di prelievo modifica i seguenti campi di intestazione del messaggio se mancanti o non corretti:

  - **Message-Id**   Se il campo `Message-Id` non è presente oppure è vuoto, la directory di prelievo aggiunge un campo Message-Id utilizzando il formato *\<GUID\>*@*\<dominiopredefinito\>*.

  - **Data**   Se il campo `Date` non è presente oppure non è corretto, la directory di prelievo aggiunge la data e l'ora di elaborazione del messaggio da parte della directory.

Inizio pagina

## Requisiti relativi ai file dei messaggi della directory di riesecuzione

La directory di riesecuzione viene utilizzata per inoltrare nuovamente i messaggi esportati di Exchange e per ricevere i messaggi da server gateway esterni. Questi messaggi sono già formattati per la directory di riesecuzione. Non è necessario che l'amministratore o un'altra applicazione compongano e inoltrino nuovi file dei messaggi utilizzando la directory di riesecuzione. È necessario utilizzare la directory di prelievo per creare e inoltrare nuovi file dei messaggi.

I messaggi della directory di riesecuzione fanno largo uso dei campi *X-Header*. I campi X-Header sono campi di intestazione del messaggio definiti dall'utente, non standard, esistenti nell'intestazione del messaggio. I campi X-Header non sono citati specificatamente nella specifica RFC 2822, ma l'utilizzo di un campo di intestazione del messaggio non definito che inizia con "X-" è diventato un modo comunemente accettato per aggiungere campi di intestazione non standard a un messaggio. I campi X-Header specifici di Exchange utilizzati nei file dei messaggi nella directory di riesecuzione possono in effetti impostare le informazioni di recapito normalmente incluse nella busta del messaggio. Questa funzionalità è necessaria per mantenere le informazioni del messaggio originale quando si utilizza la directory di riesecuzione per elaborare i messaggi esportati da un altro server Exchange.

Un file dei messaggi copiato nella directory di riesecuzione deve soddisfare i seguenti requisiti per il recapito corretto:

  - Il file dei messaggi deve essere un file di testo conforme al formato di base dei messaggi SMTP. Il contenuto e i campi di intestazione del messaggio MIME sono supportati.

  - Il file dei messaggi deve avere estensione del nome del file eml.

  - I campi X-Header devono precedere tutti i campi d'intestazione normali.

  - Tra i campi di intestazione e il corpo del messaggio deve essere presente una riga vuota.

I campi X-Header descritti nell'elenco seguente sono necessari per i messaggi nella directory di riesecuzione:

  - **X-Sender**   Questo campo X-Header sostituisce il campo di intestazione `From` in un messaggio SMTP standard. Deve essere presente un campo `X-Sender` contenente un indirizzo di posta elettronica. La directory di riesecuzione ignora il campo di intestazione `From`, se presente, anche se il client di posta elettronica del destinatario visualizza il valore del campo di intestazione `From` come mittente del messaggio. Di norma sono presenti altri parametri nel campo `X-Sender` come illustrato nell'esempio seguente.
    
        X-Sender: <bob@fabrikam.com> BODY=7bit RET=HDRS ENVID=12345ABCD auth=<someAuth>
    

    > [!NOTE]
    > Questi parametri sono i valori della busta del messaggio generati normalmente dal server di invio. È possibile visualizzare parametri simili nei file dei messaggi esportati.<BR><CODE>RET</CODE> specifica se è necessario restituire al mittente l'intero messaggio oppure solo le intestazioni, nel caso in cui non sia possibile inviare il messaggio. <CODE>RET</CODE> può assumere il valore <CODE>HDRS</CODE> o <CODE>FULL</CODE>. <CODE>ENVID</CODE> è l'identificatore della busta del messaggio. <CODE>BODY</CODE> specifica la codifica del testo del messaggio. <CODE>auth</CODE> specifica il meccanismo di autenticazione per il server Messaggistica secondo quanto descritto in RFC 2554.



  - **X-Receiver**   Questo campo X-Header sostituisce il requisito del campo di intestazione `To` in un messaggio SMTP standard. Deve essere presente almeno un campo `X-Receiver` contenente un indirizzo di posta elettronica. Sono consentiti più campi `X-Receiver` per più destinatari. La directory di riesecuzione ignora i campi di intestazione `To`, se presenti, anche se il client di posta elettronica del destinatario visualizza i valori dei campi di intestazione `To` come destinatari del messaggio. Di norma sono presenti altri parametri facoltativi nei campi `X-Receiver` come illustrato nell'esempio seguente.
    
        X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    

    > [!NOTE]
    > Questi parametri sono i valori della busta del messaggio generati normalmente dal server di invio. È possibile visualizzare parametri simili nei file dei messaggi esportati. Questi parametri sono correlati ai messaggi di notifica dello stato del recapito (DSN, Delivery Status Notification) secondo quanto descritto in RFC 1891.<BR><CODE>NOTIFY</CODE> può assumere il valore <CODE>NEVER</CODE>, <CODE>DELAY</CODE> o <CODE>FAILURE</CODE>. <CODE>ORcpt</CODE> viene utilizzato per mantenere il destinatario originale del messaggio.



I campi X-Header descritti nell'elenco seguente sono facoltativi per i file di messaggio nella directory di riesecuzione:

  - **X-CreatedBy**   Utilizzato per la funzionalità firewall dell'intestazione. Se questo campo X-Header è presente, non deve essere vuoto. Se il campo `X-CreatedBy` non esiste, viene aggiunto con il valore **Unspecified**. In genere, il valore di questo campo è **MSExchange15** ma può contenere anche il tipo di spazio indirizzi non SMTP impostato su un connettore di invio, ad esempio **Notes**.

  - **X-EndOfInjectedXHeaders**   Dimensione in byte di tutti i campi X-Header presenti. Questo campo X-Header può essere utilizzato come indicatore dell'ultimo campo X-Header prima dell'inizio dei campi di intestazione standard.

  - **X-ExtendedMessageProps**   Proprietà di messaggio estese per il messaggio.

  - **X-HeloDomain**   La stringa del dominio HELO/EHLO presentata durante la conversazione del protocollo SMTP iniziale.

  - **X-Source**   Utilizzato da Visualizzatore code nella colonna **MessageSourceName**. Se il valore di questo campo X-Header non è specificato, viene utilizzato il valore **Replay**. Altri valori possibili per il campo X-Header sono **Smtp Receive Connector** e **Smtp Send Connector**.

  - **X-SourceIPAddress**   Indirizzo IP del server di invio. Il valore del campo è `0.0.0.0` se non è specificato alcun indirizzo IP.

Con questo esempio viene mostrato un messaggio di testo normale che utilizza una formattazione accettabile per la directory di riesecuzione.

    X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345AB auth=<someAuth>
    Subject: Optional message subject
    
    This is the body of the message.

Il contenuto MIME è supportato anche nei file dei messaggi della directory di riesecuzione. MIME definisce un'ampia gamma di contenuti di messaggi comprendenti lingue che non possono essere rappresentate in testo ASCII a 7 bit, HTML e altro contenuto multimediale. Una descrizione completa e i requisiti di MIME esulano dall'ambito di questo argomento. Con questo esempio viene mostrato un messaggio MIME semplice che utilizza una formattazione accettabile per la directory di riesecuzione.

    X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345ABCD auth=<someAuth>
    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Optional message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>

Inizio pagina

## Modifiche all'intestazione del messaggio nella directory di riesecuzione

La directory di riesecuzione elimina il campo di intestazione `Bcc` dal file di messaggio.

La directory di riesecuzione aggiunge il proprio campo di intestazione `Received` al messaggio come parte del processo di invio del messaggio. Il campo di intestazione del messaggio Ricevuto viene applicato nel seguente formato.

    Received: from <ReceivingServerName> by Replay with <ExchangeServerVersion><DateTime>

La directory di riesecuzione modifica i campi di intestazione seguenti nell'intestazione di messaggio:

  - **Message-ID**   Se il campo di intestazione non è presente oppure è vuoto, la directory di riesecuzione aggiunge un campo di intestazione Message-ID utilizzando il formato *\<GUID\>*@*\<dominiopredefinito\>*.

  - **Data**   Se questo campo di intestazione del messaggio non è presente oppure non è valido, la directory di riesecuzione aggiunge il campo di intestazione Data utilizzando la data e l'ora di elaborazione del messaggio da parte della directory di riesecuzione.

Inizio pagina

## Errori nell'elaborazione del messaggio delle directory di prelievo e riesecuzione

Un file dei messaggi copiato nella directory di prelievo o riesecuzione potrebbe non essere accodato correttamente per il recapito. Possono verificarsi le seguenti categorie di errori nell'inoltro dei messaggi:

  - **Recapiti non riusciti**   Viene generato un rapporto di mancato recapito per un file dei messaggi formattato correttamente e con un mittente valido che non può essere inviato correttamente per il recapito. Anche le violazioni delle restrizioni per i messaggi della directory di prelievo o con contenuto con formato non valido potrebbero causare un rapporto di mancato recapito. Quando viene emesso un rapporto di mancato recapito durante l'elaborazione del messaggio, il messaggio originale viene allegato al rapporto di mancato recapito e il file dei messaggi viene eliminato dalla directory di prelievo o dalla directory di riesecuzione.
    

    > [!NOTE]
    > Un messaggio formattato correttamente inviato alla pipeline di trasporto può incorrere in errori di recapito in un secondo momento ed essere restituito al mittente con un rapporto di mancato recapito. Questo genere di errori può essere causato da problemi di trasmissione che non sono collegati alla directory di prelievo o di riesecuzione, ad esempio problemi del server di messaggistica o errori di instradamento lungo il percorso di recapito del messaggio.



  - **Posta scartata**   Un messaggio classificato come *posta scartata* presenta seri problemi che impediscono alle directory di prelievo e di riesecuzione di inviarlo per il recapito. In alternativa il messaggio può essere classificato come posta scartata quando il messaggio è formattato correttamente, ma i destinatari non sono validi e non è possibile inviare un rapporto di mancato recapito perché il mittente non è valido.
    
    I file dei messaggi considerati come posta scartata rimangono nella directory di prelievo o di riesecuzione e vengono rinominati da *\<nomefile\>*.eml a *\<nomefile\>*.bad. Se il file *\<nomefile\>*.bad esiste già, il file viene rinominato *\<nomefile\>\<dataora\>*.bad. Se sono presenti messaggi di posta scartata nella directory di prelievo o di riesecuzione, viene generato un errore nel registro eventi, ma gli stessi messaggi scartati non generano errori ripetuti nel registro eventi.
    

    > [!NOTE]
    > Si consiglia sempre di comporre e salvare i file di messaggio su un percorso diverso prima di copiarli nella directory di prelievo per il recapito. La directory di prelievo esegue il polling alla ricerca di nuovi messaggi ogni cinque secondi. Pertanto, se si tenta di comporre e di salvare il messaggio direttamente sulla directory di prelievo, la directory di prelievo potrebbe cercare di elaborare i file di messaggio prima della fine della composizione.



Inizio pagina

## Considerazioni sulla protezione per le directory di prelievo e riesecuzione

Nell'elenco riportato di seguito sono illustrati problemi relativi alla protezione comuni alla directory di prelievo e alla directory di riesecuzione:

  - Qualsiasi verifica della protezione configurata su un connettore di ricezione, quali rilevamento della posta indesiderata, antimalware, azioni di filtro mittente o di filtro destinatario, non viene eseguita sui messaggi inviati tramite la directory di prelievo o di riesecuzione.

  - Una directory di prelievo o una directory di riesecuzione danneggiata può fungere da inoltro aperto. Questo consente il rinvio o l'*inoltro* del messaggio utilizzando un server diverso per mascherare la vera origine dei messaggi.

Nell'elenco riportato di seguito sono illustrati altri problemi relativi alla protezione validi per la directory di riesecuzione:

  - I campi X-Header utilizzati dalla directory di riesecuzione consentono la creazione manuale della busta del messaggio. Le informazioni nei campi `X-Sender` e `X-Receiver` possono essere completamente diverse da quelle presenti nei campi di intestazione dei messaggi `To` o `From` visualizzati dai client di posta elettronica. Tale rappresentazione di un mittente e di un dominio frequentemente è denominata *spoofing*. La *posta falsificata* è un messaggio di posta elettronica in cui l'indirizzo del mittente è stato modificato in modo tale che sembra essere stato inviato da un mittente diverso dal mittente effettivo del messaggio.

  - Se il campo `X-CreatedBy` ha il valore di **MSExchange15**, la destinazione è considerata attendibile e firewall intestazioni non viene applicata. *Intestazione firewall* è un modo per Exchange devono essere mantenuti X-Header nei messaggi trasmessi tra i server Exchange attendibili o per rimuovere potenzialmente lasciando X-Header dai messaggi trasmessi a destinazioni non attendibile all'esterno dell'organizzazione di Exchange. Questi X-Header può essere utilizzato per condividere le informazioni di Exchange, ad esempio livello di probabilità posta indesiderata (SCL) messaggio firma, oppure crittografia tra server di Exchange autorizzati. Lasciando queste informazioni per le origini non autorizzate può comportare potenziali rischi di protezione. Per ulteriori informazioni sui firewall intestazione, vedere [Understanding intestazione Firewall](https://go.microsoft.com/fwlink/?linkid=268394).

È necessario rafforzare la protezione della directory di riesecuzione a causa di ulteriori minacce per la protezione associate alla directory di riesecuzione. L'accesso alla directory di prelievo può essere concesso a utenti o applicazioni che devono generare e inoltrare nuovi messaggi, mentre non dovrebbe essere necessario l'accesso alla directory di riesecuzione.

Sia la directory di prelievo che la directory di riesecuzione sono abilitate per impostazione predefinita su tutti i server Cassette postali e Trasporto Edge. È possibile disabilitare una directory di prelievo o una directory di riesecuzione che non è richiesta in uno specifico server Trasporto Cassette postali o Trasporto Edge dell'organizzazione impostando il percorso della directory sul valore `$null`. Per ulteriori informazioni, vedere [Configurare la directory di prelievo e la directory di riesecuzione](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md).

Inizio pagina

## Autorizzazioni per le directory di prelievo e riesecuzione

Per accedere alle directory di prelievo e riesecuzione sono necessarie le seguenti autorizzazioni:

  - Amministratore: Controllo completo

  - Sistema: Controllo completo

  - Servizio di rete: Lettura, Scrittura ed Eliminazione sottocartelle e file

Per impostazione predefinita, il servizio di trasporto di Microsoft Exchange utilizza le credenziali di sicurezza dell'account utente del servizio di rete per gestire il percorso e le autorizzazioni delle directory di prelievo e riesecuzione. L'account servizio di rete richiede tali autorizzazioni sulla directory di prelievo in modo che i file con estensione eml possano essere aperti, ridenominati con estensione tmp ed eliminati o ridenominati con estensione bad se il messaggio è classificato come posta scartata.

È possibile modificare il percorso di queste directory utilizzando i parametri *PickupDirectoryPath* e *ReplayDirectoryPath* sul cmdlet **Set-TransportService**. La modifica corretta del percorso della directory di prelievo dipende dai diritti concessi all'account servizio di rete nei nuovi percorsi delle directory e dall'eventualità che le nuove directory siano già presenti. Se la directory non esiste e se l'account del servizio di rete dispone dei diritti necessari per creare cartelle e applicare le autorizzazioni al nuovo percorso, la directory viene creata e le autorizzazioni corrette sono applicate alla nuova directory. Se la nuova directory esiste già, le autorizzazioni della cartella esistente non vengono controllate. Ogni volta che si spostano le directory utilizzando il parametro *PickupDirectoryPath* o *ReplayDirectoryPath* con il cmdlet **Set-TransportService**, si consiglia di verificare l'esistenza della nuova directory e le relative autorizzazioni.

Inizio pagina


---
title: 'POP3 e IMAP4 in Exchange Server 2013: Exchange 2013 Help'
TOCTitle: POP3 e IMAP4
ms:assetid: a7dc91ee-2919-4db3-ae9c-cd665d2e09ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657728(v=EXCHG.150)
ms:contentKeyID: 50481386
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP3 e IMAP4 in Exchange Server 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-08-16_

Informazioni sulle differenze tra i protocolli POP3 e IMAP4 in Exchange Server 2013 e sulla modalità di configurazione delle opzioni di accesso alle cassette postali di Exchange 2013 da diversi programmi di posta elettronica.

Per impostazione predefinita, POP3 e IMAP4 sono disabilitati in Exchange Server 2013. Per supportare i client POP3 che fanno ancora affidamento su questi protocolli, è necessario avviare due servizi POP3: il servizio POP3 di Microsoft Exchange e il servizio Back-end POP3 di Microsoft Exchange. Per supportare i client IMAP4 che fanno ancora affidamento su questi protocolli, è necessario avviare due servizi IMAP4: il servizio IMAP4 di Microsoft Exchange e il servizio Back-end IMAP4 di Microsoft Exchange.

Per la procedura dettagliata relativa all'abilitazione dei servizi POP3 e IMAP4, vedere [Abilitazione di POP3 in Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md) e [Abilitazione di IMAP4 in Exchange 2013](enable-imap4-in-exchange-2013-exchange-2013-help.md).

Per impostazione predefinita, gli utenti con cassette postali su computer che eseguono Exchange 2013 possono accedere alle cassette postali utilizzando Outlook o Outlook Web App, Exchange ActiveSync o Outlook Voice Access. Outlook, Outlook Web App e Outlook Voice Access consentono agli utenti di posta elettronica di utilizzare il set completo di funzionalità disponibili per gli utenti che dispongono di cassette postali sui server Exchange 2016.

**Sommario**

Informazioni generali sulla funzionalità POP3 e IMAP4

Connettività tra siti POP3 e IMAP4

Utilizzo di account non standard con POP3 e IMAP4

Informazioni sulle differenze tra POP3 e IMAP4

Opzioni di invio e ricezione per le applicazioni di posta elettronica POP3 e IMAP4

Applicazioni POP3 e IMAP4

Impostazioni utente per la configurazione dell'accesso tramite POP3 o IMAP4 alle cassette postali di Exchange 2013

## Informazioni generali sulla funzionalità POP3 e IMAP4

In questa sezione viene illustrata la funzionalità di POP3 e IMAP4 per Exchange 2013.

I protocolli POP3 e IMAP4 presentano i vantaggi e le limitazioni seguenti:

  - **POP3**   POP3 è stato progettato per supportare l'elaborazione della posta non in linea. Con POP3, i messaggi di posta elettronica vengono rimossi dal server e archiviati nel client POP3 locale, a meno che il client non è impostato per lasciare la posta nel server. In questo modo la gestione dei dati e le responsabilità di protezione sono affidate all'utente. POP3 non offre funzionalità avanzate di collaborazione, quali calendario, contatti e attività.

  - **IMAP4**   IMAP4 offre accesso online e offline ma, come POP3, non offre funzionalità avanzate di collaborazione, quali calendario, contatti e attività.

Le applicazioni di posta elettronica POP3 e IMAP4 non utilizzano POP3 e IMAP4 per inviare messaggi al server di posta elettronica, ma si basano sul protocollo SMTP per l'invio dei messaggi. Il connettore per la ricezione degli invii di posta elettronica da applicazioni client che utilizzano POP3 o IMAP4 viene creato automaticamente all'installazione di Exchange. Per ulteriori informazioni sui connettori, vedere [Connettori di ricezione](receive-connectors-exchange-2013-help.md).


> [!NOTE]
> Ogni volta che utente utilizza un programma di posta elettronica basato su POP o IMAP per aprire la propria posta elettronica di Office 365, riscontrerà un ritardo di alcuni secondi. Il ritardo è dovuto all'utilizzo di un server proxy, che introduce un hop aggiuntivo per l'autenticazione. Il server proxy prima cerca il server pod assegnato (server Accesso client), quindi si autentica a tale server.



## Connettività tra siti POP3 e IMAP4

Nelle versioni precedenti di Exchange, era necessario eseguire un'operazione di configurazione manuale per consentire ai client POP3 e IMAP4 di connettersi alla loro posta da un sito nell'organizzazione quando la loro cassetta postale era contenuta in un diverso sito dell'organizzazione. Per impostazione predefinita, Exchange 2013 effettua automaticamente l'inoltro da un server Accesso client in un sito al server corretto.

## Utilizzo di account non standard con POP3 e IMAP4

Non è possibile utilizzare un account anonimo o Guest per accedere a una cassetta postale di Exchange 2016 tramite POP3 o IMAP4. Gli account anonimi sono bloccati a causa delle vulnerabilità della sicurezza presenti quando si utilizzano account non standard per l'accesso tramite POP3 e IMAP4. Inoltre, non è possibile connettersi alla cassetta postale Administrator tramite POP3 o IMAP4. Questa limitazione è stata inclusa intenzionalmente in Exchange 2013 per migliorare la protezione della cassetta postale Administrator. Per accedere a tale cassetta postale, è necessario utilizzare Outlook o Outlook Web App.

## Informazioni sulle differenze tra POP3 e IMAP4

**POP3** POP3 è un protocollo Internet utilizzato frequentemente per la posta elettronica. Per impostazione predefinita, i messaggi di posta elettronica scaricati in un computer client mediante le applicazioni di posta elettronica POP3 vengono rimossi dal server. Quando una copia della posta elettronica dell'utente non viene mantenuta nel server di posta elettronica, l'utente non può accedere agli stessi messaggi di posta elettronica da più computer. Tuttavia, alcune applicazioni di posta elettronica POP3 possono essere configurate per mantenere copie dei messaggi di posta elettronica sul server per consentire l'accesso agli stessi messaggi da un altro computer. Le applicazioni client POP3 possono essere utilizzate solo per scaricare i messaggi dal server di posta elettronica in una singola cartella (generalmente nella Posta in arrivo) nel computer client. Il protocollo POP3 non è in grado di sincronizzare più cartelle nel server di posta elettronica con quelle nel computer client.

**IMAP4** Le applicazioni client di posta elettronica che utilizzano IMAP4 sono più flessibili e generalmente offrono più funzionalità rispetto alle applicazioni di posta elettronica client che utilizzano POP3. Per impostazione predefinita, quando i messaggi vengono scaricati nel computer client tramite applicazioni di posta elettronica IMAP4, una copia dei messaggi scaricati rimane nel server di posta elettronica. Di conseguenza, se nel server di posta elettronica viene conservata una copia del messaggio dell'utente, quest'ultimo può accedere allo stesso messaggio da più computer. La posta elettronica IMAP4 consente all'utente di accedere a più cartelle di posta e di crearle nel server di posta elettronica. Gli utenti possono quindi accedere ai propri messaggi presenti sul server da computer che si trovano in più posizioni. Ad esempio, quasi tutte le applicazioni di posta elettronica IMAP4 possono essere configurate per mantenere una copia degli elementi inviati di un utente nel server così da poterli visualizzare da un computer diverso. IMAP4 supporta funzionalità aggiuntive supportate da quasi tutte le applicazioni di posta elettronica IMAP4. Ad esempio, alcune applicazioni IMAP4 includono una funzionalità che consente all'utente di visualizzare solo le intestazioni dei propri messaggi di posta elettronica nel server (mittente e oggetto del messaggio) e di scaricare solo i messaggi che desidera leggere. IMAP4, inoltre, non supporta l'accesso alle cartelle pubbliche.


> [!NOTE]
> I client IMAP4 e POP3 hanno limitato l'accesso alle informazioni di calendario per Exchange. Per ulteriori informazioni, vedere <A href="configure-calendar-options-for-pop3-exchange-2013-help.md">Configurare le opzioni di calendario per POP3</A> e <A href="configure-calendar-options-for-imap4-exchange-2013-help.md">Configurare le opzioni di calendario per IMAP4</A>.



## Opzioni di invio e ricezione per le applicazioni di posta elettronica POP3 e IMAP4

Le applicazioni di posta elettronica POP3 e IMAP4 consentono agli utenti di scegliere quando connettersi al server per inviare e ricevere i messaggi di posta elettronica. In questa sezione vengono descritte alcune delle opzioni più comuni per la connettività e vengono forniti alcuni fattori da prendere in considerazione al momento della selezione delle opzioni di connessione disponibili nelle applicazioni di posta elettronica POP3 o IMAP4.

## Impostazioni di configurazione comuni

Tre delle impostazioni di connessione più comuni che possono essere configurate nell'applicazione client POP3 o IMAP4 sono:

  - Inviare e ricevere messaggi ogni volta che viene avviata l'applicazione di posta elettronica. Se si utilizza questa opzione, la posta viene inviata e ricevuta nel momento in cui l'applicazione di posta elettronica viene avviata dall'utente.

  - Inviare e ricevere manualmente i messaggi. Se si utilizza questa opzione, i messaggi vengono inviati e ricevuti soltanto quando l'utente fa clic sull'opzione "Invia e ricevi" disponibile nell'interfaccia utente client.

  - Inviare e ricevere i messaggi a un determinato intervallo di minuti impostato. Se l'utente imposta questa opzione, l'applicazione client si connette al server a intervalli regolari, in base al numero di minuti impostato, per inviare messaggi e scaricare eventuali messaggi nuovi.

Per informazioni su come configurare le impostazioni per l'applicazione di posta elettronica utilizzata, vedere la documentazione della Guida fornita con la rispettiva applicazione.

## Considerazioni per l'impostazione delle opzioni di invio e ricezione

Se il dispositivo o il computer su cui è in esecuzione l'applicazione di posta elettronica POP3 o IMAP4 è sempre connesso a Internet, gli utenti possono decidere di configurare l'applicazione per l'invio e la ricezione di messaggi a intervalli specificati in minuti. Una connessione al server a intervalli brevi consente all'utente di tenere aggiornata l'applicazione di posta elettronica con le informazioni più recenti presenti sul server. Tuttavia, se il dispositivo o il computer su cui è in esecuzione l'applicazione di posta elettronica POP3 o IMAP4 non è sempre connesso a Internet, gli utenti possono decidere di configurare l'applicazione per l'invio e la ricezione di messaggi manualmente.


> [!NOTE]
> Se l'utente utilizza un'applicazione di posta elettronica compatibile con IMAP4 che supporta il comando IMAP4 IDLE, può inviare e ricevere i messaggi di posta dalla cassetta postale di Exchange quasi in tempo reale. Per il funzionamento di questo metodo di connessione, sia l'applicazione del server di posta elettronica che l'applicazione client devono supportare il comando IMAP4 IDLE. Nella maggior parte dei casi, gli utenti non devono configurare le impostazioni nell'applicazione di posta elettronica IMAP4 per utilizzare questo metodo di connessione.



## Applicazioni POP3 e IMAP4

Poiché Exchange 2013 supporta POP3 e IMAP4, gli utenti possono utilizzare qualsiasi applicazione che supporti applicazioni client POP3 e IMAP4 per la connessione a Exchange 2013. Queste applicazioni includono Outlook, Outlook Web App, Windows Live Mail, Outlook Express, Entourage e molte applicazioni di terze parti, quali Gmail, Mozilla Thunderbird ed Eudora. Le funzionalità supportate variano a seconda dell'applicazione client. Per informazioni sulle funzionalità specifiche offerte dalle applicazioni client compatibili con POP3 e IMAP4, vedere la documentazione fornita con ciascuna applicazione.

## Impostazioni utente per la configurazione dell'accesso tramite POP3 o IMAP4 alle cassette postali di Exchange 2013

Dopo aver abilitato l'accesso client POP3 e IMAP4, è necessario fornire agli utenti le informazioni necessarie per connettere i loro programmi di posta elettronica alla loro cassetta postale di Exchange 2016.

Per connettersi dall'esterno della rete aziendale, gli utente necessitano delle seguenti informazioni:

  - Nome server POP3 o IMAP4 interno

  - Numero di porta POP3 o IMAP4 interno

  - Metodo di crittografia POP3 o IMAP4 interno

  - Nome del server posta in uscita SMTP interno

  - Numero di porta del server posta in uscita SMTP interno

  - Metodo di crittografia del server posta in uscita SMTP interno

Per connettersi da Internet, gli utenti necessitano delle seguenti informazioni:

  - Nome server POP3 o IMAP4 esterno

  - Numero di porta POP3 o IMAP4 esterno

  - Metodo di crittografia POP3 o IMAP4 esterno

  - Nome del server posta in uscita SMTP esterno

  - Numero di porta del server posta in uscita SMTP esterno

  - Metodo di crittografia del server posta in uscita SMTP esterno

È possibile rendere queste impostazioni disponibili per gli utenti tramite un messaggio di posta elettronica o altri metodi di comunicazione manuale. È anche possibile configurare Exchange in modo che gli utenti possano utilizzare Outlook Web App per controllare le proprie impostazioni.

**Configurazione di Exchange in modo che gli utenti possano controllare le proprie impostazioni dei server POP3, IMAP4 e SMTP**

Per impostazione predefinita, gli utenti non possono controllare le impostazioni del server POP3, IMAP4 e SMTP tramite Outlook Web App. Per effettuare tale operazione, è necessario utilizzare i cmdlet **Set-PopSettings** e **Set-ImapSettings**. Per consentire agli utenti di controllare le impostazioni del server SMTP (in uscita), è necessario utilizzare il cmdlet **Set-ReceiveConnector**.

Effettuare le seguenti operazioni per consentire agli utenti di cercare le proprie impostazioni dei server POP3, IMAP4 e SMTP:

  - **Impostazioni POP3**   Eseguire il cmdlet **Set-POPSettings** con il parametro *ExternalConnectionSettings*. Utilizzare il formato `Set-POPSettings -ExternalConnectionSetting {<FQDN>:995:SSL}`. Ad esempio, eseguire `Set-PopSettings -ExternalConnectionSetting {Dublin01.Contoso.com:995:SSL}` se si desidera che i client che si connettono tramite il server con nome di dominio completo Dublin01.Contoso.com possano cercare le proprie impostazioni POP.
    
    Dopo l'applicazione di questa impostazione, è necessario riavviare IIS.

  - **Impostazioni IMAP4**   Eseguire il cmdlet **Set-IMAPSettings** con il parametro *ExternalConnectionSettings*. Utilizzare il formato `Set-ImapSettings -ExternalConnectionSetting {<FQDN>:993:SSL}`. Ad esempio, eseguire `Set-IMAPSettings -ExternalConnectionSetting {Dublin01.Contoso.com:993:SSL}` se si desidera che i client che si connettono tramite il server con nome di dominio completo Dublin01.Contoso.com possano cercare la propria impostazione IMAP.
    
    Dopo l'applicazione di questa impostazione, è necessario riavviare IIS.

  - **Impostazioni SMTP**   Eseguire il cmdlet **Set-ReceiveConnector** con il parametro *AdvertiseClientSettings*. Utilizzare il formato `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN <FQDN>`. Ad esempio, eseguire `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN Dublin01.Contoso.com` se si desidera che i client che si connettono tramite il server con nome di dominio completo Dublin01.Contoso.com possano cercare la propria impostazione SMTP.
    
    Dopo l'applicazione di questa impostazione, è necessario riavviare IIS.

Dopo aver cambiato le impostazioni predefinite con i cmdlet **Set-POPSettings**, **Set-IMAPSettings** e **Set-ReceiveConnector**, gli utenti possono cercare le impostazioni dei server POP, IMAP e SMTP esterni in Outlook Web App selezionando **Impostazioni** \> **Opzioni** \> **Account** \> **Account personale** \> **Impostazioni per l'accesso POP o IMAP**.

**Mantenimento di una copia dei messaggi sul server**

L'impostazione predefinita in alcuni programmi di posta elettronica prevede la rimozione dei messaggi sul server una volta scaricati. È opportuno consigliare agli utenti di impostare il proprio programma di posta elettronica in modo che venga mantenuta una copia dei messaggi recuperati dal client sul server. Il mantenimento di una copia dei messaggi sul server consente agli utenti di accedere ai propri messaggi da un programma di posta elettronica differente.


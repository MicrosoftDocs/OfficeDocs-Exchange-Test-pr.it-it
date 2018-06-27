---
title: 'Note sulla versione di Exchange 2013: Exchange 2013 Help'
TOCTitle: Note sulla versione di Exchange 2013
ms:assetid: 1879fd5e-3d63-4264-9cc2-9c050c6ab3c5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150489(v=EXCHG.150)
ms:contentKeyID: 50480127
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Note sulla versione di Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2018-04-16_

Welcome to Microsoft Exchange Server 2013 \! In questo argomento è riportate informazioni importanti che è necessario conoscere per distribuire correttamente Exchange 2013. Leggere questo argomento completamente prima dell'inizio della distribuzione.

In questa sezione sono contenute le seguenti sezioni:

  - Setup and deployment

  - Exchange Management Shell

  - Mailbox

  - Public folders

  - Mail flow

  - Client connectivity

  - Coesistenza di Exchange 2010

## Installazione e distribuzione

  - **msExchProductId non riflette la versione definitiva di installazione di Exchange 2013** Dopo Exchange consente di estendere lo schema di Active Directory e prepara Active Directory per Exchange, numerose proprietà vengono aggiornate in modo da visualizzare preparazione completata. Una di queste proprietà è *msExchangeProductId* sotto il contenitore `CN=<your organization>, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=<domain>` nel contesto di denominazione `Configuration` . Se nessun modifiche allo schema di Active Directory vengono introdotti nella versione di Exchange 2013 che si sta installando, questa proprietà non vengono aggiornata o potrebbe visualizzare un valore imprevisto. Ciò potrebbe causare confusione se valore non corrisponde la versione di Exchange 2013 in fase di installazione.
    
    Questo comportamento è previsto come il valore di *msExchProductId* non riflette la versione di Exchange 2013 in fase di installazione. Questa proprietà riflette la versione di Exchange 2013 che ha apportato l'ultima modifiche allo schema di Active Directory. Per evitare confusione, si consiglia di eseguire le operazioni seguenti nella [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) sezione della [Preparazione di Active Directory e dei domini](prepare-active-directory-and-domains-exchange-2013-help.md) per verificare che Active Directory è stata aggiornata e pronto per la versione di Exchange 2013 che si sta installando.

  - **L'installazione richiede erroneamente .NET Framework 4.0** se si tenta di installare Exchange 2013 senza .NET Framework installato nel computer, l'installazione richiede erroneamente installare .NET Framework 4.0 quando, infatti, è necessario .NET Framework 4.5 o versione successiva.
    
    Per risolvere questo problema, installare .NET Framework 4.5 o versione successiva. Non è necessario installare .NET Framework 4.0. Per un elenco completo dei prerequisiti, vedere [Prerequisiti di Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - I file di configurazione XML di **Exchange XML vengono sovrascritti durante l'installazione dell'aggiornamento cumulativo**   Qualsiasi impostazione personalizzata per singolo server apportata nei file di configurazione XML di Exchange XML application configuration files, ad esempio, i file web.config sui server Accesso client oppure il file EdgeTransport.exe.config sui server Cassette postali, verrà sovrascritta quando si installa un aggiornamento cumulativo o un Service Pack di Exchange. Salvare queste informazioni in modo da poter facilmente riconfigurare il server dopo l'installazione. È necessario configurare nuovamente queste impostazioni dopo aver installato l'aggiornamento cumulativo o il Service Pack di Exchange.

  - **Installazione di Exchange tramite le autorizzazioni di amministratore delegato fa sì che eseguire il programma di installazione** Quando un utente appartenente solo la delega dell'installazione tenta di installare Exchange in un server già eseguito il gruppo di ruoli, il programma di installazione avrà esito negativo. Questo accade perché il gruppo configurazione delegata non dispone delle autorizzazioni necessarie per creare e configurare determinati oggetti in Active Directory.
    
    Per risolvere questo problema, effettuare una delle operazioni seguenti:
    
      - Aggiungere l'utente di installazione di Exchange per il gruppo di sicurezza gli amministratori di dominio Active Directory.
    
      - Installazione di Exchange con un utente membro del gruppo di ruoli Gestione organizzazione.

Per ulteriori informazioni su come installare i Exchange 2013, vedere [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md).

## Exchange Management Shell

  - **Caricamento in modo imprevisto della Shell di Exchange 2007 o i cmdlet di Exchange 2010** Aprire Shell su un server di Exchange 2013 genera in precedenza, nella Shell di aprire una connessione a server locale o un altro server che esegue Exchange 2013. Quando viene eseguita la connessione, vengono caricati cmdlet di Exchange 2013. A partire da Exchange 2013 CU11, Shell si connetterà alla cassetta postale dell'utente attualmente connesso al computer in cui si trova il server di Exchange. Se l'utente ha effettuato l'accesso non dispone di una cassetta postale, Shell sarà connettersi al server in cui si trova la cassetta postale di arbitraggio SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} . Server di destinazione può essere qualsiasi versione supportata di Exchange. Di conseguenza se cassetta postale dell'utente connesso (o cassetta postale di arbitraggio se l'utente non ha alcuna cassetta postale di) si trova su un server di Exchange 2010, Shell sarà connettersi al server e caricare i cmdlet di Exchange 2010. Ciò potrebbe impedire l'esecuzione di alcune attività poiché i cmdlet di Exchange 2010 non possono gestire la configurazione di Exchange 2013 o server.
    
    A partire da Exchange 2013 CU11, questo comportamento è per impostazione predefinita. Per verificare che al caricamento della Shell cmdlet di Exchange 2013, spostare la connessione nella cassetta postale in Exchange 2013. Se l'utente ha effettuato l'accesso non dispone di una cassetta postale, spostare la cassetta postale di arbitraggio SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} in un server Exchange 2013.
    
    Per informazioni su come spostare la cassetta postale di arbitraggio e ulteriori informazioni, vedere [Exchange Management Shell e cassetta postale di ancoraggio](https://go.microsoft.com/fwlink/?linkid=717722) nel blog del Team di Exchange.

## Cassetta postale

  - **Allo stesso gruppo di disponibilità del database, è possibile aggiungere i server cassette postali che eseguono versioni diverse di Exchange** Il cmdlet **Add-DatabaseAvailabilityGroupServer** e l'interfaccia di amministrazione di Exchange in modo non corretto consentire a un server Exchange 2013 da aggiungere a un Exchange 2016-basato su gruppo di disponibilità del database (DAG) e viceversa. Exchange supporta l'aggiunta di server di cassette postali solo esegue la stessa versione (Exchange 2013 e Exchange 2016, ad esempio) a un DAG. Exchange Admin Center, inoltre, viene visualizzato sia Exchange 2013Exchange 2016 server server nell'elenco dei server disponibili per l'aggiunta di un DAG. In questo modo un amministratore di inavvertitamente aggiungere un server che esegue una versione compatibile di Exchange per un DAG (ad esempio, aggiungere un server di Exchange 2013 a una Exchange 2016-base DAG).
    
    Attualmente non è disponibile alcuna soluzione alternativa a questo problema. Gli amministratori devono essere attente quando si aggiunge un server cassette postali a un DAG. Aggiungere solo Exchange 2013 server Exchange 2013-base DAG e solo Exchange 2016 server Exchange 2016-base DAG. Ogni versione di Exchange distinguere esaminando la colonna **versione** nell'elenco dei server nell'interfaccia di amministrazione di Exchange. Le versioni del server per Exchange 2013 e Exchange 2016 sono i seguenti:
    
      - **Exchange 2013** 15.0 (Build xxx.xx)
    
      - **Exchange 2016** 15.1 (Build xxx.xx)

  - **Le dimensioni delle cassette postali aumentano quando si migra dalle precedenti versioni di Exchange**   Quando si sposta una cassetta postale da una versione precedente di Exchange a Exchange 2013, le dimensioni della cassetta postale riportate possono aumentare dal 30 al 40 per cento. Lo spazio su disco utilizzato dalla cassetta postale non è aumentato, è aumentata solo l'attribuzione dello spazio utilizzato da ciascuna cassetta postale. L'aumento delle dimensioni delle cassette postali è dovuto all'inserimento delle proprietà di tutti gli elementi nei calcoli della quota, fornendo un calcolo più preciso dello spazio occupato dai vari elementi all'interno della cassetta postale. Tale aumento potrebbe causare un problema ad alcuni utenti che potrebbero superare le quote previste per le dimensioni della cassetta postale quando questa viene spostata su Exchange 2013.
    
    Per evitare che gli utenti superino la quota prevista per le dimensioni della cassetta postale, aumentare i valore delle quote del database o della cassetta postale in modo che si adattino al calcolo delle nuove quote. Per configurare i valori delle quote della cassetta postale o del database, utilizzare i parametri *IssueWarningQuota*, *ProhibitSendQuota* e *ProhibitSendReceiveQuota* rispettivamente sui cmdlet **Set-MailboxDatabase** e **Set-Mailbox**.

  - I client di **Outlook 2007 e Outlook 2010 potrebbero non essere in grado di scaricare la Rubrica fuori rete**   Se l'URL interno della Rubrica fuori rete (OAB) non è accessibile da Internet, i client di Outlook 2007 e Outlook 2010 potrebbero non essere in grado di scaricare la Rubrica fuori rete.
    
    Per risolvere il problema nei client Outlook 2007 e Outlook 2010, rendere accessibile da Internet l'URL interno della Rubrica fuori rete (OAB). Questo problema non riguarda Outlook 2013.

  - **L'installazione di Exchange 2013 in un'organizzazione di Exchange esistente potrebbe far scaricare la Rubrica fuori rete a tutti i client**   L'installazione del primo server di Exchange 2013 in un'organizzazione esistente di Exchange 2007 o Exchange 2010 potrebbe far scaricare a tutti i client nell'organizzazione una nuova copia della Rubrica fuori rete, causando saturazione della rete e problemi relativi alle prestazioni del server. Questo problema si verifica perché Exchange 2013 crea una nuova Rubrica fuori rete predefinita nell'organizzazione che sostituisce la Rubrica fuori rete di Exchange 2007 o Exchange 2010. Le cassette postali che non dispongono di una specifica Rubrica fuori rete assegnata o che si trovano in un database della cassetta postale al quale non è stata assegnata una Rubrica fuori rete specifica, scaricheranno la nuova Rubrica fuori rete predefinita.
    
    Per impedire ai client di scaricare una nuova copia della Rubrica fuori rete quando Exchange 2013 viene installato, assegnare una Rubrica fuori rete a ogni cassetta postale o a ogni database di cassette postali in cui si trova la cassetta postale. Questo deve essere fatto prima che Exchange 2013 venga installato nell'organizzazione.

  - **Gli utenti potrebbero essere instradati a una cassetta postale di generazione della Rubrica fuori rete non responsabile per la Rubrica offline richiesta** Exchange 2013 CU5 e versioni successive CUs sono state modificate le modalità di collegamento rubriche offline alle cassette postali di generazione della Rubrica fuori rete. Questa modifica rende un utente di eseguire il routing di una cassetta postale di generazione della Rubrica fuori rete che non è responsabile per la Rubrica fuori rete che richiede all'utente. Questa situazione può verificarsi se tutte le operazioni seguenti:   
    
      - Si dispone di più cassette di generazione Rubrica fuori rete nell'organizzazione.
    
      - I server Cassette postali che ospitano le cassette postali di generazione Rubrica fuori rete vengono aggiornati prima dei server Accesso client.
    
      - Si sta aggiornando i server di Exchange 2013 da una versione precedente a CU5 a una versione successiva (per esempio, l'aggiornamento da Exchange 2013 CU3 a Exchange 2013 aggiornamento cumulativo 6).
    
      - I server Accesso client eseguono una versione precedente a CU5.
    
    Per risolvere questo problema, verificare che l'aggiornamento dei server Accesso Client a Exchange 2013 aggiornamento cumulativo 6 o versioni successive prima di aggiornare il server cassette postali. Questo verrà accertarsi di conoscono i server Accesso Client come proxy le richieste di alla cassetta postale di generazione della Rubrica fuori rete che è responsabile della generazione Rubrica fuori rete dell'utente.
    
    Per saperne di più sulle modifiche della Rubrica offline in Exchange 2013 CU5, vedere [Miglioramenti della Rubrica offline in Exchange 2013 cumulativo aggiornamento 5](https://go.microsoft.com/fwlink/p/?linkid=400642).

## Cartelle pubbliche

  - **I mittenti non autorizzati non è più possono inviare messaggi alle cartelle pubbliche abilitate alla posta**   Prima dell'aggiornamento cumulativo 6 di Exchange 2013, mittenti attendibili non autorizzati potrebbero inviare messaggi alle cartelle pubbliche abilitate. Questa è consentita la possibilità per i mittenti esterni inviare posta a cartelle pubbliche abilitate alla posta indipendentemente dalle autorizzazioni impostate per la cartella pubblica.
    
    A partire da aggiornamento cumulativo 6 di Exchange 2013, se si desidera che i mittenti esterni possano inviare posta a un cartelle pubbliche abilitate alla posta, l'utente **anonimo** deve disporre almeno dell'autorizzazione **Creazione degli elementi**. Se si è mai stato eseguito configurato cartelle pubbliche abilitate alla posta elettronica, i mittenti esterni riceverà una notifica di recapito del e i messaggi non recapitati nella cartella pubblica supportano la posta elettronica.
    
    È possibile utilizzare la Shell o Outlook per impostare le autorizzazioni per l'utente anonimo. Leggere ulteriori informazioni su come impostare le autorizzazioni per l'utente anonimo, vedere [Posta elettronica attiva o Disattiva posta una cartella pubblica](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

  - Il numero massimo di cartelle pubbliche che può eseguire la migrazione a Exchange 2013 dal server Exchange legacy è 500.000. Per ulteriori informazioni sulla migrazione delle cartelle pubbliche, vedere [Utilizzare la migrazione seriale per spostare le cartelle pubbliche in Exchange 2013 dalle versioni precedenti](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md).

## Flusso di posta

  - **I cmdlet TransportAgent cmdlets sui server Accesso client richiedono Windows PowerShell locale**   Esiste un problema con i cmdlet **\*-TransportAgent** che ne impediscono l'installazione o disinstallazione e gestione degli agenti di trasporto sui server Accesso client che utilizzano Exchange Management Shell. Per installare, disinstallare e gestire gli agenti di trasporto sui server Accesso client, è necessario caricare lo snap-in di ExchangeWindows PowerShell e gestire i cmdlet **\*-TransportAgent**. Se si tenta di installare, disinstallare o gestire gli agenti di trasporto utilizzando Exchange Management Shell, le modifiche verranno applicate al server cassette postali di Exchange 2013 a cui si è connessi.
    
    Per installare, disinstallare o gestire gli agenti di trasporto sui server Accesso client, effettuare le seguenti operazioni sul server Accesso client che si desidera gestire.
    

    > [!WARNING]
    > Il caricamento dello snap-in di <CODE>Microsoft.Exchange.Management.PowerShell.SnapIn</CODE>Windows PowerShell e l'esecuzione dei cmdlet diversi dai cmdlet <STRONG>*-TransportAgent</STRONG> cnon è supportato e potrebbe dar luogo a danni irreparabili alla distribuzione di Exchange.<BR>Per installare, disinstallare o gestire gli agenti di trasporto è necessario essere un amministratore locale sul server Accesso client. Non è supportata la modifica di elenchi di controllo di accesso (ACL) sui file e directory di Exchange o sugli oggetti di Active Directory.

    

    > [!IMPORTANT]
    > Attenersi alla seguente procedura solo sul server Accesso client. Non è necessario caricare lo snap-in di ExchangeWindows PowerShell se si desidera gestire gli agenti di trasporto sui server Cassette postali.

    
    1.  Aprire una nuova finestra di Windows PoweShell.
    
    2.  Eseguire il comando riportato di seguito.
        
            Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn
    
    3.  Eseguire normalmente le attività di gestione degli agenti.
    
    4.  Ripetere questa procedura su ciascun server Accesso Client che si desidera gestire.

## Connettività dei client

  - **L'autenticazione NTLM non riesce per i client non aggiunti al domino**   L'autenticazione tra un client, come Windows Live Mail e Exchange 2013 potrebbe non riuscire se le seguenti condizioni sono vere:
    
      - Il metodo di autenticazione che utilizza il client è NTLM.
    
      - Il computer non è stato aggiunto al dominio.
    
    Per ovviare a questo problema, è possibile effettuare una delle seguenti operazioni:
    
      - Aggiungere il computer in esecuzione sul client al dominio.
    
      - Modifica il tipo di autenticazione che il client utilizza da NTLM per autenticazione di base su TLS.

  - **L'autenticazione GSSAPI non riesce quando si utilizza insieme al cmdlet Send-MailMessage**   L'autenticazione del programma GSSAPI (Generic Security Service Application Program Interface) potrebbe non riuscire quando il cmdlet **Send-MailMessage**, incluso nell'installazione predefinita di Windows PowerShell viene utilizzato per inviare la posta autenticata a Exchange 2013. Quando ciò si verifica, viene visualizzata una voce nel registro evento dell'**applicazione** nel server Accesso client di Exchange 2013 che ha ricevuto la connessione, insieme alle seguenti informazioni:
    
      - **Origine**   MSExchangeFrontEndTransport
    
      - **ID evento**   1035
    
      - **Descrizione** Autenticazione in ingresso non riuscita con errore `IllegalMessage` per il connettore di ricezione front-end client \<*nome server*\>. Il meccanismo di autenticazione è Gssapi. L'indirizzo IP di origine del client che ha tentato l'autenticazione per Exchange è \[\<*indirizzo IP client*\>\].
    
    Per risolvere questo problema, è necessario rimuovere il metodo di autenticazione `Integrated` dal connettore di ricezione client sui server Accesso client di Exchange 2013. Per rimuovere il metodo di autenticazione `Integrated` da un connettore di ricezione client, eseguire il seguente comando su ciascun server Accesso client di Exchange 2013 che può ricevere le connessioni da computer che eseguono il cmdlet **Send-MailMessage**:
    
        Set-ReceiveConnector "<server name>\Client Frontend <server name>" -AuthMechanism Tls, BasicAuth, BasicAuthRequireTLS

  - **Le prestazioni di MAPI tramite HTTP potrebbero essere ridotte quando si esegue l'aggiornamento a Exchange 2013 SP1**   Se si esegue l'aggiornamento da un aggiornamento cumulativo di Exchange 2013 a Exchange 2013 SP1 e si attiva MAPI tramite HTTP, i client che si connettono a un server di Exchange 2013 SP1 usando il protocollo potrebbero rilevare un peggioramento delle prestazioni. Questo perché le impostazioni necessarie non vengono configurate durante un aggiornamento da un aggiornamento cumulativo a Exchange 2013 SP1. Questo problema non si verifica se si esegue l'aggiornamento a Exchange 2013 SP1 da Exchange 2013 RTM o se si installa un nuovo server di Exchange 2013 SP1 o versione successiva.
    

    > [!NOTE]
    > È un problema solo se MAPI tramite protocollo HTTP è attivato nei server Accesso Client. È disabilitato per impostazione predefinita. Se MAPI tramite HTTP è disabilitato, i client usano il protocollo RPC tramite HTTP.

    
    Per risolvere il problema, procedere come segue:
    
    1.  Nei server che eseguono il ruolo del server Accesso client, eseguire i seguenti comandi in un prompt dei comandi di Windows:
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiFrontEndAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiFrontEndAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiFrontEndAppPool"
    
    2.  Nei server che eseguono il ruolo del server Cassette postali, eseguire i seguenti comandi in un prompt dei comandi di Windows:
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiMailboxAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiMailboxAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiMailboxAppPool"
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiAddressBookAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiAddressBookAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiAddressBookAppPool"

## Coesistenza di Exchange 2010

  - **La richiesta di accesso alle cassette postali di Exchange 2010 potrebbe non funzionare quando è proxy attraverso i server Accesso client di Exchange 2013**   In alcune situazioni, la richiesta proxy tra i server Accesso client di Exchange 2013 e Exchange 2010 Service Pack 3 (SP3) senza pacchetti di aggiornamento cumulativo installati potrebbero non funzionare correttamente e viene visualizzato un errore. Questo problema si verifica in presenza di tutte le seguenti condizioni:
    
      - Un utente con una cassetta postale di Exchange 2013 prova ad aprire una cassetta postale di Exchange 2010 tramite uno dei seguenti metodi:
        
          - L'opzione **Apri altra cassetta postale** in Outlook Web App**-O-**
        
          - L'opzione **Un altro utente** nell'interfaccia di amministrazione di Exchange
    
      - Il server Accesso client al quale si connette l'utente esegue Exchange 2013.
    
      - Il server Accesso client di Exchange 2010 è stato aggiornato a Exchange 2010 SP3 dalla versione RTM di Exchange 2010 o Service Pack di Exchange 2010 precedente.
    
    Se tutte le condizioni elencate sopra sono vere, l'utente non sarà in grado di accedere alle altre opzioni di Exchange 2010Outlook Web App e potrebbe essere visualizzata una pagina vuota.
    
    Per risolvere questo problema, installare Exchange 2010 SP3 Update Rollup 1 o versione successiva su ciascun server Exchange 2010.


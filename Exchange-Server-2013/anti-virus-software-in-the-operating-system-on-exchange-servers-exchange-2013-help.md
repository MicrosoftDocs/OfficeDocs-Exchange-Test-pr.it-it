---
title: 'Software antivirus nel sistema operativo dei server Exchange: Exchange 2013 Help'
TOCTitle: Software antivirus nel sistema operativo dei server Exchange
ms:assetid: 7cef6017-7a55-41f3-a636-1ca4fce575b1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb332342(v=EXCHG.150)
ms:contentKeyID: 50481038
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Software antivirus nel sistema operativo dei server Exchange

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-07-22_

In questo argomento, vengono descritti gli effetti dei programmi antivirus a livello di file sui computer su cui è installato Microsoft Exchange Server 2013. Se vengono implementate le indicazioni descritte in questo argomento, sarà possibile migliorare la protezione e l'integrità dell'organizzazione Exchange.

I programmi antivirus a livello di file vengono utilizzati di frequente, tuttavia, se configurati in modo errato, possono causare problemi in Exchange 2013. Esistono due tipi di programmi antivirus a livello di file:

  - Per *ricerca a livello di file residente in memoria* si intende una parte di software antivirus che viene sempre caricata in memoria. e che consente di controllare tutti i file utilizzati nel disco rigido e nella memoria del computer.

  - Per *ricerca a livello di file su richiesta* si intende una parte di software antivirus che può essere configurata per eseguire la ricerca nei file presenti sul disco rigido in modo manuale o in base a una pianificazione. In alcune versioni di software antivirus la ricerca su richiesta viene avviata automaticamente dopo l'aggiornamento delle impronte digitali del virus per garantire che la ricerca venga eseguita in tutti i file con le impronte più recenti.

Quando vengono utilizzati programmi antivirus a livello di file in Exchange 2013, possono verificarsi i seguenti problemi:

  - È possibile che la ricerca venga eseguita in un file mentre è in uso oppure in base a un intervallo pianificato. Pertanto, se Exchange 2013 tenta di utilizzare un file di registro o di database di Exchange, il programma antivirus potrebbe bloccare il file o metterlo in quarantena. Tale comportamento può provocare un errore grave in Exchange 2013, nonché errori nel registro eventi -1018.

  - I programmi antivirus a livello di file non forniscono protezione contro virus della posta elettronica, quali Storm Worm. Storm Worm era un programma di tipo backdoor trojan horse che si autopropagava tramite messaggi di posta elettronica. Il worm attaccava il computer infetto facendo sì che il computer iniziasse a inviare messaggi di posta indesiderata ad intervalli periodici.

## Consigli per l'utilizzo delle scansioni a livello di file con Exchange 2013

Se nei server Exchange 2013 vengono distribuiti programmi antivirus a livello di file, assicurarsi che vengano implementate le esclusioni appropriate relative a directory, processi ed estensioni di nomi file, per la ricerca a livello di file e di memoria. In questa sezione, vengono descritte le esclusioni consigliate relativamente a directory, processi ed estensioni di nomi file.

**Sommario**

Directory exclusions

Process exclusions

File name extension exclusions

## Esclusioni di directory

È necessario escludere directory specifiche per ogni server Exchange su cui viene eseguito il programma antivirus a livello di file. In questa sezione, vengono descritte le directory da escludere dalla scansione a livello di file.

  - **Server Cassette postali**
    
      - **Database delle cassette postali**
        
          - Database e file dei punti di arresto e di registro di Exchange. Per impostazione predefinita, questi elementi si trovano in sottocartelle della cartella %ExchangeInstallPath%Mailbox. Per determinare la posizione di un database di cassette postali, un file di registro delle transazioni e di un file del punto di arresto, eseguire il comando riportato di seguito: `Get-MailboxDatabase -Server <servername>| Format-List *path*`
        
          - Indici del contenuto dei database. Per impostazione predefinita, questi file si trovano nella stessa cartella del file del database.
        
          - File di metrica del gruppo. Per impostazione predefinita, questi file si trovano nella cartella %ExchangeInstallPath%GroupMetrics.
        
          - File di registro generali, ad esempio file di registro di verifica messaggi e ripristino del calendario. Per impostazione predefinita, questi file si trovano in sottocartelle delle cartelle %ExchangeInstallPath%TransportRoles\\Logs ed %ExchangeInstallPath%Logging. Per determinare i percorsi dei registri utilizzati, eseguire il comando riportato di seguito in Exchange Management Shell: `Get-MailboxServer <servername> | Format-List *path*`
        
          - I File della rubrica non in linea. Per impostazione predefinita, questi file si trovano in sottocartelle della cartella %ExchangeInstallPath%ClientAccess\\OAB.
        
          - File di sistema IIS nella cartella %SystemRoot%\\System32\\Inetsrv.
        
          - La cartella temporanea del database delle cassette postali: %ExchangeInstallPath%Mailbox\\MDBTEMP
    
      - **Membri di gruppi di disponibilità del database**
        
          - Tutti gli elementi riportati nell'elenco **Database di cassette postali** e il database di quorum cluster presente in %Windir%\\Cluster.
        
          - I file della directory di controllo. Questi file si trovano in un altro server all'interno dell'ambiente, generalmente un server Accesso client non installato sullo stesso computer del server Cassette postali. Per impostazione predefinita, i file della directory di controllo si trovano %SystemDrive%:\\DAGFileShareWitnesses\\\<DAGFQDN\>.
    
      - **Servizio di trasporto**
        
          - File di registro quali, ad esempio, registri di connettività e verifica dei messaggi. Per impostazione predefinita, questi file si trovano in sottocartelle della cartella %ExchangeInstallPath%TransportRoles\\Logs. Per determinare i percorsi dei registri utilizzati, eseguire il comando riportato di seguito in Exchange Management Shell: `Get-TransportService <servername> | Format-List *logpath*,*tracingpath*`
        
          - Cartelle di directory messaggio prelievo e riesecuzione. Per impostazione predefinita, queste cartelle si trovano nella cartella % ExchangeInstallPath % TransportRoles. Per determinare i percorsi in uso, eseguire il comando seguente in Exchange Management Shell: `Get-TransportService <servername>| Format-List *dir*path*`
        
          - Il database delle code, i punti di controllo e i file di registro. Per impostazione predefinita, si trovano nella cartella %ExchangeInstallPath%TransportRoles\\Data\\Queue.
        
          - Il database di reputazione del mittente, i punti di controllo e i file di registro. Per impostazione predefinita, si trovano nella cartella %ExchangeInstallPath%TransportRoles\\Data\\SenderReputation.
        
          - Le cartelle temporanee utilizzate per eseguire le seguenti conversioni:
            
              - Per impostazione predefinita, le conversioni del contenuto vengono eseguite nella cartella %TMP% del server Exchange.
            
              - Per impostazione predefinita, il formato RTF (RTF) per le conversioni MIME/HTML vengono eseguite nella cartella %ExchangeInstallPath%\\Working\\OleConverter.
        
          - Il componente di scansione del contenuto viene utilizzato dall'agente Malware e dal DLP. Per impostazione predefinita, questi file si trovano nella cartella %ExchangeInstallPath%FIP-FS.
    
      - **Servizio Trasporto cassette postali**
        
          - File di registro quali, ad esempio, i registri di connettività. Per impostazione predefinita, questi file si trovano in sottocartelle della cartella %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox. Per determinare i percorsi dei registri utilizzati, eseguire il comando riportato di seguito in Exchange Management Shell: `Get-MailboxTransportService <servername> | Format-List *logpath*`
    
      - **Messaggistica unificata   **
        
          - I file di grammatica per impostazioni internazionali diverse, ad esempio en-EN o es-ES. Per impostazione predefinita, questi vengono archiviati in sottocartelle della cartella %ExchangeInstallPath%UnifiedMessaging\\grammars.
        
          - Istruzioni vocali, messaggi di saluto e i file di messaggio informativo. Per impostazione predefinita, questi vengono archiviati nelle sottocartelle della cartella %ExchangeInstallPath%UnifiedMessaging\\Prompts
        
          - I file del sistema di caselle vocali vengono temporaneamente archiviati nella cartella %ExchangeInstallPath%UnifiedMessaging\\voicemail.
        
          - I file temporanei generati dalla messaggistica unificata. Per impostazione predefinita, questi vengono archiviati nella cartella %ExchangeInstallPath%UnifiedMessaging\\temp.
    
      - **Impostazione**
        
          - File temporanei dell'installazione di Exchange Server. Questi file vengono in genere si trova in % SystemRoot%\\Temp\\ExchangeSetup.
    
      - **Servizio di ricerca di Exchange**
        
          - File temporanei utilizzati dal servizio di ricerca di Exchange e Microsoft Filter Pack per eseguire la conversione dei file in un ambiente sandbox. Questi file si trovano in %SystemRoot%\\Temp\\OICE\_*\<GUID\>*\\.

<!-- end list -->

  - **Server Accesso client**
    
      - **Componenti Web**
        
          - Per i server con Internet Information Services (IIS) 7.0, la cartella di compressione viene utilizzata con Microsoft Outlook Web App. Per impostazione predefinita, la cartella di compressione di IIS 7.0 si trova in %SystemDrive%\\inetpub\\temp\\IIS Temporary Compressed Files.
        
          - File di sistema di IIS nella cartella %SystemRoot%\\System32\\Inetsrv
        
          - Inetpub\\logs\\logfiles\\w3svc
        
          - Le sottocartelle in %SystemRoot%\\Microsoft.NET\\Framework64\\v4.0.30319\\Temporary ASP.NET Files
    
      - **Registrazione protocolli POP3 e IMAP4**
        
          - Cartella POP3: %ExchangeInstallPath%Logging\\POP3
        
          - Cartella IMAP4: %ExchangeInstallPath%Logging\\IMAP4
    
      - **Servizio Trasporto front-end**
        
          - File di registro quali, ad esempio, registri di connettività e protocollo. Per impostazione predefinita, questi file si trovano in sottocartelle della cartella %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd. Per determinare i percorsi dei registri utilizzati, eseguire il comando riportato di seguito in Exchange Management Shell: `Get-FrontEndTransportService <servername> | Format-List *logpath*`
    
      - **Impostazione**
        
          - File temporanei il programma di installazione di Exchange Server. Questi file sono in genere si trova in % SystemRoot%\\Temp\\ExchangeSetup.

Inizio pagina

## Esclusioni di processi

Molti programmi antivirus a livello di file supportano la ricerca all'interno dei processi, che può influire negativamente su Microsoft Exchange se la ricerca viene eseguita nei processi errati. Pertanto, è necessario escludere i seguenti processi dal programma antivirus a livello di file.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Procedura</th>
<th>Percorso</th>
<th>Commenti</th>
<th>Server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dsamain.exe</p></td>
<td><p>%SystemRoot%\System32</p></td>
<td><p>Active Directory Lightweight Directory Services (AD LDS) nei server Trasporto Edge sottoscritto.</p></td>
<td><p>Server Trasporto Edge</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Processo di lavoro del servizio di trasporto di Microsoft Exchange</p></td>
<td><p>Server Cassette postali</p>
<p>Server Trasporto Edge</p></td>
</tr>
<tr class="odd">
<td><p>fms.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Componente di analisi del contenuto utilizzato dall'agente Malware e DLP.</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>hostcontrollerservice.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\HostController</p></td>
<td><p>Servizio Microsoft Exchange Search Host Controller (HostControllerService)</p></td>
<td><p>Server Cassette postali</p>
<p>Server Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>inetinfo.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Internet Information Services (IIS)</p></td>
<td><p>Server Cassette postali</p>
<p>Server Accesso client</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.AntispamUpdateSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio di aggiornamento di protezione da posta indesiderata di Microsoft Exchange (MSExchangeAntispamUpdate)</p></td>
<td><p>Server Cassette postali</p>
<p>Server Trasporto Edge</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.ContentFilter.Wrapper.exe</p></td>
<td><p>%ExchangeInstallPath%TransportRoles\agents\Hygiene</p></td>
<td><p>Agente filtro contenuto</p></td>
<td><p>Server Cassette postali</p>
<p>Server Trasporto Edge</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Diagnostics.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio di diagnostica di Microsoft Exchange (MSExchangeDiagnostics)</p></td>
<td><p>Server Cassette postali</p>
<p>Server Accesso client</p>
<p>Server Trasporto Edge</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Directory.TopologyService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio di topologia di Active Directory di Microsoft Exchange (MSExchangeADTopology)</p></td>
<td><p>Server Cassette postali</p>
<p>Server Accesso client</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.EdgeCredentialSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio credenziali di Microsoft Exchange (MSExchangeEdgeCredential)</p></td>
<td><p>Server Trasporto Edge</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.EdgeSyncSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio EdgeSync di Microsoft Exchange (MSExchangeEdgeSync)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Imap4.exe</p></td>
<td><p>ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Servizio IMAP4 di Microsoft Exchange (MSExchangeImap4)</p></td>
<td><p>Server Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Imap4service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Servizio Microsoft Exchange IMAP4 back-end (MSExchangeIMAP4BE)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Pop3.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Servizio POP3 di Microsoft Exchange (MSExchangePop3)</p></td>
<td><p>Server Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Pop3service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Servizio Microsoft Exchange POP3 back-end (MSExchangePOP3BE)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.ProtectedServiceHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio Host del servizio di Microsoft Exchange (MSExchangeServiceHost)</p></td>
<td><p>Server Cassette postali</p>
<p>Server Accesso client</p>
<p>Server Trasporto Edge</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.RPCClientAccess.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio Accesso Client RPC di Microsoft Exchange (MSExchangeRPC)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Search.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio di ricerca di Microsoft Exchange (MSExchangeFastSearch)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Servicehost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio Host del servizio di Microsoft Exchange (MSExchangeServiceHost)</p></td>
<td><p>Server Cassette postali</p>
<p>Server Accesso client</p>
<p>Server Trasporto Edge</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Store.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio Microsoft Exchange Information Store (MSExchangeIS)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Store.Worker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Processo di lavoro di Microsoft Exchange Information Store service</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.UM.CallRouter.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\CallRouter</p></td>
<td><p>Servizio Microsoft Exchange Unified Messaging routing delle chiamate (MSExchangeUMCR)</p></td>
<td><p>Server Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeDagMgmt.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio di gestione di Microsoft Exchange DAG (MSExchangeDagMgmt)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeDelivery.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio di recapito di trasporto delle cassette postali di Microsoft Exchange (MSExchangeDelivery)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeFrontendTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio trasporto front-end di Microsoft Exchange (MSExchangeFrontEndTransport)</p></td>
<td><p>Server Accesso client</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeHMHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio Microsoft Exchange Health Manager (MSExchangeHM)</p></td>
<td><p>Server Cassette postali</p>
<p>Server Accesso client</p>
<p>Server Trasporto Edge</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeHMWorker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Processo di lavoro di Microsoft Exchange Health Manager service</p></td>
<td><p>Server Cassette postali</p>
<p>Server Accesso client</p>
<p>Server Trasporto Edge</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio Assistenti cassette postali di Microsoft Exchange (MSExchangeMailboxAssistants)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxReplication.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio di replica delle cassette postali di Microsoft Exchange (MSExchangeMailboxReplication)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMigrationWorkflow.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio di flusso di lavoro di Microsoft Exchange Migration (MSExchangeMigrationWorkflow)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeRepl.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio di replica di Microsoft Exchange (MSExchangeRepl)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeSubmission.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio di invio di trasporto delle cassette postali di Microsoft Exchange (MSExchangeSubmission)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio di trasporto di Microsoft Exchange (MSExchangeTransport)</p></td>
<td><p>Server Cassette postali</p>
<p>Server Trasporto Edge</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeTransportLogSearch.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio Microsoft Exchange Transport Log Search (MSExchangeTransportLogSearch)</p></td>
<td><p>Server Cassette postali</p>
<p>Server Trasporto Edge</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeThrottling.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio Microsoft Exchange limitazione (MSExchangeThrottling)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>Noderunner.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\Runtime\1.0</p></td>
<td><p>Servizio di ricerca di Microsoft Exchange (MSExchangeFastSearch)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="odd">
<td><p>OleConverter.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Converte rich text format (RTF) MIME/HTML per i destinatari esterni.</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>ParserServer.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\ParserServer</p></td>
<td><p>Servizio di ricerca di Microsoft Exchange (MSExchangeFastSearch)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="odd">
<td><p>Powershell.exe</p></td>
<td><p>C:\Windows\System32\WindowsPowerShell\v1.0</p></td>
<td><p>Exchange Management Shell</p></td>
<td><p>Server Cassette postali</p>
<p>Server Accesso client</p>
<p>Server Trasporto Edge</p></td>
</tr>
<tr class="even">
<td><p>ScanEngineTest.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Componente di analisi del contenuto che viene utilizzato dall'agente Malware e DLP.</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="odd">
<td><p>ScanningProcess.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Componente di analisi del contenuto che viene utilizzato dall'agente Malware e DLP.</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>TranscodingService.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\Owa\Bin\DocumentViewing</p></td>
<td><p>Visualizzazione documenti WebReady in Outlook Web App.</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="odd">
<td><p>UmService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servizio di messaggistica unificata di Microsoft Exchange (MSExchangeUM)</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>UmWorkerProcess.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Processo di lavoro del servizio messaggistica unificata di Exchange</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="odd">
<td><p>UpdateService.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Componente di analisi del contenuto che viene utilizzato dall'agente Malware e DLP.</p></td>
<td><p>Server Cassette postali</p></td>
</tr>
<tr class="even">
<td><p>W3wp.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Internet Information Services (IIS)</p></td>
<td><p>Server Cassette postali</p>
<p>Server Accesso client</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Esclusioni di estensioni di nomi file

Oltre ad escludere le directory e i processi specifici, si devono escludere le seguenti estensioni di nomi file specifiche di Exchange in caso di errore nelle esclusioni di directory o di spostamento di file dalle loro posizioni predefinite.

  - Estensioni relative all'applicazione:
    
      - .config
    
      - .dia
    
      - .wsb

<!-- end list -->

  - Estensioni relative al database:
    
      - .chk
    
      - .edb
    
      - .jrs
    
      - .jsl
    
      - .log
    
      - .que

<!-- end list -->

  - Estensioni relative alla Rubrica fuori rete:
    
      - .lzx

<!-- end list -->

  - Estensioni relative all'indice del contenuto:
    
      - .ci
    
      - .dir
    
      - .wid
    
      - .000
    
      - .001
    
      - .002

<!-- end list -->

  - Estensioni relative alla messaggistica unificata:
    
      - .cfg
    
      - .grxml

<!-- end list -->

  - Estensioni relative alle metriche di gruppo:
    
      - .dsc
    
      - .txt

Inizio pagina


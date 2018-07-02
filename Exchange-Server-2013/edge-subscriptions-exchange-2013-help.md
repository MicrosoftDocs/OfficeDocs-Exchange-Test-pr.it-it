---
title: 'Sottoscrizioni Edge: Exchange 2013 Help'
TOCTitle: Sottoscrizioni Edge
ms:assetid: 3addd71a-4165-401f-a009-002bcd8baba6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997438(v=EXCHG.150)
ms:contentKeyID: 61183406
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Sottoscrizioni Edge

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

I server Trasporto Edge riducono la superficie di attacco gestendo tutto il flusso di posta Internet e fornendo inoltro SMTP e servizi smart host per l'organizzazione di Exchange. Ulteriori livelli di sicurezza e protezione dei messaggi sono forniti da una serie di agenti eseguiti sul server Trasporto Edge nella rete di perimetro dell'organizzazione. Tali agenti supportano le funzionalità che forniscono protezione contro i virus e la posta indesiderata e applicano le regole di trasporto per controllare il flusso dei messaggi.

Le sottoscrizioni Edge vengono utilizzate per inserire i dati di Active Directory nell'istanza del servizio directory di Active Directory Lightweight Directory Services (AD LDS) nel server Trasporto Edge. Sebbene la creazione di una sottoscrizione Edge sia facoltativa, se un server Trasporto Edge viene sottoscritto all'organizzazione di Exchange, le prestazioni di gestione e le funzionalità di protezione da posta indesiderata risulteranno migliorate. È necessario creare una sottoscrizione Edge, se si prevede di utilizzare la ricerca dei destinatari o l'aggregazione dell'elenco indirizzi attendibili oppure se si prevede di fornire protezione alle comunicazioni SMTP con domini partner utilizzando l'autenticazione MTSL (Mutual Transport Layer Security).

**Sommario**

Edge Subscription Process

Microsoft Exchange EdgeSync Service

Managing Edge Subscriptions

## Processo di sottoscrizione Edge

Un server Trasporto Edge non ha accesso diretto a Active Directory. Le informazioni sui destinatari e sulla configurazione di cui dispone il server Trasporto Edge per elaborare i messaggi vengono archiviate in AD LDS. La creazione di una sottoscrizione Edge garantisce la replica protetta e automatica delle informazioni da Active Directory ad AD LDS. Il processo di sottoscrizione Edge effettua il provisioning delle credenziali utilizzate per stabilire una connessione LDAP protetta tra i server Cassette postali di Exchange 2013 e un server Trasporto Edge sottoscritto. Il servizio Microsoft Exchange EdgeSync (EdgeSync) che viene eseguito nei server Cassette postali esegue periodicamente la sincronizzazione unidirezionale per trasferire i dati aggiornati in AD LDS. In questo modo vengono ridotte le attività di amministrazione eseguite dall'utente nella rete perimetrale permettendo di configurare il server Cassette postali e di sincronizzare le informazioni con il server Trasporto Edge.

Il server Trasporto Edge viene sottoscritto in un sito di Active Directory che contiene i server Cassette postali responsabili di trasferire i messaggi da e e verso i server Trasporto Edge. Il processo di sottoscrizione Edge consente di creare un'affiliazione di appartenenza al sito di Active Directory per il server Trasporto Edge. L'affiliazione al sito consente ai server Cassette postali nell'organizzazione di Exchange di inoltrare messaggi al server Trasporto Edge per il recapito su Internet senza dover configurare connettori di invio espliciti.

Uno o più server Trasporto Edge possono essere sottoscritti solo a un unico sito di Active Directory. Tuttavia, un server Trasporto Edge non può essere sottoscritto in più di un sito di Active Directory. Se sono distribuiti più server Trasporto Edge, è possibile sottoscrivere ciascun server a un sito diverso di Active Directory. Per ciascun server Trasporto Edge è necessaria una singola sottoscrizione Edge.

Per distribuire un server Trasporto Edge ed effettuarne la sottoscrizione a un sito di Active Directory, eseguire i passaggi riportati di seguito:

1.  Installare il ruolo del server Trasporto Edge.

2.  Verificare che i server Cassette postali e il server Trasporto Edge siano in grado di individuare le rispettive posizioni tramite la risoluzione dei nomi DNS.

3.  Nel server Cassette postali, configurare gli oggetti e le impostazioni da replicare nel server Trasporto Edge.

4.  Sul server Trasporto Hub, creare ed esportare il file di sottoscrizione Edge.

5.  Copiare il file di sottoscrizione Edge su un server Cassette postali o una condivisione file accessibile dal sito di Active Directory in cui si trovano i server Cassette postali.

6.  Importare il file di sottoscrizione di Edge nel sito di Active Directory.

## Cosa succede quando si crea una nuova sottoscrizione Edge

Quando si crea un nuovo file di sottoscrizione Edge eseguendo il cmdlet **New-EdgeSubscription** sul server Trasporto Edge, si verifica quanto segue:

  - Viene creato un account AD LDS chiamato account di replica bootstrap EdgeSync (ESBRA). Le credenziali ESBRA vengono utilizzate per autenticare la prima connessione EdgeSync al server Trasporto Edge. L'account è configurato per scadere 24 ore dopo essere stato creato. Pertanto, è necessario completare i sei passaggi della procedure di sottoscrizione descritti nella sezione precedente entro 24 ore. Se l'account ESBRA scade prima che venga completato il processo di sottoscrizione Edge, sarà necessario eseguire nuovamente il cmdlet **New-EdgeSubscription** per creare un nuovo file di sottoscrizione Edge.

  - Le credenziali dell'account ESBRA vengono recuperate da AD LDS e scritte nel file di sottoscrizione Edge. In questo file viene esportata anche la chiave pubblica del certificato autofirmato del server Trasporto Edge. Le credenziali che vengono scritte nel file di sottoscrizione Edge sono specifiche del server da cui il file è stato esportato.

  - Eventuali oggetti di configurazione creati in precedenza nel server Trasporto Edge che verrà ora replicato in AD LDS da Active Directory vengono eliminati da AD LDS e i cmdlet di Exchange Management Shell utilizzati per configurare questi oggetti vengono disabilitati. Tuttavia, è possibile utilizzare i cmdlet **Get-\*** per visualizzare tali oggetti. Eseguendo il cmdlet **New-EdgeSubscription** vengono disabilitati i seguenti cmdlet nel server Trasporto Edge:
    
      - **Set-SendConnector**
    
      - **New-SendConnector**
    
      - **Remove-SendConnector**
    
      - **New-AcceptedDomain**
    
      - **Set-AcceptedDomain**
    
      - **Remove-AcceptedDomain**
    
      - **New-MessageClassification**
    
      - **Set-MessageClassification**
    
      - **Remove-MessageClassification**
    
      - **New-RemoteDomain**
    
      - **Set-RemoteDomain**
    
      - **Remove-RemoteDomain**

Quando si importa il file di sottoscrizione Edge nel server Cassette postali eseguendo il cmdlet **New-EdgeSubscription** nel server Cassette postali:

  - Viene creata la sottoscrizione Edge, aggiungendo un server Trasporto Edge a un'organizzazione di Exchange. EdgeSync propagherà i dati di configurazione in questo server Trasporto Edge, creando un oggetto di configurazione Edge in Active Directory.

  - Ogni server Cassette postali nel sito di Active Directory riceve da Active Directory una notifica relativa alla sottoscrizione di un nuovo server Trasporto Edge. Il server Cassette postali recupera l'account ESBRA dal file sottoscrizione Edge. L'account viene quindi crittografato dal server Cassette postali tramite la chiave pubblica del certificato autofirmato del server Trasporto Edge. Le credenziali crittografate vengono scritte nell'oggetto di configurazione Edge.

  - L'account ESBRA viene crittografato anche da ogni server Cassette postali tramite la relativa chiave pubblica e le credenziali vengono archiviate nell'oggetto di configurazione corrispondente.

  - Vengono creati gli account di replica EdgeSync (ESRA) in Active Directory per ogni coppia di server Trasporto Edge-Cassette postali. Le credenziali degli account ESRA vengono archiviate in ogni server Cassette postali come attributo del relativo oggetto di configurazione.

  - Vengono automaticamente creati connettori di invio per inoltrare i messaggi in uscita dal server Trasporto Edge su Internet e i messaggi in ingresso dal server all'organizzazione di Exchange.

  - Il servizio EdgeSync di Microsoft Exchange eseguito sui server Cassette postali utilizza le credenziali dell'account ESBRA per stabilire una connessione LDAP protetta tra un server Cassette postali e il server Trasporto Edge ed esegue la replica iniziale dei dati. In AD LDS vengono replicati i seguenti dati:
    
      - Dati relativi alla topologia
    
      - Dati di configurazione
    
      - Dati del destinatario
    
      - Credenziali dell'account ESRA

  - Il servizio credenziali di Microsoft Exchange eseguito sul server Trasporto Edge consente di installare le credenziali dell'account ESRA, che verranno utilizzate per autenticare e fornire protezione alle connessioni di sincronizzazione successive.

  - Viene definita la pianificazione di sincronizzazione EdgeSync.

Il servizio EdgeSync di Microsoft Exchange in esecuzione nei server Cassette postali nel sito di Active Directory sottoscritto esegue quindi periodicamente una replica unidirezionale di dati da Active Directory a AD LDS. È possibile utilizzare il cmdlet **Start-EdgeSynchronization** per ignorare la pianificazione di sincronizzazione di EdgeSync e avviare immediatamente la sincronizzazione.

Per ulteriori informazioni sugli account ESRA e su come utilizzarli per rendere più sicuro il processo di sincronizzazione EdgeSync, vedere [Credenziali della sottoscrizione Edge](edge-subscription-credentials-exchange-2013-help.md).

In questo esempio, viene sottoscritto un server Trasporto Edge al sito specificato e viene creato il connettore di invio Internet e il connettore di invio dal server Trasporto Edge ai server Cassette postali.

    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -CreateInternetSendConnector $true -CreateInboundSendConnector $true -Site "Default-First-Site-Name" 


> [!NOTE]
> Se i valori predefiniti dei parametri <EM>CreateInternetSendConnector</EM> e <EM>CreateInboundSendConnector</EM> sono entrambi <CODE>$true</CODE>. Sono riportati solamente a scopo dimostrativo.



In questo esempio viene esportato un file di sottoscrizione di Edge.

    New-EdgeSubscription -FileName "C:\EdgeSubscriptionInfo.xml"


> [!NOTE]
> Quando si esegue il cmdlet <STRONG>New-EdgeSubscription</STRONG> sul server Trasporto Edge, viene richiesto di confermare i comandi che verranno disabilitati e la configurazione che verrà sovrascritta in questo server. Per ignorare la richiesta di conferma utilizzare il parametro <EM>Force</EM>. Questo parametro è utile quando si esegue lo script del cmdlet <STRONG>New-EdgeSubscription</STRONG>. Inoltre, il parametro <EM>Force</EM> consente di sovrascrivere un file esistente con lo stesso nome di quello creato quando si esegue nuovamente la sottoscrizione di un server Trasporto Edge.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-EdgeSubscription](https://technet.microsoft.com/it-it/library/bb123800\(v=exchg.150\)).

## Inviare connettori creati durante il processo di sottoscrizione Edge

Per impostazione predefinita, una volta completato il processo di sottoscrizione Edge consigliato importando il file di sottoscrizione Edge in un server Cassette postali, i connettori di invio necessari per abilitare il flusso di posta end-to-end tra Internet e l'organizzazione Exchange vengono creati automaticamente e tutti i connettori di invio esistenti sul server Trasporto Edge vengono eliminati. In alcuni scenari, è possibile disabilitare la creazione automatica dei connettori di invio e configurarli manualmente. Per ulteriori informazioni sulla configurazione manuale dei connettori di invio, vedere [Configurare manualmente il flusso della posta server Trasporto Edge](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md) e [Configurare il flusso della posta Internet tramite un server Trasporto Edge senza utilizzare EdgeSync](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md).

Il processo di sottoscrizione Edge prevede i seguenti connettori di invio:

  - Un connettore di invio configurato per inoltrare tutti i messaggi di posta elettronica dall'organizzazione Exchange a Internet.

  - Un connettore di invio configurato per inoltrare messaggi di posta elettronica dal server Trasporto Edge all'organizzazione di Exchange.

Inoltre, sottoscrivendo un server Trasporto Edge nell'organizzazione di Exchange si consente ai server Cassette postali nel sito di Active Directory sottoscritto di utilizzare il connettore di invio tra organizzazioni per inoltrare i messaggi al server Trasporto Edge.

## Creare automaticamente un connettore di invio in ingresso per ricevere messaggi da Internet

Per impostazione predefinita, quando si esegue il cmdlet **New-EdgeSubscription** nel server Cassette postali, il parametro del connettore di invio in entrata *CreateInboundSendConnector* è impostato sul valore `$true`. Questa operazione crea il connettore di invio necessario per inviare i messaggi all'organizzazione di Exchange. Nella seguente tabella viene illustrata la configurazione di questo connettore di invio.

### Configurazione automatica del connettore di invio in ingresso

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Proprietà</th>
<th>Valore</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - Inbound to &lt;<em>Nome sito</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:--;1</code></p>
<p>Il valore <code>--</code> nello spazio degli indirizzi rappresenta tutti i domini autorevoli e di inoltro interno accettati per l'organizzazione di Exchange. I messaggi che il server Trasporto Edge riceve per i domini accettati vengono instradati a questo connettore di invio e inoltrati agli smart host.</p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>Nome sottoscrizione Edge</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>False</p></td>
</tr>
<tr class="even">
<td><p><em>SmartHosts</em></p></td>
<td><p><code>--</code></p>
<p>Il valore <code>--</code> nell'elenco degli smart host rappresenta tutti i server Cassette postali nel sito di Active Directory sottoscritto. I server Cassette postali aggiunti al sito di Active Directory sottoscritto dopo aver stabilito la sottoscrizione Edge non partecipano al processo di sincronizzazione di EdgeSync. Tuttavia, vengono automaticamente aggiunti all'elenco di smart host per il connettore di invio in ingresso creato automaticamente. Se nel sito di Active Directory sottoscritto si trovano più server Cassette postali, il carico delle connessioni in ingresso verrà bilanciato tra gli smart host.</p></td>
</tr>
</tbody>
</table>


Non è possibile modificare lo spazio indirizzo o l'elenco degli smart host per il connettore di invio in ingresso creato automaticamente nel momento della creazione. Tuttavia, è possibile impostare il parametro *CreateInboundSendConnector* sul valore `$false` quando si crea una sottoscrizione Edge. Ciò consente di configurare manualmente un connettore di invio dal server Trasporto Edge all'organizzazione di Exchange.

## Creare automaticamente un connettore di invio in uscita per inviare messaggi a Internet

Per impostazione predefinita, quando si esegue il cmdlet **New-EdgeSubscription** nel server Cassette postali, il parametro del connettore di invio in uscita *CreateInternetSendConnector* è impostato sul valore `$true`. Questa operazione crea il connettore di invio necessario per inviare i messaggi all'organizzazione a Internet. Nella seguente tabella viene illustrata la configurazione predefinita di questo connettore di invio.

### Configurazione automatica del connettore di invio Internet

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Proprietà</th>
<th>Valore</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - &lt;<em>Nome sito</em>&gt; to Internet</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:*;100</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>Nome sottoscrizione Edge</em>&gt;</p>

> [!NOTE]
> Il nome della sottoscrizione Edge è lo stesso nome del server Trasporto Edge sottoscritto.


</td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><em>DomainSecureEnabled</em></p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


Se si sottoscrivono più server Trasporto Edge allo stesso sito di Active Directory, non verranno creati connettori di invio Internet aggiuntivi. Verranno invece aggiunte tutte le sottoscrizioni Edge allo stesso connettore di invio come server di origine. Questo carico bilancia le connessioni Internet in uscita nei server Trasporto Edge sottoscritti.

Il connettore di invio in uscita è configurato per inviare messaggi dall'organizzazione di Exchange a tutti i domini SMTP remoti, usando il routing DNS per risolvere i nomi di dominio per i record di risorse MX. Per ulteriori informazioni sulla configurazione manuale di un connettore, vedere [Configurare manualmente il flusso della posta server Trasporto Edge](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md).

## Servizio EdgeSync di Microsoft Exchange

Dopo aver sottoscritto un server Trasporto Edge in un sito di Active Directory, EdgeSync replicherà i dati di configurazione e del destinatario nei server Trasporto Edge. Il servizio replica i seguenti dati da Active Directory ad AD LDS:

  - Configurazione del connettore di invio

  - Domini accettati

  - Domini remoti

  - Classificazioni dei messaggi

  - Elenchi dei mittenti attendibili

  - Elenchi dei mittenti bloccati

  - Destinatari

  - Elenco dei domini di invio e ricezione usati nelle comunicazioni di dominio protette con i partner

  - Elenco dei server SMTP elencati come interni nella configurazione di trasporto dell'organizzazione

  - Elenco dei server Cassette postali nel sito di Active Directory sottoscritto

Per ulteriori informazioni sui dati replicati in AD LDS e sul loro utilizzo, vedere [Dati di replica EdgeSync](edgesync-replication-data-exchange-2013-help.md).

EdgeSync usa un canale LDAP protetto autorizzato e autenticato in modo reciproco per trasferire i dati dal server Cassette postali al server Trasporto Edge.

Per replicare i dati in AD LDS, il server Cassette postali effettua il binding a un server di catalogo globale e recupera i dati aggiornati. EdgeSync avvia una sessione LDAP protetta tra un server Cassette postali e il server Trasporto Edge sottoscritto sulla porta TCP 50636 non standard.

Quando si sottoscrive per la prima volta un server Trasporto Edge a un sito di Active Directory, la replica iniziale che inserisce in AD LDS i dati da Active Directory può richiedere un certo tempo, a seconda della quantità di dati nel servizio di directory. Dopo la replica iniziale, EdgeSync sincronizza solo gli oggetti nuovi e modificati e rimuove gli oggetti eliminati.

## Pianificazione della sincronizzazione

I diversi tipi di dati vengono sincronizzati in base a pianificazioni differenti. La pianificazione di sincronizzazione di EdgeSync specifica l'intervallo massimo tra le sincronizzazioni di EdgeSync. riportati di seguito:

  - Dati di configurazione: 3 minuti.

  - Dati del destinatario: 5 minuti.

  - Dati relativi alla topologia: 5 minuti

È possibile modificare tali intervalli utilizzando il cmdlet **Set-EdgeSyncServiceConfig**. Se si usa il cmdlet **Start-EdgeSynchronization** nel server Cassette postali per forzare la sincronizzazione di sottoscrizione Edge, viene ignorato il timer per la prossima sincronizzazione EdgeSync pianificata e EdgeSync viene avviato immediatamente.

## Selezione dei server Cassette postali

Ogni server Trasporto Edge sottoscritto viene associato a un determinato sito di Active Directory. Se nel sito sono presenti più server Cassette postali, ciascuno di essi può replicare i dati nei server Trasporto Edge sottoscritti. Per evitare problemi tra i server Cassette postali durante la sincronizzazione, il server Cassette postali preferito viene selezionato nel seguente modo:

1.  Il primo server Cassette postali nel sito di Active Directory che esegue un'analisi della topologia e rileva la nuova sottoscrizione Edge esegue la replica iniziale. Poiché tale rilevamento si basa sulla tempistica dell'analisi, qualunque server Cassette postali nel sito potrebbe eseguire la replica iniziale.

2.  Il server Cassette postali che esegue la replica iniziale stabilisce un'opzione di lease EdgeSync e imposta un blocco nella sottoscrizione Edge. Questa opzione di lease "contrassegna" quel server Cassette postali come preferito per fornire i servizi di sincronizzazione al server Trasporto Edge. Il blocco impedisce che il servizio EdgeSync in esecuzione su un altro server Cassette postali si appropri dell'opzione di lease.

3.  L'opzione di lease di EdgeSync ha la durata di un'ora. In quell'ora, nessun altro servizio EdgeSync può appropriarsi dell'opzione a meno che non venga avviata una sincronizzazione manuale prima del termine dell'ora. Se il server Cassette postali preferito non è disponibile per fornire il servizio EdgeSync quando viene eseguita la sincronizzazione manuale, dopo un'attesa di cinque minuti il blocco viene disattivato e un altro servizio EdgeSync utilizza l'opzione di lease ed esegue la sincronizzazione.

4.  Se la sincronizzazione manuale non viene eseguita, la sincronizzazione viene eseguita in base alla pianificazione di sincronizzazione EdgeSync. Se il server preferito non è disponibile quando viene eseguita la sincronizzazione pianificata, dopo un'attesa di cinque minuti il blocco viene disattivato e un altro servizio EdgeSync utilizza l'opzione di lease ed esegue la sincronizzazione.

Questo metodo di blocco e sblocco evita che più istanze del servizio EdgeSync trasferiscano i dati nello stesso server Trasporto Edge contemporaneamente.


> [!NOTE]
> Se nel sito di Active Directory sono presenti anche server Cassette postali di Exchange&nbsp;2010 o Exchange&nbsp;2007, i server Cassette postali di Exchange 2013 avranno sempre la precedenza ed eseguiranno la replica.




> [!NOTE]
> Quando si sottoscrive un server Trasporto Edge in un sito di Active Directory, tutti i server Cassette postali installati in quel momento nel sito di Active Directory possono partecipare la processo di sincronizzazione di EdgeSync. Se uno dei server viene rimosso, il servizio EdgeSync in esecuzione sui server Cassette postali rimanenti continua il processo di sincronizzazione dei dati. Tuttavia, se si installano nuovi server Cassette postali nel sito di Active Directory, questi non parteciperanno automaticamente alla sincronizzazione di EdgeSync. Per far sì che i nuovi server Cassette postali partecipino alla sincronizzazione di EdgeSync, sarà necessario sottoscrivere nuovamente il server Trasporto Edge.



Nella seguente tabella vengono elencate le proprietà EdgeSync relative al processo di blocco e sblocco. Utilizzare il cmdlet **Set-EdgeSyncServiceConfig** per configurare queste proprietà.

### Proprietà di lease di EdgeSync

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Valore predefinito</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>LockDuration</em></p></td>
<td><p><code>00:05:00</code> (5 minuti)</p></td>
<td><p>Questa impostazione determina la durata di un blocco da parte di un determinato servizio EdgeSync. Se il servizio EdgeSync nel server Cassette postali su cui è attivo il blocco non risponde, sarà necessario attendere cinque minuti affinché il servizio EdgeSync su un altro server Cassette postali utilizzi il lease. Se si forza immediatamente la sincronizzazione EdgeSync, questa impostazione non verrà sovrascritta.</p></td>
</tr>
<tr class="even">
<td><p><em>OptionDuration</em></p></td>
<td><p><code>01:00:00</code> 1 ora</p></td>
<td><p>Questa impostazione determina la durata che è possibile dichiarare con il servizio EdgeSync per un'opzione di lease su un server Trasporto Edge. Se il servizio EdgeSync su cui è attiva l'opzione di lease non è disponibile e non si riavvia durante il periodo di attività di questa opzione, nessun altro servizio EdgeSync di Exchange utilizzerà tale opzione, a meno che non si forzi la sincronizzazione EdgeSync.</p></td>
</tr>
<tr class="odd">
<td><p><em>LockRenewalDuration</em></p></td>
<td><p><code>00:01:00</code> (1 minuto)</p></td>
<td><p>Questa impostazione determina la frequenza con cui il campo del blocco viene aggiornato quando un servizio EdgeSync ha acquisito un blocco per un server Trasporto Edge.</p></td>
</tr>
</tbody>
</table>


## Preparazione per l'esecuzione del servizio EdgeSync

Prima di sottoscrivere un server Trasporto Edge all'organizzazione Exchange, è necessario accertarsi che l'infrastruttura e i server Cassette postali siano preparati per il servizio EdgeSync. Per prepararsi per la sincronizzazione di EdgeSync, è necessario:

  - Verificare che il firewall della rete perimetrale che separa il server Trasporto Edge dall'organizzazione Exchange sia configurato per abilitare le comunicazioni attraverso le porte corrette. Il server Trasporto Edge utilizza le porte LDAP non standard. Se l'ambiente richiede porte specifiche, è possibile modificare le porte utilizzate da AD LDS mediante lo script ConfigureAdam.ps1 fornito con Exchange. Per ulteriori informazioni, vedere [Modificare la configurazione di AD LDS](modify-ad-lds-configuration-exchange-2013-help.md). Modificare le porte prima di creare la sottoscrizione Edge. Se si modificano le porte dopo aver creato la sottoscrizione Edge, è necessario rimuovere la sottoscrizione e crearne una nuova. Per impostazione predefinita, le seguenti porte LDAP vengono utilizzate per l'accesso ad AD LDS:
    
      - **LDAP   **Porta 50389/TCP utilizzata localmente per il binding all'istanza AD LDS. Non è necessario che questa porta sia aperta nel firewall della rete perimetrale.
    
      - **LDAP protetto**   Porta 50636/TCP utilizzata per la sincronizzazione di directory dai server Cassette postali ad AD LDS. Questa porta deve essere aperta nel firewall per il completamento della sincronizzazione EdgeSync.

  - Verificare che la risoluzione del nome host DNS avvenga correttamente dal server Trasporto Edge ai server Cassette postali e dai server Cassette postali al server Trasporto Edge.

  - Assegnare la licenza al server Trasporto Edge. Le informazioni sulle licenze per il server Trasporto Edge vengono acquisite quando viene creata la sottoscrizione Edge. I server Trasporto Edge sottoscritti devono essere sottoscritti nell'organizzazione di Exchange dopo che la chiave di licenza è stata applicata al server Trasporto Edge. Se il codice di licenza viene applicato nel server Trasporto Edge dopo l'esecuzione del processo di sottoscrizione Edge, le informazioni sulla licenza non verranno aggiornate nell'organizzazione di Exchange. Sarà quindi necessario sottoscrivere nuovamente il server Trasporto Edge.

  - Per la propagazione al server Trasporto Edge, è necessario configurare le seguenti impostazioni di trasporto:
    
      - **Server SMTP interni**   Utilizzare il parametro *InternalSMTPServers* nel cmdlet **Set-TransportConfig** per specificare un elenco di indirizzi IP del server SMTP interno o intervalli di indirizzi IP che devono essere ignorati dall'ID mittente e dagli agenti filtro connessioni nel server Trasporto Edge.
    
      - **Domini accettati**   Configurare tutti i domini autorevoli, i domini di inoltro interno e i domini di inoltro esterno.
    
      - **Domini remoti**   Configurare le impostazioni dei domini remoti.

Inizio pagina

## Gestione delle sottoscrizioni Edge

Per istruzioni dettagliate sull'attività di gestione della sottoscrizione Edge, vedere [Gestione delle sottoscrizioni Edge](manage-edge-subscriptions-exchange-2013-help.md).


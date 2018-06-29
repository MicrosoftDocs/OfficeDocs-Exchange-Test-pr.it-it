---
title: 'Gestione dei gruppi di disponibilità del database: Exchange 2013 Help'
TOCTitle: Gestione dei gruppi di disponibilità del database
ms:assetid: 74be3f97-ec0f-4d2a-b5d8-7770cc489919
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298065(v=EXCHG.150)
ms:contentKeyID: 50480989
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione dei gruppi di disponibilità del database

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2017-10-04_

Un gruppo di disponibilità del database (DAG) è un insieme di 16 server Cassette postali Microsoft Exchange Server 2013 che fornisce il ripristino automatico a livello di database da un errore del database, del server o della rete. I DAG utilizzano la replica continua ed un sottogruppo di tecnologie clustering di failover di Windows per fornire un'elevata disponibilità e resilienza del sito. I server Cassette postali in un gruppo di disponibilità del database si controllano reciprocamente alla ricerca di errori. Quando un server Cassette postali viene aggiunto a un DAG, funziona con gli altri server del DAG per fornire il ripristino automatico da errori a livello di database.

Al momento della creazione, un DAG è vuoto. Quando si aggiunge il primo server a un DAG, per quel DAG viene creato automaticamente un cluster di failover. Inoltre, viene attivata l'infrastruttura che controlla i server per rilevare eventuali problemi della rete o dei server stessi. Il meccanismo heartbeat di cluster di failover e il database cluster sono poi utilizzati per tracciare e gestire le informazioni sul DAG che possono cambiare rapidamente, come lo stato di installazione del database, lo stato di replica e l'ultimo percorso d'installazione.

**Sommario**

Creating DAGs

DAG membership

Configuring DAG properties

DAG networks

Configuring DAG members

Performing maintenance on DAG members

Shutting down DAG members

Installing updates on DAG members

## Creazione di DAG

Un DAG può essere creato utilizzando la procedura guidata relativa alla creazione di un nuovo gruppo di disponibilità del database nell'interfaccia di amministrazione di Exchange (EMC) o eseguendo il cmdlet **New-DatabaseAvailabilityGroup** in Exchange Management Shell. Quando viene creato un DAG, è necessario specificare un nome per il DAG e una directory e un server di controllo facoltativi. Inoltre, è possibile assegnare uno o più indirizzi IP al DAG, utilizzando indirizzi IP statici o consentendo l'assegnazione automatica al DAG degli indirizzi IP necessari utilizzando il protocollo DHCP (Dynamic Host Configuration Protocol). È possibile assegnare manualmente indirizzi IP al DAG utilizzando il parametro *DatabaseAvailabilityGroupIpAddresses*. Se si omette questo parametro, il DAG tenta di ottenere un indirizzo IP utilizzando un server DHCP della rete.

Se è in corso la creazione di un DAG che contiene server di cassette postali che eseguono Windows Server 2012 R2, l'utente avrà la possibilità di creare un DAG senza un punto di accesso di un cluster amministrativo. In tale caso, il cluster non disporrà di un oggetto nome cluster (CNO) in Active Directory e il gruppo risorsa principale del cluster non conterrà una risorsa nome di rete o una risorsa indirizzo ID.

Per la procedura dettagliata relativa alla creazione di un DAG, vedere [Creare un gruppo di disponibilità del database](create-a-database-availability-group-exchange-2013-help.md).

Quando si crea un DAG, un oggetto vuoto che rappresenta il DAG con il nome specificato e la classe oggetto **msExchMDBAvailabilityGroup** viene creato in Active Directory.

I gruppi di disponibilità del database utilizzano la tecnologia di clustering di failover di Windows, ossia heartbeat cluster, reti cluster e database cluster (per l'archiviazione di dati che possono venire modificati rapidamente, ad esempio le modifiche di stato del database da attivo a passivo o viceversa, oppure da montato a smontato e viceversa). Poiché i gruppi di disponibilità del database si basano sulla tecnologia di clustering di failover di Windows, possono essere creati solo su server Cassette postali di Exchange 2013 che eseguono il sistema operativo Windows Server 2008 R2 Enterprise o Datacenter, il sistema operativo Windows Server 2012 Standard o Datacenter, il sistema operativo Windows Server 2012 R2 Standard o Datacenter.


> [!NOTE]
> Il cluster di failover creato e utilizzato dal DAG deve essere dedicato al DAG. Il cluster non può essere utilizzato per altre soluzioni a elevata disponibilità o per altri scopi. Ad esempio, il cluster di failover non può essere utilizzato per il cluster di altre applicazioni o servizi. L'uso di un cluster di failover del DAG specifico per scopi diversi dal DAG non è supportato.



## Server di controllo DAG e Directory di controllo

Quando si crea un DAG, è necessario specificare un nome per il DAG non più lungo di 15 caratteri e univoco all'interno della foresta di Active Directory. Inoltre, ciascun DAG viene configurato con un server e una directory di controllo. Il server di controllo e la directory relativa vengono utilizzati solo quando il gruppo di disponibilità del database contiene un numero pari di membri e quindi solo ai fini del quorum. Non è necessario creare la directory di controllo in anticipo. Exchange crea e protegge automaticamente la directory sul server di controllo. Questa directory deve essere utilizzata esclusivamente per il server di controllo del DAG.

I requisiti per il server di controllo sono i seguenti:

  - Il server di controllo non può essere un membro del DAG.

  - Il server di controllo deve essere nella stessa foresta di Active Directory del DAG.

  - Il server di controllo deve essere in esecuzione una versione supportata di Windows Server. Per ulteriori informazioni, vedere [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Un singolo server può essere utilizzato come server di controllo per più DAG. Tuttavia, ciascun DAG richiede la propria directory di controllo.

Indipendentemente dal server utilizzato come server di controllo, se è abilitato Windows Firewall sul server di controllo previsto, è necessario abilitare l'eccezione di Windows Firewall per Condivisione file e stampanti.


> [!IMPORTANT]
> Se il server di controllo specificato non è un server Exchange 2013 o Exchange&nbsp;2010, è necessario aggiungere il gruppo di protezione universale sottosistema Trusted Exchange (USG) al gruppo Administrators locale nel server di controllo prima di creare il DAG. Queste autorizzazioni di sicurezza sono necessarie per garantire che Exchange consente di creare una directory e condividere sul server di controllo in base alle esigenze.<BR>Il server di controllo utilizza la porta SMB 445.



Non è necessario che il server e la directory di controllo siano a prova di errore o che utilizzino altre forme di ridondanza o elevata disponibilità. Non è necessario utilizzare un file server in cluster per il server di controllo o impiegare qualunque altra forma di resilienza per il server di controllo. Ciò è dovuto a diversi motivi. Con DAG di dimensioni maggiori (ad esempio, con sei o più membri) devono verificarsi numerosi errori prima che sia necessario il server di controllo. Poiché un DAG con sei membri può tollerare fino a due errori del voter senza perdere il quorum, devono verificarsi almeno tre errori dei voter prima che sia necessario l'utilizzo del server di controllo per mantenere il quorum. Inoltre, se si verifica un errore che influisce sul server di controllo attuale (ad esempio, si perde il server di controllo a causa di un guasto hardware), è possibile utilizzare il cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\)) per configurare un nuovo server e una nuova directory di controllo (purché si disponga di un quorum).


> [!NOTE]
> È inoltre possibile utilizzare il cmdlet <STRONG>Set-DatabaseAvailabilityGroup</STRONG> per configurare il server e la directory di controllo nel percorso originario se il server di controllo ha perso i dati in archivio o se qualcuno ha modificato le autorizzazioni di condivisione o la directory di controllo.



## Considerazioni sulla collocazione dei server di controllo

La posizione del server di controllo del DAG dipende ai requisiti aziendali e le opzioni disponibili per l'organizzazione. Exchange 2013 include il supporto per nuove opzioni di configurazione di disponibilità del database che non sono consigliati o impossibili nelle versioni precedenti di Exchange. Queste opzioni includono l'utilizzo di una terza posizione, ad esempio un Data Center terzo, una succursale o una rete virtuale Microsoft Azure.

Nella tabella seguente sono elencate raccomandazioni generali sulla collocazione del server di controllo per diversi scenari di distribuzione.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Scenario di distribuzione</th>
<th>Raccomandazioni</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Singolo DAG distribuito in un singolo datacenter</p></td>
<td><p>Collocare il server di controllo nello stesso datacenter dei membri del DAG</p></td>
</tr>
<tr class="even">
<td><p>Singolo DAG distribuito tra due datacenter, senza ulteriori posizioni disponibili</p></td>
<td><p>Individuare il server di controllo in una rete virtuale Microsoft Azure per abilitare il failover automatico datacenter o</p>
<p>Collocare il server di controllo nel datacenter principale</p></td>
</tr>
<tr class="odd">
<td><p>Più DAG distribuiti in un singolo datacenter</p></td>
<td><p>Collocare il server di controllo nello stesso datacenter dei membri del DAG. Altre opzioni sono:</p>
<ul>
<li><p>Utilizzo dello stesso server di controllo per più DAG</p></li>
<li><p>Utilizzo di un membro del DAG come server di controllo di un altro DAG</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>Più DAG distribuiti tra due datacenter</p></td>
<td><p>Individuare il server di controllo in una rete virtuale Microsoft Azure per abilitare il failover automatico datacenter o</p>
<p>Collocare il server di controllo nel datacenter considerato principale per ciascun DAG. Altre opzioni sono:</p>
<ul>
<li><p>Utilizzo dello stesso server di controllo per più DAG</p></li>
<li><p>Utilizzo di un membro del DAG come server di controllo di un altro DAG</p>
<p></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Singolo DAG o più DAG distribuiti tra più di due datacenter</p></td>
<td><p>In questa configurazione, il server di controllo deve essere collocato nel datacenter in cui deve risiedere la maggior parte dei voti del quorum.</p></td>
</tr>
</tbody>
</table>


Quando un gruppo DAG è stato distribuito tra due datacenter, una nuova opzione di configurazione in Exchange 2013 consiste nell'utilizzare una terza posizione per ospitare il server di controllo. Se l'organizzazione dispone di una posizione terza con un'infrastruttura di rete isolata dagli errori di rete che influiscono due datacenter in cui viene distribuito il DAG, quindi è possibile distribuire il server di controllo del DAG in tale posizione terzo, in tal modo la configurazione del DAG con la possibilità automaticamente il failover database su altri Data Center in risposta a un evento di errore di livello Data Center. Se l'organizzazione dispone solo di due posizioni fisiche, è possibile utilizzare una rete virtuale Microsoft Azure come percorso terzo posizionare i server di controllo.

## Indicazione di un server e di una directory di controllo durante la creazione di un DAG

Quando si crea un DAG, è necessario specificare un nome per il DAG. Opzionalmente, è anche possibile specificare un server e una directory di controllo.

Quando si crea un DAG, sono disponibili le seguenti combinazioni di opzioni e comportamenti:

  - È possibile specificare solo un nome per il DAG e lasciare i campi **Server di controllo** e **Directory di controllo** vuoti. In questo scenario, la procedura guidata cerca nel sito Active Directory locale un server Accesso client in cui non è installato il server Cassette postali e crea automaticamente la directory predefinita (%SystemDrive%:\\DAGFileShareWitnesses\\\<*DAGFQDN*\>) e la condivisione predefinita (\<*DAGFQDN*\>) su tale server, che verrà utilizzato come server di controllo. Ad esempio, considerare un server di controllo denominato CAS3 in cui il sistema operativo è stato installato sull'unità C. Un DAG denominato DAG1 nel dominio contoso.com utilizzerebbe la directory di controllo predefinita C:\\DAGFileShareWitnesses\\DAG1.contoso.com, che verrebbe condivisa come \\\\CAS3\\DAG1.contoso.com.

  - È possibile specificare un nome per il DAG, il server di controllo che si desidera utilizzare e la directory che si desidera creare e condividere sul server di controllo.

  - È possibile specificare un nome per il DAG, il server di controllo che si desidera utilizzare e lasciare il campo **Directory di controllo** vuoto. In questo scenario, la procedura guidata crea la directory predefinita sul server di controllo specificato.

  - È possibile specificare un nome per il DAG, lasciare il campo **Server di controllo** vuoto e specificare la directory che si desidera creare e condividere sul server di controllo. In questo scenario, la procedura guidata ricerca un server Accesso client su cui non è installato il ruolo del server Cassette postali e crea automaticamente il DAG specificato su quel server, condivide la directory e utilizza il server Accesso client come server di controllo.

Quando viene costituito un DAG, questo utilizza inizialmente il modello di quorum Maggioranza dei nodi. Quando il secondo server Cassette postali viene aggiunto al DAG, il modello di quorum viene automaticamente modificato in Maggioranza dei nodi e delle condivisioni file. Con questa modifica, il cluster DAG inizia a utilizzare il server di controllo per il mantenimento di un quorum. Se la directory di controllo non esiste, Exchange la crea automaticamente, la condivide e fornisce le autorizzazioni di controllo completo per l'account sul computer dell'oggetto di rete cluster (CNO) del DAG.


> [!NOTE]
> L'utilizzo di una condivisione file che è parte di uno spazio dei nomi DFS (Distributed File System) non è supportato.



Se Windows Firewall risulta abilitato sul server di controllo prima che venga creato il DAG, ciò potrebbe bloccare la creazione del DAG. Exchange utilizza Strumentazione gestione Windows (WMI) per creare la condivisione file e la directory sul server di controllo. Se Windows Firewall è abilitato sul server di controllo e non esistono eccezioni firewall configurate per WMI, il cmdlet **New-DatabaseAvailabilityGroup** restituirà un errore. Se si specifica un server di controllo ma non una directory di controllo, viene visualizzato il seguente messaggio di errore.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Non è stato possibile creare la directory di controllo predefinita sul server &lt;<em>Nome Server</em>&gt;. Specificare manualmente una directory di controllo.</p></td>
</tr>
</tbody>
</table>


Se si specifica un server di controllo e una directory di controllo, viene visualizzato il seguente messaggio di avviso.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Impossibile accedere alle condivisioni file sul server di controllo '<em>NomeServer</em>'. Finché il problema non viene risolto, il gruppo di disponibilità del database potrebbe essere più vulnerabile agli errori. È possibile utilizzare il cmdlet Set-DatabaseAvailabilityGroup per ripetere l'operazione. Errore: Impossibile trovare il percorso di rete.</p></td>
</tr>
</tbody>
</table>


Se Windows Firewall viene abilitato sul server di controllo dopo la creazione del DAG ma prima dell'aggiunta dei server, ciò potrebbe bloccare l'aggiunta o la rimozione dei membri del DAG. Se Windows Firewall è abilitato sul server di controllo e non esistono eccezioni firewall configurate per WMI, il cmdlet **Add-DatabaseAvailabilityGroupServer** visualizza il seguente messaggio di errore.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Impossibile creare la directory di controllo di condivisione dei file 'C:\DAGFileShareWitnesses\DAG_FQDN' sul server di controllo <em>'NomeServer'</em>. Finché il problema non viene risolto, il gruppo di disponibilità del database potrebbe essere più vulnerabile agli errori. È possibile utilizzare il cmdlet Set-DatabaseAvailabilityGroup per ripetere l'operazione. Errore: Eccezione WMI nel server <em>'NomeServer'</em>: Il server RPC non è disponibile. (Eccezione da HRESULT: 0x800706BA)</p></td>
</tr>
</tbody>
</table>


Per correggere l'errore precedente e i problemi riscontrati dagli avvisi, fare quanto segue:

  - Creare manualmente la directory di controllo, condividerla sul server di controllo e assegnare l'oggetto nome cluster per il controllo totale del DAG relativamente alla directory e alla condivisione.

  - Abilitare l'eccezione WMI in Windows Firewall.

  - Disabilitare Windows Firewall.

Inizio pagina

## Appartenenza al DAG

Una volta creato un DAG, è possibile aggiungere o rimuovere i server dal DAG utilizzando la procedura guidata relativa alla gestione del gruppo di disponibilità del database nell'interfaccia di amministrazione di Exchange o utilizzando il cmdlet **Add-DatabaseAvailabilityGroupServer** o **Remove-DatabaseAvailabilityGroupServer** nella Shell. Per la procedura dettagliata sulla gestione dell'appartenenza al DAG, vedere [Gestire l'appartenenza al gruppo di disponibilità del database](manage-database-availability-group-membership-exchange-2013-help.md).


> [!NOTE]
> Ogni server Cassette postali che è membro di un DAG è anche un nodo del cluster sottostante utilizzato dal DAG. Di conseguenza, in qualsiasi momento, un server Cassette postali può essere membro di un solo DAG.



Se sul server Cassette postali aggiunto a un DAG non è installato il componente di clustering di failover, il metodo utilizzato per aggiungere il server (ad esempio, il cmdlet **Add-DatabaseAvailabilityGroupServer** o la procedura guidata relativa alla gestione del gruppo di disponibilità del database) installerà la funzionalità di clustering di failover.

Quando il primo server Cassette postali viene aggiunto a un DAG, si verifica quanto segue:

  - Se non è già installato, viene installato il componente clustering di failover di Windows.

  - Viene creato un cluster di failover utilizzando il nome del DAG. Il cluster di failover viene utilizzato esclusivamente dal DAG e il cluster deve essere dedicato al DAG. L'utilizzo del cluster non è supportato per tutti gli scopi.

  - Un oggetto nome cluster viene creato nel contenitore di computer predefinito.

  - Il nome e l'indirizzo IP del DAG vengono registrati come record Host (A) nel DNS (Domain Name System).

  - Il server viene aggiunto all'oggetto DAG in Active Directory.

  - Il database del cluster viene aggiornato con le informazioni sui database installati sul server aggiunto.

In ambienti di dimensioni notevoli o con più siti, specialmente in quelli in cui il DAG viene esteso su più siti di Active Directory, è necessario attendere che venga completata la replica Active Directory dell'oggetto DAG contenente il primo membro del DAG. Se questo oggetto Active Directory non viene replicato nell'ambiente, aggiungendo il secondo server è possibile che venga creato un nuovo cluster e un nuovo oggetto di rete cluster per il DAG. Ciò avviene in quanto l'oggetto DAG appare vuoto dal punto di vista del secondo membro aggiunto. Di conseguenza, il cmdlet **Add-DatabaseAvailabilityGroupServer** creerà un cluster e un oggetto nome cluster per il DAG, anche se questi oggetti già esistono. Per verificare che l'oggetto DAG contenente il primo server DAG sia stato replicato, utilizzare il cmdlet **Get-DatabaseAvailabilityGroup** sul secondo server aggiunto per verificare che il primo server aggiunto sia elencato come membro del DAG.

Quando il secondo e i successivi server vengono aggiunti al DAG, si verifica quanto segue:

  - Il server viene aggiunto al cluster di failover di Windows per il DAG.

  - Il modello di quorum viene adattato automaticamente:
    
      - Il modello di quorum Maggioranza dei nodi viene utilizzato per i DAG contenenti un numero dispari di membri.
    
      - Il modello di quorum Maggioranza dei nodi e delle condivisioni di file viene utilizzato per i DAG contenenti un numero pari di membri.

  - La directory di controllo e la condivisione vengono create automaticamente da Exchange quando necessario.

  - Il server viene aggiunto all'oggetto DAG in Active Directory.

  - Il database del cluster viene aggiornato con le informazioni sui database installati.


> [!NOTE]
> La modifica del modello di quorum deve avvenire automaticamente. Tuttavia, se la modifica del modello di quorum non avviene automaticamente, è possibile eseguire il cmdlet <STRONG>Set-DatabaseAvailabilityGroup</STRONG> con il solo parametro <EM>Identity</EM> per correggere le impostazioni del quorum per il DAG.



## Pregestione dell'oggetto nome cluster per un DAG

Il CNO è un account del computer creato in Active Directory e associato alla risorsa Nome del cluster. La risorsa del nome cluster è collegata all'oggetto di rete cluster, un oggetto abilitato per Kerberos che funge da identità del cluster e fornisce il contesto di sicurezza del cluster. La creazione del cluster sottostante al DAG e del CNO per quel cluster viene eseguita quando il primo membro viene aggiunto al DAG. Quando il primo server viene aggiunto al DAG, Remote Powershell contatta il servizio di replica di Microsoft Exchange sul server Cassette postali che viene aggiunto. Il servizio di replica di Microsoft Exchange installa la funzionalità di clustering di failover (se non è già installata) e avvia il processo di creazione del cluster. Il servizio di replica di Microsoft Exchange viene eseguito nel contesto di sicurezza LOCAL SYSTEM ed è in questo contesto che viene eseguita la creazione del cluster.


> [!WARNING]
> Se i membri del DAG eseguono Windows Server 2012, è necessario pregestire l'oggetto di rete cluster (CNO) prima di aggiungere il primo server al DAG. Se i membri di DAG eseguono Windows Server 2012 R2 e il DAG viene creato senza un indirizzo IP o un punto di accesso amministrativo del cluster, non viene creato un oggetto CNO e l'utente non deve creare un oggetto CNO per il DAG.



In ambienti in cui la creazione degli account computer è limitata o in cui gli account computer vengono creati in un contenitore diverso da quello predefinito dei computer, è possibile pregestire ed eseguire il provisioning dell'oggetto di rete cluster. Creare e disabilitare un account computer per il CNO, quindi:

  - Assegnare il controllo completo dell'account computer all'account computer del primo server Cassette postali aggiunto al DAG.

  - Assegnare il controllo completo dell'account computer al gruppo di protezione universale Exchange Trusted Subsystem.

L'assegnazione del controllo completo dell'account computer all'account computer del primo server Cassette postali aggiunto al DAG fa sì che il contesto di sicurezza LOCAL SYSTEM sia in grado di gestire l'account computer pregestito. Invece, è possibile utilizzare l'assegnazione del controllo completo dell'account computer al gruppo di protezione universale Exchange Trusted Subsystem in quanto tale gruppo Exchange Trusted Subsystem contiene gli account computer di tutti i server Exchange nel dominio.

Per la procedura dettagliata relativa alla pregestione e al provisioning dell'oggetto di rete cluster per un DAG, vedere [Pregestione dell'oggetto nome cluster per un gruppo di disponibilità del database](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

## Rimozioni di server da un DAG

I server Cassette postali possono essere rimossi da un DAG utilizzando la procedura guidata relativa alla gestione del gruppo di disponibilità del database nell'interfaccia di amministrazione di Exchange o il cmdlet **Remove-DatabaseAvailabilityGroupServer** nella Shell. Prima di rimuovere un server Cassette postali da un DAG, tutti i database delle cassette postali replicati devono prima essere rimossi dal server. Se si tenta di rimuovere un server Cassette postali con i database delle cassette postali replicati da un DAG, l'operazione non viene completata.

Ci sono alcuni scenari in cui è necessario rimuovere un server Cassette postali da un DAG prima di eseguire determinate operazioni. Tra questi scenari sono compresi:

  - **Esecuzione di un'operazione di ripristino del server**   Se un server Cassette postali che è un membro di un DAG viene perso o non può essere in altro modo ripristinato a seguito di errore e deve quindi essere sostituito, è possibile eseguire un'operazione di ripristino del server utilizzando l'opzione **Setup /m:RecoverServer**. Tuttavia, prima di eseguire l'operazione di ripristino, è necessario rimuovere il server dal DAG utilizzando il cmdlet [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/it-it/library/dd297956\(v=exchg.150\)) con il parametro *ConfigurationOnly*.

  - **Rimozione del gruppo di disponibilità del database**   Ci possono essere situazioni in cui è necessario rimuovere un DAG (ad esempio, quando si disabilita la modalità di replica di terze parti). Per rimuovere un DAG, occorre prima rimuovere tutti i server dal DAG. Se si tenta di rimuovere un DAG contenente uno o più membri, l'operazione non viene completata.

Inizio pagina

## Configurazione delle proprietà del DAG

Dopo aver aggiunto i server al DAG, è possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell per configurare le proprietà di un DAG, compresi il server e la directory di controllo utilizzati dal DAG e gli indirizzi IP ad esso assegnati.

Le proprietà configurabili comprendono:

  - **Server di controllo**   Il nome del server che si desidera ospiti la condivisione dei file per il server di controllo della condivisione file. Si raccomanda di specificare un server Accesso client come server di controllo. Si consente così al sistema di configurare, rendere sicura e usare la condivisione in modo automatico e si consente all'amministratore della messaggistica di essere al corrente della disponibilità del server di controllo.

  - **Directory di controllo**   Il nome di una directory da utilizzare per archiviare i dati di controllo della condivisione file. La directory verrà automaticamente creata dal sistema sul server di controllo specificato.

  - **Indirizzi IP del gruppo di disponibilità del database**   Uno o più indirizzi IP da assegnare al DAG, a meno che i membri del DAG eseguano Windows Server 2012 R2 e sia in fase di creazione un DAG senza indirizzo IP. In alternativa, gli indirizzi IP del DAG possono essere configurati utilizzando gli indirizzi IP statici assegnati manualmente o possono essere assegnati automaticamente al DAG utilizzando un server DHCP nell'organizzazione.

La Shell consente di configurare le proprietà del DAG non disponibili nell'interfaccia di amministrazione di Exchange, quali gli indirizzi IP, le impostazioni di crittografia e compressione di rete, l'individuazione della rete, la porta TCP utilizzata per la replica e le impostazioni per un server di controllo e una directory di controllo alternativi, nonché di abilitare la modalità di coordinamento dell'attivazione del datacenter.

Per la procedura dettagliata sulla configurazione delle proprietà del DAG, vedere [Configurazione delle proprietà del gruppo di disponibilità del database](configure-database-availability-group-properties-exchange-2013-help.md).

## Crittografia di rete del DAG

DAG supporta l'utilizzo della crittografia sfruttando le funzionalità di crittografia del sistema operativo Windows Server. DAG utilizzata l'autenticazione Kerberos tra i server Exchange. Microsoft Kerberos supporto provider (provider di servizi condivisi) EncryptMessage e DecryptMessage APIs punto di manipolazione di crittografia di protezione del traffico di rete del DAG. Microsoft Kerberos SSP supporta più gli algoritmi di crittografia. (Per l'elenco completo, vedere sezione 3.1.5.2, "Tipi di crittografia" delle [Estensioni del protocollo Kerberos](https://go.microsoft.com/fwlink/p/?linkid=179131)). L'handshake di autenticazione Kerberos seleziona il protocollo più sicuro di crittografia supportato nell'elenco: in genere la crittografia AES (Advanced Standard) 256 bit, potenzialmente con un Hash SHA HMAC-based Message Authentication codice () per mantenere l'integrità del dati. Per ulteriori informazioni, vedere [HMAC](https://en.wikipedia.org/wiki/hmac).

La crittografia di rete è una proprietà del DAG e non di una rete del DAG. È possibile configurare la crittografia di rete del DAG utilizzando il cmdlet **Set-DatabaseAvailabilityGroup** in Shell. Le possibili impostazioni di crittografia per le comunicazioni di rete del DAG sono elencate nella seguente tabella.

### Impostazioni di crittografia per le comunicazioni di rete del DAG

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Disabilitata</p></td>
<td><p>Non viene utilizzata la crittografia di rete.</p></td>
</tr>
<tr class="even">
<td><p>Abilitata</p></td>
<td><p>La crittografia di rete viene utilizzata per la replica e il seeding su tutte le reti del DAG.</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>Viene utilizzata la crittografia di rete sulle reti del DAG durante la replica su differenti subnet. Questa impostazione è quella predefinita.</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>Viene utilizzata la crittografia di rete su tutte le reti DAG solo per il seeding.</p></td>
</tr>
</tbody>
</table>


## Compressione di rete del DAG

DAG supporta la compressione incorporata. Quando viene attivata la compressione, le comunicazioni di rete del DAG utilizza XPRESS, ovvero l'implementazione Microsoft di algoritmo LZ77. Per ulteriori informazioni, vedere sezione 3.1.4.11.1.2.1 e [Una spiegazione dell'algoritmo concavo](http://www.zlib.net/feldspar.html) "Algoritmo di compressione LZ77" di [Specifiche del protocollo formato cablato](https://go.microsoft.com/fwlink/p/?linkid=179133). Questo è lo stesso tipo di compressione utilizzate in molti protocolli Microsoft, in particolare, compressione MAPI RPC tra Microsoft Outlook e Exchange.

Come nel caso della crittografia di rete, la compressione della rete è anche una proprietà del DAG e non di una rete del DAG. È possibile configurare la compressione di rete del DAG utilizzando il cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\)) in Shell. Le possibili impostazioni di compressione per le comunicazioni di rete del DAG sono elencate nella seguente tabella.

### Impostazioni di compressione per le comunicazioni di rete del DAG

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Disabilitato</p></td>
<td><p>Non viene utilizzata la compressione di rete.</p></td>
</tr>
<tr class="even">
<td><p>Enabled</p></td>
<td><p>La compressione di rete viene utilizzata per la replica e il seeding su tutte le reti del DAG.</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>Viene utilizzata la compressione di rete sulle reti del DAG durante la replica su differenti subnet. Questa impostazione è quella predefinita.</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>Viene utilizzata la compressione di rete su tutte le reti del DAG solo per il seeding.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Reti del DAG

Una rete DAG è un insieme di uno o più subnet utilizzato per il traffico di replica o del traffico MAPI. Ogni DAG contiene un massimo di una rete MAPI e zero o più reti di replica.

## Configurazioni delle schede di rete singola

Nelle configurazioni delle schede di rete singola, alla stessa rete viene utilizzata per il traffico di replica e MAPI. Per ridurre la complessità, una singola scheda di rete è la configurazione consigliata per i server Exchange, pertanto è possibile disporre di traffico di replica e MAPI sulla stessa rete.

## Configurazioni delle schede di rete doppia

In genere, è sufficiente utilizzare due schede di rete in cui il traffico di rete aumento ha la possibilità per saturare una singola scheda di rete.

Nelle configurazioni delle schede di rete doppia, una rete è in genere dedicata per il traffico di replica e l'altra rete viene utilizzata principalmente per il traffico MAPI. È inoltre possibile aggiungere schede di rete a ciascun membro del DAG e configurare reti DAG aggiuntive come reti di replica.


> [!NOTE]
> Quando si utilizzano più reti di replica, non è possibile specificare un ordine di precedenza per l'utilizzo della rete. Exchange seleziona a caso una rete di replica dal gruppo delle reti di replica da utilizzare per l'invio dei registri.



In Exchange 2010, la configurazione manuale della rete DAG era necessaria in molti scenari. Per impostazione predefinita in Exchange 2013, le reti DAG vengono configurate automaticamente dal sistema. Prima di poter creare o modificare reti DAG, è necessario abilitare il controllo manuale della rete DAG utilizzando i seguenti comandi:

    Set-DatabaseAvailabilityGroup <DAGName> -ManualDagNetworkConfiguration $true

Una volta abilitata la configurazione manuale della rete DAG, è possibile utilizzare il cmdlet **New-DatabaseAvailabilityGroupNetwork** nella Shell per creare una rete DAG. Per la procedura dettagliata sulla creazione di una rete DAG, vedere [Creare una rete di gruppo di disponibilità del database](create-a-database-availability-group-network-exchange-2013-help.md).

È possibile utilizzare il cmdlet **Set-DatabaseAvailabilityGroupNetwork** nella Shell per configurare le proprietà di rete DAG. Per la procedura dettagliata sulla configurazione delle proprietà della rete DAG, vedere [Configurazione delle proprietà rete gruppo di disponibilità del database](configure-database-availability-group-network-properties-exchange-2013-help.md). Ciascuna rete del DAG prevede dei parametri obbligatori e facoltativi per configurare quanto segue:

  - **Nome rete**   Un nome univoco per la rete del DAG con un massimo di 128 caratteri.

  - **Descrizione rete**   Una descrizione facoltativa per la rete del DAG con un massimo di 256 caratteri.

  - **Subnet di rete**   Una o più subnet specificate utilizzando il formato *IndirizzoIP/Maschera di bit* (ad esempio, 192.168.1.0/24 per le subnet IPv4; 2001:DB8:0:C000::/64 per le subnet IPv6).

  - **Abilita replica**   Nell'interfaccia di amministrazione di Exchange, selezionare la casella di controllo per dedicare la rete DAG al traffico di replica e bloccare il traffico MAPI. Deselezionare la casella di controllo per impedire alla replica di utilizzare la rete del DAG e abilitare il traffico MAPI. In Shell, utilizzare il parametro *ReplicationEnabled* nel cmdlet [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/it-it/library/dd298008\(v=exchg.150\)) per abilitare o disabilitare la replica.


> [!NOTE]
> La disattivazione della replica per la rete MAPI non garantisce in assoluto che il sistema non utilizzerà la rete MAPI per la replica. Quando tutte le reti di replica configurate risultano offline, non riuscite o non disponibili e rimane solo la rete MAPI (configurata come disabilitata per la replica), il sistema utilizza la rete MAPI per la replica.



Le reti DAG iniziali (ad esempio, MapiDagNetwork e ReplicationDagNetwork01) create dal sistema sono basate su sottoreti enumerate dal servizio Cluster. Ciascun membro DAG deve avere lo stesso numero di schede di rete e ciascuna scheda di rete deve disporre di un indirizzo IPv4 (e, opzionalmente, anche di un indirizzo IPv6) su una subnet univoca. Più membri DAG possono disporre di indirizzi IPv4 sulla stessa subnet, ma ciascuna scheda di rete e una coppia di indirizzi IP in un determinato membro DAG devono trovarsi su una subnet univoca. Inoltre, solo la scheda utilizzate per la rete MAPI deve essere configurata con un gateway predefinito. Le reti di replica non devono essere configurate con un gateway predefinito.

Ad esempio, considerare DAG1, un DAG con due membri in cui ciascun membro dispone di due schede di rete (una dedicata alla rete MAPI e l'altra alla rete di replica). Nella tabella seguente, sono riportati esempi di impostazioni di configurazioni di indirizzi IP.

### Esempi di impostazioni delle schede di rete

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Server-scheda di rete</th>
<th>Indirizzo IP/subnet mask</th>
<th>Gateway predefinito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1-MAPI</p></td>
<td><p>192.168.1.15/24</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX1-Replica</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>EX2-MAPI</p></td>
<td><p>192.168.1.16</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX2-Replica</p></td>
<td><p>10.0.0.16</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


Nella seguente configurazione, sono disponibili due subnet configurate nel DAG: 192.168.1.0 e 10.0.0.0. Quando EX1 ed EX2 vengono aggiunte al DAG, verranno enumerate due subnet e verranno create due reti DAG: MapiDagNetwork (192.168.1.0) e ReplicationDagNetwork01 (10.0.0.0). Tali reti verranno configurate come indicata nella tabella seguente.

### Impostazioni reti DAG enumerate per un DAG con una singola subnet

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Subnet</th>
<th>Interfacce</th>
<th>Accesso MAPI abilitato</th>
<th>Replica abilitata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.1.0/24</p></td>
<td><p>EX1 (192.168.1.15)</p>
<p>EX2 (192.168.1.16)</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p></td>
<td><p>EX1 (10.0.0.15)</p>
<p>EX2 (10.0.0.16)</p></td>
<td><p>False</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


Per completare la configurazione di ReplicationDagNetwork01 come rete di replica dedicata, disabilitare la replica per MapiDagNetwork utilizzando il seguente comando.

    Set-DatabaseAvailabilityGroupNetwork -Identity DAG1\MapiDagNetwork -ReplicationEnabled:$false

Dopo aver disabilitato la replica per MapiDagNetwork, il servizio replica Microsoft Exchange utilizza ReplicationDagNetwork01 per la replica continua. Se si verifica un errore in ReplicationDagNetwork01, il servizio Replica di Microsoft Exchange torna ad utilizzare MapiDagNetwork per la replica continua. Tale operazione viene eseguita intenzionalmente dal sistema al fine di mantenere una disponibilità elevata.

## Reti DAG e distribuzioni di più subnet

Nell'esempio precedente, anche se il DAG utilizza due subnet differenti DAG (192.168.1.0 e 10.0.0.0), il DAG viene considerato un DAG con una singola subnet, in quanto ciascun membro utilizza la stessa subnet per creare la rete MAPI. Quando i membri del DAG utilizzano subnet differenti per la rete MAPI, il DAG viene considerato come un *DAG a più subnet*. In un gruppo di disponibilità con più subnet, le appropriate subnet vengono associate automaticamente con ciascuna rete DAG.

Ad esempio, considerare DAG2, un DAG con due membri in cui ciascun membro dispone di due schede di rete (una dedicata alla rete MAPI e l'altra alla rete di replica) e ciascun membro del DAG si trova in un sito Active Directory distinto, con la relativa rete MAPI su una subnet differente. Nella tabella seguente, sono riportati esempi di impostazioni di configurazioni di indirizzi IP.

### Esempio di impostazioni di schede di rete per un DAG a più subnet

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Server-scheda di rete</th>
<th>Indirizzo IP/subnet mask</th>
<th>Gateway predefinito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1-MAPI</p></td>
<td><p>192.168.0.15/24</p></td>
<td><p>192.168.0.1</p></td>
</tr>
<tr class="even">
<td><p>EX1-Replica</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>EX2-MAPI</p></td>
<td><p>192.168.1.15</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX2-Replica</p></td>
<td><p>10.0.1.15</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


Nella seguente configurazione, sono disponibili quattro subnet configurate nel DAG: 192.168.0.0, 192.168.1.0, 10.0.0.0 e 10.0.1.0. Quando EX1 ed EX2 vengono aggiunte al gruppo di disponibilità, verranno enumerate quattro subnet e verranno create due reti DAG: MapiDagNetwork (192.168.0.0, 192.168.1.0) e ReplicationDagNetwork01 (10.0.0.0, 10.0.1.0). Tali reti verranno configurate come indicata nella tabella seguente.

### Impostazioni reti DAG enumerate per un DAG a più subnet

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Subnet</th>
<th>Interfacce</th>
<th>Accesso MAPI abilitato</th>
<th>Replica abilitata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.0.0/24</p>
<p>192.168.1.0/24</p></td>
<td><p>EX1 (192.168.0.15)</p>
<p>EX2 (192.168.1.15)</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p>
<p>10.0.1.0/24</p></td>
<td><p>EX1 (10.0.0.15)</p>
<p>EX2 (10.0.1.15)</p></td>
<td><p>False</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


## Reti DAG e reti iSCSI

Per impostazione predefinita, i DAG eseguono l'individuazione di tutte le reti rilevate e configurate per l'utilizzo da parte del cluster sottostante. Ciò include qualsiasi rete Internet SCSI (iSCSI) in uso a seguito dell'utilizzo dell'archiviazione iSCSI per uno o più membri del DAG. Secondo la procedura consigliata, l'archiviazione iSCSI deve utilizzare reti e schede di rete dedicate. Queste reti non devono essere gestite dal DAG o dal suo cluster oppure utilizzate come reti del DAG (MAPI o di replica). Al contrario, il loro utilizzo da parte del DAG deve essere disabilitato manualmente, in modo che possano essere dedicate al traffico dell'archiviazione iSCSI. Per disabilitare il rilevamento e l'utilizzo di reti iSCSI come reti DAG, configurare il gruppo di disponibilità per ignorare qualsiasi rete iSCSI attualmente rilevata utilizzando il cmdlet [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/it-it/library/dd298008\(v=exchg.150\)), come mostrato in questo esempio:

    Set-DatabaseAvailabilityGroupNetwork -Identity DAG2\DAGNetwork02 -ReplicationEnabled:$false -IgnoreNetwork:$true

Questo comando disabiliterà la rete anche per l'utilizzo da parte del cluster. Sebbene le reti iSCSI continueranno ad apparire come reti DAG, non verranno utilizzate per MAPI o traffico di replica dopo l'esecuzione del comando precedente.

Inizio pagina

## Configurazione di membri del DAG

I server Cassette postali che sono membri di un DAG dispongono di proprietà specifiche per una disponibilità elevata che dovrebbero essere configurate come descritto nelle seguenti sezioni:

  - Automatic database mount dial

  - Database copy automatic activation policy

  - Maximum active databases

## Dial di montaggio automatico del database

Il parametro *AutoDatabaseMountDial* indica il comportamento per l'installazione automatica del database dopo un failover del database. È possibile utilizzare il cmdlet [Set-MailboxServer](https://technet.microsoft.com/it-it/library/aa998651\(v=exchg.150\)) per configurare il parametro *AutoDatabaseMountDial* con uno qualsiasi dei seguenti valori:

  - `BestAvailability`   Se si specifica questo valore, il database viene installato automaticamente subito dopo il failover, se la lunghezza della coda delle copie è minore o uguale a 12. La lunghezza della coda delle copie indica il numero di registri riconosciuti dalla copia passiva che è necessario replicare. Se la lunghezza della coda delle copie è maggiore di 12, il database non viene installato automaticamente. Quando la lunghezza della coda delle copie è minore o uguale a 12, Exchange tenta di replicare i registri rimanenti sulla copia passiva e installa il database.

  - `GoodAvailability`   Se si specifica questo valore, il database viene installato automaticamente dopo il failover, se la lunghezza della coda delle copie è minore o uguale a sei. La lunghezza della coda delle copie indica il numero di registri riconosciuti dalla copia passiva che è necessario replicare. Se la lunghezza della coda delle copie è maggiore di sei, il database non viene installato automaticamente. Quando la lunghezza della coda delle copie è minore o uguale a sei, Exchange tenta di replicare i registri rimanenti sulla copia passiva e installa il database.

  - `Lossless`   Se si specifica questo valore, il database non viene installato automaticamente fino a quando tutti i registri generati sulla copia attiva non sono stati copiati sulla copia passiva. Inoltre, tale impostazione fa sì che l'algoritmo di selezione delle copie migliori ordini potenziali candidati per l'attivazione in base al valore di preferenza dell'attivazione della copia del database e non alla lunghezza della relativa coda delle copie.

Il valore predefinito è `GoodAvailability`. Se si specifica `BestAvailability` o `GoodAvailability` e non sono stati replicati sulla copia passiva tutti i registri della copia attiva, si rischia di perdere dei dati delle cassette postali. Tuttavia, la funzionalità Rete sicura (abilitata per impostazione predefinita) è un valido aiuto contro la perdita dei dati perché reinvia i messaggi che si trovano nella coda di Rete sicura.

## Esempio: configurazione del dial di montaggio automatico del database

Il seguente esempio configura un server Cassette postali con un'impostazione *AutoDatabaseMountDial* di `GoodAvailability`.

    Set-MailboxServer -Identity EX1 -AutoDatabaseMountDial GoodAvailability

## Criterio di attivazione automatica della copia del database

Il parametro *DatabaseCopyAutoActivationPolicy* consente di specificare il tipo di attivazione automatica disponibile per le copie del database delle cassette postali sui server Cassette postali selezionati. È possibile utilizzare il cmdlet [Set-MailboxServer](https://technet.microsoft.com/it-it/library/aa998651\(v=exchg.150\)) per configurare il parametro *DatabaseCopyAutoActivationPolicy* con uno qualsiasi dei seguenti valori:

  - `Blocked`   Se si specifica questo valore, non è possibile attivare automaticamente i database sui server Cassette postali selezionati.

  - `IntrasiteOnly`   Se si specifica questo valore, è possibile attivare la copia del database sui server dello stesso sito Active Directory. In questo modo si evita l'attivazione o il failover tra siti. Questa proprietà vale per le copie del database delle cassette postali in arrivo (ad esempio, una copia passiva che viene resa attiva). I database non possono essere attivati su questo server Cassette postali per le copie del database che sono attive in un altro sito Active Directory.

  - `Unrestricted`   Se si specifica questo valore, non sono presenti limitazioni particolari per quanto riguarda l'attivazione delle copie del database delle cassette postali sui server Cassette postali selezionati.

## Esempio: configurazione del criterio di attivazione automatica della copia del database

Nel seguente esempio, viene configurato un server Cassette postali con un'impostazione *DatabaseCopyAutoActivationPolicy* di `Blocked`.

    Set-MailboxServer -Identity EX1 -DatabaseCopyAutoActivationPolicy Blocked

## Numero massimo di database attivi

Il parametro *MaximumActiveDatabases* (utilizzato anche con il cmdlet [Set-MailboxServer](https://technet.microsoft.com/it-it/library/aa998651\(v=exchg.150\))) indica il numero di database che possono essere installati su un server Cassette postali. È possibile configurare i server Cassette postali per soddisfare i requisiti di distribuzione accertandosi di non sovraccaricare il server Cassette postali.

Il parametro *MaximumActiveDatabases*viene configurato con un valore numerico intero. Una volta raggiunto il valore massimo, le copie del database sul server non vengono attivate se si verifica un failover o un passaggio. Se le copie sono già attivate sul server, questo non consente l'installazione dei database.

## Esempio: Configurazione del numero massimo di database attivi

Nell'esempio seguente viene configurato un server Cassette postali per supportare un massimo di 20 database attivi.

    Set-MailboxServer -Identity EX1 -MaximumActiveDatabases 20

Inizio pagina

## Esecuzione della manutenzione sui membri del DAG

Prima di eseguire interventi di manutenzione software o hardware su un membro del DAG, è necessario collocare il membro del DAG in modalità manutenzione. A tale scopo è necessario rimuovere tutti i database attivi dal server e impedire ai database di passare sul server. In tal modo si garantisce anche che tutte le funzionalità di supporto del DAG critiche che potrebbero trovarsi sul server (ad esempio, il ruolo PAM, Primary Active Manager) vengano spostate su un altro server e non possano tornare sul server. Nello specifico, è necessario effettuare le seguenti attività:

1.  Per iniziare il processo di svuotamento delle code di trasposto, eseguire `Set-ServerComponentState <ServerName> -Component HubTransport -State Draining -Requester Maintenance`

2.  Per iniziare il processo di svuotamento delle code di trasposto, eseguire `Restart-Service MSExchangeTransport`

3.  Per iniziare il processo di svuotamento di tutte le chiamate di messaggistica unificata, eseguire `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Draining -Requester Maintenance`

4.  Per reindirizzare i messaggi con recapito in sospeso nelle code locali al server Cassette postali specificato dal parametro Destinazione, eseguire `Redirect-Message -Server <ServerName> -Target <MailboxServerFQDN>`

5.  Per sospende il nodo cluster, evitando che sia o diventi il PAM, eseguire `Suspend-ClusterNode <ServerName>`

6.  Per spostare tutti i database attivi ospitati nel membro del DAG in altri membri del DAG, eseguire `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $True`

7.  Per impedire al server di ospitare copie del database attive, eseguire `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Blocked`

8.  Per mettere il server in modalità manutenzione, eseguire `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Inactive -Requester Maintenance`

Per verificare che un server sia pronto per la manutenzione, procedere come segue:

1.  Per verificare che il server sia stato messo in modalità manutenzione, eseguire `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`

2.  Per verificare che il server non ospiti alcuna copia di database attiva, eseguire `Get-MailboxServer <ServerName> | ft DatabaseCopy* -Autosize`

3.  Per verificare che il nodo sia sospeso, eseguire `Get-ClusterNode <ServerName> | fl`

4.  Per verificare che tutte le code di trasporto siano state svuotate, eseguire `Get-Queue`

Una volta che la manutenzione è stata completata e il membro DAG è pronto per il ripristino del servizio, è possibile disattivare la modalità di manutenzione per il membro del DAG e rimetterlo in produzione. Procedere come segue:

  - Per indicare che il server non è in modalità manutenzione, eseguire `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Maintenance`

  - Per consentire al server di accettare chiamate di messaggistica unificata, eseguire `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Active -Requester Maintenance`

  - Per riprendere il nodo nel cluster e abilitare le funzionalità complete del cluster per il server, eseguire `Resume-ClusterNode <ServerName>`

  - Per consentire ai database di diventare attivi sul server, eseguire `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $False`

  - Per rimuovere i blocchi di attivazione automatici, eseguire `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Unrestricted`

  - Per abilitare le code di trasporto e consentire al server di accettare ed elaborare i messaggi, eseguire `Set-ServerComponentState <ServerName> -Component HubTransport -State Active -Requester Maintenance`

  - Per riprendere l'attività di trasporto, eseguire `Restart-Service MSExchangeTransport`

Per verificare se un server è pronto per essere utilizzato in ambienti di produzione, eseguire le operazioni riportate di seguito:

1.  Per verificare che il server non sia in modalità di manutenzione, eseguire `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`

Se si sta installando un aggiornamento di Exchange e il processo ha esito negativo, è possibile mantenere alcuni componenti server nello stato inattivo, il quale verrà visualizzato nell'output del precedente cmdlet Get-ServerComponentState. Per risolvere il problema, eseguire i comandi riportati di seguito:

  - `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component Monitoring -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component RecoveryActionsEnabled -State Active -Requester Functional`

Inizio pagina

## Chiusura dei membri del DAG

La soluzione ad elevata disponibilità Exchange 2013 è integrata con la procedura di chiusura di Windows. Se un amministratore o un'applicazione avvia la chiusura di un server Windows in un DAG che dispone di un database replicato in uno o più membri DAG, il sistema cerca di attivare un'altra copia del database installato prima di permettere il completamento della procedura di chiusura.

Tuttavia, questo nuovo comportamento non garantisce un'attivazione `lossless` per tutti i database sul server in chiusura. Di conseguenza, la procedura consigliata prevede di eseguire uno switchover del server prima di arrestare un server membro di un gruppo di disponibilità del database.

Inizio pagina

## Installazione di aggiornamenti sui membri del DAG

L'installazione degli aggiornamenti di Microsoft Exchange Server 2013 su un server che è membro di un DAG è un'operazione relativamente semplice. Quando si installa un aggiornamento su un server che è membro di un DAG, diversi servizi verranno arrestati durante l'installazione, compresi tutti i servizi di Exchange e il servizio Cluster. La procedura generale per l'applicazione degli aggiornamenti a un membro del DAG è la seguente:

1.  Seguire i passaggi descritti precedentemente per mettere il membro del DAG in modalità manutenzione.

2.  Installare l'aggiornamento.

3.  Utilizzare i passaggi descritti precedentemente per disattivare la modalità di manutenzione per il membro del DAG e rimetterlo in produzione.

4.  Facoltativamente, utilizzare lo script RedistributeActiveDatabases.ps1 per riequilibrare le copie del database attive nel DAG.

È possibile scaricare l'aggiornamento cumulativo più recente per Exchange 2013 dall'[Area download Microsoft](http://www.microsoft.com/downloads/it-it/).

Inizio pagina


---
title: 'Disponibilità gestita: Exchange 2013 Help'
TOCTitle: Disponibilità gestita
ms:assetid: ceb99e6f-6dca-446d-abfb-3e6fc6a72704
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn482056(v=EXCHG.150)
ms:contentKeyID: 59890032
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disponibilità gestita

 

_**Si applica a:** Exchange Online, Exchange Server 2013 SP1_

_**Ultima modifica dell'argomento:** 2017-03-29_

Assicurare che gli utenti abbiano un'esperienza ottimale con la posta elettronica è sempre stato l'obiettivo principale degli amministratori di sistema. Per garantire la disponibilità e l'affidabilità dell'organizzazione Exchange Server 2013 di Microsoft, tutti gli aspetti del sistema devono essere monitorati attivamente e tutti i problemi individuati devono essere risolti rapidamente. Nelle versioni precedenti di Exchange, i componenti del sistema critico di monitoraggio comprendevano l'utilizzo di un'applicazione esterna, come ad esempio Microsoft System Center 2012 Operations Manager, per raccogliere dati e per offrire azioni di ripristino in caso di problemi rilevati durante la raccolta dei dati. Exchange 2010 e le versioni precedenti includevano il manifesto dell'integrità e i motori di correlazione sotto forma di Management Pack. Tali componenti consentivano all'Operations Manager di determinare se un particolare componente era integro o meno. Inoltre, l'Operations Manager utilizzava anche l'infrastruttura di cmdlet di diagnostica integrata in Exchange 2010 per eseguire transazioni sintetiche nei confronti di vari aspetti del sistema.

Exchange 2013 adotta un nuovo approccio nei confronti del monitoraggio e per preservare l'esperienza dell'utente finale in modo nativo grazie a una funzionalità chiamata *Disponibilità gestita* che offre azioni di ripristino e monitoraggio integrate.

## Disponibilità gestita

La disponibilità gestita, definita anche *monitoraggio attivo* o *monitoraggio attivo locale*, è l'integrazione delle azioni di monitoraggio e ripristino integrate con la piattaforma ad elevata disponibilità di Exchange. Tale piattaforma è stata progettata per rilevare e risolvere i problemi non appena si verificano e vengono rilevati dal sistema. Diversamente dalle precedenti soluzioni e tecniche di monitoraggio esterno di Exchange, la disponibilità gestita non cerca di identificare o comunicare la causa principale di un problema. È incentrata piuttosto sugli aspetti del ripristino legati alle tre aree principali dell'esperienza utente:

  - **Disponibilità**   Gli utenti possono accedere al servizio?

  - **Latenza**   Com'è l'esperienza per gli utenti?

  - **Errori**   Gli utenti sono in grado di realizzare ciò che desiderano?

Il consolidamento del ruolo del server e altre modifiche architettoniche in Exchange 2013 richiedono un nuovo approccio alle metodologie di monitoraggio e al modello di integrità utilizzati nelle versioni precedenti di Exchange. La disponibilità gestita è stata progettata per rispondere a questi cambiamenti offrendo una soluzione nativa di monitoraggio e ripristino dell'integrità. La disponibilità gestita si discosta dal monitoraggio di singole sezioni di sistema separate per adottare il monitoraggio dell'esperienza utente end-to-end, proteggendola mediante azioni orientate al ripristino.

La disponibilità gestita è un processo interno che viene eseguito su ciascun server Exchange 2013. Effettua il polling e analizza centinaia di metriche di integrità ogni secondo. Se viene trovato qualcosa di sbagliato, la maggior parte delle volte viene risolto in modo automatico. Esistono comunque dei problemi che non possono essere risolti automaticamente. In questi casi, la disponibilità gestita passa il problema a un amministratore attraverso la registrazione eventi.

La disponibilità gestita viene implementata sotto forma di due servizi:

  - **Servizio Exchange Health Manager Service (MSExchangeHMHost.exe)**   Si tratta di un processo controller utilizzato per gestire i processi di lavoro. Viene utilizzato per realizzare, eseguire, avviare e interrompere il processo di lavoro, in base alle esigenze. Viene inoltre utilizzato per recuperare il processo di lavoro in caso di arresti anomali per impedire che questo diventi un singolo punto di errore.

  - **Processo Exchange Health Manager Worker (MSExchangeHMWorker.exe)**   Si tratta del processo di lavoro responsabile dell'esecuzione di attività in fase di esecuzione nell'ambito di disponibilità gestita.

Gestione disponibilità utilizza un'archiviazione persistente per svolgere le sue funzioni:

  - I file XML nella cartella \\bin\\Monitoring\\config vengono utilizzati per archiviare le impostazioni di configurazione di alcuni degli elementi di lavoro di probe e monitor.

  - Active Directory viene utilizzato per archiviare le sostituzioni globali.

  - Il Registro di sistema di Windows è utilizzato per memorizzare dati di runtime, ad esempio i segnalibri e le sostituzioni locali (specifiche del server).

  - L'infrastruttura del registro eventi del canale Crimson di Windows viene utilizzata per archiviare i risultati degli elementi di lavoro.

  - Le cassette postali di integrità vengono utilizzate per attività di tipo "probe". Verranno create più cassette postali di integrità in ogni database delle cassette postali esistente sul server.

Come mostrato nel disegno seguente, la disponibilità gestita include tre componenti asincroni principali costantemente attivi.

**Componenti della disponibilità gestita**

![Disponibilità gestita in Exchange Server 2013](images/Dn482056.7a54dcb5-1e28-4bd4-87e6-0d496b4ab796(EXCHG.150).gif "Disponibilità gestita in Exchange Server 2013")

Il primo componente viene chiamato un *Probe*. Probe sono responsabili della misurazioni sul server e la raccolta dei dati. I risultati di tali misurazioni flow nel componente secondi il *Monitor*. Il monitoraggio contiene tutte le regole business utilizzati dal sistema basato su ciò che viene considerato integra i dati raccolti. Analogamente a un modulo di riconoscimento motivo, il monitoraggio per i diversi motivi diversi in tutte le misurazioni raccolti, e quindi decide se un elemento è considerato integro. Infine, esistono *risponditori*che sono responsabili azioni escalation e il ripristino. Quando un elemento non è integro, la prima azione consiste nel tentare di ripristino di tale componente. Questi dati possono includere azioni di ripristino in più fasi. ad esempio, il primo tentativo potrebbe essere necessario riavviare il pool di applicazioni, il secondo potrebbe essere necessario riavviare il servizio, il tentativo di terzo potrebbe essere necessario riavviare il server e il tentativo successivo può essere per rendere il server non in linea in modo che non vengono più accettati traffico. Se le azioni di ripristino ha esito negativo, il sistema di trasformazione di un utente tramite notifica del registro eventi il problema.

Esistono tre categorie principali di probe: probe ricorrenti, le notifiche e controlli. Probe ricorrenti sono le transazioni sintetiche eseguite dal sistema per testare l'esperienza utente end-to-end. Controlli sono all'infrastruttura di eseguire la raccolta dei dati delle prestazioni, incluso il traffico di utenti e misurano i dati raccolti su soglie impostati per determinare i picchi di errori user. In questo modo l'infrastruttura di controlli essere consapevoli quando gli utenti con problemi. Infine, la logica di notifica consente il sistema dovrà eseguire immediatamente basato su un evento critico, senza dover attendere che i risultati dei dati raccolti da un probe di azione. Si tratta in genere eccezioni o condizioni che possono essere rilevate e riconosciute senza un set di campioni di grandi.

Probe ricorrenti eseguire alcuni minuti e controllare alcuni aspetti dell'integrità dei servizi. Questi probe possono mostrare un messaggio di posta elettronica tramite Exchange ActiveSync per una cassetta postale di monitoraggio, è possibile connettersi a un endpoint RPC o si potrebbe verificare la connettività Client Access-Mailbox.

Tutte le ricerche vengono definite all'avvio del servizio di gestione dello stato del canale crimson Microsoft.Exchange.ActiveMonitoring\\ProbeDefinition. Ogni definizioni di probe dispone di molte proprietà, ma le proprietà più pertinenti sono:

  - **Nome** Il nome del probe, inizia con una *SampleMask* del monitor di probe.

  - **TypeName** Il tipo di oggetto di codice del probe che contiene la logica di probe.

  - **ServiceName** Nome del set di integrità che contiene il probe.

  - **TargetResource** L'oggetto il test di convalida. Questo viene aggiunto il nome del probe quando viene eseguito di diventare un risultato di probe *ResultName*

  - **RecurrenceIntervalSeconds** La frequenza con cui viene eseguito il probe.

  - **TimeoutSeconds** Il test sarà la durata dell'attesa prima di eseguire.

Esistono centinaia di probe ricorrente. Molte di queste probe sono così come il numero all'aumentare del database, pertanto non il numero di probe per ogni database. La maggior parte dei probe sono definiti nel codice e pertanto non sono direttamente individuabili.

Informazioni di base di un probe ricorrente sono i seguenti: avviare ogni *RecurrenceIntervalSeconds* e controllare alcuni aspetti dell'integrità (o probe). Se il componente non è integro, passa il probe e scrive un evento informativo per il canale Microsoft.Exchange.ActiveMonitoring\\ProbeResult con un *ResultType* di 3. Se il controllo ha esito negativo o si verifichi il timeout, il test non riesce e scrive un evento di errore per il canale stesso. Un *ResultType* di 4 indica che il controllo non riuscito e un *ResultType* 1 indica che è verificato il timeout. Molti probe nuovamente verranno eseguita quando si timeout e al valore della proprietà *MaxRetryAttempts* .


> [!NOTE]
> <STRONG>Nota</STRONG> ProbeResult canale crimson può ottenere molto impegnato con centinaia di probe in esecuzione alcuni minuti e la registrazione di un evento in modo che può esistere un impatto reale sulle prestazioni di Exchange server se si tenta di eseguire query costosa per i registri eventi in un ambiente di produzione.



Le notifiche sono probe che non vengono eseguiti per l'infrastruttura di gestione dello stato, ma per alcuni altri servizi nel server. Questi servizi eseguono i propri il monitoraggio e inseriscono i dati framework Managed Availability scrivendo direttamente i risultati di probe. Si potrà essere visualizzato i probe nel canale ProbeDefinition, come il canale solo descrive probe che verranno eseguite dal framework di disponibilità gestita. Ad esempio, il ServerOneCopyMonitor Monitor è attivato dai risultati di probe scritti dal servizio MSExchangeDAGMgmt. Questo servizio esegue il proprio monitoraggio, determina se esiste un problema e i registri di un risultato di test. La maggior parte delle notifiche probe sono in grado di accedere sia un evento di colore rosso che consente di non integro il monitoraggio e un evento verde che rende nuovamente integro il monitoraggio.

Verifiche sono probe che registrati solo gli eventi per un contatore delle prestazioni passa sopra o sotto una soglia predefinita. Sono in realtà un caso speciale di notifica probe, come invece è un servizio i contatori delle prestazioni nel server di monitoraggio e la registrazione di eventi per il canale ProbeResult quando viene raggiunta la soglia configurata.

Per trovare il contatore delle prestazioni e soglia è considerato non integro, è possibile esaminare il monitoraggio per questo controllo. Strumenti di monitoraggio del tipo *Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueAboveThresholdMonitor* o *Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueBelowThresholdMonitor* significa che il probe che sono guardare è un probe di controllo

Con i monitoraggi vengono eseguite query sui dati raccolti dai probe per determinare se intraprendere o meno un'azione in base al set di regole predefinito. In base alla regola o alla natura del problema, il monitoraggio può anche avviare un risponditore o inoltrare il problema a un utente mediante una voce del registro eventi. Inoltre, i monitoraggi definiscono l'intervallo di tempo tra il rilevamento del problema e l'esecuzione del risponditore, nonché il flusso di lavoro dell'azione di ripristino. I monitoraggi dispongono di diversi stati. Dal punto di vista dello stato del sistema, gli stati del monitoraggio sono due:

  - **Integro** L'esecuzione del monitoraggio è corretta e tutte le metriche raccolte rientrano nell'ambito dei normali parametri di funzionamento

  - **Non integro**   Il monitoraggio non è integro ed è stato avviato il ripristino tramite un risponditore o è stata inviata una notifica all'amministratore tramite escalation.

Dal punto vista dell'amministratore, i monitoraggi dispongono di ulteriori stati che saranno visualizzati in Shell:

  - **Danneggiato**   Quando un monitoraggio si trova in uno stato non integro per un intervallo di tempo di 0-60 secondi, viene considerato danneggiato. Se un monitoraggio risulta danneggiato per più di 60 secondi, viene considerato non integro.

  - **Disabilitato** Il monitoraggio è stato disabilitato in modo esplicito da un amministratore.

  - **Non disponibile** Il servizio di integrità di Microsoft Exchange esegue periodicamente delle query su ciascun monitoraggio per verificarne lo stato. Se non si riceve alcuna risposta alla query, lo stato del monitoraggio sarà Non disponibile.

  - **Repairing**   Viene impostato da un amministratore per indicare al sistema che sono in corso azioni correttive da parte di un utente, che consentono al sistema e agli utenti di distinguere tra altri errori che potrebbero verificarsi contemporaneamente all'azione correttiva (ad esempio, un'operazione di reseeding di una copia del database).

Ogni monitor dispone di una proprietà *SampleMask* nella definizione. Quando viene eseguito il monitoraggio, la ricerca di eventi del canale ProbeResult con *ResultName* corrispondente *SampleMask* del monitor. Questi eventi potrebbero essere dal probe ricorrenti, notifiche o controlli. Se si ottengono le soglie del monitor, quest'ultimo diventa danneggiamento. Dal punto di vista del monitor, tutti i tipi di probe tre sono gli stessi man mano che ogni accedono al canale ProbeResult.

È importante notare che un errore di probe singolo non necessariamente indica che si verificano problemi con il server. È la progettazione di strumenti di monitoraggio per identificare correttamente quando si verifica un problema reale che delle modifiche necessarie. Questo è il motivo per cui molti monitor sono soglie di errori più test prima di diventare danneggiamento. Anche in molti di questi problemi possa essere risolto automaticamente tramite risponditori, in modo che sia il modo migliore per individuare i problemi che richiedono l'intervento manuale nel canale crimson Microsoft.Exchange.ManagedAvailability\\Monitoring. Ciò include l'errore probe più recente.

Come indicato dal nome, i risponditori eseguono un certo tipo di risposta a un avviso generato da un sistema di monitoraggio. I risponditori eseguono diverse azioni di ripristino, come la reimpostazione del processo di lavoro di un pool di applicazioni per il riavvio di un server. Esistono diversi tipi di risponditori:

  - **Risponditore di riavvio** Consente di terminare e riavviare un servizio

  - **Risponditore di reimpostazione di un pool di applicazioni** Consente di interrompere e riavviare un pool di applicazioni in Internet Information Services (IIS)

  - **Risponditore failover** Consente di avviare il failover di un database o server

  - **Risponditore del controllo errori** Consente di avviare un controllo sugli errori del server, causando un riavvio del server

  - **Risponditore offline** Consente di accettare un protocollo su un server fuori servizio (rifiuta le richieste dei client)

  - **Risponditore online** Consente di rimettere in servizio un protocollo su un server (accetta richieste dei client)

  - **Risponditore escalation** Consente di passare il problema all'amministratore tramite la registrazione eventi

Oltre ai risponditori elencati sopra, alcuni componenti presentano anche risponditori specializzati esclusivi.

Tutti i risponditori includono il comportamento di limitazione, che fornisce un meccanismo incorporato di sequenziamento per controllare le azioni del risponditore. Il comportamento di limitazione è progettato per garantire che il sistema non venga compromesso o peggiorato dalle azioni di ripristino del risponditore. Tutti i risponditori sono limitati in qualche modo. Quando si verifica la limitazione, l'azione di ripristino del risponditore potrebbe essere ignorata o ritardata, a seconda del tipo di azione. Ad esempio, quando il risponditore del controllo errori è limitato, l'azione viene ignorata e non ritardata.

## Set di integrità

Da una prospettiva relativa alla creazione dei report, la disponibilità gestita presenta due viste dell'integrità, una interna e una esterna. La vista interna utilizza *i set di integrità*. Ogni componente in Exchange 2013 (ad esempio, Outlook Web App, Exchange ActiveSync, il servizio Archivio informazioni, l'indicizzazione del contenuto, i servizi di trasporto e così via) viene monitorato dalla disponibilità gestita attraverso probe, strumenti di monitoraggio e risponditori. Un gruppo di probe, strumenti di monitoraggio e risponditori per un dato componente viene chiamato *set di integrità*. Un set di integrità consiste in un gruppo di probe, strumenti di monitoraggio e risponditori che determinano se il componente è integro. Lo stato corrente del set di integrità (vale a dire se è integro o meno) viene determinato utilizzando lo stato degli strumenti di monitoraggio del set di integrità. Se tutti gli strumenti di monitoraggio del set di integrità sono integri, allora il set di integrità è integro. Se anche uno degli strumenti di monitoraggio non è integro, lo stato del set di integrità verrà determinato dallo strumento di monitoraggio meno integro.

Per ulteriori informazioni sulla visualizzazione dello stato di integrità del server o dei set di integrità, vedere [Gestire i set di integrità e lo stato dei server](manage-health-sets-and-server-health-exchange-2013-help.md).

## Gruppi di integrità

La vista esterna sulla disponibilità gestita è formata da *gruppi di integrità*. I gruppi di integrità sono esposti a System Center Operations Manager 2007 R2 e System Center Operations Manager 2012.

Esistono quattro gruppi di integrità principali:

  - **Punti tocco del cliente** Componenti che influenzano interazioni dell'utente in tempo reale, quali protocolli o Archivio informazioni

  - **Componenti di servizio** Componenti senza interazioni dell'utente dirette e in tempo reale, come ad esempio il servizio di replica delle cassette postali di Microsoft Exchange o il processo di generazione della Rubrica fuori rete (OABGen)

  - **Componenti del server** Le risorse fisiche del server, come lo spazio su disco, la memoria e i servizi di rete

  - **Disponibilità delle dipendenze** La capacità del server di accedere alle dipendenze necessarie, ad esempio Active Directory, DNS e così via

Durante l'installazione di Exchange Management Pack, System Center Operations Manager (SCOM) funge da un portale di integrità per la visualizzazione delle informazioni relative all'ambiente Exchange. Dashboard di SCOM include tre visualizzazioni dell'integrità del server Exchange:

  - **Avvisi attivi** I risponditori di escalation scrivono nel registro eventi di Windows gli eventi consumati dallo strumento di monitoraggio all'interno di SCOM. Questi vengono visualizzati come avvisi nella vista Avvisi attivi.

  - **Integrità dell'organizzazione** In questa vista viene visualizzato un riepilogo cumulativo dello stato di integrità complessivo dell'organizzazione di Exchange. Tali riepiloghi includono la visualizzazione dell'integrità dei singoli gruppi di disponibilità del database e dell'integrità all'interno di siti Active Directory specifici.

  - **Integrità del server** I set di integrità correlati vengono combinati in gruppi di integrità e riepilogati in questa vista.

## Sostituzioni

Le sostituzioni consentono a un amministratore di configurare alcuni aspetti dei probe, degli strumenti di monitoraggio e dei risponditori della disponibilità gestita. Le sostituzioni consentono di ottimizzare alcuni dei limiti utilizzati dalla disponibilità gestita. Possono inoltre essere utilizzate per abilitare azioni di emergenza per eventi inattesi che richiedono impostazioni di configurazione diverse da quelle predefinite.

Le sostituzioni possono essere create e applicate a un solo server (note come *sostituzioni server*) o essere applicate a un gruppo di server *sostituzioni globali*). I dati di configurazione della sostituzione del server vengono conservati nel Registro di sistema di Windows nel server al quale viene applicata la sostituzione. I dati di configurazione della sostituzione globale vengono archiviati in Active Directory.

Le sostituzioni possono avere durata illimitata o specifica. Inoltre, le sostituzioni globali possono essere applicate a tutti i server o solo a quelli che eseguono una versione specifica di Exchange.

Quando si configura una sostituzione, essa non avrà effetto immediato. Microsoft Exchange Health Manager Service verifica l'aggiornamenti dei dati di configurazione ogni 10 minuti. Inoltre, le sostituzioni globali dipendono dalla latenza di replica di Active Directory.

Per informazioni dettagliate sulla visualizzazione o configurazione delle sostituzioni di server o globali, vedere [Configurare le sostituzioni di disponibilità gestita](configure-managed-availability-overrides-exchange-2013-help.md).

## I cmdlet e attività di gestione

Esistono tre attività operative principali che gli amministratori eseguono generalmente in relazione alla disponibilità gestita:

  - Estrazione o visualizzazione dell'integrità di sistema

  - Visualizzazione dei set di integrità e dei dettagli su probe, strumenti di monitoraggio e risponditori

  - Gestione delle sostituzioni

I due strumenti di gestione principali della disponibilità gestita sono il Registro eventi di Windows Event e Shell. La disponibilità gestita registra una grande quantità di informazioni nel registro eventi del canale Crimson ActiveMonitoring e ManagedAvailability di Exchange, come ad esempio:

  - Definizioni di probe, strumenti di monitoraggio e risponditori, registrati nei rispettivi registri di eventi \*Definition.

  - Risultati di probe, strumenti di monitoraggio e risponditori, registrati nei rispettivi registri di eventi \*Results.

  - I dettagli sulle azioni di ripristino del risponditore, compresi dati sul quando l'azione di ripristino ha inizio e quando è considerata conclusa (con esito positivo o meno), registrati nel registro eventi RecoveryActionResults.

Sono disponibili 12 cmdlet utilizzati per la disponibilità gestita, descritti nella tabella seguente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/jj218703(v=exchg.150)">Get-ServerHealth</a></p></td>
<td><p>Utilizzato per ottenere informazioni non elaborate sull'integrità del server, quali set di integrità e relativo stato corrente (integro o non integro), strumenti di monitoraggio del set di integrità, componenti del server, risorse di destinazione per probe e timestamp relativi ai tempi di avvio o interruzione di probe o strumenti di monitoraggio e ai tempi di transizione dello stato.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/it-it/library/jj218724(v=exchg.150)">Get-HealthReport</a></p></td>
<td><p>Utilizzato per ottenere una vista di riepilogo dell'integrità che include set di integrità e il relativo stato corrente.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/jj218668(v=exchg.150)">Get-MonitoringItemIdentity</a></p></td>
<td><p>Utilizzato per visualizzare probe, strumenti di monitoraggio e risponditori associati a un set di integrità specifico.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/it-it/library/jj218642(v=exchg.150)">Get-MonitoringItemHelp</a></p></td>
<td><p>Utilizzato per visualizzare le descrizioni su alcune delle proprietà di probe, strumenti di monitoraggio e risponditori.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/jj218628(v=exchg.150)">Add-ServerMonitoringOverride</a></p></td>
<td><p>Utilizzato per creare una sostituzione locale e specifica del server di un probe, uno strumento di monitoraggio o risponditore.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/it-it/library/jj218664(v=exchg.150)">Get-ServerMonitoringOverride</a></p></td>
<td><p>Utilizzato per visualizzare un elenco di sostituzioni locali sul server specificato.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/dn482411(v=exchg.150)">Remove-ServerMonitoringOverride</a></p></td>
<td><p>Utilizzato per rimuovere una sostituzione locale da un server specifico.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/it-it/library/jj218683(v=exchg.150)">Add-GlobalMonitoringOverride</a></p></td>
<td><p>Utilizzato per creare una sostituzione globale per un gruppo di server.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/jj218627(v=exchg.150)">Get-GlobalMonitoringOverride</a></p></td>
<td><p>Utilizzato per visualizzare un elenco di sostituzioni globali configurati nell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/it-it/library/jj218675(v=exchg.150)">Remove-GlobalMonitoringOverride</a></p></td>
<td><p>Utilizzato per rimuovere una sostituzione globale.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/jj218699(v=exchg.150)">Set-ServerComponentState</a></p></td>
<td><p>Utilizzato per configurare lo stato di uno o più componenti del server.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/it-it/library/jj218713(v=exchg.150)">Get-ServerComponentState</a></p></td>
<td><p>Utilizzato per visualizzare lo stato di uno o più componenti del server.</p></td>
</tr>
</tbody>
</table>


---
title: 'Suggerimenti relativi a ridimensionamento e configurazione di Exchange 2013: Exchange 2013 Help'
TOCTitle: Suggerimenti relativi a ridimensionamento e configurazione di Exchange 2013
ms:assetid: 4c4ba2fc-014a-46fb-949a-2dabba92c4a5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn879075(v=EXCHG.150)
ms:contentKeyID: 63763712
ms.date: 02/20/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Suggerimenti relativi a ridimensionamento e configurazione di Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2017-03-27_

Exchange 2013 richiede più risorse di sistema rispetto alle versioni precedenti di Exchange. Ridimensionando in modo corretto l'infrastruttura di Exchange 2013, e quindi apportando alcune configurazioni consigliate ai componenti correlati a Exchange all'interno di tale infrastruttura, è possibile porre le basi per una distribuzione con prestazioni ottimali.

## Ridimensionamento di Exchange 2013

Il ridimensionamento corretto di Exchange 2013 è uno dei modi più efficaci di evitare problemi di prestazioni. Lo strumento di calcolo dei requisiti del ruolo del server di Exchange 2013 è [disponibile qui](https://go.microsoft.com/fwlink/p/?linkid=52384). La versione più recente è 6.6, ma è consigliabile controllare periodicamente la presenza di aggiornamenti. Per utilizzare questo strumento di calcolo correttamente, è necessario consultare le indicazioni nei post di blog sullo [strumento di calcolo dei requisiti del ruolo del server di Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=38667) e sul [ridimensionamento delle distribuzioni di Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=30199).

È importante iniziare con lo strumento di calcolo prima dell'acquisto e della distribuzione dell'hardware; occorre innanzitutto determinare i requisiti delle risorse generali in base ai risultati dello strumento di calcolo. È possibile utilizzare lo strumento di calcolo per specificare le esigenze dell'organizzazione e sfruttare i risultati come linee guida per ridimensionare l'hardware. Lo strumento di calcolo non indica quanti server utilizzare, ma consente di fare una stima dell'impatto che avrà un carico di lavoro di Exchange su un determinato insieme di server. È consigliabile sperimentare diverse configurazioni per visualizzarne l'effetto sulle prestazioni, allo scopo di rispondere alle esigenze aziendali e relative all'hardware specifiche per l'ambiente.

Per semplificare le distribuzioni e sfruttare al meglio l'hardware, il gruppo di prodotti Exchange consiglia i server multiruolo. L'utilizzo di server multiruolo offre una disponibilità migliore a livello di server Accesso client (CAS), poiché sono presenti più server Accesso client disponibile per gestire le richieste in uno scenario di errore. La considerazione principale relativa alla progettazione da tenere presente per Exchange 2013 è di utilizzare server di tipo commodity "più piccoli" (eseguendo la scalabilità in orizzontale anziché quella in verticale). Le fasi di progettazione e test sono state effettuate con due computer socket contenenti fino a venti core processori, con un massimo di 96 GB di RAM. Se l'hardware a disposizione dell'utente è di dimensioni superiori, prendere in considerazione altre opzioni, come l'uso dell'hardware per altre esigenze e l'acquisto di server più piccoli per l'ambiente Exchange 2013 o la virtualizzazione.

È preferibile creare più server (scalabilità in orizzontale) piuttosto che aggiungere risorse ai server esistenti più grandi (scalabilità in verticale). La scalabilità in orizzontale consente di trarre vantaggio dalle funzionalità di disponibilità elevata integrate in Exchange 2013. Per capire perché questa configurazione è consigliata, leggere i post [L'architettura preferita](https://go.microsoft.com/fwlink/p/?linkid=52378) e [Impatto della resilienza del sito sulla disponibilità](https://go.microsoft.com/fwlink/p/?linkid=52384).

Lo strumento di calcolo non tiene conto dei prodotti di terze parti in esecuzione sui server di Exchange o dei prodotti che interagiscono con Exchange (comprese le applicazioni sviluppate internamente); ciò significa che è necessario prenderli in considerazione durante il ridimensionamento. Lync Server, ad esempio, le applicazioni dei servizi Web di Exchange (EWS) di terze parti e i dispositivi ActiveSync possono tutti aumentare in modo significativo i requisiti della CPU per ogni utente. È possibile fare riferimento alla documentazione sui prodotti di terze parti per informazioni su come questi influiscono su Exchange. Si consiglia di creare una baseline delle prestazioni per Exchange prima di implementare soluzioni di terze parti.

## Configurazioni delle prestazioni consigliate

Per l'ambiente di Exchange 2013 si consigliano le ottimizzazioni delle prestazioni riportate di seguito.

## Alimentazione

Impostare BIOS in modo da consentire al sistema operativo di gestire l'alimentazione.

Nel sistema operativo, attivare la combinazione per il risparmio di energia per le prestazioni elevate.

## Elaborazione

Disabilitare hyperthreading nei server di Exchange fisici. Con la virtualizzazione, hyperthreading potrebbe essere abilitato nel server fisico, ma a ogni server virtuale deve essere assegnato il numero necessario di CPU virtuali (non una quantità eccessiva di CPU virtuali) e ogni server deve utilizzare silo il numero di core processori fisici per i calcoli di ridimensionamento.

In Exchange Server 2013 Service Pack 1 o versioni successive, è possibile abilitare la ripartizione del carico di lavoro SSL per ridurre il consumo di CPU da parte dei server Accesso client, ma la complessa configurazione della ripartizione del carico di lavoro SSL potrebbe non giustificare il vantaggio ottenuto.

## .NET Framework


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
<th>Versione di Exchange</th>
<th>.NET Framework 4.7.1</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU19</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU16 - CU18</p></td>
<td><p></p></td>
<td><p> X</p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


Se non si è in grado di installare .net 4.5.2, fare riferimento all'articolo 2995145 della Microsoft Knowlege Base "[Problemi relativi alle prestazioni o ritardi quando ci si connette a Exchange Server 2013 in esecuzione in Windows Server](https://go.microsoft.com/fwlink/p/?linkid=52415)." Le correzioni riportate nell'articolo sono state sviluppate in base ai risultati interni sull'utilizzo della memoria di Store Worker Process. L'applicazione di queste correzioni consente di ridurre il consumo di memoria generale per tutti i processi gestiti (incluso il processo store worker) e il tempo di CPU complessivo necessario per l'attività di garbage collection (GC) di .NET.

## Hotfix

L'Exchange Performance Team consiglia di installare tutte le correzioni rapide relative alle prestazioni seguenti.

  - [È disponibile un aggiornamento che migliora la resilienza del cluster in Windows Server 2012](https://go.microsoft.com/fwlink/p/?linkid=52408)

  - [Hotfix e aggiornamenti consigliati per i cluster di failover basati su Windows Server 2012](https://go.microsoft.com/fwlink/p/?linkid=52408)

  - [Hotfix e aggiornamenti consigliati per i cluster di failover basati su Windows Server 2012 R2](https://go.microsoft.com/fwlink/p/?linkid=52409)

  - [Assegnazione del processore RSS errato su un computer basato su Windows 8 o Windows Server 2012 con processori multicore](https://go.microsoft.com/fwlink/p/?linkid=32414)

  - [Problemi relativi alle prestazioni o ritardi quando ci si connette a Exchange Server 2013 in esecuzione in Windows Server](https://go.microsoft.com/fwlink/p/?linkid=31296)

  - [problema di connettività in Outlook se SSLOffloading è "True" in Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=52409)

  - [Connessione al server prolungata per Outlook dopo un failover del database in Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=52409)

  - [Prestazioni ridotte in Outlook Web App quando Lync è integrato con Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=52409)

  - [EMS richiede molto tempo per eseguire il primo comando in un ambiente con aggiornamento cumulativo 5 per Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=52409)

  - [Latenza del routing dei messaggi se IPv6 è abilitato in Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=52409)

  - [Utilizzo della CPU elevato da parte di un'applicazione che dipende da un client LDAP Microsoft in WIndows Server 2008 R2 SP1](https://go.microsoft.com/fwlink/p/?linkid=53028)

  - [Utilizzo della CPU elevato quando si usa il protocollo RPC su HTTP in Windows 8.1 o Windows Server 2012 R2](https://go.microsoft.com/fwlink/p/?linkid=61912)

## Rete

Con Exchange 2013, è consigliabile una singola scheda di rete perché non è più necessario dividere reti MAPI e reti della replica. Per ulteriori informazioni, vedere [Network requirements](planning-for-high-availability-and-site-resilience-exchange-2013-help.md).

Usare le impostazioni di offload SNP predefinite, se disponibili, e verificare che RSS sia abilitato (l'impostazione predefinita in Windows Server 2012 e versioni successive). RSS consente di ridimensionare l'utilizzo della CPU, specialmente su 10 GbE.

Verificare che il sistema operativo non disabiliti la scheda di rete per risparmiare energia.

Mantenere aggiornati i driver NIC. Contattare il fornitore su base mensile per verificare la disponibilità di aggiornamenti per i driver.

## Internet Information Services (IIS)

Durante l'installazione, in Exchange vengono modificati alcuni limiti di connessione per IIS. Si consiglia di non regolare ulteriormente IIS.

Evitare personalizzazioni quando possibile. Qualsiasi modifica apportata a web.config o alle chiavi del Registro di sistema può essere sovrascritta dagli aggiornamenti cumulativi di Exchange o dagli aggiornamenti di Windows.

## Archiviazione

Linee guida per l'archiviazione in Exchange 2013 sono disponibili in [Opzioni di configurazione di archiviazione di Exchange 2013](exchange-2013-storage-configuration-options-exchange-2013-help.md).

## Virtualizzazione

Consultare [Requirements for hardware virtualization](exchange-2013-virtualization-exchange-2013-help.md). Tenere inoltre presente che Exchange non riconosce l'accesso non uniforme alla memoria (NUMA). Pertanto, è consigliabile utilizzare le impostazioni NUMA predefinite del produttore dell'hardware.

## Active Directory

Monitorare le prestazioni del server di directory perché le query di Active Directory influiscono direttamente sulla distribuzione di Exchange.

La durata della ricerca LDAP è un contatore critico da tenere in considerazione in merito all'integrità di Active Directory. Monitorare la CPU nei controller di dominio. I problemi relativi alla CPU nei controller di dominio comportano un calo di prestazioni nei server di Exchange.

Eseguire la "Diagnostica di Active Directory" integrata nel controller di dominio in Performance Monitor situato in "Insieme agenti di raccolta dati" per isolare la causa dei problemi relativi alle prestazioni dei controller di dominio.

Pianificare una RAM sufficiente per i controller di dominio affinché sia possibile memorizzare nella cache il file di database AD completo.

Si consiglia di distribuire 1 core di catalogo globale di Active Directory per 8 core di cassette postali che gestiscono il carico attivo (in base ai core di catalogo globale a 64 bit).

## Bilanciamento del carico

Tutti i server Accesso client devono ricevere circa lo stesso numero di connessioni in ingresso.

Per tutti i protocolli, Exchange 2013 non richiede affinità di sessione tra un determinato server Accesso client e il bilanciamento del carico.

È necessario utilizzare un dispositivo o software di bilanciamento del carico per gestire tutto il traffico in ingresso per i server Accesso client. La selezione del server di destinazione può essere effettuata in diversi modi, ad esempio "round-robin," in cui ogni connessione in ingresso passa al successivo server di destinazione in un elenco circolare, o con "meno connessioni", in cui il sistema di bilanciamento del carico invia ogni nuova connessione al server per cui è definito il minor numero di connessioni. Questi metodi sono descritti in modo dettagliato più avanti in [Bilanciamento del carico](load-balancing-exchange-2013-help.md). È inoltre necessario valutare gli aspetti seguenti:

  - Round robin ha un problema di convergenza lenta con connessioni di lunga durata (come RPC/HTTP). Quando si connettono nuovi computer, il bilanciamento di connessioni servite nei computer di destinazione richiede molto tempo per convergere.

  - Nel metodo con "meno connessioni", tenere presente che è possibile che un server Accesso client sia sottoposto a overload e non risponda in caso di guasto del server o durante operazioni di manutenzione relative all'applicazione di patch. Nel contesto delle prestazioni di Exchange, l'autenticazione è un'operazione complessa.

A causa di una serie di limitazioni con Bilanciamento carico di rete di Windows in un ambiente con Exchange 2013, illustrate in [Bilanciamento del carico](load-balancing-exchange-2013-help.md), non è consigliabile utilizzare Bilanciamento carico di rete di Windows.

## Distribuzione database e utenti

Mantenere una distribuzione bilanciata di utenti per database e database attivi per server. Distribuire in modo uniforme il consumo dello spazio su disco dei database e bilanciare gli utenti con attività intensa tra tutti i database.

È necessario profilare la base utenti per comprendere come interagiscono con Exchange (dispositivi, Outlook e OWA) e l'impatto che tali interazioni causano a livello di prestazioni. fare riferimento ai blog sullo strumento di calcolo della sezione 2 per ulteriori informazioni su come profilare l'utilizzo di Exchange per utente.

Configurare la preferenza di attivazione della copia di DB e le impostazioni "MaximumPreferredActiveDatabases" (per server) per mantenere il bilanciamento durante un failover o cambio.

Lo script RedistributeActiveDatabases.ps1 consente di ribilanciare i database attivi nei nodi DAG.

Prendere in considerazione l'applicazione di limiti del conteggio elementi di lavoro che corrispondono a Office 365. È possibile eseguire questa operazione con il cmdlet Set-Mailbox e le informazioni fornite in [Limiti cartella delle cassette postali](https://go.microsoft.com/fwlink/p/?linkid=39877).

## File di paging

Impostare le dimensioni massime per il file di paging di 32.778 MB se si usano più di 32 GB di RAM.

Il file di paging non deve essere ospitato nella stessa unità dei file di database Exchange o nei file di log di database.

È fondamentale utilizzare un file di paging di dimensioni fisse e non consentire a Windows di gestire tali dimensioni. Aumentare le dimensioni del file di paging può essere un'attività particolarmente intensa e può causare problemi quando Exchange è sovraccarico.

Se è necessario ottenere un dump del kernel completo, consultare l'articolo 969028 della Microsoft Knowledge Base, [Come generare un kernel o un file di dump della memoria completo in Windows Server 2008 e Windows Server 2008 R2](https://go.microsoft.com/fwlink/p/?linkid=52404), per il file di dump dedicato.

## Modalità di Outlook

Si consiglia la modalità cache. Per capire il vantaggio derivante dall'uso della modalità cache, vedere [Scelta tra modalità cache e modalità online per Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=52404).

È importante notare che le prestazioni possono essere influenzate da componenti aggiuntivi di server e componenti aggiuntivi di terze parti di Outlook. Quando si utilizza la modalità online, i client possono aspettarsi alcuni problemi delle prestazioni dovuti a componenti aggiuntivi di terze parti, conteggi di elementi elevati, visualizzazioni con restrizioni, il numero di utenti che accedono alla cassetta postale, tra gli altri fattori. Nei client legacy possono esserci ulteriori effetti dovuti a conteggi di elementi elevati e prestazioni rispetto a Outlook 2013.

Se un'organizzazione ha configurato Outlook in modalità online principalmente per motivi di sicurezza, prendere in considerazione l'uso di BitLocker.

Outlook 2013 offre la nuova funzionalità del "dispositivo di scorrimento di sincronizzazione" per ridurre al minimo i tempi di download e la dimensione del file OST. Per ulteriori informazioni, fare riferimento a [Configurare la modalità cache di Exchange in Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=39045).

Verificare su base mensile la disponibilità di aggiornamenti dei client di Outlook supportati nell'ambiente in uso.

## Software di terze parti

Come procedura consigliata, disinstallare o disabilitare il software di terze parti durante la risoluzione dei problemi relativi alle prestazioni di Exchange. Nell'elenco seguente sono contenuti i tipi di software di terze parti che il supporto tecnico Microsoft ha più spesso visto influenzare le prestazioni di Exchange 2013.

  - Soluzioni antivirus

  - Software di prevenzione delle intrusioni

  - Software di backup

  - Software di controllo, sia per i file che per gli utenti

  - Soluzioni di archiviazione


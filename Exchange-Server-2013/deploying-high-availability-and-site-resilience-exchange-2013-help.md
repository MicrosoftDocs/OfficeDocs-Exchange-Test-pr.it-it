---
title: 'Distribuzione di elevata disponibilità e resilienza del sito: Exchange 2013 Help'
TOCTitle: Distribuzione di elevata disponibilità e resilienza del sito
ms:assetid: 4c4e00a4-1f57-4fdb-b9b2-2779abf381a9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638129(v=EXCHG.150)
ms:contentKeyID: 50480556
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Distribuzione di elevata disponibilità e resilienza del sito

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Microsoft Exchange Server 2013 utilizza il concetto conosciuto come *distribuzione incrementale* sia per l'elevata disponibilità che per la resilienza del sito. È sufficiente installare due o più server Cassette postali di Exchange 2013 come server autonomi, quindi configurare in modo incrementale i database delle cassette postali per un'elevata disponibilità e resilienza del sito, in base alle necessità.

## Panoramica del processo di distribuzione

Mentre i passi attuali utilizzati da ogni organizzazione possono variare leggermente, l'intero processo di distribuzione di Exchange 2013 durante la configurazione con resilienza del sito o a elevata disponibilità è generalmente lo stesso. Dopo l'esecuzione delle attività di pianificazione e progettazione necessarie per la creazione e distribuzione di un gruppo di disponibilità del database (DAG) e la creazione delle copie del database delle cassette postali, fare quanto segue:

1.  Creare un DAG. Per la procedura dettagliata, vedere [Creare un gruppo di disponibilità del database](create-a-database-availability-group-exchange-2013-help.md).

2.  Se necessario, preinstallare l'oggetto del nome cluster (CNO). È richiesta la pre-installazione del CNO durante la distribuzione di un DAG con server Mailbox eseguendo Windows Server 2012. Se è in corso la distribuzione di un DAG senza un punto di accesso amministrativo utilizzando i server Mailbox eseguendo Windows Server 2012 R2, non è necessario eseguire la pre-installazione di un CNO. La pre-installazione è inoltre richiesta in ambienti in cui la creazione di account del computer è limitata o quando gli account del computer vengono creati in un container diverso da quello predefinito. Per la procedura dettagliata, vedere [Pregestione dell'oggetto nome cluster per un gruppo di disponibilità del database](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

3.  Aggiungere due o più server Cassette postali al DAG. Per la procedura dettagliata, vedere [Gestire l'appartenenza al gruppo di disponibilità del database](manage-database-availability-group-membership-exchange-2013-help.md).

4.  Configurare le proprietà del DAG in base alle esigenze:
    
    1.  Eventualmente, configurare la compressione e la crittografia DAG, la porta per la replica, gli indirizzi IP del DAG e altre proprietà del DAG. Per la procedura dettagliata, vedere [Configurazione delle proprietà del gruppo di disponibilità del database](configure-database-availability-group-properties-exchange-2013-help.md).
    
    2.  Abilitare la modalità di coordinamento dell'attivazione del datacenter (DAC) per il DAG. In questo modo il DAG viene protetto dalle condizioni split brain a livello di database durante lo switchback al datacenter primario dopo che è stato eseguito uno switchover del datacenter e viene consentito l'utilizzo dei cmdlet di ripristino del DAG incorporati. Per ulteriori informazioni, vedere [modalità di coordinamento dell'attivazione del centro dati](datacenter-activation-coordination-mode-exchange-2013-help.md).

5.  Aggiungere copie del database delle cassette postali tra i server Cassette postali nel DAG. Per la procedura dettagliata, vedere [Aggiungere una copia del database delle cassette postali](add-a-mailbox-database-copy-exchange-2013-help.md).

## Distribuzione di esempio: DAG con quattro membri in due datacenter

In questo esempio viene descritto come l'organizzazione Contoso, Ltd. configura e distribuisce un DAG con quattro membri che verrà esteso in due posizioni fisiche: Redmond, Washington e Portland, Oregon.

## Infrastruttura di base

Ogni percorso contiene gli elementi dell'infrastruttura necessari per far funzionare un'infrastruttura di messaggistica basata su Exchange 2013, cioè:

  - I servizi directory (Active Directory o Servizi di dominio di Active Directory)

  - La risoluzione del nome DNS (Domain Name System)

  - Server Accesso client di Exchange 2013 multipli

  - Server Cassette postali Exchange 2013 multipli

Nella figura seguente è illustrata la configurazione Contoso.

**Gruppo di disponibilità del database esteso tra due siti**

![Gruppo di disponibilità del database esteso a due siti](images/Dd638129.1c326fd4-3c7b-4416-a63d-fbfdd0cc6b18(EXCHG.150).gif "Gruppo di disponibilità del database esteso a due siti")

## Configurazione di rete

Come illustrato nella figura precedente, la soluzione include l'utilizzo di più subnet e più reti. Ogni server Cassette postali nel DAG ha due schede di rete su subnet separate. In ogni server Cassette postali, una scheda di rete verrà utilizzata per la rete MAPI (192.168.*x*.*x*) e una scheda di rete verrò utilizzata per la rete di replica (10.0.*x*.*x*). Solo la rete MAPI fornisce la connettività a Active Directory, ai servizi DNS e ad altri server e client Exchange. La scheda utilizzata per la rete di replica in ogni membro fornisce la connettività solo alle schede di rete di replica negli altri membri del DAG.

Le impostazioni per ogni scheda di rete in ogni nodo sono descritte in dettaglio nella tabella seguente.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Indirizzo IPv4</th>
<th>Subnet mask</th>
<th>Gateway predefinito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MBX1 (MAPI)</p></td>
<td><p>192.168.1.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (MAPI)</p></td>
<td><p>192.168.1.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (MAPI)</p></td>
<td><p>192.168.2.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (MAPI)</p></td>
<td><p>192.168.2.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX1 (replica)</p></td>
<td><p>10.0.1.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Nessuna</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (replica)</p></td>
<td><p>10.0.1.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Nessuna</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (replica)</p></td>
<td><p>10.0.2.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Nessuna</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (replica)</p></td>
<td><p>10.0.2.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Nessuna</p></td>
</tr>
</tbody>
</table>


Come illustrato nella tabella precedente, le schede utilizzate per le reti di replica non utilizzano gateway predefiniti. Per fornire la connettività di rete tra tutte le schede di rete di replica, Contoso utilizza route statiche permanenti che eseguono la configurazione mediante lo strumento Netsh.exe.

Per configurare il routing per le schede di rete di replica su MBX1 e MBX2, questo comando veniva eseguito su ogni server.

    netsh interface ipv4 add route 10.0.2.0/24 <NetworkName> 10.0.1.254

Per configurare il routing per le schede di rete di replica su MBX3 e MBX4, questo comando veniva eseguito su ogni server.

    netsh interface ipv4 add route 10.0.1.0/24 <NetworkName> 10.0.2.254

Sono state configurate anche le seguenti impostazioni di rete aggiuntive:

  - La casella di controllo **Registra tale indirizzo di connessione nel DNS** è selezionata per ogni scheda di rete MAPI del membro DAG e deselezionata per ogni scheda di rete di replica.

  - Viene configurato almeno un indirizzo del server DNS configurato per ogni scheda di rete MAPI del membro DAG, mentre non ne viene configurato alcuno per le schede di rete di replica. Per la ridondanza, Contoso utilizza più indirizzi del server DNS per le schede di rete MAPI.

  - Contoso non utilizza Windows Firewall che è disattivato sui server.

Dopo che le schede di rete sono state configurate, Contoso è pronto a creare un DAG e ad aggiungere i server Cassette postali al DAG.

## Creazione e configurazione del gruppo di disponibilità del database

L'amministratore ha deciso di creare uno script dell'interfaccia della riga dei comandi di Windows PowerShell che esegue diverse attività:

  - Viene utilizzato il cmdlet [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd351107\(v=exchg.150\)) per creare il DAG. Dal momento che REDMOND viene considerato il datacenter primario, Contoso ha scelto di utilizzare un server di controllo nello stesso datacenter, cioè, CAS1.

  - Viene utilizzato il cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\)) per preconfigurare un server di controllo alternativo e una directory di controllo alternativa nel caso sia necessario uno switchover del datacenter.

  - Viene utilizzato il cmdlet [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/it-it/library/dd298049\(v=exchg.150\)) per aggiungere ciascuno dei quattro server Cassette postali al DAG.

  - Viene utilizzato il cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\)) per configurare il DAG per la modalità DAC. Per ulteriori informazioni relative alla modalità DAC, vedere [modalità di coordinamento dell'attivazione del centro dati](datacenter-activation-coordination-mode-exchange-2013-help.md).

Di seguito sono riportati i comandi utilizzati nello script:

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer CAS1 -WitnessDirectory C:\DAGWitness\DAG1.contoso.com -DatabaseAvailabilityGroupIPAddresses 192.168.1.8,192.168.2.8

Il comando precedente crea un gruppo di disponibilità del database DAG1, configura CAS1 in modo che funzioni come server di controllo, configura una directory di controllo specifica (C:\\DAGWitness\\DAG1.contoso.com) e configura due indirizzi IP per il DAG (uno per ogni subnet sulla rete MAPI).

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGWitness\DAG1.contoso.com -AlternateWitnessServer CAS4

Il comando precedente configura DAG1 per utilizzare un server di controllo alternativo di CAS4 e una directory di controllo alternativa su CAS4 che utilizza lo stesso percorso configurato su CAS1.


> [!NOTE]
> L'utilizzo dello stesso percorso non è necessario. Contoso ha deciso di standardizzare la configurazione.



    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX3
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX2
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX4

I comandi precedenti aggiungono un server Cassette postali alla volta al DAG. I comandi installano anche il componente clustering di failover di Windows su ogni server Cassette postali (se non è già installato), creano un cluster di failover e aggiungono ogni server Cassette postali al cluster appena creato.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly

Il comando precedente abilità la modalità DAC per il DAG.

## Database delle cassette postali e copie del database delle cassette postali

Dopo aver creato il DAG e aggiunto i server Cassette postali al DAG, Contoso si prepara alla creazione di database delle cassette postali e di copie del database delle cassette postali. Per creare un sistema a prova di errori, Contoso intende configurare ogni database delle cassette postali con tre copie del database non ritardate e una copia del database ritardata. La copia ritardata avrà un ritardo di riesecuzione dei file di registro configurato di tre giorni.

Questa configurazione fornisce un totale di quattro copie per ogni database (una attiva, due passive non ritardate e una passiva ritardata). Contoso intende disporre di quattro database attivi per ciascun server. Con quattro database attivi per ciascun server e tre copie passive di ogni database, la soluzione Contoso contiene in totale 16 copie del database.

Come illustrato nella figura seguente, Contoso desidera ottenere un layout bilanciato dei database.

**Layout della copia del database per Contoso, Ltd**

![Layout della copia del database per Contoso, Ltd](images/Dd638129.41d0c78e-ccaf-4b67-8bab-6fb344668ead(EXCHG.150).gif "Layout della copia del database per Contoso, Ltd")

Ogni server Cassette postali ospita una copia del database delle cassette postali attiva, due copie del database passive non ritardate e una copia del database passiva ritardata. La copia ritardata di ciascun database delle cassette postali attivo è ospitata su un server Cassette postali nell'altro sito.

Per creare questa configurazione, l'amministratore esegue diversi comandi.

In MBX1, eseguire i comandi riportati di seguito.

    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -SuspendComment "Seed from MBX4" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB1\MBX3 -SourceServer MBX4
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -ActivationOnly

In MBX2, eseguire i comandi riportati di seguito.

    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -SuspendComment "Seed from MBX3" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB2\MBX4 -SourceServer MBX3
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -ActivationOnly

In MBX3, eseguire i comandi riportati di seguito.

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -SuspendComment "Seed from MBX2" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB3\MBX1 -SourceServer MBX2
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -ActivationOnly

In MBX4, eseguire i comandi riportati di seguito.

    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX2 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -SuspendComment "Seed from MBX1" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB4\MBX2 -SourceServer MBX1
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -ActivationOnly

Negli esempi precedenti per il cmdlet **Add-MailboxDatabaseCopy**, il parametro *ActivationPreference* non è stato specificato. L'attività aumenta automaticamente il numero della preferenza di attivazione con ogni copia aggiunta. Il numero della preferenza del database originale è sempre 1. Alla prima copia aggiunta con il cmdlet **Add-MailboxDatabaseCopy** viene assegnato automaticamente il numero della preferenza 2. Partendo dal presupposto che nessuna copia viene rimossa, alla successiva copia aggiunta viene assegnato il numero della preferenza 3 e così via. In questo modo, negli esempi precedenti, il numero della preferenza di attivazione della copia passiva nello stesso datacenter della copia attiva è 2; quello della copia passiva non ritardata nel datacenter remoto è 3 e quello della copia passiva ritardata nel datacenter remoto è 4.

Anche se esistono due copie di ogni database attivo nella rete WAN in un altro percorso, il seeding nella rete WAN è stato eseguito solo una volta. Ciò perché Contoso sta sfruttando la capacità di Exchange 2013 di utilizzare una copia passiva di un database come origine del seeding. L'utilizzo del cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd298105\(v=exchg.150\)) con il parametro *SeedingPostponed* impedisce all'attività di eseguire automaticamente il seeding della copia del database appena creata. Quindi, l'amministratore può sospendere la copia priva di seeding e utilizzando il cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)) con il parametro *SourceServer*, può specificare la copia locale del database come origine dell'operazione di seeding. Di conseguenza, il seeding della seconda copia del database aggiunta a ogni percorso si verifica localmente e non nella rete WAN.


> [!NOTE]
> Nell'esempio precedente, viene eseguito il seeding della copia del database non ritardata nella rete WAN e tale copia viene utilizzata per eseguire il seeding della copia ritardata del database che si trova nello stesso datacenter della copia non ritardata.



Contoso ha configurato una copia passiva di ciascun database delle cassette postali come copia del database ritardata per garantire la protezione nel caso si verifichi il danneggiamento logico del database. Di conseguenza, l'amministratore configura le copie ritardate come bloccate per l'attivazione utilizzando il cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd351074\(v=exchg.150\)) con il parametro *ActivationOnly*. In questo modo le copie del database ritardate non verranno attivate se si verifica il failover del server o del database.

## Convalida della soluzione

Dopo aver distribuito e configurato la soluzione, l'amministratore esegue diverse attività che convalidano la conformità della soluzione prima di spostare le cassette postali di produzione nei database del DAG. È necessario verificare la soluzione utilizzando diversi metodi, comprese le simulazioni di errore. Per convalidare la soluzione, l'amministratore esegue diverse attività.

Per verificare lo stato generale del DAG, l'amministratore esegue il cmdlet [Test-ReplicationHealth](https://technet.microsoft.com/it-it/library/bb691314\(v=exchg.150\)). Questo cmdlet controlla diversi aspetti dello stato di riesecuzione e di replica per fornire le informazioni relative a ogni server Cassette postali e alla copia del database nel DAG.

Per verificare le operazioni di riesecuzione e di replica, l'amministratore esegue il cmdlet [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/it-it/library/dd298044\(v=exchg.150\)). Questo cmdlet è in grado di fornire informazioni sullo stato in tempo reale relative a una copia specifica del database delle cassette postali o per tutte le copie del database delle cassette postali su un server specifico. Per ulteriori informazioni relative al monitoraggio dell'integrità e dello stato dei database replicati in un DAG, vedere [Gruppi di disponibilità del database di monitoraggio](monitoring-database-availability-groups-exchange-2013-help.md).

Per verificare che le operazioni di switchover funzionino nel modo previsto, l'amministratore utilizza il cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/it-it/library/dd298068\(v=exchg.150\)) per eseguire una serie di switchover del server e del database. Al termine di queste attività, l'amministratore utilizza lo stesso cmdlet per spostare le copie del database attive nei percorsi originali.

Per verificare i comportamenti previsti in diversi scenari di errore, l'amministratore esegue diverse attività che simulano o causano effettivamente degli errori. Ad esempio, l'amministratore può fare quanto segue:

  - Scollegare il cavo di alimentazione su MBX1, attivando un failover del server. L'amministratore verifica che DB1 diventi attivo su un altro server (preferibilmente MBX2, in base ai valori della preferenza di attivazione).

  - Scollegare il cavo di rete per la scheda di rete MAPI su MBX2, attivando un failover del server. L'amministratore verifica che DB2 diventi attivo su un altro server (preferibilmente MBX1, in base ai valori della preferenza di attivazione).

  - Prendere in modalità offline il disco utilizzato dalla copia attiva di DB3, attivando un failover del database. L'amministratore verifica che DB3 diventi attivo su un altro server (preferibilmente MBX4, in base ai valori della preferenza di attivazione).

Potrebbero esistere altri scenari di errore verificati dall'organizzazione, in base alle esigenze. Dopo aver simulato un errore (ad esempio, tirando il cavo di alimentazione) e verificando il comportamento della soluzione, l'amministratore può ripristinare la configurazione originale della soluzione. In alcuni casi, la soluzione potrebbe essere testata per più errori simultanei. Il piano di verifica della soluzione stabilirà se ripristinare la configurazione originale della soluzione al termine di ogni simulazione di errore.

Inoltre, un amministratore può decidere di interrompere la connessione di rete tra due datacenter, simulando un errore nel sito. L'esecuzione di uno switchover del datacenter è un processo molto più complesso e coordinato; tuttavia è un processo consigliato se la soluzione distribuita è stata progettata per fornire la resilienza del sito per i dati e i servizi di messaggistica.

## Passaggio alla fase operativa

Dopo aver distribuito la soluzione, può essere estesa ulteriormente utilizzando la distribuzione incrementale. A questo punto, la gestione della soluzione passerà alla fase operativa e verranno eseguite queste attività:

  - Monitorare l'integrità e lo stato dei DAG e copie del database delle cassette postali. Per ulteriori informazioni, vedere [Gruppi di disponibilità del database di monitoraggio](monitoring-database-availability-groups-exchange-2013-help.md).

  - Eseguire switchover dei database secondo necessità. Per ulteriori informazioni sull'esecuzione di uno switchover del database, vedere [Attivare una copia del database delle cassette postali](activate-a-mailbox-database-copy-exchange-2013-help.md).

Per ulteriori informazioni sulla gestione della soluzione, vedere [Gestione di elevata disponibilità e resilienza del sito](managing-high-availability-and-site-resilience-exchange-2013-help.md).


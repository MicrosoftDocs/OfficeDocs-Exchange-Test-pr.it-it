---
title: 'Virtualizzazione di Exchange 2013: Exchange 2013 Help'
TOCTitle: Virtualizzazione di Exchange 2013
ms:assetid: 36184b2f-4cd9-48f8-b100-867fe4c6b579
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619301(v=EXCHG.150)
ms:contentKeyID: 50480333
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Virtualizzazione di Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-08-08_

È possibile distribuire Microsoft Exchange Server 2013 in un ambiente virtualizzato. In questo argomento sono disponibili informazioni generali sugli scenari supportati per la distribuzione di Exchange 2013 su software di virtualizzazione dell'hardware.

**Sommario**

Requirements for hardware virtualization

Host machine storage requirements

Exchange storage requirements

Exchange memory requirements and recommendations

Host-based failover clustering and migration for Exchange

In questa descrizione della virtualizzazione di Exchange vengono utilizzati i seguenti termini:

  - **Avvio a freddo**   Quando si avvia un sistema operativo partendo da un sistema spento, l'azione viene definita un *avvio a freddo*. In questo caso non persiste alcuno stato del sistema operativo.

  - **Stato salvato**   Quando viene spenta una macchina virtuale, gli hypervisor in genere possono salvare lo stato della macchina virtuale, in modo che alla riattivazione venga ripristinato lo *stato salvato*, anzichè lo stato derivante da un avvio a freddo.

  - **Migrazione pianificata**   Se un amministratore di sistema inizia lo spostamento di una macchina virtuale da un host hypervisor all'altro, l'azione è definita *migrazione pianificata*. L'azione può corrispondere a una migrazione singola, ma l'amministratore di sistema può inoltre configurare l'automazione per spostare la macchina virtuale con intervalli pianificati. Una migrazione pianificata può inoltre essere il risultato di eventi che si verificano nel sistema, nonché di errori hardware o software. Il punto è che la macchina virtuale di Exchange opera normalmente e deve essere riposizionata per qualche motivo. Questo riposizionamento può essere eseguito tramite una tecnologia come Live Migration o vMotion. Tuttavia, se la macchina virtuale di Exchange o l'host hypervisor su cui si trova la macchina virtuale è in una condizione di errore, il risultato non presenta le caratteristiche di una migrazione pianificata.

## Requisiti per la virtualizzazione hardware

Microsoft supporta Exchange 2013 nella produzione con software di virtualizzazione dell'hardware solo se vengono soddisfatte tutte le seguenti condizioni:

  - Il software di virtualizzazione dell'hardware esegue uno dei seguenti software:
    
      - Qualsiasi versione di Windows Server con tecnologia Hyper-V o Microsoft Hyper-V Server
    
      - Qualsiasi hypervisor di terze parti che è stato convalidato in [Windows Server Virtualization Validation Program](https://go.microsoft.com/fwlink/p/?linkid=125375).
    

    > [!NOTE]
    > Distribuzione di Exchange 2013 con provider di infrastruttura-as-a-Service (IaaS) è supportata se sono soddisfatti tutti i requisiti di supporto. Nel caso di provider che provisioning di macchine virtuali, questi requisiti includono verificando che hypervisor utilizzato per le macchine virtuali di Exchange è completamente supportata e che l'infrastruttura per essere utilizzata dal Exchange soddisfi i requisiti di prestazioni sono stati determinati durante il processo di ridimensionamento. Distribuzione di macchine virtuali di Microsoft Azure è supportata se tutti i volumi di archiviazione utilizzato per i database di Exchange e registri delle transazioni del database (compresi i database di trasporto) sono configurati per l'archiviazione Premium di Azure.



  - Il computer virtuale guest Exchange ha le seguenti condizioni:
    
      - Utilizza Exchange 2013.
    
      - Viene distribuito su Windows Server 2008 R2 SP1 (o versioni successive), Windows Server 2012 o su Windows Server 2012 R2.

Per le distribuzioni di Exchange 2013:

  - Tutti i ruoli dei server di Exchange 2013 sono supportati in una macchina virtuale.

  - Le macchine virtuali del server Exchange (comprese le macchine virtuali con ruolo Cassette postali di Exchange che fanno parte di un gruppo di disponibilità del database) possono essere combinate con la tecnologia di migrazione e clustering di failover basata su host, purché le macchine virtuali siano configurate in modo tale da non salvare e ripristinare lo stato su disco dopo uno spostamento o il passaggio alla modalità offline. Tutte le attività di failover che si verificano a livello di hypervisor devono generare un avvio a freddo quando la macchina virtuale viene attivata sul nodo di destinazione. La migrazione pianificata deve provocare un arresto e un avvio a freddo, o una migrazione online che utilizza una tecnologia come Hyper-V Live Migration. La migrazione hypervisor delle macchine virtuali è supportata dal fornitore dell'hypervisor; pertanto è necessario assicurarsi che tale fornitore abbia testato e supporti la migrazione delle macchine virtuali di Exchange. Microsoft supporta la migrazione Hyper-V Live Migration di queste macchine virtuali.

  - Solo il software di gestione (ad esempio software antivirus, di backup o di gestione della macchina virtuale) può essere distribuito sul computer host fisico. Nessun'altra applicazione basata su server (ad esempio Exchange, SQL Server, Active Directory o SAP) deve essere installata sul computer host. Il computer host deve essere dedicato all'esecuzione di macchine virtuali guest.

  - Alcuni hypervisor includono funzionalità per l'esecuzione di istantanee delle macchine virtuali. Tali istantanee acquisiscono lo stato di una macchina virtuale mentre questa è in esecuzione. Questa funzionalità consente di eseguire più istantanee di una macchina virtuale e quindi di ripristinarla a uno stato precedente applicandovi una determinata istantanea. Tuttavia, le istantanee delle macchine virtuali non sono in grado di rilevare le applicazioni, pertanto il loro utilizzo può portare a conseguenze impreviste e indesiderate per un'applicazione server che gestisce dati di stato, come ad esempio Exchange. Di conseguenza, l'esecuzione di istantanee di una macchina virtuale guest di Exchange non è supportata.

  - Molti prodotti per la virtualizzazione hardware consentono di specificare il numero di processori virtuali che dovrebbero essere assegnate a ogni macchina virtuale guest. I processori virtuali nella macchina virtuale guest condividano un numero fisso di core di elaborazione fisica del sistema fisico. Exchange supporta un rapporto di base del processore virtuale processore-fisici non superiore a 2:1, sebbene sia consigliabile un rapporto di 1:1. Ad esempio un sistema doppio processore con processori quad-core contiene un totale di 8 core fisici nel sistema host. In un sistema con questa configurazione non più di un totale di 16 processori virtuali per tutte le macchine virtuali guest combinate allocare.

  - Quando si calcola il numero totale di processori virtuali richiesti dal computer host, occorre tenere in considerazione sia i requisiti di I/O che quelli del sistema operativo. Nella maggioranza dei casi, il numero equivalente di processori virtuali richiesti nel sistema operativo host per un sistema che ospita macchine virtuali Exchange è 2. Questo valore deve essere utilizzato come riferimento per il processore virtuale del sistema operativo host quando si calcola il rapporto complessivo tra core fisici e processori virtuali. Se il monitoraggio delle prestazioni del sistema operativo host indica che l'utilizzo del processore è superiore all'equivalente di 2 processori, è necessario ridurre in maniera corrispondente il numero di processori virtuali assegnati alle macchine virtuali guest e verificare che il rapporto complessivo tra processori virtuali e core fisici non sia superiore a 2:1.

  - Il sistema operativo per una macchina guest di Exchange deve utilizzare un disco con dimensione minima pari ad almeno 15 GB più la dimensione della memoria virtuale assegnata alla macchina guest. Tale requisito è indispensabile per soddisfare le esigenze di spazio su disco relative al sistema operativo e al file di paging. Ad esempio, se alla macchina guest sono stati assegnati 16 GB di memoria, lo spazio minimo su disco necessario per il disco del sistema operativo guest è pari a 31 GB.
    
    Inoltre, è possibile che alle macchine virtuali guest venga impedito di comunicare direttamente con schede bus host (HBA) Fibre Channel o SCSI installate sul computer host. In questo caso, è necessario configurare le schede nel sistema operativo del computer host e presentare i numeri di unità logica (LUN) alle macchine virtuali guest come disco virtuale o come disco pass-through.

  - L'unico metodo supportato per inviare messaggi di posta elettronica a domini esterni da Azure compute risorse è tramite un relay SMTP (noto anche come un SmartHost SMTP). La risorsa Azure compute Invia messaggio di posta elettronica per l'inoltro SMTP e quindi il provider di inoltro SMTP recapita il messaggio di posta elettronica al dominio esterno. Microsoft Exchange Online Protection è un provider di inoltro SMTP, ma un numero di provider di terze parti anche. Per ulteriori informazioni, vedere il blog del Team di Microsoft Azure supporto post [L'invio di posta elettronica da Azure Compute risorse per i domini esterni](https://go.microsoft.com/fwlink/p/?linkid=799723).

Inizio pagina

## Requisiti di archiviazione per il computer host

I requisiti di spazio su disco minimo per ogni computer host sono i seguenti:

  - Computer host di alcune applicazioni di virtualizzazione dell'hardware può richiedere lo spazio di archiviazione per un sistema operativo e dei relativi componenti. Ad esempio, quando si esegue Windows Server 2008 R2 con Hyper-V, è necessario almeno 10 GB per soddisfare i requisiti per Windows Server 2008. Per ulteriori informazioni, vedere [Requisiti di sistema di Windows Server 2008 R2](https://go.microsoft.com/fwlink/p/?linkid=125378). Ulteriore spazio di archiviazione è inoltre necessaria per supportare i file di paging del sistema operativo, il software di gestione e bloccarsi dei file di recupero (dump).

  - Alcuni hypervisor mantengono sul computer host file univoci per ogni macchina virtuale guest. Ad esempio, in un ambiente Hyper-V viene creato e mantenuto per ogni macchina guest un file di archiviazione temporaneo (file BIN). La dimensione di ciascun file BIN è pari alla quantità di memoria assegnata alla macchina guest. È possibile, inoltre, che nella macchina host vengano creati e mantenuti altri file per ogni macchina guest.

  - Esegue il computer host Hyper-V 2012 o Windows Server 2012 Hyper-V, se si sta configurando un cluster di failover basato su host che ospiterà il server cassette postali Exchange in un gruppo di disponibilità del database, è consigliabile seguenti le linee guida descritte Nell'articolo della Microsoft Knowledge Base, [2872325, Cluster Guest Hyper-V i nodi potrebbero non essere in grado di creare o partecipare a](https://support.microsoft.com/kb/2872325).

Inizio pagina

## Requisiti di archiviazione di Exchange

I requisiti di archiviazione relativi a un server di Exchange virtualizzato sono i seguenti:

  - A ogni macchina guest di Exchange deve essere assegnato uno spazio di archiviazione sufficiente sul computer host per il disco fisso contenente il sistema operativo guest, eventuali file di archiviazione della memoria temporanea in uso e i file della macchina virtuale correlata ospitati nel computer host. Inoltre, per ogni macchina guest di Exchange, è necessario allocare uno spazio di archiviazione sufficiente per contenere le code dei messaggi e uno spazio sufficiente per i database e i file di registro presenti nei server Cassette postali.

  - La memoria utilizzata da un computer guest Exchange per la memorizzazione dei dati Exchange (ad esempio, database delle cassette postali e code di trasporto) può essere archiviazione virtuali di dimensioni fisse (ad esempio i dischi rigidi virtuali (VHD o VHDX) in un ambiente Hyper-V), archiviazione virtuali dinamica quando si utilizzano file VHDX con Hyper-V, archiviazione pass-through SCSI o archiviazione iSCSI (Internet SCSI). L'archiviazione pass-through è archiviazione sia configurata a livello di host e dedicato alla macchina uno guest. Tutti i archiviazione utilizzata da un computer guest Exchange per l'archiviazione dei dati Exchange deve essere blocco a livello di archiviazione perché Exchange 2013 non supporta l'utilizzo di network attached storage (NAS) volumi, diverso da quello nello scenario relativo a SMB 3.0 descritti più avanti in questo argomento. Inoltre, archiviazione NAS presentato agli guest come archiviazione a livello di blocco tramite hypervisor non è supportata.

  - Fissi o dinamici dischi virtuali possono essere archiviati in file SMB 3.0 che sono supportati da archiviazione a livello di blocco se la macchina guest è in esecuzione in Windows Server 2012 Hyper-V (o versione successiva di Hyper-V). Supportato esclusivamente l'utilizzo di 3.0 SMB condivisioni di file sia per la memorizzazione dei dischi virtuali fissi o dinamici. Tali condivisioni di file non possono essere utilizzate per l'archiviazione diretta dei dati Exchange. Quando si utilizzano le condivisioni di file SMB 3.0 per archiviare i dischi virtuali fissi o dinamici, la condivisione di file l'archiviazione deve essere configurato per la disponibilità elevata garantire la migliore disponibilità possibili del servizio di Exchange.

  - Il sistema di archiviazione utilizzato da Exchange deve essere ospitato in assi di disco separati dal sistema di archiviazione che ospita il sistema operativo della macchina virtuale guest.

  - La configurazione dell'archiviazione iSCSI per l'utilizzo di un iniziatore iSCSI all'interno di una macchina virtuale guest di Exchange è supportata. Tuttavia, con questa configurazione le prestazioni vengono ridotte se lo stack di rete all'interno della macchina virtuale non è completo (ad esempio, non tutti gli stack di rete virtuali supportano i frame jumbo).

Inizio pagina

## Requisiti di memoria e consigli per Exchange

Alcuni hypervisor hanno la possibilità di riservare o regolare dinamicamente la quantità di memoria disponibile per una macchina guest specifica basandosi sulla rilevazione dell'utilizzo di memoria percepito di quella macchina comparata alle esigenze delle altre macchine guest gestite dallo stesso hypervisor. Questa tecnologia è efficace nei carichi di lavoro in cui la memoria è necessaria per brevi periodi e può essere sottratta ad altri usi. Tuttavia, non può essere efficace per carichi di lavoro in cui l'utilizzo della memoria è previsto su base continuativa. Exchange, così come molte applicazioni server in cui l'ottimizzazione delle prestazioni prevede la memorizzazione nella cache dei dati in memoria, può causare una riduzione delle prestazioni del sistema e risultare inaccettabile per i client se non ha il pieno controllo dell'allocazione della memoria alle macchine fisiche o virtuali sulle quali è in esecuzione. Di conseguenza, l'utilizzo di funzionalità di memoria dinamica per Exchange non è supportato.

Inizio pagina

## Migrazione e clustering di failover basato su host per Exchange

Di seguito, sono riportate le risposte ad alcune domande frequenti sulla tecnologia di migrazione e clustering di failover basato su host con i gruppi di disponibilità del database di Exchange 2013:

  - **Microsoft supporta la tecnologia di migrazione di terze parti?**
    
    Microsoft non è in grado di supportare l'integrazione di prodotti hypervisor di terze parti che utilizzano queste tecnologie con Exchange, dal momento che tali tecnologie non sono parte del programma SVVP (Server Virtualization Validation Program). Il programma SVVP copre gli altri aspetti del supporto di Microsoft per gli hypervisor di terze parti. È necessario verificare che il fornitore dell'hypervisor supporti la combinazione della sua tecnologia di migrazione e clustering con Exchange. Se il fornitore dell'hypervisor supporta la relativa tecnologia di migrazione con Exchange, Microsoft supporterà Exchange con tale tecnologia di migrazione.

  - **Come viene definito da Microsoft il clustering di failover basato su host?**
    
    Il clustering di failover basato su host indica una qualsiasi tecnologia che fornisce la capacità di reagire automaticamente agli errori a livello di host e di avviare le macchine virtuali interessate su server alternativi. L'utilizzo di questa tecnologia è supportato purché, in caso di errore, la macchina virtuale venga avviata a freddo sull'host alternativo. Questa tecnologia aiuta a garantire che la macchina virtuale non venga mai riattivata da uno stato salvato conservato su disco, perché risulterebbe obsoleto rispetto agli altri membri del gruppo di disponibilità del database.

  - **Che cosa intende Microsoft per supporto della migrazione?**
    
    Per tecnologia di migrazione si intende una qualsiasi tecnologia che consente lo spostamento pianificato di una macchina virtuale da una macchina host all'altra. Lo spostamento può anche essere automatizzato e avvenire durante un bilanciamento del carico delle risorse, ma non è correlato a un errore nel sistema. Le migrazioni sono supportate finché le macchine virtuali non vengono riattivate da uno stato salvato su disco. In pratica, per l'utilizzo con Exchange è supportata la tecnologia che sposta una macchina virtuale trasportando lo stato e la memoria della macchina stessa sulla rete senza tempi di inattività percepiti. Un fornitore di hypervisor di terze parti deve fornire il supporto per la tecnologia di migrazione, mentre Microsoft fornisce il supporto per Exchange se utilizzato in questa configurazione.

Inizio pagina


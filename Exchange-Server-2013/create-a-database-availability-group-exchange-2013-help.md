---
title: 'Creare un gruppo di disponibilità del database: Exchange 2013 Help'
TOCTitle: Creare un gruppo di disponibilità del database
ms:assetid: d6b98299-e203-488b-af73-50753fe152c8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351172(v=EXCHG.150)
ms:contentKeyID: 50481775
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un gruppo di disponibilità del database

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-07_

Un gruppo di disponibilità del database (DAG) è un insieme di 16 server Cassette postali Microsoft Exchange Server 2013 che fornisce il ripristino automatico a livello di database da un errore del database, del server o della rete. Quando un server Cassette postali viene aggiunto a un DAG, collabora con gli altri server nel DAG per fornire il ripristino automatico a livello di database da errori di database, server e rete.

Per informazioni sulle altre attività di gestione relative ai gruppi di disponibilità del database? vedere [Gestione dei gruppi di disponibilità del database](managing-database-availability-groups-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di disponibilità del database" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Quando si crea un DAG con i server Cassette postali su cui è in esecuzione Windows Server 2012, è necessario pregestire l'oggetto nome cluster (CNO) prima di aggiungere membri al DAG. Se si sta creando un DAG senza un punto di accesso amministrativo con i server di cassette postali che eseguono Windows Server 2012 R2, non è necessario pregestire l'oggetto nome cluster (CNO) per il DAG. Per la procedura dettagliata, vedere [Pregestione dell'oggetto nome cluster per un gruppo di disponibilità del database](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

  - Quando si crea un DAG, è necessario specificare un nome univoco per il DAG (massimo 15 caratteri). Oltre a fornire un nome per il DAG, è anche necessario assegnare uno o più indirizzi IP (IPv4 o IPv4 e IPv6) al DAG, a meno che non si stia creando un DAG di Windows Server 2012 R2 senza un punto di accesso amministrativo e non si stiano assegnando indirizzi IP al DAG. Altrimenti, gli indirizzi IP assegnati devono trovarsi sulla subnet prevista per la rete MAPI e devono essere disponibili per l'uso. Se si specificano uno o più indirizzi IPv4 e il sistema è configurato per utilizzare IPv6, l'operazione tenterà di assegnare automaticamente al DAG uno o più indirizzi IPv6.

  - Quando si crea un DAG, è possibile specificare un server e una directory di controllo. Se non si specifica un server di controllo, è consigliabile utilizzare un server Accesso client in cui non sia installato il ruolo del server Cassette postali. In questo modo gli amministratori di Exchange possono conoscere la disponibilità del controllo e viene garantito che tutte le autorizzazioni di protezione necessarie per l'utilizzo del server di controllo sono predisposte.
    
    Sono disponibili le seguenti combinazioni di opzioni e comportamenti:
    
      - È possibile specificare solo un nome per il DAG e lasciare i campi **Server di controllo** e **Directory di controllo** vuoti. In questo scenario l'attività effettua una ricerca di un server Accesso client in cui non è installato il ruolo del server Cassette postali. Verranno create automaticamente la directory di controllo e la condivisione nel server Accesso client e verrà configurato il DAG per utilizzare il server come server di controllo.
    
      - È possibile specificare un nome per il DAG, il server di controllo che si desidera utilizzare e la directory che si desidera creare e condividere sul server di controllo.
    
      - È possibile specificare un nome per il DAG e il server di controllo che si desidera utilizzare e lasciare il campo **Directory di controllo** vuoto. In questo scenario, l'attività creerà la directory di controllo predefinita sul server di controllo specificato.
    
      - È possibile specificare un nome per il DAG, lasciare il campo **Server di controllo** vuoto e specificare la directory che si desidera creare e condividere sul server di controllo. In questo scenario, la procedura guidata cercherà un server Accesso client in cui non è installato il ruolo del server Cassette postali e creerà automaticamente la directory di controllo specificata su quel server, condividerà la directory e configurerà il DAG all'utilizzo del server Accesso client come server di controllo.
    

    > [!IMPORTANT]
    > Se il server di controllo specificato non è un server Exchange 2013 o Exchange&nbsp;2010, è necessario aggiungere il gruppo di protezione universale sottosistema Trusted Exchange al gruppo Administrators locale nel server di controllo. Queste autorizzazioni di sicurezza sono necessarie per garantire che Exchange consente di creare una directory e condividere sul server di controllo in base alle esigenze. Se non sono configurate le autorizzazioni appropriate, viene restituito l'errore seguente:<BR><CODE>Error: An error occurred during discovery of the database availability group topology. Error: An error occurred while attempting a cluster operation. Error: Cluster API "AddClusterNode() (MaxPercentage=12) failed with 0x80070005. Error: Access is denied."</CODE>



  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Creazione di un gruppo di disponibilità del database tramite EAC

1.  In Interfaccia di amministrazione di Exchange, accedere a **Server** \> **Gruppi di disponibilità del database**.

2.  Fare clic su ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per creare un DAG.

3.  
    
    Nella pagina **Nuovo gruppo di disponibilità del database** specificare le seguenti informazioni per il DAG:
    
      - **Nome del gruppo di disponibilità del database**   Utilizzare questo campo per digitare un nome valido e univoco per il DAG, utilizzando al massimo 15 caratteri. Il nome è equivalente a un nome di computer, pertanto in Active Directory verrà creato un oggetto di rete cluster (CNO) con quel nome. Il nome corrisponde sia al nome del DAG che al nome del cluster sottostante.
    
      - **Server di controllo**   Utilizzare questo campo per specificare un server di controllo per il DAG. Se si lascia il campo vuoto, verrà tentata la selezione automatica di un server Accesso client nel sito di Active Directory locale non installato in un computer con il server Cassette postali da utilizzare come server di controllo.
        

        > [!NOTE]
        > Se si specifica un server di controllo, è necessario utilizzare un nome host o un nome di dominio completo (FQDN). L'uso di un indirizzo IP o di un nome con caratteri jolly non è supportato. Inoltre, il server di controllo non può essere un membro del DAG.

    
      - **Directory di controllo**   Utilizzare questo campo per digitare il percorso di una directory nel server di controllo che verrà utilizzato per memorizzare i dati di controllo. Se la directory non esiste, il sistema la creerà automaticamente sul server di controllo. Se si lascia il campo vuoto, verrà creata la directory predefinita (%SystemDrive%\\DAGFileShareWitnesses\\\<DAG FQDN\>) sul server di controllo.
    
      - **Indirizzi IP del gruppo di disponibilità del database**   Utilizzare questo campo per assegnare uno o più indirizzi IPv4 statici al DAG. Inserire un indirizzo IPv4 e fare clic su ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungerlo. Lasciare il campo vuoto se si desidera che il DAG utilizzi il protocollo DHCP (Dynamic Host Configuration Protocol) per ottenere gli indirizzi IPv4 necessari. In alternativa, immettere 255.255.255.255 per creare un DAG senza un indirizzo IP o un punto di accesso amministrativo cluster, valido soltanto per i DAG che contengono i server di cassette postali che eseguono Windows Server 2012 R2.

4.  Fare clic su **Salva** per creare il DAG.

## Utilizzare la shell per creare un gruppo di disponibilità del database

Con questo esempio viene creato il DAG DAG1 configurato per utilizzare il server di controllo FILESRV1 e la directory locale C:\\DAG1. DAG1 viene inoltre configurato per utilizzare DHCP per gli indirizzi IP del DAG.

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer FILESRV1 -WitnessDirectory C:\DAG1

Questo esempio crea un DAG denominato DAG2. Il sistema seleziona automaticamente il server Accesso client nel sito locale di Active Directory che non contiene il ruolo server di cassetta postale come server di controllo del DAG. A DAG2 è assegnato un singolo indirizzo IP statico in quanto, in questo esempio, la rete MAPI di tutti i membri del DAG si trova nella stessa subnet.

    New-DatabaseAvailabilityGroup -Name DAG2 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

Questo esempio crea un DAG denominato DAG3. DAG3 è configurato per utilizzare un server di controllo MBX2 e una directory locale C:\\DAG3. A DAG3 vengono assegnati più indirizzi IP statici, perché le reti MAPI dei relativi membri DAG si trovano in subnet diverse.

    New-DatabaseAvailabilityGroup -Name DAG3 -WitnessServer MBX2 -WitnessDirectory C:\DAG3 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,192.168.0.8

Con questo esempio viene creato il DAG DAG4 configurato per utilizzare DHCP. Inoltre, il server di controllo verrà selezionato automaticamente dal sistema e verrà creata la directory predefinita del server di controllo.

    New-DatabaseAvailabilityGroup -Name DAG4

In questo esempio viene creato il DAG DAG5 che non avrà un punto di accesso amministrativo (valido solo per i DAG di Windows Server 2012 R2). Inoltre, MBX4 verrà utilizzato come server di controllo per il DAG e verrà creata la directory di controllo predefinita.

    New-DatabaseAvailabilityGroup -Name DAG5 -DatabaseAvailabilityGroupIPAddresses ([System.Net.IPAddress]::None) -WitnessServer MBX4

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la creazione corretta di un DAG, effettuare una delle operazioni seguenti:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Gruppi di disponibilità del database**. Verrà visualizzato il DAG appena creato.

  - In Shell eseguire il comando seguente per verificare la creazione del DAG e visualizzare le informazioni sulle proprietà relative.
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## Ulteriori informazioni

[Gruppi di disponibilità dei database (DAG)](database-availability-groups-dags-exchange-2013-help.md)

[Configurazione delle proprietà del gruppo di disponibilità del database](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\))

[New-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd351107\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/it-it/library/dd335225\(v=exchg.150\))

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/it-it/library/dd298049\(v=exchg.150\))


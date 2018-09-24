---
title: 'Macch. virt. Azure Microsoft come server di controllo DAG: Exchange 2013 Help'
TOCTitle: Utilizzo di una macchina virtuale Azure Microsoft come server di controllo del DAG
ms:assetid: 03d1e215-518b-4b48-bfcd-8d187ff8f5ef
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn903504(v=EXCHG.150)
ms:contentKeyID: 63892226
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzo di una macchina virtuale Azure Microsoft come server di controllo del DAG

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Exchange Server 2013 modo è possibile configurare i database delle cassette postali in un gruppo di disponibilità del database (DAG) per il failover automatico datacenter. Questa configurazione è necessario tre posizioni fisiche separate: due datacenter per server cassette postali e una terza posizione in cui collocare il server di controllo per il DAG. Le organizzazioni con solo due posizioni fisiche ora possono usufruire di failover automatico datacenter utilizzando una macchina virtuale di Microsoft Azure file server che funga da server di controllo del DAG.

In questo articolo viene descritto il posizionamento del controllo del DAG in Microsoft Azure e si presume che hanno familiarità con i concetti di resilienza dei siti e già dispongono di un'infrastruttura di disponibilità del database completamente funzionante che si estende su due datacenter. Se si dispone già configurato l'infrastruttura di disponibilità del database, è consigliabile leggere gli articoli seguenti:

[Disponibilità elevata e resilienza del sito](high-availability-and-site-resilience-exchange-2013-help.md)

[Gruppi di disponibilità dei database (DAG)](database-availability-groups-dags-exchange-2013-help.md)

[Pianificazione della disponibilità elevata e della resilienza del sito](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)

## Modifiche apportate a Microsoft Azure

Questa configurazione richiede una connessione VPN con più siti. È sempre stato possibile connettere Microsoft Azure utilizzando una connessione VPN da sito della rete aziendale. In passato, tuttavia, Azure supportata solo una rete VPN del sito a sito singola. Poiché la configurazione di un DAG e il controllo tra tre datacenter obbligatorio VPN da sito più, posizionamento del controllo del DAG in una macchina virtuale Azure non è stato inizialmente possibile.

Giugno 2014, Microsoft Azure introdotto il supporto di più siti VPN, che le organizzazioni a cui connettersi alla stessa rete virtuale Azure più centri dati abilitata. Questa modifica anche consentito per le organizzazioni con due datacenter utilizzare Microsoft Azure come percorso terzo posizionare i server di controllo del DAG. Per ulteriori informazioni sulla funzionalità multi-sito VPN in Azure, vedere [configurare una connessione VPN multisito](http://go.microsoft.com/fwlink/?linkid=522621).


> [!NOTE]
> Questa configurazione si basa su una rete VPN multisita e macchine virtuali Azure per la distribuzione di server di controllo e non utilizza il server di controllo Cloud di Azure.



## Controllo server file Microsoft Azure

Nel diagramma seguente viene fornita una panoramica dell'utilizzo di un server di file di Microsoft Azure VM di controllo DAG. È necessario disporre di una rete virtuale Azure, una rete VPN multisita cui i Data Center si connette alla rete virtuale Azure e un controller di dominio e un file server distribuiti nelle macchine virtuali Azure.


> [!NOTE]
> È possibile tecnicamente utilizzare una singola macchina virtuale Azure per questo scopo ed effettuare la condivisione di file controllo nel controller di dominio. Tuttavia, il risultato è l'elevazione dei privilegi non necessari. Pertanto, non è una configurazione consigliata.



**Server di controllo del DAG in Microsoft Azure**

![Panoramica sul controllo DAG di Exchange in Azure](images/Dn903504.7cbda882-bbae-4be7-b0ea-60947b8aa4ef(EXCHG.150).png "Panoramica sul controllo DAG di Exchange in Azure")

Come prima cosa che è necessario eseguire per utilizzare una macchina virtuale Azure Microsoft per il controllo del DAG è possibile ottenere una sottoscrizione. Vedere [come acquistare Azure](http://go.microsoft.com/fwlink/?linkid=398989) per il sistema ideale per acquistare una sottoscrizione di Azure.

Dopo aver ottenuto l'abbonamento Azure, è necessario eseguire le operazioni seguenti nell'ordine indicato:

1.  Preparare la rete virtuale a Microsoft Azure

2.  Configurare una connessione VPN con più siti

3.  Configurazione di macchine virtuali

4.  Configurare il controllo del DAG


> [!NOTE]
> Gran parte delle istruzioni contenute in questo articolo comporta la configurazione di Microsoft Azure. Collegamenti alla documentazione per Azure pertanto, viene utilizzato ogni volta che è applicabile.



## Prerequisiti

  - Due Data Center in grado di supportare una distribuzione di resilienza Exchange siti e disponibilità elevata. Vedere [Pianificazione della disponibilità elevata e della resilienza del sito](planning-for-high-availability-and-site-resilience-exchange-2013-help.md) per ulteriori informazioni

  - Un indirizzo IP pubblico che non è dietro NAT per il gateway VPN in ciascun sito

  - Dispositivo VPN in ogni sito in cui è compatibile con Microsoft Azure. Per ulteriori informazioni sui dispositivi compatibili, vedere [Informazioni sui dispositivi VPN per rete virtuale](http://go.microsoft.com/fwlink/?linkid=522619)

  - Conoscenza del linguaggio concetti di disponibilità del database e gestione

  - Certa familiarità con Windows PowerShell

## Fase 1: Preparare la rete virtuale Microsoft Azure

Configurazione della rete Microsoft Azure è la parte più importante del processo di distribuzione. Al termine di questa fase, è necessario utilizzare una rete virtuale Azure completamente funzionante connesso alle due datacenter tramite una rete VPN più siti.

## Registrare i server DNS

Poiché questa configurazione richiede la risoluzione dei nomi tra i server locali e macchine virtuali di Azure, è necessario configurare Azure per l'utilizzo di server DNS. [La risoluzione dei nomi (DNS Domain)](http://msdn.microsoft.com/en-us/library/azure/jj156088.aspx) argomento fornisce una panoramica della risoluzione dei nomi in Azure.

Eseguire le operazioni seguenti per registrare i server DNS:

1.  Nel portale di Azure, accedere alle **reti** e quindi scegliere **Nuovo**.

2.  Fare clic su **servizi di rete** \> **rete virtuale** \> **registrare SERVER DNS**.

3.  Digitare il nome e indirizzo IP del server DNS. Il nome specificato qui è il nome logico utilizzato nel portale di gestione e non deve corrispondere al nome effettivo del server DNS.

4.  Ripetere i passaggi da 1 a 3 per eventuali altri server DNS che si desidera aggiungere.
    

    > [!NOTE]
    > I server DNS che registrazione non vengono utilizzati in modalità round robin. Macchine virtuali Azure utilizzeranno il primo server DNS elencato e utilizzeranno eventuali server aggiuntivi solo se il primo non è disponibile.



5.  Ripetere i passaggi da 1 a 3 per aggiungere l'indirizzo IP che verrà utilizzato per il controller di dominio che verrà distribuito in Microsoft Azure.

## Creare locale oggetti di rete (locale) in Azure

Successivamente, eseguire le operazioni seguenti per creare gli oggetti di rete logica che rappresentano i Data Center in Microsoft Azure:

1.  Nel portale Azure e quindi passare a **rete** e quindi **Nuovo**.

2.  Fare clic su **servizi di rete** \> **rete virtuale** \> **Aggiungi rete locale**.

3.  Digitare il nome per il primo sito del Data Center e l'indirizzo IP del dispositivo VPN di tale sito. Questo indirizzo IP deve essere un indirizzo IP statico pubblico che non è controllato dal NAT.

4.  Nella schermata successiva, specificare le subnet IP per il primo sito.

5.  Ripetere i passaggi 1through 4 per il secondo sito.

## Creare la rete virtuale Azure

A questo punto, eseguire il cmdlet seguente per creare una rete virtuale Azure che verrà utilizzata per le macchine virtuali:

1.  Nel portale di Azure, accedere alle **reti** e fare clic su **Nuovo**.

2.  Fare clic su **servizi di rete** \> **rete virtuale** \> **Crea personalizzato**.

3.  Nella pagina **Dettagli sulla rete virtuale**, specificare un nome per la rete virtuale e selezionare una posizione geografica per la rete.

4.  Nella pagina **server DNS e connettività VPN** verificare server DNS, sono elencati i server DNS che è registrato in precedenza.

5.  Selezionare la casella di controllo **Configura una connessione VPN da sito** sotto **La connettività da sito**.
    

    > [!IMPORTANT]
    > Non selezionare <STRONG>Usa ExpressRoute</STRONG> perché questo modo si eviteranno le modifiche necessarie configurazione necessarie per configurare una connessione VPN con più siti.



6.  In **Rete locale**, selezionare una delle due reti locali che è stato configurato.

7.  Nella pagina **Spazi indirizzo rete virtuali**, specificare l'intervallo di indirizzi IP che verrà utilizzato per la rete virtuale Azure.

## Checkpoint: Verifica della configurazione di rete

A questo punto, quando si passa alla **rete**, è consigliabile vedere la rete virtuale che è stato configurato in **Reti VIRTUALI,** siti locali in **Reti locali** e i server DNS registrati in **Server DNS**.

## Fase 2: Configurare una connessione VPN su più siti

Il passaggio successivo consiste nel definire i gateway VPN per i siti locali. A tale scopo, è necessario:

1.  Stabilire un gateway VPN a uno dei siti tramite il portale di Azure.

2.  Esportare le impostazioni di configurazione di rete virtuale.

3.  Modificare il file di configurazione per più siti VPN.

4.  Importare la configurazione della rete Azure aggiornati.

5.  Registrare l'indirizzo IP del gateway Azure e alle chiavi.

6.  Configurare dispositivi VPN in locale.

Per ulteriori informazioni sulla configurazione di una rete VPN più siti, vedere [configurare una connessione VPN multisito](http://go.microsoft.com/fwlink/?linkid=522621).

## Definire un gateway VPN per il primo sito

Quando si crea il gateway virtuale, si noti che già che verrà connesso al primo sito locale. Quando si passa nel dashboard rete virtuale, si vedono che non è stato creato il gateway.

Per stabilire il gateway VPN sul lato Azure, seguire le istruzioni nella sezione [avviare il gateway di rete virtuale](http://msdn.microsoft.com/en-us/library/azure/jj156210.aspx#bkmk_startgateway) di [configurare un Gateway di rete virtuale nel portale di gestione](http://msdn.microsoft.com/en-us/library/azure/jj156210.aspx).


> [!IMPORTANT]
> Solo effettuare le operazioni della sezione "Avvio gateway rete virtuale" dell'articolo e non più nelle sezioni successive.



## Esportare impostazioni di configurazione rete virtuale

Portale di gestione Azure non attualmente consente di configurare una connessione VPN più siti. Per questa configurazione, è necessario esportare le impostazioni di configurazione di rete virtuale in un file XML e quindi modificare tale file. Seguire le istruzioni[all'Esportazione di impostazioni di rete virtuale in un File di rete](http://msdn.microsoft.com/en-us/library/azure/dn133804.aspx) per esportare le impostazioni.

## Modificare le impostazioni di configurazione di rete per la rete VPN più siti

Aprire il file esportato in un qualsiasi editor XML. Le connessioni gateway nei siti locali sono elencate nella sezione "ConnectionsToLocalNetwork". Ricerca per tale termine nel file XML per individuare la sezione. In questa sezione nel file di configurazione sarà simile al seguente (presupponendo che il nome del sito creato per il sito locale è "Sito A").
```powershell
    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>
```

Per configurare il secondo sito, aggiungere un'altra sezione "LocalNetworkSiteRef" nella sezione "ConnectionsToLocalNetwork". La sezione nel file di configurazione aggiornate avrà aspetto analogo al seguente (presupponendo che il nome del sito per sito locale in secondo luogo è "Sito B").
```powershell
    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
        <LocalNetworkSiteRef name="Site B">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>
```

Salvare il file di impostazioni di configurazione aggiornata.

## Importare impostazioni di configurazione di rete virtuale

Il secondo riferimento al sito che aggiunta del file di configurazione attiverà Microsoft Azure per creare un nuovo tunnel. Importare il file aggiornato utilizzando le istruzioni contenute [Importa un File di configurazione rete](http://msdn.microsoft.com/en-us/library/azure/jj156213.aspx). Dopo aver completato l'importazione, il dashboard di rete virtuale mostrerà le connessioni di gateway a entrambi i siti locali.

## Registrare l'indirizzo IP del gateway Azure e chiavi condivise

Dopo l'importano, le nuove impostazioni configurazione rete dashboard rete virtuale verrà visualizzato l'indirizzo IP del gateway Azure. Questo è l'indirizzo IP che si connetteranno a dispositivi VPN su entrambi i propri siti. Registrare l'indirizzo IP di riferimento.

È inoltre necessario ottenere le chiavi IPsec/IKE condivise per ogni tunnel è stato creato. Utilizzare queste sequenze di tasti con indirizzo IP del gateway Azure per configurare i dispositivi VPN in locale.

È necessario utilizzare PowerShell per ottenere le chiavi condivise. Se non si ha familiarità con utilizzo di PowerShell per gestire Azure, vedere [Azure PowerShell](http://msdn.microsoft.com/en-us/library/azure/jj156055.aspx).

Il cmdlet [Get-AzureVNetGatewayKey](http://msdn.microsoft.com/en-us/library/azure/dn495198.aspx) per estrarre chiavi condivise. Eseguire questo cmdlet una sola volta per ogni tunnel. Nell'esempio seguente i comandi è necessario eseguire per estrarre i tasti per i tunnel tra la rete virtuale "Azure sito" e siti di "Sito A" e "sito b". In questo esempio, l'output vengono salvate nel file separati. In alternativa, è possibile pipeline queste sequenze di tasti altri cmdlet di PowerShell o utilizzarli in uno script.
```powershell
    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site A" > C:\Keys\KeysForTunnelToSiteA.txt 
```
```powershell    
    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site B" > C:\Keys\KeysForTunnelToSiteB.txt
```

## Configurare i dispositivi VPN locale

Microsoft Azure fornisce script di configurazione dispositivo VPN per dispositivi VPN supportati. Fare clic sul collegamento di **Download VPN dispositivo Script** nel dashboard di rete virtuale per lo script appropriato per i dispositivi VPN.

Lo script che scarica avrà l'impostazione di configurazione per il primo sito configurato quando si imposta la rete virtuale e può essere utilizzato come per configurare il dispositivo VPN per il sito. Ad esempio, se è stato specificato il sito della **Rete locale** al momento della creazione della rete virtuale, lo script di dispositivo VPN utilizzabile per sito A. Tuttavia, è necessario modificarla per configurare il dispositivo VPN per il sito B. In particolare, è necessario aggiornare la chiave per corrispondere alla chiave per il secondo sito.

Ad esempio, se si utilizza un dispositivo di Routing e VPN Remote Access Service (configurazione) per i siti, è necessario:

1.  Aprire lo script di configurazione in un editor di testo.

2.  Individuare la sezione `#Add S2S VPN interface` .

3.  Il comando **Add-VpnS2SInterface** disponibile in questa sezione. Verificare che il valore del parametro *SharedSecret* corrisponde alla chiave già condivisa per il sito per cui si sta configurando il dispositivo VPN.

Altri dispositivi potrebbero richiedere ulteriori verifiche. Ad esempio, gli script di configurazione per dispositivi Cisco impostare ACL regole con gli intervalli di indirizzi IP locali. Si desidera esaminare e verificare tutti i riferimenti a siti locali nello script di configurazione prima di utilizzarlo. Vedere gli argomenti seguenti per ulteriori informazioni:

[Modelli di routing e Remote Access Service (configurazione)](http://msdn.microsoft.com/en-us/library/azure/dn133801.aspx)

[Modelli di ASR Cisco](http://msdn.microsoft.com/en-us/library/azure/dn133802.aspx)

[Modelli di Cisco ISR](http://msdn.microsoft.com/en-us/library/azure/dn133800.aspx)

[Juniper SRX modelli](http://msdn.microsoft.com/en-us/library/azure/dn133794.aspx)

[Modelli Juniper J-serie](http://msdn.microsoft.com/en-us/library/azure/dn133799.aspx)

[Juniper ISG modelli](http://msdn.microsoft.com/en-us/library/azure/dn133797.aspx)

[Juniper SSG modelli](http://msdn.microsoft.com/en-us/library/azure/dn133796.aspx)

## Checkpoint: Controllare lo stato VPN

A questo punto, entrambi i siti sono connessi alla rete virtuale Azure attraverso il gateway VPN. È possibile verificare lo stato della rete VPN multisito eseguendo il comando seguente in PowerShell.
```powershell
    Get-AzureVnetConnection -VNetName "Azure Site" | Format-Table LocalNetworkSiteName, ConnectivityState
```
Se entrambi i tunnel siano in esecuzione, l'output del comando sarà simile le operazioni seguenti.
```powershell
    LocalNetworkSiteName    ConnectivityState
    
    --------------------    -----------------
    
    Site A                  Connected
    
    Site B                  Connected
```
È inoltre possibile verificare la connettività esaminando il dashboard di rete virtuale in Azure management portal. Nella colonna **stato** sia siti verrà visualizzati come **connesso**.


> [!NOTE]
> Può richiedere diversi minuti dopo la connessione è stata stabilita la modifica di stato venga visualizzato in Azure management portal.



## Fase 3: Configurare le macchine virtuali

È necessario creare almeno due macchine virtuali in Microsoft Azure per la distribuzione: un controller di dominio e un file server che verrà utilizzato come server di controllo DAG.

1.  Creare le macchine virtuali per controller di dominio e il server di file utilizzando le istruzioni fornite nella [macchina virtuale che esegue Windows crea](http://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-tutorial/). Accertarsi di selezionare la rete virtuale creato per **Area/AFFINITÀ gruppo/VIRTUAL NETWORK** per specificare le impostazioni delle macchine virtuali.

2.  Specificare indirizzi IP Preferiti per il controller di dominio e il file server utilizzando Azure PowerShell. Quando si specifica un indirizzo IP preferito per una macchina virtuale, deve essere aggiornato, sarà necessario riavviare la macchina virtuale. Questo esempio imposta gli indirizzi IP per Azure DC e Azure FSW 10.0.0.10 e 10.0.0.11 rispettivamente.
    ```powershell
        Get-AzureVM Azure-DC | Set-AzureStaticVNetIP -IPAddress 10.0.0.10 | Update-AzureVM
    ```
    ```powershell    
        Get-AzureVM Azure-FSW | Set-AzureStaticVNetIP -IPAddress 10.0.0.11 | Update-AzureVM
    ```

    > [!NOTE]
    > Una macchina virtuale con un indirizzo IP preferito tenterà di utilizzare tale indirizzo. Tuttavia, se tale indirizzo è stato assegnato a una macchina virtuale diversa, la macchina virtuale con la configurazione di indirizzi IP preferita non verrà avviato. Per evitare questo problema, verificare che all'indirizzo IP utilizzato non è assegnato a un altro macchina virtuale. Per ulteriori informazioni, vedere <A href="http://msdn.microsoft.com/library/azure/dn630228.aspx">configurare un indirizzo IP interno statico per una macchina virtuale</A> .



3.  Effettuare il provisioning del controller di macchine Virtuali su Azure utilizzando gli standard utilizzati dall'organizzazione.

4.  Preparare il server di file con i prerequisiti per un server di controllo di Exchange DAG:
    
    1.  Aggiungere il ruolo del Server di File mediante Aggiungi ruoli e funzionalità di creazione guidata o il cmdlet [Add-WindowsFeature](http://technet.microsoft.com/en-us/library/ee662309.aspx) .
    
    2.  Aggiungere il gruppo di protezione universale Exchange Trusted sottosistemi al gruppo Administrators locale.

## Checkpoint: Controllare lo stato macchina virtuale

A questo punto, le macchine virtuali devono essere attivo e in esecuzione e deve essere in grado di comunicare con i server in entrambi i datacenter in locale:

  - Verificare che i controller di dominio in Azure viene replicato con i controller di dominio locale.

  - Verificare che è possibile raggiungere il server file su Azure in base al nome e stabilire una connessione SMB dal server Exchange.

  - Verificare che è possibile raggiungere il server di Exchange in base al nome di file server su Azure.

## Fase 4: Configurare il controllo del DAG

Infine, è necessario configurare la disponibilità del database per utilizzare il nuovo server di controllo. Per impostazione predefinita, Exchange utilizza il C:\\DAGFileShareWitnesses come il percorso di controllo della condivisione file sul server di controllo. Se si utilizza un percorso personalizzato, è consigliabile aggiornare anche la directory di controllo per la condivisione specifica.

1.  Connettersi a Exchange Management Shell.

2.  Eseguire il comando seguente per configurare il server di controllo per il DAG.
    
    ```powershell
        Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessServer Azure-FSW
    ```

Vedere gli argomenti seguenti per ulteriori informazioni:

[Proprietà del gruppo di disponibilità del database Configure](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](http://technet.microsoft.com/en-us/library/dd297934\(v=exchg.150\).aspx)

## Checkpoint: Convalidare il server di controllo DAG condivisione file

A questo punto è stato configurato il DAG per l'utilizzo del file server su Azure come il controllo del DAG. Eseguire il comando seguente per convalidare la configurazione:

1.  Convalida della configurazione di disponibilità del database eseguendo il comando seguente.
    ```powershell
        Get-DatabaseAvailabilityGroup -Identity DAG1 -Status | Format-List Name, WitnessServer, WitnessDirectory, WitnessShareInUse
    ```

    Verificare che il parametro *WitnessServer* è impostato su file server su Azure, il parametro *WitnessDirectory* è impostato per il percorso corretto e il parametro *WitnessShareInUse* Mostra **Primary**.

2.  Se la disponibilità del database è un numero pari di nodi, verrà configurato il controllo della condivisione di file. Convalidare il controllo di condivisione file impostazione nelle proprietà del cluster eseguendo il comando seguente. Il valore del parametro *SharePath* deve puntare al file server e visualizzare il percorso corretto.
    
    ```powershell
        Get-ClusterResource -Cluster MBX1 | Get-ClusterParameter | Format-List
    ```

3.  Quindi, verificare lo stato della risorsa cluster "File Condividi controllo" eseguendo il comando seguente. *State* la risorsa del cluster deve essere visualizzata **Online**.
    
    ```powershell
        Get-ClusterResource -Cluster MBX1
    ```

4.  Infine, verificare che la condivisione sia stata creata nel file server esaminando la cartella in Esplora File e le condivisioni in Server Manager.

## Vedere anche


[Pianificazione della disponibilità elevata e della resilienza del sito](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
[Passaggi e failover](switchovers-and-failovers-exchange-2013-help.md)  
[Gestione dei gruppi di disponibilità del database](managing-database-availability-groups-exchange-2013-help.md)


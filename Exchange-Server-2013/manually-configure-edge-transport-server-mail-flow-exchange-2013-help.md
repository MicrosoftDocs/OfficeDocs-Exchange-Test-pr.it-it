---
title: 'Config. manualmente flusso posta server Trasporto Edge: Exchange 2013 Help'
TOCTitle: Configurare manualmente il flusso della posta server Trasporto Edge
ms:assetid: cb4cc165-6c09-44ab-a95f-167ae8ed2485
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn606261(v=EXCHG.150)
ms:contentKeyID: 61183412
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare manualmente il flusso della posta server Trasporto Edge

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-02-21_

Questo argomento descrive le procedure per apportare modifiche manuale alla configurazione relativa alla gestione del flusso di posta da parte del server Trasporto Edge. Tali procedure consentono di risolvere problemi specifici. Se la propria organizzazione non ha bisogno di apportare modifiche di configurazione manuali, si consiglia di utilizzare la configurazione predefinita quando si sottoscrivono i server Trasporto Edge.

**Sommario**

Manually configure Send connectors

Intra-Organization Send Connectors

Create additional Send connectors after Edge subscription

Reasons to suppress automatic creation of Send connectors

Partition mail flow

Route outbound email to a smart host

Configure Send connectors for external relay domains

## Configurazione manuale dei connettori di invio

È possibile modificare manualmente la configurazione dei connettori di invio. Ad esempio, se è necessario instradare la posta elettronica in uscita tramite uno smart host, è possibile annullare la creazione automatica di un connettore di invio e configurare manualmente un connettore di invio a Internet.

## Connettori di invio tra organizzazioni

Il connettore di invio tra organizzazioni è un connettore di invio implicito e nascosto che, calcolato automaticamente da Exchange, consente al servizio Trasporto dei server di cassette postali che si trovano nella stessa organizzazione di inoltrarsi reciprocamente i messaggi senza utilizzare i connettori di invio espliciti. Poiché esiste un oggetto di configurazione con un'associazione al sito di Active Directory in Active Directory per una sottoscrizione Edge, il connettore di invio tra organizzazioni verrà anche utilizzato per inoltrare i messaggi al server Trasporto Edge.

Soltanto i server di cassette postali situati nel sito di Active Directory sottoscritto possono trasferire messaggi di posta elettronica direttamente al server Trasporto Edge sottoscritto e viceversa. Nel caso di una foresta con più siti e se la foresta di Active Directory ed Exchange vengono distribuiti in più di un sito, i server di cassette postali nei siti non sottoscritti instraderanno la posta elettronica in uscita al sito sottoscritto. Un server di cassetta postale nel sito sottoscritto instraderà la posta elettronica in uscita al server Trasporto Edge.

## Creazione di connettori di invio aggiuntivi dopo la sottoscrizione a Edge

Una volta sottoscritto il server Trasporto Edge a un sito di Active Directory, i cmdlet per la creazione e la modifica dei connettori di invio sul server Trasporto Edge sono disabilitati. Se si desidera creare un connettore di invio per il quale il server Trasporto Edge sia il server di origine, è necessario creare il connettore di invio all'interno dell'organizzazione di Exchange. È possibile specificare una o più sottoscrizioni a Edge come server di origine per un connettore di invio. Non è possibile specificare sia i server di cassette postali che le sottoscrizioni a Edge come server di origine per lo stesso connettore di invio. In occasione della successiva sincronizzazione EdgeSync dei dati, il connettore di invio verrà replicato nell'istanza AD LDS sul server Trasporto Edge configurato come server di origine. Se si specificano più sottoscrizioni Edge come server di origine, il carico delle connessioni al connettore di invio sarà bilanciato tra i server Trasporto Edge sottoscritti. Per ottenere il bilanciamento del carico, i server Trasporto Edge dovranno essere sottoscritti allo stesso sito di Active Directory. Se le sottoscrizioni Edge nei diversi siti di Active Directory sono configurate come server di origine sullo stesso connettore di invio, i server Trasporto Edge eseguiranno il routing solo al server di origine più vicino.

Sarà necessario creare manualmente i connettori di invio nei casi riportati di seguito:

  - È stata annullata la creazione automatica dei connettori di invio a Internet o in ingresso.

  - Esistono domini accettati nell'organizzazione che sono configurati come domini di inoltro esterno.

## Esistono motivi per annullare la creazione automatica dei connettori di invio

In base alla topologia dell'organizzazione di Exchange, è possibile decidere di disabilitare la creazione automatica dei connettori di invio. Negli esempi seguenti vengono descritte le situazioni nelle quali è necessario annullare la creazione automatica dei connettori di invio.

## Partizionamento del flusso di posta

Se si decide di eseguire la partizione dell'elaborazione della posta in ingresso e in uscita tra due server Trasporto Edge, uno dei server è responsabile per l'elaborazione del flusso di posta in uscita e il secondo è responsabile per l'elaborazione della posta in ingresso. A tale scopo, configurare le sottoscrizioni Edge nel modo riportato di seguito:

  - Per il server Trasporto Edge in uscita, eseguire il seguente comando nel server di cassetta postale.
    ```powershell
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $false -CreateInternetSendConnector $true
    ```
  - Per il server Trasporto Edge in ingresso, eseguire il seguente comando nel server di cassetta postale.
    ```powershell
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $true -CreateInternetSendConnector $false
    ```
## Instradamento della posta in uscita verso uno smart host

Se l'organizzazione di Exchange instrada tutta la posta elettronica in uscita tramite uno smart host, il connettore di invio a Internet creato automaticamente non sarà configurato correttamente.

Eseguire il seguente comando sul server di cassetta postale per annullare la creazione automatica del connettore di invio a Internet.
```powershell
    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInternetSendConnector $false
```

Una volta completato il processo di sottoscrizione Edge, creare manualmente il connettore di invio a Internet. Creare il connettore di invio all'interno dell'organizzazione di Exchange e selezionare la sottoscrizione Edge come server di origine per il connettore. Selezionare l'utilizzo `Custom` e configurare uno o più smart host. In occasione della successiva sincronizzazione EdgeSync dei dati di configurazione, il nuovo connettore di invio verrà replicato nell'istanza AD LDS sul server Trasporto Edge. È possibile forzare la sincronizzazione automatica di Edge Sync eseguendo il cmdlet **Start-EdgeSynchronization** su un server di cassetta postale.

Esempio: Se si utilizza la shell per configurare un connettore di invio affinché il server Trasporto Edge sottoscritto instradi i messaggi di tutti gli spazi indirizzo Internet tramite uno smart host. Eseguire questa attività sul server di cassetta postale situato all'interno dell'organizzazione di Exchange, non nel server Trasporto Edge.
```powershell
    New-SendConnector -Name "EdgeSync - Site-A to Internet" -Usage Custom -AddressSpaces SMTP:*;100 -DNSRoutingEnabled $false -SmartHosts 192.168.10.1 -SmartHostAuthMechanism None -SourceTransportServers EdgeSubscriptionName
```

> [!IMPORTANT]
> In questo esempio non viene indicato alcun meccanismo di autenticazione smart host. Assicurarsi di aver configurato il corretto meccanismo di autenticazione e di aver fornito tutte le credenziali necessarie quando si crea un connettore smart host nell'organizzazione di Exchange.



## Configurazione dei connettori di invio per i domini di inoltro esterno

Se esistono domini accettati nell'organizzazione di Exchange configurati come domini di inoltro esterno, è necessario creare manualmente un connettore di invio per gli spazi indirizzo. I messaggi che vengono recapitati ai domini di inoltro esterno sono inoltrati dal server Trasporto Edge. Nel processo di sottoscrizione Edge i connettori di invio non vengono creati né configurati automaticamente per i domini di inoltro esterno. È quindi necessario configurare i connettori di invio per questi domini e specificare una o più sottoscrizioni Edge come server di origine per i connettori di invio.

Il record di risorse MX DNS per un dominio di inoltro esterno viene risolto nel server Trasporto Edge. È possibile configurare un connettore di invio che inoltra la posta elettronica a un dominio di inoltro esterno per utilizzare lo smart host per il routing. Se il connettore di invio viene configurato affinché il dominio di inoltro esterno utilizzi il routing DNS, si crea un loop di routing. Per ulteriori informazioni sui domini di inoltro esterno, vedere [Domini accettati](accepted-domains-exchange-2013-help.md).

Inizio pagina


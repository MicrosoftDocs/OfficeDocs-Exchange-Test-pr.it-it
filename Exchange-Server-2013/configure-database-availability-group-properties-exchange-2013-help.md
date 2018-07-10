---
title: 'Configurazione delle proprietà del gruppo di disponibilità del database: Exchange 2013 Help'
TOCTitle: Configurazione delle proprietà del gruppo di disponibilità del database
ms:assetid: 50daeac5-a16f-4362-a325-19e0fe25d59d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd297985(v=EXCHG.150)
ms:contentKeyID: 50480660
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione delle proprietà del gruppo di disponibilità del database

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-06-24_

È possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell per configurare le proprietà di un gruppo di disponibilità del database (DAG), inclusi la configurazione dell''indirizzo IP del DAG, il server di controllo e la directory utilizzati dal DAG. Shell consente di configurare le proprietà del gruppo di disponibilità del database non disponibili nell'interfaccia di amministrazione di Exchange, quali il server di controllo alternativo e le informazioni sulla directory di controllo alternativa, la porta TCP utilizzata per la replica e la modalità di coordinamento dell'attivazione del datacenter (DAC).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di disponibilità del database" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - I valori delle proprietà DAG vengono archiviati sia in Active Directory che nel database del cluster. Tuttavia, alcune proprietà vengono archiviate solo nel database del cluster. Di conseguenza, è necessario che il cluster sottostante al DAG sia in esecuzione e che disponga del quorum per impostare le proprietà per gli elementi seguenti:
    
      - ReplicationPort
    
      - NetworkCompression
    
      - NetworkEncryption
    
      - DiscoverNetworks

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]  
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Configurazione delle proprietà del gruppo di disponibilità del database tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Gruppi di disponibilità del database**.

2.  Selezionare il DAG che si desidera configurare e fare clic su ![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.      
    Utilizzare la pagina **Generale** per visualizzare l'appartenenza al DAG e lo stato operativo e configurare il server di controllo del DAG, la directory di controllo e la configurazione automatica della rete:
    
      - **Server di controllo**   Il nome host o il nome di dominio completo (FQDN) del server di controllo per il gruppo di disponibilità del database. Anche se questa è una proprietà richiesta per tutti i DAG, il server di controllo verrà utilizzato quando ci sarà un numero pari di membri del DAG e il modello di quorum in uso da parte del cluster sarà Maggioranza dei nodi e della condivisione file.
    
      - **Directory di controllo**   Il percorso completo della directory utilizzata per archiviare il file di registro di controllo sul server di controllo. Anche se questa è una proprietà richiesta per tutti i DAG, la directory di controllo verrà utilizzata solo quando il server di controllo del DAG è in uso.
    
      - **Server operativi**   Questo è un campo di sola lettura che visualizza un elenco dei membri del DAG e il loro stato operativo corrente.
    
      - **Configura la rete dei gruppi di database manualmente**   Selezionare questa casella se si desidera configurare tutte le reti dei DAG manualmente. Quando la casella di controllo viene lasciata deselezionata, il sistema configura automaticamente le reti del gruppo di disponibilità del database sulla base della configurazione dell''interfaccia della rete. Se la casella di spunta è deselezionata, i cmdlet **Set-DatabaseAvailabilityGroupNetwork** e **New-DatabaseAvailabilityGroupNetwork** sono disabilitati per l'uso amministrativo rispetto al gruppo di disponibilità del database.

4.      
    Utilizzare la pagina **Indirizzi IP** per visualizzare e modificare gli indirizzi IP assegnati al DAG:
    
      - Selezionare un indirizzo IP esistente e fare clic su ![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per modificarlo.
    
      - Selezionare un indirizzo IP esistente e fare clic sull'icona del meno per modificarlo.
    
      - Immettere un indirizzo IP e fare clic su ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungerlo al DAG.

5.      
    Fare clic su **Salva** per salvare le modifiche apportate.

## Configurazione delle proprietà del gruppo di disponibilità del database tramite Shell

Con questo esempio la directory di controllo per il gruppo di disponibilità del database DAG1 viene impostata su C:\\DAG1DIR.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessDirectory C:\DAG1DIR

In questo esempio viene preconfigurato un server di controllo alternativo CAS3 e una directory di controllo alternativa C:\\DAGFileShareWitnesses\\DAG1.contoso.com per il gruppo di disponibilità del database DAG1.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGFileShareWitnesses\DAG1.contoso.com -AlternateWitnessServer CAS3

In questo esempio il gruppo di disponibilità del database DAG1 viene configurato per utilizzare DHCP (Dynamic Host Configuration Protocol) per ottenere un indirizzo IP.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 0.0.0.0

In questo esempio il gruppo di disponibilità del database DAG1 viene configurato per utilizzare l'indirizzo IP statico 10.0.0.8.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

Con questo esempio il gruppo di disponibilità del database su più subnet DAG1 viene configurato con più indirizzi IP statici.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,10.0.1.8

In questo esempio il gruppo di disponibilità del database DAG1 viene configurato per la modalità di coordinamento dell'attivazione del data center.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly

In questo esempio, la porta per la replica per un un gruppo di disponibilità del database DAG1 viene configurata in modo da corrispondere a 63132.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -ReplicationPort 63132


> [!NOTE]  
> Una volta modificata la porta predefinita per la replica per un DAG, è necessario modificare manualmente le eccezioni Windows Firewall su ogni membro del DAG per consentire le comunicazioni sulla porta specificata.



## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che il gruppo di disponibilità del database sia stato configurato correttamente, procedere come segue:

  - In Shell, utilizzare il comando seguente per visualizzare le impostazioni di configurazione del DAG e verificare che sia stato configurato correttamente.
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## Ulteriori informazioni

[Creare un gruppo di disponibilità del database](create-a-database-availability-group-exchange-2013-help.md)

[Rimuovere un gruppo di disponibilità del database](remove-a-database-availability-group-exchange-2013-help.md)

[Creare una rete di gruppo di disponibilità del database](create-a-database-availability-group-network-exchange-2013-help.md)

[Gestire l'appartenenza al gruppo di disponibilità del database](manage-database-availability-group-membership-exchange-2013-help.md)

[Get-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd351226\(v=exchg.150\))

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\))


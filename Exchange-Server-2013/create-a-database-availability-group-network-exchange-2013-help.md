---
title: 'Creare una rete di gruppo di disponibilità del database: Exchange 2013 Help'
TOCTitle: Creare una rete di gruppo di disponibilità del database
ms:assetid: 6caec7be-788a-4058-87a7-f31c575b870c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298051(v=EXCHG.150)
ms:contentKeyID: 50480939
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare una rete di gruppo di disponibilità del database

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-11-02_

Se necessario, è possibile creare altre reti da utilizzare in un gruppo di disponibilità del database. Per creare una rete del gruppo di disponibilità del database (DAG) è possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell.

Per informazioni sulle altre attività di gestione relative ai gruppi di disponibilità del database? vedere [Gestione dei gruppi di disponibilità del database](managing-database-availability-groups-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di disponibilità del database" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Per creare una rete per il gruppo di disponibilità del database, è necessario che la configurazione automatica della rete sia stata disabilitata per il gruppo. Per le procedure dettagliate per disabilitare la configurazione automatica della rete per un gruppo di disponibilità del database, vedere [Configurazione delle proprietà del gruppo di disponibilità del database](configure-database-availability-group-properties-exchange-2013-help.md).

  - Quando si crea una rete per il gruppo di disponibilità del database, è necessario assegnarle subnet univoche che non siano già utilizzate da una rete di un altro gruppo di disponibilità del database. Se si utilizzano subnet assegnate a una rete del gruppo di disponibilità del database esistente, le subnet verranno rimosse da quella rete e aggiunte alla rete appena creata.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Utilizzo dell'interfaccia di amministrazione di Exchange per la creazione della rete per il gruppo di disponibilità del database

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Gruppi di disponibilità del database**.

2.  Selezionare il DAG che si desidera configurare, quindi fare clic su ![Aggiunta di una rete del gruppo di disponibilità del database](images/Dd298051.befcdc4e-7f7a-451d-a0a8-608c79f5d186(EXCHG.150).gif "Aggiunta di una rete del gruppo di disponibilità del database").

3.  
    
    Nella pagina **Nuova rete gruppo di disponibilità del database**, fornire le seguenti informazioni:
    
      - **Nome della rete per il gruppo di disponibilità del database**   In questo campo digitare un nome per la rete univoco nel gruppo di disponibilità del database.
    
      - **Descrizione**   In questo campo immettere una descrizione della rete per il gruppo di disponibilità del database.
    
      - **Subnet**   In questo campo associare una o più subnet alla rete per il gruppo di disponibilità del database. Fare clic su ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere una subnet, su ![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per modificare una subnet e sul segno meno (-) per rimuovere una subnet.

4.  Fare clic su **Salva** per creare la rete per il gruppo di disponibilità del database.

## Creazione della rete per il gruppo di disponibilità del database tramite Shell

In questo esempio viene creata la rete ReplicationDagNetwork02 con una subnet di 10.0.0.0 e una maschera di bit di 8 nel gruppo di disponibilità del database DAG1. La replica viene abilitata per la rete e viene aggiunta anche una descrizione facoltativa della rete.

    New-DatabaseAvailabilityGroupNetwork -DatabaseAvailabilityGroup DAG1 -Name ReplicationDagNetwork02 -Description "Replication network 2" -Subnets 10.0.0.0/8 -ReplicationEnabled:$True

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta creazione della rete per il gruppo di disponibilità del database, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Gruppi di disponibilità del database**. Selezionare il gruppo di disponibilità del database appropriato e la rete appena creata verrà visualizzata nel riquadro dei dettagli.

  - In Shell, utilizzare il seguente comando per verificare che la rete per il gruppo di disponibilità del database sia stata creata correttamente e per visualizzare le informazioni sulla configurazione della rete.
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## Ulteriori informazioni

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/it-it/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/it-it/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/it-it/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/it-it/library/dd298131\(v=exchg.150\))


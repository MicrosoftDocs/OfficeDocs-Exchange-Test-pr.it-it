---
title: 'Configurazione delle proprietà rete gruppo di disponibilità del database: Exchange 2013 Help'
TOCTitle: Configurazione delle proprietà rete gruppo di disponibilità del database
ms:assetid: 41197639-988f-476c-9788-51d5191a7dce
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd297927(v=EXCHG.150)
ms:contentKeyID: 50480461
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione delle proprietà rete gruppo di disponibilità del database

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-31_

Ogni rete per il gruppo di disponibilità del database (DAG) dispone di varie proprietà che è possibile configurare, inclusi il nome della rete DAG, un campo di descrizione per la rete DAG, un elenco di subnet utilizzate dalla rete DAG e se la rete DAG è abilitata o meno per la replica.

Per informazioni sulle altre attività di gestione relative ai gruppi di disponibilità del database? vedere [Gestione dei gruppi di disponibilità del database](managing-database-availability-groups-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di disponibilità del database" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - È possibile configurare una rete DAG solo quando viene disattivata la configurazione automatica per un DAG. Per le procedure dettagliate per disabilitare la configurazione automatica della rete per un gruppo di disponibilità del database, vedere [Configurazione delle proprietà del gruppo di disponibilità del database](configure-database-availability-group-properties-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Configurazione delle proprietà della rete per il gruppo di disponibilità del database tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Gruppi di disponibilità del database**.

2.  Selezionare il DAG che si desidera configurare e nel riquadro Dettagli, sotto la rete dei DAG che si desidera configurare, scegliere:
    
      - **Disabilita la replica** o **Abilita la replica**   Consente di configurare le impostazione di replica per la rete del gruppo di disponibilità del database.
    
      - **Rimuovi**   Consente di rimuovere una rete del gruppo di disponibilità del database. Per rimuovere una rete DAG, è necessario prima rimuovere tutte le subnet associate dalla rete dei DAG.
    
      - **Visualizza dettagli**   Consente di configurare le proprietà della rete del gruppo di disponibilità del database, inclusi il nome, la descrizione e le subnet associate. È inoltre possibile visualizzare le interfacce di rete associate a queste subnet e abilitare o disabilitare la replica per la rete del gruppo di disponibilità del database.

## Configurazione delle proprietà della rete per il gruppo di disponibilità del database tramite Shell

In questo esempio, la subnet of 10.0.0.0 e la subnet mask 255.0.0.0 vengono aggiunte alla rete del gruppo di disponibilità del database MapiDagNetwork nel gruppo di disponibilità del database DAG1.

    Set-DatabaseAvailabilityGroupNetwork -Subnets 10.0.0.0/8 -Identity DAG1\MapiDagNetwork

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver configurato correttamente la rete del gruppo di disponibilità del database, fare quanto segue:

  - In Shell, utilizzare il seguente comando per visualizzare le impostazioni di configurazione della rete del gruppo di disponibilità del database e verificare che la rete sia stata configurata correttamente.
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## Ulteriori informazioni

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/it-it/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/it-it/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/it-it/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/it-it/library/dd298131\(v=exchg.150\))


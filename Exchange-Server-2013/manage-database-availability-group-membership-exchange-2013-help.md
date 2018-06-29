---
title: "Gestire l'appartenenza al gruppo di disponibilità del database: Exchange 2013 Help"
TOCTitle: Gestire l'appartenenza al gruppo di disponibilità del database
ms:assetid: fb2ea15e-96d5-4045-b75b-b0aa5fc60479
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351278(v=EXCHG.150)
ms:contentKeyID: 50482070
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire l'appartenenza al gruppo di disponibilità del database

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-08-13_

Quando si aggiunge un server a un gruppo di disponibilità del database (DAG), il server collabora con gli altri server nel DAG per fornire il ripristino automatico a livello di database da errori di database, server e rete. Quando si rimuove un server da un DAG, il server non viene più protetto automaticamente dagli errori.

Per informazioni sulle altre attività di gestione relative ai gruppi di disponibilità del database? vedere [Gestione dei gruppi di disponibilità del database](managing-database-availability-groups-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti per ogni server

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di disponibilità del database" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - I DAG utilizzano le tecnologie Windows Failover Clustering (WFC). Ogni server Cassette postali che è membro di un DAG è anche un nodo del cluster sottostante utilizzato dal DAG. Di conseguenza un server Cassette postali può essere membro di un solo DAG in un momento specifico. Poiché i DAG utilizzano la tecnologia WFC, tutti i server aggiunti a un DAG devono eseguire lo stesso sistema operativo: Windows Server 2008 R2 Enterprise o Datacenter Edition oppure Windows Server 2012 o Windows Server 2012 R2 Standard o Datacenter Edition.

  - Se si aggiungono i server Cassette postali su cui è in esecuzione Windows Server 2012, è necessario pregestire l'oggetto nome cluster (CNO) per il DAG. Se si aggiungono server Cassette postali che eseguono Windows Server 2012 R2 e al DAG non è assegnato punto di accesso amministrativo, non è necessario pregestire l'oggetto nome cluster (CNO) poiché i DAG senza punti di accesso amministrativi non dispongono di oggetti nome cluster. Per la procedura dettagliata, vedere [Pregestione dell'oggetto nome cluster per un gruppo di disponibilità del database](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

  - Per poter aggiungere membri a un DAG, è necessario prima crearlo. Per la procedura dettagliata, vedere [Creare un gruppo di disponibilità del database](create-a-database-availability-group-exchange-2013-help.md).

  - È necessario rimuovere tutte le copie del database replicate dal server prima di poterlo rimuovere da un DAG.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Gestione dell'appartenenza a un gruppo di disponibilità del database tramite l'interfaccia di amministrazione di Exchange

1.  In Interfaccia di amministrazione di Exchange, accedere a **Server** \> **Gruppi di disponibilità del database**.

2.  Selezionare il DAG che si desidera configurare, quindi fare clic su ![Gestione dei membri DAG](images/Dd351278.d567ae56-d6cd-4edb-ab67-ad8f7c58f337(EXCHG.150).gif "Gestione dei membri DAG").
    
      - Per aggiungere uno o più server Cassette postali a un DAG, fare clic su ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), selezionare i server dall'elenco, fare clic su **Aggiungi**, quindi su **OK**.
    
      - Per rimuovere uno più server Cassette postali dal DAG, selezionare i server, quindi fare clic sull'icona meno (-).

3.  Fare clic su **Salva** per salvare le modifiche.

4.  Al termine dell'operazione, fare clic su **Chiudi**.

## Utilizzare la shell per gestire l'appartenenza a un gruppo di disponibilità del database

Con questo esempio viene aggiunto il server Cassette postali MBX1 nel DAG DAG1.

    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

Con questo esempio il server Cassette postali MBX1 viene rimosso dal gruppo di disponibilità del database DAG1. Prima di eseguire il comando, assicurarsi che non esistano database replicati sul server di cassette postali.

    Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

In questo esempio vengono rimosse le impostazioni di configurazione del server Cassette postali MBX4 dal gruppo di disponibilità del database DAG2. MBX4 deve essere offline per un periodo prolungato, quindi la configurazione viene rimossa dal DAG mentre è offline per stabilire il quorum con i membri del DAG online rimanenti.

    Remove-DatabaseAvailabilityGroupServer -Identity DAG2 -MailboxServer MBX4 -ConfigurationOnly

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'appartenenza al DAG sia stata gestita correttamente, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Gruppi di disponibilità del database**. L'appartenenza al DAG corrente viene visualizzata nella colonna **Server membri**.

  - In Shell, eseguire il comando riportato di seguito per visualizzare informazioni sull'appartenenza al DAG.
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List Servers

## Ulteriori informazioni

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/it-it/library/dd298049\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/it-it/library/dd297956\(v=exchg.150\))


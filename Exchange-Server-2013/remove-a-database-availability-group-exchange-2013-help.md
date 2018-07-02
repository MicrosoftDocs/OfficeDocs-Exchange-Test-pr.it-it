---
title: 'Rimuovere un gruppo di disponibilità del database: Exchange 2013 Help'
TOCTitle: Rimuovere un gruppo di disponibilità del database
ms:assetid: 071296e9-31b0-40f4-9a02-177d97486ebd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335069(v=EXCHG.150)
ms:contentKeyID: 50479951
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere un gruppo di disponibilità del database

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-16_

L'eliminazione di un gruppo di disponibilità del database è un'attività rapida e semplice. Per rimuovere un gruppo di disponibilità del database è possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell.

Per informazioni sulle altre attività di gestione relative ai gruppi di disponibilità del database? vedere [Gestione dei gruppi di disponibilità del database](managing-database-availability-groups-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di disponibilità del database" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Prima di poterlo rimuovere, un gruppo di responsabilità del database deve essere vuoto. Se il gruppo di disponibilità del database da eliminare contiene server Casette postali, per prima cosa è necessario rimuovere i server dal gruppo di disponibilità del database. Per la procedura dettagliata relativa alla rimozione di un server Cassette postali da un gruppo di disponibilità del database, vedere [Gestire l'appartenenza al gruppo di disponibilità del database](manage-database-availability-group-membership-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Eliminazione di un gruppo di disponibilità del database tramite Interfaccia di amministrazione di Exchange

1.  Accedere a **Server** \> **Gruppi di disponibilità del database**.

2.  Selezionare il gruppo di disponibilità del database che si desidera rimuovere e fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

3.  Fare clic su **Sì** per confermare l'avviso e rimuovere il gruppo di disponibilità del database.

## Eliminazione di un gruppo di disponibilità del database tramite Shell

In questo esempio viene eliminato il gruppo di disponibilità del database DAG1.

    Remove-DatabaseAvailabilityGroup -Identity DAG1

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare l'avvenuta eliminazione del gruppo di disponibilità del database, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Gruppi di disponibilità del database** e vedere se il gruppo di disponibilità del database è ancora visualizzato.

  - In Shell, utilizzare il seguente comando per vedere se il gruppo di disponibilità del database esiste ancora:
    
        Get-DatabaseAvailabilityGroup <DAGName>
    
    Se l'eliminazione del gruppo di disponibilità del database è riuscita, il precedente comando produrrà un messaggio di errore in cui è indicato che non è stato possibile trovare l'oggetto.


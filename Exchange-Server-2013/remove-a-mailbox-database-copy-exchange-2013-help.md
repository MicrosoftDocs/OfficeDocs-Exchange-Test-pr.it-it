---
title: 'Rimuovere una copia del database delle cassette postali: Exchange 2013 Help'
TOCTitle: Rimuovere una copia del database delle cassette postali
ms:assetid: 99fecdde-b158-4dfc-9ca7-ff7c0ada7819
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298164(v=EXCHG.150)
ms:contentKeyID: 50481283
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere una copia del database delle cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-06_

Tali procedure mostrano come rimuovere una copia di un database delle cassette postali. Non è possibile utilizzare tali procedure per rimuovere l'ultima copia di un database delle cassette postali. Per la procedura dettagliata su come rimuovere l'ultima copia di un database delle cassette postali, vedere [Remove a mailbox database](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md) o [Remove-MailboxDatabase](https://technet.microsoft.com/it-it/library/aa997931\(v=exchg.150\)).

Per informazioni sulle altre attività di gestione correlate alle copie del database delle cassette postali? vedere [Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Copie del database cassette postali" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Le copie del database delle cassette postali possono essere rimosse solo da un gruppo di disponibilità del database (DAG) integro. Se il DAG non è integro (ad esempio, il cluster sottostante del DAG è inattivo a causa della perdita del quorum) non sarà possibile rimuovere le copie del database delle cassette postali.

  - Se si sta rimuovendo l'ultima copia passiva del database, non deve essere abilitata la registrazione circolare a replica continua (CRCL) per il database delle cassette postali specificato. Se è abilitata la registrazione circolare, è necessario prima disabilitarla. Una volta rimossa la copia del database delle cassette postali, è possibile abilitare la registrazione circolare. Dopo avere eseguito l'abilitazione per un database delle cassette postali non replicato, al posto della registrazione circolare CRCL viene utilizzata la registrazione circolare JET. Se non si sta rimuovendo l'ultima copia passiva di un database, la registrazione circolare CRCL può restare abilitata.

  - Una volta rimossa una copia del database, è necessario eliminare manualmente tutti i file di registro del database e delle transazioni dal server da cui viene rimossa la copia del database.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Utilizzare EAC per rimuovere una copia del database delle cassette postali

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Database**.

2.  Selezionare il database delle cassette postali di cui si desidera rimuovere la copia.

3.  Nel riquadro dei dettagli, individuare la copia passiva che si desidera rimuovere e fare clic su **Rimuovi**.

4.  Per confermare la rimozione nella finestra di dialogo di avviso, fare clic su **Sì**.

5.  Fare clic su **OK** per confermare la rimozione dopo aver riesaminato eventuali messaggi.

6.  Eliminare manualmente i file di log del database e delle transazioni dal server da cui è stata rimossa la copia del database.

## Rimozione di una copia del database delle cassette postali tramite Shell

In questo esempio viene rimossa una copia del database delle cassette postali DB1 dal server Cassette postali MB1.

    Remove-MailboxDatabaseCopy -Identity DB1\MBX1 -Confirm:$False

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta rimozione di una copia del database delle cassette postali, effettuare una delle seguenti operazioni:

  - In EAC, individuare **Server** \> **Database**. Selezionare il database appropriato; la copia passiva rimossa non dovrebbe più essere elencata nel riquadro dei dettagli.

  - Nella shell, eseguire il comando riportato di seguito per verificare la rimozione della copia.
    
        Get-MailboxDatabase <DatabaseName> | Format-List DatabaseCopies
    
    La copia passiva rimossa non è più elencata.


---
title: 'Attivare una copia del database delle cassette postali: Exchange 2013 Help'
TOCTitle: Attivare una copia del database delle cassette postali
ms:assetid: d948269b-c902-4d8d-8c2b-269473359baa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee364750(v=EXCHG.150)
ms:contentKeyID: 50481821
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Attivare una copia del database delle cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-01_

L'attivazione di una copia del database delle cassette postali è il processo con cui una specifica copia passiva viene designata come nuova copia attiva di un database delle cassette postali. Questo processo viene definito *passaggio di database*. Un passaggio di database richiede lo smontaggio del database attivo corrente e il montaggio della copia del database sul server specificato come nuova copia attiva del database delle cassette postali. La copia del database che diverrà il database delle cassette postali attivo deve essere integra e aggiornata.

Per informazioni sulle altre attività di gestione che hanno per oggetto le copie del database delle cassette postali? vedere [Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Copie del database cassette postali" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Spostamento del database delle cassette postali attivo tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Database**.

2.  Selezionare il database di cui si desidera attivare la copia.

3.  Nel riquadro Dettagli, in **Copie di database** fare clic su **Attiva** sotto la copia di database che si desidera attivare.

4.  Fare clic su **Sì** per attivare la copia di database.

## Spostamento del database delle cassette postali attivo tramite Shell

Con questo esempio viene attivata e montata una copia del database DB4 ospitata in MBX3 come nuovo database delle cassette postali attivo. Questo comando imposta DB4 come nuovo database delle cassette postali attivo e non sostituisce le impostazioni di montaggio del database su MBX3.

    Move-ActiveMailboxDatabase DB4 -ActivateOnServer MBX3 -MountDialOverride:None

In questo esempio viene eseguito un passaggio del database DB2 sul server Cassette postali MBX1. Al termine del comando, MBX1 ospita la copia attiva di DB2. Poiché il parametro *MountDialOverride* è impostato su `None`, MBX1 esegue il montaggio del database utilizzando le proprie impostazioni del dial di montaggio automatico del database.

    Move-ActiveMailboxDatabase DB2 -ActivateOnServer MBX1 -MountDialOverride:None

In questo esempio viene eseguito un passaggio del database DB1 sul server Cassette postali MBX3. Al termine del comando, MBX3 ospita la copia attiva di DB1. Perché il parametro *MountDialOverride* viene specificato con un valore `Good Availability`, MBX3 esegue il montaggio del database utilizzando un'impostazione del dial di montaggio automatico del database pari a *GoodAvailability*.

    Move-ActiveMailboxDatabase DB1 -ActivateOnServer MBX3 -MountDialOverride:GoodAvailability

In questo esempio viene eseguito un passaggio del database DB3 sul server Cassette postali MBX4. Al termine del comando, MBX4 ospita la copia attiva di DB3. Poiché il parametro *MountDialOverride* non è specificato, MBX4 monta il database utilizzando un'impostazione di montaggio automatico del database di *Lossless*.

    Move-ActiveMailboxDatabase DB3 -ActivateOnServer MBX4

In questo esempio viene eseguito un passaggio di server per il server Cassette postali MBX1. Tutte le copie del database delle cassette postali attive su MBX1 vengono attivate in uno o più server Cassette postali con copie integre dei database attivi su MBX1.

    Move-ActiveMailboxDatabase -Server MBX1

In questo esempio viene eseguito un passaggio del database DB4 sul server Cassette postali MBX5. In questo esempio la copia del database su MBX5 dispone di una coda di riesecuzione maggiore di 6. Di conseguenza, è necessario specificare il parametro *SkipLagChecks* per attivare la copia del database su MBX5.

    Move-ActiveMailboxDatabase DB4 MBX5 -SkipLagChecks

In questo esempio viene eseguito un passaggio del database DB5 sul server Cassette postali MBX6. In questo esempio la copia del database su MBX6 utilizza Failed come valore di *ContentIndexState*. Di conseguenza, è necessario specificare il parametro *SkipClientExperienceChecks* per attivare la copia del database su MBX6.

    Move-ActiveMailboxDatabase DB5 MBX6 -SkipClientExperienceChecks

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare l'attivazione corretta di una copia di database delle cassette postali, effettuare una delle seguenti operazioni:

  - In EAC, individuare **Server** \> **Database**. Selezionare il database appropriato e, nel riquadro Dettagli, fare clic su **Visualizza dettagli** per visualizzare le proprietà di copia del database.

  - In Shell eseguire il comando riportato di seguito per visualizzare le informazioni di stato per una copia del database.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

## Ulteriori informazioni

[Copie del database delle cassette postali](mailbox-database-copies-exchange-2013-help.md)

[Configurazione delle proprietà della copia del database delle cassette postali](configure-mailbox-database-copy-properties-exchange-2013-help.md)


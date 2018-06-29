---
title: 'Configurazione delle proprietà della copia del database delle cassette postali: Exchange 2013 Help'
TOCTitle: Configurazione delle proprietà della copia del database delle cassette postali
ms:assetid: cf186561-ab2c-45c0-90f5-8d3ecfabeeac
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351151(v=EXCHG.150)
ms:contentKeyID: 50481703
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione delle proprietà della copia del database delle cassette postali

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-11-01_

Ogni copia del database delle cassette postali dispone di proprietà configurabili. che comprendono l'intervallo di riesecuzione e troncamento e il numero di preferenza di attivazione. Per ulteriori informazioni sull'intervallo di riesecuzione e troncamento e sul numero di preferenza di attivazione, vedere [Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Copie del database cassette postali" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Configurazione delle proprietà della copia del database delle cassette postali tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Database**.

2.  Selezionare il database da configurare.

3.  Nel riquadro dei dettagli sotto **Copie database** fare clic su **Visualizza dettagli** per la copia di database desiderata, quindi visualizzare o configurare quanto segue:
    
      - **Database**   Visualizza il nome del database selezionato.
    
      - **Server Cassette postali**   Visualizza il nome del server Cassette postali che ospita la copia del database selezionato.
    
      - **Stato indice contenuto** Visualizza lo stato corrente dell'indice del contenuto per la copia del database selezionato.
    
      - **Stato**   Visualizza lo stato corrente della copia del database selezionato.
    
      - **Lunghezza coda di copia**   Indica il numero di file di registro in attesa di essere copiati nella copia del database selezionato. Questo campo è rilevante solo per le copie passive del database.
    
      - **Lunghezza coda di riesecuzione**   Indica il numero di file di registro in attesa di essere rieseguiti nella copia del database selezionato. Questo campo è rilevante solo per le copie passive del database.
    
      - **Messaggi di errore** Visualizza i messaggi di errore per le copie del database con stato `Failed` o `Failed and Suspended`.
    
      - **Ultimo log disponibile** Visualizza data e timestamp del file di registro generato più recentemente sulla copia attiva del database. Questo campo è rilevante solo per le copie passive del database. Nelle copie del database attive (replicate e autonome), il valore inserito nel campo sarà **mai**.
    
      - **Ora ultimo file di log ispezionato** Visualizza data e timestamp dell'ultimo file di registro ispezionato da LogInspector sulla copia del database selezionato. Questo campo è rilevante solo per le copie passive del database. Nelle copie del database attive (replicate e autonome), il valore inserito nel campo sarà **mai**.
    
      - **Ora ultimo file di log copiato** Visualizza data e timestamp dell'ultimo file di registro copiato da LogCopier sulla copia del database selezionato. Questo campo è rilevante solo per le copie passive del database. Nelle copie del database attive (replicate e autonome), il valore inserito nel campo sarà **mai**.
    
      - **Ora ultimo file di log rieseguito** Visualizza data e timestamp dell'ultimo file di registro rieseguito da LogReplayer sulla copia del database selezionato. Questo campo è rilevante solo per le copie passive del database. Nelle copie del database attive (replicate e autonome), il valore inserito nel campo sarà **mai**.
    
      - **Numero di preferenza di attivazione** Visualizza il numero di preferenza di attivazione. Viene utilizzato come parte della selezione della copia migliore di Active Manager e per bilanciare il DAG ridistribuendo i database delle cassette postali attive all'intero DAG tramite lo script RedistributeActiveDatabases.ps1. Il valore per la preferenza di attivazione è un numero uguale o maggiore a 1, dove 1 si trova al vertice dell'ordine di preferenza. Il numero non può essere superiore al numero di copie del database delle cassette postali.
    
      - **Intervallo di riesecuzione (giorni)** Visualizza la quantità di tempo di attesa per il servizio Archivio informazioni di Microsoft Exchange prima di rieseguire i file di registro che sono stati copiati dal servizio Replica di Microsoft Exchange nella copia passiva del database. Impostando questo parametro su un valore superiore a 0 si crea una copia del database ritardata. Il valore predefinito per questa impostazione è 0 giorni. Il valore massimo consentito per questa impostazione è 14 giorni. Il valore minimo consentito è 0 giorni e l'impostazione del valore su 0 disabilita l'intervallo di riesecuzione.

## Utilizzare la shell per configurare le proprietà della copia del database delle cassette postali

In questo esempio viene configurata la copia di un database delle cassette postali con numero della preferenza di attivazione pari a 3.

    Set-MailboxDatabaseCopy -Identity DB3\EX3 -ActivationPreference 3

In questo esempio viene configurata una copia del database DB1 e ospitata su Server1 con un intervallo di riesecuzione e troncamento di un giorno e un numero della preferenza di attivazione pari a 2.

    Set-MailboxDatabaseCopy -Identity DB1\Server1 -ReplayLagTime 1.0:0:0 -TruncationLagTime 1.0:0:0 -ActivationPreference 2

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la configurazione corretta di una copia di database delle cassette postali, effettuare una delle seguenti operazioni:

  - In EAC, individuare **Server** \> **Database**. Selezionare il database appropriato e, nel riquadro Dettagli, fare clic su **Visualizza dettagli** per visualizzare le proprietà di copia del database.

  - In Shell eseguire il comando riportato di seguito per visualizzare le informazioni di configurazione per una copia del database.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

## Ulteriori informazioni

[Set-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd298104\(v=exchg.150\))

[Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/it-it/library/dd298044\(v=exchg.150\))

[Get-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb124924\(v=exchg.150\))


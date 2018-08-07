---
title: 'Attiva copia database cassette postali ritardata: Exchange 2013 Help'
TOCTitle: Attivare una copia del database delle cassette postali ritardata
ms:assetid: 493d9c40-644d-49d6-9291-949acbcfdcb6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd979786(v=EXCHG.150)
ms:contentKeyID: 50480529
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Attivare una copia del database delle cassette postali ritardata

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-01-28_

Una copia del database della cassette postali ritardata è una copia del database delle cassette postali configurata con un valore relativo all'intervallo di riproduzione maggiore di 0. L'attivazione e il recupero di una copia del database delle cassette postali ritardata è un processo semplice se si desidera che il database esegua nuovamente tutti i file di registro e renda attuale la copia del database. Se si desidera, invece, eseguire nuovamente i file di registro fino a un determinato momento, l'operazione può rivelarsi più complicata in quanto è necessario manipolare manualmente i file di registro ed eseguire Eseutil.

Ulteriori informazioni sulle copie del database delle cassette postali ritardate? vedere [Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md).


> [!NOTE]
> La quantità di tempo richiesta per attivare direttamente una copia del database delle cassette postali ritardata dipende dal numero di file di registro per i quali è necessario ripetere l'esecuzione e dalla velocità impiegata dall'hardware per riprodurli. Come minimo, viene osservata una velocità di riproduzione di almeno due registri al secondo per database.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 1 minuto, oltre al tempo che occorre per duplicare la copia ritardata, per riprodurre i file di registro necessari ed estrarre i dati o installare il database per l'attività dei client.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Copie del database cassette postali" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - La copia del database delle cassette postali da attivare deve essere configurata con un intervallo di riproduzione maggiore di 0.

  - La copia del database delle cassette postali da attivare deve contenere tutti i file di registro fino al momento specifico in cui si desidera effettuare il recupero. Tenere presente che le transazioni del database possono estendersi a più file di registro quando viene definito il momento specifico in cui si desidera eseguire il recupero.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Attivazione della copia del database delle cassette postali ritardata fino a un determinato momento tramite Shell


> [!NOTE]
> Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per attivare una copia del database delle cassette postali ritardata fino a un determinato momento. Invece si possono eseguire una serie di passaggi utilizzando Shell e la riga di comando.



1.  In questo esempio, viene sospesa la replica per la copia ritardata attivata utilizzando il cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd351074\(v=exchg.150\)).
    
        Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false

2.  Facoltativamente, se si desidera mantenere una copia ritardata, fare una copia della copia del database e dei relativi file di registro.
    

    > [!NOTE]
    > Se si continua a eseguire tale procedura sul volume esistente, potrebbero esserci delle conseguenze sulle prestazioni di scrittura della copia. Per evitare ciò, è possibile copiare i file di registro e database su un altro volume per eseguire il recupero.



3.  Stabilire quali sono i file di registro necessari per la riproduzione nel database affinché venga rispettato il requisito temporale per tale recupero (in base all'ora e alla data del file di registro, come indicato in Windows Explorer). Tutti i registri creati dopo questo periodo di tempo devono essere spostati in una directory differente, fino al termine del processo di recupero, e i registri non sono più necessari.

4.  Eliminare il file del punto di arresto (.chk) per il database.

5.  In questo esempio, viene utilizzato Eseutil per eseguire l'operazione di recupero.
    
        Eseutil.exe /r eXX /a
    

    > [!NOTE]
    > Nell'esempio precedente, e<EM>XX</EM> è il prefisso di generazione dei registri per il database (ad esempio, E00, E01, E02 e così via).

    

    > [!IMPORTANT]
    > A seconda di diversi fattori, quali la lunghezza dell'intervallo di riproduzione, il numero di file di registro generati durante tale periodo e la velocità a cui l'hardware è in grado di riprodurre tali registri nel database da recuperare, tale operazione potrebbe richiedere molto tempo.



6.  Una volta terminata la riproduzione dei registri, il database viene a trovarsi in uno stato di arresto regolare e può essere copiato e utilizzato per scopi di recupero.

7.  Una volta completato il processo di recupero, viene ripresa la replica per il database utilizzato come parte del processo di recupero, come illustrato in questo esempio.
    
        Resume-MailboxDatabaseCopy DB1\EX3

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd351074\(v=exchg.150\)) o [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335220\(v=exchg.150\)).

## Utilizzare Shell per attivare una copia del database delle cassette postali ritardata riproducendo tutti i file di registro non impegnati

1.  Facoltativamente, se si desidera mantenere una copia ritardata, fare una copia della copia del database e dei relativi file di registro.
    
    1.  In questo esempio, viene sospesa la replica per la copia ritardata attivata utilizzando il cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd351074\(v=exchg.150\)).
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  Facoltativamente, se si desidera mantenere una copia ritardata, fare una copia della copia del database e dei relativi file di registro.
        

        > [!NOTE]
        > Se si continua a eseguire tale procedura sul volume esistente, potrebbero esserci delle conseguenze sulle prestazioni di scrittura della copia. Per evitare ciò, è possibile copiare i file di registro e database su un altro volume per eseguire il recupero.



2.  In questo esempio, viene attivata la copia ritardata del database delle cassette postali utilizzando il cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/it-it/library/dd298068\(v=exchg.150\)) con il parametro *SkipLagChecks*.
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -SkipLagChecks

## Attivazione di una copia ritardata del database delle cassette postali con il recupero SafetyNet tramite Shell

1.  Facoltativamente, se si desidera mantenere una copia ritardata è possibile creare uno snapshot di Servizio Copia Shadow del volume (VSS) basato su file system (che non riconosce Exchange) per i volumi che contengono la copia del database e i relativi file di registro.
    
    1.  In questo esempio, viene sospesa la replica per la copia ritardata attivata utilizzando il cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd351074\(v=exchg.150\)).
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  Facoltativamente, se si desidera mantenere una copia ritardata, fare una copia della copia del database e dei relativi file di registro.
        

        > [!NOTE]
        > Se si continua a eseguire tale procedura sul volume esistente, potrebbero esserci delle conseguenze sulle prestazioni di scrittura della copia. Per evitare ciò, è possibile copiare i file di registro e database su un altro volume per eseguire il recupero.



2.  Stabilire i registri necessari per la copia ritardata del database cercando il "Registro necessario": valore dell'output di intestazione del database in ESEUTIL
    
        Eseutil /mh <DBPath> | findstr /c:"Log Required"
    
    Prendere nota dei numeri esadecimali tra parentesi. Il primo numero è la generazione più bassa (definita LowGeneration) e il secondo è il numero della generazione più alta (definita HighGeneration). Spostare tutti i file di generazione del registro che hanno una sequenza di generazione più grande di HighGeneration in una posizione diversa, in modo che non vengano riprodotti nel database.

3.  Sul server che ospita la copia attiva del database, eliminare i file di registro della copia ritardata attivata dalla copia attiva oppure arrestare il servizio Replica di Microsoft Exchange.

4.  Eseguire lo switchover del database e attivare la copia ritardata. In questo esempio viene attivato il database utilizzando il cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/it-it/library/dd298068\(v=exchg.150\)) con diversi parametri.
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -MountDialOverride BestEffort -SkipActiveCopyChecks -SkipClientExperienceChecks -SkipHealthChecks -SkipLagChecks

5.  A questo punto, il database verrà montato automaticamente e verrà richiesto un nuovo recapito dei messaggi mancanti da SafetyNet.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta attivazione di una copia ritardata del database delle cassette postali, effettuare una delle seguenti operazioni:

  - In EAC, individuare **Server** \> **Database**. Selezionare il database appropriato e, nel riquadro Dettagli, fare clic su **Visualizza dettagli** per visualizzare le proprietà di copia del database.

  - In Shell, utilizzare il seguente comando per visualizzare le informazioni sulla stato per una copia del database.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List


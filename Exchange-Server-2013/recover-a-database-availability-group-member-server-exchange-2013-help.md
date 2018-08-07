---
title: 'Ripristina server membro gruppo disponibilità database: Exchange 2013 Help'
TOCTitle: Ripristinare un server membro di database availability group
ms:assetid: eccd8f61-9706-4bb7-a62a-ec7c166f8019
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638206(v=EXCHG.150)
ms:contentKeyID: 50481964
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ripristinare un server membro di database availability group

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Se un server cassette postali che è un membro di un gruppo di disponibilità del database (DAG) si perde o in caso contrario ha esito negativo e non è ripristinabile e debba essere sostituita, è possibile eseguire un'operazione di ripristino server. Microsoft Exchange Server 2013 il programma di installazione include l' opzione */m:RecoverServer* che può essere utilizzato per eseguire l'operazione di ripristino server. Eseguire il programma di installazione con i */m:RecoverServer* fa sì che il programma di installazione per leggere le informazioni di configurazione del server da Active Directory per un server con lo stesso nome del server da cui si sta eseguendo il programma di installazione. Al termine della configurazione di server informazioni raccolte dal Active Directory, i file originali Exchange e servizi vengono installati sul server e i ruoli e le impostazioni archiviate nel Active Directory quindi vengono applicate al server.

Per informazioni sulle altre attività di gestione relative ai gruppi di disponibilità del database? vedere [Gestione dei gruppi di disponibilità del database](managing-database-availability-groups-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 30 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Copie del database cassette postali" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Se Exchange è installato in una posizione diversa da quella predefinita, è necessario utilizzare l'opzione di installazione */TargetDir* per specificare il percorso dei file di programma di Exchange. Se non si utilizza l'opzione */TargetDir* , i file di programma Exchange verranno installati nel percorso predefinito (%programfiles%\\Microsoft\\Exchange Server\\V15).
    
    Per determinare il percorso di installazione, procedere come segue:
    
    1.  Aprire ADSIEDIT.MSC o LDP.EXE.
    
    2.  Accedere al percorso seguente: **CN=ExServerName,CN=Servers,CN=First Administrative Group,CN=Administrative Groups,CN=ExOrg Name,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=DomainName,CN=Com**
    
    3.  Fare clic con il pulsante destro del mouse sull'oggetto server Exchange, quindi scegliere **Proprietà**.
    
    4.  Individuare l'attributo **msExchInstallPath**. in cui è memorizzato il percorso di installazione corrente.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo di /m:RecoverServer per il ripristino di un server

1.  Recuperare eventuali impostazioni dell'intervallo di riesecuzione o troncamento per qualsiasi copia del database delle cassette postali esistente sul server in fase di ripristino per mezzo del cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb124924\(v=exchg.150\)):
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  Rimuovere eventuali copie del database delle cassette postali esistenti sul server in fase di ripristino per mezzo del cmdlet [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335119\(v=exchg.150\)):
    
        Remove-MailboxDatabaseCopy DB1\MBX1

3.  Rimuovere la configurazione del server dal gruppo di disponibilità del database utilizzando il cmdlet [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/it-it/library/dd297956\(v=exchg.150\)):
    
        Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
    

    > [!NOTE]
    > Se il membro DAG da rimuovere non è in linea e non è possibile portare in linea, è necessario aggiungere il parametro <EM>ConfigurationOnly</EM> per il comando precedente. Se si utilizza l'opzione <EM>ConfigurationOnly</EM> , è necessario rimuovere anche manualmente il nodo dal cluster.



4.  Reimpostare l'account del computer server in Active Directory. Per ulteriori informazioni, vedere [reimpostare un Account Computer](http://go.microsoft.com/fwlink/p/?linkid=167188).

5.  Aprire una finestra del prompt dei comandi. Utilizzando il supporto di installazione originale, eseguire il comando riportato di seguito:
    
        Setup /m:RecoverServer

6.  Al termine del processo di ripristino, aggiungere il server ripristinato al gruppo di disponibilità del database utilizzando il cmdlet [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/it-it/library/dd298049\(v=exchg.150\)):
    
        Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

7.  Dopo aver aggiunto il server al gruppo di disponibilità del database, è possibile riconfigurare le copie del database delle cassette postali utilizzando il cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd298105\(v=exchg.150\)). Se una delle copie del database aggiunte in precedenza presenta un intervallo di riesecuzione o troncamento superiore a 0, è possibile utilizzare i parametri *ReplayLagTime* e *TruncationLagTime* del cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd298105\(v=exchg.150\)) per riconfigurare tali impostazioni:
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX1
        Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00
        Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -TruncationLagTime 3.00:00:00

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che è stato ripristinato il membro DAG, eseguire le operazioni seguenti:

  - Nella Shell, eseguire il comando seguente per verificare l'integrità e lo stato del membro DAG ripristinato.

       ```
        Test-ReplicationHealth <ServerName>
       ```
       ```
        Get-MailboxDatabaseCopyStatus -Server <ServerName>
       ```

    Tutti i test dello stato di replica deve hanno esito positivo e lo stato dei database e dei relativi indici contenuti deve essere integro.


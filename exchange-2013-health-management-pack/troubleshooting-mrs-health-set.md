---
title: Risoluzione dei problemi di Set di integrità MRS
TOCTitle: Risoluzione dei problemi di Set di integrità MRS
ms:assetid: 21947ed6-1584-4db9-9cd6-f6c1de22e352
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.mrs(v=EXCHG.150)
ms:contentKeyID: 53275532
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di Set di integrità MRS

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

L'integrità del servizio di replica delle cassette postali controlla l'impostazione di integrità complessiva del servizio MRS.

## Descrizione

Il servizio MRS viene monitorato utilizzando i seguenti probe e sistemi di monitoraggio.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Probe</th>
<th>Impostazione di integrità</th>
<th>Dipendenze</th>
<th>Monitor associati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MRSServiceCrashingProbe</p></td>
<td><p>MRS</p></td>
<td><p>Archivio informazioni</p></td>
<td><p>MRSServiceCrashingMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Azione utente

È possibile che il servizio venga ripristinato dopo aver inoltrato l'avviso. Di conseguenza, quando si riceve un avviso che specifica che l'integrità è danneggiata, verificare se il problema persiste. Se il problema persiste, eseguire le azioni di ripristino illustrate nelle seguenti sezioni.

## Verifica della persistenza del problema

1.  Identificare il nome dell'impostazione di integrità e del server nell'avviso.

2.  I dettagli relativi al messaggio forniscono informazioni relative alla causa esatta dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio offrono informazioni sufficienti sulla risoluzione dei problemi per identificare la causa principale. Se i dettagli del messaggio non sono chiari, effettuare le seguenti operazioni:
    
    1.  Aprire Exchange Management Shell, quindi eseguire il seguente comando per recuperare i dettagli dell'impostazione di integrità che ha generato l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli dell'impostazione di integrità di MRS per server1.contoso.com, eseguire il seguente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "MRS"}
    
    2.  Esaminare l'output del comando per determinare in quale monitor viene riportato l'errore. Il valore **AlertValue** relativo al monitor che ha rilasciato l'avviso corrisponde a `Unhealthy`.
    
    3.  Eseguire nuovamente il probe associato al monitor danneggiato. Fare riferimento alla tabella nella sezione Explanation per trovare il probe associato. A tale scopo, eseguire il comando seguente:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si supponga che il sistema di monitoraggio con errori sia **MRSServiceCrashingMonitor**. Il probe associato a tale sistema di monitoraggio è **MRSServiceCrashingProbe**. Per eseguire il probe sul server1.contoso.com, utilizzare il comando indicato di seguito:
        
            Invoke-MonitoringProbe MRS\MRSServiceCrashingProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, controllare il valore **Risultato** del probe. Se il valore è **Riuscito**, il problema consisteva in un errore temporaneo e non esiste più. In caso contrario, fare riferimento alle procedure di ripristino descritte nelle sezioni seguenti.

## Problemi comuni

Quando si riceve un avviso da un'impostazione di integrità, il messaggio di posta elettronica conterrà le seguenti informazioni:

  - Nome del server da cui è stato inviato l'avviso

  - Ora e data in cui è stato generato l'avviso

  - Meccanismo di autenticazione utilizzato e informazioni sulle credenziali

  - La traccia completa delle eccezioni dell'ultimo errore, compresi i dati diagnostici e le informazioni specifiche sull'intestazione HTTP
    
    È possibile utilizzare le informazioni nella traccia completa delle eccezioni per risolvere il problema. L'eccezione generata dal probe include una causa dell'errore che descrive il motivo per cui si è verificato l'errore del probe.

**Cassetta postale bloccata**

Quando una cassetta postale è bloccata, si potrebbe ricevere un avviso analogo al seguente:

*MailboxIdentity: namprd03.prod.outlook.com/Microsoft Exchange Hosted Organizations/example.com/User6 MailboxGuid: Primary (00000000-abcd-01234-5678-1234567890ab) RequestFlags: IntraOrg, Pull, Protected Database: exampledb-db089 Exception: MapiExceptionADUnavailable: impossibile popolare la cache per l'utente …*

Questo indica che una cassetta postale è bloccata. Per sbloccare la cassetta postale, eseguire il comando indicato di seguito:

    New-MailboxRepairRequest -CorruptionType LockedMoveTarget -Identity <mailboxIdentity> [-Archive]

**Nota**   In questo comando, sostituire \<*mailboxIdentity*\> con il nome della cassetta postale fornita nel messaggio di posta elettronica come **MailboxIdentity**. Se la cassetta postale è una cassetta postale per l'archiviazione, è necessario selezionare **–Archivio**. È possibile determinare se una cassetta postale è principale o di archiviazione visualizzando il campo **MailboxGuid** nell'avviso.

**Processo di migrazione corrotto**

Quando un processo di migrazione si corrompe, è possibile ricevere un avviso analogo al seguente:

*Notifica generata da MailboxMigration il 9/7/2012 alle 21:08:32. Dettagli: Informazioni di diagnostica: ProcessCacheEntry: Prima organizzazione: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

La corruzione si verifica quando si presentano problemi nei metadati della migrazione. Dopo la corruzione, Microsoft riceverà un rapporto Watson che verrà verificato. Per effettuare il ripristino dopo il problema, è necessario rimuovere il batch di migrazione e ricreare il batch. A tale scopo, seguire questa procedura:

1.  Per rimuovere un batch corrotto, eseguire il comando riportato di seguito:
    
        Remove-MigrationBatch -Identity

2.  Per creare nuovamente il processo del batch, eseguire il comando riportato di seguito:
    
        New-MigrationBatch -Local -Name

Per ulteriori informazioni, vedere [Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))

**Avviso MailboxMigration: CriticalError**

Quando si verifica un errore critico durante la migrazione della posta, è possibile ricevere un avviso analogo al seguente:

*Notifica generata da MailboxMigration il 9/7/2012 alle 21:08:32. Dettagli: Informazioni di diagnostica: ProcessCacheEntry: Prima organizzazione: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

Per risolvere il problema, è necessario provare nuovamente la migrazione. A tale scopo, eseguire il seguente comando o premere il pulsante **Start** nell'interfaccia di amministrazione di Exchange (EAC).

    Call start-migrationbatch -Identity batchName

Quando si verifica questo problema, un messaggio di Dr. Watson viene inviato a Microsoft per effettuare controlli.

**Il servizio di replica di Microsoft Exchange non è attivo**

Quando viene visualizzato questo errore, è possibile verificare l'integrità del servizio eseguendo il seguente comando:

    Test-MRSHealth <servername> -MonitoringContext:$true

È inoltre possibile provare ad avviare il servizio eseguendo il seguente comando:

    Start-Service msexchangemailboxreplication

**MSExchangeMailboxReplication RCP Ping non riuscito**

Quando viene visualizzato questo messaggio di errore, è possibile ricevere un avviso analogo al seguente:

*Un problema con MRS è stato rilevato il 26/06/2012 6:08:47. Dettagli: Controllo RPC Ping di MRS del server \<NomeServer\> non riuscito con il seguente errore: L'endpoint RPC del servizio di replica delle cassette postali di Microsoft Exchange non risponde:*

Quando si verifica questo errore, è possibile verificare l'integrità del servizio eseguendo il seguente comando:

    Test-MRSHealth <servername> -MonitoringContext:$true

È inoltre possibile provare ad avviare il servizio eseguendo il seguente comando:

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication Service si arresta continuamente in modo anomalo**

Quando il servizio MSExchangeMailboxReplication si arresta in modo anomalo o si blocca, si potrebbe ricevere un avviso analogo al seguente:

*Il processo MRS si è arrestato in modo anomalo almeno 3 volte negli ultimi. \<b\>Messaggio di Dr. Watson:\</b\> Il rapporto Watson sta per essere inviato per l'ID di processo: 41432, con parametri: E12, \<NomeServer\>, 15.00.0516.024, MSExchangeMailboxReplication, M.Exchange.MailboxReplicationService, M.E.M.BaseJob.BeginJob, System.ApplicationException, 7ec9, 15.00.0516.024. ErrorReportingEnabled: True.*

Quando si verifica questo errore, è possibile verificare l'integrità del servizio eseguendo il seguente comando:

    Test-MRSHealth <servername> -MonitoringContext:$true

È inoltre possibile provare ad avviare il servizio eseguendo il seguente comando:

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication non sta analizzando le code MDB**

Quando il servizio MSExchangeMailboxReplication non analizza le code, si potrebbe ricevere un avviso analogo al seguente:

*Un problema con MRS è stato rilevato il 12.06.12 18:20:44. Dettagli: Dettagli: Verifica scansione code MRS per il server \<nomeserver\> non riuscito con il seguente codice di errore: Il servizio di replica delle cassette postali di Microsoft Exchange non cerca processi nelle code del database di cassette postali. Ultima scansione: 04:38:02.1959439..*

Quando si verifica questo errore, è possibile verificare l'integrità del servizio eseguendo il seguente comando:

    Test-MRSHealth <servername> -MonitoringContext:$true

È inoltre possibile provare ad avviare il servizio eseguendo il seguente comando:

    Restart-Service msexchangemailboxreplication

**Ulteriori procedure di risoluzione dei problemi**

1.  Avviare Gestione IIS, quindi connettersi al server che ha riportato il problema per verificare che il pool di applicazioni **MSExchangeServicesAppPool** è in esecuzione.

2.  In Gestione IIS, fare clic su **Pool di applicazioni**, quindi riciclare il pool di applicazioni **MSExchangeServicesAppPool** eseguendo il seguente comando da Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  Eseguire di nuovo il probe associato così come mostrato nel passaggio 2c alla sezione Verifying the issue still exists.

4.  Se il problema persiste, riciclare il servizio IIS tramite l'utilità IISReset oppure eseguendo il seguente comando:
    
        Iisreset /noforce

5.  Eseguire di nuovo il probe associato così come mostrato nel passaggio 2c alla sezione Verifying the issue still exists.

6.  Se il problema persiste, riavviare il server.

7.  Dopo aver riavviato il server, eseguire nuovamente il probe associato come indicato nel passaggio 2c nella sezione Verifying the issue still exists.

8.  Se il probe non funziona, è necessaria l'assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))


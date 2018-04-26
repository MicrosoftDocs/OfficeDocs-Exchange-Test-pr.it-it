---
title: Risoluzione dei problemi di integrità DataProtection impostare
TOCTitle: Risoluzione dei problemi di integrità DataProtection impostare
ms:assetid: cde3cc34-2076-4e30-8d3c-265b66d00ae8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.dataprotection(v=EXCHG.150)
ms:contentKeyID: 53275542
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di integrità DataProtection impostare

 

_**Si applica a:**Exchange Server 2013, Project Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Il set di integrità DataProtection monitora la ridondanza dei database in un gruppo di disponibilità del database (DAG).

Un avviso che specifica che DataProtection non è integro indica un problema che può influire sulla replica o sui componenti del cluster e che può impedire l'accesso ai database di Exchange.

## Descrizione

Il servizio di integrità DataProtection viene monitorato utilizzando i seguenti probe e controlli:


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
<th>Set di integrità</th>
<th>Dipendenze</th>
<th>Controlli associati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ClusterEndpointProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ClusterEndpointMonitor</p></td>
</tr>
<tr class="even">
<td><p>ClusterGroupProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ClusterGroupMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ClusterNetworkProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ClusterNetworkMonitor</p></td>
</tr>
<tr class="even">
<td><p>ClusterServiceCrashProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ClusterServiceCrashMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ServerOneCopyProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Director</p></td>
<td><p>ServerOneCopyMonitor</p></td>
</tr>
<tr class="even">
<td><p>ServerOneCopyInternalMonitorProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServerOneCopyInternalMonitorMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ServiceHealthMSExchangeReplEndpointProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServiceHealthMSExchangeReplEndpointMonitor</p></td>
</tr>
<tr class="even">
<td><p>ServiceHealthMSExchangeReplCrashProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServiceHealthMSExchangeReplCrashMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ServerSiteFailureProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServerSiteFailureMonitor</p></td>
</tr>
<tr class="even">
<td><p>StorageApparentControllerIssuesProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>StorageApparentControllerIssuesMonitor</p></td>
</tr>
<tr class="odd">
<td><p>DatabaseHealthTooManyMountedDatabaseProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>DatabaseHealthTooManyMountedDatabaseMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Azione utente

È possibile che il servizio venga ripristinato dopo l'emissione dell'avviso. Di conseguenza, se si riceve un avviso indicante che il set di integrità non è in integro, verificare prima che il problema sia ancora presente. Se il problema ancora esiste, eseguire le azioni di ripristino appropriate delineate nelle sezioni seguenti.

## Verifica dell'esistenza del problema

1.  Identificare il nome del set di integrità e il nome del server nell'avviso.

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio contengono informazioni di risoluzione dei problemi sufficienti ad identificare la causa principale. Se i dettagli del messaggio non sono chiari, procedere come segue:
    
    1.  Aprire Exchange Management Shell, quindi utilizzare il seguente comando per recuperare i dettagli del set di integrità che ha emesso l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli del set di integrità Autodiscover.Protocol su server1.contoso.com, utilizzare il seguente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover.Protocol"}
        
        Esaminare l'output del comando per determinare quale controllo ha segnalato l'errore. Il valore **AlertValue** del controllo che ha emesso l'avviso sarà `Unhealthy`.
    
    2.  Identificare il probe su cui si basa il controllo. Tenere presente che la maggior parte dei probe ha lo stesso prefisso del nome. Utilizzando l'esempio precedente, cercare \&quot;**ClusterNetwork\***\&quot;:
        
            Get-MonitoringItemIdentity -Identity DataProtection -Server server1.contoso.com | ?{$_.Name -like "ClusterNet ItemType  
            work*"}
        
        I risultati restituiti appariranno simili ai seguenti.
        
        
        <table>
        <colgroup>
        <col style="width: 25%" />
        <col style="width: 25%" />
        <col style="width: 25%" />
        <col style="width: 25%" />
        </colgroup>
        <tbody>
        <tr class="odd">
        <td><p><code>ItemType</code></p></td>
        <td><p><code>HealthSetName</code></p></td>
        <td><p><code>Name</code></p></td>
        <td><p><code>TargetResource</code></p></td>
        </tr>
        <tr class="even">
        <td><p><code>Probe</code></p></td>
        <td><p><code>DataProtection</code></p></td>
        <td><p><code>ClusterNetworkProbe</code></p></td>
        <td><p><code>MSExchangeRepl</code></p></td>
        </tr>
        </tbody>
        </table>
    
    3.  Eseguire di nuovo il probe associato per il controllo in stato non integro. Per trovare il probe associato, fare riferimento alla tabella nella sezione Explanation. A tale scopo, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si presuma che il controllo con l'errore sia **AutodiscoverSelfTestMonitor**. Il probe associato a tale controllo è **AutodiscoverSelfTestProbe**. Per eseguire tale probe su server1.contoso.com, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe Autodiscover.Protocol\AutodiscoverSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, verificare il valore **Result** del probe. Se il valore è **Succeeded**, l'errore era transitorio e non esiste più. Altrimenti, fare riferimento alla procedura di ripristino delineata nella sezioni seguenti.

## Procedura di risoluzione dei problemi

Quando si riceve un avviso da un set di integrità, il messaggio di posta elettronica contiene le informazioni seguenti:

  - Nome del server che ha inviato l'avviso

  - Ora e data in cui si è verificato l'avviso

  - Meccanismo di autenticazione utilizzato e informazioni sulle credenziali

  - Traccia di eccezione completa dell'ultimo errore, inclusi i dati diagnostici e le informazioni specifiche dell'intestazione HTTP
    
    È possibile utilizzare le informazioni contenute nella traccia di eccezione completa per risolvere il problema. L'eccezione generata dal probe contiene una Causa errore che descrive perché il probe non è riuscito.

Per ma maggior parte degli errori che si verificano in ambienti ad alta disponibilità, è possibile eseguire il cmdlet **Test-ReplicationHealth** per la risoluzione dei problemi di cluster, rete, ActiveManager o servizi. Per altri set d integrità o componenti occorre utilizzare altri cmdlet Test-\*.

Ad esempio:

    Test-ReplicationHealth <ServerName>

I risultati restituiti appariranno simili ai seguenti:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><code>Server</code></p></td>
<td><p><code>Check</code></p></td>
<td><p><code>Result</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>ClusterService</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>ReplayService</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>ActiveManager</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>TasksRpcListener</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>TcpListener</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>ServerLocatorService</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>DagMembersUp</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>ClusterNetwork</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>QuorumGroup</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>FileShareQuorum</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>DatabaseRedundancyCheck</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>DatabaseAvailabilityCheck</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>DBCopySuspended</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>DBCopyFailed</code></p></td>
<td><p>Passed</p></td>
</tr>
<tr class="even">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>DBInitializing</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>DBDisconnected</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>DBLogCopyKeepingUp</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;NomeServer&gt;</em></p></td>
<td><p><code>DBLogReplayKeepingUp</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
</tbody>
</table>


Se la colonna **Result** contiene il risultato **Passed**, provare a eseguire di nuovo il probe associato come illustrato nel passaggio 2c della sezione Verifying the issue still exists.

Se il problema ancora esiste, riavviare il server. Dopo il riavvio del server, eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

Se il probe continua a incontrare un errore, chiedere assistenza. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))


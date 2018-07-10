---
title: Risoluzione dei problemi di integrità ActiveSync impostare
TOCTitle: Risoluzione dei problemi di integrità ActiveSync impostare
ms:assetid: 8a0b8b26-b4ef-41b8-8f71-8271c1735a69
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.activesync(v=EXCHG.150)
ms:contentKeyID: 53275550
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di integrità ActiveSync impostare

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

L'impostazione di integrità di Exchange ActiveSync controlla l'integrità complessiva del servizio ActiveSync per i clienti mobili dell'organizzazione. L'impostazione di integrità di ActiveSync è strettamente correlata alle seguenti impostazioni di integrità:

[Risoluzione dei problemi Set di integrità ActiveSync.Protocol](troubleshooting-activesync-protocol-health-set.md)

[Risoluzione dei problemi del set di integrità Troubleshooting ActiveSync.Proxy](troubleshooting-activesync-proxy-health-set.md)

Se si riceve un allarme che indica che l'impostazione di integrità ActiveSync non risulta integra, potrebbe verificarsi un problema che potrebbe impedire agli utenti di accedere alle proprie cassette postali con ActiveSync.

## Descrizione

Il servizio ActiveSync viene controllato tramite i seguenti probe e monitor.


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
<td><p>ActiveSyncCTPProbe</p></td>
<td><p>ActiveSync</p></td>
<td><p>Active Directory</p>
<p>Autenticazione</p>
<p>Autenticazione server Cassette postali</p>
<p>Archivio informazioni</p>
<p>Disponibilità elevata</p>
<p>Rete</p></td>
<td><p>ActiveSyncCTPMonitor (impostazione di integrità di ActiveSync)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncProxyTestProbe</p></td>
<td><p>ActiveSync.Proxy</p></td>
<td><p>-</p></td>
<td><p>ActiveSyncProxyTestMonitor (impostazione di integrità di ActiveSync.Proxy)</p></td>
</tr>
<tr class="odd">
<td><p>ActiveSyncDeepTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticazione</p>
<p>Archivio informazioni</p>
<p>Disponibilità elevata</p></td>
<td><p>ActiveSyncDeepTestMonitor (impostazione di integrità di ActiveSync)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncSelfTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticazione</p></td>
<td><p>ActiveSyncSelfTestMonitor (impostazione di integrità di ActiveSync.Protocol)</p>
<p>RequestsQueuedGt500Monitor (impostazione di integrità di ActiveSync)</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Azione utente

È possibile che il servizio sia stato ripristinato dopo l'emissione dell'allarme. Pertanto, quando si riceve un allarme che specifica che l'impostazione di integrità ActiveSync non è integra, è necessario verificare innanzitutto se il problema sussiste ancora. Se il problema persiste, eseguire le azioni di ripristino appropriate riportate nelle sezioni seguenti.

## Verifica del problema

1.  Identificare il nome dell'impostazione di integrità e il nome del server riportati nell'allarme.

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'allarme. Nella maggior parte dei casi, i dettagli del messaggio forniscono informazioni per la risoluzione dei problemi sufficienti a consentire di identificare la causa principale. Se i dettagli del messaggio non sono chiari, procedere come segue:
    
    1.  Aprire Exchange Management Shell ed eseguire il seguente comando per recuperare i dettagli dell'impostazione di integrità che ha emesso l'allarme:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli dell'impostazione di integrità ActiveSync relativi a server1.contoso.com, eseguire il comando riportato:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "ActiveSync"}
    
    2.  Esaminare l'output comando per stabilire quale monitor ha segnalato l'errore. Il valore **AlertValue** per il monitor che ha emesso l'allarme sarà **Danneggiato**.
    
    3.  Eseguire nuovamente il probe associato per il monitor nello stato danneggiato. Fare riferimento alla tabella nella sezione Explanation per trovare il probe associato. A tale scopo, eseguire il comando seguente:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si supponga che il monitor che riporta l'errore sia **ActiveSyncCTPMonitor**. Il probe associato al monitor è **ActiveSyncCTPProbe**. Per eseguire il probe su server1.contoso.com, eseguire il comando riportato:
        
            Invoke-MonitoringProbe ActiveSync\ActiveSyncCTPProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output comando, esaminare la sezione "Risultato" del probe. Se il valore è **Riuscito**, si è trattato di un errore temporaneo che non sussiste più. In caso contrario, fare riferimento alla procedura di ripristino riportata nelle sezioni seguenti.

## Operazioni di recupero ActiveSyncDeepTestMonitor e ActiveSyncSelfTestMonitor

Questo allarme monitor viene generalmente emesso su server Cassette postali. Per eseguire le azioni di recupero, attenersi alla procedura riportata:

1.  Avviare IIS Manager, quindi eseguire la connessione al server che segnala l'errore. Fare clic su **Pool di applicazioni**, quindi eseguire il riciclo del pool di applicazioni di ActiveSync denominato **MSExchangeSyncAppPool**.

2.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue.

3.  Se il problema persiste, eseguire il riciclo dell'intero servizio IIS tramite l'utilità IISReset.

4.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue.

5.  Se il problema persiste, riavviare il server. A tal fine, eseguire innanzitutto il failover dei database ospitati sul server tramite il seguente comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    Nel seguente codice di esempio e in tutti quelli successivi, sostituire *server1.contoso.com* con il nome del server effettivo.

6.  Quindi, verificare che tutti i database siano stati spostati fuori dal server che segnala il problema. A tale scopo, eseguire il comando seguente:
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status

7.  Se l'output comando del passaggio 6 non mostra copie attive sul server, riavviare il server. Se l'output mostra copie attive, eseguire nuovamente i passaggi 5 e 6.

8.  Dopo il riavvio del server, eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue.

9.  In caso di esito positivo del probe, eseguire il failover dei database eseguendo il comando seguente:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

10. In caso di esito ancora negativo del probe, potrebbe essere necessaria ulteriore assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Operazioni di recupero ActiveSyncCTPMonitor

Questo allarme monitor viene generalmente emesso su Accesso client (CAS, Client Access Server).

1.  Avviare IIS Manager, quindi eseguire la connessione al server che segnala l'errore. Fare clic su **Pool di applicazioni**, quindi eseguire il riciclo del pool di applicazioni di ActiveSync denominato **MSExchangeSyncAppPool**.

2.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue.

3.  Se il problema persiste, eseguire il riciclo dell'intero servizio IIS tramite l'utilità IISReset.

4.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue.

5.  Se il problema persiste, è necessario verificare lo stato di integrità sul server Cassette postali corrispondente. Il nome del server Cassette postali è il valore `_Mbx:` fornito nel messaggio di errore.
    
    1.  Per visualizzare il server Cassette postali appropriato, eseguire il comando riportato. Ad esempio, eseguire il comando seguente per il server Cassette postali denominato mailbox1.contoso.com:
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "ActiveSync*"}
    
    2.  Se uno dei monitor presente nell'elenco dell'output comando viene segnalato come danneggiato, è necessario risolvere prima il problema di tale monitor. A tale scopo, attenersi alla procedura di risoluzione dei problemi riportata nella sezione ActiveSyncDeepTestMonitor and ActiveSyncSelfTestMonitor Recovery Actions.

6.  Se tutti i monitor sul server Cassette postali sono integri, riavviare il server Accesso clienti.

7.  Dopo il riavvio del server, eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue.

8.  In caso di esito ancora negativo del probe, potrebbe essere necessaria ulteriore assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Operazioni di recupero RequestsQueuedGt500Monitor

Questo allarme monitor viene generalmente emesso su server Accesso client.

1.  Avviare IIS Manager, quindi eseguire la connessione al server che segnala l'errore. Fare clic su **Pool di applicazioni**, quindi eseguire il riciclo del pool di applicazioni di ActiveSync denominato **MSExchangeSyncAppPool**.

2.  Attendere 10 minuti per vedere se il monitor rimane integro. Dopo 10 minuti, eseguire il comando riportato per il server appropriato. Ad esempio, eseguire il comando seguente per server1.contoso.com:
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "ActiveSync*"}

3.  Se il problema persiste, eseguire il riciclo dell'intero servizio IIS tramite l'utilità IISReset.

4.  Attendere 10 minuti, quindi eseguire nuovamente il comando mostrato nel passaggio 2 per vedere se il monitor rimane integro.

5.  Se il problema persiste, riavviare il server. Se il server è un server Accesso client, è sufficiente riavviarlo. Se il server è un server Cassette postali, procedere come segue:
    
    1.  Eseguire il failover dei database ospitati sul server. A tale scopo, eseguire il comando seguente:
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **Nota**   Nel seguente codice di esempio e in tutti quelli successivi, sostituire *server1.contoso.com* con il nome del server effettivo.
    
    2.  Verificare che tutti i database siano stati spostati fuori dal server che segnala il problema. A tale scopo, eseguire il comando seguente:
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        Se l'output comando non mostra copie attive sul server, riavviare il server.

6.  Dopo il riavvio del server, attendere 10 minuti, quindi eseguire nuovamente il comando mostrato nel passaggio 2 per determinare se il monitor rimane integro.

7.  Se il monitor rimane integro e se si tratta di un server Cassette postali, eseguire il failover dei database tramite il comando seguente:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

8.  In caso di esito ancora negativo del probe, potrebbe essere necessaria ulteriore assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Exchange ActiveSync](https://technet.microsoft.com/it-it/library/aa998357\(v=exchg.150\))

[Dispositivi mobili](https://technet.microsoft.com/it-it/library/bb232129\(v=exchg.150\))

[Attività di gestione directory virtuale di Exchange ActiveSync](https://technet.microsoft.com/it-it/library/bb125170\(v=exchg.150\))


---
title: Risoluzione dei problemi Set di integrità POP
TOCTitle: Risoluzione dei problemi Set di integrità POP
ms:assetid: 6114e9fe-d037-4cb9-a643-933eb5fabc45
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.pop(v=EXCHG.150)
ms:contentKeyID: 53275535
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi Set di integrità POP

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

L'impostazione di integrità POP monitora lo stato generale e la disponibilità del servizio e della connettività dei client POP3 di Microsoft Exchange. L'impostazione di integrità POP è strettamente legata alle seguenti impostazioni d'integrità:

  - [Risoluzione dei problemi POP. Set di integrità di protocollo](troubleshooting-pop-protocol-health-set.md)

  - [Risoluzione dei problemi POP. Set di integrità proxy](troubleshooting-pop-proxy-health-set.md)

Se viene ricevuto un avviso che specifica la non integrità del servizio POP, ciò ravvisa un problema che può impedire agli utenti di accedere alle proprie cassette postali utilizzando POP3 nell'ambiente di Exchange.

## Descrizione

Il servizio POP è monitorato utilizzando i seguenti probe e monitor.


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
<th>Impostazione d'integrità</th>
<th>Dipendenze</th>
<th>Monitor associati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PopCTPProbe</p></td>
<td><p>POP</p></td>
<td><p>Active Directory</p>
<p>Autenticazione</p>
<p>Autenticazione server Cassette postali</p>
<p>Archivio informazioni</p>
<p>Disponibilità elevata</p>
<p>Rete</p></td>
<td><p>PopCTPMonitor (impostazione di integrità POP)</p></td>
</tr>
<tr class="even">
<td><p>PopProxyTestProbe</p></td>
<td><p>POP.Proxy</p></td>
<td><p>Nessuno</p></td>
<td><p>PopProxyTestMonitor (impostazione di integrità POP.Proxy)</p></td>
</tr>
<tr class="odd">
<td><p>PopDeepTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticazione</p>
<p>Archivio informazioni</p>
<p>Disponibilità elevata</p></td>
<td><p>PopDeepTestMonitor (impostazione di integrità POP.Protocol)</p></td>
</tr>
<tr class="even">
<td><p>PopSelfTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>Nessuno</p></td>
<td><p>PopSelfTestMonitor (impostazione di integrità POP.Protocol)</p>
<p>AverageCommandProcessingTimeGt60sMonitor (impostazione di integrità POP)</p></td>
</tr>
</tbody>
</table>


## Azione utente

È possibile che il servizio venga ripristinato dopo aver inoltrato l'avviso. Pertanto, quando si visualizza un avviso che specifica che l'impostazione di integrità è venuta a mancare, verificare innanzitutto che il problema esiste effettivamente. Se il problema esiste, effettuare le azioni di ripristino appropriate descritte nelle sezioni che seguono.

## Verifica della persistenza del problema

1.  Identificare il nome dell'impostazione di integrità e del server nell'avviso.

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio offrono informazioni sufficienti sulla risoluzione dei problemi per identificare la causa principale. Se i dettagli del messaggio non sono chiari, effettuare le seguenti operazioni:
    
    1.  Aprire Exchange Management Shell, quindi eseguire il seguente comando per recuperare i dettagli dell'impostazione di integrità che ha generato l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli dell'impostazione d'integrità POP su server1.contoso.com, eseguire il seguente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "POP"}
    
    2.  Controllare l'output del comando per determinare quale monitor abbia segnalato l'errore. Il valore **AlertValue** del sistema di monitoraggio che ha emesso l'avviso sarà `Unhealthy`.
    
    3.  Eseguire nuovamente il probe associato per il sistema di monitoraggio che si trova in uno stato non integro. Fare riferimento alla tabella nella sezione Explanation per trovare il probe associato. A tale scopo, eseguire il comando seguente:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si supponga che il sistema di monitoraggio con errori sia **PopCTPMonitor**. Il probe associato a tale sistema di monitoraggio è **PopCTPProbe**. Per eseguire il probe sul server1.contoso.com, utilizzare il comando indicato di seguito:
        
            Invoke-MonitoringProbe POP\PopCTPProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, controllare il valore del probe **Risultato**. Se il valore è **Completato**, il problema risulta superato poiché si trattava di un errore temporaneo. In caso contrario, fare riferimento alle procedure di ripristino descritte nelle sezioni seguenti.

## Azioni di recupero di PopTestDeepMonitor e PopSelfTestMonitor

L'avviso del monitor è in genere rilasciato sui server Cassette postali.

1.  Riavviare il servizio back-end POP3. Per ulteriori informazioni, vedere [Avviare e arrestare i servizi POP3](https://technet.microsoft.com/it-it/library/aa997475\(v=exchg.150\)).

2.  Eseguire nuovamente il probe associato così come mostrato nel passaggio 2c nella sezione Verifying the issue still exists.

3.  Se il probe non funziona, eseguire il failover dei database ospitati sul server Cassette postali tramite il seguente comando:
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  Dopo che tutti i database vengono rimossi dal server Cassette postali, è necessario verificare che i database siano stati spostati correttamente. A tale scopo, eseguire il comando seguente:
    
        Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status

5.  Assicurarsi che il server non ospiti alcuna copia attiva del database. Quindi riavviare il server.

6.  Dopo che il server è stato riavviato correttamente, eseguire nuovamente il probe associato così come mostrato nel passaggio 2c alla sezione Verifying the issue still exists.

7.  Se il probe funziona correttamente, effettuare il failover dei database eseguendo il comando seguente:
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

8.  Se il probe ancora non funziona correttamente, è necessaria l'assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Azioni di recupero di POPCTPMonitor

L'avviso del monitor è in genere rilasciato sui server Accesso client.

1.  Riavviare il servizio POP3 sui server che eseguono il ruolo di server Accesso client. Per ulteriori informazioni, vedere [Avviare e arrestare i servizi POP3](https://technet.microsoft.com/it-it/library/aa997475\(v=exchg.150\)).

2.  Eseguire di nuovo il probe associato così come mostrato nel passaggio 2c alla sezione Verifying the issue still exists.

3.  Se il problema persiste, eseguire i seguenti comandi in Windows PowerShell:
    
    1.  ``` 
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $true
        ```
    
    2.  Riavviare il servizio POP3 sui server che eseguono il ruolo del server Accesso client.
    
    3.  Eseguire di nuovo il probe associato così come mostrato nel passaggio 2c alla sezione Verifying the issue still exists.
    
    4.  Eseguire il seguente comando, quindi trovare il percorso del file di registro:
        
            Get-PopSettings -server <CAS server name>
    
    5.  Eseguire il seguente comando per determinare quale cassetta postale utilizza il comando confrontando data e ora con il probe:
        
            Get-ServerHealth <mailbox server name> | ?{ $_.HealthSetName -like "POP*"}
    
    6.  Se uno qualsiasi di questi server è segnalato come non integro, seguire la procedura descritta nella sezione PopTestDeepMonitor and PopSelfTestMonitor Recovery Actions.

4.  Se il server Cassette postali viene segnalato come integro, riavviare il server Accesso client.

5.  Dopo il riavvio del server, eseguire nuovamente il probe associato così come descritto al passaggio 2c nella sezione Verifying the issue still exists.

6.  Disattivare la registrazione del protocollo eseguendo il seguente comando:
    
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  Riavviare il servizio POP3 sui server che eseguono il ruolo di server Accesso client. Per ulteriori informazioni, vedere [Avviare e arrestare i servizi POP3](https://technet.microsoft.com/it-it/library/aa997475\(v=exchg.150\)).

8.  Se il probe non funziona ancora, è necessaria l'assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Azioni di recupero PopProxyTestMonitor

1.  Riavviare il servizio POP3 sui server che eseguono il ruolo di server Accesso client. Per ulteriori informazioni, vedere [Avviare e arrestare i servizi POP3](https://technet.microsoft.com/it-it/library/aa997475\(v=exchg.150\)).

2.  Eseguire di nuovo il probe associato così come mostrato nel passaggio 2c alla sezione Verifying the issue still exists.

3.  Se il probe non funziona, riavviare il server Accesso client.

4.  Dopo il riavvio del server, eseguire nuovamente il probe associato così come descritto al passaggio 2c nella sezione Verifying the issue still exists.

5.  Se il probe non funziona, è necessaria l'assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Azioni di recupero di AverageCommandProcessingTimeGt60sMonitor

Questo avviso del monitor è in genere rilasciato sui server Accesso client e Cassette postali.

1.  Riavviare il servizio POP3 sui server Accesso client e Cassette postali. Per ulteriori informazioni, vedere [Avviare e arrestare i servizi POP3](https://technet.microsoft.com/it-it/library/aa997475\(v=exchg.150\)).

2.  Attendere 10 minuti per vedere se il monitor rimane in uno stato di integrità. Dopo 10 minuti, eseguire il seguente comando (nell'esempio viene utilizzato il server1.contoso.com).
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "POP*"}

3.  Se il problema persiste, è necessario riavviare il server. Se il server è un server Accesso client, è sufficiente riavviarlo. Se il server è un server Cassette postali, è necessario il failover del database e verificare i risultati. A tale scopo, seguire questa procedura:
    
    1.  Eseguire il failover dei database ospitati sul server utilizzando il seguente comando:
        
            Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **Nota**   In questo e in tutti gli esempi di codice successivi, sostituire *server1.contoso.com* con il nome effettivo del server.
    
    2.  Verificare che tutti i database siano stati spostati dal server che ha segnalato il problema. A tale scopo, eseguire il comando seguente:
        
            Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status
        
        Se l'output del comando non mostra le copie attive sul server, riavviare il server.

4.  Dopo il riavvio del server, attendere 10 minuti, quindi eseguire di nuovo il comando mostrato nel passaggio 2 per vedere se il monitor rimane in uno stato integro.

5.  Se il monitor è integro e il server è di Cassette postali, rieseguire il failover dei database sul server Cassette postali utilizzando il seguente comando:
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

6.  Se il probe non funziona, è necessaria l'assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Avviare e arrestare i servizi POP3](https://technet.microsoft.com/it-it/library/aa997475\(v=exchg.150\))

[Test-PopConnectivity](https://technet.microsoft.com/it-it/library/bb738143\(v=exchg.150\))


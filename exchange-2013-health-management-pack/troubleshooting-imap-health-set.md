---
title: Risoluzione dei problemi Set di integrità IMAP
TOCTitle: Risoluzione dei problemi Set di integrità IMAP
ms:assetid: 2a06e671-4cc2-4ce5-bf53-6243ea140f20
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.imap(v=EXCHG.150)
ms:contentKeyID: 53275547
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi Set di integrità IMAP

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

L'impostazione di integrità IMAP controlla la disponibilità dell'infrastruttura proxy IMAP4 sul server CAS (server Accesso client). L'impostazione di integrità IMAP è strettamente correlata alle seguenti impostazioni di integrità:

[Risoluzione dei problemi IMAP. Set di integrità di protocollo](troubleshooting-imap-protocol-health-set.md)

[Risoluzione dei problemi IMAP. Set di integrità proxy](troubleshooting-imap-proxy-health-set.md)

Se si riceve un avviso il quale specifica che IMAP è danneggiato, si sta verificando un problema che impedisce agli utenti di accedere alle proprie cassette postali utilizzando IMAP.

## Descrizione

Il servizio IMAP4 viene monitorato utilizzando i seguenti monitor e probe.


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
<th>Sistemi di monitoraggio associati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ImapCTPProbe</p></td>
<td><p>IMAP</p></td>
<td><p>Active Directory</p>
<p>Autenticazione</p>
<p>Autenticazione del server Cassette postali</p>
<p>Disponibilità elevata</p>
<p>Rete</p></td>
<td><p>ImapCTPMonitor (impostazione di integrità IMAP)</p></td>
</tr>
<tr class="even">
<td><p>ImapProxyTestProbe</p></td>
<td><p>Proxy IMAP</p></td>
<td><p>Active Directory</p>
<p>Autenticazione</p></td>
<td><p>ImapProxyTestMonitor (impostazione di integrità IMAP.Proxy)</p></td>
</tr>
<tr class="odd">
<td><p>ImapDeepTestProbe</p></td>
<td><p>Protocollo IMAP</p></td>
<td><p>Active Directory</p>
<p>Autenticazione</p>
<p>Archivio informazioni</p>
<p>Disponibilità elevata</p></td>
<td><p>IMAP.Protocol (impostazione di integrità IMAP.Protocol)</p></td>
</tr>
<tr class="even">
<td><p>ImapSelfTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticazione</p></td>
<td><p>IMAP.Protocol (impostazione di integrità IMAP.Protocol)</p>
<p>Tempo medio di elaborazione dei comandi su monitor Gt60 (impostazione di integrità IMAP)</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Azione utente

È possibile che il servizio venga ripristinato dopo la pubblicazione dell'avviso. Di conseguenza, quando si riceve un avviso che specifica che l'integrità è danneggiata, verificare se il problema persiste. Se il problema persiste, eseguire le azioni di ripristino illustrate nelle seguenti sezioni.

## Verifica della persistenza del problema

1.  Identificare il nome dell'impostazione di integrità e del server nell'avviso.

2.  I dettagli del messaggio forniscono informazioni sull'esatta causa dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio offrono informazioni sufficienti sulla risoluzione dei problemi per identificare la causa principale. Se le informazioni contenute nel messaggio non sono chiare, effettuare le seguenti operazioni:
    
    1.  Aprire Exchange Management Shell ed eseguire il comando per il recupero delle informazioni relative all'impostazione di integrità che ha causato l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli dell'impostazione di integrità IMAP relativi a server1.contoso.com, eseguire il comando seguente:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    2.  Verificare l'output del comando per determinare in quale monitor viene riportato l'errore. Il **Valore avviso** dell'avviso riportato nel monitor sarà `Unhealthy`.
    
    3.  Eseguire nuovamente il probe associato al monitor danneggiato. Fare riferimento alla tabella nella sezione Explanation per individuare il probe associato. A tale scopo, eseguire il comando seguente:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si ipotizzi che il monitor danneggiato è **ImapCTPMonitor**. Il probe associato al monitor sarà **ImapCTPProbe**. Per eseguire il probe su server1.contoso.com, eseguire il comando seguente:
        
            Invoke-MonitoringProbe IMAP\ImapCTPProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, verificare il valore **Risultato** del probe. Se il valore è **Riuscito**, il problema consisteva in un errore temporaneo e non esiste più. In caso contrario, fare riferimento alle azioni di ripristino descritte nelle sezioni riportate di seguito.

## Azioni di ripristino ImapTestDeepMonitor e ImapSelfTestMonitor

1.  Riavviare il servizio IMAP4 Exchange sul server back-end. Per ulteriori informazioni su come arrestare e avviare il servizio IMAP4, vedere [Avviare e arrestare i servizi IMAP4](https://technet.microsoft.com/it-it/library/bb124022\(v=exchg.150\)).

2.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

3.  Se il problema persiste, è necessario eseguire il failover dei database ospitati sul server della cassetta postale utilizzando il comando seguente:
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  Assicurarsi che tutti i database siano stati rimossi dal server nel quale si è verificato il problema. A tale scopo, eseguire il comando seguente:
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    Se l'output del comando mostra le copie del server non attive, riavviare il server.

5.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

6.  Se il probe riesce, eseguire il failover del database utilizzando il comando seguente:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  Se il probe non riesce, potrebbe essere necessaria l'assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Azioni di ripristino ImapCTPMonitor

Generalmente, questo avviso si verifica nei server CAS.

1.  Riavviare il servizio IMAP4 Exchange sul server back-end. Per ulteriori informazioni su come arrestare e avviare il servizio IMAP4, vedere [Avviare e arrestare i servizi IMAP4](https://technet.microsoft.com/it-it/library/bb124022\(v=exchg.150\))

2.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2.c della sezione Verifying the issue still exists.

3.  Se il problema persiste, è necessario attivare la registrazione del protocollo IMAP per risolvere il problema. A tale scopo, seguire questa procedura:
    
    1.  In Windows PowerShell, eseguire il comando seguente:
        
            Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $true
    
    2.  Riavviare il servizio IMAP4 Exchange sul server back-end. Per ulteriori informazioni su come arrestare e avviare il servizio IMAP4, vedere [Avviare e arrestare i servizi IMAP4](https://technet.microsoft.com/it-it/library/bb124022\(v=exchg.150\))
    
    3.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.
    
    4.  Eseguire il comando seguente, quindi stabilire il percorso del file di registro. A tale scopo, eseguire il comando seguente:
        
            Get-ImapSettings -server <CAS server name>
    
    5.  Individuare la cassetta postale che dispone di questo comando. Il nome del server della cassetta postale è il valore `_Mbx:` contenuto nel messaggio di errore.
    
    6.  Eseguire il comando seguente:
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "IMAP*"}
        
        **Nota**In questo comando, sostituire *mailbox1.contoso.com* con il nome attuale del server Cassetta postale.
    
    7.  Se alcuni dei monitor elencati nell'output del comando vengono riportati come danneggiati, è necessario indirizzarli. Eseguire i passaggi riportati nella sezione ImapTestDeepMonitor and ImapSelfTestMonitor Recovery Actions per la risoluzione dei problemi.

4.  Se il server Cassetta postale è riportato come integro, riavviare il CAS.

5.  Dopo aver riavviato il server, eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

6.  Disattivare la registrazione del protocollo. A tale scopo, eseguire il comando Windows PowerShell:
    
        Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  Riavviare il servizio IMAP4.

8.  Se il probe non riesce, potrebbe essere necessaria l'assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Azioni di ripristino ImapProxyTestMonitor

1.  Riavviare il servizio IMAP4.

2.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

3.  Se il probe non riesce, riavviare il CAS.

4.  Dopo aver riavviato il server, eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

5.  Se il probe non riesce, potrebbe essere necessaria l'assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Azione di ripristino QueuedGt500Monitor per il tempo medio di elaborazione dei comandi su monitor Gt60

Generalmente, questo avviso si verifica nei server CAS e Cassetta postale.

1.  Riavviare il servizio IMAP4 Exchange sul server back-end o CAS. Per ulteriori informazioni su come arrestare e avviare il servizio IMAP4, vedere [Avviare e arrestare i servizi IMAP4](https://technet.microsoft.com/it-it/library/bb124022\(v=exchg.150\))

2.  Attendere 10 minuti per verificare se il monitor funziona correttamente. Al termine dei 10 minuti, eseguire il comando seguente:
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    **Nota**   In questo comando, sostituire *server1.contoso.com* con il nome attuale del server.

3.  Attendere 10 minuti, quindi eseguire il comando riportato nel passaggio 2 per verificare se il monitor funziona correttamente.

4.  Se il problema persiste, è necessario riavviare il server. Se si tratta del server CAS, riavviarlo semplicemente. Se si tratta del server Cassetta postale, procedere come segue:
    
    1.  Eseguire il failover dei database ospitati sul server. A tale scopo, eseguire il comando seguente:
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **Nota**   In questi esempi di codice e in tutti i successivi, sostituire *server1.contoso.com* con il nome effettivo del server.
    
    2.  Assicurarsi che tutti i database siano stati rimossi dal server nel quale si è verificato il problema. A tale scopo, eseguire il comando seguente:
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        Se l'output del comando mostra le copie del server non attive, riavviare il server.

5.  Dopo aver riavviato il server, attendere 10 minuti, quindi eseguire il comando riportato nel passaggio 2 per verificare se il monitor funziona correttamente.

6.  Se il monitor funziona correttamente e se si tratta di un server Cassetta postale, eseguire il failover dei database utilizzando il comando seguente:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  Se il probe non riesce, potrebbe essere necessaria l'assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[POP3 e IMAP4 in Exchange Server 2013](https://technet.microsoft.com/it-it/library/jj657728\(v=exchg.150\))

[Abilitazione di IMAP4 in Exchange 2013](https://technet.microsoft.com/it-it/library/bb124489\(v=exchg.150\))

[Test-ImapConnectivity](https://technet.microsoft.com/it-it/library/bb738126\(v=exchg.150\))


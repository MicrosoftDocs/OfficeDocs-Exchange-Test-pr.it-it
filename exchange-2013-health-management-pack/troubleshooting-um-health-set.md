---
title: Risoluzione dei problemi di messaggistica unificata Set di integrità
TOCTitle: Risoluzione dei problemi di messaggistica unificata Set di integrità
ms:assetid: db947791-63ce-45dd-8634-1dfa5f55e2c2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.um(v=EXCHG.150)
ms:contentKeyID: 53275555
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di messaggistica unificata Set di integrità

 

_**Si applica a:** Exchange Server 2013, Project Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Il set di integrità Unified Messaging (UM) monitora lo stato generale del servizio di messaggistica unificata nell'organizzazione.

Un avviso che specifica che UM non è integro indica un problema che potrebbe impedire agli utenti di utilizzare il servizio di messaggistica unificata nell'organizzazione. Il set di integrità UM è strettamente correlato ai seguenti set di integrità:

[Risoluzione dei problemi di messaggistica unificata. Set di integrità CallRouter](troubleshooting-um-callrouter-health-set.md)

[Risoluzione dei problemi di messaggistica unificata. Set di integrità di protocollo](troubleshooting-um-protocol-health-set.md)

## Descrizione

Il servizio di messaggistica unificata viene monitorato utilizzando i seguenti probe e controlli.


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
<td><p>UMSelfTestProbe</p></td>
<td><p>UM.Protocol</p></td>
<td><p>Active Directory Servizi di dominio (AD DS)</p></td>
<td><p>UMSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>UMCallRouterTestProbe</p></td>
<td><p>UM.CallRouter</p></td>
<td><p>Active Directory Servizi di dominio (AD DS)</p></td>
<td><p>UMCallRouterTestMonitor</p></td>
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
        
        Ad esempio, per recuperare i dettagli del set di integrità UM.Protocol su server1.contoso.com, utilizzare il seguente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  Esaminare l'output del comando per determinare quale controllo ha segnalato l'errore. Il valore **AlertValue** del controllo che ha emesso l'avviso sarà `Unhealthy`.
    
    3.  Eseguire di nuovo il probe associato per il controllo in stato non integro. Per trovare il probe associato, fare riferimento alla tabella nella sezione Explanation. A tale scopo, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si presuma che il controllo con l'errore sia **UMSelfTestMonitor**. Il probe associato a tale controllo è **UMSelfTestProbe**. Per eseguire tale probe su server1.contoso.com, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, verificare il valore **Result** del probe. Se il valore è **Succeeded**, l'errore era transitorio e non esiste più. Altrimenti, fare riferimento alla procedura di ripristino delineata nella sezioni seguenti.

## Procedura di risoluzione dei problemi

Quando si riceve un avviso da un set di integrità, il messaggio di posta elettronica contiene le informazioni seguenti:

  - Nome del server che ha inviato l'avviso

  - Ora e data in cui si è verificato l'avviso

  - Meccanismo di autenticazione utilizzato e informazioni sulle credenziali

  - Traccia di eccezione completa dell'ultimo errore, inclusi i dati diagnostici e le informazioni specifiche dell'intestazione HTTP
    
    **Nota**   È possibile utilizzare le informazioni contenute nella traccia di eccezione completa per risolvere il problema. L'eccezione generata dal probe contiene una Causa errore che descrive perché il probe non è riuscito.

**Opzioni Sip per il servizio di messaggistica unificata non riuscite**

Controllare se il servizio di messaggistica unificata è stato disabilitato. Se il servizio non è stato avviato o è stato disabilitato, riavviarlo.

**Più del {0}% di chiamate in ingresso rifiutate dal servizio di messaggistica unificata nell'ultima ora**

Esaminare i registri eventi sul server Accesso client per stabilire se gli oggetti di messaggistica unificata, ad esempio **umipgateway** e **umhuntgroup**, sono stati configurati correttamente.

Se i registri eventi non contengono informazioni sufficienti, è possibile abilitare i registri eventi di messaggistica unificata a livello Esperto ed esaminare quindi i file di registro traccia di messaggistica unificata.

** Più del {0}% di chiamate in ingresso rifiutate dal processo di lavoro di messaggistica unificata nell'ultima ora**

Esaminare i registri eventi sul server Accesso client per stabilire se gli oggetti di messaggistica unificata, ad esempio **umipgateway** e **umhuntgroup**, sono stati configurati correttamente.

Se i registri eventi non contengono informazioni sufficienti, è possibile abilitare i registri eventi di messaggistica unificata a livello Esperto ed esaminare quindi i file di registro traccia di messaggistica unificata.

**Meno del {0}% di messaggi elaborati correttamente nell'ultima ora**

Esaminare i registri eventi sul server Accesso client per stabilire se gli oggetti di messaggistica unificata, ad esempio **umipgateway** e **umhuntgroup**, sono stati configurati correttamente.

Se i registri eventi non contengono informazioni sufficienti, è possibile abilitare i registri eventi di messaggistica unificata a livello Esperto ed esaminare quindi i file di registro traccia di messaggistica unificata.

**Il servizio di messaggistica unificata di Microsoft Exchange ha rifiutato una chiamata perché la pipeline di messaggistica unificata è piena**

Esaminare i registri eventi sul server Accesso client per stabilire se gli oggetti di messaggistica unificata, ad esempio **umipgateway** e **umhuntgroup**, sono stati configurati correttamente.

Se i registri eventi non contengono informazioni sufficienti, è possibile abilitare i registri eventi di messaggistica unificata a livello Esperto ed esaminare quindi i file di registro traccia di messaggistica unificata.

**Il servizio A/V Edge non è configurato correttamente o non è in esecuzione**

1.  Esaminare i registri eventi sul server Cassette postali per stabilire perché le chiamate dal server Lync non riescono. Quindi, eseguire la procedura riportata di seguito:
    
      - Accertarsi che il pool Lync selezionato dal servizio di messaggistica unificata sia operativo.
    
      - Per utilizzare uno specifico server Lync, utilizzare il comando seguente:
        
            Set-UMServer ExchangeUMServer -SIPAccessService <ServerName>

**Il server di messaggistica unificata non è stato in grado di acquisire le credenziali correttamente con il servizio A/V Edge di Communications Server**

Esaminare i registri eventi per scoprire quale pool Lync è stato selezionato e se è operativo.

**Audio/Video Edge di Communications Server non è stato in grado di aprire una porta o allocare risorse durante il tentativo di stabilire una sessione**

Esaminare i registri eventi per scoprire quale pool Lync è stato selezionato e se è operativo.

**Il certificato del servizio di messaggistica unificata di Microsoft Exchange sta per scadere**

Rinnovare il certificato di messaggistica unificata sul server Cassette postali.

**Ulteriori passaggi per la risoluzione dei problemi:** 

1.  Avviare Gestione IIS, quindi connettersi al server che segnala l'errore per determinare se il pool di applicazioni **MSExchangeServicesAppPool** è in esecuzione.

2.  In Gestione IIS fare clic su **Pool di applicazioni** e riavviare il pool di applicazioni **MSExchangeServicesAppPool**. A tale scopo, utilizzare il seguente comando da Exchange Management Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  Eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

4.  Se il problema ancora esiste, riavviare il servizio IIS utilizzando l'utilità IISReset o il seguente comando:
    
        Iisreset /noforce

5.  Eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

6.  Se il problema ancora esiste, riavviare il server.

7.  Dopo il riavvio del server, eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

8.  Se il probe continua a incontrare un errore, chiedere assistenza. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))


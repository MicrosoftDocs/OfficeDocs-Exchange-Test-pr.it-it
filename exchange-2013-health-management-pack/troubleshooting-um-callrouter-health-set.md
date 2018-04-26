---
title: Risoluzione dei problemi di messaggistica unificata. Set di integrità CallRouter
TOCTitle: Risoluzione dei problemi di messaggistica unificata. Set di integrità CallRouter
ms:assetid: 444a9038-0952-4823-98fb-99fa59f4a378
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.um.callrouter(v=EXCHG.150)
ms:contentKeyID: 53275546
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di messaggistica unificata. Set di integrità CallRouter

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

L'impostazione di integrità del routing di chiamate di messaggistica unificata di Microsoft Exchange monitora lo stato del servizio di routing di chiamate di messaggistica unificata.

Se si riceve un avviso il quale specifica che la messaggistica unificata è danneggiata, significa che si sta verificando un problema che impedisce agli utenti di utilizzare il servizio di messaggistica unificata all'interno dell'organizzazione. L'impostazione di integrità di messaggistica unificata è strettamente correlata alle seguenti integrità impostate:

[Risoluzione dei problemi di messaggistica unificata Set di integrità](troubleshooting-um-health-set.md)

[Risoluzione dei problemi di messaggistica unificata. Set di integrità di protocollo](troubleshooting-um-protocol-health-set.md)

## Descrizione

Il servizio UM.Protocol viene monitorato utilizzando i seguenti monitor e probe


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
<td><p>UMCallRouterTestProbe</p></td>
<td><p>Routing di chiamate di messaggistica unificata</p></td>
<td><p>Servizi di dominio Active Directory (AD DS)</p></td>
<td><p>UMCallRouterTestMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Azione utente

È possibile che il servizio venga ripristinato dopo la pubblicazione dell'avviso. Di conseguenza, quando si riceve un avviso che specifica che l'integrità è danneggiata, verificare se il problema persiste. Se il problema persiste, eseguire le azioni di ripristino illustrate nelle seguenti sezioni.

## Verifica della persistenza del problema

1.  Identificare il nome dell'integrità impostata e del server nell'avviso.

2.  I dettagli del messaggio forniscono informazioni sull'esatta causa dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio offrono informazioni sufficienti sulla risoluzione dei problemi per identificare la causa principale. Se le informazioni contenute nel messaggio non sono chiare, effettuare le seguenti operazioni:
    
    1.  Aprire Exchange Management Shell ed eseguire il comando per il recupero delle informazioni relative all'impostazione di integrità che ha causato l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli dell'impostazione di integrità di UM.CallRouter relativi a server1.contoso.com, eseguire il comando seguente:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.CallRouter"}
    
    2.  Verificare l'output del comando per determinare in quale monitor viene riportato l'errore. Il **Valore avviso** dell'avviso riportato nel monitor sarà `Unhealthy`.
    
    3.  Eseguire nuovamente il probe associato al monitor danneggiato. Fare riferimento alla tabella nella sezione Explanation per individuare il probe associato. A tale scopo, eseguire il comando seguente:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si supponga che il sistema di monitoraggio con errori sia **UMCallRouterTestMonitor**. Il probe associato a tale sistema di monitoraggio è **UMCallRouterTestProbe**. Per eseguire il probe su server1.contoso.com, eseguire il comando seguente:
        
            Invoke-MonitoringProbe UM.CallRouter\UMCallRouterTestMonitor -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, verificare il valore **Risultato** del probe. Se il valore è **Riuscito**, il problema consisteva in un errore temporaneo e non esiste più. In caso contrario, fare riferimento alle azioni di ripristino descritte nelle sezioni riportate di seguito.

## Istruzioni per la risoluzione dei problemi

Quando si riceve un avviso da un'impostazione di integrità, il messaggio di posta elettronica conterrà le seguenti informazioni:

  - Nome del server che ha inviato l'avviso

  - Ora e data in cui è stato generato l'avviso

  - Meccanismo di autenticazione utilizzato e informazioni sulle credenziali

  - Traccia completa dell'eccezione dell'ultimo errore, compresi i dati diagnostici e informazioni specifiche sull'intestazione HTTP
    
    **Nota**   È possibile utilizzare le informazioni nella traccia completa dell'eccezione per risolvere il problema. L'eccezione generata dal probe contiene un motivo errore che spiega l'errore del probe.

**Errore nelle opzioni Sip per il servizio di routing di chiamate di messaggistica unificata**

Stabilire se il servizio di routing di chiamate di messaggistica unificata è disattivo. Se il servizio di routing di chiamate di messaggistica unificata non è stato avviato o è disattivo, riavviare il servizio Messaggistica unificata.

**Nell'ultima ora, più del 50% delle chiamate in ingresso sono state rifiutate dal routing di chiamate di messaggistica unificata**

Esaminare il registro eventi sul server Accesso client per stabilire se gli oggetti di messaggistica unificata come ad esempio **umipgateway** e **umhuntgroup**, sono configurati correttamente.

Se il registro eventi non contiene informazioni sufficienti, è necessario impostare il livello del registro eventi di messaggistica unificata su Massimo e controllare i file registri analisi di messaggistica unificata.

**Più del {0}% di notifiche proxy di chiamata senza risposta non riuscite sul routing di chiamata di messaggistica unificata nell'ultima ora.**

Esaminare il registro eventi sul server CAS per stabilire se gli oggetti di messaggistica unificata come ad esempio **umipgateway** e **umhuntgroup**, sono configurati correttamente.

Se il registro eventi non contiene informazioni sufficienti, è necessario impostare il livello del registro eventi di messaggistica unificata su Massimo e controllare i file registri analisi di messaggistica unificata.

**Il certificato del routing delle chiamate di messaggistica unificata di Microsoft Exchange sta per scadere**

Rinnovare il certificato del servizio di routing delle chiamate di messaggistica unificata sul CAS.

**Istruzioni aggiuntive per la risoluzione dei problemi:**

1.  Avviare Gestione Internet Information Services (IIS) e collegare il server sul quale si verifica il problema per stabilire se il pool di applicazioni **MSExchangeServicesAppPool** è in esecuzione.

2.  In Gestione Internet Information Services (IIS), fare clic su **Pool di applicazioni**, quindi riciclare il pool di applicazioni **MSExchangeServicesAppPool** eseguendo il comando riportato di seguito da Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

4.  Se il problema persiste, riciclare il servizio Internet Information Services utilizzando l'utilità IISReset o eseguendo il comando seguente:
    
        Iisreset /noforce

5.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

6.  Se il problema persiste, riavviare il server.

7.  Dopo aver riavviato il server, eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

8.  Se il probe non riesce, potrebbe essere necessaria l'assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))


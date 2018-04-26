---
title: Risoluzione dei problemi di OWA. Set di integrità proxy
TOCTitle: Risoluzione dei problemi di OWA. Set di integrità proxy
ms:assetid: 1eaa26ad-b489-402a-ad2d-bfae3b083f42
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.owa.proxy(v=EXCHG.150)
ms:contentKeyID: 53275540
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di OWA. Set di integrità proxy

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

L'impostazione di integrità OWA.Proxy controlla l'integrità complessiva del servizio Outlook Web App.

Se si riceve un avviso che specifica che OWA.Proxy non è integro, ciò indica l'esistenza di un problema che potrebbe impedire agli utenti di utilizzare il servizio Outlook Web App.

## Descrizione

Il servizio Outlook Web App viene monitorato utilizzando i seguenti probe e sistemi di monitoraggio.


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
<td><p>OWAProxyTestProbe</p></td>
<td><p>OWA.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OWAProxyTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>OWAanonymouscalendarProbe</p></td>
<td><p>OWA.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OWAProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e sistemi di monitoraggio, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Problemi comuni

Il non funzionamento del probe potrebbe essere dovuto a una delle seguenti cause:

  - Il pool di applicazioni ospitato ne server Accesso client monitorato non funziona correttamente.

  - Le credenziali dell'account di monitoraggio non sono corrette.

  - I controller di dominio non rispondono.

## Azione utente

È possibile che il servizio venga ripristinato dopo aver inoltrato l'avviso. Di conseguenza, quando si riceve un avviso che specifica che l'integrità è danneggiata, verificare se il problema persiste. Se il problema persiste, eseguire le azioni di ripristino illustrate nelle seguenti sezioni.

## Verifica della persistenza del problema

1.  Identificare il nome dell'impostazione di integrità e del server nell'avviso.

2.  I dettagli relativi al messaggio forniscono informazioni relative alla causa esatta dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio offrono informazioni sufficienti sulla risoluzione dei problemi per identificare la causa principale. Se i dettagli del messaggio non sono chiari, effettuare le seguenti operazioni:
    
    1.  Aprire Exchange Management Shell, quindi eseguire il seguente comando per recuperare i dettagli dell'impostazione di integrità che ha generato l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli dell'impostazione di integrità OWA.Proxy per server1.contoso.com, eseguire il seguente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
    
    2.  Esaminare l'output del comando per determinare in quale monitor viene riportato l'errore. Il valore **AlertValue** relativo al monitor che ha rilasciato l'avviso corrisponde a `Unhealthy`.
    
    3.  Eseguire nuovamente il probe associato al monitor che si trova in stato di errore. Fare riferimento alla tabella nella sezione Explanation per trovare il probe associato. A tale scopo, eseguire il comando seguente:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si supponga che il sistema di monitoraggio con errori sia **OWAProxyTestMonitor**. Il probe associato a tale sistema di monitoraggio è **OWAProxyTestProbe**. Per eseguire tale probe su server1.contoso.com, eseguire il comando seguente:
        
            Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, esaminare il valore **Result** del probe. Se il valore è **Riuscito**, il problema consisteva in un errore temporaneo e non esiste più. In caso contrario, fare riferimento alla procedura di ripristino descritta nelle sezioni seguenti.

## Azioni di ripristino OWAProxyTestMonitor

Quando si riceve un avviso da un'impostazione di integrità, il messaggio di posta elettronica conterrà le seguenti informazioni:

  - Nome del server Accesso client che ha inviato l'avviso

  - Traccia completa delle eccezioni relativa all'errore più recente, che include i dati di diagnostica e le informazioni dell'intestazione HTTP  
    
    **Nota**   È possibile utilizzare le informazioni nella traccia completa delle eccezioni per risolvere il problema.

  - Ora e data in cui è stato generato il problema

Per risolvere questo problema, procedere come segue:

1.  Verificare i registri di protocollo nei server Accesso client. I registri di protocollo si trovano nella cartella *\<directory di installazione del server exchange\>*\\Logging\\HttpProxy*\\\<protocol\>* nel server Accesso client.

2.  Creare un account utente di prova, quindi accedere al server Accesso client utilizzando tali credenziali. Ad esempio, accedere utilizzando: https://*\<nomeserver\>*/owa.

3.  Avviare Gestione IIS, quindi connettersi al server che ha riportato il problema per determinare se i pool di applicazioni **MSExchangeServicesAppPools** vengono eseguiti nel server Accesso client.

4.  Fare clic su **Pool di applicazioni**, quindi riciclare i pool di applicazioni **MSExchangeOWAAppPool** e **MSExchangeOWACalendarAppPool** eseguendo il seguente comando da Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle APPPOOL MSExchangeOWACalendarAppPool

5.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c nella sezione Verifying the issue still exists.

6.  Se il problema persiste, riciclare il servizio IIS utilizzando l'utilità IISReset.

7.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c nella sezione Verifying the issue still exists.

8.  Se il problema persiste, riavviare il server.

9.  Dopo aver riavviato il server, eseguire nuovamente il probe associato come mostrato nel passaggio 2c nella sezione Verifying the issue still exists.

10. Se l'esecuzione del probe continua ad avere esito negativo, potrebbe essere necessaria assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))

[Managing Outlook Web App](https://technet.microsoft.com/it-it/3814b665-01e8-4881-9a44-163f14789ee4\(exchg.150\)#managing)


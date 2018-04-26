---
title: Risoluzione dei problemi di servizi Web Exchange. Set di integrità proxy
TOCTitle: Risoluzione dei problemi di servizi Web Exchange. Set di integrità proxy
ms:assetid: 5bfbf7e9-d52d-4a3d-91ac-72427c6cb37d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.ews.proxy(v=EXCHG.150)
ms:contentKeyID: 53275548
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di servizi Web Exchange. Set di integrità proxy

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

L'impostazione di integrità EWS.Proxy controlla la disponibilità dell'infrastruttura proxy dei servizi Web di Exchange sul server Accesso client. L'impostazione di integrità EWS.Proxy è strettamente legata alla seguente impostazione di integrità:

[Risoluzione dei problemi di Set di integrità ClientAccess.Proxy](troubleshooting-clientaccess-proxy-health-set.md)

Se viene visualizzato un avviso che indica la non integrità di EWS.Proxy, ciò significa che un problema può impedire agli utenti di accedere al servizio EWS.

## Descrizione

Il servizio EWS viene monitorato tramite i seguenti probe e monitor.


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
<td><p>EWSProxyTestProbe</p></td>
<td><p>EWS.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>EWSProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e sistemi di monitoraggio, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Problemi comuni

Il non funzionamento del probe potrebbe essere dovuto a una delle seguenti cause:

  - Il pool di applicazioni ospitato sul server Accesso client monitorato non funziona correttamente.

  - Le credenziali dell'account di monitoraggio non sono corrette.

  - I controller di dominio non rispondono.

## Azione utente

È possibile che il servizio venga ripristinato dopo aver inoltrato l'avviso. Pertanto, quando si visualizza un avviso che specifica che l'impostazione di integrità è venuta a mancare, verificare innanzitutto che il problema esiste effettivamente. Se il problema esiste, effettuare le azioni di ripristino appropriate descritte nelle sezioni che seguono.

## Verifica della persistenza del problema

1.  Identificare il nome dell'impostazione di integrità e del server nell'avviso.

2.  I dettagli del messaggio forniscono informazioni sull'esatta causa dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio offrono informazioni sufficienti sulla risoluzione dei problemi per identificare la causa principale. Se i dettagli del messaggio non sono chiari, effettuare le seguenti operazioni:
    
    1.  Aprire Exchange Management Shell, quindi eseguire il seguente comando per recuperare i dettagli dell'impostazione di integrità che ha generato l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli dell'impostazione di integrità EWS.Proxy sul server1.contoso.com, eseguire il comando indicato di seguito:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS.Proxy"}
    
    2.  Controllare l'output del comando per determinare quale monitor abbia segnalato l'errore. Il valore **AlertValue** del sistema di monitoraggio che ha emesso l'avviso sarà `Unhealthy`.
    
    3.  Eseguire nuovamente il probe associato per il sistema di monitoraggio che si trova in uno stato non integro. Fare riferimento alla tabella nella sezione Verifying the issue still exists per trovare il probe associato. A tale scopo, eseguire il comando indicato di seguito:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si supponga che il sistema di monitoraggio con errori sia **EWSProxyTestMonitor**. Il probe associato a tale sistema di monitoraggio è **EWSProxyTestProbe**. Per eseguire il probe sul server1.contoso.com, utilizzare il comando indicato di seguito:
        
            Invoke-MonitoringProbe EWS.Proxy\EWSProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, controllare il valore del probe **Risultato**. Se il valore è **Completato**, il problema risulta superato poiché si trattava di un errore temporaneo. In caso contrario, fare riferimento alle procedure di ripristino descritte nelle sezioni seguenti.

## Azioni di ripristino EWSProxyTestMonitor

Quando si riceve un avviso da un'impostazione di integrità, il messaggio di posta elettronica contiene le seguenti informazioni:

  - Nome del server Accesso client che ha inviato l'avviso

  - La traccia completa dell'eccezione dell'ultimo errore, compresi i dati diagnostici e le informazioni specifiche sull'intestazione HTTP
    
    È possibile utilizzare le informazioni nella traccia completa dell'eccezione per risolvere il problema.

  - Ora e data in cui è stato generato il problema

Per risolvere questo problema, procedere come segue:

1.  Verificare i registri di protocollo nei server Accesso client. I registri di protocollo si trovano nella cartella *\<directory di installazione Exchange Server\>*\\Logging\\HttpProxy*\\\<protocol\>* nel server Accesso client.

2.  Creare un account utente di prova, quindi accedere al server Accesso client utilizzando tali credenziali. Ad esempio, utilizzare il seguente indirizzo di accesso: https://*\<nomeserver\>*/owa

3.  Avviare Gestione IIS, quindi connettersi al server che ha riportato il problema per determinare se il pool di applicazioni **MSExchangeServicesAppPool** è in esecuzione sul server Accesso client.

4.  Fare clic su **Pool di applicazioni**, quindi riciclare il pool di applicazioni **MSExchangeServicesAppPool** eseguendo il seguente comando da Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

5.  Eseguire nuovamente il probe associato come indicato nel passaggio 2c nella sezione Verifying the issue still exists.

6.  Se il problema persiste, riciclare il servizio IIS tramite l'utilità IISReset.

7.  Eseguire nuovamente il probe associato come indicato nel passaggio 2c nella sezione Verifying the issue still exists.

8.  Se il problema persiste, riavviare il server.

9.  Dopo aver riavviato il server, eseguire nuovamente il probe associato come indicato nel passaggio 2c nella sezione Verifying the issue still exists.

10. Se il probe continua a non funzionare, potrebbe essere necessario chiedere assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))


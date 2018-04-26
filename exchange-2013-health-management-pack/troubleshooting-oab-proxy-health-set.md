---
title: Risoluzione dei problemi della Rubrica fuori rete. Set di integrità proxy
TOCTitle: Risoluzione dei problemi della Rubrica fuori rete. Set di integrità proxy
ms:assetid: b717fc00-a787-44d6-8ccb-0eb4b2ea9e73
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.oab.proxy(v=EXCHG.150)
ms:contentKeyID: 53275541
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi della Rubrica fuori rete. Set di integrità proxy

 

_**Si applica a:**Exchange Server 2013, Project Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Il set di integrità OAB.Proxy monitora la disponibilità dell'infrastruttura proxy della rubrica offline sul server Accesso client.

Un eventuale avviso che specifica che il set di integrità OAB.Proxy non è integro indica un problema che potrebbe impedire agli utenti l'uso della rubrica offline.

## Descrizione

Il servizio Rubrica offline viene monitorato utilizzando i seguenti probe e controlli:


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
<td><p>OABProxyTestProbe</p></td>
<td><p>OAB.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OABProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Problemi comuni

Le cause di errore comuni di questo probe sono:

  - Il pool di applicazioni ospitato sul server Accesso client monitorato non funziona correttamente.

  - Le credenziali dell'account di monitoraggio non cono corrette.

  - I controller di dominio non rispondono.

## Azione utente

È possibile che il servizio venga ripristinato dopo l'emissione dell'avviso. Di conseguenza, se si riceve un avviso indicante che il set di integrità non è in integro, verificare prima che il problema sia ancora presente. Se il problema ancora esiste, eseguire le azioni di ripristino appropriate delineate nelle sezioni seguenti.

## Verifica dell'esistenza del problema

1.  Identificare il nome del set di integrità e il nome del server nell'avviso.

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio contengono informazioni di risoluzione dei problemi sufficienti ad identificare la causa principale. Se i dettagli del messaggio non sono chiari, procedere come segue:
    
    1.  Aprire Exchange Management Shell, quindi utilizzare il seguente comando per recuperare i dettagli del set di integrità che ha emesso l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli del set di integrità OAB.Proxy su server1.contoso.com, utilizzare il seguente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OAB.Proxy"}
    
    2.  Esaminare l'output del comando per determinare quale controllo ha segnalato l'errore. Il valore **AlertValue** del controllo che ha emesso l'avviso sarà `Unhealthy`.
    
    3.  Eseguire di nuovo il probe associato per il controllo in stato non integro. Per trovare il probe associato, fare riferimento alla tabella nella sezione Explanation. A tale scopo, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si presuma che il controllo con l'errore sia **OABProxyTestMonitor**. Il probe associato a tale controllo è **OABProxyTestProbe**. Per eseguire tale probe su server1.contoso.com, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe |OAB.Proxy\OABProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, verificare il valore **Result** del probe. Se il valore è **Succeeded**, l'errore era transitorio e non esiste più. Altrimenti, fare riferimento alla procedura di ripristino delineata nella sezioni seguenti.

## Azioni di ripristino di OABProxyTestMonitor

Quando si riceve un avviso da un set di integrità, il messaggio di posta elettronica contiene le informazioni seguenti:

  - Nome del server Accesso client che ha inviato l'avviso

  - Traccia di eccezione completa dell'ultimo errore, inclusi i dati diagnostici e le informazioni specifiche dell'intestazione HTTP  
    
    **Nota**   È possibile utilizzare le informazioni contenute nella traccia di eccezione completa per risolvere il problema.

  - Ora e data in cui si è verificato il problema

Per risolvere il problema, procedere come segue:

1.  Esaminare i registri di protocollo sul server Accesso client. I registri di protocollo si trovano nella cartella *\<directory di installazione del server exchange\>*\\Logging\\HttpProxy*\\\<protocollo\>* sul server Accesso client.

2.  Creare un account utente di prova, quindi accedere al server Accesso client con tale account. Ad esempio, accedere con: https://*\<nomeserver\>*/owa.

3.  Avviare Gestione IIS, quindi connettersi al server che segnala l'errore per determinare se il pool di applicazioni **MSExchangeOABAppPool** è in esecuzione sul server Accesso client.

4.  Fare clic su **Pool di applicazioni** e riavviare il pool di applicazioni **MSExchangeOABAppPool** eseguendo il comando di seguito riportato da Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOABAppPool

5.  Eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

6.  Se il problema ancora esiste, riavviare il servizio IIS tramite l'utilità IISReset.

7.  Eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

8.  Se il problema ancora esiste, riavviare il server.

9.  Dopo il riavvio del server, eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

10. Se il probe continua a incontrare un errore, chiedere assistenza. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Rubriche offline](https://technet.microsoft.com/it-it/library/bb232155\(v=exchg.150\))

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))


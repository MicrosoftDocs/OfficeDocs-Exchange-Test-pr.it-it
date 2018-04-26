---
title: Set di integrità FIPS la risoluzione dei problemi
TOCTitle: Set di integrità FIPS la risoluzione dei problemi
ms:assetid: 96e1b096-9cb5-426f-a84e-50d5599e4bbb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.fips(v=EXCHG.150)
ms:contentKeyID: 54652921
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Set di integrità FIPS la risoluzione dei problemi

 

_**Si applica a:**Exchange Server 2013, Project Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Set di integrità **FIPS** esegue il monitoraggio dell'integrità globale delle impostazioni di elaborazione standard FIPS (Federal Information) nei server Exchange. Per ulteriori informazioni su FIPS 140, vedere [FIPS 140 convalida](https://go.microsoft.com/fwlink/p/?linkid=521913).

Se si riceve un avviso che indica che il set di integrità **FIPS** è integro, ciò indica un problema che potrebbe impedire l'utilizzo di processi e FIPS 140-componenti compatibili con il server Exchange.

## Descrizione

Il servizio **FIPS** viene monitorato utilizzando i seguenti probe e monitor.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Probe</th>
<th>Set di integrità</th>
<th>Controlli associati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>FIPS</p></td>
<td><p>CrashEvent.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceFailureMonitor.FIPS</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceTimeoutMonitor.FIPS</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetError.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeError.scanningprocess</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Azione utente

È possibile che il servizio di ripristino dopo che lo ha emesso l'avviso. Pertanto, quando si riceve un avviso che indica che il set di integrità **FIPS** non è integro, innanzitutto verificare che il problema persiste. Se il problema esiste, eseguire le azioni di ripristino appropriata descritte nella sezione seguente.

## Verifica del problema

1.  Identificare il nome dell'impostazione di integrità e il nome del server riportati nell'allarme.

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'allarme. Nella maggior parte dei casi, i dettagli del messaggio forniscono informazioni per la risoluzione dei problemi sufficienti a consentire di identificare la causa principale. Se i dettagli del messaggio non sono chiari, procedere come segue:
    
    1.  Aprire Exchange Management Shell ed eseguire il seguente comando per recuperare i dettagli dell'impostazione di integrità che ha emesso l'allarme:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare **FIPS** integrità impostare informazioni dettagliate su Server1. contoso.com, eseguire il comando seguente:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "FIPS"}
    
    2.  Esaminare l'output comando per stabilire quale monitor ha segnalato l'errore. Il valore **AlertValue** per il monitor che ha emesso l'allarme sarà **Danneggiato**.


---
title: Risoluzione dei problemi di integrità MailboxTransport impostare
TOCTitle: Risoluzione dei problemi di integrità MailboxTransport impostare
ms:assetid: 02bfa4cf-6929-437e-bae5-079ea1b92373
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.mailboxtransport(v=EXCHG.150)
ms:contentKeyID: 54652896
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di integrità MailboxTransport impostare

 

_**Si applica a:** Exchange Server 2013, Project Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Set di integrità **MailboxTransport** consente di monitorare l'integrità generale dei servizi di invio del trasporto delle cassette postali e il recapito di trasporto delle cassette postali sui server cassette postali. Questi servizi sono responsabili dell'invio di posta da e verso i database delle cassette postali. Per ulteriori informazioni, vedere [Flusso di posta](https://technet.microsoft.com/it-it/library/aa996349\(v=exchg.150\)).

Se si riceve un avviso che indica che il set di integrità **MailboxTransport** è integro, ciò indica un problema che potrebbe impedire la posta proveniente da inviati o ricevuti dal database delle cassette postali.

## Descrizione

Il servizio **MailboxTransport** viene monitorato utilizzando i seguenti probe e monitor.


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
<td><p>MailboxDeliveryAvailability</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>MailboxDeliveryAvailabilityAggregationProbe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryAvailabilityAggregationMonitor</p></td>
</tr>
<tr class="odd">
<td><p>MailboxDeliveryInstanceAvailabilityProbe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryInstanceAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>MailboxTransportDeliveryServiceRunning</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportDeliveryServiceRunningMonitor</p></td>
</tr>
<tr class="odd">
<td><p>MailboxTransportSubmissionServiceRunning</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportSubmissionServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>Mapi.Submit.Probe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>Mapi.Submit.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>CrashEvent.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>CrashEvent.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>DeliveryBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>DeliveryInterceptorStoreDriverAgentPctPermFailedMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportUserQuarantineMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MBTSubmissionInterceptorSubmissionAgentMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MSExchangeAsstAvgEventProcessingTimeSubmissionMonitor50</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MSExchangeAsstAvgEventProcessingTimeSubmissionMonitor70</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>SubmissionBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>SubmissionInterceptorSubmissionAgentPctPermFailedMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno (notifica o controllo)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>TransportDeliveryFailuresDeliveryStoreDriver560Monitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Azione utente

È possibile che il servizio di ripristino dopo che lo ha emesso l'avviso. Pertanto, quando si riceve un avviso che indica che il set di integrità **MailboxTransport** è integro, innanzitutto verificare che il problema persiste. Se il problema esiste, eseguire le azioni di ripristino appropriata descritte nella sezione seguente.

## Verifica del problema

1.  Identificare il nome dell'impostazione di integrità e il nome del server riportati nell'allarme.

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'allarme. Nella maggior parte dei casi, i dettagli del messaggio forniscono informazioni per la risoluzione dei problemi sufficienti a consentire di identificare la causa principale. Se i dettagli del messaggio non sono chiari, procedere come segue:
    
    1.  Aprire Exchange Management Shell ed eseguire il seguente comando per recuperare i dettagli dell'impostazione di integrità che ha emesso l'allarme:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare **MailboxTransport** integrità impostare informazioni dettagliate su mailbox1.contoso.com, eseguire il comando seguente:
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealthSetName -eq "MailboxTransport"}
    
    2.  Esaminare l'output comando per stabilire quale monitor ha segnalato l'errore. Il valore **AlertValue** per il monitor che ha emesso l'allarme sarà **Danneggiato**.
    
    3.  Eseguire nuovamente il probe associato per il monitor nello stato danneggiato. Fare riferimento alla tabella nella sezione [Explanation](troubleshooting-activesync-health-set.md) per trovare il probe associato. A tale scopo, eseguire il comando seguente:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si presuppone che il monitor problemi sia **MailboxDeliveryAvailabilityMonitor**. Il probe associato al monitor è **MailboxDeliveryAvailability**. Per eseguire questo probe su mailbox1.contoso.com, eseguire il comando seguente:
        
            Invoke-MonitoringProbe MailboxTransport\MailboxDeliveryAvailabilityMonitor -Server mailbox1.contoso.com | Format-List
    
    4.  Nell'output del comando, vedere la sezione "Risultati" del probe. Se il valore è **Succeeded**, il problema è stato un errore temporaneo e non esiste più.


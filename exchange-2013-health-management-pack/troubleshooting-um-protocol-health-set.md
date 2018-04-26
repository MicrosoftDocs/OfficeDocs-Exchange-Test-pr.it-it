---
title: Risoluzione dei problemi di messaggistica unificata. Set di integrità di protocollo
TOCTitle: Risoluzione dei problemi di messaggistica unificata. Set di integrità di protocollo
ms:assetid: 8dd9a16f-77a1-4a8d-aea4-5e96ab922dd4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.um.protocol(v=EXCHG.150)
ms:contentKeyID: 53275537
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di messaggistica unificata. Set di integrità di protocollo

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

L'impostazione di integrità UM.Protocol controlla il protocollo di messaggistica unificata sul server Cassette postali.

Se si riceve un allarme che specifica che UM.Protocol non risulta integro, potrebbe verificarsi un problema che potrebbe impedire agli utenti di accedere al servizio di messaggistica unificata nell'organizzazione. L'impostazione di integrità UM.Protocol è strettamente correlata alle seguenti impostazioni di integrità:

[Risoluzione dei problemi di messaggistica unificata Set di integrità](troubleshooting-um-health-set.md)

[Risoluzione dei problemi di messaggistica unificata. Set di integrità CallRouter](troubleshooting-um-callrouter-health-set.md)

## Descrizione

Il servizio UM.Protocol viene controllato tramite i seguenti probe e monitor.


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
<td><p>UMSelfTestProbe</p></td>
<td><p>UM.Protocol</p></td>
<td><p>Active Directory Servizi di dominio (AD DS)</p></td>
<td><p>UMSelfTestMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Azione utente

È possibile che il servizio sia stato ripristinato dopo l'emissione dell'allarme. Pertanto, quando si riceve un allarme che specifica che l'impostazione di integrità è danneggiata, è necessario verificare innanzitutto se il problema sussiste ancora. Se il problema persiste, eseguire le azioni di ripristino appropriate riportate nelle sezioni seguenti.

## Verifica della persistenza del problema

1.  Identificare il nome dell'impostazione di integrità e il nome del server riportati nell'allarme.

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'allarme. Nella maggior parte dei casi, i dettagli del messaggio forniscono informazioni per la risoluzione dei problemi sufficienti a identificare la causa principale. Se i dettagli del messaggio non sono chiari, procedere come segue:
    
    1.  Aprire Exchange Management Shell ed eseguire il seguente comando per recuperare i dettagli dell'impostazione di integrità che ha emesso l'allarme:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli dell'impostazione di integrità UM.Protocol relativi a server1.contoso.com, eseguire il comando riportato:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  Esaminare l'output comando per stabilire quale monitor ha segnalato l'errore. Il valore **AlertValue** per il monitor che ha emesso l'allarme sarà `Unhealthy`.
    
    3.  Eseguire nuovamente il probe associato per il monitor nello stato danneggiato. Fare riferimento alla tabella nella sezione Explanation per trovare il probe associato. A tale scopo, eseguire il comando seguente:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si supponga che il monitor che riporta l'errore sia **UMSelfTestMonitor**. Il probe associato al monitor è **UMSelfTestProbe**. Per eseguire il probe su server1.contoso.com, eseguire il comando riportato:
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  Nell'output comando, esaminare il valore **Risultato** del probe. Se il valore è **Riuscito**, si è trattato di un errore temporaneo che non sussiste più. In caso contrario, fare riferimento alla procedura di ripristino riportata nelle sezioni seguenti.

## Procedura di risoluzione dei problemi

Quando si riceve un allarme da questa impostazione di integrità, il messaggio di posta elettronica contiene le seguenti informazioni:

  - Nome del server che ha inviato l'allarme

  - Ora e data in cui si è verificato l'allarme

  - Meccanismo di autenticazione utilizzato e informazioni sulle credenziali

  - Analisi completa delle eccezioni dell'ultimo errore, inclusi i dati di diagnostica e le informazioni delle intestazioni HTTP specifiche
    
    **Nota**   È possibile utilizzare queste informazioni nell'analisi completa delle eccezioni per facilitare la risoluzione del problema. L'eccezione generata dal probe contiene la descrizione del motivo di errore del probe.

Per ulteriori informazioni sulla risoluzione dei problemi di messaggi di allarme UJM, vedere [Risoluzione dei problemi di messaggistica unificata Set di integrità](troubleshooting-um-health-set.md)

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))


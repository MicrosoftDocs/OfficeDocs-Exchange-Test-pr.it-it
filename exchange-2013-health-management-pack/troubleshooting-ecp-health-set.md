---
title: Risoluzione dei problemi Set di integrità ECP
TOCTitle: Risoluzione dei problemi Set di integrità ECP
ms:assetid: 0a1cfcd5-585c-4a0a-9d3c-28dc49e16a6c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.ecp(v=EXCHG.150)
ms:contentKeyID: 53275530
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi Set di integrità ECP

 

_**Si applica a:**Exchange Server 2013, Project Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

L'impostazione di integrità del Pannello di controllo di Exchange (ECP, Exchange Control Panel) consente di monitorare l'integrità globale dell'interfaccia di amministrazione di Exchange (EAC) e le impostazioni utente del servizio Outlook Web App (OWA). L'impostazione di integrità ECP è strettamente correlata all'impostazione di integrità riportata di seguito:

[Risoluzione dei problemi di ECP. Set di integrità proxy](troubleshooting-ecp-proxy-health-set.md)

Se si riceve un avviso che indica che il set di integrità ECP è integro, che ciò indica un problema che potrebbe impedire agli utenti di accesso a EAC.

## Descrizione

Il servizio EAC viene monitorato utilizzando i probe e i monitor riportati di seguito.


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
<td><p>EacSelfTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EacDeepTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni relative a probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Azione utente

Quando si riceve un avviso da un'impostazione di integrità, il messaggio di posta elettronica conterrà le seguenti informazioni:

  - Nome del server da cui è stato inviato l'avviso

  - Ora e data in cui è stato generato l'avviso

  - Informazioni sull'autenticazione e sulle credenziali

  - Traccia di eccezione completa dell'ultimo errore, inclusi i dati diagnostici e le informazioni specifiche dell'intestazione HTTP
    
    **Nota**   È possibile utilizzare le informazioni relative alla traccia completa delle eccezioni per risolvere il problema.

È possibile che il servizio venga ripristinato dopo la pubblicazione dell'avviso. Di conseguenza, quando si riceve un avviso che specifica che l'integrità è danneggiata, verificare se il problema persiste. Se il problema persiste, eseguire le azioni di ripristino illustrate nelle seguenti sezioni.

## Verifica della persistenza del problema

1.  Identificare il nome dell'impostazione di integrità e del server nell'avviso.

2.  I dettagli relativi al messaggio forniscono informazioni relative alla causa esatta dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio offrono informazioni sufficienti sulla risoluzione dei problemi per identificare la causa principale. Se i dettagli del messaggio non sono chiari, attenersi alla seguente procedura:
    
    1.  Aprire Exchange Management Shell, quindi eseguire il seguente comando in modo da recuperare i dettagli relativi all'impostazione di integrità che ha rilasciato l'avviso:
        
            Get-ServerHealth -Identity <ServerName> -HealthSet <HealthSetName>
        
        Ad esempio, per recuperare il ECP integrità impostare i dettagli relativi Server1. contoso.com, eseguire il comando seguente:
        
            Get-ServerHealth -Identity server1.contoso.com -HealthSetName ECP
    
    2.  Esaminare l'output del comando per determinare in quale monitor viene riportato l'errore. Il valore **AlertValue** relativo al monitor che ha rilasciato l'avviso corrisponde a `Unhealthy`.
    
    3.  Eseguire nuovamente il probe associato al monitor che si trova in stato di errore. Fare riferimento alla tabella riportata nella sezione Explanation per individuare il probe associato. A tale scopo, eseguire il comando seguente:
        
            Invoke-MonitoringProbe <HealthSetName>\<ProbeName> -Server <ServerName> | Format-List
        
        Ad esempio, si ipotizzi che il monitor in stato di errore sia **EacSelfTestMonitor**. Il probe associato a tale monitor sarà **EacSelfTestProbe**. Per eseguire il probe su server1.contoso.com, eseguire il comando riportato di seguito:
        
            Invoke-MonitoringProbe ECP\EacSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, esaminare il valore **Risultato** relativo al probe. Se il valore corrisponde a **Riuscito**, il problema consisteva in un errore temporaneo e non esiste più. In caso contrario, fare riferimento alla procedura di ripristino descritta nelle sezioni seguenti.

## Operazioni di ripristino di EacSelfTestMonitor e EacDeepTestMonitor

1.  Avviare Gestione IIS e connettersi al server che riporta il problema. Fare clic su **Pool di applicazioni** e quindi riavviare il pool di applicazioni ECP denominato **MSExchangeECPAppPool**.

2.  Eseguire nuovamente il probe associato, come descritto nel passaggio 2c della sezione Verifying the issue still exists.

3.  Se il problema persiste, riciclare il servizio IIS utilizzando l'utilità IISReset.

4.  Eseguire nuovamente il probe associato, come descritto nel passaggio 2c della sezione Verifying the issue still exists.

5.  Se l'esecuzione del probe non riesce, riavviare il server.

6.  Dopo aver riavviato il server, eseguire nuovamente il probe associato, come descritto nel passaggio 2c della sezione Verifying the issue still exists.

7.  Se l'esecuzione del probe continua ad avere esito negativo, potrebbe essere necessaria assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))

[Interfaccia di amministrazione di Exchange in Exchange 2013](https://technet.microsoft.com/it-it/library/jj150562\(v=exchg.150\))


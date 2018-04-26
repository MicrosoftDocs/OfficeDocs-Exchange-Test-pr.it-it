---
title: Risoluzione dei problemi Set di integrità Autodiscover.Protocol
TOCTitle: Risoluzione dei problemi Set di integrità Autodiscover.Protocol
ms:assetid: 06afdcc8-7920-4e88-b85a-98e67a19d221
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.autodiscover.protocol(v=EXCHG.150)
ms:contentKeyID: 53275529
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi Set di integrità Autodiscover.Protocol

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

L'impostazione di integrità Autodiscover.Protocol monitora il protocollo di comunicazione Autodiscover sul server Cassette postali.

Se viene visualizzato un avviso in cui è indicato lo stato di non integrità dell'impostazione Autodiscover.Protocol, significa che è presente un problema che potrebbe impedire agli utenti di accedere alle proprie cassette postali.

## Descrizione

Il servizio Autodiscover.Protocol viene monitorato utilizzando i probe e monitor riportati di seguito.


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
<td><p>AutodiscoverSelfTestProbe</p></td>
<td><p>Autodiscover.Protocol</p></td>
<td><p>Active Directory</p></td>
<td><p>AutodiscoverSelfTestMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni relative a probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Problemi comuni

Il non funzionamento del probe potrebbe essere dovuto a una delle seguenti cause:

  - Il pool di applicazioni Autodiscover (MSExchangeAutodiscoverAppPool) ospitato sul server Accesso client (CAS, Client Access Server) monitorato non risponde. Oppure, il pool di applicazioni Autodiscover ospitato su uno o più server Cassette postali non risponde.

  - I controller di dominio non rispondono.

## Azione utente

È possibile che il servizio venga ripristinato dopo la pubblicazione dell'avviso. Di conseguenza, quando si riceve un avviso che specifica che l'integrità è danneggiata, verificare se il problema persiste. Se il problema persiste, eseguire le azioni di ripristino illustrate nelle seguenti sezioni.

## Verifica della persistenza del problema

1.  Identificare il nome dell'impostazione di integrità e del server nell'avviso.

2.  I dettagli relativi al messaggio forniscono informazioni sull'esatta causa dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio offrono informazioni sufficienti sulla risoluzione dei problemi per identificare la causa principale. Se i dettagli del messaggio non sono chiari, effettuare la seguente operazione:
    
    1.  Aprire Exchange Management Shell, quindi eseguire il seguente comando in modo da recuperare i dettagli relativi all'impostazione di integrità che ha rilasciato l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli dell'impostazione di integrità Autodiscover.Protocol relativi a server1.contoso.com, eseguire il seguente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover.Protocol"}
    
    2.  Verificare l'output del comando per determinare in quale monitor viene riportato l'errore. Il valore **AlertValue** relativo al monitor che ha rilasciato l'avviso corrisponde a `Unhealthy`.
    
    3.  Eseguire nuovamente il probe associato al monitor che si trova in stato di errore. Fare riferimento alla tabella riportata nella sezione Explanation per individuare il probe associato. A tale scopo, eseguire il comando seguente:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si ipotizzi che il monitor danneggiato è **AutodiscoverSelfTestMonitor**. Il probe associato a tale sistema di monitoraggio sarà **AutodiscoverSelfTestProbe**. Per eseguire il probe su server1.contoso.com, eseguire il comando seguente:
        
            Invoke-MonitoringProbe Autodiscover.Protocol\AutodiscoverSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, esaminare il valore **Risultato** del probe. Se il valore corrisponde a **Riuscito**, il problema consisteva in un errore temporaneo e non esiste più. In caso contrario, fare riferimento alle azioni di ripristino descritte nelle sezioni riportate di seguito.

## Operazioni di ripristino per AutodiscoverSelfTestProbe

Quando si riceve un avviso da un'impostazione di integrità, il messaggio di posta elettronica conterrà le seguenti informazioni:

  - Nome del server Cassette postali da cui è stato inviato l'avviso

  - Nome del server Cassette postali in fase di monitoraggio

  - Ora e data in cui è stato generato l'avviso

  - Meccanismo di autenticazione utilizzato e informazioni sulle credenziali

  - Traccia completa dell'eccezione dell'ultimo errore, compresi i dati diagnostici e informazioni specifiche sull'intestazione HTTP

È possibile utilizzare le informazioni della traccia completa delle eccezioni per risolvere il problema. L'eccezione generata dal probe include una causa dell'errore che descrive il motivo per cui si è verificato l'errore del probe.

Per risolvere questo problema, procedere come segue:

1.  Verificare i registri di protocollo nei server Cassette postali. Per impostazione predefinita, i file di registro del protocollo si trovano nella cartella della ***\<directory di installazione di exchange server\>*\\Logging\\Autodiscover**.

2.  Creare un account utente di prova, quindi accedere al server Cassette postali utilizzando l'account utente di prova nell'indirizzo. Ad esempio, accedere tramite: https://*\<servername\>*:444/autodiscover/autodiscover.xml.
    
    Se il nome dell'account utente di prova viene ammesso, è possibile che il problema interessi il server Cassette postali che ospita la cassetta postale in fase di monitoraggio.

3.  Provare a ripetere i passaggi precedenti utilizzando un account di prova sul server Cassette postali.

4.  Verificare eventuali avvisi sull'impostazione di integrità Autodiscover.Proxy, i quali possono indicare la presenza di un problema che interessa un server Cassette postali specifico. Per ulteriori informazioni, vedere [Risoluzione dei problemi Set di integrità Autodiscover.Proxy](troubleshooting-autodiscover-proxy-health-set.md).

5.  Verificare eventuali avvisi sull'impostazione di integrità Autodiscover, i quali possono indicare la presenza di un problema che interessa server Cassette postali specifici. Per ulteriori informazioni, vedere [Impostare la risoluzione dei problemi di integrità di individuazione automatica](troubleshooting-autodiscover-health-set.md).

6.  Avviare Gestione IIS, quindi effettuare la connessione al server Cassette postali in cui è presente il problema. Verificare che il pool di applicazione **MSExchangeAutodiscoverAppPool** sia in esecuzione sul server Cassette postali.

7.  In Gestione IIS, fare clic su **Pool di applicazioni**, quindi eseguire il riciclo del pool di applicazione **MSExchangeAutodiscoverAppPool**, eseguendo in Shell il comando riportato di seguito:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeAutodiscoverAppPool

8.  Eseguire nuovamente il probe associato, come descritto nel passaggio 2c della sezione Verifying the issue still exists.

9.  Se il problema persiste, eseguire il riciclo del servizio IIS utilizzando l'utilità IISReset o eseguendo il comando riportato di seguito:
    
        Iisreset /noforce

10. Eseguire nuovamente il probe associato, come descritto nel passaggio 2c della sezione Verifying the issue still exists.

11. Se il problema persiste, riavviare il server.

12. Dopo aver riavviato il server, eseguire nuovamente il probe associato, come descritto nel passaggio 2c della sezione Verifying the issue still exists.

13. Se l'esecuzione del probe continua ad avere esito negativo, potrebbe essere necessaria assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))


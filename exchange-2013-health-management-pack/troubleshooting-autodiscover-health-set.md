---
title: Impostare la risoluzione dei problemi di integrità di individuazione automatica
TOCTitle: Impostare la risoluzione dei problemi di integrità di individuazione automatica
ms:assetid: bc933621-df73-4d1d-bdef-825b98be8e09
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.autodiscover(v=EXCHG.150)
ms:contentKeyID: 53275554
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare la risoluzione dei problemi di integrità di individuazione automatica

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Il set di integrità Autodiscover monitora l'integrità generale del servizio Individuazione automatica per i client.

Un eventuale avviso che specifica che Autodiscover non è integro indica un problema che potrebbe impedire agli utenti l'accesso alla propria cassetta postale tramite il processo Individuazione automatica.

## Descrizione

Il servizio Individuazione automatica viene monitorato utilizzando i seguenti probe e controlli:


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
<td><p>AutodiscoverCtpProbe</p></td>
<td><p>Individuazione automatica</p></td>
<td><p>Active Directory</p></td>
<td><p>AutodiscoverCtpMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Problemi comuni

Le cause di errore comuni di questo probe sono:

  - Il pool di applicazioni di Individuazione automatica (MSExchangeAutodiscoverAppPool) ospitato sul server Accesso client non risponde. Oppure, il pool di applicazioni di Individuazione automatica ospitato su uno o più server Cassette postali non risponde.

  - Il server Accesso client ha incontrato problemi di rete e non è in grado di connettersi al server Cassette postali o al controller di dominio.

  - Le credenziali dell'account di monitoraggio non cono corrette.

  - I controller di dominio non rispondono.

## Azione utente

È possibile che il servizio venga ripristinato dopo l'emissione dell'avviso. Di conseguenza, se si riceve un avviso indicante che il set di integrità non è in integro, verificare prima che il problema sia ancora presente. Se il problema ancora esiste, eseguire le azioni di ripristino appropriate delineate nelle sezioni seguenti.

## Verifica dell'esistenza del problema

1.  Identificare il nome del set di integrità e il nome del server nell'avviso.

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio contengono informazioni di risoluzione dei problemi sufficienti ad identificare la causa principale. Se i dettagli del messaggio non sono chiari, procedere come segue:
    
    1.  Aprire Exchange Management Shell, quindi utilizzare il seguente comando per recuperare i dettagli del set di integrità che ha emesso l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli del set di integrità Autodiscover su server1.contoso.com, utilizzare il seguente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover"}
    
    2.  Esaminare l'output del comando per determinare quale controllo ha segnalato l'errore. Il valore **AlertValue** del controllo che ha emesso l'avviso è `Unhealthy`.
    
    3.  Eseguire di nuovo il probe associato per il controllo in stato non integro. Per trovare il probe associato, fare riferimento alla tabella nella sezione Explanation. A tale scopo, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si presuma che il controllo con l'errore sia **AutodiscoverCtpMonitor**. Il probe associato a tale controllo è **AutodiscoverCtpProbe**. Per eseguire tale probe su server1.contoso.com, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe Autodiscover\AutodiscoverCtpProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, verificare il valore **Result** del probe. Se il valore è **Succeeded**, l'errore era transitorio e non esiste più. Altrimenti, fare riferimento alla procedura di ripristino delineata nella sezioni seguenti.

## Azioni di ripristino per AutodiscoverCtpMonitor

Quando si riceve un avviso da un set di integrità, il messaggio di posta elettronica contiene le informazioni seguenti:

  - Nome del server che ha inviato l'avviso

  - Nome del server Cassette postali monitorato dal probe

  - Ora e data in cui si è verificato l'avviso

  - Meccanismo di autenticazione utilizzato e informazioni sulle credenziali

  - Traccia di eccezione completa dell'ultimo errore, inclusi i dati diagnostici e le informazioni specifiche dell'intestazione HTTP

È possibile utilizzare le informazioni contenute nella traccia di eccezione completa per risolvere il problema. L'eccezione generata dal probe contiene una Causa errore che descrive perché il probe non è riuscito. Ad esempio, la Causa errore potrebbe essere:

  - **X-FEServer**   Indica il server Accesso client su cui è stato eseguito il probe

  - **X-CalculatedBETarget**   Indica il server Cassette postali a cui è stata instradata la richiesta

  - **X-DiagInfo**   Indica il server Cassette postali che ha ricevuto la richiesta

Per risolvere il problema, procedere come segue:

1.  Esaminare i registri di protocollo sui server Accesso client e Cassette postali. Per impostazione predefinita, i registri di protocollo sul server Accesso client si trovano nella cartella ***\<directory di installazione del server exchange\>*\\Logging\\HttpProxy\\Autodiscover**. Per impostazione predefinita, i file di registro di protocollo sul server Cassette postali si trovano nella cartella ***\<directory di installazione del server exchange\>*\\Logging\\Autodiscover**.

2.  Creare un account utente di prova, quindi accedere al server Accesso client con tale account. Ad esempio, accedere con: https://*\<nome server\>*/autodiscover/autodiscover.xml.
    
    Se il nome dell'account utente di prova passa, un problema potrebbe influire sul server Cassette postali che ospita la cassetta potale monitorata.
    
    Provare a ripetere la procedura precedente utilizzando un account di prova sul server Cassette postali. Se questo tentativo non riesce, ritentare la prova con un server Accesso client diverso per verificare se il problema si sta verificando su uno specifico server Accesso client e non sul server Cassette postali.

3.  Verificare la connettività di rete tra server Accesso client e Cassette postali. Utilizzare ping.exe per verificare che ogni server risponda.

4.  Esaminare il set di integrità Autodiscover.Proxy per verificare l'eventuale presenza di avvisi indicanti un problema che influisce su uno specifico server Cassette postali. Per ulteriori informazioni, vedere [Risoluzione dei problemi Set di integrità Autodiscover.Proxy](troubleshooting-autodiscover-proxy-health-set.md).

5.  Esaminare il set di integrità Autodiscover.Protocol per verificare l'eventuale presenza di avvisi indicanti un problema che influisce su specifici server Cassette postali. Per ulteriori informazioni, vedere [Risoluzione dei problemi Set di integrità Autodiscover.Protocol](troubleshooting-autodiscover-protocol-health-set.md).

6.  Avviare Gestione IIS, quindi connettersi al server che segnala il problema. Verificare che il pool di applicazioni **MSExchangeAutodiscoverAppPool** sia in esecuzione sui server Accesso clienti e Cassette postali.

7.  In Gestione IIS, fare clic su **Pool di applicazioni** e riavviare il pool di applicazioni **MSExchangeAutodiscoverAppPool** eseguendo il comando di seguito riportato da Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeAutodiscoverAppPool

8.  Eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

9.  Se il problema ancora esiste, riavviare il servizio IIS utilizzando l'utilità IISReset o il seguente comando:
    
        Iisreset /noforce

10. Eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

11. Se il problema ancora esiste, riavviare il server.

12. Dopo il riavvio del server, eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

13. Se il probe continua a incontrare un errore, chiedere assistenza. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))


---
title: Risoluzione dei problemi del set di integrità EWS
TOCTitle: Risoluzione dei problemi del set di integrità EWS
ms:assetid: f5aaacdd-7f4a-4d63-8440-1c564e644dfc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.ews(v=EXCHG.150)
ms:contentKeyID: 53275549
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi del set di integrità EWS

 

_**Si applica a:**Exchange Server 2013, Project Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

L'integrità dei servizi Web di Exchange (EWS, Exchange Web Services) controlla l'impostazione di integrità complessiva del servizio EWS. L'impostazione di integrità di EWS è strettamente correlata alle seguenti impostazioni di integrità:

[Risoluzione dei problemi di servizi Web Exchange. Set di integrità di protocollo](troubleshooting-ews-protocol-health-set.md)

[Risoluzione dei problemi di servizi Web Exchange. Set di integrità proxy](troubleshooting-ews-proxy-health-set.md)

Se si riceve un avviso che specifica che EWS non è integro, ciò indica l'esistenza di un problema che potrebbe impedire agli utenti di comunicare con il server di Exchange.

## Descrizione

EWS viene monitorato utilizzando i seguenti probe e controlli:


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
<td><p>EwsCtpProbe</p></td>
<td><p>EWS</p></td>
<td><p>Archivio informazioni</p>
<p>Servizi di dominio Active Directory</p></td>
<td><p>EwsCtpMonitor (set di integrità EWS)</p></td>
</tr>
<tr class="even">
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Servizi di dominio Active Directory</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="odd">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Archivio informazioni</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Il probe esegue un accesso completo EWS dal server Accesso client (CAS) al server di cassetta postale tramite un account di monitoraggio. Il probe chiama il metodo **GetFolder** su EWS. Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Problemi comuni

Le cause di errore comuni di questo probe sono:

  - È presente una mancata corrispondenza tra il meccanismo di autenticazione che viene utilizzato dal probe e il meccanismo di autenticazione utilizzato sulla directory virtuale di CAS.

  - Il pool di applicazioni EWS in CAS in fase di monitoraggio, non risponde.

  - Sono stati riscontrati problemi di rete in CAS, quando si connette al server di cassetta postale.

  - Sono stati riscontrati problemi di comunicazione in CAS, quando si connette ai controller di dominio.

  - I controller di dominio non rispondono.

  - Il pool di applicazioni EWS ospitato su uno o più server di cassette postali non risponde.

  - Il database dell'utente non è montato oppure l'Archivio informazioni non è disponibile per una cassetta postale specifica.

  - Sono stati riscontrati problemi relativi al servizio Archivio informazioni su uno o più server di cassette postali.

## Azione utente

È possibile che il servizio venga ripristinato dopo l'emissione dell'avviso. Di conseguenza, se si riceve un avviso indicante che il set di integrità non è in integro, verificare prima che il problema sia ancora presente. Se il problema ancora esiste, eseguire le azioni di ripristino appropriate delineate nelle sezioni seguenti.

## Verifica dell'esistenza del problema

1.  Identificare il nome del set di integrità e il nome del server nell'avviso.
    
    Quando si riceve un allarme da questa impostazione di integrità, il messaggio di posta elettronica contiene le seguenti informazioni:
    
    1.  Il nome del CAS su cui ha avuto origine l'errore
    
    2.  Il nome del server di cassetta postale monitorato dal probe come risorsa di destinazione
    
    3.  Traccia di eccezione completa dell'ultimo errore, inclusi i dati diagnostici e le informazioni specifiche dell'intestazione HTTP
    
    4.  Ora in cui si è verificato l'evento imprevisto
    
    5.  Meccanismo di autenticazione utilizzato e informazioni sulle credenziali
    
    Le informazioni di traccia sull'eccezione forniscono il suggerimento principale sul motivo del mancato funzionamento del probe. Il messaggio di escalation comprende anche le seguenti intestazioni HTTP:
    
    1.  **X-FEServer**   Indica il server Accesso client su cui è stato eseguito il probe
    
    2.  **X-TargetBEServer**   Indica su quale server MBX viene instradata la richiesta
    
    3.  **X-DiagInfo**   Indica il server MBX che ha ricevuto la richiesta

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio contengono informazioni di risoluzione dei problemi sufficienti ad identificare la causa principale. Se i dettagli del messaggio non sono chiari, procedere come segue:
    
    1.  Aprire Exchange Management Shell, quindi utilizzare il seguente comando per recuperare i dettagli del set di integrità che ha emesso l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli dell'impostazione di integrità EWS relativi a server1.contoso.com, eseguire il seguente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS"}
    
    2.  Esaminare l'output del comando per determinare quale controllo ha segnalato l'errore. Il valore **AlertValue** del controllo che ha emesso l'avviso sarà `Unhealthy`.
    
    3.  Eseguire di nuovo il probe associato per il controllo in stato non integro. Per trovare il probe associato, fare riferimento alla tabella nella sezione Explanation. A tale scopo, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Per il set di integrità EWS, si presuma che il controllo in errore sia **EWSCtpMonitor**. Il probe associato a tale sistema di monitoraggio è **EWSCtpProbe**. Per eseguire tale probe su server1.contoso.com, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe EWS\EWSCtpProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, verificare il valore **Result** del probe. Se il valore è **Succeeded**, l'errore era transitorio e non esiste più. Altrimenti, fare riferimento alla procedura di ripristino delineata nella sezioni seguenti.

## Azioni di ripristino di EwsCtpMonitor

1.  Avviare IIS Manager, quindi eseguire la connessione al server che riporta il problema per stabilire se il pool di applicazioni **MSExchangeServicesAppPool** è in esecuzione su entrambi i server Accesso client e Cassette postali.

2.  Individuare MailboxDatabase per i probe in errore. In seguito, verificare che il database della cassetta postale sia attivo per il relativo server e che l'archivio delle informazioni sia integro.

3.  Fare clic su **Pool di applicazioni**, quindi eseguire il riciclo del pool di applicazioni **MSExchangeServicesAppPool** eseguendo il seguente comando da Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  Eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

5.  Se il problema persiste, eseguire il riciclo dell'intero servizio IIS tramite l'utilità IISReset.

6.  Eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

7.  Se il problema persiste, analizzare i file di registro del protocollo sui server CA e di cassette postali. I registri del protocollo relativi al CAS si trovano nella cartella *\<directory di installazione del server exchange\>\\Logging\\HttpProxy\\Ews*. Sul server di cassette postali, i registri risiedono nella cartella *\<directory di installazione del server exchange\>\\Logging\\Cartella Ews*.

8.  Creare un account utente di prova, quindi accedere eseguendo l'account utente di prova sul CAS. Ad esempio, accedere con: https:// \<nomeserver\>/ews/exchange.asmx. Se il problema persiste, provare a utilizzare un CAS differente per determinare se il problema fa riferimento a quel CAS, piuttosto che al server di cassetta postale. Se il nome utente di prova supera l'operazione, è probabile che il problema interessi un database di cassetta postale specifico o il server di cassetta postale nel quale è presente la cassetta postale di monitoraggio. Ripetere questo passaggio tramite l'account di prova presente nel database di cassetta postale.

9.  Verificare la connettività di rete tra server Accesso client e Cassette postali.

10. Verificare l'eventuale presenza di allarmi sul set di integrità EWS.Proxy che potrebbe indicare un problema che interessa il server Accesso client specifico.

11. Verificare l'eventuale presenza di allarmi sull'impostazione di integrità EWS.Protocol che potrebbe indicare un problema che interessa il server Cassette postali specifico.

12. Se il problema ancora esiste, riavviare il server. A questo scopo, eseguire innanzitutto il failover dei database ospitati sul server. A tale scopo, utilizzare il seguente comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    **Nota**   Nel seguente codice di esempio e in tutti quelli successivi, sostituire *server1.contoso.com* con il nome del server effettivo.

13. Verificare che tutti i database siano stati spostati fuori dal server che segnala il problema. A tale scopo, utilizzare il seguente comando:
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    Se l'output comando non mostra copie attive sul server, riavviare il server.

14. Dopo il riavvio del server, eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

15. In caso di esito positivo del probe, eseguire il failback dei database nel server di cassetta postale eseguendo il comando seguente:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

16. In caso di esito ancora negativo del probe, potrebbe essere necessaria assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))


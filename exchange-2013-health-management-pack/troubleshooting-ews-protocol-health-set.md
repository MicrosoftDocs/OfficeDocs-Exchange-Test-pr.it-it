---
title: Risoluzione dei problemi di servizi Web Exchange. Set di integrità di protocollo
TOCTitle: Risoluzione dei problemi di servizi Web Exchange. Set di integrità di protocollo
ms:assetid: 826b2d5b-adbb-4bf5-94b6-0a8de2e3aac0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.ews.protocol(v=EXCHG.150)
ms:contentKeyID: 53275534
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di servizi Web Exchange. Set di integrità di protocollo

 

_**Si applica a:** Exchange Server 2013, Project Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

L'impostazione di integrità EWS.Protocol controlla il protocollo delle comunicazioni dei Servizi Web Exchange sul server Cassette postali. L'impostazione di integrità di EWS.Protocol è strettamente correlata alle seguenti impostazioni di integrità:

[Risoluzione dei problemi del set di integrità EWS](troubleshooting-ews-health-set.md)

[Risoluzione dei problemi di servizi Web Exchange. Set di integrità proxy](troubleshooting-ews-proxy-health-set.md)

Se si riceve un allarme che specifica che EWS.Protocol non risulta integro, potrebbe verificarsi un problema che potrebbe impedire agli utenti di accedere a Exchange.

## Descrizione

L'impostazione di integrità di EWS.Protocol è composta dai probe seguenti:

1.  EwsSelfTestProbe

2.  EwsDeepTestProbe

EwsSelfTestProbe non si basa sull'Archivio informazioni. Tuttavia, il probe EwsDeepTestProbe si basa sull'Archivio informazioni. Entrambi eseguono operazioni EWS sul server Cassette postali e utilizzano lo stesso metodo di autenticazione come un server Accesso client. EwsSeftTestProbe richiama il metodo **ConvertId** e EwsDeepTestProbe richiama il metodo **GetFolder**.


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
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Active Directory</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Archivio informazioni</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

Quando si riceve un allarme da questa impostazione di integrità, il messaggio di posta elettronica contiene le seguenti informazioni:

1.  Il nome del server Cassette postali su cui ha avuto origine l'errore

2.  Analisi completa delle eccezioni dell'ultimo errore, inclusi i dati di diagnostica e le informazioni delle intestazioni HTTP specifiche

3.  Ora in cui si è verificato l'evento imprevisto

## Problemi comuni

Questo probe può riportare un errore per uno qualsiasi dei motivi seguenti:

  - Il pool delle applicazioni di EWS sul server Cassette postali controllato non funziona correttamente.

  - I controller di dominio non rispondono oppure non possono comunicare con il server Cassette postali.

  - Il database dell'utente non è montato oppure l'Archivio informazioni non è disponibile per una cassetta postale specifica.

## Azione utente

È possibile che il servizio sia stato ripristinato dopo l'emissione dell'allarme. Pertanto, quando si riceve un allarme che specifica che l'impostazione di integrità è danneggiata, è necessario verificare innanzitutto se il problema sussiste ancora. Se il problema persiste, eseguire le azioni di ripristino appropriate riportate nelle sezioni seguenti.

## Verifica della persistenza del problema

1.  Identificare il nome dell'impostazione di integrità e il nome del server riportati nell'allarme.

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'allarme. Nella maggior parte dei casi, i dettagli del messaggio forniscono informazioni per la risoluzione dei problemi sufficienti a identificare la causa principale. Se i dettagli del messaggio non sono chiari, procedere come segue:
    
    1.  Aprire Exchange Management Shell ed eseguire il seguente comando per recuperare i dettagli dell'impostazione di integrità che ha emesso l'allarme:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli dell'impostazione di integrità EWS.Protocol relativi a server1.contoso.com, eseguire il comando riportato:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS.Protocol"}
    
    2.  Esaminare l'output comando per stabilire quale monitor ha segnalato l'errore. Il valore **AlertValue** per il monitor che ha emesso l'allarme sarà `Unhealthy`.
    
    3.  Eseguire nuovamente il probe associato per il monitor nello stato danneggiato. Fare riferimento alla tabella nella sezione Explanation per trovare il probe associato. A tale scopo, eseguire il comando seguente:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si supponga che il monitor che riporta l'errore sia **EWSSelfTestMonitor**. Il probe associato al monitor è **EWSSelfTestProbe**. Per eseguire il probe su server1.contoso.com, eseguire il comando riportato:
        
            Invoke-MonitoringProbe EWS.Protocol\EWSSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output comando, esaminare il valore **Risultato** del probe. Se il valore è **Riuscito**, si è trattato di un errore temporaneo che non sussiste più. In caso contrario, fare riferimento alla procedura di ripristino riportata nelle sezioni seguenti.

## Operazioni di recupero EWSSelfTestMonitor e EWSDeepTestMonitor

Questo allarme monitor viene generalmente emesso per server Cassette postali.

1.  Avviare IIS Manager, quindi eseguire la connessione al server che riporta il problema per stabilire se MSExchangeServicesAppPool è in esecuzione su entrambi i server Accesso client e Cassette postali.

2.  Individuare MailboxDatabase per i probe in errore, quindi verificare che MailboxDatabase sia attivo per MailboxServer e che Archivio informazioni sia integro.

3.  Fare clic su **Pool di applicazioni**, quindi eseguire il riciclo del pool di applicazioni **MSExchangeServicesAppPool** eseguendo il seguente comando da Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

5.  Se il problema persiste, riavviare il servizio IIS tramite l'utilità IISReset.

6.  Eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

7.  Se il problema persiste, analizzare i file di registro del protocollo sul server Cassette postali. Sul server Cassette postali, i registri risiedono nella directory di installazione del server *\<Exchange\>*\\Logging\\Cartella Ews.

8.  Creare un account utente di prova, quindi utilizzarlo per accedere al server Cassette postali fornito sulla porta 444 https://*\<servername\>*:444/ews/exchange.asmx. Se la prova riesce un problema potrebbe interessare il database della cassetta postale specifica oppure il server Cassette postali su cui viene eseguito il controllo della cassetta postale. Ripetere questo passaggio tramite l'account di prova sul database.

9.  Verificare l'eventuale presenza di allarmi sull'impostazione di integrità EWS.Protocol che potrebbe indicare un problema che interessa il server Cassette postali specifico.

10. Se il problema persiste, riavviare il server. A tal fine, eseguire innanzitutto il failover dei database ospitati sul server tramite il seguente comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    Nel seguente codice di esempio e in tutti quelli successivi, sostituire *server1.contoso.com* con il nome del server effettivo.

11. Verificare che tutti i database siano stati spostati fuori dal server che segnala il problema. A tale scopo, eseguire il comando seguente:
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    Se l'output comando non mostra copie attive sul server, riavviare il server.

12. Dopo il riavvio del server, eseguire nuovamente il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

13. In caso di esito positivo del probe, eseguire il failover dei database eseguendo il comando seguente:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

14. In caso di esito ancora negativo del probe, potrebbe essere necessaria assistenza per risolvere il problema. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))


---
title: Risoluzione dei problemi Set di integrità OWA
TOCTitle: Risoluzione dei problemi Set di integrità OWA
ms:assetid: eae9dbd7-2ce6-43ce-b9a1-b114fd0c3ab4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.owa(v=EXCHG.150)
ms:contentKeyID: 53275556
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi Set di integrità OWA

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Il set di integrità Outlook Web App (OWA) monitora l'integrità generale del servizio Outlook Web App.

Un eventuale avviso che specifica che Outlook Web App non è integro indica un problema che potrebbe impedire agli utenti l'accesso alle proprie cassette postali tramite Outlook Web App.

## Descrizione

Il servizio Outlook Web App viene monitorato utilizzando i seguenti probe e controlli:


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
<td><p>OwaCtpProbe</p></td>
<td><p>Outlook Web App</p></td>
<td><p>Active Directory</p>
<p>Archivio informazioni</p></td>
<td><p>OwaCtpMonitor</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Problemi comuni

Questo probe può non riuscire per diversi motivi. Di seguito sono elencate alcune delle cause più comuni:

  - L'applicazione Outlook Web App ospitata sul server Accesso client monitorato non risponde o il pool di applicazioni ospitato nel server Cassette postali non risponde.

  - Il server Accesso client ha incontrato problemi di rete e non è in grado di connettersi al server Cassette postali o al controller di dominio.

  - Le credenziali dell'account di monitoraggio non cono corrette.

  - Il database dell'utente non è montato o l'archivio informazioni non è accessibile per tale cassetta postale.

  - L'archivio informazioni non risponde.

  - I controller di dominio non rispondono.

## Azione utente

È possibile che il servizio venga ripristinato dopo l'emissione dell'avviso. Di conseguenza, se si riceve un avviso indicante che il set di integrità non è in integro, verificare prima che il problema sia ancora presente. Se il problema ancora esiste, eseguire le azioni di ripristino appropriate delineate nelle sezioni seguenti.

## Verifica dell'esistenza del problema

1.  Identificare il nome del set di integrità e il nome del server nell'avviso.

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio contengono informazioni di risoluzione dei problemi sufficienti ad identificare la causa principale. Se i dettagli del messaggio non sono chiari, procedere come segue:
    
    1.  Aprire Exchange Management Shell, quindi utilizzare il seguente comando per recuperare i dettagli del set di integrità che ha generato l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Per i dettagli del set di integrità Outlook Web App su server1.contoso.com, utilizzare il seguente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA"}
    
    2.  Esaminare l'output del comando per determinare quale controllo ha segnalato l'errore. Il valore **AlertValue** del controllo che ha emesso l'avviso è `Unhealthy`.
    
    3.  Eseguire di nuovo il probe associato per il controllo in stato non integro. Per trovare il probe associato, fare riferimento alla tabella nella sezione Explanation. A tale scopo, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, per creare un probe di monitoraggio Exchange ActiveSync su *server1.contoso.com*, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe -Identity ActiveSync.Protocol\ActiveSyncSelfTestProbe -Server server1.contoso.com
    
    4.  Nell'output del comando, verificare il valore **Result** del probe. Se il valore è **Succeeded**, l'errore era transitorio e non esiste più. Altrimenti, fare riferimento alla procedura di ripristino delineata nella sezioni seguenti.

## Azioni di ripristino per OwaCtpMonitor

Un avvisto tramite posta elettronica proveniente da un set di integrità contiene le seguenti informazioni:

  - Nome del server che ha inviato l'avviso

  - Traccia di eccezione completa dell'ultimo errore, inclusi i dati diagnostici e le informazioni specifiche dell'intestazione HTTP  
    
    **Nota**   È possibile utilizzare le informazioni contenute nella traccia di eccezione completa per risolvere il problema. L'eccezione generata dal probe contiene una Causa errore che descrive perché il probe non è riuscito. Ad esempio, l'eccezione contiene le seguenti informazioni:
    
      - **MissingKeyword**   Una parola chiave prevista non è stata trovata nella risposta del server. In questo caso, l'eccezione contiene le parole chiave previste.
    
      - **NameResolution**   La risoluzione non è in grado di risolvere un determinato nome server.
    
      - **NetworkConnection**   Il probe sta ricevendo un errore di connessione di rete mentre tentava di collegarsi al pool di app OWA su CAFE.
    
      - **UnexpectedHttpResponseCode**   Risposta con codice HTTP imprevisto. Ad esempio, il server ha restituito il codice HTTP **503**.
    
      - **RequestTimeout**   Il server ha impiegato troppo tempo per rispondere a una richiesta del client.
    
      - **ScenarioTimeout**   Il probe è terminato correttamente ma ha impiegato più di un minuto. Questa condizione in genere indica un sovraccarico del sistema.
    
      - **OwaErrorPage**   Outlook Web App ha restituito una pagina di errore. Il nome dell'errore che ha causato l'esito negativo in genere è disponibile nel messaggio di eccezione.
    
      - **OwaMailboxErrorPage**   Outlook Web App ha restituito una pagina di errore contenente un errore correlato all'Archivio cassette postali. In genere questo evento indica che l'Archivio cassette postali è inattivo o che le cassette postali sono in fase di smontaggio.
    
    La traccia dell'eccezione contiene un campo importante denominato **FailingComponent**. Il probe tenta di stabilire l'errore, come nell'esempio seguente:
    
      - **Cassetta postale**   Il probe può raggiungere Outlook Web App, ma non è in grado di collegarsi all'Archivio cassette postali. In questo caso, il probe non è riuscito o la latenza di accesso alla cassetta postale ha causate l'esito negativo del probe e ha generato un errore **ScenarioTimeout**. Quando si verificano questi tipi di errori, è necessario controllare l'integrità dei server Cassette postali.
    
      - **Active Directory**    Il probe può raggiungere Outlook Web App ma non è in grado di collegarsi a Active Directory. In questo caso, il probe non è riuscito o le latenze di chiamata di Active Directory potrebbero averne causato la scadenza. Quando si verificano questi tipi di errori, è necessario controllare l'integrità dei controller di dominio nonché le connessioni di rete tra i server Accesso client e Cassette postali e i controller di dominio.
    
      - **Owa**   In genere indica un errore che si è verificato nel livello Outlook Web App. Quando si verificano questi tipi di errori, è necessario verificare l'integrità del processo Outlook Web App sui server Accesso client e Cassette postali, nonché le connessioni di rete.
    
    L'eccezione contiene anche le informazioni più recenti su richiesta HTTP e risposta ricevute prima dell'errore del probe. Il corpo dell'escalation contiene il percorso dei registri dei probe. È possibile utilizzare queste informazioni per determinare le richieste e le riposte Web HTTP complete inviate al momento dell'errore del probe. Il file contiene solo i dati dei probe non riusciti perché vengono registrati sono i tentativi falliti. È possibile utilizzare tali informazioni per ottenere una visualizzazione più completa del motivo della mancata riuscita del test.

  - Livello a cui è calata la metrica della disponibilità (x%).

  - Il percorso completo della cartella contenente le tracce delle richiese HTTP complete per il probe. Per impostazione predefinita le informazioni si trovano nella cartella *\<ExchangeServer\>*\\Logging\\Monitoring\\OWA\\ClientAccessProbe.

  - La data e l'ora in cui si è verificato l'avviso.

Per risolvere il problema, procedere come segue:

1.  Creare un account utente di prova, quindi accedere al server Accesso client con tale account. Ad esempio, accedere utilizzando https:// *\<nomeserver\>*/owa.
    
    Se non riesce, provare a usare un altro server Accesso client per verificare se il problema di verifica su uno specifico server Accesso client e non sul server Cassette postali.

2.  Verificare la connettività di rete tra server Accesso client e Cassette postali. Utilizzare ping.exe per verificare che ogni server risponda.

3.  Verificare che non presenti avvisi sul set di integrità OWA.Protocol indicanti un problema che influisce su uno specifico server Cassette postali. Per ulteriori informazioni, vedere [Risoluzione dei problemi di OWA. Set di integrità di protocollo](troubleshooting-owa-protocol-health-set.md).

4.  Avviare Gestione IIS, quindi connettersi al server che segnala il problema per verificare se il pool di applicazioni MSExchangeOwaAppPool è in esecuzione sul server Accesso client.

5.  In Gestione IIS, verificare che il sito Web Default sia in esecuzione.

6.  Individuare il database delle cassette postali per i probe non riusciti e verificare che il database delle cassette postali sia attivo su un server Cassette postali e che l'Archivio cassette postali sia attivo. Per individuare le informazioni sul GUID del database non riuscito, aprire le informazioni sulla traccia delle eccezioni. Ogni errore deve contenere una voce simile al seguente esempio:
    
    Starting Owa probe with Target: https://localhost/owa/, Username: *HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com*

7.  Copiare il GUID HealthMailbox ed eseguire il comando di seguito riportato in Shell:
    
        Get-Mailbox -Monitoring -Identity <username>
    
    Ad esempio, eseguire il seguente comando:
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    Nell'oggetto restituito è possibile individuare il nome del database e stabilire dove risiede il database attivo.

8.  Se è stato configurato il reindirizzamento tra siti, è possibile che i probe non riescano e generino un errore MissingKeyword. Questo si verifica perché per impostazione predefinita i probe Accesso client vengono eseguiti sugli account per qualsiasi posizione e perché il probe non tenta di verificare un server Accesso client su un sito diverso quando utilizza il rendirizzamento. Per risolvere il problema, accertarsi che i server su ogni sito siano contenuti in MonitoringGroups. I server Accesso client di un determinato gruppo di monitoraggio si verificano solo insieme ai server Cassette postali dello stesso gruppo.
    
    Per stabilire i gruppi di monitoraggio per i server, utilizzare il seguente comando:
    
        Get-ExchangeServer | ft MonitoringGroup
    
    Per modificare il gruppo di monitoraggio su un server, utilizzare il parametro *MonitoringGroup* insieme al cmdlet **Set-ExchangeServer**. Ad esempio, utilizzare:
    
        Set-ExchangeServer -Identity "ServerName" -MonitoringGroup "Primary"

9.  In Gestione IIS, fare clic su **Pool di applicazioni** e riavviare il pool di applicazioni **MSExchangeAutodiscoverAppPool** eseguendo il comando di seguito riportato da Exchange Management Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

10. Eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

11. Se il problema ancora esiste, riavviare il servizio IIS utilizzando l'utilità IISReset o il seguente comando:
    
        Iisreset /noforce

12. Eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

13. Se il problema ancora esiste, riavviare il server.

14. Dopo il riavvio del server, eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

15. Se il probe continua a incontrare un errore, chiedere assistenza. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))


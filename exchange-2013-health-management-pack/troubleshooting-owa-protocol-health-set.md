---
title: Risoluzione dei problemi di OWA. Set di integrità di protocollo
TOCTitle: Risoluzione dei problemi di OWA. Set di integrità di protocollo
ms:assetid: fe172da8-65d3-43e0-ba62-d36a1b05fc11
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.owa.protocol(v=EXCHG.150)
ms:contentKeyID: 53275558
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di OWA. Set di integrità di protocollo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Il set di integrità OWA.Protocol monitora il protocollo Outlook Web App sul server Cassette postali.

Un eventuale avviso che specifica che OWA.Protocol non è integro indica un problema che potrebbe impedire agli utenti l'accesso alle proprie cassette postali tramite Outlook Web App.

## Descrizione

Il servizio OWA viene monitorato utilizzando i seguenti probe e controlli:


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
<td><p>OwaSelfTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>Nessuna</p></td>
<td><p>OwaSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>OwaDeepTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>Active Directory</p>
<p>Archivio informazioni</p></td>
<td><p>OwaDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Il probe **OwaSelfTestProbe** invia una singola richiesta HTTP al seguente indirizzo: https://hostlocale:444/owa/exhealth.check. Il probe conferma che il pool di applicazioni risponde restituendo il codice di stato **200 OK**. Questo probe non ha dipendenze con altri componenti di Exchange.

Il probe **OwaDeepTestProbe** viene eseguito su ogni database delle cassette postali utilizzando copie sul server corrente. Il probe determina che sia possibile eseguire l'accesso completo su tale server. A tale scopo simula il tipo di traffico generato da un server Accesso client su tale server specifico. Il probe dipende da Servizi di dominio Active Directory (AD DS) per l'autenticazione e dell'archivio cassette postali per l'accesso alle cassette postali. Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Problemi comuni

Le cause di errore comuni di questo probe sono:

  - Il pool di applicazioni OWA ospitato sul server Accesso client monitorato non risponde o il pool di applicazioni ospitato nel server Cassette postali non risponde.

  - Il server Accesso client o Cassette postali ha incontrato problemi di rete e non è in grado di connettersi all'altro server o a un controller di dominio.

  - Le credenziali dell'account di monitoraggio non cono corrette.

  - Il database dell'utente non è montato o l'archivio informazioni non è accessibile per tale cassetta postale.

  - L'archivio informazioni non risponde.

  - I controller di dominio non rispondono.

## Azione utente

È possibile che il servizio venga ripristinato dopo l'emissione dell'avviso. Di conseguenza, se si riceve un avviso indicante che il set di integrità non è in integro, verificare prima che il problema sia ancora presente. Se il problema ancora esiste, eseguire le azioni di ripristino appropriate delineate nelle sezioni seguenti.

## Verifica dell'esistenza del problema

1.  Identificare il nome del set di integrità e il nome del server nell'avviso.

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio contengono informazioni di risoluzione dei problemi sufficienti ad identificare la causa principale. Se i dettagli del messaggio non sono chiari, procedere come segue:
    
    1.  Aprire Exchange Management Shell, quindi utilizzare il seguente comando per recuperare i dettagli del set di integrità che ha emesso l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli del set di integrità OWA.Protocol su server1.contoso.com, utilizzare il seguente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Protocol"}
    
    2.  Esaminare l'output del comando per determinare quale controllo ha segnalato l'errore. Il valore di **AlertValue** per il controllo che ha emesso l'avviso sarà `Unhealthy`.
    
    3.  Eseguire di nuovo il probe associato per il controllo in stato non integro. Per trovare il probe associato, fare riferimento alla tabella nella sezione Explanation. A tale scopo, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Ad esempio, si presuma che il controllo con l'errore sia **OwaSelfTestMonitor**. Il probe associato a tale controllo è **OwaSelfTestProbe**. Per eseguire tale probe su server1.contoso.com, utilizzare il seguente comando:
        
            Invoke-MonitoringProbe OWA.Protocol\OwaSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  Nell'output del comando, verificare il valore **Result** del probe. Se il valore è **Succeeded**, l'errore era transitorio e non esiste più. Altrimenti, fare riferimento alla procedura di ripristino delineata nella sezioni seguenti.

Quando si riceve un avviso da un set di integrità, il messaggio di posta elettronica contiene le informazioni seguenti:

  - Nome del server che ha inviato l'avviso

  - Tipo di probe non riuscito (SelfTest o DeepTest)

  - Ora e data in cui si è verificato l'avviso

  - Percorso della cartella in cui risiedono le tracce delle richieste HTTP per il probe
    
      
    Per impostazione predefinita, questi file si trovano nelle seguenti cartelle:
    
      - SelfTestProbe: \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\ProtocolProbe
    
      - DeepTestProbe: \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\MailboxProbe

  - Traccia di eccezione completa dell'ultimo errore, inclusi i dati diagnostici e le informazioni specifiche dell'intestazione HTTP  
    
    **Nota**   È possibile utilizzare le informazioni contenute nella traccia di eccezione completa per risolvere il problema. L'eccezione generata dal probe contiene una Causa errore che descrive perché il probe non è riuscito. La Causa errore può essere:
    
      - **MissingKeyword**   Una parola chiave prevista non è stata trovata nella risposta del server. In questo caso, l'eccezione contiene le parole chiave previste.
    
      - **NameResolution**   La risoluzione DNS non è in grado di risolvere un determinato nome server.
    
      - **NetworkConnection**   Il probe sta ricevendo un errore di connessione di rete mentre tenta di collegarsi al pool di applicazioni OWA su CAFE.
    
      - **UnexpectedHttpResponseCode**   La riposta conteneva codice HTTP imprevisto. Ad esempio, il server ha restituito il codice HTTP **503**.
    
      - **RequestTimeout**   Il server ha impiegato troppo tempo per rispondere a una richiesta del client.
    
      - **UnexpectedHttpResponseCode**   La riposta ha restituito codice HTTP imprevisto. Ad esempio, il server ha restituito il codice HTTP **503**.
    
      - **ScenarioTimeout**   Il probe è terminato correttamente ma ha impiegato più di un minuto. Questa condizione in genere indica un sovraccarico del sistema.
    
      - **OwaErrorPage**   OWA ha restituito una pagina di errore. Il nome dell'errore che ha causato l'esito negativo in genere è disponibile nel messaggio di eccezione.
    
      - **OwaMailboxErrorPage**   OWA ha restituito una pagina di errore contenente un errore correlato all'Archivio cassette postali. Ciò in genere indica problemi quali l'inattività dell'archivio cassette postali o cassette postali smontate.
    
    La traccia delle eccezioni contiene un campo importante denominato **FailingComponent** in cui il probe tenta di determinare e classificare l'errore. Ad esempio, il probe potrebbe restituire uno dei seguenti valori:
    
      - **Cassetta postale**   Il probe può raggiungere OWA, ma non è in grado di collegarsi all'Archivio cassette postali. In questo caso, il probe non è riuscito o la latenza di accesso alla cassetta postale ha causato l'esito negativo del probe e ha generato un errore **ScenarioTimeout**. Quando si verificano questi tipi di errori, è necessario controllare l'integrità dei server Cassette postali.
    
      - **Active Directory**   Il probe è in grado di raggiungere OWA ma non di collegarsi a AD DS. In questo caso il probe non è riuscito o le latenze delle chiamate AD DS potrebbero causare il timeout del probe. Quando si verificano questi tipi di errori, è necessario controllare l'integrità dei controller di dominio nonché le connessioni di rete tra i server Accesso client e Cassette postali e i controller di dominio.
    
      - **OWA**   In genere indica un errore che si è verificato nel livello di OWA. Quando si verificano questi tipi di errori, è necessario verificare l'integrità del processo OWA sui server Accesso client e Cassette postali, nonché le connessioni di rete.
    
    L'eccezione contiene anche le informazioni più recenti su richiesta HTTP e risposta ricevute prima dell'errore del probe.  
      
    Il corpo dell'escalation contiene il percorso dei registri dei probe che è possibile utilizzare per verificare le richieste Web HTTP complete e le risposte inviate quando il probe non è riuscito. Il file contiene solo i dati dei probe non riusciti perché vengono registrati sono i tentativi falliti. È possibile utilizzare tali informazioni per ottenere una visualizzazione più completa del motivo della mancata riuscita del test.

## Azioni di ripristino di OwaSelfTestProbe

Poiché questo probe presenta pochissime dipendenze, gli errori in genere si verificano quando il processo del pool di applicazioni OWA non risponde.

Per risolvere il problema, procedere come segue:

1.  Fare clic sull'URL del registro di traccia del probe nel corpo del messaggio di posta elettronica di avviso per verificare se si stanno verificando nuovi errori.

2.  Creare un account utente di prova sullo stesso server su cui è montata la cassetta postale. Provare ad accedere per verificare se è possibile riprodurre il problema.

3.  Verificare se sono presenti avvisi sul set di integrità OWA che indicano un problema che influisce su uno specifico server Cassette postali. Per ulteriori informazioni, vedere [Risoluzione dei problemi Set di integrità OWA](troubleshooting-owa-health-set.md).

4.  Avviare Gestione IIS, quindi connettersi al server che segnala l'errore per determinare se il pool di applicazioni **MSExchangeOwaAppPool** è in esecuzione sul server Accesso client.

5.  In Gestione IIS, verificare che il sito Web Default sia in esecuzione.

6.  In Gestione IIS, fare clic su **Pool di applicazioni** e riavviare il pool di applicazioni **MSExchangeAutodiscoverAppPool** eseguendo il comando di seguito riportato da Exchange Management Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

7.  Eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

8.  Se il problema ancora esiste, riavviare il servizio IIS utilizzando l'utilità IISReset o il seguente comando:
    
        Iisreset /noforce

9.  Eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

10. Se il problema ancora esiste, riavviare il server.

11. Dopo il riavvio del server, eseguire di nuovo il probe associato come mostrato nel passaggio 2c della sezione Verifying the issue still exists.

12. Se il probe continua a incontrare un errore, chiedere assistenza. Contattare un responsabile del supporto tecnico Microsoft per risolvere il problema. Per contattare un responsabile del supporto tecnico Microsoft, visitare il [Centro di supporto di Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809) Nel riquadro di spostamento, fare clic su **Opzioni e risorse di supporto** e usare una delle opzioni elencate in **Richiedi supporto tecnico** per contattare un responsabile del supporto tecnico Microsoft. Dal momento che l'organizzazione potrebbe avere una procedura specifica per contattare direttamente il Servizio Supporto Tecnico Clienti Microsoft, esaminare innanzitutto le linee guida dell'organizzazione.

## Azioni di ripristino di OwaDeepTestProbe

1.  Per stabilire se il problema ancora esiste, creare un account utente di prova sullo stesso server su cui è montata la cassetta postale e tentare di accedere a OWA. Ad esempio, accedere con: https://*\<nomeserver\>*/owa.

2.  Verificare se sono presenti avvisi sul set di integrità OWA che indicano un problema che influisce su uno specifico server Cassette postali. Per ulteriori informazioni, vedere [Risoluzione dei problemi Set di integrità OWA](troubleshooting-owa-health-set.md).

3.  Avviare Gestione IIS, quindi connettersi al server che segnala l'errore per determinare se il pool di applicazioni **MSExchangeOwaAppPool** è in esecuzione sul server Accesso client.

4.  In Gestione IIS, verificare che il sito Web Default sia in esecuzione.

5.  Individuare il database delle cassette postali per i probe non riusciti e verificare che il database delle cassette postali sia attivo sul server Cassette postali e che l'Archivio cassette postali sia integro. Per individuare le informazioni sul GUID del database non riuscito, aprire le informazioni sulla traccia delle eccezioni. Ogni errore deve contenere una voce simile al seguente esempio:
    
    `Starting Owa probe with Target: https://localhost/owa/, Username:  HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com`

6.  Copiare il GUID HealthMailbox ed eseguire il comando di seguito riportato in Shell:
    
        Get-Mailbox -Monitoring -Identity <username>
    
    Ad esempio, eseguire il seguente comando:
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    Nell'oggetto restituito è possibile individuare il nome del database e stabilire dove risiede il database attivo.

7.  In Gestione IIS, fare clic su **Pool di applicazioni** e riavviare il pool di applicazioni **MSExchangeOWAAppPool** eseguendo il comando di seguito riportato da Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

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


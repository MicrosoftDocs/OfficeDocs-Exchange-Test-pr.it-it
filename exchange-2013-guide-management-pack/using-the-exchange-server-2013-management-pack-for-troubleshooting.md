---
title: Utilizzo del Management Pack di Exchange Server 2013 per la risoluzione dei problemi
TOCTitle: Utilizzo del Management Pack di Exchange Server 2013 per la risoluzione dei problemi
ms:assetid: c9672dad-1e67-4f07-bad9-539a67f2ac70
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn195913(v=EXCHG.150)
ms:contentKeyID: 53275566
ms.date: 08/30/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utilizzo del Management Pack di Exchange Server 2013 per la risoluzione dei problemi

 

_**Ultima modifica dell'argomento:**  2013-04-09_

[Guida introduttiva a Exchange Server 2013 Management Pack](getting-started-with-exchange-server-2013-management-pack.md) fornisce una panoramica del dashboard del Management Pack. In questo argomento viene indicato come può essere utile per risolvere un problema. Per illustrare il processo, viene utilizzato un esempio. Si prenda in considerazione il seguente scenario:

Rob Fielder è un amministratore di Exchange presso Contoso. Apre la console SCOM e fa clic su **Integrità del server** nel dashboard di Exchange Server 2013 per controllare lo stato dei suoi server Exchange. Nota uno stato critico per **Componenti del servizio** su uno dei server Accesso client.

![Errore del server Accesso client](images/Dn195913.32a265d9-68e0-4d8c-9f83-1d10cdda1f84(EXCHG.150).png "Errore del server Accesso client")

Quindi fa doppio clic sul server per aprire la finestra **Esplora stati**. In tale finestra nota che il componente del servizio in stato non integro è il set di integrità OWA.Proxy. Fa clic per visualizzare le informazioni rilevanti per il set di integrità.

![Dettagli dell'integrità del server Accesso client con errore](images/Dn195913.8e4d05a6-9128-40d8-b262-e60e9affc973(EXCHG.150).png "Dettagli dell'integrità del server Accesso client con errore")

Il collegamento fornito sotto External Knowledge Resources porta Rob all'argomento [Risoluzione dei problemi relativi all'impostazione di integrità di OWA.Proxy](https://technet.microsoft.com/it-it/library/jj737712\(v=exchg.150\)). Leggendo l'articolo Rob apprende che la prima cosa da fare è verificare che il problema esista ancora. Seguendo le istruzioni, utilizza il seguente comando per verificare lo stato corrente del set di integrità OWA.Proxy in Shell:

```Powershell
    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
```

L'esecuzione del comando restituisce il seguente output:

```Powershell
    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Unhealthy  OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy
```

Rob nota che il problema riguarda il pool di applicazioni OWA. Il passaggio successivo è la riesecuzione del probe associato per il monitor in stato non integro. Facendo riferimento alla tabella dell'argomento “Risoluzione dei problemi del set di integrità OWA.Proxy”, stabilisce che il probe da rieseguire è OWAProxyTestProbe. Esegue il comando indicato di seguito:

```Powershell
    Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server Server1.contoso.com | Format-List
```

Cerca nell'output il valore di ResultType e scopre che il probe non è riuscito:

```Powershell
    ResultType : Failed
```

Passa alla sezione “Azioni di ripristino di OWAProxyTestMonitor” dell'articolo. Si connette a Server1 tramite Gestione IIS per verificare se MSExchangeOWAAppPool è in esecuzione sul server IIS. Dopo aver verificato che è in esecuzione, riavvia MSExchangeOWAAppPool:

```Powershell
    C:\Windows\System32\Inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool
```

Dopo il riavvio di MSExchangeOWAAppPool, verifica di nuovo che il problema esista ancora rieseguendo il probe tramite il cmdlet Invoke-MonitoringProbe e questa volta ottiene un risultato di esito positivo. Quindi utilizza il comando seguente per verificare che il set di integrità riporti lo stato **Integro**:

```Powershell
    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
```

Questa volta rileva che il problema si è risolto.

```Powershell
    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Healthy    OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy
```

Torna alla console SCOM e verifica che il problema è risolto.

![Integrità del server](images/Dn195908.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "Integrità del server")

Lo scenario precedentemente descritto è una semplice dimostrazione del flusso di lavoro della risoluzione dei problemi da seguire quando viene visualizzato un avviso nella console SCOM. Anche se i dettagli possono variare, in genere il flusso di lavoro è simile per ogni problema segnalato nella console.


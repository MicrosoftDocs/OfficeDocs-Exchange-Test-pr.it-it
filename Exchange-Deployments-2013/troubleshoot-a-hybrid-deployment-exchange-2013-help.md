---
title: 'Risolvere i problemi relativi a una distribuzione ibrida: Exchange 2013 Help'
TOCTitle: Risolvere i problemi relativi a una distribuzione ibrida
ms:assetid: bbae72f3-6a1e-4cbf-80da-d8f73d969c6b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ659053(v=EXCHG.150)
ms:contentKeyID: 50482155
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Risolvere i problemi relativi a una distribuzione ibrida

 

_<strong>Si applica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2016-04-29_

Configurare una distribuzione ibrida in Exchange con la procedura guidata per la configurazione ibrida riduce sensibilmente la possibilità che si verifichino problemi nella distribuzione ibrida. Esistono, tuttavia, alcune aree tipiche che non rientrano nell'ambito della procedura guidata per la configurazione ibrida che, se non configurate correttamente, potrebbero presentare problemi in una distribuzione ibrida. In questo argomento vengono illustrate le seguenti aree comuni in cui potrebbero verificarsi dei problemi e vengono illustrati i passaggi di base per verificare o correggere i problemi:

  - Server Exchange locali

  - Certificati

  - Errori specifici della procedura guidata per la configurazione ibrida


> [!NOTE]
> In questo argomento, "server Exchange" indica quanto segue: 
> <UL>
> <LI>
> <P><STRONG>Server Accesso Client</STRONG> Exchange 2013 e versioni precedenti</P>
> <LI>
> <P><STRONG>Server Cassette postali</STRONG> Exchange 2016 e versioni successive</P></LI></UL>



Per ulteriori informazioni, vedere [Distribuzioni ibride di Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

Per le attività di gestione aggiuntive correlate alle distribuzioni ibride, vedere [Procedure di distribuzione ibrida](hybrid-deployment-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: varia a seconda del tipo di problemi relativi alla distribuzione ibrida

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere voce "Distribuzioni ibride" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](https://technet.microsoft.com/it-it/library/dd638114\(v=exchg.150\)).

  - Le istruzioni in questo argomento si applicano a distribuzioni ibride configurate con la procedura guidata per la configurazione ibrida. Le distribuzioni ibride configurate manualmente non sono supportate.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](https://technet.microsoft.com/it-it/library/jj150484\(v=exchg.150\)).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Risoluzione dei problemi con i server Exchange locali

La configurazione dei server Exchange locali è in genere l'area di una distribuzione ibrida in cui può verificarsi la maggior parte dei problemi. Generalmente, le aree che devono essere esaminate sono le seguenti:

  - **Disponibilità**   Pubblicare correttamente i server Exchange locali in Internet è fondamentale affinché le funzionalità operino correttamente nella distribuzione ibrida. A tal fine, è necessario configurare il firewall locale o altre appliance di sicurezza per consentire l'accesso in ingresso da Internet agli endpoint di individuazione automatica e dei servizi Web di Exchange nei server Exchange locali. Inoltre, i server Exchange devono essere configurati per accettare la posta SMTP in ingresso. Se il servizio Microsoft Exchange Online Protection (EOP) incluso nell'organizzazione tenant Office 365 non riesce a raggiungere i server Exchange locali, il trasporto posta sicuro dall'organizzazione di Exchange Online all'organizzazione locale non funzionerà correttamente.

  - **Certificati**   Il certificato digitale utilizzato per il trasporto posta sicuro tra le organizzazioni locali e di Exchange Online deve essere installato in tutti i server Exchange locali con connessione a Internet che comunicheranno con Exchange Online, deve essere rilasciato da un'autorità di certificazione di terze parti (CA), non deve essere scaduto e deve avere i servizi IIS e SMTP assegnati. Se questi requisiti del certificato non vengono rispettati, il trasporto posta sicuro dall'organizzazione di Exchange Online all'organizzazione locale non funzionerà correttamente. Ulteriori informazioni sui requisiti del certificato vengono fornite in "Risoluzione dei problemi relativi ai certificati" più avanti in questo argomento.

## Come si stabilisce se i server Exchange sono configurati correttamente?

Per verificare che i server Exchange locali siano stati pubblicati correttamente, utilizzare Analizzatore connettività remota di Microsoft per verificare la connettività Internet in ingresso per i server Exchange locali. Eseguire le operazioni seguenti:

1.  Andare allo strumento [Analizzatore connettività remota](https://www.testexchangeconnectivity.com/).

2.  Questo passaggio è un test generale delle attività EWS per confermare che funzionino e che l'endpoint EWS sia configurato.
    
    Eseguire il test **Sincronizzazione, Notifica, Disponibilità e Risposte automatiche (Fuori sede)** nella sezione **Prove di connettività dei servizi Web di Microsoft Exchange** e verificare che non siano presenti errori. Se si verificano errori, correggere gli elementi identificati dal test.

3.  Questo passaggio è un test generale del servizio di individuazione automatica per confermarne il funzionamento e per verificare che l'endpoint di individuazione automatica sia configurato.
    
    Eseguire il test **Individuazione automatica di Outlook** nella sezione **Prove di connettività di Microsoft Office Outlook** e verificare che non siano presenti errori. Se si verificano errori, correggere gli elementi identificati dal test.

4.  Si tratta di un passaggio di un test generale della connettività SMTP, in grado di confermare che i server Exchange siano in grado di ricevere posta Internet in ingresso.
    
    Eseguire il test **Posta elettronica SMTP in ingresso** nella sezione **Prove di posta elettronica Internet** e verificare che non siano presenti errori. Se si verificano errori, correggere gli elementi identificati dal test.

## Risoluzione dei problemi relativi ai certificati

La configurazione dei certificati installati nei server Exchange locali potrebbe essere l'origine dei problemi che si verificano in una distribuzione ibrida. Nella maggior parte dei casi, i seguenti problemi relativi ai certificati influiscono sulla funzionalità ibrida:

  - **Tipo di certificato**   Il certificato digitale utilizzato per il trasporto ibrido sicuro e definito nella procedura guidata per la configurazione ibrida deve essere emesso da un'autorità di certificazione di terze parti. Non è possibile utilizzare i certificati autofirmati per l'autenticazione del trasporto ibrido. Se un certificato autofirmato viene inavvertitamente selezionato o assegnato, il trasporto posta sicuro tra Exchange Online e le organizzazioni locali non funzionerà correttamente.

  - **Servizi assegnati**   Internet Information Service (IIS) e Simple Mail Transport Protocol (SMTP) devono essere assegnati al certificato digitale utilizzato per il trasporto ibrido. Se i servizi non vengono assegnati, il trasporto posta sicuro tra Exchange Online e le organizzazioni locali non funzionerà correttamente.

  - **Installazione**   Il certificato digitale utilizzato per il trasporto posta sicuro tra le organizzazioni locali e di Exchange Online deve essere installato in tutti i server Exchange locali. Se si sta eseguendo la distribuzione ibrida con i server Trasporto Edge locali, il certificato digitale deve essere installato anche nei server Trasporto Edge. Se il certificato non viene installato nei server locali, il trasporto posta sicuro tra Exchange Online e le organizzazioni locali non funzionerà correttamente.

  - **Scadenza**   Il certificato digitale utilizzato per il trasporto posta sicuro tra le organizzazioni locali e di Exchange Online non deve essere scaduto. Se il certificato è scaduto, il trasporto posta sicuro tra Exchange Online e le organizzazioni locali non funzionerà correttamente.

## Come si stabilisce se i certificati sono configurati correttamente?

Per verificare che il certificato per il trasporto posta ibrido sia configurato correttamente nei server Exchange locali, eseguire le operazioni seguenti:

1.  In un server x di Exchange locale, aprire Exchange Management Shell.

2.  In Exchange Management Shell, eseguire il comando seguente.
    
        Get-ExchangeCertificate| format-list

3.  Individuare le informazioni relative al certificato definito nella procedura guidata per la configurazione ibrida che verrà usato per il trasporto posta sicuro.

4.  Verificare che i seguenti valori dei parametri siano assegnati al certificato:
    
      - **Parametro IsSelfSigned**   Questo valore parametro deve essere uguale a *False*.
    
      - **Parametro RootCAType**   Questo valore parametro deve essere uguale a *Third Party*.
    
      - **Parametro Services**   Questo valore parametro deve essere uguale a *IIS, SMTP*.
    
      - **Parametro NotAfter**   Questo valore parametro è la data di scadenza del certificato. La data elencata qui non deve essere scaduta.

## Risoluzione degli errori specifici della procedura guidata per la configurazione ibrida

Se viene visualizzato un errore durante l'esecuzione della procedura guidata per la configurazione ibrida, è spesso possibile risolvere il problema eseguendo alcuni semplici controlli o azioni. Vedere i seguenti suggerimenti per la risoluzione dei problemi o messaggi specifici che potrebbero essere visualizzati durante l'esecuzione della procedura guidata per la configurazione ibrida.

  - **Messaggio:"Impossibile trovare il connettore di ricezione predefinito nel server \<Nome server\>"**   Questo messaggio viene visualizzato se il connettore di ricezione in qualsiasi server Exchange elencato nel seguente attributo non ascolta la porta TCP 25 per i protocolli IPv4 e IPv6: `(Get-HybridConfiguration).ReceivingTransportServers.`
    
      -    Per verificare che i connettori di ricezione sui server Exchange elencati durante l'esecuzione di `(Get-HybridConfiguration).ReceivingTransportServers.` presentino i binding corretti, utilizzare il seguente comando in Exchange Management Shell.
        
      Get-ReceiveConnector -Server <Server Name> | FT Identity, Bindings
        
      Viene visualizzata la voce seguente elencata per i serverExchange: `{[::]:25, 0.0.0.0:25}`
        
      Se l'associazione non è elencata, è necessario aggiungerla al connettore di ricezione usando il parametro *Bindings* del cmdlet **Set-ReceiveConnector**. Per informazioni dettagliate, vedere [Set-ReceiveConnector](https://technet.microsoft.com/it-it/library/bb125140\(v=exchg.150\)).


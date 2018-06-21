---
title: 'Gestione ibrida nelle distribuzioni ibride di Exchange 2013/Exchange 2007: Exchange 2013 Help'
TOCTitle: Gestione ibrida nelle distribuzioni ibride di Exchange 2013/Exchange 2007
ms:assetid: 4b4370d5-1645-4b44-b4e0-c585fcaf970f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn151299(v=EXCHG.150)
ms:contentKeyID: 54651639
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestione ibrida nelle distribuzioni ibride di Exchange 2013/Exchange 2007

Questo argomento è in fase di definizione.  

_<strong>Si applica a:</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>Ultima modifica dell'argomento:</strong>2016-12-09_

Quando si installa un server che esegue Exchange Server 2013 nell'organizzazione Exchange 2007 locale, gli strumenti di gestione di Exchange 2013 vengono automaticamente installati sul server. È possibile utilizzare gli strumenti elencati di seguito per configurare e gestire la funzionalità ibrida di entrambe le organizzazioni locali di Exchange e di Exchange Online:

  - **Interfaccia di amministrazione di Exchange**   L'interfaccia di amministrazione di Exchange è una console di gestione basata sul Web inclusa in Exchange 2013, facile da usare e ottimizzata per le distribuzioni locali, online o ibride di Exchange. L'interfaccia di amministrazione di Exchange integra Exchange Management Console e il Pannello di controllo di Exchange, ovvero le interfacce utilizzate per la gestione di Exchange Server 2007.

  - **Exchange Management Shell**Exchange Management Shell è un'interfaccia della riga di comando basata su Windows PowerShell.

## Interfaccia di amministrazione di Exchange

L'interfaccia di amministrazione di Exchange consente di eseguire numerose attività di distribuzione e le più comuni attività amministrative quotidiane sia nei server Exchange locali che nell'organizzazione di Exchange Online. Viene installata per impostazione predefinita in tutti i server Exchange 2013. Inoltre, poiché si tratta di una console di gestione basata sul Web, è accessibile anche tramite un Web browser da altri computer della rete o via Internet, utilizzando l'URL della directory virtuale ECP.


> [!IMPORTANT]
> Per accedere all'interfaccia di amministrazione di Exchange utilizzando un account con una cassetta postale collocata su un server Cassette postali di Exchange 2007 (ad esempio un account di amministratore di dominio), è necessario utilizzare l'indirizzo seguente nel browser:<BR>https://<EM>&lt;FQDN of Exchange 2013 Client Access server&gt;</EM>/ECP? ExchClientVer=15



Per accedere all'organizzazione di Exchange Online nell'interfaccia di amministrazione di Exchange è necessario selezionare la scheda per l'esplorazione cross-premises di Office 365. L'esplorazione cross-premises permette di passare velocemente dall'organizzazione di Exchange Online all'organizzazione di Exchange locale e viceversa. Se è stata configurata una distribuzione ibrida, selezionando la scheda Office 365 è possibile gestire gli oggetti dell'organizzazione di Exchange Online e dei destinatari. Se non è presente alcuna organizzazione di Exchange Online, facendo clic sul collegamento a Office 365 si accede alla pagina di iscrizione a Office 365.

Per ulteriori informazioni sull'interfaccia di amministrazione di Exchange, vedere [Interfaccia di amministrazione di Exchange in Exchange 2013](https://technet.microsoft.com/it-it/library/jj150562\(v=exchg.150\)).

## Exchange Management Shell

Exchange Management Shell consente di eseguire le stesse attività dell'interfaccia di amministrazione di Exchange e alcune attività aggiuntive che possono essere eseguite solo nella Exchange Management Shell. Exchange Management Shell è un insieme di script e di cmdlet di Windows PowerShell installati su un computer insieme agli strumenti di gestione di Exchange 2013. Gli script e i cmdlet vengono caricati quando Exchange Management Shell viene aperto utilizzando l'icona di Exchange Management Shell. Se Windows PowerShell viene aperto direttamente, gli script e i cmdlet di Exchange non saranno caricati e non sarà possibile gestire l'organizzazione locale.


> [!NOTE]
> È possibile creare una connessione manuale di Windows PowerShell all'organizzazione locale, con una procedura simile a quella utilizzata per la connessione manuale all'organizzazione Exchange Online riportata di seguito. Si consiglia tuttavia di utilizzare l'icona di Exchange Management Shell per aprire la Exchange Management Shell e gestire i server di Exchange locali.



Quando Exchange Management Shell viene aperto utilizzando l'icona di Exchange Management Shell in un computer in cui sono installati gli strumenti di gestione, è possibile gestire l'organizzazione locale. Tuttavia, non è possibile gestire l'organizzazione Exchange Online quando Exchange Management Shell viene aperto utilizzando tale icona. Ciò accade perché, quando Exchange Management Shell viene aperto utilizzando l'icona di Exchange Management Shell, l'utente viene connesso automaticamente a un server Exchange locale.

Per gestire l'organizzazione Exchange Online utilizzando Windows PowerShell, è necessario aprire Windows PowerShell direttamente e non tramite l'icona di Exchange Management Shell. Quando viene aperto Windows PowerShell, è possibile specificare manualmente l'obiettivo di connessione desiderato. Quando si crea una connessione manuale, viene specificato un account amministratore nell'organizzazione tenant Office 365, quindi viene eseguito un comando per creare la connessione. Una volta stabilità la connessione, i cmdlet di Exchange che si è autorizzati ad eseguire diventano disponibili per l'utente. Per ulteriori informazioni, vedere [Utilizzare Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=209660).

Se è la prima volta che si utilizza la Exchange Management Shell e sono necessarie informazioni di base sul funzionamento della Exchange Management Shell, la sintassi dei comandi e molto altro ancora, vedere [Utilizzo di PowerShell con Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/it-it/library/bb123778\(v=exchg.150\)).


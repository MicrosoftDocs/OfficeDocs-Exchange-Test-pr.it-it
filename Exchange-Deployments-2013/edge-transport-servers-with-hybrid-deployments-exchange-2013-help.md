---
title: 'Server Trasporto Edge con distribuzioni ibride: Exchange 2013 Help'
TOCTitle: Server Trasporto Edge con distribuzioni ibride
ms:assetid: 166b1490-5c56-40df-a17b-e8bb36224fd9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh134662(v=EXCHG.150)
ms:contentKeyID: 50482143
ms.date: 04/26/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Server Trasporto Edge con distribuzioni ibride

 

_<strong>Si applica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2018-04-16_

Il ruolo del server Trasporto Edge è un ruolo facoltativo che viene in genere distribuito in un computer che si trova nella rete perimetrale di un'organizzazione di Exchange ed è progettato per ridurre al minimo la superficie soggetta ad attacchi dell'organizzazione. Il ruolo server Trasporto Edge gestisce tutto il flusso di posta Internet che fornisce i servizi di inoltro SMTP e smart host per i server Exchange locali interni all'organizzazione.

## Il server Trasporto Edge nelle organizzazioni con distribuzione ibrida basate su Exchange

Le organizzazioni di Exchange 2016 che desiderano utilizzare i server Trasporto Edge, possono distribuire i server Trasporto Edge che eseguono la versione più recente di Exchange 2016 e versioni successive, Exchange 2013 o Exchange 2010. Utilizzare i server Trasporto Edge se non si desidera esporre i server Exchange interni direttamente a Internet. Quando si distribuisce un server Trasporto Edge in una distribuzione ibrida, Exchange Online, tramite il servizio Exchange Online Protection, consentirà di connettersi al server Trasporto Edge per recapitare i messaggi. Il server Trasporto Edge recapiterà quindi i messaggi al server Cassette postali di Exchange locale, dove si trova la cassetta postale del destinatario.


> [!IMPORTANT]
> Non inserire server, servizi o dispositivi, in grado di elaborare o modificare il traffico SMTP, tra i server Exchange locali e Office 365. Il flusso di posta sicura tra l'organizzazione di Exchange locale e Office 365 dipende dalle informazioni contenute nei messaggi inviati tra le organizzazioni. Sono supportati i firewall che consentano il traffico SMTP sulla porta TCP 25 senza alcuna modifica. Se un server, un servizio o un dispositivo elabora un messaggio inviato tra l'organizzazione di Exchange locale e Office 365, queste informazioni vengono rimosse. In questo caso, il messaggio non verrà più considerato interno all'organizzazione e sarà soggetto ai filtri di posta indesiderata, alle regole di trasporto e di journal e ad altri criteri che potrebbero non essere applicati.




> [!IMPORTANT]
> Se sono disponibili altri server Trasporto Edge di Exchange in altri percorsi che non devono gestire il trasporto ibrido, non è necessario effettuarne l'aggiornamento per supportare una distribuzione ibrida. Tuttavia, se in futuro EOP dovrà connettersi ad altri server Trasporto Edge per il trasporto ibrido, dovranno eseguire la versione più recente di Exchange 2016 e versioni successive, Exchange&nbsp;2010 o Exchange 2013.



## Aggiunta di un server Trasporto Edge a una distribuzione ibrida

Quando si configura una distribuzione ibrida, la distribuzione di un server Trasporto Edge nell'organizzazione locale è facoltativa. Quando si configura la distribuzione ibrida la procedura guidata di configurazione ibrida consente di selezionare uno o più server Exchange locali o di selezionare uno o più server Trasporto Edge locali per gestire il trasporto ibrido della posta con l'organizzazione di Exchange Online.

Quando si aggiunge un server Trasporto Edge alla distribuzione ibrida, tale server comunica con EOP per conto dei server Exchange interni. Il server Trasporto Edge agisce da inoltro tra i server Exchange interni ed EOP per i messaggi in uscita dall'organizzazione locale e indirizzati all'organizzazione di Exchange Online. Il server Trasporto Edge, inoltre, agisce da inoltro tra i server Exchange interni e l'organizzazione locale per i messaggi in entrata e provenienti dall'organizzazione di Exchange Online. Tutti gli aspetti della sicurezza delle connessioni che in precedenza venivano gestiti dai server Exchange interni vengono ora gestiti dal server Trasporto Edge. La ricerca dei destinatari, i criteri di conformità e altre ispezioni sui messaggi vengono ancora eseguiti nei server Exchange interni.

Se si aggiunge un server Trasporto Edge alla distribuzione ibrida, non è necessario instradare la posta elettronica inviata tra gli utenti locali e i destinatari di Internet utilizzando tale server. Soltanto i messaggi inviati tra l'ambiente locale e le organizzazioni di Exchange Online verranno instradati attraverso il server Trasporto Edge.

## Flusso di posta senza un server Trasporto Edge

Il processo e il diagramma riportati di seguito descrivono il percorso compiuto dai messaggi tra un'organizzazione locale ed Exchange Online quando non è disponibile un server Trasporto Edge:

1.  I messaggi in uscita provenienti dall'organizzazione locale e indirizzati ai destinatari nell'organizzazione di Exchange Online vengono inviati da una cassetta postale presente in un server Exchange interno.

2.  Il server Exchange invia il messaggio direttamente a Exchange Online Protection.

3.  EOP recapita il messaggio all'organizzazione di Exchange Online.

I messaggi inviati dall'organizzazione Exchange Online ai destinatari nell'organizzazione locale seguono il percorso inverso.

**Flusso di posta in una distribuzione ibrida senza un server Trasporto Edge distribuito**

![Flusso di posta ibrido senza un server Trasporto Edge](images/Hh134662.a95b4d1e-fd4a-4952-b891-22f84c9e71a3(EXCHG.150).png "Flusso di posta ibrido senza un server Trasporto Edge")

## Flusso di posta con un server Trasporto Edge

La seguente procedura consente di descrivere il percorso dei messaggi scambiati tra l'organizzazione locale ed Exchange Online, nel caso in cui sia stato distribuito un server Trasporto Edge. I messaggi dell'organizzazione locale diretti ai destinatari dell'organizzazione di Exchange Online vengono inviati dai server Exchange interni:

1.  I messaggi provenienti dall'organizzazione locale e indirizzati ai destinatari nell'organizzazione di Exchange Online vengono inviati da una cassetta postale presente in un server Exchange interno.

2.  Il server Exchange invia il messaggio a un server Trasporto Edge che esegue una versione supportata di Exchange.

3.  Il server Trasporto Edge invia il messaggio a EOP.

4.  EOP recapita il messaggio all'organizzazione di Exchange Online.

I messaggi inviati dall'organizzazione Exchange Online ai destinatari nell'organizzazione locale seguono il percorso inverso.

**Flusso di posta in una distribuzione ibrida in cui è stato distribuito un server Trasporto Edge**

![Flusso di posta ibrido con un server Trasporto Edge](images/Hh134662.821fe099-56f5-4501-8e1a-e184ba07a653(EXCHG.150).png "Flusso di posta ibrido con un server Trasporto Edge")


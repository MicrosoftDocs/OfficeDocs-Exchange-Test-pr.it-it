---
title: 'Server Trasporto Edge nelle distribuzioni ibride di Exchange 2013/Exchange 2010: Exchange 2013 Help'
TOCTitle: Server Trasporto Edge nelle distribuzioni ibride di Exchange 2013/Exchange 2010
ms:assetid: 924f895e-5987-48d0-b113-9d26dcbcdae0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn393965(v=EXCHG.150)
ms:contentKeyID: 59634762
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Server Trasporto Edge nelle distribuzioni ibride di Exchange 2013/Exchange 2010

Questo argomento è in fase di definizione.  

_**Si applica a:**Exchange Online, Exchange Server, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

I server Trasporto Edge in Microsoft Exchange vengono distribuiti nella rete perimetrale locale dell'organizzazione. Si tratta di computer non aggiunti al dominio che gestiscono il flusso di posta elettronica con connessione Internet e fungono da inoltro SMTP e smart host per i server Exchange nella rete interna.

Le organizzazioni Exchange 2013 che desiderano utilizzare i server Trasporto Edge hanno la possibilità di distribuire i server Trasporto Edge di Exchange Server 2013 o Exchange 2010 eseguendo il Service Pack 3 (SP3) per Exchange 2010. Utilizzare i server Trasporto Edge se non si desidera esporre i server interni Accesso client o Cassette postali di Exchange 2013 direttamente a Internet.

Per ulteriori informazioni sul server Trasporto Edge di Exchange 2013, vedere [Server Trasporto Edge](https://technet.microsoft.com/it-it/library/bb124701\(v=exchg.150\)).

Per ulteriori informazioni sul ruolo del server Trasporto Edge di Exchange 2010, vedere [Panoramica sul ruolo del server Trasporto Edge](http://go.microsoft.com/fwlink/p/?linkid=183473).

## Server Trasporto Edge in Exchange 2013 in organizzazioni con distribuzione ibrida di Exchange 2013

I messaggi instradati tra le organizzazioni locali e di Exchange Online in una distribuzione ibrida richiedono che il servizio Microsoft Exchange Online Protection (EOP) si connetta direttamente ai server Trasporto Edge dotati di Exchange 2013 o Exchange 2010 SP3 per conto di Exchange Online.


> [!IMPORTANT]
> Se sono disponibili altri server Trasporto Edge di Exchange&nbsp;2010 in altri percorsi che non devono gestire il trasporto ibrido, non è necessario effettuarne l'aggiornamento a Exchange&nbsp;2010 SP3. Tuttavia, se in futuro EOP dovrà connettersi ad altri server Trasporto Edge per il trasporto ibrido, sarà necessario aggiornarli con Exchange&nbsp;2010 SP3 o a server Trasporto Edge di Exchange 2013.



## Aggiunta di un server Trasporto Edge a una distribuzione ibrida

Quando si configura una distribuzione ibrida, la distribuzione di un server Trasporto Edge nell'organizzazione locale è facoltativa. Quando si configura la distribuzione ibrida la procedura guidata di configurazione ibrida consente di selezionare uno o più server Accesso client e Cassette postali per il trasporto ibrido della posta, o di selezionare uno o più server Trasporto Edge locali per gestire il trasporto ibrido della posta con l'organizzazione di Exchange Online.

Quando si aggiunge un server Trasporto Edge alla distribuzione ibrida, tale server comunica con EOP per conto dei server Accesso client interni e sei server Cassette postali di Exchange 2013. Il server Trasporto Edge agisce da server di inoltro fra il server Cassette postali locale ed EOP per i messaggi in uscita dall'organizzazione locale e indirizzati all'organizzazione di Exchange Online. Il server Trasporto Edge agisce da server di inoltro anche fra il server Accesso client locale e l'organizzazione locale per i messaggi in entrata dall'organizzazione di Exchange Online. Tutti gli aspetti della sicurezza delle connessioni che in precedenza venivano gestiti dal server Accesso client vengono ora gestiti dal server Trasporto Edge. La ricerca dei destinatari, i criteri di conformità e altre ispezioni sui messaggi vengono ancora eseguiti nei server Accesso client.

## Flusso di posta senza un server Trasporto Edge

Il processo e il diagramma riportati di seguito descrivono il percorso compiuto dai messaggi tra un'organizzazione locale ed Exchange Online quando non è disponibile un server Trasporto Edge:

1.  I messaggi in uscita dall'organizzazione locale ai destinatari nell'organizzazione di Exchange Online vengono inviati da una cassetta postale del server Cassette postali di Exchange 2010 a un server Trasporto Hub di Exchange 2010.

2.  Il server Trasporto Hub di Exchange 2010 invia il messaggio al server Cassette postali di Exchange 2013.

3.  Il server Cassette postali di Exchange 2013 invia il messaggio direttamente alla società Exchange Online EOP.

4.  EOP recapita il messaggio all'organizzazione di Exchange Online. In questo esempio, i ruoli Accesso client e Cassette postali sono installati sullo stesso server Exchange 2013.

I messaggi inviati dall'organizzazione Exchange Online ai destinatari nell'organizzazione locale seguono il percorso inverso.

**Flusso di posta in una distribuzione ibrida senza un server Trasporto Edge distribuito**

![Organizzazioni locali senza server Trasporto Edge](images/Dn393965.37bbe430-b157-4f52-83da-6d44f4459425(EXCHG.150).png "Organizzazioni locali senza server Trasporto Edge")

## Flusso di posta con un server Trasporto Edge

Il seguente processo illustra il percorso seguito dai messaggi tra l'organizzazione locale e l'organizzazione di Exchange Online quando è disponibile un server Trasporto Edge. I messaggi dall'organizzazione locale indirizzati ai destinatari nell'organizzazione di Exchange Online vengono inviati dal server Cassette postali di Exchange 2010:

1.  I messaggi in uscita dall'organizzazione locale ai destinatari nell'organizzazione di Exchange Online vengono inviati da una cassetta postale del server Cassette postali di Exchange 2010 a un server Trasporto Hub di Exchange 2010.

2.  Il server Trasporto Hub di Exchange 2010 invia il messaggio al server Cassette postali di Exchange 2013.

3.  Il server Cassette postali di Exchange 2013 invia il messaggio a un server Trasporto Edge di Exchange 2013 o Exchange 2010 SP3.

4.  Il server Trasporto Edge invia il messaggio all'azienda EOP di Exchange Online.

5.  EOP recapita il messaggio all'organizzazione di Exchange Online. In questo esempio, i ruoli Accesso client e Cassette postali sono installati sullo stesso server Exchange 2013.

I messaggi inviati dall'organizzazione Exchange Online ai destinatari nell'organizzazione locale seguono il percorso inverso.

**Flusso di posta in una distribuzione ibrida con un server Trasporto Edge di Exchange 2013 o 2010 SP3**

![Organizzazioni locali con server Trasporto Edge](images/Dn393965.f1039133-249b-401d-bd39-3672442a06c9(EXCHG.150).png "Organizzazioni locali con server Trasporto Edge")


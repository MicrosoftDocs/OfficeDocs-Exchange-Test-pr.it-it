---
title: 'Server Trasporto Edge nelle distribuzioni ibride di Exchange 2013/Exchange 2007: Exchange 2013 Help'
TOCTitle: Server Trasporto Edge nelle distribuzioni ibride di Exchange 2013/Exchange 2007
ms:assetid: 4e4d7c19-78b8-44bb-bdff-3ea97ea59a5d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn151300(v=EXCHG.150)
ms:contentKeyID: 54651640
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Server Trasporto Edge nelle distribuzioni ibride di Exchange 2013/Exchange 2007

Questo argomento è in fase di definizione.  

_<strong>Si applica a:</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>Ultima modifica dell'argomento:</strong>2016-12-09_

I server Trasporto Edge di Microsoft Exchange vengono distribuiti nella rete perimetrale locale dell'organizzazione. Sono computer non aggiunti al dominio che gestiscono il flusso di posta elettronica con connessione Internet e fungono da inoltro SMTP e smart host per i server Exchange nella rete interna.

Le organizzazioni Exchange 2013 che desiderano utilizzare i server Trasporto Edge hanno la possibilità di distribuire i server Trasporto Edge di Exchange Server 2013 o Exchange 2010 eseguendo il Service Pack 3 (SP3) per Exchange 2010. Utilizzare i server Trasporto Edge se non si desidera esporre i server interni Accesso client o Cassette postali di Exchange 2013 direttamente a Internet.

Per ulteriori informazioni sul Exchange 2013 ruolo server Trasporto Edge, consultare [Server Trasporto Edge](https://technet.microsoft.com/it-it/library/bb124701\(v=exchg.150\)).

Per ulteriori informazioni sul ruolo del server Trasporto Edge di Exchange 2010, vedere [Panoramica sul ruolo del server Trasporto Edge](http://go.microsoft.com/fwlink/p/?linkid=183473).

## Server Trasporto Edge di Exchange 2013 in organizzazioni di Exchange 2013 basate su distribuzione ibrida

I messaggi instradati fra l'organizzazione locale e l'organizzazione di Exchange Online in una distribuzione ibrida richiedono che il servizio Microsoft Exchange Online Protection (EOP) si connetta direttamente ai server Trasporto Edge dotati di Exchange 2013 o Exchange 2010 SP3 per conto di Exchange Online.


> [!IMPORTANT]
> Se sono disponibili altri server Trasporto Edge di Exchange&nbsp;2010 in posizioni diverse, che non devono gestire il trasporto ibrido, non è necessario effettuarne l'aggiornamento a Exchange&nbsp;2010 SP3. Se in futuro EOP dovrà connettersi ad altri server Trasporto Edge per il trasporto ibrido, sarà necessario aggiornarli a Exchange&nbsp;2010 SP3 oppure ai server Trasporto Edge di Exchange 2013.



## Aggiunta di un server Trasporto Edge a una distribuzione ibrida

Quando si configura una distribuzione ibrida, la distribuzione di un server Trasporto Edge nell'organizzazione locale è facoltativa. Quando si configura la distribuzione ibrida la procedura guidata di configurazione ibrida consente di selezionare uno o più server Accesso client e Cassette postali per il trasporto ibrido della posta, o di selezionare uno o più server Trasporto Edge locali per gestire il trasporto ibrido della posta con l'organizzazione di Exchange Online.

Quando si aggiunge un server Trasporto Edge alla distribuzione ibrida, tale server comunica con EOP per conto dei server Accesso client interni e sei server Cassette postali di Exchange 2013. Il server Trasporto Edge agisce da server di inoltro fra il server Cassette postali locale ed EOP per i messaggi in uscita dall'organizzazione locale e indirizzati all'organizzazione di Exchange Online. Il server Trasporto Edge agisce da server di inoltro anche fra il server Accesso client locale e l'organizzazione locale per i messaggi in entrata dall'organizzazione di Exchange Online. Tutti gli aspetti della sicurezza delle connessioni che in precedenza venivano gestiti dal server Accesso client vengono ora gestiti dal server Trasporto Edge. La ricerca dei destinatari, i criteri di conformità e altre ispezioni sui messaggi vengono ancora eseguiti nei server Accesso client.

## Flusso di posta senza un server Trasporto Edge

Il processo e il diagramma riportati di seguito descrivono il percorso compiuto dai messaggi tra un'organizzazione locale ed Exchange Online quando non è disponibile un server Trasporto Edge:

1.  I messaggi in uscita dall'organizzazione locale ai destinatari nell'organizzazione di Exchange Online vengono inviati da una cassetta postale del server Cassette postali di Exchange 2007 a un server Trasporto Hub.

2.  Il server Trasporto Hub di Exchange 2007 invia il messaggio al server Cassette postali di Exchange 2013.

3.  Il server Cassette postali di Exchange 2013 invia il messaggio direttamente alla società Exchange Online EOP.

4.  EOP recapita il messaggio all'organizzazione di Exchange Online. In questo esempio, i ruoli Accesso client e Cassette postali sono installati sullo stesso server Exchange 2013.

I messaggi inviati dall'organizzazione Exchange Online ai destinatari nell'organizzazione locale seguono il percorso inverso.

**Flusso di posta in una distribuzione ibrida senza un server Trasporto Edge distribuito**

![Organizzazione locale senza server Edge](images/Dn151300.e7206c51-b61c-41e3-a446-9270f131fbaa(EXCHG.150).png "Organizzazione locale senza server Edge")

## Flusso di posta con un server Trasporto Edge

Il seguente processo illustra il percorso seguito dai messaggi tra l'organizzazione locale e l'organizzazione di Exchange Online quando è disponibile un server Trasporto Edge. I messaggi dall'organizzazione locale indirizzati ai destinatari nell'organizzazione di Exchange Online vengono inviati dal server Cassette postali di Exchange 2007:

1.  I messaggi in uscita dall'organizzazione locale ai destinatari nell'organizzazione di Exchange Online vengono inviati da una cassetta postale del server Cassette postali di Exchange 2007 a un server Trasporto Hub.

2.  Il server Trasporto Hub di Exchange 2007 invia il messaggio al server Cassette postali di Exchange 2013.

3.  Il server Cassette postali di Exchange 2013 invia il messaggio a un server Trasporto Edge di Exchange 2013 o Exchange 2010 SP3.

4.  Il server Trasporto Edge invia il messaggio all'organizzazione di Exchange Online EOP.

5.  EOP recapita il messaggio all'organizzazione di Exchange Online. In questo esempio, i ruoli Accesso client e Cassette postali sono installati sullo stesso server Exchange 2013.

I messaggi inviati dall'organizzazione Exchange Online ai destinatari nell'organizzazione locale seguono il percorso inverso.

**Flusso di posta in una distribuzione ibrida con un server Trasporto Edge di Exchange 2013 o 2010 SP3**

![Organizzazione locale con server Edge](images/Dn151300.91bf5390-c4d7-4aa9-b911-0c1c559d4365(EXCHG.150).png "Organizzazione locale con server Edge")


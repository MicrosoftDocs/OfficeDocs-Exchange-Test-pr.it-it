---
title: 'Agenti di recapito e connettori agente di recapito: Exchange 2013 Help'
TOCTitle: Agenti di recapito e connettori agente di recapito
ms:assetid: 38c942ee-b59d-47ec-87eb-bebad441ada5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638118(v=EXCHG.150)
ms:contentKeyID: 50480358
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agenti di recapito e connettori agente di recapito

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Un agente di recapito può recapitare i messaggi dall'ambiente SMTP di Exchange Server a un sistema che non utilizza il protocollo SMTP. Ciascun agente di recapito è associato a un connettore Agente di recapito che accoda i messaggi instradati all'agente di recapito affinché possano essere elaborati e recapitati al dispositivo o sistema non SMTP.


> [!TIP]
> Mentre l'architettura dei connettori esterni rimane in Microsoft Exchange 2013, si consiglia l'utilizzo degli agenti di recapito per il routing dei messaggi ai sistemi non SMTP quando possibile. Il motivo principale di questa scelta è rappresentato dalla possibilità di utilizzare la gestione delle code per i messaggi, di verificare il recapito dei messaggi e di evitare la gestione del trasferimento dei file a una directory di destinazione.



**Sommario**

Function and benefits of Delivery Agents

Adding Delivery Agents to your organization

Delivery Agent connectors

Default text messaging Delivery Agent connector

## Funzione e vantaggi degli agenti di consegna

Un agente di gestione è un componente installato nel servizio di trasporto di un server Cassette postali che può effettuare le seguenti attività:

  - Stabilire una connessione con il sistema esterno per il recapito dei messaggi.

  - Recuperare i messaggi dalle code di recapito sui server Cassette postali.

  - Recapitare i messaggi al sistema esterno.

  - Confermare il corretto recapito di ogni messaggio.

Mentre l'architettura dei connettori esterni rimane in Microsoft Exchange Server 2013, si consiglia l'utilizzo degli agenti di recapito per il routing dei messaggi ai sistemi non SMTP quando possibile. Gli agenti di recapito offrono i seguenti vantaggi:

  - Consentono di gestire le code dei messaggi instradati a sistemi esterni.

  - Siccome i messaggi non devono più essere scritti e letti dal file system, le prestazioni di recapito dei messaggi sono migliorate.

  - Forniscono l'accesso alle proprietà dei messaggi con gli eventi completi per gli sviluppatori degli agenti.

  - I tempi di sviluppo per un agente di recapito sono più veloci rispetto all'implementazione di un connettore esterno, in quanto l'agente di recapito può utilizzare la rappresentazione dei messaggi e le funzionalità di gestione di Exchange.

  - È possibile verificare che i messaggi vengano recapitati a un sistema esterno, invece che semplicemente scritti nella directory di destinazione.

  - L'utilizzo dei connettori Agente di recapito consente l'analisi del contratto di servizio, in quanto è possibile tenere traccia della latenza di recapito dei messaggi al sistema esterno.

## Aggiunta degli agenti di recapito all'organizzazione

Per utilizzare un agente di recapito nell'organizzazione, è necessario completare le seguenti operazioni:

1.  Acquisire l'agente di recapito. In genere, gli agenti di recapito vengono scritti da terze parti. Per impostazione predefinita, Exchange 2013 viene fornito con un solo connettore Agente di recapito: il connettore Agente di recapito di messaggistica di testo.

2.  Installare l'agente di recapito nel servizio di trasporto dei server Cassette postali che fungerà da server di origine per i connettori Agente di recapito.

3.  Creare un connettore Agente di recapito per il protocollo specifico.

Una volta completata questa procedura, i messaggi ai sistemi esterni verranno instradati attraverso i connettori Agente di recapito ed elaborati dall'agente di recapito.

[Spazio dei nomi vedere](https://go.microsoft.com/fwlink/?linkid=262690) vengono fornite ulteriori informazioni sullo sviluppo di un agente di recapito.

## Connettori Agente di recapito

Un connettore Agente di recapito in Exchange 2013 è simile al connettore Agente di recapito introdotto in Exchange 2010. Instradano i messaggi indirizzati a sistemi esterni che non utilizzano il protocollo SMTP. Quando un messaggio viene instradato a un connettore Agente di recapito, l'agente di recapito associato esegue la conversione del contenuto e il recapito del messaggio. Generalmente, gli agenti di recapito vengono creati da terzi e configurati in modo da essere compatibili con un connettore Agente di recapito nell'organizzazione dell'utente.

Impossibile creare un connettore Agente di recapito nell'interfaccia di amministrazione di Exchange. Piuttosto, creare un connettore Agente di recapito in Exchange Management Shell con il cmdlet [New-DeliveryAgentConnector](https://technet.microsoft.com/it-it/library/dd351063\(v=exchg.150\)) e modificare le proprietà del connettore con [Set-DeliveryAgentConnector](https://technet.microsoft.com/it-it/library/dd351159\(v=exchg.150\)). È possibile specificare uno o più server Cassette postali host per il connettore utilizzando il parametro *SourceTransportServers* facoltativo.

## Il connettore Agente di recapito SMS predefinito

È possibile utilizzare il connettore Agente di recapito SMS per instradare i messaggi ai dispositivi mobili. Sul server Exchange, eseguire `Get-DeliveryAgentConnector | fl` per visualizzare il connettore e i relativi parametri. Notare che *DeliveryProtocol* è impostato su `MOBILE`.


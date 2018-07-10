---
title: 'Domini: Exchange 2013 Help'
TOCTitle: Domini
ms:assetid: 11748c2d-2e32-43a4-b77d-e0c17db6200b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673041(v=EXCHG.150)
ms:contentKeyID: 50480020
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Domini

 

_**Si applica a:** Exchange Server 2013, Office 365_

_**Ultima modifica dell'argomento:** 2012-10-11_

I domini rappresentano gli spazi dei nomi SMTP per cui sono configurate le cassette postali e le directory di posta elettronica. Configurando i domini che interagiscono con l'organizzazione Microsoft Exchange Server 2013, è possibile configurare in che modo Exchange deve elaborare la posta elettronica ricevuta e inviata da diversi domini.

## Domini accettati

Un dominio accettato è rappresentato da un qualsiasi spazio di nomi SMTP per conto del quale un'organizzazione Exchange invia o riceve la posta elettronica. I domini accettati includono quelli per cui l'organizzazione Exchange è autorevole, così come i domini di inoltro interni ed esterni. Un'organizzazione di Exchange è autorevole quando gestisce il recapito della posta elettronica per i destinatari nel dominio accettato. I domini accettati includono anche quelli per cui l'organizzazione Exchange riceve la posta e la inoltra a un server di posta elettronica esterno all'organizzazione.

Per ulteriori informazioni sui domini accettati, vedere [Domini accettati](accepted-domains-exchange-2013-help.md).

## Domini remoti

In Exchange 2013, è possibile creare voci dei domini remoti per definire le impostazioni per il trasferimento dei messaggi tra l'organizzazione Exchange e i domini all'esterno dell'organizzazione. Quando si crea una voce del dominio remoto, è possibile controllare i tipi di messaggi inviati al dominio. È inoltre possibile applicare criteri di formato dei messaggi e set di caratteri accettabili per messaggi inviati da utenti nella propria organizzazione al dominio remoto.

Per i domini remoti vengono utilizzate impostazioni di configurazione globali per l'organizzazione Exchange. Le impostazioni del dominio remoto vengono applicate ai messaggi durante la categorizzazione. Quando si verifica la risoluzione dei destinatari, il dominio destinatari viene confrontato ai domini remoti configurati. Se una configurazione del dominio remoto impedisce l'invio di un tipo specifico di messaggi ai destinatari del dominio, il messaggio viene eliminato. Se si specifica un particolare formato dei messaggi per il dominio remoto, il contenuto e le intestazioni dei messaggi vengono modificati. Le impostazioni vengono applicate a tutti i messaggi elaborati dall'organizzazione Exchange.

Per ulteriori informazioni sui domini remoti, vedere [Domini remoti](remote-domains-exchange-2013-help.md).


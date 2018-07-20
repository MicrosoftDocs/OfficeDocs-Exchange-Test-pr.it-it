---
title: 'Server Trasporto Edge: Exchange 2013 Help'
TOCTitle: Server Trasporto Edge
ms:assetid: cfff9f59-afac-447c-8297-afcebe49a52d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124701(v=EXCHG.150)
ms:contentKeyID: 61183413
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Server Trasporto Edge

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-09-29_

Server Trasporto Edge di ridurre al minimo la superficie di attacco gestendo il flusso di posta con connessione Internet, che fornisce servizi smart host per l'organizzazione Exchange e inoltro SMTP (Simple Mail Transfer Protocol). Gli agenti in esecuzione nel server Trasporto Edge forniscono ulteriori livelli di sicurezza e la protezione dei messaggi. Questi agenti forniscono una protezione contro la posta indesiderata e applicano le regole di trasporto per il controllo del flusso della posta.

Dal momento che il server Trasporto Edge è installato nella rete perimetrale, non rappresenta mai un membro della foresta Active Directory interna dell'organizzazione e non dispone di accesso alle informazioni di Active Directory. Tuttavia, il server Trasporto Edge necessita dei dati che risiedono in Active Directory, ad esempio le informazioni del connettore per il flusso di posta e le informazioni sul destinatario per le attività di protezione da posta indesiderata o di ricerca del destinatario. Tali dati vengono sincronizzati con il server Trasporto Edge dal servizio Microsoft Exchange EdgeSync. EdgeSync consiste una raccolta di processi eseguiti su un server di cassetta postale di Exchange 2013 al fine di stabilire una replica monodirezionale del destinatario e le informazioni di configurazione da Active Directory all'istanza AD LDS nel server Trasporto Edge. EdgeSync consente di copiare soltanto le informazioni necessarie al server Trasporto Edge per eseguire attività di configurazione di protezione da posta indesiderata e per abilitare il flusso di posta end-to-end. EdgeSync esegue gli aggiornamenti pianificati così da mantenere aggiornate le informazioni contenute in AD LDS.

È possibile installare più server Edge Transport nella rete perimetrale. La distribuzione di più server Trasporto Edge mette a disposizione la ridondanza e le capacità di failover per il flusso di messaggi in entrata. È possibile bilanciare il carico del traffico SMTP dell'organizzazione tra i server Trasporto Edge definendo più di un record MX con lo stesso valore di priorità del dominio di posta. È possibile ottenere una configurazione coerente tra più server Edge Transport utilizzando script di configurazione clonati.

Il ruolo del server Trasporto Edge consente all'utente di gestire le seguenti situazioni relative all'elaborazione dei messaggi.

## flusso della posta Internet

I server Trasporto Edge accettano provenienti da Internet nell'organizzazione Exchange. Al termine dell'elaborazione dei messaggi da parte del server Trasporto Edge, la destinazione del successivo instradamento dipende dalla configurazione dei server Exchange interni:

  - Se il server Accesso client e il server di cassetta postale sono installate su computer diversi, la posta viene instrada al servizio di trasporto sul server di cassetta postale. Il server Accesso client viene ignorato per il flusso di posta SMTP in uscita.

  - Se il server Accesso client e il server di cassetta postale sono installati sullo stesso computer, la posta viene instradata al servizio Trasporto Front End sul server Accesso client, quindi sul servizio Trasporto nel server di cassetta postale.

Tutti i messaggi inviati a Internet dall'organizzazione vengono instradati ai server Trasporto Edge dopo che i messaggi sono stati elaborati dal servizio Trasporto sul server di cassetta postale. È possibile configurare il server Trasporto Edge per utilizzare il DNS per la risoluzione dei record di risorse MX per i domini SMTP esterni oppure per l'inoltro dei messaggi a uno SmartHost per la risoluzione del DNS.

## Protezione dalla posta indesiderata

In Exchange 2013, le funzionalità di protezione da posta indesiderate forniscono servizi per bloccare posta commerciale indesiderata (spam) nella rete perimetrale.

Gli spammer ricorrono a diverse tecniche per inviare posta indesiderata all'organizzazione. I server Trasporto Edge consentono di evitare che gli utenti ricevano posta indesiderata grazie a una serie di agenti che interagiscono per offrire livelli diversi di protezione e filtro della posta indesiderata: Stabilire intervalli di tarpitting sui connettori rende inefficaci i tentativi di attacco della posta elettronica.

## Regole di trasporto Edge

Le regole di trasporto Edge vengono utilizzate per controllare il flusso dei messaggi inviati a o ricevuti da Internet. Le regole di trasporto Edge vengono configurate su ogni server Trasporto Edge per proteggere le risorse di rete aziendali e i dati, applicando un'azione ai messaggi che soddisfano determinate condizioni. Le condizioni delle regole di trasporto Edge si basano sui dati, ad esempio su parole specifiche o modelli di testo nell'oggetto, nel corpo o nell'intestazione del messaggio, sull'indirizzo nel campo Da, sul livello di probabilità di posta indesiderata o sul tipo di allegato. Le azioni determinano il modo in cui il messaggio viene elaborato quando si realizza una determinata condizione. Le possibili azioni includono la messa in quarantena di un messaggio, l'eliminazione o il rifiuto del messaggio, l'aggiunta di ulteriori destinatari o la registrazione di un evento. Eccezioni facoltative possono impedire che un'azione venga applicata a determinati messaggi.

## Riscrittura degli indirizzi

La riscrittura degli indirizzi consente di presentare un aspetto uniforme dell'indirizzo di posta elettronica ai destinatari esterni. È possibile configurare la riscrittura degli indirizzi sui server Trasporto Edge al fine di modificare gli indirizzi SMTP nei messaggi in ingresso e in uscita. La riscrittura degli indirizzi è utile soprattutto per le organizzazioni appena fuse che desiderano presentare un aspetto uniforme dell'indirizzo di posta elettronica.

Per ulteriori informazioni sulla riscrittura degli indirizzi, vedere [Indirizzo riscrittura su server Trasporto Edge](address-rewriting-on-edge-transport-servers-exchange-2013-help.md).


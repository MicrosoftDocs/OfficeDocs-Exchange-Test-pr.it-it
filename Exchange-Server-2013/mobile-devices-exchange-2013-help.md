---
title: 'Dispositivi mobili: Exchange 2013 Help'
TOCTitle: Dispositivi mobili
ms:assetid: 93a949e7-b3ef-43ea-ae0c-6698826fc8d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232129(v=EXCHG.150)
ms:contentKeyID: 50481194
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Dispositivi mobili

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-09-24_

I dispositivi mobili abilitati per MicrosoftExchange ActiveSync consentono agli utenti di accedere alla maggior parte dei dati delle cassette postali di Microsoft Exchange in qualsiasi momento e in qualsiasi luogo. Esistono molti telefoni cellulari e dispositivi mobili diversi abilitati per Exchange ActiveSync. Sono compresi i dispositivi Windows Phone, i telefoni cellulari Nokia, i cellulari e i tablet Android e i prodotti Apple iPhone, iPod e iPad.

Nonostante Exchange ActiveSync sia supportato sia dai telefoni cellulari che da altri dispositivi mobili, nella maggior parte della documentazione di Exchange ActiveSync viene utilizzato il termine *dispositivo mobile*. A meno che le funzionalità trattate richiedano un segnale del telefono cellulare, ad esempio una notifica di un SMS, con il termine dispositivo mobile si fa riferimento sia ai telefoni cellulari sia ad altri dispositivi mobili quali i tablet.

## Exchange ActiveSync

Exchange ActiveSync è un protocollo per le comunicazioni che consente l'accesso da un dispositivo mobile wireless ai messaggi di posta elettronica, ai dati di pianificazione, ai contatti e alle attività. Exchange ActiveSync è disponibile sugli smartphone Windows e di terze parti abilitati per Exchange ActiveSync.

Exchange ActiveSync offre la tecnologia Direct Push. Direct Push utilizza una connessione HTTPS crittografata stabilita e gestita tra il dispositivo mobile e il server per inviare nuovi messaggi di posta elettronica e altri dati di Exchange allo smartphone.

Per utilizzare Direct Push con MicrosoftExchange Server 2013, gli utenti devono disporre di un dispositivo mobile progettato per supportare Direct Push.

## Funzionalità di Exchange ActiveSync

Exchange ActiveSync consente l'accesso a molte funzionalità diverse che consentono di applicare criteri di sicurezza ai dispositivi mobili. Utilizzando Exchange 2013, è possibile configurare più criteri cassette postali del dispositivo mobile e controllare quali dispositivi mobili sono in grado di eseguire la sincronizzazione con il server di Exchange. Exchange ActiveSync consente di inviare un comando di cancellazione remota dati nel dispositivo in modo da cancellare tutti i dati da un dispositivo mobile in caso di smarrimento o furto. La cancellazione remota dati nel dispositivo può anche essere avviata da Outlook Web App.

Exchange ActiveSync consente agli utenti di generare una password di ripristino. La password di ripristino viene salvata sul dispositivo mobile e viene utilizzata quando gli utenti dimenticano la loro password. Gli utenti creano la password di ripristino nello stesso momento in cui creano la password del dispositivo o il PIN. La password di ripristino può essere utilizzata per sbloccare il dispositivo mobile. Subito dopo aver utilizzato la password di ripristino, all'utente verrà richiesto di creare un nuovo PIN.

## POP3 e IMAP4

Se il dispositivo mobile non supporta Exchange ActiveSync o se non si necessita dell'ampio set di funzionalità fornito da Exchange ActiveSync, è possibile utilizzare POP3 o IMAP4 per accedere alla posta elettronica sul dispositivo mobile. Per ulteriori informazioni sull'accesso POP3 e IMAP4 alla cassetta postale, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).


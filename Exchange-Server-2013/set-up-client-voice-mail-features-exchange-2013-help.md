---
title: 'Installazione delle funzionalità di posta vocale del client: Exchange 2013 Help'
TOCTitle: Installazione delle funzionalità di posta vocale del client
ms:assetid: 5e661cfd-d34e-4caa-91a5-967bbecb75eb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673529(v=EXCHG.150)
ms:contentKeyID: 50555601
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Installazione delle funzionalità di posta vocale del client

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-20_

In questo argomento sono descritte le funzionalità che permettono agli utenti abilitati alla messaggistica unificata di Exchange di accedere ai messaggi di posta e vocali presenti nella loro cassetta postale. Tramite queste funzionalità, gli utenti possono accedere facilmente ai loro messaggi di posta e vocali e migliorare di conseguenza il loro utilizzo del prodotto.

**Sommario**

Voice mail client support

Outlook Voice Access

Forwarding calls

Voice Mail Preview

Receiving faxes

## Supporto dei client per la posta vocale

**Client Exchange ActiveSync**   Il protocollo di Microsoft Exchange ActiveSync viene utilizzato per connettere i client mobili, quali quelli presenti nei dispositivi mobili con funzionalità Internet, a una cassetta postale di Exchange. Gli utenti possono utilizzare i dispositivi mobili per accedere alla loro cassetta postale e visualizzare i messaggi di posta elettronica, ascoltare i messaggi vocali, visualizzare e modificare le voci di calendario e le informazioni di contatto. Possono inoltre sincronizzare la posta, la posta vocale, le voci di calendario e le informazioni di contatto con altri dispositivi.

**Integrazione con Outlook**   Microsoft Outlook consente agli utenti di accedere alla loro cassetta postale e visualizzare i messaggi di posta elettronica nella cartella Posta in arrivo, di visualizzare e modificare le informazioni di calendario, di ascoltare i messaggi vocali usando Microsoft Windows Media Player, incorporato nei messaggi di posta elettronica. Grazie all'uso del client di posta elettronica supportato, gli utenti potranno usufruire di funzionalità aggiuntive, come la funzionalità Ascolta al telefono.

**Integrazione Outlook Web App**   Microsoft Outlook Web App fornisce agli utenti un set di strumenti e interfacce di messaggistica unificata molto simile a un client di posta elettronica completo come Outlook. Grazie a Outlook Web App, gli utenti possono accedere alla loro cassetta postale di Exchange utilizzando un browser compatibile. Proprio come Outlook, anche Outlook Web App fornisce Windows Media Player incorporato nei messaggi di posta elettronica e ciò permette agli utenti di ascoltare i messaggi vocali e accedere a funzionalità quali Ascolta al telefono.

## Outlook Voice Access

Nella messaggistica unificata di Exchange, un utente abilitato alla messaggistica unificata può eseguire una chiamata a un numero telefonico interno o esterno configurato su un dial plan di messaggistica unificata per accedere alla sua cassetta postale e utilizzare il sistema di menu disponibile in Outlook Voice Access. Utilizzando questo menu, gli utenti abilitati alla messaggistica unificata possono leggere i messaggi di posta elettronica, ascoltare i messaggi vocali, interagire con il loro calendario di Outlook, accedere ai contatti personali ed eseguire attività quali la configurazione del PIN di Outlook Voice Access o la registrazione dei messaggi di saluto. Per ulteriori informazioni, vedere [Configurazione di Outlook Voice Access](setting-up-outlook-voice-access-exchange-2013-help.md).

## Inoltro delle chiamate

Un utente abilitato alla messaggistica unificata può creare e configurare delle regole di ricezione chiamata utilizzando Outlook o Outlook Web App. Tramite queste regole, gli utenti possono stabilire come gestire le loro chiamate in ingresso. Queste regole vengono applicate alle chiamate in ingresso in modo simile a come le regole di Posta in arrivo vengono applicate ai messaggi in ingresso e vengono archiviate insieme alle altre impostazioni vocali nella cassetta postale dell'utente. È possibile configurare nove regole di ricezione chiamata per ciascuna cassetta postale. Queste regole sono indipendenti dalle regole di Posta in arrivo e non vengono considerate nel calcolo della quota delle regole di Posta in arrivo. Per ulteriori informazioni, vedere [Consentire agli utenti di posta elettronica di inoltrare le chiamate vocali](allow-voice-mail-users-to-forward-calls-exchange-2013-help.md).

## Anteprima casella vocale

Anteprima messaggio vocale è una funzionalità disponibile per gli utenti che ricevono i messaggi vocali tramite un sistema di messaggistica unificata. Anteprima messaggio vocale migliora le funzionalità esistenti della casella vocale di messaggistica unificata offrendo una versione di testo delle registrazioni audio. Per ulteriori informazioni, vedere [Consentire agli utenti di visualizzare una trascrizione di posta vocale](allow-users-to-see-a-voice-mail-transcript-exchange-2013-help.md).

## Ricezione dei fax

La messaggistica unificata consente di inoltrare le chiamate fax in ingresso a una soluzione partner fax dedicata che stabilisce la connessione con il mittente e riceve il fax per conto dell'utente abilitato alla messaggistica unificata. Prima che l'utente abilitato alla messaggistica unificata possa ricevere i messaggi fax nella sua cassetta postale, è necessario fare quanto segue:

  - Abilitare la ricezione fax in ingresso sul dial plan di messaggistica unificata collegato agli utenti impostando il parametro *FaxEnabled* su `$true`.

  - Abilitare la ricezione fax in ingresso sul dial plan di messaggistica unificata collegato agli utenti impostando il parametro *Allowfax* su `$true`.

  - Abilitare la ricezione fax in ingresso per gli utenti impostando il parametro *FaxEnabled* su `$true`.

  - Impostare l'URI del server fax del partner in modo che consenta la ricezione fax in ingresso.

  - Configurare l'autenticazione tra il server Cassette postali e il server partner fax.


---
title: 'Analizzatore connettività remota di Exchange: Exchange 2013 Help'
TOCTitle: Analizzatore connettività remota di Exchange
ms:assetid: dd26698e-d00c-47f5-a7aa-c3894fe86c75
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff701693(v=EXCHG.150)
ms:contentKeyID: 50481839
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Analizzatore connettività remota di Exchange

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-09-22_

L'MicrosoftExchange Analizzatore connettività remota (ExRCA) consente di assicurarsi che la connettività dei server Exchange sia configurata correttamente. In caso di problemi, inoltre, aiuta a rilevare e correggere questi problemi. Il sito Web ExRCA consente di eseguire test per verificare Servizi Web MicrosoftExchange ActiveSync, Exchange, MicrosoftOutlook e connettività di posta elettronica Internet.

## Test disponibili in Analizzatore connettività remota

È possibile eseguire diversi test con ExRCA. I seguenti test funzionano su Exchange 2007 e versioni successive:

  - Exchange ActiveSync

  - Servizi Web di Exchange

  - Outlook

  - Posta elettronica Internet

## Test per Exchange ActiveSync

È possibile eseguire i seguenti test per Exchange ActiveSync:

  - **Exchange ActiveSync:** questo test simula la procedura utilizzata da un dispositivo mobile per connettersi a un server Exchange tramite Exchange ActiveSync.

  - **Individuazione automatica di Exchange ActiveSync:** illustra i passaggi utilizzati dai dispositivi Exchange ActiveSync per ottenere le informazioni dal servizi di individuazione automatica.

## Test di connettività per i Servizi Web Exchange

I test di servizi Web Exchange controllare le impostazioni per molte delle Exchange servizi Web. È possibile eseguire i seguenti test per Exchange servizi Web:

  - **Sincronizzazione, Notifica, Disponibilità e Risposte automatiche:** questi test esamineranno numerose attività di base di Servizi Web Exchange per verificare che funzionano correttamente. Questa operazione è utile per gli amministratori IT che desiderano risolvere i problemi di accesso esterno tramite Entourage EWS o altri client di servizi Web.

  - **Accesso account servizio (sviluppatori):** questo test verifica la capacità dell'account di servizio di accedere a una cassetta di posta specificata, creare ed eliminare elementi all'interno di questa e accedere alla cassetta postale tramite la rappresentazione di Exchange. Questo test è utilizzato principalmente dagli sviluppatori di applicazioni per verificare la capacità di accesso alle cassette postali con credenziali alternative.

## Prove di connettività di Microsoft Office Outlook

È possibile eseguire i seguenti test per la connettività Outlook:

  - **Outlook via Internet (RPC su HTTP):** questo test illustra i passaggi utilizzati da Outlook per connettersi tramite Outlook via Internet (RPC su HTTP).

  - **Individuazione automatica di Outlook:** questo test illustra i passaggi utilizzati da Outlook per ottenere impostazioni dal servizio Individuazione automatica, ma non stabilisce realmente una connessione a una cassetta postale.

## Test per posta elettronica Internet

È possibile eseguire i seguenti test per la posta elettronica Internet:

  - **Posta elettronica SMTP** **in ingresso:** questo test illustra i passaggi utilizzati da un server di posta elettronica Internet per inviare la posta elettronica SMTP in ingresso al dominio.

  - **Posta elettronica SMTP in uscita:** questo test verifica l'aderenza a requisiti specifici dell'indirizzo IP in uscita. Sono inclusi i controlli DNS inversa, ID mittente e RBL.

  - **Posta elettronica POP:** questo test illustra i passaggi utilizzati da un client di posta elettronica per connettersi a una cassetta postale tramite POP3.

  - **Posta elettronica IMAP:** questo test illustra i passaggi utilizzati da un client di posta elettronica per connettersi a una cassetta postale tramite IMAP.


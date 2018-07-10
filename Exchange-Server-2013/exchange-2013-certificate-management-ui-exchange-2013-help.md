---
title: 'Interfaccia utente per la gestione dei certificati in Exchange 2013: Exchange 2013 Help'
TOCTitle: Interfaccia utente per la gestione dei certificati in Exchange 2013
ms:assetid: 8975848d-07f0-4643-9eac-20aece69945f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ984582(v=EXCHG.150)
ms:contentKeyID: 52063084
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Interfaccia utente per la gestione dei certificati in Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-04-21_

La gestione dei certificati in una distribuzione Exchange Server è una delle attività amministrative più importanti. Impostare e configurare correttamente i certificati è fondamentale per offrire un'infrastruttura di messaggistica sicura all'organizzazione. In Exchange 2010, Exchange Management Console (EMC) era il mezzo primario per la gestione dei certificati. In Exchange 2013, la funzionalità di gestione dei certificati è fornita in Interfaccia di amministrazione di Exchange, la nuova interfaccia utente amministratore di Exchange 2013. In Exchange 2013, l'attenzione è incentrata sulla riduzione del numero dei certificati che un amministratore deve gestire, sulla riduzione delle interazioni dell'amministratore con i certificati e sulla possibilità di gestire i certificati da una posizione centrale.

## Certificati del server Accesso client

Il server Accesso client in Exchange 2013 è un thin server che non presenta informazioni sullo stato, progettato per accettare le connessioni client in ingresso e inoltrarle tramite proxy al server Cassette postali corretto. L'interfaccia utente di gestione dei certificati di Exchange Certificate sul server Accesso client può essere utile in varie attività, inclusa la richiesta di nuovi certificati e il rinnovo di certificati scaduti o in procinto di scadenza.

## Informazioni sull'interfaccia utente di gestione dei certificati

È possibile accedere all'interfaccia utente di gestione dei certificati di Exchange tramite EAC selezionando **Server** e quindi **Certificati**. L'utilizzo dell'interfaccia utente di gestione consente di effettuare le seguenti azioni:

  - **Creare un nuovo certificato**   Selezionando **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") viene avviata la procedura guidata Nuovo certificato di Exchange.

  - **Modificare un certificato esistente**   Selezionando **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") in un certificato valido è possibile visualizzare la pagina delle proprietà del certificato.

  - **Eliminare un certificato**   Selezionando **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina") quando un certificato è selezionato, viene avviata la finestra di dialogo di conferma dell'eliminazione.

  - **Eseguire altre azioni**   Selezionando **Altre opzioni**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni") è possibile esportare o importare un certificato. Se si desidera esportare un certificato, questo deve essere valido.

## Scadenza del certificato

Nelle versioni precedenti di Microsoft Exchange era difficile vedere quando un certificato digitale era prossimo alla scadenza. In Exchange 2013, il centro Notifiche visualizza avvisi quando un certificato archiviato su un qualsiasi server Accesso client di Exchange 2013 sta per scadere.

## Certificati del server Cassette postali

Una differenza fondamentale tra Exchange 2010 e Exchange 2013 sta nel fatto che i certificati che vengono utilizzati nel server Cassette postali di Exchange 2013 sono autofirmati. Siccome tutti i client si connettono a un server Cassette postali Exchange 2013 tramite server Accesso client Exchange 2013, i soli certificati che è necessario gestire sono quelli sui server Accesso client. Il server Accesso client ritiene automaticamente attendibile il certificato autofirmato sul server Cassette postali, in modo che i client non ricevano l'avviso su un certificato autofirmato non considerato attendibile, purché il server Accesso client disponga di un certificato non autofirmato di un'Autorità di certificazione di Windows o di terze parti ritenute attendibili. Non sono disponibili strumenti né cmdlets per la gestione dei certificati autofirmati sul server Cassette postali. Una volta che il server è stato installato correttamente, non è necessario preoccuparsi dei certificati sul server Cassette postali.

## Scadenza dei certificati autofirmati

Per impostazione predefinita, il certificato autofirmato installato sul server Cassette postali di Exchange 2013 scade dopo cinque anni dalla data di installazione.

## Cmdlet dei certificati

È possibile utilizzare i seguenti cmdlet per gestire i certificati digitali su un server Accesso client di Exchange:

  - Import-ExchangeCertificate   Questo cmdlet viene utilizzato per importare certificati in un server. È possibile importare un certificato firmato dall'autorità di certificazione (per completare una richiesta di firma del certificato in sospeso) oppure un certificato con una chiave privata (file PKCS \#12, in genere con estensione .pfx, esportati in precedenza da un server insieme a una chiave privata).

  - Remove-ExchangeCertificate   Questo cmdlet viene utilizzato per rimuovere certificati da un server.

  - Enable-ExchangeCertificate   Questo cmdlet viene utilizzato per assegnare servizi a un certificato.

  - Get-ExchangeCertificate   Questo cmdlet viene utilizzato per recuperare un certificato Exchange in base a diversi criteri.

  - New-ExchangeCertificate   Questo cmdlet viene utilizzato per creare un nuovo certificato autofirmato o una richiesta di firma del certificato.


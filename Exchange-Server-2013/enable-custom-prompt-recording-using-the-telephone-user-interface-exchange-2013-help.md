---
title: "Abilitare la registrazione di prompt personalizzata utilizzando l'interfaccia utente di telefono: Exchange 2013 Help"
TOCTitle: Abilitare la registrazione di prompt personalizzata utilizzando l'interfaccia utente di telefono
ms:assetid: f2e5c636-2be9-4d48-b5e7-37913ded62d1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb691404(v=EXCHG.150)
ms:contentKeyID: 54652893
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare la registrazione di prompt personalizzata utilizzando l'interfaccia utente di telefono

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2014-09-17_

È possibile utilizzare Shell per abilitare la registrazione delle istruzioni e dei messaggi di saluto personalizzati per i dial plan e gli operatori automatici di messaggistica unificata utilizzando l'interfaccia telefonica (TUI). Questa possibilità può essere utile quando si desidera modificare un messaggio di saluto o un annuncio personalizzato tramite EAC o Shell oppure quando si verifica un'emergenza, ad esempio la chiusura dell'organizzazione per cattive condizioni meteo. Quando si modifica un messaggio di saluto o un annuncio personalizzato in un operatore automatico di messaggistica unificata, è necessario abilitare la registrazione delle istruzioni dell'interfaccia telefonica nel dial plan a cui è collegato l'operatore automatico di messaggistica unificata.

Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" e \&quot;Operatori automatici di messaggistica unificata\&quot; nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Abilitazione della registrazione di un prompt o di un messaggio di saluto personalizzato utilizzando l'interfaccia telefonica tramite Shell

Per registrare le istruzioni e i messaggi di saluto personalizzati utilizzando l'interfaccia telefonica (TUI), procedere come segue:

1.  Creare un account utente di dominio che non possa accedere in modo interattivo.

2.  Delegare il ruolo di amministratore dell'organizzazione di Exchange all'account utente di dominio.

3.  Creare una cassetta postale per l'utente di domino.

4.  Abilitare la cassetta postale dell'utente di domino alle funzionalità di messaggistica unificata.
    

    > [!IMPORTANT]
    > Consentire solo agli amministratori che si occuperanno della gestione delle istruzioni e dei messaggi di saluto l'accesso al numero di interno e al PIN per l'account utente. Utilizzare l'account utente solo per la gestione delle istruzioni al telefono.



5.  Creare e salvare un file WAV o WMA da utilizzare per un messaggio di saluto personalizzato per il dial plan o l'operatore automatico di messaggistica unificata.
    

    > [!NOTE]
    > I file MP3 non possono essere utilizzati per le istruzioni personalizzate.



6.  Utilizzare EAC o Shell per configurare il dial plan per l'uso della formula di benvenuto personalizzata oppure configurare l'operatore automatico per l'uso del messaggio di saluto per l'orario di ufficio e non di ufficio. Per i dettagli sulla configurazione di un dial plan, vedere [Consentire a un messaggio di saluto personalizzato per gli utenti di Outlook Voice Access](enable-a-customized-greeting-for-outlook-voice-access-users-exchange-2013-help.md). Per i dettagli sulla configurazione di un operatore automatico, vedere [Abilitare un orario di ufficio personalizzato messaggio di saluto](enable-a-customized-business-hours-greeting-exchange-2013-help.md)[Abilitare un personalizzata non di ufficio messaggio di saluto](enable-a-customized-non-business-hours-greeting-exchange-2013-help.md).

7.  Eseguire il seguente cmdlet:
    
        Set-UMDialPlan -identity MyUMDialPlan -TUIPromptEditingEnabled $true


> [!NOTE]
> Prima di abilitare la registrazione di un'istruzione o di un messaggio di saluto personalizzato, è necessario accedere alla cassetta postale configurata per la registrazione delle istruzioni. Una volta registrata la nuova istruzione o il nuovo messaggio di saluto, è necessario scollegarsi e riaccedere per poter ascoltare la nuova istruzione o il nuovo messaggio di saluto quando si utilizza l'interfaccia telefonica.



## Esecuzione della registrazione delle istruzioni dell'interfaccia telefonica su un operatore automatico di messaggistica unificata

1.  Verificare che l'operatore automatico sia collegato al dial plan abilitato per la registrazione delle istruzioni dell'interfaccia telefonica.

2.  Chiamare un numero di telefono configurato per l'operatore automatico di messaggistica unificata.

3.  Durante la riproduzione del messaggio di saluto per l'orario di ufficio o l'orario non di ufficio per l'operatore automatico, premere il tasto cancelletto (\#), quindi premere il tasto asterisco (\*).

4.  Verrà chiesto di immettere il numero di interno dell'utente. Immettere il numero di interno dell'utente abilitato alla messaggistica unificata che dispone dell'autorizzazione a eseguire la registrazione delle istruzioni dell'interfaccia telefonica.

5.  Verrà richiesta l'immissione del PIN. Immettere il PIN dell'utente.

6.  Seguire le istruzioni del sistema per modificare e aggiornare il messaggio di saluto o l'annuncio informativo per l'operatore automatico.

## Esecuzione delle istruzioni dell'interfaccia telefonica per un dial plan di messaggistica unificata

1.  Chiamare un numero di Outlook Voice Access utilizzato per accedere a Outlook Voice Access.

2.  Durante la riproduzione della formula di benvenuto per il dial plan, premere il tasto cancelletto (\#), quindi premere il tasto asterisco (\*).

3.  Se la chiamata viene effettuata da un telefono utilizzato da un utente abilitato alla messaggistica unificata, verrà richiesto il PIN. Anziché immettere il PIN, premere il tasto asterisco (\*). Verrà richiesto un numero di interno. Immettere il numero di interno dell'utente abilitato alla messaggistica unificata che dispone dell'autorizzazione a eseguire la registrazione delle istruzioni dell'interfaccia telefonica.

4.  Se la chiamata viene effettuata da un telefono non utilizzato da un utente abilitato alla messaggistica unificata, verrà richiesto un numero di interno. Immettere il numero di interno dell'utente abilitato alla messaggistica unificata che dispone dell'autorizzazione a eseguire la registrazione delle istruzioni dell'interfaccia telefonica.

5.  Verrà richiesta l'immissione del PIN. Immettere il PIN dell'utente.

6.  Seguire le istruzioni del sistema per modificare o aggiornare la formula di benvenuto per il dial plan o l'annuncio informativo.


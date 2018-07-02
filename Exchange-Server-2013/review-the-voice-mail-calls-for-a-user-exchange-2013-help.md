---
title: 'Esaminare le chiamate di posta vocale di un utente: Exchange 2013 Help'
TOCTitle: Esaminare le chiamate di posta vocale di un utente
ms:assetid: 95768fe3-3ae2-43bd-9cbf-18c3b85c4592
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ659070(v=EXCHG.150)
ms:contentKeyID: 50555647
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Esaminare le chiamate di posta vocale di un utente

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

I registri chiamate dell'utente vengono utilizzati per visualizzare le informazioni seguenti relative a utenti specifici di messaggistica unificata:

  - Dettagli sulle chiamate di messaggistica unificata di un utente degli ultimi 90 giorni.

  - Qualità audio di ogni chiamata. La metrica della qualità audio potrebbe non essere disponibile per tutte le chiamate, perché dipende da diversi fattori, ad esempio il tipo e la lunghezza della chiamata.

Per ulteriori attività relative ai rapporti di messaggistica unificata, vedere [Procedure di rapporti di messaggistica unificata](um-reports-procedures-exchange-2013-help.md).

## Come ottenere i registri chiamate per un utente abilitato per la messaggistica unificata?

1.  Nell'interfaccia di amministrazione di Exchange, selezionare **Messaggistica unificata** \> **Altre opzioni**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni") \> **Registri chiamate utente**.

2.  Fare clic su **Seleziona utente**, quindi selezionare l'utente di cui si desidera visualizzare i dati.

3.  Per ottenere maggiori informazioni sulla qualità audio per una riga del rapporto, selezionare la riga e fare clic su **Dettagli qualità audio**. Per ulteriori informazioni sull'interpretazione della qualità audio, vedere [Esaminare la qualità dell'audio delle chiamate vocali per un utente](investigate-the-audio-quality-of-voice-calls-for-a-user-exchange-2013-help.md).

4.  Per copiare il report negli Appunti, fare clic su **Copia tutte le righe negli Appunti**.

## Come interpretare il registro chiamate dell'utente di messaggistica unificata?

Nel registro chiamate dell'utente sono incluse le informazioni seguenti per ogni chiamata:

  - **DATA E ORA** La data e l'ora della chiamata, nel fuso orario impostato dall'utente selezionato in Outlook Web App.

  - **DURATA** Durata della chiamata, in minuti (MM) e secondi (SS) nel formato seguente: MM:SS.

  - **TIPO DI CHIAMATA**Il tipo di chiamata:
    
      - **Risponditore automatico** Nessuna risposta alla chiamata. La chiamata è stata inoltrata ai server Cassette postali e il chiamante ha lasciato un messaggio vocale.
    
      - **Chiamate senza risposta al risponditore automatico**   Non vi è stata risposta alla chiamata, pertanto è stata inoltrata ai server Cassette postali e il chiamante non ha lasciato alcun messaggio vocale.
    
      - **Accesso sottoscrittore** È stata effettuata una chiamata al numero di accesso del sottoscrittore. Il chiamante ha effettuato l'accesso ed è stato autenticato alla messaggistica unificata con numero di interno e password personali per accedere ai messaggi di posta elettronica, calendari e messaggi vocali tramite telefono.
    
      - **Operatore automatico** Un operatore automatico di messaggistica unificata ha risposto alla chiamata. In genere, si tratta delle chiamate per le quali il chiamante ha composto il numero di telefono principale dell'organizzazione.
    
      - **Fax** Chiamata durante la quale viene rilevato un segnale fax. Se sono stati configurati partner fax, la chiamata viene inviata al partner.
    
      - **Ascolta al telefono** Chiamata effettuata dalla messaggistica unificata poiché l'utente ha fatto clic sul pulsante Ascolta al telefono in Microsoft Outlook Web App o in Outlook.
    
      - **Trovami** Chiamata in uscita effettuata dalla messaggistica unificata a causa della regola Trovami in una regola ricezione chiamata.
    
      - **Numero pilota non autenticato**   Chiamata effettuata al numero di Outlook Voice Access. Il chiamante non ha effettuato l'accesso e non è stato autenticato.
    
      - **Registrazione messaggi di saluto**   Chiamata effettuata dalla messaggistica unificata per registrare messaggi di saluto personali per un utente.
    
      - **Nessuno** Chiamata per cui non è stato definito alcun tipo.

  - **NUMERO CHIAMATO** Numero di telefono o indirizzo SIP del chiamante.

  - **NUMERO CHIAMATO** Numero di telefono o indirizzo SIP (per utenti con dial plan SIP, ad esempio utenti di Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server) del destinatario della chiamata.

  - **GATEWAY IP DI MESSAGGISTICA UNIFICATA** Gateway che ha ricevuto la chiamata.

  - **QUALITÀ AUDIO** Qualità audio complessiva della chiamata. Per maggiori dettagli sulla qualità audio, selezionare la riga e fare clic su **Dettagli qualità audio**.


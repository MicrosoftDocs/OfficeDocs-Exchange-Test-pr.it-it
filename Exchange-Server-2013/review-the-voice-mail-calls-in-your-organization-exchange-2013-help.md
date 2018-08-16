---
title: "Esamina chiamate posta vocale nell'organizzazione: Exchange 2013 Help"
TOCTitle: Esaminare le chiamate di posta vocale all'interno dell'organizzazione
ms:assetid: f6fdbe17-d1d2-442a-aa13-06b908d9c33a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ659073(v=EXCHG.150)
ms:contentKeyID: 50555710
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Esaminare le chiamate di posta vocale all'interno dell'organizzazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile utilizzare il rapporto Statistiche chiamate per visualizzare le informazioni sul tipo e lo stato delle chiamate in ingresso gestite dai server Exchange dell'organizzazione. Il rapporto contiene informazioni statistiche sulle chiamate inoltrate alla messaggistica unificata o effettuate da essa per l'organizzazione. È possibile utilizzare le informazioni per tenere traccia dell'utilizzo della pianificazione delle capacità, del monitoraggio e della risoluzione dei problemi di disponibilità e qualità audio della messaggistica unificata, nonché la risoluzione dei problemi delle chiamate con errori.

Il presente argomento include le risposte alle domande seguenti:

  - How do I get call statistics for UM?

  - How do I interpret UM call statistics?

Per ulteriori attività relative ai rapporti di messaggistica unificata, vedere [Procedure di rapporti di messaggistica unificata](um-reports-procedures-exchange-2013-help.md).

## Come ottenere statistiche sulle chiamate per la messaggistica unificata?

1.  Nell'interfaccia di amministrazione di Exchange (EAC), fare clic su **Messaggistica unificata** \>**Ulteriori opzioni**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni")**Statistiche sulle chiamate**.

2.  Scegliere le informazioni da includere nel rapporto. Il rapporto viene aggiornato automaticamente con la selezione delle opzioni seguenti:
    
      - **Mostra**  Scegliere il tipo di statistiche delle chiamate da visualizzare:
        
          - **Ogni giorno (90 giorni)**  Selezionare Ogni giorno per visualizzare i dettagli per tutte le chiamate degli ultimi 90 giorni.
        
          - **Mensile (12 mesi)**   Selezionare Mensile per visualizzare un riepilogo mensile delle chiamate per gli ultimi 12 mesi.
        
          - **Tutto**   Selezionare Tutto per visualizzare le statistiche combinate per tutte le chiamate ricevute dall'inizio dell'utilizzo della messaggistica unificata per la gestione delle chiamate.
    
      - **Dial plan di messaggistica unificata**   Per limitare i dati del rapporto alle sole chiamate di un dial plan di messaggistica unificata specifico, selezionare tale dial plan.
    
      - **Gateway IP di messaggistica unificata**   Per limitare i dati del rapporto alle sole chiamate di un gateway IP di messaggistica unificata specifico, selezionare tale gateway. Se si seleziona prima un dial plan di messaggistica unificata, nell'elenco saranno disponibili solo i gateway IP di messaggistica unificata associati a tale dial plan.

3.  Per ottenere maggiori informazioni sulla qualità audio per una riga del rapporto, selezionare la riga e fare clic su **Dettagli qualità audio**. Per ulteriori informazioni sull'interpretazione della qualità audio, vedere [Esaminare la qualità dell'audio delle chiamate vocali all'interno dell'organizzazione](investigate-the-audio-quality-of-voice-calls-in-your-organization-exchange-2013-help.md).

4.  Per copiare il rapporto negli Appunti, fare clic su **Copia**.

5.  Per i rapporti giornalieri, è possibile esportare i dettagli per un giorno specifico in un file con estensione CSV.
    
    1.  Selezionare il giorno e fare clic su **Esporta giorno**.
    
    2.  Nella casella di conferma **Download del file** fare clic su **Apri** o su **Salva**.
    
    Il file esportato sarà denominato um\_cdr\_*AAAA-MM-GG*.csv dove *AAAA-MM-GG* rappresenta l'anno, il mese e il giorno in cui è stato eseguito il rapporto. Per ulteriori informazioni, vedere [Interpretazione dei record di mail chiamate vocali](interpret-voice-mail-call-records-exchange-2013-help.md).
    

    > [!NOTE]
    > Nella pagina del rapporto, è possibile scaricare un modello di Microsoft Excel utilizzabile per importare il file CSV per un giorno specifico.



Inizio pagina

## Come interpretare le statistiche sulle chiamate di messaggistica unificata?

Il rapporto sulle statistiche delle chiamate di messaggistica unificata include le seguenti informazioni:

  - **DATA**   Data UTC per i dati della chiamata. Il formato della data dipende dal tipo di rapporto scelto e dalle impostazioni internazionali. È possibile scegliere uno dei seguenti comandi:
    
      - **---**  Vengono visualizzate tutte le chiamate.
    
      - **MMM/AA**   Mese delle chiamate. ad esempio Gen/13.
    
      - **MM/GG/AA**   Giorno delle chiamate. ad esempio 6/23/13.

  - **TOTALE**   Numero complessivo di chiamate per il dial plan di messaggistica unificata selezionato o il gateway IP di messaggistica unificata per tale data.

  - **MESSAGGIO VOCALE**   Percentuale di chiamate in entrata a cui ha risposto il servizio di messaggistica unificata per conto degli utenti e in cui chiamanti hanno lasciato un messaggio vocale.

  - **SENZA RISPOSTA**   Percentuale di chiamate in ingresso a cui ha risposto il servizio di messaggistica unificata per conto degli utenti e in cui i chiamanti non hanno lasciato un messaggio vocale, generando così una notifica di chiamata senza risposta.

  - **OUTLOOK VOICE ACCESS**   Percentuale di chiamate in ingresso in cui gli utenti hanno effettuato l'accesso alla messaggistica unificata, e sono stati autenticati, per accedere alla posta elettronica, ai calendari e ai messaggi vocali.

  - **IN USCITA**   Percentuale di chiamate effettuate o trasferite dalla messaggistica unificata per conto di utenti autenticati o non autenticati. Questa statistica include i tipi di chiamata Trovami, Ascolta al telefono e Messaggi di saluto Ascolta al telefono.

  - **OPERATORE AUTOMATICO**   Percentuale di chiamate in entrata a cui hanno risposto gli operatori automatici di messaggistica unificata.

  - **FAX**   Percentuale di chiamate in entrata reindirizzate a un partner fax.

  - **ALTRO**   Percentuale di altre chiamate in ingresso o in uscita che non appartengono alle categorie precedenti. Queste chiamate includono quelle effettuate ai numeri di Outlook Voice Access in cui gli utenti non hanno effettuato l'accesso e non sono stati autenticati.

  - **NON RIUSCITE O RIFIUTATE**   Percentuale di chiamate non riuscite o rifiutate dalla messaggistica unificata. Si noti che le chiamate non riuscite non vengono conteggiate due volte. Ad esempio, se una chiamata a Outlook Voice Access ha esito negativo, viene conteggiata solo come non riuscita, non anche come chiamata a Outlook Voice Access.

  - **QUALITÀ AUDIO**   Rappresentazione grafica della qualità audio complessiva nell'intervallo di tempo selezionato per l'organizzazione.

Inizio pagina

## Ulteriori informazioni

[Esaminare la qualità dell'audio delle chiamate vocali all'interno dell'organizzazione](investigate-the-audio-quality-of-voice-calls-in-your-organization-exchange-2013-help.md)

[Interpretazione dei record di mail chiamate vocali](interpret-voice-mail-call-records-exchange-2013-help.md)


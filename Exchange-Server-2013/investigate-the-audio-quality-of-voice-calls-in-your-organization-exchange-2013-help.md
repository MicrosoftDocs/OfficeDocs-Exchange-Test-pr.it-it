---
title: "Esaminare la qualità dell'audio delle chiamate vocali all'interno dell'organizzazione: Exchange 2013 Help"
TOCTitle: Esaminare la qualità dell'audio delle chiamate vocali all'interno dell'organizzazione
ms:assetid: 8a87694b-1678-4a01-859f-5ad3b2c73db5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ659069(v=EXCHG.150)
ms:contentKeyID: 50555634
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Esaminare la qualità dell'audio delle chiamate vocali all'interno dell'organizzazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-21_

Se nell'organizzazione si verificano problemi di qualità audio per le chiamate di messaggistica unificata e i messaggi vocali, utilizzare il rapporto Statistiche sulle chiamate per cercare di individuare la causa dei problemi.


> [!NOTE]
> La qualità audio di una chiamata può subire gli effetti di fattori che non vengono considerati nei rapporti. Ad esempio, se nel server Exchange è presente un carico di memoria o CPU eccessivo, la qualità delle chiamate può risultare scarsa, anche se nei rapporti viene segnalata una qualità audio eccellente.



Per le attività aggiuntive relative alle statistiche delle chiamate, vedere [Procedure di rapporti di messaggistica unificata](um-reports-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cmdlet dei rapporti di riepilogo e dei dati sulle chiamate di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Acquisizione delle statistiche sulla qualità audio per l'organizzazione tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, passare a **Messaggistica unificata** \> **Altre opzioni**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni") \> **Statistiche sulle chiamate**.

2.  Scegliere le statistiche delle chiamate da includere nel rapporto. Il rapporto viene aggiornato automaticamente con la selezione delle opzioni seguenti.
    
      - **Mostra **  Scegliere il tipo di statistiche delle chiamate da visualizzare:
        
          - **Ogni giorno (90 giorni) **  Selezionare Ogni giorno per visualizzare i dettagli per tutte le chiamate degli ultimi 90 giorni.
        
          - **Mensile (12 mesi)**   Selezionare Mensile per visualizzare un riepilogo mensile delle chiamate per gli ultimi 12 mesi.
        
          - **Tutto**   Selezionare Tutto per visualizzare le statistiche combinate per tutte le chiamate ricevute dall'inizio dell'utilizzo della messaggistica unificata per la gestione delle chiamate.
    
      - **Dial plan di messaggistica unificata**   Per limitare i dati del rapporto alle sole chiamate di un dial plan di messaggistica unificata specifico, selezionare tale dial plan.
    
      - **Gateway IP di messaggistica unificata**   Per limitare i dati del rapporto alle sole chiamate di un gateway IP di messaggistica unificata specifico, selezionare tale gateway. Se si seleziona prima un dial plan di messaggistica unificata, nell'elenco saranno disponibili solo i gateway IP di messaggistica unificata associati a tale dial plan.

3.  Per ottenere maggiori informazioni sulla qualità audio per una riga del rapporto, selezionare la riga e fare clic su **Dettagli qualità audio**. Sono disponibili le seguenti informazioni:
    
      - **DATA E ORA**   Data e ora UTC in cui sono state acquisite le statistiche delle chiamate.
    
      - **DIAL PLAN DI MESSAGGISTICA UNIFICATA**   Dial plan per le chiamate incluse nelle statistiche.
    
      - **Gateway IP di messaggistica unificata**   Gateway IP di messaggistica unificata che ha ricevuto le chiamate incluse nelle statistiche.
    
      - **NMOS   ** Punteggio NMOS (Network Mean Opinion Score) per la chiamata. Il punteggio NMOS indica la qualità audio della chiamata con un numero su una scala da 1 a 5, dove 5 rappresenta l'eccellenza.
        

        > [!NOTE]
        > Il punteggio NMOS massimo di una chiamata dipende dal codec audio utilizzato. Il punteggio NMOS potrebbe non essere disponibile per le chiamate molto brevi di durata inferiore a 10&nbsp;secondi.

    
      - **DEGRADAZIONE NMOS** Quantità di degradazione audio del punteggio NMOS dal valore massimo possibile per il codec audio in uso. Ad esempio, se il valore di degradazione NMOS per una chiamata fosse 1,2 e il punteggio NMOS indicato per la chiamata fosse 3,3, il punteggio NMOS massimo per questa chiamata particolare sarebbe pari a 4,5 (1,2 + 3,3).
    
      - **INSTABILITÀ** Variazione media nell'arrivo dei pacchetti di dati per la chiamata.
    
      - **PERDITA PACCHETTI** Percentuale media di perdita dei pacchetti di dati per la chiamata selezionata. La perdita di pacchetti è un'indicazione dell'affidabilità della connessione.
    
      - **ANDATA E RITORNO** Punteggio del percorso medio di andata e ritorno, in millisecondi, per l'audio della chiamata selezionata. Il punteggio del percorso di andata e ritorno consente di misurare la latenza della connessione.
    
      - **DURATA PERDITA BURST** Durata media della perdita di pacchetti durante i burst di perdite per la chiamata selezionata.
    
      - **NUMERO DI ESEMPI**   Numero di chiamate campionate per calcolare le medie.

4.  Per la metrica dettagliata della qualità audio di chiamate specifiche, vedere [Esaminare la qualità dell'audio delle chiamate vocali per un utente](investigate-the-audio-quality-of-voice-calls-for-a-user-exchange-2013-help.md).


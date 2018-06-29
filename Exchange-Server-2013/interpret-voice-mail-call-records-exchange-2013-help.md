---
title: 'Interpretazione dei record di mail chiamate vocali: Exchange 2013 Help'
TOCTitle: Interpretazione dei record di mail chiamate vocali
ms:assetid: 368d9c58-61a2-43d5-8189-d3469a9e2a8d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ659061(v=EXCHG.150)
ms:contentKeyID: 50555566
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Interpretazione dei record di mail chiamate vocali

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-22_

Per visualizzare informazioni dettagliate sulle chiamate gestite dai server di Exchange in un giorno specifico, esportare i dati della chiamata per quel giorno dal rapporto sulle statistiche delle chiamate. I dati giornalieri sulle chiamate, disponibili per i 90 giorni precedenti, possono consentire di diagnosticare problemi relativi alla qualità audio o a chiamate rifiutate e forniscono informazioni per i controlli o i rapporti sui server di Exchange della propria organizzazione.

Per ulteriori attività relative ai rapporti di messaggistica unificata, vedere [Procedure di rapporti di messaggistica unificata](um-reports-procedures-exchange-2013-help.md).

## Esportazione giornaliera dei record delle chiamate di messaggistica tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Messaggistica unificata** \> **Altre opzioni**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni") \> **Statistiche chiamate**.

2.  In **Mostra**, fare clic su **Ogni giorno (90 giorni)**, quindi scegliere il dial plan di messaggistica unificata, il gateway IP di messaggistica unificata o entrambi. Il rapporto viene aggiornato automaticamente mentre si scelgono le opzioni.

3.  Selezionare il giorno per il quale si desidera esportare i record delle chiamate, quindi fare clic su **Esporta giorno**.

4.  Nella finestra di conferma **Download file**, fare clic su **Apri** o su **Salva**.
    
    Il file esportato sarà denominato um\_cdr\_*AAAA-MM-GG*.csv dove *AAAA-MM-GG* rappresenta l'anno, il mese e il giorno in cui è stato eseguito il rapporto.
    

    > [!NOTE]
    > Nella pagina del rapporto, è possibile scaricare un modello di Microsoft Excel utilizzabile per importare il file .csv per un determinato giorno.



5.  Utilizzare un'applicazione come Excel per elaborare il file con estensione csv e compilare i rapporti personalizzati.

## Interpretazione dei dati delle chiamate di messaggistica unificata

Nei dati delle chiamate di messaggistica unificata esportati sono incluse le seguenti informazioni dettagliate su ogni chiamata gestita dalla messaggistica unificata in un determinato giorno.


> [!NOTE]
> Nel rapporto Statistiche chiamate, i giorni sono indicati nel formato ora UTC.



  - **OraInizioChiamata   **La data e l'ora di gestione della chiamata da parte della messaggistica unificata, in formato UTC. Data e ora UTC sono rappresentate nel seguente formato: *AAAA-MM-GG hh:mm:SSZ*, dove *AAAA* = anno, *MM* = mese, *GG* = giorno, *hh* = ora , nel formato 24 ore, *mm* = minuti, ss = secondi. Z sta per Zulu, che è il modo utilizzato per indicare l'ora UTC (come +*hh*:*mm* o -*hh*:*mm*, che fornisce l'offset orario da UTC). Poiché tutte le ore delle chiamate di questo rapporto sono in formato UTC, la Z sarà sempre presente.
    
    Ad esempio, per una chiamata effettuata il 23.06.13 alle 14.23, l'ora di inizio della chiamata viene mostrata come 23/06/2013 14:23:11Z.

  - **Tipo di chiamata   **Tipo di chiamata:
    
      - **Messaggio vocale del risponditore automatico**   Non vi è stata risposta alla chiamata, pertanto è stata inoltrata ai server di Exchange e il chiamante ha lasciato un messaggio vocale.
    
      - **Chiamate senza risposta risponditore automatico**   Non vi è stata risposta alla chiamata, pertanto è stata inoltrata ai server di Exchange e il chiamante non ha lasciato alcun messaggio vocale.
    
      - **Accesso sottoscrittore**   È stata effettuata una chiamata al numero di accesso del sottoscrittore. Il chiamante ha effettuato l'accesso ed è stato autenticato nella messaggistica unificata con il proprio interno e la password per accedere ai messaggi di posta elettronica, ai calendari e ai messaggi vocali sul telefono.
    
      - **Operatore automatico**   La risposta alla chiamata è stata effettuata da un operatore automatico di messaggistica unificata. In genere, si tratta delle chiamate per le quali il chiamante ha composto il numero di telefono principale dell'organizzazione.
    
      - **Fax**   È stata ricevuta una chiamata durante la quale è stato rilevato un segnale fax. Se vi sono partner fax configurati, la chiamata è stata inviata al partner.
    
      - **Ascolta al telefono**   Chiamata effettuata dalla messaggistica unificata poiché l'utente ha fatto clic sul pulsante Ascolta al telefono in un messaggio vocale in Microsoft Outlook Web App o Outlook.
    
      - **Trovami**   È stata effettuata una chiamata in uscita dalla messaggistica unificata in conseguenza a una regola Trovami in una regola ricezione chiamata.
    
      - **Numero pilota non autenticato**   È stata effettuata una chiamata al numero di Outlook Voice Access. Il chiamante non ha effettuato l'accesso e non è stato autenticato.
    
      - **Registrazione messaggi di saluto**  È stata effettuata una chiamata dalla messaggistica unificata per registrare messaggi di saluto personali per un utente.
    
      - **Nessuno**   È stata effettuata una chiamata di cui, però, non è stato definito il tipo.

  - **Identità chiamata** L'identità della chiamata SIP fornita dal gateway IP di messaggistica unificata.

  - **Identità chiamata principale** L'identità della sessione SIP che ha dato origine a questa chiamata. Questa casella viene utilizzata quando si seleziona la funzionalità Trovami di Regole ricezione chiamata o si effettuano trasferimenti di chiamata, inclusi quelli tra operatori automatici di messaggistica unificata.

  - **NomeServerMessaggisticaUnificata** Il nome del server Cassette postali tramite cui viene gestita la chiamata, se presente. Queste informazioni vengono fornite solo se si dispone di un server Cassette postali locale.

  - **NomeDialPlan** Il dial plan di messaggistica unificata tramite cui è stata gestita la chiamata.

  - **Durata chiamata** La durata totale della chiamata.

  - **IndirizzoGatewayIP** Il nome di dominio completo (FQDN) del gateway IP tramite che ha gestito la chiamata.

  - **NumeroTelefonoChiamato** Il numero di telefono o indirizzo SIP del destinatario della chiamata (per utenti in dial plan SIP con Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server).

  - **NumeroTelefonoChiamante** Il numero di telefono o indirizzo SIP del chiamante.

  - **OffriRisultato** Lo stato della chiamata:
    
      - **Risposta**   La messaggistica unificata ha risposto o effettuato correttamente una chiamata. La chiamata non è stata né trasferita né reindirizzata. Si tratta delle chiamate con esito positivo a Outlook Voice Access, Ascolta al telefono o agli operatori automatici della messaggistica unificata e delle chiamate gestite dalla messaggistica unificata quando non vi è stata risposta da parte dell'interno chiamato.
    
      - **Non riuscita**   La messaggistica unificata ha accettato o effettuato una chiamata, ma la chiamata non è riuscita. Si tratta delle chiamate in cui il numero o l'indirizzo chiamato è occupato, non risponde o non esiste, in cui il chiamante ha riagganciato prima che la chiamata venisse collegata, in cui le impostazioni dei criteri del dial plan di messaggistica unificata o della cassetta postale di messaggistica unificata hanno impedito la chiamata oppure in cui non è stato possibile raggiungere il gateway o il sistema di telefonia.
    
      - **Rifiutata**   La messaggistica unificata ha rifiutato la chiamata, generalmente a causa di un errore di configurazione. Si tratta delle chiamate in cui il gateway IP di messaggistica unificata non è associato a un dial plan di messaggistica unificata o in cui si verificano errori di incompatibilità.
    
      - **Reindirizzata**   La messaggistica unificata ha accettato la chiamata, ma l'ha reindirizzata a un altro server Cassette postali. Queste chiamate includono quelle in cui il chiamante ha utilizzato il menu della messaggistica unificata per chiamare un contatto nella directory o contatti personali oppure in cui il chiamante ha chiamato un numero di Outlook Voice Access utilizzando un numero di telefono non associato alla cassetta postale dell'utente. In questi casi, la messaggistica unificata trasferisce la chiamata al server Exchange associato all'account di quell'utente.
    
      - **Nessuno**   Lo stato della chiamata non è noto.

  - **MotivoInterruzioneChiamata** Il motivo per cui la chiamata è stata disconnessa, se la messaggistica unificata è stata in grado di determinarlo. Ad esempio, se il chiamante ha riagganciato, viene mostrata l'indicazione Interruzione regolare.

  - **MotivoDellaChiamata** La modalità di connessione della chiamata:
    
      - **Diretta**   Il chiamante ha composto il numero chiamato direttamente.
    
      - **TrasferimentoInoltro**   Il chiamante ha composto un numero e la persona chiamata ha reindirizzato la chiamata alla segreteria telefonica della messaggistica unificata.
    
      - **TrasferimentoOccupato**  Il chiamante ha composto un numero e il telefono era occupato, pertanto la chiamata è stata reindirizzata alla segreteria telefonica della messaggistica unificata.
    
      - **TrasferimentoNessunaRisposta **  Il chiamante ha composto un numero e la persona chiamata non ha risposto, pertanto la chiamata è stata reindirizzata alla segreteria telefonica della messaggistica unificata.
    
      - **In uscita**   La chiamata è stata effettuata dalla messaggistica unificata per riprodurre, ad esempio, un messaggio vocale utilizzando Ascolta al telefono.
    
      - **Nessuno**   Non è stato indicato alcun motivo per la chiamata.

  - **StringaComposta** L'indirizzo o il numero di telefono della persona a cui questa chiamata era destinata o a cui è stata trasferita. Questo valore si riferisce anche all'indirizzo o al numero di telefono utilizzato per le chiamate Ascolta al telefono.

  - **AliasCassettaPostaleChiamante** L'alias della cassetta postale del chiamante (ovvero, la parte dell'indirizzo di posta elettronica che precede il simbolo @). Questo valore è disponibile solo se il chiamante ha eseguito l'accesso a Outlook Voice Access.

  - **AliasCassettaPostaleChiamante** L'alias della cassetta postale del destinatario desiderato della chiamata, se quest'ultimo è un utente abilitato alla messaggistica unificata.

  - **Nome operatore automatico** Il nome dell'operatore automatico associato alla chiamata.

  - **Punteggio NMOS** Il punteggio NMOS (Network Mean Opinion Score) per la chiamata. Il punteggio NMOS indica la qualità audio della chiamata con un numero su una scala da 1 a 5, dove 5 rappresenta l'eccellenza.
    

    > [!NOTE]
    > <STRONG>Nota</STRONG>&nbsp;&nbsp;&nbsp;Il punteggio NMOS massimo consentito per una chiamata dipende dal codec audio utilizzato. Il punteggio NMOS potrebbe non essere disponibile per molte chiamate brevi di durata inferiore ai 10&nbsp;secondi.



  - **DegradazioneNMOS** La quantità di degradazione audio del punteggio NMOS dal valore massimo consentito per il codec audio utilizzato. Ad esempio, se il valore di degradazione NMOS per una chiamata fosse 1,2 e il punteggio NMOS indicato per la chiamata fosse 3,3, il punteggio NMOS massimo per questa chiamata particolare sarebbe pari a 4,5 (1,2 + 3,3).

  - **Instabilità DegradazioneNMOS** La degradazione NMOS totale causata dall'instabilità.

  - **PerditaPacchetti DegradazioneNMOS** La degradazione NMOS totale dovuta alla perdita di pacchetti.

  - **Instabilità   **Variazione media nell'arrivo dei pacchetti di dati per la chiamata.

  - **PerditaPacchetti    **Percentuale media di perdita dei pacchetti di dati per la chiamata selezionata. La perdita di pacchetti è un'indicazione dell'affidabilità della connessione.

  - **Andata e ritorno** Il percorso medio di andata e ritorno, in millisecondi, per l'audio della chiamata selezionata. Il punteggio del percorso di andata e ritorno consente di misurare la latenza della connessione.

  - **DensitàBurst   **Percentuale di pacchetti persi e rimossi all'interno di un periodo di burst (frequenza di perdita elevata).

  - **Durata interruzione burst   **Durata media della perdita di pacchetti durante i burst di perdite per la chiamata selezionata.

  - **Codec audio   **Codec audio utilizzato durante la chiamata.


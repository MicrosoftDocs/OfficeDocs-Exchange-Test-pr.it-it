---
title: 'Traccia di conversione del contenuto: Exchange 2013 Help'
TOCTitle: Traccia di conversione del contenuto
ms:assetid: eb9c7df2-9093-49f9-aa4f-044909bd2225
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb397226(v=EXCHG.150)
ms:contentKeyID: 50481983
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Traccia di conversione del contenuto

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-09-25_

L'analisi della conversione del contenuto acquisisce gli errori nella conversione del contenuto MAPI eseguita dal servizio di trasporto alle cassette postali nei messaggi in ingresso e in uscita su un server Cassette postali di Microsoft Exchange Server 2013.

Il servizio di trasporto alle cassette postali su un server Cassette postali è responsabile della conversione del contenuto dei messaggi inviati da e ai destinatari delle cassette postali. In particolare il servizio Invio alle cassette postali converte da MAPI a MIME i messaggi in uscita provenienti da utenti di cassette postali. Il servizio di recapito alle cassette postali converte da MIME a MAPI i messaggi in ingresso per utenti di cassette postali. L'analisi della conversione del contenuto è responsabile dell'acquisizione di questi errori di conversione MAPI.

Il categorizzatore presente sul server Cassette postali è responsabile della conversione del contenuto di tutti i messaggi inviati a destinatari esterni. Questa funzionalità non acquisisce alcun errore di conversione del contenuto rilevato dal categorizzatore nel servizio di trasporto durante la conversione di messaggi inviati a destinatari esterni.

**Sommario**

Configure content conversion tracing

How content conversion tracing works

Considerations for content conversion tracing

## Configurazione dell'analisi della conversione del contenuto

L'analisi della conversione del contenuto è controllata dai seguenti parametri nei cmdlet **Set-TransportService** e **Set-MailboxTransportService** in Exchange Management Shell:

  - *ContentConversionTracingEnabled*   Parametro che consente di abilitare o disabilitare l'analisi della conversione del contenuto nel servizio di trasporto sul server Cassette postali o nel servizio di trasporto alle cassette postali sul server Cassette postali. Valori validi per questo parametro sono `$true` e `$false`. Il valore predefinito è `$false`. Se l'organizzazione Exchange contiene più server Cassette postali, è necessario abilitare l'analisi della conversione del contenuto su ciascun server Cassette postali.

  - *PipelineTracingPath*   Questo parametro, sebbene sia associato all'analisi pipeline, consente inoltre di specificare il percorso radice dei file di analisi di conversione del contenuto. Il percorso predefinito del servizio di trasporto è `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`. Il percorso predefinito del servizio Trasporto cassette postali è `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`. Il percorso deve essere locale nel computer Exchange.

La conversione del contenuto crea una cartella denominata `ContentConversionTracing` nel percorso specificato dal parametro *PipelineTracingPath*. All'interno della cartella `ContentConversionTracing` la conversione del contenuto crea due sottocartelle: `InboundFailures` e `OutboundFailures`. la cartella `InboundFailures` contiene informazioni sugli errori di conversione del contenuto dei messaggi in ingresso. la cartella `OutboundFailures` contiene informazioni sugli errori di conversione del contenuto dei messaggi in uscita.

Le dimensioni massime per tutti i file della cartella `InboundFailures` o `OutboundFailures` è 128 megabyte (MB). L'analisi della conversione del contenuto non utilizza la registrazione circolare per rimuovere i file meno recenti, ma si basa sulle dimensioni o sulla data di creazione dei file. Non appena viene raggiunta la dimensione massima per una cartella, l'analisi della conversione del contenuto interrompe la scrittura delle informazioni nella cartella. Per assicurarsi che i limiti massimi per le dimensioni della cartella non vengano superati, è possibile creare un'attività pianificata che sposta periodicamente i file dell'analisi della conversione del contenuto in una posizione diversa.

Le autorizzazioni richieste sulle cartelle e sottocartelle utilizzate nell'analisi di conversione del contenuto sono le seguenti:

  - Amministratori: controllo completo

  - Servizio di rete: controllo completo

  - Sistema: controllo completo


> [!WARNING]
> L'analisi della conversione del contenuto copia l'intero contenuto dei messaggi di posta elettronica. Per evitare la divulgazione di informazioni riservate, è necessario impostare apposite autorizzazioni di protezione sulla posizione dei file di analisi della conversione del contenuto.



Inizio pagina

## Come funziona l'analisi della conversione del contenuto

Quando si verifica un errore nella conversione del contenuto dei messaggi in ingresso, al mittente del messaggio viene inviata una notifica sullo stato del recapito (DSN) con codice di stato 5.6.0. Se l'analisi della conversione del contenuto è abilitata, le informazioni sull'errore vengono registrate al momento della generazione del messaggio DSN 5.6.0. Ciascun errore di conversione del contenuto genera due file separati.

Un errore di conversione del contenuto che si verifica quando un messaggio in ingresso viene convertito da MIME a MAPI genera i seguenti due file nella cartella InboundFailures:

  - **\<GUID\>.eml**   Questo file contiene il messaggio non riuscito in formato di testo.

  - **\<GUID\>.txt**   Questo file contiene la descrizione dell'eccezione, i risultati della conversione, le opzioni di conversione e i limiti alle dimensioni dei messaggi imposti a tutti i messaggi dal servizio Trasporto cassette postali.

Un errore di conversione del contenuto che si verifica quando un messaggio in uscita viene convertito da MAPI a MIME genera i seguenti due file nella cartella OutboundFailures:

  - **\<GUID\>.msg**   Questo file contiene il messaggio non recapitato in formato messaggio di Outlook.

  - **\<GUID\>.txt**   Questo file contiene la descrizione dell'eccezione, i risultati della conversione, le opzioni di conversione e i limiti per le dimensioni dei messaggi imposti su tutti i messaggi dal driver di archivio.

Il segnaposto \<*GUID*\> è lo stesso in entrambi i nomi file. Ciascun errore di conversione del contenuto genera un GUID diverso che viene utilizzato nel nome dei file di messaggio e di testo corrispondenti. Un esempio di GUID utilizzato nei nomi file è `038b930e-61fd-4bfd-b9b4-0374c18b73f7`.

Inizio pagina

## Considerazioni sull'analisi della conversione del contenuto

È possibile lasciare l'analisi della conversione del contenuto abilitata per il monitoraggio proattivo. In alternativa, attivare l'analisi di conversione del contenuto per risolvere un errore specifico. Generalmente è possibile riprodurre errori della conversione del contenuto in ingresso chiedendo al destinatario del messaggio DSN 5.6.0 di inviare nuovamente il messaggio originale.

Gli errori della conversione del contenuto in ingresso sono i più comuni. Alcuni dei motivi per errori della conversione del contenuto in ingresso sono:

  - **Violazioni dei limiti delle dimensioni dei messaggi   ** Limiti imposti dal servizio Trasporto cassette postali per evitare attacchi DoS (Denial of Service). Tali limiti per i messaggi sono elencati nel file \<*GUID*\>.txt. Ad esempio:
    
      - **MaxMimeTextHeaderLength**   Questo limite specifica il numero massimo di caratteri di testo utilizzabili in un'intestazione MIME. Il valore predefinito è 2000.
    
      - **MaxMimeSubjectLength**   Questo limite specifica il numero massimo di caratteri di testo utilizzabili nella riga dell'oggetto. Il valore predefinito è 255.
    
      - **MSize**   Questo limite specifica la dimensione massima per i messaggi. Il valore predefinito è 2147483647 byte.
    
      - **MaxMimeRecipients**   Questo limite specifica il numero totale di destinatari consentiti per i campi A, Cc e Ccn. Il valore predefinito è 12288.
    
      - **MaxRecipientPropertyLength**   Questo limite specifica il numero massimo di caratteri di testo utilizzabili come descrizione del destinatario. Il valore predefinito è 1000.
    
      - **MaxBodyPartsTotal**   Questo limite specifica il numero massimo di parti di messaggio utilizzabili in un messaggio multipart MIME. Il valore predefinito è 250.
    
      - **MaxEmbeddedMessageDepth**   Questo limite specifica il numero massimo di messaggi inoltrati che possono esistere in un messaggio. Il valore predefinito è 30.
    
    Per ulteriori informazioni sui limiti configurabili per le dimensioni dei messaggi utilizzati nel servizio di trasporto o nei server Trasporto Edge, vedere [Limiti di dimensione dei messaggi](message-size-limits-exchange-2013-help.md).

  - **Impossibile convertire un messaggio iCalendar in ingresso in una convocazione di riunione**   RFC 2445 definisce iCalendar come uno standard per lo scambio dei dati del calendario. Tra le cause specifiche dell'errore di conversione:
    
      - Uso non corretto di iCalendar da parte dell'agente mittente.
    
      - Costrutti di iCalendar non supportati dallo schema di calendario di Outlook o di Exchange.
    
    In caso di errori di conversione di iCalendar, il mittente non riceve un messaggio DSN 5.6.0, ma il messaggio viene recapitato con un file ICS allegato contenente il corpo del messaggio iCalendar.

  - **Errori causati da un'errata formattazione del messaggio MIME**   I messaggi commerciali indesiderati e altra posta indesiderata possono presentare errori di formattazione nell'intestazione del messaggio, ad esempio virgolette incomplete nelle descrizioni dei destinatari. Un numero molto inferiore di errori causati da un'errata formattazione dei messaggi MIME è considerato come un bug.

Gli errori della conversione del contenuto in uscita sono molto meno comuni degli errori in ingresso. Quando si verificano, gli errori in uscita sono causati generalmente da bug di codice di Exchange o da contenuto corrotto nel messaggio.

Inizio pagina


---
title: 'Miglioramenti alla segreteria telefonica preview: Exchange 2013 Help'
TOCTitle: Miglioramenti alla segreteria telefonica preview
ms:assetid: 1fcccec1-4edc-40b8-948c-111647d7d770
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150501(v=EXCHG.150)
ms:contentKeyID: 50480205
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Miglioramenti alla segreteria telefonica preview

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-07-05_

Anteprima messaggio vocale è una funzionalità disponibile per gli utenti che utilizzano la messaggistica unificata di Exchange Server 2010 o Exchange Server 2013 per ricevere i messaggi vocali. Anteprima messaggio vocale migliora le funzionalità esistenti della casella vocale di messaggistica unificata offrendo una versione di testo delle registrazioni audio. Il testo del messaggio vocale viene visualizzato in un messaggio di posta elettronica in Microsoft Office Outlook Web App, Outlook 2010 e altri programmi di posta.

## Miglioramenti all'anteprima dei messaggi vocali

In Exchange 2013, la messaggistica unificata include numerosi miglioramenti all'interfaccia utente dei client Outlook Web App e Outlook e ai livelli di precisione e accuratezza dell'anteprima dei messaggi vocali. Inoltre, Microsoft Speech Platform (Versione 11.0) e Unified Communications Managed API (UCMA) 4.0 forniscono ulteriori miglioramenti ai servizi vocali grazie a una generazione avanzata della grammatica e al supporto di un maggior numero di lingue.

La messaggistica unificata ha introdotto la funzionalità Anteprima messaggio vocale in Exchange 2010. Anteprima messaggio vocale utilizza il riconoscimento vocale automatico per aggiungere una versione di testo del file audio di un messaggio vocale. Il riconoscimento vocale automatico non è preciso al 100%, soprattutto quando viene utilizzato per registrare un messaggio audio con voci sconosciute e rumori.

Alcune organizzazioni richiedono trascrizioni dei messaggi vocali che siano completamente o quasi completamente prive di errori per alcuni, se non tutti, i loro utenti. Il programma partner Anteprima messaggio vocale consente alle organizzazioni di questo tipo di soddisfare tali requisiti. Il programma partner Anteprima messaggio vocale era stato messo a punto per Exchange 2010 per migliorare i risultati offerti da Anteprima messaggio vocale, ma non veniva utilizzato dagli utenti di Exchange 2010 a causa dei costi diretti e indiretti che implicava. Per risolvere questi problemi, in Exchange 2013 sono presenti i seguenti miglioramenti per Anteprima messaggio vocale:

  - **Migliore normalizzazione audio**   La normalizzazione dell'audio è il processo che aumenta (o diminuisce) in modo uniforme l'ampiezza di un intero segnale audio in modo che l'ampiezza di picco risultante corrisponda a un valore specificato o alla norma. La messaggistica unificata normalizza la registrazione audio prima di comprimerla e inviarla all'utente.

  - **Riconoscimento vocale avanzato**   Tramite la raccolta dei messaggi vocali (eseguita solo se l'utente di Exchange sceglie di condividere queste informazioni), i risultati delle anteprime dei messaggi vocali possono essere utilizzati per aggiungere parole e frasi al motore vocale. Per fare ciò, impostare il parametro *VoiceMailAnalysisEnabled* su `$true` tramite il cmdlet **Set-UMMailbox** oppure il parametro *AllowVoiceMailAnalysis* su `$true` tramite il cmdlet **Set-UMMailboxPolicy**. Inoltre, la messaggistica unificata di Exchange 2013 utilizza in modo più efficiente le informazioni ottenute dai thread di posta elettronica creati da un utente tramite Outlook Voice Access. Queste informazioni includono dati (Active Directory o contatto personale) sul partecipante (paese, città, azienda) e il numero telefonico dell'utente di Outlook Voice Access.

  - **Attendibilità dell'anteprima del messaggio vocale**   Il grado di attendibilità è il numero assegnato dalla messaggistica unificata ed è direttamente correlato alla precisione della trascrizione. I calcoli effettuati dalla messaggistica unificata per stabilire questo valore sono stati corretti affinché risultassero più precisi e rispecchiassero il grado di precisione del messaggio trascritto.

  - **Filtro**   Le eventuali parole offensive o inappropriate vengono individuate e filtrate e i risultati vengono inseriti nella cache e archiviati nella cassetta postale dell'utente.

  - **Mancata visualizzazione dell'anteprima**   Se il grado di attendibilità dell'anteprima di un messaggio vocale è inferiore a una data soglia, il testo dell'anteprima viene nascosto. Se il testo è nascosto, il messaggio vocale includerà un messaggio che informa l'utente che il grado di attendibilità era troppo basso per visualizzare il risultato ottenuto.

  - **Prestazioni della trascrizione**   L'anteprima dei messaggi vocali è un'operazione che richiede un notevole dispendio a livello di CPU e impiega circa il doppio del tempo necessario per elaborare un file audio. Se la creazione dell'anteprima del messaggio vocale richiede troppo tempo, la limitazione della CPU arresta l'elaborazione dell'anteprima. In Exchange 2010, la messaggistica unificata non tentava di trascrivere i messaggi vocali che superavano i 75 secondi. In Exchange 2013, l'intero messaggio vocale viene trascritto, ma il testo del messaggio non viene incluso se supera i 75 secondi.

  - **Schema dei colori**   A causa della confusione dei colori utilizzati per individuare i diversi gradi di affidabilità dell'anteprima dei messaggi vocali, lo schema dei colori è stato rimosso in Exchange 2013 per Outlook Web App e Outlook.


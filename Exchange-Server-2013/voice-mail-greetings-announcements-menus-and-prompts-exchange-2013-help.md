---
title: 'Messaggi di saluto, gli annunci, menu e prompt: Exchange 2013 Help'
TOCTitle: Messaggi di saluto, gli annunci, menu e prompt
ms:assetid: df61105d-c9d8-452c-b028-50cbda47aecf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124902(v=EXCHG.150)
ms:contentKeyID: 54652889
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Messaggi di saluto, gli annunci, menu e prompt

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2015-03-09_

Con la messaggistica unificata viene installato un insieme comune di file audio predefiniti utilizzati per il sistema di caselle vocali, le istruzioni di menu, i messaggi di saluto e gli annunci informativi. Anche se è possibile creare una operatore automatico o un dial plan di messaggistica unificata completamente funzionale che utilizzi solo le istruzioni audio predefinite, per molte aziende tali istruzioni sono troppo generiche per servire da interfaccia pubblica accettabile. In questo argomento vengono descritti i prompt di sistema e le istruzioni di menu, i messaggi di saluto e gli annunci informativi utilizzati dai dial plan e dagli operatori automatici di messaggistica unificata, nonché il loro utilizzo quando i chiamanti accedono al sistema di caselle vocali.

**Sommario**

Overview of audio prompts and greetings

System prompts

UM dial plan greetings and announcements

UM auto attendant greetings, announcements, and menu prompts

Customizing greetings, announcements, and menu prompts

## Panoramica delle istruzioni audio e dei messaggi di saluto

Dopo l'installazione della messaggistica unificata, i file audio per i dial plan e gli operatori automatici di messaggistica unificata vengono copiati nel server Cassette postali. Per impostazione predefinita, il programma di installazione copia i file audio nella cartella Programmi\\Microsoft\\Exchange Server\\V15\\Unified Messaging\\Prompts*\\\<lingua\>*. Se è installata la versione Inglese (Stati Uniti), durante l'installazione verrà creata una cartella denominata \\en in cui vengono conservate le versioni in inglese dei prompt di sistema. Il server Cassette postali riproduce tali prompt ai chiamanti per consentire loro di ascoltare messaggi di saluto, istruzioni di menu e annunci informativi e di navigare nei menu di messaggistica unificata.

I file audio del sistema o prompt non devono mai essere sostituiti. Tuttavia, la messaggistica unificata consente di personalizzare le formule di benvenuto dei dial plan e degli operatori automatici di messaggistica unificata, le istruzioni di menu principali e gli annunci informativi.

Nella seguente tabella sono elencati le istruzioni e i messaggi di saluto utilizzati con i dial plan di messaggistica unificata.

### Istruzioni audio per i dial plan di messaggistica unificata

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Istruzioni e messaggi di saluto</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Prompt di sistema</p></td>
<td><p>Da non modificare.</p></td>
</tr>
<tr class="even">
<td><p>Formula di benvenuto</p></td>
<td><p>La formula di benvenuto predefinita è un prompt di sistema che viene eseguito per impostazione predefinita. L'utente può comunque utilizzare un messaggio di saluto personalizzato di sua creazione.</p></td>
</tr>
<tr class="odd">
<td><p>Annuncio informativo</p></td>
<td><p>Per impostazione predefinita, gli annunci informativi sono disabilitati. Se si abilita un annuncio informativo, è necessario specificare un messaggio di saluto personalizzato.</p></td>
</tr>
</tbody>
</table>


Nella seguente tabella sono elencati le istruzioni e i messaggi di saluto utilizzati con gli operatori automatici di messaggistica unificata.

### Istruzioni audio per gli operatori automatici di messaggistica unificata

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Istruzioni e messaggi di saluto</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Prompt di sistema</p></td>
<td><p>Da non modificare.</p></td>
</tr>
<tr class="even">
<td><p>Istruzioni di menu per gli orari di ufficio</p></td>
<td><p>Per impostazione predefinita, le istruzioni di menu per gli orari di ufficio sono disabilitate e viene eseguito un prompt di sistema. L'utente può comunque utilizzare un messaggio di saluto personalizzato di sua creazione.</p></td>
</tr>
<tr class="odd">
<td><p>Istruzioni di menu per altri orari</p></td>
<td><p>Per impostazione predefinita, le istruzioni di menu per altri orari sono disabilitate e viene riprodotto un prompt di sistema. L'utente può comunque utilizzare un messaggio di saluto personalizzato di sua creazione.</p></td>
</tr>
<tr class="even">
<td><p>Messaggio di saluto Orario di ufficio</p></td>
<td><p>Per impostazione predefinita, viene abilitato un messaggio di saluto per l'orario di ufficio e viene eseguito un prompt di sistema. L'utente può comunque utilizzare un messaggio di saluto personalizzato di sua creazione. Questo messaggio è denominato anche formula di benvenuto.</p></td>
</tr>
<tr class="odd">
<td><p>Messaggio di saluto Orario non di ufficio</p></td>
<td><p>Per impostazione predefinita, viene abilitato un messaggio di saluto per l'orario non di ufficio e viene eseguito un prompt di sistema. L'utente può comunque utilizzare un messaggio di saluto personalizzato di sua creazione. Questo messaggio è denominato anche formula di benvenuto.</p></td>
</tr>
<tr class="even">
<td><p>Annuncio informativo</p></td>
<td><p>Per impostazione predefinita, gli annunci informativi sono disabilitati. Se si abilita un annuncio informativo, è necessario specificare un messaggio di saluto personalizzato.</p></td>
</tr>
</tbody>
</table>



> [!WARNING]
> La modifica dei prompt di sistema installati non è supportata.



Inizio pagina

## Prompt di sistema

La messaggistica unificata viene installata con un insieme di istruzioni audio predefinite da utilizzate con Outlook Voice Access, dial plan e operatori automatici. Per ciascuna lingua vengono installati sul server di Cassette postali centinaia di prompt di sistema. Il server Cassette postali riproduce i file audio di tali prompt quando i chiamanti accedono al sistema di caselle postali. Di seguito sono riportati alcuni esempi di questi prompt di sistema:

  - "Inserire il PIN."

  - "Immettere l'interno per accedere alla cassetta postale."

  - "Per contattare qualcuno, premere il tasto \#."

  - "Sillabare il nome della persona chiamata, iniziando dal cognome."

  - "Per raggiungere una determinata persona, è sufficiente pronunciarne il nome."


> [!WARNING]
> La modifica dei prompt di sistema installati non è supportata.




> [!NOTE]
> Quando il servizio Messaggistica unificata viene avviato sul server Cassette postali, verrà eseguito un controllo per verificare che tutti i prompt di sistema siano disponibili. Nel caso in cui un prompt di sistema non venga trovato, verrà restituito un errore di messaggistica unificata. Per risolvere l'errore, individuare l'evento utilizzando Visualizzatore eventi e copiare il file elencato nella finestra <STRONG>Proprietà evento</STRONG> dal DVD di installazione nell'apposita cartella sul server Cassette postali.



## Messaggi di saluto e annunci dei dial plan di messaggistica unificata

Una volta installato il ruolo server Cassette postali e creato un dial plan di messaggistica unificata, è possibile utilizzare i file audio per i prompt di sistema predefiniti creati durante l'installazione oppure creare file audio personalizzati da utilizzare con i dial plan di messaggistica unificata.

I dial plan di messaggistica unificata hanno un messaggio di saluto e un annuncio informativo opzionale che possono essere modificati. La formula di benvenuto viene utilizzata quando un utente di Outlook Voice Access o un altro chiamante effettua una chiamata al numero accesso sottoscrittore. I chiamanti ascoltano una formula di benvenuto predefinita che dice, "Benvenuti, siete connessi a Microsoft Exchange." È possibile sostituire questa formula predefinita con una specifica per la propria società, ad esempio "Benvenuti in Outlook Voice Access per Woodgrove Bank". Se si decide di personalizzare la formula, è necessario registrare la formula personalizzata, salvarla come file .wav, quindi configurare il dial plan affinché la utilizzi.

La messaggistica unificata consente di far seguire un annuncio informativo alla formula di benvenuto. Per impostazione predefinita non è configurato nessun annuncio informativo. Tuttavia, è possibile che si desideri metterne uno a disposizione dei chiamanti. L'annuncio informativo viene utilizzato per annunci generici che cambiano con maggior frequenza rispetto alla formula di benvenuto, oppure per annunci richiesti dai criteri di conformità aziendali. Quando è importante che venga ascoltato l'intero messaggio informativo, è possibile configurarlo in modo che non venga interrotto. In questo modo si evita che i chiamanti premano un tasto o pronuncino un comando per interrompere e arrestare l'annuncio informativo.

Nella seguente tabella sono descritti i messaggi di saluto e gli annunci informativi dei dial plan di messaggistica unificata.

### Messaggi di saluto e annunci informativi dei dial plan di messaggistica unificata

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Messaggio di saluto</th>
<th>Esempio predefinito</th>
<th>Esempio personalizzato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Formula di benvenuto</p></td>
<td><p>&quot;Benvenuti, siete connessi a Microsoft Exchange.&quot;</p></td>
<td><p>&quot;Benvenuti in Outlook Voice Access della Woodgrove Bank.&quot;</p></td>
</tr>
<tr class="even">
<td><p>Annuncio informativo</p></td>
<td><p>Per impostazione predefinita, non è stato configurato alcun messaggio informativo.</p></td>
<td><p>&quot;Utilizzando il sistema, lei accetta di attenersi a tutti i criteri aziendali relativi all'accesso al sistema.&quot;</p></td>
</tr>
</tbody>
</table>


Quando si personalizzano e si configurano i messaggi di saluto e gli annunci, verificare che l'impostazione della lingua configurata sul dial plan di messaggistica unificata sia la stessa della lingua delle istruzioni personalizzate create dall'utente. In caso contrario, un chiamante può ascoltare un messaggio o un saluto in una lingua e un altro messaggio o saluto in una lingua diversa.

Inizio pagina

## Messaggi di saluto, annunci e istruzioni di menu di messaggistica unificata

Come avviene con i dial plan di messaggistica unificata, gli operatori automatici di messaggistica unificata hanno una formula di benvenuto, un annuncio informativo opzionale e un'istruzione di menu personalizzata opzionale. È possibile configurare diverse versioni delle formule di benvenuto e delle istruzioni di menu per l'orario di ufficio e non di ufficio. Tutte queste formule possono essere modificate.

La formula di benvenuto è il primo messaggio che un chiamante ascolta quando un operatore automatico di messaggistica unificata risponde alla chiamata. Per impostazione predefinita, si sentirà il messaggio: "Benvenuti nell'operatore automatico di Microsoft Exchange." Il file audio che viene eseguito durante la chiamata è il prompt di sistema predefinito per l'operatore automatico di messaggistica unificata. Tuttavia è possibile fornire un messaggio di saluto alternativo specifico per l'azienda, ad esempio "Grazie per avere chiamato Woodgrove Bank". Se si decide di personalizzare la formula, è necessario registrare la formula personalizzata, salvarla come file .wav, quindi configurare l'operatore automatico affinché la utilizzi. Anche i prompt di menu possono essere personalizzati, come avviene per le formule di benvenuto.

Il servizio di messaggistica unificata consente la riproduzione di un annuncio informativo dopo il messaggio di saluto per l'orario di ufficio o non di ufficio. Per impostazione predefinita, non è configurato alcun annuncio informativo, sebbene sia possibile predisporne uno per i chiamanti. L'annuncio informativo potrebbe indicare l'orario lavorativo settimanale dell'azienda, ad esempio: "I nostri uffici sono aperti dalle 8,00 alle 17,00, dal lunedì al venerdì, e dalle 8,30 alle 13 il sabato". L'annuncio informativo può anche fornire informazioni richieste per la conformità con i criteri dell'azienda; ad esempio: "È possibile che le chiamate siano monitorate a scopo formativo." Quando è importante che venga ascoltato l'intero messaggio informativo, è possibile configurarlo in modo che non venga interrotto. In questo modo si evita che i chiamanti premano un tasto o pronuncino un comando per interrompere e arrestare l'annuncio informativo.

Nella seguente tabella sono descritti i messaggi di saluto e gli annunci informativi degli operatori automatici di messaggistica unificata.

### Messaggi di saluto, annunci informativi e istruzioni di menu dell'operatore automatico di messaggistica unificata

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Messaggio di saluto</th>
<th>Esempio predefinito</th>
<th>Esempio personalizzato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Messaggio di saluto Orario di ufficio</p></td>
<td><p>&quot;Benvenuti nell'operatore automatico di Microsoft Exchange.&quot;</p></td>
<td><p>&quot;Grazie per avere chiamato la Woodgrove Bank.&quot;</p></td>
</tr>
<tr class="even">
<td><p>Messaggio di saluto Orario non di ufficio</p></td>
<td><p>Non vengono eseguiti messaggi di saluto predefiniti per l'orario non di ufficio, a meno che non venga configurato l'orario di ufficio per l'operatore automatico. Il messaggio di saluto per l'orario di ufficio viene comunque eseguito in ogni momento della giornata.</p></td>
<td><p>&quot;In questo momento gli uffici della Woodgrove Bank sono chiusi. I nostri uffici sono aperti dalle 8 alle 17, dal lunedì al venerdì.&quot;</p></td>
</tr>
<tr class="odd">
<td><p>Annuncio informativo</p></td>
<td><p>Per impostazione predefinita, gli annunci informativi non sono configurati.</p></td>
<td><p>&quot;È possibile che le chiamate siano monitorate a scopo di formazione del personale.&quot;</p></td>
</tr>
<tr class="even">
<td><p>Prompt menu principale Orario di ufficio</p></td>
<td><p>Fino a quando non viene configurata un'associazione di tasti sull'operatore automatico, non verranno riprodotte istruzioni di menu principali per l'orario di ufficio predefinite.</p></td>
<td><p>&quot;Per il supporto tecnico, premere o dire 1. Per gli uffici e l'amministrazione, premere o dire 2. Per l'ufficio vendite, premere o dire 3.&quot;</p></td>
</tr>
<tr class="odd">
<td><p>Istruzione di menu principale per orario non di ufficio</p></td>
<td><p>Fino a quando non viene configurata un'associazione di tasti e l'orario di ufficio sull'operatore automatico, non verranno riprodotte istruzioni di menu principali per l'orario non di ufficio predefinite.</p></td>
<td><p>&quot;La ringraziamo per la sua chiamata. Tuttavia, in questo momento gli uffici della Woodgrove Bank sono chiusi. Se desidera lasciare un messaggio, prema o dica 1. Provvederemo a ricontattarla non appena possibile.&quot;</p></td>
</tr>
</tbody>
</table>


Come avviene con i dial plan di messaggistica unificata, verificare che l'impostazione della lingua configurata nell'operatore automatico di messaggistica unificata sia la stessa della lingua dei messaggi di saluto personalizzati creati e che venga configurata la stessa lingua del dial plan di messaggistica unificata. In caso contrario, un chiamante può ascoltare un messaggio o un saluto in una lingua e un altro messaggio o saluto in una lingua diversa.

Inizio pagina

## Personalizzazione dei messaggi di saluto, degli annunci, delle istruzioni di menu e dei menu di navigazione

Sebbene i prompt di sistema non debbano essere sostituiti o modificati, è possibile personalizzare i messaggi di saluto, gli annunci informativi, le istruzioni di menu e i menu di navigazione utilizzati con i dial plan e gli operatori automatici di messaggistica unificata. Dopo l'installazione, è possibile configurare i dial plan di messaggistica unificata e gli operatori automatici per l'uso di file audio personalizzati (.wav or .wma). Prima di poter abilitare le istruzioni vocali personalizzate per i chiamanti, è necessario eseguire le seguenti operazioni:

1.  Registrare i messaggi di saluto, gli annunci e le istruzioni personalizzate e salvarli come file WAV. Per codificare i file WAV è necessario utilizzare il codec audio Linear PCM (16 bit/campione) a 8 kHz. Se non si utilizza questo formato specifico per i file .wav, verrà generato un errore indicante che il formato del file di origine non è supportato. Sebbene venga generato, l'errore non viene visualizzato nel Visualizzatore eventi.

2.  Configurare il dial plan o l'operatore automatico di messaggistica unificata per l'utilizzo di messaggi di saluto, annunci e istruzioni personalizzate.

Per impostazione predefinita, quando si crea un operatore automatico di messaggistica unificata i prompt o i messaggi di saluto per l'orario di ufficio e non di ufficio non sono configurati e non è stato definito il mapping dei tasti per le istruzioni del menu principale dell'orario di ufficio o non di ufficio. Per configurare correttamente i messaggi di saluto personalizzati per un operatore automatico, è necessario:

  - Configurare l'orario di ufficio e non di ufficio dalla pagina **Orario di ufficio**.

  - Creare i file audio (.wav o .wma) dei messaggi di saluto da utilizzare per l'orario di ufficio e non di ufficio.

  - Configurare le formule di benvenuto per gli orari di ufficio e non di ufficio nella pagina **Messaggi di saluto**.

  - Creare i file dei messaggi di saluto da utilizzare per i messaggi di saluto dell'istruzione di menu principale dell'orario di ufficio e non di ufficio.

  - Configurare i messaggi si saluto delle istruzioni di menu principali per gli orari di ufficio e non di ufficio nella pagina **Messaggi di saluto**.

  - Abilitare e configurare la navigazione dei menu negli orari di ufficio e non di ufficio nella pagina **Navigazione dei menu**.

Inizio pagina


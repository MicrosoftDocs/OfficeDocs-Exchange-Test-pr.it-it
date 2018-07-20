---
title: 'Conversione del contenuto: Exchange 2013 Help'
TOCTitle: Conversione del contenuto
ms:assetid: bc367eb3-0306-4da9-9a84-4341caef77af
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232174(v=EXCHG.150)
ms:contentKeyID: 50481521
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conversione del contenuto

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

La *conversione del contenuto* è il processo che consente di formattare correttamente un messaggio in base al destinatario. La decisione di eseguire la conversione del contenuto su un messaggio dipende dalla destinazione e dal formato del messaggio in fase di elaborazione. In Microsoft Exchange Server 2013 sono presenti due diversi tipi di conversione del contenuto:

  - **Conversione dei messaggi per i destinatari esterni**   Questo tipo di conversione del contenuto include le opzioni di conversione TNEF (Transport Neutral Encapsulation Format) e le opzioni di codifica dei messaggi per i destinatari esterni. I messaggi inviati ai destinatari all'interno dell'organizzazione di Exchange non richiedono questo tipo di conversione del contenuto. Questo tipo di conversione del contenuto viene gestito dal classificatore nel servizio Trasporto sul server Cassette postali. La classificazione di ogni messaggio avviene non appena un nuovo messaggio viene inserito nella coda di invio. Sul messaggio, oltre alla risoluzione dei destinatari e del routing e prima del suo inserimento nella coda di recapito, viene eseguita la conversione del contenuto. Se un singolo messaggio contiene più destinatari, il classificatore del contenuto determina la codifica appropriata per ciascun destinatario dei messaggi. Questa funzionalità non acquisisce alcun errore di conversione del contenuto rilevato dal classificatore durante la conversione di messaggi inviati a destinatari esterni.

  - **Conversione MAPI per destinatari interni**   Questo tipo di conversione del contenuto viene gestito dal servizio Trasporto cassette postali. Il servizio Trasporto cassette postali è presente nei server Cassette postali per trasmettere i messaggi tra i database delle cassette postali sul server locale e il servizio Trasporto nei server Cassette postali. In modo particolare il servizio Invio Trasporto cassette postali trasmette i messaggi dalla casella della posta in uscita del mittente al servizio Trasporto su un server Cassette postali. Il servizio Recapito Trasporto cassette postali trasmette i messaggi dal servizio Trasporto su un server Cassette postali alla casella di posta in arrivo del destinatario. Il servizio Invio Trasporto cassette postali converte tutti i messaggi in uscita da MAPI e il servizio Recapito Trasporto cassette postali converte tutti i messaggi in entrata in MAPI. L'analisi della conversione del contenuto consente di acquisire questi errori di conversione MAPI. Per ulteriori informazioni, vedere [Traccia di conversione del contenuto](content-conversion-tracing-exchange-2013-help.md).

Questo argomento illustra le opzioni di conversione dei messaggi per i destinatari esterni.

**Sommario**

Exchange and Outlook message formats

Content conversion options for external recipients

Understanding the structure of email messages

## Formati di messaggio di Exchange e Outlook

Nel seguente elenco sono descritti i formati di base dei messaggi disponibili in Exchange e Microsoft Outlook:

  - **Testo normale**   Un messaggio di testo normale utilizza solo testo US-ASCII come descritto in RFC 2822. Il messaggio non può contenere caratteri diversi o altri formati di testo. Per un messaggio di testo normale possono essere utilizzati i seguenti due formati:
    
      - Le intestazioni e il corpo dei messaggi sono costituiti da testo US-ASCII. Gli allegati devono essere codificati con *Uuencode*. Uuencode è l'abbreviazione di "Unix-to-Unix encoding" e definisce un algoritmo di codifica che consente di memorizzare allegati binari nel corpo di un messaggio di posta elettronica utilizzando caratteri di testo US-ASCII.
    
      - Il messaggio è codificato in base allo standard MIME con text/plain come valore Content-Type e 7bit come valore Content-Transfer-Encoding per le parti di testo di un messaggio costituito da più parti. Tutti gli allegati sono codificati con Quoted-Printable o Base64. Per impostazione predefinita, quando si compone e invia un messaggio di testo normale in Outlook, il messaggio è codificato in base allo standard MIME con text/plain come valore Content-Type.

  - **HTML**   Un messaggio HTML supporta la formattazione di testo, immagini in background, tabelle, elenchi puntati e altri elementi grafici. Per definizione, un messaggio in formato HTML deve esse codificato in base allo standard MIME per preservare questi elementi di formattazione.

  - **RTF (Rich Text Format)**   Il formato RTF supporta la formattazione del testo e altri elementi grafici. RTF è sinonimo di TNEF. TNEF e RTF possono essere utilizzati in modo intercambiabile. Il formato RTF dei messaggi è completamente diverso dal formato RTF dei documenti disponibile in Microsoft Word.
    
    Solo Outlook e pochi altri client di posta elettronica MAPI sono in grado di leggere i messaggi RTF.

  - **TNEF**   TNEF (Transport Neutral Encapsulation Format) è un formato specifico di Microsoft per l'incapsulamento delle proprietà dei messaggi MAPI. Un messaggio TNEF contiene una versione di testo normale del messaggio e un allegato binario che riunisce la versione formattata originale del messaggio. In genere questo allegato è denominato Winmail.dat e contiene le seguenti informazioni:
    
      - La versione formattata originale del messaggio, comprensiva ad esempio di tipi di carattere, dimensioni del testo e colori del testo
    
      - Gli oggetti OLE inclusi, ad esempio, le immagini incorporate o i documenti di Microsoft Office incorporati
    
      - Funzionalità speciali di Outlook, compresi ad esempio moduli personalizzati, pulsanti di voto o convocazioni di riunione
    
      - Allegati normali che si trovavano nel messaggio originale
    
    Il messaggio di testo normale risultante può essere rappresentato nei seguenti formati:
    
      - Un messaggio conforme a RFC 2822 composto solo da testo US-ASCII con un allegato Winmail.dat con codifica Uuencode
    
      - Un messaggio con codifica MIME multipart con un allegato Winmail.dat
    
    Un client di posta elettronica conforme a MAPI che legge perfettamente il formato TNEF, ad esempio Outlook, elabora l'allegato Winmail.dat e visualizza il contenuto del messaggio originale senza visualizzare l'allegato Winmail.dat. Un client di posta elettronica che non legge il formato TNEF può presentare un messaggio TNEF nei seguenti modi:
    
      - Viene visualizzata la versione di testo normale del messaggio, e il messaggio contiene un allegato denominato Winmail.dat, Win.dat o con altri nomi generici come Att*nnnnn*.dat o Att*nnnnn*.eml in cui il segnaposto *nnnnn* rappresenta un numero casuale.
    
      - Viene visualizzata la versione di testo normale del messaggio, mentre l'allegato TNEF viene ignorato o rimosso. Ne risulta un messaggio di testo normale.
    
      - I server di messaggistica che leggono il formato TNEF possono essere configurati per la rimozione degli allegati TNEF dai messaggi in arrivo. Ne risulta un messaggio di testo normale. Inoltre, alcuni client di posta elettronica come Microsoft Outlook Express possono non riuscire a leggere il formato TNEF, ma sono in grado di riconoscere e ignorare gli allegati in tale formato. Ne risulta un messaggio di testo normale.
    
    Alcune utilità di terze parti sono in grado di convertire gli allegati Winmail.dat.
    
    TNEF viene letto da tutte le versioni di Exchange a partire da Exchange Server versione 5.5.

  - **STNEF (Summary Transport Neutral Encapsulation Format)**   STNEF equivale a TNEF. Tuttavia, i messaggi STNEF sono codificati in modo diverso rispetto ai messaggi TNEF. In particolare, i messaggi STNEF sono sempre codificati in base allo standard MIME e come valore di Content-Transfer-Encoding utilizzano sempre Binary. Quindi non è presente alcuna rappresentazione in testo normale del messaggio e il corpo del messaggio non contiene alcun allegato Winmail.dat distinto. L'intero messaggio è rappresentato utilizzando solo dati binari. I messaggi che utilizzano Binary come valore di Content-Transfer-Encoding possono essere trasferiti solo tra server di messaggistica SMTP che supportano e annunciano le estensioni SMTP BINARYMIME e CHUNKING secondo quanto definito in RFC 3030. I messaggi vengono trasferiti tra i server di messaggistica SMTP utilizzando sempre il comando BDAT, al posto del comando DATA standard.
    
    STNEF viene letto da tutte le versioni di Exchange a partire da Exchange 2000. STNEF viene utilizzato automaticamente per tutti i messaggi trasferiti tra server di Exchange nell'organizzazione a partire dalla modalità nativa di Exchange Server 2003.
    
    Exchange non invia mai messaggi STNEF a destinatari esterni. Solo i messaggi TNEF possono essere inviati a destinatari esterni all'organizzazione di Exchange.

Inizio pagina

## Opzioni di conversione del contenuto per destinatari esterni

Le opzioni di conversione del contenuto impostabili in un'organizzazione di Exchange possono essere raggruppate nelle seguenti categorie:

  - **Opzioni di conversione TNEF**   Queste opzioni di conversione specificano se mantenere o rimuovere TNEF dai messaggi in uscita dall'organizzazione di Exchange.

  - **Opzioni di codifica dei messaggi**   Queste opzioni specificano le opzioni di codifica dei messaggi, ad esempio set di caratteri MIME e non MIME, la codifica dei messaggi e i formati degli allegati.

Queste opzioni di conversione e codifica sono indipendenti le une dalle altre. Ad esempio, l'uscita dei messaggi TNEF dall'organizzazione di Exchange non è legata alle impostazioni di codifica MIME o di testo normale di tali messaggi.

È possibile specificare la conversione del contenuto nei vari livelli dell'organizzazione di Exchange come descritto nell'elenco seguente:

  - **Impostazioni dei domini remoti**   I domini remoti definiscono le impostazioni per i trasferimenti dei messaggi in uscita tra l'organizzazione di Exchange e i domini esterni. Anche se non si creano voci del dominio remoto per domini specifici, esiste un dominio remoto predefinito, denominato Predefinito, che si applica a tutti gli spazi degli indirizzi remoti (\*).

  - **Impostazioni dell'utente di posta e del contatto di posta**   Gli utenti di posta somigliano ai contatti di posta: entrambi hanno indirizzi di posta elettronica esterni e contengono informazioni su persone esterne all'organizzazione di Exchange. La differenza principale è che gli utenti di posta possono essere utilizzati per accedere al dominio Active Directory e alle risorse nell'organizzazione.

  - **Impostazioni di Outlook**   In Outlook è possibile impostare le opzioni di formattazione e codifica dei messaggi descritte nell'elenco seguente:
    
      - **Formato del messaggio**   È possibile impostare il formato predefinito per tutti i messaggi. Inoltre, quando si compone un messaggio specifico, è possibile ignorare il formato predefinito.
    
      - **Formato del messaggio Internet**   È possibile controllare l'invio dei messaggi TNEF a destinatari remoti oppure la loro preventiva conversione in un formato più compatibile. Inoltre, è possibile specificare diverse opzioni di codifica per i messaggi inviati a destinatari remoti. Queste impostazioni non si applicano ai messaggi inviati ai destinatari nell'organizzazione di Exchange.
    
      - **Formato del messaggio per destinatari Internet**   È possibile controllare l'invio dei messaggi TNEF a destinatari specifici oppure la loro preventiva conversione in un formato più compatibile. Durante la composizione di un messaggio è possibile impostare le opzioni di conversione per contatti specifici nella propria cartella Contatti e ignorare le opzioni di conversione per un destinatario specifico nei campi A, Cc o Ccn. Queste opzioni di conversione non sono disponibili per i destinatari nell'organizzazione di Exchange.
    
      - **Opzioni di codifica dei messaggi per destinatari Internet**   È possibile controllare le opzioni di codifica MIME o di testo normale per contatti specifici nella propria cartella Contatti e ignorare le opzioni di conversione per un destinatario specifico nei campi A, Cc o Ccn durante la composizione di un messaggio. Queste opzioni di conversione non sono disponibili per i destinatari nell'organizzazione di Exchange.
    
      - **Opzioni internazionali**   È possibile controllare i set di caratteri utilizzati nei messaggi.

## Opzioni di conversione TNEF

È possibile specificare le opzioni di conversione TNEF nei seguenti livelli:

  - Impostazioni del dominio remoto

  - Impostazioni dell'utente di posta e del contatto di posta

  - Impostazioni di Outlook, tra cui:
    
      - Formato del messaggio
    
      - Formato del messaggio Internet
    
      - Formato del messaggio per destinatari Internet

## Opzioni di codifica dei messaggi

È possibile specificare le opzioni di codifica dei messaggi nei seguenti livelli:

  - Impostazioni del dominio remoto

  - Impostazioni dell'utente di posta e del contatto di posta

  - Impostazioni di Outlook, tra cui:
    
      - Formato del messaggio
    
      - Messaggio Internet
    
      - Formato del messaggio per destinatari Internet
    
      - Opzioni di codifica del set di caratteri del messaggio

Per ulteriori informazioni, vedere [Opzioni di codifica dei messaggi](message-encoding-options-exchange-2013-help.md).

Inizio pagina

## Concetti relativi alla struttura dei messaggi di posta elettronica

Per comprendere meglio le opzioni di conversione del contenuto per i destinatari esterni, è necessario comprendere la struttura dei messaggi di posta elettronica. Un messaggio SMTP si basa su testo normale in formato US-ASCII a 7 bit per la composizione e l'invio di messaggi di posta elettronica. Un messaggio SMTP standard è costituito dai seguenti elementi:

  - **Busta del messaggio**   La busta del messaggio è definita in RFC 2821. Contiene le informazioni necessarie per trasmettere e recapitare il messaggio. I destinatari non vedono mai la busta del messaggio, perché viene generata dal processo di trasmissione del messaggio e non è parte integrante del contenuto.

  - **Contenuto del messaggio**   Il contenuto del messaggio è definito in RFC 2822. È composto dai seguenti elementi:
    
      - **Intestazione del messaggio**   L'intestazione del messaggio è un insieme di campi di intestazione. I campi di intestazione consistono di un nome di campo, seguito da due punti (:) e dal corpo del campo, e terminano con una combinazione di caratteri ritorno a capo/avanzamento riga (CR/LF).
        
        Un nome di campo deve essere composto da caratteri di testo US-ASCII stampabili, ad eccezione dei due punti (:). In particolare, sono consentiti i caratteri ASCII con valori compresi tra 33 e 57 e tra 59 e 126.
        
        Il corpo di un campo può essere composto da qualsiasi carattere in formato US-ASCII, ad eccezione dei caratteri di ritorno a capo (CR) e avanzamento riga (LF). Tuttavia, il corpo di un campo può contenere la combinazione di caratteri CR/LF quando è utilizzato in un'*intestazione su più righe*. L'intestazione su più righe corrisponde alla divisione del corpo di un singolo campo di intestazione in più righe, come descritto nella sezione 2.2.3 di RFC 2822. Altri requisiti di sintassi del corpo del campo sono descritti nelle sezioni 3 e 4 di RFC 2822.
    
      - **Corpo del messaggio**   Il corpo del messaggio è un insieme di righe di caratteri di testo US-ASCII visualizzate dopo l'intestazione del messaggio. L'intestazione e il corpo del messaggio sono separati da una riga vuota che termina con la combinazione di caratteri CR/LF. Il corpo del messaggio è facoltativo. Ciascuna riga di testo nel corpo del messaggio deve essere inferiore a 998 caratteri. I caratteri di ritorno a capo e avanzamento riga possono essere inseriti solo insieme per indicare la fine di una riga.

Quando i messaggi SMTP contengono elementi che non sono testo US-ASCII normale, il messaggio deve essere codificato per preservare tali elementi. Lo standard MIME definisce un metodo di codifica del contenuto diverso dal testo presente nei messaggi. MIME consente di utilizzare testo appartenente ad altri set di caratteri, allegati privi di testo, corpi di messaggi costituiti da più parti e campi di intestazione che utilizzano altri set di caratteri. MIME è definito in RFC 2045, RFC 2046, RFC 2047, RFC 2048 e RFC 2077. MIME definisce un insieme di campi di intestazione che specificano altri attributi dei messaggi. Nella seguente tabella vengono descritti alcuni campi di intestazione MIME importanti.

### Campi di intestazione MIME importanti

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome del campo di intestazione</th>
<th>Valore predefinito</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MIME-Version</p></td>
<td><p>1.0</p></td>
<td><p>Questo è il primo campo di intestazione MIME visualizzato in un messaggio in formato MIME. Viene visualizzato dopo gli altri campi di intestazione RFC 2822 standard e prima di qualsiasi altro campo di intestazione MIME. I client di posta elettronica basati su MIME utilizzano questo campo di intestazione per identificare un messaggio con codifica MIME. Se il campo di intestazione è assente, i client di posta elettronica basati su MIME identificano il messaggio come testo normale.</p></td>
</tr>
<tr class="even">
<td><p>Content-Type</p></td>
<td><p>text/plain</p></td>
<td><p>In questo campo di intestazione identifica il tipo di supporto del contenuto del messaggio, come descritto in RFC 2046. Un tipo di supporto è costituita da un tipo, un sottotipo e uno o più parametri facoltativi, ad esempio un parametro <em>charset=</em> che definisce la codifica dei caratteri MIME. Tipi che iniziano con &quot;x-&quot; non standard. I sottotipi che iniziano con &quot;vnd.&quot; sono specifico del fornitore. Internet assegnati numeri Authority (IANA) è presente un elenco di tipi di contenuto multimediale registrati. Per ulteriori informazioni, vedere <a href="https://www.iana.org/assignments/media-types/">Tipi di contenuto multimediale MIME</a>.</p>
<p>Il tipo di supporto <em>costituito da più parti</em> consente di inserire più parti del messaggio nello stesso messaggio utilizzando sezioni definite da tipi di supporti diversi. Alcuni valori possibili per il campo Content-Type sono text/plain, text/html, multipart/mixed e multipart/alternative.</p></td>
</tr>
<tr class="odd">
<td><p>Content-Transfer-Encoding</p></td>
<td><p>7bit</p></td>
<td><p>Questo campo di intestazione consente di descrivere le seguenti informazioni sul messaggio:</p>
<ul>
<li><p>L'algoritmo di codifica utilizzato per trasformare tutti i dati binari o di testo diversi da US-ASCII presenti nel corpo del messaggio.</p></li>
<li><p>Un indicatore della condizione corrente del corpo del messaggio.</p></li>
</ul>
<p>Possono essere presenti più valori per il campo di intestazione Content-Transfer-Encoding in un messaggio MIME. Se il campo di intestazione Content-Transfer-Encoding è presente nell'intestazione del messaggio, viene applicato all'intero corpo del messaggio. Se il campo di intestazione è presente solo in una parte di un messaggio costituito da più parti, viene applicato solo a quella determinata parte del messaggio.</p>
<p>Quando un algoritmo di codifica viene applicato ai dati del corpo del messaggio, i dati del corpo del messaggio vengono trasformati in testo US-ASCII normale. Questa trasformazione consente al messaggio di passare attraverso i server di messaggistica SMTP precedenti che supportano solo messaggi in formato di testo US-ASCII. I valori del campo di intestazione Content-Transfer-Encoding che indicano l'utilizzo di un algoritmo di codifica sul corpo del messaggio sono i seguenti:</p>
<ul>
<li><p><strong>Quoted-Printable</strong>   Questo algoritmo di codifica utilizza caratteri US-ASCII stampabili per codificare i dati del corpo del messaggio. Se il testo del messaggio originale è principalmente in formato US-ASCII, la codifica Quoted-Printable restituisce risultati alquanto compatti e leggibili. Tutti i caratteri di testo US-ASCII stampabili, ad eccezione del segno di uguale (=), possono essere rappresentati senza codifica.</p></li>
<li><p><strong>Base64</strong>   Questo algoritmo di codifica si basa principalmente sullo standard PEM (Privacy-Enhanced Mail) definito in RFC 1421. La codifica Base64 utilizza l'algoritmo di codifica con alfabeto a 64 caratteri e i caratteri di spaziatura interna di output definiti da PEM per codificare i dati del corpo del messaggio. Un messaggio con codifica Base64 è generalmente più grande del 33% rispetto all'originale. La codifica Base64 crea un aumento prevedibile nelle dimensioni dei messaggi ed è ottimale per i dati binari e il testo diverso da US-ASCII.</p></li>
</ul>
<p>Generalmente nello stesso messaggio non vengono utilizzati più algoritmi di codifica.</p>
<p>Se per il corpo del messaggio non è stato utilizzato alcun algoritmo di codifica, il campo di intestazione Content-Transfer-Encoding identifica solamente lo stato attuale dei dati del corpo del messaggio. I seguenti valori del campo di intestazione Content-Transfer-Encoding indicano che non è stato utilizzato alcun algoritmo di codifica sul corpo del messaggio:</p>
<ul>
<li><p><strong>7bit</strong>   Questo valore indica che i dati del corpo del messaggio sono già nel formato di RFC 2822. In particolare devono verificarsi le seguenti condizioni:</p>
<ul>
<li><p>Nessuna riga di testo deve superare 998 caratteri.</p></li>
<li><p>Tutti i caratteri devono essere nel formato di testo US-ASCII, con valori compresi tra 1 e 127.</p></li>
<li><p>I caratteri di ritorno a capo e avanzamento riga possono essere utilizzati solamente insieme per indicare la fine di una riga di testo.</p></li>
</ul>
<p>L'intero corpo del messaggio può utilizzare 7bit, oppure solo parte del corpo di un messaggio costituito da più parti può utilizzare 7bit. Se il messaggio costituito da più parti contiene altre parti con dati binari o testo diverso da US-ASCII, tali parti del messaggio devono essere codificate utilizzando gli algoritmi di codifica Quoted-Printable o Base64.</p>
<p>I messaggi con corpo 7bit possono essere trasmessi da un server di messaggistica SMTP all'altro utilizzando il comando DATA standard.</p></li>
<li><p><strong>8bit</strong>   Questo valore indica che i dati del corpo del messaggio contengono caratteri diversi da US-ASCII. In particolare devono verificarsi le seguenti condizioni:</p>
<ul>
<li><p>Nessuna riga di testo deve superare 998 caratteri.</p></li>
<li><p>Uno o più caratteri presenti nel corpo del messaggio hanno valori superiori a 127.</p></li>
<li><p>I caratteri di ritorno a capo e avanzamento riga possono essere utilizzati solamente insieme per indicare la fine di una riga di testo.</p></li>
</ul>
<p>L'intero corpo del messaggio può utilizzare 8bit, oppure solo parte del corpo di un messaggio costituito da più parti può utilizzare 8bit. Se il messaggio costituito da più parti contiene altre parti con dati binari, tali parti devono essere codificate utilizzando gli algoritmi di codifica Quoted-Printable o Base64.</p>
<p>I messaggi con corpo 8bit possono essere trasmessi solo tra server di messaggistica SMTP che supportano l'estensione SMTP 8BITMIME definita in RFC 1652, ad esempio i server su cui viene eseguito Exchange 2000 Server o versioni successive. In particolare devono verificarsi le seguenti condizioni:</p>
<ul>
<li><p>La parola chiave 8BITMIME deve essere annunciata nella risposta EHLO del server.</p></li>
<li><p>Il trasferimento dei messaggi avviene ancora con il comando DATA standard di SMTP. Tuttavia alla fine del comando MAIL FROM deve essere aggiunto il parametro BODY=8BITMIME.</p></li>
</ul></li>
<li><p><strong>Binary</strong>   Questo valore indica che il corpo del messaggio contiene dati binari o testo diverso da US-ASCII. In particolare si verificano le seguenti condizioni:</p>
<ul>
<li><p>Qualsiasi sequenza di caratteri è consentita.</p></li>
<li><p>Nessuna limitazione di lunghezza delle righe.</p></li>
<li><p>Gli elementi del messaggio binario non richiedono alcuna codifica.</p></li>
</ul>
<p>I messaggi con corpo 8bit possono essere trasmessi solo tra server di messaggistica SMTP che supportano l'estensione SMTP BINARYMIME definita in RFC 3030, ad esempio i server su cui viene eseguito Exchange 2000 Server o versioni successive. In particolare devono verificarsi le seguenti condizioni:</p>
<ul>
<li><p>La parola chiave BINARYMIME deve essere annunciata nella risposta EHLO del server.</p></li>
<li><p>L'estensione SMTP BINARYMIME può essere utilizzata solo con l'estensione SMTP CHUNKING. L'estensione <em>Chunking</em> consente di inviare messaggi con corpo di grandi dimensioni in suddivisioni più piccole. L'estensione Chunking è definita anche in RFC 3030. La parola chiave CHUNKING, inoltre, deve essere annunciata nella risposta EHLO del server.</p></li>
<li><p>I messaggi vengono trasferiti utilizzando il comando BDAT al posto del comando DATA standard.</p></li>
<li><p>Il parametro <em>BODY=BINARYMIME</em> deve essere aggiunto alla fine del comando MAIL FROM se il messaggio è provvisto di un corpo.</p></li>
</ul></li>
</ul>
<p>I valori 7bit, 8bit e Binary non sono mai presenti insieme nello stesso messaggio costituito da più parti. I valori si escludono reciprocamente. I valori Quoted-Printable o Base64 possono essere visualizzati nel corpo di un messaggio costituito da più parti 7bit o 8bit, ma mai in un corpo Binary. Se il corpo di un messaggio costituito da più parti contiene diverse parti con contenuto 7bit e 8bit, l'intero messaggio viene classificato come 8bit. Se il corpo di un messaggio costituito da più parti contiene diverse parti con contenuto 7bit, 8bit e Binary, l'intero messaggio viene classificato come Binary.</p></td>
</tr>
<tr class="even">
<td><p>Content-Disposition</p></td>
<td><p>Attachment</p></td>
<td><p>Questo campo di intestazione indica a un client di posta elettronica abilitato a MIME come visualizzare un file allegato ed è descritto in RFC 2183. I valori di questo campo possono essere Inline o Attachment. Quando il valore di questo campo è Inline, l'allegato viene visualizzato nel corpo del messaggio. Quando il valore di questo campo è Attachment, il file allegato viene visualizzato come allegato normale separato dal corpo del messaggio. Quando il valore è Attachment sono disponibili altri parametri, ad esempio Filename, Creation-date e Size.</p></td>
</tr>
</tbody>
</table>


Inizio pagina


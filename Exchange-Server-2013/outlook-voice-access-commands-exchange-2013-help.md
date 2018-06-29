---
title: 'Comandi di Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Comandi di Outlook Voice Access
ms:assetid: 8fe9247c-695f-47d8-827e-c79d0426854b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn205137(v=EXCHG.150)
ms:contentKeyID: 54652845
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Comandi di Outlook Voice Access

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-03-09_

Outlook Voice Access consente agli utenti abilitati alla messaggistica unificata di accedere alla cassetta postale utilizzando telefoni analogici, digitali o cellulari. Utilizzando il sistema di menu di Outlook Voice Access, gli utenti abilitati alla messaggistica unificata possono leggere messaggi di posta elettronica, ascoltare messaggi vocali, interagire con il proprio calendario di Outlook, accedere ai contatti personali e gestire opzioni personali quali la configurazione del PIN di Outlook Voice Access o la registrazione dei messaggi vocali. Questo argomento contiene un elenco dei comandi di Outlook Voice Access e una descrizione di come questi possano essere utilizzati dagli utenti che accedono alla propria cassetta postale chiamando un numero Outlook Voice Access.

## Outlook Voice Access, interfacce utente

Outlook Voice Access consiste in due interfacce utente: l'interfaccia telefonica (TUI) che utilizza la tastiera del telefono e l'interfaccia vocale (VUI), che utilizza comandi vocali. Outlook Voice Access può essere utilizzato dagli utenti che accedono al sistema di posta vocale da un telefono interno o esterno per accedere ai messaggi di posta elettronica, ai messaggi vocali, ai contatti e alle informazioni di calendario presenti nella propria cassetta postale.

## Riferimento ai comandi della posta elettronica e del sistema di caselle vocali

In qualità di utente di Outlook Voice Access, quando si compone il numero Outlook Voice Access, vengono presentate opzioni di menu che consentono di accedere alla cassetta postale personale e di gestire la posta elettronica e il sistema di caselle vocali. Nella tabella che segue vengono elencati i comandi disponibili per la gestione della posta elettronica e del sistema di caselle vocali.

### Riferimento ai comandi della posta elettronica e del sistema di caselle vocali

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Comando vocale</th>
<th>Comando basato su toni</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&quot;Riproduci&quot;</p></td>
<td><p></p></td>
<td><p>Viene riprodotto il messaggio vocale o di posta elettronica corrente.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Successivo&quot;</p></td>
<td><p>#</p></td>
<td><p>Viene letto il messaggio vocale o di posta elettronica successivo.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Successivo non letto&quot;</p></td>
<td><p>00 seguito da ##</p></td>
<td><p>Viene letto il messaggio successivo non letto. L'opzione è disponibile solo per i messaggi di posta elettronica.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Elimina&quot;</p></td>
<td><p>7</p></td>
<td><p>Viene eliminato il messaggio vocale o di posta elettronica corrente.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Rispondi&quot;</p></td>
<td><p>8</p></td>
<td><p>Consente di rispondere all'utente che ha inviato il messaggio di posta elettronica o vocale corrente.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Rispondi a tutti&quot;</p></td>
<td><p>00 seguito da 88</p></td>
<td><p>Consente di rispondere a tutti gli utenti del messaggio corrente di posta elettronica. Opzione non disponibile per i messaggi vocali.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Segna come da leggere&quot;</p></td>
<td><p>9</p></td>
<td><p>Il messaggio di posta elettronica viene contrassegnato come Non letto.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Fine&quot;</p></td>
<td><p>33</p></td>
<td><p>La lettura viene interrotta e si passa alla fine del messaggio vocale o di posta elettronica corrente.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Altre opzioni&quot;</p></td>
<td><p>00</p></td>
<td><p>Viene aperto il menu Ulteriori opzioni.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Precedente&quot;</p></td>
<td><p>00 seguito da 11</p></td>
<td><p>Viene letto il messaggio vocale o di posta elettronica precedente.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Leggi intestazione&quot;</p></td>
<td><p></p></td>
<td><p>Viene letta l'intestazione del messaggio vocale o di posta elettronica.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Chiama mittente&quot;</p></td>
<td><p>00 seguito da 2</p></td>
<td><p>Viene chiamato l'utente che ha inviato il messaggio di posta elettronica o vocale corrente.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Inoltra&quot;</p></td>
<td><p>00 seguito da 6</p></td>
<td><p>Il messaggio di posta elettronica o vocale corrente viene inoltrato ad altri gruppi o destinatari di posta elettronica.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Contrassegna per il completamento&quot;</p></td>
<td><p>00 seguito da 44</p></td>
<td><p>Il messaggio vocale o di posta elettronica corrente viene contrassegnato per il successivo completamento.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Trova per nome&quot;</p></td>
<td><p></p></td>
<td><p>Il nome dell'utente viene utilizzato per trovare messaggi vocali o di posta elettronica nella cassetta postale dell'utente.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Elimina conversazione&quot;</p></td>
<td><p>00 seguito da 77</p></td>
<td><p>Tutti i messaggi di posta elettronica associati a una conversazione vengono eliminati. L'opzione è disponibile solo per i messaggi di posta elettronica.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Nascondi conversazione&quot;</p></td>
<td><p>00 seguito da 99</p></td>
<td><p>I messaggi di posta elettronica aggiuntivi contenuti nella stessa conversazione vengono nascosti. L'opzione è disponibile solo per i messaggi di posta elettronica.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Informazioni sulla busta&quot;</p></td>
<td><p>00 seguito da 5</p></td>
<td><p>Vengono lette le informazioni sulla busta del messaggio vocale o di posta elettronica.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Seleziona lingua&quot;</p></td>
<td><p>00 seguito da 55</p></td>
<td><p>Consente di selezionare la lingua in cui deve essere letto il messaggio vocale o di posta elettronica.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Indietro&quot; o &quot;Ripeti&quot;</p></td>
<td><p>1</p></td>
<td><p>Viene nuovamente riprodotto o ripetuto il messaggio vocale o di posta elettronica corrente. L'opzione è disponibile solo durante la riproduzione del messaggio.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Pausa&quot;</p></td>
<td><p>2</p></td>
<td><p>Viene messo in pausa il messaggio vocale o di posta elettronica corrente. L'opzione è disponibile solo durante la riproduzione del messaggio.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Avanti veloce&quot;</p></td>
<td><p>3</p></td>
<td><p>Viene riprodotto velocemente il messaggio vocale o di posta elettronica corrente. L'opzione è disponibile solo durante la riproduzione del messaggio.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Rallenta&quot;</p></td>
<td><p>4</p></td>
<td><p>Il messaggio vocale o di posta elettronica corrente viene letto o riprodotto più lentamente. L'opzione è disponibile solo durante la riproduzione del messaggio.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Più veloce&quot;</p></td>
<td><p>6</p></td>
<td><p>Il messaggio vocale o di posta elettronica corrente viene letto o riprodotto più velocemente. L'opzione è disponibile solo durante la riproduzione del messaggio.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Precedente&quot;</p></td>
<td><p>11</p></td>
<td><p>Il messaggio di posta elettronica precedente viene letto dall'inizio. L'opzione è disponibile solo per i messaggi di posta elettronica.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Riproduzione&quot;</p></td>
<td><p>00 seguito da 1</p></td>
<td><p>Viene ripetuta la riproduzione del messaggio vocale o di posta elettronica corrente.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Ripeti&quot;</p></td>
<td><p>0</p></td>
<td><p>Vengono ripetute le opzioni del menu corrente.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Menu principale&quot;</p></td>
<td><p>*</p></td>
<td><p>Consente di tornare al menu principale.</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> Per accedere al messaggio di posta elettronica dopo averlo eliminato utilizzando Outlook Voice Access, è possibile utilizzare Outlook Web App°oppure Outlook per riportare il messaggio di posta elettronica nella cartella appropriata dalla cartella Posta eliminata. Non è possibile utilizzare Outlook Voice Access per accedere alla cartella Posta eliminata.



## Riferimento del comando Opzioni calendario

In qualità di utente di Outlook Voice Access, quando si compone il numero Outlook Voice Access, vengono presentate opzioni di menu che consentono di accedere alla cassetta postale personale e di gestire il calendario. Nella tabella riportata di seguito sono elencati i comandi disponibili per la gestione del calendario.

### Comandi del calendario

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Comando vocale</th>
<th>Comando basato su toni</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&quot;Successivo&quot;</p></td>
<td><p>#</p></td>
<td><p>Viene letto l'appuntamento del calendario successivo.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Giorno successivo&quot;</p></td>
<td><p>##</p></td>
<td><p>Vengono aperti e letti gli appuntamenti del calendario per il giorno successivo.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Ripeti&quot;</p></td>
<td><p>0</p></td>
<td><p>Vengono ripetute le opzioni di menu disponibili. Altrimenti, se si sta utilizzando l'interfaccia vocale, il sistema legge nuovamente l'appuntamento del calendario.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Altre opzioni&quot;</p></td>
<td><p>00</p></td>
<td><p>Vengono riprodotti gli altri menu delle opzioni del calendario.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Ripeti&quot;</p></td>
<td><p>1</p></td>
<td><p>Viene letto nuovamente l'appuntamento del calendario.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Riunione precedente&quot;</p></td>
<td><p>00 seguito da 11</p></td>
<td><p>Viene aperta la riunione pianificata precedente.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Chiama luogo riunione&quot;</p></td>
<td><p>2</p></td>
<td><p>Viene chiamato il numero di telefono specificato per il luogo della riunione.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Chiama organizzatore&quot;</p></td>
<td><p>00 seguito da 22</p></td>
<td><p>Viene chiamato il numero di telefono specificato per l'organizzatore della riunione.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Arriverò in ritardo&quot;</p></td>
<td><p>3</p></td>
<td><p>Viene inviato il messaggio &quot;Arriverò in ritardo&quot; a tutti i partecipanti alla riunione.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Accetta&quot; o &quot;Accetta provvisoriamente&quot;</p></td>
<td><p>4</p></td>
<td><p>La convocazione di riunione viene accettata o accettata provvisoriamente.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Informazioni sulla riunione&quot;</p></td>
<td><p>5</p></td>
<td><p>Vengono lette o nuovamente riprodotte le informazioni sulla riunione di cui è in corso la lettura.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Informazioni sui partecipanti&quot;</p></td>
<td><p>00 seguito da 55</p></td>
<td><p>Vengono lette o nuovamente riprodotte le informazioni su una riunione pianificata.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Inoltra&quot;</p></td>
<td><p>00 seguito da 6</p></td>
<td><p>La convocazione di riunione viene inoltrata a un altro utente.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Rifiuta&quot; o &quot;Annulla&quot;</p></td>
<td><p>7</p></td>
<td><p>La convocazione di riunione viene rifiutata o annullata.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Cancella calendario&quot;</p></td>
<td><p>00 seguito da 77</p></td>
<td><p>Una specifica fascia oraria del calendario viene cancellata per quel giorno.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Rispondi&quot;</p></td>
<td><p>00 seguito da 8</p></td>
<td><p>Consente di rispondere all'organizzatore della riunione.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Rispondi a tutti&quot;</p></td>
<td><p>00 seguito da 88</p></td>
<td><p>Consente di rispondere a tutti i partecipanti alla riunione.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Ripeti menu&quot;</p></td>
<td><p>5 seguito da 0</p></td>
<td><p>Vengono ripetute le opzioni di menu disponibili.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Indietro&quot;</p></td>
<td><p>5 seguito da 1</p></td>
<td><p>Vengono ripetute le informazioni sulla riunione.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5 seguito da 11</p></td>
<td><p>Si ritorna all'inizio delle informazioni sulla riunione.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>5 seguito da 2</p></td>
<td><p>Viene interrotta e quindi ripresa la riproduzione delle informazioni sulla riunione.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Avanti veloce&quot;</p></td>
<td><p>5 seguito da 3</p></td>
<td><p>Vengono riprodotte velocemente le informazioni sulla riunione.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Fine&quot;</p></td>
<td><p>5 seguito da 33</p></td>
<td><p>Si passa alla fine delle informazioni sulla riunione.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5 seguito da 4</p></td>
<td><p>Le informazioni sulla riunione vengono riprodotte o lette più lentamente.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>5 seguito da 55</p></td>
<td><p>Consente di selezionare la lingua da utilizzare per la lettura delle informazioni sulla riunione.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5 seguito da 6</p></td>
<td><p>Le informazioni sulla riunione vengono riprodotte o lette più velocemente.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Menu principale&quot;</p></td>
<td><p>*</p></td>
<td><p>Consente di tornare al menu principale.</p></td>
</tr>
</tbody>
</table>


## Riferimento ai comandi per trovare un contatto

In qualità di utente di Outlook Voice Access, quando si compone un numero Outlook Voice Access, vengono presentate opzioni di menu che consentono di accedere alla cassetta postale, di modificare le opzioni personali o di chiamare o inviare un messaggio a un contatto. Se si utilizza la voce, selezionata per impostazione predefinita, e si seleziona l'opzione menu dei contatti, il sistema di caselle vocali chiederà di utilizzare la tastiera del telefono per accedere alle opzioni per trovare un contatto. È inoltre possibile individuare un utente nella directory o un contatto, tramite la tastiera del telefono. Nella tabella riportata di seguito sono elencati i comandi disponibili per la gestione dei contatti o per la ricerca di un utente.

### Comandi dei contatti

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Comando vocale</th>
<th>Comando basato su toni</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&quot;Directory&quot;</p></td>
<td><p>00</p></td>
<td><p>Consente di cercare un utente nella directory.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Riproduci informazioni&quot;</p></td>
<td><p>1</p></td>
<td><p>Vengono riprodotte le informazioni sul contatto personale, ad esempio i numeri di telefono specificati per il contatto.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Invia un messaggio&quot;</p></td>
<td><p>3</p></td>
<td><p>Viene inviato un messaggio al contatto personale selezionato.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Trova un altro contatto&quot;</p></td>
<td><p>4</p></td>
<td><p>Consente di trovare un altro contatto personale.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Chiama cellulare&quot;</p></td>
<td><p>2 seguito da 1</p></td>
<td><p>Consente di chiamare il numero telefonico del cellulare specificato per il contatto personale.</p></td>
</tr>
<tr class="even">
<td><p>&quot;Chiama ufficio&quot;</p></td>
<td><p>2 seguito da 2</p></td>
<td><p>Consente di chiamare il numero telefonico dell'ufficio o del luogo di lavoro specificato per il contatto personale.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Chiama casa&quot;</p></td>
<td><p>2 seguito da 3</p></td>
<td><p>Consente di chiamare il numero telefonico di casa specificato per il contatto personale.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>##</p></td>
<td><p>Consente di immettere l'alias o il nome di posta elettronica per l'utente presente nella directory se si utilizza la funzionalità di ricerca nelle directory.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Menu principale&quot;</p></td>
<td><p>*</p></td>
<td><p>Consente di tornare al menu principale.</p></td>
</tr>
</tbody>
</table>


## Riferimento ai comandi delle opzioni personali

In qualità di utente di Outlook Voice Access, quando si compone il numero Outlook Voice Access, vengono presentate opzioni di menu che consentono di accedere alla cassetta postale personale e di gestire le opzioni personali. Quando si configurano le opzioni personali utilizzando Outlook Voice Access, è possibile utilizzare solo la tastiera del telefono per accedere ai menu. L'utilizzo della voce per accedere ai menu non è disponibile per la configurazione delle opzioni personali. Nella tabella riportata di seguito sono elencati i comandi disponibili per la gestione delle opzioni personali.

### Comandi delle opzioni personali

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Comando vocale</th>
<th>Comando basato su toni</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>1</p></td>
<td><p>Consente di attivare o disattivare il messaggio di saluto Fuori sede del telefono.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>2</p></td>
<td><p>Consente di registrare il messaggio vocale personale o il messaggio di saluto Fuori sede.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>3</p></td>
<td><p>Consente di modificare il PIN utilizzato per Outlook Voice Access.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>4</p></td>
<td><p>Consente di eseguire l'avvio utilizzando l'interfaccia vocale o l'interfaccia a toni.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>5</p></td>
<td><p>Consente di impostare il fuso orario locale da utilizzare.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>6</p></td>
<td><p>Consente di selezionare il formato 12 o 24 ore.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>*</p></td>
<td><p>Consente di tornare al menu principale.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>0</p></td>
<td><p>Vengono ripetute le opzioni di menu disponibili.</p></td>
</tr>
</tbody>
</table>


## Ulteriori informazioni

[Configurazione di Outlook Voice Access](setting-up-outlook-voice-access-exchange-2013-help.md)

[Installazione delle funzionalità di posta vocale del client](set-up-client-voice-mail-features-exchange-2013-help.md)


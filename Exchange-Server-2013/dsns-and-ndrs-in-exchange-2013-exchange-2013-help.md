---
title: 'DSN e NDR in Exchange 2013: Exchange 2013 Help'
TOCTitle: DSN e NDR in Exchange 2013
ms:assetid: 8e91de84-76fa-49b2-898c-c5eface76560
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232118(v=EXCHG.150)
ms:contentKeyID: 50481160
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DSN e NDR in Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_


> [!NOTE]
> Se hai bisogno di informazioni rapporti di mancato recapito in Office 365 o Exchange Online, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=524931">rapporti di mancato recapito di posta elettronica in Office 365</A>.



Quando si verifica un problema di recapito di un messaggio, Exchange Server 2013 invia una notifica stato recapito (DSN) al mittente del messaggio. Questi messaggi generati dal sistema sono noti anche come messaggi di rimbalzo e contengono un codice di errore, dettagli tecnici sul problema e in alcuni casi passaggi di risoluzione dei problemi per il mittente del messaggio. Rapporto di mancato recapito (NDR) i messaggi è un tipo di notifica dello stato. In questo argomento per gli amministratori di posta elettronica viene possibili cause e soluzioni per i codici di stato numerosi rapporti di mancato Recapito. Inoltre viene spiegato come leggere e interpretare i messaggi di rapporto di mancato Recapito.

**Sommario**

Codici di stato avanzati più comuni

Sezioni dei rapporti di mancato recapito

Esempi di messaggi di rapporti di mancato recapito

## Codici di stato avanzati più comuni

Nella seguente tabella è riportato un elenco dei codici di stato avanzati restituiti nei rapporti di mancato recapito per gli errori di recapito dei messaggi più comuni.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Codice di stato avanzato</th>
<th>Descrizione</th>
<th>Possibile causa</th>
<th>Informazioni aggiuntive</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>4.3.1</p></td>
<td><p><code>Insufficient system resources</code></p></td>
<td><p>Si è verificato un errore di memoria esaurita. Il problema può essere causato da un problema di risorse, quale un disco pieno.</p>
<p>Invece di un errore di disco pieno, potrebbe essere visualizzato un errore di memoria esaurita.</p></td>
<td><p>Verificare che il server Exchange disponga di spazio sufficiente su disco.</p></td>
</tr>
<tr class="even">
<td><p>4.3.2</p></td>
<td><p><code>System not accepting network messages</code></p></td>
<td><p>Questo rapporto di mancato recapito viene generato quando una coda è stata bloccata.</p></td>
<td><p>È possibile risolvere il problema sbloccando la coda.</p></td>
</tr>
<tr class="odd">
<td><p>4.4.1</p></td>
<td><p><code>Connection timed out</code></p></td>
<td><p>Server di destinazione non risponde. Questo errore può essere causato da condizioni di rete temporanee. Il server Exchange tenta automaticamente di connettersi nuovamente al server e recapitare la posta. In caso di errore dopo tentativi di più, viene generato un rapporto di mancato Recapito di un codice di errore permanente.</p></td>
<td><p>Controllare la situazione. Si può trattare di un problema temporaneo che potrebbe risolversi senza intervento da parte dell'utente.</p></td>
</tr>
<tr class="even">
<td><p>4.4.2</p></td>
<td><p><code>Connection dropped</code></p></td>
<td><p>Una connessione tra i server si è interrotta. L'errore può essere causato da condizioni di rete temporanee o un server in cui si sono verificati problemi. Il server di invio tenterà nuovamente di recapitare il messaggio per un periodo di tempo specifico, quindi genererà ulteriori rapporti di stato.</p></td>
<td><p>Controllare la situazione mentre il server tenta di eseguire nuovamente il recapito. Si può trattare di un problema temporaneo che potrebbe risolversi senza intervento da parte dell'utente.</p>
<p>Questa situazione si verifica anche quando viene raggiunto il limite della dimensione dei messaggi per la connessione o se la velocità di invio dei messaggi per l'indirizzo IP client ha superato il limite configurato.</p></td>
</tr>
<tr class="odd">
<td><p>4.4.7</p></td>
<td><p><code>Message expired</code></p></td>
<td><p>Il messaggio nella coda è scaduto. Il server mittente ha tentato di inoltrare o recapitare il messaggio, ma l'operazione non è stata completata prima che si verificasse il timeout di scadenza del messaggio. Questo messaggio può anche indicare che è stato raggiunto un limite dell'intestazione dei messaggi su un server remoto o che si è verificato il timeout di un altro protocollo durante la comunicazione con il server remoto.</p></td>
<td><p>In genere il messaggio indica un problema del server di destinazione. Controllare la validità dell'indirizzo del destinatario e determinare se il server di destinazione è configurato correttamente per ricevere messaggi.</p>
<p>Potrebbe essere necessario ridurre il numero di destinatari nell'intestazione del messaggio per l'host relativamente al quale si riceve l'errore. Se il messaggio viene inviato di nuovo, viene nuovamente inserito nella coda. Se il server destinatario è disponibile, il messaggio viene recapitato.</p></td>
</tr>
<tr class="even">
<td><p>5.0.0</p></td>
<td><p><code>HELO / EHLO requires domain address</code></p></td>
<td><p>Questa situazione è un errore permanente. Tra le possibili cause sono incluse le seguenti:</p>
<ul>
<li><p>Non è disponibile una route per lo spazio degli indirizzi specificato. Ad esempio, un connettore SMTP è configurato ma l'indirizzo non corrisponde.</p></li>
<li><p>Il DNS ha restituito un host autorevole che non era stato trovato per il dominio.</p></li>
<li><p>Si è verificato un errore SMTP.</p></li>
</ul></td>
<td><p>Tra le possibili soluzioni sono incluse le seguenti:</p>
<ul>
<li><p>In uno o più connettori SMTP aggiungere un valore asterisco (<strong>*</strong>) come spazio degli indirizzi SMTP.</p></li>
<li><p>Verificare che il DNS funzioni.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>5.1.0</p></td>
<td><p><code>Sender denied</code></p></td>
<td><p>In questo rapporto di mancato Recapito è causato da un errore generale (errore di indirizzo). Impossibile trovare un indirizzo di posta elettronica o un altro attributo in servizi di dominio Active Directory. Questo problema può essere causato da voci dei contatti senza il set di attributi <strong>targetAddress</strong> . Un altro è possibile che l'attributo <strong>homeMDB</strong> di un utente non è stato determinato. L'attributo <strong>homeMDB</strong> corrisponde al server Exchange in cui la cassetta postale dell'utente.</p>
<p>Questo rapporto di mancato recapito può essere generato anche quando si utilizza Microsoft Outlook per salvare un messaggio di posta elettronica come file e qualcuno ha aperto il messaggio non in linea e ha risposto al messaggio. La proprietà del messaggio conserva solo l'attributo <strong>legacyExchangeDN</strong> quando Outlook recapita il messaggio, quindi la ricerca può avere esito negativo.</p></td>
<td><p>L'indirizzo del destinatario non è formattato correttamente oppure non è stato possibile risolvere correttamente il destinatario. Il primo passaggio per risolvere questo errore consiste nel controllare l'indirizzo del destinatario e nell’inviare nuovamente il messaggio.</p></td>
</tr>
<tr class="even">
<td><p>5.1.1</p></td>
<td><p><code>Bad destination mailbox address</code></p></td>
<td><p>Questo errore potrebbe essere causato dalle seguenti condizioni:</p>
<ul>
<li><p>Il mittente ha immesso l'indirizzo di posta elettronica del destinatario in modo errato.</p></li>
<li><p>Non esiste alcun destinatario nel sistema di posta elettronica di destinazione.</p></li>
<li><p>La cassetta postale del destinatario è stata spostata e la cache dei destinatari di Outlook sul computer del mittente non è stata aggiornata.</p></li>
<li><p>Esiste un nome di dominio (DN) legacy non valido per la cassetta postale del destinatario in Servizi di dominio Active Directory.</p></li>
</ul></td>
<td><p>Questo errore si verifica in genere quando il mittente del messaggio immette l'indirizzo di posta elettronica del destinatario in modo non corretto. Il mittente deve controllare l'indirizzo di posta elettronica del destinatario e inviare nuovamente il messaggio. L'errore può verificarsi anche se l'indirizzo di posta elettronica del destinatario era corretto in passato, ma è stato modificato o rimosso dal sistema di posta elettronica di destinazione.</p>
<p>Se il mittente del messaggio è nella stessa organizzazione Exchange come destinatario e cassetta postale del destinatario è ancora presente, determinare se cassetta postale del destinatario è stata spostata in un nuovo server di posta elettronica. In questo caso, Outlook potrebbero non essere aggiornati nella cache del destinatario correttamente. Chiedere al mittente di rimuovere l'indirizzo del destinatario dalla cache del destinatario Outlook del mittente e quindi creare un nuovo messaggio. Inviare il messaggio originale, verrà generato l'errore stesso.</p>
<p>Questo errore potrebbe essere causato da altri problemi, ad esempio un nome distinto (DN) legacy non valido in Servizi di dominio Active Directory. Esaminare e correggere il DN precedente della cassetta postale del destinatario. Indicare al mittente di rimuovere l'indirizzo del destinatario dalla propria cache dei destinatari di Outlook e creare un nuovo messaggio. Il nuovo invio del messaggio originale genera lo stesso errore.</p></td>
</tr>
<tr class="odd">
<td><p>5.1.2</p></td>
<td><p><code>Invalid X.400 address</code></p></td>
<td><p>Il destinatario possiede un indirizzo non SMTP che non può essere associato a una destinazione. L'indirizzo non sembra essere locale e non sono configurati connettori con spazi degli indirizzi che contengano l'indirizzo del destinatario.</p></td>
<td><p>Verificare che l'indirizzo del destinatario sia stato immesso correttamente. Se l'indirizzo del destinatario si trova in un sistema di posta elettronica non SMTP a cui si desidera recapitare specificamente la posta, è necessario aggiungere il tipo appropriato di connettore alla topologia e configurarlo in modo che fornisca il servizio al sistema di posta elettronica del destinatario.</p></td>
</tr>
<tr class="even">
<td><p>5.1.3</p></td>
<td><p><code>Invalid recipient address</code></p></td>
<td><p>Questo messaggio indica che l'indirizzo del destinatario è visualizzato in modo non corretto nel messaggio.</p></td>
<td><p>L'indirizzo del destinatario non è formattato correttamente oppure non è stato possibile risolvere correttamente l'indirizzo del destinatario. Il primo passaggio per risolvere questo errore prevede di controllare l'indirizzo del destinatario e di inviare nuovamente il messaggio.</p>
<p>Inoltre, esaminare il criterio del destinatario SMTP e assicurarsi che ciascun dominio di posta per il quale si desidera accettare la posta sia visualizzato correttamente.</p></td>
</tr>
<tr class="odd">
<td><p>5.1.4</p></td>
<td><p><code>Destination mailbox address ambiguous</code></p></td>
<td><p>Due o più destinatari nell'organizzazione Exchange hanno lo stesso indirizzo.</p></td>
<td><p>Questo errore si verifica in genere a causa di una configurazione non corretta in servizi di dominio Active Directory. Probabilmente a causa di problemi di replica, due oggetti destinatario in servizi di dominio Active Directory avere lo stesso indirizzo SMTP o Exchange Server (EX) indirizzo.</p></td>
</tr>
<tr class="even">
<td><p>5.1.7</p></td>
<td><p><code>Invalid address</code></p></td>
<td><p>Il mittente ha un indirizzo SMTP non corretto o mancante, l'attributo <strong>mail</strong> nel servizio directory. Non è possibile recapitare l'elemento di posta senza un attributo <strong>mail</strong> valido.</p></td>
<td><p>Controllare la struttura di directory del mittente e determinare se è presente l'attributo <strong>mail</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>5.2.1</p></td>
<td><p><code>Mailbox cannot be accessed</code></p></td>
<td><p>Impossibile accedere alla cassetta postale. La cassetta postale potrebbe essere disattivata o non in linea, oppure il messaggio è stato messo in quarantena da una regola.</p></td>
<td><p>Controllare se il database del destinatario è in linea, se la cassetta postale è disattivata o se il messaggio è stato messo in quarantena.</p></td>
</tr>
<tr class="even">
<td><p>5.2.2</p></td>
<td><p><code>Mailbox full</code></p></td>
<td><p>La cassetta postale del destinatario ha superato la quota di archiviazione e non può più accettare nuovi messaggi.</p></td>
<td><p>Questo errore si verifica quando la cassetta postale del destinatario ha superato la quota di archiviazione. Il destinatario deve ridurre la dimensione della cassetta postale o l'amministratore deve aumentare la quota di archiviazione, per consentire la riuscita del recapito.</p></td>
</tr>
<tr class="odd">
<td><p>5.2.3</p></td>
<td><p><code>Message too large</code></p></td>
<td><p>Il messaggio è troppo grande e viene superata la quota locale. Ad esempio, un utente remoto Exchange può avere una restrizione sulla dimensione massima dei messaggi in arrivo.</p></td>
<td><p>Inviare nuovamente il messaggio senza allegati o impostare il limite dal lato server o client in modo da consentire una dimensione maggiore dei messaggi.</p></td>
</tr>
<tr class="even">
<td><p>5.2.4</p></td>
<td><p><code>Mailing list expansion problem</code></p></td>
<td><p>Il destinatario è una lista di distribuzione dinamica configurata in modo errato. La stringa di filtro o il nome distinto (DN) di base della lista di distribuzione non sono validi.</p></td>
<td><p>Impostare il livello di registrazione eventi del classificatore almeno sul livello minimo e inviare un altro messaggio alla lista di distribuzione dinamica. Controllare se nel registro applicazioni è presente un evento 6025 o 6026 in cui viene descritto in dettaglio quale attributo è configurato in modo errato nell'oggetto lista di distribuzione dinamica.</p></td>
</tr>
<tr class="odd">
<td><p>5.3.3</p></td>
<td><p><code>Unrecognized command</code></p></td>
<td><p>Quando il server remoto Exchange raggiunge la capacità della relativa archiviazione su disco per conservare la posta, potrebbe rispondere a questo rapporto di mancato Recapito. Questo errore si verifica quando il server di invio è l'invio dei messaggi con un comando ESMTP BDAT. Questo errore indica inoltre un messaggio di errore protocollo SMTP.</p></td>
<td><p>Assicurarsi che nel server remoto sia presente una capacità di archiviazione sufficiente per contenere la posta. Controllare il registro SMTP.</p></td>
</tr>
<tr class="even">
<td><p>5.3.4</p></td>
<td><p><code>Message too big for system</code></p></td>
<td><p>Il messaggio supera il limite di dimensione configurato su un database di trasporto o di cassette postali e non può essere accettato. Questo errore può essere generato sia dal sistema di posta elettronica di invio, sia dal sistema di posta elettronica del destinatario.</p></td>
<td><p>L'errore si verifica quando la dimensione del messaggio inviato dal mittente supera la dimensione massima consentita dei messaggi per il passaggio attraverso un componente di trasporto o un database delle cassette postali. Per fare in modo che il messaggio venga recapitato correttamente, il mittente deve ridurne la dimensione. Per ulteriori informazioni sulla configurazione del limite per la dimensione dei messaggi, vedere <a href="message-size-limits-exchange-2013-help.md">Limiti di dimensione dei messaggi</a>.</p></td>
</tr>
<tr class="odd">
<td><p>5.3.5</p></td>
<td><p><code>System incorrectly configured</code></p></td>
<td><p>È stata rilevata una situazione di loop della posta, ovvero il server è configurato per inviare la posta a se stesso.</p></td>
<td><p>Controllare la presenza di loop nella configurazione dei connettori del server e assicurarsi che ogni connettore sia definito da una porta in ingresso univoca. Se sono presenti più server virtuali, assicurarsi che nessuno sia impostato su &quot;Tutti non assegnati&quot;.</p></td>
</tr>
<tr class="even">
<td><p>5.4.4</p></td>
<td><p><code>Invalid arguments</code></p></td>
<td><p>Questo rapporto di mancato recapito viene generato se non è presente una route per il recapito dei messaggi o se il classificatore non è stato in grado di determinare la destinazione dell'hop successivo.</p></td>
<td><p>Controllare che il nome di dominio specificato sia valido e che sia presente un record di Mail Exchanger (MX).</p></td>
</tr>
<tr class="odd">
<td><p>5.4.6</p></td>
<td><p><code>Routing loop detected</code></p></td>
<td><p>Un errore di configurazione ha causato un ciclo di posta elettronica. Per impostazione predefinita, dopo 20 iterazioni di un ciclo di posta elettronica, Exchange interrompe il ciclo di e genera un rapporto di mancato Recapito per il mittente del messaggio.</p></td>
<td><p>Questo errore si verifica quando il recapito di un messaggio genera un altro messaggio in risposta. Messaggio genera un terzo messaggio, quindi il processo viene ripetuto, la creazione di un ciclo. Per proteggere il esaurire le risorse di sistema, Exchange interrompe il ciclo di posta elettronica dopo 20 iterazioni. Cicli di posta elettronica vengono creati in genere a causa di un errore di configurazione nel server di posta elettronica invio, il server della posta o entrambi. Verificare la configurazione di regole della cassetta postale del mittente e del destinatario per determinare se è abilitato l'inoltro automatico dei messaggi.</p></td>
</tr>
<tr class="even">
<td><p>5.5.2</p></td>
<td><p><code>Send hello first</code></p></td>
<td><p>Si verifica un errore SMTP generico quando i comandi SMTP vengono inviati fuori sequenza. Ad esempio, un server tenta di inviare un comando AUTH (autorizzazione) prima di identificare se stesso con un comando EHLO.</p>
<p>È possibile che questo errore si verifichi anche quando il disco di sistema è pieno.</p></td>
<td><p>Visualizzare il registro SMTP o un'analisi di Netmon e assicurarsi che siano disponibili archiviazione su disco e memoria virtuale adeguate.</p></td>
</tr>
<tr class="odd">
<td><p>5.5.3</p></td>
<td><p><code>Too many recipients</code></p></td>
<td><p>Il totale dei destinatari presenti nelle righe A, Cc e Ccn del messaggio supera il numero totale dei destinatari che è consentito inserire in un singolo messaggio.</p></td>
<td><p>Questo errore si verifica quando il mittente ha incluso nel messaggio troppi destinatari. Il mittente deve ridurre il numero di indirizzi di destinatari presenti nel messaggio o è necessario aumentare il numero massimo di destinatari, per consentire il corretto recapito del messaggio.</p></td>
</tr>
<tr class="even">
<td><p>5.5.4</p></td>
<td><p><code>Invalid domain name</code></p></td>
<td><p>Il messaggio contiene un mittente non valido o un formato non corretto dell'indirizzo del destinatario.</p>
<p>Una possibile causa è che il formato del mittente del destinatario contiene caratteri non conformi agli standard Internet.</p></td>
<td><p>Controllare che l'indirizzo del destinatario non includa caratteri non standard.</p></td>
</tr>
<tr class="odd">
<td><p>5.5.6</p></td>
<td><p><code>Invalid message content</code></p></td>
<td><p>Questo messaggio indica un possibile errore del protocollo.</p></td>
<td><p>Controllare la presenza di possibili errori nel registro eventi.</p></td>
</tr>
<tr class="even">
<td><p>5.7.1</p></td>
<td><p><code>Delivery not authorized</code></p></td>
<td><p>Al mittente non è consentito inviare messaggi al destinatario.</p></td>
<td><p>L'errore si verifica quando il mittente tenta di inviare un messaggio a un destinatario non essendo però autorizzato a eseguire tale operazione. Ciò accade spesso quando un mittente tenta di inviare un messaggio a un gruppo di distribuzione configurato per accettare messaggi solo da membri del gruppo o da altri mittenti autorizzati. Il mittente deve richiedere l'autorizzazione a inviare messaggi al destinatario.</p>
<p>Questo errore può verificarsi anche se una regola di trasporto Exchange un messaggio viene rifiutato perché il messaggio con corrispondenza condizioni configurate nella regola di trasporto.</p></td>
</tr>
<tr class="odd">
<td><p>5.7.1</p></td>
<td><p><code>Unable to relay</code></p></td>
<td><p>Il sistema di posta elettronica di invio non è autorizzato a inviare un messaggio a un sistema di posta elettronica se quest'ultimo non è la destinazione finale del messaggio.</p></td>
<td><p>Questo errore si verifica quando il sistema di posta elettronica di invio tenta di inviare un messaggio anonimo a un sistema di posta elettronica ricevente e quest'ultimo non accetta messaggi per il dominio o i domini specificati in uno o più destinatari. Di seguito sono riportate le cause più comuni dell'errore:</p>
<ul>
<li><p>Una terza parte tenta di utilizzare un sistema di posta elettronica di ricezione per inviare posta indesiderata e il sistema di posta elettronica ricevente rifiuta il tentativo. Per la natura stessa della posta indesiderata, l'indirizzo di posta elettronica del mittente potrebbe essere contraffatto e il rapporto di mancato recapito risultante potrebbe essere inviato all'indirizzo di posta elettronica di un mittente ignaro di tutto. È difficile evitare questa situazione.</p></li>
<li><p>Un record MX per un dominio punta a un sistema di posta elettronica ricevente il cui dominio non è accettato. L'amministratore responsabile del nome di dominio specifico deve correggere il record MX o configurare il sistema di posta elettronica di ricezione perché accetti messaggi inviati al dominio in questione.</p></li>
<li><p>Un sistema o un client di posta elettronica di invio che deve utilizzare il sistema di posta elettronica di ricezione per l'inoltro di messaggi non possiede le autorizzazioni corrette allo scopo.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>5.7.1</p></td>
<td><p><code>Client was not authenticated</code></p></td>
<td><p>Il sistema di posta elettronica di invio non è stato autenticato con il sistema di posta elettronica di ricezione. Il sistema di posta elettronica di ricezione richiede l'autenticazione prima dell'invio dei messaggi.</p></td>
<td><p>Questo errore si verifica quando il server di ricezione deve essere autenticato prima dell'invio dei messaggi e il sistema di posta elettronica di invio non è stato autenticato con il sistema di posta elettronica di ricezione. Perché il recapito abbia esito positivo, l'amministratore del sistema di posta elettronica di invio deve configurare tale sistema per l'autenticazione con il sistema di posta elettronica di ricezione. L'errore può verificarsi anche se si tenta di accettare messaggi anonimi provenienti da Internet su un server Cassette postali non configurato allo scopo.</p></td>
</tr>
<tr class="odd">
<td><p>5.7.3</p></td>
<td><p><code>Not Authorized</code></p></td>
<td><p>Il mittente ha vietato la riassegnazione al destinatario alternativo.</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Sezioni dei rapporti di mancato recapito

In Exchange 2013, rapporti di mancato recapito sono progettati per essere semplici da leggere e comprendere da utenti finali e amministratori. Informazioni visualizzate in un rapporto di mancato Recapito sono suddivisa in due aree seguenti:

  - Una sezione di informazioni sull'utente

  - Una sezione di informazioni sull'amministratore

Le informazioni di ogni sezione sono destinate ai lettori della sezione in questione. La sezione delle informazioni sull'utente viene visualizzata per prima e contiene commenti mirati ad aiutare gli utenti a comprendere, in termini non tecnici, il motivo per cui il recapito del messaggio ha avuto esito negativo. La sezione **Informazioni di diagnostica per gli amministratori** offre informazioni tecniche più approfondite, quali le intestazioni del messaggio originale, che aiutano gli amministratori della posta elettronica a risolvere un problema di recapito. Nella seguente figura vengono illustrate la sezione delle informazioni utente e la sezione **Informazioni di diagnostica per gli amministratori** di un rapporto di mancato recapito.

**Sezioni dei rapporti di mancato recapito**

![Rapporto di mancato recapito indicante informazioni di diagnostica dell'amministratore e dell'utente](images/Bb232118.96245455-5fb9-4669-a931-5563ddd3ab35(EXCHG.150).png "Rapporto di mancato recapito indicante informazioni di diagnostica dell'amministratore e dell'utente")

## Sezione delle informazioni sull'utente

La sezione informazioni utente di un rapporto di mancato Recapito generato da Exchange contiene informazioni che si desidera comunicare agli utenti finali che ha inviato un messaggio di successivamente restituito con un rapporto di mancato Recapito. Dal server che ha generato il rapporto di mancato Recapito Exchange viene inserito il testo che viene visualizzato in questa sezione.

Il testo nella sezione delle informazioni sull'utente è progettato per consentire agli utenti finali di determinare per quale motivo il messaggio è stato rifiutato e in che modo è possibile inviarlo nuovamente perché sia correttamente recapitato. Nei casi in cui è possibile, nella sezione Informazioni utente è contenuto anche il nome di dominio completo (FQDN, Fully Qualified Domain Name) del server che ha rifiutato il messaggio. Se il recapito ha esito negativo per più destinatari, vengono elencati gli indirizzi di posta elettronica di tutti i destinatari e, nello spazio sotto ogni singolo indirizzo, viene specificato il motivo del mancato recapito.

È possibile modificare il testo della sezione Informazioni utente utilizzando il cmdlet **New-SystemMessage**. Creando un messaggio personalizzato, è possibile fornire informazioni specifiche agli utenti finali, ad esempio un numero di telefono da utilizzare per contattare il reparto del supporto tecnico o un collegamento ipertestuale da utilizzare per ottenere un supporto self-service.

Inizio pagina

## Informazioni di diagnostica per gli amministratori

La sezione **Informazioni di diagnostica per gli amministratori** contiene informazioni più dettagliate sull'errore specifico che si è verificato durante il recapito del messaggio, sul server che ha generato il rapporto di mancato recapito e sul server che ha rifiutato il messaggio. I seguenti campi sono presenti nella maggior parte dei rapporti di mancato recapito e sono visibili nella figura "Sezioni dei rapporti di mancato recapito" precedentemente riportata in questo argomento:

  - **Server di generazione**   Il server di generazione è il server SMTP che ha creato il rapporto di mancato Recapito. Il server di generazione richiede il codice di stato avanzato che è descritto più avanti in questo argomento. Il codice seguente crea un rapporto di mancato Recapito di facile lettura. Se nessun server remoto è elencato sotto l'indirizzo di posta elettronica del mittente nella sezione **informazioni di diagnostica per gli amministratori**, il server di generazione è anche il server che ha rifiutato il messaggio di posta elettronica originale. Se il recapito dei messaggi ha esito negativo se il messaggio viene inviato a un altro destinatario nell'organizzazione Exchange, lo stesso server in genere rifiuta il messaggio originale e genera il rapporto di mancato Recapito.

  - **Destinatario rifiutato**   Il destinatario rifiutato è l'indirizzo di posta elettronica del destinatario per cui il recapito del messaggio originale ha avuto esito negativo. Se il recapito ha esito negativo per più destinatari, vengono elencati gli indirizzi di posta elettronica di tutti i destinatari. Il campo del destinatario rifiutato contiene anche i seguenti sottocampi per ogni indirizzo di posta elettronica elencato:
    
      - **Server remoto**   Il campo del server remoto contiene il nome di dominio completo (FQDN) del server che ha rifiutato il recapito del messaggio durante la conversazione SMTP. Il campo Server remoto viene compilato solo quando viene tentato il recapito a un server remoto e tale tentativo di recapito viene rifiutato prima che il server di ricezione riconosca il messaggio dopo l'invio del corpo del messaggio. Se il messaggio originale viene riconosciuto dal server di ricezione e quindi rifiutato, ad esempio, per restrizioni relative al contenuto, il campo Server remoto non viene compilato.
    
      - **Codice di stato avanzato**   Nel codice di stato avanzato è il codice restituito dal server che ha rifiutato il messaggio originale. Il codice di stato avanzato indica il motivo per cui è stato rifiutato il messaggio originale. Il codice di stato avanzato non riscritto per Exchange ma viene utilizzato per determinare il testo da visualizzare nella sezione informazioni utente. I codici di stato avanzato che si è molto probabile sono elencati in "Codici di stato avanzato comuni" più avanti in questo argomento. Per un elenco dettagliato dei codici di stato avanzato, vedere RFC 3463.
    
      - **Risposta SMTP**   La risposta SMTP è il testo di computer leggibili restituito dal server che ha rifiutato il messaggio originale. La risposta SMTP in genere contiene una stringa breve che fornisce una spiegazione del codice di stato avanzato che viene inoltre restituito. La risposta SMTP non è stato riscritto per Exchange. Inoltre, questa risposta viene sempre visualizzata nel formato US-ASCII.

  - **Intestazioni originali del messaggio**   La sezione Intestazioni originali del messaggio contiene le intestazioni del messaggio rifiutato. Queste intestazioni possono fornire informazioni di diagnostica utili, ad esempio, per determinare il percorso seguito dal messaggio prima di essere rifiutato o per stabilire se il campo **A** corrisponde all'indirizzo di posta elettronica specificato nel campo del destinatario rifiutato.

Inizio pagina

## Esempi di rapporti di mancato recapito

Nelle seguenti sezioni vengono forniti esempi di due possibili modalità di generazione dei rapporti di mancato recapito:

  - Dallo stesso server

  - Da server diversi

## Rapporto di mancato recapito generato e messaggio originale rifiutato dallo stesso server

Nell'esempio di seguito viene mostrato che cosa accade quando un'organizzazione di posta elettronica remota accetta il recapito di un messaggio di posta elettronica tramite un server Trasporto Edge e quindi rifiuta il messaggio per una restrizione relativa ai criteri presente sulla cassetta postale del destinatario. In questo caso, il mittente non sarà autorizzato a inviare messaggi al destinatario. I server Trasporto Edge non eseguono la convalida della dimensione dei messaggi, quindi, in questo esempio, il server Trasporto Edge accetta il messaggio perché ha un indirizzo del destinatario valido e non viola altre restrizioni relative al contenuto. Poiché l'organizzazione di posta elettronica remota accetta l'intero messaggio, incluso il relativo contenuto, è responsabile del rifiuto del messaggio e della generazione del rapporto di mancato recapito da inviare al mittente.

**Generazione del rapporto di mancato recapito e rifiuto del messaggio da parte dello stesso server**

![Rapporto di mancato recapito indicante lo stesso server di generazione e rifiuto](images/Bb232118.c9a7cd2d-f35f-4d77-8225-c29585fa3ccd(EXCHG.150).gif "Rapporto di mancato recapito indicante lo stesso server di generazione e rifiuto")

Inoltre, in genere verranno rifiutati i messaggi che vengono rifiutati quando vengono inviati a destinatari che fanno parte della stessa organizzazione Exchange dallo stesso server di posta elettronica che genera il rapporto di Mancato recapito. È possono rifiutare i messaggi inviati a destinatari locali per diversi motivi, ad esempio le cassette postali che hanno superato la quota mancanza di autorizzazione per inviare messaggi per l'indirizzo del destinatario o errori hardware che causare una perdita della connettività ad altri server nell'organizzazione estesa.

In tutte le situazioni descritte non viene incluso alcun server remoto sotto l'indirizzo di posta elettronica dei destinatari elencati nel rapporto di mancato recapito.

Inizio pagina

## Rapporto di mancato recapito generato e messaggio originale rifiutato da server diversi

Nell'esempio di seguito viene mostrato che cosa accade quando un'organizzazione di posta elettronica remota rifiuta il recapito di un messaggio di posta elettronica ancora prima di accettare il messaggio. In questo esempio, il server remoto rifiuta il messaggio e restituisce un codice di stato avanzato al server di invio locale poiché il destinatario specificato non esiste. Il rifiuto avviene prima che il server di ricezione riconosca il messaggio. Poiché il server di ricezione non arriva a riconoscere il messaggio, non ne è responsabile. È quindi il server di invio locale a generare il rapporto di mancato recapito e a inviarlo al mittente del messaggio originale.

**Generazione del rapporto di mancato recapito e rifiuto del messaggio da parte di server diversi**

![Rapporto di mancato recapito indicante server di generazione/invio diversi](images/Bb232118.adfb8d5a-9c1d-4cd9-8a71-ce14224434f8(EXCHG.150).gif "Rapporto di mancato recapito indicante server di generazione/invio diversi")

Inizio pagina

## Vedere anche


[Che cosa sono i rapporti di mancato recapito Exchange in Exchange Online e Office 365](https://go.microsoft.com/fwlink/p/?linkid=524931)


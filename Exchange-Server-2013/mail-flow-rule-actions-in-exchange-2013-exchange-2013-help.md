---
title: 'Azioni della regola di trasporto: Exchange 2013 Help'
TOCTitle: Azioni relative alla regola del flusso di posta
ms:assetid: 5d11a955-b1cc-4150-a0b9-a8cc48ba9bde
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998315(v=EXCHG.150)
ms:contentKeyID: 50480693
ms.date: 02/14/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Azioni della regola di trasporto

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2017-05-03_

Le azioni nelle regole del flusso di posta elettronica (note anche come regole di trasporto) specificano l'oggetto da eseguire per i messaggi che soddisfano le condizioni della regola. Ad esempio, è possibile creare una regola che inoltra messaggi da mittenti specifici a un moderatore o aggiunge una dichiarazione di non responsabilità o una firma personalizzata a tutti i messaggi in uscita.

In genere, per le azioni sono necessarie proprietà aggiuntive. Ad esempio, quando la regola reindirizza un messaggio, è necessario specificare la posizione cui reindirizzare il messaggio. Alcune azioni hanno più proprietà che sono disponibili o richieste. Ad esempio, quando la regola aggiunge un campo di intestazione all'intestazione del messaggio, è necessario specificare sia il nome che il valore dell'intestazione. Quando la regola aggiunge una dichiarazione di non responsabilità ai messaggi, è necessario specificare il testo della dichiarazione di non responsabilità, ma è inoltre possibile specificare la posizione in cui inserire il testo o cosa fare se la dichiarazione di non responsabilità non può essere aggiunta al messaggio. In genere, è possibile configurare più azioni in una regola, ma alcune azioni sono esclusive. Ad esempio, una regola non può rifiutare e reindirizzare il messaggio stesso.

Per ulteriori informazioni sulle regole del flusso di posta in Exchange Server 2013, vedere [Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

Per ulteriori informazioni sulle condizioni e le eccezioni nelle regole del flusso di posta, vedere [Condizioni delle regole di trasporto (predicati)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

Per ulteriori informazioni sulle azioni nelle regole del flusso di posta in Exchange Online o Exchange Online Protection, vedere [Posta azioni delle regole del flusso di Exchange Online](https://technet.microsoft.com/it-it/library/jj919237\(v=exchg.150\)) o [Posta elettronica di azioni delle regole del flusso di Exchange Online Protection](https://technet.microsoft.com/it-it/library/jj920117\(v=exchg.150\)).

## Azioni per le regole del flusso di posta nei server delle cassette postali

Le azioni disponibili nelle regole del flusso di posta nei server delle cassette postali sono descritte nella tabella seguente. I valori validi per ogni proprietà sono descritti nella sezione Valori delle proprietà.

**Note**:

  - Dopo aver selezionato un'azione in Interfaccia di amministrazione di Exchange (EAC), il valore che viene visualizzato alla fine nel campo **Eseguire le operazioni seguenti** spesso è diverso dal percorso selezionato. Inoltre, quando si creano nuove regole, è possibile talvolta (in base alle selezioni effettuate) selezionare un nome azione breve da un modello (un elenco filtrato delle azioni) invece di seguire il percorso selezionabile completo. I nomi brevi e i valori dei percorsi selezionabili completi vengono visualizzati nella colonna EAC della tabella.

  - I nomi di alcune delle azioni restituite dal cmdlet **Get-TransportRuleAction** sono diversi dai nomi dei parametri corrispondenti e un’azione potrebbe richiedere più parametri.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Azione in EAC</th>
<th>Parametro di azione in Exchange Management Shell</th>
<th>Proprietà</th>
<th>Descrizione</th>
<th>Disponibile in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Inoltra il messaggio per l'approvazione a queste persone</strong></p>
<p><strong>Inoltra il messaggio per l'approvazione</strong> &gt; <strong>a queste persone</strong></p></td>
<td><p><em>ModerateMessageByUser</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Inoltra il messaggio ai moderatori specificati come allegato a una richiesta di approvazione. Per ulteriori informazioni, vedere <a href="common-message-approval-scenarios-exchange-2013-help.md">Scenari comuni di approvazione messaggio</a>. Tenere presente che non è possibile utilizzare un gruppo di distribuzione come moderatore.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Inoltra il messaggio per l'approvazione al gestore del mittente</strong></p>
<p><strong>Inoltra il messaggio per l'approvazione</strong> &gt; <strong>al gestore del mittente</strong></p></td>
<td><p><em>ModerateMessageByManager</em></p></td>
<td><p>n/d</p></td>
<td><p>Inoltra il messaggio al gestore del mittente per l'approvazione.</p>
<p>Questa operazione funziona solo se l’attributo <strong>Manager</strong> del mittente è definito in Active Directory. In caso contrario, il messaggio viene recapitato ai destinatari senza moderazione.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Consente di reindirizzare il messaggio a questi destinatari</strong></p>
<p><strong>Consente di reindirizzare il messaggio a</strong> &gt; <strong>questi destinatari</strong></p></td>
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Reindirizza il messaggio ai destinatari specificati. Il messaggio non viene recapitato ai destinatari originali e non viene inviata nessuna notifica né a questi né al mittente.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Rifiuta il messaggio e includi la spiegazione</strong></p>
<p><strong>Blocca il messaggio</strong> &gt; <strong>Rifiuta il messaggio e includi una spiegazione</strong></p></td>
<td><p><em>RejectMessageReasonText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Restituisce il messaggio al mittente in un rapporto di mancato recapito (noto anche come rapporto di mancato recapito o messaggio di e-mail non recapitato) con il testo specificato come motivo del rifiuto. Il destinatario non riceve il messaggio originale o la notifica.</p>
<p>Il codice di stato avanzato predefinito utilizzato è <code>5.7.1</code>.</p>
<p>Quando si crea o si modifica la regola in Exchange Management Shell, è possibile specificare il codice DSN utilizzando il parametro <em>RejectMessageEnhancedStatusCode</em>.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rifiuta il messaggio con codice di stato avanzato</strong></p>
<p><strong>Blocca il messaggio</strong> &gt; <strong>Rifiuta il messaggio con codice di stato avanzato</strong></p></td>
<td><p><em>RejectMessageEnhancedStatusCode</em></p></td>
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>Restituisce il messaggio al mittente in un rapporto di mancato recapito con il codice di notifica (DSN) sullo stato del recapito avanzato specificato. Il destinatario non riceve il messaggio originale o la notifica.</p>
<p>Codici DSN validi sono <code>5.7.1</code> o <code>5.7.900</code> tramite <code>5.7.999</code>.</p>
<p>Il testo del motivo predefinito utilizzato è <code>Delivery not authorized, message refused</code>.</p>
<p>Quando si crea o si modifica la regola in Exchange Management Shell, è possibile specificare il testo del motivo del rifiuto utilizzando il parametro <em>RejectMessageReasonText</em>.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Elimina il messaggio senza inviare alcuna notifica</strong></p>
<p><strong>Blocca il messaggio</strong> &gt; <strong>Elimina il messaggio senza inviare alcuna notifica</strong></p></td>
<td><p><em>DeleteMessage</em></p></td>
<td><p>n/d</p></td>
<td><p>Rimuove il messaggio di posta elettronica senza inviare alcuna notifica né al mittente né al destinatario.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Aggiungi destinatari alla casella Ccn</strong></p>
<p><strong>Aggiungi destinatari</strong> &gt; <strong>alla casella Ccn</strong></p></td>
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Aggiunge uno o più destinatari nel campo <strong>Bcc</strong> del messaggio. I destinatari originali non ricevono notifica e non possono leggere gli indirizzi aggiuntivi.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Aggiungi destinatari alla casella A</strong></p>
<p><strong>Aggiungi destinatari</strong> &gt; <strong>alla casella A</strong></p></td>
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Aggiunge uno o più destinatari nel campo <strong>To</strong> del messaggio. I destinatari originali possono leggere gli indirizzi aggiuntivi.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Aggiungi destinatari alla casella Cc</strong></p>
<p><strong>Aggiungi destinatari</strong> &gt; <strong>alla casella Cc</strong></p></td>
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Aggiunge uno o più destinatari nel campo <strong>Cc</strong> del messaggio. I destinatari originali possono leggere l’indirizzo.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Aggiungi il responsabile del mittente come destinatario</strong></p>
<p><strong>Aggiungi destinatari</strong> &gt; <strong>Aggiungi il responsabile del mittente come destinatario</strong></p></td>
<td><p><em>AddManagerAsRecipientType</em></p></td>
<td><p><code>AddedManagerAction</code></p></td>
<td><p>Aggiunge il responsabile del mittente al messaggio come tipo di destinatario specificato (<strong>To</strong>, <strong>Cc</strong>, <strong>Bcc</strong>) o reindirizza il messaggio al gestore del mittente senza indicare il mittente o il destinatario.</p>
<p>Questa operazione funziona solo se l’attributo <strong>Manager</strong> del mittente è definito in Active Directory.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Aggiungi una dichiarazione di non responsabilità</strong></p>
<p><strong>Inserisci una dichiarazione di non responsabilità nel messaggio</strong> &gt; <strong>Aggiungi una dichiarazione di non responsabilità</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>Proprietà principale: <code>DisclaimerText</code></p>
<p>Proprietà secondaria: <code>DisclaimerFallbackAction</code></p>
<p>Proprietà terza (solo Exchange Management Shell): <code>DisclaimerTextLocation</code></p></td>
<td><p>Si applica la dichiarazione di non responsabilità HTML specificata alla fine del messaggio.</p>
<p>Quando si crea o si modifica la regola in Exchange Management Shell, utilizzare il parametro <em>ApplyHtmlDisclaimerTextLocation</em> con il valore <code>Append</code>.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Anteponi una dichiarazione di responsabilità</strong></p>
<p><strong>Inserisci una dichiarazione di non responsabilità nel messaggio</strong> &gt; <strong>Anteponi una dichiarazione di non responsabilità</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>Proprietà principale: <code>DisclaimerText</code></p>
<p>Proprietà secondaria: <code>DisclaimerFallbackAction</code></p>
<p>Proprietà terza (solo Exchange Management Shell): <code>DisclaimerTextLocation</code></p></td>
<td><p>Si applica la dichiarazione di non responsabilità HTML specificata all’inizio del messaggio.</p>
<p>Quando si crea o si modifica la regola in Exchange Management Shell, utilizzare il parametro <em>ApplyHtmlDisclaimerTextLocation</em> con il valore <code>Prepend</code>.</p>
<p></p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rimuovi questa intestazione</strong></p>
<p><strong>Modifica le proprietà dei messaggi</strong> &gt; <strong>Rimuovi un'intestazione del messaggio</strong></p></td>
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Rimuove il campo di intestazione specificato da un’intestazione del messaggio.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Imposta l'intestazione del messaggio su questo valore</strong></p>
<p><strong>Modifica le proprietà dei messaggi</strong> &gt; <strong>Imposta un'intestazione del messaggio</strong></p></td>
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>Proprietà principale: <code>MessageHeaderField</code></p>
<p>Proprietà secondaria: <code>String</code></p></td>
<td><p>Aggiunge o modifica il campo di intestazione specificato nell'intestazione del messaggio e imposta il campo di intestazione sul valore specificato.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Applica una classificazione dei messaggi</strong></p>
<p><strong>Modifica le proprietà dei messaggi</strong> &gt; <strong>Applica una classificazione di messaggi</strong></p></td>
<td><p><em>ApplyClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>Applica una classificazione dei messaggi specifica a un messaggio.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Imposta il livello di probabilità di posta indesiderata su</strong></p>
<p><strong>Modifica le proprietà del messaggio</strong> &gt; <strong>Imposta il livello di probabilità di posta indesiderata</strong></p></td>
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Imposta il livello di probabilità di posta indesiderata del messaggio sul valore specificato.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Applica protezione dei diritti al messaggio con</strong></p>
<p><strong>Modifica la sicurezza del messaggio</strong> &gt; <strong>Applica protezione dei diritti</strong></p></td>
<td><p><em>ApplyRightsProtectionTemplate</em></p></td>
<td><p><code>RMSTemplate</code></p></td>
<td><p>Applica al messaggio il modello RMS (Rights Management Services) specificato.</p>
<p>RMS richiede Exchange licenze CAL (Client Access License) Enterprise per ogni cassetta postale. Per ulteriori informazioni sulle licenze CAL, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=23729">Domande frequenti sulle licenze di Exchange</a>.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Richiedi crittografia TLS</strong></p>
<p><strong>Modifica la sicurezza del messaggio</strong> &gt; <strong>Richiede la crittografia TLS</strong></p></td>
<td><p><em>RouteMessageOutboundRequireTls</em></p></td>
<td><p><code>n/a</code></p></td>
<td><p>Impone l'indirizzamento dei messaggi in uscita tramite connessione crittografata TLS.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Anteponi all'oggetto del messaggio</strong></p></td>
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Consente di aggiungere il testo specificato all'inizio del campo <strong>Subject</strong> del messaggio. Valutare l'uso di uno spazio o dei due punti (:) come ultimo carattere del testo specificato per distinguerlo dal testo dell'oggetto originale.</p>
<p>Per impedire che la stessa stringa venga aggiunta ai messaggi che contengono già il testo nell'oggetto (ad esempio, risposte), aggiungere l’eccezione <strong>L’oggetto include</strong> (<em>ExceptIfSubjectContainsWords</em>) alla regola.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Notifica al mittente con un suggerimento per il criterio</strong></p></td>
<td><p><em>NotifySender</em></p>
<p><em>RejectMessageReasonText</em></p>
<p><em>RejectMessageEnhancedStatusCode</em> (solo Exchange Management Shell)</p></td>
<td><p>Proprietà principale: <code>NotifySenderType</code></p>
<p>Proprietà secondaria: <code>String</code></p>
<p>Proprietà terza (solo Exchange Management Shell): <code>DSNEnhancedStatusCode</code></p></td>
<td><p>Notifica il mittente o blocca il messaggio quando il messaggio corrisponde a un criterio DLP.</p>
<p>Quando si utilizza questa azione, è necessario utilizzare la condizione <strong>Il messaggio contiene informazioni riservate</strong> (<em>MessageContainsDataClassification</em>).</p>
<p>Quando si crea o si modifica la regola in Exchange Management Shell, il parametro <em>RejectMessageReasonText</em> è facoltativo. Se non si utilizza questo parametro, viene utilizzato il testo predefinito <code>Delivery not authorized, message refused</code>.</p>
<p>In Exchange Management Shell, è inoltre possibile utilizzare il parametro <em>RejectMessageEnhancedStatusCode</em> per specificare il codice di stato avanzato. Se non si utilizza questo parametro, viene utilizzato il codice di stato avanzato predefinito <code>5.7.1</code>.</p>
<p>Questa azione consente di limitare altre condizioni, eccezioni e azioni per la configurazione nella regola.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Genera il rapporto degli eventi imprevisti e invialo a</strong></p></td>
<td><p><em>GenerateIncidentReport</em></p>
<p><em>IncidentReportContent</em></p></td>
<td><p>Proprietà principale: <code>Addresses</code></p>
<p>Proprietà secondaria: <code>IncidentReportContent</code></p></td>
<td><p>Invia un rapporto operazioni non consentite che contiene il contenuto specificato ai destinatari specificati.</p>
<p>Un rapporto sulle operazioni non consentite viene generato per i messaggi che corrispondono a criteri DLP dell'organizzazione.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Invia una notifica al destinatario tramite messaggio</strong></p></td>
<td><p><em>GenerateNotification</em></p></td>
<td><p><code>NotificationMessageText</code></p></td>
<td><p>Specifica testo, tag HTML e parole chiave del messaggio da includere nel messaggio di notifica che viene inviato ai destinatari del messaggio. Ad esempio, è possibile informare i destinatari che un messaggio è stato rifiutato dalla regola oppure è stato contrassegnato come posta indesiderata e recapitato nella cartella Posta indesiderata.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Proprietà della regola</strong> sezione &gt; <strong>Controlla questa regola con livello di gravità</strong></p></td>
<td><p><em>SetAuditSeverity</em></p></td>
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>Specifica se:</p>
<ul>
<li><p>Impedire la generazione di un rapporto operazioni non consentite e la voce corrispondente nel Registro di verifica dei messaggi.</p></li>
<li><p>Generare un rapporto operazioni non consentite e la voce corrispondente nel Registro di verifica messaggio con il livello di gravità specificato (basso, medio o alto).</p></li>
</ul></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Proprietà della regola</strong> sezione &gt; <strong>Arrestare l'elaborazione di più regole</strong></p>
<p><strong>Altre opzioni</strong> &gt; <strong>Proprietà della regola</strong> sezione &gt; <strong>Arrestare l'elaborazione di più regole</strong></p></td>
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>n/d</p></td>
<td><p>Specifica che dopo che la regola è influenzata dal messaggio, il messaggio è escluso dall’elaborazione da altre regole.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Azioni per le regole del flusso di posta nei server Trasporto Edge

Un piccolo sottoinsieme di azioni disponibili nei server della cassetta postale sono disponibili anche nei server Trasporto Edge, ma esistono anche alcune azioni che sono disponibili solo in server Trasporto Edge. Non esiste alcun EAC nei server Trasporto Edge, in modo che è possibile gestire solo regole del flusso di posta elettronica in Exchange Management Shell sul server Trasporto Edge locale. Le operazioni sono descritte nella tabella seguente. I tipi di proprietà sono descritti nella sezione Valori proprietà.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro di azione in Exchange Management Shell</th>
<th>Proprietà</th>
<th>Descrizione</th>
<th>Disponibile su</th>
<th>Disponibile in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Aggiunge uno o più destinatari nel campo <strong>To</strong> del messaggio. I destinatari originali possono leggere gli indirizzi aggiuntivi.</p></td>
<td><p>Cassette postali e server Trasporto Edge</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Aggiunge uno o più destinatari nel campo <strong>Bcc</strong> del messaggio. I destinatari originali non ricevono notifica e non possono leggere gli indirizzi aggiuntivi.</p></td>
<td><p>Cassette postali e server Trasporto Edge</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Aggiunge uno o più destinatari nel campo <strong>Cc</strong> del messaggio. I destinatari originali possono leggere l’indirizzo.</p></td>
<td><p>Cassette postali e server Trasporto Edge</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>DeleteMessage</em></p></td>
<td><p>n/d</p></td>
<td><p>Rimuove il messaggio di posta elettronica senza inviare alcuna notifica né al mittente né al destinatario.</p></td>
<td><p>Cassette postali e server Trasporto Edge</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><em>Disconnect</em></p></td>
<td><p>n/d</p></td>
<td><p>Interrompe la connessione SMTP tra il server di invio e il server Trasporto Edge senza generare un NDR.</p></td>
<td><p>Solo server Trasporto Edge</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>LogEventText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Genera un evento con il testo specificato nel registro dell'applicazione del server Trasporto Edge locale. Ogni voce include le seguenti informazioni:</p>
<ul>
<li><p><strong>Livello</strong>   <code>Information</code></p></li>
<li><p><strong>Origine</strong>   <code>MSExchange Messaging Policies</code></p></li>
<li><p><strong>ID evento</strong>   <code>4000</code></p></li>
<li><p><strong>Categoria attività</strong>   <code>Rules</code></p></li>
<li><p><strong>EventData</strong>   <code>The following message is logged by an action in the rules: &lt;text you specify&gt;.</code></p></li>
</ul></td>
<td><p>Solo server Trasporto Edge</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Consente di aggiungere il testo specificato all'inizio del campo <strong>Subject</strong> del messaggio. Valutare l'uso di uno spazio o dei due punti (:) come ultimo carattere del testo specificato per distinguerlo dall’oggetto originale.</p></td>
<td><p>Cassette postali e server Trasporto Edge</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>Quarantine</em></p></td>
<td><p>n/d</p></td>
<td><p>Recapita il messaggio nella cassetta postale per la quarantena definito nella configurazione del filtro contenuto sul server Trasporto Edge. Per ulteriori informazioni, vedere <a href="configure-a-spam-quarantine-mailbox-exchange-2013-help.md">Configurare una cassetta postale di quarantena della posta indesiderata</a>.</p>
<p>Se non è configurata una cassetta postale per la quarantena, viene restituito il messaggio al mittente in un rapporto di mancato recapito.</p></td>
<td><p>Solo server Trasporto Edge</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Reindirizza il messaggio ai destinatari specificati. Il messaggio non viene recapitato ai destinatari originali e non viene inviata nessuna notifica né a questi né al mittente.</p></td>
<td><p>Cassette postali e server Trasporto Edge</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Rimuove il campo di intestazione specificato da un’intestazione del messaggio.</p></td>
<td><p>Cassette postali e server Trasporto Edge</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>Proprietà principale: <code>MessageHeaderField</code></p>
<p>Proprietà secondaria: <code>String</code></p></td>
<td><p>Aggiunge o modifica il campo di intestazione specificato nell'intestazione del messaggio e imposta il campo di intestazione sul valore specificato.</p></td>
<td><p>Cassette postali e server Trasporto Edge</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Imposta il livello di probabilità di posta indesiderata del messaggio sul valore specificato.</p></td>
<td><p>Cassette postali e server Trasporto Edge</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><em>SmtpRejectMessageRejectText</em></p>
<p><em>SmtpRejectMessageRejectStatusCode</em></p></td>
<td><p>Proprietà principale: <code>String</code></p>
<p>Proprietà secondaria: <code>SMTPStatusCode</code></p></td>
<td><p>Termina la connessione SMTP tra il server mittente e il server Trasporto Edge con il codice di stato SMTP specificato e il testo di rifiuto specificato. Il destinatario non riceve il messaggio originale o la notifica.</p>
<p>I valori validi per il codice di stato SMTP sono numeri interi da <code>400</code> a <code>500</code> come definito in RFC 3463.</p>
<p>Se si digita il testo di rifiuto senza specificare il codice di stato SMTP, viene utilizzato il codice predefinito <code>550</code>.</p>
<p>Se si specifica il codice di stato SMTP senza specificare il testo di rifiuto, il testo che viene utilizzato è <code>Delivery not authorized, message refused</code>.</p></td>
<td><p>Solo server Trasporto Edge</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>n/d</p></td>
<td><p>Specifica che dopo che la regola è influenzata dal messaggio, il messaggio è escluso dall’elaborazione da altre regole.</p></td>
<td><p>Cassette postali e server Trasporto Edge</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
</tbody>
</table>


## Valori delle proprietà

I valori delle proprietà utilizzati per le operazioni nelle regole del flusso di posta elettronica sono descritti nella tabella seguente.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Proprietà</th>
<th>Valori validi</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>AddedManagerAction</code></p></td>
<td><p>Uno dei seguenti valori:</p>
<ul>
<li><p><strong>A</strong></p></li>
<li><p><strong>Cc</strong></p></li>
<li><p><strong>Ccn</strong></p></li>
<li><p><strong>Reindirizza</strong></p></li>
</ul></td>
<td><p>Specifica come includere il responsabile del mittente nei messaggi.</p>
<ul>
<li><p>Se si seleziona <strong>A</strong>, <strong>Cc</strong> o <strong>Ccn</strong>, il responsabile del mittente viene aggiunto come destinatario nel campo specificato.</p></li>
<li><p>Se si seleziona <strong>Reindirizza</strong>, il messaggio viene recapitato solo al responsabile del mittente senza indicare il mittente o il destinatario.</p></li>
</ul>
<p>Questa operazione funziona solo se l’attributo <strong>Manager</strong> del mittente è definito in Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Destinatari di Exchange</p></td>
<td><p>In base all'operazione, l’utente può specificare qualsiasi oggetto abilitato alla posta elettronica dell'organizzazione o potrebbe essere limitato a un tipo di oggetto specifico. In genere, è possibile selezionare più destinatari, ma è possibile inviare un rapporto operazioni non consentite solo a un destinatario.</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>Uno dei seguenti valori:</p>
<ul>
<li><p>Deselezionare <strong>Controlla questa regola con livello di gravità</strong> oppure selezionare <strong>Controllare questa regola con livello di gravità</strong> con il valore <strong>Non specificato</strong> (<code>DoNotAudit</code>)</p></li>
<li><p><strong>Basso</strong></p></li>
<li><p><strong>Medio</strong></p></li>
<li><p><strong>Alto</strong></p></li>
</ul></td>
<td><p>I valori <strong>Basso</strong>, <strong>Medio</strong> o <strong>Alto</strong> specificano il livello di gravità assegnato al rapporto operazioni non consentite e la voce corrispondente nel Registro di verifica messaggio.</p>
<p>L'altro valore impedisce la generazione di un rapporto operazioni non consentite e impedisce di scrivere la voce corrispondente nel Registro di verifica messaggio.</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerFallbackAction</code></p></td>
<td><p>Uno dei seguenti valori:</p>
<ul>
<li><p><strong>Racchiudi</strong></p></li>
<li><p><strong>Ignora</strong></p></li>
<li><p><strong>Rifiuta</strong></p></li>
</ul></td>
<td><p>Specifica cosa fare se una dichiarazione di non responsabilità non può essere applicata a un messaggio. In alcuni casi non è possibile alterare il contenuto di un messaggio, ad esempio perché è crittografato. Le azioni di fallback disponibili sono:</p>
<ul>
<li><p><strong>Racchiudi</strong>   Il messaggio originale viene &quot;racchiuso&quot; in una nuova busta del messaggio e la dichiarazione di non responsabilità viene inserita nel corpo del nuovo messaggio. Questo è il valore predefinito.</p>
<p><strong>Note</strong>:</p>
<ul>
<li><p>Le regole del flusso di posta vengono applicate alla nuova busta del messaggio, non al messaggio originale. Pertanto, è possibile configurare queste regole con una priorità più bassa rispetto alle altre.</p></li>
<li><p>Se non può essere racchiuso in una nuova busta di messaggio, il messaggio originale non viene recapitato e viene restituito al mittente in un rapporto di mancato recapito.</p></li>
</ul></li>
<li><p><strong>Ignora</strong>   La regola viene ignorata e il messaggio viene recapitato senza la dichiarazione di non responsabilità</p></li>
<li><p><strong>Rifiuta</strong>   Il messaggio viene restituito al mittente in un rapporto di mancato recapito.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DisclaimerText</code></p></td>
<td><p>Stringa HTML</p></td>
<td><p>Specifica il testo della dichiarazione di non responsabilità, che può includere tag HTML, tag foglio di stile CSS inline e le immagini utilizzando il tag IMG. La lunghezza massima è 5000 caratteri, tag inclusi.</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerTextLocation</code></p></td>
<td><p>Valore singolo: <code>Append</code> o <code>Prepend</code></p></td>
<td><p>In Exchange Management Shell, si utilizza <em>ApplyHtmlDisclaimerTextLocation</em> per specificare la posizione del testo dichiarazione di non responsabilità nel messaggio:</p>
<ul>
<li><p><code>Append</code>   Aggiungi la dichiarazione di non responsabilità alla fine del corpo del messaggio. Questo è il valore predefinito.</p></li>
<li><p><code>Prepend</code>   Aggiungi la dichiarazione di non responsabilità all’inizio del corpo del messaggio.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>Valore codice DSN singolo:</p>
<ul>
<li><p><code>5.7.1</code></p></li>
<li><p>Da <code>5.7.900</code> a <code>5.7.999</code></p></li>
</ul></td>
<td><p>Specifica il codice DSN utilizzato. È possibile creare DSN personalizzati utilizzando il cmdlet <strong>New-SystemMessage</strong>.</p>
<p>Se non si specifica il testo del motivo del rifiuto insieme al codice DSN, il testo del motivo predefinito utilizzato è <code>Delivery not authorized, message refused</code>.</p>
<p>Quando si crea o si modifica la regola in Exchange Management Shell, è possibile specificare il testo del motivo del rifiuto utilizzando il parametro <em>RejectMessageReasonText</em>.</p></td>
</tr>
<tr class="even">
<td><p><code>IncidentReportContent</code></p></td>
<td><p>Uno o più dei valori seguenti:</p>
<ul>
<li><p><strong>Mittente</strong></p></li>
<li><p><strong>Destinatari</strong></p></li>
<li><p><strong>Oggetto</strong></p></li>
<li><p><strong>Destinatari Cc</strong> (<code>Cc</code>)</p></li>
<li><p><strong>Destinatari Ccn</strong> (<code>Bcc</code>)</p></li>
<li><p><strong>Gravità</strong></p></li>
<li><p><strong>Informazioni su override mittente</strong> (<code>Override</code>)</p></li>
<li><p><strong>Regole di corrispondenza</strong> (<code>RuleDetections</code>)</p></li>
<li><p><strong>Percentuale di falsi positivi</strong> (<code>FalsePositive</code>)</p></li>
<li><p><strong>Classificazioni dei dati rilevati</strong> (<code>DataClassifications</code>)</p></li>
<li><p><strong>Contenuto corrispondente</strong> (<code>IdMatch</code>)</p></li>
<li><p><strong>Messaggio originale</strong> (<code>AttachOriginalMail</code>)</p></li>
</ul></td>
<td><p>Specifica le proprietà del messaggio originale da includere nel rapporto operazioni non consentite. È possibile scegliere di includere qualsiasi combinazione di queste proprietà. Oltre alle proprietà specificate viene sempre incluso l'ID messaggio. Le proprietà disponibili sono:</p>
<ul>
<li><p><strong>Mittente</strong>   Il mittente del messaggio originale.</p></li>
<li><p><strong>Destinatari</strong>, <strong>Destinatari Cc</strong> e <strong>Destinatari Ccn</strong>   Tutti i destinatari del messaggio o solo i destinatari nei campi <strong>Cc</strong> o <strong>Bcc</strong>. Per ogni proprietà, nel rapporto operazioni non consentite sono inclusi solo i primi 10 destinatari.</p></li>
<li><p><strong>Oggetto</strong>   Il campo <strong>Subject</strong> del messaggio originale.</p></li>
<li><p><strong>Gravità</strong>   Consente di specificare la gravità relativa al controllo della regola che è stata attivata. I registri di verifica messaggio includono tutti i livelli di gravità del controllo. Inoltre, è possibile filtrarli in base al livello di gravità del controllo. In EAC, se si deseleziona la casella di controllo <strong>Controlla questa regola con livello di gravità</strong> (in Exchange Management Shell, il valore del parametro <em>SetAuditSeverity</em><code>DoNotAudit</code>), le corrispondenze della regola non verranno visualizzate nei report. Se un messaggio viene elaborato da più di una regola, il massimo livello di gravità viene incluso in qualsiasi rapporto operazioni non consentite.</p></li>
<li><p><strong>Informazioni su override mittente</strong>   L’override se il mittente ha scelto di sostituire un suggerimento per i criteri. Se il mittente ha fornito una giustificazione, vengono inclusi anche i primi 100 caratteri della giustificazione.</p></li>
<li><p><strong>Regole corrispondenti</strong>    Include l'elenco delle regole attivate dal messaggio.</p></li>
<li><p><strong>Rapporti Falso positivo</strong>   Il falso positivo se il mittente ha contrassegnato il messaggio come falso positivo per un suggerimento per i criteri.</p></li>
<li><p><strong>Classificazioni dati rilevati</strong>   L'elenco dei tipi di informazioni sensibili rilevato nel messaggio.</p></li>
<li><p><strong>Contenuto corrispondente</strong>   Il tipo di informazioni sensibili rilevato, il contenuto del messaggio con la corrispondenza esatta e i 150 caratteri prima e dopo la corrispondenza delle informazioni riservate.</p></li>
<li><p><strong>Messaggio originale</strong>   L'intero messaggio che ha attivato la regola è allegato al rapporto operazioni non consentite.</p></li>
</ul>
<p>In Exchange Management Shell, è possibile specificare più valori separati da virgole.</p></td>
</tr>
<tr class="odd">
<td><p><code>MessageClassification</code></p></td>
<td><p>Oggetto singolo classificazione dei messaggi</p></td>
<td><p>In EAC, è possibile selezionare dall'elenco di classificazioni dei messaggi disponibili.</p>
<p>In Exchange Management Shell, utilizzare il cmdlet <strong>Get-MessageClassification</strong> per visualizzare la classificazione dei messaggi per gli oggetti che sono disponibili.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Stringa singola</p></td>
<td><p>Specifica il campo di intestazione del messaggio SMTP da aggiungere, rimuovere o modificare.</p>
<p>L'<em>intestazione del messaggio</em> è una raccolta di campi di intestazione obbligatori e facoltativi nel messaggio. Esempi di campi di intestazione sono <strong>To</strong>, <strong>From</strong>, <strong>Received</strong> e <strong>Content-Type</strong>. I campi di intestazione ufficiali sono definiti nel documento RFC 5322. I campi di intestazione non ufficiali iniziano con <strong>X-</strong> e sono noti come <em>X-Header</em>.</p></td>
</tr>
<tr class="odd">
<td><p><code>NotificationMessageText</code></p></td>
<td><p>Qualsiasi combinazione di testo normale, tag HTML e parole chiave</p></td>
<td><p>Il testo da utilizzare in un messaggio di notifica del destinatario specificato.</p>
<p>Oltre a testo normale e tag HTML, è possibile specificare le seguenti parole chiave che utilizzano i valori dal messaggio originale:</p>
<ul>
<li><p><code>%%From%%</code></p></li>
<li><p><code>%%To%%</code></p></li>
<li><p><code>%%Cc%%</code></p></li>
<li><p><code>%%Subject%%</code></p></li>
<li><p><code>%%Headers%%</code></p></li>
<li><p><code>%%MessageDate%%</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>NotifySenderType</code></p></td>
<td><p>Uno dei seguenti valori:</p>
<ul>
<li><p><strong>Notifica al mittente, ma consentigli di procedere con l'invio</strong> (<code>NotifyOnly</code>)</p></li>
<li><p><strong>Blocca il messaggio</strong> (<code>RejectMessage</code>)</p></li>
<li><p><strong>Blocca il messaggio, a meno che non è un falso positivo</strong> (<code>RejectUnlessFalsePositiveOverride</code>)</p></li>
<li><p><strong>Blocca il messaggio, ma consenti al mittente di eseguire l'override e di procedere con l’invio</strong> (<code>RejectUnlessSilentOverride</code>)</p></li>
<li><p><strong>Blocca il messaggio, ma consenti all'utente di eseguire l'override con una giustificazione aziendale e inviare il messaggio</strong> (<code>RejectUnlessExplicitOverride</code>)</p></li>
</ul></td>
<td><p>Specifica il tipo di suggerimento per i criteri che il mittente riceve se il messaggio viola i criteri DLP. Le impostazioni vengono descritte nell'elenco seguente:</p>
<ul>
<li><p><strong>Notifica al mittente, ma consentigli di procedere con l'invio</strong> Il mittente riceve una notifica, ma il messaggio viene recapitato normalmente.</p></li>
<li><p><strong>Blocca il messaggio</strong>   Il messaggio viene rifiutato e viene inviata una notifica al mittente.</p></li>
<li><p><strong>Blocca il messaggio, a meno che non è un falso positivo</strong> Il messaggio viene rifiutato a meno che non venga contrassegnato come falso positivo dal mittente.</p></li>
<li><p><strong>Blocca il messaggio, ma consenti al mittente di eseguire l'override e di procedere con l’invio</strong> Il messaggio viene rifiutato, a meno che il mittente non abbia scelto di ignorare la restrizione del criterio.</p></li>
<li><p><strong>Blocca il messaggio, ma consenti all'utente di eseguire l'override con una giustificazione aziendale e inviare il messaggio</strong> È simile al tipo <strong>Blocca il messaggio, ma consenti al mittente di eseguire l'override e di procedere con l’invio</strong>, ma il mittente fornisce anche una giustificazione per ignorare la restrizione del criterio.</p></li>
</ul>
<p>Quando si utilizza questa azione, è necessario utilizzare la condizione <strong>Il messaggio contiene informazioni riservate</strong> (<em>MessageContainsDataClassification</em>).</p></td>
</tr>
<tr class="odd">
<td><p><code>RMSTemplate</code></p></td>
<td><p>Oggetto modello RMS singolo</p></td>
<td><p>Specifica il modello RMS (Rights Management Services) applicato al messaggio.</p>
<p>In EAC, selezionare il modello RMS da un elenco.</p>
<p>In Exchange Management Shell, utilizzare il cmdlet <strong>Get-RMSTemplate</strong> per visualizzare i modelli RMS disponibili.</p>
<p>RMS richiede Exchange licenze CAL (Client Access License) Enterprise per ogni cassetta postale. Per ulteriori informazioni sulle licenze CAL, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=23729">Domande frequenti sulle licenze di Exchange</a>.</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>Uno dei seguenti valori:</p>
<ul>
<li><p><strong>Ignora il filtro posta indesiderata</strong> (<code>-1</code>)</p></li>
<li><p>Numeri interi da 0 a 9</p></li>
</ul></td>
<td><p>Specifica il livello di probabilità di posta indesiderata (SCL) assegnato al messaggio. Più alto è il valore di SCL, maggiore è la probabilità che si tratti di un messaggio di posta indesiderata.</p></td>
</tr>
<tr class="odd">
<td><p><code>String</code></p></td>
<td><p>Stringa singola</p></td>
<td><p>Specifica il testo che viene applicato al campo di intestazione, al rapporto di mancato recapito o alla voce di registro eventi del messaggio specificato.</p>
<p>In Exchange Management Shell, se il valore contiene degli spazi, è necessario racchiuderlo tra virgolette (&quot;).</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Ulteriori informazioni

[Gestire le regole di flusso di posta elettronica](manage-mail-flow-rules-exchange-2013-help.md)

[Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Condizioni delle regole di trasporto (predicati)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Posta azioni delle regole del flusso di Exchange Online](https://technet.microsoft.com/it-it/library/jj919237\(v=exchg.150\)) per Exchange Online

[Posta elettronica di azioni delle regole del flusso di Exchange Online Protection](https://technet.microsoft.com/it-it/library/jj920117\(v=exchg.150\)) per Exchange Online Protection

[Intestazioni, piè di pagina, firme o dichiarazioni di non responsabilità nei messaggi per tutta l'organizzazione in Office 365](https://technet.microsoft.com/it-it/library/dn600323\(v=exchg.150\))


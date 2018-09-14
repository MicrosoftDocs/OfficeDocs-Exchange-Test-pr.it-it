---
title: 'Condizioni delle regole di trasporto (predicati): Exchange 2013 Help'
TOCTitle: Condizioni ed eccezioni della regola del flusso di posta (predicati)
ms:assetid: c918ea00-1e68-4b8b-8d51-6966b4432e2d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638183(v=EXCHG.150)
ms:contentKeyID: 50481655
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Condizioni delle regole di trasporto (predicati)

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-12-20_

Le condizioni e le eccezioni nelle regole del flusso di posta (note anche come regole di trasporto) identificano i messaggi a cui una regola viene applicata o non viene applicata. Se la regola aggiunge una dichiarazione di non responsabilità ai messaggi, ad esempio, è possibile configurarla perché venga applicata solo ai messaggi contenenti parole specifiche, ai messaggi inviati da utenti specifici o a tutti i messaggi tranne quelli inviati dai membri di un gruppo specifico. Collettivamente, le condizioni e le eccezioni nelle regole del flusso di posta sono anche note come *predicati* poiché per ogni condizione esiste un'eccezione corrispondente che utilizza le stesse esatte impostazioni e sintassi. L'unica differenza è che le condizioni specificano i messaggi da includere mentre le eccezioni specificano i messaggi da escludere.

La maggior parte delle condizioni e delle eccezioni presenta una proprietà che richiede uno o più valori. Ad esempio, la condizione **Il mittente è** richiede che si specifichi il mittente del messaggio. Alcune condizioni dispongono di due proprietà. Ad esempio, la condizione **Un'intestazione di messaggio include una di queste parole** richiede una proprietà per specificare il campo dell'intestazione del messaggio e un'altra proprietà per specificare il testo da cercare nel campo dell'intestazione. Alcune condizioni o eccezioni non dispongono di alcuna proprietà. Ad esempio, la condizione **L'allegato ha contenuto eseguibile** consente semplicemente di cercare gli allegati dei messaggi contenenti contenuto eseguibile.

Per ulteriori informazioni sulle regole del flusso di posta in Exchange Server 2013, vedere [Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

Per ulteriori informazioni sulle condizioni ed eccezioni di regole del flusso di posta elettronica in Exchange Online Protection o Exchange Online, vedere [Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online](https://technet.microsoft.com/it-it/library/jj919235\(v=exchg.150\)) o [Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online Protection](https://technet.microsoft.com/it-it/library/jj919234\(v=exchg.150\)).

## Condizioni ed eccezioni per le regole di flusso di posta elettronica sui server cassette postali

Le tabelle nelle sezioni seguenti vengono descritte le condizioni ed eccezioni disponibili nelle regole di flusso di posta elettronica sui server cassette postali. I tipi di proprietà sono descritti nella sezione tipi di proprietà .

Mittenti

Destinatari

Oggetto del messaggio o nel corpo

Allegati

Tutti i destinatari

Tipi di informazioni riservate, dei messaggi a e Cc i valori, dimensioni e set di caratteri

Mittente e destinatario

Proprietà del messaggio

Intestazioni dei messaggi

**Note**:

  - Dopo aver selezionato una condizione o eccezione in Interfaccia di amministrazione di Exchange (EAC), il valore che viene visualizzato alla fine nel campo **Applica la regola se** o **Eccetto se** spesso è diverso (più breve) dal valore del percorso di clic selezionato. Inoltre, quando si creano nuove regole in base a un modello (un elenco filtrato di scenari), spesso è possibile selezionare un nome condizione breve anziché seguire il percorso di clic completo. I nomi brevi e i valori dei percorsi di clic completi vengono visualizzati nella colonna EAC delle tabelle.

  - Se si seleziona **\[applica a tutti i messaggi\]** in EAC, è possibile specificare altre condizioni. L'equivalente Exchange Management Shell consiste nel creare una regola senza specificare alcun parametro condizione.

  - Le impostazioni e le proprietà sono le stesse che per le condizioni e le eccezioni, pertanto l'output del cmdlet **Get-TransportRulePredicate** non riporta le eccezioni separatamente. Inoltre, i nomi di alcuni dei predicati restituiti da questo cmdlet sono diversi dai nomi dei parametri corrispondenti e un predicato potrebbe richiedere più parametri.

## Mittenti

Per le condizioni e le eccezioni che esaminano l'indirizzo del mittente, è possibile specificare il punto in cui la regola deve cercare l'indirizzo del mittente.

In EAC, nella sezione **proprietà della regola**, fare clic su **indirizzo mittente corrispondenza nel messaggio**. Si noti che potrebbe essere necessario fare clic su **altre opzioni** per visualizzare questa impostazione. In Exchange Management Shell, il parametro è *SenderAddressLocation*. I valori disponibili sono:

  - **Intestazione**    Esaminare solo i mittenti nelle intestazioni del messaggio (ad esempio, i campi **From**, **Sender**o **Reply-To** ). Questo è il valore predefinito e consente di regole del flusso di posta elettronica ha avuto esito positivo prima Exchange 2013 aggiornamento cumulativo 1 (CU1).

  - **Busta**: esaminare solo i mittenti sulla busta del messaggio (il valore **MAIL FROM** utilizzato nella trasmissione SMTP, in genere memorizzato nel campo **Return-Path**). Si noti che la ricerca sulla busta del messaggio è disponibile solo per le seguenti condizioni (e le eccezioni corrispondenti):
    
      - **Il mittente è** (*From*)
    
      - **Il mittente è un membro di** (*FromMemberOf*)
    
      - **L'indirizzo del mittente include** (*FromAddressContainsWords*)
    
      - **L'indirizzo del mittente corrisponde a** (*FromAddressMatchesPatterns*)
    
      - **Il dominio del mittente è** (*SenderDomainIs*)

  - **Intestazione o busta** (`HeaderOrEnvelope`): esaminare i mittenti inclusi nell'intestazione del messaggio e sulla busta del messaggio.


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
<th>Condizione o eccezione in EAC</th>
<th>Parametri condizione e l'eccezione in Exchange Management Shell</th>
<th>Tipo di proprietà</th>
<th>Descrizione</th>
<th>Disponibile in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Il mittente è</strong></p>
<p><strong>Il mittente</strong> &gt; <strong>è questa persona</strong></p></td>
<td><p><em>From</em></p>
<p><em>ExceptIfFrom</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messaggi inviati dalle cassette postali specificate, gli utenti di posta o contatti di posta elettronica nell'organizzazione Exchange.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Il mittente si trova in</strong></p>
<p><strong>Il mittente</strong> &gt; <strong>è esterno/interno</strong></p></td>
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>Messaggi inviati da mittenti interni o mittenti esterni.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Il mittente è un membro di</strong></p>
<p><strong>Il mittente</strong> &gt; <strong>è un membro di questo gruppo</strong></p></td>
<td><p><em>FromMemberOf</em></p>
<p><em>ExceptIfFromMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messaggi inviati da un membro del gruppo specificato.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>L'indirizzo del mittente include</strong></p>
<p><strong>Il mittente</strong> &gt; <strong>ha un indirizzo che include una di queste parole</strong></p></td>
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messaggi che contengono le parole specificate nell'indirizzo e-mail del mittente.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>L'indirizzo del mittente corrisponde a</strong></p>
<p><strong>Il mittente</strong> &gt; <strong>ha un indirizzo che corrisponde a uno di questi modelli di testo</strong></p></td>
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messaggi in cui l'indirizzo e-mail del mittente contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Le proprietà specificate del mittente includono una o più delle seguenti parole</strong></p>
<p><strong>Il mittente</strong> &gt; <strong>ha proprietà specifiche che includono una o più delle seguenti parole</strong></p></td>
<td><p><em>SenderADAttributeContainsWords</em></p>
<p><em>ExceptIfSenderADAttributeContainsWords</em></p></td>
<td><p>Proprietà principale: <code>ADAttribute</code></p>
<p>Proprietà secondaria: <code>Words</code></p></td>
<td><p>Messaggi in cui l'attributo specificato Active Directory del mittente contiene una delle parole specificate.</p>
<p>Si noti che l'attributo <strong>Country</strong> richiede il valore di codice paese a due lettere (ad esempio DE per la Germania).</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Le proprietà specificate del mittente corrispondono a questi modelli di testo</strong></p>
<p><strong>Il mittente</strong> &gt; <strong>ha proprietà specifiche che corrispondono a questi modelli</strong></p></td>
<td><p><em>SenderADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfSenderADAttributeMatchesPatterns</em></p></td>
<td><p>Proprietà principale: <code>ADAttribute</code></p>
<p>Proprietà secondaria: <code>Patterns</code></p></td>
<td><p>Messaggi in cui l'attributo specificato Active Directory del mittente contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Il mittente ha sovrascritto il suggerimento per il criterio</strong></p>
<p><strong>Il mittente</strong> &gt; <strong>ha ignorato il suggerimento per i criteri</strong></p></td>
<td><p><em>HasSenderOverride</em></p>
<p><em>ExceptIfHasSenderOverride</em></p></td>
<td><p>n/d</p></td>
<td><p>Messaggi in cui il mittente ha scelto di ignorare un criterio di prevenzione della perdita di dati (DLP). Per ulteriori informazioni sui criteri DLP, vedere <a href="https://docs.microsoft.com/it-it/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention">Prevenzione della perdita di dati</a>.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>L'indirizzo IP del mittente ricade nell'intervallo</strong></p>
<p><strong>Il mittente</strong> &gt; <strong>ha un indirizzo IP che è incluso in uno di questi intervalli o corrisponde esattamente a</strong></p></td>
<td><p><em>SenderIPRanges</em></p>
<p><em>ExceptIfSenderIPRanges</em></p></td>
<td><p><code>IPAddressRanges</code></p></td>
<td><p>Messaggi in cui l'indirizzo IP del mittente corrisponde all'indirizzo IP specificato o ricade nell'intervallo di indirizzi IP specificato.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Il dominio del mittente è</strong></p>
<p><strong>Il mittente</strong> &gt; <strong>Il dominio è</strong></p></td>
<td><p><em>SenderDomainIs</em></p>
<p><em>ExceptIfSenderDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>Messaggi in cui il dominio dell'indirizzo di posta elettronica del mittente corrisponde al valore specificato.</p>
<p>Se occorre trovare domini del mittente che <em>contengono</em> il dominio specificato, ad esempio un sottodominio di un dominio, utilizzare la condizione <strong>L'indirizzo del mittente corrisponde a</strong> (<em>FromAddressMatchesPatterns</em>) e specificare il dominio utilizzando la sintassi: <code>'@domain\.com$'</code>.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Destinatari


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
<th>Condizione o eccezione in EAC</th>
<th>Parametri condizione e l'eccezione in Exchange Management Shell</th>
<th>Tipo di proprietà</th>
<th>Descrizione</th>
<th>Disponibile in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Il destinatario è</strong></p>
<p><strong>Il destinatario</strong> &gt; <strong>è questa persona</strong></p></td>
<td><p><em>SentTo</em></p>
<p><em>ExceptIfSentTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>I messaggi in cui uno dei destinatari è la cassetta postale specificata, utente di posta elettronica o stampa contatti all'interno dell'organizzazione Exchange. I destinatari possono essere nei campi <strong>To</strong>, <strong>Cc</strong>o <strong>Bcc</strong> del messaggio.</p>
<p><strong>Nota:</strong> non è possibile specificare gruppi di distribuzione o gruppi di sicurezza abilitati alla posta. Se è necessario eseguire un'azione su messaggi inviati a un gruppo, utilizzare la condizione <strong>La casella A contiene</strong> (<em>AnyOfToHeader</em>).</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Il destinatario si trova in</strong></p>
<p><strong>Il destinatario</strong> &gt; <strong>è esterno/interno</strong></p></td>
<td><p><em>SentToScope</em></p>
<p><em>ExceptIfSentToScope</em></p></td>
<td><p><code>UserScopeTo</code></p></td>
<td><p>Messaggi inviati a destinatari interni, i destinatari esterni, i destinatari esterni nelle organizzazioni partner o destinatari esterni nelle organizzazioni partner non.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Il destinatario è un membro di</strong></p>
<p><strong>Il destinatario</strong> &gt; <strong>è un membro di questo gruppo</strong></p></td>
<td><p><em>SentToMemberOf</em></p>
<p><em>ExceptIfSentToMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messaggi che contengono destinatari che sono membri del gruppo specificato. Il gruppo può essere nei campi <strong>To</strong>, <strong>Cc</strong> o <strong>Bcc</strong> del messaggio.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>L'indirizzo del destinatario include</strong></p>
<p><strong>Il destinatario</strong> &gt; <strong>ha un indirizzo che include una di queste parole</strong></p></td>
<td><p><em>RecipientAddressContainsWords</em></p>
<p><em>ExceptIfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messaggi che contengono le parole specificate nell'indirizzo e-mail del destinatario.</p>
<p><strong>Nota:</strong> questa condizione non considera i messaggi che vengono inviati all'indirizzo proxy del destinatario. Esegue la corrispondenza solo dei messaggi che vengono inviati all'indirizzo e-mail principale del destinatario.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>L'indirizzo del destinatario corrisponde a</strong></p>
<p><strong>Il destinatario</strong> &gt; <strong>ha un indirizzo che corrisponde a uno di questi modelli di testo</strong></p></td>
<td><p><em>RecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messaggi in cui l'indirizzo e-mail del destinatario contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p>
<p><strong>Nota:</strong> questa condizione non considera i messaggi che vengono inviati all'indirizzo proxy del destinatario. Esegue la corrispondenza solo dei messaggi che vengono inviati all'indirizzo e-mail principale del destinatario.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Le proprietà specificate del destinatario includono una o più delle seguenti parole</strong></p>
<p><strong>Il destinatario</strong> &gt; <strong>ha proprietà specifiche che includono una o più delle seguenti parole</strong></p></td>
<td><p><em>RecipientADAttributeContainsWords</em></p>
<p><em>ExceptIfRecipientADAttributeContainsWords</em></p></td>
<td><p>Proprietà principale: <code>ADAttribute</code></p>
<p>Proprietà secondaria: <code>Words</code></p></td>
<td><p>Messaggi in cui l'attributo specificato Active Directory di un destinatario contiene una delle parole specificate.</p>
<p>Si noti che l'attributo <strong>Country</strong> richiede il valore di codice paese a due lettere (ad esempio DE per la Germania).</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Le proprietà specificate del destinatario corrispondono a questi modelli di testo</strong></p>
<p><strong>Il destinatario</strong> &gt; <strong>ha proprietà specifiche che corrispondono a questi modelli</strong></p></td>
<td><p><em>RecipientADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfRecipientADAttributeMatchesPatterns</em></p></td>
<td><p>Proprietà principale: <code>ADAttribute</code></p>
<p>Proprietà secondaria: <code>Patterns</code></p></td>
<td><p>Messaggi in cui l'attributo specificato Active Directory di un destinatario contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Il dominio di un destinatario è</strong></p>
<p><strong>Il destinatario</strong> &gt; <strong>Il dominio è</strong></p></td>
<td><p><em>RecipientDomainIs</em></p>
<p><em>ExceptIfRecipientDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>Messaggi in cui il dominio dell'indirizzo e-mail del destinatario corrisponde al valore specificato.</p>
<p>Se occorre trovare domini del destinatario che <em>contengono</em> il dominio specificato, ad esempio un sottodominio di un dominio, utilizzare la condizione <strong>L'indirizzo del destinatario corrisponde</strong> (<em>RecipientAddressMatchesPatterns</em>) e specificare il dominio utilizzando la sintassi: <code>'@domain\.com$'</code>.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Oggetto o corpo del messaggio


> [!NOTE]
> La ricerca di due parole o sequenze di testo nell'oggetto o in altri campi dell'intestazione avviene <EM>dopo</EM> che il messaggio è stato decodificato tramite metodo di codifica per il trasferimento dei contenuti che è stato usato per trasmettere il messaggio binario tra i server SMTP in testo ASCII. Non è possibile utilizzare condizioni o eccezioni per cercare i valori codificati non elaborati (in genere, Base64) dell'oggetto o di altri campi dell'intestazione dei messaggi.




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
<th>Condizione o eccezione in EAC</th>
<th>Parametri condizione e l'eccezione in Exchange Management Shell</th>
<th>Tipo di proprietà</th>
<th>Descrizione</th>
<th>Disponibile in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>L'oggetto o il corpo include</strong></p>
<p><strong>L'oggetto o il corpo</strong> &gt; <strong>l'oggetto o il corpo include una o più delle seguenti parole</strong></p></td>
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messaggi che contengono le parole specificate nel campo <strong>Subject</strong> o nel corpo del messaggio.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>L'oggetto o il corpo corrisponde a</strong></p>
<p><strong>L'oggetto o il corpo</strong> &gt; <strong>l'oggetto o il corpo del messaggio corrisponde a questi modelli di testo</strong></p></td>
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messaggi in cui il campo <strong>Subject</strong> o il corpo del messaggio contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>L'oggetto include</strong></p>
<p><strong>L'oggetto o il corpo</strong> &gt; <strong>l'oggetto include una o più delle seguenti parole</strong></p></td>
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messaggi che contengono le parole specificate nel campo <strong>Subject</strong>.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>L'oggetto corrisponde a</strong></p>
<p><strong>L'oggetto o il corpo</strong> &gt; <strong>l'oggetto corrisponde a questi modelli di testo</strong></p></td>
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messaggi in cui il campo <strong>Subject</strong> contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Allegati

Per ulteriori informazioni su come regole del flusso di posta elettronica esaminare messaggi con allegati, vedere [Utilizzare le regole di trasporto per esaminare messaggi con allegati](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md).


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
<th>Condizione o eccezione in EAC</th>
<th>Parametri condizione e l'eccezione in Exchange Management Shell</th>
<th>Tipo di proprietà</th>
<th>Descrizione</th>
<th>Disponibile in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Il contenuto di qualsiasi allegato include</strong></p>
<p><strong>Un allegato</strong> &gt; <strong>ha un contenuto che include una di queste parole</strong></p></td>
<td><p><em>AttachmentContainsWords</em></p>
<p><em>ExceptIfAttachmentContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messaggi in cui un allegato contiene le parole specificate.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Il contenuto di qualsiasi allegato corrisponde</strong></p>
<p><strong>Un allegato</strong> &gt; <strong>ha un contenuto che corrisponde a questi modelli di testo</strong></p></td>
<td><p><em>AttachmentMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messaggi in cui un allegato contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p>
<p><strong>Nota:</strong> vengono analizzati solo i primi 150 kilobyte (KB) degli allegati.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Il contenuto degli allegati non può essere esaminato</strong></p>
<p><strong>Un allegato</strong> &gt; <strong>impossibile controllare il contenuto</strong></p></td>
<td><p><em>AttachmentIsUnsupported</em></p>
<p><em>ExceptIfAttachmentIsUnsupported</em></p></td>
<td><p>n/d</p></td>
<td><p>Messaggi in cui un allegato in modo nativo non viene riconosciuto dal Exchange e il filtro IFilter richiesto non è installato nel server cassette postali. Per ulteriori informazioni, vedere <a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">Registrazione dei IFilter di Filter Pack con Exchange 2013</a>.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Il nome di qualsiasi allegato è uguale a</strong></p>
<p><strong>Un allegato</strong> &gt; <strong>ha un nome di file che corrisponde a questi modelli di testo</strong></p></td>
<td><p><em>AttachmentNameMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentNameMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messaggi in cui il nome di file di un allegato contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>L'estensione di qualsiasi allegato è uguale a</strong></p>
<p><strong>Un allegato</strong> &gt; <strong>ha un'estensione di file che include queste parole</strong></p></td>
<td><p><em>AttachmentExtensionMatchesWords</em></p>
<p><em>ExceptIfAttachmentExtensionMatchesWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messaggi in cui l'estensione di un file allegato corrisponde a una delle parole specificate.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Qualsiasi allegato è maggiore o uguale a</strong></p>
<p><strong>L'allegato &gt; dimensione è maggiore o uguale a</strong></p></td>
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Messaggi in cui un allegato ha una dimensione uguale o superiore al valore specificato.</p>
<p>In EAC è possibile specificare le dimensioni solo in kilobyte (KB).</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Non ho completato l'analisi del messaggio</strong></p>
<p><strong>Qualsiasi allegato</strong> &gt; <strong>non ha completato l'analisi</strong></p></td>
<td><p><em>AttachmentProcessingLimitExceeded</em></p>
<p><em>ExceptIfAttachmentProcessingLimitExceeded</em></p></td>
<td><p>n/d</p></td>
<td><p>Messaggi in cui il motore delle regole non ha completato l'analisi degli allegati. È possibile utilizzare questa condizione per creare regole che interagiscono per identificare ed elaborare i messaggi in cui non è stato possibile analizzare completamente il contenuto.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>L'allegato ha contenuto eseguibile</strong></p>
<p><strong>Un allegato</strong> &gt; <strong>ha contenuto eseguibile</strong></p></td>
<td><p><em>AttachmentHasExecutableContent</em></p>
<p><em>ExceptIfAttachmentHasExecutableContent</em></p></td>
<td><p>n/d</p></td>
<td><p>Messaggi in cui un allegato è un file eseguibile. Il sistema esamina le proprietà del file anziché affidarsi all'estensione del file.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Tutti gli allegati sono protetti da password</strong></p>
<p><strong>Un allegato</strong> &gt; <strong>è protetto da password</strong></p></td>
<td><p><em>AttachmentIsPasswordProtected</em></p>
<p><em>ExceptIfAttachmentIsPasswordProtected</em></p></td>
<td><p>n/d</p></td>
<td><p>Messaggi in cui un allegato è protetto da password (e pertanto non può essere analizzato). Il rilevamento delle password funziona solo per documenti Office e file ZIP.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Un destinatario

Le condizioni ed eccezioni in questa sezione forniscono una funzionalità univoca che influisce su *tutti i* destinatari quando il messaggio contiene almeno uno dei destinatari specificati. Si supponga, ad esempio, che è presente una regola che rifiuta i messaggi. Se si utilizza una condizione di destinatari nella sezione destinatari , il messaggio viene rifiutato solo per i destinatari specificati. Ad esempio, se la regola rileva che il destinatario specificato in un messaggio, ma il messaggio contiene cinque altri destinatari. Il messaggio viene rifiutato per che un destinatario e recapitato ai destinatari presenti altri cinque.

Se si aggiunge una condizione di destinatario di questa sezione, lo stesso messaggio viene rifiutato per il destinatario rilevato e gli altri cinque destinatari.

Al contrario, un'eccezione di destinatario di questa sezione *impedisce* l'applicazione dell'azione della regola a *tutti* i destinatari del messaggio, non solo ai destinatari rilevati.

**Nota:**  questa condizione non considera i messaggi che vengono inviati all'indirizzo proxy del destinatario. Esegue la corrispondenza solo dei messaggi che vengono inviati all'indirizzo e-mail principale del destinatario.


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
<th>Condizione o eccezione in EAC</th>
<th>Parametri condizione e l'eccezione in Exchange Management Shell</th>
<th>Tipo di proprietà</th>
<th>Descrizione</th>
<th>Disponibile in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>L'indirizzo del destinatario include</strong></p>
<p><strong>Un destinatario</strong> &gt; <strong>ha un indirizzo che include una di queste parole</strong></p></td>
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messaggi che contengono le parole specificate nei campi <strong>To</strong>, <strong>Cc</strong> o <strong>Bcc</strong> del messaggio.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>L'indirizzo del destinatario corrisponde a</strong></p>
<p><strong>Un destinatario</strong> &gt; <strong>ha un indirizzo che corrisponde a uno di questi modelli di testo</strong></p></td>
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messaggi in cui il campo <strong>To</strong>, <strong>Cc</strong> o <strong>Bcc</strong> contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Tipi di informazioni riservate, valori di A e Cc, dimensioni e set di caratteri del messaggio

Le condizioni in questa sezione tale aspetto per i valori nei campi **To** e **Cc** si comportano come le condizioni nella sezione gli eventuali destinatari (*tutti i* destinatari del messaggio sono interessati dalla regola, non solo la rilevato destinatari).

**Nota:**  questa condizione non considera i messaggi che vengono inviati all'indirizzo proxy del destinatario. Esegue la corrispondenza solo dei messaggi che vengono inviati all'indirizzo e-mail principale del destinatario.


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
<th>Condizione o eccezione in EAC</th>
<th>Parametri condizione e l'eccezione in Exchange Management Shell</th>
<th>Tipo di proprietà</th>
<th>Descrizione</th>
<th>Disponibile in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Il messaggio contiene informazioni riservate</strong></p>
<p><strong>Il messaggio</strong> &gt; <strong>contiene tutti questi tipi di informazioni riservate</strong></p></td>
<td><p><em>MessageContainsDataClassifications</em></p>
<p><em>ExceptIfMessageContainsDataClassifications</em></p></td>
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>Messaggi che contengono informazioni riservate definite dai criteri di prevenzione della perdita di dati (DLP).</p>
<p>Questa condizione è richiesta per ruoli che utilizzano l'azione <strong>Notifica al mittente con un suggerimento per i criteri</strong> (<em>NotifySender</em>).</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>La casella A contiene</strong></p>
<p><strong>Il messaggio</strong> &gt; <strong>contiene questa persona nella casella A</strong></p></td>
<td><p><em>AnyOfToHeader</em></p>
<p><em>ExceptIfAnyOfToHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messaggi in cui il campo <strong>To</strong> contiene uno dei destinatari specificati.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>La casella A contiene un membro di</strong></p>
<p><strong>Il messaggio</strong> &gt; <strong>contiene un membro di questo gruppo nella casella Cc</strong></p></td>
<td><p><em>AnyOfToHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messaggi in cui il campo <strong>To</strong> contiene un destinatario che è membro del gruppo specificato.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>La casella Cc contiene</strong></p>
<p><strong>Il messaggio</strong> &gt; <strong>contiene questa persona nella casella Cc</strong></p></td>
<td><p><em>AnyOfCcHeader</em></p>
<p><em>ExceptIfAnyOfCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messaggi in cui il campo <strong>Cc</strong> contiene uno dei destinatari specificati.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>La casella Cc contiene un membro di</strong></p>
<p><strong>Il messaggio</strong> &gt; <strong>contiene un membro di questo gruppo</strong></p></td>
<td><p><em>AnyOfCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messaggi in cui il campo <strong>Cc</strong> contiene un destinatario che è membro del gruppo specificato.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>La casella A o Cc contiene</strong></p>
<p><strong>Il messaggio</strong> &gt; <strong>contiene questa persona nella casella A o Cc</strong></p></td>
<td><p><em>AnyOfToCcHeader</em></p>
<p><em>ExceptIfAnyOfToCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messaggi in cui il campo <strong>To</strong> o <strong>Cc</strong>contiene uno dei destinatari specificati.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>La casella A o Cc contiene un membro di</strong></p>
<p><strong>Il messaggio</strong> &gt; <strong>contiene un membro di questo gruppo nella casella A o Cc</strong></p></td>
<td><p><em>AnyOfToCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messaggi in cui il campo <strong>To</strong> o <strong>Cc</strong> contiene un destinatario che è membro del gruppo specificato.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>La dimensione del messaggio è maggiore o uguale a</strong></p>
<p><strong>Il messaggio</strong> &gt; <strong>ha dimensione maggiore o uguale a</strong></p></td>
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Messaggi in cui la dimensione totale (messaggio più allegato) è uguale o superiore al valore specificato.</p>
<p>In EAC è possibile specificare le dimensioni solo in kilobyte (KB).</p>
<p><strong>Nota:</strong> i limiti di dimensione dei messaggi per le cassette postali vengono valutati prima delle regole del flusso di posta. Un messaggio troppo grande per una cassetta postale verrà rifiutato prima che una regola con questa condizione possa essere applicata al messaggio.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Il nome del set di caratteri del messaggio include una di queste parole</strong></p>
<p><strong>Il messaggio</strong> &gt; <strong>ha un nome del set di caratteri che contiene una di queste parole</strong></p></td>
<td><p><em>ContentCharacterSetContainsWords</em></p>
<p><em>ExceptIfContentCharacterSetContainsWords</em></p></td>
<td><p><code>CharacterSets</code></p></td>
<td><p>Messaggi che contengono i nomi dei set di caratteri specificati.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Mittente e destinatario


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
<th>Condizione o eccezione in EAC</th>
<th>Parametri condizione e l'eccezione in Exchange Management Shell</th>
<th>Tipo di proprietà</th>
<th>Descrizione</th>
<th>Disponibile in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Il mittente è uno dei destinatari</strong></p>
<p><strong>Il mittente e il destinatario</strong> &gt; <strong>la relazione tra il mittente e un destinatario è</strong></p></td>
<td><p><em>SenderManagementRelationship</em></p>
<p><em>ExceptIfSenderManagementRelationship</em></p></td>
<td><p><code>ManagementRelationship</code></p></td>
<td><p>Messaggi in cui il mittente è il responsabile di un destinatario oppure un destinatario è il responsabile del mittente.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>il messaggio è compreso tra i membri di questi gruppi</strong></p>
<p><strong>Il mittente e il destinatario</strong> &gt; <strong>il messaggio viene scambiato tra i membri di questi gruppi</strong></p></td>
<td><p><em>BetweenMemberOf1</em> e <em>BetweenMemberOf2</em></p>
<p><em>ExceptIfBetweenMemberOf1</em> e <em>ExceptIfBetweenMemberOf2</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Messaggi inviati tra i membri dei gruppi specificati.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Il responsabile del mittente o del destinatario è</strong></p>
<p><strong>Il mittente e il destinatario</strong> &gt; <strong>il responsabile del mittente o del destinatario è questa persona</strong></p></td>
<td><p><em>ManagerForEvaluatedUser</em> e <em>ManagerAddress</em></p>
<p><em>ExceptIfManagerForEvaluatedUser</em> e <em>ExceptIfManagerAddress</em></p></td>
<td><p>Proprietà principale: <code>EvaluatedUser</code></p>
<p>Proprietà secondaria: <code>Addresses</code></p></td>
<td><p>Messaggi in cui un utente specificato è il responsabile del mittente o un utente specificato è il responsabile di un destinatario.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Confronto proprietà del mittente e di un destinatario come</strong></p>
<p><strong>Il mittente e il destinatario</strong> &gt; <strong>il confronto delle proprietà di mittente e destinatario determina</strong></p></td>
<td><p><em>ADAttributeComparisonAttribute</em> e <em>ADComparisonOperator</em></p>
<p><em>ExceptIfADAttributeComparisonAttribute</em> e <em>ExceptIfADComparisonOperator</em></p></td>
<td><p>Proprietà principale: <code>ADAttribute</code></p>
<p>Proprietà secondaria: <code>Evaluation</code></p></td>
<td><p>Messaggi in cui l'attributo specificato Active Directory per il mittente e il destinatario corrisponde o non corrisponde.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Proprietà del messaggio


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
<th>Condizione o eccezione in EAC</th>
<th>Parametri condizione e l'eccezione in Exchange Management Shell</th>
<th>Tipo di proprietà</th>
<th>Descrizione</th>
<th>Disponibile in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Il tipo di messaggio è</strong></p>
<p><strong>Le proprietà del messaggio</strong> &gt; <strong>includono il tipo di messaggio</strong></p></td>
<td><p><em>MessageTypeMatches</em></p>
<p><em>ExceptIfMessageTypeMatches</em></p></td>
<td><p><code>MessageType</code></p></td>
<td><p>Messaggi del tipo specificato.</p>

> [!NOTE]
> Quando Outlook o Outlook Web App è configurato per inoltrare un messaggio, la proprietà <STRONG>ForwardingSmtpAddress</STRONG> viene aggiunta al messaggio. Il tipo di messaggio non viene modificato in <CODE>AutoForward</CODE>.


</td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Il messaggio è classificato come</strong></p>
<p><strong>Le proprietà del messaggoo</strong> &gt; <strong>includono questa classificazione</strong></p></td>
<td><p><em>HasClassification</em></p>
<p><em>ExceptIfHasClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>Messaggi che presentano la classificazione dei messaggi specificata. Si tratta di una classificazione dei messaggi personalizzata che è possibile creare all'interno dell'organizzazione tramite il cmdlet <strong>New-MessageClassification</strong>.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Il messaggio non è contrassegnato con alcuna classificazione</strong></p>
<p><strong>Le proprietà del messaggio</strong> &gt; <strong>non includono alcuna classificazione</strong></p></td>
<td><p><em>HasNoClassification</em></p>
<p><em>ExceptIfHasNoClassification</em></p></td>
<td><p>n/d</p></td>
<td><p>Messaggi privi di una classificazione dei messaggi.</p></td>
<td><p>Exchange 2010 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>Il messaggio ha un livello di probabilità di posta indesiderata maggiore di o uguale a</strong></p>
<p><strong>Le proprietà del messaggio</strong> &gt; <strong>includono un SCL maggiore o uguale a</strong></p></td>
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Messaggi a cui è assegnato un livello di probabilità di posta indesiderata (SCL) uguale o superiore al valore specificato.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><strong>Il messaggio è contrassegnato con una priorità di</strong></p>
<p><strong>Le proprietà del messaggio</strong> &gt; <strong>includono il livello di priorità</strong></p></td>
<td><p><em>WithImportance</em></p>
<p><em>ExceptIfWithImportance</em></p></td>
<td><p><code>Importance</code></p></td>
<td><p>Messaggi contrassegnati con il livello di priorità specificato.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Intestazioni del messaggio


> [!NOTE]
> La ricerca di due parole o sequenze di testo nell'oggetto o in altri campi dell'intestazione avviene <EM>dopo</EM> che il messaggio è stato decodificato tramite metodo di codifica per il trasferimento dei contenuti che è stato usato per trasmettere il messaggio binario tra i server SMTP in testo ASCII. Non è possibile utilizzare condizioni o eccezioni per cercare i valori codificati non elaborati (in genere, Base64) dell'oggetto o di altri campi dell'intestazione dei messaggi.




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
<th>Condizione o eccezione in EAC</th>
<th>Parametri condizione e l'eccezione in Exchange Management Shell</th>
<th>Tipo di proprietà</th>
<th>Descrizione</th>
<th>Disponibile in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>L'intestazione di un messaggio include</strong></p>
<p><strong>L'intestazione di un messaggio</strong> &gt; <strong>include una di queste parole</strong></p></td>
<td><p><em>HeaderContainsMessageHeader</em> e <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> e <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>Proprietà principale: <code>MessageHeaderField</code></p>
<p>Proprietà secondaria: <code>Words</code></p></td>
<td><p>Messaggi che contengono il campo di intestazione specificato e il valore di tale campo di intestazione contiene le parole specificate.</p>
<p>Il nome del campo di intestazione e il valore del campo di intestazione vengono sempre utilizzati insieme.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><strong>L'intestazione di un messaggio è uguale a</strong></p>
<p><strong>L'intestazione di un messaggio</strong> &gt; <strong>corrisponde a questi modelli di testo</strong></p></td>
<td><p><em>HeaderMatchesMessageHeader</em> e <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> e <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>Proprietà principale: <code>MessageHeaderField</code></p>
<p>Proprietà secondaria: <code>Patterns</code></p></td>
<td><p>Messaggi che contengono il campo di intestazione specificato e il valore di tale campo di intestazione contiene le espressioni regolari specificate.</p>
<p>Il nome del campo di intestazione e il valore del campo di intestazione vengono sempre utilizzati insieme.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Condizioni ed eccezioni per le regole di flusso di posta elettronica nei server Trasporto Edge

Le condizioni ed eccezioni disponibili nelle regole di flusso di posta elettronica nei server Trasporto Edge sono un piccolo sottogruppo delle funzionalità disponibile nei server cassette postali. Non esiste alcun EAC nei server Trasporto Edge, in modo che è possibile gestire solo le regole di flusso di posta elettronica in Exchange Management Shell sul server Trasporto Edge locale. Nella tabella seguente sono descritte le condizioni ed eccezioni. I tipi di proprietà sono descritti nella sezione tipi di proprietà .


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametri condizione e l'eccezione in Exchange Management Shell</th>
<th>Tipo di proprietà</th>
<th>Descrizione</th>
<th>Disponibile in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messaggi che contengono le parole specificate nel campo <strong>To</strong>, <strong>Cc</strong>o <strong>Bcc</strong> .</p>
<p>Quando un messaggio contenga il destinatario specificato, l'azione della regola è applicata o non applicato a <em>tutti i</em> destinatari del messaggio. Ad esempio, il messaggio viene rifiutato per tutti i destinatari del messaggio, non solo per il destinatario specificato.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messaggi in cui il campo <strong>To</strong>, <strong>Cc</strong> o <strong>Bcc</strong> contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p>
<p>Quando un messaggio contenga il destinatario specificato, l'azione della regola è applicata o non applicato a <em>tutti i</em> destinatari del messaggio. Ad esempio, il messaggio viene rifiutato per tutti i destinatari del messaggio, non solo per il destinatario specificato.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Messaggi con allegati in qualsiasi allegato è maggiore o uguale al valore specificato.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messaggi che contengono le parole specificate nell'indirizzo e-mail del mittente.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messaggi in cui l'indirizzo e-mail del mittente contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>Messaggi inviati da mittenti interni o mittenti esterni.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><em>HeaderContainsMessageHeader</em> e <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> e <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>Proprietà principale: <code>MessageHeaderField</code></p>
<p>Proprietà secondaria: <code>Words</code></p></td>
<td><p>Messaggi che contengono il campo di intestazione specificato e il valore di tale campo di intestazione contiene le parole specificate.</p>
<p>Il nome del campo di intestazione e il valore del campo di intestazione vengono sempre utilizzati insieme.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>HeaderMatchesMessageHeader</em> e <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> e <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>Proprietà principale: <code>MessageHeaderField</code></p>
<p>Proprietà secondaria: <code>Patterns</code></p></td>
<td><p>Messaggi che contengono il campo di intestazione specificato e il valore di tale campo di intestazione contiene le espressioni regolari specificate.</p>
<p>Il nome del campo di intestazione e il valore del campo di intestazione vengono sempre utilizzati insieme.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Messaggi in cui la dimensione totale (messaggio più allegato) è uguale o superiore al valore specificato.</p></td>
<td><p>Exchange 2013 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Messaggi vengono assegnati un SCL è maggiore o uguale al valore specificato.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messaggi che contengono le parole specificate nel campo <strong>Subject</strong> .</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messaggi in cui il campo <strong>Subject</strong> contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Messaggi che contengono le parole specificate nel corpo del messaggio o campo <strong>Subject</strong> .</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Messaggi in cui il campo <strong>Subject</strong> o il corpo del messaggio contiene modelli di testo che corrispondono alle espressioni regolari specificate.</p></td>
<td><p>Exchange 2007 o versioni successive</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Tipi di proprietà

I tipi di proprietà che vengono usati nelle condizioni e nelle eccezioni sono descritti nella tabella seguente.


> [!NOTE]
> Se la proprietà è una stringa, gli spazi finali non sono consentiti.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di proprietà</th>
<th>Valori validi</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ADAttribute</code></p></td>
<td><p>Selezionare da un elenco predefinito di attributi Active Directory</p></td>
<td><p>UNRESOLVED_TOKENBLOCK_VAL(PD_Transport_Rules_ADAttributes_Snippet)</p>
<p>In EAC, per specificare più parole o modelli di testo per lo stesso attributo, separare i valori con virgole. Ad esempio, il valore <strong>San Francisco, Palo Alto</strong> per l'attributo <strong>Città</strong> consente di cercare &quot;Città è uguale a San Francisco&quot; o Città è uguale a Palo Alto &quot;.</p>
<p>Exchange Management Shell, utilizzare la sintassi <code>&quot;AttributeName1:Value1,Value 2 with spaces,Value3...&quot;,&quot;AttributeName2:Word4,Value 5 with spaces,Value6...&quot;</code>, dove <code>Value</code> è il modello di word o testo che si desidera trovare.</p>
<p>Ad esempio, <code>&quot;City:San Francisco,Palo Alto&quot;</code>, <code>&quot;City:San Francisco,Palo Alto&quot;</code> o <code>&quot;Department:Sales,Finance&quot;</code>.</p>
<p>Quando si specificano più attributi o più valori per lo stesso attributo, viene utilizzato l‘operatore <strong>or</strong>. Non usare valori con spazi iniziali o finali.</p>
<p>Si noti che l'attributo <strong>Country</strong> richiede il valore di codice paese a due lettere ISO 3166-1 (ad esempio DE per la Germania). Per cercare i valori, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=331680">https://go.microsoft.com/fwlink/p/?LinkId=331680</a>.</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Destinatari di Exchange</p></td>
<td><p>A seconda della natura dell'eccezione o condizione, è possibile specificare qualsiasi oggetto abilitato alla posta nell'organizzazione (ad esempio condizioni correlate al destinatario) oppure solo uno specifico tipo di oggetto (ad esempio i gruppi per le condizioni di appartenenza al gruppo). La condizione o eccezione, inoltre, potrebbe richiedere un valore o consentire più valori.</p>
<p>In Exchange Management Shell, separare più valori da una virgola.</p>
<p><strong>Nota:</strong> questa condizione non considera i messaggi che vengono inviati all'indirizzo proxy del destinatario. Esegue la corrispondenza solo dei messaggi che vengono inviati all'indirizzo e-mail principale del destinatario.</p></td>
</tr>
<tr class="odd">
<td><p><code>CharacterSets</code></p></td>
<td><p>Matrice di nomi di set di caratteri</p></td>
<td><p>Uno o più set di caratteri contenuti presenti in un messaggio. Ad esempio:</p>
<ul>
<li><p><code>Arabic/iso-8859-6</code></p></li>
<li><p><code>Chinese/big5</code></p></li>
<li><p><code>Chinese/euc-cn</code></p></li>
<li><p><code>Chinese/euc-tw</code></p></li>
<li><p><code>Chinese/gb2312</code></p></li>
<li><p><code>Chinese/iso-2022-cn</code></p></li>
<li><p><code>Cyrillic/iso-8859-5</code></p></li>
<li><p><code>Cyrillic/koi8-r</code></p></li>
<li><p><code>Cyrillic/windows-1251</code></p></li>
<li><p><code>Greek/iso-8859-7</code></p></li>
<li><p><code>Hebrew/iso-8859-8</code></p></li>
<li><p><code>Japanese/euc-jp</code></p></li>
<li><p><code>Japanese/iso-022-jp</code></p></li>
<li><p><code>Japanese/shift-jis</code></p></li>
<li><p><code>Korean/euc-kr</code></p></li>
<li><p><code>Korean/johab</code></p></li>
<li><p><code>Korean/ks_c_5601-1987</code></p></li>
<li><p><code>Turkish/windows-1254</code></p></li>
<li><p><code>Turkish/iso-8859-9</code></p></li>
<li><p><code>Vietnamese/tcvn</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>DomainName</code></p></td>
<td><p>Matrice di domini SMTP</p></td>
<td><p>Ad esempio, <code>contoso.com</code> o <code>eu.contoso.com</code>.</p>
<p>In Exchange Management Shell, è possibile specificare più domini separati da virgole.</p></td>
</tr>
<tr class="odd">
<td><p><code>EvaluatedUser</code></p></td>
<td><p>Valore singolo di <strong>Mittente</strong> o <strong>Destinatario</strong></p></td>
<td><p>Specifica se la regola cerca il responsabile del mittente o il responsabile del destinatario.</p></td>
</tr>
<tr class="even">
<td><p><code>Evaluation</code></p></td>
<td><p>Valore singolo di <strong>Uguale</strong> o <strong>Diverso</strong> (<code>NotEqual</code>)</p></td>
<td><p>Quando si confronta l'attributo Active Directory del mittente e i destinatari, consente di specificare se i valori devono corrispondere o non corrispondere.</p></td>
</tr>
<tr class="odd">
<td><p><code>Importance</code></p></td>
<td><p>Singolo valore di <strong>Bassa</strong>, <strong>Normale</strong> o <strong>Elevata</strong></p></td>
<td><p>Il livello di priorità assegnato al messaggio dal mittente in Outlook o Outlook Web App.</p></td>
</tr>
<tr class="even">
<td><p><code>IPAddressRanges</code></p></td>
<td><p>Matrice di indirizzi o intervalli di indirizzi IP</p></td>
<td><p>Immettere gli indirizzi IPv4 utilizzando la seguente sintassi:</p>
<ul>
<li><p><strong>Singolo indirizzo IP</strong>   Ad esempio, <code>192.168.1.1</code>.</p></li>
<li><p><strong>Intervallo di indirizzi IP</strong>   Ad esempio, <code>192.168.0.1-192.168.0.254</code>.</p></li>
<li><p><strong>Intervallo di indirizzi CIDR (Classless InterDomain Routing)</strong>  Ad esempio, <code>192.168.0.1/25</code>.</p></li>
</ul>
<p>In Exchange Management Shell, è possibile specificare più indirizzi IP o intervalli separati da virgole.</p></td>
</tr>
<tr class="odd">
<td><p><code>ManagementRelationship</code></p></td>
<td><p>Valore singolo di <strong>Responsabile</strong> o <strong>Superiore diretto</strong>(<code>DirectReport</code>)</p></td>
<td><p>Consente di specificare la relazione tra il mittente e i destinatari. La regola controlla l’attributo <strong>Manager</strong> in Active Directory per verificare se il mittente è il responsabile di un destinatario oppure se un destinatario è il responsabile del mittente.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageClassification</code></p></td>
<td><p>Singolo classificazione dei messaggi</p></td>
<td><p>In EAC, è possibile selezionare dall'elenco di classificazioni dei messaggi create.</p>
<p>In Exchange Management Shell, il cmdlet <strong>Get-MessageClassification</strong> consente di identificare la classificazione dei messaggi. Ad esempio, utilizzare il comando seguente per cercare i messaggi con la classificazione <code>Company Internal</code> e anteporre l'oggetto del messaggio con il valore <code>CompanyInternal</code>.</p>
<p><code>New-TransportRule &quot;Rule Name&quot; -HasClassification @(Get-MessageClassification &quot;Company Internal&quot;).Identity -PrependSubject &quot;CompanyInternal&quot;</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Stringa singola</p></td>
<td><p>Specifica il nome del campo di intestazione. Il nome del campo dell'intestazione è sempre associato al valore del campo dell'intestazione (corrispondenza di parola o modello di testo).</p>
<p>L'<em>intestazione del messaggio</em> è una raccolta di campi di intestazione obbligatori e facoltativi nel messaggio. Esempi di campi di intestazione sono <strong>To</strong>, <strong>From</strong>, <strong>Received</strong> e <strong>Content-Type</strong>. I campi di intestazione ufficiali sono definiti nel documento RFC 5322. I campi di intestazione non ufficiali iniziano con <strong>X-</strong> e sono noti come <em>X-Header</em>.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageType</code></p></td>
<td><p>Valore del tipo di messaggio singolo</p></td>
<td><p>Specifica uno dei seguenti tipi di messaggio:</p>
<ul>
<li><p><strong>Risposta automatica</strong> (<code>OOF</code>)</p></li>
<li><p><strong>Inoltro automatico</strong> (<code>AutoForward</code>)</p></li>
<li><p><strong>Crittografato</strong></p></li>
<li><p><strong>Calendarizzazione</strong></p></li>
<li><p><strong>Controllato da autorizzazioni</strong> (<code>PermissionControlled</code>)</p></li>
<li><p><strong>Segreteria telefonica</strong></p></li>
<li><p><strong>Firmato</strong></p></li>
<li><p><strong>Richiesta di approvazione</strong> (<code>ApprovalRequest</code>)</p></li>
<li><p><strong>Conferma di lettura</strong> (<code>ReadReceipt</code>)</p></li>
</ul>

> [!NOTE]
> Quando Outlook o Outlook Web App è configurato per inoltrare un messaggio, la proprietà <STRONG>ForwardingSmtpAddress</STRONG> viene aggiunta al messaggio. Il tipo di messaggio non viene modificato in <CODE>AutoForward</CODE>.


</td>
</tr>
<tr class="odd">
<td><p><code>Patterns</code></p></td>
<td><p>Matrice di espressioni regolari</p></td>
<td><p>Specifica uno o più espressioni regolari utilizzate per definire i modelli di testo nei valori. Per ulteriori informazioni, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=180327">Sintassi delle espressioni regolari</a>.</p>
<p>In Exchange Management Shell, si specificano più espressioni regolari separate da virgole e ogni espressione regolare racchiuso tra virgolette (&quot;).</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>Uno dei seguenti valori:</p>
<ul>
<li><p><strong>Ignora il filtro posta indesiderata</strong> (<code>-1</code>)</p></li>
<li><p>Numeri da 0 a 9</p></li>
</ul></td>
<td><p>Specifica il livello di probabilità di posta indesiderata (SCL) assegnato a un messaggio. Più alto è il valore di SCL, maggiore è la probabilità che si tratti di un messaggio di posta indesiderata.</p></td>
</tr>
<tr class="odd">
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>Matrice di tipi di informazioni riservate</p></td>
<td><p>Specifica i tipi di informazioni riservate definiti nell'organizzazione. Per un elenco dei tipi di informazioni riservate predefiniti, vedere <a href="what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md">Cosa cercare i tipi di informazioni riservate in Exchange</a>.</p>
<p>In Exchange Management Shell, utilizzare la sintassi <code>@{&lt;SensitiveInformationType1&gt;},@{&lt;SensitiveInformationType2&gt;},...</code>. Ad esempio, per cercare i contenuti che includono almeno due numeri di carta di credito e almeno un numero di registrazione ABA, utilizzare il valore <code>@{Name=&quot;Credit Card Number&quot;; minCount=&quot;2&quot;},@{Name=&quot;ABA Routing Number&quot;; minCount=&quot;1&quot;}</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Size</code></p></td>
<td><p>Valore di dimensione singola</p></td>
<td><p>Specifica le dimensioni di un allegato o dell'intero messaggio.</p>
<p>In EAC è possibile specificare le dimensioni solo in kilobyte (KB).</p>
<p>In Exchange Management Shell, quando si immette un valore, qualificarlo con una delle seguenti unità:</p>
<ul>
<li><p><code>B</code> (byte)</p></li>
<li><p><code>KB</code> (kilobyte)</p></li>
<li><p><code>MB</code> (megabyte)</p></li>
<li><p><code>GB</code> (gigabyte)</p></li>
</ul>
<p>Esempio: <code>20MB</code></p>
<p>I valori non qualificati vengono in genere considerati byte, ma i valori bassi possono essere arrotondati al valore in kilobyte più vicino.</p></td>
</tr>
<tr class="odd">
<td><p><code>UserScopeFrom</code></p></td>
<td><p>Singolo valore di <strong>Interno all'organizzazione</strong> (<code>InOrganization</code>) o <strong>Esterno dell'organizzazione</strong> (<code>NotInOrganization</code>)</p></td>
<td><p>Un mittente è considerato interno all'organizzazione se una delle seguenti condizioni è vera:</p>
<ul>
<li><p>Il mittente è una cassetta postale, un utente di posta, un gruppo o una cartella pubblica abilitata alla posta esistente in Active Directory nell'organizzazione.</p></li>
<li><p>L'indirizzo e-mail del mittente si trova in un dominio accettato configurato come dominio autorevole o dominio di inoltro interno <strong>e</strong> il messaggio è stato inviato o ricevuto tramite una connessione autenticata. Per ulteriori informazioni sui domini accettati, vedere <a href="accepted-domains-exchange-2013-help.md">Domini accettati</a>.</p></li>
</ul>
<p>Un mittente è considerato esterno all'organizzazione se una delle seguenti condizioni è vera:</p>
<ul>
<li><p>L'indirizzo e-mail del mittente non si trova in un dominio accettato.</p></li>
<li><p>L'indirizzo e-mail del mittente si trova in un dominio accettato configurato come dominio di inoltro esterno.</p></li>
</ul>

> [!NOTE]
> Per stabilire se i contatti di posta sono considerati interni o esterni all'organizzazione, la parte del dominio dell'indirizzo del mittente viene confrontato con i domini accettati dell'organizzazione.


</td>
</tr>
<tr class="even">
<td><p><code>UserScopeTo</code></p></td>
<td><p>Uno dei seguenti valori:</p>
<ul>
<li><p><strong>Interno all'organizzazione</strong> (<code>InOrganization</code>)</p></li>
<li><p><strong>Esterno all'organizzazione</strong> (<code>NotInOrganization</code>)</p></li>
<li><p><strong>In un'organizzazione partner esterni</strong> (<code>ExternalPartner</code>)</p></li>
<li><p><strong>In un'organizzazione partner non esterna</strong> (<code>ExternalNonPartner</code>)</p></li>
</ul></td>
<td><p>Un destinatario è considerato interno all'organizzazione se una delle seguenti condizioni è vera:</p>
<ul>
<li><p>Il destinatario è una cassetta postale, un utente di posta, un gruppo o una cartella pubblica abilitata alla posta esistente in Active Directory dell'organizzazione.</p></li>
<li><p>L'indirizzo e-mail del destinatario si trova in un dominio accettato configurato come dominio autorevole o come dominio di inoltro interno <strong>e</strong> il messaggio è stato inviato o ricevuto tramite una connessione autenticata.</p></li>
</ul>
<p>Un destinatario viene considerato esterno all'organizzazione se una delle seguenti condizioni è vera:</p>
<ul>
<li><p>L'indirizzo e-mail del destinatario si trova un dominio accettato.</p></li>
<li><p>L'indirizzo e-mail del destinatario si trova in un dominio accettato configurato come dominio di inoltro esterno.</p></li>
</ul>
<p>Le organizzazioni partner esterni sono i domini esterni in cui è stato configurato protezione del dominio (autenticazione reciproca TLS) per l'invio di posta elettronica.</p>
<p>Le organizzazioni non partner esterne sono tutti gli altri domini esterni che non sono considerati domini partner.</p></td>
</tr>
<tr class="odd">
<td><p><code>Words</code></p></td>
<td><p>Matrice di stringhe</p></td>
<td><p>Specifica una o più parole da cercare. Nella ricerca non viene fatta distinzione tra maiuscole e minuscole e il testo può essere racchiuso tra spazi e segni di punteggiatura. Non sono supportati i caratteri jolly e le corrispondenze parziali.</p>
<p>Ad esempio, &quot;contoso&quot; corrisponde a &quot;Contoso&quot;. Tuttavia, se il testo è delimitato da altri caratteri, non è considerato una corrispondenza. Ad esempio, &quot;contoso&quot; non corrisponde ai seguenti valori:</p>
<ul>
<li><p>Acontoso</p></li>
<li><p>Contosoa</p></li>
<li><p>Acontosob</p></li>
</ul>
<p>L'asterisco (*) viene considerato un carattere letterale e non viene utilizzato come carattere jolly.</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Ulteriori informazioni

[Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Azioni della regola di trasporto](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[Le procedure di regola trasporto o flusso di posta](mail-flow-or-transport-rule-procedures-exchange-2013-help.md)

[Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online](https://technet.microsoft.com/it-it/library/jj919235\(v=exchg.150\)) per Exchange Online

[Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online Protection](https://technet.microsoft.com/it-it/library/jj919234\(v=exchg.150\)) per Exchange Online Protection


---
title: 'Sistema di caselle vocali protette: Exchange 2013 Help'
TOCTitle: Sistema di caselle vocali protette
ms:assetid: a88d41d5-2e70-4193-bcd3-dec50dff412b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351041(v=EXCHG.150)
ms:contentKeyID: 52057310
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Sistema di caselle vocali protette

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

Alcuni sistemi di telefonia IP PBX e il legacy Private Branch eXchange (PBX) consentono al chiamante di contrassegnare un messaggio della segreteria telefonica come privato, bloccare il destinatario del messaggio di inoltro ad altri utenti. In sistemi di segreteria telefonica integrata, un messaggio vocale è possibile accedere in diversi modi, che rende più complessa per evitare messaggi vocali contrassegnati come privati dall'esposizione a listener impreviste.

Messaggistica unificata (UM) può essere configurato per utilizzare Active Directory Rights Management Services (AD RMS) per proteggere i messaggi vocali per un'organizzazione. Questa funzionalità è noto come posta vocale protetta.

Quando un messaggio vocale è protetto, il destinatario non verrà bloccato solo da inoltrare il messaggio, ma UM anche garantisce che solo il destinatario o destinatari del messaggio possono accedere al relativo contenuto. Messaggi vocali protetti possono essere accessibile tramite MicrosoftOutlook 2010 o versioni successive, Outlook Web App o Outlook Voice Access.

**Sommario**

Overview of Protected Voice Mail

Panoramica di Active Directory Rights Management Services

Client support and end-user features

Protected voice mail structure

Composing a Protected Voice Mail message

UM mailbox policies

Text message notifications and Protected Voice Mail

## Informazioni generali sul Sistema di caselle vocali protette

La caratteristica di posta vocale protetta è disponibile con Exchange 2010 e versioni successive di messaggistica unificata (UM). Possono essere configurato in un criterio cassetta postale di messaggistica UNIFICATA e tutte le impostazioni di posta vocale protetta possono essere configurate utilizzando la Console di gestione di Exchange o Shell in Exchange 2010 o utilizzando l'interfaccia di amministrazione Exchange (EAC) o i cmdlet della shell di Exchange 2013.

Il Sistema di caselle vocali protette viene implementato applicando Information Rights Management (IRM) ai messaggi vocali. Quando i messaggi vocali sono protetti dalla messaggistica unificata:

  - Gli utenti possono rispondere ai messaggi vocali protetti.

  - I destinatari di un messaggio vocale non possono inoltrarlo.

  - Gli utenti non possono salvare una copia del messaggio vocale.

  - Gli utenti non possono salvare o copiare il file audio allegato del messaggio vocale.

  - I messaggi vocali possono essere aperti solo dai destinatari previsti.

È possibile utilizzare la messaggistica unificata per proteggere sia i messaggi vocali risponditore automatico che i messaggi vocali interpersonali (messaggi vocali inviati a un utente utilizzando Outlook Voice Access). Tuttavia, la protezione non sarà applicata ai seguenti tipi di messaggi:

  - Messaggi fax.

  - Messaggi non vocali. Ad esempio, messaggi di posta elettronica o convocazioni a riunioni, anche quando vengono creati utilizzando Outlook Voice Access (risposte vocali).

Inizio pagina

## Panoramica di Active Directory Rights Management Services

AD RMS, un componente di Windows Server 2008 e versioni successive, è disponibile per proteggere i file in modo che solo gli utenti che il mittente intende visualizzare un file possono farlo. AD RMS protegge un file specificando i diritti che un utente deve disporre di accesso al file. Diritti possono essere configurati per consentire a un utente di aprire, modificare, stampare o inoltrare o eseguire altre operazioni su information rights Management. Con AD RMS, è possibile proteggere i dati quando viene distribuito all'esterno della rete.

Un sistema di AD RMS è un server sia un componente client, inclusi i seguenti:

  - Un server con Windows Server 2008 R2 o versione successiva che esegue il ruolo di server Rights Management Services Active Directory, che consente di gestire i certificati e licenze.

  - Un server di database.

  - Client AD RMS. La versione più recente del client AD RMS è inclusa come parte di Windows 7 e i sistemi operativi Windows 8.

Il componente server è costituito da diversi servizi web in esecuzione su un server Microsoft, ad esempio Windows Server 2008 o versione successiva. Il componente client può essere eseguito su un client o server del sistema operativo e include funzioni che consentono di un'applicazione per crittografare, decrittografare il contenuto, recuperare gli elenchi di revoche di certificati e modelli e acquistare le licenze e i certificati da un server.

Utilizzando il client AD RMS e AD RMS, è possibile integrare la strategia di protezione dell'organizzazione per la protezione delle informazioni tramite criteri di utilizzo permanenti che restano con le informazioni, indipendentemente dalla posizione. È possibile utilizzare AD RMS per evitare che le informazioni riservate, quali report finanziari, specifiche del prodotto, i dati dei clienti e messaggi di posta di posta elettronica e vocali confidential, ovvero da intenzionalmente o accidentalmente Guida in malintenzionati. Per informazioni dettagliate, vedere [Panoramica di AD RMS](https://go.microsoft.com/fwlink/p/?linkid=199436).

In messaggistica UNIFICATA di Exchange è possibile utilizzare le funzionalità di Information Rights Management (IRM) per applicare la protezione persistente a messaggi e allegati.

Utilizzando le funzionalità IRM e posta vocale protetta, l'organizzazione e gli utenti possono controllare i diritti destinatari dispongono di messaggi posta elettronica e vocali. IRM può essere inoltre utilizzato per limitare le azioni del destinatario, ad esempio inoltrare un messaggio a altri destinatari, stampare un messaggio o un allegato o estrazione messaggio o un allegato contenuto da copiare e incollare.

## Requisiti IRM

Prima di implementare IRM in Exchange, è necessario distribuire e configurare l'infrastruttura di AD RMS. Per informazioni dettagliate, vedere [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=199439). Per implementare IRM per il supporto di posta vocale protetta nella propria organizzazione di Exchange, la distribuzione deve soddisfare i requisiti seguenti.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Server</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cluster AD RMS</p></td>
<td><ul>
<li><p>Windows Server 2008 R2 Standard o Enterprise con SP1 o Windows Server 2012 Standard o Datacenter. Per ulteriori informazioni sui requisiti di sistema, vedere <a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisiti di sistema di Exchange 2013</a>.</p></li>
<li><p><strong>Punto di connessione del servizio (SCP)</strong> applicazioni che supportano AD RMS e Exchange 2013 utilizzano SCP registrata in Active Directory per individuare i cluster AD RMS e gli URL. AD RMS consente di registrare SCP all'interno dell'installazione di AD RMS. Se l'account utilizzato per configurare AD RMS non è un membro del gruppo di protezione Enterprise Admins, registrazione SCP può essere eseguita dopo l'installazione. Esiste una sola SCP ad RMS in una foresta Active Directory.   </p></li>
<li><p><strong>Autorizzazioni</strong>   Server del gruppo di server Exchange o singole Exchange devono essere assegnati le autorizzazioni di lettura ed esecuzione per la pipeline di certificazione del server AD RMS. Il percorso predefinito è \inetpub\wwwroot\_wmcs\certification\ServerCertification.asmx sui server AD RMS.</p></li>
<li><p><strong>Utenti con privilegi avanzati di AD RMS</strong>   Per attivare la decrittografia di trasporto, decrittografia dei rapporti del journal, IRM in Outlook Web App e IRM per Exchange ricerca, è necessario aggiungere la cassetta postale di recapito federato, una cassetta postale di sistema creata durante l'installazione di Exchange, al gruppo di utenti con privilegi avanzati AD RMS nel cluster AD RMS. Per informazioni dettagliate, vedere <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Configurazione e verifica di IRM

Utilizzare la Shell per configurare le funzionalità IRM. Per configurare le funzionalità IRM singole, utilizzare il cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)) . Per ulteriori informazioni su come configurare le funzionalità IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

Dopo aver configurato un server di Exchange, è possibile utilizzare il cmdlet [Test-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979798\(v=exchg.150\)) per eseguire test end-to-end della distribuzione di IRM. Questo cmdlet consente di verificare la configurazione di IRM per l'organizzazione e deve essere eseguito prima di abilitare alla posta vocale protetta. Il cmdlet **Test-IRMConfiguration** esegue i test seguenti:

  - Controlla se la configurazione di IRM per l'organizzazione di Exchange.

  - Controlla il server AD RMS per informazioni sulla versione e hotfix.

  - Verifica se un server Exchange può essere attivata la funzionalità RMS recuperando un certificato per Account con diritti e un certificato concessore di licenze Client (CLC).

  - Acquisisce i modelli di criteri per i diritti AD RMS dal server AD RMS.

  - Verifica che il mittente specificato possa inviare i messaggi protetti tramite IRM.

  - Recupera una licenza d'uso degli utenti con privilegi avanzati per il destinatario specificato.

  - Acquisisce una pre-licenza per il destinatario specificato.

Inizio pagina

## Supporto client e funzionalità per l'utente finale

Il software client di posta elettronica utilizzato per ascoltare un messaggio di posta vocale protetta deve supportare IRM e in grado di leggere un messaggio vocale protetta alla messaggistica UNIFICATA. Client di posta elettronica supportati includono MicrosoftOutlook 2010 o versioni successive, Outlook Web App e Outlook Voice Access. Nella tabella seguente contiene un elenco dei client di posta elettronica e indica se è supportate.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Client di posta elettronica</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>I messaggi vocali protetti sono supportati in Outlook 2010 e versioni successive.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><ul>
<li><p>Outlook Web App Exchange 2010 o versioni successive supporta i messaggi di posta vocale protetta. Le versioni precedenti di Outlook Web App, noto come Outlook Web Access non li supportano.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook Voice Access</p></td>
<td><ul>
<li><p>Outlook Accesso vocale nelle versioni successive e Exchange 2010 supporta la posta vocale protetta. Outlook Accesso vocale incluso in Exchange 2007 non supporta posta vocale protetta.</p></li>
<li><p>Cassetta postale dell'utente deve trovarsi in un server cassette postali in Exchange 2010 o versione successiva.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Windows Mobile o Windows Phone</p></td>
<td><ul>
<li><p>Windows Mobile non supporta il Sistema di caselle vocali protette. Windows Phone 7 e Windows Phone 8, invece, supportano questo sistema.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>Posta vocale protetta è supportata in Exchange 2010 SP1 e versioni successive.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Altri client di posta elettronica</p></td>
<td><ul>
<li><p>Il Sistema di caselle vocali protette non è supportato.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Inizio pagina

## Struttura del messaggio vocale protetto

Per ogni messaggio del Sistema di caselle vocali protette sono effettivamente coinvolti due messaggi. Il primo messaggio è il messaggio esterno, che non è crittografato. Contiene un allegato denominato message.rpmsg. L'allegato contiene il messaggio vocale protetto da IRM e i dati di controllo per la gestione dei diritti interni. I dati di controllo per la gestione dei diritti includono una chiave del contenuto e le informazioni sui diritti, con l'indicazione degli utenti a cui è consentito accedere al messaggio vocale e delle modalità di accesso.

I messaggi vocali protetti sono visualizzati nella Posta in arrivo dell'utente nella cartella di ricerca **Sistema di caselle vocali**. L'utente può ascoltare i messaggi vocali utilizzando il lettore audio incorporato come se si trattasse di un messaggio vocale standard, con la sola eccezione che il pulsante Inoltra sarà disabilitato e verrà visualizzata una nota nella parte superiore del messaggio in cui si avvisa che il messaggio è protetto e non è possibile inoltrarlo.

Per i client di posta elettronica che non supportano il Sistema di caselle vocali protette, verrà visualizzato il corpo del messaggio esterno. Gli amministratori possono includere il testo quando il software del client non supporta il Sistema di caselle vocali protette utilizzando i criteri cassetta postale di messaggistica unificata. È possibile personalizzare il testo predefinito incluso nel messaggio di posta elettronica configurando un criterio cassetta postale di messaggistica unificata. Ad esempio, è possibile configurare il criterio cassetta postale di messaggistica unificata con un testo personalizzato come *"Impossibile aprire il messaggio vocale in quanto è protetto. Per visualizzare o ascoltare il messaggio vocale, accedere alla cassetta postale all'indirizzo https://mail.contoso.com oppure comporre il numero +1 (425) 555-1234 per chiamare Outlook Voice Access."*

Inizio pagina

## Composizione di un messaggio del Sistema di caselle vocali protette

Esistono due casi in cui è possibile creare messaggi vocali protetti:

  - **Risponditore automatico**   Il risponditore automatico interviene quando un chiamante chiama un utente abilitato alla messaggistica unificata, ma questi non è disponibile per rispondere alla chiamata o la inoltra direttamente alla casella vocale. In scenari questo tipo di scenario, il sistema di caselle vocali riprodurrà una serie di istruzioni vocali dopo che il chiamante ha registrato il proprio messaggio vocale.
    
    Il chiamante può quindi scegliere tra le varie opzioni aggiuntive disponibili per i messaggi, inclusa l'opzione che consente di contrassegnare il messaggio vocale come privato premendo il tasto cancelletto (\#). Se il chiamante preme il tasto \#, può seguire le istruzioni fornite dalla messaggistica unificata per contrassegnare il messaggio come privato, rimuovere il contrassegno Privato dal messaggio vocale o contrassegnare il messaggio vocale con Priorità alta. Nel diagramma seguente vengono illustrate le opzioni di menu disponibili per i chiamanti quando viene lasciato un messaggio vocale privato per un utente.
    

    > [!NOTE]
    > Poiché il chiamate non è autenticato, per le chiamate con risponditore automatico la messaggistica unificata utilizza le impostazioni del Sistema di caselle vocali protette del criterio cassetta postale di messaggistica unificata del destinatario previsto del messaggio.

    
    **Creazione di un messaggio del Sistema di caselle vocali protette mediante il risponditore automatico**
    
    ![Creazione di caselle vocali protette con il risponditore automatico](images/Dd351041.4e9f50bf-5066-4d0a-b3eb-0515a2fc4560(EXCHG.150).jpg "Creazione di caselle vocali protette con il risponditore automatico")  

  - **Outlook Voice Access**   Outlook Voice Access consente agli utenti abilitati alla messaggistica unificata di accedere alla propria cassetta postale utilizzando telefoni analogici, digitali o cellulari componendo il proprio numero di Outlook Voice Access. Per gli utenti abilitati alla messaggistica unificata sono disponibili due interfacce utente di messaggistica unificata: l'interfaccia utente telefonica (TUI) e l'interfaccia utente vocale (VUI).
    
    Gli utenti di Outlook Voice Access possono cercare i contatti nella directory e inviare messaggi vocali. Se il sistema di caselle vocali protette è stato attivato per i destinatari abilitati alla messaggistica unificata, i chiamanti possono contrassegnare i messaggi come privati dopo averli registrati. In alternativa, gli amministratori possono configurare un criterio cassetta postale di messaggistica unificata per assicurarsi che tutti i messaggi vocali inviati da utenti autenticati siano protetti dalla messaggistica unificata.
    

    > [!NOTE]
    > Se un chiamante è autenticato, vengono applicate le impostazioni del Sistema di caselle vocali protette del criterio cassetta postale di messaggistica unificata collegato al chiamante, indipendentemente dalle impostazioni del criterio cassetta postale di messaggistica unificata per il destinatario previsto del messaggio vocale.

    
    **Creazione di un messaggio del Sistema di caselle vocali protette mediante l'interfaccia utente vocale**
    
    ![Creazione di caselle vocali protette tramite interfaccia vocale](images/Dd351041.6b425ee4-5171-4a63-961f-bdbc6c79e1be(EXCHG.150).jpg "Creazione di caselle vocali protette tramite interfaccia vocale")  
    
    **Creazione un messaggio del Sistema di caselle vocali protette mediante l'interfaccia telefonica**
    
    ![Creazione di un sistema di caselle vocali protette con l'input di composizione a toni](images/Dd351041.dd58fd38-c4c3-437c-adc1-497deb3c8a9f(EXCHG.150).jpg "Creazione di un sistema di caselle vocali protette con l'input di composizione a toni")  

Inizio pagina

## Criteri cassetta postale di messaggistica unificata

È possibile creare un criterio cassetta postale di messaggistica unificata per applicare un set di impostazioni di criteri di messaggistica UNIFICATA, ad esempio le impostazioni di criteri PIN, le restrizioni di composizione e le impostazioni di posta vocale protetta comuni a un insieme di cassette postali abilitate alla messaggistica UNIFICATA. Per ulteriori informazioni sui criteri cassetta postale di messaggistica UNIFICATA, vedere [Gestire i criteri cassetta postale di messaggistica unificata](manage-a-um-mailbox-policy-exchange-2013-help.md).

Per configurare le opzioni del Sistema di caselle vocali protette, è possibile utilizzare EAC o il cmdlet **Set-UMMailboxPolicy**. Nella tabella seguente sono elencate le impostazioni configurabili del Sistema di caselle vocali protette.

**Impostazioni del Sistema di caselle vocali protette**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro Shell</th>
<th>Impostazione disponibile in EAC</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ProtectAuthenticatedVoiceMail</em></p></td>
<td><p>Sì</p></td>
<td><p>Il parametro <em>ProtectAuthenticatedVoiceMail</em> specifica se gli utenti abilitati alla messaggistica unificata sono autorizzati a inviare messaggi vocali protetti durante l'accesso alla cassetta postale mediante Outlook Voice Access. L'impostazione predefinita è <code>None</code>. Ciò significa che non viene applicata alcuna protezione durante la composizione dei messaggi vocali e che i chiamanti non potranno contrassegnare i messaggi vocali come privati. Se il valore è impostato su <code>Private</code>, verranno protetti solo i messaggi contrassegnati come privati dal chiamante. Se il valore è impostato su <code>All</code>, verrà protetto ogni messaggio vocale, indipendentemente dall'opzione selezionata dal chiamante.</p></td>
</tr>
<tr class="even">
<td><p><em>ProtectUnauthenticatedVoiceMail</em></p></td>
<td><p>Sì</p></td>
<td><p>Il parametro <em>ProtectUnauthenticatedVoiceMail</em> consente di specificare se i server Cassette postali che rispondono alle chiamate per gli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata creano messaggi vocali protetti. L'impostazione viene applicata anche quando un messaggio viene inviato da un operatore automatico di messaggistica unificata a un utente abilitato alla messaggistica unificata. L'impostazione predefinita è <code>None</code>. Ciò significa che non viene applicata alcuna protezione ai messaggi vocali e che il chiamante non potrà contrassegnare il messaggio come Privato. Se il valore è impostato su <code>Private</code>, verranno protetti solo i messaggi contrassegnati come privati dal chiamante. Se il valore è impostato su <code>All</code>, verrà protetto ogni messaggio vocale, che sia stato contrassegnato o meno come Privato dal chiamante.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProtectedVoiceMailText</em></p></td>
<td><p>Sì</p></td>
<td><p>Il parametro <em>ProtectedVoiceMailText</em> consente di specificare il testo da includere nel corpo del messaggio esterno di un messaggio del Sistema di caselle vocali protette. Il testo verrà visualizzato in tutte le applicazioni client di posta elettronica che non supportano i messaggi del Sistema di caselle vocali protette. Quando la proprietà è impostata su <code>Null</code> o è vuota, è sempre disponibile un messaggio predefinito fornito dalla messaggistica unificata.</p></td>
</tr>
<tr class="even">
<td><p><em>RequireProtectedPlayOnPhone</em></p></td>
<td><p>Sì</p></td>
<td><p>Il parametro <em>RequireProtectedPlayOnPhone</em> consente di specificare se per gli utenti associati al criterio cassetta postale di messaggistica unificata verrà forzato l'ascolto al telefono del messaggio vocale protetto (utilizzando Ascolta al telefono). Il valore predefinito è <code>$false.</code>. Quando il valore è impostato su <code>$true</code>, il lettore multimediale audio nei moduli del Sistema di caselle vocali protette in Outlook o Outlook Web App sarà visualizzato come disabilitato. È sempre possibile accedere all'anteprima del testo del messaggio vocale. L'utente non potrà riprodurre il file audio mediante un qualsiasi software per lettore multimediale o utilizzare il lettore multimediale incorporato per ascoltare il messaggio vocale.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowVoiceResponseToOtherMessageTypes</em></p></td>
<td><p>Sì</p></td>
<td><p>Il parametro <em>AllowVoiceResponseToOtherMessageTypes</em> consente di specificare se i chiamanti autenticati in Outlook Voice Access per accedere alla propria posta elettronica potranno comporre una risposta vocale ai messaggi di posta elettronica e alle convocazioni di riunione.</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni sulla gestione delle impostazioni del Sistema di caselle vocali, vedere [Procedure della casella vocale protette](protected-voice-mail-procedures-exchange-2013-help.md) o [Set-UMMailboxPolicy](https://technet.microsoft.com/it-it/library/bb124903\(v=exchg.150\)).

Inizio pagina

## Notifiche tramite SMS e Sistema di caselle vocali protette

Gli utenti che configurano il proprio account di messaggistica unificata per l'invio di notifiche tramite SMS al proprio telefono cellulare quando ricevono messaggi vocali riceveranno anche il testo della trascrizione audio (Anteprima messaggio vocale) integrato nel corpo del messaggio di testo. Per il Sistema di caselle vocali protette ciò rappresenta tuttavia un problema di protezione, in quanto il contenuto dei messaggi vocali deve essere sempre protetto.

Quando nella messaggistica unificata viene creata una notifica tramite messaggio di testo per un messaggio vocale protetto, l'applicazione controlla se il messaggio vocale è contrassegnato come Privato. In caso affermativo, la trascrizione del testo audio non verrà aggiunta al messaggio di testo inviato al telefono cellulare. Il testo seguente verrà invece incluso nel messaggio di testo: "Utilizzare Outlook Voice Access per accedere al messaggio vocale protetto."

Inizio pagina


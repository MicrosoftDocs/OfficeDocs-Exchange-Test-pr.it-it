---
title: 'Risoluzione dei destinatari: Exchange 2013 Help'
TOCTitle: Risoluzione dei destinatari
ms:assetid: 09deda5a-d405-45b1-a3ff-fefd3d76cdea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb430743(v=EXCHG.150)
ms:contentKeyID: 52063040
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei destinatari

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-03-17_

*Soluzione destinatario* è il processo di espansione e la risoluzione di tutti i destinatari in un messaggio. Atto di risoluzione dei destinatari corrisponde a un destinatario a cui l'oggetto di Active Directory corrispondente nell'organizzazione di Microsoft Exchange. L'azione di espansione destinatari espande tutti i gruppi di distribuzione in un elenco dei destinatari singoli. Risoluzione dei destinatari consente limiti dei messaggi e destinatari alternativi da applicare in modo corretto per ciascun destinatario.

In un'organizzazione di Exchange Server 2013 Microsoft, la risoluzione dei destinatari viene eseguita dal classificatore nel servizio di trasporto sui server cassette postali. Categorizzazione su ogni messaggio verrà eseguita dopo un messaggio appena arrivato viene inserito in coda di invio. Risoluzione dei destinatari, oltre a conversione del contenuto e il routing, viene eseguita nel messaggio prima che il messaggio viene messo in una coda di recapito. Classificatore esegue la risoluzione del destinatario prima di routing. Il componente di classificatore responsabile per la risoluzione dei destinatari frequentemente viene chiamato il *sistema di risoluzione*.

**Sommario**

Soluzione principale

Espansione

La moltiplicazione e controllare l'espansione dei destinatario

Diagnostica di risoluzione dei destinatari

## Soluzione principale

*Soluzione principale* è la prima fase di risoluzione dei destinatari. Soluzione principale consente di associare ogni destinatario in un messaggio in arrivo a un oggetto destinatario corrispondente in Active Directory. Durante la risoluzione dei principale, classificatore consente di creare un elenco contenente il mittente e gli indirizzi di posta elettronica del destinatario non espansa, iniziale presenti all'interno del messaggio. Classificatore quindi utilizza tale elenco di indirizzi di posta elettronica alla query Active Directory per trovare tutti gli oggetti abilitati alla posta elettronica con corrispondenza gli attributi dell'indirizzo di posta elettronica. Quando viene rilevata una corrispondenza, le proprietà di oggetti Active Directory corrispondenti vengono memorizzati nella cache per un successivo utilizzo. Qualsiasi mittente messaggio anche restrizioni.

## Indirizzi di posta elettronica del destinatario

Soluzione principale inizia con un messaggio e l'elenco non espansa, iniziale dei destinatari dalla *busta del messaggio*. La busta del messaggio contiene i comandi utilizzati per trasmettere i messaggi tra i server di messaggistica SMTP. Indirizzo di posta elettronica del mittente è incluso nel comando **MAIL FROM:**  . Indirizzo di posta elettronica di ogni destinatario è contenuta in un comando separato **RCPT TO:**  . Il mittente della busta e destinatari busta in genere vengono creati dal mittente e destinatari nei campi dell'intestazione `To:`, `From:`, `Cc:`e `Bcc:` nell'intestazione del messaggio. Tuttavia, questo non è sempre true. I campi dell'intestazione `To:`, `From:`, `Cc:`e `Bcc:` in un messaggio sono integrati e potrebbero non corrispondere effettivo mittente o indirizzi di posta elettronica del destinatario che sono stati utilizzati per trasmettere il messaggio.

## Indirizzi di posta elettronica incapsulati

Indirizzi di posta elettronica SMTP standard seguono le specifiche RFC 2821 e RFC 2822, ad esempio chris@contoso.com, ad esempio. Tuttavia, è necessario un indirizzo di posta elettronica può inoltre essere un indirizzo di posta elettronica non SMTP incapsulato all'interno di un indirizzo SMTP valido. Exchange supporta incapsulati gli indirizzi che utilizzano il metodo encapsulation Internet Mail Connector Encapsulated Address (IMCEA).

Questo metodo encapsulation richiede la codifica dei caratteri non validi in indirizzi di posta elettronica SMTP. Caratteri alfanumerici, il segno di uguale (=) e il segno meno (-) non richiedono la codifica. Altri caratteri, utilizzare la sintassi di codifica seguente:

  - Una barra (/) è stata sostituita da un carattere di sottolineatura (\_).

  - Altri caratteri US-ASCII sono state sostituite da un segno di addizione (+) e le due cifre del suo valore ASCII vengono scritte in esadecimale. Ad esempio, il carattere spazio ha il valore codificato `+20`.

Il metodo incapsulamento IMCEA utilizza la sintassi seguente: `IMCEA<Type>-<address>@<domain>`

Il segnaposto \<*Type*\> identifica il tipo di indirizzi non SMTP, ad esempio `EX`, `X400`o `FAX`.


> [!NOTE]
> Sebbene <CODE>SMTP</CODE> e <CODE>X500</CODE> sono i valori validi teoricamente per &lt;<EM>Type</EM>&gt;, la risoluzione dei destinatari di Exchange rifiuta tutti gli indirizzi con codifica IMCEA che utilizzano uno di questi tipi.



Il segnaposto \<*address*\> corrisponde all'indirizzo originale codificato. Il segnaposto \<*domain*\> rappresenta il dominio SMTP che consente di incapsulare indirizzi non SMTP, ad esempio, contoso.com

Con il metodo incapsulamento IMCEA, gli indirizzi sono unencapsulated solo quando il dominio corrisponde il dominio autorevole predefinito nell'organizzazione di Exchange. Per ulteriori informazioni sui domini accettati, vedere [Domini accettati](accepted-domains-exchange-2013-help.md).

La lunghezza massima per un indirizzo di posta elettronica SMTP in Exchange è 571 caratteri. Questo limite include quanto segue:

  - 315 caratteri per la parte del nome dell'indirizzo

  - 255 caratteri per il nome di dominio

  - Il simbolo chiocciola (@) carattere di separazione tra la parte del nome dell'indirizzo dal nome di dominio

Si noti che Exchange non supporta i messaggi che vengono codificati con il metodo incapsulamento IMCEA quando la parte del nome dell'indirizzo supera 315 caratteri, anche se l'indirizzo di posta elettronica completo è inferiore a 571 caratteri.

## Risoluzione dell'indirizzo

Per ogni messaggio, l'indirizzo di posta elettronica del mittente e tutti gli indirizzi di posta elettronica del destinatario vengono aggiunti a un elenco è utilizzato per eseguire una query Active Directory. Uno o più indirizzi incapsulati sono unencapsulated prima che sta aggiunti all'elenco di indirizzi di posta elettronica. La query di Active Directory viene eseguita in un massimo di 20 indirizzi di posta elettronica alla volta. Se la query di Active Directory si verificano errori temporanei, il messaggio viene restituito alla coda di invio e rinviato per il periodo di tempo specificato dalla chiave *ResolverRetryInterval* in `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` applicazione file di configurazione XML associato il servizio di trasporto di Microsoft Exchange. Il valore predefinito è 30 minuti.

Nella tabella seguente vengono descritti gli oggetti destinatario presenti in Active Directory. Per ulteriori informazioni sui tipi di destinatari di Exchange, vedere [Destinatari](recipients-exchange-2013-help.md).

### Oggetti destinatario in Active Directory

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di destinatario di Active Directory</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DistributionGroup</p></td>
<td><p>Tutti gli oggetti abilitati alla posta elettronica gruppo. I tipi di oggetto gruppo di distribuzione sono i seguenti:</p>
<ul>
<li><p><strong>MailUniversalDistributionGroup</strong>   Un oggetto gruppo di distribuzione universale</p></li>
<li><p><strong>MailUniversalSecurityGroup</strong>   Un oggetto gruppo di protezione universale con un indirizzo di posta elettronica</p></li>
<li><p><strong>MailNonUniversalGroup</strong>   Un oggetto gruppo di sicurezza locale o di un oggetto gruppo di protezione globale con un indirizzo di posta elettronica</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DynamicDistributionGroup</p></td>
<td><p>Oggetto contenente le classi di Active Directory <strong>msExchDynamicDistributionList</strong>. Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/manage-dynamic-distribution-groups">Gestione dei gruppi di distribuzione dinamici</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p>Un oggetto utente che dispone di un parametro definito <em>Database</em> e un indirizzo di posta elettronica</p></td>
</tr>
<tr class="even">
<td><p>MailUser</p></td>
<td><p>Un oggetto utente che dispone di un indirizzo di posta elettronica senza un parametro definito <em>Database</em> . Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-mail-users">Gestire gli utenti di posta</a>.</p></td>
</tr>
<tr class="odd">
<td><p>MailContact</p></td>
<td><p>Un oggetto contatto che ha un indirizzo di posta elettronica. In genere, un contatto di posta elettronica viene utilizzato per destinatari esterni all'organizzazione di Exchange. Un contatto di posta elettronica viene utilizzato anche in ambienti Exchange tra foreste. Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-mail-contacts">Gestire i contatti di posta</a>.</p></td>
</tr>
<tr class="even">
<td><p>MailPublicFolder</p></td>
<td><p>Un oggetto di cartelle pubbliche con un indirizzo di posta elettronica.</p></td>
</tr>
<tr class="odd">
<td><p>MicrosoftExchangeRecipient</p></td>
<td><p>Oggetto contenente le classi di Active Directory <strong>msExchExchangeServerRecipient</strong>. Per ulteriori informazioni relative all'oggetto destinatario di Microsoft Exchange, vedere <a href="recipients-exchange-2013-help.md">Destinatari</a>.</p></td>
</tr>
<tr class="even">
<td><p>SystemAttendantMailbox</p></td>
<td><p>Oggetto contenente le classi di Active Directory <strong>exchangeAdminService</strong>. Deve esistere una sola cassetta postale del Supervisore nell'organizzazione di Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox</p></td>
<td><p>Un oggetto utente che dispone di un indirizzo di posta elettronica che si trova nel contenitore oggetti di sistema di Microsoft Exchange. Deve essere presente una cassetta postale di sistema per ogni database delle cassette postali nell'organizzazione di Exchange.</p></td>
</tr>
</tbody>
</table>


Un oggetto che contiene le proprietà critiche mancante o non valido viene classificato dalla query Active Directory come un oggetto non valido. Ad esempio, un oggetto gruppo di distribuzione dinamico senza un indirizzo di posta elettronica è considerato non valido. I messaggi inviati a destinatari classificati come oggetti non validi generano un rapporto di mancato recapito (NDR).

Per ogni indirizzo di posta elettronica, viene eseguita una singola query iniziale per tutte le proprietà dei destinatari possibili, ad esempio il destinatari identificatori, tipo di destinatario, limiti dei messaggi, indirizzi di posta elettronica e destinatari alternativi. Proprietà applicabili per il destinatario vengono memorizzati nella cache per un successivo utilizzo. Risoluzione dei destinatari classifica i destinatari in base a come i destinatari vengono risolti similarità tra e la similarità applicabile proprietà del destinatario.

Di seguito viene illustrato il filtro LDAP utilizzato per la risoluzione degli indirizzi:

  - Per il tipo di indirizzo di posta elettronica **EX** , il filtro LDAP è basato sull'attributo di Active Directory del destinatario **legacyExchangeDN** o il destinatario **proxyAddresses** attributo di Active Directory. L'attributo di Active Directory **legacyExchangeDN** ha la precedenza.

  - Per tutti gli altri tipi di indirizzi di posta elettronica, viene utilizzato l'attributo di Active Directory del destinatario **proxyAddresses** come filtro LDAP.

Se l'indirizzo di posta elettronica utilizzato nel messaggio non corrisponde l'indirizzo SMTP primario dell'oggetto Active Directory corrispondente, classificatore riscrive l'indirizzo di posta elettronica nel messaggio in modo che corrisponda all'indirizzo SMTP primario. L'indirizzo di posta elettronica originale verrà salvato nella voce `ORCPT=` nel comando **RCPT TO:**  la busta del messaggio.

## Limitazioni dei mittenti messaggio

La dimensione utilizzato per la restrizione della dimensione messaggio mittente è il valore del **X-MS-Exchange-organizzazione-OriginalSize:**  campo di intestazione nell'intestazione del messaggio. Exchange utilizza questo campo di intestazione per registrare la dimensione del messaggio originale del messaggio quando immessa l'organizzazione di Exchange. Ogni volta che il messaggio viene confrontato con la dimensione massima dei messaggi specificata, viene utilizzato il valore minore della dimensione messaggio corrente o l'intestazione di dimensione messaggio originale. Per la conversione del contenuto, la codifica e l'elaborazione dell'agente può modificare la dimensione del messaggio. Se questo campo di intestazione non esiste, viene creato utilizzando il valore di dimensione messaggio corrente. Se il messaggio è troppo grande, viene generato un rapporto di mancato recapito e l'elaborazione dei messaggi aggiuntivi viene interrotta.

Numero massimo di destinatari mittente viene applicato solo nel servizio di trasporto nel primo server cassette postali che elabora il messaggio. Il numero di destinatari busta messaggio originale e non espansa viene confrontato con il numero massimo di destinatari mittente. Il numero di destinatari busta messaggio originale e non espansa viene utilizzato per evitare i problemi di recapito messaggio parziale che si sono verificati in Microsoft Exchange Server 2003 liste di distribuzione nidificate utilizzati server di espansione remoto.

Il mittente del messaggio e tutti i destinatari sono contrassegnati come risolto da indicatori di una proprietà estesa nel messaggio. Questa proprietà estesa consente il bypass soluzione principale se il messaggio deve passare nuovamente attraverso la risoluzione dei destinatari del messaggio. Un messaggio potrebbe essere necessario passare attraverso la risoluzione dei destinatari nuovamente perché riavviare il servizio di trasporto di Microsoft Exchange.

Inizio pagina

## Espansione

L'espansione viene generato dopo la soluzione principale. Espansione espande completamente annidati i livelli dei destinatari in singoli destinatari. Espansione può richiedere più viaggi tramite il processo di espansione per espandere tutti i destinatari. Non tutti i destinatari devono essere espansi. Tuttavia, tutti i destinatari devono passare attraverso il processo di espansione. Inoltre, il processo di espansione impone restrizioni destinatario messaggi per tutti i tipi di destinatari.

Nell'elenco seguente vengono descritti i tipi di destinatari che richiedono l'espansione:

  - **Gruppi di distribuzione e gruppi di distribuzione dinamici**   Gruppi di distribuzione vengono espansi basata su **memberOf** proprietà di Active Directory. Gruppi di distribuzione dinamici sono espansi mediante la definizione della query Active Directory. Se il parametro *ExpansionServer* è impostato sul gruppo, il gruppo non viene espanso per il server corrente. Il gruppo di distribuzione viene instradato al server specificato per l'espansione.
    

    > [!NOTE]
    > Se si seleziona un server di trasporto specifica all'interno dell'organizzazione come server di espansione, l'utilizzo dei gruppi di distribuzione diventa dipende dalla disponibilità del server di espansione. Se il server di espansione è disponibile, i messaggi inviati al gruppo di distribuzione non recapitati. Se si prevede di utilizzare i server di espansione specifici per i gruppi di distribuzione, per ridurre il rischio di interruzione del servizio, è consigliabile utilizzare l'implementazione di soluzioni a disponibilità elevata per questi server.



  - **Destinatari alternativi**   Il parametro *ForwardingAddress* può essere impostato nelle cassette postali e cartelle pubbliche abilitate alla posta elettronica. Il parametro *ForwardingAddress* reindirizza tutti i messaggi al destinatario alternativo specificato. Questo è noto come un *destinatario inoltrato*. Quando un indirizzo alternativo è specificato nel parametro *ForwardingAddress* e il parametro *DeliverToMailboxAndForward* è impostato su `$true`, il messaggio viene recapitato al destinatario originale e il destinatario alternativo. Questa operazione è denominata *recapitato e inoltrata destinatario*.

  - **Catene di contatto**   Un *contatto catena* è un utente di posta elettronica o un contatto di posta elettronica con il parametro *ExternalEmailAddress* impostato sull'indirizzo di posta elettronica del destinatario di un altro nell'organizzazione di Exchange.

## Rilevamento di cicli di destinatari

Come la distribuzione gruppi, i destinatari alternativi e catene di contatti vengono espanse, classificatore verifica la presenza di *reindirizzamento continuo dei destinatari*. Un ciclo destinatario è un problema di configurazione del destinatario che causa il recapito dei messaggi agli stessi destinatari in un cerchio infinito. Nell'elenco seguente vengono descritti i diversi tipi di destinatari viene eseguito a ciclo:

  - **Ciclo destinatario dannosa**   Un ciclo dannoso del destinatario determina il recapito dei messaggi ha esito positivo. Nell'elenco seguente vengono descritti due scenari quando si verificano dannoso cicli destinatari:
    
      - Se due gruppi di distribuzione tra loro includono come membri.
    
      - Quando le cassette postali o cartelle pubbliche abilitate alla posta elettronica sono impostate su fornire e inoltrare uno a altro. Si verifica quando il parametro *DeliverToMailboxAndForward* di entrambi i destinatari è impostato su `$true` e il parametro *ForwardingAddress* viene impostato uno a altro.
    
    Quando viene rilevato un ciclo destinatario dannoso, il messaggio viene recapitato al destinatario ma non aggiuntivi vengono eseguiti tentativi di recapitare il messaggio al destinatario stesso.

  - **Esegue un ciclo destinatario interrotto**   Un ciclo destinatario interrotto non può comportare il recapito dei messaggi ha esito positivo. Un esempio di un ciclo destinatario interrotto è quando le cassette postali o cartelle pubbliche abilitate alla posta elettronica hanno il parametro *ForwardingAddress* impostato uno a altro. Quando il classificatore rileva un ciclo destinatario interrotto, attività di espansione per il destinatario interrotta e viene generato un rapporto di mancato recapito per il destinatario.

Rilevamento di cicli del destinatario non impedisce il recapito dei messaggi duplicati. Ad esempio, il gruppo di distribuzione C osserveranno il recapito dei messaggi duplicati se si verificano le condizioni seguenti:

  - Gruppo di distribuzione B e C gruppo di distribuzione sono membri del gruppo di distribuzione A.

  - Gruppo di distribuzione C è anche membro del gruppo di distribuzione B.

## Reindirizzamento dei rapporti di recapito per i gruppi di distribuzione

Quando viene espanso un gruppo di distribuzione, viene controllato il tipo di messaggio per stabilire se si tratta di un messaggio di report di recapito. Se il messaggio è un rapporto di recapito, le impostazioni di reindirizzamento del gruppo di distribuzione vengono controllate per determinare se il reindirizzamento del rapporto di recapito è obbligatorio. È possibile eliminare i rapporti di recapito in quanto i rapporti di recapito divulgare indesiderati le informazioni relative al gruppo di distribuzione e la propria appartenenza.

Nell'elenco seguente vengono descritte le impostazioni di reindirizzamento di report di recapito che sono disponibili per i gruppi di distribuzione e gruppi di distribuzione dinamici:

  - **ReportToManagerEnabled**   Questo parametro consente i rapporti di recapito vengano inviate al manager del gruppo di distribuzione. I valori validi sono `$true` o `$false`. Il valore predefinito è `$false`. Per un gruppo di distribuzione, il responsabile è controllato dal parametro *ManagedBy* nel cmdlet **Set-Group** . Per un gruppo di distribuzione dinamico, il responsabile è controllato dal parametro *ManagedBy* nel cmdlet **Set-DynamicDistributionGroup** .

  - **ReportToOriginatorEnabled**   Questo parametro consente i rapporti di recapito vengano inviate al mittente di messaggi di posta elettronica inviati a questo gruppo di distribuzione. I valori validi sono `$true` o `$false`. Il valore predefinito è `$true`.
    

    > [!NOTE]
    > Entrambi i valori di parametro <EM>ReportToManagerEnabled</EM> e il parametro <EM>ReportToOriginatorEnabled</EM> non possono essere <CODE>$true</CODE>. Se un parametro è impostato su <CODE>$true</CODE>, l'altra deve essere impostata a <CODE>$false</CODE>. I valori di entrambi i parametri possono essere <CODE>$false</CODE>. Consente di ignorare tutti il reindirizzamento di tutti i messaggi di report di recapito.



Nell'elenco seguente vengono descritti i messaggi di report di recapito disponibili:

  - **Recapito (ripristino di emergenza)**   In questo report conferma che un messaggio è stato recapitato al destinatario previsto.

  - **Notifica stato recapito (DSN)**   In questo report viene descritto il risultato di un tentativo di inviare un messaggio. Per ulteriori informazioni sui messaggi DSN, vedere [DSN e NDR in Exchange 2013](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md).

  - **Messaggio di notifica di eliminazione (MDN)**   In questo report viene descritto lo stato di un messaggio dopo che è stato inviato a un destinatario. Una notifica di lettura (RN) e una notifica di lettura non (NRN) sono entrambi gli esempi di un messaggio MDN. I messaggi MDN definiti in RFC 2298 e sono controllati dal campo dell'intestazione **Disposition-Notification-To:**  nell'intestazione del messaggio. Impostazioni MDN che utilizzano il campo di intestazione `Disposition-Notification-To:` sono compatibili con numerosi server messaggio diverso. Sono inoltre possibile definire impostazioni MDN tramite la proprietà MAPI in Microsoft Outlook ed Exchange.

  - **Rapporto di mancato recapito (NDR)**   Questo rapporto indica al mittente del messaggio che non è stato possibile recapitare il messaggio ai destinatari specificati.

  - **Notifica di lettura non (NRN)**   Questo rapporto indica che un messaggio è stato eliminato prima che è stato letto.

  - **Fuori sede (OOF)**   Questo rapporto indica che il destinatario non risponde ai messaggi di posta elettronica. Le date di fuori sede acronimo a Microsoft originale messaging system dove la notifica corrispondente è stata denominata "fuori facility."

  - **Notifica di lettura (RN)**   Questo rapporto indica che il messaggio è stato letto.

  - **Rapporto di richiamo**   Questo rapporto indica lo stato di una richiesta di richiamo per un destinatario specifico. Una richiesta di richiamo è quando un mittente tenta di richiamare un messaggio inviato utilizzando Outlook.

Quando viene inviato un messaggio di report di recapito di un gruppo di distribuzione, le impostazioni seguenti causano il messaggio di rapporto da eliminare:

  - Reindirizzamento di report non è stato impostato. In alternativa, il reindirizzamento dei rapporti è impostato per il mittente del messaggio.

  - Il reindirizzamento dei rapporti è impostato sul responsabile del gruppo di distribuzione e il messaggio di report di recapito non è un rapporto di mancato recapito.

Quando viene inviato un messaggio di report di recapito di un gruppo di distribuzione, è possibile recapitare il messaggio di report recapito al manager del gruppo di distribuzione. Si verifica quando il reindirizzamento dei rapporti è impostato sul responsabile del gruppo di distribuzione e il messaggio di report è un rapporto di mancato recapito.

Quando viene inviato un messaggio in cui non è un messaggio di report di recapito di un gruppo di distribuzione, il messaggio verrà recapitato ai membri del gruppo di distribuzione. Nell'elenco seguente sono riepilogate le impostazioni di richiesta di report:

  - Se il reindirizzamento dei rapporti è impostato per il mittente del messaggio, non vengono modificate le impostazioni della richiesta di report.

  - Se non viene impostato il reindirizzamento dei rapporti, vengono eliminate tutte le impostazioni di richiesta di report. Viene aggiunta la voce `NOTIFY=NEVER`**RCPT TO:**  per ciascun destinatario sulla busta del messaggio.

  - Se il reindirizzamento dei rapporti è impostato per il responsabile del gruppo di distribuzione, ad eccezione dei messaggi di rapporto di mancato recapito inviati al manager del gruppo di distribuzione vengono eliminate tutte le impostazioni di richiesta di report.

## Restrizioni dei messaggi sui destinatari

Il processo di espansione impone anche eventuali restrizioni di messaggio che sono configurati per i destinatari. È possibile configurare queste restrizioni singolarmente per ciascun destinatario o dislocati per tutti i server Trasporto Hub nell'organizzazione di Exchange. Nella tabella seguente vengono descritti i limiti di messaggi che sono configurati per i destinatari.

### Restrizioni dei messaggi sui destinatari

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origine</th>
<th>Parametro</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-TransportConfig</strong></p></td>
<td><p><em>MaxReceiveSize</em></p></td>
<td><p>Il parametro <em>MaxReceiveSize</em> specifica la dimensione utilizzato per le restrizioni di messaggio che sono configurate per i destinatari è il valore del campo dell'intestazione <strong>X-MS-Exchange-Organization-OriginalSize:</strong> nell'intestazione del messaggio. Exchange utilizza questo campo di intestazione per registrare la dimensione del messaggio originale del messaggio quando immessa l'organizzazione di Exchange. Ogni volta che il messaggio viene confrontato con la dimensione massima dei messaggi specificata, viene utilizzato il valore minore della dimensione messaggio corrente o l'intestazione di dimensione messaggio originale. Per la conversione del contenuto, la codifica e l'elaborazione dell'agente può modificare la dimensione del messaggio. Se questo campo di intestazione non esiste, viene creato utilizzando il valore di dimensione messaggio corrente. Se il messaggio è troppo grande, viene generato un rapporto di mancato recapito e l'elaborazione dei messaggi aggiuntivi viene interrotta.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>RequireSenderAuthenticationEnabled</em></p></td>
<td><p>Il parametro <em>RequireSenderAuthenticationEnabled</em> richiede che tutti i messaggi inviati al destinatario provengano da utenti autenticati. Quando il valore di questo parametro è impostato su <code>$true</code>, verranno rifiutati i messaggi da mittenti non autenticati. Tutti i mittenti che inviano messaggi alle cassette postali di sistema e operatore di sistema devono essere autenticati.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>AcceptMessagesOnlyFromSendersOrMembers</em></p>
<p><em>RejectMessagesFromSendersOrMembers</em></p></td>
<td><p>Il parametro <em>AcceptMessagesOnlyFromSendersOrMembers</em> specifica i mittenti o gruppi di distribuzione cui membri possono inviare messaggi al destinatario. Si noti che questo parametro combina le funzionalità dei parametri <em>AcceptMessagesOnlyFrom</em> e <em>AcceptMessagesOnlyFromDLMembers</em> precedenti.</p>
<p>Il parametro <em>RejectMessagesFromSendersOrMembers</em> specifica i mittenti o i gruppi di distribuzione i cui membri non sono consentiti inviare messaggi al destinatario. Si noti che questo parametro combina le funzionalità dei parametri <em>RejectMessagesFrom</em> e <em>RejectMessagesFromDLMembers</em> precedenti.</p>
<p>Classificatore controlla l'autorizzazione del destinatario in due passaggi. Il primo passaggio determina se il mittente è presente nel parametro <em>AcceptOnlyMessagesFromSendersOrMembers</em> o <em>RejectMessagesFromSendersOrMembers</em> . Se il mittente non viene trovato in entrambi i parametri, i gruppi di distribuzione di questi parametri sono completamente espansa. Questa espansione dei gruppi di distribuzione completa potrebbe richiedere molto tempo. È consigliabile ridurre al minimo la profondità dei gruppi di distribuzione nidificate in questi parametri.</p></td>
</tr>
</tbody>
</table>


Alcuni tipi di messaggi inviati da utenti autenticati sono esenti dai restrizioni. Nell'elenco seguente vengono descritti i messaggi che sono esenti dalla restrizioni destinatario:

  - **Tutti i messaggi che vengono inviati al destinatario di Microsoft Exchange**   Questi messaggi includono i messaggi DSN, rapporti del journal, i messaggi di quota e altri messaggi generati dal sistema inviati ai mittenti interni. Per ulteriori informazioni sul destinatario Microsoft, vedere [Destinatari](recipients-exchange-2013-help.md).

  - **Tutti i messaggi che vengono inviati dall'indirizzo postmaster esterno**   Questi messaggi sono messaggi DSN e altri messaggi generati dal sistema inviati ai mittenti dei messaggi esterni. Per ulteriori informazioni sull'indirizzo postmaster esterno, vedere [Configurare l'indirizzo postmaster esterno](configure-the-external-postmaster-address-exchange-2013-help.md).

Alcuni tipi di messaggi vengono bloccate quando vengono inviati dall'organizzazione di Exchange per i domini esterni. Le impostazioni sono controllate dai parametri seguenti nel cmdlet **Set-RemoteDomain** :

  - *AllowedOOFType*

  - *AutoForwardEnabled*

  - *AutoReplyEnabled*

  - *DeliveryReportEnabled*

  - *NDREnabled*

Per ulteriori informazioni, vedere [Domini remoti](remote-domains-exchange-2013-help.md).

Inizio pagina

## La moltiplicazione e controllare l'espansione dei destinatario

Perché l'elenco completo dei destinatari del messaggio viene espansa e risolto per la risoluzione dei destinatari, esistono casi quando è necessario creare copie diverse dello stesso messaggio. Per gli scenari seguenti vengono descritti tali situazioni:

  - **Quando i destinatari del messaggio richiedono impostazioni diversi messaggi**   Proprietà del messaggio, ad esempio leggere conferme potrebbero essere necessario da abilitare per alcuni dei destinatari e bloccati per gli altri destinatari. Creazione di una nuova versione del messaggio con proprietà leggermente diversa rispetto al messaggio originale viene chiamato *la moltiplicazione*.

  - **Per limitare il numero di destinatari busta in un singolo messaggio**   Il processo di espansione del destinatario può generare migliaia di singoli destinatari quando vengono espansi i gruppi di distribuzione di grandi dimensioni. In Exchange anziché creare una sola copia del messaggio con migliaia di destinatari busta, vengono create più copie dello stesso messaggio con un numero limitato di destinatari busta.

## Moltiplicazione

Risoluzione dei destinatari moltiplica un messaggio se si verificano le condizioni seguenti:

  - Se il mittente del messaggio in **MAIL FROM:** sulla busta del messaggio è stato aggiornato. Un esempio è quando il parametro *ReportToManagerEnabled* in un gruppo di distribuzione ha un valore pari a `$true`.

  - Quando i messaggi di risposta automatica, ad esempio DSN, i messaggi fuori sede e rapporti richiamo devono essere eliminati.

  - Quando vengono espansi i destinatari alternativi.

  - Quando un campo di intestazione **Resent-From:**  deve essere aggiunto all'intestazione del messaggio. Reinviare intestazione campi sono campi dell'intestazione informativo che possono essere utilizzati per determinare se è stato inoltrato un messaggio da un utente. Reinviare intestazione campi vengono utilizzati in modo che viene visualizzato il messaggio al destinatario come se è stato inviato direttamente dal mittente originale. Il destinatario è possibile visualizzare l'intestazione del messaggio per individuare chi ha inoltrato il messaggio. Reinviare intestazione campi sono definiti nella sezione 3.6.6 di RFC 2822.

  - Se la cronologia di espansione del gruppo di distribuzione deve essere trasmessi.

## Controllo dell'espansione dei destinatario

Quando il numero di destinatari espansi è troppo grande, il messaggio viene divisa classificatore in più copie. Questa operazione viene eseguita per limitare l'utilizzo delle risorse del sistema durante l'espansione di un messaggio. Il numero massimo di destinatari busta in un messaggio è controllato dalla chiave *ExpansionSizeLimit* nel file di configurazione dell'applicazione `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` . Il valore predefinito è 1000.


> [!WARNING]
> È consigliabile non modificare il valore della chiave <EM>ExpansionSizeLimit</EM> in un server di trasporto di Exchange in un ambiente di produzione.



Inizio pagina

## Diagnostica di risoluzione dei destinatari

Vengono fornite informazioni di creazione di relazioni e diagnostiche per la risoluzione dei destinatari per i contatori delle prestazioni e le voci del Registro di verifica dei messaggi. Queste origini consentono di identificare e diagnosticare i problemi relativi alla risoluzione dei destinatari.

## Contatori delle prestazioni per la risoluzione dei destinatari

Nella tabella seguente vengono descritti i contatori delle prestazioni disponibili per la risoluzione dei destinatari.

### Contatori delle prestazioni per la risoluzione dei destinatari

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome contatore</th>
<th>Nome visualizzato</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AmbiguousRecipientsTotal</p></td>
<td><p>Destinatari ambigui</p></td>
<td><p>Questo è il numero totale di destinatari ambigui che sono stati rilevati durante la risoluzione dei destinatari. Destinatari ambigui sono diversi destinatari che dispongono di attributi di Active Directory corrispondenti <strong>legacyExchangeDN</strong> o gli attributi di Active Directory corrispondenti <strong>proxyAddresses</strong> .</p></td>
</tr>
<tr class="even">
<td><p>AmbiguousSendersTotal</p></td>
<td><p>Mittenti ambigui</p></td>
<td><p>Questo è il numero dei mittenti ambigui che sono stati rilevati durante la risoluzione dei destinatari. Mittenti ambigui sono mittenti diversi attributi di Active Directory corrispondenti <strong>legacyExchangeDN</strong> o gli attributi di Active Directory corrispondenti <strong>proxyAddresses</strong> .</p></td>
</tr>
<tr class="odd">
<td><p>FailedRecipientsTotal</p></td>
<td><p>Destinatari non riusciti</p></td>
<td><p>Questo è il numero di destinatari non riusciti che sono stati rilevati durante la risoluzione dei destinatari.</p></td>
</tr>
<tr class="even">
<td><p>LoopRecipientsTotal</p></td>
<td><p>Destinatari loop</p></td>
<td><p>Questo è il numero di destinatari che non sono stati la risoluzione dei destinatari a causa di reindirizzamento continuo dei destinatari.</p></td>
</tr>
<tr class="odd">
<td><p>MessagesChippedTotal</p></td>
<td><p>Messaggi schegge</p></td>
<td><p>Questo è il numero totale di copie dello stesso messaggio che sono stati creati durante la risoluzione del destinatario per controllare il numero di destinatari busta in un singolo messaggio. In Exchange questo processo è denominato <em>chipping</em>.</p></td>
</tr>
<tr class="even">
<td><p>MessagesCreatedTotal</p></td>
<td><p>Messaggi creati</p></td>
<td><p>Questo è il numero di messaggi che sono stati creati durante la risoluzione dei destinatari.</p></td>
</tr>
<tr class="odd">
<td><p>MessagesRetriedTotal</p></td>
<td><p>Messaggi ritentati</p></td>
<td><p>Questo è il numero di messaggi il cui pianificate per un nuovo tentativo durante la risoluzione dei destinatari.</p></td>
</tr>
<tr class="even">
<td><p>UnresolvedOrgRecipientsTotal</p></td>
<td><p>Destinatari organizzazione non risolte</p></td>
<td><p>Questo è il numero di destinatari non risolti da un dominio attendibile che sono stati rilevati durante la risoluzione dei destinatari.</p></td>
</tr>
<tr class="odd">
<td><p>UnresolvedOrgSendersTotal</p></td>
<td><p>Mittenti organizzazione non risolte</p></td>
<td><p>Questo è il numero dei mittenti non risolti da un dominio attendibile che sono stati rilevati durante la risoluzione dei destinatari.</p></td>
</tr>
</tbody>
</table>


## Eventi di risoluzione dei destinatari nel Registro di verifica messaggi

Nella tabella seguente vengono descritti gli eventi di risoluzione dei destinatari che vengono scritti nel Registro di verifica messaggi.

### Eventi di risoluzione dei destinatari nel Registro di verifica messaggi

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Evento di verifica messaggi</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ESPANDERE</p></td>
<td><p>Questo evento indica che è stato espanso un gruppo di distribuzione.</p></td>
</tr>
<tr class="even">
<td><p>REINDIRIZZAMENTO</p></td>
<td><p>Questo evento indica che un messaggio inviato al destinatario una cassetta postale o un destinatario abilitato alla posta cartelle pubbliche è stato reindirizzato a un destinatario alternativo come specificato dal parametro <em>ForwardingAddress</em> .</p></td>
</tr>
<tr class="odd">
<td><p>RISOLVERE</p></td>
<td><p>Questo evento indica che un indirizzo di posta elettronica del destinatario è stato modificato per l'indirizzo di posta elettronica SMTP primario dell'oggetto destinatario di Active Directory corrispondente.</p></td>
</tr>
<tr class="even">
<td><p>TRASFERIMENTO</p></td>
<td><p>Questo evento indica che la moltiplicazione messaggio o chipping si sono verificati.</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni sulla verifica messaggi, vedere [Verifica messaggi](message-tracking-exchange-2013-help.md).


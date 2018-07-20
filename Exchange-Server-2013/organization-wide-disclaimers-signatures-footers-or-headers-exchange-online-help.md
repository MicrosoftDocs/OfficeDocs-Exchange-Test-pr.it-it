---
title: "Intestazioni, piè di pagina, firme o dichiarazioni di non responsabilità per tutta l'organizzazione: Exchange 2013 Help"
TOCTitle: Intestazioni, piè di pagina, firme o dichiarazioni di non responsabilità per tutta l'organizzazione
ms:assetid: e45e33c9-e53b-427c-ada5-70901bc399b8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn600437(v=EXCHG.150)
ms:contentKeyID: 61060491
ms.date: 02/14/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Intestazioni, piè di pagina, firme o dichiarazioni di non responsabilità per tutta l'organizzazione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile aggiungere una dichiarazione di non responsabilità per le e-mail, una dichiarazione di non responsabilità legale, una dichiarazione di trasparenza, una firma o altre informazioni nella parte superiore o inferiore dei messaggi di posta elettronica inviati o ricevuti dall'organizzazione. Ciò potrebbe essere necessario per requisiti legali, aziendali o normativi, per identificare messaggi di posta elettronica potenzialmente non sicuri o per altri motivi specifici per la propria organizzazione.

Per configurare una dichiarazione di non responsabilità, si crea una regola di trasporto che include le condizioni (come quando il mittente è in un gruppo specifico o quando il messaggio include specifici pattern di testo) e il testo da aggiungere. Per applicare più dichiarazioni di non responsabilità a un singolo messaggio di posta elettronica, si utilizzano più regole di trasporto.


> [!IMPORTANT]
> <UL>
> <LI>
> <P>Se si desidera che le informazioni vengano aggiunte solo ai messaggi in uscita, è necessario aggiungere una condizione relativa ai destinatari situati all'esterno dell'organizzazione. Per impostazione predefinita, le regole di trasporto vengono applicate sia ai messaggi in arrivo sia ai messaggi in uscita.</P></LI></UL>



**Sommario**

Esempi

Ambito della dichiarazione di non responsabilità

Formattazione della dichiarazione di non responsabilità

Opzioni di fallback se non è possibile aggiungere la dichiarazione di non responsabilità

Ulteriori informazioni

Per informazioni sulle procedure, vedere [Intestazioni, piè di pagina, firme o dichiarazioni di non responsabilità nei messaggi per tutta l'organizzazione in Office 365](https://technet.microsoft.com/it-it/library/dn600323\(v=exchg.150\)).

## Esempi

Di seguito sono riportati dei suggerimenti su come poter utilizzare le dichiarazioni di non responsabilità.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo</th>
<th>Testo di esempio aggiunto</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Note legali – messaggi in uscita</p></td>
<td><p>Questo messaggio di posta elettronica e i file trasmessi con esso sono confidenziali e destinati esclusivamente all'uso dei singoli utenti o enti ai quali sono indirizzati. Nel caso in cui il messaggio sia stato ricevuto per errore, si prega di informare il gestore di sistema.</p></td>
</tr>
<tr class="even">
<td><p>Note legali – messaggi in arrivo</p></td>
<td><p>I dipendenti non devono rilasciare dichiarazioni diffamatorie né violare in nessun modo il copyright o altri diritti legali tramite comunicazioni via posta elettronica. I dipendenti che ricevono messaggi di posta elettronica di questo tipo devono comunicarlo immediatamente al proprio supervisore.</p></td>
</tr>
<tr class="odd">
<td><p>Il messaggio è stato inviato a un alias</p></td>
<td><p>Questo messaggio è stato inviato al gruppo di discussione Vendite.</p></td>
</tr>
<tr class="even">
<td><p>Firma – pull dei dati per ogni dipendente</p></td>
<td><p>Kathleen Mayer<br />
Sales Department<br />
Contoso<br />
www.contoso.com<br />
kathleen@contoso.com<br />
cell: 111-222-1234</p></td>
</tr>
<tr class="odd">
<td><p>Annuncio</p></td>
<td><p>Fare clic qui per le promozioni di marzo</p></td>
</tr>
</tbody>
</table>


Gli esempi in questo articolo non sono destinati all'utilizzo nella forma in cui sono riportati. Modificarli in base alle proprie esigenze.

## Ambito della dichiarazione di non responsabilità

Durante la creazione delle dichiarazioni di non responsabilità, tenere in considerazione a quali messaggi devono essere applicate. Ad esempio, è possibile specificare dichiarazioni di non responsabilità diverse per messaggi interni ed esterni oppure per messaggi inviati da utenti in reparti specifici. Per assicurarsi che una dichiarazione di non responsabilità venga visualizzata solo nel primo messaggio di una conversazione, aggiungere un'eccezione che individui il testo univoco nella dichiarazione di non responsabilità.

Di seguito sono riportati alcuni esempi delle condizioni ed eccezioni che è possibile utilizzare.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Descrizione</th>
<th>Condizioni ed eccezioni nell'Interfaccia di amministrazione di Exchange</th>
<th>Condizioni ed eccezioni in Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>All'esterno dell'organizzazione, se il messaggio originale non include il testo della dichiarazione di non responsabilità, come &quot;CONTOSO LEGAL NOTICE&quot; (Note legali Contoso)</p></td>
<td><p>Condizione: <strong>Il destinatario si trova</strong> &gt; <strong>Al di fuori dell'organizzazione</strong>.</p>
<p>Eccezione: <strong>L'oggetto o il corpo</strong> &gt; <strong>l'oggetto o il corpo del messaggio corrisponde a questi modelli di testo</strong> &gt; <strong>CONTOSO LEGAL NOTICE</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -ExceptIf -SubjectOrBodyMatches &quot;CONTOSO LEGAL NOTICE&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>Messaggi in arrivo con allegati eseguibili</p></td>
<td><p>Condizione 1: <strong>Il mittente si trova</strong> &gt; <strong>Al di fuori dell'organizzazione</strong></p>
<p>Condizione 2: <strong>L'allegato</strong> &gt; <strong>ha contenuto eseguibile</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -AttachmentHasExecutableContent</code></pre></td>
</tr>
<tr class="odd">
<td><p>Il mittente è del reparto Marketing</p></td>
<td><p>Condizione: <strong>Il mittente</strong> &gt; <strong>è un membro del gruppo</strong> &gt; <strong>nome gruppo</strong></p></td>
<td><pre><code>-FromMemberOf &quot;Marketing Team&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>Tutti i messaggi provenienti da un mittente esterno destinati al gruppo di discussione Vendite</p></td>
<td><p>Condizione 1: <strong>Il mittente si trova</strong> &gt; <strong>Al di fuori dell'organizzazione</strong></p>
<p>Condizione 2: <strong>Il messaggio</strong> &gt; <strong>contiene questa persona nella casella A o Cc</strong> &gt; <strong>nome gruppo</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -SentTo &quot;Sales Discussion Group&quot; -PrependSubject &quot;Sent to Sales Discussion Group: &quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>Anteporre un annuncio ai messaggi in uscita per un mese</p></td>
<td><p>Condizione 1: <strong>Il destinatario si trova</strong> &gt; <strong>Al di fuori dell'organizzazione</strong></p>
<p>Specificare le date nella parte inferiore della casella di dialogo <strong>Nuova regola</strong>.</p></td>
<td><p>-ApplyHtmlDisclaimerLocation 'Prepend' -SentToScope 'NotInOrganization' –ActivationDate ‘03/1/2014’ –ExpiryDate ‘03/31/2014’</p></td>
</tr>
</tbody>
</table>


Per un elenco completo delle condizioni per le regole di trasporto che è possibile utilizzare per definire la dichiarazione di non responsabilità, vedere uno dei seguenti argomenti:

  - [Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online](https://technet.microsoft.com/it-it/library/jj919235\(v=exchg.150\)) (Exchange Online)

  - [Condizioni delle regole di trasporto (predicati)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) (Exchange 2013)

  - [Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online](https://technet.microsoft.com/it-it/library/jj919235\(v=exchg.150\)) (Exchange Online Protection)

## Formattazione della dichiarazione di non responsabilità

È possibile formattare la dichiarazione di non responsabilità in base alle esigenze. Di seguito è riportato quello che è possibile includere nel testo della dichiarazione di non responsabilità.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di informazioni</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Testo</p></td>
<td><p>La lunghezza massima è di 5.000 caratteri, compresi tag HTML e CSS (Cascading Style Sheets) incorporati.</p></td>
</tr>
<tr class="even">
<td><p>HTML e CSS incorporati</p></td>
<td><p>È possibile utilizzare stili HTML e CSS incorporati per formattare il testo. Ad esempio, utilizzare il tag <code>&lt;HR&gt;</code> per aggiungere una riga prima della dichiarazione di non responsabilità.</p>
<p>Se la dichiarazione di non responsabilità viene aggiunta a un messaggio di testo normale, il tag HTML viene ignorato.</p></td>
</tr>
<tr class="odd">
<td><p>Aggiunta di immagini</p></td>
<td><p>Utilizzare il tag <code>&lt;IMG&gt;</code> per puntare a un'immagine disponibile su Internet. Esempio: <code>&lt;IMG src=&quot;http://contoso.com/images/companylogo.gif&quot; alt=&quot;Contoso logo&quot;&gt;</code></p>
<p>Tenere presente che Outlook Web App e Outlook bloccano per impostazione predefinita il contenuto Web esterno (incluse le immagini). Può essere necessario che gli utenti eseguano un'azione specifica se desiderano visualizzare il contenuto esterno bloccato. Pertanto, le immagini aggiunte utilizzando il tag <code>IMG</code> potrebbero non essere visibili per impostazione predefinita. È consigliabile provare le dichiarazioni di non responsabilità con tag <code>IMG</code> nei client di posta elettronica probabilmente utilizzati dai destinatari per assicurarsi che vengano visualizzate correttamente.</p></td>
</tr>
<tr class="even">
<td><p>Aggiunta di informazioni per firme personalizzate</p></td>
<td><p>Se si desidera che tutti abbiano firme con la stessa formattazione e con le stesse informazioni, è possibile aggiungere informazioni univoche per ogni dipendente, come <code>DisplayName</code>, <code>FirstName</code>, <code>LastName</code>, <code>PhoneNumber</code>, <code>Email</code>, <code>FaxNumber</code> e <code>Department</code>. Queste informazioni devono essere racchiuse tra due segni di percentuale (%%) su ciascun lato delle informazioni. Ad esempio, per utilizzare <code>DisplayName</code>, è necessario inserire <strong>%%DisplayName%%</strong> nella dichiarazione di non responsabilità.</p>
<p>Quando una regola relativa alle dichiarazioni di non responsabilità è attivata, vengono inseriti i valori corrispondenti per l'utente. I dati provengono dall'account utente di Active Directory del mittente (per un server Exchange locale) o da un account di Office 365 del mittente per Exchange Online.</p>
<p>Per un elenco completo degli attributi che è possibile utilizzare nelle dichiarazioni di non responsabilità e nelle firme personalizzate, vedere la descrizione della proprietà <code>ADAttribute</code> in <a href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">Condizioni delle regole di trasporto (predicati)</a> (Exchange Server), <a href="https://technet.microsoft.com/it-it/library/jj919235(v=exchg.150)">Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online</a> (Exchange Online) o <a href="https://technet.microsoft.com/it-it/library/jj919234(v=exchg.150)">Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online Protection</a> (Exchange Online Protection).</p></td>
</tr>
</tbody>
</table>


Di seguito è riportato un esempio di una dichiarazione di non responsabilità HTML che include una firma, un tag `IMG` e CSS incorporato.

    <div style="font-size:9pt;  font-family: 'Calibri',sans-serif;">
    %%displayname%%</br>
    %%title%%</br>
    %%company%%</br>
    %%street%%</br>
    %%city%%, %%state%% %%zipcode%%</div>
    &nbsp;</br>
    <div style="background-color:#D5EAFF; border:1px dotted #003333; padding:.8em; ">
    <div><img alt="Fabrikam"  src="http://fabrikam.com/images/fabrikamlogo.png"></div>
    <span style="font-size:12pt;  font-family: 'Cambria','times new roman','garamond',serif; color:#ff0000;">HTML Disclaimer Title</span></br>
    <p style="font-size:8pt; line-height:10pt; font-family: 'Cambria','times roman',serif;">This message contains confidential information and is intended only for the individual(s) addressed in the message. If you are not the named addressee, you should not disseminate, distribute, or copy this e-mail. If you are not the intended recipient, you are notified that disclosing, distributing, or copying this e-mail is strictly prohibited.  </p>
    <span style="padding-top:10px; font-weight:bold; color:#CC0000; font-size:10pt; font-family: 'Calibri',Arial,sans-serif; "><a href="http://www.fabrikam.com">Fabrikam, Inc. </a></span></br></br>
    </div>

## Opzioni di fallback se non è possibile aggiungere la dichiarazione di non responsabilità

Alcuni messaggi, ad esempio i messaggi crittografati, impediscono che Exchange modifichi il contenuto del messaggio originale. È possibile controllare le modalità con cui l'organizzazione gestisce tali messaggi. È possibile specificare se inserire un messaggio non modificabile in una busta del messaggio contenente la dichiarazione di non responsabilità, se rifiutare il messaggio se non è possibile aggiungere una dichiarazione di non responsabilità oppure se ignorare l'azione della dichiarazione di non responsabilità e recapitare il messaggio senza una dichiarazione di non responsabilità.

Nell'elenco seguente viene descritta ciascuna azione di fallback:

  - **Racchiudi**   Se la dichiarazione di non responsabilità non può essere inserita nel messaggio originale, Exchange "racchiude" questo in una nuova busta di messaggio. La dichiarazione di non responsabilità viene quindi inserita nel nuovo messaggio. Se non può essere racchiuso in una nuova busta di messaggio, il messaggio originale non viene recapitato. Il mittente del messaggio riceve un rapporto di mancato recapito (NDR, Non-Delivery Report) in cui sono spiegati i motivi per i quali il messaggio non è stato recapitato.
    

    > [!IMPORTANT]
    > Se un messaggio originale viene racchiuso in una nuova busta del messaggio, le regole di trasporto successive vengono applicate alla nuova busta di messaggio e non al messaggio originale. È necessario quindi configurare le regole di trasporto con le azioni della dichiarazione di non responsabilità che racchiudono i messaggi originali in un nuovo corpo del messaggio dopo che sono state configurate altre regole di trasporto.



  - **Rifiuta**   Se la dichiarazione di non responsabilità non può essere inserita nel messaggio originale, il messaggio non viene recapitato da Exchange. Il mittente del messaggio riceve un rapporto di mancato recapito in cui sono spiegati i motivi per i quali il messaggio non è stato recapitato.

  - **Ignora**   Se la dichiarazione di non responsabilità non può essere inserita nel messaggio originale, Exchange recapita inalterato il messaggio originale. Non viene aggiunta alcuna dichiarazione di non responsabilità.

## Ulteriori informazioni

[Intestazioni, piè di pagina, firme o dichiarazioni di non responsabilità nei messaggi per tutta l'organizzazione in Office 365](https://technet.microsoft.com/it-it/library/dn600323\(v=exchg.150\))

[Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

[Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) (Exchange Online)

[Regole del flusso di posta (regole di trasporto in Exchange Online Protection](https://technet.microsoft.com/it-it/library/dn271424\(v=exchg.150\)) (Exchange Online Protection)


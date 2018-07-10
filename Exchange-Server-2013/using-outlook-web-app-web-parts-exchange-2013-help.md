---
title: 'Utilizzo di Outlook Web App Web parts: Exchange 2013 Help'
TOCTitle: Utilizzo di Outlook Web App Web parts
ms:assetid: 7272e3ab-430c-4d6c-8621-9535236ce463
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt574711(v=EXCHG.150)
ms:contentKeyID: 70076149
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzo di Outlook Web App Web parts

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-07-31_

È possibile utilizzare MicrosoftOfficeOutlook Web App Web part per specificare la cassetta postale per aprire, nella cartella all'interno di tale cassetta postale per aprire e la visualizzazione del contenuto da utilizzare.

Outlook Web App Web part consentono di accedere al contenuto Outlook Web App direttamente da un URL. L'URL può essere immesso in un Web browser o incorporato in un'applicazione. Web part non sono in genere creata manualmente. In realtà, vengono creati a livello di programmazione in base alle selezioni eseguite in un'interfaccia utente (UI) o sono stati incorporati direttamente in un'applicazione, ad esempio una pagina di SharePoint Server. Code-behind dell'interfaccia utente crea quindi l'URL. È possibile utilizzare Outlook Web App le Web part è per la visualizzazione calendario o posta in arrivo dell'utente in una pagina di SharePoint.


> [!NOTE]
> Per utilizzare Outlook Web App le Web part, sia cassetta postale dell'utente e la cassetta postale vengono aperti tramite una Web Part devono trovarsi nella stessa foresta Active Directory.



## Autorizzazioni per l'utilizzo di Web part di Outlook Web Access

Per utilizzare Outlook Web App Web part, è necessario, come minimo essere delega per l'accesso al contenuto che si desidera aprire "Revisore". Se è stato incorporato un Outlook Web App Web Part che richiede l'autenticazione in un'applicazione, è necessario passare le informazioni di autenticazione tramite con la richiesta per la Web Part. Per ottenere questo risultato, è necessario configurare la directory virtuale Outlook Web App per utilizzare l'autenticazione integrata Windows. Autenticazione integrata Windows consente agli utenti che già siano effettuato l'accesso tramite loro di utilizzare account Active DirectoryOutlook Web App senza dover immettere di nuovo le proprie credenziali.

## Sintassi di Outlook Web App Web part

Outlook Web App in Exchange 2013 dispone di un formato di URL da utilizzare per le richieste per la directory virtuale /owa. Digitare un URL direttamente in un Web browser o incorporando l'URL in un'applicazione Web, ad esempio una pagina di SharePoint Server, è possibile effettuare queste richieste.

Outlook Web App Web part può essere utilizzata per creare gli URL di complessità diversi. Un URL semplice di Web Part può essere utilizzato per aprire la cartella Posta in arrivo di qualsiasi cassetta postale. Un URL di Web Part più complesse è utilizzato per specificare la cassetta postale per aprire, nella cartella all'interno di tale cassetta postale per aprire e la visualizzazione del contenuto da utilizzare.

A seconda delle misure di protezione che sono state applicate alla propria rete, è necessario configurare la codifica per l'URL di Web part. Dopo aver configurato la codifica, code-behind dell'interfaccia utente verrà creato l'URL utilizzando i parametri URL codificato. Parametri con codifica URL utilizzano % 20 al posto di spazi e % 2f al posto delimitatore percorso "/". Tutti gli esempi in questo argomento utilizzano codificato.

Nella tabella seguente sono elencati i parametri di una Web Part e gli esempi di come utilizzarli.

### Parametri di Web Part e modalità di utilizzo

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro URL</th>
<th>Descrizione</th>
<th>Esempi e i valori</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nome del server e directory (obbligatorio)</p></td>
<td><p>L'URL della directory virtuale Outlook Web App.</p></td>
<td><p>Ciò può essere lo stesso URL utilizzato dagli utenti per accedere a Outlook Web App, ad esempio:</p>
<p>https://&lt;<em>server name</em>&gt; / owa</p></td>
</tr>
<tr class="even">
<td><p>Identificazione della cassetta postale di Exchange 2013 esplicita di accesso (facoltativo)</p></td>
<td><p>Qualsiasi indirizzo SMTP è associato alla cassetta postale da aprire.</p>
<p>Se in questa sezione dell'URL non è presente, verrà aperta la cassetta postale predefinito dell'utente autenticato.</p>
<p>Se viene specificato alcun parametro aggiuntivo, il comportamento predefinito consiste nell'aprire la cartella Posta in arrivo.</p></td>
<td><p>Per aprire la cassetta postale con tsmith@fourthcoffee.com l'indirizzo SMTP, utilizzare l'URL seguente:</p>
<p>https://&lt;<em>server name</em>&gt;/owa/tsmith@fourthcoffee.com</p></td>
</tr>
<tr class="odd">
<td><p>cmd (obbligatorio se si specificano i parametri diversi dall'identificazione delle cassette postali di accesso esplicito)</p></td>
<td><p>? cmd = Outlook Web App Web Part specificato dai parametri anziché l'interfaccia utente completa Outlook Web App consente di visualizzare contenuto.</p></td>
<td><p>Se delle cassette postali sono specificata, il parametro cmd segua l'indirizzo di accesso, come indicato di seguito:</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd = contenuto</p>
<p>Se una cassetta postale è specificata, il parametro cmd viene dopo l'identificazione esplicita delle cassette postali, come indicato di seguito:</p>
<p>https://&lt;<em>server name</em>&gt; /owa/ &lt;<em>SMTP address</em>&gt; / ?cmd = contenuto</p>
<p>Se non vengono specificati parametri aggiuntivi, il comportamento predefinito consiste nell'aprire la cartella Posta in arrivo.</p></td>
</tr>
<tr class="even">
<td><p>exsvurl</p></td>
<td><p>Questo parametro deve essere incluso quando si utilizza l'autenticazione LiveID</p>
<p>Verranno eliminati tutti i parametri durante l'autenticazione LiveID se &quot;exsvurl = 1&quot; non è presente. Questo parametro è riservato solo cassette postali di Office 365.</p></td>
<td><p>nome https://&lt;server &gt; /owa/? cmd = contenuto &amp; exsvurl = 1</p></td>
</tr>
<tr class="odd">
<td><p>fpath (facoltativo)</p></td>
<td><p>Questa parte dell'URL potrebbe essere scritto utilizzando la codifica degli URL in modo che possa passare attraverso i firewall.</p>
<p>Quando si utilizza la codifica degli URL, uno spazio diventa % 20, mentre un delimitatore di percorso (/) diventa % 2f.</p>
<p>Dalla radice della cassetta postale deve iniziare la gerarchia di cartelle.</p>
<p>In questo percorso della cartella consente di scegliere le normali cartelle o le cartelle ricerche.</p></td>
<td><p>Per aprire i progetti di sottocartelle nella posta in arrivo, utilizzare l'URL seguente:</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd = contenuto &amp; fpath = 2fprojects % posta in arrivo</p></td>
</tr>
<tr class="even">
<td><p>modulo (facoltativo)</p></td>
<td><p>Questo parametro può essere utilizzato per specificare una delle cartelle predefinite senza conoscere il nome localizzato.</p></td>
<td><p>I valori per il parametro module sono maiuscole/minuscole e sono incluse le seguenti:</p>
<ul>
<li><p>Posta in arrivo</p></li>
<li><p>Calendario</p></li>
<li><p>Teammailbox</p></li>
</ul>
<p>Per aprire il calendario di una cassetta postale indipendentemente dalla localizzazione, utilizzare l'URL seguente:</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd = contenuto &amp; modulo = Calendario</p></td>
</tr>
<tr class="odd">
<td><p>visualizzazione (facoltativo)</p></td>
<td><p>Questo parametro specifica la visualizzazione da visualizzare per la cartella.</p>
<p>Le visualizzazioni predefinite quando questo parametro non è presente sono i seguenti:</p>
<ul>
<li><p>Calendario ogni giorno</p></li>
<li><p>Messaggi dei messaggi</p></li>
</ul>

> [!NOTE]
> Le stringhe per le visualizzazioni predefinite vengono automaticamente URL codificato.


<p>L'ordinamento predefinito per una visualizzazione è il metodo che della cartella verranno ordinata se è stata aperta nel client Outlook Web App.</p>
<p>Le stringhe che identificano le visualizzazioni non sono localizzate e non fanno distinzione tra maiuscole e minuscole.</p></td>
<td><p>Le visualizzazioni disponibili variano in base al tipo di cartella.</p>
<p>Visualizzazioni del calendario:</p>
<ul>
<li><p>Visualizzazione calendario ogni giorno giornaliero</p></li>
<li><p>Visualizzazione calendario settimanale settimanale</p></li>
<li><p>Visualizzazione calendario mensile mensile</p></li>
</ul>
<p>Visualizzazioni dei messaggi:</p>
<ul>
<li><p>Visualizzazione di messaggi di messaggi, con ordinamento predefinito</p></li>
<li><p>Per 20Sender % visualizzazione dei messaggi ordinati in base dal mittente cui nome inizia con &quot;a&quot; in primo piano</p></li>
<li><p>Dalla visualizzazione di messaggi 20Subject % ordinati in base all'oggetto con oggetti che iniziano con &quot;a&quot; in primo piano</p></li>
<li><p>Da % 20Conversation % 20Topic conversazione consente di visualizzare, non è disponibile nella versione light di Outlook Web App</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>d, m, y (facoltativo)</p></td>
<td><p>Specifica la data di cui deve essere visualizzato nel calendario. Questi parametri possono essere immesso in qualsiasi ordine e possono essere utilizzati individualmente o insieme.</p>
<p>Se uno di questi parametri non è specificato, i valori predefiniti sono i valori di giorno, mese e anno correnti. Ad esempio, se il giorno corrente sia 3 maggio 2016 e si specifica un valore del mese di &quot;9&quot; per settembre, la data visualizzata sarà 3 settembre 2016.</p></td>
<td><p>I valori validi per i parametri di dati sono i seguenti:</p>
<p>g = [1-31]</p>
<p>m = [1-12]</p>
<p>y = [anno a quattro cifre]</p>
<p>Per aprire un calendario per la data 3 maggio 2016, è necessario utilizzare l'URL seguente: https://&lt;<em>server name</em>&gt;/owa/?cmd = contenuto &amp; fpath = calendario &amp; visualizzazione = giornaliera &amp; d = m &amp; 3 = 5 &amp; y = 2016</p></td>
</tr>
<tr class="odd">
<td><p>parte (facoltativo)</p></td>
<td><p>Specifica che Outlook Web App deve essere visualizzata una Web Part di dimensioni ridotte.</p></td>
<td><p>Quando si utilizza Web part per accedere al contenuto Outlook Web App, l'interfaccia utente visualizzata è minore completo Outlook Web App dell'interfaccia utente. Il parametro part consente di ridurre ulteriormente l'interfaccia utente. L'URL di esempio seguente viene visualizzato l'elenco attività nel formato più piccolo di Web Part:</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd = contenuto &amp; parte = 1</p>
<p>Parametro parte non si applica alla funzionalità calendario.</p></td>
</tr>
<tr class="even">
<td><p>FolderList</p></td>
<td><p>Questo parametro parte include il controllo elenco di cartelle per gli utenti per spostarsi tra le sottocartelle. Si applica solo alle cartelle di posta elettronica.</p></td>
<td><p>nome https://&lt;server &gt; /owa/? cmd = contenuto &amp; folderlist = 1</p></td>
</tr>
</tbody>
</table>


## Immettere manualmente Web part di Outlook Web App

Outlook Web App Web part può essere anche essere immesso manualmente in un Web browser. Ad esempio, un utente può utilizzare un Outlook Web App URL delle Web Part per aprire il calendario di un altro utente.

Nell'esempio seguente viene illustrato come accedere direttamente alle visualizzazioni di Outlook Web App comuni:

  - **Cartella Posta in arrivo:**  https://*\<server name\>*/owa/?cmd = contenuto & modulo = posta in arrivo

  - **(Oggi) del calendario:** https://*\<server name\>*/owa/?cmd contenuto & modulo calendario & exsvurl = 1

  - **(Weekly) del calendario:**  https://*\<server name\>*/owa/?cmd = contenuto & modulo = calendario & visualizzazione = settimanale & exsvurl = 1

  - **Calendario (mensile):**  https://*\<server name\>*/owa/?cmd = contenuto & modulo = calendario & visualizzazione mensile & exsvurl = 1

## Per ulteriori informazioni

  - [Personalizzare le pagine di accesso, di selezione della lingua e di errore di Outlook Web App](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md)

  - [Creare un tema per Outlook Web App](create-a-theme-for-outlook-web-app-exchange-2013-help.md)


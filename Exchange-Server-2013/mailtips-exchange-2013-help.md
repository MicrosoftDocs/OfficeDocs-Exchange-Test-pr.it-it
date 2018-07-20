---
title: 'MailTips: Exchange 2013 Help'
TOCTitle: MailTips
ms:assetid: 9c989167-cc0c-40a6-82ba-383f573bd2d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ649091(v=EXCHG.150)
ms:contentKeyID: 50481276
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# MailTips

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-04-28_

I suggerimenti messaggio sono messaggi informativi visualizzati agli utenti mentre compongono un messaggio. Microsoft Exchange Server 2013 analizza il messaggio, incluso l'elenco di destinatari a cui è indirizzato e, se rileva un potenziale problema, lo notifica all'utente con i suggerimenti messaggio prima di inviare il messaggio. Con l'aiuto delle informazioni fornite dai suggerimenti messaggio, i mittenti possono adattare il messaggio che stanno componendo per evitare situazioni indesiderate o rapporti di mancato recapito.

## Come funzionano i Suggerimenti messaggio

I Suggerimenti messaggio sono implementati come servizio Web in Exchange 2013. Quando un mittente compone un messaggio, il software client effettua una chiamata di tipo servizio Web di Exchange al server Accesso client per ottenere l'elenco dei Suggerimenti messaggio. Il server risponde inviando l'elenco di Suggerimenti messaggio appropriati per quel messaggio e il software client visualizza i Suggerimenti messaggio al mittente.

I seguenti scenari sono comuni in qualsiasi ambiente di messaggistica:

  - Rapporti di mancato recapito risultanti da messaggi che violano le restrizioni configurate in un'organizzazione (ad esempio, limitazioni nella dimensione dei messaggi o numero massimo di destinatari per messaggio).

  - Rapporti di mancato recapito risultanti da messaggi inviati a destinatari che non esistono o che sono soggetti a restrizioni oppure a utenti la cui cassetta postale è piena.

  - Invio di messaggi a utenti con la funzionalità Risposte automatiche configurata.

Tutti questi scenari prevedono che l'utente invii un messaggio e si aspetti che questo venga recapitato, ma riceva invece una risposta che lo informa che il messaggio non è stato recapitato. Anche nell'ipotesi migliore, ad esempio nel caso di risposta automatica, questi eventi provocano una perdita di produttività. In caso di un rapporto di mancato recapito, questo scenario può portare ad una costosa chiamata al centro di supporto.

Vi sono altresì numerosi scenari in cui l'invio di un messaggio non provocherà un errore, ma potrebbe avere conseguenze indesiderate, se non addirittura imbarazzanti:

  - Messaggi inviati a gruppi di distribuzione estremamente numerosi.

  - Messaggi inviati a gruppi di distribuzione non appropriati.

  - Messaggi inavvertitamente inviati a destinatari esterni all'organizzazione.

  - Utilizzo della funzione **Rispondi a tutti** per un messaggio ricevuto come destinatario Ccn.

Tutti questi potenziali problemi possono essere mitigati se si informano gli utenti del possibile risultato dell'invio già mentre stanno componendo il messaggio. Ad esempio, se i mittenti vengono informati che la dimensione del messaggio che stanno cercando di inviare supera il criterio aziendale, non tenteranno di inviarlo. Allo stesso modo, se i mittenti vengono informati del fatto che il messaggio che stanno cercando di inviare verrà recapitato anche a persone esterne all'organizzazione, è probabile che verificheranno che il contenuto e il tono del messaggio siano appropriati.

I seguenti client di messaggistica supportano i suggerimenti messaggio:

  - Outlook Web App

  - Microsoft Outlook 2010 o versioni successive

## Suggerimenti messaggio in Exchange

Nella tabella di seguito sono elencati i Suggerimenti messaggio disponibili in Exchange 2013.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Avviso messaggio</th>
<th>Disponibilità</th>
<th>Scenario</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Destinatario interno non valido</p></td>
<td><p>Outlook</p></td>
<td><p>Il suggerimento Destinatario interno non valido viene visualizzato se il mittente aggiunge un destinatario che sembra essere interno all'organizzazione ma non esiste.</p>
<p>Questo problema può verificarsi se il mittente indirizza un messaggio a un utente che non fa più parte dell'azienda, ma il cui indirizzo si risolve con la cache risoluzione nomi o una voce nella cartella Contatti del mittente. Può inoltre verificarsi se il mittente digita un indirizzo SMTP con un dominio per cui Exchange è autorevole e l'indirizzo non viene risolto in un destinatario esistente.</p>
<p>Il suggerimento indica il destinatario non valido e consente al mittente di rimuoverlo dal messaggio.</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale piena</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>Il suggerimento Cassetta postale piena viene visualizzato se il mittente aggiunge un destinatario la cui cassetta postale è piena e l'organizzazione ha implementato una limitazione di ricevimento proibito nel caso le cassette postali superino una certa dimensione.</p>
<p>Il suggerimento indica il destinatario la cui cassetta postale è piena e consente al mittente di rimuoverlo dal messaggio.</p>
<p>Il suggerimento è accurato al momento della visualizzazione. Se il messaggio non viene inviato immediatamente, l'avviso messaggio viene aggiornato ogni due ore. Ciò vale per i messaggi inviati nella cartella Bozze e riaperti dopo due ore.</p></td>
</tr>
<tr class="odd">
<td><p>Risposte automatiche</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>L'avviso messaggio Risposte automatiche viene visualizzato se il mittente aggiunge un destinatario che ha attivato la funzionalità Risposte automatiche.</p>
<p>Il suggerimento indica il destinatario ha attivato la funzionalità risposte automatiche e vengono inoltre visualizzati i primi 175 caratteri della risposta automatica configurata dal destinatario.</p>
<p>Il suggerimento è accurato al momento della visualizzazione. Se il messaggio non viene inviato immediatamente, l'avviso messaggio viene aggiornato ogni due ore. Ciò vale per i messaggi inviati nella cartella Bozze e riaperti dopo due ore.</p>
<p>Se parte delle cassette postali utente sono ospitate in Exchange Online ed è presente una coesistenza con lo scenario di Exchange Online, l'impostazione sull'oggetto dominio remoto che rappresenta la parte remota dell'organizzazione influisce direttamente sulla modalità di elaborazione di questo avviso messaggio.</p>
<p>In Exchange 2013, gli utenti possono configurare risposte automatiche differenti per mittenti interni ed esterni. Se il dominio remoto è configurato come un dominio interno (mediante l'impostazione del parametro <em>IsInternal</em> sull'oggetto dominio remoto su <code>$true</code>), la risposta automatica interna viene restituita a tutti gli utenti dell'organizzazione indipendentemente dal punto in cui risiede la relativa cassetta postale. Tuttavia, se il dominio remoto non è configurato come un dominio interno, la risposta automatica interna viene restituita a tutti gli utenti le cui cassette postali si trovano nel dominio locale e la risposta automatica esterna viene restituita agli utenti le cui cassette postali si trovano nel dominio remoto.</p></td>
</tr>
<tr class="even">
<td><p>Personalizzato</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>Un suggerimento personalizzato viene visualizzato se il mittente aggiunte un destinatario è per cui è stato configurato un suggerimento personalizzato.</p>
<p>Un suggerimento personalizzato può essere utile perché fornisce informazioni specifiche su un destinatario. Ad esempio, è possibile creare un suggerimento personalizzato per un gruppo di distribuzione in cui viene spiegato il suo obiettivo, così da ridurne l'errato utilizzo. Per ulteriori informazioni, vedere <a href="configure-custom-mailtips-for-recipients-exchange-2013-help.md">Configurazione di Suggerimenti messaggio personalizzati per i destinatari</a>.</p>
<p>Per impostazione predefinita, i suggerimenti personalizzati non vengono visualizzati se al mittente non è consentito inviare messaggi a quel destinatario. In tal caso, viene visualizzato il suggerimento Destinatario con limitazioni. Tuttavia, è possibile modificare questa configurazione e far comparire il suggerimento personalizzato.</p></td>
</tr>
<tr class="odd">
<td><p>Destinatario con limitazioni</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>Il suggerimento Destinatario con limitazioni viene visualizzato se il mittente aggiunge un destinatario per cui sono configurare delle limitazioni di recapito che non consentono a questo mittente di inviare messaggi.</p>
<p>Il suggerimento indica il destinatario a cui il mittente non può inviare messaggi e consente al mittente di rimuoverlo dal messaggio. Inoltre, informa chiaramente il mittente che il messaggio, se inviato, non verrà recapitato.</p>
<p>Se il destinatario con limitazioni è esterno o se si tratta di un gruppo di distribuzione che contiene destinatari esterni, questa informazione viene fornita anche al mittente. Tuttavia, i seguenti suggerimenti, se applicabile, vengono soppressi:</p>
<ul>
<li><p>Risposte automatiche</p></li>
<li><p>Cassetta postale piena</p></li>
<li><p>Suggerimento personalizzato</p></li>
<li><p>Destinatario moderato</p></li>
<li><p>Messaggio troppo grande</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Destinatari esterni</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>Il suggerimento Destinatari esterni viene visualizzato se il mittente aggiunge un destinatario esterno o un gruppo di distribuzione che contiene destinatari esterni.</p>
<p>Questo suggerimento informa il mittente che il messaggio che sta componendo verrà inviato al di fuori dell'organizzazione in modo che possa scegliere oculatamente contenuto, parole e tono da utilizzare.</p>
<p>Per impostazione predefinita, questo suggerimento è disattivato. È possibile attivarlo utilizzando il cmdlet <strong>Set-OrganizationConfig</strong>. Per ulteriori informazioni, vedere <a href="mailtips-over-organization-relationships-exchange-2013-help.md">Suggerimenti messaggio tramite le relazioni dell'organizzazione</a>.</p>
<p>Se parte delle cassette postali utente sono ospitate in Exchange Online ed è presente una coesistenza con lo scenario di Exchange Online, l'impostazione sull'oggetto dominio remoto che rappresenta la parte remota dell'organizzazione influisce direttamente sulla modalità di elaborazione di questo avviso messaggio.</p>
<p>Se il dominio remoto è configurato come un dominio interno (mediante l'impostazione del parametro <em>IsInternal</em> sull'oggetto dominio remoto su <code>$true</code>), tutti i destinatari in questo dominio remoto verranno considerati come interni e, pertanto, l'avviso messaggio Destinatari esterni non verrà visualizzato. Tuttavia, se il dominio remoto non è configurato come un dominio interno, i destinatari in quel dominio verranno considerati esterni e questo avviso messaggio verrà visualizzato quando viene composto un messaggio per quei destinatari.</p>

> [!NOTE]
> Tale avviso messaggio non viene preso in considerazione durante la composizione di un messaggio per un gruppo di distribuzione nel dominio remoto.


</td>
</tr>
<tr class="odd">
<td><p>Pubblico esteso</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>Il suggerimento Pubblico esteso viene visualizzato se il mittente aggiunge un gruppo di distribuzione i cui membri superino il valore di 'pubblico esteso' definito dall'organizzazione. Per impostazione predefinita, Exchange visualizza questo avviso messaggio per i messaggi inviati a gruppi di distribuzione con più di 25 membri. Per dettagli, vedere <a href="configure-the-large-audience-size-for-your-organization-exchange-2013-help.md">Configurare le dimensioni di grandi dimensioni gruppo di destinatari per l'organizzazione</a>.</p>
<p>La dimensione dei gruppi di distribuzione non viene calcolata ogni volta. Al contrario, le informazioni sul gruppo di distribuzione vengono ricavate dai dati della metrica di gruppo.</p></td>
</tr>
<tr class="even">
<td><p>Destinatario moderato</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>Il suggerimento Destinatario moderato viene visualizzato se il mittente aggiunge un destinatario soggetto moderazione.</p>
<p>Il suggerimento indica quale destinatario è soggetto a moderazione e informa il mittente che questa situazione potrebbe ritardare il recapito del messaggio.</p>
<p>Se il mittente è anche il moderatore, questo suggerimento non viene visualizzato. Allo stesso modo, non viene visualizzato se al mittente è stato esplicitamente consentito di inviare messaggi a quel destinatario (cioè, il nome del mittente è stato incluso nell'elenco del destinatario 'Accetta messaggi solo da').</p>
<p>Per istruzioni su come configurare i destinatari con moderatore Exchange 2013, vedere <a href="common-message-approval-scenarios-exchange-2013-help.md">Scenari comuni di approvazione messaggio</a>.</p>
<p>Per istruzioni su come configurare i destinatari con moderatore Exchange Online, vedere <a href="https://technet.microsoft.com/it-it/library/jj983442(v=exchg.150)">Configurazione di un destinatario moderato in Exchange Online</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Rispondi a tutti in Ccn</p></td>
<td><p>Outlook Web App</p></td>
<td><p>Il suggerimento Rispondi a tutti in Ccn viene visualizzato se il mittente riceve in Ccn a copia del messaggio e seleziona <strong>Rispondi a tutti</strong>.</p>
<p>Quando un utente seleziona <strong>Rispondi a tutti</strong> a un messaggio di questo tipo, il fatto che l'utente abbia ricevuto una copia Ccn del messaggio è reso noto agli altri destinatari del messaggio. Nella maggior parte dei casi, questa situazione non è auspicabile e il suggerimento ne informa l'utente.</p></td>
</tr>
<tr class="even">
<td><p>Messaggio troppo grande</p></td>
<td><p>Outlook</p></td>
<td><p>Il suggerimento Messaggio troppo grande viene visualizzato se il messaggio che il mittente sta componendo supera la dimensione massima per i messaggi configurata dall'organizzazione.</p>
<p>Il suggerimento viene visualizzato se la dimensione del messaggio viola una delle seguenti limitazioni:</p>
<ul>
<li><p>Impostazione della dimensione massima di invio sulla cassetta postale del mittente</p></li>
<li><p>Impostazione della dimensione massima di ricezione sulla cassetta postale del destinatario</p></li>
<li><p>Restrizione della dimensione massima dei messaggi per l'organizzazione</p></li>
</ul>

> [!NOTE]
> A causa della complessità dell'implementazione, i limiti per la dimensione dei messaggi sui connettori nell'organizzazione non vengono considerati.


</td>
</tr>
</tbody>
</table>


## Restrizioni dell'avviso messaggio

Gli avvisi messaggio sono soggetti alle seguenti restrizioni:

  - I Suggerimenti messaggio non sono supportati quando si lavora nella modalità offline di Outlook.

  - Quando un messaggio è indirizzato a un gruppo di distribuzione, i suggerimenti per i singoli destinatari che sono membri del gruppo di destinazione non vengono esaminati. Tuttavia, se nel gruppo vi sono destinatari esterni, viene visualizzato il suggerimento Destinatari esterni che indica al mittente il numero di destinatari esterni presenti nel gruppo.

  - Se il messaggio è indirizzato a più di 200 destinatari, i suggerimenti per le singole cassette postali non vengono esaminati per non creare problemi a livello di prestazioni.

  - I suggerimenti personalizzati sono superare i 175 caratteri.

  - Mentre Exchange 2010 sarebbe popolare i suggerimenti interamente, verranno visualizzate solo Exchange 2013 fino a 1000 caratteri.

  - Se il mittente inizia a comporre un messaggio e lo lascia aperto per un certo periodo di tempo, gli avvisi messaggio Risposte automatiche e Cassetta postale piena verranno esaminati ogni due ore.


---
title: 'Tag di conservazione e criteri di conservazione: Exchange 2013 Help'
TOCTitle: Tag di conservazione e criteri di conservazione
ms:assetid: 48c13be5-3f01-4849-a089-766210e54f89
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd297955(v=EXCHG.150)
ms:contentKeyID: 50480581
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Tag di conservazione e criteri di conservazione

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

In Microsoft Exchange Server 2013 e Exchange Online, la funzione Gestione record di messaggistica permette alle organizzazioni di gestire il ciclo di vita dei messaggi di posta elettronica e ridurre i rischi legali associati alla posta elettronica e ad altre forme di comunicazione. Con Gestione record di messaggistica diventa più facile conservare i messaggi necessari per soddisfare criteri aziendali, normative o esigenze legali così come rimuovere i contenuti che non hanno alcun valore legale o aziendale.

Guardare questo [video](http://go.microsoft.com/fwlink/?linkid=825854) per una rapida panoramica di come applicare i tag di conservazione e criteri di conservazione a una cassetta postale in Exchange Online.

Stai cercando le procedure dettagliate per la gestione MRM? Vedere [Messaggistica Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

**Sommario**

Strategia di gestione dei record di messaggistica

Retention tags

Retention policies

Managed Folder Assistant

Retention hold

## Strategia di Gestione record di messaggistica

Per gestire i record di messaggistica in Exchange 2013 e Exchange Online si utilizzano i *tag di conservazione* e i *criteri di conservazione*. Prima di illustrare in dettaglio queste funzionalità di conservazione, è importante comprendere in che modo vengono utilizzate nella strategia globale di gestione dei record di messaggistica. Questa strategia si basa su:

  - Assegnazione dei *tag del criterio di conservazione* alle cartelle predefinite, come Posta eliminata.

  - Applicazione dei *tag dei criteri predefiniti* (DTP) alle cassette postali per gestire la conservazione di tutti gli elementi senza tag.

  - Assegnazione dei *tag personali* da parte dell'utente alle cartelle personalizzate e ai singoli elementi.

  - Separazione della funzionalità MRM dalla gestione della Posta in arrivo degli utenti e dalle abitudini di archiviazione. Non è necessario che gli utenti archivino i messaggi nelle cartelle gestite in base ai requisiti di conservazione. I singoli messaggi possono disporre di un tag di conservazione diverso da quello applicato alla cartella in cui si trovano.

Nella figura seguente vengono illustrate le attività coinvolte nell'implementazione di questa strategia.

![Uso dei criteri di conservazione per la conservazione dei messaggi](images/Dd297955.429b51d5-51b8-4816-b8a4-221e0915d0c0(EXCHG.150).gif "Uso dei criteri di conservazione per la conservazione dei messaggi")

Inizio pagina

## Tag di conservazione

Come illustrato nella figura precedente, i tag di conservazione vengono utilizzati per applicare le impostazioni di conservazione alle cartelle e ai singoli elementi, come i messaggi vocali e di posta elettronica. Queste impostazioni specificano per quanto tempo un messaggio rimane in una cassetta postale e le operazioni da eseguire quando il messaggio raggiunge il periodo specificato di validità della conservazione. Quando un messaggio raggiunge la fine del suo periodo di conservazione, viene spostato nella cassetta postale locale di archiviazione dell'utente oppure viene eliminato.

![Impostazioni in un tag di conservazione](images/Dd297955.936edd6a-8bc4-4c03-94a3-c240ffe7dd6a(EXCHG.150).png "Impostazioni in un tag di conservazione")

I tag di conservazione consentono agli utenti di contrassegnare i propri cartelle delle cassette postali e ai singoli elementi di conservazione. Gli utenti non è più necessario elementi file in cartelle gestite a provisioning da un amministratore in base ai requisiti di conservazione di messaggio.

## Tipi di tag di conservazione

I tag di conservazione sono classificati in tre seguenti tipi di base che è possibile applicarli e dove in una cassetta postale possono essere applicati.


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
<th>Tipo di tag di conservazione</th>
<th>Applied...</th>
<th>Applicati dal...</th>
<th>Azioni disponibili...</th>
<th>Dettagli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tag dei criteri predefiniti (DPT)</p></td>
<td><p>Automaticamente per l'intera cassetta postale</p>
<p>Un DPT si applica agli elementi <em>senza tag</em> , ovvero elementi delle cassette postali che non dispongono di un tag di conservazione applicato direttamente o ereditati dalla cartella.</p></td>
<td><p>Amministratore</p></td>
<td><ul>
<li><p>Spostamento nell'archivio</p></li>
<li><p>Elimina e consenti ripristino</p></li>
<li><p>Elimina definitivamente</p></li>
</ul></td>
<td><p>Gli utenti non possono modificare DTP applicato a una cassetta postale.</p></td>
</tr>
<tr class="even">
<td><p>Tag criterio di conservazione (TAG)</p></td>
<td><p>Automaticamente in una cartella predefinita</p>
<p>Cartelle predefinite sono cartelle create automaticamente in tutte le cassette postali, ad esempio: <strong>posta in arrivo</strong>, <strong>Posta eliminata</strong> e <strong>Posta inviata</strong>. Vedere l'elenco delle cartelle predefinite supportate in <a href="default-folders-that-support-retention-policy-tags-exchange-2013-help.md">Cartelle predefinite che supportano i tag del criterio di conservazione</a>.</p></td>
<td><p>Amministratore</p></td>
<td><ul>
<li><p>Elimina e consenti ripristino</p></li>
<li><p>Elimina definitivamente</p></li>
</ul></td>
<td><p>Gli utenti non possono modificare i TAG applicati a una cartella predefinita.</p></td>
</tr>
<tr class="odd">
<td><p>Tag personale</p></td>
<td><p>Manualmente a elementi e cartelle</p>
<p>Gli utenti possono automatizzare tagging utilizzando regole posta in arrivo a spostare in un messaggio in una cartella che dispone di un tag specifico o per applicare un tag personale a del messaggio.</p></td>
<td><p>Utenti</p></td>
<td><ul>
<li><p>Spostamento nell'archivio</p></li>
<li><p>Elimina e consenti ripristino</p></li>
<li><p>Elimina definitivamente</p></li>
</ul></td>
<td><p>Tag personali consentono agli utenti di determinare quanto tempo deve essere un elemento mantenuti. Ad esempio, la cassetta postale può avere un tag di criteri predefinito per eliminare gli elementi nel sette anni, ma un utente può creare un'eccezione per gli elementi, ad esempio newsletter e notifiche automatizzate per l'applicazione di un tag personale per eliminarli in tre giorni.</p></td>
</tr>
</tbody>
</table>


## Per ulteriori informazioni sui tag personali

Tag personali sono disponibili per gli utenti Outlook 2010 e Outlook Web App come parte del loro criterio di conservazione. In Outlook 2010 e Outlook Web App, i tag personali con l'azione **Sposta nell'archivio** visualizzati come **Criteri di archiviazione** e i tag personali con **Elimina e Consenti ripristino** o **Elimina definitivamente** azioni vengono visualizzate come **Criterio di conservazione**, come illustrato nella figura riportata di seguito.

![Tag personali in Outlook 2010 e Outlook Web App](images/Dd297955.2dbaee13-fdd0-4c30-b821-e662ce2587bb(EXCHG.150).gif "Tag personali in Outlook 2010 e Outlook Web App")

Gli utenti possono applicare i tag personali per le cartelle creati o per singoli elementi. Messaggi il cui applicato un tag personale vengono sempre elaborati dipende dalle impostazioni dei tag personali. Gli utenti possono applicare un tag personale a un messaggio in modo che è spostato o eliminato prima o poi che le impostazioni specificate nel DPT o i tag rpt applicato alla cassetta postale dell'utente. È inoltre possibile creare i tag personali alla conservazione disabilitato. Ciò consente agli utenti di contrassegnare gli articoli in modo che non è mai spostati in un archivio o Nessuna scadenza.


> [!NOTE]
> I criteri di archiviazione possono essere applicati a cartelle predefinite, cartelle o sottocartelle create dagli utenti e singoli elementi. I criteri di conservazione possono essere applicati a cartelle o sottocartelle create dagli utenti e a singoli elementi (inclusi elementi e sottocartelle in una cartella predefinita), ma non alle cartelle predefinite.



Gli utenti possono anche utilizzare l'interfaccia di amministrazione di Exchange per selezionare altri tag personali non associati ad alcun criterio di conservazione. I tag selezionati diventano così disponibili in Outlook 2010 e Outlook Web App. Per consentire agli utenti di selezionare ulteriori tag dall'interfaccia di amministrazione di Exchange, è necessario aggiungere [Ruolo MyRetentionPolicies](myretentionpolicies-role-exchange-2013-help.md) ai criteri di assegnazione dei ruoli. Per ulteriori informazioni sui criteri di assegnazione dei ruoli per gli utenti, vedere [Informazioni sui criteri di assegnazione di ruolo di gestione](understanding-management-role-assignment-policies-exchange-2013-help.md). Se si consente agli utenti di selezionare ulteriori tag personali, tutti i tag personali presenti nell'organizzazione Exchange risulteranno disponibili.


> [!NOTE]
> I tag personali sono una funzionalità avanzata. Le cassette postali con criteri che contengono questi tag (o quelle risultanti dall'aggiunta di questi tag da parte degli utenti) richiedono una licenza CAL Exchange Enterprise.



Inizio pagina

## Periodo di conservazione

Quando si abilita un tag di conservazione, è necessario specificare un periodo di validità della conservazione per il tag. Questo periodo di validità indica il numero di giorni in cui un messaggio viene conservato una volta arrivato nella cassetta postale dell'utente.

Il periodo di validità della conservazione per gli elementi non ricorrenti (ad esempio, i messaggi di posta elettronica) viene calcolato in modo diverso rispetto agli elementi che dispongono di una data di fine o agli elementi ricorrenti (ad esempio, le riunioni e le attività). Per informazioni sul calcolo del periodo di validità della conservazione per i diversi tipi di elementi, vedere [Calcolo del periodo di conservazione](how-retention-age-is-calculated-exchange-2013-help.md).

È inoltre possibile creare i tag di conservazione con conservazione disabilitata o disattivare i tag dopo che vengono creati. Dal momento che i messaggi che contengono un tag disabilitato applicato non vengono elaborati, viene eseguita alcuna azione di conservazione. Di conseguenza, gli utenti possono utilizzare un tag personale disabilitato come un tag **Mai spostare** o **Eliminare mai** di ignorare un DPT o TAG che verrebbero altrimenti si applicano a del messaggio.

## Azioni di conservazione

Durante la creazione o la configurazione di un tag di conservazione, è possibile selezionare una delle seguenti azioni di conservazione a da eseguire quando un elemento raggiunge il periodo di conservazione:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Azione di conservazione</th>
<th>Azione eseguita...</th>
<th>Ad eccezione di...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Sposta nell'archivio</strong> 1</p></td>
<td><ul>
<li><p>Sposta il messaggio nella cassetta postale di archivio dell'utente</p></li>
<li><p>Sono disponibili solo per DTP e i tag personali</p></li>
</ul>
<p>Per ulteriori informazioni sull'archiviazione, vedere:</p>
<ul>
<li><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">Archiviazione sul posto di Exchange 2013</a></p></li>
<li><p><a href="https://technet.microsoft.com/it-it/library/dn922147(v=exchg.150)">Cassette postali di archiviazione in Exchange Online</a></p></li>
</ul></td>
<td><ul>
<li><p>Se l'utente non dispone di una cassetta postale di archivio, viene eseguita alcuna azione.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Elimina e Consenti ripristino</strong></p></td>
<td><ul>
<li><p>Emula il comportamento quando l'utente Svuota la cartella Posta eliminata.</p></li>
<li><p>Gli elementi vengono spostati <a href="recoverable-items-folder-exchange-2013-help.md">Cartella Elementi ripristinabili</a> nella cassetta postale e mantenuti finché il periodo di <em>mantenimento degli elementi eliminati</em> .</p></li>
<li><p>Consente all'utente un'altra possibilità di ripristinare l'elemento utilizzando la finestra di dialogo <strong>Recupera elementi eliminati</strong> casella Outlook o Outlook Web App</p></li>
</ul></td>
<td><ul>
<li><p>Se il periodo di mantenimento elementi eliminati è impostato su zero giorni, gli elementi vengono eliminati definitivamente. Per ulteriori informazioni, vedere <a href="https://technet.microsoft.com/it-it/library/dn163584(v=exchg.150)">Vengono conservati gli elementi eliminato in modo permanente il tempo di modifica per una cassetta postale di Exchange Online</a>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Eliminazione definitiva</strong></p></td>
<td><ul>
<li><p>Consente di eliminare definitivamente i messaggi.</p></li>
<li><p>È possibile recuperare i messaggi dopo vengono eliminati in modo definitivo.</p></li>
</ul></td>
<td><ul>
<li><p>Se cassetta postale si trova in <a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Archiviazione sul posto e conservazione per controversia legale</a> o conservazione per controversia legale, gli elementi vengono mantenuti nella cartella elementi ripristinabili in base ai parametri esenzione. <a href="in-place-ediscovery-exchange-2013-help.md">eDiscovery sul posto</a> continuerà a restituire questi elementi nei risultati della ricerca.</p>
<p></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Segna come ultimi limite di conservazione</strong></p></td>
<td><ul>
<li><p>Contrassegna un messaggio come scaduto. In Outlook 2010 o versioni successive e Outlook Web App, gli elementi scaduti vengono visualizzati con la notifica che indica 'in questo articolo è scaduto' e &quot;elemento scadrà 0 giorni&quot;. In Outlook 2007, gli elementi contrassegnati come scaduti vengono visualizzati con testo barrato.</p></li>
</ul></td>
<td><p>N. D.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1 in una distribuzione ibrida Exchange, è possibile abilitare una cassetta postale di archiviazione basate su cloud per una cassetta postale principale in locale. Se si assegna un criterio di archiviazione in una cassetta postale locale, vengono spostati gli elementi nell'archivio basato su cloud. Se un elemento viene spostato la cassetta postale di archiviazione, una copia non viene mantenuta nella cassetta postale locale. Se la cassetta postale locale viene messa in attesa, criteri di archiviazione verranno comunque di spostare gli elementi di cassetta postale di archiviazione basate su cloud dove vengono conservate per la durata specificata per la sospensione.



Per i dettagli sulla creazione dei tag di conservazione, vedere [Creare un criterio di conservazione](create-a-retention-policy-exchange-2013-help.md).

Inizio pagina

## Criteri di conservazione

Per applicare uno o più tag di conservazione a una cassetta postale, è necessario aggiungerli a un criterio di conservazione, quindi applicare il criterio alle cassette postali. Una cassetta postale non può avere più criteri di conservazione. I tag di conservazione possono essere collegati o scollegati da un criterio di conservazione in qualsiasi momento e le modifiche diventano automaticamente effettive per tutte le cassette postali a cui è applicato il criterio.

Un criterio di conservazione può avere i seguenti tag di conservazione:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di tag di conservazione</th>
<th>Tag di un criterio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tag dei criteri predefiniti (DPT)</p></td>
<td><ul>
<li><p>Un tag DPT con l'azione <strong>Sposta nell'archivio</strong></p></li>
<li><p>Un tag DPT con l'azione <strong>Elimina e consenti ripristino</strong> o <strong>Elimina definitivamente</strong></p></li>
<li><p>Un tag DPT per messaggi vocali con l'azione <strong>Elimina e Consenti ripristino</strong> o <strong>Elimina definitivamente</strong></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Tag dei criteri di conservazione (RPT)</p></td>
<td><ul>
<li><p>Un tag dei criteri di conservazione per ogni cartella predefinita supportata</p>

> [!NOTE]
> Non è possibile collegare più di un tag del criterio di conservazione per una determinata cartella predefinita (come <STRONG>Elementi eliminati</STRONG>) a uno stesso criterio di conservazione.


</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Tag personali</p></td>
<td><ul>
<li><p>Qualsiasi numero di tag personali</p></li>
</ul>

> [!TIP]
> Tag personali molti in un criterio può confondere gli utenti. È consigliabile aggiungere non più di 10 tag personale a criteri di conservazione.


</td>
</tr>
</tbody>
</table>



> [!NOTE]
> Anche se un criterio di conservazione non deve avere alcun tag di conservazione collegato, si consiglia di non utilizzare questo scenario. Se alle cassette postali con criteri di conservazione non è collegato alcun tag di conservazione, gli elementi delle cassette postali potrebbero non scadere mai.



Un criterio di conservazione può contenere tag di archiviazione (tag che spostano gli elementi nella cassetta postale di archiviazione personale) e tag di eliminazione (tag che eliminano gli elementi). A un elemento della cassetta postale possono anche essere applicati entrambi i tipi di tag. Le cassette postali di archiviazione non dispongono di un altro criterio di conservazione. Lo stesso criterio di conservazione viene applicato alla cassetta postale principale e di archiviazione.

Quando si pianifica la creazione dei criteri di conservazione, è necessario considerare se comprenderanno sia i tag di archiviazione che di eliminazione. Come accennato in precedenza, un criterio di conservazione può disporre di un tag DPT che utilizza l'azione **Sposta nell'archivio** e di un tag DPT che utilizza l'azione **Elimina e consenti ripristino** o **Elimina definitivamente**. Il tag DPT con l'azione **Sposta nell'archivio** deve disporre di un periodo di validità della conservazione inferiore rispetto al tag DPT con un'azione di eliminazione. Ad esempio, è possibile utilizzare un tag DPT con l'azione **Sposta nell'archivio** per spostare gli elementi nella cassetta postale di archiviazione entro due anni e un tag DPT con un'azione di eliminazione per rimuovere gli elementi dalla cassetta postale entro sette anni. Gli elementi nelle cassette postali primaria e di archiviazione verranno eliminati dopo sette anni.

Per un elenco delle attività di gestione relative ai criteri di conservazione, vedere [Messaggistica Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

## Criterio di conservazione predefinito

Exchange Programma di installazione creato il criterio di conservazione **Criterio MRM predefinito**. Criterio MRM predefinito verrà applicato automaticamente nuove cassette postali di Exchange Online. In Exchange Server, i criteri vengono applicati automaticamente se si crea un archivio per il nuovo utente e non viene specificato un criterio di conservazione

È possibile modificare tag inclusi nel criterio MRM predefinito, ad esempio modificando il periodo di conservazione o l'azione di conservazione, disabilitare un tag o modificare i criteri mediante l'aggiunta o rimozione di tag da esso. Per le cassette postali viene applicato il criterio aggiornato alla successiva che essere state elaborate dall'Assistente cartelle gestite.

Per informazioni dettagliate, incluso un elenco dei tag di conservazione collegati al criterio, vedere [Criterio di conservazione predefinito in Exchange Online ed Exchange Server](default-retention-policy-in-exchange-online-and-exchange-server-exchange-2013-help.md).

Inizio pagina

## Assistente cartelle gestite

L'Assistente cartelle gestite, un'assistente delle cassette postali eseguito sui server Cassette postali, elabora le cassette postali a cui è applicato un criterio di conservazione.

L'assistente cartelle gestite applica il criterio di conservazione esaminando gli elementi della cassetta postale e determinando se sono soggetti alla conservazione. Quindi, timbra gli elementi soggetti alla conservazione con i tag appropriati ed esegue l'azione di conservazione specificata sugli elementi che hanno superato il periodo di validità.

Assistente cartelle gestite è un assistente basato sulle limitazioni. Gli assistenti basati sulla limitazione sono sempre in esecuzione e non è necessario programmarli. Le risorse del sistema che consumano sono limitate. È possibile configurare l'Assistente cartelle gestite per elaborare tutte le cassette postali su un server Cassette postali entro un certo periodo di tempo (noto come *ciclo di lavoro*). Inoltre, a un intervallo specificato (noto come *checkpoint del ciclo di lavoro*), l'assistente aggiorna l'elenco delle cassette postali da elaborare. Durante l'aggiornamento, l'assistente aggiunge le cassette postali recentemente create o spostate nella coda. Inoltre, assegna di nuovo la priorità alle cassette postali esistenti non elaborate in modo corretto a causa di errori e le sposta nella parte superiore della coda in modo che possano essere elaborate durante lo stesso ciclo di lavoro.

Per attivare manualmente l'assistente ed elaborare una cassetta postale specificata, è possibile utilizzare anche il cmdlet [Start-ManagedFolderAssistant](https://technet.microsoft.com/it-it/library/aa998864\(v=exchg.150\)). Per ulteriori informazioni, vedere [Configurazione dell'Assistente cartelle gestite](configure-the-managed-folder-assistant-exchange-2013-help.md).


> [!NOTE]
> L'Assistente cartelle gestite non esegue alcuna azione sui messaggi non soggetti alla conservazione, specificati disabilitando il tag di conservazione. È possibile disabilitare un tag di conservazione anche per sospendere temporaneamente l'elaborazione degli elementi con quel tag.



## Spostamento degli elementi tra le cartelle

Un elemento della cassetta postale spostato da una cartella a un'altra eredita tutti i tag applicati alla cartella in cui viene spostato. Se un elemento viene spostato in una cartella a cui non è assegnato alcun tag, viene applicato il tag predefinito del criterio. Se all'elemento viene assegnato un tag in modo esplicito, questo tag ha sempre la precedenza su qualsiasi tag a livello di cartella o sul tag predefinito.

## Applicazione di un tag di conservazione a una cartella dell'archivio

Quando un utente applica un tag persona a una cartella nell'archivio, se esiste una cartella con lo stesso nome nella cassetta postale principale e con un tag differente, il tag della cartella nell'archivio cambia per rispettare il tag nella cassetta postale principale. È un'impostazione predefinita per evitare confusione sugli elementi in una cartella nell'archivio con un comportamento di scadenza diverso da quello della stessa cartella nella cassetta postale principale dell'utente. Ad esempio, l'utente con una cartella chiamata Project Contoso nella cassetta postale principale con un tag *Elimina – 3 anni* e la cartella Project Contoso esiste anche nella cassetta postale di archiviazione. Se l'utente applica un tag personale *Elimina – 1 anno* per eliminare gli elementi nella cartella dopo un anno, quando la cassetta postale viene nuovamente elaborata, la cartella riapplica il tag Elimina – 3 anni.

## Rimozione o eliminazione di un tag da un criterio di conservazione

Quando un tag viene rimosso dal criterio di conservazione applicato a una cassetta postale, il tag non è più disponibile per l'utente e non può essere applicato agli elementi della cassetta postale.

Gli elementi esistenti contrassegnati con quel tag continuano a essere elaborati dall'Assistente cartelle gestite in base a quelle impostazioni e a quei messaggi viene applicata qualsiasi azione di conservazione specificata nel tag.

Tuttavia, se si elimina il tag, viene rimossa anche la definizione del tag archiviata in Active Directory. In questo modo, l'Assistente cartelle gestite elabora tutti gli elementi di una cassetta postale e contrassegna di nuovo quelli a cui è applicato il tag rimosso. A seconda del numero di cassette postali e di messaggi, questo processo può utilizzare una notevole quantità di risorse su tutti i server Cassette postali contenenti le cassette postali con i criteri di conservazione che comprendono il tag rimosso.


> [!IMPORTANT]
> Se un tag viene rimosso da un criterio di conservazione, la scadenza di tutti gli elementi esistenti della cassetta postale a cui è applicato il tag continuerà a dipendere dalle impostazioni del tag. Per evitare l'applicazione delle impostazioni del tag a tutti gli elementi, è necessario eliminare il tag. L'eliminazione di un tag lo rimuove da tutti i criteri di conservazione in cui è incluso.



## Disabilitazione di un tag di conservazione

Se si disabilita un tag di conservazione, l'Assistente cartelle gestite ignora gli elementi a cui è applicato il tag. Gli elementi che dispongono di un tag di conservazione per il quale la conservazione è disabilitata non vengono mai spostati o eliminati, in base all'azione di conservazione specificata. Siccome questi elementi non sono ancora considerati contrassegnati, il DPT non viene applicato. Ad esempio, se si desidera risolvere i problemi relativi alle impostazioni del tag di conservazione, è possibile disabilitare temporaneamente il tag per arrestare l'elaborazione dei messaggi con quel tag da parte dell'Assistente cartelle gestite.


> [!NOTE]
> Il periodo di validità della conservazione per un tag di conservazione disabilitato viene visualizzato all'utente come <STRONG>Mai</STRONG>. Se un utente contrassegna un elemento credendo di non eliminarlo mai, un'abilitazione successiva del tag può comportare un'eliminazione involontaria degli elementi che l'utente non voleva eliminare. Lo stesso vale per i tag con l'azione <STRONG>Sposta nell'archivio</STRONG>.



Inizio pagina

## Attesa di conservazione

Quando gli utenti sono temporaneamente assenti dal lavoro e non hanno accesso alla posta elettronica, è possibile applicare le impostazioni di conservazione ai nuovi messaggi prima che gli utenti tornino al lavoro o accedano alla posta elettronica. In base al criterio di conservazione, i messaggi possono essere eliminati o spostati nell'archivio personale dell'utente. È possibile sospendere l'elaborazione di una cassetta postale da parte dei criteri di conservazione per un determinato periodo di tempo posizionando la cassetta postale in attesa di conservazione. Quando si posiziona una cassetta postale in attesa di conservazione, è possibile anche specificare un commento che informa l'utente della cassetta postale (o un altro utente autorizzato ad accedere alla cassetta postale) sull'attesa di conservazione, anche quando l'attesa viene pianificata dall'inizio alla fine. I commenti di conservazione vengono visualizzati nei client Outlook supportati. Inoltre, è possibile localizzare il commento dell'attesa di conservazione nella lingua preferita dell'utente.


> [!NOTE]
> Il posizionamento di una cassetta postale in attesa di conservazione non interessa l'elaborazione delle quote di archiviazione della cassetta postale. In base all'utilizzo e alle quote della cassetta postale applicabili, tenere presente l'aumento temporaneo della quota di archiviazione per gli utenti quando sono in vacanza o non hanno accesso alla posta elettronica per un periodo prolungato. Per ulteriori informazioni sulle quote di archiviazione della cassetta postale, vedere <A href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">Configurazione delle quote di archiviazione per una cassetta postale</A>.



Durante lunghe assenze dal lavoro, gli utenti possono accumulare una grande quantità di posta elettronica. In base al volume della posta elettronica e alla durata dell'assenza, potrebbero essere necessarie diverse settimane per leggere tutti i messaggi. In questi casi, tenere presente l'ulteriore tempo necessario per recuperare la posta prima di rimuovere i messaggi dall'attesa di conservazione.

Se l'organizzazione non ha mai implementato MRM e gli utenti non hanno familiarità con le funzionalità, è possibile utilizzare la conservazione anche durante la fase iniziale di *avvio e formazione*della distribuzione di MRM. È possibile creare e distribuire i criteri di conservazione e istruire gli utenti sul loro utilizzo senza correre il rischio di spostare o eliminare gli elementi prima che gli utenti possano contrassegnarli. Qualche giorno prima, è necessario ricordare agli utenti la scadenza del periodo di avvio e di formazione. Dopo la scadenza, è possibile rimuovere la conservazione dalle cassette postali degli utenti, consentendo all'Assistente cartelle gestite di elaborare gli elementi delle cassette postali e di eseguire l'azione di conservazione specificata.

Per i dettagli sul posizionamento di una cassetta postale in attesa di conservazione, vedere [Archiviazione sul posto una cassetta postale di conservazione](place-a-mailbox-on-retention-hold-exchange-2013-help.md).

Inizio pagina


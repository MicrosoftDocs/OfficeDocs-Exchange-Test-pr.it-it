---
title: 'Cartella Elementi ripristinabili: Exchange 2013 Help'
TOCTitle: Cartella Elementi ripristinabili
ms:assetid: efc48fb4-2ed8-4d05-93af-f3505fbc389d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee364755(v=EXCHG.150)
ms:contentKeyID: 50481994
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cartella Elementi ripristinabili

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Per proteggere da eliminazioni accidentali o dolose e facilitare le azioni di individuazione comunemente intraprese prima o durante controversie o indagini, Microsoft Exchange Server 2013 e Exchange Online usano la cartella Elementi ripristinabili. La cartella Elementi ripristinabili sostituisce la funzionalità conosciuta come *dumpster* nelle versioni precedenti di Exchange. La cartella Elementi ripristinabili viene utilizzata dalle seguenti funzionalità di Exchange:

  - Mantenimento elementi eliminati

  - Ripristino di un unico elemento

  - Blocco sul posto

  - Conservazione in caso di dispute

  - Registrazione di controllo delle cassette postali

  - Registrazione del calendario

**Sommario**

Terminologia

Cartella degli elementi ripristinabili

  - Mantenimento elementi eliminati

  - Ripristino di un unico elemento

  - Blocco sul posto e blocco per controversia legale

  - Protezione delle pagine copy-on-write ed elementi modificati

Quote Elementi ripristinabili e cassette postali

## Terminologia

Conoscere il significato dei termini seguenti consente di comprendere i contenuti cui si fa riferimento in questo argomento.

  - **Elimina**  
    Descrive quando un elemento viene eliminato da una qualsiasi cartella e posto nella cartella predefinita Posta eliminata.

<!-- end list -->

  - **Elimina definitivamente**  
    Descrive quando un elemento viene eliminato da una qualsiasi cartella e posto nella cartella Elementi ripristinabili. Descrive inoltre quando un utente di Microsoft Outlook elimina un elemento premendo i tasti Maius+Canc che ignora la cartella Posta eliminata e sposta l'elemento direttamente nella cartella Elementi ripristinabili.

<!-- end list -->

  - **Eliminato**  
    Descrive quando un elemento viene contrassegnato per essere eliminato dal database delle cassette postali. Questa operazione è definita come *eliminazione definitiva dall'archivio*.

Inizio pagina

## Cartella degli elementi ripristinabili

La cartella Elementi ripristinabili risiede nella sottostruttura non IPM di ciascuna cassetta postale. La sottostruttura non IPM è un'area di archiviazione nella cassetta postale che contiene dati operativi relativi alla cassetta postale. Questa sottostruttura non è visibile agli utenti utilizzando Outlook, Microsoft OfficeOutlook Web App o altri client di posta elettronica.

Questa modifica architetturale fornisce i seguenti benefici chiave:

  - Quando una cassetta postale viene spostata in un altro database di cassette postali, anche la cartella Elementi ripristinabili viene spostata.

  - La cartella Elementi ripristinabili viene indicizzata da Exchange Search e può essere individuata utilizzando eDiscovery sul posto.

  - La cartella degli elementi ripristinabili ha una propria quota di archiviazione.

  - Exchange può prevenire la cancellazione dei dati dalla cartella Elementi ripristinabili.

  - Exchange può tenere traccia delle modifiche di alcuni contenuti.

La cartella Elementi ripristinabili contiene le seguenti sottocartelle:

  - **Eliminazione**   Questa cartella contiene tutti gli elementi eliminati dalla cartella Posta eliminata. In Outlook, un utente può eliminare definitivamente un elemento premendo MAIUSC + CANC. Questa sottocartella viene mostrata all'utente tramite la funzionalità Recupera posta eliminata in Outlook e Outlook Web App.

  - **Versioni**   In caso di attivazione del blocco sul posto o del blocco per controversia legale, questa sottocartella contiene gli elementi originali e le copie modificate di quelli eliminati. Questa cartella non è visibile all'utente finale.

  - **Eliminazioni**   In caso di attivazione del blocco per controversia legale o del ripristino del singolo elemento, questa sottocartella contiene tutti gli elementi eliminati. Questa cartella non è visibile all'utente finale.

  - **Controlli**   Se è attiva la registrazione di controllo delle cassette postali, questa sottocartella contiene le voci del log di controllo. Per ulteriori informazioni sulla registrazione di controllo delle cassette postali, vedere [Registrazione di controllo delle cassette postali](mailbox-audit-logging-exchange-2013-help.md).

  - **DiscoveryHolds**   In caso di attivazione del blocco sul posto, questa sottocartella conterrà tutti gli elementi che soddisfano i parametri query di archiviazione che saranno eliminati.

  - **Registrazione calendario**   Questa sottocartella contiene le modifiche al calendario apportate in una cassetta postale. Questa cartella non è disponibile per gli utenti.

La figura seguente mostra le sottocartelle presenti nelle cartelle Elementi ripristinabili. Mostra anche la conservazione degli elementi eliminati, il recupero di un singolo elemento e i processi di mantenimento del flusso di lavoro che vengono descritti nelle sezioni seguenti.

![Cartella degli elementi ripristinabili](images/Ee364755.a1a08afc-3617-4adb-83ab-a6904516954e(EXCHG.150).gif "Cartella degli elementi ripristinabili")

Inizio pagina

## Mantenimento elementi eliminati

Un elemento viene considerato come eliminato definitivamente nei seguenti casi:

  - Un utente elimina un elemento o svuota tutti gli elementi della cartella Posta eliminata.

  - Un utente preme Maius+Canc per eliminare un elemento da qualunque altra cartella della cassetta postale.

Gli elementi eliminati definitivamente vengono spostati nella sottocartella Eliminazione della cartella Elementi ripristinabili. Ciò fornisce un ulteriore livello di protezione che consente all'utente di ripristinare gli elementi eliminati definitivamente senza chiedere l'intervento del servizio di assistenza. Gli utenti possono utilizzare la funzionalità Recupera posta eliminata in Outlook o Outlook Web App per ripristinare un elemento eliminato. Gli utenti possono utilizzare questa funzionalità anche per eliminare definitivamente un elemento. Per ulteriori informazioni, vedere:

  - [Recuperare gli elementi eliminati in Outlook](https://go.microsoft.com/fwlink/p/?linkid=524923)

  - [Recuperare elementi o messaggi di posta elettronica eliminati in Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

Gli elementi rimangono nella sottocartella Eliminazione fino alla scadenza del periodo di conservazione. Il periodo di conservazione predefinito di un elemento eliminato è di 14 giorni. È possibile modificare questo periodo per il database delle cassette posatali o per una specifica cassetta postale. In aggiunta al periodo di conservazione degli elementi eliminati, la cartella Elementi ripristinabili è anche soggetta a quote. Per ulteriori informazioni, vedere Quote Elementi ripristinabili e cassette postali più avanti in questo argomento.

Alla scadenza del periodo di conservazione degli elementi eliminati, l'elemento viene spostato nella cartella Ripuliture e non è più visibile. Quando Assistente cartelle gestite elabora la cassetta postale, gli elementi nella cartella Ripuliture vengono eliminati dal database delle cassette postali e non è possibile ripristinarli.

Inizio pagina

## Ripristino di un unico elemento

Se un elemento vien rimosso dalla sottocartella Eliminazione, sia da un utente che elimina un elemento utilizzando la funzionalità Recupera posta eliminata che da un processo automatizzato quale Assistente cartelle gestite, l'elemento non può essere ricuperato dall'utente. Nelle precedenti versioni di Exchange, il ripristino di questi elementi richiedeva all'amministratore di ripristinare il database delle cassette postali o la cassetta postale da una copia di backup. Questo procedimento generalmente ritardava il ripristino di minuti o ore, a seconda del meccanismo di backup utilizzato.

In Exchange 2013 è possibile ricorrere al *ripristino del singolo elemento* per recuperare elementi senza dover ripristinare il database delle cassette postali utilizzando i supporti di backup. Questo produce una considerevole riduzione dei tempi di ripristino. Quando Assistente cartelle gestite elabora la cartella Elementi ripristinabili per una cassetta postale su cui è abilitato il ripristino del singolo elemento, qualsiasi elemento nella sottocartella Ripuliture non viene eliminato se non è scaduto il suo periodo di conservazione.

La tabella seguente elenca i contenuti di una azione che può essere eseguita nella cartella Elementi ripristinabili se è selezionato il ripristino del singolo elemento.

### Cartella Elementi ripristinabili e ripristino del singolo elemento

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
<th>Stato del ripristino del singolo elemento</th>
<th>La cartella Elementi ripristinabili contiene gli elementi eliminati definitivamente</th>
<th>La cartella Elementi ripristinabili contiene gli elementi eliminati</th>
<th>Gli utenti possono eliminare gli elementi dalla cartella Elementi ripristinabili</th>
<th>Assistente cartelle gestite elimina automaticamente gli elementi dalla cartella Elementi ripristinabili</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Attivato</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì. Gli utenti possono eliminare gli elementi con la funzionalità Recupero degli elementi eliminati in Outlook o Outlook Web App. Tuttavia, gli elementi eliminati non saranno cancellati definitivamente dal database della cassetta postale fino alla scadenza del periodo di conservazione previsto per l'elemento eliminato.</p></td>
<td><p>Sì. Per impostazione predefinita, tutti gli elementi vengono eliminati dopo 14 giorni, ad eccezione degli elementi di calendario che vengono eliminati dopo 31 giorni.</p></td>
</tr>
<tr class="even">
<td><p>Disabilitata</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>Sì. In questo caso, gli elementi eliminati vengono contrassegnati affinché siano rimossi definitivamente dal database della cassetta postale, senza possibilità di ripristinarli.</p></td>
<td><p>Sì. Per impostazione predefinita, tutti gli elementi vengono eliminati dopo 14 giorni, ad eccezione degli elementi di calendario che vengono eliminati dopo 31 giorni. Se viene raggiunto il limite della quota di avviso di Elementi ripristinabili prima che scada il periodo di conservazione degli elementi eliminati, gli elementi vengono eliminati nell'ordine FIFO (first in, first out).</p></td>
</tr>
</tbody>
</table>


Come impostazione predefinita, in Exchange 2013 il ripristino del singolo elemento non viene abilitato per le nuove cassette postali o per le cassette postali spostate da una precedente versione di Exchange. Si deve utilizzare Exchange Management Shell per abilitare il ripristino del singolo elemento per una cassetta posale, e quindi configurare o modificare il periodo di conservazione degli elementi eliminati. Per informazioni relative all'esecuzione del ripristino di un singolo elemento, vedere [Recuperare i messaggi eliminati nella cassetta postale dell'utente](recover-deleted-messages-in-a-user-s-mailbox-exchange-2013-help.md).

Inizio pagina

## Blocco sul posto e blocco per controversia legale

In Exchange 2013 e Exchange Online, il responsabile dell'individuazione può utilizzare eDiscovery in locale con le autorizzazioni delegate [Gestione individuazione](discovery-management-exchange-2013-help.md) per eseguire ricerche eDiscovery del contenuto della cassetta postale. In Exchange 2013 e Exchange Online è disponibile anche Blocco sul posto, utile per conservare gli elementi della cassetta postale che soddisfano i parametri di query e non consentire l'eliminazione di tali elementi da parte degli utenti o dei processi automatici. È possibile anche utilizzare il blocco per controversia legale per conservare tutti gli elementi delle cassette postali degli utenti e non consentirne l'eliminazione da parte di utenti o processi automatici.

Se per una cassetta postale si imposta lo stato Blocco sul posto o Blocco per controversia legale, si impedisce ad Assistente cartelle gestite di eliminare automaticamente i messaggi dalle sottocartelle Individuazione esenzioni e Ripuliture. Inoltre, viene anche abilitata la protezione copy-on-write delle pagine per la cassetta postale. La protezione copy-on-write delle pagine crea una copia dell'elemento originale prima che qualsiasi modifica venga scritta nell'archivio di Exchange. Dopo aver rimosso la cassetta postale dal blocco per controversia legale, Assistente cartelle gestite riprende l'eliminazione automatica.

La tabella seguente elenca i contenuti di una azione che può essere eseguita nella cartella Elementi ripristinabili se è selezionato il blocco per controversia legale.

### Cartella Elementi ripristinabili e conservazioni

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
<th>Stato del blocco</th>
<th>La cartella Elementi ripristinabili contiene gli elementi eliminati definitivamente</th>
<th>La cartella Elementi ripristinabili contiene gli elementi modificati ed eliminati</th>
<th>Gli utenti possono eliminare gli elementi dalla cartella Elementi ripristinabili</th>
<th>Assistente cartelle gestite elimina automaticamente gli elementi dalla cartella Elementi ripristinabili</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Attivato</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì. Gli utenti possono eliminare gli elementi con la funzionalità Recupero degli elementi eliminati in Outlook o Outlook Web App. Ma Assistente cartelle gestite non li rimuove definitivamente dal database della cassetta postale se quest'ultima è in stato di blocco.</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Disabilitata</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su eDiscovery in locale, blocco sul posto e blocco per controversia legale, vedere gli argomenti seguenti:

  - [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md)

  - [Archiviazione sul posto e conservazione per controversia legale](in-place-hold-and-litigation-hold-exchange-2013-help.md)

Inizio pagina

## Protezione delle pagine copy-on-write ed elementi modificati

Se l'utente con blocco sul posto o con blocco per controversia legale modifica proprietà specifiche di un elemento della cassetta postale, prima di applicare la modifica viene creata una copia dell'elemento originale. La copia originale viene salvata nella cartella Versioni. Questa procedura è nota come *protezione copy-on-write delle pagine* e viene applicata agli elementi che si trovano in qualsiasi cartella della cassetta postale. La sottocartella Versioni non è visibile agli utenti.

Nella tabella seguente sono elencate le proprietà dei messaggi che attivano la protezione delle pagine copy-on-write.

### Proprietà che attivano la protezione delle pagine copy-on-write

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di elemento</th>
<th>Proprietà che attivano la protezione delle pagine copy-on-write</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Messaggi (IPM.Note*)</p>
<p>Post (IPM.Post*)</p></td>
<td><ul>
<li><p>Argomento</p></li>
<li><p>Corpo</p></li>
<li><p>Allegati</p></li>
<li><p>Mittenti e destinatari</p></li>
<li><p>Date di invio e ricezione</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Elementi diversi da messaggi e post</p></td>
<td><p>Qualsiasi modifica apportata a una proprietà visibile, ad eccezione delle seguenti:</p>
<ul>
<li><p>Percorso dell'elemento (quando un elemento viene spostato tra le cartelle)</p></li>
<li><p>Modifica dello stato dell'elemento (letto o non letto)</p></li>
<li><p>Modifiche apportate a un tag di conservazione applicato a un elemento</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Elementi nella cartella Bozze predefinita</p></td>
<td><p>Nessuno. Agli elementi nella cartella Bozze non viene applicata la protezione delle pagine copy-on-write.</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> La protezione delle pagine copy-on-write non salva la versione di una riunione quando l'organizzatore della riunione riceve le risposte dai partecipanti e vengono aggiornate le informazioni di verifica della riunione. Inoltre, le modifiche ai feed RSS non vengono acquisite dalla protezione delle pagine copy-on-write.



Quando una cassetta postale non si trova più nello stato Blocco sul posto o Blocco per controversia legale, le copie degli elementi modificati archiviate nella cartella Versioni vengono rimosse.

Inizio pagina

## Quote Elementi ripristinabili e cassette postali

Quando un elemento viene spostato nella cartella Elementi ripristinabili, la sua dimensione viene tolta alla quota della cassetta postale ed aggiunta alla dimensione della cartella Elementi ripristinabili. In Exchange 2013 il database delle cassette postali ha una quota di avviso configurabile della cartella Elementi ripristinabili (*limite flessibile*) di 20 GB e una quota di Elementi ripristinabili (*limite rigido*) di 30 GB. Per impostazione predefinita, questi limiti vengono ereditati da tutte le cassette postali nel database. Tuttavia, è possibile configurare le cassette postali con quote diverse. Per ulteriori informazioni, vedere [Configurare il periodo di mantenimento degli elementi eliminati e delle quote di elementi ripristinabili](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md).

In Exchange Online i limiti predefiniti previsti per la quota di elementi recuperabili sono gli stessi di Exchange 2013; un limite flessibile di 20 GB e un limite di rigido di 30 GB. Le quote per la cartella Elementi ripristinabili vengono automaticamente aumentate a 90 GB e 100 GB quando per una cassetta postale si attiva il blocco per controversia legale o sul posto.

Quando la cartella Elementi ripristinabili raggiunge la quota Elementi ripristinabili, non è più possibile memorizzare altri elementi nella cartella. Questo influenza la funzionalità della cassetta postale come segue:

  - L'utente della cassetta postale non può eliminare gli elementi.

  - Assistente cartelle gestite non può eliminare elementi basandosi sul tag di conservazione o sulle impostazioni delle cartelle gestite.

  - Per le cassette postali con ripristino del singolo elemento, blocco sul posto o blocco per controversia legale abilitati, la protezione delle pagine copy-on-write non è in grado di conservare le versioni di elementi modificati dall'utente.

  - Per le cassette postali che hanno abilitato la registrazione di controllo delle cassette postali, non possono essere salvate voci del log di controllo nella sottocartella Controlli.

Nel caso delle cassette postali a cui non è applicato il blocco sul posto o il blocco per controversia legale, Assistente cartelle gestite elimina automaticamente gli elementi dalla cartella Elementi ripristinabili alla scadenza del periodo di conservazione degli elementi eliminati. Se la cartella raggiunge la quota Elementi ripristinabili, l'assistente elimina automaticamente gli elementi nell'ordine FIFO.

Quando la cartella Elementi ripristinabili raggiunge i limiti flessibili e rigidi predefiniti, si riceve una notifica mediante un registro eventi e di un avviso di Microsoft System Center Operations Manager. Questo avviso si attiva quando la cartella Elementi ripristinabili raggiunge i limiti flessibili e rigidi predefiniti, poi una volta la giorno nei giorni successivi.

La tabella che segue elenca gli eventi registrati quando la cartella Elementi ripristinabili raggiunge i limiti flessibili e rigidi predefiniti.

### Avvisi ed errori della quota Elementi ripristinabili

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ID evento</th>
<th>Tipo</th>
<th>Origine</th>
<th>Messaggio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10024</p></td>
<td><p>Avviso</p></td>
<td><p>MSExchangeIS Mailbox Store</p></td>
<td><p>La cassetta postale per &lt;<em>mailbox user</em>&gt; (<em>GUID</em>) ha superato la quota di avviso degli elementi recuperabili. Si prega di rimuovere elementi da Elementi ripristinabili o aumentare la quota di avviso degli Elementi ripristinabili o la quota Elementi ripristinabili Se si supera la quota Elementi ripristinabili, l'utente non sarà in grado di eliminare elementi dalla cassetta postale.</p></td>
</tr>
<tr class="even">
<td><p>10023</p></td>
<td><p>Errore</p></td>
<td><p>MSExchangeIS Mailbox Store</p></td>
<td><p>La cassetta postale per &lt;<em>mailbox user</em>&gt; (<em>GUID</em>) ha superato la quota massima degli elementi recuperabili. Non è possibile eliminare elementi dalla cassetta postale. Notificare al proprietario la condizione della cassetta postale al più presto possibile. Si prega di rimuovere elementi da Elementi ripristinabili o aumentare la quota Elementi ripristinabili per ripristinare la funzionalità.</p></td>
</tr>
<tr class="odd">
<td><p>10023</p></td>
<td><p>Avviso</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>Cassetta postale: &lt;<em>mailbox user</em>&gt;la dimensione di Elementi ripristinabili ha superato il limite della quota di avviso. Sono stati rimossi elementi dalla cartella Elementi ripristinabili per prevenire l'interruzione della cassetta postale. Quota di avviso di Elementi ripristinabili: 20 GB (21.474.836.480 byte) Dimensione originale di Elementi ripristinabili: 21475005311 Dimensione attuale di Elementi ripristinabili: 21474823820 Stati della cartella: - cartelle elaborate RecoverableItemsRoot, RecoverableItemsVersions, RecoverableItemsPurges, RecoverableItemsDeletions - Dimensioni originali della cartella: 21391661934, 55190914, 1987247, 26157788 (conteggio elementi: 276828, 400, 84, 646) - Dimensione attuale della cartella: 21391480443, 55190914, 1987247, 26157788 (conteggio elementi: 276817, 400, 84, 646)</p></td>
</tr>
</tbody>
</table>


Se la cassetta postale si trova in Blocco sul posto o Blocco per controversia legale, la protezione copy-on-write delle pagine non è in grado di conservare le versioni degli elementi modificati. Per mantenere le versioni degli elementi modificati è necessario ridurre le dimensioni della cartella Elementi ripristinabili. Si può utilizzare il cmdlet [Search-Mailbox](https://technet.microsoft.com/it-it/library/dd298173\(v=exchg.150\)) per copiare i messaggi dalla cartella Elementi ripristinabili di una cassetta postale a una cassetta postale di individuazione, quindi eliminare gli elementi dalla cassetta postale. In alternativa, è anche possibile aumentare la quota Elementi ripristinabili per la cassetta postale. Per ulteriori dettagli, vedere [Pulire la cartella elementi ripristinabili](clean-up-the-recoverable-items-folder-exchange-2013-help.md).

Inizio pagina

## Ulteriori informazioni

  - Copy-on-write è disponibile solo se per una cassetta postale è stato attivato il blocco sul posto oppure il blocco per controversia legale.

  - Se gli utenti devono recuperare gli elementi eliminati dalla cartella Elementi ripristinabili, suggerire loro i seguenti argomenti:
    
      - [Recuperare gli elementi eliminati in Outlook](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [Recuperare elementi o messaggi di posta elettronica eliminati in Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

Inizio pagina


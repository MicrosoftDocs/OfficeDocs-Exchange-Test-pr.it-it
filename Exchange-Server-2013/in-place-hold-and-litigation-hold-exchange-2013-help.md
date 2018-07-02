---
title: 'Archiviazione sul posto e conservazione per controversia legale: Exchange 2013 Help'
TOCTitle: Archiviazione sul posto e conservazione per controversia legale
ms:assetid: 71031c06-852d-44d8-b558-dff444eaef8c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff637980(v=EXCHG.150)
ms:contentKeyID: 50480969
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Archiviazione sul posto e conservazione per controversia legale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-11-15_


> [!NOTE]
> La scadenza per la creazione di blocchi sul posto in Exchange Online (nei piani autonomi di Office 365 e Exchange Online) è stata rimandata al 1° luglio 2017. Tuttavia, nell'ultima parte di quest'anno oppure all'inizio del prossimo, non sarà possibile creare nuovi blocchi sul posto in Exchange Online. Come alternativa al blocco sul posto, è possibile usare <A href="https://go.microsoft.com/fwlink/?linkid=780738">i casi di eDiscovery</A> oppure <A href="https://go.microsoft.com/fwlink/?linkid=827811">i criteri di conservazione</A> nel Centro sicurezza e conformità di Office 365. Una volta sospesa la creazione di nuovi blocchi sul posto, sarà possibile modificare i blocchi sul posto esistenti e creare nuovi blocchi sul posto nelle distribuzioni ibride di Exchange Server 2013 e Exchange. Inoltre, sarà ancora possibile applicare un blocco per controversia legale alle cassette postali.



In presenza di un ragionevole rischio di controversia, le organizzazioni sono tenute a conservare le informazioni in forma elettronica, inclusi i messaggi pertinenti al caso. Questa aspettativa spesso diventa realtà prima che siano note le specifiche del caso, richiedendo pertanto una conservazione ad ampio spettro. Le organizzazioni potrebbero aver bisogno di conservare tutti i messaggi di posta elettronica relativi a un determinato argomento oppure tutti i messaggi di posta elettronica di determinati individui. A seconda delle procedure di individuazione elettronica (eDiscovery) dell'organizzazione, è possibile adottare le seguenti misure per la conservazione della posta elettronica:

  - È possibile che agli utenti finali venga richiesto di non eliminare alcun messaggio per conservare la posta elettronica. Tuttavia, gli utenti possono ancora eliminare i messaggi di posta elettronica, consapevolmente o inavvertitamente.

  - È possibile che vengano sospesi i meccanismi di eliminazione automatica, ad esempio Gestione record di messaggistica (MRM). In questo modo la posta elettronica potrebbe intasare la cassetta postale dell'utente, influendo sulla sua produttività. La sospensione dell'eliminazione automatica, inoltre, non impedisce l'eliminazione manuale di messaggi di posta elettronica da parte degli utenti.

  - Alcune organizzazioni copiano o spostano la posta elettronica in un archivio per assicurarsi che non venga eliminata, modificata o manomessa. Ciò comporta un aumento dei costi dovuto al lavoro manuale richiesto per copiare o spostare i messaggi in un archivio o all'acquisto di prodotti di terze parti utilizzati per raccogliere e archiviare la posta elettronica all'esterno di Microsoft Exchange.

La mancata conservazione della posta elettronica può esporre un'organizzazione a rischi legali e finanziari, quali l'esame minuzioso dei processi conoscitivi e di conservazione dei registri dell'organizzazione, sentenze legali avverse, sanzioni o multe.

È possibile utilizzare Archiviazione sul posto o Conservazione per controversia legale per raggiungere i seguenti obiettivi:

  - Bloccare sul posto le cassette postali dell'utente e conservare in modo irreversibile gli elementi delle cassette postali.

  - Conservare gli elementi delle cassette postali eliminati dagli utenti o da processi di eliminazione automatica, come Gestione record di messaggistica.

  - Utilizzo della conservazione in locale basata su query per la ricerca e la conservazione degli elementi corrispondenti ai criteri specificati.

  - Conservare elementi a tempo indeterminato o per un determinato periodo di tempo.

  - Attribuire a un utente più conservazioni per casi o indagini differenti.

  - Mantenere trasparenti le archiviazioni dell'utente, non dovendo sospendere Gestione record di messaggistica.

  - Abilitare le ricerche di eDiscovery sul posto degli elementi conservati.

**Sommario**

Scenari relativi a Conservazione in locale

Archiviazione sul posto e conservazione per controversia legale

Conservazione in locale di una cassetta postale

Applicare un blocco alle cartelle pubbliche

Cartella Archiviazioni ed elementi ripristinabili

Blocchi e quota della cassetta postale

Archiviazioni e inoltro della posta elettronica

Conservazione del contenuto Lync archiviato

Eliminazione di una cassetta postale bloccata

Migrazione delle cassette postali bloccate da Exchange 2013 a Office 365

## Scenari relativi a Conservazione in locale

In Exchange Server 2010, la nozione di conservazione legale equivale a conservare tutti i dati di una cassetta postale per un utente a tempo indeterminato o fino a quando non viene rimossa la conservazione. In Exchange 2013, Conservazione in locale introduce un nuovo modello che consente di specificare i seguenti parametri:

  - **Cosa conservare**   È possibile specificare quali elementi conservare utilizzando parametri di query, quali parole chiave, mittenti e destinatari, date di inizio e di fine, nonché specificare i tipi di messaggio, quali messaggi di posta elettronica, elementi del calendario e così via, che si desidera conservare.

  - **Durata della conservazione**   È possibile specificare una durata per la conservazione degli elementi.

Grazie all'uso di questo nuovo modello, Conservazione in locale consente di creare criteri di conservazione granulari per conservare elementi della cassetta postale nei seguenti scenari:

  - **Conservazione indefinita**   Lo scenario relativo alla conservazione indefinita è uguale a quello della conservazione per controversia legale. Ha lo scopo di conservare gli elementi della cassetta postale affinché l'utente possa soddisfare i requisiti di eDiscovery. Durante il periodo della controversia o dell'indagine, gli elementi non vengono mai eliminati. La durata non si conosce in anticipo e, pertanto, non viene configurata alcuna data di fine. Per conservare tutti gli elementi a tempo indeterminato, è necessario evitare di specificare qualsiasi parametro query o periodo di tempo al momento della creazione di un'archiviazione sul posto.

  - **Conservazione basata su query**   Se l'organizzazione conserva gli elementi in base a determinati parametri di query, è possibile utilizzare una conservazione in locale basata su query. È possibile specificare parametri di query, quali parole chiave, date di inizio e di fine, indirizzi di mittenti e destinatari e tipi di messaggio. Una volta creata una conservazione in locale basata su query, vengono conservati tutti gli elementi della cassetta postale esistenti e futuri (inclusi i messaggi ricevuti in data successiva) corrispondenti ai parametri di query.
    

    > [!IMPORTANT]
    > Anche gli elementi contrassegnati come non ricercabili, in genere perché non è possibile indicizzare un allegato, vengono conservati, poiché non è possibile determinare se corrispondono a parametri query. Per ulteriori dettagli sull'elemento non ricercabile, vedere <A href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Elementi non ricercabili in Exchange eDiscovery</A>.



  - **Conservazione basata sul tempo**   Archiviazione sul posto e Blocco per controversia legale consentono di specificare un periodo di tempo per il quale vengono conservati gli elementi. La durata viene calcolata a partire dalla data di ricezione o creazione dell'elemento della cassetta postale.
    
    Se l'organizzazione richiede che vengano conservati tutti gli elementi della cassetta postale per un determinato periodo di tempo (ad esempio, 7 anni), è possibile creare una conservazione basata sul tempo. In Exchange 2013, è possibile specificare un periodo di conservazione per gli elementi. Gli elementi conservati vengono datati in base alla relativa data di ricezione. Ad esempio, prendere in considerazione una cassetta postale posizionata in una conservazione in locale basata sul tempo e con un periodo di conservazione di 360 giorni. Se un elemento in quella cassetta postale viene eliminato dopo 300 giorni dalla data di ricezione, viene mantenuto per altri 65 giorni prima di essere eliminato in modo definitivo. È possibile utilizzare una conservazione in locale basata sul tempo insieme a un criterio di conservazione per accertarsi che gli elementi vengano conservati per l'intervallo di tempo specificato ed eliminati in modo definitivo al termine di tale periodo.

È possibile utilizzare Conservazione in locale per attribuire a un utente più conservazioni. Quando un utente ha più blocchi, le query di ricerca da blocchi basati su query vengono combinate (con operatori **OR**). In questo caso, il numero massimo di parole chiave in tutti i blocchi basati su query che vengono bloccate in una cassetta postale è pari a 500. Se sono presenti più di 500 parole chiave, tutto il contenuto della cassetta postale viene bloccato (non solo il contenuto che corrisponde ai criteri di ricerca). Tutto il contenuto viene bloccato finché non viene ridotto a 500 o meno il numero totale di parole chiave.

Torna su

## Archiviazione sul posto e conservazione per controversia legale

La conservazione per controversia legale, la funzionalità di conservazione introdotta in Exchange 2010 per conservare i dati per eDiscovery, è ancora disponibile in Exchange 2013. La conservazione per controversia legale utilizza la proprietà **LitigationHoldEnabled** di una cassetta postale. Mentre Archiviazione sul posto fornisce una funzionalità di conservazione granulare basata su parametri e la possibilità di attivare più blocchi, Conservazione per controversia legale consente solo di bloccare tutti gli elementi. È inoltre possibile specificare un periodo di tempo di conservazione degli elementi quando si attiva Conservazione per controversia legale per una cassetta postale. La durata viene calcolata a partire dalla data di ricezione o creazione dell'elemento della cassetta postale. Se la durata non è impostata, gli elementi vengono conservati a tempo indeterminato o fino a quando non viene rimossa la conservazione.

Quando si attivano contemporaneamente una o più archiviazioni sul posto e la conservazione per controversia legale per una cassetta postale, tutti gli elementi vengono conservati a tempo indeterminato o fino a quando non vengono rimosse le conservazioni. Se si elimina la conservazione per controversia legale e l'utente dispone ancora di una o più archiviazioni sul posto attive, gli elementi corrispondenti ai criteri per l'archiviazione sul posto vengono conservati per il periodo di tempo specificato nelle impostazioni di conservazione. Quando si sposta una cassetta postale sottoposta a conservazione per controversia legale di Exchange 2010 in un server Cassette postali di Exchange 2013, l'impostazione relativa alla conservazione per controversia legale rimane attiva; in questo modo, è possibile continuare a soddisfare i requisiti di conformità durante e dopo lo spostamento.


> [!NOTE]
> Quando si imposta una cassetta postale sull'archiviazione sul posto o sul blocco per controversia legale, la conservazione interessa sia la cassetta postale primaria che quella di archiviazione. Se si inserisce una cassetta postale principale locale nell'archiviazione in una distribuzione ibrida di Exchange, viene conservata anche la cassetta postale di archiviazione basata sul cloud (se abilitata).



Per ulteriori informazioni, vedere:

  - [Conservazione in caso di dispute di una cassetta postale](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - [Mettere in attesa tutte le cassette postali](place-all-mailboxes-on-hold-exchange-2013-help.md)

## Conservazione in locale di una cassetta postale

Gli utenti autorizzati che sono stati aggiunti al gruppo di ruoli Controllo di accesso basato sui ruoli (RBAC) di [Gestione individuazione](discovery-management-exchange-2013-help.md) o che sono stati assegnati ai ruoli di gestione della conservazione legale e della ricerca delle cassette postali possono attivare la conservazione in locale per gli utenti delle cassette postali. È possibile delegare l'attività ai gestori dei record, ai responsabili della conformità o agli avvocati della divisione legale dell'azienda, assegnando privilegi minimi. Per ulteriori informazioni sull'assegnazione del gruppo di ruoli Gestione individuazione, vedere [Assegnare le autorizzazioni di eDiscovery di Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).


> [!IMPORTANT]
> In Exchange&nbsp;2010, il ruolo di Conservazione per controversia legale forniva a un utente le autorizzazioni sufficienti per attivare la conservazione per controversia legale per le cassette postali. In Exchange 2013, è possibile utilizzare la stessa autorizzazione per attivare un'archiviazione sul posto indefinita o basata sul tempo. Tuttavia, per creare un'archiviazione sul posto basata su query, l'utente deve godere del ruolo Ricerca nelle cassette postali. Il gruppo di ruoli Gestione individuazione dispone di entrambi questi ruoli.



In Exchange 2013, la funzionalità Conservazione in locale è integrata con le ricerche eDiscovery in locale. È possibile utilizzare la procedura guidata **eDiscovery e conservazione in locale** in Interfaccia di amministrazione di Exchange o **New-MailboxSearch** e i relativi cmdlet in Exchange Management Shell per attivare la conservazione in locale per una cassetta postale. Per ulteriori informazioni sull'attivazione della conservazione in locale per una cassetta postale, vedere [Creare o rimuovere un'archiviazione sul posto](create-or-remove-an-in-place-hold-exchange-2013-help.md).


> [!NOTE]
> Se si utilizza Archiviazione di Exchange Online per il provisioning di un archivio basato su cloud per le proprie cassette postali locali, è necessario gestire Conservazione in locale dalla propria organizzazione di Exchange 2013 locale. Le impostazioni di conservazione vengono propagate automaticamente all'archivio basato su cloud tramite DirSync. Come descritto in precedenza, quando si imposta la conservazione per una cassetta postale locale, la conservazione viene abilitata anche per l'archivio basato su cloud corrispondente.



Molte organizzazioni richiedono che gli utenti siano informati quando è attiva la conservazione. Inoltre, quando si attiva la conservazione per una cassetta postale, i criteri di conservazione applicabili all'utente della cassetta postale non devono essere sospesi. Dal momento che i messaggi continuano ad essere eliminati come previsto, è possibile che gli utenti non si accorgano dell'attivazione della conservazione. Se l'organizzazione richiede che gli utenti vengano informati sulla conservazione, è possibile aggiungere un messaggio di notifica alla proprietà **Retention Comment** dell'utente della cassetta postale e utilizzare la proprietà **RetentionUrl** per effettuare il collegamento a una pagina Web per ulteriori informazioni. Outlook 2010 e versioni successive visualizza la notifica e l'URL nell'area di backstage. È necessario utilizzare Shell per aggiungere e gestire queste proprietà per una cassetta postale.

Torna su

## Applicare un blocco alle cartelle pubbliche

In Exchange Online, è possibile applicare un blocco alle cartelle pubbliche tramite blocco sul posto. Il blocco per controversia legale non è supportato per le cartelle pubbliche. Quando si crea un blocco sul posto, l'unica opzione disponibile è quella di applicare un blocco a tutte le cartelle pubbliche dell'organizzazione. Di conseguenza, il blocco sul posto viene applicato a tutte le cassette postali delle cartelle pubbliche.

Inoltre, quando si applica il blocco sul posto alle cartelle pubbliche, vengono conservate le e-mail relative al processo di sincronizzazione della gerarchia di cartelle pubbliche. Ciò potrebbe generare la conservazione di migliaia di e-mail correlate alla sincronizzazione della gerarchia. Questi messaggi possono riempire la quota di archiviazione per la cartella Elementi ripristinabili sulle cassette postali delle cartelle pubbliche. Per evitare questo problema, è possibile creare una query basata sul blocco sul posto e aggiungere la coppia `property:value` seguente alla query di ricerca:

    NOT(subject:HierarchySync*)

Il risultato è che tutti i messaggi (correlati alla sincronizzazione della gerarchia della cartella pubblica) che includono la frase "HierarchySync" nell'oggetto non vengono bloccate.

## Cartella Archiviazioni ed elementi ripristinabili

Archiviazione sul posto e Conservazione per controversia legale utilizzano la cartella Elementi ripristinabili per conservare gli elementi. La cartella Elementi ripristinabili sostituisce la funzionalità conosciuta come *dumpster* nelle precedenti versioni di Exchange. La cartella Elementi ripristinabili è nascosta dalla visualizzazione predefinita di Outlook, Outlook Web App e altri client di posta elettronica. Per ulteriori informazioni sulla cartella Elementi ripristinabili, vedere [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md).

Per impostazione predefinita, quando un utente elimina un messaggio da una cartella (fatta eccezione per la cartella Posta eliminata), il messaggio viene trasferito nella cartella Posta eliminata. Questa caratteristica è nota con il nome di *spostamento*. Quando un utente *elimina temporaneamente* un elemento (premendo MAIUSC+CANC) o elimina un elemento dalla cartella Posta eliminata, il messaggio viene spostato nella cartella Elementi ripristinabili, scomparendo dalla vista dell'utente.

Gli elementi nella cartella Elementi ripristinabili vengono conservati per il periodo di conservazione degli elementi eliminati configurato nel database delle cassette postali dell'utente. Per impostazione predefinita, il periodo di conservazione degli elementi eliminati è impostato su 14 giorni per i database delle cassette postali. È anche possibile configurare una quota di archiviazione per la cartella Elementi ripristinabili. In questo modo è possibile proteggere l'organizzazione da un potenziale attacco DoS (Denial of Service) dovuto alla rapida crescita della cartella degli elementi ripristinabili e di conseguenza del database delle cassette postali. Se per una cassetta postale non viene attivata la conservazione in locale o la conservazione per controversia legale, se viene superata la quota di archiviazione della cartella Elementi ripristinabili o se l'elemento si trova nella cartella da un periodo di tempo superiore a quello di conservazione degli elementi eliminati, gli elementi vengono eliminati definitivamente dalla cartella degli elementi ripristinabili con la procedura First In, First Out.

La cartella Elementi ripristinabili contiene le seguenti sottocartelle utilizzate per archiviare gli elementi eliminati in diversi siti e facilitare l'archiviazione sul posto e la conservazione per controversia legale:

  - **Deletions**   Gli elementi rimossi dalla cartella Posta eliminata o eliminati temporaneamente da altre cartelle vengono spostati nella sottocartella Deletions e l'utente può vederli quando utilizza la funzionalità Recupera elementi eliminati in Outlook e Outlook Web App. Per impostazione predefinita, gli elementi risiedono in questa cartella fino alla scadenza del periodo di conservazione degli elementi eliminati configurato per la cassetta postale.

  - **Purges**   Quando un utente elimina un elemento dalla cartella Elementi ripristinabili (utilizzando lo strumento Recupera elementi eliminati in Outlook e Outlook Web App), l'elemento viene spostato nella cartella Purges. Anche gli elementi che superano il periodo di conservazione degli elementi eliminati configurato nel database delle cassette postali o nella cassetta postale vengono spostati nella cartella Purges. Gli elementi in questa cartella non sono visibili agli utenti che utilizzano lo strumento Recupera elementi eliminati. Quando l'assistente della cassetta postale elabora la cassetta postale, gli elementi nella cartella Purges vengono eliminati dal database delle cassette postali. Quando si attiva la conservazione per controversia legale per l'utente della cassetta postale, l'assistente della cassetta postale non elimina gli elementi presenti in questa cartella.

  - **DiscoveryHold**   Se si attiva la conservazione in locale per un utente, gli elementi eliminati vengono spostati in questa cartella. Quando l'assistente della cassetta postale elabora la cassetta postale, valuta i messaggi in questa cartella. Gli elementi che corrispondono alla query per la conservazione in locale vengono conservati per l'intero periodo di tempo specificato nella query. Se non viene specificato alcun periodo di conservazione, gli elementi vengono conservati a tempo indeterminato o fino a quando non viene annullata la conservazione per l'utente.

  - **Versions**   Quando viene attivata la conservazione in locale o la conservazione per controversia legale per un utente, gli elementi della cassetta postale devono essere protetti da manomissioni o modifiche da parte dell'utente o di un processo. Questa operazione viene eseguita tramite un processo di *copia in scrittura*. Quando un utente o un processo modifica determinate proprietà di un elemento della cassetta postale, una copia dell'elemento originale viene salvata nella cartella Versions prima che le modifiche diventino effettive. Il processo viene ripetuto per le modifiche successive. Gli elementi acquisiti nella cartella Versions vengono anche indicizzati e restituiti nelle ricerche eDiscovery in locale. Una volta rimossa la conservazione, le copie presenti nella cartella Versions vengono rimosse dall'Assistente cartelle gestite.

### Proprietà che attivano la copia in scrittura

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di elemento</th>
<th>Proprietà che attivano la copia in scrittura</th>
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
<li><p>Mittenti/Destinatari</p></li>
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
<td><p>Nessuno (gli elementi nella cartella Bozze sono esenti dalla copia in scrittura)</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> La copia su scrittura è disabilitata per gli elementi del calendario nella cassetta postale dell'organizzatore quando si ricevono le risposte dei partecipanti alle convocazioni di riunione e le informazioni di verifica della riunione vengono aggiornate. Per gli elementi del calendario e per quelli con un promemoria impostato, l'opzione copy-on-write è disabilitata per le proprietà ReminderTime e ReminderSignalTime. Le modifiche a tali proprietà non vengono acquisite da copy-on-write. Le modifiche apportate ai feed RSS non vengono acquisite mediante la copia in scrittura.



Sebbene le cartelle DiscoveryHold, Purges e Versions non siano visibili all'utente, tutti gli elementi nella cartella Elementi ripristinabili vengono indicizzati da Ricerca di Exchange e possono essere individuati utilizzando eDiscovery in locale. Una volta annullata la conservazione in locale o la conservazione per controversia legale per l'utente di una cassetta postale, gli elementi nelle cartelle DiscoveryHold, Purges e Versions vengono eliminati dall'Assistente cartelle gestite.

Torna su

## Blocchi e quota della cassetta postale

Il calcolo degli elementi nella cartella Elementi ripristinabili non viene considerato nella quota della cassetta postale dell'utente. In Exchange la cartella Elementi ripristinabili ha una propria quota. Per Exchange, i valori predefiniti per le proprietà delle cassette postali *RecoverableItemsWarningQuota* e *RecoverableItemsQuota* sono impostate rispettivamente su 20 e 30 GB. Per modificare questi valori per un database di cassette postali di Exchange Server 2013, utilizzare il cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\)). Per modificarli per le singole cassette postali, utilizzare il cmdlet [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

Quando la cartella degli elementi ripristinabili di un utente supera la quota di avviso per gli elementi ripristinabili (secondo quanto specificato dal parametro *RecoverableItemsWarningQuota*), nel registro eventi Applicazione del server Cassette postali. Quando la cartella supera la quota per gli elementi ripristinabili (secondo quanto specificato dal parametro *RecoverableItemsQuota*), gli utenti non saranno in grado di svuotare la cartella Posta eliminata o di eliminare definitivamente gli elementi della cassetta postale. Anche copy-on-write non sarà in grado di creare copie degli elementi modificati. Di conseguenza, è fondamentale controllare le quote degli elementi ripristinabili per gli utenti delle cassette postali sottoposti ad archiviazione sul posto.

In Exchange Online, la quota per la cartella Elementi ripristinabili (nella cassetta postale primaria) viene automaticamente aumentata a 100 GB quando per una cassetta postale si attiva la Conservazione per controversia legale o Archiviazione sul posto. Quando la quota di archiviazione per la cartella Elementi ripristinabili nella cassetta postale principale di una cassetta postale in blocco sta per raggiungere il limite, è possibile eseguire le operazioni seguenti:

  - **Abilitare la cassetta postale di archiviazione e attivare la funzione di espansione automatica dell'archiviazione**   Per abilitare una capacità di archiviazione illimitata per la cartella Elementi ripristinabili, abilitare la cassetta postale di archiviazione e attivare la funzione di espansione automatica dell’archiviazione in Exchange Online. Risulteranno 100 GB per la cartella Elementi ripristinabili nella cassetta postale principale e capacità illimitata di archiviazione per la cartella Elementi ripristinabili nell'archivio dell'utente. Vedere: [Abilitare le cassette postali di archiviazione nel Centro sicurezza e conformità di Office 365](https://go.microsoft.com/fwlink/p/?linkid=863320) e [Abilitare l'archiviazione illimitata in Office 365](https://go.microsoft.com/fwlink/p/?linkid=844569).
    
    **Note**:
    
      - Dopo aver abilitato l'archiviazione per una cassetta postale che sta per superare la quota di archiviazione per la cartella Elementi ripristinabili, è consigliabile eseguire l'Assistente cartelle gestite per attivare manualmente l’elaborazione della cassetta postale da parte dell’assistente, in modo che gli elementi scaduti vengano spostati nella cartella Elementi ripristinabili della cassetta postale di archiviazione. Per istruzioni, vedere il Passaggio 4 in [Aumentare la quota degli elementi ripristinabili per le cassette postali bloccate](https://go.microsoft.com/fwlink/p/?linkid=786479).
    
      - Tenere presente che altri elementi nella cassetta postale dell'utente potrebbero essere spostati nella nuova cassetta postale di archiviazione. Prendere in considerazione l’opzione di informare l’utente che potrebbe verificarsi questa situazione dopo aver abilitato la cassetta postale di archiviazione.

  - **Creazione di un criterio di conservazione personalizzato per le cassette postali in blocco**    Oltre ad attivare la cassetta postale di archiviazione e la funzione di espansione automatica dell’archiviazione per le cassette postali in blocco per controversia legale o in blocco sul posto, è possibile creare criteri di conservazione personalizzati per le cassette postali in blocco. Ciò consente di applicare criteri di conservazione alle cassette postali in blocco differenti dai criteri di gestione record di messaggistica predefiniti applicati alle cassette postali che non sono in blocco. In questo modo è possibile applicare tag di conservazione progettati specificamente per le cassette postali in blocco. Include la creazione di un nuovo tag di conservazione per la cartella Elementi ripristinabili.

Per ulteriori informazioni, vedere [Aumentare la quota degli elementi recuperabili per le cassette postali in attesa](https://go.microsoft.com/fwlink/p/?linkid=786479).

## Archiviazioni e inoltro della posta elettronica

Gli utenti possono usare Outlook e Outlook Web App per configurare l'inoltro della posta elettronica per la propria cassetta postale. L'inoltro della posta elettronica consente agli utenti di configurare la propria cassetta postale per inoltrare i messaggi di posta elettronica inviati alla propria cassetta postale a un'altra cassetta posizionata all'interno o all'esterno dell'organizzazione. L'inoltro della posta elettronica può essere configurato in modo che tutti i messaggi inviati alla cassetta postale originale non vengono copiati in tale cassetta postale e vengano inviati solo all'indirizzo di inoltro.

Se l'inoltro della posta elettronica è impostato per una cassetta postale e i messaggi non vengono copiati nella cassetta postale originale, cosa succede se la cassetta postale è bloccata? Il comportamento è diverso a seconda che la cassetta postale si trovi in un'organizzazione di Exchange 2013 o Exchange Online.

  - **Exchange Online**   Le impostazioni di blocco per la cassetta postale vengono controllate durante il processo di recapito. Se il messaggio soddisfa i criteri di blocco della cassetta postale, una copia del messaggio viene salvata nella cartella Elementi ripristinabili. Questo significa che è possibile usare eDiscovery sul posto per eseguire la ricerca dei messaggi originali inoltrati all'altra cassetta postale.

  - **Exchange 2013**   Se i messaggi vengono inoltrati a un'altra cassetta postale e non vengono copiati nella cassetta postale originale, essi non vengono acquisiti e copiati nella cartella Elementi ripristinabili. Ciò significa che i messaggi inoltrati non vengono restituiti in una ricerca di eDiscovery sul posto. Per risolvere questo problema, le organizzazioni di Exchange 2013 possono provare a rimuovere la possibilità per gli utenti di configurare l'inoltro della posta elettronica.

Torna su

## Conservazione del contenuto Lync archiviato

Exchange 2013, Microsoft Lync 2013 e Microsoft SharePoint 2013 offrono una conservazione integrata e un'esperienza eDiscovery che consentono di conservare e ricercare elementi nei differenti archivi di dati. Exchange 2013 consente di archiviare il contenuto Lync Server 2013 in Exchange, eliminando la necessità di un'archiviazione del contenuto Lync da parte di un database SQL Server distinto. La funzionalità di eDiscovery e conservazione integrata in SharePoint 2013 consente di conservare e ricercare i dati in tutti gli archivi da una singola console.

Quando si attiva la conservazione in locale o la conservazione per controversia legale per una cassetta postale di Exchange 2013, il contenuto Microsoft Lync 2013 (quali, conversazioni di messaggistica istantanea e i file condivisi in una riunione online) vengono archiviati nella cassetta postale. Se si cerca la cassetta postale utilizzando Centro eDiscovery in Microsoft SharePoint 2013 o eDiscovery in locale in Exchange 2013, viene restituito nei risultati della ricerca anche tutto il contenuto Lync archiviato corrispondente alla query di ricerca. È anche possibile restringere la ricerca al contenuto Lync archiviato nella cassetta postale.

Per abilitare l'archiviazione del contenuto Lync nella cassetta postale di Exchange 2013, è necessario configurare l'integrazione Lync 2013 con Exchange 2013. Per informazioni dettagliate, vedere i seguenti argomenti:

  - [Pianificazione per l'archiviazione](https://technet.microsoft.com/it-it/library/jj205069\(v=ocs.15\))

  - [Distribuzione dell'archiviazione](https://technet.microsoft.com/it-it/library/jj205147\(v=ocs.15\))

Torna su

## Eliminazione di una cassetta postale bloccata

Quando si elimina una cassetta postale sottoposta ad Archiviazione sul posto o Conservazione per controversia legale, il risultato è diverso a seconda che la cassetta postale si trovi in un'organizzazione di Exchange 2013 o Exchange Online.

  - **Exchange 2013**   Se un amministratore elimina un account utente che dispone di una cassetta postale, l'archivio informazioni di Exchange rileva che la cassetta postale non è più collegata all'account utente e la contrassegna come da eliminare, anche se è bloccata. Se si desidera conservare la cassetta postale, eseguire queste operazioni:
    
    1.  Disattivare l'account utente invece di eliminarlo.
    
    2.  Modificare le proprietà della cassetta postale al fine di limitarne uso e accesso. Ad esempio, impostare la quota di invio e ricezione su 1, bloccare gli utenti che possono inviare messaggi alla cassetta postale e limitare gli utenti che possono accedere alla cassetta postale.
    
    3.  Conservare la cassetta postale fino a quando tutti i dati sono stati rimossi o fino a quando la conservazione dei dati non è più necessaria.

  - **Exchange Online**   Se la cassetta postale di un utente è sottoposta ad Archiviazione sul posto o Conservazione per controversia legale e l'account di Office 365 corrispondente viene eliminato, la cassetta postale viene convertita in una *cassetta postale inattiva*, ovvero un tipo di cassetta postale eliminata temporaneamente. Le cassette postali inattive vengono utilizzate per conservare il contenuto della cassetta postale di un utente dopo che ha lasciato l'organizzazione. I contenuti di una cassetta postale inattiva vengono conservati per tutta la durata del blocco applicato alla cassetta postale prima che fosse resa inattiva. Ciò consente agli amministratori, ai responsabili della conformità o ai responsabili dei record di utilizzare la funzionalità eDiscovery sul posto per accedere al contenuto di una cassetta postale inattiva. Le cassette postali inattive non possono ricevere posta elettronica e non vengono visualizzate nella rubrica condivisa dell'organizzazione o in altri elenchi. Per altre informazioni, vedere [Cassette postali inattive in Exchange Online](https://technet.microsoft.com/it-it/library/dn798632\(v=exchg.150\)).

Torna su

## Migrazione delle cassette postali bloccate da Exchange 2013 a Office 365

Se si dispone di una distribuzione ibrida di Exchange, le seguenti condizioni sono vere quando si sposta (carica) una cassetta postale locale di Exchange 2013 da Exchange Online a Office 365:

  - Se la cassetta postale locale è sottoposta a Conservazione per controversia legale o Archiviazione sul posto, le impostazioni di blocco vengono mantenute dopo la cassetta postale viene spostata in Exchange Online.

  - Se la cassetta postale locale è sottoposta a Conservazione per controversia legale o Archiviazione sul posto, qualsiasi contenuto nella cartella Elementi ripristinabili viene spostato nella cassetta postale di Exchange Online.


> [!NOTE]
> Le impostazioni di blocco e i contenuti nella cartella Elementi ripristinabili vengono mantenuti anche quando si sposta (trasferisce) una cassetta postale di Exchange Online nell'organizzazione di Exchange 2013 locale.



Esistono altri modi per eseguire la migrazione dei dati di posta elettronica locali in Office 365, ad esempio usando una migrazione a fasi di Exchange o completa di Exchange.

  - La migrazione a fasi può essere utilizzata per eseguire la migrazione delle cassette postali da Exchange 2003 o Exchange 2007 a Office 365. In queste versioni di Exchange, non esiste la cartella Elementi ripristinabili (e le relative funzionalità). Pertanto, quando si esegue la migrazione di cassette postali di Exchange 2003 o Exchange 2007 in Office 365, non esiste alcuna cartella Elementi ripristinabili in cui spostare i contenuti.

  - La migrazione completa può essere utilizzata per eseguire la migrazione delle cassette postali da Exchange 2003, Exchange 2007 e Exchange 2010 a Office 365. Come affermato in precedenza, le cassette postali di Exchange 2003 e Exchange 2007 non dispongono di una cartella Elementi ripristinabili che può essere migrata. Poiché la cartella Elementi ripristinabili è stata introdotta in Exchange 2010, il contenuto nella cartella verrà migrato in Office 365 quando si utilizza una migrazione completa per eseguire la migrazione delle cassette postali di Exchange 2010.


> [!TIP]
> Per Exchange 2013 e Exchange&nbsp;2010, una distribuzione ibrida di Exchange è il modo consigliato per eseguire la migrazione delle cassette postali locali in Office 365.



Torna su


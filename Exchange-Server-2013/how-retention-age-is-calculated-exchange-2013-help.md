---
title: 'Calcolo del periodo di conservazione: Exchange 2013 Help'
TOCTitle: Calcolo del periodo di conservazione
ms:assetid: a7daf7aa-0411-4b26-a422-eefd1b113f9f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb430780(v=EXCHG.150)
ms:contentKeyID: 50481385
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Calcolo del periodo di conservazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-07-27_

L'Assistente cartelle gestite (MFA, Managed Folder Assistant) è uno dei numerosi processi per *assistente cassette postali* eseguito sui server Cassette postali. Il suo lavoro consiste nel processare le cassette postali con criterio di conservazione applicato, aggiungere i tag di conservazione inclusi nel criterio alla cassetta postale ed elaborare gli elementi nella cassetta postale. Se gli elementi hanno un tag di conservazione, l'assistente verifica la validità di tali elementi. Se un elemento ha superato il *periodo di conservazione*, esegue l'*azione di conservazione* specificata. Le azioni di conservazione includono lo spostamento di un elemento nell'archivio dell'utente, l'eliminazione dell'elemento e l'autorizzazione di ripristino o l'eliminazione permanente dell'elemento.

Per ulteriori informazioni, vedere [Tag di conservazione e criteri di conservazione](retention-tags-and-retention-policies-exchange-2013-help.md).

## Determinazione della scadenza di diversi tipi di elementi

Il periodo di conservazione degli elementi della cassetta postale viene calcolato la data di consegna o nel caso di elementi quali le bozze che non vengono recapitati ma creati dall'utente, la data di che creazione di un elemento. Quando l'Assistente cartelle gestite elabora elementi in una cassetta postale, contrassegna una data di inizio e data di scadenza di tutti gli elementi contenenti i tag di conservazione con l'azione di conservazione **Elimina e Consenti ripristino** o **Elimina definitivamente**. Gli elementi con un tag di archiviazione vengono inoltre corredati una move date.

Gli elementi nella cartella Elementi eliminati e gli elementi che hanno una data di inizio e una di fine, ad esempio gli elementi del calendario (riunioni e appuntamenti) e le attività, vengono gestiti in modo diverso come mostrato nella tabella.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Se il tipo di elemento è...</th>
<th>E l'elemento è...</th>
<th>Il periodo di conservazione viene calcolato in base a...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Messaggio di posta elettronica</p></li>
<li><p>Documento</p></li>
<li><p>Fax</p></li>
<li><p>Elemento del Diario</p></li>
<li><p>Convocazione di riunione, risposta o annullamento</p></li>
<li><p>Chiamata senza risposta</p></li>
</ul></td>
<td><p>In una cartella diversa da Elementi eliminati</p></td>
<td><p>Data di consegna o data di creazione</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>Messaggio di posta elettronica</p></li>
<li><p>Documento</p></li>
<li><p>Fax</p></li>
<li><p>Elemento del Diario</p></li>
<li><p>Convocazione di riunione, risposta o annullamento</p></li>
<li><p>Chiamata senza risposta</p></li>
</ul></td>
<td><p>Nella cartella Elementi eliminati</p></td>
<td><ul>
<li><p>Data di recapito o di creazione se l'elemento non è stato eliminato da una cartella che non ha un tag di conservazione ereditato o implicito.</p></li>
<li><p>Se un elemento è in una cartella che non ha un tag ereditato o implicito applicato, l'elemento non viene elaborato dal MFA e pertanto non ha una data di inizio da esso contrassegnato. Quando l'utente elimina tale tipo di elemento e il MFA lo elabora per la prima volta nella cartella Elementi eliminati, contrassegna la data corrente come data di inizio.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Calendario</p></td>
<td><p>In una cartella diversa da Elementi eliminati</p></td>
<td><ul>
<li><p>Gli elementi del Calendario non ricorrenti scadono in base alla data di fine.</p></li>
<li><p>Gli elementi del Calendario ricorrenti scadono in base alla data di fine dell'ultima occorrenza. Gli elementi del Calendario ricorrenti senza una data di fine non scadono.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Calendario</p></td>
<td><p>Nella cartella Elementi eliminati</p></td>
<td><ol>
<li><p>Un elemento del Calendario scade in base alla <code>message-received date</code>, se presente.</p></li>
<li><p>Se un elemento del Calendario non possiede una <code>message-received date</code>, la scadenza viene stabilita in base alla <code>message-creation date</code>.</p></li>
<li><p>Se un elemento del Calendario non possiede una <code>message-received date</code> né una <code>message-creation date</code>, non scade.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Attività</p></td>
<td><p>In una cartella diversa da Elementi eliminati</p></td>
<td><ul>
<li><p>Attività non ricorrenti:</p>
<ol>
<li><p>Un'attività non ricorrente scade in base alla <code>message-received date</code>, se presente.</p></li>
<li><p>Se un'attività non possiede una <code>message-received date</code>, la scadenza viene stabilita in base alla <code>message-creation date</code>.</p></li>
<li><p>Se un'attività non ricorrente non possiede una <code>message-received date</code> né una <code></code><code>message-creation date</code>, non ha scadenza.</p></li>
</ol></li>
<li><p>Un'attività ricorrente scade in base alla <code>end date</code> dell'ultima occorrenza. Se un'attività ricorrente non ha una <code>end date</code>, non scade.</p></li>
<li><p>Un'attività rigenerante (ovvero un'attività ricorrente che viene rigenerata una volta trascorso un tempo specificato dal completamento dell'istanza precedente dell'attività) non scade.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Attività</p></td>
<td><p>Nella cartella Elementi eliminati</p></td>
<td><ol>
<li><p>Un'attività scade in base alla <code>message-received date</code>, se presente.</p></li>
<li><p>Se un'attività non possiede una <code>message-received date</code>, la scadenza viene stabilita in base alla <code>message-creation date</code>.</p></li>
<li><p>Se un'attività non possiede una <code>message-received date</code> né una <code>message-creation date</code>, non scade.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Contact</p></td>
<td><p>In qualsiasi cartella</p></td>
<td><p>Contatti non sono contrassegnati con una data di inizio o una data di scadenza, in modo che sta ignorati dall'Assistente cartelle gestite e non scadono.</p></td>
</tr>
<tr class="even">
<td><p>Danneggiato</p></td>
<td><p>In qualsiasi cartella</p></td>
<td><p>Gli elementi danneggiati vengono ignorati dall'Assistente cartelle gestite e non scadono.</p></td>
</tr>
</tbody>
</table>


## Esempi


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Se l'utente..</th>
<th>I tag di conservazione nella cartella...</th>
<th>L'Assistente cartelle gestite...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ol>
<li><p>Riceve un messaggio nella Posta in arrivo in data 26/01/2013.</p></li>
<li><p>Elimina il messaggio in data 27/02/2013.</p></li>
</ol>
<p></p></td>
<td><ul>
<li><p>Posta in arrivo: Elimina in 365 giorni</p></li>
<li><p>Elementi eliminati: Elimina in 30 giorni</p></li>
</ul>
<p></p></td>
<td><ol>
<li><p>Elabora il messaggio nella Posta in arrivo in data 26/01/2013, lo contrassegna con <em>data di inizio</em> 26/01/2013 e <em>data di scadenza</em> 26/01/2014.</p></li>
<li><p>Elabora nuovamente il messaggio nella cartella Elementi eliminati in data 27/02/2013. Ricalcola la data di scadenza in base alla stessa data di inizio (26/01/2013).</p></li>
<li><p>Poiché l'elemento è più vecchio di 30 giorni, scade immediatamente.</p></li>
</ol></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Riceve un messaggio nella Posta in arrivo in data 26/01/2013.</p></li>
<li><p>Elimina il messaggio in data 27/02/2013.</p></li>
</ol></td>
<td><ul>
<li><p>Posta in arrivo: Nessun elemento (ereditato o implicito)</p></li>
<li><p>Elementi eliminati: Elimina in 30 giorni</p></li>
</ul></td>
<td><ol>
<li><p>Elabora il messaggio nella cartella Elementi eliminati in data 27/02/2013 e determina che l'elemento non ha una data di inizio. Applica quindi al messaggio la data corrente come data di inizio e la data 27/03/13 come data di scadenza.</p></li>
<li><p>L'elemento scade in data 27/03/13, 30 giorni dopo l'eliminazione o lo spostamento nella cartella Elementi eliminati da parte dell'utente.</p></li>
</ol></td>
</tr>
</tbody>
</table>


## Ulteriori informazioni

  - Nella Exchange Online, l'Assistente cartelle gestite elabora una cassetta postale di una sola volta in sette giorni. In questo caso, gli elementi da scaduto fino a sette giorni dopo la data di scadenza contrassegnate per l'elemento.

  - Gli elementi nelle cassette postali messa in attesa di conservazione non vengono elaborati dall'Assistente cartelle gestite fino a quando non viene rimosso il mantenimento.

  - Se viene eseguito il mantenimento su una cassetta postale in stato di blocco sul posto o per controversia legale, gli elementi in scadenza vengono rimossi dalla Posta in arrivo, ma vengono conservati nella cartella Elementi recuperabili fino alla rimozione della cassetta di posta da [Archiviazione sul posto e conservazione per controversia legale](in-place-hold-and-litigation-hold-exchange-2013-help.md).

  - Nelle distribuzioni ibride, è necessario che i criteri di conservazione e i tag di conservazione siano gli stessi nelle organizzazioni locali e in Exchange Online, per spostare e fare scadere gli elementi coerentemente nelle organizzazioni. Per ulteriori informazioni, vedere [Esportare e importare i tag di conservazione](export-and-import-retention-tags-exchange-2013-help.md).


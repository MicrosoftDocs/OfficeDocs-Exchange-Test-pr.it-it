---
title: 'Mantenere Ccn e i destinatari del gruppo di destinazione espanso per eDiscovery: Exchange 2013 Help'
TOCTitle: Mantenere Ccn e i destinatari del gruppo di destinazione espanso per eDiscovery
ms:assetid: eb8ddf15-0080-457e-9d83-e73e193da334
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn770225(v=EXCHG.150)
ms:contentKeyID: 62517051
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mantenere Ccn e i destinatari del gruppo di destinazione espanso per eDiscovery

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**Ultima modifica dell'argomento:**2017-06-19_

Blocco sul posto, blocco per controversia legale e i [criteri di conservazione di Office 365](http://go.microsoft.com/fwlink/?linkid=827811) (creati nel Centro sicurezza e conformità di Office 365) consentono di mantenere i contenuti delle cassette postali per soddisfare i requisiti di eDiscovery e la conformità alle normative. Per impostazione predefinita, le informazioni sui destinatari inseriti direttamente nei campi A e Cc di un messaggio sono incluse in tutti i messaggi, ma l'organizzazione può richiedere la possibilità di cercare e riprodurre i dettagli di tutti i destinatari di un messaggio. Ciò include:

  - **Destinatari inseriti utilizzando il campo Ccn di un messaggio**   I destinatari Ccn vengono archiviati nel messaggio nella cassetta postale del mittente, ma non vengono inclusi nelle intestazioni del messaggio recapitato ai destinatari.

  - **Destinatari del gruppo di distribuzione espanso**   I destinatari che ricevono il messaggio perché sono membri di un gruppo di distribuzione al quale è indirizzato il messaggio, inseriti nei campi A, Cc o Ccn.

Exchange Online e Exchange Server 2013 (aggiornamento cumulativo 7 e versioni successive) conservano informazioni sui destinatari Ccn e dei gruppi di distribuzione espansi. È possibile cercare queste informazioni utilizzando una ricerca eDiscovery sul posto nell'Interfaccia di amministrazione di Exchange o una ricerca contenuto nel Centro sicurezza e conformità.

## Come mantenere i destinatari Ccn e del gruppo di distribuzione espanso

Come già indicato, le informazioni sui destinatari Ccn vengono archiviate con il messaggio nella cassetta postale del mittente. Queste informazioni sono indicizzate e disponibili per i blocchi e le ricerche eDiscovery.

Le informazioni relative ai destinatari del gruppo di distribuzione espanso vengono archiviate con il messaggio dopo aver abilitato il blocco sul posto o il blocco per controversia legale per una cassetta postale. In Office 365, queste informazioni sono inoltre memorizzate quando un criterio di conservazione di Office 365 viene applicato a una cassetta postale. L'appartenenza al gruppo di distribuzione viene determinata al momento dell'invio del messaggio. L'elenco dei destinatari espanso archiviato con il messaggio non viene influenzato dalle modifiche apportate all'appartenenza del gruppo dopo l'invio del messaggio.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Informazioni su...</th>
<th>Sono archiviati in...</th>
<th>Sono archiviati per impostazione predefinita?</th>
<th>Sono accessibili a...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Destinatari A e Cc</p></td>
<td><p>Proprietà del messaggio nelle cassette postali del mittente e dei destinatari.</p></td>
<td><p>Sì</p></td>
<td><p>Mittente, destinatari e responsabili della conformità</p></td>
</tr>
<tr class="even">
<td><p>Destinatari Ccn</p></td>
<td><p>Proprietà del messaggio nella cassetta postale del mittente.</p></td>
<td><p>Sì</p></td>
<td><p>Mittente e responsabili della conformità</p></td>
</tr>
<tr class="odd">
<td><p>Destinatari del gruppo di distribuzione espanso</p></td>
<td><p>Proprietà del messaggio nella cassetta postale del mittente.</p></td>
<td><p>No. Le informazioni relative ai destinatari del gruppo di distribuzione espanso vengono archiviate dopo aver abilitato il blocco sul posto o il blocco per controversia legale o dopo aver assegnato un criterio di conservazione di Office 365 a una cassetta postale.</p></td>
<td><p>Responsabili della conformità</p></td>
</tr>
</tbody>
</table>


## Cercare i messaggi inviati a destinatari Ccn e del gruppo di distribuzione espanso

Quando si cercano i messaggi inviati a un destinatario, i risultati della ricerca eDiscovery ora includono i messaggi inviati a un gruppo di distribuzione di cui è membro il destinatario. Nella tabella seguente vengono illustrati gli scenari in cui i messaggi inviati ai destinatari Ccn e del gruppo di distribuzione espanso sono restituiti nelle ricerche eDiscovery.

Scenario 1: John è un membro del gruppo di distribuzione Vendite USA In questa tabella sono riportati i risultati della ricerca eDiscovery quando Bob invia un messaggio a John direttamente o indirettamente tramite un gruppo di distribuzione.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Quando si effettua una ricerca nella cassetta postale di Bobper i messaggi inviati…</th>
<th>E il messaggio è inviato con...</th>
<th>I risultati includono il messaggio?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>A:John</p></td>
<td><p>John in A</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>A:John</p></td>
<td><p>Vendite USA in A</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>A: Vendite USA</p></td>
<td><p>Vendite USA in A</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Cc:John</p></td>
<td><p>John in Cc</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Cc:John</p></td>
<td><p>Vendite USA in Cc</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Cc:Vendite USA</p></td>
<td><p>Vendite USA in Cc</p></td>
<td><p>Sì</p></td>
</tr>
</tbody>
</table>


Scenario 2: Bob invia un'e-mail a John (A/Cc) e Jack (Ccn direttamente o indirettamente tramite un gruppo di distribuzione). Nella tabella seguente sono mostrati i risultati della ricerca eDiscovery.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Quando si effettua una ricerca nella...</th>
<th>Per i messaggi inviati...</th>
<th>I risultati includono il messaggio?</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cassetta postale di Bob</p></td>
<td><p>A/Cc:John</p></td>
<td><p>Sì</p></td>
<td><p>Presenta un'indicazione del fatto che Jack fosse incluso in Ccn.</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale di Bob</p></td>
<td><p>Ccn:Jack</p></td>
<td><p>Sì</p></td>
<td><p>Presenta un'indicazione del fatto che Jack fosse incluso in Ccn.</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale di Bob</p></td>
<td><p>Ccn:Jack (tramite gruppo di distribuzione)</p></td>
<td><p>Sì</p></td>
<td><p>L'elenco di membri del gruppo di distribuzione incluso in Ccn, espanso quando il messaggio è stato inviato, è visibile nell'anteprima, nell'esportazione e nei log della ricerca eDiscovery.</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale di John</p></td>
<td><p>A/Cc:John</p></td>
<td><p>Sì</p></td>
<td><p>Nessuna indicazione dei destinatari Ccn.</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale di John</p></td>
<td><p>Ccn:Jack (direttamente o tramite gruppo di distribuzione)</p></td>
<td><p>No</p></td>
<td><p>Le informazioni su Ccn non vengono archiviate nel messaggio recapitato ai destinatari. È necessario eseguire una ricerca nella cassetta postale del mittente.</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale di Jack</p></td>
<td><p>A/Cc:John (direttamente o tramite gruppo di distribuzione)</p></td>
<td><p>Sì</p></td>
<td><p>Le informazioni su A/Cc sono incluse nel messaggio recapitato a tutti i destinatari.</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale di Jack</p></td>
<td><p>Ccn:Jack (direttamente o tramite gruppo di distribuzione)</p></td>
<td><p>No</p></td>
<td><p>Le informazioni su Ccn non vengono archiviate nel messaggio recapitato ai destinatari. È necessario eseguire una ricerca nella cassetta postale del mittente.</p></td>
</tr>
</tbody>
</table>


## Domande frequenti

**D. Quando e dove vengono archiviate le informazioni dei destinatari Ccn?**  
R. Per impostazione predefinita, le informazioni dei destinatari Ccn vengono mantenute nel messaggio originale nella cassetta postale del mittente. Se il destinatario Ccn è un gruppo di distribuzione, l'appartenenza a tale gruppo viene espansa solo se è attivo un blocco sulla cassetta postale del mittente o a questa è assegnato un criterio di conservazione di Office 365.

**D. Quando e dove viene archiviato l'elenco dei destinatari del gruppo di distribuzione espanso?**  
R. L'appartenenza al gruppo viene espansa al momento dell'invio del messaggio. L'elenco dei membri del gruppo di distribuzione espanso viene archiviato nel messaggio originale nella cassetta postale del mittente. Sulla cassetta postale del mittente deve essere applicato il blocco sul posto o il blocco per controversia legale o deve essere assegnato un criterio di conservazione di Office 365.

**D. I destinatari A/Cc sono in grado di visualizzare quali destinatari sono stati inclusi come Ccn?**  
R. No. Queste informazioni non sono incluse nelle intestazioni dei messaggi e non sono visibili per i destinatari A/Cc. Il mittente può visualizzare il campo Ccn memorizzato nel messaggio originale archiviato nella cassetta postale. I responsabili della conformità possono visualizzare queste informazioni quando eseguono una ricerca nella cassetta postale del mittente.

**D. Come è possibile verificare che i destinatari del gruppo di distribuzione espanso siano sempre mantenuti?**  
R. Per verificare che i destinatari del gruppo di distribuzione espanso siano sempre mantenuti con un messaggio, [Mettere in attesa tutte le cassette postali](place-all-mailboxes-on-hold-exchange-2013-help.md) o creare un criterio di conservazione di Office 365 a livello di organizzazione.

**D. Quali tipi di gruppi sono supportati?**  
R. Sono supportati i gruppi di distribuzione, i gruppi di protezione abilitati alla posta e i gruppi di distribuzione dinamici.

**D. È previsto un limite sul numero di destinatari del gruppo di distribuzione che viene espanso e archiviato nel messaggio?**  
R. È possibile mantenere fino a 10.000 membri di un gruppo di distribuzione.

**D. I gruppi di distribuzione annidati sono supportati?**  
R. Sì, vengono espansi 25 livelli di gruppi di distribuzione annidati.

**D. Dove sono visibili le informazioni sui destinatari del gruppo di distribuzione espanso e Ccn?**  
R. Le informazioni sui destinatari del gruppo di distribuzione e Ccn sono visibili per i responsabili della conformità quando eseguono una ricerca eDiscovery. I destinatari del gruppo di distribuzione espanso e Ccn sono inclusi nei risultati di ricerca copiati in una cassetta postale di Discovery o esportati in un file PST e nel log di eDiscovery incluso nei risultati di ricerca. Le informazioni sui destinatari Ccn sono disponibili anche nell'anteprima di ricerca.

**D. Cosa succede se un membro di un gruppo di distribuzione è nascosto dall'elenco indirizzi globale (GAL) dell'organizzazione?**  
R. Non vi è nessun impatto. Se i destinatari sono nascosti dall'elenco indirizzi globale, sono comunque inclusi nell'elenco dei destinatari per il gruppo di distribuzione espanso.


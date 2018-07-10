---
title: 'Criterio di conservazione predefinito in Exchange Online ed Exchange Server: Exchange 2013 Help'
TOCTitle: Criterio di conservazione predefinito
ms:assetid: bcf31b2d-463b-4623-b488-c8ac40f14f62
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn775046(v=EXCHG.150)
ms:contentKeyID: 62625488
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criterio di conservazione predefinito in Exchange Online ed Exchange Server

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Exchange consente di creare il criterio di conservazione dei criteri di gestione record di messaggistica predefinito nel Exchange Online e Exchange organizzazione locale. Il criterio viene applicato automaticamente ai nuovi utenti in Exchange Online. Nelle organizzazioni locali, viene applicato il criterio quando si crea un archivio per la cassetta postale. È possibile modificare il criterio di conservazione applicato a un utente in qualsiasi momento.

È possibile modificare i tag inclusi nell'oggetto criterio di gestione record di messaggistica predefinito, ad esempio modificando il periodo di conservazione o le azioni di conservazione, disabilitare un tag o modificare il criterio aggiungendo o rimuovendo i tag da essa. Per le cassette postali viene applicato il criterio aggiornato alla successiva che essere state elaborate dall'Assistente cartelle gestite

## Tag di conservazione legati al criterio di Gestione record di messaggistica predefinito

Nella tabella seguente sono elencati i tag di conservazione predefiniti collegati al criterio di Gestione record di messaggistica predefinito.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Tipo</th>
<th>Periodo di validità della conservazione (giorni)</th>
<th>Azione di conservazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Spostamento nell'archivio predefinito dopo 2 anni</p></td>
<td><p>Tag criterio predefinito (DPT)</p></td>
<td><p>730</p></td>
<td><p>Sposta in archivio</p></td>
</tr>
<tr class="even">
<td><p>Spostamento degli elementi ripristinabili nell'archivio dopo 14 giorni</p></td>
<td><p>Cartella degli elementi ripristinabili</p></td>
<td><p>14</p></td>
<td><p>Sposta in archivio</p></td>
</tr>
<tr class="odd">
<td><p>Spostamento nell'archivio personale dopo 1 anno</p></td>
<td><p>Tag personale</p></td>
<td><p>365</p></td>
<td><p>Sposta in archivio</p></td>
</tr>
<tr class="even">
<td><p>Spostamento nell'archivio personale dopo 5 anni</p></td>
<td><p>Tag personale</p></td>
<td><p>1,825</p></td>
<td><p>Sposta in archivio</p></td>
</tr>
<tr class="odd">
<td><p>Nessuno spostamento nell'archivio personale</p></td>
<td><p>Tag personale</p></td>
<td><p>Non applicabile</p></td>
<td><p>Sposta in archivio</p></td>
</tr>
<tr class="even">
<td><p>Elimina dopo 1 settimana</p></td>
<td><p>Tag personale</p></td>
<td><p>7</p></td>
<td><p>Elimina e consenti ripristino</p></td>
</tr>
<tr class="odd">
<td><p>Elimina dopo 1 mese</p></td>
<td><p>Tag personale</p></td>
<td><p>30</p></td>
<td><p>Elimina e consenti ripristino</p></td>
</tr>
<tr class="even">
<td><p>Elimina dopo 6 mesi</p></td>
<td><p>Tag personale</p></td>
<td><p>180</p></td>
<td><p>Elimina e consenti ripristino</p></td>
</tr>
<tr class="odd">
<td><p>Elimina dopo 1 anno</p></td>
<td><p>Tag personale</p></td>
<td><p>365</p></td>
<td><p>Elimina e consenti ripristino</p></td>
</tr>
<tr class="even">
<td><p>Elimina dopo 5 anni</p></td>
<td><p>Tag personale</p></td>
<td><p>1,825</p></td>
<td><p>Elimina e consenti ripristino</p></td>
</tr>
<tr class="odd">
<td><p>Non eliminare mai</p></td>
<td><p>Tag personale</p></td>
<td><p>Non applicabile</p></td>
<td><p>Elimina e consenti ripristino</p></td>
</tr>
</tbody>
</table>


## Cosa può fare con il criterio di gestione record di messaggistica predefinito


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>È possibile...</th>
<th>In Exchange Online...</th>
<th>In Exchange Server...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Applicare i criteri di gestione record di messaggistica predefinito automaticamente ai nuovi utenti</p></td>
<td><p>Sì, applicata per impostazione predefinita. È necessaria alcuna azione.</p></td>
<td><p>Sì, applicata per impostazione predefinita, se si crea anche un archivio per il nuovo utente.</p>
<p>Se si crea un archivio per l'utente in seguito, il criterio viene applicato automaticamente solo se l'utente non dispone di un criterio di conservazione esistente.</p></td>
</tr>
<tr class="even">
<td><p>Modificare il periodo di conservazione o l'azione di conservazione di un tag di conservazione collegato al criterio</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Disattivare un tag di conservazione collegato al criterio</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Aggiungere un tag di conservazione per il criterio</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Rimuovere un tag di conservazione dal criterio</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Impostare un altro criterio come criterio di conservazione predefinito da applicare automaticamente ai nuovi utenti</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


## Ulteriori informazioni

  - Un Tag di conservazione possono essere collegato a uno o più criteri di conservazione. Per ulteriori informazioni sulla gestione [Tag di conservazione e criteri di conservazione](retention-tags-and-retention-policies-exchange-2013-help.md), vedere [Messaggistica Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

  - Il criterio di gestione record di messaggistica predefinito non include un tag di criteri predefinito per l'eliminazione automatica degli elementi, ma contengono i tag personali con l'azione di conservazione Elimina che gli utenti possono applicare agli elementi della cassetta postale. Se si desidera eliminare automaticamente gli elementi dopo un periodo di tempo specificato, si creare un DPT con l'azione Elimina necessari e aggiungerlo al criterio. Per ulteriori informazioni, vedere [Creare un criterio di conservazione](create-a-retention-policy-exchange-2013-help.md) e [I tag di conservazione per aggiungere o rimuovere i tag di conservazione da un criterio di conservazione](add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md).

  - I criteri di conservazione vengono applicati agli utenti della cassetta postale. Per la cassetta postale dell'utente e l'archivio si applicano gli stessi criteri.


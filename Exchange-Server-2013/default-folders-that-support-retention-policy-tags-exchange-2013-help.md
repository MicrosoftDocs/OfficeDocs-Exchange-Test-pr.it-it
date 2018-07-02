---
title: 'Cartelle predefinite che supportano i tag del criterio di conservazione: Exchange 2013 Help'
TOCTitle: Cartelle predefinite che supportano i tag del criterio di conservazione
ms:assetid: d2e2064f-4102-4018-b688-504d09da6d39
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn783294(v=EXCHG.150)
ms:contentKeyID: 62836449
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cartelle predefinite che supportano i tag del criterio di conservazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-04-20_

È possibile utilizzare [Tag di conservazione e criteri di conservazione](retention-tags-and-retention-policies-exchange-2013-help.md) per la gestione del ciclo di vita della posta elettronica. I criteri di conservazione includono tag di conservazione, vale a dire impostazioni da usare per specificare in quale momento un messaggio deve essere spostato automaticamente nell'archivio oppure quando deve essere eliminato.

Un tag di criteri di conservazione (RPT) è un tipo di tag di conservazione che può essere applicato alle cartelle predefinite di una cassetta postale, ad esempio **Posta in arrivo** ed **Elementi eliminati**.

![Creare un tag criterio di conservazione](images/Dn783294.b59a96fd-94e1-4c9b-bff6-97a1bd98dfe7(EXCHG.150).png "Creare un tag criterio di conservazione")

## Cartelle predefinite supportate

È possibile creare i tag RPT per le cartelle predefinite indicate nella tabella seguente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome della cartella</th>
<th>Dettagli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Archivio</p></td>
<td><p>Questa cartella è la destinazione predefinita per i messaggi archiviati con il pulsante Archivia in Outlook. La funzionalità di archiviazione offre un modo rapido per rimuovere messaggi dalla Posta in arrivo senza eliminarli completamente.</p>
<p>Questo RPT è disponibile soltanto in Exchange Online.</p></td>
</tr>
<tr class="even">
<td><p>Calendario</p></td>
<td><p>Questa cartella predefinita viene utilizzata per archiviare appuntamenti e riunioni.</p></td>
</tr>
<tr class="odd">
<td><p>Messaggi secondari</p></td>
<td><p>Questa cartella contiene messaggi di posta elettronica con priorità bassa. I messaggi secondari cercano le attività passate dell'utente per determinare quali messaggi è più probabile che ignorerà. Poi, sposta tali messaggi nella cartella <strong>Messaggi secondari</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Cronologia conversazione</p></td>
<td><p>Questa cartella è stata creata da Microsoft Lync (in precedenza Microsoft Office Communicator). Anche se non viene trattata come cartella predefinita da Outlook, viene trattata come cartella speciale da Exchange e può disporre dei tag RPT applicati.</p></td>
</tr>
<tr class="odd">
<td><p>Elementi eliminati</p></td>
<td><p>Questa cartella predefinita viene utilizzata per archiviare gli elementi eliminati da altre cartelle della cassetta postale. Gli utenti di Outlook e Outlook Web App possono svuotare manualmente la cartella. Gli utenti possono anche configurare Outlook in modo da svuotare la cartella al momento della chiusura di Outlook.</p></td>
</tr>
<tr class="even">
<td><p>Bozze</p></td>
<td><p>Questa cartella predefinita viene utilizzata per archiviare le bozze dei messaggi non inviati dall'utente. Outlook Web App utilizza questa cartella anche per salvare i messaggi inviati dall'utente, ma non inoltrati al server Trasporto Hub.</p></td>
</tr>
<tr class="odd">
<td><p>Posta in arrivo</p></td>
<td><p>Questa cartella predefinita viene utilizzata per archiviare i messaggi recapitati a una cassetta postale.</p></td>
</tr>
<tr class="even">
<td><p>Journal</p></td>
<td><p>Questa cartella predefinita contiene le azioni selezionate dall'utente. Queste azioni vengono registrate automaticamente da Outlook e collocate in una visualizzazione della cronologia.</p></td>
</tr>
<tr class="odd">
<td><p>Posta indesiderata</p></td>
<td><p>Questa cartella predefinita viene utilizzata per salvare i messaggi contrassegnati come posta indesiderata dal filtro contenuto su un server Exchange o dal filtro posta indesiderata in Outlook.</p></td>
</tr>
<tr class="even">
<td><p>Note</p></td>
<td><p>Questa cartella contiene le note create dagli utenti in Outlook. Queste note sono visibili anche in Outlook Web App.</p></td>
</tr>
<tr class="odd">
<td><p>Posta in uscita</p></td>
<td><p>Questa cartella predefinita viene utilizzata per archiviare i messaggi inviati dall'utente fino a quando non vengono inoltrati a un server Trasporto Hub. Una copia dei messaggi inviati viene salvata nella cartella predefinita Posta inviata. Dal momento che generalmente i messaggi rimangono in questa cartella per un breve periodo di tempo, non è necessario creare un tag RPT per questa cartella.</p></td>
</tr>
<tr class="even">
<td><p>Feed RSS</p></td>
<td><p>Questa cartella predefinita contiene i feed RSS.</p></td>
</tr>
<tr class="odd">
<td><p>Elementi recuperabili</p></td>
<td><p>Questa è una cartella nascosta nel sottoalbero non IPM. Contiene le sottocartelle Eliminazioni, Versioni, Ripuliture, Blocchi per individuazione e Controlli. I tag di conservazione per questa cartella spostano gli elementi dalla cartella Elementi ripristinabili nella cassetta principale dell'utente alla cartella Elementi ripristinabili nella sua cassetta postale di archiviazione. Ai tag in questa cartella è possibile assegnare solo le azioni di conservazione <strong>Sposta nell'archivio</strong>. Per ulteriori informazioni, vedere <a href="recoverable-items-folder-exchange-2013-help.md">Cartella Elementi ripristinabili</a>.</p></td>
</tr>
<tr class="even">
<td><p>Elementi inviati</p></td>
<td><p>Questa cartella predefinita viene utilizzata per archiviare i messaggi inviati a un server Trasporto Hub.</p></td>
</tr>
<tr class="odd">
<td><p>Problemi di sincronizzazione</p></td>
<td><p>Questa cartella contiene i registri di sincronizzazione. Per ulteriori informazioni, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=19821">Cartelle relative agli errori di sincronizzazione</a>.</p></td>
</tr>
<tr class="even">
<td><p>Attività</p></td>
<td><p>Questa cartella predefinita viene utilizzata per archiviare le attività. Per creare un RPT per la cartella Attività, è necessario utilizzare Exchange Management Shell. Per ulteriori informazioni, vedere <a href="https://technet.microsoft.com/it-it/library/dd335226(v=exchg.150)">New-RetentionPolicyTag</a>. Dopo avere creato l'RPT per la cartella Attività, è possibile gestirla utilizzando l'interfaccia di amministrazione di Exchange.</p></td>
</tr>
</tbody>
</table>


## Ulteriori informazioni

  - Gli RPT sono tag di conservazione dedicati alle cartelle predefinite. È possibile selezionare soltanto un'azione di eliminazione per RPT **eliminando e consentendo il recupero** oppure **eliminando in modo definitivo**.

  - È possibile creare un RPT per spostare i messaggi nell'archivio. Per spostare gli elementi meno recenti nell'archivio, è possibile creare un *tag Criterio predefinito* (DPT) che si applica a tutta la cassetta postale oppure *tag personali* che vengono visualizzati in Outlook e Outlook Web App (OWA) come criteri di archiviazione. Gli utenti possono applicarli alle cartelle o ai singoli messaggi.

  - Non è possibile applicare i tag RPT alla cartella Contatti.

  - È possibile aggiungere soltanto un RPT per una cartella predefinita a un criterio di conservazione. Ad esempio, se il criterio di conservazione ha un tag Posta in arrivo, non è possibile aggiungere un altro RPT oppure il tipo Posta in arrivo a quel criterio di conservazione.

  - Per informazioni su come creare RPT o altri tipi di tag di conservazione e su come aggiungerli a un criterio di conservazione, vedere [Creare un criterio di conservazione](create-a-retention-policy-exchange-2013-help.md).

  - In Exchange 2013 e Exchange Online, alle cartelle predefinite **Calendario** e **Attività** viene applicato un tag del criterio predefinito (DPT). Ciò potrebbe causare l'eliminazione o lo spostamento di elementi nell'archivio in base alle impostazioni DPT. Per impedire che le impostazioni DTP causino l'eliminazione degli elementi in queste cartelle, creare RPT con la conservazione disabilitata. Per impedire che le impostazioni DPT causino lo spostamento di elementi in una cartella predefinita, è possibile creare un tag personale disabilitato con l'azione di spostamento nell'archivio, aggiungerlo al criterio di conservazione e poi permettere agli utenti di applicarlo alla cartella predefinita. Per i dettagli, vedere [Impedire l'archiviazione degli elementi in una cartella predefinita di Exchange 2010](https://go.microsoft.com/fwlink/?linkid=51107).


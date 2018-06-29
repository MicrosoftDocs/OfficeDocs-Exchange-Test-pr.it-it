---
title: 'Formati di file indicizzati da ricerca di Exchange: Exchange 2013 Help'
TOCTitle: Formati di file indicizzati da ricerca di Exchange
ms:assetid: e5110ac1-28e1-4554-acc3-85d08c997bc5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633485(v=EXCHG.150)
ms:contentKeyID: 52063137
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Formati di file indicizzati da ricerca di Exchange

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-07-21_

In MicrosoftExchange Server 2013 e Exchange Online, Ricerca di Exchange include filtri per l'indicizzazione dei tipi più comuni di formati di file come allegati ai messaggi. È inoltre possibile installare filtri per indicizzare altri tipi di file.


> [!NOTE]
> In Exchange 2013, non è necessario installare e registrare Microsoft Office Filter Pack.<BR>Per impostazione predefinita, la dimensione massima del file che possono essere indicizzati da Exchange Server 2013 locale è 32 MB. Per aumentare le dimensioni massime, è necessario aggiungere la chiave del Registro di sistema seguente in tutti i server accesso client e server con più ruoli all'interno dell'organizzazione:<BR><CODE>@"SOFTWARE\Microsoft\ExchangeServer\V15\Search\SystemParameters" DWORD: "MaxAttachmentSize"</CODE>



Quando si gestisce o si utilizza Ricerca di Exchange e le funzionalità dipendenti (come [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md)), tenere presente la differenza tra elementi non ricercabili e formati di file disabilitati per l'indicizzazione o con contenuto non indicizzabile.

  - **Elementi non ricercabili**   Se la ricerca di Exchange non è in grado di indicizzare un particolare tipo di file per qualsiasi ragione (ad esempio se un filtro non è installato), la ricerca per quel tipo di file ha esito negativo. Messaggi contenenti allegati contrassegnati come *parzialmente indicizzati*. Gli elementi non ricercabili possono essere recuparati tramite il cmdlet [Get-FailedContentIndexDocuments](https://technet.microsoft.com/it-it/library/dd351154\(v=exchg.150\)). Quando si copiano i risultati della ricerca di eDiscovery sul posto in una cassetta postale di individuazione o si riportano i risultati della ricerca in un file PST, è possibile includere elementi non ricercabili. Per ulteriori informazioni, vedere [Elementi non ricercabili in Exchange eDiscovery](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

  - **Formati di file che non possono essere indicizzati**   Alcuni tipi di file come Windows Media Video (WMV) non presentano contenuto che può essere indicizzato e pertanto non sono indicizzati. I messaggi contenenti allegati di questi tipo di file vengono restituiti anche come elementi senza funzioni di ricerca nelle ricerche di eDiscovery sul posto.

  - **Formati di file disabilitati** Nelle organizzazioni locali, un amministratore può disabilitare l'indicizzazione di uno specifico formato di file. I messaggi contenenti un allegato in un formato disabilitato vengono restituiti come elementi senza funzioni di ricerca.


> [!IMPORTANT]
> Anche se un allegato non presenta funzioni di ricerca o è in un formato di file che non può essere indicizzato, l'oggetto, il corpo e altri metadati del messaggio possono essere indicizzati in modo che il messaggio venga restituito nelle ricerche.



Per ulteriori attività di gestione correlate a Ricerca di Exchange nelle organizzazioni locali, vedere [Exchange Search procedures](exchange-search-procedures-exchange-2013-help.md).

## Filtri predefiniti

Nella seguente tabella sono elencati i filtri di ricerca predefiniti installati su un server Cassette postali di Exchange 2013 e in Exchange Online. È possibile recuperare l'elenco di filtri predefiniti utilizzando il cmdlet [Get-SearchDocumentFormat](https://technet.microsoft.com/it-it/library/jj873755\(v=exchg.150\)).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Filtro</th>
<th>Estensione del file</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Messaggio di posta elettronica</p></td>
<td><p>.eml</p></td>
</tr>
<tr class="even">
<td><p>GIF (Graphics Interchange Format)</p></td>
<td><p>.gif</p></td>
</tr>
<tr class="odd">
<td><p>JPEG</p></td>
<td><p>.jpeg</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Excel</p></td>
<td><p>.xls, .xlt, .xlsx, .xlsm, .xlb, .xlc, .xlsb</p></td>
</tr>
<tr class="odd">
<td><p>File di Excel</p></td>
<td><p>odbcexcel</p></td>
</tr>
<tr class="even">
<td><p>Microsoft InfoPath</p></td>
<td><p>.infopathml</p></td>
</tr>
<tr class="odd">
<td><p>Raccoglitore di Microsoft Office</p></td>
<td><p>.obt, obd</p></td>
</tr>
<tr class="even">
<td><p>Microsoft PowerPoint</p></td>
<td><p>.pptx, .pptm, .ppt, .ppsx, .ppsm, .pps, .ppam, .potm, .pot, .potx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Publisher</p></td>
<td><p>.pub</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Word</p></td>
<td><p>.doc, .docm, .dotx, .dotm, .dot, .docx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft XML Paper Specification</p></td>
<td><p>.xps</p></td>
</tr>
<tr class="even">
<td><p>OneNote</p></td>
<td><p>.one</p></td>
</tr>
<tr class="odd">
<td><p>Presentazione OpenDocument</p></td>
<td><p>.odp</p></td>
</tr>
<tr class="even">
<td><p>Foglio di calcolo OpenDocument</p></td>
<td><p>.ods</p></td>
</tr>
<tr class="odd">
<td><p>Testo OpenDocument</p></td>
<td><p>.odt</p></td>
</tr>
<tr class="even">
<td><p>Elemento di Outlook</p></td>
<td><p>.msg</p></td>
</tr>
<tr class="odd">
<td><p>PDF (Portable Document Format)</p></td>
<td><p>.pdf</p></td>
</tr>
<tr class="even">
<td><p>Rich Text</p></td>
<td><p>.rtf</p></td>
</tr>
<tr class="odd">
<td><p>Testo</p></td>
<td><p>.txt</p></td>
</tr>
<tr class="even">
<td><p>vCalendar</p></td>
<td><p>.vcs</p></td>
</tr>
<tr class="odd">
<td><p>vCard</p></td>
<td><p>.vcf</p></td>
</tr>
<tr class="even">
<td><p>Visio</p></td>
<td><p>.vdw, .vsd, .vss, .vst, .vsx, .vtx, .vssx, .vssm, .vsdm, .vstx, .vstm, .vdx</p></td>
</tr>
<tr class="odd">
<td><p>Archivio Web</p></td>
<td><p>.mhtml</p></td>
</tr>
<tr class="even">
<td><p>Pagina Web</p></td>
<td><p>.html</p></td>
</tr>
<tr class="odd">
<td><p>Documento XML</p></td>
<td><p>.xml</p></td>
</tr>
<tr class="even">
<td><p>Archivio ZIP</p></td>
<td><p>.zip</p></td>
</tr>
</tbody>
</table>


## Formati di file disabilitati

Nella seguente tabella sono elencati i filtri di ricerca disabilitati per l'indicizzazione per impostazione predefinita in un server Cassette postali di Exchange 2013 e in Exchange Online. In Exchange 2013, gli amministratori possono disattivare o riattivare un formato di file supportato per l'indicizzazione, utilizzando il cmdlet [Set-SearchDocumentFormat](https://technet.microsoft.com/it-it/library/jj873756\(v=exchg.150\)). Il cmdlet non è disponibile in Exchange Online.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Filtro</th>
<th>Estensione del file</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AVI</p></td>
<td><p>.avi</p></td>
</tr>
<tr class="even">
<td><p>Bitmap</p></td>
<td><p>.bmp</p></td>
</tr>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>.mp3</p></td>
</tr>
<tr class="even">
<td><p>MPEG</p></td>
<td><p>.mpeg</p></td>
</tr>
<tr class="odd">
<td><p>PNG</p></td>
<td><p>.png</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Windows Wave Audio</p></td>
<td><p>.wav</p></td>
</tr>
</tbody>
</table>


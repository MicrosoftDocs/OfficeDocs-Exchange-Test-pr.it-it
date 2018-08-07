---
title: 'Regole trasporto per esaminare messaggi con allegati: Exchange 2013 Help'
TOCTitle: Utilizzare le regole di trasporto per esaminare messaggi con allegati
ms:assetid: c0de687e-e33c-4e8a-b253-771494678795
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ674307(v=EXCHG.150)
ms:contentKeyID: 50481576
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzare le regole di trasporto per esaminare messaggi con allegati

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-27_

È possibile esaminare gli allegati di posta elettronica nell'organizzazione configurando le regole di trasporto. Exchange offre regole di trasporto che consentono la possibilità di esaminare allegati di posta elettronica come parte della protezione dei messaggi e requisiti di conformità. Quando si esaminano gli allegati, è possibile agire sui messaggi esaminati in base al contenuto o alle caratteristiche di tali allegati. Ecco alcune attività relative agli allegati che si possono eseguire tramite l'utilizzo delle regole di trasporto:

  - Ricercare file in allegati compressi come file .zip e .rar, e se c'è un qualsiasi testo che corrisponde a un modello specificato, aggiungere una dichiarazione di non responsabilità alla fine del messaggio.

  - Esaminare il contenuto all'interno degli allegati, nel caso ci sia una qualsiasi parola chiave specificata, reindirizzare il messaggio ad un moderatore per l'approvazione prima che venga distribuito.

  - Controllare i messaggi con allegati che non possono essere esaminati e quindi bloccare l'invio dell'intero messaggio.

  - Controllare gli allegati che eccedono una certa dimensione e quindi notificare l'informazione al mittente nel caso si scelga di impedirne l'invio.

  - Creare notifiche che avvisino gli utenti se inviano un messaggio che corrisponde a una regola di trasporto.

  - Consente di bloccare tutti i messaggi contenenti allegati. Per esempi, vedere [Scenari comuni relativi al blocco degli allegati](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md).

Gli amministratori di Exchange possono creare regole di trasporto andando su **Exchange Admin Center** \> **Flusso di posta** \> **Regole**. È necessario disporre delle autorizzazioni prima di poter eseguire questa procedura. Dopo aver creato una nuova regola, è possibile visualizzare l'elenco completo di condizioni relative agli allegati facendo clic su **Altre opzioni** \> **Qualsiasi allegato** sotto **Applica questa regola se**. Le opzioni relative agli allegati sono mostrate nel seguente diagramma.

![Finestra di dialogo per selezionare le regole correlate agli allegati](images/JJ674307.2ae4a179-bfd2-4a0e-abe1-53ed4e9e3368(EXCHG.150).jpg "Finestra di dialogo per selezionare le regole correlate agli allegati")

Per ulteriori informazioni sulle regole di trasporto, inclusa la gamma completa di condizioni e azioni tra cui scegliere, vedere [Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md). Exchange Online Protection (EOP) e clienti ibridi possono beneficiare delle migliori regole di trasporto fornite in [Procedure consigliate per la configurazione di EOP](https://technet.microsoft.com/it-it/library/jj723164\(v=exchg.150\)). Se si è pronti per creare regole, vedere [Gestire le regole di flusso di posta elettronica](manage-mail-flow-rules-exchange-2013-help.md).

## Esaminare il contenuto all'interno di allegati

Si possono utilizzare le condizioni di regole di trasporto nella tabella seguente per esaminare il contenuto degli allegati dei messaggi. Per queste condizioni, solo i primi 150 KB di un allegato vengono esaminati. Per iniziare a utilizzare queste condizioni quando si esaminano i messaggi, è necessario aggiungerle a una regola di trasporto. Informazioni su come imparare o modificare regole su [Gestire le regole di flusso di posta elettronica](manage-mail-flow-rules-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome della condizione nell'interfaccia di amministrazione di Exchange</th>
<th>Nome della condizione in Shell</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Il contenuto di un allegato include una o più delle seguenti parole</strong></p></td>
<td><p><code>AttachmentContainsWords</code></p></td>
<td><p>Questa condizione cerca una corrispondenza con i messaggi a cui sono allegati tipi di file supportati contenenti una stringa o un gruppo di caratteri specificati.</p></td>
</tr>
<tr class="even">
<td><p><strong>Il contenuto di un allegato corrisponde a questi modelli di testo</strong></p></td>
<td><p><code>AttachmentMatchesPatterns</code></p></td>
<td><p>Questa condizione genera una corrispondenza per i messaggi a cui sono allegati tipi di file supportati che contengono un modello di testo che corrisponde a un'espressione regolare specificata.</p></td>
</tr>
</tbody>
</table>


I nomi Exchange Management Shell per le condizioni qui elencate sono parametri che richiedono il cmdlet `TransportRule`

  -  Per ulteriori informazioni sul cmdlet, vedere [New-TransportRule](https://technet.microsoft.com/it-it/library/bb125138\(v=exchg.150\)).

  -  Per ulteriori informazioni sui tipi di proprietà per queste condizioni su [Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

Le regole di trasporto possono esaminare solo il contenuto dei tipi di file supportati. Se l'agente delle regole di trasporto rileva un allegato non incluso nell'elenco dei tipi di file supportati, viene attivata la condizione `AttachmentIsUnsupported`. I tipi di file supportati sono elencati nella sezione seguente. I file non elencati attiveranno la condizione `AttachmentIsUnsupported`.

## File di archivio compressi

Se il messaggio contiene un file di archivio compresso quale un file .zip o .cab, l'agente delle regole di trasporto esaminerà i file contenuti nell'allegato. Tali messaggi vengono elaborati in modo simile ai messaggi con più allegati. Le proprietà dei file di archivio compressi non sono esaminate. Se ad esempio il tipo di file del contenitore supporta i commenti, il campo non viene esaminato.

## Tipi di file supportati per esaminare le regole di trasporto

Nella tabella seguente sono elencati i tipi di file supportati dalle regole di trasporto. Il sistema usa il rilevamento automatico di tipi di file attraverso l'ispezione delle proprietà dei file invece che dell'estensione effettiva del file, impedendo in questo modo ad hacker malintenzionati di superare il filtro delle regole di trasporto rinominando l'estensione del file. Un elenco di tipi di file con codici eseguibili che possono essere controllati nel contesto delle regole di trasporto viene riportato successivamente in questo argomento.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Category</th>
<th>Estensione del file</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Office 2013, Office 2010 e Office 2007</p></td>
<td><p>.docm, .docx, .pptm, .pptx, .pub, .one, .xlsb, .xlsm, .xlsx</p></td>
<td><p>Per impostazione predefinita non sono supportati i file Microsoft OneNote e Microsoft Publisher, anche se è possibile abilitarne il supporto con l'integrazione IFilter. Per ulteriori informazioni, vedere <a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">Registrazione dei IFilter di Filter Pack con Exchange 2013</a>.</p>
<p>Anche il contenuto delle parti incorporate comprese in questi tipi di file viene esaminato. Tuttavia, gli oggetti che non sono incorporati, ad esempio i documenti collegati, non vengono esaminati.</p></td>
</tr>
<tr class="even">
<td><p>Office 2003</p></td>
<td><p>.doc, .ppt, .xls</p></td>
<td><p>None</p></td>
</tr>
<tr class="odd">
<td><p>Ulteriori file di Office</p></td>
<td><p>.rtf, .vdw, .vsd, .vss, .vst</p></td>
<td><p>None</p></td>
</tr>
<tr class="even">
<td><p>Adobe PDF</p></td>
<td><p>.pdf</p></td>
<td><p>None</p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p>.html</p></td>
<td><p>None</p></td>
</tr>
<tr class="even">
<td><p>XML</p></td>
<td><p>.xml, .odp, .ods, .odt</p></td>
<td><p>None</p></td>
</tr>
<tr class="odd">
<td><p>Testo</p></td>
<td><p>.txt, .asm, .bat, .c, .cmd, .cpp, .cxx, .def, .dic, .h, .hpp, .hxx, .ibq, .idl, .inc, inf, .ini, inx, .js, .log, .m3u, .pl, .rc, .reg, .txt, .vbs, .wtx</p></td>
<td><p>None</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument</p></td>
<td><p>.odp, .ods, .odt</p></td>
<td><p>Non vengono elaborate parti di file .odf. Se, ad esempio, il file .odf contiene un documento incorporato, il contenuto del documento non viene esaminato.</p></td>
</tr>
<tr class="odd">
<td><p>Disegno di AutoCAD</p></td>
<td><p>.dxf</p></td>
<td><p>Non sono supportati i file AutoCAD 2013.</p></td>
</tr>
<tr class="even">
<td><p>Immagine</p></td>
<td><p>.jpg, .tiff</p></td>
<td><p>Solo il testo dei metadati associato a questi file di immagine viene esaminato. Non è prevista alcun riconoscimento ottico dei caratteri.</p></td>
</tr>
</tbody>
</table>


## Esaminare le proprietà del file degli allegati

La seguente condizione di regola di trasporto esamina le proprietà di un file allegato a un messaggio. Per iniziare a utilizzare queste condizioni quando si esaminano i messaggi, è necessario aggiungerle a una regola di trasporto. Un elenco di tipi di file con codici eseguibili che possono essere controllati nel contesto delle regole di trasporto è qui riportato. Per ulteriori informazioni sulla creazione o la modifica di regole di trasporto, vedere [Gestire le regole di flusso di posta elettronica](manage-mail-flow-rules-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome della condizione nell'interfaccia di amministrazione di Exchange</th>
<th>Nome della condizione in Shell</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Qualsiasi nome di allegato del file corrisponde a questi modelli di testo</strong></p></td>
<td><p><code>AttachmentNameMatchesPatterns</code></p></td>
<td><p>Questa condizione corrisponde a messaggi a cui sono allegati tipi di file supportati quando detti allegati hanno un nome che contiene i caratteri specificati.</p></td>
</tr>
<tr class="even">
<td><p><strong>Qualsiasi estensione di file allegato include queste parole</strong></p></td>
<td><p><code>AttachmentExtensionMatchesWords</code></p></td>
<td><p>Questa condizione corrisponde a messaggi a cui sono allegati tipi di file supportati quando l'estensione del nome del file corrisponde con quello specificato.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Qualsiasi allegato è maggiore o uguale a</strong></p></td>
<td><p><code>AttachmentSizeOver</code></p></td>
<td><p>Questa condizione corrisponde a messaggi a cui sono allegati tipi di file supportati quando quegli allegati sono più grandi delle dimensioni specificate.</p></td>
</tr>
<tr class="even">
<td><p><strong>Gli allegati non hanno completato la scansione</strong></p></td>
<td><p><code>AttachmentProcessingLimitExceeded</code></p></td>
<td><p>Questa condizione corrisponde ai messaggi quando un allegato non viene esaminato dall'agente delle regole di trasporto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>L'allegato ha contenuto eseguibile</strong></p></td>
<td><p><code>AttachmentHasExecutableContent</code></p></td>
<td><p>Questa condizione genera una corrispondenza per i messaggi che contengono file eseguibili come allegati. Di seguito sono elencati i tipi di file supportati.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tutti gli allegati sono protetti da password</strong></p></td>
<td><p><code>AttachmentIsPasswordProtected</code></p></td>
<td><p>Questa condizione corrisponde a messaggi a cui sono allegati tipi di file supportati quando quegli allegati sono protetti da password.</p></td>
</tr>
</tbody>
</table>


I nomi Exchange Management Shell per le condizioni qui elencate sono parametri che richiedono il cmdlet `TransportRule`

  -  Per ulteriori informazioni sul cmdlet, vedere [New-TransportRule](https://technet.microsoft.com/it-it/library/bb125138\(v=exchg.150\)).

  -  Per ulteriori informazioni sui tipi di proprietà per queste condizioni su [Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

## Tipi di file eseguibili supportati per esaminare le regole di trasporto

L'agente di trasporto utilizza il rilevamento True Type verificando le proprietà del file invece delle estensioni. In questo modo si impedisce ad hacker malintenzionati di ignorare la regola rinominando un'estensione di file. Nella tabella seguente sono elencati i tipi di file eseguibili supportati da queste condizioni. Se viene trovato un file non elencato qui, viene attivata la condizione `AttachmentIsUnsupported`.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di file</th>
<th>Estensione nativa</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>File di archivio autoestraente creato con l'archiviazione WinRAR.</p></td>
<td><p>.rar</p></td>
</tr>
<tr class="even">
<td><p>File eseguibile di Windows a 32 bit con estensione di libreria di collegamento dinamico.</p></td>
<td><p>.dll</p></td>
</tr>
<tr class="odd">
<td><p>File di programma eseguibile autoestraente.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>File di archivio Java.</p></td>
<td><p>.jar</p></td>
</tr>
<tr class="odd">
<td><p>File eseguibile di disinstallazione.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>File di collegamento del programma.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>File di codice sorgente compilato o file oggetto 3D o file di sequenza.</p></td>
<td><p>.obj</p></td>
</tr>
<tr class="even">
<td><p>File eseguibile di Windows a 32 bit.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>File di disegno di Microsoft Visio XML.</p></td>
<td><p>.vxd</p></td>
</tr>
<tr class="even">
<td><p>File del sistema operativo OS/2.</p></td>
<td><p>.os2</p></td>
</tr>
<tr class="odd">
<td><p>File eseguibile di Windows a 16 bit.</p></td>
<td><p>.w16</p></td>
</tr>
<tr class="even">
<td><p>File di sistema operativo su disco.</p></td>
<td><p>.dos</p></td>
</tr>
<tr class="odd">
<td><p>File di test di virus dello standard dello European Institute for Computer Antivirus Research.</p></td>
<td><p>.com</p></td>
</tr>
<tr class="even">
<td><p>File di informazioni del programma di Windows.</p></td>
<td><p>.pif</p></td>
</tr>
<tr class="odd">
<td><p>File di programma eseguibile di Windows.</p></td>
<td><p>.exe</p></td>
</tr>
</tbody>
</table>


## Estensione del numero dei tipi di file supportati

I tipi di file supportati elencati in questo argomento possono essere rivisti in qualsiasi momento utilizzando l'integrazione di IFilter. Per ulteriori informazioni, vedere [Registrazione dei IFilter di Filter Pack con Exchange 2013](register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md).

I tipi di file aggiunti utilizzando il processo diventano supportati e non attivano più la condizione `AttachmentIsUnsupported`.

## Criteri di prevenzione della perdita di dati e regole di trasporto degli allegati

Per gestire più facilmente informazioni importanti aziendali nella posta elettronica, è possibile includere qualsiasi delle condizioni relative agli allegati insieme con le regole di un criterio di prevenzione della perdita di dati (DLP). Per esempio, si potrebbe consentire l'invio di messaggi con numeri di passaporto solo se questi si trovano in un allegato protetto da password. A tale scopo, effettuare le seguenti operazioni:

  - Creare un criterio di prevenzione della perdita di dati (DLP) che esamini la posta elettronica alla ricerca di dati sensibili relativi al passaporto. Per ulteriori informazioni, vedere [Procedure DLP](dlp-procedures-exchange-2013-help.md).

  - Aggiungere l'eccezione **Tutti gli allegati sono protetti da password** nell'area della regola di trasporto **Tranne se…**

  - Definire una misura da adottare per la posta che contiene numeri di passaporto che non sono in file protetti.

Criteri di prevenzione della perdita di dati (DLP) e condizioni relative agli allegati possono soddisfare maggiormente le necessità aziendali definendo quelle condizioni delle regole di trasporto, eccezioni e azioni. Includendo l'ispezione di dati sensibili in un criterio di prevenzione della perdita di dati (DLP), tutti gli allegati vengono esaminati solo per quel dato richiesto. Tuttavia, le condizioni relative agli allegati come dimensione e tipo di file, non sono incluse fintantoché non vengano aggiunte le condizioni elencate in questo argomento. Criteri di prevenzione della perdita di dati non sono disponibili con tutte le versioni di Exchange; per ulteriori informazioni, vedere [Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md).

## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Condizioni delle regole di trasporto (predicati)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/it-it/library/jj919236\(v=exchg.150\)) in Exchange Online


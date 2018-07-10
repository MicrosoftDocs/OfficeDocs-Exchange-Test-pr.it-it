---
title: 'Cassetta postale di importare ed esportare le richieste: Exchange 2013 Help'
TOCTitle: Cassetta postale di importare ed esportare le richieste
ms:assetid: 157a7d88-d3aa-4056-9a50-df67451b14be
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633455(v=EXCHG.150)
ms:contentKeyID: 50480098
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cassetta postale di importare ed esportare le richieste

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Utilizzando il cmdlet **MailboxImportRequest** o **MailboxExportRequest** imposta in Exchange Management Shell, è possibile importare dati da o esportare dati nei file. pst. Dopo aver avviare un'importazione delle cassette postali o esportare richiesta, il completamento del processo asincrono dal servizio di replica delle cassette postali (MRS) Microsoft Exchange. MRS si trova in tutti i server Accesso Client Exchange 2010 e del servizio di responsabile per lo spostamento delle cassette postali e importazione ed esportazione di file con estensione pst.

**Sommario**

Reasons to import or export mailbox data

Advantages to using import and export requests

Considerations

Importing mailbox data

Exporting mailbox data

## Motivi per importare o esportare i dati delle cassette postali

Si potrebbe voler importare o esportare dati delle cassette postali per i seguenti motivi:

  - **Soddisfare i requisiti di conformità**   È possibile esportare il contenuto di una cassetta postale in un file .pst per l'esibizione di documenti probatori. Una volta completata l'esportazione, è possibile importare il contenuto di una cassetta postale speciale utilizzata per motivi di conformità.

  - **Creare un'istantanea della cassetta postale in un determinato momento**   È possibile creare un'istantanea per determinate cassette postali per evitare di dover conservare l'intero set di backup per un database delle cassette postali.

  - **Spostare il file .pst di un utente nella sua cassetta postale o nel suo archivio personale**   Gli utenti di Microsoft Outlook possono salvare in locale i loro messaggi di posta elettronica come file .pst. Utilizzando il cmdlet [New-MailboxImportRequest](https://technet.microsoft.com/it-it/library/ff607310\(v=exchg.150\)), è possibile spostare i dati dal file .pst file di un utente nella sua cassetta postale o nel suo archivio personale. Si tratta di un metodo semplice per trasferire i messaggi di posta elettronica dal computer locale dell'utente ai server Exchange.

## Vantaggi legati all'utilizzo delle richieste di importazione ed esportazione

I vantaggi legati all'utilizzo delle richieste di importazione ed esportazione in Exchange 2013 includono i seguenti:

  - In Exchange 2013 è incluso un provider .pst in grado di leggere e scrivere i file .pst.

  - Le richieste di importazione ed esportazione sono asincrone. Il processo è eseguito dal servizio di replica delle cassette postali che si avvale degli ambiti funzionali di limitazione e accodamento.

  - I file .pst possono essere importati direttamente nell'archivio personale dell'utente.

  - È possibile importare o esportare contemporaneamente più file .pst.

  - I file .pst possono essere salvati su qualsiasi unità di rete condivisa accessibile dai server Exchange.

  - Exchange 2013supporta questi file .pst: File Unicode creati da Office Outlook 2007 e Outlook 2010

## Considerazioni

Prima di importare o esportare i dati delle cassette postali, tenere presente quanto segue:

  - Per importare o esportare i dati delle cassette postali, è necessario configurare una cartella di rete condivisa alla quale possano accedere i server Exchange. È altresì necessario concedere al sottogruppo Sottosistema attendibile Exchange l'autorizzazione di lettura/scrittura in modo che il gruppo possa accedere alla condivisione di rete dove i dati verranno importati ed esportati. Se questa autorizzazione non viene concessa, si riceverà un messaggio di errore che segnala che Exchange non è in grado di stabilire una connessione alla cassetta postale di destinazione.

  - La dimensione massima supportata da Outlook per il file .pst è 50 GB. Di conseguenza, è consigliabile non importare file .pst la cui dimensione sia superiore a 50 GB. È possibile creare più file .pst per le cassette postali la cui dimensione supera i 50 GB. Per fare ciò, specificare le singole cartelle da includere o escludere oppure utilizzare un filtro per il contenuto.

  - Le richieste di importazione ed esportazione vengono eseguite dal servizio di replica delle cassette postali che elabora anche le richieste di spostamento e ripristino delle cassette postali. Tutte le richieste vengono accodate e limitate dal servizio di replica delle cassette postali.

  - Le operazioni di importazione ed esportazione dei dati delle cassette postali possono durare diverse ore; il tempo necessario dipende dalla dimensione del file, dalla larghezza di banda e dalla limitazione del servizio di replica delle cassette postali.

  - Non è possibile importare i dati in una cartella pubblica o nel database delle cartelle pubbliche.

## Importazione dei dati delle cassette postali

Utilizzare il cmdlet **MailboxImportRequest** per importare dati da un file .pst in una cassetta postale o un archivio personale. Di seguito viene fornito un elenco delle opzioni che è possibile specificare quando si importano i dati delle cassette postali da un file .pst:


> [!NOTE]
> La cassetta postale in cui si importano i dati deve esistere. Non è possibile importare i dati in un account utente che non dispone di una cassetta postale.



  - È possibile importare i dati in un account utente diverso da quello da cui sono stati esportati. Ad esempio, è possibile esportare i dati da john@contoso.com e importarli in legaldiscovery@contoso.com.

  - Per importare gli elementi solo nell'archivio personale dell'utente, specificare il parametro *IsArchive*.

  - Se nel file .pst sono presenti messaggi associati alla cartella, è possibile importarli utilizzando il parametro *AssociatedMessagesCopyOption*. I messaggi associati contengono i dati nascosti con informazioni sulle regole, le visualizzazioni e i moduli. Se esistono nel file .pst, vengono importati tutti i messaggi dalla rete sicura.

  - È possibile includere o escludere specifiche cartelle utilizzando il parametro *IncludeFolders* o *ExcludeFolders*.

  - È possibile escludere la cartella Elementi ripristinabili utilizzando il parametro *ExcludeDumpster*. Per impostazione predefinita, una richiesta di importazione include la cartella Elementi ripristinabili dell'utente se è presente nel file .pst.

## Cmdlet di richiesta di importazione della cassetta postale

Utilizzare i seguenti cmdlet per le richieste di importazione delle cassette postali.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607310(v=exchg.150)">New-MailboxImportRequest</a></p></td>
<td><p>Consente di avviare il processo di importazione di un file .pst in una cassetta postale o un archivio personale. È possibile creare più richieste di importazione per ciascuna cassetta postale. Ciascuna richiesta deve avere un nome univoco.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607317(v=exchg.150)">Set-MailboxImportRequest</a></p></td>
<td><p>Consente di modificare le opzioni della richiesta di importazione dopo che è stata creata o di recuperare una richiesta non riuscita.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607309(v=exchg.150)">Suspend-MailboxImportRequest</a></p></td>
<td><p>Consente di sospendere una richiesta di importazione di cassette postali in qualsiasi momento dopo la sua creazione, ma prima del suo completamento.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607306(v=exchg.150)">Resume-MailboxImportRequest</a></p></td>
<td><p>Consente di riprendere una richiesta di importazione sospesa o non riuscita.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607311(v=exchg.150)">Remove-MailboxImportRequest</a></p></td>
<td><p>Consente di rimuovere le richieste di importazione completate almeno parzialmente. Le richieste di importazione completate non vengono cancellate automaticamente. È necessario utilizzare questo cmdlet per eliminarle.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607368(v=exchg.150)">Get-MailboxImportRequest</a></p></td>
<td><p>Consente di visualizzare informazioni generiche su una richiesta di importazione.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607315(v=exchg.150)">Get-MailboxImportRequestStatistics</a></p></td>
<td><p>Consente di visualizzare informazioni dettagliate su una richiesta di importazione.</p></td>
</tr>
</tbody>
</table>


## Esportazione dei dati delle cassette postali

Utilizzare il gruppo di cmdlet **MailboxExportRequest** per esportare i dati delle cassette postali in un file .pst. È possibile esportare una o più cassette postali, ma su ciascun file .pst viene scritta una sola richiesta alla volta. Di seguito viene fornito un elenco delle opzioni che è possibile specificare quando si esportano i dati delle cassette postali in un file .pst:

  - È possibile esportare i dati degli archivi personali utilizzando il parametro *IsArchive*.

  - È possibile filtrare le richieste esportate utilizzando il parametro *ContentFilter*. È possibile filtrare i messaggi per contenuto, allegati, mittenti, destinatari, categoria Posta in arrivo, importanza, tipologia, dimensione, data e ora di invio, ricezione e scadenza.

  - È possibile specificare le cartelle da includere o escludere utilizzando il parametro *IncludeFolders* o *ExcludeFolders*. Se si esportano i dati da una cassetta postale di Exchange 2013, è anche possibile escludere la cartella Elementi ripristinabili utilizzando il parametro *ExcludeDumpster*.

  - È possibile esportare i messaggi associati utilizzando il parametro *AssociatedMessagesCopyOption*. I messaggi associati contengono i dati nascosti con informazioni sulle regole, le visualizzazioni e i moduli. Per impostazione predefinita, gli elementi associati non vengono copiati nel file .pst.

## Cmdlet di richiesta di esportazione della cassetta postale

Utilizzare i seguenti cmdlet per le richieste di esportazione delle cassette postali.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607299(v=exchg.150)">New-MailboxExportRequest</a></p></td>
<td><p>Consente di avviare il processo di esportazione di una cassetta postale o un archivio personale in un file .pst. È possibile creare più richieste di esportazione per ciascuna cassetta postale. Ciascuna richiesta deve avere un nome univoco.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607312(v=exchg.150)">Set-MailboxExportRequest</a></p></td>
<td><p>Consente di modificare le opzioni della richiesta di esportazione dopo che è stata creata o di recuperare una richiesta non riuscita.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607305(v=exchg.150)">Suspend-MailboxExportRequest</a></p></td>
<td><p>Consente di sospendere una richiesta di esportazione di cassette postali in qualsiasi momento dopo la sua creazione, ma prima del suo completamento.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607476(v=exchg.150)">Resume-MailboxExportRequest</a></p></td>
<td><p>Consente di riprendere una richiesta di esportazione sospesa o non riuscita.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607464(v=exchg.150)">Remove-MailboxExportRequest</a></p></td>
<td><p>Consente di rimuovere le richieste di esportazione completate almeno parzialmente. Le richieste di esportazione completate non vengono cancellate automaticamente. È necessario utilizzare questo cmdlet per eliminarle.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607479(v=exchg.150)">Get-MailboxExportRequest</a></p></td>
<td><p>Consente di visualizzare informazioni generiche su una richiesta di esportazione.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/ff607316(v=exchg.150)">Get-MailboxExportRequestStatistics</a></p></td>
<td><p>Consente di visualizzare informazioni dettagliate su una richiesta di esportazione.</p></td>
</tr>
</tbody>
</table>


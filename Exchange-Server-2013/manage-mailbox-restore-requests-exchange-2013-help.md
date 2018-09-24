---
title: 'Gestire le richieste di ripristino delle cassette postali: Exchange 2013 Help'
TOCTitle: Gestire le richieste di ripristino delle cassette postali
ms:assetid: 8e668a52-c601-4d96-a51c-ab60267e1321
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ863437(v=EXCHG.150)
ms:contentKeyID: 50555624
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire le richieste di ripristino delle cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Le richieste di ripristino delle cassette postali sono utilizzate per ripristinare le cassette postali disconnesse. Una cassetta postale disconnessa è una cassetta postale nel database delle cassette postali di Exchange non associata a un account utente in Active Directory. Le cassette postali vengono disconnesse quando vengono disabilitate, eliminate o spostate in un database diverso. Per ulteriori informazioni, vedere [Cassette postali disconnesse](disconnected-mailboxes-exchange-2013-help.md).

Le cassette postali disconnesse rimangono nel database delle cassette postali per il periodo di tempo specificato nelle impostazioni di conservazione delle cassette postali eliminate relative al database delle cassette postali. Per impostazione predefinita, le cassette postali vengono mantenute per 30 giorni. Durante il periodo di conservazione, il contenuto della cassetta postale eliminata può essere ripristinato (copiato) in una cassetta postale esistente. In questo argomento viene descritto l'utilizzo della shell per la gestione delle richieste di ripristino delle cassette postali.

Per le attività di gestione aggiuntive relative alle cassette postali disconnesse, vedere i seguenti argomenti:

[Disabilitazione o eliminazione di una cassetta postale](disable-or-delete-a-mailbox-exchange-2013-help.md)

[Connettere una cassetta postale disabilitata](connect-a-disabled-mailbox-exchange-2013-help.md)

[La connessione o il ripristino di una cassetta postale eliminata](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

[Ripristinare una cassetta postale eliminata](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

[Eliminare definitivamente una cassetta postale](permanently-delete-a-mailbox-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Richiesta di ripristino della cassetta postale" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Le procedure descritte in questo argomento possono essere eseguite solo in Shell. Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per gestire le richieste di ripristino delle cassette postali.

  - Per visualizzare il valore della proprietà *Identity* per tutte le richieste di ripristino delle cassette postali, eseguire il comando riportato di seguito.
    
    ```powershell
        Get-MailboxRestoreRequest | Format-Table Identity
    ```
    
    È possibile utilizzare il valore Identity per specificare la richiesta di ripristino di una specifica cassetta postale quando si eseguono le procedure descritte nel presente argomento.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Visualizzazione delle proprietà della richiesta di ripristino tramite Shell

È possibile visualizzare le proprietà della richiesta di ripristino di una cassetta postale, ottenendo in tal modo informazioni di base sullo stato della richiesta di ripristino di una cassetta postale.

Per visualizzare l'elenco e il valore della proprietà *Identity* per tutte le richieste di ripristino della cassetta postale, eseguire il comando riportato di seguito.

```powershell
Get-MailboxRestoreRequest | Format-Table Identity
```

Per ottenere informazioni sulle richieste di ripristino di una determinata cassetta postale, è possibile utilizzare l'identità.

In questo esempio viene restituito lo stato della richiesta di ripristino "Pilar Pinilla \\MailboxRestore" utilizzando il parametro *Identity*.

```powershell
Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore"
```

In questo esempio vengono restituite tutte le informazioni relative alla seconda richiesta di ripristino della cassetta postale di destinazione Pilar Pinilla.

```powershell
Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1" | Format-List
```

In questo esempio viene restituito lo stato delle richieste di ripristino in corso dal database di origine MBD01.

```powershell
Get-MailboxRestoreRequest -SourceDatabase MBD01
```

In questo esempio vengono restituite tutte le richieste di ripristino attualmente in corso.

```powershell
Get-MailboxRestoreRequest -Status InProgress
```

Sono disponibili altre utili informazioni sullo stato, tra cui `Queued`, `Completed`, `Suspended` e `Failed`.

In questo esempio vengono restituite tutte le richieste di ripristino sospese.

```powershell
Get-MailboxRestoreRequest -Suspend $true
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829907\(v=exchg.150\)).

## Output di Get-MailboxRestoreRequest

Per impostazione predefinita, il cmdlet **Get-MailboxRestoreRequest** restituisce il nome della richiesta, la cassetta postale di destinazione in cui ripristinare i dati e lo stato della richiesta. Nella seguente tabella sono riportate le informazioni utili restituite quando si esegue il pipeline del cmdlet al cmdlet **Format-List**.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valore</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SourceDatabase</code></p></td>
<td><p>Specifica il database che contiene la cassetta postale disconnessa ripristinata.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetMailbox</code></p></td>
<td><p>Specifica la cassetta postale in cui si intende ripristinare i dati.</p></td>
</tr>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>Specifica il nome della richiesta.</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>Indica il database in cui il servizio Replica delle cassette postali (MRS) di Microsoft Exchange archivia i dettagli sullo stato della richiesta.</p></td>
</tr>
<tr class="odd">
<td><p><code>Status</code></p></td>
<td><p>Specifica lo stato della richiesta.</p></td>
</tr>
<tr class="even">
<td><p><code>Suspend</code></p></td>
<td><p>Specifica se la richiesta è sospesa. Il ripristino di una cassetta postale può essere sospeso quando viene creato utilizzando il cmdlet <strong>New-MailboxRestoreRequest</strong> con il parametro <em>Suspend</em>. Può inoltre essere sospeso se l'operazione di ripristino della cassetta postale si conclude con esito negativo o essere sospeso da un amministratore mediante il cmdlet <strong>Suspend-MailboxRestoreRequest</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>Specifica l'identità della richiesta. Questa identità è una combinazione del nome della cassetta postale di destinazione e il nome di richiesta.</p></td>
</tr>
</tbody>
</table>


## Come verificare se l'operazione ha avuto esito positivo?

Eseguire il cmdlet **Get-MailboxRestoreRequest** per verificare se sia possibile visualizzare le proprietà della richiesta di ripristino della cassetta postale. Se il cmdlet restituisce un errore, verificare che la sintassi e l'identità utilizzate siano corrette. In alcuni casi, il cmdlet può avere avuto esito positivo e non restituire alcun risultato. Ad esempio, se è stata inviata la richiesta di ripristino di una cassetta postale, è stato eseguito il comando `Get-MailboxRestoreRequest -Status InProgress` e non viene restituito alcun risultato, nessuna richiesta di ripristino è attualmente in esecuzione.

## Visualizzazione delle statistiche sulle richieste di ripristino tramite Shell

È possibile visualizzare le statistiche di una richiesta di ripristino di una cassetta postale, in grado di fornire informazioni dettagliate utilizzabili per la risoluzione dei problemi.

In questo esempio vengono restituite le statistiche predefinite per la richiesta di ripristino danp\\MailboxRestore1. Per impostazione predefinita, le informazioni restituite includono nome, cassetta postale, stato e percentuale di completamento.

```powershell
Get-MailboxRestoreRequestStatistics -Identity danp\MailboxRestore1
```

In questo esempio vengono restituite le statistiche per la cassetta postale di Dan Park e il report viene esportato in un file CSV.
```powershell
    Get-MailboxRestoreRequestStatistics -Identity "Dan Park\MailboxRestore" | Export-CSV \\SERVER01\RestoreRequest_Reports\DanPark_Restorestats.csv
```
In questo esempio vengono restituite informazioni aggiuntive sulla richiesta di ripristino per la cassetta postale di Pilar Pinilla utilizzando il parametro *IncludeReport* ed eseguendo il pipelining dei risultati mediante il cmdlet **Format-List**.
```powershell
    Get-MailboxRestoreRequestStatistics -Identity "Pilar Pinilla\MailboxRestore" -IncludeReport | Format-List 
```
In questo esempio vengono restituite informazioni aggiuntive per tutte le richieste di ripristino con stato `Failed` utilizzando il parametro *IncludeReport*. Le informazioni vengono quindi salvate nel file AllRestoreReports.txt nella posizione in cui viene eseguito il comando.
```powershell
    Get-MailboxRestoreRequest -Status Failed | Get-MailboxRestoreRequestStatistics -IncludeReport | Format-List > AllRestoreReports.txt
```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/it-it/library/ff829912\(v=exchg.150\)) e [Get-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829907\(v=exchg.150\)).

## Output di MailboxRestoreRequestStatistics

Per impostazione predefinita, il cmdlet [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/it-it/library/ff829912\(v=exchg.150\)) restituisce il nome e lo stato della richiesta, l'alias della cassetta postale di destinazione e la percentuale completata. Nella seguente tabella sono riportate altre utili informazioni restituite quando si esegue il pipeline del cmdlet al cmdlet **Format-List**.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valore</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>Specifica il nome della richiesta.</p></td>
</tr>
<tr class="even">
<td><p><code>Status</code></p></td>
<td><p>Specifica lo stato della richiesta.</p></td>
</tr>
<tr class="odd">
<td><p><code>StatusDetail</code></p></td>
<td><p>Specifica ulteriori informazioni circa lo stato della richiesta. Ad esempio, se il valore <code>Status</code> restituisce <code>InProgress</code>, il valore <code>StatusDetail</code> restituirà le specifiche fasi dello stato <code>InProgress</code>, come <code>CreatingFolderHierarchy</code> e <code>CopyingMessages</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>SyncStage</code></p></td>
<td><p>Specifica a che punto è la richiesta di ripristino.</p></td>
</tr>
<tr class="odd">
<td><p><code>Suspend</code></p></td>
<td><p>Specifica se la richiesta di ripristino è sospesa. Questo valore è <code>true</code> nello scenario seguente:</p>
<ul>
<li><p>MRS ha bloccato o sta bloccando la richiesta a causa di un errore.</p></li>
<li><p>Un amministratore ha sospeso la richiesta.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SourceExchangeGuid</code></p></td>
<td><p>Specifica il GUID della cassetta postale di origine da cui si intende ripristinare i dati.</p></td>
</tr>
<tr class="odd">
<td><p><code>SourceRootFolder</code></p></td>
<td><p>Specifica il nome della cartella radice nella gerarchia della cassetta postale di origine da cui si intende ripristinare i dati. Se questo valore è vuoto, i dati vengono ripristinati nella cartella di livello superiore dell'archivio informazioni.</p></td>
</tr>
<tr class="even">
<td><p><code>SourceDatabase</code></p></td>
<td><p>Specifica il nome del database in cui si trova la cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxRestoreFlags</code></p></td>
<td><p>Specifica che la cassetta postale ripristinata è <code>Disabled</code> o <code>Soft-Deleted</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetAlias</code></p></td>
<td><p>Indica l'alias della cassetta postale di destinazione.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetIsArchive</code></p></td>
<td><p>Specifica se la cassetta postale è in fase di ripristino in un archivio.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetExchangeGuid</code></p></td>
<td><p>Indica il GUID della cassetta postale di destinazione.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetRootFolder</code></p></td>
<td><p>Specifica il nome della cartella radice nella gerarchia della cassetta postale di destinazione in cui si intende ripristinare i dati. Se questo valore è vuoto, i dati vengono ripristinati nella cartella di livello superiore dell'archivio informazioni.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetDatabase</code></p></td>
<td><p>Specifica il nome del database in cui si trova la cassetta postale di destinazione.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetMailboxIdentity</code></p></td>
<td><p>Specifica l'identità della cassetta postale di destinazione.</p></td>
</tr>
<tr class="even">
<td><p><code>IncludeFolders</code></p></td>
<td><p>Specifica l'elenco delle cartelle da includere durante il ripristino. Se questo valore è vuoto, al momento della creazione della richiesta non è stata specificata alcuna cartella e quindi tutte le cartelle verranno ripristinate nella cassetta postale (a meno che non si utilizzi il parametro <em>ExcludeFolders</em> per escludere determinate cartelle).</p></td>
</tr>
<tr class="odd">
<td><p><code>ExcludeFolders</code></p></td>
<td><p>Specifica l'elenco delle cartelle da escludere durante il ripristino. Se questo valore è vuoto, al momento della creazione della richiesta non è stata specificata alcuna cartella e quindi tutte le cartelle verranno ripristinate nella cassetta postale (a meno che non si utilizzi il parametro <em>IncludeFolders</em> per includere determinate cartelle).</p></td>
</tr>
<tr class="even">
<td><p><code>ExcludeDumpster</code></p></td>
<td><p>Indica se la cartella Elementi ripristinabili è stata esclusa al momento della creazione della richiesta.</p></td>
</tr>
<tr class="odd">
<td><p><code>ConflictResolutionOption</code></p></td>
<td><p>Indica come si deve comportare il servizio di replica delle cassette postali se nelle cartelle di destinazione e di origine rileva la presenza di messaggi uguali.</p></td>
</tr>
<tr class="even">
<td><p><code>AssociatedMessagesCopyOption</code></p></td>
<td><p>Indica se i messaggi associati vengono copiati durante l'elaborazione della richiesta. I messaggi associati sono messaggi speciali che contengono dati nascosti con informazioni sulle regole, sulle visualizzazioni e sui moduli.</p></td>
</tr>
<tr class="odd">
<td><p><code>BadItemLimit</code></p></td>
<td><p>Indica il numero di elementi in errore che il servizio di replica delle cassette postali può ignorare se la richiesta rileva messaggi danneggiati.</p></td>
</tr>
<tr class="even">
<td><p><code>BadItemsEncountered</code></p></td>
<td><p>Indica il numero di messaggi danneggiati rilevati dal comando. Se il valore <em>BadItemsEncountered</em> è maggiore del valore <em>BadItemLimit</em>, la richiesta non viene eseguita.</p></td>
</tr>
<tr class="odd">
<td><p><code>QueuedTimeStamp</code></p></td>
<td><p>Indica la data e l'ora per l'inizializzazione della richiesta al servizio di replica delle cassette postali.</p></td>
</tr>
<tr class="even">
<td><p><code>StartTimeStamp</code></p></td>
<td><p>Specifica la data e l'ora in cui il servizio di replica delle cassette postali ha avviato l'elaborazione della richiesta di ripristino.</p></td>
</tr>
<tr class="odd">
<td><p><code>LastUpdateTimeStamp</code></p></td>
<td><p>Indica la data e l'ora in cui è stata apportata l'ultima modifica alla richiesta. La modifica potrebbe essere stata apportata da un amministratore oppure dal servizio di replica delle cassette postali.</p></td>
</tr>
<tr class="even">
<td><p><code>SuspendTimeStamp</code></p></td>
<td><p>Indica la data e l'ora in cui la richiesta è stata sospesa.</p></td>
</tr>
<tr class="odd">
<td><p><code>OverallDuration</code></p></td>
<td><p>Indica il tempo impiegato per il completamento della richiesta. Se lo stato della richiesta è <code>Failed</code>, questo valore indica il tempo trascorso tra l'inizio della richiesta e l'errore che non ne ha permesso il completamento. Se la richiesta non è stata completata, questo valore indica il tempo trascorso tra l'inizio della richiesta e l'esecuzione del cmdlet <strong>Get-MailboxRestoreRequestStatistics</strong>.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalSuspendedDuration</code></p></td>
<td><p>Indica l'intervallo di tempo in cui la richiesta è rimasta nello stato <code>Suspended</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalFailedDuration</code></p></td>
<td><p>Indica l'intervallo di tempo in cui la richiesta è rimasta nello stato <code>Failed</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalQueuedDuration</code></p></td>
<td><p>Indica l'intervallo di tempo in cui la richiesta è rimasta nello stato <code>Queued</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalInProgressDuration</code></p></td>
<td><p>Indica l'intervallo di tempo in cui la richiesta è rimasta nello stato <code>In Progress</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalStalledDueToHADuration</code></p></td>
<td><p>Indica l'intervallo di tempo in cui la richiesta è rimasta bloccata a causa dell'alta disponibilità.</p></td>
</tr>
<tr class="odd">
<td><p><code>MRSServerName</code></p></td>
<td><p>Indica il nome del server Accesso client che ha elaborato la richiesta.</p></td>
</tr>
<tr class="even">
<td><p><code>EstimatedTransferSize</code></p></td>
<td><p>Specifica la dimensione totale del file ripristinato o la dimensione del file che il servizio di replica delle cassette postali prevede di ripristinare, se la richiesta è nello stato <code>In Progress</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>EstimatedTransferItemCount</code></p></td>
<td><p>Indica il numero di elementi importati o il numero di elementi che il il servizio di replica delle cassette postali prevede di ripristinare, se la richiesta di ripristino è nello stato <code>In Progress</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>BytesTransferredPerMinute</code></p></td>
<td><p>Indica il numero medio di byte trasferiti al minuto.</p></td>
</tr>
<tr class="odd">
<td><p><code>ItemsTransferred</code></p></td>
<td><p>Indica il numero di elementi che sono stati trasferiti.</p></td>
</tr>
<tr class="even">
<td><p><code>PercentComplete</code></p></td>
<td><p>Indica la percentuale di completamento della richiesta.</p></td>
</tr>
<tr class="odd">
<td><p><code>CompletedRequestAgeLimit</code></p></td>
<td><p>Specifica la durata del periodo di conservazione di una richiesta di ripristino completata prima dell'eliminazione. Il valore predefinito è 30 giorni.</p></td>
</tr>
<tr class="even">
<td><p><code>PositionInQueue</code></p></td>
<td><p>Se la richiesta non è stata ancora avviata, questo valore indica la posizione della richiesta all'interno della coda.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureCode</code></p></td>
<td><p>Se si è verificato un errore, questo valore indica il codice di errore.</p></td>
</tr>
<tr class="even">
<td><p><code>FailureType</code></p></td>
<td><p>Se si è verificato un errore, questo valore indica il tipo di errore.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureSide</code></p></td>
<td><p>Se si è verificato un errore, questo valore indica che si è verificato un errore nella cassetta postale di destinazione o nella cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><code>Message</code></p></td>
<td><p>Se si è verificato un errore, questo valore indica il messaggio di errore. Questo valore può anche indicare il commento di sospensione.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureTimestamp</code></p></td>
<td><p>Se la richiesta non è stata completata, questo valore indica la data e l'ora in cui si è verificato l'errore.</p></td>
</tr>
<tr class="even">
<td><p><code>FailureContext</code></p></td>
<td><p>Se la richiesta non è stata completata, questo valore indica le informazioni sull'azione eseguita al momento dell'errore.</p></td>
</tr>
<tr class="odd">
<td><p><code>ValidationMessage</code></p></td>
<td><p>Se la richiesta non è valida, questo valore indica il motivo.</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>Indica il database in cui il servizio di replica delle cassette postali archivia i dettagli sullo stato della richiesta.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>Specifica l'identità della richiesta.</p></td>
</tr>
<tr class="even">
<td><p><code>Report</code></p></td>
<td><p>Se è stato utilizzato il parametro <em>IncludeReport</em>, questo valore indica le informazioni che possono essere utilizzate per risolvere i problemi della richiesta.</p></td>
</tr>
</tbody>
</table>


## Come verificare se l'operazione ha avuto esito positivo?

Eseguire il cmdlet **Get-MailboxRestoreRequestStatistics** per verificare che sia possibile visualizzare le statistiche delle richieste di ripristino della cassetta postale. Se il cmdlet restituisce un errore, verificare che la sintassi e l'identità della richiesta di ripristino utilizzate siano corrette.

## Modifica delle proprietà della richiesta di ripristino tramite Shell

Se una richiesta di ripristino non va a buon fine, è possibile utilizzare il cmdlet **Set-MailboxRestoreRequest** per modificare le proprietà della richiesta e tentare di risolvere il problema.

In questo esempio viene specificato che la richiesta di ripristino MailboxRestore1 per la cassetta postale di Debra Garcia ignora 10 elementi danneggiati di cassette postali.

```powershell
Set-MailboxRestoreRequest -Identity "Debra Garcia\MailboxRestore1" -BadItemLimit 10
```

In questo esempio viene specificato che la richiesta di ripristino MailboxRestore1 per la cassetta postale di Florence Flipo ignora 100 elementi danneggiati di cassette postali. Poiché il valore *BadItemLimit* è maggiore di 50, è necessario specificare il parametro *AcceptLargeDataLoss*.
```powershell
    Set-MailboxRestoreRequest -Identity "Florence Flipo\MailboxRestore1" -BadItemLimit 100 -AcceptLargeDataLoss
```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829909\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta modifica delle proprietà di una richiesta di ripristino, eseguire il cmdlet **Get-MailboxRestoreRequestStatistics** per visualizzare le proprietà della richiesta di ripristino revisionate. Se la richiesta di ripristino è stata creata correttamente, la proprietà *Status* avrà il valore di `Queued`, `InProgress` o `Completed`. Una volta completata la richiesta di ripristino, il contenuto della cassetta postale con eliminazione reversibile verrà visualizzato nella cassetta postale di destinazione.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/it-it/library/ff829912\(v=exchg.150\)).

## Sospensione di una richiesta di ripristino tramite Shell

È possibile sospendere una richiesta di ripristino in qualsiasi momento dopo la sua creazione, ma prima che raggiunga lo stato `Completed`. Per la sintassi dei comandi che consente di riprendere la richiesta di ripristino utilizzando il cmdlet [Resume-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829908\(v=exchg.150\)), vedere Use the Shell to resume a restore request più avanti in questo argomento.

In questo esempio viene sospesa la richiesta di ripristino MailboxRestore1 della cassetta postale di Pilar Pinilla.

```powershell
Suspend-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

In questo esempio vengono sospese tutte le richieste di ripristino in corso. A tale scopo, tutte le richieste di ripristino con stato `InProgress` vengono recuperate e quindi inviate tramite pipeline al cmdlet **Suspend-MailboxRestoreRequest** con il commento di sospensione "Resume after FY13Q2 Maintenance."
```powershell
    Get-MailboxRestoreRequest -Status InProgress | Suspend-MailboxRestoreRequest -SuspendComment "Resume after FY13Q2 Maintenance"
```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Suspend-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829906\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta sospensione della richiesta di ripristino di una cassetta postale, eseguire il comando riportato di seguito.

```powershell
Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status
```

Se il valore della proprietà *Suspend* è uguale a `True`, la richiesta di ripristino è stata sospesa correttamente. Inoltre, il valore `Suspended` della proprietà *Status* indica che la richiesta di ripristino è stata sospesa.

## Riavvio di una richiesta di ripristino tramite Shell

Utilizzare il cmdlet **Resume-MailboxRestoreRequest** per riprendere una richiesta di ripristino che è stata sospesa o non è riuscita.

In questo esempio viene ripresa la richiesta di ripristino Pilar Pinilla\\MailboxRestore1.

```powershell
Resume-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

In questo esempio vengono riprese tutte le richieste di ripristino con stato Non riuscito.

```powershell
Get-MailboxRestoreRequest -Status Failed | Resume-MailboxRestoreRequest
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Resume-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829908\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che una richiesta di ripristino sia stata ripresa correttamente, eseguire il comando riportato di seguito.

```powershell
Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status
```

Se il valore della proprietà *Suspend* è uguale a `False`, la richiesta di ripristino è stata ripresa correttamente. Inoltre, il valore `InProgress` della proprietà *Status* indica che la richiesta di ripristino è stata ripresa.

## Rimozione di una richiesta di ripristino tramite Shell

Utilizzare il cmdlet **Remove-MailboxRestoreRequest** per rimuovere le richieste di ripristino della cassetta postale. Se si rimuove una richiesta di ripristino dopo l'inizio della copia dei dati verso la cassetta postale di destinazione, i dati già copiati rimangono nella cassetta postale di destinazione.


> [!NOTE]
> Come già indicato in precedenza, le richieste di ripristino completate vengono conservate per 30 giorni per impostazione predefinita prima di essere eliminate automaticamente.



In questo esempio viene eliminata la richiesta di ripristino Pilar Pinilla\\MailboxRestore1.

```powershell
Remove-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

In questo esempio vengono rimosse tutte le richieste di ripristino con stato Completato.

```powershell
Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest
```

In questo esempio viene annullata la richiesta di ripristino utilizzando il parametro *RequestGuid* per una richiesta memorizzata in MBXDB01. L'impostazione del parametro che richiede i parametri *RequestGuid* e *RequestQueue* viene utilizzata unicamente a scopo di debug di MRS. Utilizzare questo parametro soltanto se è stato richiesto dal Servizio assistenza e supporto tecnico Microsoft.

```powershell
Remove-MailboxRestoreRequest -RequestQueue MBXDB01 -RequestGuid 25e0eaf2-6cc2-4353-b83e-5cb7b72d441f
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829910\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta eliminazione della richiesta di ripristino di una cassetta postale, eseguire il comando riportato di seguito.

```powershell
Get-MailboxRestoreRequest -Identity <identity of removed restore request>
```

Il comando restituirà un errore con la segnalazione che la richiesta di ripristino non esiste.

È inoltre possibile eseguire il cmdlet **Get-MailboxRestoreRequest**. Se la richiesta di ripristino è stata eliminata correttamente, non sarà inclusa nei risultati.


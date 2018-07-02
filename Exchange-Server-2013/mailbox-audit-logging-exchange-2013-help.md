---
title: 'Registrazione di controllo delle cassette postali: Exchange 2013 Help'
TOCTitle: Registrazione di controllo delle cassette postali
ms:assetid: 29b67d58-eef9-4ad4-863f-562405ea8794
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff459237(v=EXCHG.150)
ms:contentKeyID: 50480299
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registrazione di controllo delle cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Dal momento che le cassette postali possono contenere informazioni riservate sia a livello aziendale che di singolo utente, è fondamentale tenere traccia di chi accede alle cassette postali nell'organizzazione e che attività esegue su di esse. È soprattutto importante controllare gli accessi alle cassette postali eseguiti da utenti che non ne sono i legittimi proprietari. Questi utenti sono definiti *delegati*.

Utilizzando la *registrazione di controllo delle cassette postali*, è possibile registrare gli accessi effettuati dai proprietari delle cassette postali, dai delegati (inclusi gli amministratori con autorizzazioni di accesso completo alle cassette postali) e dagli amministratori.

Quando si abilita la registrazione di controllo delle cassette postali, è possibile specificare quali azioni (ad esempio, accesso oppure spostamento o eliminazione di un messaggio) verranno registrate per ciascun tipo di utente (amministratore, utente delegato o proprietario). Le registrazioni includono anche informazioni importanti quali indirizzo IP del client, nome host e processo o client utilizzato per accedere alla cassetta postale. Per gli elementi spostati, nella registrazione viene riportato il nome della cartella di destinazione.

## Registri di controllo delle cassette postali

I registri di controllo vengono generati per tutte le cassette postali per cui è abilitata la registrazione di controllo. Le voci del registro vengono archiviate nella cartella degli elementi ripristinabili nella cassetta postale controllata, nella sottocartella Controlli. In questo modo, tutte le voci registrate sono disponibili in un unico percorso, indipendentemente dal metodo scelto per accedere alla cassetta postale o dal server o workstation che l'amministratore ha utilizzato per accedere al registro di controllo. Se si sposta una cassetta postale su un altro server Cassette postali, anche i registri di controllo della cassetta postale vengono spostati perché si trovano al suo interno.

Per impostazione predefinita, le voci del registro di controllo di una cassetta postale vengono conservate nella cassetta postale per 90 giorni e quindi eliminate. È possibile modificare questo periodo di conservazione utilizzando il parametro *AuditLogAgeLimit* con il cmdlet [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)). Se una cassetta postale è in Archiviazione sul posto o in conservazione per controversia legale., le voci del registro di controllo vengono conservate solo fino alla scadenza del periodo di mantenimento del registro di controllo per la cassetta postale. Per conservare le voci del registro di controllo per più tempo, è necessario aumentare il periodo di mantenimento modificando il valore per il parametro *AuditLogAgeLimit*. È anche possibile esportare le voci del registro di controllo prima della scadenza del periodo di mantenimento. Per ulteriori informazioni, vedere:

  - [Esportare registri di controllo delle cassette postali](export-mailbox-audit-logs-exchange-2013-help.md)

  - [Creare una ricerca dei registri di controllo delle cassette postali](create-a-mailbox-audit-log-search-exchange-2013-help.md)

## Abilitazione della registrazione di controllo delle cassette postali

La registrazione di controllo delle cassette postali è abilitata per ogni cassetta postale. Utilizzare il cmdlet **Set-Mailbox** per abilitare o disabilitare la registrazione di controllo delle cassette postali. Per ulteriori informazioni, vedere [Abilitare o disabilitare la registrazione per una cassetta postale di controllo delle cassette postali](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

Quando si abilita la registrazione di controllo per una cassetta postale, gli accessi alla cassetta e alcune azioni eseguite dagli amministratori e dai delegati vengono registrate per impostazione predefinita. Per registrare anche le azioni eseguite dal proprietario della cassetta postale, è necessario specificare le azioni da sottoporre a controllo.

## Azioni inserite nella registrazione di controllo delle cassette postali

Nella tabella seguente vengono indicate le azioni inserite nel registro di controllo delle cassette postali, incluso il tipo di accesso che genera la registrazione di ciascuna tipologia di azione.


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
<th>Azione</th>
<th>Descrizione</th>
<th>Amministratore</th>
<th>Delegato</th>
<th>Proprietario</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Copia</p></td>
<td><p>Un elemento viene copiato in un'altra cartella.</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Crea</p></td>
<td><p>Elemento creato nella cartella Calendario, Contatti, Note o Attività nella cassetta postale; ad esempio, viene creata una nuova convocazione di riunione. La creazione della cartella o del messaggio non viene sottoposta a controllo.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì*</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Bind della cartella</p></td>
<td><p>Accesso effettuato a una cartella della cassetta postale.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì**</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Eliminazione definitiva</p></td>
<td><p>Un elemento viene eliminato definitivamente dalla cartella Elementi ripristinabili.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì*</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Bind del messaggio</p></td>
<td><p>Un elemento viene aperto o vi si accede nel riquadro di lettura.</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Sposta</p></td>
<td><p>Un elemento viene spostato in un'altra cartella.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Sposta in Posta eliminata</p></td>
<td><p>Un elemento viene spostato nella cartella Posta eliminata.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Invia come</p></td>
<td><p>Un messaggio viene inviato con l'autorizzazione Invia come.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì*</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>Invia per conto di</p></td>
<td><p>Un messaggio viene inviato con l'autorizzazione Invia per conto di.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>Eliminazione temporanea</p></td>
<td><p>Un elemento viene eliminato dalla cartella Posta eliminata.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì*</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Aggiorna</p></td>
<td><p>Le proprietà di un elemento vengono aggiornate.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì*</p></td>
<td><p>Sì</p></td>
</tr>
</tbody>
</table>


\* Controllo eseguito per impostazione predefinita, se per la cassetta postale è abilitato il controllo.

\* \* Voci per le azioni di binding cartella eseguite dai delegati vengono consolidate. Una voce di registro viene generata per l'accesso alle cartelle singole durante un periodo di 24 ore.

Se non è più necessario registrare determinati tipi di azioni, modificare la configurazione di registrazione per disabilitarle. Le voci presenti nel registro non vengono eliminate fino a quando non raggiungono la loro scadenza naturale.

## Ricerche nelle voci del registro di controllo delle cassette postali

È possibile utilizzare i seguenti metodi per effettuare una ricerca nelle voci nel registro di controllo:

  - **Ricerca sincrona in una singola cassetta postale**   È possibile utilizzare il cmdlet [Search-MailboxAuditLog](https://technet.microsoft.com/it-it/library/ff522360\(v=exchg.150\)) per eseguire una ricerca sincrona nelle voci del registro di controllo per una singola cassetta postale. Il cmdlet visualizza i risultati della ricerca nella finestra di Exchange Management Shell. Per ulteriori informazioni, vedere [Il Registro di controllo delle cassette postali per una cassetta postale di ricerca](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md).

  - **Ricerca asincrona in una o più cassette postali**   È possibile creare una ricerca nel registro di controllo delle cassette postali per eseguire una ricerca asincrona nei registri di controllo di una o più cassette postali e quindi inviare i risultati della ricerca all'indirizzo di posta elettronica specificato. I risultati della ricerca vengono inviati come allegato XML. Per creare la ricerca, utilizzare il cmdlet [New-MailboxAuditLogSearch](https://technet.microsoft.com/it-it/library/ff522362\(v=exchg.150\)). Per ulteriori informazioni, vedere [Creare una ricerca dei registri di controllo delle cassette postali](create-a-mailbox-audit-log-search-exchange-2013-help.md).

  - **Utilizzo dei rapporti di controllo in EAC (Exchange Admin Center)**   È possibile utilizzare la scheda **Controllo** in EAC per creare un record di accesso non proprietario alla casella postale o esportare le voci dal registro di controllo della cassetta postale. Per dettagli, vedere:
    
      - [Eseguire un rapporto di accesso non proprietario della cassetta postale](run-a-non-owner-mailbox-access-report-exchange-online-help.md)
    
      - [Esportare registri di controllo delle cassette postali](export-mailbox-audit-logs-exchange-2013-help.md)

## Voci del registro di controllo delle cassette postali

Nella tabella seguente vengono illustrati i campi inseriti nel registro di controllo delle cassette postali.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Campo</th>
<th>Compilato con</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Operation</strong></p></td>
<td><p>Una delle seguenti azioni:</p>
<ul>
<li><p>Copia</p></li>
<li><p>Crea</p></li>
<li><p>Bind della cartella</p></li>
<li><p>Eliminazione definitiva</p></li>
<li><p>Bind del messaggio</p></li>
<li><p>Sposta</p></li>
<li><p>Sposta in Posta eliminata</p></li>
<li><p>Invia come</p></li>
<li><p>Invia per conto di</p></li>
<li><p>Eliminazione temporanea</p></li>
<li><p>Aggiorna</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>OperationResult</strong></p></td>
<td><p>Una dei seguenti risultati:</p>
<ul>
<li><p>Operazione non riuscita</p></li>
<li><p>Operazione parzialmente completata</p></li>
<li><p>Operazione completata</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>LogonType</strong></p></td>
<td><p>Il tipo di accesso dell'utente che ha eseguito l'operazione. I tipi di accesso sono:</p>
<ul>
<li><p>Proprietario</p></li>
<li><p>Delegato</p></li>
<li><p>Amministratore</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DestFolderId</strong></p></td>
<td><p>GUID della cartella di destinazione per le operazioni di spostamento.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestFolderPathName</strong></p></td>
<td><p>Percorso della cartella di destinazione per le operazioni di spostamento.</p></td>
</tr>
<tr class="even">
<td><p><strong>FolderId</strong></p></td>
<td><p>GUID della cartella.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderPathName</strong></p></td>
<td><p>Percorso della cartella.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientInfoString</strong></p></td>
<td><p>Dettagli per l'identificazione del client o del componente Exchange che ha eseguito l'operazione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientIPAddress</strong></p></td>
<td><p>Indirizzo IP del computer client.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientMachineName</strong></p></td>
<td><p>Nome del computer client.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientProcessName</strong></p></td>
<td><p>Nome del processo dell'applicazione client.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientVersion</strong></p></td>
<td><p>Versione dell'applicazione client.</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalLogonType</strong></p></td>
<td><p>Il tipo di accesso dell'utente che ha eseguito l'operazione. I tipi di accesso sono:</p>
<ul>
<li><p>Proprietario</p></li>
<li><p>Delegato</p></li>
<li><p>Amministratore</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>MailboxOwnerUPN</strong></p></td>
<td><p>Nome dell'entità utente (UPN) del proprietario della cassetta postale.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxOwnerSid</strong></p></td>
<td><p>ID di sicurezza (SID) del proprietario della cassetta postale.</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerUPN</strong></p></td>
<td><p>Nome dell'entità utente (UPN) del proprietario della cassetta postale di destinazione, registrato per le operazioni che coinvolgono più cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestMailboxOwnerSid</strong></p></td>
<td><p>ID di sicurezza (SID) del proprietario della cassetta postale di destinazione, registrato per le operazioni che coinvolgono più cassette postali.</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerGuid</strong></p></td>
<td><p>GUID del proprietario della cassetta postale di destinazione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CrossMailboxOperation</strong></p></td>
<td><p>Indica se l'operazione registrata viene eseguita tra più cassette postali (ad esempio, la copia o lo spostamento dei messaggi tra cassette postali).</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserDisplayName</strong></p></td>
<td><p>Nome visualizzato dell'utente che ha eseguito l'accesso.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DelegateUserDisplayName</strong></p></td>
<td><p>Nome visualizzato dell'utente delegato.</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserSid</strong></p></td>
<td><p>ID di sicurezza (SID) dell'utente che ha eseguito l'accesso.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SourceItems</strong></p></td>
<td><p>ID degli elementi della cassetta postale su cui viene eseguita l'azione registrata (ad esempio, lo spostamento o l'eliminazione). Se l'operazione viene eseguita su diversi elementi, in questo campo viene riportata la raccolta di elementi.</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceFolders</strong></p></td>
<td><p>GUID della cartella di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ItemId</strong></p></td>
<td><p>ID dell'elemento.</p></td>
</tr>
<tr class="even">
<td><p><strong>ItemSubject</strong></p></td>
<td><p>Oggetto dell'elemento.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxGuid</strong></p></td>
<td><p>GUID della cassetta postale.</p></td>
</tr>
<tr class="even">
<td><p><strong>MailboxResolvedOwnerName</strong></p></td>
<td><p>Nome risolto del proprietario della cassetta postale nel formato <em>DOMINIO</em>\<em>Nome account SAM</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastAccessed</strong></p></td>
<td><p>Ora di esecuzione dell'operazione.</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>ID della voce del registro di controllo.</p></td>
</tr>
</tbody>
</table>


## Ulteriori informazioni

  - **Accesso amministratore alle cassette postali** Si presume che alla cassetta postale acceda un amministratore esclusivamente nei seguenti scenari:
    
      - La funzionalità [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md) viene utilizzata per effettuare una ricerca in una cassetta postale.
    
      - Il cmdlet [New-MailboxExportRequest](https://technet.microsoft.com/it-it/library/ff607299\(v=exchg.150\)) viene utilizzato per esportare una cassetta postale.
    
      - [Editor MAPI di Microsoft Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=204086) viene utilizzato per accedere alla cassetta postale.

  - **Ignorare le registrazioni di controllo delle cassette postali** Gli accessi eseguiti da alcuni processi automatizzati autorizzati (ad esempio, gli account utilizzati da strumenti di terzi o per il monitoraggio a fini legali) possono creare un numero notevole di voci nel registro di controllo della cassetta postale e tuttavia non essere di alcun interesse per l'organizzazione. È possibile configurare questi account in modo che vengano ignorati dalle registrazioni di controllo delle cassette postali. Per ulteriori informazioni, vedere [Bypass di un account utente dal controllo delle cassette postali registrazione](bypass-a-user-account-from-mailbox-audit-logging-exchange-2013-help.md).

  - **Operazioni di registrazione del proprietario dalle cassetta postale** Nelle cassette postali che, come quella per la ricerca Discovery, possono contenere informazioni molto riservate, può essere opportuno abilitare la registrazione di controllo anche per il proprietario così da poter tenere traccia anche delle azioni, come l'eliminazione dei messaggi, da lui eseguite.

Inizio pagina


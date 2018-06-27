---
title: 'Cassette postali disconnesse: Exchange 2013 Help'
TOCTitle: Cassette postali disconnesse
ms:assetid: 508ebe2b-387d-4867-bdb0-028ef351ce56
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232039(v=EXCHG.150)
ms:contentKeyID: 50555589
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cassette postali disconnesse

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Ciascuna cassetta postale di Microsoft Exchange comprende un account utente di Active Directory e i dati della cassetta postale archiviati nel database delle cassette postali di Exchange. Tutti i dati di configurazione di una cassetta postale sono archiviati negli attributi di Exchange dell'oggetto utente di Active Directory. Nel database delle cassette postali sono contenuti i dati di posta presenti nella cassetta postale associata all'account utente. Nella figura seguente, sono riportati i componenti di una cassetta postale.

**Componenti della cassetta postale**

![Parti che costituiscono una cassetta postale](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "Parti che costituiscono una cassetta postale")

Una *cassetta postale disconnessa* è un oggetto cassetta postale nel database delle cassette postali che non è associato a un account utente in Active Directory. Esistono due tipi di cassette postali disconnesse:

  - **Cassette postali disabilitate**   Quando si disabilita o elimina una cassetta postale nell'interfaccia di amministrazione di Exchange o utilizzando il cmdlet **Disable-Mailbox** o **Remove-Mailbox** in Exchange Management Shell, Exchange conserva la cassetta postale eliminata nel database delle cassette postali e imposta la cassetta postale sulla stato disabilitato. È per questo motivo che le cassette postali disabilitate o eliminate vengono definite *cassette postali disabilitate*. La differenza è che quando si disabilita una cassetta postale, gli attributi di Exchange vengono rimossi dal corrispondente account utente in Active Directory, ma l'account utente viene mantenuto. Quando si elimina una cassetta postale, vengono eliminati sia gli attributi di Exchange sia l'account utente in Active Directory.
    
    Le cassette postali disabilitate ed eliminate vengono mantenute nel database delle cassette postali fino alla scadenza del periodo di conservazione della cassetta postale eliminata, che, per impostazione predefinita, equivale a 30 giorni. Una volta trascorso il periodo di conservazione, la cassetta postale viene *eliminata* definitivamente. Se si elimina una cassetta postale utilizzando il cmdlet **Remove-Mailbox**, questa viene mantenuta anche per la durata del periodo di conservazione.
    

    > [!IMPORTANT]
    > Se si elimina una cassetta postale utilizzando il cmdlet <STRONG>Remove-Mailbox</STRONG> o il parametro <EM>Permanent</EM> o <EM>StoreMailboxIdentity</EM>, questa verrà immediatamente eliminata dal database delle cassette postali.

    
    Per identificare le cassette postali disabilitate nella propria organizzazione, utilizzare il seguente comando in Shell.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "Disabled" } | ft DisplayName,Database,DisconnectDate

  - **Cassette postali eliminate temporaneamente**   Quando una cassetta postale viene spostata in un database delle cassette postali diverso, Exchange non elimina completamente la cassetta postale dal database delle cassette postali di origine al termine dello spostamento. Al contrario, la cassetta postale nel database di origine delle cassette postali passa allo stato di *eliminazione reversibile*. Come nel caso delle cassette postali disabilitate, le cassette postali con eliminazione reversibile vengono mantenute nel database di origine fino alla scadenza del periodo di conservazione della cassetta postale eliminata o fino a quando non si utilizza il cmdlet **Remove-StoreMailbox** per eliminare la cassetta postale.
    
    Utilizzare il seguente comando per identificare le cassette postali con eliminazione reversibile nell'organizzazione.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | ft DisplayName,Database,DisconnectDate

**Sommario**

Utilizzo delle cassette postali disabilitate

Utilizzo delle cassette postali di archiviazione disabilitate

Utilizzo delle cassette postali con eliminazione reversibile

Riepilogo dell'utilizzo delle cassette postali disconnesse

Documentazione sulla cassetta postale disconnessa

## Utilizzo delle cassette postali disabilitate

È possibile eseguire diverse operazioni su una cassetta postale disabilitata prima che questa venga eliminata dal database delle cassette postali:

  - Ricollegarla allo stesso account utente.

  - Collegarla a un account utente differente non abilitato alla posta elettronica, il che implica che l'account utente non dispone di una cassetta postale.

  - Ripristinarla su un account utente che dispone di una cassetta postale esistente. Ad esempio, se un utente la cui cassetta postale è stata eliminata dispone di una nuova cassetta, è possibile ripristinare la cassetta postale disabilitata dell'utente nella nuova cassetta postale.

  - Eliminarla definitivamente dal database delle cassette postali di Exchange.

## Connessione o ripristino di una cassetta postale disabilitata

Di seguito, sono riportati scenari in cui è possibile che si desideri connettere o ripristinare una cassetta postale disabilitata prima della scadenza del relativo periodo di conservazione o prima che questa venga eliminata in modo permanente:

  - Si è disabilitata una cassetta postale e ora si desidera ricollegarla allo stesso account utente di Active Directory.

  - Si è eliminata una cassetta postale utilizzando l'interfaccia di amministrazione di Exchange o il cmdlet [Remove-Mailbox](https://technet.microsoft.com/it-it/library/aa995948\(v=exchg.150\)) e ora si desidera ricollegarla a un account utente di Active Directory differente.

  - Si è eliminata una cassetta postale e ora si desidera ripristinarla in una cassetta postale esistente. Ad esempio, se un utente la cui cassetta postale è stata eliminata dispone di una nuova cassetta, è possibile ripristinare la cassetta postale disabilitata dell'utente nella nuova cassetta postale.

  - Si desidera convertire una cassetta postale utente in una cassetta postale collegata associata a un account utente esterno alla foresta in cui risiede l'organizzazione di Exchange. Questa associazione potrebbe essere necessaria, ad esempio, nello scenario di una foresta di risorse. In questo scenario, gli oggetti utente nella foresta di Exchange dispongono di cassette postali, ma non sono abilitati per l'accesso. È necessario associare una cassetta postale nella foresta di Exchange a un account utente nella foresta degli account esterni.

Sono disponibili due modi per poter riconnettere o ripristinare una cassetta postale disabilitata. Il primo metodo è di utilizzare l'interfaccia di amministrazione di Exchange o il cmdlet **Connect-Mailbox** per connettere una cassetta postale disabilitata a un account utente. Per la procedura da seguire per riconnettere le cassette postali disabilitate, vedere [Connettere una cassetta postale disabilitata](connect-a-disabled-mailbox-exchange-2013-help.md).

Il secondo metodo utilizza il cmdlet **New-MailboxRestoreRequest** per unire il contenuto della cassetta postale disabilitata a una cassetta postale esistente. Questo cmdlet utilizza il servizio di replica delle cassette postali per ripristinare la cassetta postale. Per la procedura da seguire per ripristinare le cassette postali disabilitate, vedere [La connessione o il ripristino di una cassetta postale eliminata](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md).

## Eliminazione definitiva di una cassetta postale disabilitata

Come indicato in precedenza, Exchange mantiene le cassette postali disabilitate nel database delle cassette postali in base alle impostazioni di conservazione delle cassette postali eliminate configurate per il database delle cassette postali. Una volta trascorso il periodo di conservazione specificato, una cassetta postale disabilitata viene eliminata dal database delle cassette postali di Exchange. È anche possibile eliminare in modo definitivo una cassetta postale disabilitata e l'intero contenuto dei messaggi dal database delle cassette postali utilizzando il cmdlet **Remove-StoreMailbox**. Una volta che la cassetta postale è stata eliminata automaticamente o in modo definitivo da un amministratore, la perdita di dati è permanente e non è possibili ripristinare la cassetta postale.

Per ulteriori informazioni, vedere [Eliminare definitivamente una cassetta postale](permanently-delete-a-mailbox-exchange-2013-help.md).

Utilizzo delle cassette postali disabilitate

## Utilizzo delle cassette postali di archiviazione disabilitate

Le cassette postali di archiviazione vengono disconnesse nel momento in cui vengono disabilitate. Come nel caso delle cassette postali principali disabilitate, è possibile connettere una cassetta postale di archiviazione disconnessa utilizzando il cmdlet **Connect-Mailbox** con il parametro *Archive*.

La cassetta postale principale e la cassetta postale di archiviazione condividono lo stesso nome distinto legacy (DN). Pertanto, è necessario connettere la cassetta postale di archiviazione alla stessa cassetta postale utente a cui era collegata in precedenza. Non è possibile connettere la cassetta postale di archiviazione a una cassetta postale utente differente.

È possibile eseguire due operazioni su una cassetta postale disconnessa:

  - **Collegarla a una cassetta postale principale esistente**   Come nel caso della cassetta postale disconnessa, una cassetta postale di archiviazione disconnessa viene mantenuta nel database delle cassette postali fino alla scadenza del periodo di conservazione della cassetta postale eliminata, che, per impostazione predefinita, equivale a 30 giorni. Durante questo periodo, è possibile ripristinare la cassetta postale di archiviazione ricollegandola allo stesso account utente cui era collegata prima che venisse disabilitata.
    

    > [!NOTE]
    > Se si disabilita una cassetta postale di archiviazione per una cassetta postale utente e poi si abilità una cassetta postale di archiviazione per quello stesso utente, quest'ultimo 'utente otterrà una nuova cassetta postale di archiviazione. È possibile utilizzare il cmdlet <STRONG>Connect-Mailbox</STRONG> per connettere una cassetta postale principale a un utente, ma è necessario utilizzare il cmdlet <STRONG>Enable-Mailbox</STRONG> per connettere una cassetta postale di archiviazione a una cassetta postale esistente.

    
    Per ulteriori informazioni, vedere [Gestione degli archivi In Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md).

  - **Elimina definitivamente dal database delle cassette postali di Exchange**    Exchange mantiene le cassette postali di archiviazione disconnesse in base alle impostazioni di conservazione delle cassette postali eliminate configurate per il database delle cassette postali. Il periodo di mantenimento predefinito è di 30 giorni. Una volta trascorso il periodo di conservazione specificato, una cassetta postale di archiviazione disconnessa viene eliminata dal database delle cassette postali di Exchange.
    
    Come per la cassetta postale principale disabilitata, è possibile eliminare in modo definitivo una cassetta postale di archiviazione disabilitata in qualsiasi momento utilizzando il cmdlet **Remove-StoreMailbox**. Per ulteriori informazioni, vedere [Eliminare definitivamente una cassetta postale](permanently-delete-a-mailbox-exchange-2013-help.md).

Utilizzo delle cassette postali disabilitate

## Utilizzo delle cassette postali con eliminazione reversibile

Una cassetta postale con eliminazione reversibile viene creata quando una cassetta postale viene spostata da un database delle cassette postali di Exchange a un altro database. Exchange non elimina completamente la cassetta postale dal database di origine dopo lo spostamento, per evitare la perdita della cassetta postale in caso di errore nel database di destinazione. In caso di errore, è possibile ripristinare la cassetta postale di origine e riprovare lo spostamento. Exchange manterrà la cassetta postale con eliminazione reversibile per l'intera durata del periodo di conservazione della cassetta postale.

È possibile eseguire due operazioni su una cassetta postale con eliminazione reversibile:

  - Ripristinarla in una cassetta postale esistente.

  - Eliminarla definitivamente dal database delle cassette postali di Exchange.

Le procedure da seguire per il ripristino e l'eliminazione definitiva di una cassetta postale con eliminazione reversibile sono le stesse di quelle utilizzate per una cassetta postale disabilitata. Per ulteriori informazioni, vedere i seguenti argomenti:

  - [Ripristinare una cassetta postale eliminata](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

  - [Eliminare definitivamente una cassetta postale](permanently-delete-a-mailbox-exchange-2013-help.md)

Utilizzo delle cassette postali disabilitate

## Riepilogo dell'utilizzo delle cassette postali disconnesse

Nella seguente tabella, vengono riepilogate le informazioni sulle cassette postali disconnesse, inclusa la modalità di disconnessione della cassetta postale, su cosa succede all'account utente di Active Directory corrispondente quando si disconnette una cassetta postale e le opzioni e gli strumenti di cui si dispone per la connessione o il ripristino delle cassette postali disconnesse.


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
<th>Modalità di disabilitazione della cassetta postale</th>
<th>Valore della proprietà <em>DisconnectReason</em></th>
<th>L'account utente di Active Directory viene mantenuto?</th>
<th>Connessione o ripristino delle opzioni</th>
<th>Strumenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Interfaccia di amministrazione di Exchange: <strong>Destinatari</strong> &gt; <strong>Cassette postali</strong> &gt; <strong>Disabilita</strong></p></li>
<li><p>Shell: cmdlet <strong>Disable-Mailbox</strong></p></li>
</ul></td>
<td><p>Disabilitata</p></td>
<td><p>Sì</p></td>
<td><p>Connessione allo stesso account utente</p></td>
<td><ul>
<li><p>Interfaccia di amministrazione di Exchange: <strong>Destinatari</strong> &gt; <strong>Cassette postali</strong> &gt; <strong>Connetti una cassetta postale</strong></p></li>
<li><p>Shell: cmdlet <strong>Connect-Mailbox</strong></p></li>
</ul></td>
</tr>
<tr class="even">
<td><ul>
<li><p>Interfaccia di amministrazione di Exchange: <strong>Destinatari</strong> &gt; <strong>Cassette postali</strong> &gt; <strong>Elimina</strong></p></li>
<li><p>Shell: cmdlet <strong>Remove-Mailbox</strong></p></li>
</ul></td>
<td><p>Disabilitata</p></td>
<td><p>No</p></td>
<td><ul>
<li><p>Connessione a un account utente differente</p></li>
<li><p>Ripristino in una cassetta postale differente</p></li>
</ul></td>
<td><ul>
<li><p>Interfaccia di amministrazione di Exchange: <strong>Destinatari</strong> &gt; <strong>Cassette postali</strong> &gt; <strong>Connetti una cassetta postale</strong></p></li>
<li><p>Shell: cmdlet <strong>Connect-Mailbox</strong></p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>Shell: cmdlet <strong>New-MailboxRestore</strong></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Spostamento in un database delle cassette postali differente</p></td>
<td><p>SoftDeleted</p></td>
<td><p>Sì</p></td>
<td><ul>
<li><p>Connessione a un account utente differente</p></li>
<li><p>Ripristino in una cassetta postale differente</p></li>
</ul></td>
<td><ul>
<li><p>Interfaccia di amministrazione di Exchange: <strong>Destinatari</strong> &gt; <strong>Cassette postali</strong> &gt; <strong>Connetti una cassetta postale</strong></p></li>
<li><p>Shell: cmdlet <strong>Connect-Mailbox</strong></p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>Shell: cmdlet <strong>New-MailboxRestore</strong></p></li>
</ul></td>
</tr>
</tbody>
</table>


Utilizzo delle cassette postali disabilitate

## Documentazione sulla cassetta postale disconnessa

Nella seguente tabella, sono riportati i collegamenti agli argomenti utili per la gestione delle cassette postali disconnesse. Ciò include la gestione delle cassette postali utente disconnesse, delle cassette postali collegate, delle cassette postali per le risorse e delle cassette postali condivise.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Argomento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="disable-or-delete-a-mailbox-exchange-2013-help.md">Disabilitazione o eliminazione di una cassetta postale</a></p></td>
<td><p>Ulteriori informazioni su come disabilitare o eliminare le cassette postali.</p></td>
</tr>
<tr class="even">
<td><p><a href="connect-a-disabled-mailbox-exchange-2013-help.md">Connettere una cassetta postale disabilitata</a></p></td>
<td><p>Ulteriori informazioni su come connettere una cassetta postale disabilitata a un account utente esistente.</p></td>
</tr>
<tr class="odd">
<td><p><a href="connect-or-restore-a-deleted-mailbox-exchange-2013-help.md">La connessione o il ripristino di una cassetta postale eliminata</a></p></td>
<td><p>Ulteriori informazioni su come connettere una cassetta postale eliminata a un account utente o ripristinare il contenuto di una cassetta postale eliminata in una cassetta postale esistente.</p></td>
</tr>
<tr class="even">
<td><p><a href="restore-a-soft-deleted-mailbox-exchange-2013-help.md">Ripristinare una cassetta postale eliminata</a></p></td>
<td><p>Ulteriori informazioni su come connettere una cassetta postale con eliminazione reversibile a un account utente o ripristinare una cassetta postale con eliminazione reversibile in una cassetta postale esistente.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mailbox-restore-requests-exchange-2013-help.md">Gestire le richieste di ripristino delle cassette postali</a></p></td>
<td><p>Ulteriori informazioni su come gestire le richieste di ripristino delle cassette postali tramite Shell.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><a href="permanently-delete-a-mailbox-exchange-2013-help.md">Eliminare definitivamente una cassetta postale</a></p></td>
<td><p>Ulteriori informazioni su come eliminare definitivamente una cassetta postale.</p></td>
</tr>
</tbody>
</table>


Utilizzo delle cassette postali disabilitate


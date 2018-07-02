---
title: 'Ripristinare una cassetta postale eliminata: Exchange 2013 Help'
TOCTitle: Ripristinare una cassetta postale eliminata
ms:assetid: 4f3f5ce4-9d12-4ed8-9f70-d8a6aa8a1b2e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ863435(v=EXCHG.150)
ms:contentKeyID: 50555586
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ripristinare una cassetta postale eliminata

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-29_

Connessione di una cassetta postale eliminata in maniera reversibile a un account utente di Active Directory tramite Shell. Una cassetta postale diventa *eliminata in maniera reversibile* nel database delle cassette postali di origine quando viene spostata su un diverso database delle cassette postali. Exchange non elimina completamente la cassetta postale dal database delle cassette postali di origine quando lo spostamento viene completato. la cassetta postale nel database di origine delle cassette postali passa allo stato di eliminata temporaneamente. Ciò consente di ripristinare la cassetta postale di origine nel caso in cui si verifichino errori durante lo spostamento che provochino un danneggiamento della cassetta postale nel database di destinazione. Se ciò accade, è possibile ripristinare la cassetta postale di origine e tentare di spostarla nuovamente.

Le cassette postali eliminate in maniera reversibile vengono mantenute nel database di origine fino alla scadenza del periodo di conservazione della cassetta postale o fino a quando non si utilizza il cmdlet **Remove-StoreMailbox** per eliminare la cassetta postale in maniera non reversibile. Finché una cassetta postale eliminata in maniera reversibile non sarà eliminata definitivamente dal database delle cassette postali di Exchange, è possibile utilizzare Shell per ripristinare i contenuti della cassetta postale eliminata in maniera reversibile su una cassetta postale esistente o una cassetta postale di archiviazione.

Per ulteriori informazioni sulle cassette postali eliminate in maniera reversibile e per eseguire altre attività di gestione correlate, vedere i seguenti argomenti:

  - [Cassette postali disconnesse](disconnected-mailboxes-exchange-2013-help.md)

  - [La connessione o il ripristino di una cassetta postale eliminata](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [Gestire le richieste di ripristino delle cassette postali](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [Eliminare definitivamente una cassetta postale](permanently-delete-a-mailbox-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Le procedure descritte in questo argomento possono essere eseguite solo in Shell. Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per ripristinare cassette postali eliminate in maniera reversibile.

  - Eseguire il comando riportato qui di seguito per verificare che la cassetta postale eliminata in maniera reversibile che si desidera collegare a un account utente esista ancora nel database delle cassette postali e non è una cassetta postale disattivata.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,DisconnectReason,DisconnectDate
    
    La cassetta postale eliminata in maniera reversibile deve esistere nel database delle cassette postali e il valore per la proprietà *DisconnectReason* deve essere `SoftDeleted`. Se la cassetta postale è stata eliminata dal database, il comando non restituirà nessun risultato.
    
    In alternativa, eseguire il comando riportato qui di seguito per visualizzare tutte le cassette postali eliminate in maniera reversibile nell'organizzazione.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | fl DisplayName,DisconnectReason,DisconnectDate

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## Ripristino di una cassetta postale eliminata in maniera reversibile tramite Shell

È possibile utilizzare Shell per ripristinare una cassetta postale eliminata in maniera reversibile su una cassetta postale esistente utilizzando il cmdlet **New-MailboxRestoreRequest**. Quando si ripristina una cassetta postale eliminata in maniera non reversibile, i contenuti vengono copiati su una cassetta postale esistente, che viene denominata *cassetta postale di destinazionee*. Dopo che una richiesta di ripristino della cassetta postale sarà stata completata con esito positivo, la richiesta verrà conservata per impostazione predefinita per 30 giorni prima di essere rimossa. È possibile rimuoverla prima di utilizzare il **Remove-MailboxRestoreRequest** cmdlet.

Dopo che la cassetta postale eliminata in maniera reversibile sarà stata ripristinata, verrà mantenuta nel database delle cassette postali finché non sarà eliminata definitivamente da un amministratore o eliminata quando il periodo di conservazione della cassetta postale sarà scaduto.

Per creare una richiesta di ripristino di una cassetta postale, è necessario utilizzare il nome visualizzato, il GUID della cassetta postale o il nome distinto legacy (DN) della cassetta postale eliminata in maniera reversibile. Utilizzare il cmdlet **Get-MailboxStatistics** per visualizzare i valori del **DisplayName**, **MailboxGuid** e le proprietà **LegacyDN** per la casella postale eliminata in maniera non reversibile che si desidera ripristinare. Ad esempio, eseguire il comando riportato qui di seguito per restituire queste informazioni per tutte le caselle postali eliminate in maniera reversibile nell'organizzazione.

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "SoftDeleted"} | fl DisplayName,MailboxGuid,LegacyDN,Database

In questo esempio viene ripristinata una cassetta postale eliminata in maniera reversibile, che viene eliminata con il nome visualizzato nel parametro *SourceStoreMailbox* e si trova nel database della cassetta postale MBXDB01, sulla cassetta postale destinazione denominata Debra Garcia. Il parametro *AllowLegacyDNMismatch* viene utilizzato in modo che la cassetta postale di origine possa essere ripristinata su una cassetta postale che non ha lo stesso valore nome distinto legacy (DN) della cassetta postale eliminata in maniera reversibile.

    New-MailboxRestoreRequest -SourceStoreMailbox "Debra Garcia" -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

In questo esempio, la cassetta postale di archiviazione di Pilar Pinilla eliminata in maniera reversibile, che è identificata dal GUID della cassetta postale, viene ripristinata sulla sua attuale cassetta postale di archiviazione. Il parametro *AllowLegacyDNMismatch* non è necessario perché una cassetta postale primaria e la corrispondente cassetta postale di archiviazione hanno lo stesso nome distinto legacy (DN).

    New-MailboxRestoreRequest -SourceStoreMailbox dc35895a-a628-4bba-9aa9-650f5cdb9ae7 -SourceDatabase MBXDB02 -TargetMailbox pilarp@contoso.com -TargetIsArchive

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829875\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che una cassetta postale eliminata in maniera reversibile sia stata ripristinata con esito positivo sulla cassetta postale di destinazione, eseguire il cmdlet **Get-MailboxRestoreRequest** o il cmdlet **Get-MailboxRestoreRequestStatistics** per visualizzare le informazioni sulla richiesta di ripristino. Se la richiesta di ripristino è stata creata con esito positivo, la proprietà *Status* avrà un valore di **Queued**, **InProgress** o **Completed**. Dopo che la richiesta di ripristino sarà stata completata, i contenuti della cassetta postale eliminata in maniera reversibile appariranno nella cassetta postale di destinazione.

Per ulteriori informazioni, vedere:

  - [Gestire le richieste di ripristino delle cassette postali](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [Get-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829907\(v=exchg.150\))

  - [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/it-it/library/ff829912\(v=exchg.150\))


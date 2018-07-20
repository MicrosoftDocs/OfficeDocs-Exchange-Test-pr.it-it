---
title: 'Eliminare definitivamente una cassetta postale: Exchange 2013 Help'
TOCTitle: Eliminare definitivamente una cassetta postale
ms:assetid: df35765a-0bef-4561-9846-d91d69c0269c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ863440(v=EXCHG.150)
ms:contentKeyID: 50555703
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Eliminare definitivamente una cassetta postale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-16_

Quando si eliminano in maniera definitiva le cassette postali attive e quelle disconnesse, tutto il contenuto relativo viene eliminato dal database delle cassette postali di Exchange con perdita di dati permanente. Quando si elimina definitivamente una cassetta postale attiva, viene eliminato l'account utente di Active Directory associato.

Un'alternativa per eliminare definitivamente una cassetta postale è disconnetterla. Dopo che è stata disconnessa, per impostazione predefinita, la cassetta postale viene conservata nel database relativo per 30 giorni. In questo modo è possibile riconnettere o ripristinare una cassetta postale prima che venga eliminata dal database.

Per ulteriori informazioni sulle cassette postali disconnesse e per eseguire altre attività di gestione relative, vedere gli argomenti seguenti:

  - [Cassette postali disconnesse](disconnected-mailboxes-exchange-2013-help.md)

  - [Disabilitazione o eliminazione di una cassetta postale](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [Connettere una cassetta postale disabilitata](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [La connessione o il ripristino di una cassetta postale eliminata](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)


> [!NOTE]
> Non è possibile utilizzare EAC per eliminare definitivamente una cassetta postale attiva o disconnessa.



## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Eliminare definitivamente una cassetta postale attiva

## Eliminazione permanente di una cassetta postale attiva tramite Shell

Eseguire il comando seguente per eliminare definitivamente una cassetta postale attiva e l'account utente Active Directory associato.

    Remove-Mailbox -Identity <identity> -Permanent $true


> [!NOTE]
> Se non viene incluso il parametro <EM>Permanent</EM>, per impostazione predefinita, la cassetta postale eliminata viene conservata nel database delle cassette postali per 30 giorni prima di essere eliminata definitivamente.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-Mailbox](https://technet.microsoft.com/it-it/library/aa995948\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta eliminazione definitiva di una cassetta postale attiva, effettuare le operazioni seguenti:

1.  Verificare che la cassetta postale non sia più elencata in EAC.

2.  Verificare che l'account utente associato non sia elencato in Utenti e computer di Active Directory.

3.  Eseguire il comando riportato di seguito per verificare che la cassetta postale sia stata eliminata correttamente dal database delle cassette postali di Exchange.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }
    
    Se la cassetta postale è stata eliminata correttamente, il comando non restituirà alcun risultato. Se la cassetta postale non è stata eliminata, il comando restituirà le informazioni relative alla cassetta postale.

## Eliminare in maniera definitiva una cassetta postale disconnessa

## Rimozione permanente di una cassetta postale disconnessa tramite Shell

Esistono due tipi di cassette postali disconnesse: disabilitate e con eliminazione reversibile. Quando si esegue il cmdlet per eliminare definitivamente la cassetta postale, è necessario specificare uno di questi tipi. Se il tipo specificato non corrisponde al tipo effettivo della cassetta postale disconnessa, il comando non viene completato.

Eseguire il comando riportato di seguito per determinare se la cassetta postale disconnessa è disabilitata o eliminata in maniera reversibile.

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,MailboxGuid,Database,DisconnectReason

Il valore della proprietà *DisconnectReason* per le cassette postali disconnesse sarà `Disabled` o `SoftDeleted`.

È possibile eseguire il comando seguente per visualizzare il tipo di tutte le cassette postali disconnesse nell'organizzazione.

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -ne $null } | fl DisplayName,MailboxGuid,Database,DisconnectReason


> [!WARNING]
> Quando si utilizza il cmdlet <STRONG>Remove-StoreMailbox</STRONG> per eliminare definitivamente una cassetta postale disconnessa, tutto il contenuto viene eliminato dal database delle cassette postali e la perdita dei dati è permanente.



In questo esempio viene eliminata permanentemente la cassetta postale disabilitata con GUID 2ab32ce3-fae1-4402-9489-c67e3ae173d3 dal database delle cassette postali MBD01.

    Remove-StoreMailbox -Database MBD01 -Identity "2ab32ce3-fae1-4402-9489-c67e3ae173d3" -MailboxState Disabled

Con questo esempio viene eliminata permanentemente la cassetta postale con eliminazione reversibile di Dan Jump dal database delle cassette postali MBD01.

    Remove-StoreMailbox -Database MBD01 -Identity "Dan Jump" -MailboxState SoftDeleted

In questo esempio vengono eliminate permanentemente tutte le cassette postali con eliminazione reversibile dal database delle cassette postali MBD01.

    Get-MailboxStatistics -Database MBD01 | where {$_.DisconnectReason -eq "SoftDeleted"} | ForEach {Remove-StoreMailbox -Database $_.Database -Identity $_.MailboxGuid -MailboxState SoftDeleted}

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-StoreMailbox](https://technet.microsoft.com/it-it/library/ff829913\(v=exchg.150\)) e [Get-MailboxStatistics](https://technet.microsoft.com/it-it/library/bb124612\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta eliminazione definitiva di una cassetta postale disconnessa dal database delle cassette postali di Exchange, eseguire il comando seguente.

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }

Se la cassetta postale è stata eliminata correttamente, il comando non restituirà alcun risultato. Se la cassetta postale non è stata eliminata, il comando restituirà le informazioni relative alla cassetta postale.


---
title: 'Archiviazione sul posto una cassetta postale di conservazione: Exchange 2013 Help'
TOCTitle: Archiviazione sul posto una cassetta postale di conservazione
ms:assetid: 2baac4a7-3402-4142-bfb3-1649a950e677
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335168(v=EXCHG.150)
ms:contentKeyID: 50480307
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Archiviazione sul posto una cassetta postale di conservazione

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-14_

La conservazione di una cassetta postale sospende l'elaborazione di un criterio di conservazione o di un criterio cassetta postale per cartelle gestite per tale cassetta postale. La conservazione è progettata per gli scenari in cui, ad esempio, un utente è in vacanza o non è al computer per un breve periodo di tempo.

Durante la conservazione, gli utenti possono accedere alla cassetta postale e modificare o eliminare gli elementi. Quando si esegue una ricerca nella cassetta postale, gli elementi eliminati che hanno superato il periodo di conservazione non vengono restituiti nei risultati della ricerca. Per garantire che gli elementi modificati o eliminati dagli utenti vengano conservati negli scenari di conservazione legale, è necessario selezionare una cassetta postale per la conservazione legale. Per ulteriori informazioni, vedere [Creare o rimuovere un'archiviazione sul posto](create-or-remove-an-in-place-hold-exchange-2013-help.md).

È possibile anche includere i commenti di conservazione per le cassette postali per le quali si desidera la conservazione. I commenti vengono visualizzati nelle versioni supportate di Microsoft Outlook.

Per altre attività di gestione relative a Gestione record di messaggistica, vedere [Messaggistica Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione record di messaggistica" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per applicare la conservazione a una cassetta postale. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Conservazione di una cassetta postale tramite Shell

In questo esempio viene eseguita la conservazione della cassetta postale di Michael Allen.

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $true

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Eliminazione della conservazione per una cassetta postale tramite Shell

In questo esempio viene eliminata la conservazione per la cassetta postale di Michael Allen.

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $false

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente applicato la conservazione a una cassetta postale, utilizzare il cmdlet [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) per recuperare la proprietà *RetentionHoldEnabled* della cassetta postale.

Questo comando consente di visualizzare la proprietà *RetentionHoldEnabled* per la cassetta postale di Michael Allen.

    Get-Mailbox "Michael Allen" | Select RetentionHoldEnabled

Questo comando consente di visualizzare tutte le cassette postali nell'organizzazione Exchange, di filtrare quelle a cui è applicata la conservazione e di visualizzarle in un elenco con il criterio di conservazione applicato loro.


> [!IMPORTANT]
> Dal momento che <EM>RetentionHoldEnabled</EM> non è una proprietà filtrabile in Exchange 2013, non è possibile utilizzare il parametro <EM>Filter</EM> con il cmdlet <STRONG>Get-Mailbox</STRONG> per filtrare le cassette postali a cui è applicata la conservazione sul lato server. Questo comando consente di visualizzare un elenco di tutte le cassette postali e di filtrarle sul client su cui è attiva la sessione di Shell. Negli ambienti di grandi dimensioni in cui sono presenti migliaia di cassette postali, il completamento dell'operazione potrebbe richiedere molto tempo.



    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionHoldEnabled -eq $true} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto


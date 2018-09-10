---
title: 'Ottenere le statistiche cartella elementi ripristinabili: Exchange 2013 Help'
TOCTitle: Ottenere le statistiche cartella elementi ripristinabili
ms:assetid: dee77958-ee87-4908-85e4-ad053bacd8b0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff714343(v=EXCHG.150)
ms:contentKeyID: 52063104
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ottenere le statistiche cartella elementi ripristinabili

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-01-22_

La cartella elementi ripristinabili contiene gli elementi eliminati da Microsoft Outlook e Microsoft OfficeOutlook Web App utenti o dall'Assistente delle cassette postali. La durata di permanenza degli elementi eliminati in questa cartella è basato sulle impostazioni di mantenimento elementi eliminati configurate per il database delle cassette postali o per la cassetta postale. Per impostazione predefinita, un database delle cassette postali è configurato per conservare gli elementi eliminati 14 giorni e la quota di avviso degli elementi recuperabili e degli elementi recuperabili quote sono impostate su 20 gigabyte (GB) e 30 GB rispettivamente. Tuttavia, se conservazione In locale o conservazione per controversia legale è abilitata per la cassetta postale, gli elementi recuperabili può vengono accumulati cartella Posta eliminata oltre il periodo di conservazione specificato e può inoltre mantenere versioni diverse di elementi della cassetta postale modificata.

Quando la cartella elementi ripristinabili raggiunge la quota di avviso degli elementi recuperabili, un evento di avviso viene registrato nel registro eventi dell'applicazione. Se non è presente la cassetta postale di conservazione per controversia legale, gli elementi vengono rimosse in una funzionalità in base prima FIFO. Tuttavia, se la cassetta postale di conservazione per controversia legale, la cassetta postale non viene mai svuotata e al sta per raggiungere la quota degli elementi recuperabili, la funzionalità cassette postali è interessata.

Di conseguenza, è importante controllare il registro eventi per gli avvisi generati quando le cassette postali di raggiungono le quote degli elementi recuperabili. È anche possibile utilizzare la procedura seguente per le statistiche di report per la cartella elementi ripristinabili, in particolare per le cassette postali inserita nella conservazione per controversia legale.

Per ulteriori informazioni, vedere gli argomenti seguenti:

  - [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md)

  - [Archiviazione sul posto e conservazione per controversia legale](https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-and-litigation-holds)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cartelle delle cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange (EAC) per recuperare le statistiche relative alla cartella degli elementi ripristinabili per una cassetta postale.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Operazione desiderata

## Richiamo delle statistiche relative alla cartella di elementi ripristinabili per una cassetta postale

In questo esempio le statistiche relative alla cartella degli elementi ripristinabili per Soumya Singhi vengono recuperate e visualizzate sotto forma di elenco.

    Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-List

In questo esempio vengono recuperate le statistiche relative alla cartella degli elementi ripristinabili per Soumya Singhi e viene visualizzata una tabella contenente il nome, il percorso, il numero degli elementi inclusi e la dimensione della cartella.

    Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-Table Name,FolderPath,ItemsInFolder,FolderAndSubfolderSize

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-MailboxFolderStatistics](https://technet.microsoft.com/it-it/library/aa996762\(v=exchg.150\)).

## Ottenere le statistiche cartella elementi recuperabili per tutte le cassette postali conservazione per controversia legale

In questo esempio viene recuperato un elenco di tutte le cassette postali inserita nella conservazione per controversia legale e consente di recuperare le statistiche per la cartella elementi recuperabili della cassetta postale e le relative sottocartelle per ciascuna cassetta postale. Proprietà **FolderAndSubfolderSize** e **Identity** (identità cartella della cassetta postale) vengono visualizzate in formato tabella.

    Get-Mailbox -ResultSize Unlimited -Filter {LitigationHoldEnabled -eq $true} | Get-MailboxFolderStatistics | Format-Table Identity,FolderAndSubfolderSize

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) e [Get-MailboxFolderStatistics](https://technet.microsoft.com/it-it/library/aa996762\(v=exchg.150\)).

## Ottenere quota degli elementi recuperabili per una cassetta postale

In questo esempio visualizza la quota e quota di avviso per la cartella elementi recuperabili per una cassetta postale utente. Nell'esempio viene recuperato anche informazioni se viene effettuata una conservazione per controversia legale o an In-Place Hold sulla cassetta postale.

    Get-Mailbox -Identity <identity of mailbox> | Format-List RecoverableItems*,LitigationHoldEnabled,InPlaceHolds

Questo esempio visualizza le quote e quota di avviso per la cartella elementi recuperabili per tutte le cassette postali nell'organizzazione. Nell'esempio viene recuperato anche informazioni relative alle esenzioni.

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Format-List Name,RecoverableItems*,LitigationHoldEnabled,InPlaceHolds


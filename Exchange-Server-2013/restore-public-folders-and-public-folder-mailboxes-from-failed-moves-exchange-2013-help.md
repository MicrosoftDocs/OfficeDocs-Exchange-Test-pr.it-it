---
title: 'Riprist. cart. pubbl./cass. post. da spost. non riusciti: Exchange 2013 Help'
TOCTitle: Ripristinare le cartelle pubbliche e cassette postali delle cartelle pubbliche da spostamenti non riusciti
ms:assetid: 2ade83c9-5f9b-4945-bf32-48fa8185b515
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ983802(v=EXCHG.150)
ms:contentKeyID: 52063055
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ripristinare le cartelle pubbliche e cassette postali delle cartelle pubbliche da spostamenti non riusciti

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-13_

Se una richiesta di spostamento per una cartella pubblica o per una cassetta postale della cartella pubblica non riesce, è possibile ripristinare la cartella o la cassetta postale fintanto che si applicano le condizioni riportate di seguito:

  - **Spostamento della cartella pubblica non riuscito**   Una copia della cartella pubblica eliminata in maniera reversibile esiste ancora nella cassetta postale della cartella pubblica di origine e si trova ancora nel periodo di mantenimento.

  - **Spostamento della cassetta postale della cartella pubblica non riuscito**   Una copia della cassetta postale della cartella pubblica eliminata in maniera reversibile esiste ancora nel database delle cassette postali di origine e si trova ancora nel periodo di mantenimento delle cassette postali.

Se il periodo di mantenimento della cassetta postale è scaduto, è possibile recuperare una singola cassetta postale della cartella pubblica dal backup. Successivamente è possibile estrarre i dati dalla cassetta postale ripristinata e copiarli in una cartella di destinazione o unirli a un'altra cassetta postale. Per ulteriori informazioni, vedere [Recupero dei dati utilizzando un database di ripristino](restore-data-using-a-recovery-database-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Richiesta di ripristino della cassetta postale" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare Shell.

  - Per creare una richiesta di ripristino, è necessario fornire i valori per i parametri *DisplayName*, *LegacyDN* o *MailboxGUID* per la cassetta postale della cartella pubblica eliminata in maniera reversibile.

  - Per impostazione predefinita, le cartelle dumpster verranno ripristinate insieme alle cartelle normali. Questa viene specificata utilizzando il parametro *ExcludeDumpster*.

  - Se le cassette postali della cartella pubblica da ripristinare sono diverse dalle cassette postali normali, non verranno create in quelle cartelle se non esistono nella cassetta postale di destinazione. Le cartelle mancanti verranno visualizzate in un messaggio di avviso al termine della richiesta di ripristino.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Ripristino di una cartella pubblica eliminata in maniera reversibile

In questo esempio viene ripristinata la cartella pubblica \\Dev\\CustomerEnagagements nella cassetta postale della cartella pubblica di destinazione Development01.

    New-MailboxRestoreRequest -SourceStoreMailbox Development -SourceDatabase MBX_DB01 -TargetMailbox Development01 -AllowLegacyDNMismatch -IncludeFolders \Dev\CustomerEngagements

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829875\(v=exchg.150\)).

## Ripristino di una cassetta postale della cartella pubblica eliminata in maniera reversibile

In questo esempio viene ripristinata la cassetta postale della cartella pubblica PF\_Singapore in una nuova cassetta postale della cartella pubblica PF\_Singapore\_Restore.

    New-MailboxRestoreRequest -SourceStoreMailbox PF_Singapore -SourceDatabase MBX_DB01 -TargetMailbox PF_Singapore_Restore -AllowLegacyDNMismatch

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829875\(v=exchg.150\)).


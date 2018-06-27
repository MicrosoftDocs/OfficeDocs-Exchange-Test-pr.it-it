---
title: 'Spostare una cassetta postale di cartelle pubbliche a un database delle cassette postali diverse: Exchange 2013 Help'
TOCTitle: Spostare una cassetta postale di cartelle pubbliche a un database delle cassette postali diverse
ms:assetid: 67601d45-4824-4ae6-9a7e-b645ec3af4d3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ906434(v=EXCHG.150)
ms:contentKeyID: 51407379
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Spostare una cassetta postale di cartelle pubbliche a un database delle cassette postali diverse

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-07-21_

Potrebbe essere necessario spostare una cassetta postale delle cartelle pubbliche in un diverso database delle cassette postali per bilanciare il carico o per spostare le risorse in modo che siano più coerenti alla relativa collocazione geografica. Affine allo spostamento di una casetta postale normale, si utilizzano i cmdlet **MoveRequest** per spostare una cassetta postale delle cartelle pubbliche. Per ulteriori informazioni sullo spostamento di cassette postali, vedere [Spostamenti di cassette postali di Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Il tempo stimato per il completamento dipende dalla dimensione della cassetta postale delle cartelle pubbliche.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di migrazione e spostamento delle cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Non è possibile eseguire questa procedura nell'interfaccia di amministrazione di Exchange. È possibile eseguire questa procedura esclusivamente in Shell.

  - A seconda delle dimensioni della cassetta postale delle cartelle pubbliche, lo spostamento potrebbe richiedere diverse ore per il completamento. Durante lo spostamento, non è possibile per gli utenti accedere alle cartelle pubbliche. Gli utenti, inoltre, non hanno accesso alle cartelle pubbliche per il breve periodo in cui la cartella risulta in uno stato di "Completamento in corso".

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Creazione di una richiesta di spostamento

Il cmdlet **New-MoveRequest** cmdlet inserisce la cassetta postale delle cartelle pubbliche nella coda del servizio di replica delle cassette postali di Microsoft Exchange. Quando il servizio di replica delle cassette postali di Microsoft Exchange risulta disponibile, per il suo tramite viene raccolta la richiesta di spostamento e lo spostamento della cassetta postale delle cartelle pubbliche inizia. L'intera richiesta viene completata dall'inizio alla fine.

In questo esempio, viene mostrato come inizia la richiesta di spostamento per la cassetta postale delle cartelle pubbliche PF\_SanFrancisco verso il database della cassetta postale MBX\_DB01.

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\)).

## Creazione di una richiesta di spostamento da completare in un secondo momento

Durante la fase finale della richiesta di spostamento, quando è in fase di `CompletionInProgress` , gli utenti possono essere temporaneamente bloccati la cassetta postale di cartelle pubbliche. Se necessario, è possibile sospendere la richiesta di spostamento prima che raggiunga tale fase e riprendere l'applicazione alla volta quando gli utenti non essere influenzati.

In questo esempio viene mostrato come inizia la richiesta di spostamento per la cassetta postale delle cartelle pubbliche PF\_SanFrancisco nel database della cassetta postale MBX\_DB01 e come viene sospeso quando la richiesta di spostamento è pronta per il completamento.

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01 -SuspendWhenReadyToComplete

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\)).

In questo esempio viene recuperato lo stato di spostamento della cassetta postale in corso nella cassetta postale delle cartelle pubbliche PF\_SanFrancisco.

    Get-MoveRequest -Identity "PF_SanFrancisco"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-MoveRequest](https://technet.microsoft.com/it-it/library/dd335227\(v=exchg.150\)).

Quando la richiesta di spostamento raggiunge lo stato di Sospeso, è possibile riprendere la richiesta. In questo esempio viene ripresa la richiesta di spostamento per la cassetta postale delle cartelle pubbliche PF\_SanFrancisco.

    Resume-MoveRequest -Identity "PF_SanFrancisco"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Resume-MoveRequest](https://technet.microsoft.com/it-it/library/ee332320\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la richiesta di spostamento è stata creata correttamente, eseguire il seguente comando:

    Get-MoveRequestStatistics -Identity PF_SanFrancisco | Format-List Status

Uno stato di `Completed` indica che la richiesta di spostamento è stata completata correttamente.

Se la richiesta di spostamento non è stata completata, potrebbe essere necessario ripristinare la cartella pubblica. Per ulteriori informazioni, vedere [Ripristinare le cartelle pubbliche e cassette postali delle cartelle pubbliche da spostamenti non riusciti](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).


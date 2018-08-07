---
title: 'Sposta cart. pubb. in cass. postale cartelle pubb. diverse: Exchange 2013 Help'
TOCTitle: Spostare una cartella pubblica in una cassetta postale di cartelle pubbliche diversi
ms:assetid: b8744934-a3cb-443e-acce-a9a6ca5d88f6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ906435(v=EXCHG.150)
ms:contentKeyID: 51407402
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Spostare una cartella pubblica in una cassetta postale di cartelle pubbliche diversi

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-11-16_

Se il contenuto di una cassetta postale delle cartelle pubbliche inizia a superare le quote delle cassette postali, potrebbe essere necessario spostare le cartelle pubbliche in un'altra cassetta postale. È possibile eseguire questa operazione in due modi. Per spostare una o più cartelle pubbliche che non contengono sottocartelle, è possibile utilizzare i cmdlet **PublicFolderMoveRequest**. Per spostare un intero ramo di cartelle pubbliche, che include la cartella pubblica padre e tutte le sottocartelle, è possibile utilizzare lo script `Move-PublicFolderBranch.ps1` disponibile durante l'installazione di Exchange 2013.

Per ulteriori attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Il tempo stimato per il completamento di questa attività dipende dalla dimensione della cartella pubblica.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cartelle pubbliche" nell'argomento [Autorizzazioni di condivisione e collaborazione](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure non è possibile utilizzare EAC, è necessario utilizzare Shell.

  - Se la cartella da spostare contiene sottocartelle, queste non verranno spostate per impostazione predefinita. Per spostare una cartella pubblica e tutte le relative sottocartelle, utilizzare lo script **Move-PublicFolderBranch.ps1**.

  - Lo spostamento delle cartelle pubbliche consente di spostare solo il contenuto fisico della cartella pubblica, senza cambiare la gerarchia logica.

  - A seconda della dimensione della cartella pubblica e della quantità di dati contenuti, lo spostamento potrebbe richiedere diverse ore. Durante questo tempo, gli utenti possono accedere alle cartelle pubbliche, tranne che per un breve periodo di tempo in cui la cartella è in stato "Completamento in corso".

  - È possibile eseguire una sola richiesta di spostamento delle cartelle pubbliche alla volta. Per rimuovere la richiesta dopo averla completata, è necessario utilizzare il cmdlet **Remove-PublicFolderMoveRequest**.

  - Per verificare lo stato di una richiesta di spostamento delle cartelle pubbliche in corso, eseguire il cmdlet [Get-PublicFolderMoveRequest](https://technet.microsoft.com/it-it/library/jj878076\(v=exchg.150\)).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Spostamento di una singola cartella pubblica

In questo esempio viene avviata la richiesta di spostamento per la cartella pubblica \\CustomerEnagagements dalla cassetta postale delle cartelle pubbliche DeveloperReports a DeveloperReports01

    New-PublicFolderMoveRequest -Folders \DeveloperReports\CustomerEngagements -TargetMailbox DeveloperReports01


> [!NOTE]
> Cassetta postale di cartelle pubbliche di destinazione verrà bloccata mentre è attiva la richiesta di spostamento.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-PublicFolderMoveRequest](https://technet.microsoft.com/it-it/library/jj878081\(v=exchg.150\)).

## Spostamento di più cartelle pubbliche

In questo esempio viene iniziata la richiesta di spostamento per le cartelle pubbliche appartenenti al ramo \\Dev nella cassetta postale delle cartelle pubbliche di destinazione DeveloperReports01. In questo esempio la cartella pubblica \\Dev non viene spostata.

    New-PublicFolderMoveRequest -Folders \Dev\CustomerEngagements,\Dev\RequestsforChange,\Dev\Usability -TargetMailbox DeveloperReports01


> [!NOTE]
> Cassetta postale di cartelle pubbliche di destinazione verrà bloccata mentre è attiva la richiesta di spostamento.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-PublicFolderMoveRequest](https://technet.microsoft.com/it-it/library/jj878081\(v=exchg.150\)).

## Spostamento di un ramo di cartelle pubbliche

In questo esempio viene utilizzato lo script `Move-PublicFolderBranch.ps1` per spostare un ramo di cartelle pubbliche. Viene avviata la richiesta di spostamento per la cartella pubblica \\Dev e tutte le relative sottocartelle nella cassetta postale delle cartelle pubbliche DeveloperReports01. Lo script si trova nella cartella degli script e deve essere eseguito da tale posizione.

    CD $env:ExchangeInstallPath\scripts
    
    .\Move-PublicFolderBranch.ps1 -FolderRoot \Dev -TargetPublicFolderMailbox DeveloperReports01

## Come verificare se l'operazione ha avuto esito positivo

Per verificare l'esito dello spostamento delle cartelle pubbliche, utilizzare il seguente comando:

    Get-PublicFolderMoveRequest | Format-List Status

Lo stato `Completed` indica che la richiesta di spostamento ha avuto esito positivo.

In caso di esito negativo, è necessario ripristinare la cartella pubblica o il relativo contenuto. Per ulteriori informazioni, vedere [Ripristinare le cartelle pubbliche e cassette postali delle cartelle pubbliche da spostamenti non riusciti](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).


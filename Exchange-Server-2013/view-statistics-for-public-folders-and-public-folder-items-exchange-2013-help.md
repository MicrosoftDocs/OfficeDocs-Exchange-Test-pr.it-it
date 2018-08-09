---
title: 'Visualizza statistiche/elementi cartelle pubbliche: Exchange 2013 Help'
TOCTitle: Visualizzare le statistiche per le cartelle pubbliche e gli elementi della cartella pubblica
ms:assetid: 4e412710-9a74-4649-ab01-502e969a7eda
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997949(v=EXCHG.150)
ms:contentKeyID: 50480645
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizzare le statistiche per le cartelle pubbliche e gli elementi della cartella pubblica

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-14_

In questo argomento viene descritto come recuperare le statistiche su una cartella pubblica, ad esempio il nome visualizzato, la data di creazione, l'ora dell'ultima modifica, l'ultimo accesso da parte dell'utente e la dimensione dell'elemento. È possibile utilizzare queste informazioni per decidere se eliminare o mantenere le cartelle pubbliche.


> [!NOTE]
> Nell'interfaccia di amministrazione di Exchange, è possibile visualizzare alcune delle quote e le informazioni di utilizzo per le cartelle pubbliche accedendo a <STRONG>Cartelle pubbliche</STRONG> &gt; <STRONG>Modifica</STRONG><IMG title="Icona Modifica" alt="Icona Modifica" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif"> &gt; <STRONG>Utilizzo cassetta postale</STRONG>. Tuttavia, queste informazioni sono incomplete e si raccomanda di utilizzare Shell per visualizzare le statistiche delle cartelle pubbliche.



Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche in Office 365 ed Exchange Online](https://technet.microsoft.com/it-it/library/jj966272\(v=exchg.150\)).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cartelle pubbliche" nell'argomento [Autorizzazioni di condivisione e collaborazione](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per recuperare le statistiche sulle cartelle pubbliche.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Recupero delle statistiche sulle cartelle pubbliche tramite Shell

In questo esempio vengono restituite le statistiche sulla cartella pubblica Marketing con un comando reindirizzato per formattare l'elenco.

    Get-PublicFolderStatistics -Identity \Marketing | Format-List


> [!NOTE]
> Il valore per il parametro <EM>Identity</EM> deve includere il percorso alla cartella pubblica. Ad esempio, se la cartella pubblica Marketing fosse contenuta nella cartella padre Business, sarebbe necessario fornire il seguente valore: <CODE>\Business\Marketing</CODE>



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-PublicFolderStatistics](https://technet.microsoft.com/it-it/library/aa998663\(v=exchg.150\)).

## Utilizzo di Shell per la visualizzazione delle statistiche relative agli elementi delle cartelle pubbliche

È possibile visualizzare le seguenti informazioni sugli elementi in una cartella pubblica:

  - Tipo di elemento

  - Oggetto

  - Data/ora dell'ultima modifica da parte dell'utente

  - Data/ora dell'ultimo accesso da parte dell'utente

  - Data/ora di creazione

  - Allegati

  - Dimensione messaggio

È possibile utilizzare queste informazioni per stabilire quali azioni intraprendere sulle cartelle pubbliche (ad esempio, quali eliminare). Ad esempio, si potrebbe voler eliminare una cartella pubblica se i suoi elementi non sono stati utilizzati per più di due anni oppure si potrebbe voler convertire una cartella pubblica utilizzata come repository di documenti in un'altra applicazione con accesso client.

In questo esempio vengono restituite le statistiche predefinite per tutti gli elementi nella cartella pubblica Pamphlets sotto il percorso \\Marketing\\2013. Tra le informazioni predefinite sono incluse l'identità degli elementi, la data di creazione e l'oggetto.

    Get-PublicFolderItemStatistics -Identity "\Marketing\2013\Pamphlets"

In questo esempio vengono restituite ulteriori informazioni sugli elementi all'interno della cartella pubblica Pamphlet come oggetto, ora dell'ultima modifica, data di creazione, allegati, dimensione dei messaggi e tipo di articolo. Include anche un comando reindirizzato per formattare l'elenco.

    Get-PublicFolderItemStatistics -Identity "\Marketing\2010\Pamphlets" | Format-List

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-PublicFolderItemStatistics](https://technet.microsoft.com/it-it/library/ee332344\(v=exchg.150\)).

## Utilizzo di Shell per l'esportazione dell'output del cmdlet Get-PublicFolderItemStatistics in un file .csv

In questo esempio viene esportato l'output del cmdlet al file PFItemStats.csv contenente le seguenti informazioni per tutti gli elementi all'interno della cartella pubblica \\Marketing\\Reports:

  - Oggetto del messaggio (`Subject`)

  - Data e ora dell'ultima modifica dell'elemento (`LastModificationTime`)

  - Presenza o meno di allegati (`HasAttachments`)

  - Tipo di elemento (`ItemType)`)

  - Dimensioni dell'elemento (`MessageSize`)

<!-- end list -->

    Get-PublicFolderItemStatistics -Identity "\Marketing\Reports" | Select Subject,LastModificationTime,HasAttachments,ItemType,MessageSize | Export-CSV C:\PFItemStats.csv

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-PublicFolderItemStatistics](https://technet.microsoft.com/it-it/library/ee332344\(v=exchg.150\)).


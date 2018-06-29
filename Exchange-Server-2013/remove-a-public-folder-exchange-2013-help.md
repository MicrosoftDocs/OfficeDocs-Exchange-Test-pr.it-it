---
title: 'Rimuovere una cartella pubblica: Exchange 2013 Help'
TOCTitle: Rimuovere una cartella pubblica
ms:assetid: 334b831d-e372-4d85-a407-5c8a5d0e78de
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997202(v=EXCHG.150)
ms:contentKeyID: 50480287
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere una cartella pubblica

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-11-16_

Potrebbe essere necessario rimuovere le cartelle pubbliche che non vengono più utilizzate nell'organizzazione. Per stabilire quali cartelle pubbliche devono essere rimosse, vedere [Visualizzare le statistiche per le cartelle pubbliche e gli elementi della cartella pubblica](view-statistics-for-public-folders-and-public-folder-items-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche](public-folder-procedures-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alle cartelle pubbliche, vedere [Procedure per le cartelle pubbliche in Office 365 ed Exchange Online](https://technet.microsoft.com/it-it/library/jj966272\(v=exchg.150\)).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cartelle pubbliche" nell'argomento [Autorizzazioni di condivisione e collaborazione](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Non è possibile eliminare una cartella pubblica abilitata per la posta. Per poterla eliminare, è necessario innanzitutto disabilitarla per la posta elettronica. Per ulteriori informazioni, vedere [Posta elettronica attiva o Disattiva posta una cartella pubblica](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Rimozione di una cartella pubblica tramite l'interfaccia di amministrazione di Exchange

1.  Accedere a **Cartelle pubbliche** \> **Cartelle pubbliche**.

2.  Nella visualizzazione elenco, selezionare la cartella pubblica che si desidera eliminare. Si noti che facendo clic sul nome della cartella verranno visualizzati le sottocartelle in essa contenuti, eventuali. A questo punto è possibile fare clic su una specifica sottocartella da rimuovere.
    
    Per eliminare una cartella o sottocartella, fare clic sulla riga della cartella ad eccezione del nome sottolineato della cartella e quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina"). Se si sceglie il nome della cartella sottolineato, non sarà disponibile per selezionare l'opzione **Elimina**.
    
    ![Selezione di una cartella pubblica da rimuovere](images/Aa997202.8666290d-3f19-4c70-afe3-45569762718b(EXCHG.150).png "Selezione di una cartella pubblica da rimuovere")  

3.  Verrà visualizzato un avviso che richiede se si è certi di voler eliminare la cartella pubblica. Fare clic su **Sì** per continuare.

## Eliminazione di una cartella pubblica tramite Shell

In questo esempio viene eliminata la cartella pubblica Help Desk\\Resolved. Questo comando presuppone che nella cartella pubblica Resolved non siano presenti delle sottocartelle.

    Remove-PublicFolder -Identity "\Help Desk\Resolved"

In questo esempio, il comando precedente viene controllato senza che vengano apportate modifiche.

    Remove-PublicFolder -Identity "\HelpDesk\Resolved" -WhatIf

In questo esempio, la cartella pubblica Marketing e tutte le sue sottocartelle vengono rimosse perché il comando viene eseguito in modo ricorrente.

    Remove-PublicFolder -Identity "\Marketing" -Recurse:$True

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-PublicFolder](https://technet.microsoft.com/it-it/library/bb124894\(v=exchg.150\)).


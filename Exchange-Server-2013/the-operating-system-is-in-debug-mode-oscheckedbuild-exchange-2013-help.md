---
title: 'Il sistema operativo è in mode_OSCheckedBuild debug: Exchange 2013 Help'
TOCTitle: Il sistema operativo è in mode_OSCheckedBuild debug
ms:assetid: 93a1380f-1388-494d-8f78-92dfefd069bd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.oscheckedbuild(v=EXCHG.150)
ms:contentKeyID: 50481217
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Il sistema operativo è in mode\_OSCheckedBuild debug

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-15_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server Analyzer Tool query nella classe **Win32\_OperatingSystem** Microsoft Windows® Management Instrumentation (WMI) per determinare se è impostato un valore della proprietà **di Debug** . Se il valore di questa chiave su un computer Exchange Server è impostato su **True**, viene visualizzato un errore.

Viene attivata la modalità di debug Windows aggiungendo il **parametro/debug** nel file Boot. ini. **Quando/debug** è specificato nel file Boot. ini di un computer Windows Server, debugger kernel caricati durante l'avvio e mantenuto in memoria in ogni momento. In questo modo il supporto tecnico accedere al sistema sottoposti a debug e di accedere al debugger, anche quando il sistema non è sospeso in una schermata di ARRESTO del Kernel. A differenza di switch **/crashdebug** , **l'opzione/debug** utilizza la porta COM per il debug o non. Questa opzione viene utilizzata durante il debug problemi regolarmente riproducibili. È probabile che il **parametro/debug** è stato impostato come mezzo per la risoluzione dei problemi ed è stato impostato su accidentalmente a sinistra.

A causa di altri processi che vengono eseguiti, influisce negativamente sulle prestazioni notevolmente. Pertanto, non è consigliabile che esegue Exchange Server in un computer in cui è in esecuzione Windows in modalità di debug.

Per eliminare questo errore, modificare il file Boot. ini e rimuovere il **parametro/debug** .

## Per risolvere il problema

1.  In Esplora risorse, passare alla partizione di sistema. Questa è la partizione che contiene i file specifici dell'hardware, ad esempio Boot. ini e NTLDR.

2.  Se è possibile visualizzare il file Boot. ini, potrebbe essere **Le opzioni della cartella** viene impostata l'opzione **Nascondi protetti file del sistema operativo**. In questo caso, nella finestra Esplora risorse fare clic su **Strumenti**, fare clic su **Opzioni cartella**e fare clic su **Visualizza**. Deselezionare la casella di controllo **Nascondi protetti di file del sistema operativo (scelta consigliata)** . Quando richiesto, fare clic su **Sì**.

3.  Quando il file Boot. ini è visibile in Esplora risorse, il file, fare clic su **Apri con**e quindi selezionare **il blocco note** aprire il file.

4.  Nella sezione **\[Operating Systems\]** , rimuovere il **parametro/debug** .

5.  Salvare e chiudere il file e quindi riavviare il computer di Exchange Server rendere effettive le modifiche.

Per ulteriori informazioni sui parametri che possono essere utilizzati nel file Boot. ini, vedere l'articolo della Microsoft Knowledge Base 833721 "opzioni dei parametri disponibili per Windows XP e Windows Server 2003 Boot. ini file" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=833721](https://go.microsoft.com/fwlink/?linkid=3052&kbid=833721)).


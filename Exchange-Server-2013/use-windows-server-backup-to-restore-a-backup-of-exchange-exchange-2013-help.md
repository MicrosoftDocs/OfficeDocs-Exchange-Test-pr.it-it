---
title: 'Ripristino di un backup di Exchange tramite Windows Server Backup: Exchange 2013 Help'
TOCTitle: Ripristino di un backup di Exchange tramite Windows Server Backup
ms:assetid: 2d0f31dc-eb32-451a-8852-591269026506
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876864(v=EXCHG.150)
ms:contentKeyID: 50480243
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ripristino di un backup di Exchange tramite Windows Server Backup

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-06-18_

È possibile utilizzare Windows Server Backup per eseguire il backup e il ripristino dei database di Exchange. Exchange include un plug-in per Windows Server Backup che consente di creare backup basati sul servizio Copia Shadow del volume dei dati di Exchange. Per ulteriori informazioni, vedere [Utilizzo di Windows Server Backup per eseguire il backup e il recupero dei dati di Exchange](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 1 minuto più il tempo necessario per il ripristino dei dati

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ripristino delle cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - La funzionalità Windows Server Backup deve essere installata nel computer locale.

  - Quando si ripristina un database nel percorso originale, questo può rimanere nello stato di arresto anomalo e essere installabile dal sistema. Quando si effettua il ripristino in un percorso alternativo (ad esempio, prima di utilizzare un database di ripristino), il database deve essere portato a uno stato di chiusura normale utilizzando le utilità del database di Exchange Server (Eseutil.exe).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Ripristino di un backup di Exchange tramite Windows Server Backup

1.  Avviare Windows Server Backup.

2.  Selezionare **Backup locale**.

3.  Nel pannello Azioni, fare clic su **Ripristina…** per avviare il ripristino guidato.

4.  Nella pagina **Guida introduttiva** effettuare una delle seguenti operazioni:
    
      - Se è stato eseguito il backup dei dati ripristinati nel server locale, selezionare **Questo server (NomeServer)**, quindi fare clic su **Avanti**.
    
      - Se è stato eseguito il ripristino dei dati da un altro server o se il backup che si ripristina si trova in un altro computer, selezionare **Altro server**, quindi selezionare **Avanti**. Nella pagina **Impostazione tipo di percorso**, selezionare **Unità locali** o **Cartella condivisa remota**, quindi fare clic su **Avanti**. Se si seleziona **Unità locali**, selezionare l'unità che comprende il backup nella pagina **Selezione percorso di backup**, quindi fare clic su **Avanti**. Se si seleziona **Cartella condivisa remota**, immettere il percorso UNC per i dati di backup nella pagina **Impostazione cartella remota**, quindi fare clic su **Avanti**.

5.  Nella pagina **Selezione data backup**, selezionare la data e l'ora del backup da ripristinare, quindi fare clic su **Avanti**.

6.  Nella pagina **Seleziona tipo di ripristino**, selezionare **Applicazioni** e fare clic su **Avanti**.
    

    > [!NOTE]
    > Se non è possibile selezionare <STRONG>Applicazioni</STRONG>, vuol dire che il backup da ripristinare era a livello di cartella e non a livello di volume. È necessario eseguire backup a livello di volume quando si esegue il backup dei dati di Exchange con Windows Server Backup.



7.  Nella pagina **Seleziona applicazione**, verificare che Exchange sia selezionato nel campo **Applicazioni**. Fare clic su **Visualizza dettagli** per visualizzare i componenti dei backup dell'applicazione. Se il backup ripristinato è il più recente, viene visualizzata la casella di controllo **Non eseguire il ripristino roll forward dei database dell'applicazione**. Selezionare questa casella di controllo se si desidera evitare che Windows Server Backup esegua il roll forward del database ripristinato salvando tutti i registri delle transazioni non salvate. Fare clic su **Avanti**.

8.  Nella pagina **Impostazione opzioni di ripristino**, specificare la posizione di ripristino dei dati, quindi fare clic su **Avanti**:
    
      - Scegliere **Ripristina nel percorso originale** se si desidera ripristinare i dati di Exchange direttamente nel percorso originale. Se si utilizza questa opzione, non è possibile scegliere i database da ripristinare. Tutti i database di cui si esegue il backup nel volume verranno ripristinati nei relativi percorsi originali.
    
      - Scegliere **Ripristina in un percorso diverso** per ripristinare singoli database e file in un percorso specifico. Fare clic su **Sfoglia** per specificare un percorso alternativo. Se si utilizza questa opzione, è possibile scegliere i database da ripristinare. Al termine dell'operazione, i file di dati possono essere spostati nel database di ripristino, trasferiti di nuovo nel percorso originale o posizionati in un altro punto dell'organizzazione di Exchange tramite [Portabilità del database](database-portability-exchange-2013-help.md). Durante il ripristino di un database in un percorso alternativo, il database ripristinato passerà nello stato di arresto anomalo. Al termine del ripristino, è necessario portare il database in uno stato di arresto normale utilizzando Eseutil.exe.

9.  Nella pagina **Conferma**, esaminare le impostazioni di ripristino e fare clic su **Ripristina**.

10. Nella pagina **Stato ripristino**, è possibile visualizzare lo stato e l'avanzamento dell'operazione di ripristino.

11. Al termine dell'operazione di ripristino, fare clic su **Chiudi**.

## Come verificare se l'operazione ha avuto esito positivo?

Nella pagina **Stato ripristino** viene indicato se la procedura di ripristino è stata eseguita correttamente. Per verificare il corretto ripristino dei dati, fare quanto segue:

  - Esaminare la directory di destinazione della copia di backup per verificare che contenga i dati ripristinati.

  - Sul server su cui è stato eseguito Windows Server Backup, verificare che il lavoro sia stato completato visualizzando i registri di backup.

  - Aprire Visualizzatore eventi e verificare che nel registro eventi dell'applicazione sia stato inserito un evento di completamento del ripristino.


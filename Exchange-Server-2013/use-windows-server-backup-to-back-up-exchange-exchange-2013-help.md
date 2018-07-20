---
title: 'Utilizzare Windows Server Backup per eseguire il backup di Exchange: Exchange 2013 Help'
TOCTitle: Utilizzare Windows Server Backup per eseguire il backup di Exchange
ms:assetid: 188a8291-0a41-4ca2-b6d2-94242e2b1ffc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876854(v=EXCHG.150)
ms:contentKeyID: 50480085
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzare Windows Server Backup per eseguire il backup di Exchange

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-06-18_

È possibile utilizzare Windows Server Backup per eseguire il backup e il ripristino dei database di Exchange. Exchange include un plug-in per Windows Server Backup che consente di creare backup basati sul servizio Copia Shadow del volume dei dati di Exchange.

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 1 minuto, oltre al tempo necessario per eseguire il backup dei dati

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ripristino delle cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - La funzionalità Windows Server Backup deve essere installata nel computer locale.

  - Durante l'operazione di backup, i file di dati in Exchange vengono controllati per verificare che siano integri e possano essere utilizzati per il ripristino. Se questa verifica ha esito positivo, i dati di Exchange potranno essere ripristinati dal backup. Se la verifica ha esito negativo, i dati di Exchange non saranno disponibili per il ripristino. Windows Server Durante il backup viene eseguita una verifica dei dati sullo snapshot effettuato per il backup. Di conseguenza, prima di copiare i file dallo snapshot sui supporti di backup, si conosce già l'esito della verifica dei dati i risultati della verifica vengono notificati all'utente.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzare Windows Server Backup per eseguire il backup di Exchange

1.  Avviare Windows Server Backup.

2.  Selezionare **Backup locale**.

3.  Nel pannello Azioni, fare clic su **Backup unico...** per avviare la creazione guidata del backup unico.

4.  Nella pagina **Opzioni di backup**, selezionare **Opzioni diverse**, quindi fare clic su **Avanti**.

5.  Nella pagina **Selezionare la configurazione del backup** selezionare **Personalizzata**, quindi fare clic su **Avanti**.

6.  Nella pagina **Selezione elementi di backup**, fare clic su **Aggiungi elementi** per selezionare i volumi per i quali eseguire il backup, quindi fare clic su **OK**.
    

    > [!NOTE]
    > Scegliere volumi e non singole cartelle. L'unico modo per eseguire il backup o il ripristino a livello di volume consiste nella selezione dell'intero volume.



7.  Fare clic su **Impostazioni avanzate**. Nella scheda **Esclusioni**, selezionare **Aggiungi esclusione** per aggiungere file o tipi di file che si desidera escludere dal backup.
    

    > [!NOTE]
    > Per impostazione predefinita, i volumi che contengono applicazioni o componenti del sistema operativo vengono inclusi nel backup e non possono essere esclusi.



8.  Nella scheda **Impostazioni servizio Copia Shadow del volume**, selezionare **Backup completo del Servizio Copia Shadow del volume**, quindi fare clic su **OK** e infine su **Avanti**.

9.  Nella pagina **Impostazione tipo di destinazione**, selezionare il percorso in cui si desidera archiviare il backup, quindi fare clic su **Avanti**.
    
      - Se si seleziona **Unità locali**, viene visualizzata la pagina **Seleziona destinazione di backup**. Selezionare un'opzione dall'elenco a discesa **Destinazione backup**, quindi fare clic su **Avanti**.
    
      - Se si seleziona **Cartella condivisa remota**, viene visualizzata la pagina **Impostazione cartella remota**. Specificare un percorso UNC dei file di backup, quindi configurare le impostazioni controllo di accesso. Scegliere **Non ereditare** se si desidera che il backup sia accessibile solo tramite un account specifico. Indicare un nome utente e una password per un account che disponga delle autorizzazioni di scrittura sul computer che ospita la cartella remota, quindi fare clic su **OK**. In alternativa, selezionare **Eredita** se si desidera che il backup sia accessibile da chiunque disponga di accesso alla cartella remota. Fare clic su **Avanti**.

10. Nella pagina **Conferma**, esaminare le impostazioni di backup e fare clic su **Backup**.

11. Nella pagina **Stato backup**, è possibile visualizzare lo stato e l'avanzamento dell'operazione di backup.

12. Fare clic su **Chiudi** per uscire dalla pagina **Stato backup** in qualsiasi momento. Tutti i backup in corso continueranno ad essere eseguiti in background.

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che il backup dei dati sia stato eseguito correttamente, procedere come segue:

  - Nel server nel quale viene eseguito Windows Server Backup, viene visualizzato l'ultimo stato del backup: dovrebbe essere indicato che l'operazione è riuscita. Inoltre, è possibile verificare se il backup è riuscito consultando i registri di Windows Server Backup.

  - Aprire il visualizzatore eventi e verificare che il completamento del backup sia registrato nel registro eventi Applicazione.

  - Eseguire il seguente comando in Exchange Management Shell per verificare che per ogni database presente nel volume selezionato sia stato eseguito correttamente il backup:
    
        Get-MailboxDatabase -Server <ServerName> -Status | fl Name,*FullBackup
    
    Le proprietà *SnapshotLastFullBackup* e *LastFullBackup* del database indicato che il backup più recente è stato eseguito correttamente e si trattava di un backup VSS completo.


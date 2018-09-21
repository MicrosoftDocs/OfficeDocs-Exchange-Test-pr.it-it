---
title: 'Gestire database cassette postali in Exchange 2013: Exchange 2013 Help'
TOCTitle: Gestire il database delle cassette postali in Exchange 2013
ms:assetid: ead4a96b-1717-435b-bcfc-9901ac4e3b58
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150580(v=EXCHG.150)
ms:contentKeyID: 50481973
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestire il database delle cassette postali in Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-04-29_

Un database delle cassette postali è un'unità di granularità in cui vengono create e archiviate le cassette postali. Un database delle cassette postali viene archiviato come un file del database di Exchange (con estensione edb). In Microsoft Exchange Server 2013, tutti i database delle cassette postali dispongono di proprie proprietà che possono essere configurate.

In questo argomento viene descritto come eseguire le attività di configurazione correlate alla gestione dei database delle cassette postali in Exchange Server 2013.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Database delle cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Creazione di un database delle cassette postali

## Creazione di un database delle cassette postali tramite l'interfaccia di amministrazione di Exchange

1.  Nell’interfaccia di amministrazione di Exchange, passare a **Server**.

2.  Selezionare **Database**, quindi fare clic sul simbolo **+** per creare un database.

3.  Creazione del nuovo database mediante la procedura guidata.

## Creazione di un database delle cassette postali tramite Shell

Per un esempio di creazione di un database delle cassette postali, vedere l'esempio 1 in [New-MailboxDatabase](https://technet.microsoft.com/it-it/library/aa997976\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la creazione del database sia stata eseguita correttamente, procedere come segue:

  - Nell'interfaccia di amministrazione di Exchange, verificare che il database delle cassette postali creato sia elencato nella scheda **Database**.

  - In Shell, verificare che il database sia stato creato sul server Mailbox01 eseguendo il comando riportato di seguito.
    
    ```powershell
Get-MailboxDatabase -Server "Mailbox01"
```

## Visualizzazione delle proprietà del database delle cassette postali

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb124924\(v=exchg.150\)).

## Visualizzazione delle proprietà di un database delle cassette postali tramite Shell

Per un esempio di come visualizzare le proprietà del database delle cassette postali, vedere l’esempio 2 in [New-MailboxDatabase](https://technet.microsoft.com/it-it/library/aa997976\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che le informazioni sul database delle cassette postali siano state recuperate correttamente, procedere come segue:

In Shell, verificare che tutte le informazioni sul database delle cassette postali siano state visualizzate correttamente.

## Impostazione delle proprietà del database delle cassette postali

## Impostazione delle proprietà di un database delle cassette postali tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server**.

2.  Selezionare **Database**, quindi scegliere il database delle cassette postali da configurare.

3.  Fare clic su **Modifica** ![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica")per configurare gli attributi di un database delle cassette postali.

4.      
    Utilizzare la scheda **Generale** per visualizzare lo stato del database delle cassette postali, incluso il percorso del database delle cassette postali, l'ultimo backup e lo stato del database:
    
      - **Percorso database**   In questo campo di sola lettura viene visualizzato il percorso completo per il database (EDB) di Exchange 2013  per il database delle cassette postali selezionato. Per visualizzare il percorso completo, selezionare il percorso e premere la freccia destra. Non è possibile utilizzare questo campo per modificare il percorso. Per modificare il percorso dei file di database, utilizzare il cmdlet [Move-DatabasePath](https://technet.microsoft.com/it-it/library/bb124742\(v=exchg.150\)).
    
      - **Ultimo backup completo**   In questo campo di sola lettura vengono visualizzate la data e l'ora dell'ultimo backup completo del database delle cassette postali.
    
      - **Ultimo backup incrementale**   In questo campo di sola lettura vengono visualizzate la data e l'ora dell'ultimo backup incrementale del database delle cassette postali.
    
      - **Stato**   In questo campo di sola lettura viene indicato se il database delle cassette postali è installato o disinstallato.
    
      - **Installato sul server**   In questo campo di sola lettura viene visualizzato il server in cui è installato il database.
    
      - **Master**   In questo campo di sola lettura viene visualizzato il server master per il database delle cassette postali. Il server Cassette postali che ospita la copia attiva di un database viene denominato master del database delle cassette postali.
    
      - **Tipo master**   In questo campo di sola lettura viene visualizzato il tipo di master del database delle cassette postali.
    
      - **Modificato**   In questo campo di sola lettura sono visualizzate la data e l'ora dell'ultima modifica del database.
    
      - **Server che ospitano una copia del database**   In questo campo di sola lettura vengono visualizzati gli altri server che dispongono di una copia di questo database.

5.  Utilizzare la scheda **Manutenzione** per configurare le impostazioni del database delle cassette postali, incluse la definizione del destinatario journal, l'impostazione di una pianificazione di manutenzione e l'installazione del database all'avvio:
    
      - **Destinatario journal**   Fare clic su **Sfoglia** per specificare un destinatario di cui abilitare l'inserimento nel journal sul database delle cassette postali. Rimuovere il destinatario dall'elenco per disabilitarne l'inserimento nel journal.
    
      - **Pianificazione manutenzione**   Utilizzare questo elenco per selezionare una delle pianificazioni di manutenzione preimpostate. È inoltre possibile creare una pianificazione personalizzata. Per configurare una pianificazione personalizzata, fare clic su **Personalizza**.
    
      - **Abilita manutenzione database in background (analisi ESE 24/7)   **Selezionare questa casella di controllo per abilitare l'analisi online del database che continua a essere eseguita in background. L'analisi online del database esegue il calcolo del checksum del database e altre operazioni che consentono a Exchange di analizzare lo spazio perso sul database e di ripristinarlo. Se si seleziona questa casella di controllo, Exchange eseguirà l'analisi del database non più di una volta al giorno e invierà un evento di avviso se non è in grado di completare l'analisi del database in sette giorni.
    
      - **Non installare database all'avvio**   Selezionare tale casella di controllo per evitare che Exchange installi questo database delle cassette postali quando viene avviato.
    
      - **Il database può essere sovrascritto da un ripristino**   Selezionare tale casella di controllo per consentire al database delle cassette postali di essere sovrascritto durante un processo di ripristino.
    
      - **Abilita registrazione circolare**   Selezionare tale casella di controllo per abilitare la registrazione circolare.

6.  Utilizzare la scheda **Limiti** per specificare i limiti di archiviazione, l'intervallo per i messaggi di avviso e le impostazioni di eliminazione per un database delle cassette postali.
    
      - **Invia avviso in corrispondenza di (GB)**   Selezionare questa casella di controllo per inviare un avviso automatico agli utenti informandoli che la propria cassetta postale sta raggiungendo il limite di archiviazione. Per specificare il limite di archiviazione, selezionare la casella di controllo, quindi specificare in gigabyte (GB) la quantità di contenuto archiviabile nella cassetta postale prima che venga inviato un messaggio di avviso mediante posta elettronica agli utenti delle cassette postali. È possibile immettere un valore compreso tra 0 e 2.097.151 megabyte (MB) (2,0 terabyte).
    
      - **Non consentire l'invio a (GB)**   Selezionare questa casella di controllo per non consentire agli utenti l'invio di nuovi messaggi di posta elettronica una volta che le dimensioni della cassetta postale hanno raggiunto il limite specificato. Per specificare il limite, selezionare la casella di controllo, quindi digitare le dimensioni della cassetta postale in GB raggiunte le quali si desidera impedire l'invio di nuovi messaggi di posta elettronica e inviare una notifica all'utente. È possibile immettere un valore compreso tra 0 e 2.097.151 MB (2,0 terabyte).
    
      - **Non consentire l'invio e la ricezione a (GB)**   Selezionare questa casella di controllo per non consentire agli utenti l'invio e la ricezione di messaggi di posta elettronica dopo che le dimensioni della cassetta postale hanno raggiunto il limite specificato. Per specificare il limite, selezionare la casella di controllo, quindi digitare le dimensioni della cassetta postale in GB, raggiunte le quali si desidera impedire l'invio e la ricezione di nuovi messaggi di posta elettronica e inviare una notifica all'utente. È possibile immettere un valore compreso tra 0 e 2.097.151 MB (2,0 terabyte).
    
      - **Mantieni elementi eliminati per (giorni)**   Selezionare tale casella di controllo per specificare per quanti giorni gli elementi eliminati vengono conservati in una cassetta postale. È possibile immettere un valore compreso tra 0 e 24.855 giorni.
    
      - **Mantieni cassette postali eliminate per (giorni)**   Selezionare questa casella di controllo per specificare per quanti giorni vengono mantenute le cassette postali eliminate. È possibile immettere un valore compreso tra 0 e 24.855 giorni.
    
      - **Non eliminare definitivamente elementi prima del backup del database**   Selezionare questa casella di controllo per non consentire l'eliminazione definitiva delle cassette postali e dei messaggi di posta elettronica prima che venga eseguito il backup del database delle cassette postali.

7.  Nella scheda **Impostazioni client** selezionare la rubrica offline (OAB) per la cassetta postale:
    
      - **Rubrica offline**   Per seleziona una rubrica offline, fare clic su **Sfoglia**, quindi selezionare la rubrica offline.

## Impostazione delle proprietà di un database delle cassette postali tramite Shell

Per un esempio di impostazione delle proprietà della cassetta postale, vedere l’esempio 1 in [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che gli attributi siano stati impostati correttamente, procedere come segue:

  - Verificare che le modifiche siano state salvate nell'interfaccia di amministrazione di Exchange.

  - In Shell, immettere il comando seguente per recuperare le proprietà del database delle cassette postali.
    
    ```powershell
Get-MailboxDatabase -Identity MailboxDatabase01 -Status | Format-List
```

## Modifica del percorso di un database delle cassette postali

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Move-DatabasePath](https://technet.microsoft.com/it-it/library/bb124742\(v=exchg.150\)).

## Modifica del percorso di un database delle cassette postali tramite Shell

Per un esempio di impostazione delle proprietà della cassetta postale, vedere l’esempio 1 in [Move-DatabasePath](https://technet.microsoft.com/it-it/library/bb124742\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il percorso del database sia stato modificato correttamente, procedere come segue:

1.  In EAC selezionare **Server** \> **Database** e quindi selezionare la cassetta postale appropriata.

2.  Fare clic sul simbolo **penna** e verificare che il percorso del database sia corretto.

## Installazione di un database delle cassette postali

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Mount-Database](https://technet.microsoft.com/it-it/library/aa998871\(v=exchg.150\)).

## Installazione di un database delle cassette postali tramite Shell

Per un esempio di installazione di un database delle cassette postali, vedere l'esempio 1 in [Mount-Database](https://technet.microsoft.com/it-it/library/aa998871\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il database delle cassette postali sia stato installato correttamente, procedere come segue.

  - In Shell, immettere il comando seguente per recuperare le proprietà del database delle cassette postali per tutte le cassette postali.
    
    ```powershell
Get-MailboxDatabase -IncludePreExchange2013
```

## Disinstallazione di un database delle cassette postali

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Dismount-Database](https://technet.microsoft.com/it-it/library/bb124936\(v=exchg.150\)).

## Disinstallazione di un database delle cassette postali tramite Shell

Per un esempio di disinstallazione di un database delle cassette postali, vedere l'esempio 1 in [Dismount-Database](https://technet.microsoft.com/it-it/library/bb124936\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il database delle cassette postali sia stato disinstallato correttamente, procedere come segue:

1.  In EAC selezionare **Server** \> **Database** e quindi selezionare la cassetta postale appropriata.

2.  Fare clic sul simbolo **penna** e verificare che lo stato del database sia **Disinstallato**.

## Eliminazione di un database delle cassette postali

## Eliminazione di un database delle cassette postali tramite l'interfaccia di amministrazione di Exchange

1.  In EAC selezionare **Server** \> **Database** e quindi selezionare la cassetta postale appropriata.

2.  Fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina")per rimuovere il database delle cassette postali.

## Eliminazione di un database delle cassette postali tramite Shell

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-MailboxDatabase](https://technet.microsoft.com/it-it/library/aa997931\(v=exchg.150\)).

1.  Eseguire il comando riportato di seguito per rimuovere il database delle cassette postali MyDatabase.
    
    ```powershell
Remove-MailboxDatabase -Identity "MyDatabase"
```

2.  Quando viene richiesta conferma per l'esecuzione dell'azione, digitare **S**.

3.  Quando viene visualizzata la finestra di dialogo che indica l'esito positivo della rimozione, prendere nota della posizione del file (.edb) del database di Exchange 2013. Se si desidera rimuovere il file dal disco rigido, è necessario rimuoverlo manualmente.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il database delle cassette postali sia stato rimosso correttamente, procedere come segue:

  - Nell'interfaccia di amministrazione di Exchange, selezionare **Server** \> **Database**.

  - Verificare che il database delle cassette postali sia stato rimosso.


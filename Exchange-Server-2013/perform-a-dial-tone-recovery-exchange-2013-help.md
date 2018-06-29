---
title: 'Esecuzione di un ripristino del segnale: Exchange 2013 Help'
TOCTitle: Esecuzione di un ripristino del segnale
ms:assetid: 158817fa-4b17-4fa9-8341-a86609e6a388
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd979810(v=EXCHG.150)
ms:contentKeyID: 51407342
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Esecuzione di un ripristino del segnale

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-06-27_

La portabilità consente agli utenti di disporre di una cassetta postale temporanea per l'invio e la ricezione di posta elettronica durante il ripristino o la riparazione della cassetta postale originale. La cassetta postale temporanea può trovarsi sullo stesso server Cassette postali Exchange 2013 o su qualsiasi altro server Cassette postali Exchange 2013 nell'organizzazione. Il procedimento per utilizzare la portabilità è denominato ripristino del segnale di linea, che comporta la creazione di un database vuoto su un server delle cassette postali per sostituire un database danneggiato. Per ulteriori informazioni, vedere [Portabilità temporanea](dial-tone-portability-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti più il tempo necessario per il ripristino dei dati.

  - È necessario avere meno del numero massimo dei database distribuiti per creare un database del segnale di linea. L'edizione standard di Exchange 2013 supporta un massimo di 5 database per server. Exchange 2013 Enterprise Edition supporta massimo 50 database per server in RTM e CU1 e 100 database per server in CU2 e versioni successive.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ripristino delle cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Ripristino di segnale di linea su un unico server tramite Shell


> [!NOTE]
> Non è possibile utilizzare EAC per eseguire un ripristino di segnale di linea su un unico server.



1.  Accertarsi che tutti i file esistenti del database in fase di ripristino siano preservati poiché potrebbero essere necessari in seguito per ulteriori operazioni di ripristino.

2.  Utilizzare il cmdlet [New-MailboxDatabase](https://technet.microsoft.com/it-it/library/aa997976\(v=exchg.150\)) per creare un database del segnale di linea, come mostrato in questo esempio.
    
        New-MailboxDatabase -Name DTDB1 -EdbFilePath D:\DialTone\DTDB1.EDB

3.  Utilizzare il cmdlet [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)) per ricollocare in sede le cassette postali degli utenti ospitate sul database in fase di ripristino, come mostrato nell'esempio seguente.
    
        Get-Mailbox -Database DB1 | Set-Mailbox -Database DTDB1

4.  Utilizzare il cmdlet [Mount-Database](https://technet.microsoft.com/it-it/library/aa998871\(v=exchg.150\)) per installare il database in modo che i computer dei client possano accedere al database e inviare e ricevere messaggi, come mostrato nell'esempio seguente.
    
        Mount-Database -Identity DTDB1

5.  Creare un RDB (database di ripristino) e ripristinare o copiare il database e i file di registro contenenti i dati che si desidera ripristinare nell'RDB. Per la procedura dettagliata, vedere [Creare un database di ripristino](create-a-recovery-database-exchange-2013-help.md).

6.  Dopo che i dati saranno stati copiati nell'RDB, ma prima di installare il database ripristinato, copiare tutti i file di registro dal database danneggiato sulla cartella di registro del database di ripristino, in modo che possano essere eseguiti sul database ripristinato.

7.  Montare l'RDB, quindi utilizzare il cmdlet [Dismount-Database](https://technet.microsoft.com/it-it/library/bb124936\(v=exchg.150\)) per smontarlo, come mostrato nell'esempio seguente.
    
        Mount-Database -Identity RDB1
        Dismount-Database -Identity RDB1

8.  Dopo che l'RDB sarà stato smontato, spostare il database e i file di registro correnti all'interno della cartella dell'RDB in una posizione più sicura. Ciò viene fatto in preparazione dello scambio del database ripristinato con il database del segnale di linea.

9.  Disinstallare il database del segnale di linea, come illustrato in questo esempio. Si noti che gli utenti finali avranno un'interruzione del servizio quando questo database verrà disinstallato.
    
        Dismount-Database -Identity DTDB1

10. Spostare il database e i file di registro dalla cartella del database del segnale di linea nella cartella dell'RDB.

11. Spostare il database e i file di registro dalla posizione sicura contenente il database ripristinato nella cartella del database del segnale di linea, quindi installare il database, come mostrato nell'esempio seguente.
    
        Mount-Database -Identity DTDB1
    
    Questo termina l'interruzione del servizio per gli utenti finali. Gli utenti saranno in grado di accedere al database di produzione originale e inviare e ricevere messaggi.

12. Installare l'RDB come illustrato in questo esempio.
    
        Mount-Database -Identity RDB1

13. Utilizzare i cmdlet [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) e [New-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829875\(v=exchg.150\)) per esportare i dati dall'RDB e importarli nel database ripristinato, come mostrato in questo esempio. In questo modo tutti i messaggi inviati e ricevuti verranno importati utilizzando il database del segnale di linea nel database di produzione.
    
        $mailboxes = Get-Mailbox -Database DTDB1
    
        $mailboxes | %{ New-MailboxRestoreRequest -SourceStoreMailbox $_.ExchangeGuid -SourceDatabase RDB1 -TargetMailbox $_ }

14. Quando l'operazione di ripristino sarà stata completata, sarà possibile disinstallare e rimuovere l'RDB, come mostrato nell'esempio seguente.
    
        Dismount-Database -Identity RDB1
        Remove-MailboxDatabase -Identity RDB1

Per ulteriori informazioni sulla sintassi e sui parametri, vedere gli argomenti seguenti:

  - [New-MailboxDatabase](https://technet.microsoft.com/it-it/library/aa997976\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\))

  - [Mount-Database](https://technet.microsoft.com/it-it/library/aa998871\(v=exchg.150\))

  - [Dismount-Database](https://technet.microsoft.com/it-it/library/bb124936\(v=exchg.150\))

  - [Remove-MailboxDatabase](https://technet.microsoft.com/it-it/library/aa997931\(v=exchg.150\))

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la cassetta postale è stata spostata correttamente, procedere come segue:

  - Aprire la cassetta postale utilizzando Microsoft Office Outlook Web App.

  - Aprire una cassetta utilizzando Microsoft Outlook.


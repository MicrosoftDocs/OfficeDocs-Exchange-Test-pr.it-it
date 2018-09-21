---
title: 'Errore di installazione ruolo server_InstallWatermark: Exchange 2013 Help'
TOCTitle: Errore di installazione si sono verificati durante l'installazione di un server role_InstallWatermark
ms:assetid: ad89ebd5-f9bb-40c1-8811-09b145c2b341
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.installwatermark(v=EXCHG.150)
ms:contentKeyID: 50481440
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Errore di installazione si sono verificati durante l'installazione di un server role\_InstallWatermark

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Perché si è verificato un errore il programma di installazione durante l'installazione di un ruolo del server, non continuare l'installazione di Microsoft Exchange Server 2007.

Installazione di Exchange 2007 è necessario che un'installazione del ruolo server in errore sia corretta nuovamente installato o rimosso dal processo di installazione prima di proseguire con altre attività di configurazione.

Per risolvere questo problema, reinstallare solo i ruoli dei server non riuscito o rimuovere i ruoli dei server.

Reinstallare il ruolo del server non riuscito dalla riga di comando

1.  Aprire una finestra del prompt dei comandi e quindi passare al file di installazione.

2.  Eseguire il comando indicato di seguito:
    
    ```powershell
Setup /roles:<Failed Server Role>
```
    
    Selezionare uno o più dei seguenti ruoli, in un elenco separato da virgole:
    
    Accesso client (o autorità di certificazione o C)
    
    EdgeTransport (o ET oppure E)
    

    > [!NOTE]
    > Il ruolo del server Trasporto Edge non può coesistere nello stesso computer di qualsiasi altro ruolo del server.

    

    > [!NOTE]
    > È necessario distribuire il ruolo del server Trasporto Edge nella rete perimetrale e all'esterno della foresta Active Directory.

    
    Trasporto hub (o HT o H)
    
    Cassette postali (o MB o M)
    
    Messaggistica unificata (o alla messaggistica UNIFICATA o U)
    
    ManagementTools (o MT o M)
    

    > [!NOTE]
    > Se si specifica ManagementTools, si installerà Exchange Console di gestione, i cmdlet Exchange per Exchange Management Shell, Exchange file della Guida, Exchange Best Practices Analyzer Tool e Exchange Assistente per la risoluzione dei problemi. Se si installa qualsiasi altro ruolo del server, gli strumenti di gestione verranno installati automaticamente.

    
    Ad esempio, per aggiungere il ruolo del server Trasporto Hub al server della cassetta postale esistente, digitare quanto segue: **%LocalExchangeInstallationDir%\\bin\\Setup.com /role:HubTransport /Mode**


> [!NOTE]
> Se un ruolo di server di Exchange Server 2007 già installato correttamente, il programma di installazione guidata verrà eseguito in modalità manutenzione. Se non ruoli del server Exchange 2007 in precedenza sono stati installati correttamente, verrà avviata l'installazione guidata dal punto di interruzione.



Utilizzare la procedura guidata installazione di Exchange Server 2007 in modalità manutenzione per reinstallare il ruolo del server non riuscito

1.  Accedere al server per il quale si desidera reinstallare un ruolo del server.

2.  Aprire il pannello di controllo e quindi fare doppio clic su **Installazione applicazioni**.

3.  Nella pagina **Cambia / Rimuovi programmi** selezionare **Microsoft Exchange Server** e quindi fare clic su **Cambia**.

4.  Nell'Installazione guidata Exchange Server 2007, nella pagina **Modalità manutenzione**, fare clic su **Avanti**.

5.  Nella pagina **Selezione ruolo Server** selezionare le caselle di controllo per i ruoli del server che si desidera installare e quindi fare clic su **Avanti**.
    

    > [!NOTE]
    > Il ruolo del server Trasporto Edge non può coesistere nello stesso computer di qualsiasi altro ruolo del server.

    

    > [!NOTE]
    > È necessario distribuire il ruolo del server Trasporto Edge nella rete perimetrale e all'esterno della foresta Active Directory.

    

    > [!NOTE]
    > Se si fa clic su strumenti di gestione, si installerà Exchange Management Console, i cmdlet di ExchangeExchange Management Shell e il file della Guida Exchange. Gli strumenti di gestione verranno installati automaticamente se si esegue l'installazione di qualsiasi altro ruolo del server.



6.  Se si seleziona **Ruolo Trasporto Hub** e se si sta installando Exchange 2007 in una foresta con un esistente Exchange Server 2003 o Exchange 2000 Server organizzazione, nella pagina **Impostazioni flusso di posta**, selezionare un server testa di ponte nell'organizzazione esistente che fa parte del Exchange 2003 o gruppo di routing Exchange 2000 a cui si desidera creare un connettore.

7.  Nella pagina **Controlla lo stato di preparazione** Visualizza lo stato per determinare se controlli dei prerequisiti di ruolo dell'organizzazione e il server sia stata completata correttamente. Se sono stati completati correttamente, fare clic su **Installa** per installare Exchange 2007.

8.  Nella pagina **Completamento** fare clic su **Fine**.

Per utilizzare la procedura guidata installazione di Exchange Server 2007 per reinstallare il ruolo del server non riuscito quando nessun altro ruolo del server in precedenza è stato installato correttamente

1.  Seguire le istruzioni nella "Modalità per eseguire un personalizzato installazione utilizzando Installazione di Exchange 2007" ([https://go.microsoft.com/fwlink/?LinkId=86648](https://go.microsoft.com/fwlink/?linkid=86648)) nella documentazione del prodotto Exchange Server 2007.

Per rimuovere il ruolo del server non riuscito

1.  Seguire le istruzioni nella "Modalità per rimuovere Exchange 2007 ruoli del Server" ([https://go.microsoft.com/fwlink/?LinkId=86649](https://go.microsoft.com/fwlink/?linkid=86649)) nella documentazione del prodotto Exchange Server 2007.

## Per ulteriori informazioni

Per ulteriori informazioni sull'installazione di Exchange 2007 in modalità automatica, vedere "Come per installare Exchange 2007 in modalità automatica" ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476)).


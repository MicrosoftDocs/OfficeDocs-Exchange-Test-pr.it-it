---
title: 'Non in domain_NotInSchemaMasterDomain o i siti master schema: Exchange 2013 Help'
TOCTitle: Non in domain_NotInSchemaMasterDomain o i siti master schema
ms:assetid: 5e44eb33-4c30-4c3d-ba68-5c30bef1731f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.notinschemamasterdomain(v=EXCHG.150)
ms:contentKeyID: 50480768
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Non in domain\_NotInSchemaMasterDomain o i siti master schema

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Dal momento che il computer che esegue il programma di installazione non è nello stesso sito del servizio di directory Active Directory® o dominio del server che viene assegnato il dominio ruolo master schema, noti anche come operazioni a master singolo o FSMO, non può continuare l'installazione di Microsoft® Exchange Server 2007.

Controller di dominio che funge da master schema dominio essere nello stesso sito e dominio del computer locale che esegue l'installazione di Exchange richiede l'installazione di Exchange 2007.

Il master schema dominio controlla tutti gli aggiornamenti e le modifiche allo schema di Active Directory.

Per risolvere questo problema, eseguire il programma di installazione di Exchange Server 2007 utilizzando le opzioni **/prepareschema** e **/prepareAD** del sito e il dominio del master schema di dominio.

Per ulteriori informazioni sulle opzioni di installazione **/prepareschema** e **/prepareAD**, vedere l'argomento della documentazione del prodotto Exchange 2007 "Come per preparare Active Directory e dei domini" (<https://go.microsoft.com/fwlink/?linkid=78453>)

È possibile utilizzare lo strumento Master Schema per identificare il ruolo. Tuttavia, la DLL schmmgmt deve essere registrata per rendere disponibile come snap-in MMC lo strumento di schemi.

Per visualizzare il master schema corrente

1.  Al prompt dei comandi, digitare **regsvr32 schmmgmt. dll**
    

    > [!NOTE]
    > <STRONG>RegSvr32</STRONG> è stato registrato correttamente quando viene visualizzata la finestra di dialogo seguente:<BR>DllRegisterServer in schmmgmt riuscito.



2.  Per aprire una nuova console di gestione, fare clic su **Start**, scegliere **Esegui** e quindi digitare **mmc**.

3.  Nel menu della Console, fare clic su **Aggiungi/Rimuovi Snap-in**.

4.  Fare clic su **Aggiungi** per aprire la finestra di dialogo **Aggiungi Snap-in autonomo**.

5.  Selezionare **Schema di Active Directory** e quindi fare clic su **Aggiungi**.

6.  "Schema di active Directory" viene visualizzato in Aggiungi/Rimuovi snap-in fare clic su **Chiudi** e quindi fare clic su **OK** per tornare alla console.

7.  Selezionare **Schema di Active Directory** in modo che le sezioni di **classi** e nuovi **attributi** vengono visualizzate sul lato destro.

8.  Il pulsante destro **Schema di Active Directory** e quindi fare clic su **Master operazioni**.

9.  Viene visualizzato il master schema corrente

Dopo aver identificato il master schema corrente, determinare la subnet in cui si trova nel master schema. Quindi, utilizzare uno dei metodi seguenti per installare Exchange:

  - Modificare la subnet sul server di Exchange per spostare nel sito in cui si trova il master schema. Quindi, installare Exchange.

  - Temporaneamente forzare una modifica l'appartenenza al sito in Exchange server e quindi installare Exchange. Dopo l'installazione di Exchange, restituisce il server di Exchange nel sito originale.

Per forzare l'appartenenza ai siti

1.  Nel server in cui si desidera installare Exchange, avviare l'Editor del Registro di sistema. A tale scopo, fare clic su **Start**, scegliere **Esegui**, digitare **regedit**e quindi fare clic su **OK**.

2.  Individuare la seguente sottochiave del Registro di sistema:
    
    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\Netlogon\\Parameters**

3.  Creare il nuovo valore di **stringa** seguente:
    
    Nome valore: **NomeSito**
    
    Tipo di valore: **REG\_SZ**
    
    Dati valore: **\< site\_that\_contains\_the\_schema\_master \>**

4.  Chiudere l'Editor del Registro di sistema e quindi riavviare il servizio Netlogon. Questa azione forza il server di Exchange per partecipare al sito specificato.

5.  Installazione di Exchange.

6.  Rimuovere la voce del Registro di sistema che è stato aggiunto nel passaggio 3.

7.  Riavviare il servizio Netlogon. Questa azione restituisce Exchange nel sito originale.


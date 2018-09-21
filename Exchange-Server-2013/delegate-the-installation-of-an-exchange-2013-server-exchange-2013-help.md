---
title: "Delegare l'installazione di un server Exchange 2013: Exchange 2013 Help"
TOCTitle: Delegare l'installazione di un server Exchange 2013
ms:assetid: f2fc8680-0c7c-4a29-b8f5-d77404fec280
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201741(v=EXCHG.150)
ms:contentKeyID: 62615209
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Delegare l'installazione di un server Exchange 2013

 

_**Si applica a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-07-31_

Exchange Server 2013 consente di delegare l'installazione dei server Exchange a coloro che non è membri del gruppo di ruoli Gestione organizzazione Exchange 2013. Questo è spesso utile per aziende di grandi dimensioni dove gli utenti che installare e configurare server non sono le stesse persone che gestiscono servizi, quali Exchange. Se questo sembra un elemento da eseguire, in questo argomento viene automaticamente.

In genere, durante l'installazione di Exchange, le persone installandolo necessario essere membri del gruppo di ruoli [Gestione organizzazione](organization-management-exchange-2013-help.md) . Ciò avviene perché quando viene installato Exchange, vengono apportate modifiche a Active Directory e solo Exchange, gli amministratori membri del gruppo di ruoli Gestione organizzazione, è possono apportare le modifiche. Nell'elenco seguente sono riportate le modifiche apportate:

  - Un oggetto server viene creato nella partizione di configurazione **CN=Servers,CN=Exchange Administrative Group (FYDIBOHF23SPDLT),CN=Administrative Groups,CN=\<Organization Name\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<Root Domain\>** .

  - Voci di controllo di accesso (ACE) seguente vengono aggiunti all'oggetto server all'interno della partizione di configurazione per il gruppo di ruoli configurazione delegata:
    
      - Controllo completo per l'oggetto server e i relativi oggetti figlio
    
      - Nega voce di controllo di accesso per Invia come diritto esteso
    
      - Nega voce di controllo di accesso per Ricevi come diritto esteso
    
      - Negare le autorizzazioni CreateChild e DeleteChild per Exchange gli oggetti di archivio delle cartelle pubbliche
    

    > [!NOTE]
    > Le cartelle pubbliche vengono amministrate un livello di organizzazione; di conseguenza, la creazione e l'eliminazione di archivi di cartelle pubbliche è limitato agli amministratori di Exchange.



  - L'account del computer Active Directory per il server viene aggiunto al gruppo di server Exchange.

  - Il server viene aggiunto come server di provisioning in Exchange interfaccia di amministrazione.

In aziende di grandi dimensioni, le persone che installare e configurare nuovi server spesso non sono amministratori Exchange. Per consentire loro di installare Exchange, un amministratore Exchange può *eseguire il provisioning* nel server Active Directory. Quando viene eseguito il provisioning di un server, tutte le modifiche necessarie per il nuovo server Exchange alla funzione vengono apportate Active Directory separatamente dall'installazione effettivo di Exchange in un computer. Un amministratore Exchange è possibile effettuare il provisioning di un nuovo server in Active Directory ore o giorni pari prima dell'installazione di Exchange nel nuovo computer. Dopo un server è stato eseguito il provisioning, la persona che ha eseguito le esigenze di installazione solo come membro del gruppo di ruoli [Installazione delegata](delegated-setup-exchange-2013-help.md) per installare Exchange. Il gruppo di ruoli configurazione delegata consente solo ai membri di installare i server di provisioning.

Quando si pensare tramite delega dell'installazione, tenere presente quanto segue:

  - Almeno un server Exchange 2013 deve essere già stato installato prima che è possibile delegare l'installazione del server aggiuntivi. La persona che consente di installare il primo server deve essere un amministratore Exchange. Per ulteriori informazioni, vedere [Elenco di controllo: Eseguire una nuova installazione di Exchange 2013](checklist-perform-a-new-installation-of-exchange-2013-exchange-2013-help.md).

  - Un utente delegato non è in grado di disinstallare un server Exchange. Per disinstallare un server Exchange, è necessario essere un amministratore Exchange.

## Come è possibile effettuare il provisioning di un server Exchange 2013?

Per eseguire il provisioning di un server per Exchange, è necessario utilizzare Exchange 2013 il programma di installazione da riga di comando. Se non si è estrema familiarità con Windows al prompt dei comandi, non bisogna preoccuparsi. In questo argomento i passaggi ciò che ti occorre eseguire. Prima di iniziare, di seguito sono due aspetti da tenere presenti:

  - È necessario essere membri del gruppo di ruoli Gestione organizzazione per eseguire il provisioning di un server.

  - Si dovrebbe ottenere la versione più recente di Exchange 2013. È possibile ottenere il collegamento di download dal [Aggiornamenti per Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

Il comando che si desidera utilizzare per eseguire il provisioning del server varia a seconda se si esegue il programma di installazione dal computer che sta provisioning o se in esecuzione da un altro computer. Scegliere il comando nei passaggi seguenti che corrisponde a cui si esegue il programma di installazione:

1.  Premere il tasto Windows + "R" per aprire la finestra **Esegui**.

2.  **Aprire**, digitare**cmd.exe**e quindi premere INVIO per aprire un **prompt dei comandi di Windows**.

3.  Passare alla directory in cui è stato scaricato ed espansi i file di installazione Exchange 2013. Se i file di installazione si trovano in `C:\Downloads\Exchange 2013`, utilizzare il seguente comando.
    
    ```powershell
CD "C:\Downloads\Exchange 2013"
```

4.  Scegliere il comando genera una corrispondenza per cui si esegue il programma di installazione:
    
      - **Se si sta eseguendo il programma di installazione nel computer in cui viene eseguito il provisioning**, eseguire il comando seguente:
        
        ```powershell
Setup.exe /NewProvisionedServer /IAcceptExchangeServerLicenseTerms
```
    
      - **Se si sta eseguendo il programma di installazione in un altro computer**, eseguire il comando seguente:
        
        ```powershell
Setup.exe /NewProvisionedServer:<ComputerName> /IAcceptExchangeServerLicenseTerms
```

5.  Dopo che si effettua il provisioning del server, è necessario assicurarsi che si sono aggiunti gli utenti che devono essere in grado di installare Exchange nei server di provisioning al gruppo di ruoli configurazione delegata. Per informazioni su come aggiungere utenti a un gruppo di ruoli, vedere [Add members to a role group](manage-role-group-members-exchange-2013-help.md).

Una volta terminato con la procedura seguente, il computer sarà pronto per Exchange da installare. Exchange 2013 può essere installato in un server di provisioning eseguendo le operazioni in [Installazione di Exchange 2013 utilizzando l'installazione guidata](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

## Come sapere se l'operazione ha avuto esito positivo

Per verificare che il server è stato correttamente il provisioning per Exchange, è possibile eseguire le operazioni seguenti:

1.  Passare a **Start** \> **Strumenti di amministrazione** e quindi aperto **e computer di Active Directory Users**.

2.  Selezionare **Microsoft Exchange Security Groups**, fare doppio clic sul **Server Exchange** e quindi selezionare la scheda **membri**.

3.  Nella scheda **membri**, verificare se il server che il provisioning è elencato come membro del gruppo di protezione.

Se il server è elencato come membro del gruppo di protezione Exchange Servers, è stato eseguito correttamente il provisioning. Un utente membro del gruppo di ruoli configurazione delegata possibile installare Exchange in tale server.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.


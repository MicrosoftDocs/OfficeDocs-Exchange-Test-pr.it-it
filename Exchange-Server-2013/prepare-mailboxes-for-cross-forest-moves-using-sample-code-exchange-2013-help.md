---
title: 'Preparare le cassette postali per gli spostamenti tra foreste con codice di esempio: Exchange 2013 Help'
TOCTitle: Preparare le cassette postali per gli spostamenti tra foreste con codice di esempio
ms:assetid: f35ac7a5-bb84-4653-b6d0-65906e93627b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee861124(v=EXCHG.150)
ms:contentKeyID: 50482012
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Preparare le cassette postali per gli spostamenti tra foreste con codice di esempio

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Microsoft Exchange 2013 supporta spostamenti e migrazioni utilizzando i cmdlet **New-MoveRequest** e **New-MigrationBatch** . È inoltre possibile spostare la cassetta postale tramite l'interfaccia di amministrazione di Exchange (EAC). È possibile spostare una cassetta postale da un insieme di strutture Exchange origine a una foresta di destinazione Exchange 2010.

Per eseguire **New-MoveRequest**, è necessario che nella foresta di Exchange di destinazione sia disponibile un utente di posta elettronica dotato di un insieme minimo di attributi di Active Directory obbligatori.  È possibile creare l'utente di posta richiesto nella foresta Exchange di destinazione personalizzando la distribuzione di Microsoft Identity Lifecycle Manager (ILM) 2007. Il codice di esempio per l'estensione delle regole basato su ILM descritto in questo argomento mostra la personalizzazione della distribuzione ILM corrente per creare gli utenti necessari abilitati alla posta elettronica nella foresta Exchange 2013 di destinazione.

Per ulteriori informazioni sulla preparazione degli spostamenti tra foreste, inclusa una descrizione degli attributi di Active Directory necessari, vedere [Preparare le cassette postali per le richieste di spostamento tra foreste](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Nella pagina [Preparazione per lo spostamento delle cassette postali Online](https://go.microsoft.com/fwlink/p/?linkid=177882) in Microsoft Download Center, scaricare il codice di esempio.

  - Per eseguire il codice di esempio, è necessario ILM 2007 Feature Pack 1 Service Pack 1 (SP1). Per scaricare il Feature Pack, vedere l'articolo 977791 della Microsoft Knowledge Base, [Service Pack 1 (build 3.3.1139.2) è disponibile per Identity Lifecycle Manager 2007 Feature Pack 1](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=977791).

  - È inoltre necessario quanto segue:
    
      - Una foresta di origine su cui è installato Exchange 2013, in cui si trova al momento la cassetta postale.
    
      - Una foresta di destinazione con installato Exchange 2013, in cui verrà spostata la cassetta di postale.

  - Per connettersi alla foresta Exchange 2013 di destinazione, è necessario disporre dell'autorizzazione appropriata per eseguire il cmdlet **UpdateRecipient**. Per visualizzare le autorizzazioni necessarie, vedere la sezione "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passaggio 1: Installazione del codice di esempio per ILM

1.  In Microsoft Visual Studio 2008, aprire Microsoft.Exchange.Sample.OneWayGALSync.sln per visualizzare il codice di esempio. Il codice di esempio include quanto segue:
    
      - Microsoft.MetadirectoryServicesEx.dll è il file binario forniti con ILM 2007 FP1 SP1 in "\\Programmi\\Microsoft Identity Integration Server\\Bin\\Assemblies?. Vi viene fatto riferimento dal codice di esempio.
    
      - OneWaySync.xml: è un file a cui viene fatto riferimento dal codice di esempio.
    
      - Cartella ILMServerConfig: contiene i file di configurazione di ILM per l'agente di gestione di origine, l'agente di gestione di destinazione e il metaverse di ILM.
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll e Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll (creata nell'esempio di codice) sono in "\\obj\\Debug?

2.  Sul server ILM copiare quanto segue in \\Programmi\\Microsoft Identity Integration Server\\Extensions:
    
      - OneWaySync.xml
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll

3.  Modificare il file OneWaySync.xml copiato nella cartella ILM Extensions nel passaggio 1 specificando il nome distinto del contenitore TargetOU nella foresta di Exchange di destinazione in cui si desidera creare gli utenti di posta. Se non si conosce il nome del contenitore TargetOU, è possibile utilizzare LDP.exe o ADSIEdit.exe per la ricerca del nome.
    

    > [!NOTE]
    > Se si utilizza questo esempio insieme a ILM GalSync 2007, escludere questo contenitore dall'elenco dei contenitori gestiti da GalSync2007.



4.  In ILM Identity Manager Console, accedere a **File** \> **Import Server Configuration** per importare la configurazione del server ILM dalla cartella ILMServerConfig. Durante tale azione verranno importati due agenti di gestione di Active Directory, oltre alla regola di provisioning e allo schema del metaverse.
    

    > [!NOTE]
    > Durante l'importazione è necessario specificare il nome e le credenziali per la foresta, quindi associare le partizioni dell'agente di gestione di Active Directory importato al nome della partizione nella configurazione in uso, sia per gli agenti di gestione di origine che per quelli di destinazione.



5.  Per ADMA supportare la foresta di destinazione Exchange 2013, nella pagina **Create Management Agent** nel riquadro **Configure Extensions** seleziona **Exchange 2013** nell'elenco a discesa **per il provisioning** e quindi immettere l'URI di PowerShell remota di Windows di un server Accesso Client Exchange 2010**nell'URI di richieste al secondo di Exchange 2013**.
    
    **Pagina Create Management Agent**
    
    ![Provisioning dell'agente di gestione di Exchange 2010](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "Provisioning dell'agente di gestione di Exchange 2010")  

6.  Nel riquadro **Create Management Agent** di ILM Identity Manager Console aprire la finestra delle proprietà dell'agente di gestione della foresta di origine. Selezionare la procedura guidata **Configure Directory Partitions** e quindi fare clic su **Containers** per selezionare il contenitore in cui verranno inserite le cassette postali da spostare nella foresta di destinazione. Deselezionare tutti gli altri contenitori, ovvero limitare l'ambito dell'agente di gestione a questo singolo contenitore. Analogamente, per l'agente di gestione della foresta di destinazione selezionare il contenitore in cui eseguire il provisioning degli utenti abilitati alla posta elettronica, ovvero il contenitore TargetOU specificato nel passaggio 2.
    

    > [!NOTE]
    > Se si utilizza questo esempio insieme a ILM GalSync 2007, escludere entrambi i contenitori dall'elenco dei contenitori gestiti da GalSync 2007.



7.  Eseguire un'importazione completa iniziale (di solo appoggio) negli agenti di gestione, di modo che ILM sia in grado di individuare il contenitore TargetOU specificato nel passaggio 2.

## Passaggio 2: Creazione di un utente di posta nella foresta Exchange di destinazione

Dopo avere installato il codice di esempio, utilizzare la procedura seguente per creare l'utente di posta necessario nella foresta di Exchange di destinazione, in modo da poter eseguire il cmdlet **New-MoveRequest** per effettuare lo spostamento della cassetta postale online.

1.  Nella foresta di origine, utilizzare l'interfaccia di amministrazione di Exchange per creare utenti di cassette postali nel contenitore selezionato nel passaggio 4 della procedura "Installazione di un codice di esempio ILM". È possibile anche utilizzare Utenti e computer di Active Directory per spostare utenti di cassette postali esistenti nel contenitore.

2.  Eseguire un'importazione delta e una sincronizzazione delta sull'agente di gestione di origine per individuare le cassette postali aggiunte al contenitore di origine ed eseguire il provisioning degli utenti di posta nell'agente di gestione di destinazione.

3.  Eseguire un'esportazione sull'agente di gestione di destinazione per esportare nel sito di Active Directory di destinazione gli utenti di posta di cui è stato eseguito il provisioning nel passaggio 1.

4.  Eseguire un'importazione delta sull'agente di gestione di destinazione per confermare le modifiche esportate nel passaggio 2.

5.  Nella foresta di destinazione aprire Exchange Management Shell e utilizzare il cmdlet **New-MoveRequest** per spostare le cassette postali dalla foresta di origine.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la migrazione sia stata eseguita correttamente, procedere come segue:

  - Nella foresta di destinazione, verificare che gli utenti spostati dalla foresta di origine siano presenti nella foresta di destinazione.


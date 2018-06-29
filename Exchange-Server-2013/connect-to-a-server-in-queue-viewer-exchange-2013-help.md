---
title: 'Connettersi a un server nel Visualizzatore di code: Exchange 2013 Help'
TOCTitle: Connettersi a un server nel Visualizzatore di code
ms:assetid: 6c1ad574-9ab5-4dcc-9398-ec10eca4fd11
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998669(v=EXCHG.150)
ms:contentKeyID: 50480935
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Connettersi a un server nel Visualizzatore di code

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-03_

Quando si utilizza Visualizzatore code nella Casella degli strumenti di Exchange su un server Microsoft Exchange Server 2013 che si trova all'interno dell'organizzazione Exchange, è possibile connettersi agli altri server Cassette postali. Per impostazione predefinita, quando si apre Vista code su un server Cassette postali, Visualizzatore code si connette al database delle code sul server locale. È possibile avviare più di una istanza del Visualizzatore code in modo che ciascuna istanza faccia riferimento a un server diverso. Le finestre del Visualizzatore code possono essere affiancate per poter facilmente controllare più server Cassette postali contemporaneamente.

È anche possibile specificare il server che utilizza Remote PowerShell per eseguire le attività specificate in Vista code. Non è necessario che questo server corrisponda al server remoto che si sta gestendo in Visualizzatore code.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Code" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Le procedure descritte in questo argomento non si applicano ai server Trasporto Edge. Quando si utilizza il Visualizzatore code su un server Trasporto Edge, non è possibile modificare la priorità dello strumento.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo della Casella degli strumenti di Exchange per specificare il server che si desidera gestire in Visualizzatore code

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange Server 2013** \> **Casella degli strumenti di Exchange**.

2.  In **Strumenti flusso di posta**, fare doppio clic su **Visualizzatore code**.

3.  Nel riquadro azioni, fare clic su **Connetti al server**.

4.  Nella finestra **Connetti al server**, fare clic su **Sfoglia** per visualizzare un elenco dei server Cassette postali disponibili.

5.  Nella finestra **Seleziona Exchange Server**, selezionare un server Cassette postali. Per cercare un server Cassette postali, utilizzare una delle seguenti procedure:
    
      - Immettere il nome esatto del server o solo le prime lettere del nome nel campo **Cerca**, quindi fare clic su **Trova**. Selezionare un server dal riquadro dei risultati.
    
      - Selezionare il menu **Visualizza** e fare clic su **Mostra filtro**. Nella colonna **Nome** o nella colonna **Versione**, fare clic sull'icona del filtro e selezionare l'operatore filtro. Digitare i criteri di filtro nel campo **Immettere il testo qui**. Premere Invio. Selezionare un server dal riquadro dei risultati.

6.  Fare clic su **OK** per chiudere la finestra **Seleziona Exchange Server**.

7.  Una volta selezionato un server, nella finestra **Connetti al server**, selezionare la casella di controllo **Imposta come server predefinito** se si desidera che il Visualizzatore code faccia riferimento prima a questo server quando viene aperto.

8.  Nella finestra **Connetti al server**, fare clic su **Connetti**.

## Utilizzo di Casella degli strumenti di Exchange per specificare il server che Visualizzatore code utilizza per gestire Remote PowerShell

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange Server 2013** \> **Casella degli strumenti di Exchange**.

2.  In **Strumenti flusso di posta**, fare doppio clic su **Visualizzatore code**.

3.  Nel riquadro azioni, fare clic su **Proprietà**.

4.  Nella finestra di dialogo**Vista code - \<nome server\> Proprietà**, selezionare una delle seguenti opzioni:
    
      - **Connetti al server selezionato automaticamente**   Selezionare questa opzione per connettersi automaticamente al server di cui si stanno gestendo le code per eseguire Remote Shell.
    
      - **Specifica un server a cui connettersi**   Selezionare questa opzione per specificare un server in modo da eseguire Remote PowerShell. Se si seleziona questa opzione, fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona Exchange Server**. Selezionare li server su cui su desidera eseguire Remote PowerShell e fare clic su **OK**.

## Come verificare se l'operazione ha avuto esito positivo

L'utente dovrebbe essere in grado di gestire le code sul server Cassette postali specificato.


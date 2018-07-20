---
title: 'Impostare le opzioni Visualizzatore code: Exchange 2013 Help'
TOCTitle: Impostare le opzioni Visualizzatore code
ms:assetid: 03a9134c-0714-4c13-b286-92bccc7ec05e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa995934(v=EXCHG.150)
ms:contentKeyID: 50479920
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare le opzioni Visualizzatore code

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

È possibile impostare le opzioni nel Visualizzatore di code per regolare il numero di elementi visualizzati nella pagina e modificare l'intervallo di aggiornamento automatico. L'intervallo di aggiornamento automatico determina la frequenza con cui vengono aggiornati i risultati nel Visualizzatore di code.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Code" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare la casella degli strumenti di Exchange per impostare le opzioni Visualizzatore code

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange Server 2013** \> **Casella degli strumenti di Exchange**.

2.  In **Strumenti flusso di posta**, fare doppio clic su **Visualizzatore code**.

3.  Nel Visualizzatore di code, fare clic su **Visualizza** \> **Opzioni** per configurare le impostazioni seguenti nella finestra di dialogo **Opzioni Visualizzatore code**:
    
    1.  Nel campo **intervallo aggiornamento (secondi)** immettere la frequenza con cui il Visualizzatore code deve aggiornare la visualizzazione.
        

        > [!NOTE]
        > L'intervallo di aggiornamento automatico predefinito è 30 secondi e non possono essere definita per un periodo di tempo più breve. Se si disabilita la funzionalità di aggiornamento automatico, deselezionare la casella di controllo <STRONG>Aggiorna automaticamente schermata</STRONG> della pagina <STRONG>Opzioni Visualizzatore code</STRONG>, è necessario aggiornare manualmente i risultati vengono visualizzati nel Visualizzatore code fare clic su <STRONG>Aggiorna</STRONG>.

    
    2.  Nella casella **numero di elementi da visualizzare in ogni pagina**, immettere il numero massimo di elementi da visualizzare nel Visualizzatore di code. Questo numero deve essere compreso tra 1 e 10.000. Se si dispone di più elementi superiore a questo limite, verrà visualizzato gli elementi in gruppi il numero massimo di elementi. Ad esempio, nella figura seguente è illustrata una coda messaggi 14 con Visualizzatore code configurato per la visualizzazione di 10 elementi su ogni pagina. Il numero di oggetti nella pagina viene visualizzato in alto a destra. Nella parte inferiore della pagina, è possibile visualizzare il numero totale di elementi in coda. È possibile utilizzare i controlli di spostamento per visualizzare ulteriori elementi nella coda.

4.  Al termine, fare clic sul pulsante **OK**.
    
    **Visualizzatore code**
    
    ![Visualizzatore code con più elementi del limite elementi](images/Aa995934.e82196e6-002a-4e9e-823d-b244b0bd25e2(EXCHG.150).gif "Visualizzatore code con più elementi del limite elementi")  

## Come verificare se l'operazione ha avuto esito positivo

Significa questa procedura ha avuto esito positivo se il Visualizzatore code viene utilizzato l'intervallo di aggiornamento e il numero di elementi per le impostazioni delle pagine.


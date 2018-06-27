---
title: 'Personalizzare i modelli di informazioni: Exchange 2013 Help'
TOCTitle: Personalizzare i modelli di informazioni
ms:assetid: b4beeedd-e46f-442e-844a-e8575f95dca0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.toolbox.detailstemplate(v=EXCHG.150)
ms:contentKeyID: 50481482
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Personalizzare i modelli di informazioni

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-09-25_

L'Editor modelli di informazioni consente di personalizzare la presentazione dell'interfaccia utente grafica (GUI) lato client per le proprietà dell'oggetto a cui si accede utilizzando gli elenchi di indirizzi in MicrosoftOutlook. Ad esempio, quando un elenco di indirizzi viene aperto in Outlook, le proprietà di un determinato oggetto vengono visualizzate in base al modello di informazioni definito nell'organizzazione di Exchange. Gli oggetti possono essere personalizzati modificando le dimensioni del campo, aggiungendo o rimuovendo campi, aggiungendo o rimuovendo schede e riorganizzando i campi. Il layout dei modelli può variare in base alla lingua.

## Che cosa è necessario sapere prima di iniziare

  - Nell'Editor modelli di informazioni non è disponibile alcuna opzione di annullamento. In caso di errore, è necessario ripristinare la versione precedente. Per ulteriori informazioni, vedere [Ripristinare un modello di dettagli per la configurazione predefinita](restore-a-details-template-to-the-default-configuration-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Modelli di informazioni" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Personalizzazione dei modelli di informazioni

1.  Nella **Casella degli strumenti di Exchange** fare clic su **Editor modelli di informazioni** quindi, nel riquadro azioni, fare clic su **Apri strumento**.

2.  Nell'albero della console di Editor modelli di informazioni, fare clic su **Modelli di informazioni**.
    
    Nel riquadro dei dettagli sono visualizzate le seguenti colonne:
    
      - **Lingua**   In questa colonna vengono elencate le lingue in cui viene creato il modello.
    
      - **Tipo di modello**   In questa colonna vengono elencati i tipi di modello personalizzabili.
    
      - **Identità**   In questa colonna viene visualizzata l'identità univoca del modello.
    
      - **Creato**   In questa colonna vengono visualizzate la data e l'ora di creazione del modello.
    
      - **Modificato**   In questa colonna vengono visualizzate la data e l'ora dell'ultima modifica del modello.

3.  Per modificare un modello, fare clic sul modello desiderato e, nel riquadro azioni, scegliere **Modifica**. Ad esempio, nella seguente figura è visualizzato il modello di informazioni dei contatti **Inglese (Stati Uniti)**.
    
    **Modello di informazioni predefinito visualizzato da Outlook 2013**
    
    ![Modello predefinito di informazioni in Outlook 2007](images/JJ673049.a0af8aca-663d-4702-ab2f-9a342f481cdf(EXCHG.150).gif "Modello predefinito di informazioni in Outlook 2007")  

4.  Dopo aver scelto **Modifica**, sono disponibili numerose attività per la personalizzazione di un modello di informazioni:
    
      - Per spostare un oggetto nel riquadro di progettazione, selezionare l'oggetto, quindi trascinarlo nella nuova posizione sul modello. Durante lo spostamento dell'oggetto vengono fornite righe di allineamento.
    
      - Per modificare il testo di un'etichetta, selezionare l'etichetta nel riquadro di progettazione. Nel riquadro delle proprietà digitare il nuovo testo nella casella **Testo**. Per creare tasti di scelta rapida, è possibile utilizzare il simbolo e commerciale (&). Posizionare la e commerciale (&) prima della lettera che si desidera utilizzare come scelta rapida.
    
      - Per modificare la dimensione di un oggetto, selezionare l'oggetto, quindi trascinare i quadratini di ridimensionamento fino a raggiungere la forma e la dimensione dell'oggetto desiderate.
    
      - Per eliminare un oggetto, selezionarlo e premere CANC.
        

        > [!NOTE]
        > L'Editor modelli di informazioni non contiene il pulsante <STRONG>Annulla</STRONG> e non è possibile utilizzare i tasti di scelta rapida per annullare un'azione. Per annullare un'aggiunta al modello, utilizzare il tasto CANC. Per annullare un'eliminazione, riapplicare l'impostazione. È possibile ripristinare le impostazioni originali anche chiudendo Editor modelli di informazioni senza salvare le modifiche. Se si desidera annullare le modifiche dopo aver salvato, ripristinare il modello. Quando si ripristina un modello, tutta la personalizzazione viene persa e viene ripristinata la configurazione originale del modello. Per ulteriori informazioni su come ripristinare il modello di informazioni, vedere <A href="restore-a-details-template-to-the-default-configuration-exchange-2013-help.md">Ripristinare un modello di dettagli per la configurazione predefinita</A>.

    
      - Per aggiungere caselle di testo "Modifica", caselle di riepilogo, caselle di riepilogo a discesa multivalore o caselle di riepilogo multivalore, trascinare l'oggetto dal riquadro della casella degli strumenti al riquadro di progettazione. Impostare l'attributo dell'oggetto facendo clic sulla casella a discesa nel riquadro delle proprietà e selezionando l'attributo che verrà utilizzato da Exchange.
        

        > [!NOTE]
        > È necessario collegare l'oggetto a un attributo affinché possa essere utilizzato da Exchange. Inoltre, l'attributo determina anche il contenuto visualizzato all'utente finale in Outlook. Se non si seleziona un attributo, ne verrà selezionato automaticamente uno a caso.

    
      - Per aggiungere una casella di gruppo, trascinare l'oggetto nel riquadro di progettazione. Nel riquadro delle proprietà digitare un nome nella casella **Testo**. Utilizzare le caselle di gruppo per raggruppare oggetti simili.
    
      - Per aggiungere una scheda al modello, fare clic con il pulsante destro del mouse su una scheda esistente, quindi fare clic su **Aggiungi scheda**. Viene visualizzata una scheda vuota. Per denominare la scheda, digitare il nome nella casella **Testo** nel riquadro delle proprietà.
    
      - Per rimuovere una scheda dal modello, fare clic con il pulsante destro del mouse sulla scheda, quindi fare clic su **Rimuovi scheda**. Verrà visualizzato un avviso. Fare clic su **OK** per confermare la rimozione della scheda.
    
      - Per modificare l'ordine di tabulazione degli oggetti in una scheda, in modo da consentire agli utenti di passare da un oggetto all'altro nell'ordine desiderato premendo TAB, selezionare l'oggetto nel riquadro di progettazione. Nel riquadro delle proprietà, utilizzare la casella **TabIndex** per modificare l'ordine.
        

        > [!NOTE]
        > Per assicurarsi che gli utenti non siano in grado di utilizzare TAB per accedere alle etichette di un oggetto (ad esempio <STRONG>Nome</STRONG> o <STRONG>Alias</STRONG>), modificare l'ordine delle etichette così che risultino alla fine dell'ordine di tabulazione.



5.  Per salvare le modifiche al modello di informazioni, nel menu **File** fare clic su **Salva**.

6.  Per chiudere il modello scegliere **Chiudi** dal menu **File**.


---
title: 'Gestire criteri cassetta postale messaggistica unificata: Exchange 2013 Help'
TOCTitle: Gestire i criteri cassetta postale di messaggistica unificata
ms:assetid: 704b001c-3e6f-4ed5-bbe5-42a778f6ac0d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998829(v=EXCHG.150)
ms:contentKeyID: 50555615
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMMailboxPolicyGeneralTab
ms.translationtype: MT
---

# Gestire i criteri cassetta postale di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

Dopo aver creato un criterio cassetta postale di messaggistica unificata (UM), è possibile visualizzare e configurare diverse impostazioni. Ad esempio, è possibile configurare funzionalità di messaggistica unificata, come Anteprima messaggio vocale o Ascolta al telefono e altre opzioni relative alla protezione, come Sistema di caselle vocali protette e le impostazioni dei criteri del PIN.

Per le attività di gestione aggiuntive relative ai criteri cassetta postale di messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Utilizzo dell'interfaccia di amministrazione di Exchange per gestire un criterio cassetta postale di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale messaggistica unificata**, sulla barra degli strumenti, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    
      - Utilizzare **Generale** per visualizzare e configurare le impostazioni per un criterio cassetta postale di messaggistica unificata. Ad esempio, è possibile visualizzare i dial plan associati al criterio cassetta postale di messaggistica unificata o disabilitare le notifiche di chiamata senza risposta per gli utenti associati a uno specifico criterio cassetta postale di messaggistica unificata. Quando vengono modificate le impostazioni di un criterio cassetta postale di messaggistica unificata, tali impostazioni vengono applicate a tutti gli utenti associati a tale criterio. È possibile visualizzare o configurare quanto segue:
        
          - **Dial plan di messaggistica unificata**   Consente di visualizzare il nome del dial plan associato al criterio cassetta postale di messaggistica unificata. Si tratta del nome del dial plan visualizzato in Shell.
            
            Quando viene creato un nuovo criterio cassetta postale di messaggistica unificata, è necessario associarlo a un dial plan. Dopo aver creato un criterio cassetta postale di messaggistica unificata e averlo associato a un dial plan, le impostazioni definite su tale criterio vengono applicate agli utenti associati al dial plan. Per impostazione predefinita, quando viene creato un dial plan di messaggistica unificata tramite Shell, viene creato anche un criterio cassetta postale di messaggistica unificata.
        
          - **Nome** Digitare il nome del dial plan. Il nome del dial plan di messaggistica unificata è obbligatorio e deve essere univoco. Tuttavia, viene utilizzato solo per la visualizzazione in EAC e in Shell. Se si desidera modificare il nome visualizzato del dial plan al termine del processo di creazione, prima è necessario eliminare il dial plan esistente e crearne un'altro con il nome corretto. Se l'organizzazione utilizza più dial plan di messaggistica unificata, si consiglia di utilizzare nomi significativi per tali dial plan. La lunghezza massima per il nome di un dial plan di messaggistica unificata è di 64 caratteri e può contenere spazi. Se si sta effettuando un'integrazione con Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server si sconsiglia l'uso degli spazi. Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **Limite per i messaggi di saluto personali (minuti)**   Utilizzare questa casella di testo per immettere il numero massimo di minuti a disposizione degli utenti associati al criterio cassetta postale di messaggistica unificata per la registrazione di messaggi di saluto della segreteria telefonica. È possibile modificare questa impostazione dopo aver creato il criterio cassetta postale di messaggistica unificata. Sono consentiti solo caratteri numerici. L'intervallo valido per il messaggio di saluto è compreso tra 1 e 10 minuti. L'impostazione predefinita è di 5 minuti.
        
          - **Consenti anteprima messaggio vocale**   Selezionare o deselezionare questa casella di controllo per abilitare o disabilitare la funzionalità Anteprima messaggio vocale per gli utenti associati al criterio cassetta postale di messaggistica unificata. L'abilitazione di questa impostazione consente agli utenti di ricevere il testo di un messaggio vocale nel corpo di un messaggio di posta elettronica o di testo. L'impostazione predefinita è Abilitato.
        
          - **Consenti agli utenti di configurare le regole di risposta chiamata**   Selezionare questa casella di controllo per consentire agli utenti associati al criterio cassetta postale di messaggistica unificata di creare regole di risposta alle chiamate. Se questa opzione viene disabilitata sul dial plan di messaggistica unificata, questa funzionalità non sarà disponibile per gli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata. L'impostazione predefinita è Abilitato.
        
          - **Consenti indicatore di messaggi in attesa**   Selezionare o deselezionare questa casella di controllo per abilitare o disabilitare la funzionalità Indicatore di messaggi in attesa per gli utenti associati al criterio cassetta postale di messaggistica unificata. Message Waiting Indicator è una funzionalità di molti sistemi di caselle vocali legacy. Nella modalità più comune, sull'apparecchio telefonico dell'utente della segreteria telefonica si accende una luce che indica la presenza di un nuovo messaggio vocale. La funzionalità Indicatore di messaggi in attesa può consistere anche in un messaggio di testo inviato al cellulare dell'utente abilitato alla messaggistica unificata. L'impostazione predefinita è Abilitato.
        
          - **Consenti Outlook Voice Access**   Selezionare o deselezionare questa casella di controllo per abilitare o disabilitare l'accesso a Outlook Voice Access per gli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata. Outlook Voice Access è una funzionalità utilizzata dagli utenti abilitati alla messaggistica unificata per accedere alla cassetta postale tramite apparecchio telefonico. Questa impostazione è abilitata per impostazione predefinita.
        
          - **Consenti notifiche di chiamate senza risposta**   Selezionare o deselezionare questa casella di controllo per abilitare o disabilitare le notifiche di chiamata senza risposta per gli utenti associati al criterio cassetta postale di messaggistica unificata. Una notifica di chiamata senza risposta consiste in un messaggio di posta elettronica inviato alla cassetta postale di un utente nel caso in cui l'utente non risponda a una chiamata in arrivo. Si tratta di un messaggio di posta elettronica diverso da quello contenente il messaggio di segreteria telefonica lasciato per un utente.
            

            > [!NOTE]
            > Durante l'integrazione della messaggistica unificata con Lync Server a livello locale, le notifiche di chiamata senza risposta non sono disponibili per gli utenti la cui cassetta postale si trova su un server Cassette postali di Exchange 2007 o Exchange 2010. Una notifica di chiamata senza risposta viene generata quando un utente effettua la disconnessione prima che la chiamata sia inviata alla messaggistica unificata.

            
            In genere, quando non risponde a una chiamata in arrivo, l'utente riceve due messaggi di posta elettronica: un messaggio che contiene il messaggio di segreteria telefonica e un messaggio di notifica della chiamata senza risposta. Per impostazione predefinita, le notifiche di chiamata senza risposta vengono abilitate quando viene creato un criterio cassetta postale di messaggistica unificata.
        
          - **Consenti Ascolta al telefono per la casella vocale**   Selezionare o deselezionare questa casella di controllo per abilitare o disabilitare la funzionalità Ascolta al telefono per gli utenti associati al criterio cassetta postale di messaggistica unificata. Questa opzione viene abilitata per impostazione predefinita e consente agli utenti di riprodurre i messaggi vocali tramite telefono, incluso un telefono dell'ufficio o un cellulare.
        
          - **Consenti fax in ingresso**   Selezionare o deselezionare questa casella di controllo per abilitare o disabilitare i fax in entrata per gli utenti associati al criterio cassetta postale di messaggistica unificata. Per impostazione predefinita, quando gli utenti vengono abilitati alla messaggistica unificata, la loro cassetta postale è abilitata alla ricezione dei fax. Tuttavia, Se questa opzione viene disabilitata sul dial plan di messaggistica unificata, non sarà possibile la ricezione dei fax da parte degli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata. L'impostazione predefinita sul criterio cassetta postale di messaggistica unificata è disabilitata.
            
            Dopo aver abilitato l'impostazione **Consenti fax in ingresso**, sarà necessario specificare l'URI per il server del partner fax. Se il criterio cassetta postale di messaggistica unificata viene collegato a un dial plan che utilizza TCP e TLS, sarà necessario immettere URL sia per TCP che per TLS.
        
          - **Consenti a Microsoft di migliorare l'anteprima della casella vocale**   Queste opzioni consentono a Microsoft di migliorare la qualità di Anteprima messaggio vocale. È possibile attivare le seguenti impostazioni:
            
              - **Consenti analisi dei messaggi vocali lasciati dai chiamanti**   Utilizzare questa opzione per contribuire al miglioramento della qualità dell'anteprima del messaggio vocale nelle versioni future di Microsoft Exchange inoltrando a Microsoft le copie dei messaggi vocali per l'analisi. Non è possibile impostare questa opzione se tutti i messaggi vocali sono protetti.
            
              - **Indicare ai chiamanti che i messaggi vocali possono essere oggetto di analisi**   Utilizzare questa opzione per indicare ai chiamanti che i messaggi che lasciano possono essere analizzati da Microsoft per migliorare la qualità dell'anteprima del messaggio vocale e per consentire loro di rifiutare.
    
      - 
        
        Utilizzare **Testo messaggio** per configurare le impostazioni del testo dei messaggi per gli utenti associati a un criterio cassetta postale di messaggistica unificata. Ad esempio, è possibile specificare il testo del messaggio di posta elettronica inviato agli utenti dopo la reimpostazione del PIN di messaggistica unificata. È possibile configurare quanto segue:
        
          - **Quando un utente è abilitato alla Messaggistica unificata**   Il testo immesso in questa casella di testo viene visualizzato nel messaggio di posta elettronica inviato agli utenti quando questi sono abilitati alla messaggistica unificata. Quando una casella postale di un destinatario è abilitata alla messaggistica unificata ed è abilitata alla casella vocale, all'utente viene inviato un messaggio di posta elettronica di benvenuto alla messaggistica unificata. La casella di testo ha un limite di 512 caratteri e può contenere una semplice formattazione HTML. Per impostazione predefinita, in questa casella di testo non viene definito alcun testo.
            
            Questo messaggio di benvenuto contiene il testo di benvenuto e le informazioni sul PIN che l'utente utilizzerà per accedere al sistema di messaggistica unificata o al sistema di caselle vocali. Il testo immesso in questa casella di testo è incluso nella parte inferiore di questo messaggio di benvenuto. La casella di testo può essere utilizzata per includere informazioni, quali i numeri di telefono del supporto tecnico per la casella vocale o i numeri di Outlook Voice Access.
            
            Se il testo non viene immesso nella casella di testo, il testo predefinito generato dalla messaggistica unificata o dal sistema delle caselle vocali viene incluso nel messaggio di posta elettronica.
            
            Il testo immesso in questa casella di testo può essere testo normale. È possibile inserire anche semplici tag HTML di formattazione per evidenziare il testo o aggiungere collegamenti ipertestuali ad altri contenuti.
            
            **Esempio 1**   Per eventuali domande o suggerimenti relativi al servizio di posta vocale, chiamare il supporto tecnico all'interno 4200.
            
            **Esempio 2:**   Per eventuali domande o suggerimenti sul \<b\>servizio delle caselle vocali\</b\>, chiamare il supporto tecnico all'interno 4200 o visitare il sito Web all'indirizzo \<a href=”http://emp.contoso.com/itinfo/vmail”\>\</a\>.
        
          - **Quando il PIN di Outlook Voice Access di un utente viene reimpostato**   Il testo immesso in questa casella di testo viene incluso nel messaggio di posta elettronica inviato agli utenti abilitati alla messaggistica unificata quando il PIN di messaggistica unificata viene reimpostato.
            
            Un PIN viene reimpostato dalla messaggistica unificata o dal sistema di caselle vocali se vengono eseguiti più di 10 (per impostazione predefinita) tentativi di accesso non riusciti o se gli utenti reimpostano il PIN utilizzando le funzionalità di messaggistica unificata incluse in Microsoft Outlook Outlook Web App, o Outlook Voice Access da un telefono. Nella casella di testo è possibile includere informazioni, quali gli avvisi di protezione o altre informazioni relative alla protezione nel messaggio di posta elettronica.
            
            Se il testo non viene immesso nella casella di testo, il testo predefinito generato dal sistema viene incluso nel messaggio di posta elettronica.
            
            Questa casella di testo accetta un massimo di 512 caratteri. Per impostazione predefinita, in questa casella di testo non viene definito alcun testo.
            
            Il testo immesso in questa casella di testo può essere testo normale. È possibile inserire anche semplici tag HTML di formattazione per evidenziare il testo o aggiungere collegamenti ipertestuali ad altri contenuti.
        
          - **Quando un utente riceve un messaggio vocale**   Il testo immesso in questa casella di testo viene incluso nel messaggio di posta elettronica inviato agli utenti alla ricezione di un messaggio vocale da un chiamante in arrivo. Ad esempio, questo testo può includere dichiarazioni che contengono informazioni sull'inoltro dei messaggi vocali o sui criteri di protezione del sistema che descrivono il modo corretto di gestire i messaggi vocali nell'organizzazione.
            
            Se il testo non viene immesso nella casella di testo, il testo predefinito generato dal sistema viene incluso nel messaggio di posta elettronica. Questa casella di testo accetta un massimo di 512 caratteri. Per impostazione predefinita, in questa casella di testo non viene definito alcun testo.
            
            Il testo immesso in questa casella di testo può essere testo normale. È possibile inserire anche semplici tag HTML di formattazione per evidenziare il testo o aggiungere collegamenti ipertestuali ad altri contenuti.
        
          - **Quando un utente riceve un messaggio fax**   Il testo immesso in questa casella di testo viene incluso nel messaggio di posta elettronica inviato agli utenti alla ricezione di un messaggio fax in Posta in arrivo. La casella di testo consente di includere dichiarazioni che contengono informazioni sull'inoltro dei messaggi fax o sui criteri di protezione del sistema relativi al modo corretto di gestire i messaggi fax nell'organizzazione.
            
            Se il testo non viene immesso nella casella di testo, il testo predefinito generato dal sistema viene incluso nel messaggio di posta elettronica. Questa casella di testo accetta un massimo di 512 caratteri. Per impostazione predefinita, in questa casella di testo non viene definito alcun testo.
    
      - 
        
        Utilizzare **Criteri PIN** per configurare le impostazioni del PIN per gli utenti associati a un criterio cassetta postale di messaggistica unificata. I PIN della messaggistica unificata consentono agli utenti di accedere alle cartelle Posta in arrivo tramite un apparecchio telefonico. La configurazione delle impostazioni su questa pagina consente di specificare il numero minimo di cifre per un PIN di messaggistica unificata o il numero di tentativi di accesso non riusciti che gli utenti possono effettuare prima di essere bloccati per la cassetta postale di messaggistica unificata.
        
        Assicurarsi di pianificare molto attentamente i criteri PIN di messaggistica unificata implementati nell'ambiente. Se non vengono pianificati e implementati i criteri PIN di messaggistica unificata appropriati, è possibile che venga minacciato il sistema di protezione e consentito per errore l'accesso non autorizzato alla rete. È possibile configurare quanto segue:
        
          - **Lunghezza minima PIN (cifre)**   Utilizzare questa casella di testo per specificare il numero minimo di cifre che possono essere contenute nel PIN di un utente di messaggistica unificata. L'impostazione predefinita è di sei cifre. L'intervallo dei caratteri numerici è compreso tra 4 e 24. L'impostazione non può essere disabilitata.
            
            L'aumento del numero di cifre richieste per un PIN aumenta il livello di protezione per il sistema di messaggistica unificata. La diminuzione del numero di cifre richieste per un PIN riduce il livello di protezione per la rete. Minore è il numero di cifre richieste in un PIN, maggiore è la probabilità di potenziali attacchi in grado di identificarlo.
            
            Se il valore di questa impostazione è troppo elevato, gli utenti potrebbero avere qualche difficoltà nella memorizzazione del PIN. Tuttavia, se il valore è troppo basso, si corre il rischio di consentire un accesso non autorizzato al sistema di messaggistica unificata.
        
          - **Numero di ricicli del PIN**   Utilizzare questa impostazione per impostare il numero di PIN univoci che devono essere utilizzati dagli utenti prima che possano riutilizzare un PIN precedente. Per la maggior parte delle organizzazioni, l'impostazione predefinita di questo valore è di 5, il numero di PIN memorizzati nel sistema. La cronologia dei PIN non può essere disabilitata.
            
            Il valore è compreso tra 1 e 20. Se il valore impostato è troppo alto, gli utenti potrebbero avere alcune difficoltà nella memorizzazione di una quantità elevata di PIN. Un valore troppo basso potrebbe costituire una minaccia al sistema di protezione della rete.
        
          - **Consenti modelli di PIN comuni**   Utilizzare questa impostazione per impostare i requisiti di complessità dei PIN per la messaggistica unificata. Questi requisiti di complessità vengono applicati in caso di modifiche al PIN o se vengono creati nuovi PIN.
            
            Se questa opzione è disabilitata, i numeri sequenziali e ripetuti e il suffisso dell'estensione della cassetta postale verranno rifiutati. Se questa opzione è abilitata, verrà rifiutato solo il suffisso dell'estensione della cassetta postale.
            
            Si consiglia di disabilitare questa impostazione per consentire una maggiore protezione. Se questa impostazione è disabilitata, i PIN degli utenti non possono contenere quanto segue:
            
            Numeri sequenziali, quali 123456 o 456789.
            
            Numeri che si ripetono, quali 111111 o 8888888.
            
            Suffisso dell'estensione della cassetta postale.
        
          - **Imponi durata PIN (giorni)**   Utilizzare questa casella di testo per configurare il numero di giorni rimanenti prima della scadenza del PIN di un utente abilitato alla messaggistica unificata. Dopo la scadenza del PIN, l'utente deve creare un nuovo PIN di messaggistica unificata. Per la maggior parte delle organizzazioni, l'impostazione predefinita di questo valore è di 60 giorni.
            
            Il valore di questa impostazione è compreso tra 0 e 999. Se il valore è impostato su 0, il PIN non ha scadenza. L'impostazione di un valore troppo basso può creare alcune difficoltà agli utenti perché costretti a creare e a memorizzare nuovi PIN con troppa frequenza.
        
          - **Numero di errori di accesso prima della reimpostazione del PIN**   Utilizzare questa casella di testo per immettere il numero di tentativi sequenziali di accesso non riusciti o con errore che possono essere effettuati prima della reimpostazione automatica del PIN di un utente. Per la maggior parte delle organizzazioni, l'impostazione predefinita di questo valore è di 5 tentativi.
            
            Il valore di questa impostazione è compreso tra 0 e 999. Se impostata su 0, questa impostazione viene disabilitata e i PIN degli utenti non verranno reimpostati automaticamente. L'impostazione di un valore troppo basso può creare alcune difficoltà agli utenti, mentre l'impostazione di un valore troppo alto può facilitare la determinazione del PIN da parte di utenti malintenzionati.
            
            È necessario che il valore impostato sia minore del valore configurato nell'impostazione **Numero di errori accesso prima del blocco**. Questa impostazione è stata progettata per prevenire un attacco massiccio ai PIN degli utenti.
        
          - **Numero di errori accesso prima del blocco**   Utilizzare questa casella di testo per immettere il numero massimo di tentativi sequenziali di accesso non riusciti o con errore che gli utenti possono effettuare prima di essere bloccati per la cassetta postale.
            
            Se, ad esempio, un utente effettua cinque tentativi non riusciti di accesso alla cassetta postale, in base all'impostazione **Numero di errori di accesso prima della reimpostazione del PIN**, il PIN dell'utente verrà reimpostato. Se l'utente effettua altri cinque tentativi non riusciti per il nuovo PIN, il PIN verrà comunque reimpostato. Tuttavia, in seguito ad altri cinque tentativi non riusciti, avverrà il blocco della cassetta postale per l'utente. Dopo il blocco, un amministratore deve reimpostare manualmente o sbloccare la cassetta postale dell'utente.
            
            Questo valore può essere impostato tra 1 e 999. L'impostazione di un valore troppo basso può creare alcune difficoltà agli utenti, mentre l'impostazione di un valore troppo alto può facilitare la determinazione del PIN da parte di utenti malintenzionati. Per la maggior parte delle organizzazioni, l'impostazione predefinita di questo valore è di 15 tentativi.
            
            È necessario che il numero impostato sia maggiore del numero impostato in **Numero di errori di accesso prima della reimpostazione del PIN**. Questa impostazione è stata progettata per prevenire un attacco massiccio ai PIN degli utenti.
    
      - 
        
        Utilizzare **Autorizzazione di composizione** per configurare le regole di composizione per gli utenti abilitati alla messaggistica unificata che sono associati al criterio cassetta postale di messaggistica unificata.
        
        È possibile utilizzare queste impostazioni per controllare i numeri di interni che possono essere raggiunti o i numeri di telefono che possono essere composti dagli utenti abilitati alla messaggistica unificata che sono associati al criterio cassetta postale di messaggistica unificata. È possibile configurare quanto segue:
        
          - **Consenti chiamate nello stesso dial plan di messaggistica unificata**   Selezionare questa casella di controllo per consentire agli utenti abilitati alla messaggistica unificata che compongono un numero di accesso del sottoscrittore configurato in un dial plan e accedono correttamente alla cassetta postale di effettuare o trasferire chiamate a utenti abilitati alla messaggistica unificata con numeri di interni contenuti nello stesso dial plan. Questa impostazione è abilitata per impostazione predefinita.
            
            Quando questa impostazione viene disabilitata, gli utenti abilitati alla messaggistica unificata che chiamano il numero di accesso di un sottoscrittore configurato in un dial plan e che accedono correttamente alla cassetta postale possono effettuare o trasferire chiamate agli utenti non abilitati alla messaggistica unificata o ad altri numeri di interni non associati a un utente abilitato alla messaggistica unificata. Tuttavia, non possono trasferirle agli utenti abilitati alla messaggistica unificata nello stesso dial plan. Questa situazione si verifica poiché l'impostazione **Consenti chiamate a qualsiasi interno** è abilitata per impostazione predefinita.
        
          - **Consenti chiamate a qualsiasi interno**   Quando questa impostazione è abilitata, gli utenti che chiamano il numero di accesso di un sottoscrittore configurato in un dial plan e che accedono correttamente alla cassetta postale possono effettuare chiamate agli utenti non abilitati alla messaggistica unificata, ad altri numeri di interni non associati a un utente abilitato alla messaggistica unificata e a utenti abilitati alla messaggistica unificata nello stesso dial plan. Tale condizione si verifica perché l'impostazione **Chiamate nello stesso dial plan di messaggistica unificata** è abilitata per impostazione predefinita.
            
            Quando questa impostazione è disabilitata, gli utenti che chiamano il numero di Outlook Voice Access configurato in un dial plan e che accedono correttamente alla cassetta postale non possono effettuare chiamate agli utenti non abilitati alla messaggistica unificata o ad altri numeri di interni non associati a un utente abilitato alla messaggistica unificata. Tuttavia, tali utenti possono effettuare chiamate o trasferirle a numeri di interni associati a utenti abilitati alla messaggistica unificata. Tale condizione si verifica perché l'impostazione **Chiamate nello stesso dial plan di messaggistica unificata** è abilitata per impostazione predefinita. Per impostazione predefinita, l'impostazione **Consenti chiamate a qualsiasi interno** è abilitata.
            
            È possibile abilitare questa impostazione in un ambiente in cui non tutti gli utenti sono stati abilitati alla messaggistica unificata. Questa impostazione si rivela utile anche quando si desidera consentire agli utenti che chiamano il numero di Outlook Voice Access configurato in un dial plan di effettuare chiamate a numeri di interni non associati a un utente abilitato alla messaggistica unificata.
        
          - **Gruppi di regole nazionali consentiti dal dial plan**   Utilizzare questa sezione per aggiungere o rimuovere i gruppi di regole di composizione nazionali consentiti. Per impostazione predefinita, non sono presenti gruppi di regole di composizione nazionali configurati nei criteri cassetta postale di messaggistica unificata.
            
            I gruppi di regole di composizione nazionali sono utilizzati per consentire o limitare i numeri di telefono di un paese che gli utenti di Outlook Voice Access possono comporre. Ciò consente di evitare chiamate non necessarie o non autorizzate e costi relativi alle chiamate.
            
            Per aggiungere gruppi di regole di composizione nazionali, è necessario innanzitutto creare gruppi di regole di composizione nazionali appropriati nel dial plan associato al criterio cassetta postale di messaggistica unificata, quindi aggiungere le voci delle regole di composizione appropriate nel gruppo di regole di composizione. Una volta creati i gruppi di regole di composizione richiesti nel dial plan, è necessario aggiungere tali gruppi all'elenco delle restrizioni di composizione sotto **Autorizzazione di composizione** nel criterio cassetta postale di messaggistica unificata.
            
            I gruppi di regole di composizione nazionali possono essere utilizzati per abilitare Messaggistica unificata al fine di consentire o limitare l'accesso ai numeri di telefono nazionali. Questa impostazione viene applicata agli utenti di Outlook Voice Access che hanno chiamato un numero di Outlook Voice Access.
        
          - **Gruppi di regole internazionali consentiti dal dial plan**   Utilizzare questa sezione per aggiungere o rimuovere i gruppi di regole di composizione internazionali consentiti. Per impostazione predefinita, non sono presenti gruppi di regole di composizione internazionali configurati nei criteri cassetta postale di messaggistica unificata.
            
            Per aggiungere gruppi di regole di composizione internazionali, è necessario innanzitutto creare gruppi di regole di composizione internazionali appropriati nel dial plan associato al criterio cassetta postale di messaggistica unificata, quindi aggiungere le voci delle regole di composizione appropriate nel gruppo di regole di composizione. Una volta creati i gruppi di regole di composizione richiesti, è necessario aggiungere tali gruppi alle restrizioni di composizione nel criterio cassetta postale di messaggistica unificata.
            
            I gruppi di regole di composizione internazionali possono essere utilizzati per abilitare Messaggistica unificata al fine di consentire o limitare l'accesso ai numeri di telefono internazionali. Questa impostazione viene applicata agli utenti di Outlook Voice Access che hanno chiamato un numero di Outlook Voice Access.
            
            I gruppi di regole di composizione internazionali vengono utilizzati per consentire o limitare i numeri di telefono internazionali che gli utenti di Outlook Voice Access possono comporre. Ciò consente di evitare chiamate non necessarie o non autorizzate e costi relativi alle chiamate.
    
      - 
        
        Utilizzare **Casella vocale protetta** per configurare le seguenti impostazioni:
        
          - **Proteggi messaggi vocali da parte di chiamanti non autenticati**   Selezionare una delle seguenti opzioni dall'elenco a discesa per determinare se una chiamata in entrata a cui risponde Messaggistica unificata proteggerà i messaggi vocali. Questa impostazione si applica ai messaggi vocali inviati agli utenti abilitati alla messaggistica unificata quando non rispondono al telefono. Questa impostazione viene applicata anche ai messaggi vocali inviati direttamente agli utenti abilitati alla messaggistica unificata quando il chiamante utilizza un operatore automatico di messaggistica unificata. È possibile configurare quanto segue:
            
            **Nessuno**   Utilizzare questa impostazione per non avere alcuna protezione applicata a qualsiasi messaggio vocale inviato agli utenti abilitati alla messaggistica unificata.
            
            **Privato**   Utilizzare questa impostazione quando si desidera applicare la protezione solo ai messaggi vocali contrassegnati come privati dal chiamante.
            
            **Tutti**   Utilizzare questa impostazione se si desidera applicare la protezione a tutti i messaggi vocali, compresi quelli non contrassegnati come privati.
        
          - **Proteggi messaggi vocali da parte di chiamanti autenticati**   Selezionare una delle seguenti opzioni dall'elenco a discesa per determinare se una chiamata in entrata a cui risponde Messaggistica unificata proteggerà i messaggi vocali. Questa impostazione si applica ai messaggi vocali inviati agli utenti abilitati alla messaggistica unificata quando non rispondono al telefono. L'impostazione si applica anche quando i chiamanti accedono alla loro cassetta postale utilizzando Outlook Voice Access e successivamente creano e inviano un messaggio vocale. È possibile configurare quanto segue:
            
            **Nessuno**   Utilizzare questa impostazione per non avere alcuna protezione applicata a qualsiasi messaggio vocale inviato agli utenti abilitati alla messaggistica unificata.
            
            **Privato**   Utilizzare questa impostazione quando si desidera applicare la protezione solo ai messaggi vocali contrassegnati come privati dal chiamante.
            
            **Tutti**   Utilizzare questa impostazione se si desidera applicare la protezione a tutti i messaggi vocali, compresi quelli non contrassegnati come privati.
        
          - **Richiedi Ascolta al telefono per i messaggi vocali protetti**   Selezionare questa casella di controllo se si desidera imporre agli utenti che ricevono messaggi vocali protetti di utilizzare la funzionalità Ascolta al telefono. Oppure, se il software client non supporta la gestione dei diritti, gli utenti devono utilizzare Outlook Voice Access. La funzionalità Ascolta al telefono viene applicata solo ai client con una versione di Outlook che supporta la gestione dei diritti. Per Outlook 2007 e versioni precedenti che non supportano la gestione dei diritti e per i client Outlook Web App, Outlook Voice Access è l'unico modo con cui gli utenti possono ascoltare la posta vocale protetta.
            
            L'impostazione predefinita richiede che tutti gli utenti associati al criterio cassetta postale di messaggistica unificata utilizzino la funzionalità Ascolta al telefono per ascoltare i messaggi vocali protetti. In questo modo, si impedisce ad altre persone di ascoltare il messaggio vocale utilizzando un lettore multimediale sugli altoparlanti del computer o utilizzando un lettore multimediale su un cellulare. Anche se la funzionalità è abilitata, un utente abilitato alla messaggistica unificata può ancora utilizzare Outlook Voice Access per ascoltare la posta vocale protetta.
            
            Ciò è particolarmente utile quando gli utenti abilitati alla messaggistica unificata utilizzano computer pubblici, computer portatili in luoghi pubblici o il lettore multimediale del cellulare per ascoltare la posta vocale protetta contenente informazioni private.
        
          - **Consenti risposte vocali a messaggi di posta elettronica e elementi del calendario**   Utilizzare questa opzione per consentire agli utenti di messaggistica unificata di inviare risposte vocali a messaggi vocali protetti. L'impostazione predefinita è abilitata. Se questa opzione viene disabilitata, quando un utente abilitato alla messaggistica unificata riceve un messaggio vocale protetto, non sarà in grado di utilizzare Outlook Voice Access per rispondere a messaggi di posta elettronica e elementi del calendario.
        
          - **Messaggio per gli utenti senza il supporto di Windows Rights Management**   L'accesso ai messaggi vocali protetti è consentito solo ai client di posta elettronica che supportano Information Rights Management (IRM) o se un utente abilitato alla messaggistica unificata utilizza Outlook Voice Access per accedere al messaggio vocale protetto.
            
            Se un messaggio vocale protetto viene inviato a un client di posta elettronica che non supporta IRM, il testo immesso nella casella verrà inviato all'utente in un messaggio di posta elettronica. Queste informazioni devono includere le istruzioni su cosa fare per ricevere la posta vocale protetta.

## Gestione di un criterio cassetta postale di messaggistica unificata tramite Shell

In questo esempio vengono impostate le impostazioni del PIN per gli utenti associati al criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN that is used to allow you access to your mailbox using Outlook Voice Access has been reset."

In questo esempio vengono selezionati i gruppi nazionali e i gruppi internazionali tra quelli configurati nel dial plan di messaggistica unificata associato al criterio cassetta postale di messaggistica unificata. Gli utenti abilitati alla messaggistica unificata associati a tale criterio potranno effettuare chiamate in uscita in base alle regole definite in tali gruppi.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowDialPlanSubscribers $true -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2 -AllowExtensions $true 

In questo esempio viene configurato il testo dei messaggi vocali inviati agli utenti abilitati alla messaggistica unificata e il testo incluso in un messaggio di posta elettronica inviato a un utente abilitato alla messaggistica unificata.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -UMEnabledText "You have been enabled for Unified Messaging." -VoiceMailText "You have received a voice message from Microsoft Exchange 2013 Unified Messaging." 

## Visualizzazione delle proprietà dei criteri cassetta postale di messaggistica unificata tramite Shell

In questo esempio viene restituito un elenco formattato di tutti i criteri cassetta postale di messaggistica unificata creati nella foresta di Active Directory.

    Get-UMMailboxPolicy | Format-List

In questo esempio vengono restituite le proprietà e i valori per il criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Get-UMMailboxPolicy -Identity MyUMMailboxPolicy


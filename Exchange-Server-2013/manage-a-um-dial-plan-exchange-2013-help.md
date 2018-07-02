---
title: 'Gestire un dial plan di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Gestire un dial plan di messaggistica unificata
ms:assetid: a89735e4-36ec-49fb-ad0f-192fad37e801
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124090(v=EXCHG.150)
ms:contentKeyID: 50481367
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.DialPlanGeneralPropertyPage
ms.translationtype: MT
---

# Gestire un dial plan di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2018-04-26_

Dopo aver creato un dial plan di messaggistica unificata, è possibile visualizzare e configurare numerose impostazioni. Ad esempio, è possibile configurare il livello di protezione VoIP (Voice over IP), il codec audio e le restrizioni di composizione. Le impostazioni configurate sul dial plan di messaggistica unificata interessano tutti gli utenti collegati al dial plan per mezzo di un criterio cassetta postale di messaggistica unificata.

Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare EAC per visualizzare o configurare le proprietà del dial plan di messaggistica unificata

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera visualizzare o modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Nuovo dial plan di messaggistica unificata** fare clic su **Configura**. Utilizzare le opzioni di configurazione per visualizzare le impostazioni specifiche del dial plan oppure per abilitare o disabilitare le funzionalità descritte nei passaggi seguenti.

4.  **Generale**   Utilizzare questa pagina per visualizzare le impostazioni specifiche del dial plan oppure per abilitare o disabilitare le funzionalità per gli utenti abilitati alla messaggistica unificata:
    
      - **Nome**   Digitare il nome del dial plan creato. La lunghezza massima per il nome di un dial plan di messaggistica unificata è di 64 caratteri e può contenere spazi. Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - Anche se è possibile includere spazi nel nome di un dial plan di messaggistica unificata, se la messaggistica unificata viene integrata con Office Communications Server 2007 R2 o Microsoft Lync Server, il nome del dial plan non può contenere spazi. Di conseguenza, se è stato creato un dial plan con spazi nel nome visualizzato e la messaggistica unificata viene integrata con Office Communications Server 2007 R2 o Lync Server 2010, è necessario prima eliminare il dial plan, quindi crearne un altro il cui nome visualizzato non contenga spazi.
        

        > [!IMPORTANT]
        > Anche se la casella per il nome del dial plan può contenere fino a 64 caratteri, il nome del dial plan non può superare i 49 caratteri. Se si cerca di creare un nome di dial plan che contiene più di 49 caratteri, verrà visualizzato un messaggio di errore indicante che non è stato possibile creare il criterio cassetta postale di messaggistica unificata perché il nome del dial plan di messaggistica unificata era troppo lungo. Ciò accade perché, come giù spiegato in precedenza, quando si crea un dial plan viene creato anche un criterio cassetta postale di messaggistica unificata predefinito denominato <EM>&lt;DialPlanName&gt;</EM>. Quando i 15 caratteri del criterio predefinito vengono aggiunti al nome del dial plan, i caratteri totali superano il limite. Il parametro <EM>name</EM> può contenere 64 caratteri per il dial plan e il criterio cassetta postale di messaggistica unificata. Tuttavia, se il nome del dial plan è più lungo di 49 caratteri, il nome del criterio cassetta postale di messaggistica unificata predefinito sarà più lungo di 64 caratteri superando il limite consentito.

    
      - **Lunghezza numero interno (cifre)**   Il numero di cifre nei numeri interni per gli utenti associati a questo dial plan. Ad esempio, se un utente associato a un dial plan utilizza un numero di interno di 4 cifre per chiamare un altro utente nello stesso dial plan, selezionare 4 come numero di cifre dell'interno.
        
        Il numero di cifre dei numeri interni è basato sul dial plan di telefonia creato su un IP-PBX o un PBX. È un campo obbligatorio il cui intervallo di valori è compreso tra 1 e 20. La lunghezza tipica dell'interno è compresa tra 3 e 7 cifre. Se l'ambiente di telefonia esistente contiene numeri di interno, è necessario specificare un numero di cifre corrispondente al numero di cifre di quegli interni durante la creazione del dial plan di messaggistica unificata.
    
      - **Tipo di dial plan**   Un URI (Uniform Resource Identifier) è una stringa di caratteri che identifica o denomina una risorsa. Lo scopo principale di questa identificazione è consentire a dispositivi VoIP e PBX di comunicare tramite protocolli specifici con altri dispositivi collegati in rete. Gli URI vengono definiti in base a schemi che, a loro volta, specificano la sintassi, il formato e i protocolli utilizzati per la chiamata. In parole semplici, questo formato vien passato da IP PBX o PBX e il tipo di dial plan creato deve corrispondere al formato. Dopo aver creato un dial plan di messaggistica unificata, per modificare il tipo di dial plan sarà necessario eliminarlo e ricrearne uno del tipo corretto. È possibile selezionare uno dei seguenti tipi di dial plan:
        
          - **Interno telefonico**   Rappresenta il tipo di dial plan più diffuso. Le informazioni relative alle parti chiamante e chiamata fornite dal gateway VoIP o dal IP PBX (Private Branch eXchange) sono elencate in uno dei seguenti formati: Tel:512345 oppure 512345@\<*indirizzo IP*\>. Questo è il tipo di predefinito per i dial plan.
        
          - **URI SIP**   Utilizzare questo tipo di dial plan per creare un dial plan URI SIP (Session Initiation Protocol), ad esempio per un IP PBX che supporta il routing SIP, un PBX abilitato a SIP o per l'integrazione di Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server e messaggistica unificata. Le informazioni relative alle parti chiamante e chiamata dal gateway VoIP. L'IP PBX, il PBX abilitato a SIP, Communications Server 2007 R2 o Lync Server è elencato come indirizzo SIP nel formato seguente: sip:\<*nomeutente*\>@\<*dominio* o *indirizzo IP*\>:Porta.
        
          - **E.164**   E.164 è un piano di numerazione internazionale per reti telefoniche pubbliche in cui ciascun numero include un codice di paese, un codice di destinazione nazionale e un numero di sottoscrittore. Le informazioni relative alle parti chiamante e chiamata inviate dal gateway VoIP e PBX o IP PBX vengono elencate nel formato seguente: Tel:+14255550123.
        

        > [!NOTE]
        > Dopo aver creato un dial plan, per modificarne il tipo sarà necessario eliminarlo e ricrearne uno del tipo corretto.

    
      - modalità **Protezione VoIP**   Utilizzare questo elenco a discesa per selezionare l'impostazione di protezione VoIP per il dial plan di messaggistica unificata. Per il dial plan è possibile selezionare una delle impostazioni di protezione seguenti:
        
          - **Non protetto**   Per impostazione predefinita, quando si crea un dial plan di messaggistica unificata, la segnalazione SIP o il traffico RTP non vengono crittografati. In modalità non protetta, i server Exchange associati al dial plan di messaggistica unificata inviano e ricevono dati dai gateway VoIP, IP PBX, SBC e altri server Exchange senza utilizzare la crittografia. Nella modalità non protetta, le informazioni relative al canale di supporto RTP e alla segnalazione SIP non vengono crittografate.
        
          - **SIP con protezione**   Quando si seleziona **SIP con protezione**, viene crittografato solo il traffico della segnalazione SIP e i canali di supporto RTP utilizzano sempre il protocollo TCP, non crittografato. Con la modalità SIP protetta, per crittografare il traffico di segnalazione SIP e i dati VoIP, viene utilizzato MTLS (Mutual Transport Layer Security).
        
          - **Protetto**   Quando si seleziona **Protetto**, vengono crittografati sia il traffico di segnalazione SIP che i canali di supporto RTP. Sia il canale dei supporti di segnalazione protetto che utilizza il protocollo SRTP (Secure Realtime Transport Protocol) che il traffico di segnalazione SIP utilizzeranno Mutual TLS per crittografare i dati VoIP.

5.  **Codici di chiamata**   Utilizzare questa pagina per configurare i codici di composizione per un dial plan di messaggistica unificata. È possibile configurare diversi codici di chiamata sul dial plan. Un esempio sono le opzioni per le chiamate in ingresso e in uscita. È possibile configurare quanto segue:
    
      - **Codici di chiamata per le chiamate in uscita**   Utilizzare queste impostazioni per specificare i codici di composizione per le chiamate in uscita che possono essere effettuate dagli utenti abilitati alla messaggistica unificata. Queste chiamate in uscita vengono effettuate utilizzando Outlook Voice Access o da un messaggio della segreteria telefonica.
        
          - **Codice di accesso linea esterna**   Utilizzare questo campo per immettere il numero o i numeri utilizzati per accedere a un numero di telefono esterno per le chiamate esterne in uscita. Questo numero precederà il numero di telefono composto. Questo codice viene anche denominato codice di accesso a linea interurbana. Il campo consente di immettere da 1 a 16 cifre. Per molte organizzazioni il numero corrisponde a 9. Per impostazione predefinita questo campo è vuoto.
            
            Di frequente tale impostazione è utilizzata in ambienti di telefonia in cui un IP-PBX è collocato in sede o è mantenuto in un'organizzazione. La configurazione può non essere necessaria se l'ambiente di telefonia dell'organizzazione è gestito da un'azienda esterna o da un fornitore.
        
          - **Codice di accesso internazionale**   Utilizzare questo campo per immettere il codice numerico utilizzato per accedere ai numeri di telefono internazionali per le chiamate in uscita. Questo numero precederà il numero di telefono composto. Per impostazione predefinita, questo campo è vuoto. Il campo consente di immettere da 1 a 4 cifre. Ad esempio, il prefisso internazionale per gli Stati Uniti è 011, per l'Europa è 00.
        
          - **Prefisso numero nazionale**   Utilizzare questo campo per immettere il codice numerico utilizzato per comporre numeri di telefono nazionali. Questo numero precederà il numero di telefono composto. Per impostazione predefinita, questo campo è vuoto. Il campo consente di immettere da 1 a 4 cifre. Ad esempio, 0 è utilizzato in Europa e 1 nel Nord America.
        
          - **Codice paese**   Utilizzare questo campo per digitare il numero del codice paese utilizzato per le chiamate in uscita. Questo numero precederà il numero di telefono composto. Per impostazione predefinita, questo campo è vuoto. Il campo consente di immettere da 1 a 4 cifre. Ad esempio, negli Stati Uniti il codice paese è 1, nel Regno Unito è 44.
    
      - **Formati di numero per la composizione nei dial plan di messaggistica unificata**   Utilizzare queste impostazioni per configurare le chiamate tra gli utenti in dial plan separati quando effettuano chiamate tra i dial plan.
        
          - **Formato numero nazionale**   Utilizzare questo campo per specificare le modalità di composizione del numero di telefono di un utente da parte dei server Exchange quando gli utenti si trovano in un dial plan diverso ma con lo stesso codice di paese. Verrà utilizzato dagli operatori automatici e quando un utente di Outlook Voice Access cerca e prova a chiamare l'utente nella directory.
            
            Questa voce è costituita da un prefisso numerico e da un numero variabile di caratteri (ad esempio 020*xxxxxxx*). Per determinare il numero di telefono, la messaggistica unificata aggiungerà le ultime *x* cifre dal numero di telefono specificato nella directory al prefisso specificato.
        
          - **Formato numero internazionale**   Utilizzare questo campo per specificare le modalità di composizione del numero di telefono di un utente tramite messaggistica unificata quando gli utenti si trovano in dial plan diversi con codici di paese differenti. Verrà utilizzato da un operatore automatico e quando un utente di Outlook Voice Access cerca e prova a chiamare l'utente nella directory.
            
            Questa voce è costituita da un prefisso numerico e da un numero variabile di caratteri (ad esempio 4420*xxxxxxx*). Per determinare il numero di telefono, Messaggistica unificata aggiungerà le ultime *x* cifre dal numero di telefono specificato nella directory al prefisso specificato.
        
          - **Formati dei numeri delle chiamate in ingresso nello stesso dial plan**   Utilizzare questo campo per aggiungere e rimuovere un formato di numero per le chiamate in ingresso effettuate tra utenti nello stesso dial plan. Questo campo accetta sia i numeri sia la lettera "x" come carattere jolly. Nel campo non possono essere utilizzate altre lettere.
            
            Per le chiamate in arrivo nello stesso dial plan, aggiungere un formato di numero. Ad esempio, per aggiungere un formato di numero per gli interni con 5 cifre, immettere 142570xxxxx e fare clic su ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per rimuovere un formato di numero, fare clic su ![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

6.  **Outlook Voice Access**   Utilizzare questa pagina per configurare le impostazioni di Outlook Voice Access per il dial plan di messaggistica unificata. Outlook Voice Access consente agli utenti di accedere alle proprie cassette postali per recuperare messaggi di posta elettronica, messaggi vocali, contatti e informazioni del calendario per mezzo di un telefono. È possibile visualizzare o configurare quanto segue:
    
      - **Formula di benvenuto**   Questo campo di sola visualizzazione mostra il nome del file audio che sarà utilizzato per la formula di benvenuto.
        
          - **Messaggio di saluto predefinito**   Il messaggio di saluto è utilizzato quando un utente di Outlook Voice Access o un altro chiamante contatta il numero di Outlook Voice Access ed esegue una ricerca nella directory. Questo file audio è la formula predefinita per un dial plan di messaggistica unificata. Tuttavia, è possibile che si desideri modificare questo messaggio di saluto con una formula specifica per la propria società, ad esempio "Benvenuti in Outlook Voice Access per Contoso, Ltd."
            
            Se si decide di personalizzare la formula, è necessario innanzitutto registrare la formula personalizzata, salvarla come file WAV, quindi configurare il dial plan affinché la utilizzi. Il nome del file e il percorso non devono superare 255 caratteri.
            
            È possibile aggiungere un messaggio di saluto personalizzato scegliendo **Cambia** e poi facendo clic su **Sfoglia** per selezionare un messaggio di saluto personalizzato registrato in precedenza e specificare il file audio (WAV) da utilizzare per il messaggio di saluto. Se non si specifica un file audio, gli utenti di Outlook Voice Access ascolteranno la formula di benvenuto predefinita: "Benvenuti. Siete connessi a Microsoft Exchange."
    
      - **Messaggio informativo**   Quando è abilitata, questa registrazione facoltativa viene riprodotta subito dopo il messaggio di saluto Orario non di ufficio o Orario di ufficio. Un messaggio informativo può dichiarare i criteri di sicurezza dell'organizzazione per l'accesso al sistema, ad esempio: "Una volta ottenuto l'accesso al sistema tramite Outlook Voice Access, l'utente accetta le condizioni del nostro contratto commerciale e tutti i criteri di sicurezza dell'organizzazione. L'accesso al sistema è monitorato ed eventuali tentativi di accesso illegali saranno perseguiti a norma di legge." L'annuncio informativo può anche fornire informazioni conformi ai criteri aziendali, ad esempio: "È possibile che le chiamate siano monitorate a scopo di training." Se è importante che i chiamanti ascoltino l'intero messaggio informativo, può essere impostato come continuo.
        
        Per impostazione predefinita, nei dial plan di messaggistica unificata non è configurato alcun messaggio informativo. Per abilitare un messaggio informativo e utilizzare un file audio personalizzato specifico per l'organizzazione, fare clic su **Cambia** e quindi su **Sfoglia**.
    
      - **Consenti interruzione annuncio**   Selezionare questa casella di controllo per consentire all'utente di Outlook Voice Access di interrompere il messaggio informativo. È opportuno abilitare questa opzione se si riproducono messaggi informativi lunghi. Gli utenti di Outlook Voice Access potrebbero spazientirsi se il messaggio informativo è lungo e se non possono interromperlo per accedere alle opzioni fornite dal dial plan di messaggistica unificata.
    
      - **Numeri di Outlook Voice Access**   Utilizzare questo campo per aggiungere un numero di telefono o di interno o un URI SIP che un utente di Outlook Voice Access potrà chiamare per accedere al sistema di segreteria telefonica utilizzando Outlook Voice Access. Nella maggior parte dei casi, è sufficiente immettere un numero di interno o un numero di telefono esterno. Tuttavia, poiché questo campo accetta tutti i caratteri alfanumerici, è possibile utilizzare un URI SIP se si utilizza un IP-PBX, Office Communications Server 2007 R2 o Microsoft Lync Server.
        
        Per impostazione predefinita, quando si crea un dial plan non vengono definiti numeri di Outlook Voice Access. Per consentire agli utenti di Outlook Voice Access di chiamare Outlook Voice Access, è necessario configurare almeno un numero di telefono. Non è possibile immettere più di 20 caratteri alfanumerici.
        
        Quando si configura questo numero nel dial plan, il numero sarà visualizzato in Microsoft OfficeOutlook 2007 o versioni successive e in Outlook Web App per le opzioni della segreteria telefonica.
        
        Per aggiungere un nuovo numero di Outlook Voice Access, immettere il numero nella casella e fare clic su ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per rimuovere un numero di Outlook Voice Access, fare clic su ![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

7.  **Impostazioni**   Utilizzare questa pagina per configurare le impostazioni del dial plan per la messaggistica unificata. Quando si configurano le impostazioni in questa pagina, è possibile controllare in che modo gli utenti di Outlook Voice Access e i chiamanti esterni che contattano un operatore automatico collegato al dial plan possono individuare gli utenti nell'organizzazione, il codec audio utilizzato per i messaggi della segreteria telefonica, il numero di errori di accesso e i valori di timeout. È possibile configurare quanto segue:
    
      - **Metodo principale di ricerca dei nomi**   Utilizzare questo elenco per selezionare il metodo principale con cui i chiamanti possono individuare un utente quando effettuano una chiamata telefonica al sistema.
        
        La selezione predefinita è **Cognome Nome**. In pratica, quando gli utenti cercano un utente nella directory, digiteranno prima il cognome e poi il nome dell'utente da cercare.
        
        Quando un utente di Outlook Voice Access effettua la chiamata a un numero Outlook Voice Access per accedere alla cassetta postale, un utente effettua una chiamata al numero Outlook Voice Access per eseguire la ricerca nella directory oppure un chiamante chiama un operatore automatico collegato a un dial plan di messaggistica unificata, può cercare un utente nella directory pronunciandone il nome o l'alias.
        
        È necessario selezionare uno dei metodi supportati per poter utilizzare il metodo principale di composizione per nome. Di seguito sono elencati i metodi supportati:
        
          - **Cognome Nome (impostazione predefinita)**
        
          - **Nome Cognome**
        
          - **Indirizzo SMTP**
    
      - **Metodo secondario di ricerca dei nomi**   Utilizzare questo elenco per selezionare il metodo secondario con cui i chiamanti possono individuare un utente quando effettuano una chiamata telefonica al sistema.
        
        Per impostazione predefinita è selezionato **Indirizzo SMTP**. In pratica, quando gli utenti cercano un utente nella directory, digiteranno l'alias di posta elettronica o l'indirizzo SMTP dell'utente da cercare.
        
        Quando un utente di Outlook Voice Access effettua la chiamata a un numero Outlook Voice Access per accedere alla cassetta postale, un utente effettua una chiamata al numero Outlook Voice Access per eseguire la ricerca nella directory oppure un chiamante chiama un operatore automatico collegato a un dial plan di messaggistica unificata, può cercare un utente nella directory pronunciandone il nome o l'alias. Quando si seleziona una di queste opzioni, i chiamanti possono utilizzare il metodo principale o secondario di ricerca dei nomi per individuare gli utenti nella directory.
        
        Non è necessario selezionare nessuno dei quattro metodi supportati. Tuttavia, se non si seleziona un metodo secondario per la ricerca degli utenti, ai chiamanti sarà fornito un solo metodo per la ricerca di un utente. Sono disponibili le seguenti opzioni:
        
          - **Cognome Nome**
        
          - **Nome Cognome**
        
          - **Indirizzo SMTP** (impostazione predefinita)
        
          - **Nessuno**
    
      - **Codec audio**   Questo elenco consente di selezionare il codec audio che sarà utilizzato dal dial plan. Quando un chiamante effettua una chiamata a un utente associato al dial plan e lascia un messaggio vocale, la messaggistica unificata utilizza il codec audio selezionato da questo elenco per registrare i messaggi vocali che verranno inviati agli utenti abilitati alla segreteria telefonica. Di seguito sono riportati i codec audio supportati:
        
          - **MP3** (predefinito)
        
          - **WMA** (Windows Media Audio)
        
          - **G711** (PCM (Pulse Code Modulation) lineare)
        
          - **GSM** (Group System Mobile 06.10)
        
        Per impostazione predefinita è selezionato il formato MP3. Il formato MP3 è un formato comune per i file audio, utilizzato per ridurre notevolmente la dimensione del file audio e impiegato comunemente dai dispositivi audio personali o dai lettori MP3. MP3 è un tipo di codec audio multipiattaforma utilizzato per la compatibilità con numerosi telefoni cellulari, dispositivi e diversi sistemi operativi per computer.
        
        Il codec audio WMA viene utilizzato per la compressione e la qualità elevate. PCM lineare G.711 è un codec audio di qualità telefonica che presenta una compressione inferiore e la qualità minima tra i diversi formati. GSM 06.10 è un formato per codec audio utilizzato dai produttori di telefoni cellulari ed è lo standard per i servizi digitali di telefonia cellulare.
        
        Se è necessario attenersi alle quote disco assegnate agli utenti, selezionare il codec audio WMA. Le dimensioni dei file vocali salvati in formato .wma sono circa la metà di quelle della stessa registrazione vocale effettuata con uno degli altri codec audio.
    
      - **Estensione operatore**   Questa casella di testo consente di specificare il numero di telefono o un numero di interno per l'operatore del dial plan. È diverso da un interno di operatore configurato su un operatore automatico di messaggistica unificata. Tuttavia, è possibile inserire lo stesso numero di telefono o di interno per entrambi i tipi di operatore.
        
        È possibile configurare questa impostazione affinché le chiamate vengano trasferite a un operatore automatico (se configurato), a un operatore, oppure a numeri di telefono esterni o di interno.
        
        Quando un chiamante che utilizza il tastierino numerico del telefono preme il tasto 0 o pronuncia le parole "centralino" o "operatore", oppure supera la soglia **Numero di errori di input prima della disconnessione**, viene trasferito al numero di telefono o di interno specificato in questa casella di testo.
        
        Questo numero di telefono può essere un numero esterno all'organizzazione oppure un numero di interno. Ad esempio, se il numero di interno del centralinista o dell'operatore è 81964 e l'organizzazione dispone di un solo dial plan, immettere 81964.
        
        Per impostazione predefinita, questa impostazione è vuota. Se in questa casella di testo non si specifica alcun numero di telefono, la possibilità di trasferire le chiamate all'operatore è disabilitata e i chiamanti vengono disconnessi perché nessuno può rispondere alla chiamata.
        
        Si consiglia di compilare questa casella di testo con un numero di telefono che trasferisca i chiamanti a un operatore nel caso in cui non riuscissero a individuare l'utente specificato nella directory.
    
      - **Numero di errori di accesso prima della disconnessione**   Questa casella di testo consente di specificare il numero consentito di tentativi di accesso non riusciti consecutivi prima della disconnessione di un chiamante.
        
        Il valore di questa impostazione può essere compreso tra 1 e 20. L'impostazione di un valore troppo basso può causare alcune difficoltà agli utenti. Per la maggior parte delle organizzazioni, l'impostazione predefinita di questo valore dovrebbe essere di tre tentativi.
    
      - **Timeout e tentativi**   Queste impostazioni si applicano agli utenti di Outlook Voice Access e ai chiamanti esterni che chiamano un operatore automatico di messaggistica unificata.
        
          - **Durata massima chiamata (minuti)**   Questa casella di testo consente di specificare il numero massimo di minuti per cui una chiamata in arrivo può rimanere connessa al sistema senza essere trasferita a un numero di interno valido prima che sia terminata. Per la maggior parte delle organizzazioni, l'impostazione predefinita di questo valore dovrebbe essere di 30 minuti.
            
            Questa impostazione si applica a tutti i tipi di chiamate. comprese le chiamate Outlook Voice Access in arrivo, le chiamate vocali interne all'organizzazione e le chiamate vocali e fax esterne all'organizzazione.
            
            Il valore di questa impostazione può essere compreso tra 10 e 120. L'impostazione di un valore troppo basso può causare la disconnessione delle chiamate in ingresso prima del loro completamento. Ad esempio, se l'organizzazione riceve molti messaggi fax di grandi dimensioni, è possibile che si desideri aumentare questo valore rispetto all'impostazione predefinita, così da consentire la ricezione di tutte le pagine dei fax.
        
          - **Durata massima registrazione (minuti)**   Questa casella di testo consente di immettere il numero massimo consentito di minuti per ciascuna registrazione vocale quando un chiamante lascia un messaggio vocale. Per la maggior parte delle organizzazioni, l'impostazione predefinita di questo valore dovrebbe essere di 20 minuti.
            
            Il valore di questa impostazione può essere compreso tra 1 e 100. L'impostazione di un valore troppo basso può causare la disconnessione dei messaggi vocali lunghi prima che il chiamante abbia finito di registrarli. L'impostazione di un valore troppo alto consente agli utenti di salvare messaggi vocali lunghi nelle proprie cartelle Posta in arrivo.
            
            Questa impostazione è importante qualora siano implementate quote disco rigorose per gli utenti. Questo valore deve essere inferiore a quello impostato per **Durata massima chiamata (minuti)**.
        
          - **Timeout di inattività della registrazione (secondi)**   Questa casella di testo consente di specificare il numero di secondi di silenzio consentiti dal sistema quando viene registrato un messaggio vocale prima del termine della chiamata. Per la maggior parte delle organizzazioni, l'impostazione predefinita di questo valore dovrebbe essere di 5 secondi.
            
            Il valore di questa impostazione può essere compreso tra 2 e 10. L'impostazione di un valore troppo basso può causare la disconnessione dei chiamanti da parte del sistema prima che abbiano finito di lasciare i propri messaggi vocali. L'impostazione di un valore troppo alto consente la registrazione di lunghe pause di silenzio nei messaggi vocali.
        
          - **Numero di errori di input prima della disconnessione**   Questa casella di testo consente di specificare il numero di volte per cui un chiamante può immettere scelte di menu non corrette prima che venga disconnesso. Per la maggior parte delle organizzazioni, l'impostazione predefinita di questo valore dovrebbe essere di tre tentativi. È un'impostazione importante per i dial plan di messaggistica unificata abilitati al servizio di sintesi vocale.
            
            Gli esempi di dati non corretti comprendono le richieste da parte di un chiamante di un numero di interno non presente nel sistema, l'impossibilità da parte del sistema di individuare un numero di interno dell'utente per trasferire la chiamata, oppure la selezione di un'opzione di menu non valida da parte del chiamante.
            
            Il valore di questa impostazione può essere compreso tra 1 e 20. L'impostazione di un valore troppo basso può causare la disconnessione prematura del chiamante.
    
      - **Lingua audio**   Utilizzare questo elenco per specificare la lingua predefinita utilizzata dagli utenti di Outlook Voice Access. Questa impostazione non si applica all'impostazione della lingua per un operatore automatico di messaggistica unificata. È possibile impostare per Outlook Voice Access la stessa lingua utilizzata da un operatore automatico di messaggistica unificata oppure una lingua diversa. Quando un utente chiama un utente collegato a un dial plan, questa è la lingua predefinita utilizzata dall'operatore per i messaggi vocali registrati. Le istruzioni del sistema ascoltate dai chiamanti vengono riprodotte nella stessa lingua. La lingua scelta nel dial plan di messaggistica unificata è utilizzata per leggere i messaggi di posta elettronica, i messaggi vocali e gli elementi di calendario, per pronunciare il nome dell'utente se non è stato registrato un messaggio di saluto personale, per trascrivere un messaggio vocale utilizzando la funzionalità Anteprima casella vocale e per consentire il corretto funzionamento del riconoscimento vocale automatico.
        
        Per le distribuzioni locali, l'aggiunta di altre lingue consente ad Outlook Voice Access di utilizzare una lingua diversa da Inglese (Stati Uniti). Ad esempio, se un utente di Outlook Voice Access effettua una chiamata utilizzando un numero di Outlook Voice Access da un telefono fisso, l'utente viene salutato da un messaggio preregistrato in inglese. Anche se lo stesso utente seleziona una lingua diversa, come il francese, in Outlook Web App i menu vengono ancora letti in inglese. Affinché l'utente possa ascoltare i menu dell'operatore preregistrati in francese, è necessario installare il Language Pack appropriato.
        

        > [!NOTE]
        > Per Exchange Online, sono disponibili tutte le lingue.



8.  **Regole di composizione**   Utilizzare questa pagina per specificare le regole di composizione per le chiamate nazionali e internazionali effettuate dagli utenti abilitati alla messaggistica unificata. Ogni voce definita nella regola di composizione determina i tipi di chiamata che possono effettuare gli utenti di un gruppo di regole di composizione specifico. Dopo aver utilizzato la pagina **Regole di composizione** per configurare le regole di composizione, è necessario configurare il dial plan, un criterio cassetta postale o un operatore automatico di messaggistica unificata per l'utilizzo della regola di composizione appropriata. Una volta configurato il criterio cassetta postale di messaggistica unificata per l'utilizzo di un gruppo di regole di composizione, le restrizioni di composizione configurate sono valide per tutti gli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata. Ad esempio, è possibile configurare un gruppo di regole di composizione che non richiede la composizione di un codice di accesso alla linea esterna da parte degli utenti associati al dial plan quando effettuano una chiamata verso un numero di telefono nazionale. È possibile configurare quanto segue:
    
      - **Regole di composizione nazionali**   Utilizzare questa casella di testo per aggiungere, rimuovere o modificare i gruppi di regole di composizione nazionali utilizzati dai criteri cassetta postale di messaggistica unificata. Per creare una regola di composizione, fare clic su ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per modificare una regola di composizione esistente, fare clic su ![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). Per rimuovere una regola di composizione, fare clic su ![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi"). Quando si crea una nuova regola di composizione, aggiungere le seguenti informazioni nella pagina **Nuova regola di composizione**:
        
          - **Dialing rule name**   Utilizzare questa casella di testo per immettere il nome della regola di composizione che si sta creando. È possibile utilizzare lo stesso nome per raccogliere diverse regole in un gruppo e quindi abilitarle o disabilitarle in **Autorizzazione di composizione**. Il nome può contenere fino a 32 caratteri.
        
          - **Formato numero da trasformare (maschera numero)**   Utilizzare questa casella di testo per immettere il formato numero da trasformare prima della composizione, ad esempio 91425xxxxxxx. Se un utente immette un numero che corrisponde al formato, la Messaggistica unificata trasformerà il numero selezionato in un numero composto, prima di effettuare la chiamata. È possibile immettere solo numeri e il carattere jolly "x".
        
          - **Numero composto**   Utilizzare questa casella di testo per immettere il numero che si desidera comporre, mantenendo la corrispondenza allo schema definito in **Formato numero da trasformare (maschera numero)**. Il numero composto è utilizzato per determinare la stringa di composizione effettiva inviata al gateway VoIP o all'IP-PBX. Questo numero può essere diverso dal numero ottenuto dalla messaggistica unificata per la chiamata in uscita. PBX o IP PBX possono tuttavia essere configurati in modo da escludere il prefisso per le chiamate locali e per piani di numerazione vocale privati. I caratteri jolly (*x*) della stringa di composizione vengono sostituiti dalle cifre del numero originale che erano state associate in base alla maschera del numero nella regola di composizione. Un esempio di numero composto valido è 9*xxxxxxx*. Questo campo può contenere solo numeri e il carattere *x*.
        
          - **Commento**   Questa casella di testo consente l'immissione di un commento o di una descrizione per la regola di composizione che si sta aggiungendo o modificando. Per impostazione predefinita, questa casella di testo è vuota.
            

            > [!NOTE]
            > Se si sta eseguendo l'integrazione con Office Communications Server 2007 R2 o Microsoft Lync Server, sarà probabilmente inutile configurare le regole di composizione o i gruppi di regole di composizione nella Messaggistica unificata. Office Communications Server 2007 R2 e Lync Server sono progettati per eseguire il routing delle chiamate e la conversione dei numeri per gli utenti dell'organizzazione, ed eseguono queste operazioni anche quando le chiamate vengono effettuate per conto degli utenti.

    
      - **Regole internazionali**   Utilizzare questa casella di testo per aggiungere, rimuovere o modificare i gruppi di regole di composizione internazionali che vengono utilizzati dai criteri cassetta postale di messaggistica unificata.
        
          - **Dialing rule name**   Utilizzare questa casella di testo per immettere il nome della regola di composizione che si sta creando. È possibile utilizzare lo stesso nome per raccogliere diverse regole in un gruppo e quindi abilitarle o disabilitarle in **Autorizzazione di composizione**. Il nome può contenere fino a 32 caratteri.
        
          - **Formato numero da trasformare (maschera numero)**   Utilizzare questa casella di testo per immettere il formato numero da trasformare prima della composizione, ad esempio 91425xxxxxxx. Se un utente immette un numero che corrisponde al formato, la Messaggistica unificata trasformerà il numero selezionato in un numero composto, prima di effettuare la chiamata. È possibile immettere solo numeri e il carattere jolly "x".
        
          - **Numero composto**   Utilizzare questa casella di testo per immettere il numero che si desidera comporre, mantenendo la corrispondenza allo schema definito in **Formato numero da trasformare (maschera numero)**. Il numero composto è utilizzato per determinare la stringa di composizione effettiva inviata al gateway VoIP o all'IP-PBX. Questo numero può essere diverso dal numero ottenuto dalla messaggistica unificata per la chiamata in uscita. PBX o IP PBX possono tuttavia essere configurati in modo da escludere il prefisso per le chiamate locali e per piani di numerazione vocale privati. I caratteri jolly (*x*) della stringa di composizione vengono sostituiti dalle cifre del numero originale che erano state associate in base alla maschera del numero nella regola di composizione. Un esempio di numero composto valido è 9*xxxxxxx*. Questo campo può contenere solo numeri e il carattere *x*.
        
          - **Commento**   Questa casella di testo consente l'immissione di un commento o di una descrizione per la regola di composizione che si sta aggiungendo o modificando. Per impostazione predefinita, questa casella di testo è vuota.
            

            > [!NOTE]
            > Per le distribuzioni locali, se si sta eseguendo l'integrazione con Office Communications Server 2007 R2 o Microsoft Lync Server, sarà probabilmente inutile configurare le regole di composizione o i gruppi di regole di composizione nella messaggistica unificata. Office Communications Server 2007 R2 e Lync Server sono progettati per eseguire il routing delle chiamate e la conversione dei numeri per gli utenti dell'organizzazione, ed eseguono queste operazioni anche quando le chiamate vengono effettuate per conto degli utenti.



9.  **Autorizzazione di composizione**   Utilizzare questa pagina per selezionare le regole di composizione per i chiamanti che contattano un numero Outlook Voice Access configurato in un dial plan di messaggistica unificata. Configurando i gruppi di regole di composizione e le restrizioni di composizione è possibile limitare il tipo di chiamate effettuate dai chiamanti quando un utente non autenticato o un utente di Outlook Voice Access chiama il numero di Outlook Voice Access configurato in un dial plan. È possibile configurare quanto segue:
    
      - **Consenti chiamate nello stesso dial plan di messaggistica unificata**   Selezionare questa casella di controllo per consentire agli utenti che chiamano il numero di Outlook Voice Access configurato in un dial plan di effettuare o trasferire le chiamate a un numero di interno associato a un utente abilitato alla messaggistica unificata incluso nello stesso dial plan. Questa impostazione è abilitata per impostazione predefinita.
        
        Se si disabilita questa impostazione, gli utenti che chiamano il numero di Outlook Voice Access non potranno effettuare o trasferire chiamate verso utenti che non sono abilitati alla messaggistica unificata, verso altri numeri di interno oppure verso utenti abilitati alla messaggistica unificata che sono associati allo stesso dial plan. È dovuto al fatto che, per impostazione predefinita, l'impostazione **Consenti chiamate a qualsiasi interno** è disabilitata.
    
      - **Consenti chiamate a qualsiasi interno**   Se questa impostazione è disabilitata, gli utenti che chiamano il numero di Outlook Voice Access nel dial plan non potranno effettuare chiamate verso utenti che non sono abilitati alla messaggistica unificata o verso altri numeri di interno non associati a un utente abilitato alla messaggistica unificata. Tuttavia, tali utenti possono effettuare una chiamata o trasferire chiamate a numeri di interno associati a utenti abilitati alla messaggistica unificata. Tale condizione si verifica perché l'impostazione **Chiamate nello stesso dial plan di messaggistica unificata** è abilitata per impostazione predefinita. Per impostazione predefinita, l'impostazione **Consenti chiamate a qualsiasi interno** è disabilitata.
        
        Se questa impostazione è disabilitata, gli utenti che chiamano un numero di Outlook Voice Access configurato nel dial plan potranno effettuare chiamate verso utenti che non sono abilitati alla messaggistica unificata, verso altri numeri di interno non associati a un utente abilitato alla messaggistica unificata e verso utenti abilitati alla messaggistica unificata. Tale condizione si verifica perché l'impostazione **Chiamate nello stesso dial plan di messaggistica unificata** è abilitata per impostazione predefinita.
        
        È possibile abilitare questa impostazione in un ambiente in cui non tutti gli utenti sono stati abilitati alla messaggistica unificata. Questa impostazione si rivela utile anche quando si desidera consentire agli utenti che chiamano il numero di Outlook Voice Access configurato in un dial plan di effettuare chiamate a numeri di interno non associati.
    
      - **Gruppi di regole di composizione nazionali consentiti**   Utilizzare questa sezione per aggiungere o rimuovere le regole di composizione nazionali consentite. Per impostazione predefinita, non vi sono regole di composizione nazionali configurate nei dial plan di messaggistica unificata.
        
        I gruppi di regole di composizione nazionali vengono utilizzati per consentire o limitare i numeri di telefono nazionali che possono essere composti da qualsiasi utente che ha composto il numero di accesso del sottoscrittore. Questo consente di evitare che vengano effettuate chiamate telefoniche non necessarie o non autorizzate o che vengano addebitati costi relativi a tali chiamate.
        
        Per aggiungere regole di composizione nazionali, è necessario per prima cosa creare le regole di composizione nazionali corrette nel dial plan e in seguito aggiungere le voci delle regole di composizione appropriate nelle regole di composizione. Dopo aver creato le regole di composizione richieste nel dial plan, è necessario aggiungerle all'elenco delle autorizzazioni di composizione nella pagina **Autorizzazione di composizione** nel dial plan.
        
        I gruppi di regole di composizione nazionali possono essere utilizzati per consentire o limitare l'accesso ai numeri di telefono nazionali. Questa impostazione viene applicata agli utenti che hanno chiamato un numero di Outlook Voice Access.
    
      - **Gruppi di regole di composizione internazionali consentiti**   Utilizzare questa sezione per aggiungere o rimuovere le regole di composizione internazionali consentite. Per impostazione predefinita, non vi sono regole di composizione internazionali configurate nei dial plan di messaggistica unificata.
        
        Le regole di composizione internazionali vengono utilizzate per consentire o limitare i numeri di telefono internazionali che possono essere composti da qualsiasi utente che ha composto il numero di Outlook Voice Access. Questo consente di evitare che vengano effettuate chiamate telefoniche non necessarie o non autorizzate o che vengano addebitati costi relativi a tali chiamate.
        
        Per aggiungere gruppi di regole di composizione internazionali, è necessario per prima cosa creare le regole di composizione internazionali corretti nel dial plan e in seguito aggiungere le voci delle regole di composizione appropriate. Dopo aver creato le regole di composizione richieste nel dial plan, è necessario aggiungerle all'elenco delle autorizzazioni di composizione nella pagina **Autorizzazione di composizione** nel dial plan.
        
        I gruppi di regole di composizione internazionali possono essere utilizzati per consentire o limitare l'accesso ai numeri di telefono internazionali. Questa impostazione viene applicata agli utenti che hanno chiamato un numero di Outlook Voice Access.

10. **Trasferisci e cerca**   Utilizzare questa pagina per configurare le funzionalità del dial plan di messaggistica unificata. È possibile configurare diverse funzionalità sul dial plan di messaggistica unificata. Sono incluse il trasferimento delle chiamate, l'invio di messaggi vocali e la ricerca degli utenti. È possibile configurare quanto segue:
    
      - **Consenti ai chiamanti**   Utilizzare queste impostazioni per determinare in che modo gli utenti che chiamano un numero di Outlook Voice Access possono contattare gli utenti. È possibile configurare quanto segue:
        
          - **Consenti ai chiamanti il trasferimento agli utenti**   Selezionare questa casella di controllo per consentire agli utenti di Outlook Voice Access di trasferire le chiamate agli utenti. Per impostazione predefinita, questa opzione è selezionata. Consente agli utenti associati al dial plan di trasferire le chiamate agli utenti nello stesso dial plan di messaggistica unificata. Dopo aver selezionato questa casella di controllo, è possibile impostare il gruppo di utenti che possono essere cercati dai chiamanti selezionando l'opzione appropriata nella sezione **Consenti a chiamanti di cercare gli utenti in base al nome o all'alias** in questa pagina.
            
            Se questa opzione viene disabilitata, Outlook Voice Access non consentirà ai chiamanti di essere trasferiti agli utenti nel dial plan.
        
          - **Consenti ai chiamanti di lasciare messaggi vocali senza far squillare il telefono dell'utente**   Selezionare questa casella di controllo per consentire ai chiamanti di inviare messaggi vocali agli utenti. Per impostazione predefinita, questa opzione è selezionata. Consente agli utenti di Outlook Voice Access associati al dial plan di inviare messaggi vocali agli utenti nello stesso dial plan di messaggistica unificata. Dopo aver selezionato questa casella di controllo, è possibile impostare il gruppo di utenti che possono essere cercati dai chiamanti selezionando l'opzione appropriata nella sezione **Consenti a chiamanti di cercare gli utenti in base al nome o all'alias** in questa pagina.
            
            Se questa opzione viene disabilitata, Outlook Voice Access non inviterà i chiamanti a inviare un messaggio vocale in un menu vocale del sistema.
    
      - **Consenti a chiamanti di cercare gli utenti in base al nome o all'alias**   Utilizzare queste opzioni per determinare il gruppo di utenti da includere nelle ricerche. L'opzione **Solo in questo dial pla** è selezionata per impostazione predefinita. Tuttavia, è possibile modificare il raggruppamento degli utenti. Scegliere una delle seguenti opzioni:
        
          - **Solo in questo dial plan**   Utilizzare questa opzione per consentire ai chiamanti che si collegano ad Outlook Voice Access di individuare e contattare gli utenti all'interno del dial plan di cui sono membri.
        
          - **Nell'intera organizzazione**   Utilizzare questa opzione per consentire ai chiamanti che si collegano ad Outlook Voice Access di individuare e contattare gli utenti di tutta l'organizzazione. Sono inclusi gli utenti abilitati alle cassette postali o alla messaggistica unificata in tutti i dial plan.
        
          - **Solo questo operatore automatico**   Utilizzare questo elenco per consentire agli utenti di Outlook Voice Access di collegarsi a un operatore automatico di messaggistica unificata e quindi di collegarsi a un altro operatore automatico configurato. È necessario creare questo operatore automatico per consentire ai chiamanti di trasferire la chiamata a un altro operatore automatico specificato.
        
          - **Solo questo interno**   Utilizzare questa opzione per consentire agli utenti di Outlook Voice Access di collegarsi al numero di interno specificato nel campo previsto per questa opzione. In questo campo è possibile immettere solo cifre numeriche. Il numero di cifre definito in questo campo deve corrispondere al numero di cifre configurato sul dial plan associato all'operatore automatico.
    
      - **Informazioni da includere per gli utenti con lo stesso nome**   Utilizzare questo campo per indicare in che modo il dial plan distingue gli utenti con lo stesso nome o nomi simili. Quando a un chiamante viene chiesto di immettere alcune lettere o di pronunciare un nome per trovare un utente specifico nell'organizzazione, più nomi corrispondono a tale immissione. Se esistono due utenti con lo stesso nome, la messaggistica unificata utilizzerà uno dei seguenti metodi per aggiungere ulteriori informazioni al nome dell'utente. Ad esempio, se si seleziona **Reparto**, quando un utente di Outlook Voice Access chiama Outlook Voice Access e cerca un utente, ma vi sono nomi duplicati o simili nella directory, il chiamante udirà il nome dell'utente e il reparto, ad esempio:
        
        1.  Sistema: \&quot;Benvenuti in Outlook Voice Access. Immettere il proprio PIN e premere cancelletto."
        
        2.  Il chiamante immette il suo PIN seguito dal tasto \#.
        
        3.  Sistema: "Specificare segreteria telefonica, posta elettronica, calendario, contatti personali, directory oppure opzioni personali."
        
        4.  Chiamante: \&quot;Directory\&quot;
        
        5.  Sistema: "Ricerca nella directory. Per le seguenti attività il sistema richiede di utilizzare la tastiera del telefono, anziché la voce. Utilizzare la tastiera per immettere il nome della persona da trovare, specificando prima il cognome, oppure per immettere la prima parte del suo indirizzo di posta elettronica; premere due volte il tasto cancelletto, se si conosce l'interno, quindi premere il tasto cancelletto."
        
        6.  Il chiamante utilizza il tastierino numerico per immettere "smithtony" e preme il tasto \#.
        
        7.  Sistema: "Per Tony Smith, ricerca, premere 1. Per Tony Smith, amministrazione, premere 2. Per Tony Smith, supporto tecnico, premere 3."
        
        8.  Il chiamante preme il tasto appropriato sul tastierino numerico e la chiamata viene trasferita all'utente.
        
        Per impostazione predefinita, tutti gli operatori automatici di messaggistica unificata associati a questo dial plan ereditano questa impostazione. Tuttavia, è possibile modificare questa impostazione su ciascun operatore automatico di messaggistica unificata creato.
        
        Selezionare uno dei seguenti metodi che forniscono al chiamante ulteriori informazioni per aiutarlo a scegliere l'utente corretto nell'organizzazione:
        
          - **Nessuno**   Non vengono fornite informazioni aggiuntive in caso di corrispondenza. Per impostazione predefinita, è selezionato questo metodo.
        
          - **Posizione professionale**   Il sistema di segreteria telefonica include la posizione professionale di ciascun utente in caso di corrispondenza.
        
          - **Reparto**   Il sistema di segreteria telefonica include il reparto di ciascun utente in caso di corrispondenza.
        
          - **Posizione**   Il sistema di segreteria telefonica include la posizione di ciascun utente in caso di corrispondenza.
        
          - **Prompt per l'alias**   Il sistema di segreteria telefonica richiede al chiamante l'alias dell'utente.

11. Una volta configurate le impostazioni richieste, fare clic su **Salva** per salvare le modifiche.

## Utilizzare Shell per configurare le impostazioni del dial plan di messaggistica unificata

In questo esempio viene configurato un dial plan di messaggistica unificata denominato `MyDialPlan` che utilizza il valore 9 per il codice di accesso alla linea esterna.

    Set-UMDialplan -Identity MyDialPlan -OutsideLineAccessCode 9

In questo esempio viene configurato un dial plan di messaggistica unificata denominato `MyDialPlan` per l'utilizzo di un messaggio di benvenuto.

    Set-UMDialplan -Identity MyDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename welcome.wav

In questo esempio viene configurato un dial plan di messaggistica unificata denominato `MyDialPlan` con regole di composizione.

    $csv=import-csv "C:\MyInCountryGroups.csv"
    Set-UMDialPlan -Identity MyDialPlan -ConfiguredInCountryGroups $csv
    Set-UMDialPlan -Identity MyDialPlan -AllowedInCountryGroups "local, long distance"

## Utilizzare Shell per visualizzare le impostazioni del dial plan di messaggistica unificata

In questo esempio viene visualizzato un elenco di tutti i dial plan di messaggistica unificata.

    Get-UMDialplan

In questo esempio viene visualizzato un elenco formattato di tutte le impostazioni nel dial plan di messaggistica unificata `MyUMDialPlan`.

    Get-UMDialplan -Identity MyUMDialPlan | Format-List


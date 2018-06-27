---
title: 'Gestire un operatore automatico di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Gestire un operatore automatico di messaggistica unificata
ms:assetid: 4809ff56-ae34-4ce6-8e39-9193311c3f83
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997867(v=EXCHG.150)
ms:contentKeyID: 50480576
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.AutoAttendantGeneralPropertyPage
ms.translationtype: MT
---

# Gestire un operatore automatico di messaggistica unificata

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-04-30_

Dopo aver creato un operatore automatico di messaggistica unificata, è possibile visualizzare o configurare diverse impostazioni. Ad esempio, è possibile aggiungere, rimuovere e modificare i numeri degli interni associati all'operatore automatico. Inoltre, è possibile abilitare o disabilitare il riconoscimento vocale automatico per l'operatore automatico e modificare i messaggi di saluto utilizzati per l'orario di ufficio e non di ufficio.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Visualizzazione o configurazione delle impostazioni dell'operatore automatico di messaggistica unificata tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Operatore automatico di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata che si desidera visualizzare o configurare, quindi fare clic su **Modifica** sulla barra degli strumenti ![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  
    
    Nella pagina **Operatore automatico di messaggistica unificata**, fare clic su **Generale** per visualizzare le informazioni di sola visualizzazione sull'operatore automatico di messaggistica unificata e per eseguire attività di gestione su un operatore automatico di messaggistica unificata nel seguente modo:
    
      - **Dial plan di messaggistica unificata**°°°In questa casella viene visualizzato il dial plan di messaggistica unificata associato all'operatore automatico. Una volta creato un operatore automatico, il dial plan associato all'operatore automatico non può essere modificato. Se si desidera associare un operatore automatico a un diverso dial plan, è necessario eliminare il dial plan e associare l'operatore automatico al dial plan corretto dopo averlo creato nuovamente.
    
      - **Nome**   Questa casella mostra il nome che è stato assegnato all'operatore automatico al momento della creazione. Questo è il nome che apparirà nell'interfaccia di amministrazione di Exchange.
    
      - **Stato**°°°Questa casella indica se l'operatore automatico di messaggistica unificata è abilitato o disabilitato. Per abilitare o disabilitare l'operatore automatico, chiudere la pagina **Operatore automatico di messaggistica unificata** e utilizzare la barra degli strumenti sotto **Operatori automatici di messaggistica unificata** nella pagina **Dial plan di messaggistica unificata**.
    
      - **Numeri di accesso°°°**Utilizzare questa casella per immettere il numero dell'interno o di accesso che attiva l'operatore automatico. Per impostazione predefinita, quando si crea un operatore automatico non viene configurato nessun numero dell'interno o di accesso.
        
        Il numero di cifre dei numeri di interno o dei numeri di accesso forniti deve corrispondere al numero di cifre per un numero di interno configurato nel dial plan di messaggistica unificata associato all'operatore automatico di messaggistica unificata. È anche possibile aggiungere un indirizzo SIP (Session Initiation Protocol) a questa casella. Un indirizzo SIP viene utilizzato da alcuni PBX (IP Private Branch eXchange), da PBX abilitati all'indirizzo SIP e Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server.
        
        È possibile creare il nuovo operatore automatico senza elencare un numero di interno o un numero di accesso. Per aggiungere un interno, digitare il numero in questa casella e fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). È possibile associare più numeri a un solo operatore automatico. È possibile anche modificare o rimuovere un numero di accesso esistente. Per modificare un numero esistente, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). Per rimuovere un numero di interno esistente dall'elenco, selezionarlo e fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").
    
      - **Imposta operatore automatico per rispondere ai comandi vocali**   Selezionare questa casella di controllo per abilitare gli utenti a rispondere verbalmente alle richieste dell'operatore automatico per accedere al sistema del menu. Per impostazione predefinita, un operatore automatico creato non è abilitato al servizio di sintesi vocale.
        
        Se si decide di creare l'operatore automatico di messaggistica unificata ma non di abilitarlo alla sintesi vocale, è possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell per abilitarlo alla sintesi vocale dopo la creazione.
    
      - **Utilizzare questo operatore automatico quando i comandi vocali non funzionano correttamente**   Fare clic su **Sfoglia** per selezionare l'operatore automatico che si desidera utilizzare nel caso in cui i comandi vocali non dovessero funzionare. Quest'ultimo operatore viene anche denominato Operatore automatico per il fallback del segnale multifrequenza (DTMF). Un operatore automatico per il fallback del segnale multifrequenza (DTMF) può essere utilizzato solo se è selezionata l'opzione **Imposta l'operatore automatico in modo che risponda ai comandi vocali**. È necessario prima creare un operatore automatico per il fallback del segnale multifrequenza (DTMF), quindi fare clic su **Sfoglia** per individuare l'operatore automatico DTMF appropriato.
        
        Un operatore automatico per il fallback del segnale multifrequenza (DTMF) viene utilizzato quando un operatore automatico abilitato al servizio di sintesi vocale di messaggistica unificata non è in grado di comprendere o riconoscere gli input vocali del chiamante. Se viene utilizzato l'operatore automatico DTMF, il chiamante deve utilizzare gli input DTMF per spostarsi nel sistema di menu, indicare un nome utente lettera per lettera o utilizzare un prompt menu personalizzato. Un chiamante non potrà utilizzare i comandi vocali per spostarsi in questo operatore automatico.
        
        Se non viene configurato un operatore automatico per il fallback del segnale multifrequenza (DTMF), si consiglia di configurare un numero di interno dell'operatore sull'operatore automatico. Se non viene configurato un numero di interno dell'operatore, quando i chiamanti utilizzano un operatore automatico abilitato al servizio di sintesi vocale e il sistema non riconosce gli input vocali, non potranno spostarsi nel sistema o essere trasferiti a un operatore per assistenza.
        
        Anche se non è obbligatorio, si consiglia di configurare un operatore automatico per il fallback del segnale multifrequenza (DTMF) nello stesso modo in cui viene configurato l'operatore automatico abilitato al servizio di sintesi vocale. L'operatore automatico per il fallback del segnale multifrequenza DTMF non dovrebbe essere abilitato alla sintesi vocale.
    
      - **Lingua per interfaccia vocale automatica**°°°Utilizzare questo elenco per selezionare la lingua che i chiamanti sentono quando sono messi in comunicazione con l'operatore automatico. La lingua predefinita viene determinata al momento dell'installazione di Microsoft Exchange. Per impostazione predefinita, per le distribuzioni ibride locali, viene utilizzato l'inglese americano perché l'operatore automatico utilizza l'impostazione della lingua sul dial plan di messaggistica unificata. Per disporre di altre opzioni di lingua, è necessario installare Language Pack di messaggistica unificata per le lingue da includere. Per ulteriori informazioni su come installare un Language Pack di messaggistica unificata, vedere [Installare un Language Pack di messaggistica unificata](install-a-um-language-pack-exchange-2013-help.md). Per la messaggistica unificata in Office 365, non è necessario installare language pack aggiuntivi.
        
        Sebbene sia possibile selezionare una lingua diversa dalla lingua selezionata sul dial plan di messaggistica unificata associato all'operatore automatico, si consiglia di far corrispondere le impostazioni della lingua sul dial plan con quelle dell'operatore automatico. Se le impostazioni della lingua non corrispondono, quando qualcuno chiama un numero di interno definito sul dial plan, riceverà prompt in una data lingua e, quando chiamerà un numero di interno collegato a un operatore automatico, riceverà prompt in un'altra lingua.
    
      - **Ragione sociale   **Utilizzare questa casella per immettere la ragione sociale. Per impostazione predefinita non è immessa nessuna ragione sociale. Se viene immessa una ragione sociale in questa casella, ai chiamanti verrà riprodotto un prompt con la ragione sociale, invece del messaggio di saluto predefinito.
    
      - **Sede aziendale   **Utilizzare questa casella per immettere la sede aziendale. Per impostazione predefinita non è immessa alcuna sede aziendale. Se viene immessa la sede aziendale in questa casella, ai chiamanti verrà riprodotta la sede aziendale.

4.  
    
    Utilizzo di **Messaggi di saluto** sull'operatore automatico per gestire i saluti registrati. È possibile selezionare i messaggi di saluto predefiniti o i messaggi di saluto personalizzati registrati in precedenza per l'orario di ufficio e non di ufficio. È possibile configurare quanto segue:
    
      - **Messaggio di saluto Orario di ufficio**°°°Si tratta del messaggio di saluto iniziale riprodotto quando qualcuno chiama l'operatore automatico nell'orario di ufficio dell'organizzazione. Per impostazione predefinita, gli orari d'ufficio sono dalle 12:00 alle 12:00 e non sono impostati orari non di ufficio. Se non si specifica un messaggio di saluti personalizzato, quando qualcuno chiama viene riprodotta un'istruzione di sistema che dice, "Benvenuti nell'operatore automatico di Exchange". Gli orari di ufficio e non di ufficio vengono configurati in **Orario di ufficio**°dell'operatore automatico.
        
        È anche possibile personalizzare questo messaggio di saluto in modo che rappresenti l'azienda; ad esempio: "Grazie per aver chiamato la Woodgrove Bank." È possibile configurare un messaggio di saluto personalizzato per l'orario di ufficio facendo clic su **Modifica** per selezionare un file con un messaggio di saluto personalizzato registrato in precedenza. Il messaggio di saluto personalizzato deve essere stato registrato in precedenza in un file con estensione wav o wma.
    
      - **Messaggio di saluto Orario non di ufficio**°°°Si tratta del messaggio di saluto iniziale riprodotto quando qualcuno chiama l'operatore automatico nell'orario non di ufficio dell'organizzazione. Per impostazione predefinita, l'orario non di ufficio non è configurato. Pertanto, non esiste nessun messaggio di saluto predefinito per l'orario non di ufficio. È possibile configurare l'orario di ufficio e non di ufficio in **Orario di ufficio** dell'operatore automatico.
        
        È anche possibile personalizzare questo messaggio di saluto in modo che rappresenti l'azienda; ad esempio: "Grazie per aver chiamato la Woodgrove Bank, ma in questo momento siamo chiusi." oppure \&quot;Gli uffici Contoso, Ltd. sono chiusi. Il nostro orario di ufficio va dalle ore°8 alle ore°17, dal lunedì al venerdì." È possibile configurare un messaggio di saluto personalizzato per l'orario non di ufficio facendo clic su **Modifica** per selezionare un file con un messaggio di saluto personalizzato registrato in precedenza. Il messaggio di saluto personalizzato deve essere stato registrato in precedenza in un file con estensione wav o wma.
    
      - **Messaggio informativo**   Quando è abilitata, questa registrazione facoltativa viene riprodotta subito dopo il messaggio di saluto Orario non di ufficio o Orario di ufficio. Il messaggio informativo potrebbe indicare l'orario lavorativo settimanale dell'organizzazione, ad esempio: "Il nostro orario di ufficio va dalle 8,30 alle 17,30, dal lunedì al venerdì e dalle 8,30 alle 13 il sabato." L'annuncio informativo può anche fornire informazioni richieste per la conformità con i criteri dell'azienda; ad esempio: "È possibile che le chiamate siano monitorate a scopo formativo." Se è importante che i chiamanti ascoltino l'intero messaggio informativo, può essere impostato come continuo richiedendo alla persona che chiama di ascoltare l'intero annuncio.
        
        Per impostazione predefinita, negli operatori automatici o nei dial plan di messaggistica unificata non è configurato alcun messaggio informativo. Se si abilita un annuncio informativo e si utilizza un file audio personalizzato specifico dell'organizzazione, l'opzione **Consenti interruzione annuncio** diventerà disponibile. È necessario che i messaggi siano già stati registrati come file .wav o .wma. Fare clic su **Modifica** per individuare il file di annuncio informativo personalizzato registrato in precedenza.
        
        **Consenti interruzione annuncio**   Selezionare questa casella di controllo per abilitare il chiamante a interrompere l'annuncio informativo. È necessario abilitare questa opzione per riprodurre annunci informativi lunghi. I chiamanti potrebbero spazientirsi se il messaggio informativo è lungo e se non possono interromperlo per accedere alle opzioni fornite dall'operatore automatico.

5.  Utilizzo di **Orario di ufficio** per determinare gli orari di apertura dell'organizzazione. Durante l'orario di ufficio, se in **Spostamento nei menu** sono state configurate le associazioni di tasti appropriate per l'orario di ufficio, i chiamanti ascoltano il messaggio di saluto predefinito o un messaggio di saluto personalizzato e il prompt del menu principale per l'orario di ufficio. È possibile configurare quanto segue:
    
      - **Fuso orario**°°°Utilizzare questo elenco per selezionare il fuso orario. Quando viene impostata la pianificazione, verificare se il dial plan associato all'operatore automatico copre più di un fuso orario.
        
        Per impostazione predefinita, per le distribuzioni ibride, il fuso orario viene configurato utilizzando l'ora del server locale impostata quando è stato installato il server Cassette postali su cui è in esecuzione il servizio di messaggistica unificata di Exchange.
    
      - **Orario di ufficio**   Fare clic su **Configura orario di ufficio**, quindi sulla pagina **Configura orario di ufficio**, utilizzare la griglia per configurare l'orario di ufficio dell'organizzazione.
    
      - **Pianificazione festività**°°°Utilizzare questa opzione per definire i giorni, dalle ore 00:00 alle ore 23:59, nei quali l'organizzazione sarà chiusa per le festività. I chiamanti, che raggiungono l'operatore automatico negli orari specificati nella pagina **Nuova festività**, ascoltano il file audio di un messaggio di saluto personalizzato per le festività definito dall'utente. Quando si configura la pianificazione della festività, è necessario definire il nome della festività, il file audio per il messaggio di saluto per le festività registrato e la **Data di inizio** e la **Data di fine**. È necessario che i messaggi di saluto siano già stati registrati come file .wav o .wma.

6.  Utilizzo di **Spostamento nei menu** per specificare le opzioni di menu proposte ai chiamanti durante l'orario di ufficio e non. Se si desidera abilitare lo spostamento nei menu è necessario farlo separatamente per l'orario di ufficio e l'orario non di ufficio. Ad esempio, se si desidera abilitare gli spostamenti nell'orario di ufficio, è necessario aggiungere una registrazione audio personalizzata del prompt del menu, selezionare la casella di controllo **Abilita spostamento nei menu in orario di ufficio**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), quindi impostare le opzioni nella pagina **Nuova voce di spostamento nei menu**.
    
      - **Spostamento nei menu in orario di ufficio**   Questo è l'elenco delle opzioni che i chiamanti ascoltano durante l'orario di ufficio definito nella pagina **Orario di ufficio**. Ad esempio, "Per il supporto tecnico, premere o dire 1. Per gli uffici e l'amministrazione, premere o dire 2. Per l'ufficio vendite, premere o dire 3."
        
        Per abilitare lo spostamento nei menu in orario di ufficio, fare quanto segue:
        
        1.  **Prompt menu**   Utilizzare questa opzione per specificare un file audio per i prompt di menu personalizzati. Per utilizzare un prompt del menu per l'orario di ufficio personalizzato o registrato precedentemente, fare clic su **Modifica**, quindi fare clic su **Sfoglia** per individuare la registrazione del prompt del menu.
        
        2.  **Abilita spostamento nei menu in orario di ufficio**°°°Utilizzare questa casella di controllo per abilitare le opzioni per lo spostamento nei menu da utilizzare durante l'orario di ufficio. Quando viene abilitato lo spostamento nei menu in orario di ufficio, è possibile aggiungere nuove voci dello spostamento nei menu per l'orario di ufficio.
        
        3.  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per creare una nuova voce di spostamento nei menu. Nella pagina **Nuova voce di spostamento nei menu** utilizzare le opzioni seguenti per creare una nuova voce di spostamento nei menu:
            
              - **Prompt** Utilizzare questa casella per digitare il nome del nuovo menu di navigazione. Il nome del menu di navigazione viene utilizzato solo per la visualizzazione. Questo campo è obbligatorio.
                
                Dal momento che si può scegliere di specificare più menu di navigazione, si consiglia di utilizzare nomi significativi per i mapping dei tasti. La lunghezza massima del nome di un'associazione di tasti è di 64 caratteri e sono ammessi gli spazi, Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
            
              - **Quando si preme questo tasto**   Utilizzare questo elenco per abilitare il mapping dei tasti. L'associazione di tasti è il tasto numerico che il chiamante preme affinché l'operatore automatico esegua un'operazione specifica, ad esempio, l'inoltro della chiamata a un altro operatore automatico o a un operatore. Per impostazione predefinita, non viene definita nessuna voce.
                
                Utilizzare l'elenco a discesa per selezionare il tasto numerico (da 1 a 9) che il chiamante deve premere. Il numero 0 (zero) è riservato all'operatore automatico.
                
                Se si seleziona **Timeout** dall'elenco a discesa, si abilita il trasferimento della chiamata a un interno o a un altro operatore automatico nel caso in cui il chiamante non prema nessun tasto sul tastierino del telefono. (ad esempio, "Resti in linea. La sua chiamata verrà trasferita al primo operatore disponibile.") L'impostazione predefinita è 5 secondi. Se si abilita questa opzione, viene creata un'associazione di tasti vuota.
            
              - **Riproduci il seguente file audio**   Utilizzare questa opzione per selezionare un file audio registrato in precedenza per i chiamanti. Fare clic su **Cambia**, quindi fare clic su **Sfoglia** per individuare il file audio. Se non si modifica l'impostazione predefinita \<Nessuno\> per il file audio, il modulo di sintesi vocale (TTS) del server di messaggistica unificata sintetizzerà il prompt del menu principale per l'orario di ufficio. In alternativa, è possibile creare un file audio personalizzato da utilizzare per il prompt del menu principale per l'orario di ufficio per un operatore automatico abilitato al riconoscimento vocale. Ad esempio, si potrebbe utilizzare il messaggio: "Per lasciare un messaggio vocale per il reparto vendite, dica 1. Per lasciare un messaggio vocale per il supporto tecnico, dica 2. Per lasciare un messaggio vocale per il reparto amministrazione, dica 3."
            
              - **Esegui questa ulteriore azione**   Selezionare una delle seguenti opzioni per definire l'azione che si desidera che l'operatore automatico esegua per il chiamante:
                
                  - **Nessuno**   Utilizzare questa opzione se non si desidera che l'operatore automatico trasferisca la chiamata a un interno o a un altro operatore automatico oppure per lasciare un messaggio per un utente.
                
                  - **Trasferisci a questo numero di interno**   Selezionare questa opzione per abilitare le chiamate da trasferire a un numero di interno. Se si abilita questa opzione, utilizzare la casella per digitare il numero di interno a cui trasferire la chiamata. In questo campo è possibile inserire solo caratteri numerici. Non sono ammessi i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
                
                  - **Trasferisci a questo operatore automatico di messaggistica unificata**   Selezionare questa opzione per trasferire la chiamata a un operatore automatico. Fare clic su **Sfoglia** per individuare l'operatore automatico che si desidera utilizzare. Prima di abilitare questa opzione, è necessario creare e configurare l'operatore automatico. Questa opzione viene utilizzata quando si crea una struttura padre/figlio di operatori automatici di messaggistica unificata.
                
                  - **Lascia un messaggio vocale per questo utente**   Selezionare questa opzione per abilitare un chiamante a lasciare un messaggio vocale per un utente sullo stesso dial plan dell'operatore automatico di messaggistica unificata che si sta configurando. Quando un chiamante sceglie questa opzione dal menu di un operatore automatico, gli verrà richiesto di lasciare un messaggio vocale per l'utente selezionato. Fare clic su **Sfoglia** per individuare l'utente abilitato alla messaggistica unificata.
                
                  - **Notifica sede aziendale**   Selezionare questa opzione per abilitare un chiamante a scegliere un'opzione del menu dell'operatore automatico e ascoltare le informazioni sulla sede aziendale che è configurata sull'operatore automatico di messaggistica unificata. Per abilitare correttamente l'opzione, è necessario prima inserire la sede aziendale nella casella **Sede aziendale** nella pagina **Generale** dell'operatore automatico di messaggistica unificata.
                
                  - **Notifica orario di ufficio**  Selezionare questa opzione per abilitare un chiamante a scegliere un'opzione del menu dell'operatore automatico e ascoltare le informazioni sull'orario di ufficio dell'azienda configurato sull'operatore automatico di messaggistica unificata. Per abilitare correttamente l'opzione, è necessario prima configurare l'orario di ufficio nella pagina **Orario di ufficio** dell'operatore automatico di messaggistica unificata.
    
      - **Spostamento nei menu non in orario di ufficio**   Questo è l'elenco delle opzioni che i chiamanti ascoltano nell'orario non di ufficio definito nella pagina **Orario di ufficio**. Ad esempio: "La sua chiamata è molto importante per noi. Tuttavia, in questo momento gli uffici della Woodgrove Bank sono chiusi. Se desidera lasciare un messaggio, prema o dica 1 e risponderemo alla sua chiamata il più presto possibile."
        
        Per abilitare lo spostamento nei menu non in orario di ufficio, fare quanto segue:
        
        1.  **Prompt menu**   Utilizzare questa opzione per specificare un file audio per i prompt di menu personalizzati. Per utilizzare un prompt di menu dell'orario non di ufficio personalizzato o registrato precedentemente, fare clic su **Sfoglia**.
        
        2.  **Abilita spostamento nei menu non in orario di ufficio**°°°Utilizzare questa casella di controllo per abilitare le opzioni per lo spostamento nei menu da utilizzare al di fuori dell'orario di ufficio. Quando viene abilitato lo spostamento nei menu non in orario di ufficio, è possibile aggiungere nuove voci dello spostamento nei menu non in orario di ufficio.
        
        3.  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per creare una nuova voce di spostamento nei menu. Nella pagina **Nuova voce di spostamento nei menu** utilizzare le opzioni seguenti per creare una nuova voce di spostamento nei menu:
            
              - **Prompt** Utilizzare questa casella per digitare il nome del nuovo menu di navigazione. Il nome del menu di navigazione viene utilizzato solo per la visualizzazione. Questo campo è obbligatorio.
                
                Dal momento che si può scegliere di specificare più menu di navigazione, si consiglia di utilizzare nomi significativi per i mapping dei tasti. La lunghezza massima del nome di un'associazione di tasti è di 64 caratteri e sono ammessi gli spazi, Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
            
              - **Quando si preme questo tasto**   Utilizzare questo elenco per abilitare il mapping dei tasti. L'associazione di tasti è il tasto numerico che il chiamante preme affinché l'operatore automatico esegua un'operazione specifica, ad esempio, l'inoltro della chiamata a un altro operatore automatico o a un operatore. Per impostazione predefinita, non viene definita nessuna voce.
                
                Utilizzare l'elenco a discesa per selezionare il tasto numerico (da 1 a 9) che il chiamante deve premere. Il numero 0 (zero) è riservato all'operatore automatico.
                
                Se si seleziona **Timeout** dall'elenco a discesa, si abilita il trasferimento della chiamata a un interno o a un altro operatore automatico nel caso in cui il chiamante non prema nessun tasto sul tastierino del telefono. (ad esempio, "Resti in linea. La sua chiamata verrà trasferita al primo operatore disponibile.") L'impostazione predefinita è 5 secondi. Se si abilita questa opzione, viene creata un'associazione di tasti vuota.
            
              - **Riproduci il seguente file audio**   Utilizzare questa opzione per selezionare un file audio registrato in precedenza per i chiamanti. Fare clic su **Cambia**, quindi fare clic su **Sfoglia** per individuare il file audio. Se non si modifica l'impostazione predefinita \<Nessuno\> per il file audio, il modulo di sintesi vocale (TTS) del server di messaggistica unificata sintetizzerà il prompt del menu principale per l'orario non di ufficio. In alternativa, è possibile creare un file audio personalizzato da utilizzare per il prompt del menu principale per l'orario non di ufficio per un operatore automatico abilitato al riconoscimento vocale. Ad esempio, si potrebbe utilizzare il messaggio, "Gli uffici di Contoso sono aperti dalle ore 9.00 alle ore 18.00, dal lunedì al venerdì. Per lasciare un messaggio vocale per il reparto vendite, dica 1. Per lasciare un messaggio vocale per il supporto tecnico, dica 2. Per lasciare un messaggio per il reparto amministrazione, dica 3. Per parlare con un operatore di turno, prema zero."
            
              - **Esegui questa ulteriore azione**   Selezionare una delle seguenti opzioni per definire l'azione che si desidera che l'operatore automatico esegua per il chiamante:
                
                  - **Nessuno**   Utilizzare questa opzione se non si desidera che l'operatore automatico trasferisca la chiamata a un interno o a un altro operatore automatico oppure per lasciare un messaggio per un utente.
                
                  - **Trasferisci a questo numero di interno**   Selezionare questa opzione per abilitare le chiamate da trasferire a un numero di interno. Se si abilita questa opzione, utilizzare la casella per digitare il numero di interno a cui verrà trasferita la chiamata. In questo campo è possibile inserire solo caratteri numerici. Non sono ammessi i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
                
                  - **Trasferisci a questo operatore automatico di messaggistica unificata**   Selezionare questa opzione per trasferire la chiamata a un operatore automatico esistente. Fare clic su **Sfoglia** per individuare l'operatore automatico che si desidera utilizzare. Prima di abilitare questa opzione, è necessario creare e configurare l'operatore automatico. Questa opzione viene utilizzata quando si crea una struttura padre/figlio di operatori automatici di messaggistica unificata.
                
                  - **Lascia un messaggio vocale per questo utente**   Selezionare questa opzione per abilitare un chiamante a lasciare un messaggio vocale per un utente sullo stesso dial plan dell'operatore automatico di messaggistica unificata che si sta configurando. Quando un chiamante sceglie questa opzione dal menu di un operatore automatico, gli verrà richiesto di lasciare un messaggio vocale per l'utente selezionato. Fare clic su **Sfoglia** per individuare l'utente abilitato alla messaggistica unificata.
                
                  - **Notifica sede aziendale**   Selezionare questa opzione per abilitare un chiamante a scegliere un'opzione del menu dell'operatore automatico e ascoltare le informazioni sulla sede aziendale che è configurata sull'operatore automatico di messaggistica unificata. Per abilitare correttamente l'opzione, è necessario prima inserire la sede aziendale nella casella **Sede aziendale** nella pagina **Generale** dell'operatore automatico di messaggistica unificata.
                
                  - **Notifica orario di ufficio**  Selezionare questa opzione per abilitare un chiamante a scegliere un'opzione del menu dell'operatore automatico e ascoltare le informazioni sull'orario di ufficio dell'azienda configurato sull'operatore automatico di messaggistica unificata. Per abilitare correttamente l'opzione, è necessario prima configurare l'orario di ufficio nella pagina **Orario di ufficio** dell'operatore automatico di messaggistica unificata.

7.  Utilizzo di **Accesso operatore e rubrica** per definire le funzionalità disponibili per i chiamanti che chiamano l'operatore automatico di messaggistica unificata. È possibile configurare le funzionalità dell'operatore automatico, come la lingua utilizzata quando i chiamanti contattano l'operatore automatico e la possibilità per i chiamanti di trasferimento al numero di interno dell'operatore. È possibile configurare quanto segue:
    
      - **Opzioni per contattare gli utenti**   Utilizzare queste opzioni per determinare in che modo i chiamanti possono contattare gli utenti con un messaggio vocale quando chiamano un operatore automatico di messaggistica unificata
        
          - **Consenti ai chiamanti il trasferimento agli utenti**   Selezionare questa casella di controllo per consentire ai chiamanti di trasferire le chiamate agli utenti. Per impostazione predefinita, tale opzione è abilitata e consente agli utenti associati al dial plan di trasferire le chiamate agli utenti dello stesso dial plan di messaggistica unificata. Dopo aver selezionato questa casella di controllo, è possibile configurare il gruppo di utenti a cui i chiamanti possono trasferire la chiamata selezionando l'opzione appropriata nella sezione **Opzioni per la ricerca nella rubrica** in questa pagina.
            
            Se vengono disabilitate questa opzione e l'opzione **Consenti ai chiamanti l'invio di messaggi vocali** , vengono disabilitate anche le opzioni sotto **Opzioni per la ricerca nella rubrica**.
        
          - **Consenti a chiamanti di lasciare messaggi vocali per gli utenti**   Selezionare questa casella di controllo per consentire ai chiamanti di inviare messaggi vocali agli utenti. Questa opzione è abilitata per impostazione predefinita e consente agli utenti associati al dial plan di inviare messaggi vocali agli utenti dello stesso dial plan. Dopo aver selezionato questa casella di controllo, è possibile configurare il gruppo di utenti a cui i chiamanti possono inviare messaggi vocali selezionando l'opzione appropriata nella sezione **Opzioni per la ricerca nella rubrica** in questa pagina.
            
            Se vengono disabilitate questa opzione e l'opzione **Consenti ai chiamanti di chiamare gli utenti**, vengono disabilitate anche le opzioni sotto **Opzioni per la ricerca nella rubrica**.
            
            Se questa opzione viene disabilitata, l'operatore automatico non inviterà i chiamanti a inviare un messaggio vocale durante un prompt di sistema.
    
      - **Opzioni per la ricerca nella rubrica**   Utilizzare queste opzioni per determinare un gruppo di utenti. Per impostazione predefinita, l'opzione **Consenti ai chiamanti di cercare un utente per nome o alias** è selezionata insieme all'opzione **Solo in questo dial plan**. Tuttavia è possibile modificare il gruppo di utenti per consentire ai chiamanti di trasferire le chiamate o inviare messaggi vocali agli utenti che si trovano nell'elenco di indirizzi globale dell'organizzazione. È possibile scegliere una delle seguenti opzioni:
        
          - **Consenti ai chiamanti di cercare un utente per nome o alias**   Per impostazione predefinita questa opzione è selezionata. Consente ai chiamanti che contattano questo operatore automatico di effettuare una ricerca all'interno della directory per trovare gli utenti con il nome o l'alias desiderato. Un alias viene assegnato a un utente quando viene creata per lui una cassetta postale. L'alias è la prima parte di un indirizzo SMTP, ad esempio tonysmith@contoso.com. L'indirizzo SMTP è tonysmith@contoso.com, mentre l'alias è tonysmith. Questa opzione è applicabile solo ai chiamanti che utilizzano questo operatore automatico e non a quelli che utilizzano Outlook Voice Access.
            
              - **Solo in questo dial plan**   Selezionare questa opzione per consentire ai chiamanti che si collegano all'operatore automatico di messaggistica unificata di individuare e contattare gli utenti all'interno dello stesso dial plan associato all'operatore automatico di messaggistica unificata. Per impostazione predefinita, questa opzione è abilitata sia sul dial plan sia sull'operatore automatico. Ciò vuol dire che gli utenti di Outlook Voice Access e i chiamanti nell'operatore automatico sono in grado di cercare gli utenti all'interno dello stesso dial plan.
            
              - **Nell'intera organizzazione**   Selezionare questa opzione per consentire ai chiamanti che chiamano questo operatore automatico di messaggistica unificata di cercare e contattare tutti gli utenti elencati nell'elenco indirizzi globale dell'organizzazione. Questo include non solo gli utenti abilitati all'uso della messaggistica unificata, ma anche tutti gli utenti che sono abilitati all'uso della cassetta postale. Questa opzione consente ai chiamanti di contattare gli utenti in più dial plan. Ma non è abilitata per impostazione predefinita. Questa impostazione è disponibile anche su un dial plan per gli utenti di Outlook Voice Access.
        
          - **Informazioni da includere per nomi simili**   Utilizzare questo menu a discesa per selezionare l'opzione utilizzata per l'operatore automatico di messaggistica unificata quando gli utenti hanno lo stesso nome o nomi simili. Questa impostazione viene utilizzata quando in una directory esistono due o più utenti con lo stesso nome. Viene anche chiamata campo di risoluzione ambiguità. È possibile configurare questa impostazione oppure lasciare l'impostazione predefinita sull'operatore automatico. Per impostazione predefinita, l'operatore automatico erediterà questa impostazione dall'impostazione sul dial plan collegato all'operatore automatico. Il seguente è un esempio di un operatore automatico abilitato al riconoscimento vocale:
            
            1.  Sistema: Benvenuti in Contoso. Se lo si conosce, dire il nome della persona con cui si desidera parlare."
            
            2.  Il chiamante dice "Tony Smith".
            
            3.  Ci sono più persone con questo nome. Selezionare una di queste opzioni: Per Tony Smith, ricerca, premere 1. Per Tony Smith, amministrazione, premere 2. Per Tony Smith, supporto tecnico, premere 3."
            
            4.  Il chiamante preme il tasto appropriato sulla tastiera e la chiamata viene trasferita all'utente.
                

                > [!NOTE]
                > Su un operatore automatico non abilitato al riconoscimento vocale, il sistema dirà al chiamante di utilizzare la tastiera per immettere il nome dell'utente (prima il cognome), quindi cercare l'utente. Se ci sono più persone con lo stesso nome nella directory, al chiamante vengono fornite istruzioni per premere il tasto appropriato per essere trasferito all'utente. In alternativa, è possibile creare un operatore automatico per il fallback del segnale multifrequenza (DTMF) che utilizza solo la tastiera per immettere un nome o alias.

            
            Per utilizzare queste impostazioni, è necessario aggiungere le corrette informazioni per l'utente. Ad esempio, se si desidera che l'operatore automatico utilizzi un titolo per due utenti con lo stesso nome, è necessario aggiungere questa informazione sull'account dell'utente. Selezionare uno dei seguenti metodi che forniscono al chiamante ulteriori informazioni per aiutarlo a selezionare l'utente corretto nell'organizzazione:
            
              - **InheritFromDialPlan** Selezionare questa opzione se si desidera che l'operatore automatico utilizzi le impostazioni predefinite del dial plan associato all'operatore automatico.
            
              - **Titolo**°°°Selezionare questa opzione affinché l'operatore automatico includa il titolo di ciascun utente in caso di corrispondenza.
            
              - **Reparto**°°°Selezionare questa opzione affinché l'operatore automatico includa il reparto di ciascun utente in caso di corrispondenza.
            
              - **Posizione**°°°Selezionare questa opzione affinché l'operatore automatico includa la posizione di ciascun utente in caso di corrispondenza.
            
              - **Nessuno**°°°Selezionare questa opzione se non si desiderano ulteriori informazioni in caso di corrispondenza.
            
              - **Prompt per l'alias**°°°Selezionare questa opzione affinché l'operatore automatico richieda al chiamante l'alias dell'utente.

8.  Sotto **Accesso operatore**, è possibile specificare le impostazioni dell'operatore automatico incluse le seguenti:
    
      - **Estensione operatore**°°°Utilizzare questa casella per digitare il numero di interno utilizzato per chiamare un operatore. Il numero di interno può anche collegare il chiamante a un operatore umano o a una cassetta postale abilitata alla messaggistica unificata oppure può essere configurato per chiamare un numero telefonico esterno. Per impostazione predefinita non sono inclusi interni di operatori in questa casella.
    
      - **Consenti trasferimento a operatore durante orario di ufficio**°°°Selezionare questa casella di controllo per consentire ai chiamanti di essere trasferiti a un operatore umano durante l'orario di ufficio utilizzando il numero di interno configurato nella casella **Interno operatore**. Questa opzione è disabilitata per impostazione predefinita.
        
        È utile abilitare questa opzione in modo che, se un chiamante non riesce a individuare la persona desiderata utilizzando i prompt di menu o la ricerca nella directory in orario di ufficio, sia possibile lasciare un messaggio vocale o contattare un operatore umano. Dopo aver abilitato questa opzione, è possibile configurare il numero di interno dell'operatore su una cassetta postale abilitata alla messaggistica unificata monitorata. Il chiamante può lasciare un messaggio vocale o può essere collegato al numero di interno di un operatore per ricevere assistenza.
    
      - **Consenti trasferimento a operatore durante orario di ufficio**°°°Selezionare questa casella di controllo per consentire ai chiamanti di essere trasferiti a un operatore umano durante l'orario di ufficio utilizzando il numero di interno configurato nella casella **Interno operatore**. Questa opzione è disabilitata per impostazione predefinita.
        
        È utile abilitare questa opzione in modo che, se un chiamante non riesce a individuare la persona desiderata utilizzando i prompt di menu o la ricerca nella directory dopo l'orario di ufficio, sia possibile lasciare un messaggio vocale o contattare un operatore umano. Dopo aver abilitato questa opzione, è possibile configurare il numero di interno dell'operatore configurato su una cassetta postale abilitata alla messaggistica unificata monitorata. Il chiamante può lasciare un messaggio vocale o può essere collegato al numero di interno di un operatore per ricevere assistenza.

9.  
    
    Utilizzo di **Autorizzazione di composizione** per configurare le regole di composizione per i chiamanti che chiamano un operatore automatico di messaggistica unificata. È possibile utilizzare queste impostazioni per controllare i numeri degli interni raggiungibili da un operatore automatico o per controllare i numeri di telefono che possono essere composti dai chiamanti che si sono collegati all'operatore automatico. È possibile configurare quanto segue:
    
      - **Chiamate a utenti nello stesso dial plan**   Selezionare questa casella di controllo per consentire agli utenti che chiamano un operatore automatico di effettuare o trasferire chiamate a un numero di interno associato a un utente abilitato alla messaggistica unificata nello stesso dial plan dell'operatore automatico. Questa impostazione è abilitata per impostazione predefinita.
        
        Se questa impostazione viene disabilitata, gli utenti che chiamano un operatore automatico non possono effettuare o trasferire chiamate agli utenti non abilitati alla messaggistica unificata o ad altri numeri di interni non associati a un utente abilitato alla messaggistica unificata. Gli utenti non possono trasferire le chiamate a utenti abilitati alla messaggistica unificata associati allo stesso dial plan dell'operatore automatico. Questa situazione si verifica poiché l'impostazione **Consenti le chiamate a un interno** è abilitata per impostazione predefinita.
    
      - **Consenti le chiamate a un interno**°°°Se questa impostazione viene disabilitata, gli utenti che chiamano un operatore automatico non possono effettuare chiamate agli utenti non abilitati alla messaggistica unificata o ad altri numeri di interni non associati a un utente abilitato alla messaggistica unificata. Tuttavia, tali utenti possono effettuare chiamate o trasferirle a numeri di interni associati a utenti abilitati alla messaggistica unificata. Tale condizione si verifica perché l'impostazione **Chiamate nello stesso dial plan di messaggistica unificata** è abilitata per impostazione predefinita. Per impostazione predefinita, l'impostazione **Consenti le chiamate a un interno** è abilitata.
        
        Se questa impostazione è abilitata, gli utenti che chiamano un operatore automatico possono effettuare chiamate agli utenti non abilitati alla messaggistica unificata, ad altri numeri di interni non associati a un utente abilitato alla messaggistica unificata e agli utenti abilitati alla messaggistica unificata. Tale condizione si verifica perché l'impostazione **Chiamate nello stesso dial plan di messaggistica unificata** è abilitata per impostazione predefinita.
        
        È possibile abilitare questa impostazione in un ambiente in cui non tutti gli utenti sono stati abilitati alla messaggistica unificata. Questa impostazione è utile anche quando si desidera consentire agli utenti che chiamano un numero di telefono configurato su un operatore automatico di chiamare numeri di interni non associati a un utente abilitato alla messaggistica unificata.
    
      - **Gruppi di regole nazionali consentiti dal dial plan**   Utilizzare questa sezione per aggiungere o rimuovere i gruppi di regole di composizione nazionali consentiti. Per impostazione predefinita, non è presente alcun gruppo di regole di composizione nazionale configurato sugli operatori automatici di messaggistica unificata.
        
        I gruppi di regole di composizione nazionali sono utilizzati per consentire o limitare i numeri di telefono di un paese che gli utenti che hanno chiamato l'operatore automatico di messaggistica unificata possono comporre. Ciò consente di evitare chiamate telefoniche non necessarie o non autorizzate e costi relativi alle chiamate.
        
        Per aggiungere gruppi di regole di composizione nazionali, è necessario innanzitutto creare gruppi di regole di composizione nazionali appropriati nel dial plan associato all'operatore automatico di messaggistica unificata, quindi aggiungere il gruppo di regole di composizione appropriato.
        
        I gruppi di regole di composizione nazionali possono essere utilizzati dalla Messaggistica unificata al fine di consentire o limitare l'accesso ai numeri di telefono nazionali. Questo si applica a qualsiasi utente che ha chiamato l'operatore automatico. Per ulteriori informazioni sull'effettuazione di chiamate esterne, vedere [Consentire agli utenti di effettuare chiamate](allow-users-to-make-calls-exchange-2013-help.md).
    
      - **Gruppi di regole internazionali consentiti dal dial plan**   Utilizzare questa sezione per aggiungere o rimuovere i gruppi di regole di composizione internazionali consentiti. Per impostazione predefinita, non è presente alcun gruppo di regole di composizione internazionali configurato sugli operatori automatici di messaggistica unificata.
        
        I gruppi di regole di composizione internazionali vengono utilizzati per consentire o limitare i numeri di telefono al di fuori di un paese che gli utenti che hanno chiamato l'operatore automatico di messaggistica unificata possono comporre. Ciò consente di evitare chiamate telefoniche non necessarie o non autorizzate e costi relativi alle chiamate.
        
        Per aggiungere gruppi di composizione internazionali, è necessario creare prima i gruppi internazionali corretti sul dial plan associato all'operatore automatico di messaggistica unificata. Una volta creati i gruppi di regole di composizione richiesti nel dial plan, è necessario aggiungere tali gruppi all'elenco dei gruppi di regole di composizione autorizzati sull'operatore automatico di messaggistica unificata.
        
        I gruppi di regole di composizione internazionali possono essere utilizzati dalla Messaggistica unificata al fine di consentire o limitare l'accesso ai numeri di telefono internazionali. Questo si applica a qualsiasi utente che ha chiamato l'operatore automatico. Per ulteriori informazioni sull'effettuazione di chiamate esterne, vedere [Consentire agli utenti di effettuare chiamate](allow-users-to-make-calls-exchange-2013-help.md).

10. Fare clic su **OK** per creare il nuovo menu di navigazione.

11. Nella pagina **Operatore automatico di messaggistica unificata**, fare clic su **Salva** per salvare le modifiche.

## Configurazione delle proprietà dell'operatore automatico di messaggistica unificata tramite Shell

In questo esempio viene configurato un operatore automatico di messaggistica unificata denominato `MySpeechEnabledAA` per il passaggio all'operatore automatico `MyDTMFAA`, viene impostato l'interno dell'operatore su 50100 e viene abilitato il trasferimento delle chiamate a questo numero di interno dopo l'orario di ufficio.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true

In questo esempio viene configurato un operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant` che dispone di: Orario di ufficio configurato come: la domenica dalle 10:45 alle 13:15, il lunedì dalle 09:00 alle 17:00 e il sabato dalle 09:00 alle 16:30; festività e relativi messaggi di saluto configurati come: "Buon anno" il 02.01.13 e su "Edificio chiuso per lavori" configurato dal 24 al 28.04.13.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

## Visualizzazione delle proprietà dell'operatore automatico di messaggistica unificata tramite Shell

Con questo esempio viene restituito un elenco formattato di tutti gli operatori automatici di messaggistica unificata.

    Get-UMAutoAttendant | Format-List

In questo esempio vengono visualizzate le proprietà di un operatore automatico di messaggistica unificata denominato MyUMAutoAttendant.

    Get-UMAutoAttendant -Identity MyUMAutoAttendant


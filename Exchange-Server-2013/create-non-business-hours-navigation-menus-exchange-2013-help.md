---
title: 'Creare le ore di inattività menu di spostamento: Exchange 2013 Help'
TOCTitle: Creare le ore di inattività menu di spostamento
ms:assetid: bfe81ed6-9648-4882-8baf-ac93ea30a8ca
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232175(v=EXCHG.150)
ms:contentKeyID: 50481568
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare le ore di inattività menu di spostamento

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-05_

È possibile abilitare il mapping dei tasti per l'orario non di ufficio su un operatore automatico di messaggistica unificata. Una volta creato un operatore automatico di messaggistica unificata, verrà utilizzato un menu vocale di sistema predefinito per il messaggio di saluto "Istruzione vocale menu principale Orario non di ufficio" riprodotto per i chiamanti dopo la riproduzione della formula di benvenuto per l'orario non di ufficio. Il prompt di saluto predefinito del menu principale Orario non di ufficio utilizza le parole seguenti: "Operatore automatico Orario non di ufficio di MicrosoftExchange. Dal momento che per impostazione predefinita non sono definiti mapping dei tasti, non sono disponibili voci di menu per i chiamanti, che possono solamente ascoltare il prompt del menu principale Orario non di ufficio.

Quando viene configurato il mapping dei tasti, vengono definite le opzioni e le operazioni che verranno eseguite se un chiamante pronuncia una frase mentre sta utilizzando un operatore automatico abilitato al servizio di sintesi vocale o se preme un tasto sulla tastiera del telefono mentre sta utilizzando un operatore automatico non abilitato al servizio di sintesi vocale.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un operatore automatico di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un operatore automatico di messaggistica unificata](create-a-um-auto-attendant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Abilitazione del mapping dei tasti per l'orario non di ufficio su un operatore automatico di messaggistica unificata tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  In **Operatori automatici di messaggistica unificata** della pagina **Dial plan di messaggistica unificata** selezionare l'operatore automatico di messaggistica unificata per cui si desidera creare un menu per l'orario non di ufficio. Sulla barra degli strumenti, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") nella barra degli strumenti.

3.  Nella pagina **Operatore automatico di messaggistica unificata** fare clic su **Spostamento nei menu** in **Spostamento nei menu in orario non di ufficio**, selezionare **Abilita spostamento nei menu in orario non di ufficio**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  Nella pagina **Nuova voce di spostamento nei menu** utilizzare le opzioni seguenti per creare una nuova voce di spostamento nei menu:
    
      - **Prompt**   Utilizzare questa casella per digitare il nome del nuovo menu di navigazione. Il nome del menu di navigazione viene utilizzato solo per la visualizzazione. Questo campo è obbligatorio.
        
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
        
          - **Notifica orario di ufficio**   Selezionare questa opzione per abilitare un chiamante a scegliere un'opzione del menu dell'operatore automatico e ascoltare le informazioni sull'orario di ufficio dell'azienda configurato sull'operatore automatico di messaggistica unificata. Per abilitare correttamente l'opzione, è necessario prima configurare l'orario di ufficio nella pagina **Orario di ufficio** dell'operatore automatico di messaggistica unificata.

5.  Fare clic su **OK** per creare il nuovo menu di navigazione.

6.  Nella pagina **Operatore automatico di messaggistica unificata**, fare clic su **Salva** per salvare le modifiche.

## Abilitazione del mapping dei tasti per l'orario non di ufficio su un operatore automatico di messaggistica unificata tramite Shell

Con questo esempio viene configurato un operatore automatico di messaggistica unificata denominato `MyAutoAttendant` e viene abilitato il mapping dei tasti per l'orario non di ufficio in modo che, quando i chiamanti pronunciano le parole "After Hours", vengano reindirizzati al numero di interno 12345, mentre se pronunciano "Directions" vengano reindirizzati al numero di interno 23456.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AfterHoursKeyMappingEnabled $true -AfterHoursKeyMapping "AfterhoursOperator,12345","Directions,23456"


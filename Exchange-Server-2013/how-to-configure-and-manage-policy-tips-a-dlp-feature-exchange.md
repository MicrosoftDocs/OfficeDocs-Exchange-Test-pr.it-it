---
title: 'Gestire i suggerimenti sui criteri: Exchange 2013 Help'
TOCTitle: Gestire i suggerimenti sui criteri
ms:assetid: cec50a35-1d00-47b3-b72f-ac1bb0fd630e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619307(v=EXCHG.150)
ms:contentKeyID: 50479800
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire i suggerimenti sui criteri

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Suggerimenti sui criteri sono avvisi informativi visualizzati per i mittenti di posta elettronica durante la composizione di un messaggio. Lo scopo del suggerimento criteri è formare gli utenti che possono violazione delle procedure commerciali o i criteri vengono applicate con i criteri di criterio DLP perdita di dati che è stato stabilito. Le procedure seguenti consentono di iniziare a utilizzare i suggerimenti sui criteri. Guardare questo video per ulteriori informazioni.

> [!VIDEO https://www.microsoft.com/it-it/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 30 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Prevenzione della perdita di dati (DLP)" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - I suggerimenti sul criterio vengono visualizzati per i mittenti dei messaggi solo quando vengono soddisfatte le condizioni seguenti:
    
    1.  Il programma client del mittente del messaggio è Microsoft Outlook 2013. Se la propria organizzazione ha distribuito Exchange 2013 SP1 o utilizza Exchange Online, i suggerimenti del criterio vengono visualizzati in Outlook Web App e OWA per i dispositivi.
    
    2.  Esiste una regola di trasporto che richiama le notifiche del suggerimento sul criterio. È possibile creare una tale regola di trasporto configurando un criterio DLP che includa l'azione **Notifica al mittente con un suggerimento per il criterio**.
    
    3.  Il contenuto dell'intestazione, del corpo o dell'allegato di un messaggio analizzato dall'agente di trasporto soddisfa le condizioni stabilite all'interno dei criteri DLP o delle regole che includono anche le regole per la modifica dei suggerimenti sul criterio. In altre parole, il suggerimento sul criterio viene visualizzato dagli utenti finali quando eseguono un'azione che provoca l'applicazione della regola associata.

  - Il testo di notifica del suggerimento sul criterio predefinito incorporato nel sistema viene visualizzato se non viene utilizzata la funzionalità delle impostazioni per personalizzarlo. Per ulteriori informazioni sul testo predefinito, vedere [Suggerimenti per i criteri](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Creazione o modifica di un suggerimento sul criterio di sola notifica

Questa procedura dà luogo a un suggerimento sul criterio informativo che viene visualizzato a un mittente del messaggio quando vengono soddisfatte le condizioni di una regola specifica. In Microsoft Outlook il mittente può impedire la visualizzazione del suggerimento utilizzando la finestra di dialogo delle opzioni relative. Per configurare il testo personalizzato del suggerimento per il criterio, vedere Create custom Policy Tip notification text.

## Configurazione dei suggerimenti sul criterio di sola notifica tramite EAC

1.  In EAC, andare a **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Fare doppio clic su uno dei criteri visualizzati nell'elenco dei criteri o evidenziare un elemento e selezionare **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Modifica criteri DLP**, selezionare **Regole**.

4.  Per aggiungere suggerimenti relativi al criterio a una regola esistente, evidenziare la regola e selezionare **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    
    Per aggiungere una nuova regola vuota completamente personalizzabile, selezionare **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e quindi **Crea una nuova regola**.

5.  In **Applica questa regola se**, selezionare **Il messaggio contiene informazioni riservate**. È una condizione obbligatoria.

6.  Selezionare ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), selezionare i tipi di informazioni riservate, selezionare **Aggiungi**, quindi **OK** e fare clic su **OK**.

7.  Nella casella **Procedi come segue**, selezionare **Notifica al mittente con un suggerimento per il criterio**, quindi selezionare un'opzione nell'elenco a discesa **Scegli se il messaggio è bloccato o può essere inviato**, quindi selezionare **OK**.

8.  Per aggiungere ulteriori condizioni o azioni, nella parte inferiore della finestra, selezionare **Altre opzioni**.
    

    > [!NOTE]
    > È possibile utilizzare solo le seguenti condizioni: 
    > <UL>
    > <LI>
    > <P><STRONG>SentTo (il destinatario è)</STRONG></P>
    > <LI>
    > <P><STRONG>SentToScope (il destinatario è individuato)</STRONG></P>
    > <LI>
    > <P><STRONG>Da (il mittente è)</STRONG></P>
    > <LI>
    > <P><STRONG>FromMemberOf (il mittente è un membro di)</STRONG></P>
    > <LI>
    > <P><STRONG>FromScope (il mittente è individuato)</STRONG></P></LI></UL>Non è possibile utilizzare le seguenti azioni: 
    > <UL>
    > <LI>
    > <P><STRONG>RejectMessageReasonText (rifiuta il messaggio e Includi una spiegazione)</STRONG></P>
    > <LI>
    > <P><STRONG>RejectMessageEnhancedStatusCode (rifiuta il messaggio con il codice di stato avanzato)</STRONG></P>
    > <LI>
    > <P><STRONG>DeletedMessage (Elimina il messaggio senza inviare alcuna notifica)</STRONG></P></LI></UL>



9.  Nell'elenco **Scegli una modalità per questa regola**, selezionare se si desidera che la regola venga applicata. Si consiglia prima di verificare la regola.

10. Selezionare **Salva** per terminare la modifica della regola e salvare le modifiche.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver creato correttamente un suggerimento sul criterio che invierà solo la notifica a un mittente, effettuare le operazioni seguenti:

1.  In EAC, andare a **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Selezionare il criterio che si ritiene debba contenere un messaggio di notifica.

3.  Selezionare **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"), quindi **Regole**.

4.  Selezionare la regola specifica che si ritiene debba contenere un messaggio di notifica.

5.  Verificare che l'azione **Notifica al mittente** sia visualizzata nella parte inferiore del riepilogo delle regole.

## Creazione o modifica di un suggerimento sul criterio di blocco messaggio

Questa procedura dà luogo alla visualizzazione del suggerimento sul criterio a un mittente e indica che un messaggio viene rifiutato e non sarà recapitato fino a quando sarà presente la condizione problematica. Il mittente ha a disposizione un'opzione per indicare che il messaggio di posta elettronica non contiene la condizione problematica. In questo caso si parla anche di override dei falsi positivi. Se il mittente fornisce questa indicazione, il messaggio può lasciare la casella della posta in uscita e il rapporto dell'utente può essere controllato. Exchange bloccherà tuttavia l'invio del messaggio. Per configurare il testo personalizzato del suggerimento per il criterio, vedere Create custom Policy Tip notification text.

## Configurazione dei suggerimenti sul criterio di blocco messaggio tramite EAC

1.  In EAC, andare a **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Fare doppio clic su uno dei criteri visualizzati nell'elenco dei criteri o evidenziare un elemento e selezionare **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Modifica criteri DLP**, selezionare **Regole**.

4.  Per aggiungere suggerimenti relativi al criterio a una regola esistente, evidenziare la regola e selezionare **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

5.  Per aggiungere una nuova regola vuota e personalizzarla, selezionare **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

6.  Per aggiungere un'azione che rivelerà un suggerimento sul criterio, selezionare **Altre opzioni…**, quindi il pulsante **Aggiungi azione**.

7.  Dall'elenco a discesa selezionare **Notifica al mittente con un suggerimento per il criterio** e quindi selezionare **Blocca il messaggio**.

8.  Selezionare **OK**, quindi **Salva** per terminare la modifica della regola e salvare le modifiche.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione del suggerimento sul criterio per il messaggio di rifiuto, effettuare le seguenti operazioni:

1.  In EAC, andare a **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Selezionare una sola volta per evidenziare il criterio contenente il messaggio di notifica desiderato.

3.  Selezionare **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"), quindi **Regole**.

4.  Selezionare una sola volta per evidenziare la regola specifica contenente il messaggio di notifica desiderato.

5.  Verificare che l'azione **Notifica al mittente che il messaggio non può essere inviato** sia visualizzata nella parte inferiore del riepilogo delle regole.

## Creazione o modifica di un suggerimento sul criterio di blocco se non ignorato

Sono disponibili quattro opzioni per i suggerimenti sul criterio che possono rifiutare i messaggi o impedire che lascino la casella della posta in uscita del mittente. Per ulteriori informazioni su queste opzioni, vedere [Suggerimenti per i criteri](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

## Utilizzo di EAC per configurare i suggerimenti sul criterio di blocco se non ignorato

1.  In EAC, andare a **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Fare doppio clic su uno dei criteri visualizzati nell'elenco dei criteri o evidenziare un elemento e selezionare **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Modifica criteri DLP**, selezionare **Regole**.

4.  Per aggiungere suggerimenti relativi al criterio a una regola esistente, evidenziare la regola e selezionare **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    
    Per aggiungere una nuova regola vuota completamente personalizzabile, selezionare **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), quindi **Altre opzioni…** .

5.  Per aggiungere l'azione in seguito alla quale verrà mostrato un suggerimento per il criterio, selezionare il pulsante **Aggiungi azione**.

6.  Dall'elenco a discesa selezionare **Notifica al mittente con un suggerimento per il criterio** e quindi selezionare **Blocca il messaggio, ma consenti al mittente di intervenire e inviarlo comunque**.

7.  Selezionare **OK**, quindi **Salva** per terminare la modifica della regola e salvare le modifiche.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione del suggerimento sul criterio di rifiuto se non ignorato, effettuare le seguenti operazioni:

1.  In EAC, andare a **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Selezionare una sola volta per evidenziare il criterio contenente il messaggio di notifica desiderato.

3.  Selezionare **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"), quindi **Regole**.

4.  Selezionare una sola volta per evidenziare la regola specifica contenente il messaggio di notifica desiderato.

5.  Verificare che l'azione **Blocca il messaggio, ma consenti al mittente di intervenire e inviarlo comunque** sia visualizzata nella parte inferiore del riepilogo delle regole.

## Creazione del testo di notifica personalizzato per il suggerimento sul criterio

Questa procedura facoltativa consentirà di personalizzare il testo di notifica del suggerimento sul criterio che i mittenti dei messaggi visualizzeranno nel programma di posta elettronica. In questo caso, il testo di notifica del suggerimento sul criterio personalizzato non verrà visualizzato a meno che si configuri anche la regola del criterio DLP con un'azione che causerà la visualizzazione della notifica. Tenere presente che esistono notifiche per il suggerimento sul criterio predefinite dal sistema che possono essere visualizzate se non viene personalizzato il testo di notifica del suggerimento. Per ulteriori informazioni sul testo predefinito, vedere [Suggerimenti per i criteri](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

## Creazione e gestione del testo di notifica del suggerimento sul criterio personalizzato tramite EAC

1.  In EAC, andare a **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Selezionare **Impostazioni per suggerimento criterio**![Impostazioni suggerimento per i criteri](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "Impostazioni suggerimento per i criteri").

3.  Per aggiungere un nuovo suggerimento sul criterio al messaggio personalizzato, selezionare **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per ulteriori informazioni sulle azioni possibili, vedere [Suggerimenti per i criteri](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).
    
    Per modificare un suggerimento sul criterio esistente, evidenziarlo e selezionare **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    
    Per eliminare un suggerimento sul criterio esistente, evidenziarlo e selezionare **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina"), quindi confermare l'azione.

4.  Selezionare **Salva** per completare la modifica del suggerimento sul criterio e salvare le modifiche.

5.  Fare clic su **Chiudi** per terminare la gestione dei suggerimenti sul criterio e salvare le modifiche.

## Creazione del testo di notifica per il suggerimento sul criterio personalizzato tramite Shell

Nell'esempio seguente viene creato un nuovo suggerimento sul criterio in lingua inglese che bloccherà l'invio di un messaggio. Il testo del suggerimento del criterio personalizzato è stato modificato nel valore seguente: "This message appears to contain restricted content and will not be delivered."

    New-PolicyTipConfig -Name en\Reject -Value "This message appears to contain restricted content and will not be delivered."

Per ulteriori informazioni sui cmdlet DLP, vedere [Cmdlet dei criteri e di conformità](https://technet.microsoft.com/it-it/library/dd298082\(v=exchg.150\)).

## Modifica del testo di notifica personalizzato per il suggerimento sul criterio tramite Shell

Nell'esempio seguente viene modificato un suggerimento sul criterio esistente di sola notifica in lingua inglese. Il testo di questo suggerimento sul criterio personalizzato è stato modificato in "Non è consigliabile l'invio dei numeri di conto bancario per posta elettronica.

    Set-PolicyTipConfig en\NotifyOnly "Sending bank account numbers in email is not recommended."

Per ulteriori informazioni sui cmdlet DLP, vedere [Cmdlet dei criteri e di conformità](https://technet.microsoft.com/it-it/library/dd298082\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione del testo per il suggerimento sul criterio personalizzato, effettuare le seguenti operazioni:

1.  In EAC, andare a **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Selezionare **Impostazioni per suggerimento criterio**![Impostazioni suggerimento per i criteri](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "Impostazioni suggerimento per i criteri").

3.  Selezionare **Aggiorna**![Icona Aggiorna](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icona Aggiorna").

4.  Verificare che l'azione, l'impostazione locale e il testo per l'impostazione locale vengano visualizzate nell'elenco.

## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Suggerimenti per i criteri](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)

[Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange 2013

[Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) Exchange Online

[Suggerimenti di Exchange 2010](https://go.microsoft.com/fwlink/?linkid=265179)


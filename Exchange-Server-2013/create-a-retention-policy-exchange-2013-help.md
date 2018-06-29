---
title: 'Creare un criterio di conservazione: Exchange 2013 Help'
TOCTitle: Creare un criterio di conservazione
ms:assetid: d8806c98-fea5-492f-906d-f514e25361b2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150573(v=EXCHG.150)
ms:contentKeyID: 50481801
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un criterio di conservazione

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

In Exchange Online e Exchange Server 2013, è possibile utilizzare i criteri di conservazione per la gestione del ciclo di vita di posta elettronica. Creare i tag di conservazione, aggiungendoli a un criterio di conservazione e applicare il criterio agli utenti di cassette postali vengono applicati i criteri di conservazione.

Ecco un [video](https://go.microsoft.com/fwlink/?linkid=825854) che illustra come creare un criterio di conservazione e applicare a una cassetta postale in Exchange Online.

Per le attività di gestione aggiuntive relative ai criteri di conservazione, vedere [Messaggistica Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 30 minuti.

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - Le cassette postali a cui vengono applicati i criteri di conservazione devono risiedere in server Exchange Server 2010 o versioni successive.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Come eseguire l'operazione?

## Passaggio 1: Creazione di un tag di conservazione

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione record di messaggistica" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

**Creazione di un tag conservazione tramite l'interfaccia di amministrazione di Exchange**

1.  Accedere a **Gestione della conformità** \> **Tag di conservazione**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi")

2.  Selezionare una delle seguenti opzioni:
    
      - **Applicato automaticamente all'intera cassetta postale (predefinito)**   Selezionare questa opzione per creare un tag dei criteri predefiniti (DPT). I tag dei criteri predefiniti possono essere utilizzati per creare un criterio di eliminazione e un criterio di archiviazione predefiniti applicabili a tutti gli elementi della cassetta postale.
        

        > [!NOTE]
        > Non è possibile utilizzare Interfaccia di amministrazione di Exchange per creare un tag dei criteri predefiniti (DPT) ed eliminare i messaggi vocali. Per informazioni dettagliate su come creare un DPT per eliminare messaggi vocali, vedere l'esempio Shell in basso.

    
      - **Applicato automaticamente a una cartella specifica**   Selezionare questa opzione per creare un tag criterio di conservazione (RPT) per una cartella predefinita come **Posta in arrivo** e **Posta eliminata**.
        

        > [!NOTE]
        > È possibile creare tag dei criteri di conservazione solo con le azioni <STRONG>Elimina e consenti ripristino</STRONG> o <STRONG>Elimina definitivamente</STRONG>.

    
      - **Applicato dagli utenti a elementi e cartelle (Personale)**   Selezionare questa opzione per creare tag personali. Questi tag consentono agli utenti di Outlook e Outlook Web App di applicare a un messaggio o alle cartelle impostazioni di archiviazione o eliminazione diverse dalle impostazioni applicate alla cartella principale o all'intera cassetta postale.

3.  Il titolo della pagina **Nuovo tag di conservazione** e le opzioni varieranno in base al tipo di tag selezionato. Completare i seguenti campi:
    
      - **Nome** Immettere un nome per il tag di conservazione. Il nome del tag viene utilizzato solo per la visualizzazione e non incide in alcun modo sulla cartella o sull'elemento a cui è applicato. Tenere presente che i tag personali predisposti per gli utenti diventano disponibili in Outlook e Outlook Web App.
    
      - **Applica il tag alla cartella predefinita predefinita**   Questa opzione è disponibile solo se si seleziona **Applicato automaticamente a una cartella specifica**.
    
      - **Azione conservazione**   Selezionare una delle seguenti azioni da intraprendere una volta che l'elemento ha raggiunto il periodo di conservazione:
        
          - **Elimina e consenti ripristino**   Selezionare questa azione per eliminare gli elementi ma consentire agli utenti di ripristinarli utilizzando l'opzione **Recupera elementi eliminati** disponibile in Outlook o Outlook Web App. Gli elementi vengono conservati fino al raggiungimento del periodo di mantenimento degli elementi eliminati configurato per il database delle cassette postali o per l'utente della cassetta postale.
        
          - **Elimina definitivamente** Selezionare questa opzione per eliminare definitivamente l'elemento dal database delle cassette postali.
            

            > [!IMPORTANT]
            > Le cassette postali o gli elementi soggetti all'archiviazione sul posto o alla conservazione per controversia legale verranno conservati e restituiti nelle ricerche eDiscovery in locale. Per ulteriori informazioni, vedere <A href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Archiviazione sul posto e conservazione per controversia legale</A>.

        
          - **Sposta in archivio**   Questa azione è disponibile solo se si sta creando un DPT o un tag personale. Selezionare questa azione per spostare gli elementi nell'archivio sul posto dell'utente.
    
      - **Periodo di conservazione**Selezionare una delle seguenti opzioni:
        
          - **Mai**   Selezionare questa opzione per specificare che gli elementi non devono mai essere eliminati o spostai nell'archivio.
        
          - **Al raggiungimento della seguente scadenza (in giorni)**   Selezionare questa opzione e specificare il numero di giorni per conservare gli elementi prima che vengano spostati o eliminati. Il periodo di validità della conservazione per tutti gli elementi supportati, ad eccezione di Calendario e Attività, viene calcolato a partire dalla data di ricezione o creazione dell'elemento. Il periodo di validità della conservazione per Calendario e Attività viene calcolato a partire dalla data di fine.
    
      - **Commento**   Utilizzare questo campo facoltativo per immettere note o commenti amministrativi. Il campo non viene visualizzato agli utenti.

**Creazione di un criterio di conservazione tramite Shell**

Utilizzare il cmdlet **New-RetentionPolicyTag** per creare un tag di conservazione. Le opzioni diverse disponibili nel cmdlet consentono di creare tipi diversi di tag di conservazione. Utilizzare il parametro *Type* per creare un tag dei criteri predefiniti (`All`), un tag dei criteri di conservazione (specificare un tipo di cartella predefinito, ad esempio `Inbox`) o un tag personale (`Personal`).

Con questo esempio viene creato un tag dei criteri predefiniti allo scopo di eliminare tutti i messaggi dalla cassetta postale dopo 7 anni (2.556 giorni).

    New-RetentionPolicyTag -Name "DPT-Corp-Delete" -Type All -AgeLimitForRetention 2556 -RetentionAction DeleteAndAllowRecovery

Con questo esempio viene creato un tag dei criteri predefiniti allo scopo di spostare tutti i messaggi nell'archivio sul posto dopo 2 anni (730 giorni).

    New-RetentionPolicyTag -Name "DPT-Corp-Move" -Type All -AgeLimitForRetention 730 -RetentionAction MoveToArchive

Con questo esempio viene creato un tag dei criteri predefiniti allo scopo di eliminare i messaggi vocali dopo 20 giorni.

    New-RetentionPolicyTag -Name "DPT-Corp-Voicemail" -Type All -MessageClass Voicemail -AgeLimitForRetention 20 -RetentionAction DeleteAndAllowRecovery

Con questo esempio viene creato un tag dei criteri di conservazione allo scopo di eliminare definitivamente i messaggi presenti nella cartella Posta indesiderata dopo 30 giorni.

    New-RetentionPolicyTag -Name "RPT-Corp-JunkMail" -Type JunkEmail -AgeLimitForRetention 30 -RetentionAction PermanentlyDelete

Con questo esempio viene creato un tag personale per non eliminare mai un messaggio.

    New-RetentionPolicyTag -Name "Never Delete" -Type Personal -RetentionAction DeleteAndAllowRecovery -RetentionEnabled $false

## Passaggio 2: Creazione di un criterio di conservazione

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione record di messaggistica" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

**Creazione di un criterio di conservazione tramite l'interfaccia di amministrazione di Exchange**

1.  Passare a **Gestione della conformità** \> **Criteri di conservazione**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi")

2.  In **Nuovo criterio di conservazione**, completare i seguenti campi:
    
      - **Nome**  Immettere un nome per il criterio di conservazione.
    
      - **Tag di conservazione**   Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per selezionare i tag da aggiungere al criterio.
        
        Un criterio di conservazione può contenere i seguenti tag:
        
          - Un tag DPT con l'azione **Sposta nell'archivio**
        
          - Un tag DPT con l'azione **Elimina e consenti ripristino** o **Elimina definitivamente**
        
          - Un tag DPT per i messaggi vocali con l'azione **Elimina e consenti ripristino** o **Elimina definitivamente**
        
          - Un tag dei criteri di conservazione per cartella predefinita, come **Posta in arrivo**, per eliminare gli elementi
        
          - Qualsiasi numero di tag personali
            

            > [!NOTE]
            > Anche se è possibile aggiungere qualsiasi numero di tag personali, disporre di molti tag personali con diverse impostazioni di conservazione può confondere gli utenti. Si consiglia di collegare non più di dieci tag personali a un criterio di conservazione.

        
        È possibile creare un criterio di conservazione senza aggiungervi tag di conservazione anche se gli elementi nella cassetta postale a cui viene applicato il criterio non verranno spostati o eliminati. È possibile anche aggiungere o rimuovere tag di conservazione da un criterio di conservazione dopo che è stato creato.

**Creazione di un criterio di conservazione tramite Shell**

Con questo esempio viene creato il criterio di conservazione RetentionPolicy-Corp e utilizzato il parametro *RetentionPolicyTagLinks* per associare cinque tag al criterio.

    New-RetentionPolicy "RetentionPolicy-Corp"  -RetentionPolicyTagLinks "DPT-Corp-Delete","DPT-Corp-Move","DPT-Corp-Voicemail","RPT-Corp-JunkMail","Never Delete"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-RetentionPolicy](https://technet.microsoft.com/it-it/library/dd297970\(v=exchg.150\)).

## Passaggio 3: Applicazione dei criteri di conservazione agli utenti delle cassette postali

Una volta creato un criterio di conservazione, è necessario applicarlo agli utenti delle cassette postali. È possibile applicare criteri di conservazione diversi a set di utenti diversi. Per istruzioni dettagliate, vedere [Applicazione dei criteri di conservazione alle cassette postali](apply-a-retention-policy-to-mailboxes-exchange-2013-help.md).

## Come verificare se l'operazione ha avuto esito positivo?

Una volta creati i tag di conservazione, aggiungerli a un criterio di conservazione e applicare il criterio all'utente di una cassetta postale. Alla successiva elaborazione della cassetta postale da parte dell'assistente cassette postali MRM, i messaggi verranno spostati o eliminati in base alle impostazioni configurate nei tag di conservazione.

Per verificare che il criterio di conservazione sia stato eseguito correttamente, procedere come segue:

1.  Eseguire il comando della shell per l'esecuzione manuale dell'assistente MRM per singola casetta postale.
    
        Start-ManagedFolderAssistant -Identity <mailbox identity>

2.  Accedere alla cassetta postale utilizzando Outlook o Outlook Web App e verificare che i messaggi siano stati eliminati o spostati in un archivio in base alla configurazione del criterio.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



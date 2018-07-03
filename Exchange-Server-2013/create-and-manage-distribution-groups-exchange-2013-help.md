---
title: 'Creazione e gestione dei gruppi di distribuzione: Exchange 2013 Help'
TOCTitle: Creazione e gestione dei gruppi di distribuzione
ms:assetid: c4c43493-55e1-46d2-bd4b-d6f6cecd747f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124513(v=EXCHG.150)
ms:contentKeyID: 50481611
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDistributionGroupWizardForm.CreateDistributionGroupIntroductionWizardPage
ms.translationtype: HT
---

# Creazione e gestione dei gruppi di distribuzione

 

_**Si applica a:** Exchange Online, Exchange Server 2016, Office 365_

_**Ultima modifica dell'argomento:** 2016-12-09_

Utilizzare Interfaccia di amministrazione di Exchange (EAC) oppure Exchange Management Shell per creare un nuovo gruppo di distribuzione nell'organizzazione di Exchange o per abilitare alla posta un gruppo esistente in Active Directory.

Esistono due tipi di gruppi che possono essere utilizzati per la distribuzione dei messaggi:

  - *I gruppi di distribuzione universali abilitati alla posta elettronica* (denominati anche *gruppi di distribuzione*) possono essere utilizzati solo per distribuire i messaggi.

  - *I gruppi di protezione universali abilitati alla posta elettronica* (denominati anche *gruppi di protezione*) possono essere utilizzati per distribuire i messaggi e per garantire le autorizzazioni di accesso alle risorse in Active Directory. Per ulteriori informazioni, vedere [Gestire gruppi di sicurezza abilitati alla posta elettronica](manage-mail-enabled-security-groups-exchange-2013-help.md).

È importante considerare le differenze terminologiche tra Active Directory ed Exchange. In Active Directory, con gruppo di distribuzione si intende qualsiasi gruppo che non dispone di un contesto di protezione, indipendentemente dal fatto che sia abilitato alla posta o meno. Al contrario, in Exchange tutti i gruppi abilitati alla posta sono gruppi di distribuzione, che dispongono di un contesto di protezione o meno.

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2-5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di distribuzione" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Se nell'organizzazione sono configurati i criteri di denominazione dei gruppi, vengono applicati solo ai gruppi creati dagli utenti. Quando l'utente o un amministratore utilizza Interfaccia di amministrazione di Exchange per creare gruppi di distribuzione, i criteri di denominazione dei gruppi vengono ignorati e non vengono applicati al nome del gruppo. Se tuttavia si utilizza Shell per creare o rinominare un gruppo di distribuzione, i criteri vengono applicati a meno che si utilizzi il parametro *IgnoreNamingPolicy* per ignorarli. Per ulteriori informazioni, vedere:
    
      - [Creare un gruppo di distribuzione dei criteri di denominazione](create-a-distribution-group-naming-policy-exchange-2013-help.md)
    
      - [Eseguire l'override del gruppo di distribuzione dei criteri di denominazione](override-the-distribution-group-naming-policy-exchange-2013-help.md)

## Operazione desiderata

## Creare un gruppo di distribuzione

## Utilizzo di EAC per creare un gruppo di distribuzione

1.  In Interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Gruppi**.

2.  Fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") \> **Gruppo di distribuzione**.

3.  > [!TIP]
    > <IMG title="Nuovi gruppi di Office 365" alt="Nuovi gruppi di Office 365" src="images/Bb124513.3ea82c95-9dda-450f-823b-cd0772249d81(EXCHG.150).png"><BR>È ora possibile creare un gruppo di Office 365 anziché un gruppo di distribuzione, se si dispone di un piano per le aziende di Office 365 o di un piano Exchange Online. I gruppi di Office 365 dispongono delle caratteristiche di un gruppo di distribuzione e molte altre. Con i gruppi di Office 365, è possibile inviare messaggi di posta elettronica a un gruppo, condividere un calendario comune, avere una raccolta per archiviare e utilizzare file e cartelle di gruppo. Fare clic su <STRONG>Nuovo</STRONG><IMG title="Icona Aggiungi" alt="Icona Aggiungi" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif">&nbsp;&gt;&nbsp;<STRONG>Gruppo di Office 365</STRONG> per iniziare e consultare la <A href="https://go.microsoft.com/fwlink/p/?linkid=800653">guida per amministratori sui gruppi di Office 365</A>.<BR>Se si dispone di gruppi di distribuzione esistenti che si desidera migrare ai gruppi di Office 365, consultare la <A href="https://go.microsoft.com/fwlink/p/?linkid=824756">guida per amministratori sulla migrazione delle liste di distribuzione ai gruppi di Office 365</A>.<BR>Se si desidera creare un gruppo di distribuzione, selezionare o toccare la procedura guidata <STRONG>Nuovo gruppo di distribuzione</STRONG>.



4.  Nella pagina **Nuovo gruppo di distribuzione**, completare le caselle seguenti:
    
      - \* **Nome visualizzato**   Utilizzare questa casella per digitare il nome visualizzato. Questo nome verrà visualizzato nella rubrica dell'organizzazione, nella riga A: quando il messaggio di posta elettronica viene inviato a questo gruppo e nell'elenco Gruppi nell'interfaccia di amministrazione di Exchange. Il nome visualizzato è obbligatorio e deve essere un nome descrittivo facilmente riconoscibile dagli utenti. Inoltre, deve essere univoco nella foresta.
    
      - \* **Alias**   Utilizzare questa casella per digitare il nome dell'alias per il gruppo. L'alias non può contenere più di 64 caratteri e deve essere univoco nella foresta. Quando un utente digita l'alias nella riga A: di un messaggio di posta elettronica, questo si risolve nel nome visualizzato del gruppo.
    
      - **Unità organizzativa**   (opzione disponibile solo in Exchange 2013 locale) È possibile selezionare un'unità organizzativa diversa da quella predefinita (che corrisponde all'ambito dei destinatari). Se l'ambito dei destinatari è impostato a livello di foresta, il valore predefinito è impostato sul contenitore di utenti nel dominio di Active Directory contenente il computer su cui è in esecuzione l'interfaccia di amministrazione di Exchange. Se l'ambito dei destinatari viene impostato su un dominio specifico, per impostazione predefinita verrà selezionato il contenitore di utenti del dominio in questione. Se infine come ambito dei destinatari si sceglie una specifica unità organizzativa, per impostazione predefinita verrà selezionata l'unità organizzativa specificata.
        
        Per selezionare un'unità organizzativa diversa, scegliere il pulsante **Sfoglia**. La finestra di dialogo visualizzerà tutte le unità organizzative presenti nella foresta all'interno dell'ambito specificato. Selezionare l'unità organizzativa desiderata e fare clic su **OK**.
    
      - \* **Proprietari**   Per impostazione predefinita, l'utente che crea un gruppo ne diventa proprietario. Ogni gruppo deve presentare almeno un proprietario. È possibile aggiungere proprietari facendo clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").
    
      - **Membri**   Utilizzare questa sezione per aggiungere membri e specificare se è necessaria l'approvazione per unirsi al gruppo o abbandonarlo.
        
        I proprietari di un gruppo non sono tenuti a esserne membri. Utilizzare **Aggiungi proprietari di gruppi come membri** per aggiungere o rimuovere i proprietari come membri.
        
        Per aggiungere membri al gruppo, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Al termine dell'aggiunta dei membri, fare clic su **OK** per tornare alla pagina **Nuovo gruppo di distribuzione**.
        
        In **Scegli se è necessaria l'approvazione del proprietario per unirsi al gruppo** specificare se è necessaria l'approvazione degli utenti per unirsi al gruppo. Selezionare una delle impostazioni seguenti:
        
          - **Aperto: qualsiasi utente può unirsi a questo gruppo senza l'approvazione dei proprietari**   È l'impostazione predefinita.
        
          - **Chiuso: i membri possono essere aggiunti solo dai proprietari del gruppo. Tutte le richieste di partecipazione saranno automaticamente rifiutate**
        
          - **Approvazione proprietario: tutte le richieste vengono approvate o rifiutate manualmente dai proprietari dei gruppi.**   Se si seleziona questa opzione, il proprietario o i proprietari del gruppo di distribuzione ricevono un messaggio di posta elettronica in cui si richiede di approvare la richiesta di aggiunta al gruppo.
        
        In **Scegliere se il gruppo è aperto per uscire** specificare se è necessaria l'approvazione degli utenti per lasciare il gruppo. Selezionare una delle impostazioni seguenti:
        
          - **Aperto: qualsiasi utente può lasciare questo gruppo senza l'approvazione dei proprietari**   È l'impostazione predefinita.
        
          - **Chiuso: i membri possono essere rimossi solo dai proprietari del gruppo. Tutte le richieste di lasciare il gruppo verranno rifiutate automaticamente**

5.  Al termine fare clic su **Salva** per creare il gruppo di distribuzione.


> [!NOTE]
> Per impostazione predefinita, i nuovi gruppi di distribuzione richiedono l'autenticazione di tutti i mittenti. Questo impedisce ai mittenti esterni di inviare messaggi ai gruppi di distribuzione. Per consentire a un gruppo di distribuzione di accettare i messaggi da tutti i mittenti, occorre modificare le impostazioni di restrizione di recapito dei messaggi per il dato gruppo di distribuzione.



## Utilizzo della shell per creare un gruppo di distribuzione

In questo esempio viene creato un gruppo di distribuzione con alias **itadmin** e nome **IT Administrators**. Il gruppo di distribuzione viene creato nell'unità organizzativa predefinita: tutti possono unirsi senza l'approvazione dei proprietari del gruppo.

    New-DistributionGroup -Name "IT Administrators" -Alias itadmin -MemberJoinRestriction open

Per ulteriori informazioni sull'utilizzo di Shell per creare gruppi di distribuzione, vedere [New-DistributionGroup](https://technet.microsoft.com/it-it/library/aa998856\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione di un gruppo di distribuzione, effettuare una delle seguenti operazioni:

  - In Interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Gruppi**. Il nuovo gruppo di distribuzione viene visualizzato nell'elenco dei gruppi. In **Tipo di gruppo** il tipo è **Gruppo di distribuzione**.

  - In Shell eseguire il comando seguente per visualizzare le informazioni sul nuovo gruppo di distribuzione.
    
        Get-DistributionGroup <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress


> [!NOTE]
> È possibile creare o abilitare alla posta elettronica solo i gruppi di distribuzione universali. Per convertire un gruppo globale o locale al dominio in un gruppo universale, è possibile utilizzare il cmdlet <A href="https://technet.microsoft.com/it-it/library/bb123770(v=exchg.150)">Set-Group</A> in Shell. Possono essere disponibili gruppi abilitati alla posta migrati da versioni precedenti di Exchange&nbsp;che non sono gruppi universali. Per gestire questi gruppi, è possibile utilizzare EAC o Shell



## Modifica delle proprietà del gruppo di distribuzione

## Utilizzo di EAC per modificare le proprietà del gruppo di distribuzione

1.  In Interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Gruppi**.

2.  Nell'elenco dei gruppi fare clic sul gruppo di distribuzione che si desidera visualizzare o modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del gruppo, fare clic su una delle sezioni indicate di seguito per visualizzare o modificare le proprietà.
    
      - Generale
    
      - Proprietà
    
      - Appartenenza
    
      - Approvazione dell'appartenenza
    
      - Gestione recapito
    
      - Approvazione del messaggio
    
      - Opzioni di posta elettronica
    
      - MailTip
    
      - Delega gruppo

## Generale

Utilizzare questa sezione per visualizzare o modificare le informazioni di base sul gruppo.

  - \* **Nome visualizzato**   Questo nome verrà visualizzato nella Rubrica, nei campi A: quando il messaggio di posta elettronica viene inviato a questo gruppo e nell'elenco Gruppi. Il nome visualizzato è obbligatorio e deve essere un nome descrittivo facilmente riconoscibile dagli utenti. Inoltre, deve essere univoco nel dominio in uso.
    
    Se sono stati implementati criteri di denominazione dei gruppi, il nome visualizzato deve essere conforme al formato di denominazione definito dai criteri.

  - \* **Alias**   Questa è la parte dell'indirizzo di posta elettronica visualizzata a sinistra del simbolo di chiocciola (@). Se si modifica l'alias, verrà modificato anche l'indirizzo SMTP primario del gruppo in modo che contenga il nuovo alias. Inoltre, l'indirizzo di posta elettronica con il precedente alias verrà conservato come indirizzo proxy del gruppo.

  - **Descrizione**   Utilizzare questa casella per descrivere lo scopo del gruppo. Questa descrizione viene visualizzata nella rubrica e nel riquadro Dettagli dell'interfaccia di amministrazione di Exchange.

  - **Nascondi il gruppo dagli elenchi di indirizzi**   Selezionare questa casella di controllo per evitare che gli utenti vedano questo gruppo nella rubrica. Per inviare un messaggio di posta elettronica a questo gruppo, il mittente deve digitare l'alias o l'indirizzo di posta elettronica del gruppo nella riga A: o Cc: .
    

    > [!TIP]
    > Può essere opportuno nascondere i gruppi di sicurezza, in quanto vengono in genere utilizzati per assegnare autorizzazioni ai membri del gruppo e non per inviare messaggi di posta elettronica.



  - **Unità organizzativa**   Questa casella di sola lettura visualizza l'unità organizzativa (OU) contenente il gruppo di distribuzione. È necessario utilizzare Utenti e computer di Active Directory per spostare il gruppo in un'altra unità organizzativa.

## Ownership

Utilizzare questa sezione per assegnare i proprietari del gruppo. Il proprietario del gruppo può aggiungere membri al gruppo nonché approvare o rifiutare le richieste di partecipazione o di abbandono del gruppo e i messaggi inviati al gruppo. Per impostazione predefinita, la persona che crea un gruppo ne diventa proprietario. Ogni gruppo deve presentare almeno un proprietario.

È possibile aggiungere proprietari facendo clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). È possibile rimuovere un proprietario selezionandolo e facendo clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

## Appartenenza

Utilizzare questa sezione per aggiungere o rimuovere membri. I proprietari di un gruppo non sono tenuti a esserne membri. Nella sezione **Membri**, è possibile aggiungere i membri facendo clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per rimuovere un membro è possibile selezionare un utente nell'elenco dei membri e fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

## Approvazione dell'appartenenza

Utilizzare questa sezione per specificare se è necessaria l'approvazione per unirsi al gruppo o abbandonarlo.

  - **Scegliere se è necessaria l'approvazione del proprietario per aggiungersi al gruppo**   Selezionare una delle impostazioni seguenti:
    
      - **Aperto: qualsiasi utente può partecipare a questo gruppo senza approvazione da parte dei proprietari**
    
      - **Chiuso: i membri possono essere aggiunti solo dai proprietari del gruppo. Tutte le richieste di partecipazione saranno automaticamente rifiutate**
    
      - **Approvazione proprietario: tutte le richieste vengono approvate o rifiutate dai proprietari dei gruppi.**   Se si seleziona questa opzione, il proprietario o i proprietari del gruppo ricevono un messaggio di posta elettronica in cui si richiede di approvare la richiesta di aggiunta al gruppo.

  - **Scegliere se il gruppo è aperto per uscire**   Selezionare una delle impostazioni seguenti:
    
      - **Aperto: chiunque può lasciare il gruppo senza l'approvazione dei proprietari del gruppo**
    
      - **Chiuso: i membri possono essere rimossi solo dai proprietari del gruppo. Tutte le richieste di lasciare il gruppo verranno rifiutate automaticamente**

## Gestione recapito

Utilizzare questa sezione per gestire gli utenti che possono inviare posta elettronica a questo gruppo.

  - **Solo mittenti interni all'organizzazione**   Selezionare questa opzione per consentire l'invio di messaggi al gruppo solo ai mittenti dell'organizzazione. In questo modo, se un utente esterno all'organizzazione invia un messaggio di posta elettronica a questo gruppo, tale messaggio sarà rifiutato. Questa impostazione è quella predefinita.

  - **Mittenti interni ed esterni all'organizzazione**   Selezionare questa opzione per consentire a tutti di inviare i messaggi al gruppo.
    
    È possibile limitare ulteriormente gli utenti che possono inviare messaggi al gruppo consentendo solo a mittenti specifici di inviare messaggi a questo gruppo. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e quindi selezionare uno o più destinatari. I mittenti aggiunti a questo elenco saranno i soli a poter inviare posta al gruppo. I messaggi inviati da chiunque non sia presente nell'elenco verranno rifiutati.
    
    Per rimuovere un utente o un gruppo dall'elenco, selezionarlo nell'elenco, quindi fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").
    

    > [!IMPORTANT]
    > Se il gruppo è stato configurato per consentire l'invio di messaggi al gruppo solo da parte di mittenti all'interno dell'organizzazione, i messaggi di posta elettronica inviati da un contatto di posta verranno rifiutati, anche se viene aggiunto a questo elenco.



## Approvazione del messaggio

Utilizzare questa sezione per impostare le opzioni di moderazione del gruppo. I moderatori approvano o rifiutano i messaggi inviati al gruppo prima che raggiungano i membri del gruppo.

  - **I messaggi inviati a questo gruppo sono stati approvati da un moderatore**   Per impostazione predefinita, questa casella di controllo non è selezionata. Se si seleziona questa casella di controllo, i moderatori del gruppo esaminano i messaggi in arrivo prima di procedere al relativo recapito. I moderatori del gruppo possono approvare o rifiutare i messaggi in arrivo.

  - **Moderatori del gruppo**   Per aggiungere moderatori al gruppo, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per rimuovere un moderatore, selezionarlo, quindi fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi"). Se è stata selezionata l'opzione "I messaggi inviati a questo gruppo sono stati approvati da un moderatore" senza tuttavia aver selezionato alcun moderatore, i messaggi destinati al gruppo verranno inviati ai proprietari del gruppo per l'approvazione.

  - **Mittenti che non richiedono l'approvazione dei messaggi**    Per aggiungere utenti o gruppi in grado di ignorare la moderazione del gruppo, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per rimuovere una utente o un gruppo, selezionarlo e fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

  - **Seleziona notifiche di moderazione**   Utilizzare questa sezione per stabilire in che modo gli utenti vengono avvisati dell'approvazione del messaggio.
    
      - **Notificare a tutti i mittenti che i loro messaggi non sono stati approvati**   Questa è l'impostazione predefinita. Consente di notificare qualsiasi mittente, sia esso interno o esterno all'organizzazione, in merito alla non approvazione del messaggio che ha inviato.
    
      - **Notifica ai mittenti nell'organizzazione se i rispettivi messaggi non vengono approvati**   Selezionando questa opzione, solo gli utenti o i gruppi nell'organizzazione ricevono una notifica quando un messaggio che hanno inviato al gruppo non viene approvato da un moderatore.
    
      - **Non inviare alcuna notifica quando un messaggio non è approvato**   Se si seleziona questa opzione, non vengono inviate notifiche ai mittenti quando i loro messaggi non vengono approvati dai moderatori del gruppo.

## Opzioni di posta elettronica

Utilizzare questa sezione per visualizzare o modificare gli indirizzi di posta elettronica associati al gruppo. Ciò include gli indirizzi SMTP primari del gruppo e qualsiasi indirizzo proxy ad esso associato. L'indirizzo SMTP primario (chiamato anche *indirizzo di risposta*) viene visualizzato in grassetto nell'elenco degli indirizzi, con il valore **SMTP** maiuscolo nella colonna **Tipo**.

  - **Aggiungi**  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere un nuovo indirizzo di posta elettronica per la cassetta postale. Selezionare uno dei seguenti tipi di indirizzo:
    
      - **SMTP**   Questo è il tipo di indirizzo predefinito. Fare clic su questo pulsante e quindi digitare il nuovo indirizzo SMTP nella casella \* **Indirizzo di posta elettronica**.
        

        > [!NOTE]
        > Per impostare il nuovo indirizzo SMTP come primario per il gruppo, selezionare la casella di controllo <STRONG>Imposta questo indirizzo come indirizzo di risposta</STRONG>.

    
      - **Tipo di indirizzo personalizzato**   Fare clic su questo pulsante e digitare uno dei tipi di indirizzi di posta elettronica non SMTP supportati nella casella \* **Indirizzo di posta elettronica**.
        

        > [!NOTE]
        > Fatta eccezione per gli indirizzi X.400, Exchange non convalida gli indirizzi personalizzati per verificarne la corretta formattazione. È necessario verificare che l'indirizzo personalizzato specificato sia conforme ai requisiti di formato per tale tipo di indirizzo.



  - **Modifica**   Per cambiare un indirizzo di posta elettronica associato al gruppo, selezionarlo nell'elenco e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    

    > [!NOTE]
    > Per impostare un indirizzo SMTP esistente come primario per il gruppo, selezionare la casella di controllo <STRONG>Imposta questo indirizzo come indirizzo di risposta</STRONG>.



  - **Rimuovi**   Per eliminare un indirizzo di posta elettronica associato al gruppo, selezionarlo nell'elenco e fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

  - **Aggiorna automaticamente gli indirizzi sulla base del criterio dell'indirizzo di posta elettronica applicato a questo destinatario**   Selezionare questa casella di controllo per aggiornare automaticamente gli indirizzi di posta elettronica dei destinatari in base alle modifiche apportate ai criteri degli indirizzi di posta elettronica nell'organizzazione. Tale casella è selezionata per impostazione predefinita.

## MailTip

Utilizzare questa sezione per aggiungere un avviso per informare gli utenti dei problemi che potrebbero verificarsi se inviano un messaggio a questo gruppo. Un avviso messaggio è un testo che viene visualizzato sulla barra informazioni quando questo gruppo viene aggiunto nella riga A, Cc o Ccn di un nuovo messaggio di posta elettronica. Ad esempio, è possibile aggiungere un Avviso messaggio ai gruppi di grandi dimensioni per avvertire i mittenti potenziali che il messaggio verrà inviato a molte persone.


> [!NOTE]
> Gli avvisi messaggio possono includere tag HTML, ma gli script non sono consentiti. La lunghezza di un avviso messaggio personalizzato non può superare 175 caratteri visualizzati. I tag HTML non vengono conteggiati in tale limite.



## Delega gruppo

Utilizzare questa sezione per assegnare a un utente (chiamato *delegato*) le autorizzazioni necessarie per permettergli di inviare messaggi come gruppo o per conto del gruppo. È possibile assegnare le seguenti autorizzazioni:

  - **Invia come**   Questa autorizzazione consente al delegato di inviare i messaggi come gruppo. Una volta assegnata l'autorizzazione, il delegato può scegliere di aggiungere il gruppo nella riga **Da** per indicare che il messaggio è stato inviato dal gruppo.

  - **Invia per conto di**   Anche questa autorizzazione consente a un delegato di inviare messaggi per conto del gruppo. Una volta assegnata questa autorizzazione, il delegato ha la possibilità di aggiungere il gruppo alla riga **Da**. Il messaggio risulterà essere stato inviato dal gruppo e indicherà che è stato inviato dal delegato per conto del gruppo.

Per assegnare le autorizzazioni ai delegati, fare clic su **Aggiungi** sotto l'autorizzazione desiderata per visualizzare la pagina **Scegli il destinatario** che contiene un elenco di destinatari nell'organizzazione Exchange a cui può essere assegnata l'autorizzazione. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare uno specifico destinatario digitandone il nome nella casella di ricerca e quindi facendo clic su **Cerca**.

## Utilizzo di Shell per modificare le proprietà del gruppo di distribuzione

Utilizzare i cmdlet **Get-DistributionGroup** e **Set-DistributionGroup** per visualizzare e modificare le proprietà per i gruppi di distribuzione. I vantaggi dell'utilizzo di Shell comprendono la capacità di modificare le proprietà non disponibili in EAC e di modificare le proprietà per più gruppi. Per informazioni sui parametri corrispondenti alle proprietà del gruppo di distribuzione, consultare i seguenti argomenti:

  - [Get-DistributionGroup](https://technet.microsoft.com/it-it/library/bb124755\(v=exchg.150\))

  - [Set-DistributionGroup](https://technet.microsoft.com/it-it/library/bb124955\(v=exchg.150\))

Di seguito sono riportati alcuni esempi sull'utilizzo di Shell per modificare le proprietà del gruppo di distribuzione.

In questo esempio viene modificato l'indirizzo SMTP primario (denominato anche indirizzo di risposta) per il gruppo di distribuzione Seattle Employees da employees@contoso.com a sea.employees@contoso.com. L'indirizzo di risposta precedente verrà inoltre mantenuto come indirizzo proxy.

    Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.employees@contoso.com,smtp:employees@contoso.com

In questo esempio viene limitata a 10 MB la dimensione massima dei messaggi che possono essere inviati a tutti i gruppi di distribuzione nell'organizzazione.

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalDistributionGroup')} | Set-DistributionGroup -MaxReceiveSize 10MB

In questo esempio viene abilitata la moderazione per il gruppo di distribuzione Customer Support, impostando Amy come moderatore. Inoltre, questo gruppo di distribuzione moderato avviserà i mittenti che inviano posta dall'organizzazione nel caso in cui i rispettivi messaggi non vengano approvati.

    Set-DistributionGroup -Identity "Customer Support" -ModeratedBy "Amy" -ModerationEnabled $true -SendModerationNotifications 'Internal'

In questo esempio viene modificato il gruppo di distribuzione creato dall'utente Dog Lovers in modo che richieda al gestore del gruppo di approvare le richieste degli utenti di iscrizione al gruppo. Inoltre, utilizzando il parametro *BypassSecurityGroupManagerCheck*, il gestore del gruppo non sarà avvisato quando vengono apportate modifiche alle impostazioni del gruppo di distribuzione.

    Set-DistributionGroup -Identity "Dog Lovers" -MemberJoinRestriction 'ApprovalRequired' -BypassSecurityGroupManagerCheck

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver modificato correttamente le proprietà di un gruppo di distribuzione, effettuare le operazioni seguenti:

  - Nell'interfaccia di amministrazione di Exchange, selezionare il gruppo e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare la proprietà o la funzionalità modificata. A seconda della proprietà modificata, è possibile che questa venga visualizzata nel riquadro Dettagli del gruppo selezionato.

  - In Shell, utilizzare il cmdlet **Get-DistributionGroup** per verificare le modifiche. Uno dei vantaggi offerti dall'utilizzo di Shell è la possibilità di visualizzare più proprietà per più gruppi. Nell'esempio precedente, in cui è stato modificato il numero massimo di destinatari, eseguire questo comando per verificare il nuovo valore.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,RecipientLimits
    
    Nell'esempio in alto in cui sono stati modificati i limiti dei messaggi, eseguire questo comando.
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults


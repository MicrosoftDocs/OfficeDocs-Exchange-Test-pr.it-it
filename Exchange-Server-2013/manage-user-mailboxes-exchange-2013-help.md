---
title: 'Gestire le cassette postali degli utenti: Exchange 2013 Help'
TOCTitle: Gestire le cassette postali degli utenti
ms:assetid: 957ca61c-1fa1-42ab-a0e6-8488e4782566
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123809(v=EXCHG.150)
ms:contentKeyID: 50481238
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailboxWizardForm.NewMailboxIntroductionWizardPage
ms.translationtype: HT
---

# Gestire le cassette postali degli utenti

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-05-27_

Dopo aver creato una cassetta postale utente, è possibile apportare eventuali modifiche e impostare proprietà aggiuntive utilizzando l'interfaccia di amministrazione di Exchange o la shell.

È inoltre possibile modificare le proprietà di più cassette postali utente contemporaneamente. Per ulteriori informazioni, vedere Modifica in blocco delle cassette postali utente.

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ogni attività per la cassetta postale utente: 2-5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Modificare le proprietà della cassetta postale utente

## Utilizzare EAC per modificare le proprietà delle cassette postali utente

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale di cui si desidera cambiare le proprietà, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Sulla pagina delle proprietà della cassetta postale, fare clic su una delle seguenti sezioni per visualizzare o modificare le proprietà.
    
      - Generale
    
      - Utilizzo cassetta postale
    
      - Informazioni di contatto
    
      - Organizzazione
    
      - Indirizzo di posta elettronica
    
      - Funzionalità delle cassette postali
    
      - Membro di
    
      - Avviso messaggio
    
      - Delega cassetta postale

## Generale

Utilizzare la sezione **Generale** per visualizzare o modificare le informazioni di base sull'utente.

  - **Nome**, **Iniziali**, **Cognome**

  - **\* Nome**   Questo è il nome che compare in Active Directory. Se viene modificato, non può superare i 64 caratteri.

  - **\* Nome visualizzato** Questo nome viene visualizzato nella Rubrica dell'organizzazione, nel campo A e Da: dei messaggi di posta elettronica e nell'elenco delle cassette postali. Questo nome non può contenere spazi vuoti prima o dopo il nome visualizzato.

  - **\* Alias**   Specifica l'alias di posta elettronica per l'utente. L'alias dell'utente è la parte dell'indirizzo di posta elettronica a sinistra del simbolo di chiocciola (@). Deve essere univoco nella foresta.

  - **\* Nome accesso utente**   È il nome utilizzato dall'utente per accedere alla cassetta postale e al dominio. In genere il nome di accesso utente è costituito dall'alias dell'utente a sinistra del simbolo @ e dal nome di dominio in cui risiede l'account sul lato destro del simbolo @.
    

    > [!NOTE]
    > Questa casella è etichettata come <STRONG>ID utente</STRONG> in Exchange Online.



  - **Richiedi modifica della password al successivo accesso**   Selezionare questa casella di controllo se si desidera che l'utente reimposti la sua password al successivo accesso alla cassetta postale.
    

    > [!NOTE]
    > In Exchange Online questa casella di controllo non è disponibile.



  - **Non visualizzare negli elenchi di indirizzi**   Selezionare questa casella di controllo per impedire la visualizzazione del destinatario nella rubrica e negli altri elenchi indirizzi globale definiti nell'organizzazione di Exchange. Dopo la selezione di questa casella di controllo, gli utenti possono comunque inviare messaggi al destinatario utilizzando l'indirizzo di posta elettronica.

Fare clic su **Altre opzioni** per visualizzare o modificare le seguenti proprietà aggiuntive:

  - **Unità organizzativa**   In questa casella di sola lettura è visualizzata l'unità organizzativa contenente l'account utente. È necessario utilizzare Utenti e computer di Active Directory per spostare l'account utente in un'altra unità organizzativa.
    

    > [!NOTE]
    > In Exchange Online questa casella non è disponibile.



  - **Database delle cassette postali**   In questa casella di sola lettura è visualizzato il nome del database che ospita la cassetta postale. Per spostare la cassetta postale in un database diverso, selezionarla nell'elenco delle cassette postali e fare clic su **Sposta cassetta postale in un altro database** nel riquadro dei dettagli.
    

    > [!NOTE]
    > In Exchange Online quest'opzione non è disponibile.



  - **Attributi personalizzati**   In questa sezione sono visualizzati gli attributi personalizzati definiti per la cassetta postale utente. Per specificare valori di attributo personalizzati, fare clic su **Modifica**. È possibile specificare fino a 15 attributi personalizzati per un destinatario.

## Utilizzo cassetta postale

Fare clic su **Utilizzo cassetta postale** per visualizzare o modificare la quota di archiviazione della cassetta postale e le impostazioni di conservazione degli elementi eliminati per la cassetta postale. Queste impostazioni vengono configurate per impostazione predefinita durante la creazione della cassetta postale. Utilizzano i valori configurati per il database delle cassette postali e li applicano a tutte le cassette postali in quel database. È possibile personalizzare queste impostazioni per ciascuna cassetta postale invece che utilizzare i valori predefiniti del database delle cassette postali.

  - **Ultimo accesso**   Questa casella di sola lettura visualizza l'ora in cui l'utente ha effettuato l'accesso per l'ultima volta alla sua cassetta postale.

  - **Uso della cassetta postale**   In quest'area è indicata la dimensione totale della cassetta postale e la percentuale della quota totale che è stata utilizzata.


> [!NOTE]
> Per ottenere le informazioni visualizzate nelle due precedenti caselle, l'interfaccia di amministrazione di Exchange esegue una query nel database delle cassette postali che ospita la cassetta postale. Se EAC non è in grado di comunicare con l'archivio di Exchange contenente il database delle cassette postali, queste caselle saranno vuote. Se l'utente non ha eseguito l'accesso alla cassetta postale per la prima volta, viene visualizzato un messaggio di avviso.



Fare clic su **Altre opzioni** per visualizzare o modificare la quota di archiviazione della cassetta postale e le impostazioni di conservazione degli elementi nella cassetta postale.


> [!NOTE]
> Queste impostazioni non sono disponibili nell'interfaccia di amministrazione di Exchange in Exchange Online.



  - **Impostazioni quota di archiviazione**   Per personalizzare queste impostazioni per la cassetta postale, anziché utilizzare le impostazioni predefinite del database delle cassette postali, fare clic su **Personalizza le impostazioni per questa cassetta postale**, digitare un nuovo valore e fare clic su **Salva**.
    
    L'intervallo di valori per le impostazioni della quota di archiviazione è compreso tra 0 e 2047 GB.
    
      - **Invia un avviso in corrispondenza di (GB)**   Questa casella indica il limite massimo di archiviazione che è possibile raggiungere prima che venga inviato un messaggio di avviso. Se la dimensione della cassetta postale raggiunge o supera il valore specificato, Exchange invia un avviso all'utente.
    
      - **Non consentire l'invio di (GB)**   Questa casella indica il limite di *invio non consentito* per la cassetta postale. Se la dimensione della cassetta postale raggiunge o supera il limite specificato, Exchange impedisce all'utente di inviare nuovi messaggi e visualizza un messaggio di errore descrittivo.
    
      - **Non consentire l'invio e la ricezione di (GB)**   Questa casella indica il limite di *invio e ricezione non consentiti* per la cassetta postale. Se la dimensione della cassetta postale raggiunge o supera il limite specificato, Exchange impedisce all'utente della cassetta postale di inviare nuovi messaggi e non recapiterà i nuovi messaggi alla cassetta postale. Tutti i messaggi inviati alla cassetta postale vengono restituiti al mittente con un messaggio di errore descrittivo.

  - **Impostazioni di mantenimento elementi eliminati**   Per personalizzare queste impostazioni per la cassetta postale, anziché utilizzare le impostazioni predefinite del database delle cassette postali, fare clic su **Personalizza le impostazioni per questa cassetta postale**, digitare un nuovo valore e fare clic su **Salva**.
    
      - **Conserva elementi eliminati per (giorni)**   Questa casella indica per quanto tempo gli elementi eliminati vengono conservati prima di essere eliminati definitivamente e non essere più recuperabili dall'utente. Durante la creazione della cassetta postale, questo valore si basa sulle impostazioni di conservazione degli elementi eliminati configurate per il database delle cassette postali. Per impostazione predefinita, la conservazione degli elementi eliminati in un database delle cassette postali è impostata su 14 giorni. L'intervallo di valori per questa proprietà è compreso fra 0 e 24855 giorni.
    
      - **Non eliminare definitivamente questi elementi prima di aver creato una copia di backup del database**   Selezionare questa casella di controllo per impedire che le cassette postali e i messaggi di posta elettronica vengano eliminati prima che sia stato eseguito il backup del database in cui si trova la cassetta postale in questione.

## Informazioni di contatto

Utilizzare la sezione **Informazioni di contatto** per visualizzare o modificare le informazioni di contatto dell'utente. Le informazioni di questa pagina vengono visualizzate nella Rubrica. Fare clic su **Altre opzioni** per visualizzare caselle aggiuntive.


> [!TIP]
> Il campo <STRONG>Stato/provincia</STRONG> consente di creare le condizioni relative ai destinatari per i gruppi di distribuzione dinamici, i criteri per gli indirizzi di posta elettronica o gli elenchi di indirizzi.



Gli utenti della cassetta postale possono utilizzare Outlook o Outlook Web App per visualizzare e modificare le loro informazioni sul contatto. Tuttavia, non possono modificare le informazioni nelle caselle **Note** e **Pagina Web**.

## Organizzazione

Utilizzare la sezione **Organizzazione** per registrare informazioni dettagliate sul ruolo dell'utente nell'organizzazione. Queste informazioni vengono visualizzate nella rubrica. Inoltre, è possibile creare un organigramma virtuale accessibile dai client di posta elettronica come Outlook.

  - **Titolo   **Questa casella di testo consente di visualizzare o modificare il titolo del destinatario.

  - **Reparto**   Utilizzare questa casella per visualizzare o modificare il nome del reparto in cui lavora l'utente. È possibile utilizzare questa casella per creare le condizioni relative ai destinatari per i gruppi di distribuzione dinamici, i criteri per gli indirizzi di posta elettronica o gli elenchi di indirizzi.

  - **Società**   Utilizzare questa casella per visualizzare o modificare il nome della società in cui lavora l'utente. È possibile utilizzare questa casella per creare le condizioni relative ai destinatari per i gruppi di distribuzione dinamici, i criteri per gli indirizzi di posta elettronica o gli elenchi di indirizzi.

  - **Manager**   Per aggiungere un manager, fare clic su **Sfoglia**. In **Seleziona responsabile**, selezionare una persona e quindi fare clic su **OK**.

  - **Superiore diretto**   Questo campo non può essere modificato. Un *subalterno* è un utente che risponde a un manager specifico. Se è stato specificato un responsabile per l'utente, quest'ultimo verrà visualizzato come subalterno nei dettagli della cassetta postale del responsabile. Ad esempio, Kari è responsabile di Chris e Kate, quindi la cassetta postale di Kari è specificata nella casella **Manager** della cassetta postale di Chris e di Kate, mentre Chris e Kate compaiono nella casella **Subalterni** nelle proprietà della cassetta postale di Kari.

## Indirizzo di posta elettronica

Utilizzare la sezione **Indirizzi di posta elettronica** per visualizzare o modificare gli indirizzi di posta elettronica associati alla cassetta postale utente. Sono inclusi l'indirizzo SMTP primario dell'utente e qualsiasi indirizzo proxy associato. L'indirizzo SMTP primario (chiamato anche *indirizzo di risposta predefinito*) viene visualizzato in grassetto nell'elenco degli indirizzi, con il valore **SMTP** maiuscolo nella colonna **Tipo**.

  - **Aggiungi **  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere un nuovo indirizzo di posta elettronica per la cassetta postale. Selezionare uno dei seguenti tipi di indirizzo:
    
      - **SMTP**   Questo è il tipo di indirizzo predefinito. Fare clic su questo pulsante e quindi digitare il nuovo indirizzo SMTP nella casella **\* Indirizzo di posta elettronica**.
    
      - **Messaggistica unificata di Exchange**   Un indirizzo di messaggistica unificata di Exchange viene utilizzato dal servizio di messaggistica unificata di Microsoft Exchange per individuare gli utenti abilitati alla messaggistica unificata all'interno dell'organizzazione Exchange. L'indirizzo di messaggistica unificata di Exchange è costituito dal numero di interno e dal dial plan per l'utente abilitato alla messaggistica unificata. Fare clic su questo pulsante e digitare il numero di telefono interno nella casella **Indirizzo/Estensione**. Quindi fare clic su **Sfoglia** e selezionare un dial plan per l'utente.
    
      - **Tipo di indirizzo personalizzato**   Fare clic su questo pulsante e digitare uno dei tipi di indirizzi di posta elettronica non SMTP supportati nella casella **\* Indirizzo di posta elettronica**.
        

        > [!NOTE]
        > Ad eccezione degli indirizzi X.400, Exchange non convalida gli indirizzi personalizzati per una formattazione corretta. È necessario verificare che l'indirizzo personalizzato specificato sia conforme ai requisiti di formato per tale tipo di indirizzo.

    
      - **Imposta come indirizzo di risposta**   In Exchange Online, è possibile selezionare questa casella di controllo per rendere il nuovo indirizzo di posta elettronica l'indirizzo SMTP principale della cassetta postale. Questa casella di controllo non è disponibile nell'interfaccia di amministrazione di Exchange in Exchange 2013.

  - **Aggiorna automaticamente gli indirizzi sulla base del criterio dell'indirizzo di posta elettronica applicato a questo destinatario   **Selezionare questa casella di controllo per aggiornare automaticamente gli indirizzi di posta elettronica dei destinatari in base alle modifiche apportate ai criteri degli indirizzi di posta elettronica nell'organizzazione. Tale casella è selezionata per impostazione predefinita.
    

    > [!NOTE]
    > In Exchange Online questa casella di controllo non è disponibile.



  - **Imposta come indirizzo di risposta**

## Funzionalità delle cassette postali

Utilizzare la sezione **Funzionalità delle cassette postali** per visualizzare o modificare le seguenti funzionalità e impostazioni delle cassette postali:

  - **Criterio di condivisione**   Questa casella indica il criterio di condivisione applicato alla cassetta postale. Il criterio di condivisione controlla la modalità di condivisione delle informazioni del calendario e dei contatti tra gli utenti nell'organizzazione e quelli esterni all'organizzazione Exchange. Il criterio di condivisione predefinito viene assegnato alle cassette postali al momento della loro creazione. Per modificare il criterio di condivisione assegnato all'utente, selezionare il criterio desiderato nell'elenco a discesa.

  - **Criterio di assegnazione dei ruoli**   Questa casella indica il criterio di assegnazione dei ruoli assegnato alla cassetta postale. I criteri di assegnazione dei ruoli specificano i ruoli di controllo di accesso basato su ruoli (RBAC) assegnati all'utente e controllano le specifiche impostazioni di configurazione della cassetta postale e del gruppo di distribuzione che gli utenti possono modificare. Per modificare il criterio di assegnazione dei ruoli assegnato all'utente, selezionare il criterio desiderato nell'elenco a discesa.

  - **Criterio di conservazione**   Questa casella indica il criterio di conservazione applicato alla cassetta postale. Un criterio di conservazione è costituito da un gruppo di tag di conservazione applicate alla cassetta postale dell'utente. Consentono di controllare il periodo di conservazione degli elementi nelle cassette postali degli utenti e definire l'azione da eseguire sugli elementi che hanno raggiunto un determinato limite temporale. Il criterio di conservazione non viene assegnato alle cassette postali al momento della loro creazione. Per assegnare un criterio di conservazione a un utente, selezionarlo nell'elenco a discesa.

  - **Criteri rubrica**   Questa casella mostra il criterio rubrica applicato alla cassetta postale. Un criterio rubrica consente di segmentare gli utenti in gruppi specifici per fornire visualizzazioni personalizzate della rubrica. Per applicare o modificare il criterio rubrica applicato alla cassetta postale, effettuare una selezione nell'elenco a discesa.

  - **Messaggistica unificata**   Questa funzionalità è disabilitata per impostazione predefinita. Quando si abilita la messaggistica unificata, l'utente sarà in grado di utilizzare le funzionalità di messaggistica unificata dell'organizzazione e all'utente sarà applicato un insieme predefinito di proprietà di messaggistica unificata. Fare clic su **Abilita** per abilitare la messaggistica unificata per la cassetta postale. Per informazioni su come abilitare la messaggistica unificata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).
    

    > [!NOTE]
    > Per poter abilitare la messaggistica unificata, è necessario che siano già stati creati un dial plan e un criterio cassetta postale di messaggistica unificata.



  - **Dispositivi mobili**   Utilizzare questa sezione per visualizzare e cambiare le impostazioni di Exchange ActiveSync, abilitato per impostazione predefinita. Exchange ActiveSync consente l'accesso a una cassetta postale di Exchange da un dispositivo mobile. Fare clic su **Disabilita Exchange ActiveSync** per disabilitare questa funzionalità per la cassetta postale.

  - **Outlook Web App**   Questa funzionalità è abilitata per impostazione predefinita. Outlook Web App consente di accedere a una cassetta postale di Exchange da qualsiasi browser. Fare clic su **Disabilita** per disabilitare Outlook Web App per la cassetta postale. Fare clic su **Modifica dettagli** per aggiungere o modificare un criterio cassetta postale di Outlook Web App per la cassetta postale.

  - **IMAP**   Questa funzionalità è abilitata per impostazione predefinita. Fare clic su **Disabilita** per disabilitare la funzionalità IMAP per la cassetta postale.

  - **POP3**   Questa funzionalità è abilitata per impostazione predefinita. Fare clic su **Disabilita** per disabilitare la funzionalità POP3 per la cassetta postale.

  - **MAPI**   Questa funzionalità è abilitata per impostazione predefinita. MAPI consente l'accesso a una cassetta postale di Exchange da un client MAPI, ad esempio Outlook. Fare clic su **Disabilita** per disabilitare la funzionalità MAPI per la cassetta postale.

  - **Conservazione per controversia legale**   Questa funzionalità è disabilitata per impostazione predefinita. La funzionalità di conservazione in caso di dispute consente di mantenere gli elementi eliminati dalla cassetta postale e di registrare le modifiche apportate agli elementi. Gli elementi eliminati e tutte le istanze degli elementi modificati vengono restituiti in una ricerca di individuazione. Fare clic su **Abilita** per abilitare la conservazione per controversia legale della cassetta postale. Se per la cassetta postale è abilitata la conservazione per controversia legale, fare clic su **Disabilita** per annullarla. Le cassette postali bloccate a causa di una controversia sono cassette postali inattive e non possono essere eliminate. Per eliminare la cassetta postale, eliminare la controversia. Se per la cassetta postale è abilitata la conservazione per controversia legale, fare clic su **Modifica dettagli** per visualizzare e modificare le seguenti impostazioni della conservazione:
    
      - **Conserva data**   In questa casella di sola lettura è indicata la data/ora in cui la cassetta postale è stata inserita nella conservazione per controversia legale.
    
      - **Conservazione per controversia legale effettuata da**   In questa casella di sola lettura è indicato l'utente che ha attivato la conservazione.
    
      - **Nota**   Utilizzare questa casella per inviare all'utente una notifica relativa alla conservazione per controversia legale, spiegarne le motivazioni o fornire istruzione aggiuntive, ad esempio per informare l'utente che la conservazione per controversia legale non influirà sull'utilizzo quotidiano della posta elettronica.
    
      - **URL**   Utilizzare questa casella per specificare un URL di un sito Web che fornisce informazioni o istruzioni relative alla conservazione per controversia legale della cassetta postale.
        

        > [!NOTE]
        > Il testo di queste caselle viene visualizzato nella cassetta postale dell'utente solo se utilizza Outlook 2010 o versioni successive. Non viene visualizzato in Outlook Web App o in altri client di posta elettronica. Per visualizzare il testo dei campi Nota e URL in Outlook, fare clic sulla scheda <STRONG>File</STRONG>. Nella pagina <STRONG>Informazioni</STRONG>, sotto <STRONG>Impostazioni account</STRONG>, sarà visibile il commento relativo alla conservazione per controversia legale.



  - **Archiviazione**   Se per l'utente non esiste una cassetta postale di archiviazione, questa funzionalità è disabilitata. Per abilitare una cassetta postale di archiviazione, fare clic su **Abilita**. Se l'utente ha una cassetta postale di archiviazione, ne vengono visualizzate la dimensione e le statistiche di utilizzo. Fare clic su **Modifica dettagli** per visualizzare e modificare le seguenti impostazioni della cassetta postale di archiviazione:
    
      - **Stato**   In questa casella di sola lettura è indicato se esiste una cassetta postale di archiviazione.
    
      - **Database**   In questa casella di sola lettura è visualizzato il nome del database che ospita la cassetta postale di archiviazione. In Exchange Online questa casella non è disponibile.
    
      - **Nome**   Digitare il nome della cassetta postale di archiviazione archivio in questa casella. Questo nome viene visualizzato nell'elenco delle cartelle in Outlook oppure Outlook Web App.
    
      - **Quota di archiviazione (GB)**   Questa casella indica la dimensione totale della cassetta postale di archiviazione. Per modificare la dimensione, digitare un nuovo valore nella casella o selezionare un valore nell'elenco a discesa.
    
      - **Invia avviso in corrispondenza di (GB)**   Questa casella indica il limite massimo di archiviazione che è possibile raggiungere prima che venga inviato un messaggio di avviso. Se la dimensione della cassetta postale di archiviazione raggiunge o supera il valore specificato, Exchange invia un avviso all'utente. Per modificare questo limite, digitare un nuovo valore nella casella o selezionare un valore nell'elenco a discesa.
        

        > [!NOTE]
        > La quota di archiviazione e la quota di avviso del problema relative alla cassetta postale di archiviazione non possono essere modificate in Exchange Online.



  - **Opzioni di recapito**   Utilizzare queste opzioni per inoltrare i messaggi di posta elettronica inviati all'utente a un altro destinatario e per impostare il numero massimo di destinatari a cui l'utente può inviare un messaggio. Fare clic su **Visualizza dettagli** per visualizzare e cambiare queste impostazioni.
    
      - **Indirizzo di inoltro**   Selezionare la casella di controllo **Abilita l'inoltro** e quindi fare clic su **Sfoglia** per visualizzare la pagina **Seleziona utente di posta e cassetta postale**. Utilizzare questa pagina per selezionare un destinatario a cui inoltrare tutti i messaggi di posta elettronica inviati a questa cassetta postale.
    
      - **Recapita messaggio all'indirizzo di inoltro e alla cassetta postale**   Selezionare questa casella di controllo per specificare che i messaggi di posta elettronica devono essere recapitati sia all'indirizzo di inoltro che alla cassetta postale dell'utente.
    
      - **Limite destinatari**   Questa impostazione consente di controllare il numero massimo di destinatari a cui l'utente può inviare un messaggio. Selezionare la casella di controllo **Limite massimo** per limitare il numero di destinatari consentiti nelle caselle A:, Cc: e Ccn: di un messaggio di posta elettronica e specificare il numero massimo di destinatari.
        

        > [!NOTE]
        > Per le organizzazioni Exchange locali, il numero di destinatari è illimitato. Per le organizzazioni Exchange Online, il limite è 500 destinatari.



  - **Restrizioni di dimensione per i messaggi**   Queste impostazioni controllano la dimensione dei messaggi che l'utente può inviare e ricevere. Fare clic su **Visualizza dettagli** per visualizzare e cambiare la dimensione massima dei messaggi inviati e ricevuti.
    

    > [!NOTE]
    > Queste impostazioni non possono essere modificate in Exchange Online.

    
      - **Messaggi inviati**   Per specificare una dimensione massima per i messaggi inviati da questo utente, selezionare la casella di controllo **Dimensione massima messaggio (KB)** e digitare un valore nella casella. La dimensione dei messaggi deve essere compresa tra 0 e 2.097.151 KB. Se l'utente invia un messaggio di dimensioni superiori a quelle specificate, il messaggio viene restituito all'utente con un messaggio di errore descrittivo.
    
      - **Messaggi ricevuti**   Per specificare una dimensione massima per i messaggi ricevuti da questo utente, selezionare la casella di controllo **Dimensione massima messaggio (KB)** e digitare un valore nella casella. La dimensione dei messaggi deve essere compresa tra 0 e 2.097.151 KB. Se all'utente viene inviato un messaggio di dimensioni superiori a quelle specificate, questo verrà restituito al mittente con un messaggio di errore descrittivo.

  - **Restrizioni di recapito dei messaggi**   Queste impostazioni controllano i mittenti che possono inviare a questo utente. Fare clic su **Visualizza dettagli** per visualizzare e cambiare queste restrizioni.
    
      - **Accetta messaggi da**   Utilizzare questa sezione per specificare chi può inviare messaggi a questo utente.
        
          - **Tutti i mittenti**   Selezionare questa opzione per specificare che l'utente può accettare messaggi da tutti i mittenti. Sono inclusi sia i mittenti nell'organizzazione di Exchange sia i mittenti esterni. In base all'impostazione predefinita, questo pulsante di opzione è selezionato. Questa opzione include gli utenti esterni solo se è stata deselezionata la casella di controllo **Richiedi autenticazione di tutti i mittenti**. Se si seleziona questa casella di controllo, i messaggi provenienti da utenti esterni saranno rifiutati.
        
          - **Solo i mittenti nell'elenco seguente**   Selezionare questa opzione per specificare che l'utente può accettare messaggi solo da un insieme specificato di mittenti nell'organizzazione di Exchange. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi")per visualizzare la pagina **Selezione destinatari**, in cui sono elencati tutti i destinatari dell'organizzazione di Exchange. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").
        
          - **Richiedi autenticazione di tutti i mittenti**   Selezionare questa opzione per impedire agli utenti anonimi di inviare messaggi all'utente.
    
      - **Rifiuta messaggi da**   Utilizzare questa sezione per impedire ai contatti di inviare messaggi a questo utente.
        
          - **Nessun mittente**   Selezionare questa opzione per specificare che la cassetta postale non rifiuterà i messaggi provenienti dai mittenti nell'organizzazione di Exchange. In base all'impostazione predefinita, questo pulsante di opzione è selezionato.
        
          - **Mittenti nel seguente elenco**   Selezionare questa opzione per specificare che la cassetta postale rifiuterà i messaggi da un insieme specificato di mittenti nell'organizzazione di Exchange. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per visualizzare la pagina **Selezione destinatari**, in cui è visualizzato un elenco di tutti i destinatari nell'organizzazione di Exchange. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").

## Membro di

Utilizzare la sezione **Membro di** per visualizzare un elenco dei gruppi di distribuzione o di sicurezza a cui appartiene questo utente. In questa pagina non è possibile modificare le informazioni sull'appartenenza. L'utente potrebbe soddisfare i criteri di uno o più gruppi di distribuzione dinamici nell'organizzazione. Tuttavia, i gruppi di distribuzione dinamici non sono visualizzati in questa pagina, perché la loro appartenenza viene calcolata ad ogni utilizzo.

## Avviso messaggio

Utilizzare la sezione **Avviso messaggio** per aggiungere un avviso messaggio che informi gli utenti dei problemi che potrebbero verificarsi inviando un messaggio a questo destinatario. Un avviso messaggio è un testo che viene visualizzato sulla barra informazioni quando questo destinatario viene aggiunto nelle caselle A, Cc o Ccn di un nuovo messaggio di posta elettronica.


> [!NOTE]
> Gli avvisi messaggio possono includere tag HTML, ma gli script non sono consentiti. La lunghezza di un avviso messaggio personalizzato non può superare 175 caratteri visualizzati. I tag HTML non vengono conteggiati in tale limite.



## Delega cassetta postale

Utilizzare la sezione **Delega cassetta postale** per assegnare ad altri utenti (detti anche *delegati*) autorizzazioni che consentano loro di accedere alla cassetta postale dell'utente o di inviare messaggi per conto dell'utente. È possibile assegnare le seguenti autorizzazioni:

  - **Invia come**   Questa autorizzazione consente agli utenti, diversi dal proprietario della cassetta postale, di utilizzare la cassetta postale per inviare messaggi. Dopo aver assegnato questa autorizzazione a un delegato, qualunque messaggio inviato da un delegato utilizzando questa cassetta postale apparirà come se fosse stato inviato dal proprietario della cassetta postale. Tuttavia, questa autorizzazione non consente a un delegato di accedere alla cassetta postale dell'utente.

  - **Invia per conto di**   Anche questa autorizzazione consente a un delegato di utilizzare la cassetta postale per inviare messaggi. Tuttavia, dopo l'assegnazione di questa autorizzazione a un delegato, l'indirizzo **Da:**  di qualunque messaggio inviato dal delegato indicherà che il messaggio è stato inviato dal delegato per conto del proprietario della cassetta postale.

  - **Accesso completo**   Questa autorizzazione consente a un delegato di accedere alla cassetta postale dell'utente e di visualizzare il contenuto della cassetta postale. Tuttavia, dopo l'assegnazione di questa autorizzazione a un delegato, il delegato non potrà inviare messaggi dalla cassetta postale. Per consentire a un delegato di inviare messaggi di posta elettronica dalla cassetta postale dell'utente, è ancora necessario assegnare al delegato l'autorizzazione Invia come o Invia per conto di.

Per assegnare le autorizzazioni ai delegati, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") sotto l'autorizzazione desiderata per visualizzare una pagina contenente un elenco di destinatari nell'organizzazione di Exchange a cui può essere assegnata l'autorizzazione. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").

## Utilizzare Shell per modificare le proprietà delle cassette postali utente

Utilizzare i cmdlet **Get-Mailbox** e **Set-Mailbox** per visualizzare e modificare le proprietà delle cassette postali utente. Uno dei vantaggi offerti dall'utilizzo della Shell è la possibilità di cambiare le proprietà per più cassette postali. Per informazioni sui parametri corrispondenti alle proprietà della cassetta postale, consultare i seguenti argomenti:

  - [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\))

Ecco alcuni esempi dell'utilizzo di Shell per cambiare le proprietà delle cassette postali utente.

In questo esempio viene mostrato come inoltrare i messaggi di posta elettronica di Pat Coleman alla cassetta postale di Sunil Koduri (sunilk@contoso.com).

    Set-Mailbox -Identity patc -DeliverToMailboxAndForward $true -ForwardingAddress sunilk@contoso.com

In questo esempio viene utilizzato il comando **Get-Mailbox** per trovare tutte le cassette postali utente nell'organizzazione, quindi viene utilizzato il comando **Set-Mailbox** per impostare a 500 il numero massimo di destinatari ammessi nelle caselle A:, Cc: e Ccn: di un messaggio di posta elettronica.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -RecipientLimits 500

Nel secondo esempio viene utilizzato il comando **Get-Mailbox** per trovare tutte le cassette postali nell'unità organizzativa Marketing, quindi viene utilizzato il comando **Set-Mailbox** per configurare queste cassette postali. I limiti personalizzati di avviso, invio non consentito e invio e ricezione non consentiti sono impostati rispettivamente su 200 MB, 250 MB e 280 MB, mentre i limiti predefiniti del database delle cassette postali vengono ignorati. È possibile utilizzare questo comando per configurare limiti maggiori o minori per un insieme di cassette postali specifico rispetto alle altre cassette postali nell'organizzazione.

    Get-Mailbox -OrganizationalUnit "Marketing" | Set-Mailbox -IssueWarningQuota 209715200 -ProhibitSendQuota 262144000 -ProhibitSendReceiveQuota 293601280 -UseDatabaseQuotaDefaults $false 

In questo esempio viene utilizzato il comando **Get-Mailbox** per trovare tutti gli utenti nel reparto Customer Service, quindi viene utilizzato il cmdlet **Set-Mailbox** per modificare la dimensione massima dei messaggi da inviare e portarla a 2 MB.

    Get-Mailbox -Filter "Department -eq 'Customer Service'" | Set-Mailbox -MaxSendSize 2097152

Questo esempio imposta la traduzione dell'avviso messaggio in francese e cinese.

    Set-Mailbox john@contoso.com -MailTipTranslations ("FR: C'est la langue française", "CHT: 這是漢語語言")

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta modifica delle proprietà di una cassetta postale utente, effettuare le seguenti operazioni:

  - In EAC selezionare la cassetta postale e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare le proprietà o le caratteristiche modificate. A seconda della proprietà modificata, la proprietà potrebbe essere visualizzata nel riquadro Dettagli per la cassetta postale selezionata.

  - In Shell, utilizzare il cmdlet **Get-Mailbox** per verificare le modifiche. Utilizzando Shell è possibile visualizzare più proprietà per più cassette postali. Nell'esempio precedente, in cui è stato modificato il numero massimo di destinatari, eseguire questo comando per verificare il nuovo valore.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,RecipientLimits
    
    Nell'esempio in alto in cui sono stati modificati i limiti dei messaggi, eseguire questo comando.
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

## Modifica in blocco delle cassette postali utente

Per modificare le proprietà di più cassette postali utente, è possibile utilizzare l'interfaccia di amministrazione di Exchange. Quando si selezionano due o più cassette postali utente dall'elenco delle cassette postali in EAC, le proprietà che possono essere modificate in blocco sono visualizzate nel riquadro dei dettagli. Quando si modifica una di queste proprietà, la modifica viene applicata a tutte le cassette postali selezionate.

Ecco un elenco delle proprietà e delle funzionalità delle cassette postali utente che possono essere modificate in blocco. Non tutte le proprietà in ogni area sono disponibili per la modifica.

  - **Informazioni contatto**   Modificare le proprietà condivise quali indirizzo, CAP e città.

  - **Organizzazione**   Modificare le proprietà condivise quali nome del reparto, ragione sociale e responsabile a cui fanno riferimento gli utenti selezionati.

  - **Attributi personalizzati**   Cambiare o aggiungere i valori per gli attributi personalizzati 1 - 15.

  - **Quota della cassetta postale**   Cambiare i valori di quota della cassetta postale e il periodo di conservazione degli elementi eliminati. Non è disponibile in Exchange Online.

  - **Connettività di posta elettronica**   Abilitare o disabilitare Outlook Web App, POP3, IMAP, MAPI ed Exchange ActiveSync.

  - **Archiviazione**   Abilitare o disabilitare la cassetta postale di archivio.

  - **Criteri di conservazione, di assegnazione dei ruoli e di condivisione**   Aggiornare le impostazioni per ciascuna di queste funzionalità delle cassette postali.

  - **Spostare le cassette postali in un altro database**   Spostare le cassette postali selezionate in un database diverso.

  - **Autorizzazioni delegate**   Assegnare le autorizzazioni per utenti o gruppi che consentono di aprire o inviare messaggi da alte cassette postali. È possibile assegnare autorizzazioni Complete, Invia come e Invia per conto di a utenti o gruppi. Consultare [Gestione delle autorizzazioni per i destinatari](manage-permissions-for-recipients-exchange-online-help.md) per maggiori dettagli.


> [!NOTE]
> Il tempo stimato per il completamento dell'attività è di 2 minuti, ma può essere superiore se si modificano più proprietà o caratteristiche.



## Utilizzare EAC per la modifica in blocco delle cassette postali utente

1.  In EAC, selezionare **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali, selezionare due o più cassette postali.
    

    > [!TIP]
    > È possibile selezionare più cassette postali adiacenti tenendo premuto MAIUSC e facendo clic sulla prima cassetta postale, quindi facendo clic sull'ultima cassetta postale che si desidera modificare. È inoltre possibile selezionare più cassette postali non adiacenti tenendo premuto CTRL e facendo clic su ciascuna cassetta postale da modificare.



3.  Nel riquadro dei dettagli, sotto **Modifica in blocco**, selezionare le proprietà o le funzionalità della cassetta postale che si desidera modificare.

4.  Apportare le modifiche nella pagina delle proprietà e quindi salvare le modifiche.

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta modifica in blocco delle cassette postali utente, effettuare una delle seguenti operazioni:

  - In EAC, selezionare ciascuna cassetta postale modificata in blocco e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare le proprietà o le caratteristiche modificate.

  - In Exchange Management Shell, utilizzare il cmdlet **Get-Mailbox** per verificare le modifiche. Utilizzando Shell è possibile visualizzare più proprietà per più cassette postali. Ad esempio, si supponga di aver utilizzato la funzionalità di modifica in blocco in EAC per abilitare la cassetta postale di archivio e assegnare un criterio di conservazione a tutti gli utenti nell'organizzazione. Per verificare queste modifiche, è possibile eseguire il seguente comando:
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,ArchiveDatabase,RetentionPolicy
    
    Per ulteriori informazioni sui parametri disponibili per il cmdlet **Get-Mailbox**, vedere [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)).


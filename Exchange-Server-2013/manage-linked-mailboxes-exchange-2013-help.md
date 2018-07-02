---
title: 'Gestire le cassette postali collegate: Exchange 2013 Help'
TOCTitle: Gestire le cassette postali collegate
ms:assetid: 76e12d4a-1c3a-42e2-b64c-c09d36e81bd3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673532(v=EXCHG.150)
ms:contentKeyID: 50480915
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire le cassette postali collegate

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-27_

Le cassette postali collegate sono cassette postali a cui gli utenti hanno accesso in una foresta attendibile e separata. Le cassette postali collegate possono essere necessarie per organizzazioni che distribuiscono Exchange in un foresta di risorse. La foresta delle risorse consente a un'organizzazione di centralizzare Exchange in una singola foresta, consentendo comunque l'accesso all'organizzazione di Exchange tramite account utente appartenenti a una o più foreste attendibili (chiamate *foreste account*). L'account utente che accede alla cassetta postale collegata non esiste nella foresta in cui Exchange è distribuito. Pertanto, un account utente disabilitato presente nella stessa foresta di Exchange viene creato e associato alla corrispondente cassetta postale collegata.

Nella figura seguente è illustrata la relazione tra l'account utente collegato utilizzato per accedere alla cassetta postale collegata (localizzata nella foresta account) e l'account utente disabilitato nella foresta di risorse di Exchange associato alla cassetta postale collegata.

**Cassette postali collegate**

![Organizzazione di Exchange complessa con foresta di risorse](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "Organizzazione di Exchange complessa con foresta di risorse")


> [!NOTE]
> Una relazione di trust tra la foresta di Exchange e almeno una foresta account deve essere impostata prima che si possano creare cassette postali collegate. Come minimo, si deve impostare una relazione, unidirezionale, di trust in uscita in modo che la foresta di Exchange accetti la foresta account. Per ulteriori informazioni, vedere <A href="https://technet.microsoft.com/it-it/library/jj156983(v=exchg.150)">Ulteriori informazioni su come configurare un trust tra foreste per il supporto di cassette postali collegate</A>.



## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2-5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Deve esistere un account utente (chiamato *account master collegato*) nella foresta account prima che si possa creare una cassetta postale collegata. Questo perché la cassetta postale collegata è associata a un utente nella foresta account.

  - Se è stata configurata una relazione di trust unidirezionale in uscita dove la foresta Exchange riconosce come attendibile la foresta account, sono necessarie le credenziali di amministratore per creare una cassetta postale collegata.
    
    Per creare una cassetta postale collegata senza dover fornire le credenziali di amministratore nella foresta di account, creare un trust bidirezionale oppure creare un altro trust in ingresso unidirezionale in cui la foresta di account riconosca come attendibile anche la foresta di Exchange. Anche questo passaggio richiede credenziali di amministratore nella foresta account.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Creazione di una cassetta postale collegata

## Creazione di una cassetta postale collegata tramite Interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**.

2.  Fare clic su **Nuovo** \> **Cassetta postale collegata**.

3.  Sulla pagina **Nuova cassetta postale collegata**, nella casella **Foreste attendibili nel dominio**, selezionare il nome della foresta account che contiene l'account utente per il quale si sta creando la cassetta postale collegata. Fare clic su **Avanti**.

4.  Se la propria organizzazione ha configurato una relazione di trust in uscita unidirezionale dove la foresta Exchange riconosce come attendibile la foresta account, verranno richieste le credenziali di amministratore nella foresta account in modo da ottenere l'accesso ad un controller di dominio nella foresta attendibile. Immettere il nome utente e la password per un account amministratore nella foresta account, quindi fare clic su **Avanti**.
    

    > [!NOTE]
    > Non verranno richieste le credenziali di amministratore se si è creta una relazione di trust bidirezionale o è stata creata un'altra relazione di trust unidirezionale dove la foresta account riconosce come attendibile la foresta Exchange.



5.  Completare le seguenti caselle sulla pagina **Selezionare account master collegato**.
    
      - **Controller di dominio collegato**   Selezionare un controller di dominio nella foresta account. Exchange si connetterà a questo controller di dominio per recuperare l'elenco degli account utente nella foresta account in modo che sia possibile selezionare l'account master collegato.
    
      - **Account master collegato**   Fare clic su **Sfoglia**, selezionare un account utente nella foresta account quindi fare clic su **OK**. La nuova cassetta postale collegata verrà associata a questo account.

6.  Fare clic su **Avanti** e completare le caselle seguenti sulla pagina **Immettere informazioni generali**.
    
      - **\* Nome**   Utilizzare questa casella per digitare un nome da assegnare all'utente. Questo è il nome utilizzato come nome visualizzato nell'interfaccia di amministrazione do Exchange e nella rubrica dell'organizzazione e il nome che viene elencato in Active Directory. Questo nome è obbligatorio.
    
      - **Unità organizzativa**   È possibile selezionare un'unità organizzativa diversa da quella predefinita (che corrisponde all'ambito dei destinatari). Se l'ambito dei destinatari è impostato a livello di foresta, il valore predefinito è impostato sul contenitore di utenti nel dominio di Active Directory contenente il computer su cui è in esecuzione l'interfaccia di amministrazione di Exchange. Se l'ambito dei destinatari viene impostato su un dominio specifico, per impostazione predefinita verrà selezionato il contenitore di utenti del dominio in questione. Se infine come ambito dei destinatari si sceglie una specifica unità organizzativa, per impostazione predefinita verrà selezionata l'unità organizzativa specificata.
        
        Per selezionare un'unità organizzativa diversa, scegliere il pulsante **Sfoglia**. La finestra di dialogo visualizzerà tutte le unità organizzative presenti nella foresta di Exchange nell'ambito specificato. Selezionare l'unità organizzativa desiderata e fare clic su **OK**.
    
      - **\* Nome accesso utente**   Usare questa casella per immettere il nome di accesso dell'utente necessario per creare una cassetta postale collegata. Digitare qui il nome utente. Questo nome verrà utilizzato nella parte sinistra dell'indirizzo di posta elettronica per la cassetta postale collegata se non si specifica un alias.
        

        > [!NOTE]
        > Poiché l'account utente creato nella foresta di Exchange è disabilitato quando si crea una cassetta postale collegata, l'utente non utilizza il nome di accesso utente per accedere a una cassetta postale collegata. Gli utenti accedono utilizzando le loro credenziali della foresta account.



7.  Fare clic su **Altre opzioni** per configurare le seguenti caselle. Altrimenti, passare direttamente al passo 8 per salvare la nuova cassetta postale collegata.
    
      - **Alias**   Immettere l'alias che specifica l'alias di posta elettronica per la cassetta postale collegata. L'alias dell'utente è la parte dell'indirizzo di posta elettronica a sinistra del simbolo di chiocciola (@). Deve essere univoco nella foresta.
        

        > [!NOTE]
        > Sei si lascia vuota questa casella, come alias di posta elettronica dell'utente viene utilizzata la parte del nome utente ricavata da <STRONG>Nome di accesso utente</STRONG>.

    
      - **Nome**, **Iniziali**, **Cognome**
    
      - **Database delle cassette postali**   Utilizzare questa opzione per specificare un database delle cassette postali invece che permettere a Exchange di selezionarlo automaticamente. Fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona database delle cassette postali**. In questa finestra di dialogo vengono elencati tutti i database delle cassette postali nell'organizzazione di Exchange. Per impostazione predefinita, i database delle cassette postali sono ordinati per nome. È inoltre possibile fare clic sul titolo della colonna corrispondente per ordinare i database in base al nome o alla versione del server. Selezionare il database delle cassette postali desiderato e fare clic su **OK**.
    
      - **Criterio rubrica**   Utilizzare questa opzione per specificare un criterio per la rubrica per la cassetta postale collegata. I criteri rubrica contengono un elenco di indirizzi globale, una rubrica offline , un elenco di sale e un set di elenchi di indirizzi. Quando un ABP viene assegnato agli utenti, fornisce loro un accesso ad un GAL personalizzato in Outlook e Outlook Web App. Per ulteriori informazioni, vedere [Criteri delle rubriche](address-book-policies-exchange-2013-help.md).
        
        Nell'elenco a discesa, selezionare il criterio da associare a questa cassetta postale.

8.  Al termine, scegliere **Salva** per creare la nuova cassetta postale collegata.

## Creazione di una cassetta postale collegata tramite Shell

In questo esempio viene creata una cassetta postale collegata per Ayla Kol nella foresta risorse Exchange CONTOSO. Il dominio di FABRIKAM è la foresta account. L'account di amministratore FABRIKAM \\administrator è utilizzato per accedere al controller di dominio collegato.

    New-Mailbox -Name "Ayla Kol" -LinkedDomainController "DC1_FABRIKAM" -LinkedMasterAccount " FABRIKAM\aylak" -OrganizationalUnit Users -UserPrincipalName aylak@contoso.com -LinkedCredential:(Get-Credential FABRIKAM\administrator)

Per informazioni sulla sintassi e sui parametri, vedere [New-Mailbox](https://technet.microsoft.com/it-it/library/aa997663\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta creazione della cassetta postale collegata, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**. La nuova cassetta postale collegata viene visualizzata nell'elenco delle cassette postali. In **Tipo di cassetta postale**, il tipo è **Collegata**.

  - In Shell, eseguire il seguente comando per visualizzare le informazioni relative alla nuova cassetta postale collegata.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,IsLinked,LinkedMasterAccount

## Modifica delle proprietà della cassetta postale collegata

Dopo aver creato la cassetta postale collegata, è possibile effettuare modifiche e impostare proprietà aggiuntive utilizzando l'interfaccia di amministrazione di Exchange (EAC) o Exchange Management Shell.

È anche possibile modificare contemporaneamente le proprietà di più cassette postali collegate. Per ulteriori informazioni, vedere la sezione "Modifica collettiva delle cassette postali utente" nell'argomento [Gestire le cassette postali degli utenti](manage-user-mailboxes-exchange-2013-help.md).


> [!IMPORTANT]
> Il tempo stimato per il completamento dell'attività dipende dal numero di proprietà da visualizzare o modificare.



## Utilizzo di Interfaccia di amministrazione di Exchange per modificare le proprietà delle cassette postali utente

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali, fare clic sulla cassetta postale collegata della quale si vogliono modificare le proprietà e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Sulla pagina delle proprietà della cassetta postale, fare clic su una delle seguenti sezioni per visualizzare o modificare le proprietà.
    
      - General
    
      - Mailbox Usage
    
      - Email Address
    
      - Mailbox Features
    
      - Member Of
    
      - MailTip
    
      - Mailbox Delegation

## Generale

Utilizzare la sezione **Generale** per visualizzare o modificare le informazioni di base sull'utente.

  - **\* Nome cassetta postale collegata**   Questo è il nome che compare in Active Directory. Se viene modificato, non può superare i 64 caratteri.

  - **\* Nome visualizzato**   Questo nome viene visualizzato nella Rubrica dell'organizzazione, nel campo A: e Da: del messaggio di posta elettronica e nell'elenco di cassette postali nell'interfaccia di amministrazione di Exchange. Questo nome non può contenere spazi vuoti prima o dopo il nome visualizzato.

  - **\* Nome accesso utente**    Per le cassette postali utente, questo è il nome che gli utenti utilizzano per accedere alla loro cassetta postale e per accedere al dominio. Per le cassette postali collegate, il corrispondente account utente, creato nella foresta Exchange quando è stata creata la cassetta postale collegata, è disabilitato. L'utente utilizza le credenziali della foresta account per accedere alla cassetta postale collegata.
    
    Se viene modificato questo nome, deve essere univoco nell'organizzazione.

  - **Account master collegato**   Questa casella di sola lettura visualizza l'utente (nel formato dominio\\nomeutente formato) dalla foresta account associato alla cassetta postale collegata. Per modificare l'account master collegato associato alla cassetta postale collegata si deve utilizzare il cmdlet **Set-Mailbox**in Shell. Se si modifica l'account master collegato, l'utente dovrà utilizzare le credenziali per il nuovo account master collegato per accedere alla cassetta postale collegata. Per la sintassi del comando per modificare l'account master collegato, vedere Use the Shell to change linked mailbox properties.

  - **Non visualizzare negli elenchi di indirizzi**   Selezionare questa casella di controllo per impedire la visualizzazione della cassetta postale collegata nella rubrica e in altri elenchi di indirizzi definiti nell'organizzazione di Exchange. Dopo la selezione di questa casella di controllo, gli utenti possono comunque inviare messaggi al destinatario utilizzando l'indirizzo di posta elettronica.

Fare clic su **Altre opzioni** per visualizzare o modificare le seguenti proprietà aggiuntive:

  - **Unità organizzativa**   In questa casella di sola lettura è visualizzata l'unità organizzativa contenente l'account utente. È necessario utilizzare Utenti e computer di Active Directory per spostare l'account utente in un'altra unità organizzativa.

  - **Database delle cassette postali**   In questa casella di sola lettura è visualizzato il nome del database che ospita la cassetta postale. Per spostare la cassetta postale in un diverso database, selezionarla nell'elenco cassette postali, quindi fare clic su **Spostare la cassetta postale in un database diverso** nel riquadro dei dettagli.

  - **\* Alias** Specifica l'alias di posta elettronica per la cassetta postale collegata. L'alias è la parte dell'indirizzo di posta elettronica a sinistra del simbolo di chiocciola (@). Deve essere univoco nella foresta.

  - **Nome**, **Iniziali**, **Cognome**

  - **Attributi personalizzati**   Questa sezione visualizza gli attributi personalizzati definiti per la cassetta postale collegata. Per specificare valori personalizzati per gli attributi, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). È possibile specificare fino a 15 attributi personalizzati per un destinatario.

## Utilizzo cassetta postale

Utilizzare la sezione **Utilizzo cassetta postale** per vedere o modificare la quota di archiviazione della cassetta postale e le impostazioni di mantenimento degli elementi eliminati. Queste impostazioni vengono configurate per impostazione predefinita durante la creazione della cassetta postale collegata. Utilizzano i valori configurati per il database delle cassette postali e li applicano a tutte le cassette postali in quel database. È possibile personalizzare queste impostazioni per ciascuna cassetta postale invece che utilizzare i valori predefiniti del database delle cassette postali.

  - **Ultimo accesso**   Questa casella di sola lettura visualizza l'ora in cui l'utente ha effettuato l'accesso per l'ultima volta alla cassetta postale.

  - **Uso della cassetta postale**   In quest'area è indicata la dimensione totale della cassetta postale e la percentuale della quota totale che è stata utilizzata.


> [!NOTE]
> Per ottenere le informazioni visualizzate nelle due precedenti caselle, l'interfaccia di amministrazione di Exchange esegue una query nel database delle cassette postali che ospita la cassetta postale. Se l'interfaccia di amministrazione di Exchange non è in grado di comunicare con l'archivio di Exchange contenente il database delle cassette postali, questo campo verrà lasciato vuoto. Se l'utente non ha eseguito l'accesso alla cassetta postale per la prima volta, viene visualizzato un messaggio di avviso.



Fare clic su **Altre opzioni** per visualizzare o modificare la quota di archiviazione della cassetta postale e le impostazioni di conservazione degli elementi nella cassetta postale.

  - **Impostazioni della quota di archiviazione**   Per personalizzare queste impostazioni per la cassetta postale e non utilizzare le impostazioni predefinite del database delle cassette postali, fare clic su **Personalizzare le impostazioni per questa cassetta postale**, immettere un nuovo valore e fare clic su **Salva**.
    
    L'intervallo di valori per le impostazioni della quota di archiviazione è compreso tra 0 e 2047 GB.
    
      - **Invia un avviso in corrispondenza di (GB)**   Questa casella indica il limite massimo di archiviazione che è possibile raggiungere prima che venga inviato un messaggio di avviso. Se la dimensione della cassetta postale raggiunge o supera il valore specificato, Exchange invia un avviso all'utente.
    
      - **Non consentire l'invio di (GB)**   Questa casella indica il limite di *invio non consentito* per la cassetta postale. Se la dimensione della cassetta postale raggiunge o supera il limite specificato, Exchange impedisce all'utente di inviare nuovi messaggi e visualizza un messaggio di errore descrittivo.
    
      - **Non consentire l'invio e la ricezione di (GB)**   Questa casella indica il limite di *invio e ricezione non consentiti* per la cassetta postale. Se la dimensione della cassetta postale raggiunge o supera il limite specificato, Exchange impedisce all'utente della cassetta postale di inviare nuovi messaggi e non recapiterà i nuovi messaggi alla cassetta postale. Tutti i messaggi inviati alla cassetta postale vengono restituiti al mittente con un messaggio di errore descrittivo.

  - **Impostazioni di mantenimento degli elementi eliminati**   Per personalizzare queste impostazioni per la cassetta postale e non utilizzare le impostazioni predefinite del database delle cassette postali, fare clic su **Personalizzare le impostazioni per questa cassetta postale**, immettere un nuovo valore e fare clic su **Salva**.
    
      - **Conserva elementi eliminati per (giorni)**   Questa casella indica per quanto tempo gli elementi eliminati vengono conservati prima di essere eliminati definitivamente e non essere più recuperabili dall'utente. Durante la creazione della cassetta postale, questo intervallo di tempo si basa sulle impostazioni di conservazione degli elementi eliminati configurate per il database delle cassette postali. Per impostazione predefinita, la conservazione degli elementi eliminati in un database delle cassette postali è impostata su 14 giorni. L'intervallo di valori per questa proprietà è compreso fra 0 e 24855 giorni.
    
      - **Non eliminare definitivamente questi elementi prima di aver creato una copia di backup del database**   Selezionare questa casella di controllo per impedire che le cassette postali e i messaggi di posta elettronica vengano eliminati prima che sia stato eseguito il backup del database in cui si trova la cassetta postale in questione.

## Indirizzo di posta elettronica

Utilizzare la sezione **Indirizzo di posta elettronica** per visualizzare o modificare gli indirizzi di posta elettronica associati alla cassetta postale collegata. Ciò include gli indirizzi SMTP primari dell'utente e qualsiasi indirizzo proxy ad esso associato. L'indirizzo SMTP primario (chiamato anche *indirizzo di risposta predefinito*) viene visualizzato in grassetto nell'elenco degli indirizzi, con il valore **SMTP** maiuscolo nella colonna **Tipo**.

  - **Aggiungi **  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere un nuovo indirizzo di posta elettronica per la cassetta postale. Selezionare uno dei seguenti tipi di indirizzo:
    
      - **SMTP**   Questo è il tipo di indirizzo predefinito. Fare clic su questo pulsante e quindi digitare il nuovo indirizzo SMTP nella casella **\* Indirizzo di posta elettronica**.
    
      - **Messaggistica unificata di Exchange**   Un indirizzo di messaggistica unificata di Exchange viene utilizzato dal servizio di messaggistica unificata di Microsoft Exchange per individuare gli utenti abilitati alla messaggistica unificata all'interno dell'organizzazione Exchange. L'indirizzo di messaggistica unificata di Exchange è costituito dal numero di interno e dal dial plan per l'utente abilitato alla messaggistica unificata. Fare clic su questo pulsante e digitare il numero di telefono interno nella casella **Indirizzo/Estensione**. Quindi fare clic su **Sfoglia** e selezionare un dial plan per l'utente.
    
      - **Tipo di indirizzo personalizzato**   Fare clic su questo pulsante e digitare uno dei tipi di indirizzi di posta elettronica non SMTP supportati nella casella **\* Indirizzo di posta elettronica**.
        

        > [!NOTE]
        > Ad eccezione degli indirizzi X.400, Exchange non convalida gli indirizzi personalizzati per una formattazione corretta. È necessario verificare che l'indirizzo personalizzato specificato sia conforme ai requisiti di formato per tale tipo di indirizzo.



  - **Aggiorna automaticamente gli indirizzi sulla base del criterio dell'indirizzo di posta elettronica applicato a questo destinatario   **Selezionare questa casella di controllo se si vogliono aggiornare automaticamente gli indirizzi di posta elettronica dei destinatari quando vengono apportate modifiche ai criteri degli indirizzi di posta elettronica nell'organizzazione. Tale casella è selezionata per impostazione predefinita.

## Funzionalità delle cassette postali

Utilizzare la sezione **Funzionalità delle cassette postali** per visualizzare o modificare le seguenti funzionalità e impostazioni delle cassette postali:

  - **Criterio di condivisione**   Questa casella indica il criterio di condivisione applicato alla cassetta postale. Il criterio di condivisione controlla la modalità di condivisione delle informazioni del calendario e dei contatti tra gli utenti nell'organizzazione e quelli esterni all'organizzazione Exchange. Il criterio di condivisione predefinito viene assegnato alle cassette postali al momento della loro creazione. Per modificare il criterio di condivisione assegnato all'utente, selezionare il criterio desiderato nell'elenco a discesa.

  - **Criterio di assegnazione dei ruoli**   Questa casella indica il criterio di assegnazione dei ruoli assegnato alla cassetta postale. Il criterio di assegnazione dei ruoli specifica il controllo di accesso basato sui ruoli (RBAC) assegnato all'utente e controlla quali impostazioni della cassetta postale e del gruppo di distribuzione gli utenti finali possono modificare. Per modificare il criterio di assegnazione dei ruoli assegnato all'utente, selezionare il criterio desiderato nell'elenco a discesa.

  - **Criterio di conservazione**   Questa casella indica il criterio di conservazione applicato alla cassetta postale. Un criterio di conservazione è costituito da un gruppo di tag di conservazione applicate alla cassetta postale dell'utente. I tag consentono di controllare il periodo di conservazione degli elementi nelle cassette postali degli utenti e definire l'azione da eseguire sugli elementi che hanno raggiunto un determinato limite temporale. Il criterio di conservazione non viene assegnato alle cassette postali al momento della loro creazione. Per assegnare un criterio di conservazione a un utente, selezionarlo nell'elenco a discesa.

  - **Criteri rubrica**   Questa casella mostra il criterio rubrica applicato alla cassetta postale. Un criterio rubrica consente di segmentare gli utenti in gruppi specifici per fornire visualizzazioni personalizzate della rubrica. Per applicare o modificare il criterio rubrica applicato alla cassetta postale, selezionarne uno dall'elenco a discesa.

  - **Messaggistica unificata**   Questa funzionalità è disabilitata per impostazione predefinita. Quando si abilita la messaggistica unificata (UM) l'utente sarà in grado di utilizzare le funzionalità di messaggistica unificata dell'organizzazione ed un gruppo predefinito di proprietà di messaggistica unificata viene applicato all'utente. Fare clic su **Abilita** per abilitare la messaggistica unificata per la cassetta postale. Per informazioni su come abilitare la messaggistica unificata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).
    

    > [!NOTE]
    > Per poter abilitare la messaggistica unificata, è necessario che siano già stati creati un dial plan e un criterio cassetta postale di messaggistica unificata.



  - **Dispositivi mobili**   Utilizzare questa sezione per visualizzare e cambiare le impostazioni di Exchange ActiveSync, abilitato per impostazione predefinita. Exchange ActiveSync consente l'accesso a una cassetta postale di Exchange da un dispositivo mobile. Fare clic su **Disabilita Exchange ActiveSync** per disabilitare questa funzionalità per la cassetta postale.

  - **Outlook Web App**   Questa funzionalità è abilitata per impostazione predefinita. Outlook Web App consente di accedere a una cassetta postale di Exchange da qualsiasi browser. Fare clic su **Disabilita** per disabilitare Outlook Web App per la cassetta postale. Fare clic su **Modifica dettagli** per aggiungere o modificare un criterio cassetta postale di Outlook Web App per la cassetta postale.

  - **IMAP**   Questa funzionalità è abilitata per impostazione predefinita. Fare clic su **Disabilita** per disabilitare la funzionalità IMAP per la cassetta postale.

  - **POP3**   Questa funzionalità è abilitata per impostazione predefinita. Fare clic su **Disabilita** per disabilitare la funzionalità POP3 per la cassetta postale.

  - **MAPI**   Questa funzionalità è abilitata per impostazione predefinita. MAPI consente l'accesso a una cassetta postale di Exchange da un client MAPI, ad esempio Outlook. Fare clic su **Disabilita** per disabilitare la funzionalità MAPI per la cassetta postale.

  - **Conservazione per controversia legale**Questa funzionalità è disabilitata per impostazione predefinita. La funzionalità di conservazione in caso di dispute consente di mantenere gli elementi eliminati dalla cassetta postale e di registrare le modifiche apportate agli elementi. Gli elementi eliminati e tutte le istanze degli elementi modificati vengono restituiti in una ricerca di individuazione. Fare clic su **Abilita** per abilitare la conservazione per controversia legale della cassetta postale. Se per la cassetta postale è abilitata la conservazione per controversia legale, fare clic su **Disabilita** per annullarla. Se per la cassetta postale è abilitata la conservazione per controversia legale, fare clic su **Modifica dettagli** per visualizzare e modificare le seguenti impostazioni della conservazione:
    
      - **Data di conservazione**   Questa casella di sola lettura indica la data e l'ora in cui la cassetta postale è stata posta in conservazione per controversia legale.
    
      - **Conservazione per controversia legale effettuata da**   In questa casella di sola lettura è indicato l'utente che ha attivato la conservazione.
    
      - **Nota**   Utilizzare questa casella per inviare all'utente una notifica relativa alla conservazione per controversia legale, spiegarne le motivazioni o fornire istruzione aggiuntive, ad esempio per informare l'utente che la conservazione per controversia legale non influirà sull'utilizzo quotidiano della posta elettronica.
    
      - **URL**   Utilizzare questa casella per specificare un URL di un sito Web che fornisce informazioni o istruzioni relative alla conservazione per controversia legale della cassetta postale.
        

        > [!NOTE]
        > Il testo di questi campi viene visualizzato nella cassetta postale dell'utente solo se utilizza Outlook 2010 o versioni successive. Non viene visualizzato in Outlook Web App o in altri client di posta elettronica. Per visualizzare il testo dei campi Nota e URL in Outlook, fare clic sulla scheda <STRONG>File</STRONG> e sulla pagina <STRONG>Informazioni</STRONG> in <STRONG>Impostazioni account</STRONG> verrà visualizzato il commento relativo alla conservazione per controversia legale.



  - **Archiviazione**   Se per l'utente non esiste una cassetta postale di archiviazione, questa funzionalità è disabilitata. Per abilitare una cassetta postale di archiviazione, fare clic su **Abilita**. Se l'utente ha una cassetta postale di archiviazione, ne vengono visualizzate la dimensione e le statistiche di utilizzo. Fare clic su **Modifica dettagli** per visualizzare e modificare le seguenti impostazioni della cassetta postale di archiviazione:
    
      - **Stato**   In questa casella di sola lettura è indicato se esiste una cassetta postale di archiviazione.
    
      - **Database**   In questa casella di sola lettura è visualizzato il nome del database che ospita la cassetta postale di archiviazione.
    
      - **Nome**   Digitare il nome della cassetta postale di archiviazione archivio in questa casella. Questo nome viene visualizzato nell'elenco delle cartelle in Outlook oppure Outlook Web App.
    
      - **Uso della quota**   In quest'area di sola lettura è indicata la dimensione totale della cassetta postale di archiviazione e la percentuale della quota totale che è stata utilizzata.
    
      - **Valore quota (GB)**   Questa casella indica la dimensione totale della cassetta postale di archiviazione. Per modificare la dimensione, digitare un nuovo valore nella casella o selezionare un valore nell'elenco a discesa.
    
      - **Invia avviso in corrispondenza di (GB)**   Questa casella indica il limite massimo di archiviazione che è possibile raggiungere prima che venga inviato un messaggio di avviso. Se la dimensione della cassetta postale di archiviazione raggiunge o supera il valore specificato, Exchange invia un avviso all'utente. Per modificare questo limite, digitare un nuovo valore nella casella o selezionare un valore nell'elenco a discesa.

  - **Opzioni di recapito**   Utilizzare Opzioni di recapito per inoltrare ad un altro destinatario i messaggi di posta elettronica inviati all'utente e per impostare il numero massimo di destinatari a cui l'utente può inviare messaggi. Fare clic su **Modifica dettagli** per visualizzare e cambiare queste impostazioni.
    
      - **Indirizzo di inoltro**   Selezionare la casella di controllo **Abilita l'inoltro** e quindi fare clic su **Sfoglia** per visualizzare la pagina **Seleziona utente di posta e cassetta postale**. Utilizzare questa pagina per selezionare un destinatario a cui inoltrare tutti i messaggi di posta elettronica inviati a questa cassetta postale. I messaggi possono essere inviati sia alla cassetta postale collegata che all'indirizzo di inoltro.
    
      - **Limite destinatari**   Questa impostazione consente di controllare il numero massimo di destinatari a cui l'utente può inviare un messaggio. Selezionare la casella di controllo **Numero massimo di destinatari** per limitare il numero di destinatari ammessi per i campi A: Cc: e Ccn: di un messaggio di posta elettronica e poi specificare il numero massimo di destinatari.
        

        > [!NOTE]
        > Per le organizzazioni Exchange locali, il numero di destinatari è illimitato. Per le organizzazioni Exchange Online, il limite è 500 destinatari.



  - **Restrizioni di dimensione per i messaggi**   Queste impostazioni controllano la dimensione dei messaggi che l'utente può inviare e ricevere. Fare clic su **Modifica dettagli** per visualizzare e cambiare la dimensione massima dei messaggi inviati e ricevuti.
    
      - **Messaggi inviati**   Per specificare una dimensione massima per i messaggi inviati da questo utente, selezionare la casella di controllo **Dimensione massima messaggio (KB)** e digitare un valore nella casella. La dimensione dei messaggi deve essere compresa tra 0 e 2.097.151 KB. Se l'utente invia un messaggio di dimensioni superiori a quelle specificate, il messaggio viene restituito all'utente con un messaggio di errore descrittivo.
    
      - **Messaggi ricevuti**   Per specificare una dimensione massima per i messaggi ricevuti da questo utente, selezionare la casella di controllo **Dimensione massima messaggio (KB)** e digitare un valore nella casella. La dimensione dei messaggi deve essere compresa tra 0 e 2.097.151 KB. Se all'utente viene inviato un messaggio di dimensioni superiori a quelle specificate, questo verrà restituito al mittente con un messaggio di errore descrittivo.

  - **Restrizioni di recapito dei messaggi**   Queste impostazioni controllano i mittenti che possono inviare a questo utente. Fare clic su **Modifica dettagli** per visualizzare e cambiare queste restrizioni.
    
      - **Accetta messaggi da**   Utilizzare questa sezione per specificare chi può inviare messaggi a questo utente.
        
          - **Tutti i mittenti**   Selezionare questa opzione per specificare che l'utente può accettare messaggi da tutti i mittenti. Sono inclusi sia i mittenti nell'organizzazione di Exchange sia i mittenti esterni. In base all'impostazione predefinita, questo pulsante di opzione è selezionato. Questa opzione include gli utenti esterni solo se è stata deselezionata la casella di controllo **Richiedi autenticazione di tutti i mittenti**. Se si seleziona questa casella di controllo, i messaggi provenienti da utenti esterni saranno rifiutati.
        
          - **Solo i mittenti nell'elenco seguente**   Selezionare questa opzione per specificare che l'utente può accettare messaggi solo da un insieme specificato di mittenti nell'organizzazione di Exchange. Fare clic su **Aggiungi** per visualizzare la pagina **Selezione destinatari**, in cui è visualizzato un elenco di tutti i destinatari nell'organizzazione di Exchange. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare uno specifico destinatario digitandone il nome nella casella di ricerca e quindi facendo clic su **Cerca**.
        
          - **Richiedi autenticazione di tutti i mittenti**   Selezionare questa opzione per impedire agli utenti anonimi di inviare messaggi all'utente.
    
      - **Rifiuta messaggi da**   Utilizzare questa sezione per impedire ai contatti di inviare messaggi a questo utente.
        
          - **Nessun mittente**   Selezionare questa opzione per specificare che la cassetta postale non rifiuterà i messaggi provenienti dai mittenti nell'organizzazione di Exchange. In base all'impostazione predefinita, questo pulsante di opzione è selezionato.
        
          - **Mittenti nel seguente elenco**   Selezionare questa opzione per specificare che la cassetta postale rifiuterà i messaggi da un insieme specificato di mittenti nell'organizzazione di Exchange. Fare clic su **Aggiungi** per visualizzare la pagina **Selezione destinatario**, in cui è visualizzato un elenco di tutti i destinatari nell'organizzazione di Exchange. Selezionare i destinatari per i quali si vogliono rifiutare i messaggi, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare uno specifico destinatario digitandone il nome nella casella di ricerca e quindi facendo clic su **Cerca**.

## Membro di

Utilizzare la sezione **Membro di** per visualizzare un elenco dei gruppi di distribuzione o di sicurezza a cui appartiene questo utente. In questa pagina non è possibile modificare le informazioni sull'appartenenza. L'utente potrebbe soddisfare i criteri di uno o più gruppi di distribuzione dinamici nell'organizzazione. Tuttavia, i gruppi di distribuzione dinamici non sono visualizzati in questa pagina, perché la loro appartenenza viene calcolata ad ogni utilizzo.

## Avviso messaggio

Utilizzare la sezione **Avviso messaggio** per aggiungere un avviso messaggio che informi gli utenti dei problemi che potrebbero verificarsi inviando un messaggio a questo destinatario. Un avviso messaggio è un testo che viene visualizzato sulla barra informazioni quando un destinatario viene aggiunto nella riga A, Cc o Ccn di un nuovo messaggio di posta elettronica.


> [!NOTE]
> Gli avvisi messaggio possono includere tag HTML, ma gli script non sono consentiti. La lunghezza di un avviso messaggio personalizzato non può superare 175 caratteri visualizzati. I tag HTML non vengono conteggiati in tale limite.



## Delega cassetta postale

Utilizzare la sezione **Delega cassetta postale** per assegnare ad altri utenti (detti anche *delegati*) autorizzazioni che consentano loro di accedere alla cassetta postale dell'utente o di inviare messaggi per conto dell'utente. È possibile assegnare le seguenti autorizzazioni:

  - **Invia come**   Questa autorizzazione consente agli utenti, diversi dal proprietario della cassetta postale, di utilizzare la cassetta postale per inviare messaggi. Dopo aver assegnato questa autorizzazione a un delegato, qualunque messaggio inviato da un delegato utilizzando questa cassetta postale apparirà come se fosse stato inviato dal proprietario della cassetta postale. Tuttavia, questa autorizzazione non consente a un delegato di accedere alla cassetta postale dell'utente.

  - **Invia per conto di**   Anche questa autorizzazione consente a un delegato di utilizzare la cassetta postale per inviare messaggi. Tuttavia, dopo l'assegnazione di questa autorizzazione a un delegato, l'indirizzo **Da:**  di qualunque messaggio inviato dal delegato indicherà che il messaggio è stato inviato dal delegato per conto del proprietario della cassetta postale.

  - **Accesso completo**   Questa autorizzazione consente a un delegato di accedere alla cassetta postale dell'utente e di visualizzare il contenuto della cassetta postale. Tuttavia, dopo l'assegnazione di questa autorizzazione a un delegato, il delegato non potrà inviare messaggi dalla cassetta postale. Per consentire a un delegato di inviare messaggi di posta elettronica dalla cassetta postale dell'utente, è ancora necessario assegnare al delegato l'autorizzazione Invia come o Invia per conto di.

Per assegnare le autorizzazioni ai delegati, fare clic su **Aggiungi** sotto l'autorizzazione desiderata per visualizzare la pagina **Scegli il destinatario** che contiene un elenco di destinatari nell'organizzazione Exchange a cui può essere assegnata l'autorizzazione. Selezionare i destinatari ai quali si vogliono assegnare autorizzazioni di delegato, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare uno specifico destinatario digitandone il nome nella casella di ricerca e quindi facendo clic su **Cerca**.

## Utilizzo di Shell per modificare le proprietà delle cassette postali collegate

Utilizzare i cmdlet **Get-Mailbox** e **Set-Mailbox** per visualizzare e modificare le proprietà per le cassette postali collegate. Uno dei vantaggi offerti dall'utilizzo di Shell è la possibilità di impostare le proprietà per più cassette postali collegate. Per informazioni sui parametri corrispondenti alle proprietà della cassetta postale, consultare i seguenti argomenti:

  - [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\))

Di seguito vengono forniti alcuni esempio dell'utilizzo di Shell per modificare le proprietà delle cassette postali collegate.

In questo esempio viene utilizzato il comando **Get-Mailbox** per trovare tutte le cassette postali collegate nell'organizzazione.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')}

In questo esempio viene utilizzato il comando **Set-Mailbox** per limitare il numero di destinatari ammessi per i campi A: Cc: e Ccn: di un messaggio di posta elettronica a 500. Questo limite si applica a tutte le cassette postali collegate nell'organizzazione.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')} | Set-Mailbox -RecipientLimits 500

In questo esempio viene modificato l'account master collegato nella foresta account fabrikam.com associato a una cassetta postale collegata in una foresta Exchange.

    Set-Mailbox -Identity "Ayla Kol" -LinkedDomainController DC1.fabrikam.com -LinkedMasterAccount "fabrikam\robinw" -LinkedCredential:(Get-Credential fabrikam\administrator)

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver correttamente modificato le proprietà per una cassetta postale collegata, fare quanto segue:

  - Nell'interfaccia di amministrazione Exchange selezionare la cassetta postale e quindi fare clic su **Modifica** per visualizzare le proprietà o le funzionalità modificate. A seconda della proprietà modificata, la proprietà potrebbe essere visualizzata nel riquadro Dettagli per la cassetta postale selezionata.

  - In Shell, utilizzare il cmdlet **Get-Mailbox** per verificare le modifiche. Uno dei vantaggi dell'utilizzo di Shell è che è possibile visualizzare più proprietà per più cassette postali collegate. Nell'esempio precedente, in cui è stato modificato il numero massimo di destinatari, eseguendo questo comando viene verificato il nuovo valore.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')} | fl Name,RecipientLimits
    
    Nell'esempio precedente, in cui è stato modificato l'account master collegato, eseguire questo comando per verificare il nuovo valore.
    
        Get-Mailbox "Ayla Kol" | fl LinkedMasterAccount


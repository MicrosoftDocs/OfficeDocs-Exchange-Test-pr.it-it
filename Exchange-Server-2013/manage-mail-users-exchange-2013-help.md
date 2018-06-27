---
title: 'Gestire gli utenti di posta: Exchange 2013 Help'
TOCTitle: Gestire gli utenti di posta
ms:assetid: bb8b8804-f730-4ad7-9173-896a4965b90f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124381(v=EXCHG.150)
ms:contentKeyID: 50479865
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailUserWizardForm.NewMailUserIntroductionWizardPage
ms.translationtype: MT
---

# Gestire gli utenti di posta

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Gli utenti di posta sono simili ai contatti di posta. Entrambi possiedono indirizzi di posta elettronica esterni e contengono informazioni su persone esterne all'organizzazione Exchange o Exchange Online che possono essere visualizzate nella rubrica condivisa e in altri elenchi di indirizzi. Tuttavia, a differenza di un contatto di posta, un utente di posta dispone delle credenziali di accesso nell'organizzazione Exchange o Office 365 e può accedere alle risorse. Per ulteriori informazioni, vedere [Destinatari](recipients-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Creazione di un utente di posta

## Utilizzo di EAC per creare un utente di posta

1.  In EAC, accedere a **Destinatari** \> **Contatti** \> **Nuovo** \> **Utente di posta**.

2.  Nella casella **\* Alias** della pagina **Nuovo utente di posta** digitare l'alias per l'utente di posta. L'alias non può superare i 64 caratteri e deve essere univoco nella foresta. Questa casella è obbligatoria.

3.  Per specificare il tipo di indirizzo di posta elettronica per l'utente di posta, effettuare una delle operazioni seguenti:
    
      - per specificare un indirizzo di posta elettronica SMTP per l'indirizzo esterno dell'utente di posta, fare clic su **SMTP**.
        

        > [!NOTE]
        > Exchange convalida gli indirizzi SMTP per una formattazione corretta. Se una voce è incoerente con il formato SMTP, verrà visualizzato un messaggio di errore quando si fa clic su <STRONG>Salva</STRONG> per creare l'utente di posta.

    
      - Per specificare un tipo di indirizzo personalizzato, fare clic sul pulsante di opzione, quindi digitare il tipo di indirizzo. Ad esempio, è possibile specificare un indirizzo X.500, GroupWise o di Lotus Notes.

4.  Nella casella **\* Indirizzo di posta elettronica esterno** digitare l'indirizzo di posta elettronica esterno dell'utente. I messaggi inviati all'utente di posta elettronica vengono inoltrati a questo indirizzo di posta elettronica. Questa casella è obbligatoria.

5.  
    
    Selezionare una delle seguenti opzioni:
    
      - **Utente esistente**   Selezionare questa opzione per abilitare alla posta un utente esistente.
        
        Fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona utente - Intera foresta**. Questa finestra di dialogo visualizza un elenco di account utente nell'organizzazione che non sono abilitati alla posta o che non dispongono di cassette postali. Selezionare gli account utente che si desidera abilitare alla posta e fare clic su **OK**. Se si seleziona questa opzione, non è necessario fornire le informazioni sull'account utente perché esistono già in Active Directory.
    
      - **Nuovo utente**   Selezionare l'opzione per creare un nuovo account utente in Active Directory e abilitare alla posta l'utente. Se si seleziona questa opzione, sarà necessario fornire le informazioni richieste sull'account utente.

6.  
    
    Se è stata selezionata l'opzione **Nuovo utente** nel passaggio 5, riempire le seguenti caselle nella pagina **Nuovo utente di posta**. Altrimenti, andare al passo 7.
    
      - **Nome**   Utilizzare questa casella per digitare il nome dell'utente di posta.
    
      - **Iniziali**   Utilizzare questa casella per digitare le iniziali dell'utente di posta.
    
      - **Cognome**   Utilizzare questa casella per digitare il cognome dell'utente di posta.
    
      - **\* Nome visualizzato**   Utilizzare questa casella per digitare un nome visualizzato per l'utente. Questo è il nome che compare nell'elenco dei contatti nell'interfaccia di amministrazione di Exchange e nella rubrica dell'organizzazione. Per impostazione predefinita, questa casella contiene i nomi immessi nelle caselle **Nome di battesimo**, **Iniziali** e **Cognome**. Se queste caselle non sono state utilizzate, è necessario digitare un nome in questa casella perché è obbligatoria. Il nome non può superare i 64 caratteri.
    
      - **\* Nome**   Utilizzare questa casella per digitare un nome da assegnare all'utente di posta. Si tratta del nome elencato nel servizio directory. Questa casella contiene i nomi immessi nelle caselle **Nome**, **Iniziali** e **Cognome**. Se queste caselle non sono state utilizzate, è necessario digitare un nome in questa casella perché è obbligatoria. Il nome non può superare i 64 caratteri.
        

        > [!NOTE]
        > La casella <STRONG>Nome</STRONG> è disponibile solo in Exchange Server 2013. In Exchange Online non è disponibile.

    
      - **Unità organizzativa**   È possibile selezionare un'unità organizzativa diversa da quella predefinita (che corrisponde all'ambito dei destinatari). Se l'ambito dei destinatari è impostato a livello di foresta, il valore predefinito è impostato sul contenitore di utenti nel dominio contenente il computer su cui è in esecuzione l'interfaccia di amministrazione di Exchange. Se l'ambito dei destinatari viene impostato su un dominio specifico, per impostazione predefinita verrà selezionato il contenitore di utenti del dominio in questione. Se infine come ambito dei destinatari si sceglie una specifica unità organizzativa, per impostazione predefinita verrà selezionata l'unità organizzativa specificata.
        
        Per selezionare un'unità organizzativa diversa, scegliere il pulsante **Sfoglia**. La finestra di dialogo visualizzerà tutte le unità organizzative presenti nella foresta all'interno dell'ambito specificato. Selezionare l'unità organizzativa desiderata e fare clic su **OK**.
        

        > [!NOTE]
        > La casella <STRONG>Unità organizzativa</STRONG> è disponibile solo in Exchange Server 2013. In Exchange Online non è disponibile.

    
      - **\* Nome accesso utente** Digitare il nome utilizzato dall'utente di posta per accedere al dominio. Il nome di accesso dell'utente è costituito da un nome utente a sinistra del simbolo @ e da un suffisso a destra del simbolo. In genere, come suffisso si utilizza il nome del dominio in cui risiede l'account utente.
        

        > [!NOTE]
        > In Exchange Online, questa casella è etichettata come <STRONG>ID utente</STRONG>.

    
      - **\* Nuova password**   Utilizzare questa casella per digitare la password che l'utente di posta deve utilizzare per accedere al dominio.
        

        > [!NOTE]
        > Verificare che la password immessa sia conforme ai requisiti di lunghezza, complessità e cronologia del dominio in cui viene creato l'account utente.

    
      - **\* Conferma password**   Utilizzare questa casella per confermare la password digitata nella casella **Password**.
    
      - **Richiedi modifica della password al successivo accesso**   Selezionare questa casella di controllo se si desidera che l'utente di posta reimposti la password al primo accesso al dominio.
        
        Se si seleziona questa casella di controllo, al primo accesso l'utente di posta visualizzerà una finestra di dialogo in cui potrà modificare la password. L'utente di posta non potrà eseguire alcuna operazione finché la password non viene modificata.

7.  
    
    Al termine fare clic su **Salva** per creare l'utente di posta.

## Utilizzo della shell per creare un utente di posta

In questo esempio viene creato un account utente abilitato alla posta per Jeffrey Zeng in Exchange Server 2013 con i seguenti dettagli:

  - Il nome e il nome visualizzato è Jeffrey Zeng.

  - L'alias è jeffreyz.

  - L'indirizzo di posta elettronica esterno è jzeng@tailspintoys.com.

  - Il nome è Jeffrey e il cognome è Zeng.

  - Il nome di accesso è jeffreyz@contoso.com.

  - La password è Pa$$word1.

  - L'utente di posta verrà creato nell'unità organizzativa predefinita. Per specificare un'unità organizzativa diversa, è possibile utilizzare il parametro *OrganizationalUnit*.

<!-- end list -->

    New-MailUser -Name "Jeffrey Zeng" -Alias jeffreyz -ExternalEmailAddress jzeng@tailspintoys.com -FirstName Jeffrey -LastName Zeng -UserPrincipalName jeffreyz@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)

In questo esempio viene creato un account utente abilitato alla posta per Rene Valdes in Exchange Online.

    New-MailUser -Name "Rene Valdes" -Alias renev -ExternalEmailAddress renevaldes@fineartschool.edu -FirstName Rene -LastName Valdes -MicrosoftOnlineServicesID renev@contoso.com -Password (ConvertTo-SecureString -String 'P@ssw0rd' -AsPlainText -Force)

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione dell'utente di posta, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Contatti**. Il nuovo utente di posta viene visualizzato nell'elenco dei contatti. In **Tipo di contatto** il tipo è **Utente di posta**.

  - In Shell eseguire il comando seguente per visualizzare le informazioni sul nuovo utente di posta.
    
        Get-MailUser <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## Modifica delle proprietà dell'utente di posta

Dopo aver creato un utente di posta, è possibile apportare le modifiche e impostare proprietà aggiuntive utilizzando EAC o Shell.

È inoltre possibile modificare le proprietà di più cassette postali utente contemporaneamente. Per ulteriori informazioni, vedere Bulk edit mail users.

Il tempo stimato per il completamento dell'attività dipende dal numero di proprietà da visualizzare o modificare.

## Utilizzare EAC per modificare le proprietà delle cassette postali utente

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Contatti**.

2.  Nell'elenco dei contatti fare clic sull'utente di posta di cui si desidera modificare le proprietà, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Sulla pagina delle proprietà dell'utente di posta fare clic su una delle seguenti sezioni per visualizzare o modificare le proprietà.
    
      - General
    
      - Contact Information
    
      - Organization
    
      - Email Addresses
    
      - Mail Flow Settings
    
      - Member Of
    
      - MailTip

## Generale

Utilizzare la sezione **Generale** per visualizzare o modificare le informazioni di base sull'utente di posta.

  - **Nome**, **Iniziali**, **Cognome**

  - **\* Nome**   Questo è il nome che compare in Active Directory. Se viene modificato, non può superare i 64 caratteri.

  - **\* Nome visualizzato**    Questo nome viene visualizzato nella Rubrica dell'organizzazione, nel campo A e Da: del messaggio di posta elettronica e nell'elenco dei contatti in EAC. Questo nome non può contenere spazi vuoti prima o dopo il nome visualizzato.

  - **\* Nome accesso utente**   Il nome che l'utente utilizzerà per accedere al dominio. In Exchange Online, questo è l'ID utente utilizzato dall'utente per accedere a Office 365.

  - **Non visualizzare negli elenchi di indirizzi**   Selezionare questa casella di controllo per impedire la visualizzazione dell'utente di posta nella rubrica e negli altri elenchi di indirizzi definiti nell'organizzazione di Exchange. Dopo la selezione di questa casella di controllo, gli utenti possono comunque inviare messaggi al destinatario utilizzando l'indirizzo di posta elettronica.

  - **Richiedi modifica della password al successivo accesso**   Selezionare questa casella di controllo se si desidera che l'utente reimposti la password all'accesso successivo al dominio.
    

    > [!NOTE]
    > In Exchange Online questa casella non è disponibile.



Fare clic su **Altre opzioni** per visualizzare o modificare le seguenti proprietà aggiuntive:

  - **Unità organizzativa**   In questa casella di sola lettura è visualizzata l'unità organizzativa contenente l'account dell'utente di posta. Per spostare l'account verso un'unità organizzativa (OU) diversa, è necessario utilizzare Utenti e computer di Active Directory.
    

    > [!NOTE]
    > In Exchange Online questa casella non è disponibile.



  - **Attributi personalizzati**   In questa sezione vengono visualizzati gli attributi personalizzati definiti per l'utente di posta. Per specificare valori personalizzati per gli attributi, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). È possibile specificare fino a 15 attributi personalizzati per un destinatario.

## Informazioni di contatto

Utilizzare la sezione **Informazioni di contatto** per visualizzare o modificare le informazioni di contatto dell'utente. Le informazioni di questa pagina vengono visualizzate nella Rubrica. Fare clic su **Altre opzioni** per visualizzare caselle aggiuntive.


> [!TIP]
> Il campo <STRONG>Stato/provincia</STRONG> consente di creare le condizioni relative ai destinatari per i gruppi di distribuzione dinamici, i criteri per gli indirizzi di posta elettronica o gli elenchi di indirizzi.



## Organizzazione

Utilizzare la sezione **Organizzazione** per registrare informazioni dettagliate sul ruolo dell'utente nell'organizzazione. Queste informazioni vengono visualizzate nella rubrica. Inoltre, è possibile creare il diagramma di un'organizzazione virtuale a cui è possibile accedere dai client di posta elettronica quali Outlook.

  - **Titolo   **Questa casella di testo consente di visualizzare o modificare il titolo del destinatario.

  - **Reparto**   Utilizzare questa casella per visualizzare o modificare il nome del reparto in cui lavora l'utente. È possibile utilizzare questa casella per creare le condizioni relative ai destinatari per i gruppi di distribuzione dinamici, i criteri per gli indirizzi di posta elettronica o gli elenchi di indirizzi.

  - **Società**   Utilizzare questa casella per visualizzare o modificare il nome della società in cui lavora l'utente. È possibile utilizzare questa casella per creare le condizioni relative ai destinatari per i gruppi di distribuzione dinamici, i criteri per gli indirizzi di posta elettronica o gli elenchi di indirizzi.

  - **Manager**   Per aggiungere un manager, fare clic su **Sfoglia**. In **Seleziona responsabile**, selezionare una persona e quindi fare clic su **OK**.

  - **Superiore diretto**   Questo campo non può essere modificato. Un *subalterno* è un utente che risponde a un manager specifico. Se è stato specificato un responsabile per l'utente, quest'ultimo verrà visualizzato come subalterno nei dettagli della cassetta postale del responsabile. Ad esempio, Kari è il superiore di Chris e Kate, quindi Kari è specificata nella casella **Manager** per Chris e Kate e Chris e Kate sono visualizzati nella casella **Subalterni** nelle proprietà dell'account di Kari.

## Indirizzi di posta elettronica

Utilizzare la sezione **Indirizzi di posta elettronica** per visualizzare o modificare gli indirizzi di posta elettronica associati all'utente di posta. Sono inclusi l'indirizzo SMTP primario, l'indirizzo di posta elettronica esterno e gli indirizzi proxy associati dell'utente di posta. L'indirizzo SMTP primario (chiamato anche *indirizzo di risposta predefinito*) viene visualizzato in grassetto nell'elenco degli indirizzi, con il valore **SMTP** maiuscolo nella colonna **Tipo**. Per impostazione predefinita, una volta creato l'utente di posta, l'indirizzo SMTP primario e l'indirizzo di posta elettronica esterno coincidono.

  - **Aggiungi **  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere un nuovo indirizzo di posta elettronica per la cassetta postale. Selezionare uno dei seguenti tipi di indirizzo:
    
      - **SMTP**   Questo è il tipo di indirizzo predefinito. Fare clic su questo pulsante e quindi digitare il nuovo indirizzo SMTP nella casella **\* Indirizzo di posta elettronica**.
    
      - **Tipo di indirizzo personalizzato**   Fare clic su questo pulsante e digitare uno dei tipi di indirizzi di posta elettronica non SMTP supportati nella casella **\* Indirizzo di posta elettronica**.
        

        > [!NOTE]
        > Fatta eccezione per gli indirizzi X.400, Exchange non convalida gli indirizzi personalizzati per verificarne la corretta formattazione. È necessario verificare che l'indirizzo personalizzato specificato sia conforme ai requisiti di formato per tale tipo di indirizzo.



  - **Imposta indirizzo di posta elettronica esterno**   Utilizzare questa casella per modificare l'indirizzo esterno dell'utente di posta. I messaggi inviati all'utente di posta elettronica vengono inoltrati a questo indirizzo di posta elettronica.

  - **Aggiorna automaticamente gli indirizzi sulla base del criterio dell'indirizzo di posta elettronica applicato a questo destinatario   **Selezionare questa casella di controllo per aggiornare automaticamente gli indirizzi di posta elettronica dei destinatari in base alle modifiche apportate ai criteri degli indirizzi di posta elettronica nell'organizzazione. Tale casella è selezionata per impostazione predefinita.
    

    > [!NOTE]
    > In Exchange Online questa casella di controllo non è disponibile.



## Impostazioni del flusso di posta

Utilizzare la sezione **Impostazioni del flusso di posta** per visualizzare o modificare le impostazioni seguenti:

  - **Restrizioni di dimensione per i messaggi**   Queste impostazioni controllano la dimensione dei messaggi che l'utente di posta può inviare e ricevere. Fare clic su **Visualizza dettagli** per visualizzare e cambiare la dimensione massima dei messaggi inviati e ricevuti.
    
      - **Messaggi inviati**   Per specificare una dimensione massima per i messaggi inviati da questo utente, selezionare la casella di controllo **Dimensione massima messaggio (KB)** e digitare un valore nella casella. La dimensione dei messaggi deve essere compresa tra 0 e 2.097.151 KB. Se l'utente invia un messaggio di dimensioni superiori a quelle specificate, il messaggio viene restituito all'utente con un messaggio di errore descrittivo.
    
      - **Messaggi ricevuti**   Per specificare una dimensione massima per i messaggi ricevuti da questo utente, selezionare la casella di controllo **Dimensione massima messaggio (KB)** e digitare un valore nella casella. La dimensione dei messaggi deve essere compresa tra 0 e 2.097.151 KB. Se all'utente viene inviato un messaggio di dimensioni superiori a quelle specificate, questo verrà restituito al mittente con un messaggio di errore descrittivo.

  - **Restrizioni di recapito dei messaggi**   Queste impostazioni controllano i mittenti che possono inviare a questo utente di posta. Fare clic su **Visualizza dettagli** per visualizzare e cambiare queste restrizioni.
    
      - **Accetta messaggi da**   Utilizzare questa sezione per specificare chi può inviare messaggi a questo utente.
        
          - **Tutti i mittenti**   Selezionare questa opzione per specificare che l'utente può accettare messaggi da tutti i mittenti. Sono inclusi sia i mittenti nell'organizzazione di Exchange sia i mittenti esterni. In base all'impostazione predefinita, questo pulsante di opzione è selezionato. Questa opzione include gli utenti esterni solo se è stata deselezionata la casella di controllo **Richiedi autenticazione di tutti i mittenti**. Se si seleziona questa casella di controllo, i messaggi provenienti da utenti esterni saranno rifiutati.
        
          - **Solo i mittenti nell'elenco seguente**   Selezionare questa opzione per specificare che l'utente può accettare messaggi solo da un insieme specificato di mittenti nell'organizzazione di Exchange. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per visualizzare la pagina **Selezione destinatari**, in cui sono elencati tutti i destinatari dell'organizzazione Exchange. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").
        
          - **Richiedi autenticazione di tutti i mittenti**   Selezionare questa opzione per impedire agli utenti anonimi di inviare messaggi all'utente.
    
      - **Rifiuta messaggi da**   Utilizzare questa sezione per impedire ai contatti di inviare messaggi a questo utente.
        
          - **Nessun mittente**   Selezionare questa opzione per specificare che la cassetta postale non rifiuterà i messaggi provenienti dai mittenti nell'organizzazione di Exchange. In base all'impostazione predefinita, questo pulsante di opzione è selezionato.
        
          - **Mittenti nel seguente elenco**   Selezionare questa opzione per specificare che la cassetta postale rifiuterà i messaggi da un insieme specificato di mittenti nell'organizzazione di Exchange. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per visualizzare la pagina **Selezione destinatari**, in cui sono elencati tutti i destinatari dell'organizzazione Exchange. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").

## Membro di

Utilizzare la sezione **Membro di** per visualizzare un elenco dei gruppi di distribuzione o di sicurezza a cui appartiene questo utente. In questa pagina non è possibile modificare le informazioni sull'appartenenza. L'utente potrebbe soddisfare i criteri di uno o più gruppi di distribuzione dinamici nell'organizzazione. Tuttavia, i gruppi di distribuzione dinamici non sono visualizzati in questa pagina, perché la loro appartenenza viene calcolata ad ogni utilizzo.

## Avviso messaggio

Utilizzare la sezione **Avviso messaggio** per aggiungere un avviso per informare gli utenti dei problemi che potrebbero verificarsi se inviano un messaggio a questo destinatario. Un avviso messaggio è un testo che viene visualizzato sulla barra informazioni quando questo destinatario viene aggiunto nella riga A, Cc o Ccn di un nuovo messaggio di posta elettronica.


> [!NOTE]
> Gli avvisi messaggio possono includere tag HTML, ma gli script non sono consentiti. La lunghezza di un avviso messaggio personalizzato non può superare 175 caratteri visualizzati. I tag HTML non vengono conteggiati in tale limite.



## Modifica delle proprietà di un utente di posta tramite Shell

Le proprietà per un utente di posta sono archiviate sia in Active Directory che in Exchange. In generale, utilizzare i cmdlet **Get-User** e **Set-User** per visualizzare e modificare le proprietà delle informazioni sui contatti e sull'organizzazione. Utilizzare i cmdlet **Get-MailUser** e **Set-MailUser** per visualizzare o modificare le proprietà relative alla posta, quali indirizzi di posta elettronica, MailTip, attributi personalizzati e se l'utente di posta è nascosto dagli elenchi di indirizzi.

Utilizzare i cmdlet **Get-MailUser** e **Set-MailUser** per visualizzare e modificare le proprietà per gli utenti di posta. Per informazioni, vedere i seguenti argomenti:

  - [Get-User](https://technet.microsoft.com/it-it/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/it-it/library/aa998221\(v=exchg.150\))

  - [Get-MailUser](https://technet.microsoft.com/it-it/library/aa997254\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/it-it/library/aa995971\(v=exchg.150\))

Di seguito sono riportati alcuni esempi sull'utilizzo di Shell per modificare le proprietà dell'utente di posta.

In questo esempio viene impostato l'indirizzo di posta elettronica esterno per Pilar Pinilla.

    Set-MailUser "Pilar Pinilla" -ExternalEmailAddress pilarp@tailspintoys.com

In questo esempio vengono nascosti tutti gli utenti di posta dalla rubrica dell'organizzazione.

    Get-MailUser | Set-MailUser -HiddenFromAddressListsEnabled $true

In questo esempio viene impostata la proprietà Company per tutti gli utenti di posta di Contoso.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | Set-User -Company Contoso

In questo esempio viene impostata la proprietà CustomAttribute1 su un valore ContosoEmployee per tutti gli utenti di posta con valore Contoso nella proprietà Company.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Contoso')}| Set-MailUser -CustomAttribute1 ContosoEmployee

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver modificato correttamente le proprietà degli utenti di posta, effettuare le operazioni seguenti:

  - in EAC selezionare l'utente di posta e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare le proprietà modificate.

  - In Shell, utilizzare i cmdlet **Get-User** e **Get-MailUser** per verificare le modifiche. Uno dei vantaggi offerti dall'utilizzo di Shell è la possibilità di visualizzare più proprietà per più contatti di posta.
    
        Get-MailUser | Fl Name,CustomAttribute1 
    
    Nell'esempio precedente in cui la proprietà Company è stata impostata su Contoso per tutti i contatti di posta, utilizzare il comando seguente per verificare le modifiche:
    
        Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | FL Name,Company
    
    nell'esempio precedente in cui per tutti gli utenti di posta la proprietà CustomAttribute1 è stata impostata su ContosoEmployee, utilizzare il comando seguente per verificare le modifiche.
    
        Get-MailUser | Fl Name,CustomAttribute1 

## Modifica in blocco degli utenti di posta

Per modificare le proprietà selezionate per più utenti di posta, è possibile utilizzare EAC. Quando si selezionano due o più utenti di posta dall'elenco dei contatti in EAC, è possibile modificare in blocco le proprietà visualizzate nel riquadro dei dettagli. Quando si modifica una di queste proprietà, la modifica viene applicata a tutti i destinatari selezionati.

Quando si modificano in blocco gli utenti di posta, è possibile modificare le area di proprietà seguenti:

  - **Informazioni contatto**   Modificare le proprietà condivise quali indirizzo, CAP e città.

  - **Organizzazione**   Modificare le proprietà condivise quali nome del reparto, ragione sociale e responsabile a cui riportano i contatti o gli utenti di posta selezionati.

## Utilizzo di EAC per modificare gli utenti di posta in blocco

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Contatti**.

2.  Nell'elenco dei contatti, selezionare due o più utenti di posta. Non è possibile modificare in blocco un insieme di contatti e utenti di posta.
    

    > [!TIP]
    > È possibile selezionare più utenti di posta contigui tenendo premuto il tasto Maiusc e facendo clic sul primo utente di posta, quindi selezionando l'ultimo utente da modificare. Per selezionare più utenti di posta, tenere premuto il tasto Ctrl e fare clic su ciascun utente da modificare.



3.  Nel riquadro Dettagli, in **Modifica in blocco**, fare clic su **Aggiorna** in **Informazioni contatto** oppure **Organizzazione**.

4.  Apportare le modifiche nella pagina delle proprietà e quindi salvare le modifiche.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta modifica in blocco degli utenti di posta, effettuare una delle seguenti operazioni:

  - in EAC selezionare gli utenti di posta modificati in blocco, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare le proprietà modificate.

  - In Shell, utilizzare il cmdlet **Get-User** per verificare le modifiche. Si supponga ad esempio che è stata utilizzata la funzione di modifica in blocco in EAC per modificare il manager e l'ufficio per tutti gli utenti di posta di un'azienda fornitrice denominata A. Datum Corporation. Per verificare le modifiche, è possibile utilizzare il seguente comando in Shell:
    
        Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Adatum')} | fl Name,Office,Manager

## Utilizzare la sincronizzazione delle directory per gestire gli utenti di posta in Exchange Online

In questa sezione vengono fornite informazioni sulla gestione degli utenti di posta elettronica utilizzando la sincronizzazione delle directory in Exchange Online. La sincronizzazione delle directory è disponibile per i clienti ibridi locali e ospitate nel cloud delle cassette postali e per i clienti di Exchange Online completamente ospitati con Active Directory è locale.


> [!NOTE]
> Se si utilizza la sincronizzazione della directory per gestire i destinatari, è comunque possibile aggiungere e gestire gli utenti nell'interfaccia di amministrazione di Office 365. Tuttavia questi non verranno sincronizzati con Active Directory in locale poiché la sincronizzazione della directory sincronizza solamente i destinatari dall'Active Directory locale al cloud.




> [!NOTE]
> Si consiglia di utilizzare la sincronizzazione della directory con le seguenti funzionalità: 
> <UL>
> <LI>
> <P><STRONG>Outlook attendibili e degli elenchi di mittenti bloccati</STRONG> Quando sincronizzate al servizio, tali elenchi avrà la precedenza sul filtro nel servizio di posta indesiderata. Consente agli utenti di gestire i propri elenchi attendibili e mittenti bloccati in base al dominio o per utente.</P>
> <LI>
> <P><STRONG>Directory Based Edge Blocking (DBEB)</STRONG> Per ulteriori informazioni su DBEB, vedere <A href="https://technet.microsoft.com/it-it/library/dn600322(v=exchg.150)">Utilizzare il blocco Edge basato su directory per rifiutare i messaggi inviati a destinatari non validi</A>.</P>
> <LI>
> <P><STRONG>Quarantena posta indesiderata utente finale</STRONG> Per accedere alla quarantena di posta indesiderata utente finale, utenti finali devono avere un ID utente di Office 365 valido e una password. I clienti con cassette postali locali devono essere utenti di posta elettronica valido.</P>
> <LI>
> <P><STRONG>Regole di trasporto</STRONG> Quando si utilizza la sincronizzazione delle directory, gli utenti di Active Directory esistenti e i gruppi vengono caricati automaticamente nel cloud e può quindi creare regole di trasporto che gli utenti specifici di destinazione e/o gruppi senza dover aggiungere manualmente tramite EAC o Windows PowerShell remoto. Si noti che <A href="https://go.microsoft.com/fwlink/?linkid=507569">i gruppi di distribuzione dinamico</A> non possono essere sincronizzati tramite la sincronizzazione delle directory.</P></LI></UL>



**Informazioni preliminari**

Ottenere le autorizzazioni necessarie e preparare la sincronizzazione delle directory, come descritto in [Preparazione per la sincronizzazione delle directory](https://go.microsoft.com/fwlink/p/?linkid=308908).

Per sincronizzare le directory degli utenti

1.  Attivare la sincronizzazione delle directory, come descritto in [attivare la sincronizzazione di directory](https://go.microsoft.com/fwlink/p/?linkid=308909).

2.  Impostare il computer per la sincronizzazione della directory, come descritto in [Impostare il computer per la sincronizzazione della directory](http://go.microsoft.com/fwlink/p/?linkid=308911).

3.  Sincronizzare le directory, come descritto in [Utilizzare Configurazione guidata per sincronizzare le directory](http://go.microsoft.com/fwlink/?linkid=308912).
    

    > [!IMPORTANT]
    > Al termine della Configurazione guidata dello strumento di sincronizzazione di Azure Active Directory, viene creato l'account <STRONG>MSOL_AD_SYNC</STRONG> nella foresta Active Directory. Tale account viene utilizzato per leggere e sincronizzare le informazioni dell'Active Directory locale. Per un corretto funzionamento della sincronizzazione della directory, assicurarsi che TCP 443 sul server di sincronizzazione della directory locale sia aperto.



4.  Attivare gli utenti sincronizzati, come descritto in [Attiva utenti sincronizzati](http://go.microsoft.com/fwlink/p/?linkid=308913).

5.  Gestione della sincronizzazione della directory, come descritto in [Gestione della sincronizzazione della directory](http://go.microsoft.com/fwlink/p/?linkid=308915).

6.  Verificare che Exchange Online è la sincronizzazione in modo corretto. In EAC, accedere a **destinatari** \> **contatti** e visualizzazione che l'elenco degli utenti è stato correttamente sincronizzato dall'ambiente locale.


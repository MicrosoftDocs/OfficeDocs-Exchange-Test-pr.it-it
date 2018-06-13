---
title: 'Configurare gruppi di Office 365 con ambiente ibrido di Exchange locale: Exchange 2013 Help'
TOCTitle: Configurare gruppi di Office 365 con ambiente ibrido di Exchange locale
ms:assetid: 184dfcfe-4b8e-450a-adc6-e647213b9501
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt668829(v=EXCHG.150)
ms:contentKeyID: 72513062
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurare gruppi di Office 365 con ambiente ibrido di Exchange locale

 

_**Ultima modifica dell'argomento:**2016-12-06_

In questo articolo vengono riportate informazioni su come consentire agli utenti di Exchange locale di utilizzare i gruppi di Office 365 in ambiente ibrido.

I gruppi sono un servizio di Office 365 che consente ai team di comunicare, pianificare riunioni e collaborare ai documenti più facilmente. Tutte le informazioni condivise (dai messaggi di posta elettronica inviati al gruppo, ai file archiviati in OneDrive for Business del gruppo o nelle raccolte di SharePoint) sono disponibili per ogni membro del gruppo. Se è stata configurata una distribuzione ibrida tra l'organizzazione di Exchange locale e Office 365, è possibile rendere disponibili i gruppi creati in Office 365 agli utenti locali, seguendo i passaggi descritti in questo argomento.


> [!IMPORTANT]
> L'utilizzo dei gruppi di Office 365 con gli utenti locali in una distribuzione ibrida di Exchange è una nuova funzionalità. Essendo molto recente, potrebbero verificarsi problemi durante la configurazione. Consultare la sezione Problemi noti alla fine di questo argomento per visualizzare le correzioni ai problemi che potrebbero verificarsi.



## Prerequisiti

Prima di iniziare, verificare di aver effettuato le operazioni seguenti:

  - Acquisto delle licenze per Azure Active Directory Premium per il tenant. Questo è necessario per abilitare la caratteristica writeback gruppi in Azure Active Directory Connect.

  - Configurazione di una distribuzione ibrida tra l'organizzazione di Exchange locale e Office 365 e verifica del corretto funzionamento. Per ulteriori informazioni sulle distribuzioni ibride di Exchange, vedere:
    
      - [Distribuzioni ibride di Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md)
    
      - [Prerequisiti per la distribuzione ibrida](hybrid-deployment-prerequisites-exchange-2013-help.md)

  - L'installazione di una versione supportata dell'integrazione di Exchange locale con i gruppi di Office 365 è disponibile in CU1 e versioni più recenti di Exchange 2016, nonché in CU11 e versioni più recenti di Exchange 2013. Tuttavia, l'ambiente ibrido di Exchange richiede l'installazione dell'ultima versione dell'aggiornamento cumulativo (CU) di Exchange 2013 o Exchange 2016 nei server di Exchange locali. Se non è possibile installare l'ultima versione di CU, è possibile utilizzare l'aggiornamento cumulativo rilasciato immediatamente prima di quello corrente.

  - Configurazione di Single Sign-On con Azure Active Directory Connect (Azure AD Connect). Questa impostazione è necessaria per consentire agli utenti di fare clic su **Visualizza file del gruppo** o sui collegamenti degli allegati cloud nei messaggi di posta elettronica di gruppo.
    
    Quando si configura l'accesso Single Sign-On su Azure AD Connect in una distribuzione ibrida di Exchange, è opportuno utilizzare la sincronizzazione delle password. Utilizzare Active Directory Federation Services (AD FS) soltanto nei casi seguenti: l'utente fa parte di una grande organizzazione; sono presenti distribuzioni locali di Active Directory complesse (ad esempio, foreste Active Directory multiple); un altro prodotto Microsoft necessita di AD FS per essere eseguito con Office 365 oppure quando, a causa di criteri di conformità, non è possibile sincronizzare le password all'esterno della rete locale. Per ulteriori informazioni su Single Sign-On, vedere [Integrazione delle identità locali con Azure Active Directory](http://go.microsoft.com/fwlink/p/?linkid=723513).

## Consentire writeback gruppi in Azure AD Connect

1.  Nella procedura guidata di Azure AD Connect, selezionare **Personalizza le opzioni di sincronizzazione**, quindi fare clic su **Avanti**.

2.  Nella pagina **Connessione ad Azure AD**, immettere le credenziali di Office 365 e quelle locali. Fare clic su **Avanti**.

3.  Nella pagina delle **caratteristiche facoltative**, verificare che le opzioni configurate in precedenza siano ancora selezionate. Le opzioni selezionate più frequentemente sono **Exchange ibrido** e **Sincronizzazione delle password hash**.

4.  Selezionare **writeback gruppi**, quindi fare clic su **Avanti**.

5.  Nella pagina **Writeback** selezionare un'unità organizzativa Active Directory per archiviare gli oggetti sincronizzati da Office 365 all'organizzazione locale, quindi fare clic su **Avanti**.

6.  Nella pagina **Pronto per la configurazione** fare clic su **Configura**.

7.  Una volta completata la procedura guidata, fare clic su **Esci** nella pagina **Configurazione completata**.

8.  Aprire Utenti e computer di Active Directory in un controller di dominio Active Directory, quindi individuare l'account utente che inizia con **AAD\_**. Prendere nota del nome dell'account.

9.  Aprire Exchange Management Shell su un server di Exchange locale ed eseguire i comandi seguenti.
    
        $AzureADConnectSWritebackAccount = <AAD_ account name from step 8>
        
        $GroupsOU = <writeback Active Directory OU selected in step 5>
        
        Import-Module "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1"
        
        Initialize-ADSyncGroupWriteBack -ADConnectorAccount $AzureADConnectSWritebackAccount -GroupWriteBackContainerDN $GroupsOU

## Configurare un dominio di gruppo

Il dominio SMTP principale di un gruppo di Office 365 viene definito come *dominio di gruppo*. Per impostazione predefinita, il dominio accettato automaticamente nell'organizzazione viene selezionato come dominio di gruppo. Per aggiungere un dominio di gruppo dedicato, è possibile seguire la procedura riportata di seguito. Per ulteriori informazioni sul supporto multidominio per i gruppi di Office 365, consultare [Supporto multidominio per i gruppi di Office 365](https://support.office.com/it-it/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a)

1.  Aggiungere il nuovo dominio all'organizzazione Office 365. Per informazioni di supporto su come aggiungere un dominio a Office 365, consultare [Aggiungere utenti e domini in Office 365](https://support.office.com/it-it/article/aggiungere-utenti-e-domini-in-office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611?ui=it-it%26rs=it-it%26ad=it)

2.  Aggiungere il dominio di gruppo come dominio accettato nell'organizzazione di Exchange locale utilizzando il comando seguente. Questa operazione è necessaria per utilizzare il connettore di invio ibrido per recapitare la posta in uscita al dominio di gruppo in Office 365.
    
        New-AcceptedDomain -Name groups.contoso.com -DomainName groups.contoso.com -DomainType InternalRelay

3.  Creare i seguenti record DNS pubblici con il provider DNS.
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><p>Nome del record DNS</p></th>
    <th><p>Tipo di record DNS</p></th>
    <th><p>Valore del record DNS</p></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>groups.contoso.com</p></td>
    <td><p>MX</p></td>
    <td><p>groups-contoso-com.mail.protection.outlook.com</p>

    > [!NOTE]
    > Il formato di questo valore del record DNS è <EM>&lt;domain key&gt;</EM>.mail.protection.outlook.com. Per individuare la propria chiave di dominio, consultare <A href="https://support.office.com/it-it/article/raccogliere-le-informazioni-necessarie-per-creare-record-dns-di-office-365-77f90d4a-dc7f-4f09-8972-c1b03ea85a67?ui=it-it%26rs=it-it%26ad=it">Raccogliere le informazioni necessarie per creare record DNS di Office 365</A>.


</td>
    </tr>
    <tr class="even">
    <td><p>autodiscover.groups.contoso.com</p></td>
    <td><p>CNAME</p></td>
    <td><p>autodiscover.outlook.com</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!WARNING]
    > Se il record MX DNS per il dominio di gruppo è impostato sul server di Exchange locale, il flusso di posta elettronica non funzionerà correttamente tra gli utenti locali dell'organizzazione di Exchange e il gruppo di Office 365.



4.  Aggiungere il dominio di gruppo al connettore di invio ibrido, creato dalla procedura guidata di configurazione ibrida nell'organizzazione di Exchange locale, usando il comando seguente.
    
        Set-SendConnector -Identity "Outbound to Office 365" -AddressSpaces "contoso.mail.onmicrosoft.com","groups.contoso.com"
    

    > [!NOTE]
    > Se il connettore di invio non viene aggiornato o se il dominio del gruppo non viene aggiunto come dominio accettato nell'organizzazione di Exchange locale, i messaggi inviati da una cassetta postale locale non verranno recapitati al gruppo, a meno che il gruppo non sia configurato per ricevere la posta da mittenti esterni.



## Come verificare se l'operazione ha avuto esito positivo

Per assicurarsi che i gruppi funzionino con la distribuzione ibrida di Exchange, è necessario sottoporli a test utilizzando una cassetta postale locale e una cassetta postale spostata dall'organizzazione locale in Office 365. Seguire i passaggi descritti nelle sezioni seguenti per ogni test.

## Test mediante una cassetta postale locale

1.  Aggiungere una cassetta postale locale a un gruppo di Office 365.

2.  Aggiungere una cassetta postale di Office 365 allo stesso gruppo di Office 365.

3.  Accedere alla cassetta postale di Office 365 mediante Outlook sul web.

4.  Inviare un messaggio al gruppo tramite la cassetta postale di Office 365.

5.  Aprire la cassetta postale locale mediante Outlook 2016 o Outlook sul web.

6.  Verificare che la cassetta postale abbia ricevuto un messaggio di posta elettronica contenente il post inviato al gruppo di Office 365.

7.  Nella stessa cassetta postale, scrivere una risposta al messaggio e inviarlo al gruppo.

8.  Verificare che il messaggio possa essere visualizzato da tutti i membri del gruppo.

## Test mediante una cassetta postale spostata in Office 365

1.  Spostare una cassetta postale dell'organizzazione di Exchange locale in Office 365.

2.  Aggiungere la cassetta postale a un gruppo di Office 365.

3.  In una nuova sessione del browser, accedere alla cassetta postale che è stata spostata in Office 365.

4.  In Outlook sul web, verificare che il gruppo sia elencato nella barra di spostamento sinistra.

5.  Inviare un messaggio al gruppo.

6.  Verificare che il messaggio possa essere visualizzato da tutti i membri del gruppo.

## Problemi noti

  - **I gruppi non vengono visualizzati per le cassette postali spostate in Office 365** Quando un utente viene spostato dall'organizzazione di Exchange locale in Office 365, i gruppi non vengono visualizzati nel riquadro di spostamento sinistro in Outlook o Outlook sul web. Per correggere il problema, rimuovere la cassetta postale da qualsiasi gruppo di cui fa parte e aggiungerla nuovamente a ogni gruppo.

  - **I nuovi gruppi non vengono visualizzati nell'elenco indirizzi globale (GAL) locale di Exchange** Quando viene creato un nuovo gruppo in Office 365, questo non verrà visualizzato automaticamente nel GAL locale. Per correggere il problema, aprire Exchange Management Shell su un server di Exchange locale ed eseguire il seguente comando.
    
        Update-Recipient "<group name>"

  - **I gruppi non ricevono messaggi da parte di utenti locali** Un utente locale non sarà in grado di inviare messaggi a un gruppo di Office 365 quando si verificano le seguenti condizioni:
    
      - Il dominio di gruppo è configurato come dominio autorevole nell'organizzazione di Exchange locale.
    
      - Il gruppo è stato creato di recente e le relative informazioni non sono ancora state scritte nell’Active Directory locale.
    
    Questo problema verrà risolto automaticamente all’esecuzione della sincronizzazione tra Office 365 e l’organizzazione locale da parte di Azure AD Connect. La sincronizzazione di Azure AD Connect avviene ogni 30 minuti.

  - **Gli utenti locali non possono utilizzare i collegamenti inclusi nei piè di pagina dei messaggi del gruppo**Gli utenti locali non possono utilizzare i collegamenti **Visualizza conversazioni del gruppo** o **Annulla sottoscrizione** inclusi nel piè di pagina di ogni messaggio inviato al gruppo. Per annullare la sottoscrizione a un gruppo, gli utenti locali possono contattare un amministratore del gruppo.

  - **La posta inviata all'indirizzo SMTP secondario di un gruppo non può essere recapitata** Quando più indirizzi di posta elettronica vengono aggiunti a un gruppo, solo l'indirizzo SMTP principale viene scritto nell’Active Directory locale. Se un utente locale tenta di inviare un messaggio all'indirizzo SMTP secondario di un gruppo, il messaggio non verrà recapitato. Per evitare questo problema, configurare un solo indirizzo SMTP su ogni gruppo.

  - **Gli utenti locali non possono diventare amministratori di un gruppo** Gli utenti locali non possono accedere direttamente allo spazio del gruppo. Per questo motivo, non possono essere aggiunti come amministratori di un gruppo.

  - **Il recapito della posta esterna a un gruppo non riesce se è stato abilitato il flusso di posta centralizzato** Quando si abilita il flusso di posta centralizzato, i messaggi inviati da un utente esterno a un gruppo non vengono recapitati, anche se il gruppo consente la ricezione di posta da mittenti esterni.

  - **Gli utenti locali non riescono a inviare posta come gruppo** Un utente locale che tenta di inviare un messaggio come gruppo di Office 365 visualizzerà un errore di autorizzazione negata, anche se nel gruppo hanno ricevuto le autorizzazioni "Invia come". Le autorizzazioni "Invia come" di un gruppo funzionano soltanto per gli utenti di cassette postali di Exchange Online.

  - **La selezione di un gruppo dal pannello di navigazione a sinistra di Outlook non consente di aprire la cassetta postale del gruppo** Outlook utilizza l'URL d'individuazione automatica per aprire una cassetta postale di gruppo. Se l'indirizzo di posta elettronica principale del gruppo si trova in un dominio che non punta all'URL di individuazione automatica di Office 365 (autodiscover.outlook.com), Outlook non riuscirà ad aprire la cassetta postale del gruppo. Per risolvere il problema, è possibile effettuare il provisioning dei gruppi con un indirizzo principale del dominio che punta all'URL di individuazione automatica di Office 365. È possibile configurare un criterio per l'indirizzo di posta elettronica al fine di aggiungere un indirizzo principale a tutte le cassette postali del gruppo che puntano all'URL di individuazione automatica di Office 365. Per maggiori dettagli, consultare [Supporto multidominio per i gruppi di Office 365](https://support.office.com/it-it/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a)


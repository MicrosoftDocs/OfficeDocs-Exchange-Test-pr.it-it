---
title: 'Configurazione di una relazione di trust federativa: Exchange 2013 Help'
TOCTitle: Configurazione di una relazione di trust federativa
ms:assetid: 7c2b539f-faed-4374-8578-9f329ca628db
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657462(v=EXCHG.150)
ms:contentKeyID: 50480959
ms.date: 03/28/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurazione di una relazione di trust federativa

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2017-07-26_

Un trust federativo stabilisce una relazione di trust tra una organizzazione Microsoft Exchange 2013 e il sistema di autenticazione di Azure Active Directory. Configurando una relazione di trust federativa, è possibile configurare la condivisione federata con altre organizzazioni Exchange per condividere informazioni sulla disponibilità degli utenti tra i destinatari. La condivisione federata può essere configurata tra due organizzazioni Exchange 2013 federate o tra un'organizzazione Exchange 2013 federata e organizzazioni Exchange 2010 federate. È inoltre possibile impostare la condivisione con un'organizzazione Office 365.


> [!NOTE]
> La creazione di una relazione di trust federativa è uno dei diversi passaggi della configurazione della condivisione federata nell'organizzazione di Exchange. Per esaminare tutti i passaggi, vedere <A href="configure-federated-sharing-exchange-2013-help.md">Configurare la condivisione federata</A>.



Per altre attività di gestione relative alla federazione, vedere [Procedure di federazione](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Questa funzionalità di Exchange Server 2013 non è completamente compatibile con Office 365 utilizzato da 21Vianet in Cina e potrebbe essere soggetta a limitazioni. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/?linkid=313640">Informazioni su Office 365 utilizzato da 21Vianet</A>.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 30 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni calendario e condivisione" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Il dominio utilizzato per stabilire una relazione di trust federativa deve essere risolvibile da Internet. Pertanto, è necessario che il dominio sia registrato con un registrar e che la zona DNS per il dominio sia ospitata su un server DNS accessibile da Internet. Se l'organizzazione riceve un messaggio di posta elettronica da Internet per il dominio, tali requisiti sono già soddisfatti.

  - Sarà necessario aggiungere un record TXT ai propri DNS pubblici. Rivedere i requisiti per l'aggiunta di un record TXT con l'organizzazione che ospita i record DNS pubblici.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Entrambe le organizzazioni di Exchange in una relazione di condivisione federata devono utilizzare lo stesso sistema di autenticazione Azure AD per le relative relazioni di trust federative. Tale requisito viene applicato quando si configura la condivisione federata tra due organizzazioni di Exchange locali o tra un'organizzazione Exchange locale e Exchange ospitata da [Office 365](https://go.microsoft.com/fwlink/?linkid=392576).

  - Quando viene creato un trust federativo con il sistema di autenticazione di Azure AD per l'organizzazione di Exchange 2013, il trust federativo utilizza l'istanza business del sistema di autenticazione di Azure AD. Tuttavia, altre organizzazioni Exchange federate con le versioni precedenti di Exchange e relazioni di trust federative esistenti possono utilizzare l'istanza business o consumer del sistema di autenticazione di Azure AD.
    
    Le organizzazioni di Exchange seguenti utilizzano l'istanza business del sistema di autenticazione di Azure AD per impostazione predefinita:
    
      - Le organizzazioni Exchange 2013 utilizzando la procedura guidata **Abilitare trust federativo** e certificati autofirmati per una relazione di trust federativa.
    
      - Le organizzazioni Exchange 2010 SP1 o successive utilizzando la procedura guidata **Nuovo trust federativot** e certificati autofirmati per una relazione di trust federativa.
    
      - Le organizzazioni di Exchange ospitate da Office 365, ad esempio Exchange Online.
    
    Le organizzazioni di Exchange seguenti utilizzano l'istanza del consumer del sistema di autenticazione di Azure AD per impostazione predefinita:
    
      - La versione di produzione (RTM) delle organizzazioni di Exchange 2010 utilizzano i certificati rilasciati da autorità di certificazione di terze parti.
    
    È consigliabile che tutte le organizzazioni di Exchange utilizzino l'istanza business del sistema di autenticazione di Azure AD per le relazioni di trust federative. Prima di configurare la condivisione federata tra due organizzazioni Exchange, è necessario verificare quale istanza del sistema di autenticazione di Azure AD sta utilizzando ciascuna organizzazione Exchange per tutte le relazioni di trust federativa. Per determinare quale istanza del sistema di autenticazione di Azure AD una organizzazione Exchange sta utilizzando per una relazione di trust federativa, eseguire il seguente comando Shell.
    
        Get-FederationInformation -DomainName <hosted Exchange domain namespace>
    
    L'istanza business restituisce un valore di `<uri:federation:MicrosoftOnline>` per il parametro *TokenIssuerURIs*.
    
    L'istanza consumer restituisce un valore di `<uri:WindowsLiveID>` per il parametro *TokenIssuerURIs*.
    
    Per configurare una condivisione federata con una organizzazione Exchange che possiede già una relazione di trust federativa che utilizza l'istanza business del sistema di autenticazione di Azure AD, seguire la procedura indicata. Questi passi sono tutto quello che occorre per creare una relazione di trust federativa che può essere utilizzata per abilitare la condivisione tra due organizzazioni Exchange 2013 o tra una organizzazione Exchange 2013 e una organizzazione Exchange 2010 che già utilizza una istanza business del sistema di autenticazione di Azure AD.
    
    Per configurare la condivisione federata tra l'organizzazione Exchange 2013 e un'organizzazione Exchange con una esistente relazione di trust federativa che utilizza l'istanza consumer del sistema di autenticazione di Azure AD, l'organizzazione Exchange che utilizza l'istanza consumer deve installare Exchange 2010 SP2 o versioni successive o effettuare l'aggiornamento a Exchange 2013. Se si decide di installare Exchange 2010 SP2 o versione successiva, utilizzare la procedura guidata **Nuovo trust federativo** per rimuovere e creare di nuovo i domini federati e le relazioni di trust federative. Una volta ricreate le relazioni di trust federative, viene utilizzata l'istanza business del sistema di autenticazione di Azure AD.

## Creazione e configurazione di una relazione di trust federativa tramite interfaccia di amministrazione di Exchange

1.  Su un server Exchange 2013 della propria organizzazione locale, andare a **Organizzazione** \> **Condivisione**.

2.  Fare clic su **Abilita** per avviare la procedura guidata **Abilitare trust federativot**.

3.  Una volta completata la procedura guidata, fare clic su **Chiudi**.

4.  Nella sezione **Trust federativo** della scheda **Condivisione**, fare clic su **Modifica**.

5.  In **Domini abilitati alla condivisione**, acccanto a **Passo 1**, fare clic su **Sfoglia**.

6.  In **Seleziona domini accettati**, selezionare dall'elenco il dominio condiviso primario e fare clic su **OK**.
    

    > [!NOTE]
    > Il dominio selezionato verrà utilizzato per configurare l'OrgID per la relazione di trust federativa. Per ulteriori informazioni sull'OrgID, vedere <A href="federation-exchange-2013-help.md">Federazione</A>.



7.  Annotare la stringa di prova del dominio che viene generata per il dominio condiviso primario. Questa stringa verrà utilizzata per creare un record TXT sul proprio server DNS pubblico.
    

    > [!IMPORTANT]
    > La stringa di prova del dominio federato è costituita da caratteri alfanumerici. Per evitare errori di immissione, si raccomanda di copiare la stringa dall'interfaccia di amministrazione di Exchange e incollarla in un editor di testo come Blocco note. Sarà poi possibile copiare la stringa dall'editor di testo agli Appunti e incollarla nel campo <STRONG>Testo</STRONG> quando si crea il record TXT. Se il record TXT viene creato utilizzando una stringa di prova del dominio federato non corretta, il sistema di autenticazione di Azure AD non sarà in grado di verificare la proprietà del dominio e questo non potrà essere aggiunto nell'identificatore dell'organizzazione federativa.



8.  In **Passo 2**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere domini aggiuntivi alla relazione di trust federativa per l'indirizzo di posta elettronica che verrà utilizzato dagli utenti nell'organizzazione che richiedono una funzionalità di condivisione federata. Ad esempio, se sono presenti utenti che utilizzano un sottodominio nei loro indirizzi di posta elettronica quali sales.contoso.com, si aggiungerà il dominio sales.contoso.com alla relazione di trust federativa.
    

    > [!NOTE]
    > Una stringa di prova del dominio federato verrà creata per ciascun dominio aggiuntivo selezionato. Sul server DNS pubblico si devono creare record TXT separati per ciascun dominio aggiuntivo.



9.  Utilizzando la stringa di prova del dominio federato creata per ciascun dominio, creare un record TXT sul server DNS pubblico per ciascuno di questi domini aggiuntivi. A seconda del piano di aggiornamenti dell'host DNS pubblico, la replica delle modifiche DNS può richiedere 15 minuti o più.

10. Dopo avere creato e replicato i record TXT, fare clic su **Aggiorna**.

## Utilizzo di Shell per creare e configurare una relazione di trust federativa

1.  Eseguire questo comando per creare un identificatore della chiave del soggetto univoco per il certificato della relazione di trust federativa:
    
        $ski = [System.Guid]::NewGuid().ToString("N")

2.  Utilizzare questa sintassi per creare un certificato autofirmato per questo tipo di relazione di trust:
    
        New-ExchangeCertificate -FriendlyName "<Descriptive Name>" -DomainName <domain> -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
    
    In questo esempio viene creato un certificato autofirmato per la relazione di trust federativa con il sistema di autenticazione di Azure AD. Il certificato utilizza il valore del nome descrittivo di Condivisione federata di Exchange e il valore del dominio è recuperato dalla variabile dell'ambiente di **USERDNSDOMAIN**.
    
        New-ExchangeCertificate -FriendlyName "Exchange Federated Sharing" -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski

3.  Per creare la relazione di trust federativa e distribuire automaticamente il certificato autofirmato creato nel passaggio precedente ai server Exchange nell'organizzazione, usare questa sintassi:
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "<FriendlyName>"} | New-FederationTrust -Name "<Descriptive Name>"
    
    In questo esempio viene creata la relazione di trust federativa denominata Autenticazione di Azure AD e viene distribuito il certificato autofirmato denominato Condivisione federata di Exchange.
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "Exchange Federated Sharing"} | New-FederationTrust -Name "Azure AD Authentication"

4.  Utilizzare questa sintassi per ottenere la prova del record TXT della proprietà del dominio necessaria per qualsiasi dominio che si configura per la relazione di trust federativa.
    
        Get-FederatedDomainProof -DomainName <domain>
    
    In questo esempio viene restituita la prova del record TXT della proprietà del dominio necessaria per il dominio condiviso principale contoso.com.
    
        Get-FederatedDomainProof -DomainName contoso.com
    
    **Note**:
    
      - Ogni dominio o sottodominio configurato per la relazione di trust federativa richiede una prova del record TXT della proprietà del dominio, pertanto potrebbe essere necessario eseguire questo comando più volte utilizzando valori *DomainName* diversi.
    
      - È consigliabile copiare la stringa di prova del dominio facendo clic con il pulsante destro del mouse in Shell, selezionando **Contrassegna**, quindi il valore **Prova** e infine premendo Invio per utilizzarla quando si crea il record TXT. Se il record TXT viene creato con una stringa di prova del dominio federato non corretta, il sistema di autenticazione di Azure AD non sarà in grado di verificare la proprietà del dominio e questo non potrà essere aggiunto nell'identificatore dell'organizzazione federativa.

5.  Utilizzando le informazioni fornite nel passaggio precedente, creare record TXT nel server DNS pubblico in ogni dominio che verrà incluso nella relazione di trust federativa. A seconda del piano di aggiornamenti dell'host DNS pubblico, la replica delle modifiche DNS può richiedere 15 minuti o più. Continuare dopo aver verificato che i nuovi record TXT siano disponibili.

6.  Eseguire questo comando per recuperare i metadati e il certificato da Azure AD:
    
        Set-FederationTrust -RefreshMetadata -Identity "Azure AD authentication"

7.  Utilizzare questa sintassi per configurare il dominio condiviso principale per la relazione di trust federativa creata nel passaggio 3. Il dominio specificato verrà utilizzato per configurare l'identificatore dell'organizzazione (OrgID) per la relazione di trust federativa. Per ulteriori informazioni sull'OrgID, vedere [Federated organization identifier](federation-exchange-2013-help.md).
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "<Federation Trust Name>" -AccountNamespace <Accepted Domain> -Enabled $true
    
    In questo esempio viene configurato il dominio accettato contoso.com come dominio condiviso principale per la relazione di trust federativa denominata Autenticazione di Azure AD.
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "Azure AD authentication" -AccountNamespace contoso.com -Enabled $true

8.  Per aggiungere altri domini alla relazione di trust federativa, utilizzare questa sintassi:
    
        Add-FederatedDomain -DomainName <AdditionalDomain>
    
    In questo esempio viene aggiunto il sottodominio sales.contoso.com alla relazione di trust federativa, poiché gli utenti con indirizzi e-mail nel dominio sales.contoso.com richiedono funzionalità di condivisione federata.
    
        Add-FederatedDomain -DomainName sales.contoso.com
    
    Tenere presente che qualsiasi dominio o sottodominio aggiunto alla relazione di trust federativa richiede una prova del record TXT della proprietà del dominio.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ExchangeCertificate](https://technet.microsoft.com/it-it/library/aa998327\(v=exchg.150\)), [New-FederationTrust](https://technet.microsoft.com/it-it/library/dd351047\(v=exchg.150\)), [Get-FederatedDomainProof](https://technet.microsoft.com/it-it/library/ff717833\(v=exchg.150\)), [Set-FederationTrust](https://technet.microsoft.com/it-it/library/dd298034\(v=exchg.150\)), [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/it-it/library/dd351037\(v=exchg.150\)) e [Add-FederatedDomain](https://technet.microsoft.com/it-it/library/dd351208\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Il corretto completamento delle procedure guidate **Abilitare trust federativot** e **Domini abilitati alla condivisione** saranno la prima indicazione che la relazione di trust federativa è stata configurata come ci si attendeva.

Per ulteriori verifiche della corretta creazione e configurazione della relazione di trust federativa, fare quanto segue:

1.  Eseguire questo comando Shell per verificare le informazioni di attendibilità del trust federativo.
    
        Get-FederationTrust | Format-List

2.  Sostituire *\<PrimarySharedDomain\>* con il dominio condiviso principale ed eseguire questo comando Shell per verificare che le informazioni sulla Federazione possano essere recuperate dalla propria organizzazione.
    
        Get-FederationInformation -DomainName <PrimarySharedDomain>

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-FederationTrust](https://technet.microsoft.com/it-it/library/dd351262\(v=exchg.150\)) e [Get-FederationInformation](https://technet.microsoft.com/it-it/library/dd351221\(v=exchg.150\)).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



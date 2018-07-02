---
title: 'Federazione: Exchange 2013 Help'
TOCTitle: Federazione
ms:assetid: 0046e2eb-6940-4941-bd5b-cbe6bffa3b94
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335047(v=EXCHG.150)
ms:contentKeyID: 50479890
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Federazione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Gli Information worker spesso devono collaborare con i destinatari esterni, quali fornitori, partner e clienti, e condividere le informazioni sulla disponibilità. La federazione in Microsoft Exchange Server 2013 contribuisce a tali sforzi di collaborazione. La *Federazione* fa riferimento all'infrastruttura di trust sottostante che supporta la *condivisione federata*, un metodo semplice per gli utenti per condividere le informazioni relative al calendario con i destinatari in altre organizzazioni esterne federate. Per ulteriori informazioni sulla condivisione federata, vedere [Condivisione](sharing-exchange-2013-help.md).


> [!IMPORTANT]
> Questa funzionalità di Exchange Server 2013 non è completamente compatibile con Office 365 utilizzato da 21Vianet in Cina e potrebbe essere soggetta a limitazioni. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/?linkid=313640">Informazioni su Office 365 utilizzato da 21Vianet</A>.



**Sommario**

Key terminology

Sistema di autenticazione Azure AD

Federation trust

Federated organization identifier

Federation example

Certificate requirements for Federation

Transitioning to a new certificate

Firewall Considerations for Federation

## Terminologia chiave

Nella tabella che segue sono descritti i componenti di base associati alla federazione in Exchange 2013.

  - **identificatore dell'applicazione (AppID)**  
    Un numero univoco generato dal sistema di autenticazione Azure Active Directory per identificare le organizzazioni Exchange. Il valore AppID viene generato automaticamente quando si crea una relazione di trust federativa con il sistema di autenticazione Azure Active Directory.

<!-- end list -->

  - **token di delega**  
    Token (SAML (Security Assertion Markup Language) generati dal sistema di autenticazione Azure Active Directory che consente agli utenti da un'organizzazione federata considerato attendibile da un'altra organizzazione federata. Un token di delega contiene l'indirizzo di posta elettronica dell'utente, un identificatore non modificabile e le informazioni associate all'offerta per il quale il token emesso per l'azione.

<!-- end list -->

  - **organizzazione federata esterna**  
    Un'organizzazione esterna Exchange che ha stabilito una relazione di trust federativa con il sistema di autenticazione Azure Active Directory.

<!-- end list -->

  - **condivisione federata**  
    Un gruppo Exchange funzionalità di che offre una relazione di trust federativa con il sistema di autenticazione per l'utilizzo nelle organizzazioni ExchangeAzure Active Directory, tra cui cross-premise Exchange distribuzioni. Insieme, queste funzionalità consentono di effettuare le richieste autenticate tra i server per conto degli utenti tra più organizzazioni Exchange.

<!-- end list -->

  - **dominio federato**  
    Un dominio autorevole aggiunto all'identificatore dell'organizzazione (OrgID) per un'organizzazione Exchange.

<!-- end list -->

  - **stringa di crittografia per la prova del dominio**  
    Una stringa crittograficamente sicura utilizzata da un'organizzazione Exchange per dimostrare che l'organizzazione possiede il dominio utilizzato con il sistema di autenticazione Azure Active Directory. La stringa è generata automaticamente quando si utilizza la procedura guidata **abilitare trust federativo** o possono essere generati utilizzando il cmdlet **Get-FederatedDomainProof** .

<!-- end list -->

  - **criterio di condivisione federata**  
    Un criterio a livello di organizzazione che abilita e controlla la condivisione, stabilita dall'utente e per singola persona, delle informazioni del calendario.

<!-- end list -->

  - **federazione**  
    Un accordo basato sulla fiducia tra due organizzazioni Exchange per raggiungere un obiettivo comune. Con la federazione, entrambe le organizzazioni desiderano che le asserzioni di autenticazione di una siano riconosciute anche dall'altra.

<!-- end list -->

  - **trust federativo**  
    Una relazione con il sistema di autenticazione Azure Active Directory che definisce i componenti seguenti per l'organizzazione Exchange:
    
      - Spazio dei nomi dell'account
    
      - Identificatore dell'applicazione (AppID)
    
      - Identificare dell'organizzazione (OrgID)
    
      - Domini federati
    
    Per configurare la condivisione federata con altre organizzazioni federate Exchange, è necessario stabilire una relazione di trust federativa con il sistema di autenticazione Azure Active Directory.

<!-- end list -->

  - **organizzazione non federata**  
    Organizzazioni che non dispongono di una relazione di trust federativa con il sistema di autenticazione Azure Active Directory.

<!-- end list -->

  - **identificatore dell'organizzazione (OrgID)**  
    Definisce i domini autorevoli accettati configurati in un'organizzazione abilitati per la federazione. Solo i destinatari che dispongono di indirizzi di posta elettronica con i domini federati configurati l'OrgID riconosciuti dal sistema di autenticazione Azure Active Directory e sono in grado di utilizzare le funzionalità di condivisione federata. L'OrgID è una combinazione di una stringa predefinita e il dominio accettato primo selezionato per la federazione nella procedura guidata **abilitare trust federativo**. Ad esempio, se si specifica il dominio federato contoso.com come dominio SMTP primario dell'organizzazione, lo spazio dei nomi account FYDIBOHF25SPDLT.contoso.com verranno essere create automaticamente come l'OrgID per la relazione di trust federativa.

<!-- end list -->

  - **relazione organizzativa**  
    Una relazione uno tra due organizzazioni federate Exchange che consente ai destinatari di condividere le informazioni sulla disponibilità (disponibilità di calendario). Una relazione dell'organizzazione richiede una relazione di trust federativa con il sistema di autenticazione Azure Active Directory e le sostituisce la necessità di utilizzare i trust tra foreste o domini Active Directory tra organizzazioni Exchange.

<!-- end list -->

  - **sistema di autenticazione Azure Active Directory**  
    Servizio identità basata su cloud e gratuito che funge da intermediario trust tra organizzazioni federate Exchange di Microsoft. È responsabile per l'emissione di token di delega ai destinatari Exchange quando viene richiesta di informazioni da destinatari di altre organizzazioni federate Exchange. Per ulteriori informazioni, vedere [Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500).

## Sistema di autenticazione Azure AD

Il sistema di autenticazione Azure Active Directory, un servizio basato su cloud gratuito offerti da Microsoft, funge da intermediario relazione di trust tra l'organizzazione di Exchange 2013 locale e altri federati Exchange 2010 e Exchange 2013 organizzazioni. Se si desidera configurare la federazione nell'organizzazione Exchange, è necessario stabilire una relazione di trust federativa occasionale con il sistema di autenticazione Azure Active Directory, in modo che possa diventare un partner della federazione con l'organizzazione. Con questa relazione di trust sul posto, gli utenti autenticati da Active Directory, noto come *provider di identità*, vengono inviati i token di delega (SAML (Security Assertion Markup Language) dal sistema di autenticazione Azure AD. Questi token di delega consentono agli utenti dall'organizzazione federata un Exchange considerato attendibile da un'altra organizzazione federata Exchange. Con il sistema di autenticazione Azure AD funge da intermediario relazione di trust, le organizzazioni non sono necessarie per stabilire relazioni di trust singoli più con altre organizzazioni e gli utenti possono accedere alle risorse esterne utilizzando un'esperienza single sign-on (SSO). Per ulteriori informazioni, vedere [Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500).

Inizio pagina

## Relazione di trust federativa

Per utilizzare le funzionalità di condivisione Exchange 2013 federati, è necessario stabilire una relazione di trust federativa tra l'organizzazione Exchange 2013 e il sistema di autenticazione Azure AD. Stabilire una relazione di trust federativa con il sistema di autenticazione Azure AD Scambia il certificato di protezione digitale dell'organizzazione con il sistema di autenticazione Azure AD e viene recuperato il Azure AD autenticazione certificati e federazione metadati di sistema. È possibile stabilire una relazione di trust federativa tramite la procedura guidata **abilitare trust federativo** nell'interfaccia di amministrazione di Exchange (EAC) o il cmdlet **New-FederationTrust** in Exchange Management Shell. Un certificato autofirmato viene creato automaticamente dalla procedura guidata **abilitare trust federativo** e viene utilizzato per la firma e la crittografia dei token di delega dal sistema di autenticazione Azure AD che consentono agli utenti di considerato attendibile dal esterno alle organizzazioni federate. Per informazioni dettagliate sui requisiti dei certificati, vedere Requisiti relativi ai certificati per la federazione più avanti in questo argomento.

Quando si crea una relazione di trust federativa con il sistema di autenticazione Azure AD, un *identificatore dell'applicazione* (AppID) generata automaticamente per l'organizzazione Exchange e fornito nell'output del cmdlet **Get-FederationTrust** . Il valore AppID viene utilizzato dal sistema di autenticazione Azure AD per identificare in modo univoco organizzazione Exchange. Viene inoltre utilizzato dall'organizzazione Exchange per dimostrare che l'organizzazione possiede il dominio da utilizzare con il sistema di autenticazione Azure AD. Questa operazione viene eseguita mediante la creazione di un record di testo (TXT) nell'area public Domain Name System (DNS) per ogni dominio federato.

Inizio pagina

## Identificatore di organizzazione federata

L' *identificatore di organizzazione federata* (OrgID) definisce i domini autorevoli accettati configurati nell'organizzazione abilitati per la federazione. Solo i destinatari che dispongono di indirizzi di posta elettronica con i domini accettati configurati l'OrgID riconosciuti dal sistema di autenticazione Azure AD e sono in grado di utilizzare le funzionalità di condivisione federata. Quando si crea una nuova relazione di trust federativa, viene creato automaticamente un OrgID con il sistema di autenticazione Azure AD. In questo OrgID è una combinazione di una stringa predefinita e il dominio accettato come dominio condiviso primario nella procedura guidata selezionato. Ad esempio, nella procedura guidata domini Edit Sharing-Enabled se si specifica il dominio federato **contoso.com** come dominio condiviso primario dell'organizzazione, lo spazio dei nomi account **FYDIBOHF25SPDLT.contoso.com** verrà essere creata automaticamente come OrgID per la relazione di trust federativa per l'organizzazione Exchange.

Anche se in genere il dominio SMTP principale per l'organizzazione Exchange, in questo dominio non deve essere un dominio accettato nell'organizzazione di Exchange e non richiede un domain name system (DNS prova di proprietà record TXT). L'unico requisito è che domini accettati, selezionare l'opzione per essere federato sono limitati a un massimo di 32 caratteri. L'unico scopo di questo sottodominio è come lo spazio dei nomi federato per il sistema di autenticazione Azure AD gestire gli identificatori univoci per i destinatari di token di delega SAML richiesta. Per ulteriori informazioni su token SAML, vedere [token SAML e basata sulle attestazioni](https://go.microsoft.com/fwlink/?linkid=198561)

È possibile aggiungere o rimuovere domini accettati dalla relazione di trust federativa in qualsiasi momento. Se si desidera abilitare o disabilitare tutte le funzionalità di condivisione federata nell'organizzazione, è sufficiente abilitare o disabilitare l'OrgID per la relazione di trust federativa.


> [!IMPORTANT]
> Se si modifica l'OrgID, i domini accettati o l'AppID utilizzato per la relazione di trust federativa, vengono coinvolte tutte le funzionalità di federazione nell'organizzazione. Questo influenza anche qualsiasi organizzazione di Exchange federata esterna, incluse le configurazioni di distribuzione ibrida e di Exchange Online. Si consiglia di notificare a tutti i partner federati esterni qualsiasi modifica a queste impostazioni di configurazione della relazione di trust federativa.



Inizio pagina

## Esempio di federazione

Due organizzazioni Exchange, Contoso, Ltd. e Fabrikam, Inc., desidera che gli utenti siano in grado di condividere le informazioni di disponibilità del calendario tra loro. Ciascuna organizzazione consente di creare una relazione di trust federativa con il sistema di autenticazione Azure AD e consente di configurare lo spazio dei nomi di account in modo da includere il dominio utilizzato per dominio indirizzo di posta elettronica dell'utente.

I dipendenti Contoso utilizzano uno dei seguenti domini di indirizzo di posta elettronica: contoso.com, contoso.co.uk o contoso.ca. I dipendenti Fabrikam utilizzano uno dei seguenti domini di indirizzo di posta elettronica: fabrikam.com, fabrikam.org o fabrikam.net. Entrambe le organizzazioni di verificare che tutti accettato dello spazio dei nomi di account per il trust federativo con il sistema di autenticazione Azure AD sono inclusi domini di posta elettronica. Invece di richiedere una configurazione di protezione foresta o dominio complessi Active Directory tra due organizzazioni, entrambe le organizzazioni di configurano una relazione dell'organizzazione tra loro per abilitare la condivisione di calendari libero/occupato.

La figura seguente illustra la configurazione di federazione tra Contoso, Ltd. e Fabrikam, Inc.

**Esempio di condivisione federata**

![Relazioni di trust federative e condivisione federata](images/Dd335047.310f0698-b67d-4b0e-91e4-231c6e9db952(EXCHG.150).gif "Relazioni di trust federative e condivisione federata")

## Requisiti di certificato per la federazione

Per stabilire una relazione di trust federativa con il sistema di autenticazione Azure AD un certificato autofirmato o un certificato x. 509 firmato da un'autorità di certificazione (CA) deve essere creata e installata nel server Exchange 2013 utilizzato per creare la relazione di trust. Si consiglia utilizzando un certificato autofirmato, viene automaticamente creato e installata utilizzando la procedura guidata **abilitare trust federativo** in EAC. Questo certificato viene utilizzato solo per eseguire l'accesso e crittografare i token di delega utilizzato per la condivisione federata ed è necessario un solo certificato per la relazione di trust federativa. Exchange 2013 distribuisce automaticamente il certificato a tutti gli altri server Exchange 2013 nell'organizzazione.

Se si desidera utilizzare un certificato X.509 firmato da un CA esterno, il certificato deve rispondere ai seguenti requisiti:

  - **Autorità di certificazione attendibile**   Se possibile, il certificato Secure Sockets Layer (SSL) X.509 deve essere rilasciato da un'autorità di certificazione considerata attendibile da Windows Live. È tuttavia possibile utilizzare certificati rilasciati da autorità di certificazione che non sono attualmente certificate da Microsoft. Per un elenco aggiornato delle autorità di certificazione attendibili, vedere [Autorità di certificazione radice disponibile nell'elenco locale per le relazioni di trust federative](trusted-root-certification-authorities-for-federation-trusts-exchange-2013-help.md).

  - **Identificatore chiave del soggetto**   Il certificato deve disporre del campo Identificatore chiave del soggetto. La maggior parte dei certificati X.509 rilasciati da autorità di certificazione commerciali ha questo identificativo.

  - **Provider di CryptoAPI del servizio di crittografia (CSP)**   Il certificato deve utilizzare un CSP CryptoAPI. I certificati che utilizzano l'API di crittografia: provider di prossima generazione (CNG) non sono supportati per la federazione. Se si utilizza Exchange per creare una richiesta di certificato, viene utilizzato un provider di CryptoAPI. Per ulteriori informazioni, vedere [API di crittografia: futuro](https://go.microsoft.com/fwlink/?linkid=187890).

  - **Algoritmo di firma RSA**   Il certificato deve utilizzare RSA come algoritmo di firma.

  - **Chiave privata esportabile**   La chiave privata utilizzata per generare il certificato deve essere esportabile. È possibile specificare l'esportabilità della chiave privata quando si crea la richiesta di certificato utilizzando la procedura guidata **Nuovo certificato di Exchange** nell'interfaccia di amministrazione di Exchange in EMC o il cmdlet [New-ExchangeCertificate](https://technet.microsoft.com/it-it/library/aa998327\(v=exchg.150\)) in Shell.

  - **Certificato corrente**   Il certificato deve essere corrente. Per creare una relazione di trust federativa, non è possibile utilizzare un certificato scaduto o revocato.

  - **Utilizzo chiavi avanzato**   Il certificato deve comprendere il tipo Utilizzo chiavi avanzato (EKU) **Autenticazione client (1.3.6.1.5.5.7.3.2)**. Questo tipo di utilizzo viene usato per provare la propria identità come computer remoto. Se si utilizza Interfaccia di amministrazione di Exchange o Shell per generare la richiesta di certificato, questo tipo di utilizzo è incluso per impostazione predefinita.


> [!NOTE]
> Siccome non viene utilizzato per l'autenticazione, il certificato non dispone di alcun nome del soggetto né di alcun requisito per il nome alternativo del soggetto. È possibile utilizzare un certificato con un nome del soggetto equivalente al nome host, al nome di dominio o a qualsiasi altro nome.



Inizio pagina

## Transizione a un nuovo certificato

Il certificato utilizzato per creare la relazione di trust federativa viene designato come certificato corrente. Tuttavia, potrebbe essere necessario installare ed utilizzare un nuovo certificato per relazione di trust federativa periodicamente. Ad esempio, potrebbe essere necessario utilizzare un nuovo certificato se il certificato corrente scade o per rispondere ad un nuovo requisito dell'azienda o di protezione. Per garantire un passaggio diretto a un nuovo certificato, è necessario installare il nuovo certificato sul server Exchange 2013 e configurare la relazione di trust federativa per designarlo come nuovo certificato. Exchange 2013 distribuisce automaticamente il nuovo certificato ad altri server Exchange 2013 dell'organizzazione. In base alla topologia di Active Directory, la distribuzione del certificato potrebbe richiedere alcuni minuti. È possibile verificare lo stato del certificato utilizzando il cmdlet [Test-FederationTrustCertificate](https://technet.microsoft.com/it-it/library/dd335228\(v=exchg.150\)) in Shell.

Dopo aver verificato lo stato di distribuzione del certificato, è possibile configurare la relazione di trust per l'utilizzo del nuovo certificato. Dopo il passaggio dei certificati, il certificato corrente viene designato come certificato precedente e il nuovo certificato viene designato come certificato corrente. Il nuovo certificato verrà pubblicato nel sistema di autenticazione Azure AD e tutti i nuovi token scambiate con il sistema di autenticazione Azure AD vengono crittografati utilizzando il nuovo certificato.


> [!NOTE]
> Questo processo di transizione del certificato viene utilizzato solo dalla federazione. Se si utilizza lo stesso certificato per altre funzionalità di Exchange 2013 per cui sono necessari i certificati, è necessario considerare i requisiti delle funzionalità quando si intende ottenere, installare o passare a un nuovo certificato.



Inizio pagina

## Considerazioni sul firewall per la federazione

Le funzionalità di federazione richiedono l'accesso in uscita a Internet tramite HTTPS per i server Cassette postali e Accesso client dell'organizzazione. È necessario consentire l'accesso HTTPS in uscita (porta 443 per TCP) da tutti i server Accesso client di Exchange 2013 dell'organizzazione.

Affinché un'organizzazione esterna possa avere accesso alle informazioni sulla disponibilità dell'organizzazione, è necessario pubblicare un server Accesso client su Internet. Ciò richiede l'accesso HTTPS in ingresso da Internet al server Accesso client. I server Accesso client dei siti di Active Directory che non dispongono di un server Accesso client pubblicato su Internet possono utilizzare i server Accesso client di altri siti di Active Directory accessibili da Internet. I server Accesso client non pubblicati su Internet devono disporre dell'URL esterno della directory virtuale dei servizi Web impostata con l'URL visibile alle organizzazioni esterne.

[Inizio pagina](sharing-exchange-2013-help.md)


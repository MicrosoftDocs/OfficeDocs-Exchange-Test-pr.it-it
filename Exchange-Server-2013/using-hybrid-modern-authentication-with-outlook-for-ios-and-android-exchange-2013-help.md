---
title: 'ITPro_R4_Stub_80: Exchange 2013 Help'
TOCTitle: ITPro_R4_Stub_80
ms:assetid: 0e701643-1f18-4cc3-8595-4fd4b15caf6c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt846639(v=EXCHG.150)
ms:contentKeyID: 74520293
ms.date: 04/25/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ITPro\_R4\_Stub\_80

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2018-04-19_

**Sintesi:**  informazioni su come le amministrazioni possono distribuire le funzioni di autenticazione moderna ibrida ed Enterprise Mobility + Security per le cassette postali locali di Exchange per abilitare il supporto di Outlook per iOS e Android.

L'app Outlook per iOS e Android è progettata per ottimizzare l'esperienza di Office 365 su dispositivi mobili sfruttando i servizi Microsoft per consentire agli utenti di individuare, pianificare e definire le priorità in ambito professionale e personale. Outlook fornisce la protezione, la privacy e il supporto necessari garantendo la sicurezza dei dati aziendali tramite funzionalità quali l'accesso condizionale di Azure Active Directory e i criteri di protezione dell'app Intune. Nelle sezioni seguenti viene fornita una panoramica dell'architettura di autenticazione moderna ibrida, dei prerequisiti necessari per la sua implementazione e di come distribuire in modo sicuro Outlook per iOS e Android per le cassette postali di Exchange.

## Architettura Microsoft Cloud per i clienti dell'edizione ibrida di Exchange Server

Outlook per iOS e Android è un'applicazione supportata dal cloud. Questo significa che l'esperienza dell'utente consiste in un'app installata in locale dotata di un servizio sicuro e scalabile in esecuzione in Microsoft Cloud.

Per le cassette postali di Exchange Server, la nuova architettura di Outlook per iOS e Android è caratterizzata da una progettazione simile a quella dell'architettura precedente. Tuttavia, poiché il servizio è ora integrato direttamente in Microsoft Cloud (con Office 365 e Microsoft Azure), i clienti ricevono i vantaggi aggiuntivi in merito a sicurezza, privacy, conformità integrata e operazioni trasparenti forniti da Microsoft nel [Centro protezione di Office 365](https://products.office.com/business/office-365-trust-center-welcome) e nel [Centro protezione di Azure](https://www.microsoft.com/trustcenter/cloudservices/azure).

![Diagramma dell'architettura dell'autenticazione moderna ibrida in Outlook per iOS e Android](images/Mt846639.20a7e963-916d-47e0-bffb-4d86c4777bea(EXCHG.150).png "Diagramma dell'architettura dell'autenticazione moderna ibrida in Outlook per iOS e Android")

I dati vengono passati da Exchange Online all'app Outlook tramite una connessione protetta con TLS. Il programma di traduzione del protocollo in esecuzione su Azure consente di instradare i dati, i comandi e le notifiche, ma non è in grado di leggere i dati.

La connessione Exchange ActiveSync tra Exchange Online e l'ambiente locale consente la sincronizzazione dei dati locali degli utenti e include i messaggi di posta elettronica, tutti i dati del calendario, tutti i dati dei contatti e lo stato fuori sede di quattro settimane nel tenant di Exchange Online. Questi dati verranno rimossi automaticamente da Exchange Online dopo 30 giorni dopo l'eliminazione dell'account in Azure Active Directory.

La sincronizzazione dei dati tra l'ambiente locale ed Exchange Online si verifica indipendentemente dal comportamento degli utenti. In questo modo, è possibile inviare nuovi messaggi ai dispositivi molto rapidamente.

L'elaborazione delle informazioni in Microsoft Cloud abilita funzioni e funzionalità avanzate, come la categorizzazione della posta elettronica per Posta in arrivo evidenziata, un'esperienza personalizzata per viaggi e calendario e una velocità di ricerca migliorata. L'adozione del cloud per l'elaborazione intensiva e la riduzione al minimo delle risorse necessarie per i dispositivi degli utenti consente di ottimizzare la stabilità e le prestazioni dell'app. Inoltre, consente a Outlook di creare funzionalità disponibili in tutti gli account di posta elettronica, indipendentemente dalle funzionalità tecnologiche dei server sottostanti (ad esempio diverse versioni di Office 365 o Exchange Server).

In particolare, questa nuova architettura è caratterizzata dai miglioramenti seguenti:

1.  **Supporto di Enterprise Mobility + Security:**  I clienti possono trarre vantaggio da Microsoft Enterprise Mobility + Security (EMS), compresi Microsoft Intune e Azure Active Directory Premium, per abilitare l'accesso condizionale e i criteri di protezioni dell'app Intune, che consentono di controllare e proteggere i dati di messaggistica aziendali sul dispositivo mobile.

2.  **Con tecnologia Microsoft Cloud:**  I dati delle cassette postali locali sono sincronizzati in Exchange Online, che fornisce i vantaggi di sicurezza, privacy, conformità e operazioni trasparenti garantite da Microsoft nel [Centro protezione di Office 365](https://products.office.com/business/office-365-trust-center-welcome).

3.  **OAuth consente di proteggere le password degli utenti:**  Outlook si avvale dell'autenticazione moderna ibrida (OAuth) per la protezione delle credenziali degli utenti. L'autenticazione moderna ibrida fornisce a Outlook un meccanismo sicuro per accedere ai dati di Exchange senza mai toccare o archiviare le credenziali dell'utente. All'accesso, l'utente effettua l'autenticazione direttamente in una piattaforma di identità (Azure Active Directory o un provider di identità locale come ADFS) e riceve un token di accesso, che garantisce l'accesso di Outlook ai file o alle cassette postali dell'utente. Il servizio non ha mai accesso alla password dell'utente.

4.  **Fornisce ID dispositivo univoci:**  Ogni connessione di Outlook è registrata in modo univoco in Microsoft Intune e, pertanto, può essere gestita come una connessione univoca.

5.  **Sblocca nuove funzioni su iOS e Android:**  Questo aggiornamento consente all'app Outlook di sfruttare le funzionalità di Office 365 native che al momento non sono supportate nell'ambiente locale di Exchange, come l'utilizzo della ricerca completa di Exchange Online e la Posta in arrivo evidenziata. Queste funzionalità saranno disponibili solo quando si utilizza Outlook per iOS e Android.


> [!NOTE]
> La gestione dei dispositivi tramite l'interfaccia di amministrazione di Exchange locale non è possibile. È necessario disporre di Intune per gestire i dispositivi mobili.



## Sicurezza dei dati, accesso e controlli

Con la sincronizzazione dei dati locali con Exchange Online, i clienti hanno delle domande sulla sicurezza dei dati in Exchange Online. Il white paper [Crittografia in Microsoft Cloud](http://aka.ms/office365ce) descrive come viene utilizzato BitLocker per la crittografia a livello di volume. La crittografia del servizio con l'opzione Customer Key, come descritto nel white paper, è supportata nell'architettura di Outlook per iOS e Android, ma l'utente deve disporre di una licenza Office 365 Enterprise E5 (oppure delle versioni corrispondenti di tali piani per Government o Education) per avere un criterio di crittografia assegnato.

Per impostazione predefinita, i tecnici Microsoft non hanno privilegi amministrativi e non hanno accesso ai contenuti dei clienti in Office 365. Il white paper [Controlli dell'accesso degli amministratori di Office 365](http://aka.ms/office365aac) descrive lo screening del personale, i controlli del background, Lockbox e Customer Lockbox e altro.

[La documentazione relativa ai controlli ISO in Garanzia del servizio](https://sip.protection.office.com/) fornisce lo stato dei controlli sottoposti a controllo rispetto alle normative e agli standard di sicurezza delle informazioni globali implementati da Office 365.

## Flusso di connessione

Quando Outlook per iOS e Android è abilitato con l'autenticazione moderna ibrida, il flusso di connessione è il seguente.

![Flusso di autenticazione nell'autenticazione moderna ibrida](images/Mt846639.d6e20ddb-cf8e-4154-8a17-95657ef696d1(EXCHG.150).png "Flusso di autenticazione nell'autenticazione moderna ibrida")

1.  Dopo che l'utente inserisce il proprio indirizzo di posta elettronica, Outlook per iOS e Android si connette al servizio di rilevamento automatico. Il servizio di rilevamento automatico determina il tipo di cassetta postale avviando una query di individuazione automatica per Exchange Online. Exchange Online determina che la cassetta postale dell'utente è locale e restituisce un reindirizzamento 302 al servizio di rilevamento automatico con l'URL di individuazione automatica locale. Il servizio di rilevamento automatico inizia una query nel servizio di individuazione automatica locale per determinare l'endpoint di ActiveSync per l'indirizzo di posta elettronica. L'URL tentato in locale è simile al seguente: https://autodiscover.contoso.com/autodiscover/autodiscover.json?Email=test%40contoso.com\&Protocol=activesync\&RedirectCount=3.

2.  Il servizio di rilevamento automatico avvia una connessione all'URL di ActiveSync locale ottenuto al passaggio 1 con un token di connessione vuoto. Il token di connessione vuoto indica ad ActiveSync locale che il client supporta l'autenticazione moderna. ActiveSync locale invia una risposta 401 e include l'intestazione *WWW-Authenticate: Bearer*. All'interno dell'intestazione WWW-Authenticate: Bearer è presente il valore authorization\_uri che identifica l'endpoint di Azure Active Directory (AAD) da utilizzare per ottenere un token OAuth.

3.  Il servizio di rilevamento automatico restituisce l'endpoint AAD al client. Il client inizia il flusso di accesso e l'utente visualizza un modulo Web (o viene reindirizzato all'app Microsoft Authenticator) dove può immettere le credenziali. A seconda della configurazione dell'identità, potrebbe causare o non causare un reindirizzamento dell'endpoint federato a un provider di identità locale. Infine, il client ottiene una coppia di token di accesso e aggiornamento, denominata AT1/RT1. Il token di accesso ha l'ambito del client di Outlook per iOS e Android con un gruppo di destinatari dell'endpoint di Exchange Online.

4.  Outlook per iOS e Android stabilisce una connessione al programma di traduzione del protocollo senza stato in cui il protocollo del dispositivo proprietario del client viene convertito in un protocollo che riconosce Exchange Online.

5.  Una richiesta di provisioning viene passata a Exchange Online che include il token di accesso dell'utente (AT1) e l'endpoint di ActiveSync locale.

6.  L'API di provisioning MRS in Exchange Online utilizza AT1 come input e ottiene una seconda coppia di token di accesso e aggiornamento (denominata AT2/RT2) per accedere alla cassetta postale locale tramite una chiamata per conto di ad Azure Active Directory. Questo secondo token di accesso ha l'ambito con il client in Exchange Online e un gruppo di destinatari dell'endopoint dello spazio dei nomi di ActiveSync.

7.  Se non viene effettuato il provisioning della cassetta postale, l'API di provisioning crea una cassetta postale.

8.  L'API di provisioning MRS stabilisce una connessione sicura per l'endpoint di ActiveSync locale e sincronizza i dati di messaggistica dell'utente utilizzando il token di accesso AT2 come meccanismo di autenticazione. RT2 viene utilizzato periodicamente per generare un nuovo AT2 in modo che i dati possano essere sincronizzati in background senza l'intervento dell'utente.

## Requisiti tecnici e relativi alle licenze

L'architettura di autenticazione moderna ibrida è caratterizzata dai seguenti requisiti tecnici:

1.  **Configurazione locale di Exchange**:
    
      - Una distribuzione di aggiornamento cumulativo (CU) minimo in tutti i server Exchange di Exchange Server 2016 CU8 o Exchange Server 2013 CU19. Tenere presente che i clienti con distribuzioni ibride in cui Exchange è distribuito in locale e nel cloud o che utilizzano Archiviazione Exchange Online (EOA) con Exchange in locale, devono distribuire l'aggiornamento cumulativo più recente o quello precedente all'ultimo.
    
      - Tutti i server di Exchange 2007 o Exchange 2010 devono essere rimossi dall'ambiente. Exchange Server 2010 SP3 non rientra nel supporto Mainstream e non è compatibile con Outlook per iOS e Android gestito da Intune. In questa architettura, Outlook per iOS e Android utilizza OAuth come meccanismo di autenticazione. Una delle modifiche di configurazione locali che si verifica abilita l'endpoint OAuth con Microsoft Cloud come endpoint di autorizzazione predefinito. Quando viene apportata questa modifica, i client possono iniziare a negoziare l'uso di OAuth. Trattandosi di una modifica a livello di organizzazione, le cassette postali di Exchange 2010 guidate da Exchange 2013 o 2016 penseranno erroneamente di essere in grado di eseguire OAuth ma verranno disconnesse, perché Exchange 2010 non supporta OAuth come meccanismo di autenticazione.

2.  **Sincronizzazione di Active Directory**. Sincronizzazione di Active Directory dell'intera directory locale con Azure Active Directory, tramite Azure AD Connect. È necessario verificare che gli attributi seguenti siano sincronizzati:
    
      - Office 365 ProPlus
    
      - Exchange Online
    
      - Write-back di Exchange ibrido
    
      - Azure RMS
    
      - Intune

3.  **Configurazione ibrida di Exchange:**  Richiede una relazione ibrida completa tra Exchange locale ed Exchange Online.
    
      - Il tenant di Office 365 ibrido è configurato in modalità di configurazione ibrida completa e come specificato nell'[Assistente per la distribuzione di Exchange](http://technet.microsoft.com/exdeploy)
    
      - Richiede un tenant Enterprise, Business o Education di Office 365.
    
      - I dati delle cassette postali locali sono sincronizzati nella stessa area geografica del datacenter in cui è configurato il tenant di Office 365. Per ulteriori informazioni sulla posizione dei dati di Office 365, visitare la sezione [Dove si trovano i miei dati?](http://o365datacentermap.azurewebsites.net/) nel Centro di protezione di Office 365.
    
      - L'utilizzo dei tenant di Office 365 US Government Community e Defense, dei tenant di Office 365 Germany e di Office 365 China gestiti da 21Vianet non è supportato.
    
      - I nomi host degli URL esterni per Exchange ActiveSync e Individuazione automatica devono essere pubblicati come entità servizio per Azure Active Directory con la procedura guidata di configurazione ibrida.
    
      - Gli spazi dei nomi di Individuazione automatica ed Exchange ActiveSync devono essere accessibili da Internet e non possono essere applicazioni per una soluzione di pre-autenticazione.
    
      - Verificare che l'offload di SSL o TLS non sia in uso tra il bilanciamento del carico e i server di Exchange poiché potrebbe influire sull'utilizzo del token OAuth. È supportato il bridgind SSL e TLS (terminazione e riesecuzione della crittografia).

4.  **Configurazione di Intune:**  è supportata sia la distribuzione ibrida sia quella solo cloud di Intune (MDM per Office 365 non è supportato).

5.  **Licenze di Office 365\*:**  ogni utente deve avere una delle licenze di Office 365 seguenti:
    
      - Commercial: licenze Enterprise E3, Enterprise E5, ProPlus o Business
    
      - Government: U.S. Government Community G3, U.S. Government Community G5
    
      - Education: Office 365 Education E3, Office 365 Education E5
    
    Inoltre, le licenze devono includere le applicazioni client di Office necessarie per l'uso commerciale di Outlook per iOS e Android.

6.  **Licenze di EMS\*:**  ogni utente locale deve avere una delle licenze seguenti:
    
      - Intune autonomo + Azure Active Directory Premium autonomo
    
      - Enterprise Mobility + Security E3, Enterprise Mobility + Security E5

**\***Microsoft Secure Productive Enterprise (SPE) include tutte le licenze necessarie per Office 365 ed EMS.

## Passaggi per l'implementazione

L'attivazione del supporto per l'autenticazione moderna ibrida nell'organizzazione richiede ognuno dei seguenti passaggi, descritti in modo dettagliato nelle sezioni seguenti:

1.  Creare i criteri di accesso condizionale

2.  Creare i criteri di protezione delle app di Intune

3.  Abilitare l'autenticazione moderna ibrida

4.  Contattare Microsoft

## Creare i criteri di accesso condizionale

Quando un'organizzazione decide di standardizzare la modalità di accesso degli utenti ai dati di Exchange, utilizzando Outlook per iOS e Android come unica app di posta elettronica per gli utenti finali, è possibile configurare dei criteri di accesso condizionale in grado di bloccare altri metodi di accesso mobile. Outlook per iOS e Android esegue l'autenticazione tramite l'identità dell'oggetto di Azure Active Directory e quindi stabilisce una connessione con Exchange Online. Di conseguenza, sarà necessario creare dei criteri di accesso condizionale di Azure Active Directory per limitare la connettività dei dispositivi mobili a Exchange Online. A questo scopo, sono necessari due criteri di accesso condizionale, ognuno dei quali assegnato a tutti gli utenti potenziali. Informazioni sulla creazione di tali criteri sono disponibili nell'articolo relativo ai [criteri di accesso condizionale basato su app per Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-mam#exchange-online-policy).

1.  Il primo criterio consente l'accesso a Outlook per iOS e Android e blocca la connessione a Exchange Online dei client di Exchange ActiveSync che supportano OAuth. Vedere "Passaggio 1: Configurare un criterio di accesso condizionale di Azure AD per Exchange Online".

2.  Il secondo criterio impedisce ai client di Exchange ActiveSync che sfruttano l'autenticazione di base di connettersi a Exchange Online. Vedere"Passaggio 2: Configurare un criterio di accesso condizionale di Azure AD per Exchange Online con Active Sync (EAS)."

I criteri sfruttano il controllo di concessione [Richiedi app client approvata](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference), che concede l'accesso solo alle app Microsoft con Intune SDK integrato.


> [!IMPORTANT]
> Per sfruttare i criteri di accesso condizionale basati sulle app, è necessario installare l'app Microsoft Authenticator sui dispositivi iOS. Per i dispositivi Android, viene usata l'app Portale aziendale Intune. Per ulteriori informazioni, vedere <A href="https://docs.microsoft.com/intune/app-based-conditional-access-intune">Accesso condizionale basato su app con Intune</A>.



Per impedire che altri client di dispositivi mobili (come il client di posta elettronica nativo incluso nel sistema operativo mobile) si connettano al proprio ambiente locale (che esegue l'autenticazione di base per Active Directory locale), si hanno due opzioni:

1.  È possibile utilizzare le regole di accesso ai dispositivi mobili per Exchange integrate e impedire a tutti i dispositivi mobili di connettersi tramite l'impostazione seguente in Exchange Management Shell:
    
    ```powershell
            Set-ActiveSyncOrganizationSettings -DefaultAccessLevel Block
    ```

2.  Dopo aver installato il connettore di Exchange locale, è possibile utilizzare un criterio di accesso condizionale locale con Intune. Per ulteriori informazioni, vedere [Creare criteri di accesso condizionale per Exchange locale ed Exchange Online dedicato legacy](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).


> [!NOTE]
> Quando si implementa una delle opzioni locali citate in precedenza, tenere presente che potrebbero interessare anche la connessione degli utenti a Exchange tramite i dispositivi mobili.



## Creare i criteri di protezione delle app di Intune

Dopo aver abilitato l'autenticazione moderna ibrida, tutti gli utenti mobili in locale sono in grado di utilizzare Outlook per iOS e Android con l'architettura basata su Office 365. Di conseguenza, è importante proteggere i dati aziendali con i criteri di protezione delle app di Intune.

Creare i criteri di protezione delle app di Intune per iOS e Android seguendo la procedura descritta in [Come creare e assegnare criteri di protezione delle app](https://docs.microsoft.com/intune/app-protection-policies). Ogni criterio deve avere le caratteristiche seguenti:

1.  Deve includere tutte le applicazioni mobili Microsoft, come Word, Excel o PowerPoint, poiché questo garantisce che gli utenti possano accedere e utilizzare i dati aziendali all'interno di qualsiasi app Microsoft in modo sicuro.

2.  Deve simulare le funzionalità di protezione fornite da Exchange per i dispositivi mobili, tra cui:
    
      - Richiesta di un PIN di accesso (con Selezione tipo, Lunghezza PIN, Consenti PIN semplice, Consenti tramite impronta digitale)
    
      - Crittografia dei dati dell'app
    
      - Blocco dell'esecuzione delle app gestite nei dispositivi jailbroken e rooted

3.  Devono essere assegnati a tutti gli utenti. In questo modo tutti gli utenti sono protetti, indipendentemente dal fatto che usino Outlook per iOS e Android.

Oltre ai requisiti minimi dei criteri indicati in precedenza, occorre prendere in considerazione la distribuzione di impostazioni dei criteri di protezione avanzata come **Limita le operazioni taglia, copia e incolla con le altre app** per evitare ulteriori perdite di dati aziendali. Per ulteriori informazioni sulle impostazioni disponibili, vedere [Impostazioni dei criteri di protezione delle app di Android in Microsoft Intune](https://docs.microsoft.com/intune/app-protection-policy-settings-android) e [Impostazioni dei criteri di protezione delle app per iOS](https://docs.microsoft.com/intune/app-protection-policy-settings-ios).


> [!IMPORTANT]
> Per applicare i criteri di protezione delle app di Intune sulle app nei dispositivi Android non registrati in Intune, l'utente deve installare anche il Portale aziendale Intune. Per ulteriori informazioni, vedere <A href="https://docs.microsoft.com/it-it/intune/app-protection-enabled-apps-android">Aspettative dalla gestione dell'app per Android con criteri di protezione delle app</A>.



## Abilitare l'autenticazione moderna ibrida

Se non è stata abilitata l'autenticazione moderna ibrida, consultare e seguire la procedura descritta in [Panoramica di autenticazione moderna ibrida e prerequisiti per l'utilizzo con Exchange Server e Skype for Business in locale](https://support.office.com/article/hybrid-modern-authentication-overview-and-prerequisites-for-using-it-with-on-premises-skype-for-business-and-exchange-servers-ef753b32-7251-4c9e-b442-1a5aec14e58d?).

Se è già stata abilitata l'autenticazione moderna ibrida per supportare altre versioni di Outlook, tra cui Outlook per Mac, per gli utenti locali come descritto in [Come configurare Exchange Server locale per utilizzare l'autenticazione moderna ibrida](https://support.office.com/article/how-to-configure-exchange-server-on-premises-to-use-hybrid-modern-authentication-cef3044d-d4cb-4586-8e82-ee97bd3b14ad?), there are only a few additional steps you must take:

1.  Creare una regola di accesso a un dispositivo Exchange per consentire a Exchange Online di connettersi all'ambiente locale utilizzando il protocollo ActiveSync:
    ```powershell
        If ((Get-ActiveSyncOrganizationSettings).DefaultAccessLevel -ne "Allow") {New-ActiveSyncDeviceAccessRule -Characteristic DeviceType -QueryString "OutlookService" -AccessLevel Allow}
    ```
    La gestione dei dispositivi tramite l'interfaccia di amministrazione di Exchange locale non è possibile. È necessario disporre di Intune per gestire i dispositivi mobili.

2.  Creare una regola di accesso per i dispositivi Exchange che impedisca agli utenti di connettersi all'ambiente locale con Outlook per iOS e Android tramite l'autenticazione di base con il protocollo Exchange ActiveSync:
    ```powershell
        New-ActiveSyncDeviceAccessRule -Characteristic DeviceModel -QueryString "Outlook for iOS and Android" -AccessLevel Block
    ```

    > [!NOTE]
    > Dopo aver creato la regola, gli utenti che usano Outlook per iOS e Android con l'autenticazione di base vengono bloccati.



3.  Verificare che maxRequestLength EAS sia configurato in modo da corrispondere a MaxSendSize/MaxReceiveSize della configurazione del trasporto:
    
      - Percorso: `%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config`
    
      - Proprietà: `maxRequestLength`
    
      - Valore: impostato in dimensioni KB (ad esempio, 10 MB è 10240)

## Contattare Microsoft

Per abilitare il supporto dell'autenticazione moderna ibrida per Outlook per iOS e Android, è necessario rivolgersi al team dell'account Microsoft, al contatto CSS (Customer Sales and Services) o al Technical Account Manager. Sarà necessario fornire tutti i domini SMTP (e i domini UPN nel caso in cui i domini UPN non corrispondano all'indirizzo SMTP). Dopo aver fornito e abilitato i domini, l'autenticazione moderna ibrida sarà supportata per le cassette postali locali che usano Outlook per iOS e Android.

## Funzionalità client non supportate

Le funzionalità seguenti non sono supportate per le cassette postali locali che usano l'autenticazione moderna ibrida con Outlook per iOS e Android.

  - Sincronizzazione tra le bozze e la cartella Bozza

  - Accesso al calendario condiviso e accesso al calendario delegato

  - Promemoria Cortana Time to Leave

  - Allegati del calendario

  - Gestione delle attività con Microsoft To-Do

## Domande frequenti sul flusso di connessione

**D:**  L'organizzazione ha un criterio di sicurezza che richiede che le connessioni Internet in ingresso siano limitate a FQDN e indirizzi IP approvati. È possibile con questa architettura?

**R:**  È consigliabile che gli endpoint locali per i protocolli di Individuazione automatica e ActiveSync siano aperti e accessibili da Internet senza alcuna limitazione. In alcuni casi potrebbe non essere possibile. Ad esempio, in presenza di un periodo di coesistenza con un'altra soluzione MDM, potrebbe essere necessario applicare delle limitazioni al protocollo ActiveSync per impedire agli utenti di ignorare la soluzione MDM di terze parti durante la migrazione a Intune e Outlook per iOS e Android. Se è necessario applicare limitazioni ai dispositivi gateway o firewall locali, è consigliabile filtrare per endpoint FQDN. Se non è possibile usare gli endpoint FQDN, filtrare per indirizzi IP. Verificare che gli FQDN e le subnet IP seguenti siano nell'elenco elementi consentiti:

  - Tutti gli intervalli di subnet IP e gli URL di Exchange Online sono descritti in [URL e intervalli di indirizzi IP di Office 365](https://support.office.com/article/office-365-urls-and-ip-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

  - Tutti gli FQDN dell'app Outlook per iOS e Android sono descritti in [Richieste di rete in Office 365 ProPlus e Mobile](https://support.office.com/article/network-requests-in-office-365-proplus-and-mobile-eb73fcd1-ca88-4d02-a74b-2dd3a9f3364d?).

  - Tutte le subnet IP dell'area geografica dei datacenter negli Stati Uniti e in Europa sono definite in [Intervalli IP dei datacenter Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653). Questa operazione è necessaria perché il servizio di rilevamento automatico consente di definire le connessioni all'infrastruttura locale, come illustrato nel Flusso di connessione. Attualmente, il servizio di rilevamento automatico non consente di utilizzare le limitazioni IP in Azure.

**D:**  Attualmente, l'organizzazione usa una soluzione MDM di terze parti per gestire la connettività dei dispositivi mobili. Se viene visualizzato lo spazio dei nomi di Exchange ActiveSync su Internet, viene consentito agli utenti di ignorare la soluzione MDM di terze parti durante il periodo di coesistenza. Come è possibile evitarlo?

**R:**  Esistono tre possibili soluzioni per risolvere il problema:

1.  Implementare le regole di accesso ai dispositivi mobili per Exchange per controllare quali dispositivi sono autorizzati alla connessione.

2.  Alcune soluzioni MDM di terze parti dispongono di regole di accesso ai dispositivi mobili per Exchange che impediscono l'accesso non autorizzato e aggiungono i dispositivi autorizzati nella proprietà ActiveSyncAllowedDeviceIDs dell'utente.

3.  Implementare limitazioni IP nello spazio dei nomi di Exchange ActiveSync.

**D:**  È possibile utilizzare Azure ExpressRoute per gestire il traffico tra Microsoft Cloud e l'ambiente locale?

**R:**  La connettività a Microsoft Cloud richiede una connessione Internet. Tuttavia, un sottoinsieme del traffico di rete di Office 365 potrebbe essere inoltrato tramite Azure ExpressRoute. Per ulteriori informazioni, vedere [Azure ExpressRoute per Office 365](https://support.office.com/article/azure-expressroute-for-office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).

Con ExpressRoute, non vi è alcuno spazio IP privato per le connessioni ExpressRoute e non può esserci una risoluzione DNS "privata". Questo significa che qualsiasi endpoint che l'organizzazione vuole usare su ExpressRoute deve essere risolto nel DNS pubblico. Se tale endpoint viene risolto in un IP contenuto nei prefissi annunciati associati al circuito ExpressRoute (l'organizzazione deve configurare tali prefissi nel portale di Azure quando si abilita il peering Microsoft sulla connessione ExpressRoute), la connessione in uscita da Exchange Online all'ambiente locale viene inoltrata tramite il circuito ExpressRoute. L'organizzazione deve verificare che il traffico di ritorno associato a tali connessioni passi attraverso il circuito ExpressRoute (evitando il routing asimmetrico).


> [!NOTE]
> Poiché l'organizzazione aggiungerà lo spazio dei nomi di Exchange ActiveSync ai prefissi annunciati nel circuito ExpressRoute, l'unico modo per raggiungere l'endpoint di Exchange ActiveSync sarà tramite ExpressRoute. In altre parole, l'unico dispositivo mobile al quale sarà possibile connettersi in locale tramite lo spazio dei nomi di ActiveSync sarà Outlook per iOS e Android. Tutti gli altri client di ActiveSync (come i client di posta elettronica nativi del dispositivo mobile) non saranno in grado di connettersi all'ambiente locale perché non verrà stabilita la connessione da Microsoft Cloud. Ciò è dovuto al fatto che non possono esserci sovrapposizioni dello spazio pubblico IP annunciato a Microsoft nel circuito ExpressRoute e dello spazio pubblico IP annunciato nei circuiti Internet.



**D:**  Dato che vengono sincronizzati i dati dei messaggi relativi solo a quattro settimane con Exchange Online, questo significa che le query di ricerca eseguite in Outlook per iOS e Android non possono restituire informazioni oltre i dati disponibili sul dispositivo locale?

**R:**  Quando viene eseguita una query di ricerca in Outlook per iOS e Android, gli elementi che corrispondono alla query di ricerca vengono restituiti se si trovano sul dispositivo. Inoltre, la query di ricerca viene passata a Exchange locale tramite Exchange Online. Exchange locale esegue la query di ricerca nella cassetta postale locale e restituisce i risultati a Exchange Online, che li inoltra al client. I risultati della query locale vengono archiviati in Exchange Online per un giorno prima di essere eliminati.

**D:**  Come si può sapere se l'account di posta elettronica è stato aggiunto correttamente in Outlook per iOS e Android?

**R:**  Le cassette postali locali aggiunte tramite l'autenticazione moderna ibrida sono etichettate come **Exchange (ibrido)** nelle impostazioni dell'account in Outlook per iOS e Android, come riportato nell'esempio seguente:

![Un esempio di un account Outlook per iOS e Android configurato per l'autenticazione moderna ibrida](images/Mt846639.79887a65-e5e1-4501-a274-008393dbb6c9(EXCHG.150).png "Un esempio di un account Outlook per iOS e Android configurato per l'autenticazione moderna ibrida")

## Domande frequenti sull'autenticazione

**D:**  Quali configurazioni di identità sono supportate con l'autenticazione moderna ibrida e Outlook per iOS e Android?

**R:**  Le seguenti configurazioni di identità con Azure Active Directory sono supportate con l'autenticazione moderna ibrida:

  - Identità federative con qualsiasi provider di identità locale supportato da Azure Active Directory

  - Sincronizzazione dell'hash delle password tramite Azure Active Directory Connect

  - Autenticazione pass-through tramite Azure Active Directory Connect

**D:**  Quale meccanismo di autenticazione viene utilizzato per Outlook per iOS e Android? Le credenziali vengono archiviate in Office 365?

**R:**  L'autenticazione basata su Active Directory Authentication Library (ADAL) viene utilizzata da Outlook per iOS e Android per accedere ai dati delle cassette postali locali sincronizzate con Exchange Online. Con l'autenticazione ADAL, usata dalle app di Office sia su dispositivi mobili che su desktop, gli utenti accedono direttamente ad Azure Active Directory, che è il provider di identità di Office 365, anziché fornendo le credenziali ad Outlook.

L'accesso basato su ADAL abilita OAuth per gli account locali di Exchange ibrido e fornisce ad Outlook per iOS e Android un meccanismo sicuro per accedere alla posta elettronica senza richiedere l'accesso alle credenziali dell'utente. All'accesso, l'utente viene autenticato direttamente con Microsoft Cloud e riceve un token di accesso. Il token concede ad Outlook per iOS e Android l'accesso alla cassetta postale appropriata. OAuth fornisce ad Outlook un meccanismo sicuro per accedere a Office 365 e al servizio cloud di Outlook senza richiedere o archiviare le credenziali di un utente.

Per ulteriori informazioni, vedere il post del blog di Office relativo ai [nuovi controlli di sicurezza e accesso per Outlook per iOS e Android](https://blogs.office.com/2015/06/10/new-access-and-security-controls-for-outlook-for-ios-and-android/).

**D:**  Outlook per iOS e Android e altre app per dispositivi mobili di Microsoft Office supportano Single Sign-On?

**R:**  Tutte le app di Microsoft che sfruttano Azure Active Directory Authentication Library (ADAL) supportano l'accesso Single Sign-On. Inoltre, Single Sign-On è supportato anche quando le app sono usate in combinazione con Microsoft Authenticator o con le app del Portale aziendale Microsoft.

I token possono essere condivisi e riutilizzati da altre app Microsoft (come Word Mobile) nei seguenti scenari:

1.  Quando si accede alle app tramite lo stesso certificato di accesso e si utilizza lo stesso URL del gruppo di destinatari o dell'endpoint di servizio (come l'URL di Office 365). In questo caso, il token viene memorizzato nell'archivio condiviso delle app.

2.  Quando le app sfruttano o supportano Single Sign-On con un'app broker. I token vengono memorizzati all'interno dell'app broker. Microsoft Authenticator è un esempio di app broker. Nello scenario con le app broker, dopo il tentativo di accesso ad Outlook per iOS e Android, ADAL avvia l'app Microsoft Authenticator, che consente di connettersi ad Azure Active Directory per ottenere il token. Il token viene quindi mantenuto riutilizzato per le richieste di autenticazione provenienti da altre app, finché consentito dalla durata del token configurata.

Per ulteriori informazioni, vedere [Come abilitare l'accesso Single Sign-On tra app in iOS usando ADAL](https://docs.microsoft.com/it-it/azure/active-directory/develop/active-directory-sso-ios).

**D:**  Che cos'è la durata dei token generati e usati da Active Directory Authentication Library (ADAL) in Outlook per iOS e Android?

**R:**  Quando un utente locale viene autenticato tramite le app basate su ADAL, come Outlook per iOS e Android, l'app Authenticator o l'app del Portale aziendale, vengono generati più token. La prima coppia di token di accesso e aggiornamento viene utilizzata per accedere ai dati sincronizzati in Exchange Online; la seconda coppia di token di accesso e aggiornamento viene utilizzata da Exchange Online per accedere alla cassetta postale locale tramite il protocollo Exchange ActiveSync. Il token di accesso viene utilizzato per accedere alla risorsa (come i dati dei messaggi di Exchange), mentre il token di aggiornamento viene usato per ottenere una nuova coppia di token di accesso o di aggiornamento alla scadenza del token di accesso corrente.

Per impostazione predefinita, la durata del token di accesso è un'ora e la durata del token di aggiornamento è 14 giorni. Questi valori possono essere modificati; per ulteriori informazioni, vedere [Durata dei token configurabili in Azure Active Directory (anteprima pubblica)](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes). Si noti che riducendo queste durate, è possibile che vengano ridotte anche le prestazioni di Outlook per iOS e Android, perché una durata più breve aumenta il numero di volte che l'applicazione deve acquisire un token di accesso aggiornato.

**D:**  Cosa accade al token di accesso quando viene modificata la password dell'utente?

**R:**  Un token di accesso concesso in precedenza è valido fino alla scadenza. Il modello di identità in uso per l'autenticazione influirà su come viene gestita la scadenza della password. Sono disponibili tre scenari:

1.  Per un modello di identità federativa, è necessario verificare che il provider di identità locale invii l'attestazione di scadenza della password ad Azure Active Directory; in caso contrario, Azure Active Directory non sarà in grado di gestire la scadenza della password. Per ulteriori informazioni, vedere [Configurare AD FS per l'invio delle attestazioni di scadenza della password](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims).

2.  La sincronizzazione dell'hash delle password non supporta la scadenza delle password. Questo significa che le app che in precedenza hanno ottenuto un token di accesso e aggiornamento continueranno a funzionare per tutta la durata della coppia di token o finché l'utente non modifica la propria password. Per ulteriori informazioni, vedere [Implementare la sincronizzazione dell'hash delle password con il servizio di sincronizzazione Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-hash-synchronization#how-password-synchronization-works).

3.  L'autenticazione pass-through richiede di attivare il writeback delle password in AAD Connect. Per ulteriori informazioni, vedere [Autenticazione pass-through di Azure Active Directory: domande frequenti](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication-faq#what-happens-if-my-users-password-has-expired-and-they-try-to-sign-in-by-using-pass-through-authentication).

Alla scadenza del token, il client tenterà di utilizzare il token di aggiornamento per ottenere un nuovo token di accesso, ma poiché è cambiata la password dell'utente, il token di aggiornamento verrà invalidato (presupponendo che si sia verificata la sincronizzazione delle directory tra quella locale e Azure Active Directory). Il token di aggiornamento invalidato impone all'utente di ripetere l'autenticazione per ottenere un nuovo token di accesso e aggiornare la coppia di token.

**D:**  Esiste un modo con cui l'utente può ignorare il servizio di rilevamento automatico quando aggiunge il proprio account a Outlook per iOS e Android?

**R:**  Sì, un utente può ignorare il servizio di rilevamento automatico in qualsiasi momento e configurare manualmente la connessione con l'autenticazione di base sul protocollo Exchange ActiveSync. Per far sì che l'utente non stabilisca una connessione al proprio ambiente locale con un meccanismo che non supporta l'accesso condizionale di Azure Active Directory o i criteri di protezione delle app di Intune, l'amministratore di Exchange locale deve configurare una regola di accesso ai dispositivi Exchange che impedisca la connessione ActiveSync. A tale scopo, digitare il comando seguente in Exchange Management Shell:

```powershell
 New-ActiveSyncDeviceAccessRule -Characteristic DeviceModel -QueryString "Outlook for iOS and Android" -AccessLevel Block
```


---
title: 'Prerequisiti per la distribuzione ibrida: Exchange 2013 Help'
TOCTitle: Prerequisiti per la distribuzione ibrida
ms:assetid: e7454db0-fed4-4662-8890-9501126b1ba2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh534377(v=EXCHG.150)
ms:contentKeyID: 50482161
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Prerequisiti per la distribuzione ibrida

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2017-07-25_

**Riepilogo:** requisiti dell'ambiente Exchange necessari per la configurazione di una distribuzione ibrida.

Affinché sia possibile creare e configurare una distribuzione ibrida utilizzando la procedura guidata di configurazione ibrida, è necessario che l'organizzazione locale di Exchange esistente soddisfi determinati requisiti. In caso contrario, non sarà possibile completare i passaggi della procedura guidata di configurazione ibrida e configurare una distribuzione ibrida che include l'organizzazione di Exchange locale ed Exchange Online.

## Prerequisiti per la distribuzione ibrida

Per configurare una distribuzione ibrida sono necessari i seguenti requisiti:

  - **Organizzazione di Exchange locale**   È possibile configurare distribuzioni ibride per organizzazioni locali basate su Exchange 2007 o versione successiva.
    
    La versione di Exchange installata nell'organizzazione locale determina la versione della distribuzione ibrida che è possibile installare. In genere, è necessario configurare la versione della distribuzione ibrida più recente supportata nell'organizzazione. Ad esempio, se l'organizzazione locale esegue Exchange 2007, è necessario configurare una distribuzione ibrida basata su Exchange 2013. Per informazioni complete sulla compatibilità della distribuzione ibrida di Exchange Server e Office 365 per aziende, vedere la tabella seguente.
    
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Ambiente locale</th>
    <th>Distribuzione ibrida basata su Exchange 2016</th>
    <th>Distribuzione ibrida basata su Exchange 2013</th>
    <th>Distribuzione ibrida basata su Exchange 2010</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Exchange 2016</p></td>
    <td><p>Supportato</p></td>
    <td><p>Non supportato</p></td>
    <td><p>Non supportato</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2013</p></td>
    <td><p>Supportato</p></td>
    <td><p>Supportata</p></td>
    <td><p>Non supportata</p></td>
    </tr>
    <tr class="odd">
    <td><p>Exchange 2010</p></td>
    <td><p>Supportata</p></td>
    <td><p>Supportato</p></td>
    <td><p>Supportato</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2007</p></td>
    <td><p>Non supportato</p></td>
    <td><p>Supportato</p></td>
    <td><p>Supportato</p></td>
    </tr>
    </tbody>
    </table>


  - **Versioni di Exchange locale** Le distribuzioni ibride richiedono l'aggiornamento cumulativo più recente per la versione di Exchange installata nell'organizzazione locale dell'utente. Se non è possibile installare l'aggiornamento cumulativo più recente, è supportata anche la versione immediatamente precedente. Gli aggiornamenti cumulativi meno recenti non sono supportati.
    
    Si supponga, ad esempio, di aver installato l'aggiornamento cumulativo 8 di Exchange 2013 nell'organizzazione locale e che la versione più recente di Exchange 2013 disponibile sia l'aggiornamento cumulativo 10. Per rimanere in una configurazione ibrida supportata, è necessario aggiornare i server di Exchange 2013 almeno all'aggiornamento cumulativo 9. Tuttavia, si consiglia vivamente di eseguire l'aggiornamento cumulativo 10.
    
    Gli aggiornamenti cumulativi vengono rilasciati ogni 3 mesi. Pertanto, aggiornare i server all'aggiornamento cumulativo più recente garantisce un'ulteriore flessibilità qualora fosse necessario più tempo per completare gli aggiornamenti.

  - **Ruoli server locali** I ruoli server da installare nell'organizzazione locale dipendono dalla versione di Exchange installata.
    
      - **Exchange 2010** Almeno un server con il ruolo del server Cassette postali, Trasporto Hub e Accesso client installato. Sebbene sia possibile installare i ruoli Cassette postali, Trasporto Hub e Accesso client su server separati, si consiglia vivamente di installare tutti i ruoli su ciascun server per fornire una maggiore affidabilità e prestazioni migliorate.
    
      - **Exchange 2013** Almeno un server con il ruolo del server Cassette postali e Accesso client installato. Sebbene sia possibile installare i ruoli Cassette postali e Accesso client su server separati, si consiglia vivamente di installare entrambi i ruoli su ciascun server per fornire una maggiore affidabilità e prestazioni migliorate.
    
      - **Exchange 2016 e versioni successive** Almeno un server con il ruolo del server Cassette postali installato.
    
    Le distribuzioni ibride supportano inoltre server di Exchange che eseguono il ruolo del server Trasporto Edge. È inoltre necessario aggiornare i server Trasporto Edge all'aggiornamento cumulativo più recente disponibile per la versione di Exchange installata. Si consiglia vivamente di distribuire i server Trasporto Edge in una rete perimetrale. Non è possibile distribuire i server Cassette postali e Accesso client in una rete perimetrale.

  - **Office 365**   Le distribuzioni ibride sono supportate in tutti i piani di Office 365 che supportano Sincronizzazione Azure Active Directory. Il supporto per le distribuzioni ibride è disponibile in tutti i piani di Office 365 Enterprise, Government, Academic e Midsize, ma non nei piani Office 365 Business e Home.
    
    Per ulteriori informazioni, vedere [Iscrizione a Office 365](https://go.microsoft.com/fwlink/p/?linkid=203981).

  - **Domini personalizzati**   Registrare qualunque dominio personalizzato da utilizzare nella distribuzione ibrida con Office 365. Questa operazione può essere eseguita dal portale di amministrazione di Office 365 oppure configurando Active Directory Federation Services (ADFS) nell'organizzazione locale.
    
    Per ulteriori informazioni, vedere [Aggiunta del dominio a Office 365](https://go.microsoft.com/fwlink/p/?linkid=229238).

  - **Sincronizzazione di Active Directory**   Distribuire lo strumento Azure Active Directory Connect per abilitare la sincronizzazione di Active Directory con l'organizzazione locale.
    
    Sono disponibili ulteriori informazioni nell'articolo [Opzioni di accesso utente di Azure AD Connect](http://go.microsoft.com/fwlink/p/?linkid=723514).

  - **Record DNS di individuazione automatica**   Configurare i record DNS pubblici di individuazione automatica per i domini SMTP esistenti in modo che puntino a un server Accesso client Exchange 2013 locale.

  - **Organizzazione di Office 365 nell'interfaccia di amministrazione di Exchange (EAC)**   Il nodo dell'organizzazione di Office 365 viene incluso per impostazione predefinita in EAC locale, ma per utilizzare la procedura guidata di configurazione ibrida è necessario connettere EAC all'organizzazione Office 365 utilizzando le credenziali di amministratore di Office 365. In questo modo è inoltre possibile gestire sia l'organizzazione locale che l'organizzazione di Exchange Online da una singola console di gestione.
    
    Per ulteriori informazioni, vedere [Gestione ibrida nelle distribuzioni ibride di Exchange](hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md).

  - 
    
    **Certificati**   Installare e assegnare i servizi di Exchange a un certificato digitale valido acquistato da un'autorità di certificazione (CA) pubblica attendibile. Anche se per la relazione di trust federativa locale con Microsoft Federation Gateway è possibile utilizzare certificati autofirmati, tali certificati non possono essere utilizzati per i servizi di Exchange in una distribuzione ibrida. L'istanza di Internet Information Services (IIS) nei server Exchange configurati nella distribuzione ibrida deve disporre di un certificato digitale valido acquistato da un'autorità di certificazione (CA) attendibile. Inoltre, l'URL esterno della directory EWS e l'endpoint di individuazione automatica specificato nel DNS pubblico devono essere riportati nel nome alternativo del soggetto del certificato. Tutti i certificati installati nei server Exchange utilizzati per il trasporto della posta nella distribuzione ibrida devono utilizzare lo stesso certificato (ovvero essere emessi dalla stessa CA e avere lo stesso soggetto).
    
    Per ulteriori informazioni, vedere [Requisiti dei certificati per le distribuzioni ibride](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md).

  - **EdgeSync**   Se nell'organizzazione locale sono distribuiti server Trasporto Edge e si desidera configurarli per il trasporto ibrido sicuro della posta, è necessario configurare EdgeSync prima di utilizzare la procedura guidata di configurazione ibrida. È inoltre necessario eseguire EdgeSync ogni volta che viene applicato un nuovo aggiornamento cumulativo a un server Trasporto Edge.
    

    > [!IMPORTANT]
    > Anche se EdgeSync costituisce un requisito nelle distribuzioni con server Trasporto Edge, quando si configurano i server Trasporto Edge per il trasporto ibrido sicuro della posta è necessario specificare manualmente utileriori Impostazioni di configurazione del trasporto.

    
    Per ulteriori informazioni, vedere [Server Trasporto Edge con distribuzioni ibride](edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md).

  - **Cassette postali abilitate alla messaggistica unificata** Se l'utente dispone di cassette postali abilitate alla messaggistica unificata e desidera spostarle in Office 365, deve eseguire la procedura riportata di seguito e disporre di una distribuzione ibrida di Exchange. Questi requisiti devono essere soddisfatti **prima** di spostare le cassette postali abilitate alla messaggistica unificata su Office 365.
    
      - Lync Server 2010, Lync Server 2013 o Skype for Business Server 2015 o versioni successive integrati con il sistema telefonico locale **oppure**
    
      - Skype for Business Online integrato con il sistema telefonico locale **oppure**
    
      - Una soluzione PBX o IP-PBX locale tradizionale.
    
      - Criteri della cassetta postale di messaggistica unificata creati in Exchange Online che eseguono il mirroring dei nomi dei criteri della cassetta postale di messaggistica unificata nell'organizzazione locale.
        

        > [!NOTE]
        > È possibile eseguire il mapping di più criteri della cassetta postale di messaggistica unificata locale su un criterio della cassetta postale di messaggistica unificata in Exchange Online. Per effettuare questa operazione, sarà necessario utilizzare Exchange Management Shell per mappare manualmente ogni criterio della cassetta postale di messaggistica unificata a un criterio di Exchange Online.

    
    Per ulteriori informazioni, vedere [Integrazione del telefono sistema con la messaggistica UNIFICATA](https://technet.microsoft.com/it-it/library/jj673558\(v=exchg.150\)), [Sistema di telefonia per Exchange 2013](https://technet.microsoft.com/it-it/library/ee364753\(v=exchg.150\)) e [Impostare la segreteria telefonica Cloud PBX](https://go.microsoft.com/fwlink/p/?linkid=826207).

## Protocolli, porte ed endpoint per la distribuzione ibrida

Le funzionalità e i componenti per la distribuzione ibrida richiedono l'accessibilità di determinati protocolli in ingresso, porte ed endpoint di connessione da parte di Office 365 per funzionare correttamente. Prima di configurare la distribuzione ibrida, verificare che la rete locale e la configurazione di protezione siano in grado di supportare le funzionalità e i componenti indicati nella tabella di seguito. Oltre a consentire determinati protocolli in ingresso, porte ed endpoint, i computer nella rete devono anche essere abilitati all'accesso a indirizzi IP, porte e URL elencati in [URL e intervalli di indirizzi IP di Office 365](https://go.microsoft.com/fwlink/?linkid=823100).


<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocollo di trasporto</th>
<th>Protocollo di livello superiore</th>
<th>Funzionalità/componente</th>
<th>Endpoint locale</th>
<th>Percorso locale</th>
<th>Provider di autenticazione</th>
<th>Metodo di autorizzazione</th>
<th>Autorizzazione preventiva supportata?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP 25 (SMTP)</p></td>
<td><p>SMTP/TLS</p></td>
<td><p>Flusso di posta tra Office 365 e ambienti locali</p></td>
<td><p>Exchange 2016 Cassetta postale/Edge</p>
<p>Exchange 2013 CAS/Edge</p>
<p>Exchange 2010 HUB/EDGE</p></td>
<td><p>N/D </p></td>
<td><p>N/D</p></td>
<td><p>Basato su certificato</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>Individuazione automatica</p></td>
<td><p>Individuazione automatica</p></td>
<td><p>Cassetta postale di Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Sistema di autenticazione Azure AD</p></td>
<td><p>Autenticazione WS-Security</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>Libero/occupato, Suggerimenti messaggio, Verifica messaggi</p></td>
<td><p>Cassetta postale di Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p></td>
<td><p>Sistema di autenticazione Azure AD</p></td>
<td><p>Autenticazione WS-Security</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>Ricerca in più cassette postali</p></td>
<td><p>Cassetta postale di Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Server di autenticazione</p></td>
<td><p>Autenticazione WS-Security</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>Migrazioni delle cassette postali</p></td>
<td><p>Cassetta postale di Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/mrsproxy.svc</p></td>
<td><p>NTLM</p></td>
<td><p>Di base</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>Individuazione automatica</p>
<p>EWS</p></td>
<td><p>OAuth</p></td>
<td><p>Cassetta postale di Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Server di autenticazione</p></td>
<td><p>Autenticazione WS-Security</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>N/D</p></td>
<td><p>AD FS (incluso in Windows)</p></td>
<td><p>Windows 2008/2012 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Sistema di autenticazione Azure AD</p></td>
<td><p>Varia in base alla configurazione</p></td>
<td><p>Due fattori</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>N/D</p></td>
<td><p>Azure Active Directory Connect con AD FS</p></td>
<td><p>Windows 2012 R2 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Sistema di autenticazione Azure AD</p></td>
<td><p>Varia in base alla configurazione</p></td>
<td><p>Due fattori</p></td>
</tr>
</tbody>
</table>


## Servizi e strumenti consigliati

Oltre ai prerequisiti descritti in precedenza, sono disponibili altri strumenti e servizi utili per la configurazione delle distribuzioni ibride con la procedura guidata di configurazione ibrida:

  - **Assistente per la distribuzione di Exchange Server**   L'Assistente per la distribuzione di Exchange Server è uno strumento gratuito basato sul Web che consente di distribuire Exchange nell'organizzazione locale, configurare una distribuzione ibrida tra l'organizzazione locale e Office 365 oppure di migrare completamente a Office 365. Lo strumento pone una piccola serie di domande, quindi, in base alle risposte, crea un elenco di controllo personalizzato con le istruzioni per distribuire o configurare Exchange Server. L'Assistente per la distribuzione fornisce esattamente le informazioni necessarie per configurare la distribuzione ibrida.
    
    Per ulteriori informazioni, vedere [Assistente per la distribuzione di Exchange Server](https://technet.microsoft.com/exdeploy2013).
    
     

  - **Remote Connectivity Analyzer**   Lo strumento Remote Connectivity Analyzer verifica la connettività esterna dell'organizzazione locale di Exchange e verifica che tale organizzazione sia pronta per configurare una distribuzione ibrida. È consigliabile controllare l'organizzazione locale con lo strumento Remote Connectivity Analyzer prima di configurare la distribuzione ibrida con la procedura guidata apposita.
    
    Ulteriori informazioni su [Analizzatore connettività remota di Microsoft](https://testconnectivity.microsoft.com/).
    
     

  - **Single Sign-On**   Single Sign-On permette agli utenti di accedere a entrambe le organizzazioni, locale e di Exchange Online, con un singolo nome utente e password. Offre agli utenti un'esperienza di accesso familiare e consente agli amministratori di controllare facilmente i criteri di account per le cassette postali dell'organizzazione di Exchange Online utilizzando gli strumenti di gestione di Active Directory locali.
    
    Sono disponibili due opzioni per la distribuzione di Single Sign-On: sincronizzazione password e Active Directory Federation Services. Entrambe le opzioni vengono fornite da Azure Active Directory Connect. La sincronizzazione della password consente a quasi tutte le organizzazione, indipendentemente dalle loro dimensioni, di implementare Single Sign-On senza particolari problemi. Inoltre, dal momento che l'esperienza utente in una distribuzione ibrida è notevolmente migliore con Single Sign-On attivato, è consigliabile implementarlo. Per le organizzazioni di grandi dimensioni, come quelle con più foreste di Active Directory che necessitano della distribuzione ibrida, è richiesto Active Directory Federation Services.
    
    Per ulteriori informazioni, vedere: [Accesso Single Sign-On con distribuzioni ibride](single-sign-on-with-hybrid-deployments-exchange-2013-help.md)


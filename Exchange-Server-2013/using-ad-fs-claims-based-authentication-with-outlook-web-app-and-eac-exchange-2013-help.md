---
title: 'Autenticaz. su attestazioni ADFS con Outlook Web App e EAC: Exchange 2013 Help'
TOCTitle: Utilizzando l'autenticazione basata sulle attestazioni ADFS con Outlook Web App ed EAC
ms:assetid: 919a9bfb-c6df-490a-b2c4-51796b0f0596
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn635116(v=EXCHG.150)
ms:contentKeyID: 61202270
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzando l'autenticazione basata sulle attestazioni ADFS con Outlook Web App ed EAC

 

_**Si applica a:** Exchange Server 2013 SP1_

_**Ultima modifica dell'argomento:** 2017-04-14_

**Riepilogo**:

Per le distribuzioni di on-premise Exchange 2013 Service Pack 1 (SP1), l'installazione e configurazione Active Directory Federation Services (ADFS) indica che è ora possibile utilizzare l'autenticazione basata sulle attestazioni ADFS per connettersi a Outlook Web App ed EAC. È possibile integrare ADFS e autenticazione basata sulle attestazioni con Exchange 2013 SP1. Utilizzo dell'autenticazione basata sulle attestazioni sostituisce metodi di autenticazione tradizionali, incluse le operazioni seguenti:

  - Autenticazione di Windows

  - Autenticazione basata su form

  - Autenticazione del digest

  - Autenticazione di base

  - Autenticazione certificati dei client Active Directory

L'autenticazione è il processo di verifica dell'identità di un utente. L'autenticazione convalida che l'utente sia effettivamente chi dichiara di essere. L'identità basata sulle attestazioni è un altro approccio per l'autenticazione. L'autenticazione basata sulle attestazioni rimuove la gestione dell'autenticazione dall'applicazione—in questo case, Outlook Web App e EAC—possono facilitare la gestione degli account centralizzando l'autenticazione. Outlook Web App e EAC non sono responsabili dell'autenticazione degli utenti, archiviano le password e gli account utente, ricercano i dettagli sull'identità dell'utente o li integrano con altri sistemi di identità. L'autenticazione della centralizzazione semplifica l'aggiornamento a futuri metodi di autenticazione.


> [!NOTE]
> OWA per i dispositivi non supporta l'autenticazione basata sulle attestazioni ADFS.



Sono disponibili più versioni di ADFS che può essere utilizzato, come riepilogato nella tabella seguente.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>versione Windows Server</th>
<th>Installazione</th>
<th>Versione di Active Directory FS</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2008 R2</p></td>
<td><p><strong>Download e installazione</strong> ADFS 2.0, un componente aggiuntivo di Windows.</p></td>
<td><p>ADFS 2.0</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p>Installare il ruolo del server ADFS <strong>incorporato</strong>.</p></td>
<td><p>ADFS 2.1</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p>Installare il ruolo del server ADFS <strong>incorporato</strong>.</p></td>
<td><p>ADFS 3.0</p></td>
</tr>
</tbody>
</table>


Le attività che verranno qui eseguite sono basate su Windows Server 2012 R2 che include il servizio di ruolo ADFS.

**Panoramica dei passaggi necessari**

Step 1 - Review the certificate requirements for AD FS

Step 2 - Install and configure Active Directory Federation Services (AD FS)

Passaggio 3: creare un trust relying party e regole attestazioni personalizzate per Outlook Web App ed EAC

Passaggio 4 - installare il servizio ruolo di Proxy dell'applicazione Web (facoltativo)

Passaggio 5 - configurare il servizio ruolo di Proxy dell'applicazione Web (facoltativo)

Passaggio 6 - pubblicare Outlook Web App ed EAC utilizzando Proxy applicazione Web (facoltativo)

Passaggio 7 - configurazione di Exchange 2013 per utilizzare l'autenticazione ADFS

Passaggio 8: abilitare l'autenticazione ADFS sulle directory virtuale OWA ed ECP

Passaggio 9 - riavvio o riciclo di Internet Information Services (IIS)

Passaggio 10 - verificare le attestazioni ADFS per Outlook Web App ed EAC

Additional information you might want to know

## Informazioni necessarie per iniziare

  - È necessario almeno installare server Windows Server 2012 R2 separati: uno come controller di domino che utilizza Active Directory servizi di dominio (AD DS), un server Exchange 2013, un server Proxy di applicazione Web e un server Active Directory Federation Services (ADFS). Verificare che siano installati tutti gli aggiornamenti.

  - Installare Active Directory su un numero appropriato di server Windows Server 2012 R2 dell'organizzazione. È inoltre possibile utilizzare le **Notifiche** in **Server Manager** \> **Dashboard** per **Promuovere il server a controller di dominio**.

  - Installare il numero appropriato di server di accesso Client e cassette postali per l'organizzazione. Verificare che tutti gli aggiornamenti siano stati installati, tra cui SP1, su tutti i server Exchange 2013 nell'organizzazione. Per scaricare SP1, vedere [Aggiornamenti per Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

  - La distribuzione di Proxy di applicazione Web su un server richiede autorizzazioni di amministratore locale. È necessario distribuire ADFS su un server che esegue Windows Server 2012 R2 nell'organizzazione prima di poter distribuire il Proxy di applicazione Web.

  - Installare e configurare il ruolo ADFS e creare trust relying party e regole di attestazione su Windows Server 2012 R2. A tale scopo, è necessario accedere con un account utente appartenente al gruppo Domain Admins, Enterprise Admins o Administrators locale.

  - Determinare le autorizzazioni necessarie per Exchange 2013 visualizzando i [Autorizzazioni funzionalità](feature-permissions-exchange-2013-help.md).

  - È necessario assegnare le autorizzazioni per la gestione dei Outlook Web App. Per verificare le autorizzazioni necessarie, vedere la voce "Autorizzazioni di Outlook Web App" [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - È necessario assegnare le autorizzazioni per la gestione EAC. Per sapere quali autorizzazioni sono necessarie, vedere la voce "Connettività dell'interfaccia di amministrazione di Exchange" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo la Shell per eseguire alcune procedure. Per sapere come aprire Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Passo 1 – Verificare i requisiti del certificato per ADFS

I certificati svolgono un ruolo fondamentale nelle comunicazioni di sicurezza tra server Exchange 2013 SP1; i client Web come Outlook Web App; EAC, server Windows Server 2012 R2, tra cui Active Directory server Federation Services (ADFS) e server Proxy di applicazione Web. I requisiti per i certificati variano a seconda se si sta impostando un server ADFS, proxy ADFS o un server Proxy di applicazione Web. I certificati utilizzati per i servizi ADFS tra cui SSL e certificati di firma dei token devono essere importati nell'archivio delle autorità di certificazione di origine attendibile su tutti i server di Exchange, ADFS e Proxy di applicazione Web. L'identificazione personale per il certificato importato viene inoltre utilizzato su server Exchange 2013 SP1 quando si utilizza il cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\)).

In tutte le strutture di AD FS diversi certificati da utilizzare per proteggere le comunicazioni tra gli utenti sui server ADFS Internet e Active Directory. Ogni server federativo deve disporre di un certificato di comunicazione del servizio o certificato Secure Socket Layer (SSL) e un certificato di firma di token prima del server ADFS, controller di dominio Active Directory, e i server Exchange 2013 possono comunicare e eseguire l'autenticazione. A seconda della protezione e i requisiti di budget, valutare con attenzione che i certificati vengono ottenuti dal pubblico CA o una CA dell'organizzazione. Se si desidera installare e configurare un radice dell'organizzazione o della CA subordinata, è possibile utilizzare Active Directory Servizi certificati (Servizi certificati Active Directory). Se si desidera ottenere maggiori informazioni sui servizi certificati Active Directory, vedere [Panoramica di servizi di Active Directory certificato](https://go.microsoft.com/fwlink/?linkid=392697).

Sebbene ADFS non richieda che i certificati vengano emessi da una CA, il certificato SSL (il certificato SSL utilizzato inoltre per impostazione predefinita come certificato delle comunicazioni di servizio) deve essere considerato attendibile dai client ADFS. Si consiglia di non utilizzare i certificati autofirmati. I server federativi utilizzano certificati SSL per assicurare il traffico dei servizi Web per comunicazioni SSL con client Web e con server proxy federativi. Siccome il certificato SSL deve essere considerato attendibile da computer client, si consiglia di utilizzare un certificato firmato da una CA attendibile. Tutti i certificati selezionati devono avere una chiave privata corrispondente. Dopo aver ricevuto un certificato da una CA (aziendale o pubblica), assicurarsi che tutti i certificati siano importati nell'archivio delle autorità di certificazione di origine attendibile su tutti i server. È possibile importare certificati nell'archivio con snap-in MMC **Certificati** o distribuire i certificati utilizzando Servizi certificati Active Directory. Se il certificato importato è scaduto, è importante importare manualmente un altro certificato valido.


> [!IMPORTANT]
> Se si utilizza un certificato autofirmato per la firma dei token da ADFS, è necessario importarlo nell'archivio delle autorità di certificazione di origine attendibile su tutti i server Exchange 2013. Se il certificato autofirmato per la firma dei token non è utilizzato e il Proxy di applicazione Web viene distribuito, è necessario aggiornare la chiave pubblica nella configurazione Proxy di applicazione Web e tutti i trust relying party ADFS.



Quando si configura Exchange 2013 SP1, ADFS e il Proxy di applicazione Web, attenersi ai seguenti consigli sui certificati:

  - **Server cassette postali**   I certificati utilizzati sui server cassette postali sono autofirmati al momento della creazione quando Exchange 2013 viene installato. Siccome tutti i client connessi a un server cassette postali Exchange 2013 tramite server di accesso client Exchange 2013, i soli certificati che è necessario gestire sono quelli sui server di accesso client.

  - **Server di accesso client** È richiesto un certificato SSL utilizzato per le comunicazioni di servizio. Se il certificato SSL esistente include già l'FQDN utilizzato per configurare l'endpoint trust relying party, non sono necessari ulteriori certificati.

  - **ADFS** Da ADFS sono richiesti due tipi di certificati:
    
      - Il certificato SSL utilizzato per comunicazioni di servizio
        
          - Nome soggetto: **adfs.contoso.com** (nome di distribuzione ADFS)
        
          - Nome alternativo soggetto (SAN): nessuno
    
      - Certificato per la firma di token
        
          - Nome soggetto: **tokensigning.contoso.com**
        
          - Nome alternativo soggetto (SAN): nessuno
        

        > [!NOTE]
        > Quando il certificato autofirmato per la firma di token su ADFS viene sostituito, tutti i trust relying party devono essere aggiornati per utilizzare il nuovo certificato per la firma dei token.



  - **Proxy di applicazione Web**
    
      - Il certificato SSL utilizzato per comunicazioni di servizio
        
          - Nome soggetto: **owa.contoso.com**
        
          - Nome alternativo soggetto (SAN): nessuno
        

        > [!NOTE]
        > Se l'URL esterno del proxy di applicazioni Web è lo stesso dell'URL interno, qui è possibile utilizzare nuovamente il certificato SSL di Exchange.

    
      - Certificato SSL Proxy FS Active Directory
        
          - Nome soggetto: **adfs.contoso.com** (nome di distribuzione ADFS)
        
          - Nome alternativo soggetto (SAN): nessuno
    
      - Certificato per la firma di token - Tale certificato verrà automaticamente copiato da ADFS in quanto parte della seguente procedura. Se il certificato viene utilizzato, deve essere considerato affidabile dai server Exchange 2013 nell'organizzazione.

Vedere la sezione requisiti di certificato in [Rivedere i requisiti per la distribuzione di AD FS](https://go.microsoft.com/fwlink/?linkid=392699) per ulteriori informazioni sui certificati.


> [!NOTE]
> Un certificato di crittografia SSL è ancora necessario per Outlook Web App e EAC anche se si dispone di un certificato SSL per ADFS. Il certificato SSL viene utilizzato per le directory virtuali di OWA ed ECP.



## Passaggio 2 – Installare e configurare Active Directory Federation Services (ADFS)

ADFS in Windows Server 2012 R2 fornisce federazione dell'identità della sicurezza semplificata e capacità single sign-on (SSO) Web. ADFS include un servizio federativo che consente l'autenticazione basata sulle attestazioni basate su browser Web SSO e multifattoriale. ADFS semplifica l'accesso a sistemi e applicazioni utilizzando un meccanismo di autorizzazione di accesso e di autenticazione basata sulle attestazioni per mantenere la sicurezza delle applicazioni.

Per installare ADFS in Windows Server 2012 R2:

1.  aprire **Server Manager** sulla schermata **Start** o **Server Manager** sulla barra delle applicazioni sul desktop. Fare clic su **Aggiungi ruoli e funzionalità** sul menu **Gestione**.

2.  Sulla pagina **Informazioni preliminari**, fare clic su **Avanti**.

3.  Sulla pagina **Seleziona tipo di installazione**, fare clic su **Installazione basata su ruolo o funzionalità**, quindi fare clic su **Avanti**.

4.  Sulla pagina **Seleziona server di destinazione**, fare clic su **Seleziona un server dal pool di server**, verificare che il computer locale sia selezionato, quindi fare clic su **Avanti**.

5.  Nella pagina **Seleziona ruoli server**, fare clic su **Active Directory Federation Services**, quindi fare clic su **Avanti**.
    
    Nella pagina **Seleziona funzionalità** fare clic su **Avanti**. I prerequisiti o funzionalità richiesti sono già stati selezionati automaticamente. Non è necessario riavviare alcuna funzionalità.

6.  Nella pagina **Active Directory Federation Services (ADFS)** fare clic su **Avanti**.

7.  Nella pagina **Conferma selezioni di installazione**, verificare **Se richiesto, riavviare automaticamente il server di destinazione**, quindi fare clic su **Installa**.
    

    > [!NOTE]
    > Non chiudere la procedura guidata durante il processo di installazione.



Dopo aver installato il server ADFS necessarie e generare i certificati necessari, è necessario configurare ADFS e quindi verificare il corretto funzionamento di ADFS. È inoltre possibile utilizzare l'elenco di controllo a seguito che consentono di installazione e configurazione di ADFS: [Checklist: impostazione di un Federation Server](https://go.microsoft.com/fwlink/?linkid=392700).

Per configurare server federativi Active Directory:

1.  Nella pagina **Avanzamento installazione**, nella finestra in **Active Directory Federation Services**, fare clic su **Configurazione del servizio federativo sul server**. Verrà visualizzata la configurazione guidata di Active Directory Federation Service.

2.  Nella pagina **iniziale**, fare clic su **Crea il primo server federativo in una server farm di federazione**, quindi fare clic su **Avanti**.

3.  Nella pagina **Connessione a AD DS**, specificare un account con diritti di amministratore di dominio per il corretto dominio Active Directory a cui è unito il computer e fare clic su **Avanti**. Per selezionare una posizione diversa, fare clic su **Modifica**.

4.  Nella pagina **Specificare le proprietà del servizio**, eseguire le operazioni seguenti e quindi fare clic su **Avanti**:
    
      - Importare il certificato SSL fornito in precedenza da un'autorità di certificazione pubblica o servizi certificati Active Directory. Questo certificato è il certificato di autenticazione richiesto servizio. Passare al percorso del certificato SSL. Per ulteriori informazioni sulla creazione e l'importazione dei certificati SSL, vedere [I certificati Server](https://go.microsoft.com/fwlink/?linkid=392703).
    
      - Immettere un nome per il servizio federativo, ad esempio, digitare **adfs.contoso.com**.
    
      - Per fornire un nome visualizzato per il servizio federativo, digitare il nome dell'organizzazione, ad esempio, **Contoso, Ltd.**.

5.  Nella pagina **Specificare account di servizio**, selezionare **Utilizzare un account utente del dominio esistente o account di servizio gestito**, quindi specificare l'account GMSA (FsGmsa) creato al momento della creazione del controller di dominio. Includere la password dell'account, quindi fare clic su **Avanti**.
    

    > [!NOTE]
    > Globally Managed Service Account (GMSA) è un account che deve essere creato quando si configura un controller di dominio. Durante la configurazione e installazione di ADFS è necessario l'account GMSA. Se questo account non è stato ancora creato, eseguire il seguente comando PowerShell Windows. Consente di creare l'account per il dominio contoso.com e per il server ADFS:



6.  Eseguire il comando riportato di seguito.
    
        Add-KdsRootKey -EffectiveTime (Get-Date).AddHours(-10)

7.  Questo esempio viene creato un nuovo account GMSA denominato FsGmsa per il servizio federativo denominato adfs.contoso.com. Il nome del servizio federativo è il valore che è visibile ai client.
    
        New-ADServiceAccount FsGmsa -DNSHostName adfs.contoso.com -ServicePrincipalNames http/adfs.contoso.com

8.  Nella pagina **Specificare database di configurazione**, selezionare **Creare un database sul server utilizzando Database interno di Windows**, quindi fare clic su **Avanti**.

9.  Nella pagina **Opzioni di revisione**, verificare le selezioni di configurazione. Facoltativamente è possibile utilizzare il pulsante **Visualizza script** per rendere automatiche le installazioni ADFS aggiuntive. Fare clic su **Avanti**.

10. Nella pagina **Controlli dei prerequisiti**, verificare che tutti i prerequisiti siano stati completati correttamente, quindi fare clic su **Configura**.

11. Nella pagina **Avanzamento installazione**, verificare che tutto sia installato correttamente, quindi fare clic su **Chiudi**.

12. Nella pagina **Risultati**, rivedere i risultati, verificare che la configurazione sia stata eseguita correttamente, quindi fare clic su **Passaggi successivi per il completamento della distribuzione del servizio federativo**.

I seguenti comandi di PowerShell Windows eseguire la stessa funzione dei passaggi precedenti.
```
Import-Module ADFS
```
```
Install-AdfsFarm -CertificateThumbprint 0E0C205D252002D535F6D32026B6AB074FB840E7 -FederationServiceDisplayName "Contoso Corporation" -FederationServiceName adfs.contoso.com -GroupServiceAccountIdentifier "contoso\FSgmsa`$"
```

Per informazioni dettagliate e sintassi, vedere [Install-AdfsFarm](https://go.microsoft.com/fwlink/?linkid=392704).

Per verificare l'installazione: Sul server ADFS, aprire il browser Web e selezionare l'URL dei metadati federati, ad esempio **https://adfs.contoso.com/federationmetadata/2007-06/federationmetadata.xml**.

## Passaggio 3: creare un trust relying party e regole attestazioni personalizzate per Outlook Web App ed EAC

Per tutte le applicazioni e servizi che si desidera pubblicare tramite Proxy dell'applicazione Web, è necessario configurare un trust relying party nel server ADFS. Per le distribuzioni con più siti Active Directory che utilizzano spazi dei nomi distinti, è necessario aggiungere un trust relying party per Outlook Web App ed EAC per ogni spazio dei nomi.

EAC utilizza la directory virtuale ECP. È possibile visualizzare o configurare le impostazioni per EAC utilizzando i cmdlet [Get-EcpVirtualDirectory](https://technet.microsoft.com/it-it/library/dd351058\(v=exchg.150\)) e [Set-EcpVirtualDirectory](https://technet.microsoft.com/it-it/library/dd297991\(v=exchg.150\)). Per accedere a EAC, è necessario utilizzare un browser Web e accedere a **http://server1.contoso.com/ecp**.


> [!NOTE]
> L'inclusione di barra finale <STRONG>/</STRONG> negli esempi URL indicato di seguito è intenzionale. È importante verificare che il trust relying party di ADFS e <STRONG>sono identici dell'URI gruppo di destinatari di Exchange</STRONG>. Ciò significa AD FS relying party trust e dell'URI di Exchange gruppo di destinatari devono <STRONG>disporre</STRONG> o <STRONG>entrambi emettere</STRONG> le finali barre negli URL. Gli esempi illustrati in questa sezione contengono le finali <STRONG>/</STRONG> dopo un url che termina con "owa" (/owa/) o "ecp" (/ecp/).



Per Outlook Web App, creare trust relying party utilizzando snap-in di gestione ADFS in Windows Server 2012 R2:

1.  In **Server Manager**, fare clic su **Strumenti**, quindi selezionare **Gestione di Active Directory FS**.

2.  Su **snap-in ADFS**, in **Relazioni di trust\\ADFS**, fare clic con il pulsante destro del mouse su **Trust relying party**, quindi fare clic su **Aggiungi trust Relying Party** per aprire la procedura guidata **Aggiungi trust Relying Party**.

3.  Nella pagina **iniziale**, fare clic su **Start**.

4.  Nella pagina **Seleziona fonte dati**, fare clic su **Immettere manualmente dati su relying party**, quindi fare clic su **Avanti**.

5.  Nella pagina **Specificare il nome visualizzato** nella casella **Nome visualizzato** digitare **Outlook Web App**e quindi digitare una descrizione per il trust relying party (ad esempio, **si tratta di una relazione di trust per https://mail.contoso.com/owa/**) in **note**, e Fare clic su **Avanti**.

6.  Nella pagina **Scegli profilo**, scegliere **Profilo ADFS**, quindi scegliere **Avanti**.

7.  Nella pagina **Configurazione certificato**, fare clic su **Avanti**.

8.  Nella pagina **Configurazione URL**, fare clic su **Abilita il supporto del protocollo WS-Federation Passive** e quindi in **URL di protocollo Relying party WS-Federation Passive**, **type https://mail.contoso.com/owa/**, quindi fare clic su Avanti .

9.  Nella pagina **Configurazione identificatori**, specificare uno o più identificatori per la relying party, fare clic su **Aggiungi** per aggiungerli all'elenco, quindi fare clic su **Avanti**.

10. Nella pagina **Configurare autenticazione a più fattori?**, selezionare **Configurare impostazioni autenticazione a più fattori per il trust relying party**.

11. Nella pagina **Configurazione autenticazione a più fattori**, verificare che sia selezionato **Non desidero configurare le impostazioni autenticazione a più fattori per il trust relying party** e selezionare **Avanti**.

12. Nella pagina **Scelta ruoli autorizzazioni del rilascio**, selezionare **Consenti a tutti gli utenti di accedere al relying party**, quindi selezionare **Avanti**.

13. Nella pagina **Pronto per aggiungere Trust**, rivedere le impostazioni, quindi scegliere **Avanti** per salvare le informazioni trust relying party.

14. Nella pagina **Fine**, verificare che **Apri la finestra di dialogo Modifica regole attestazioni per il trust relying party al termine della procedura guidata** non sia selezionata, quindi scegliere **Chiudi**.

Per creare trust relying party per EAC, è necessario eseguire nuovamente la seguente procedura e creare un secondo trust relying party ma, invece di inserire **Outlook Web App** per il nome visualizzato, immettere **EAC**. Per la descrizione, immettere **This is a trust for the Exchange Admin Center**, poi **URL protocollo Relying party WS-Federation Passive** è **https://mail.contoso.com/ecp**.

In un modello identità basato sulle attestazioni, la funzione di Active Directory Federation Services (ADFS) come servizio federativo è di rilasciare un token contenente un insieme di attestazioni. Le regole attestazioni regolano le decisioni riguardo le attestazioni emesse da ADFS. Le regole attestazioni e tutti i dati sulle configurazioni server vengono archiviati nel database di configurazione di ADFS.

È necessario creare due regole attestazione:

  - Active Directory SID utente

  - Active Directory UPN

Per aggiungere le regole attestazione necessarie:

1.  In **Server Manager**, fare clic su **Strumenti**, quindi selezionare **Gestione di Active Directory FS**.

2.  Nella struttura della console, in **Relazioni di trust\\ADFS**, fare clic su **Trust provider attestazioni** o **Trust Relying Party**, quindi fare clic su trust relying party per Outlook Web App.

3.  Nella finestra **Trust Relying Party**, fare clic con il pulsante destro del mouse su trust Outlook Web App, quindi fare clic con **Modifica regole attestazioni**.

4.  Nella finestra **Modifica regole attestazioni**, nella scheda **Regole trasformazione rilascio**, fare clic su **Aggiungi regola** per avviare la procedura guidata Aggiungi regola trasformazione attestazioni.

5.  Nella pagina **Seleziona modello regola**, in **Modello di regola reclamo**, selezionare **Invia attestazioni utilizzando una regola personalizzata** nell'elenco, quindi fare clic su **Avanti**.

6.  Nella pagina **Configurazione regola**, nel passaggio **Scegli tipo di regola**, in **Nome regola attestazioni**, immettere il nome per la relativa regola. Utilizzare un nome descrittivo per la regola attestazione, ad esempio, **ActiveDirectoryUserSID**. In **Regole personalizzate**, immettere la seguente sintassi di linguaggio regola attestazione per questa regola:
    
        c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value);

7.  Nella pagina **Configura regola**, fare clic su **Fine**.

8.  Nella finestra **Modifica regole attestazioni**, nella scheda **Regole trasformazione rilascio**, fare clic su **Aggiungi regola** per avviare la procedura guidata Aggiungi regola trasformazione attestazioni.

9.  Nella pagina **Seleziona modello regola**, in **Modello di regola reclamo**, selezionare **Invia attestazioni utilizzando una regola personalizzata** nell'elenco, quindi fare clic su **Avanti**.

10. Nella pagina **Configurazione regola**, nel passaggio **Scegli tipo di regola**, in **Nome regola attestazioni**, immettere il nome per la relativa regola. Utilizzare un nome descrittivo per la regola attestazione, ad esempio, **ActiveDirectoryUPN**. In **Regole personalizzate**, immettere la seguente sintassi di linguaggio regola attestazione per questa regola:
    
        c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

11. Fare clic su **Fine**.

12. Nella finestra **Modifica regole attestazione**, fare clic su **Applica**, quindi su **OK**.

13. Ripetere i passaggi 3-12 di questa procedura per EAC relying trust di terze parti.

In alternativa, è possibile creare trust inoltro party e regole di attestazione utilizzando Windows PowerShell:

1.  Creare i due file IssuanceAuthorizationRules.txt e IssuanceTransformRules.txt con estensione .txt.

2.  Importare il contenuto in due variabili.

3.  Eseguire i due seguenti cmdlet per creare i trust relying party. In questo esempio, vengono anche configurate le regole attestazione.

**IssuanceAuthorizationRules.txt contiene:** 

    @RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

**IssuanceTransformRules.txt contiene:** 

    @RuleName = "ActiveDirectoryUserSID" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value); 
    
    @RuleName = "ActiveDirectoryUPN" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

**Eseguire i comandi seguenti:** 

    [string]$IssuanceAuthorizationRules=Get-Content -Path C:\IssuanceAuthorizationRules.txt
    
    [string]$IssuanceTransformRules=Get-Content -Path c:\IssuanceTransformRules.txt
    
    Add-ADFSRelyingPartyTrust -Name "Outlook Web App" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/owa/" -WSFedEndpoint https://mail.contoso.com/owa/ -Identifier https://mail.contoso.com/owa/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules
    
    Add-ADFSRelyingPartyTrust -Name "Exchange Admin Center (EAC)" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/ecp/" -WSFedEndpoint https://mail.contoso.com/ecp/ -Identifier https://mail.contoso.com/ecp/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules

## Passaggio 4: installare il servizio ruolo di Proxy dell'applicazione Web (facoltativo)


> [!NOTE]
> Passaggio 4, il passaggio 5 e 6 passaggio sono per gli utenti desiderano pubblicare Exchange OWA ed ECP tramite Proxy dell'applicazione Web e che desiderano avere Proxy dell'applicazione Web di eseguire l'autenticazione ADFS. Pubblicazione di Exchange con Proxy dell'applicazione Web non sono necessarie, pertanto è possibile procedere al passaggio 7 Se non si utilizzano Proxy dell'applicazione Web e si desidera che Exchange per eseguire l'autenticazione ADFS stesso.



Proxy applicazione Web è un nuovo servizio ruolo Accesso remoto Windows Server 2012 R2. Proxy applicazione Web offre funzionalità di proxy inverso per le applicazioni web all'interno della rete aziendale consentire agli utenti in diversi dispositivi per accedervi dall'esterno della rete aziendale. Proxy applicazione Web Preautentica accesso alle applicazioni web mediante Active Directory Federation Services (ADFS) e funge inoltre da un proxy di AD FS. Sebbene Proxy dell'applicazione Web non è obbligatorio, è consigliabile quando ADFS è possibile accedere ai client esterni. Accesso non in linea in Outlook Web App, tuttavia, non è supportata quando si utilizza l'autenticazione ADFS tramite Proxy dell'applicazione Web. È possibile trovare ulteriori informazioni sull'integrazione con Proxy dell'applicazione Web visualizzando [installazione e configurazione di Proxy dell'applicazione Web per pubblicare applicazioni interne](https://go.microsoft.com/fwlink/?linkid=392705)


> [!WARNING]
> Non è possibile installare Proxy di applicazione Web nello stesso server con ADFS installati.



Per distribuire Proxy di applicazioni Web, è necessario installare il ruolo server Accesso remoto con il servizio ruolo Proxy di applicazioni Web su un server che agirà come server Proxy di applicazioni Web. Per installare il servizio ruolo di Proxy di applicazione Web:

1.  Nel server Proxy applicazione Web, in **Server Manager**, fare clic su **Gestione**, quindi scegliere **Aggiungi ruoli e funzionalità**.

2.  Nella procedura guidata Aggiungi ruoli e funzionalità, fare clic su **Avanti** per tre volte per ottenere la pagina **Ruoli server**.

3.  Nella pagina **Ruoli server**, selezionare **Accesso remoto** nell'elenco, e fare clic su **Avanti**.

4.  Nella pagina **Funzionalità**, fare clic su **Avanti**.

5.  Nella pagina **Accesso remoto**, leggere le informazioni e fare clic su **Avanti**.

6.  Nella pagina **Servizi ruolo**, selezionare **Proxy applicazione Web**. Quindi nella finestra **Procedura guidata Aggiungi ruoli e funzionalità**, fare clic su **Aggiungi funzionalità**, quindi fare clic su **Avanti**.

7.  Nella finestra **Conferma**, fare clic su **Installa**. È anche possibile verificare **Se richiesto, riavviare automaticamente il server di destinazione**.

8.  Nella finestra di dialogo **Avanzamento installazione**, verificare che l'installazione è stata eseguita correttamente, quindi fare clic su **Chiudi**.

Il seguente cmdlet Windows PowerShell svolge la stessa funzione dei passaggi precedenti.

```powershell
Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools
```

## Passaggio 5: consente di configurare il servizio ruolo di Proxy dell'applicazione Web (facoltativo)

È necessario configurare il Proxy applicazione Web per connettersi al server ADFS. Ripetere la procedura per tutti i server che si desidera distribuire come server Proxy applicazione Web.

Per configurare il servizio ruolo dell'applicazione Web:

1.  Nel server Proxy applicazione Web, in **Server Manager**, fare clic su **Strumenti**, quindi scegliere **Gestione accesso remoto**.

2.  Nella pagina **Configurazione**, fare clic su **Proxy applicazione Web**.

3.  Nella console **Gestione accesso remoto**, nel riquadro centrale, fare clic **Esegui la procedura guidata di configurazione del Proxy applicazione Web**.

4.  Nella procedura guidata di configurazione del Proxy applicazione Web, nella finestra di dialogo **iniziale**, fare clic su **Avanti**.

5.  Nella pagina **Server federativo**, eseguire le operazioni seguenti e fare clic su **Avanti**:
    
      - Nella casella **Nome del Servizio federativo**, immettere il nome di dominio completo (FQDN) del server ADFS, ad esempio, **adfs.contoso.com**.
    
      - Nelle caselle **Nome utente** e **Password**, digitare le credenziali di un account amministratore locale su server ADFS.

6.  Nella finestra di dialogo **Certificato Proxy ADFS**, nell'elenco dei certificati attualmente installati sul server Proxy applicazione Web, selezionare il certificato che deve utilizzare il Proxy applicazione Web per la funzionalità proxy ADFS e fare clic su **Avanti**. Il certificato scelto dovrebbe essere quello il cui oggetto corrisponde al nome Servizio federativo, ad esempio, **adfs.contoso.com**.

7.  Nella finestra di dialogo **Conferma**, rivedere le impostazioni. Se richiesto, è possibile copiare il cmdlet PowerShell Windows per le installazioni automatiche aggiuntive. Fare clic su **Configura**.

8.  Nella finestra di dialogo **Risultati**, verificare che la configurazione è stata eseguita correttamente, quindi fare clic su **Chiudi**.

Il seguente cmdlet Windows PowerShell svolge la stessa funzione dei passaggi precedenti.

    Install-WebApplicationProxy -CertificateThumprint 1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b -FederationServiceName adfs.contoso.com

## Passaggio 6 – pubblicazione Outlook Web App ed EAC utilizzando Proxy applicazione Web (facoltativo)

Nel passaggio 3, è stato creato l'inoltro di trust di terze parti per Outlook Web App ed EAC basata sulle attestazioni e a questo punto è necessario pubblicare entrambe le applicazioni. Ma prima che in caso contrario, verificare che sia stata creata una relazione di trust relying party per tali e verificare di disporre di un certificato nel server Proxy dell'applicazione Web che è idonea per Outlook Web App ed EAC. Per tutti gli endpoint AD FS che devono essere pubblicati da Proxy dell'applicazione Web, nella console di gestione ADFS, è necessario impostare l'endpoint per essere **Abilitato per i Proxy**.

Attenersi alla seguente procedura per la pubblicazione di Outlook Web App utilizzando il Proxy applicazione Web. Per EAC, è necessario ripetere questi passaggi. Quando si pubblica EAC, è necessario modificare il nome, l'URL esterno, il certificato esterno e l'URL back-end.

Per pubblicare Outlook Web App ed EAC utilizzando Proxy applicazione Web:

1.  Sul server Proxy applicazione Web, nella console **Gestione accesso remoto**, nel riquadro **Navigazione**, fare clic su **Proxy applicazione Web** e poi nel riquadro **Attività**, fare clic su **Pubblica**.

2.  Durante la procedura guidata Pubblicazione nuova applicazione, nella pagina **iniziale**, fare clic su **Avanti**.

3.  Nella pagina **Autenticazione preliminare**, fare clic su **Active Directory Federation Services (ADFS)**, quindi fare clic su **Avanti**.

4.  Nella pagina **Relying Party**, nell'elenco relying party, selezionare il relying party per l'applicazione che si desidera pubblicare, quindi fare clic su **Avanti**.

5.  Nella pagina **Impostazioni di pubblicazione**, eseguire le operazioni seguenti e fare clic su **Avanti**:
    
    1.  Nella casella **Nome**, immettere un nome descrittivo per l'applicazione. Tale nome viene utilizzato solo nell'elenco delle applicazioni pubblicate nella **Console di gestione accesso remoto**. È possibile utilizzare **OWA** e **EAC** per i nomi.
    
    2.  Nella casella **URL esterno** immettere l'URL esterno per l'applicazione, ad esempio <strong>https://external.contoso.com/owa/</strong>Outlook Web App e **https://external.contoso.com/ecp/** per EAC.
    
    3.  Nell'elenco **Certificato esterno**, selezionare il certificato il cui oggetto coincide con il nome host dell'URL esterno.
    
    4.  Nella casella **URL del server di back-end**, immettere l'URL del server back-end. Si noti che questo valore viene inserito automaticamente quando si immettere l'URL esterno ed è necessario modificare solo se l'URL del server di back-end è diverso, ad esempio <strong>https://mail.contoso.com/owa/</strong>Outlook Web App e **https://mail.contoso.com/ecp/** per EAC.
    

    > [!NOTE]
    > Il Proxy applicazione Web può convertire i nomi host negli URL, ma non può convertire i percorsi. Pertanto, è possibile immettere nomi host diversi, ma è necessario immettere lo stesso percorso. Ad esempio, è possibile immettere un URL esterno di <EM>https://external.contoso.com/app1/</EM> e un URL del server back-end di <EM>https://mail.contoso.com/app1/</EM>. Tuttavia, non è possibile immettere un URL esterno di <EM>https://external.contoso.com/app1/</EM> e un URL del server back-end di <EM>https://mail.contoso.com/internal-app1/</EM>.



6.  Nella pagina **Conferma**, esaminare le impostazioni di backup e fare clic su **Pubblica**. È possibile copiare il comando PowerShell Windows per impostare applicazioni pubblicate aggiuntive.

7.  Nella pagina **Risultati**, assicurarsi che l'applicazione sia stata pubblicata correttamente, quindi fare clic su **Chiudi**.

Il seguente cmdlet PowerShell Windows esegue le stesse attività della procedura precedente per Outlook Web App.

    Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/owa/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/owa/' -Name 'OWA' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Outlook Web App'

Il seguente cmdlet PowerShell Windows esegue le stesse attività della procedura precedente per EAC.

    Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/ecp/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/ecp/' -Name 'EAC' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Exchange Admin Center'

Dopo aver completato questi passaggi, Proxy applicazione Web eseguire l'autenticazione ADFS per i client Outlook Web App ed EAC e, verrà inoltre proxy le connessioni a Exchange per loro conto. Non è necessario configurare Exchange direttamente per l'autenticazione ADFS, in modo che procedere al passaggio 10 per testare la configurazione.

## Passaggio 7 – Configura Exchange 2013 per utilizzare l'autenticazione ADFS

Quando si configura ADFS in modo che sia utilizzabile per l'autenticazione basata sulle attestazioni con Outlook Web App e EAC in Exchange 2013, è necessario abilitare ADFS per l'organizzazione Exchange. È necessario utilizzare il cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\)) per configurare le impostazioni di ADFS per l'organizzazione:

  - Impostare l'autorità emittente di ADFS per **https://adfs.contoso.com/adfs/ls/**.

  - Impostare gli URI di ADFS per **https://mail.contoso.com/owa/** e **https://mail.contoso.com/ecp/**.

  - Individuare il token ADFS identificazione personale del certificato di firma utilizzando Windows PowerShell nel server ADFS e immissione `Get-ADFSCertificate -CertificateType "Token-signing"`. Assegnare la firma di token identificazione personale del certificato trovato. Se il certificato di firma di token ADFS è scaduto, è necessario aggiornare l'identificazione personale del certificato di firma di token ADFS nuovo utilizzando il cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\)) .

Eseguire i seguenti comandi in Exchange Management Shell.

    $uris = @(" https://mail.contoso.com/owa/","https://mail.contoso.com/ecp/")
    Set-OrganizationConfig -AdfsIssuer "https://adfs.contoso.com/adfs/ls/" -AdfsAudienceUris $uris -AdfsSignCertificateThumbprint "88970C64278A15D642934DC2961D9CCA5E28DA6B"


> [!NOTE]
> Il parametro <EM>-AdfsEncryptCertificateThumbprint</EM> non è supportato per questi scenari.



Per informazioni dettagliate e sintassi, vedere [Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\)) e [Get-ADFSCertificate](https://go.microsoft.com/fwlink/?linkid=392706).

## Passaggio 8 – abilitare l'autenticazione ADFS sulle directory virtuale OWA ed ECP

Per le directory virtuali di OWA ed ECP, abilitare l'autenticazione ADFS come unico metodo di autenticazione e disabilitare tutti gli altri moduli di autenticazione.


> [!WARNING]
> Prima di configurare la directory virtuale di OWA, è necessario configurare la directory virtuale ECP.



Configurare la directory virtuale ECP utilizzando Exchange Management Shell. Nella finestra della Shell, eseguire il comando seguente.

    Get-EcpVirtualDirectory | Set-EcpVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false

Configurare la directory virtuale OWA utilizzando Exchange Management Shell. Nella finestra della Shell, eseguire il comando seguente.

    Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false -OAuthAuthentication $false


> [!NOTE]
> I comandi riportati in Exchange Management Shell configurare le directory virtuali di OWA ed ECP in ogni server Accesso Client nell'organizzazione. Se non si desidera applicare queste impostazioni a tutti i server Accesso Client, utilizzare il parametro <EM>-Identity</EM> e specificare il server Accesso Client. È probabile che è possibile applicare queste impostazioni solo ai server Accesso Client nell'organizzazione sono Internet facing.



Per dettagli e sintassi, vedere [Get-OwaVirtualDirectory](https://technet.microsoft.com/it-it/library/aa998588\(v=exchg.150\)) e [Set-OwaVirtualDirectory](https://technet.microsoft.com/it-it/library/bb123515\(v=exchg.150\)) o [Get-EcpVirtualDirectory](https://technet.microsoft.com/it-it/library/dd351058\(v=exchg.150\)) e [Set-EcpVirtualDirectory](https://technet.microsoft.com/it-it/library/dd297991\(v=exchg.150\)).

## Passaggio 9 – riavvio o riciclo di Internet Information Services (IIS)

Dopo aver completato tutti i passaggi richiesti, tra cui le modifiche alle directory virtuali di Exchange, è necessario riavviare Internet Information Services. A tale scopo, è possibile utilizzare uno dei seguenti metodi:

  - Utilizzo di Windows PowerShell:
    
    ```powershell
Restart-Service W3SVC,WAS -noforce
```

  - Utilizzo di una riga di comando: Fare clic su **Start**, **Esegui**, digitare `IISReset /noforce`, quindi fare clic su **OK**.

  - Utilizzo di Gestione Internet Information Servers (IIS): In **Server Manager** \> **IIS**, fare clic su **Strumenti**, quindi fare clic su **Gestione Internet Information Services (IIS)**. Nella finestra **Gestione Internet Information Servers (IIS)**, nel riquadro azioni in **Gestione server**, fare clic su **Riavvia**.

## Passaggio 10 - verificare le attestazioni ADFS per Outlook Web App ed EAC

Per testare le attestazioni ADFS per Outlook Web App:

  - Nel web browser, accedere a Outlook Web App, ad esempio, **https://mail.contoso.com/owa**

  - Nella finestra del browser, se viene visualizzato un errore relativo ai certificati, continuare semplicemente nel sito Web di Outlook Web App. Deve essere reindirizzato per ADFS la pagina di accesso o la ADFS richiedere le credenziali.

  - Digitare nome utente (dominio\\utente) e password, quindi fare clic su **Accedi**.

Outlook Web App verrà caricato nella finestra.

Per eseguire il test delle attestazioni per EAC:

1.  Nel browser Web, accedere a **https://mail.contoso.com/ecp**.

2.  Nella finestra del browser, se viene visualizzato un errore relativo ai certificati, continuare semplicemente nel sito Web ECP. Deve essere reindirizzato per ADFS la pagina di accesso o la ADFS richiedere le credenziali.

3.  Digitare nome utente (dominio\\utente) e password, quindi fare clic su **Accedi**.

4.  ECP dovrebbe essere caricato nella finestra.

## Ulteriori informazioni che potrebbero risultare utili

**Autenticazione a più fattori**

Per distribuzioni Exchange 2013 SP1 in locale, distribuire e configurare Active Directory Federation Services (ADFS) 2.0 utilizzando le attestazioni indica che Outlook Web App e EAC in Exchange 2013 SP1 possono supportare i metodi di autenticazione a più fattori, come l'autenticazione basata sui certificati, token di autenticazione e sicurezza e l'autenticazione con impronta digitale. L'autenticazione a due fattori viene spesso confusa con altre forme di autenticazione. L'autenticazione a più fattori richiede l'utilizzo di due dei tre fattori di autenticazione. Tali fattori sono:

  - Un elemento che solo l'utente conosce (ad esempio, password, PIN o modello)

  - Un elemento disponibile solo per l'utente (ad esempio, scheda ATM, token di sicurezza, smart card o telefono cellulare)

  - Un elemento personale dell'utente (ad esempio, caratteristica biometrica come un'impronta digitale)

Per ulteriori informazioni sull'autenticazione a più fattori in Windows Server 2012 R2, vedere [Overview: gestione dei rischi con autenticazione a più fattori aggiuntivi per le applicazioni sensibili](https://go.microsoft.com/fwlink/?linkid=392707) e [Guida procedura dettagliata: gestione dei rischi con Autenticazione a più fattori aggiuntivi per le applicazioni sensibili](https://go.microsoft.com/fwlink/?linkid=392708).

In Windows Server 2012 servizio ruolo ADFS R2, il servizio federativo funge da un servizio token di sicurezza, sono disponibili i token di sicurezza che vengono utilizzati con basata sulle attestazioni e offre la possibilità per supportare l'autenticazione a più fattori. Il servizio federativo rilascia token in base alle credenziali che sono disponibili. Dopo che l'archivio account consente di verificare le credenziali dell'utente, basata sulle attestazioni per l'utente viene generati in base alle regole dei criteri di protezione e quindi aggiunto a un token di sicurezza che deve essere stato emesso il client. Per ulteriori informazioni sulle attestazioni, vedere [Informazioni sulle attestazioni](https://go.microsoft.com/fwlink/?linkid=392709).

**Coesistenza con altre versioni di Exchange**

È possibile utilizzare l'autenticazione ADFS per Outlook Web App ed EAC quando si dispone di più versioni di Exchange distribuiti nell'organizzazione. In questo scenario è supportato solo per le distribuzioni di Exchange 2010 ed Exchange 2013 e solo se tutti i client si connettono tramite Exchange 2013 server **e** i server Exchange 2013 sono stati configurati per l'autenticazione ADFS.

Gli utenti con una cassetta postale su un Server di Exchange 2010 possono accedere alle cassette postali tramite un server di Exchange 2013 configurato per l'autenticazione ADFS. La connessione client iniziale del server Exchange 2013 utilizza l'autenticazione ADFS. La connessione al server Exchange 2010 elaborata, tuttavia, utilizzeranno Kerberos. Non è supportato per configurare Exchange Server 2010 per indirizzare l'autenticazione ADFS.


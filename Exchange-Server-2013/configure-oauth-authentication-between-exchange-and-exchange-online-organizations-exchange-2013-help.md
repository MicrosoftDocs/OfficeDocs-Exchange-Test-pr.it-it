---
title: "Configurazione dell'autenticazione OAuth tra organizzazioni di Exchange ed Exchange Online: Exchange 2013 Help"
TOCTitle: Configurazione dell'autenticazione OAuth tra organizzazioni di Exchange ed Exchange Online
ms:assetid: f703e153-98e2-4268-8a6e-07a86b0a1d22
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn594521(v=EXCHG.150)
ms:contentKeyID: 61170787
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione dell'autenticazione OAuth tra organizzazioni di Exchange ed Exchange Online

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Quando si utilizza la procedura guidata di configurazione ibrida le distribuzioni ibride esclusive per Exchange 2013 configurano l'autenticazione OAuth. Per le distribuzioni ibride miste Exchange 2013/2010 ed Exchange 2013/2007, la nuova connessione di autenticazione basata su OAuth della distribuzione ibrida tra le organizzazioni Office 365 ed Exchange locali non viene configurata dalla procedura guidata di configurazione ibrida. Tali distribuzioni continuano a utilizzare il processo di trust federativo per impostazione predefinita. Tuttavia, determinate funzionalità di Exchange 2013 sono completamente disponibili all'interno dell'organizzazione solo utilizzando il nuovo protocollo di autenticazione OAuth di Exchange.

Il nuovo processo di autenticazione OAuth di Exchange attualmente abilita le seguenti funzionalità di Exchange:

  - Message Rights Management (MRM)

  - eDiscovery in locale di Exchange

  - Archiviazione in locale di Exchange

Si consiglia a tutte le organizzazioni con Exchange che implementano una distribuzione ibrida con Exchange 2013 ed Exchange Online di configurare l'autenticazione OAuth di Exchange dopo aver configurato la distribuzione ibrida tramite la procedura guidata dedicata.


> [!IMPORTANT]
> Se l'organizzazione locale è in esecuzione solo i server Exchange 2013 con aggiornamento cumulativo 5 o versioni successive, eseguire la distribuzione guidata ibrida anziché eseguire i passaggi descritti in questo argomento.<BR>Questa funzionalità di Exchange Server 2013 non è completamente compatibile con Office 365 utilizzato da 21Vianet in Cina e potrebbe essere soggetta a limitazioni. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/?linkid=313640">Informazioni su Office 365 utilizzato da 21Vianet</A>.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni calendario e condivisione" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Configurazione della distribuzione ibrida tramite la distribuzione ibrida guidata completata. Per ulteriori informazioni, vedere [Distribuzioni ibride di Exchange Server](https://technet.microsoft.com/it-it/library/jj200581\(v=exchg.150\)).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come si configura l'autenticazione OAuth tra l'organizzazione Exchange locale e quella Exchange Online?

## Passaggio 1: creare un oggetto server di autorizzazione per l'organizzazione di Exchange Online

Per eseguire questa procedura, è necessario specificare un dominio verificato per la propria organizzazione di Exchange Online. Tale dominio deve essere lo stesso che viene utilizzato come dominio SMTP primario negli account di posta elettronica basati sul cloud. Tale dominio viene identificato come *\<dominio verificato\>* nella seguente procedura.

Eseguire il comando riportato di seguito in Exchange Management Shell (Exchange PowerShell) nell'organizzazione di Exchange locale.

    New-AuthServer -Name "WindowsAzureACS" -AuthMetadataUrl https://accounts.accesscontrol.windows.net/<your verified domain>/metadata/json/1

## Passaggio 2: abilitare l'applicazione partner per l'organizzazione di Exchange Online

Eseguire il comando seguente in Exchange PowerShell nella propria organizzazione Exchange locale.

    Get-PartnerApplication |  ?{$_.ApplicationIdentifier -eq "00000002-0000-0ff1-ce00-000000000000" -and $_.Realm -eq ""} | Set-PartnerApplication -Enabled $true

## Passaggio 3: esportare il certificato di autorizzazione in locale

In questo passaggio, è necessario eseguire uno script di PowerShell al fine di esportare il certificato di autorizzazione in locale, il quale verrà importato nell'organizzazione di Exchange Online durante il passaggio successivo.

1.  Salvare il testo seguente in un file di script di PowerShell denominato, ad esempio, **ExportAuthCert.ps1**.
    
        $thumbprint = (Get-AuthConfig).CurrentCertificateThumbprint
         
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
         
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.Thumbprint -match $thumbprint}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)

2.  In Exchange PowerShell della propria organizzazione Exchange locale, eseguire lo script di PowerShell che è stato creato al passaggio precedente. Ad esempio:
    
        .\ExportAuthCert.ps1

## Passaggio 4: Caricare il certificato di autorizzazione in locale in Azure Active Directory ACS

Successivamente, è necessario utilizzare Windows PowerShell per caricare il certificato di autorizzazione in locale esportato nel passaggio precedente per Servizi di controllo per l'accesso ad Azure Active Directory (ACS). A tale scopo, i cmdlet Azure Active Directory Module per Windows PowerShell deve essere installato. Se non è installato, vedere <https://aka.ms/aadposh> per installare Azure Active Directory Module per Windows PowerShell. Eseguire le operazioni seguenti dopo l'installazione di Azure Active Directory Module per Windows PowerShell.

1.  Fare clic sul collegamento di **Azure Active Directory Module per Windows PowerShell** per aprire un'area di lavoro di Windows PowerShell con i cmdlet Azure AD installati. Tutti i comandi in questo passaggio è eseguito utilizzando Windows PowerShell per Azure Active Directory console.

2.  Salvare il testo seguente in un file di script di PowerShell denominato, ad esempio, **UploadAuthCert.ps1**.
    
        Connect-MsolService;
        Import-Module msonlineextended;
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        $objFSO = New-Object -ComObject Scripting.FileSystemObject;
        $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
        $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
        $cer.Import($CertFile);
        $binCert = $cer.GetRawCertData();
        $credValue = [System.Convert]::ToBase64String($binCert);
        
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
        New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue

3.  Eseguire lo script di PowerShell creato nel passaggio precedente. Ad esempio:
    
        .\UploadAuthCert.ps1

4.  Dopo avere avviato lo script, viene visualizzata una finestra di dialogo delle credenziali. Immettere le credenziali per l'account di amministratore tenant dell'organizzazione Azure AD Microsoft Online. Dopo aver eseguito lo script, lasciare Windows PowerShell per sessione Azure AD aperto. Si utilizzerà per eseguire uno script di PowerShell nel passaggio successivo.

## Passaggio 5: Registrare tutte le autorità nome host per gli endpoint HTTP Exchange locali ed esterni con Azure Active Directory

È necessario eseguire lo script di questo passaggio per ogni endpoint dell'organizzazione locale di Exchange alla quale è possibile accedere pubblicamente. Si consiglia di usare caratteri jolly, se possibile. Ad esempio, si presuma che Exchange sia disponibile dall'esterno su **https://mail.contoso.com/ews/exchange.asmx**. In questo caso, è possibile utilizzare un unico carattere jolly: **\*.contoso.com**. In questo modo vengono inclusi gli endpoint autodiscover.contoso.com e mail.contoso.com. Tuttavia, non viene incluso il dominio di livello superiore, **contoso.com**. Nei casi in cui sia possibile accedere dall'esterno ai server Accesso client di Exchange 2013 con l'autorità nome host, quest'ultima deve essere registrata come **contoso.com**. Non è presente un limite relativo alla registrazione di ulteriori autorità nome host esterne.

Se non si è certi degli endpoint di Exchange esterni della propria organizzazione, è possibile visualizzare un elenco degli endpoint dei servizi Web configurati in esterno eseguendo il comando seguente in Exchange PowerShell nella propria organizzazione locale di Exchange:

    Get-WebServicesVirtualDirectory | FL ExternalUrl


> [!NOTE]
> Correttamente esegue le operazioni seguenti script è necessario che Windows PowerShell per Azure Active Directory sia connesso al tenant Azure AD di Microsoft Online, come descritto nel passaggio 4 della sezione precedente.



1.  Salvare il testo seguente in un file di script di PowerShell denominato, ad esempio, **RegisterEndpoints.ps1**. In questo esempio viene utilizzato un carattere jolly per registrare tutti gli endpoint per contoso.com. Sostituire **contoso.com** con un'autorità nome host per la tua organizzazione di Exchange locale.
    
        $externalAuthority="*.contoso.com"
         
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
         
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName;
         
        $spn = [string]::Format("{0}/{1}", $ServiceName, $externalAuthority);
        $p.ServicePrincipalNames.Add($spn);
         
        Set-MsolServicePrincipal -ObjectID $p.ObjectId -ServicePrincipalNames $p.ServicePrincipalNames;

2.  In Windows PowerShell per Azure Active Directory, eseguire lo script di Windows PowerShell che è stato creato nel passaggio precedente. Per esempio:
    
        .\RegisterEndpoints.ps1

## Passaggio 6: creare un connettore IntraOrganizationConnector tra la propria organizzazione locale e Office 365

È necessario definire un indirizzo di destinazione per le cassette postali ospitate in Exchange Online. Tale indirizzo di destinazione viene creato automaticamente quando viene creato il tenant di Office 365. Ad esempio, se il dominio dell'organizzazione ospitato nel tenant di Office 365 corrisponde a "contoso.com", l'indirizzo del servizio di destinazione sarà "contoso.mail.onmicrosoft.com".

Utilizzando Exchange PowerShell, eseguire il seguente cmdlet nell'organizzazione locale:

    New-IntraOrganizationConnector -name ExchangeHybridOnPremisesToOnline -DiscoveryEndpoint https://outlook.office365.com/autodiscover/autodiscover.svc -TargetAddressDomains <your service target address>

## Passaggio 7: creare un connettore IntraOrganizationConnector tra il tenant Office 365 e l'organizzazione di Exchange locale

È necessario definire un indirizzo di destinazione per le cassette postali ospitate nell'organizzazione locale. Se l'indirizzo SMTP principale dell'organizzazione corrisponde a "contoso.com" sarà "contoso.com".

Inoltre, è necessario definire l'endpoint di individuazione automatica esterno della propria organizzazione locale. Se la società corrisponde a "contoso.com", solitamente avrà uno degli aspetti seguenti:

  - https://autodiscover.\<dominio SMTP principale\>/autodiscover/autodiscover.svc

  - https://\<dominio SMTP principale\>/autodiscover/autodiscover.svc


> [!NOTE]
> È possibile utilizzare il cmdlet <A href="https://technet.microsoft.com/it-it/library/dn551183(v=exchg.150)">Get-IntraOrganizationConfiguration</A> nei tenant locali e di Office 365 per determinare i valori di endpoint necessari al cmdlet <A href="https://technet.microsoft.com/it-it/library/dn551178(v=exchg.150)">New-IntraOrganizationConnector</A>.



Utilizzando Windows PowerShell eseguire il cmdlet indicato di seguito:

    $UserCredential = Get-Credential
    
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    
    Import-PSSession $Session
    
    New-IntraOrganizationConnector -name ExchangeHybridOnlineToOnPremises -DiscoveryEndpoint <your on-premises Autodiscover endpoint> -TargetAddressDomains <your on-premises SMTP domain>

## Passaggio 8: Configurare uno AvailabilityAddressSpace per uno dei server precedenti a Exchange 2013 SP1

Quando si configura una distribuzione ibrida in un'organizzazione precedente a Exchange 2013, è necessario installare almeno un server Exchange 2013 SP1 o versione successiva con i ruoli server Accesso client e Cassette postali nell'organizzazione Exchange esistente. I server Accesso client e Cassette postali Exchange 2013 funzionano da server frontend e coordinano le comunicazioni tra l'organizzazione locale esistente Exchange e l'organizzazione Exchange Online. Queste comunicazioni comprendono le funzionalità di trasporto dei messaggi e messaggistica tra le organizzazioni locali e le organizzazioni Exchange Online. È consigliabile installare più server Exchange 2013 nell'organizzazione locale per aumentare l'affidabilità e la disponibilità delle funzioni di distribuzione ibrida.

In una distribuzione mista, con Exchange 2013/2010 o Exchange 2013/2007, è consigliabile che tutti i server frontend connessi a Internet dell'organizzazione locale siano server Accesso client con Exchange 2013 SP1 o versione successiva. Tutte le richieste di Servizi Web di Exchange (EWS) provenienti da Office 365 ed Exchange Online devono connettersi ai server Accesso client Exchange 2013 nella distribuzione locale. Inoltre, tutte le richieste EWS provenienti dalle organizzazioni Exchange locali per Exchange Online devono essere trasmesse tramite proxy a un server Accesso client con Exchange 2013 SP1 o versione successiva. Poiché questi server Accesso client Exchange 2013 devono gestire queste richieste EWS aggiuntive in ingresso e in uscita, è importante disporre di un numero di server Accesso client Exchange 2013 sufficiente a gestire il carico di elaborazione e a fornire ridondanza di connessione. Il numero di server Accesso client necessari dipende dalla quantità media di richiesta EWS e varia in base all'organizzazione.

Prima di completare il passaggio seguente, verificare quanto segue:

  - I server frontend ibridi sono Exchange 2013 SP1 o versione successiva

  - Si dispone di un URL EWS esterno univoco per i server Exchange 2013. Il tenant di Office 365 deve essere connesso a questi server affinché le richieste basate su cloud per le funzionalità ibride funzionino correttamente.

  - I server dispongono sia del ruolo Cassetta postale che del ruolo Accesso client

  - Eventuali server Cassetta postale e Accesso client Exchange 2010/2007 dispongono dell'aggiornamento cumulativo o del Service Pack.
    

    > [!NOTE]
    > I server Cassetta postale Exchange 2010/2007 possono continuare a utilizzare i server Accesso client Exchange per i server frontend per le connessioni alle funzionalità non ibrida2010/2007 Client Access servers for frontend servers for non-hybrid feature connections. Solo le richieste di funzionalità di distribuzione ibrida dal tenant Office 365 devono connettersi ai server Exchange 2013.



È necessario configurare un parametro *AvailabilityAddressSpace* sui server Accesso client precedenti a Exchange 2013 che punti all'endpoint Servizi Web Exchange dei server Accesso client locali di Exchange 2013 SP1. Questo endpoint è lo stesso precedentemente delineato nel Passaggio 5 oppure può essere determinato eseguendo il seguente cmdlet sul server locale Accesso client di Exchange 2013 SP1.

    Get-WebServicesVirtualDirectory | FL AdminDisplayVersion,ExternalUrl


> [!NOTE]
> Se le informazioni di directory virtuale vengono restituite da più server, assicurarsi di utilizzare l'endpoint restituito per un server Accesso client di Exchange 2013 SP1. Verrà visualizzata la versione 15.0 (Build 847.32) o superiore per il parametro <EM>AdminDisplayVersion</EM>.



Per configurare *AvailabilityAddressSpace*, utilizzare Exchange PowerShell e lanciare il seguente cmdlet nell'organizzazione locale:

    Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl <your on-premises External Web Services URL> -ForestName <your Office 365 service target address> -UseServiceAccount $True

## Come verificare se l'operazione ha avuto esito positivo

È possibile verificare che la configurazione OAuth sia corretta utilizzando il cmdlet [Test-OAuthConnectivity](https://technet.microsoft.com/it-it/library/jj218623\(v=exchg.150\)). Il cmdlet consente di verificare se gli endpoint di Exchange in locale ed Exchange Online riescano ad autenticare le richieste reciproche.


> [!IMPORTANT]
> Quando si stabilisce una connessione con l'organizzazione di Exchange Online utilizzando Remote PowerShell, potrebbe essere necessario utilizzare il parametro <EM>AllowClobber</EM> con il cmdlet <STRONG>Import-PSSession</STRONG> al fine di importare i comandi più recenti all'interno della sessione PowerShell locale.



Per verificare se la propria organizzazione Exchange può connettersi a Exchange Online ed eseguire il comando seguente in Exchange PowerShell della propria organizzazione locale:

    Test-OAuthConnectivity -Service EWS -TargetUri https://outlook.office365.com/ews/exchange.asmx -Mailbox <On-Premises Mailbox> -Verbose | fl

Per verificare se la propria organizzazione di Exchange Online può connettersi a quella di Exchange locale, utilizzare [Remote PowerShell](https://technet.microsoft.com/it-it/library/jj984289\(v=exchg.150\)) per connettersi all'organizzazione di Exchange Online ed eseguire il comando riportato di seguito:

    Test-OAuthConnectivity -Service EWS -TargetUri <external hostname authority of your Exchange On-Premises deployment>/metadata/json/1 -Mailbox <Exchange Online Mailbox> -Verbose | fl

In tal caso, ad esempio, Test-OAuthConnectivity-servizio EWS - TargetUri https://lync.contoso.com/metadata/json/1-ExchangeOnlineBox1 delle cassette postali-Verbose | fl


> [!IMPORTANT]
> È possibile ignorare l'errore "Nessuna cassetta postale associata per l'indirizzo SMTP". È importante che il parametro <EM>ResultTask</EM> restituisca un valore corrispondente a <STRONG>Riuscito</STRONG>. Ad esempio, l'ultima sezione del risultato del test dovrà essere:<BR><CODE>ResultType: Success</CODE><BR><CODE>Identity: Microsoft.Exchange.Security.OAuth.ValidationResultNodeId</CODE><BR><CODE>IsValid: True</CODE><BR><CODE>ObjectState: New</CODE>




> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



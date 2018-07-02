---
title: "Configurazione delle notifiche push che eseguono l'inoltro di OWA per i dispositivi: Exchange 2013 Help"
TOCTitle: Configurazione delle notifiche push che eseguono l'inoltro di OWA per i dispositivi
ms:assetid: c0f4912d-8bd3-4a54-9097-03619c645c6a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn511017(v=EXCHG.150)
ms:contentKeyID: 59954037
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione delle notifiche push che eseguono l'inoltro di OWA per i dispositivi

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Abilitazione delle notifiche push di OWA per i dispositivi (OWA per iPhone e OWA per iPad) per una distribuzione locale di Microsoft Exchange 2013 consente agli utenti di ricevere aggiornamenti sull'icona di Outlook Web App o su OWA per iPhone/iPad, i quali indicano il numero di messaggi non letti presenti nella cartella Posta in arrivo. Se le notifiche push non sono configurate e abilitate, un utente con OWA per i dispositivi non può sapere in alcun modo quanti messaggi non letti sono presenti nella cartella Posta in arrivo, senza avviare l'app. Quando è disponibile un nuovo messaggio, il badge di OWA per i dispositivi viene aggiornato sul dispositivo dell'utente e avrà il seguente aspetto.

![Badge di OWA per dispositivi](images/Dn511017.f399ba74-5395-4d24-ae7d-d16bf0ac7b35(EXCHG.150).png "Badge di OWA per dispositivi")

## Come è possibile attivare le notifiche push?

Per abilitare le notifiche push, è necessario che i server locali di Exchange 2013 si connettano al servizio di notifica push di Office 365 al fine di inviare notifiche push a iPhone e iPad. I server locali di Exchange 2013 instradano le notifiche di aggiornamento attraverso i servizi di notifica di Office 365 al fine di eliminare la necessità di registrare gli account degli sviluppatori sui servizi di notifica push di terze parti. Il seguente diagramma illustra il processo relativo alla ricezione di aggiornamenti badge da parte di iPhone e iPad in merito ai messaggi non letti.

![Procedura per notifiche push](images/Dn511017.36764ce6-7351-492f-a17e-c42b781e2781(EXCHG.150).jpg "Procedura per notifiche push")

Per abilitare le notifiche push, l'amministratore deve effettuare le seguenti operazioni:

1.  Registrare l'organizzazione dell'utente in Office 365 per le aziende.

2.  Aggiornare tutti i server locali a Exchange Server 2013 Cumulative Update 3 (CU3) o a una versione successiva.

3.  Configurare Exchange 2013 locale per l'autenticazione di Office 365

4.  Abilitare le notifiche push da Exchange Server 2013 a Office 365 e verificare tali notifiche push funzionino.

## Registrare l'organizzazione dell'utente in Office 365 per le aziende

Office 365 è un servizio basato su cloud studiato per rispondere alle esigenze di sicurezza, affidabilità e produttività delle organizzazioni. Office 365 fa riferimento a piani di sottoscrizione che includono l'accesso alle applicazioni di Office e ad altri servizi per la produttività che vengono attivati tramite Internet (servizi cloud), ad esempio conferenza Web di Lync e la posta elettronica per le aziende ospitata su Exchange Online.

Molti piani di Office 365 includono anche la versione desktop delle applicazioni Office più recenti che possono essere installate su più computer e dispositivi. Tutti i piani di Office 365 vengono pagati in forma di sottoscrizione mensile o annuale. Per ulteriori informazioni o per registrare la tua organizzazione a Office 365, vedere [Che cos'è Office 365 per le aziende?](http://go.microsoft.com/fwlink/?linkid=335705). Per ulteriori informazioni su tutti i servizi offerti tramite Office 365, vedere [Descrizione dei servizi di Office 365](http://go.microsoft.com/fwlink/?linkid=335704).

## Aggiornare a CU3 o versione successiva

Cumulative Update 3 (CU3) per Exchange Server 2013 consente di risolvere problemi rilevati in Exchange Server 2013 dal momento di rilascio del prodotto dalla versione RTM. L'aggiornamento contiene tutti i problemi e le risoluzione di CU1 e CU2 e include ulteriori correzioni e aggiornamenti relativi al periodo successivo al rilascio di CU2. Si consiglia di eseguire questo aggiornamento per tutti i clienti locali di Exchange 2013 ed è necessario per le notifiche push. Per ulteriori informazioni sugli aggiornamenti cumulativi, compreso quello CU3, vedere [Aggiornamenti per Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

## Configurare Exchange 2013 locale per l'autenticazione di Office 365

L'utilizzo di un metodo unico e standard per l'autenticazione tra server rappresenta l'approccio di Exchange Server 2013. [Exchange Server 2013](http://go.microsoft.com/fwlink/?linkid=290946) (nonché [Lync Server 2013](http://go.microsoft.com/fwlink/?linkid=273796) e [SharePoint 2013](http://go.microsoft.com/fwlink/?linkid=335701)) e [Office 2013](http://go.microsoft.com/fwlink/?linkid=335696) supportano il protocollo OAuth (Open Authorization) per l'autorizzazione e l'autenticazione tra server. Con OAuth, un protocollo di autorizzazione standard utilizzato da diversi siti Web importanti, le credenziali e le password dell'utente non vengono trasferite da un computer a un altro. Al contrario, l'autenticazione e l'autorizzazione si basano sui token di sicurezza OAuth. Tali token forniscono accesso a un gruppo specifico di risorse per un periodo di tempo specifico.

Di solito, l'autenticazione OAuth comprende tre componenti: un server di autorizzazione singolo e due aree di autenticazione che devono comunicare fra loro. I token di sicurezza vengono rilasciati dal server di autorizzazione (noto anche come server del token di sicurezza) nelle due aree di autenticazione che devono comunicare. Questi due token verificano che le comunicazioni originate da un'area di autenticazione siano considerate attendibili dall'altra area di autenticazione. Ad esempio, il server di autorizzazione può rilasciare token che verificano se gli utenti di un'area di autenticazione specifica di Lync Server 2013 sono in grado di accedere a un'area di autenticazione di Exchange 2013 specifica e viceversa.


> [!TIP]
> Un'area di autenticazione rappresenta un contenitore di sicurezza.



Tuttavia, per l'autenticazione tra server locali non è necessario utilizzare server di token di terze parti. I prodotti server quali Lync Server 2013 ed Exchange 2013 dispongono di un server di token integrato che può essere utilizzato per eseguire l'autenticazione con altri server Microsoft (ad esempio, SharePoint Server) che supportano l'autenticazione tra server. Ad esempio, Lync Server 2013 può rilasciare e firmare un token di sicurezza in modo autonomo, quindi può utilizzare quel token per comunicare con Exchange 2013. In questo caso, non è necessario un server di token di terze parti.

Al fine di configurare l'autenticazione tra server per un'implementazione locale di Exchange Server 2013 su Office 365, è necessario effettuare due passaggi:

  -  
    **Passaggio 1: assegnare un certificato all'autorità emittente del token incorporato di Exchange Server.** Innanzitutto, un amministratore locale di Exchange deve utilizzare il seguente script di Exchange Management Shell per creare un certificato, se non è stato creato prima, e assegnarlo all'autorità emittente del token incorporato del server locale di Exchange. Si tratta di un processo di un solo passaggio. Dopo la creazione del certificato, quest'ultimo deve essere utilizzato di nuovo per altre situazioni di autenticazione e non deve essere sostituito. Assicurarsi di aggiornare il valore di *$tenantDomain* sul nome del proprio dominio. A tale scopo, copiare e incollare il codice seguente.
    

    > [!WARNING]
    > Se si copia e incolla il codice all'interno di un editor di testo, ad esempio Blocco note, e lo si salva con estensione ps1, l'esecuzione degli script nella shell risulta più facile.

    
        # Make sure to update the following $tenantDomain with your Office 365 tenant domain.
        
        $tenantDomain = "Fabrikam.com"
        
        # Check whether the cert returned from Get-AuthConfig is valid and keysize must be >= 2048
        
        $c = Get-ExchangeCertificate | ?{$_.CertificateDomains -eq $env:USERDNSDOMAIN -and $_.Services -ge "SMTP" -and $_.PublicKeySize -ge 2048 -and $_.FriendlyName -match "OAuth"}
        If ($c.Count -eq 0)
        {
            Write-Host "Creating certificate for oAuth..."
            $ski = [System.Guid]::NewGuid().ToString("N")
            $friendlyName = "Exchange S2S OAuth"
            New-ExchangeCertificate -FriendlyName $friendlyName -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
            $c = Get-ExchangeCertificate | ?{$_.friendlyname -eq $friendlyName}
        }
        ElseIf ($c.Count -gt 1)
        {
            $c = $c[0]
        }
        
        $a = $c | ?{$_.Thumbprint -eq (get-authconfig).CurrentCertificateThumbprint}
        If ($a.Count -eq 0)
        {
            Set-AuthConfig -CertificateThumbprint $c.Thumbprint
        }
        Write-Host "Configured Certificate Thumbprint is:"(get-authconfig).CurrentCertificateThumbprint
        
        # Export the certificate
        
        Write-Host "Exporting certificate..."
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
        
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.FriendlyName -match "OAuth"}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)
        
        # Set AuthServer
        $authServer = Get-AuthServer MicrosoftSts;
        if ($authServer.Length -eq 0)
        {
            Write-Host "Creating AuthServer Config..."
            New-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        elseif ($authServer.AuthMetadataUrl -ne "https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain")
        {
            Write-Warning "AuthServer config already exists but the AuthMetdataUrl doesn't match the appropriate value. Updating..."
            Set-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        else
        {
            Write-Host "AuthServer Config already exists."
        }
        Write-Host "Complete."
    
    Il risultato previsto dovrebbe avere un aspetto analogo al seguente.
    
        Configured Certificate Thumbprint is: 7595DBDEA83DACB5757441D44899BCDB9911253C
        Exporting certificate...
        Complete.
    

    > [!WARNING]
    > Prima di continuare, è necessario disporre dei cmdlet di Azure Active Directory Module per Windows PowerShell. Se i cmdlet di Azure Active Directory Module per Windows PowerShell (in precedenza noto come modulo dei Microsoft Online Services per Windows PowerShell) non sono stati installati, è possibile farlo accedendo a <A href="http://aka.ms/aadposh">Gestione di Azure AD tramite Windows PowerShell</A>.



  -  
    **Passaggio 2: configurare Office 365 affinché comunichi con Exchange 2013 locale.** Configurare il server di Office 365 con cui comunica Exchange Server 2013 affinché sia un'applicazione partner. Ad esempio, se Exchange Server 2013 locale deve comunicare con Office 365, è necessario configurare Exchange locale affinché sia un'applicazione partner. Un'applicazione partner rappresenta qualsiasi applicazione con la quale Exchange 2013 può scambiare token di sicurezza in modo diretto, senza necessità di passare attraverso un server di token di sicurezza di terze parti. Un amministratore di Exchange 2013 locale deve utilizzare il seguente script di Exchange Management Shell per configurare il tenant di Office 365 con il quale comunica Exchange 2013 affinché sia un'applicazione partner. Durante l'esecuzione, verrà visualizzato un prompt per inserire il nome utente e la password dell'amministratore del dominio tenant di Office 365, ad esempio administrator@fabrikam.com. Assicurarsi di aggiornare il valore di *$CertFile* sul percorso del certificato, se non è stato creato dallo script precedente. A tale scopo, copiare e incollare il codice seguente.
    
        # Make sure to update the following $CertFile with the path to the cert if not using the previous script.
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        If (Test-Path $CertFile)
        {
            $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
            $objFSO = New-Object -ComObject Scripting.FileSystemObject;
            $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
            $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
            $cer.Import($CertFile);
            $binCert = $cer.GetRawCertData();
            $credValue = [System.Convert]::ToBase64String($binCert);
        
            Write-Host "Please enter the administrator user name and password of the Office 365 tenant domain..."
        
            Connect-MsolService;
            Import-Module msonlineextended;
        
            Write-Host "Adding a key to Service Principal..."
        
            $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
            New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue -StartDate $cer.GetEffectiveDateString() -EndDate $cer.GetExpirationDateString()
        }
        Else
        {
            Write-Error "Cannot find certificate."
        } 
    
    Il risultato previsto dovrebbe avere un aspetto analogo al seguente.
    
        Please enter the administrator user name and password of the Office 365 tenant domain...
        Adding a key to Service Principal...
        Complete.

## Abilitare l'inoltro delle notifiche push

Dopo aver effettuato la procedura precedente e dopo aver configurato l'autenticazione OAuth, un amministratore locale deve attivare l'inoltro della notifica push utilizzando lo script seguente. Assicurarsi di aggiornare il valore di *$tenantDomain* sul nome del proprio dominio. A tale scopo, copiare e incollare il codice seguente.

    $tenantDomain = "Fabrikam.com"
    Enable-PushNotificationProxy -Organization:$tenantDomain

Il risultato previsto dovrebbe avere un aspetto analogo al seguente.

    RunspaceId        : 4f2eb5cc-b696-482f-92bb-5b254cd19d60
    DisplayName       : On Premises Proxy app
    Enabled           : True
    Organization      : fabrikam.com
    Uri               : https://outlook.office365.com/PushNotifications
    Identity          : OnPrem-Proxy
    IsValid           : True
    ExchangeVersion   : 0.20 (15.0.0.0)
    Name              : OnPrem-Proxy
    DistinguishedName : CN=OnPrem-Proxy,CN=Push Notifications Settings,CN=First Organization,CN=Microsoft
                        Exchange,CN=Services,CN=Configuration,DC=Domain,DC=extest,DC=microsoft,DC=com
    Guid              : 8b567958-58a4-403c-a8f0-524d7f1e9279
    ObjectCategory    : fabrikam.com/Configuration/Schema/ms-Exch-Push-Notifications-App
    ObjectClass       : {top, msExchPushNotificationsApp}
    WhenChanged       : 8/27/2013 7:23:47 PM
    WhenCreated       : 8/14/2013 1:30:27 PM
    WhenChangedUTC    : 8/28/2013 2:23:47 AM
    WhenCreatedUTC    : 8/14/2013 8:30:27 PM
    OrganizationId    :
    OriginatingServer : server.fabrikam.com
    ObjectState       : Unchanged

## Verificare che le notifiche push funzionino

Dopo aver effettuato la procedura precedente, le notifiche push devono essere provate in questo modo:

  - **Invio di un messaggio di posta elettronica di testo alla cassetta postale dell'utente:** 
    
    1.  Configurare un account in OWA per dispositivi su un dispositivo mobile al fine di eseguire la sottoscrizione per le notifiche.
    
    2.  Tornare alla schermata principale del dispositivo, che inserisce OWA per dispositivi in background.
    
    3.  Inviare un messaggio di posta elettronica da un altro dispositivo, ad esempio un PC, che viene inserito nella cartella Posta in arrivo dell'account configurato sul dispositivo mobile.
    
    4.  Si dovrebbe ottenere un conteggio nascosto che viene indicato sull'icona dell'app in pochi minuti.

  - **Abilitazione del monitoraggio.** Un metodo alternativo per testare le notifiche push o per capire il motivo del mancato funzionamento delle notifiche consiste nel monitoraggio di un server di cassette postali nell'organizzazione dell'utente. L'amministratore di un server di Exchange 2013 locale deve richiamare il monitoraggio di inoltro delle notifiche push utilizzando il seguente script. A tale scopo, copiare e incollare il codice seguente.
    
        # Send a push notification to verify connectivity.
        
        $s = Get-ExchangeServer | ?{$_.ServerRole -match "Mailbox"}
        If ($s.Count -gt 1)
        {
            $s = $s[0]
        }
        If ($s.Count -ne 0)
        {
            # Restart the monitoring service to clear the cache from when push was previously disabled.
            Restart-Service MSExchangeHM
        
            # Give the monitoring service enough time to load.
            Start-Sleep -Seconds:120
        
            Invoke-MonitoringProbe PushNotifications.Proxy\PushNotificationsEnterpriseConnectivityProbe -Server:$s.Fqdn | fl ResultType, Error, Exception
        }
        Else
        {
            Write-Error "Cannot find a Mailbox server in the current site."
        }
    
    Il risultato previsto dovrebbe avere un aspetto analogo al seguente.
    
        ResultType : Succeeded
        Error      :
        Exception  :


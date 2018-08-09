---
title: 'Config. autentic. Kerberos-Accesso client con bilanc. car.: Exchange 2013 Help'
TOCTitle: Configurazione dell'autenticazione Kerberos per i server Accesso client con bilanciamento del carico
ms:assetid: 8f4faeea-a825-438d-97dc-1c398ce7aba5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff808312(v=EXCHG.150)
ms:contentKeyID: 62835887
ms.date: 01/08/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurazione dell'autenticazione Kerberos per i server Accesso client con bilanciamento del carico

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

**Sintesi:**  Viene descritto come utilizzare l'autenticazione Kerberos con i server Accesso client con carico bilanciato in Exchange 2013.

Per utilizzare l'autenticazione Kerberos con i server Accesso client con carico bilanciato, è necessario completare la procedura di configurazione illustrata in questo articolo.

## Creazione della credenziale di account del servizio alternativo in Servizi di dominio Active Directory

Tutti i server Accesso client che condividono gli stessi spazi dei nomi e URL devono utilizzare le stesse credenziali dell'account del servizio alternativo. In generale, è sufficiente disporre di un singolo account per una foresta per ogni versione di Exchange. *Credenziale dell'account del servizio alternativo* o *credenziale ASA*.


> [!IMPORTANT]
> Exchange 2010 ed Exchange 2013 non possono condividere la stessa credenziale ASA. È necessario creare una nuova credenziale ASA per Exchange 2013.




> [!IMPORTANT]
> I record CNAME sono supportati per gli spazi dei nomi condivisi, ma si consiglia di utilizzare i record A. In questo modo il client invia correttamente una richiesta del ticket Kerberos in base al nome condiviso, e non all'FQDN del server.



Durante l'impostazione della credenziale ASA, tenere presenti le indicazioni seguenti:

  - **Tipo account.** È consigliabile creare un account computer anziché un account utente. Siccome non consente l'accesso interattivo, un account computer presenta criteri di sicurezza più semplici di un account utente. Se si crea un account computer, la password non scade, ma si consiglia comunque di aggiornarla periodicamente. È possibile utilizzare il criterio di gruppo locale per specificare una validità massima per l'account computer e gli script per eliminare periodicamente gli account computer che non soddisfano i criteri correnti. I criteri di sicurezza locali, inoltre, determinano quando è necessario modificare la password. È consigliabile utilizzare un account computer, ma è possibile creare un account utente.

  - **Nome account.** Non esistono requisiti per il nome dell'account. È possibile utilizzare qualsiasi nome conforme allo schema di denominazione.

  - **Gruppo di account.** L'account utilizzato per la credenziale ASA non richiede privilegi speciali di sicurezza. Se si usa un account computer, è sufficiente che l'account sia membro del gruppo di sicurezza Domain Computers. Se si usa un account utente, è sufficiente che l'account sia membro del gruppo di sicurezza Domain Users.

  - **Password account.** La password fornita al momento della creazione dell'account non verrà utilizzata. In questo modo, quando si crea l'account, è necessario utilizzare una password complessa e verificare che sia conforme ai requisiti dell'organizzazione.

**Per creare la credenziale ASA come account computer**

1.  In un computer aggiunto al dominio, avviare Windows PowerShell o Exchange Management Shell.
    
    Utilizzare il cmdlet **Import-Module** per importare il modulo Active Directory.
    
        Import-Module ActiveDirectory

2.  Utilizzare il cmdlet **New-ADComputer** per creare un nuovo account computer di Active Directory tramite la seguente sintassi:
    
        New-ADComputer [-Name] <string> [-AccountPassword <SecureString>] [-AllowReversiblePasswordEncryption <System.Nullable[boolean]>] [-Description <string>] [-Enabled <System.Nullable[bool]>]
    
    **Esempio:** 
    
        New-ADComputer -Name EXCH2013ASA -AccountPassword (Read-Host 'Enter password' -AsSecureString) -Description 'Alternate Service Account credentials for Exchange' -Enabled:$True -SamAccountName EXCH2013ASA
    
    Dove *EXCH2013ASA* è il nome dell'account, la descrizione *Alternate Service Account credentials for Exchange* è qualsiasi elemento si desideri e il valore del parametro *SamAccountName*, in questo caso *EXCH2013ASA*, deve essere univoco nella directory.

3.  Utilizzare il cmdlet **Set-ADComputer** per abilitare il supporto della crittografia AES 256 utilizzato da Kerberos tramite la seguente sintassi:
    
        Set-ADComputer [-Name] <string> [-add @{<attributename>="<value>"]
    
    **Esempio:** 
    
        Set-ADComputer EXCH2013ASA -add @{"msDS-SupportedEncryptionTypes"="28"}
    
    Dove *EXCH2013ASA* è il nome dell'account e l'attributo da modificare è *msDS-SupportedEncryptionTypes* con un valore decimale di 28, che consente di abilitare le seguenti crittografie: RC4-HMAC, AES128-CTS-HMAC-SHA1-96, AES256-CTS-HMAC-SHA1-96.

Per ulteriori informazioni su questi cmdlet, vedere [Import-Module](https://technet.microsoft.com/library/hh849725.aspx) e [New-ADComputer](https://technet.microsoft.com/library/ee617245.aspx).

## Scenari tra foreste

Se si dispone di una distribuzione tra foreste o a foresta di risorse e gli utenti si trovano all'esterno della foresta di Active Directory contenente Exchange, è necessario configurare le relazioni di trust tra foreste. Inoltre, per ogni foresta nella distribuzione, è necessario configurare una regola di routing che abilita il trust tra tutti i suffissi dei nomi all'interno della foresta e tra foreste. Per ulteriori informazioni sulla gestione di trust tra foreste, vedere [Gestire i trust tra foreste](https://technet.microsoft.com/library/cc772440.aspx).

## Identificare i nomi dell'entità servizio da associare alla credenziale ASA

Dopo aver creato la credenziale ASA, è necessario associare i nomi dell'entità servizio (SPN) di Exchange a tale credenziale. L'elenco dei nomi principali del servizio di Exchange può variare in base alla configurazione, ma deve includere almeno i seguenti elementi:

  - **http/**   Usare questo SPN per Outlook via Internet, MAPI su HTTP, Servizi Web Exchange, individuazione automatica e rubrica offline.

I valori SPN devono corrispondere al nome del servizio di bilanciamento del carico della rete invece che sui singoli server. Per consentire una pianificazione dei valori SPN da utilizzare, considerare i seguenti scenari:

  - Sito singolo di Active Directory

  - Più siti di Active Directory

In ciascuno di questi scenari, si ipotizza che i nomi di dominio completi (FQDN) con bilanciamento del carico siano stati distribuiti per gli URL interni, gli URL esterni e gli URL di individuazione automatica utilizzati dai membri del server Accesso client. Per ulteriori informazioni, vedere Informazioni su inoltro e reindirizzamento.

## Sito singolo di Active Directory

Se si dispone di un sito singolo di Active Directory, l'ambiente potrebbe assomigliare a quello riportato nella seguente figura:

![Matrice CAS con AD singolo e autenticazione Kerberos](images/Ff808312.97a1a926-f4ac-4498-bc6b-32e7fb1b70f1(EXCHG.150).jpg "Matrice CAS con AD singolo e autenticazione Kerberos")

In base agli FQDN utilizzati dai client Outlook interni indicati nella figura precedente, è necessario associare i seguenti SPN alla credenziale ASA:

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

## Più siti di Active Directory

Se si dispone di più siti di Active Directory, l'ambiente potrebbe assomigliare a quello riportato nella seguente figura:

![Matrice CAS con più siti AD e autenticazione Kerberos](images/Ff808312.95b52bd8-7074-4055-8bd2-e6bf1f112b42(EXCHG.150).jpg "Matrice CAS con più siti AD e autenticazione Kerberos")

In base agli FQDN utilizzati dai client Outlook indicati nella figura precedente, è necessario associare i seguenti SPN alla credenziale ASA utilizzata dai server Accesso client in ADSite 1:

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

È inoltre necessario associare i seguenti SPN alla credenziale ASA utilizzata dai server Accesso client in ADSite 2:

  - http/mailsdc.corp.tailspintoys.com

  - http/autodiscoversdc.corp.tailspintoys.com

## Configurare e verificare la configurazione della credenziale ASA in ogni server Accesso Client

Dopo aver creato l'account, è necessario verificare che l'account sia replicato in tutti i controller di dominio di Servizi di dominio Active Directory. In particolare, l'account deve essere presente in ogni server Accesso client che usa la credenziale ASA. Successivamente, configurare l'account come credenziale ASA in ogni server Accesso client nella distribuzione.

Configurare la credenziale ASA tramite Exchange Management Shell come descritto in una delle seguenti procedure:

  - Distribuire la credenziale ASA al primo server Accesso client di Exchange 2013

  - Distribuire la credenziale ASA ai successivi server Accesso client di Exchange 2013

L'unico metodo supportato per distribuire la credenziale ASA consiste nell'uso dello script RollAlternateServiceAcountPassword.ps1. Per ulteriori informazioni, vedere [Utilizzando lo Script RollAlternateserviceAccountCredential.ps1 in Shell](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md). Una volta eseguito lo script, si consiglia di verificare che tutti i server di destinazione siano stati correttamente aggiornati.

## Distribuire la credenziale ASA al primo server Accesso client di Exchange 2013

1.  Aprire Exchange Management Shell su un server Exchange 2013.

2.  Modificare le directory in *\<Exchange 2013 installation directory\>*\\V15\\Scripts.

3.  Eseguire il comando seguente per distribuire la credenziale ASA al primo server Accesso client di Exchange 2013:
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-1.corp.tailspintoys.com -GenerateNewPasswordFor tailspin\EXCH2013ASA$

4.  Quando viene richiesto se si desidera modificare la password per l'account del servizio alternativo, rispondere **Sì**.

Di seguito è riportato un esempio dell'output visualizzato quando si esegue lo script RollAlternateServiceAccountPassword.ps1.

    ========== Starting at 01/12/2015 10:17:47 ==========
    Creating a new session for implicit remoting of "Get-ExchangeServer" command...
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-1                                                   cas-1.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    
    Prior to pushing new credentials, all existing credentials that are invalid or no longer work will be removed from  the destination servers.
    Pushing credentials to server cas-1
    Setting a new password on Alternate Serice Account in Active Directory
    
    Password change
    Do you want to change password for tailspin\EXCH2013ASA$ in Active Directory at this time?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
    Preparing to update Active Directory with a new password for tailspin\EXCH2013ASA$ ...
    Resetting a password in the Active Directory for tailspin\EXCH2013ASA$ ...
    New password was successfully set to Active Directory.
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: {mail.corp.tailspintoys.com}
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-1 Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
              ...
    
    ========== Finished at 01/12/2015 10:20:00 ==========
    
            THE SCRIPT HAS SUCCEEDED

## Distribuire la credenziale ASA a un altro server Accesso client di Exchange 2013

1.  Aprire Exchange Management Shell su un server Exchange 2013.

2.  Modificare le directory in *\<Exchange 2013 installation directory\>*\\V15\\Scripts.

3.  Eseguire il comando seguente per distribuire la credenziale ASA a un altro server Accesso client di Exchange 2013:
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-2.corp.tailspintoys.com -CopyFrom cas-1.corp.tailspintoys.com

4.  Ripetere il passaggio 3 per ogni server Accesso client in cui distribuire la credenziale ASA.

Di seguito è riportato un esempio dell'output visualizzato quando si esegue lo script RollAlternateServiceAccountPassword.ps1.

    ========== Starting at 01/12/2015 10:34:35 ==========
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-2                                                   cas-2.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    Prior to pushing new credentials, all existing credentials will be removed from the destination servers.
    Pushing credentials to server cas-2
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: cas-2.corp.tailspintoys.com
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-2 Latest: 1/12/2015 10:37:59 AM, tailspin\EXCH2013ASA$
              ...
    
    
    ========== Finished at 01/12/2015 10:38:13 ==========
    
            THE SCRIPT HAS SUCCEEDED

## Verificare la distribuzione della credenziale ASA

  - Aprire Exchange Management Shell su un server Exchange 2013.

  - Eseguire il comando indicato per verificare le impostazioni su un server Accesso client:
    
        Get-ClientAccessServer CAS-3 -IncludeAlternateServiceAccountCredentialStatus | Format-List Name, AlternateServiceAccountConfiguration

  - Ripetere il passaggio 2 in ogni server Accesso client in cui si desidera verificare la distribuzione della credenziale ASA.

Di seguito è riportato un esempio dell'output visualizzato quando si esegue il comando Get-ClientAccessServer sopra indicato e non è stata impostata nessuna credenziale ASA in precedenza.

    Name                                 : CAS-1
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: <Not set>
                                               ...

Di seguito è riportato un esempio dell'output visualizzato quando si esegue il comando Get-ClientAccessServer sopra indicato ed è stata impostata una credenziale ASA in precedenza. Vengono restituite credenziale ASA, data e ora impostate in precedenza.

    Name                                 : CAS-3
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: 7/15/2014 12:58:35 PM, tailspin\oldSharedServiceAccountName$
                                               ...

## Associare i nomi dell'entità servizio (SPN) alla credenziale ASA


> [!IMPORTANT]
> Non associare SPN a una credenziale ASA se questa non è stata distribuita in almeno un server Exchange, come descritto in precedenza in Distribuire la credenziale ASA al primo server Accesso client di Exchange 2013. In caso contrario, si riscontrano errori di autenticazione Kerberos.



Prima di associare gli SPN alla credenziale ASA, è necessario verificare che gli SPN di destinazione non siano stati già associati a un account diverso nella foresta. Le credenziali ASA devono essere l'unico account della foresta associato a questi nomi principali di servizio. È possibile verificare che nessun altro account della foresta sia associato agli SPN eseguendo il comando **setspn** dalla riga di comando.

**Verificare che l'SPN non sia già associato a un account in una foresta eseguendo il comando setspn**

1.  Premere **Start**. Nella casella **Cerca**, digitare **Prompt dei comandi**, quindi selezionare **Prompt dei comandi** nell'elenco dei risultati.

2.  Al prompt dei comandi, digitare il seguente comando:
    
        setspn -F -Q <SPN>
    
    Dove \<SPN\> è l'SPN da associare alla credenziale ASA. Ad esempio:
    
        setspn -F -Q http/mail.corp.tailspintoys.com
    
    Il comando non dovrebbe restituire nulla. Se restituisce qualche risultato, il nome principale del servizio è già associato a un altro account. Ripetere questo passaggio una volta per ogni SPN da associare alla credenziale ASA.

**Associare un SPN a una credenziale ASA tramite il comando setspn**

1.  Premere **Start**. Nella casella **Cerca**, digitare **Prompt dei comandi**, quindi selezionare **Prompt dei comandi** nell'elenco dei risultati.

2.  Al prompt dei comandi, digitare il seguente comando:
    
        setspn -S <SPN> <Account>$
    
    Dove \<SPN\> è l'SPN da associare alla credenziale ASA e \<Account\> è l'account associato a tale credenziale. Ad esempio:
    
        setspn -S http/mail.corp.tailspintoys.com tailspin\EXCH2013ASA$
    
    Eseguire questo comando una volta per ogni SPN da associare alla credenziale ASA.

**Verificare di avere associato gli SPN alle credenziali ASA tramite il comando setspn**

1.  Premere **Start**. Nella casella **Cerca**, digitare **Prompt dei comandi**, quindi selezionare **Prompt dei comandi** nell'elenco dei risultati.

2.  Al prompt dei comandi, digitare il seguente comando:
    
        setspn -L <Account>$
    
    Dove \<Account\> è l'account associato alla credenziale ASA. Ad esempio:
    
        setspn -L tailspin\EXCH2013ASA$
    
    È sufficiente eseguire questo comando una volta.

## Abilitare l'autenticazione Kerberos per i client Outlook

1.  Aprire Exchange Management Shell su un server Exchange 2013.

2.  Per abilitare l'autenticazione Kerberos per i client Outlook via Internet, eseguire il comando seguente nel server Accesso client:
    
        Get-OutlookAnywhere -server CAS-1 | Set-OutlookAnywhere -InternalClientAuthenticationMethod  Negotiate

3.  Per abilitare l'autenticazione Kerberos per i client MAPI su HTTP, eseguire il comando seguente nel server Accesso client di Exchange 2013:
    
        Get-MapiVirtualDirectory -Server CAS-1 | Set-MapiVirtualDirectory -IISAuthenticationMethods Ntlm, Negotiate

4.  Ripetere i passaggi 2 e 3 per ogni server Accesso client di Exchange 2013 in cui si desidera abilitare l'autenticazione Kerberos.

## Convalidare l'autenticazione Kerberos dei client Exchange

Dopo la configurazione di Kerberos e della credenziale ASA, verificare la corretta autenticazione dei client come descritto in queste attività.

## Verificare che Microsoft Exchange Service Host sia in esecuzione

Microsoft Exchange Service Host service (MSExchangeServiceHost) sul server Accesso client è responsabile della gestione delle credenziali ASA. Se questo servizio non è in esecuzione, l'autenticazione Kerberos non sarà possibile. Per impostazione predefinita, il servizio è configurato per avviarsi automaticamente quando viene avviato il computer.

**Per verificare che Microsoft Exchange Service Host sia stato avviato**

1.  Fare clic su **Start**, digitare **services.msc**, quindi selezionare **services.msc** dall'elenco.

2.  Nella finestra **Servizi**, individuare il servizio **Microsoft Exchange Service Host** nell'elenco.

3.  Lo stato del servizio sarà **In esecuzione**. Se lo stato non è **In esecuzione**, fare clic con il pulsante destro del mouse sul servizio e quindi scegliere **Avvia**.

## Convalidare Kerberos dal server Accesso client

Quando è stata configurata la credenziale ASA in ogni server Accesso client, è stato eseguito il cmdlet **set-ClientAccessServer**. Dopo aver eseguito questo cmdlet, è possibile utilizzare i log per verificare le connessioni Kerberos con esito positivo.

**Per accertarsi del corretto funzionamento di Kerberos tramite il file di log HttpProxy**

1.  In un editor di testo, passare alla cartella in cui è archiviato il log HttpProxy. Per impostazione predefinita, il log viene memorizzato nella seguente cartella:
    
    %ExchangeInstallPath%\\Logging\\HttpProxy\\RpcHttp

2.  Aprire il file di log più recente e cercare la parola **Negotiate**. La riga nel file di log sarà simile all'esempio seguente:
    
        2014-02-19T13:30:49.219Z,e19d08f4-e04c-42da-a6be-b7484b396db0,15,0,775,22,,RpcHttp,mail.corp.tailspintoys.com,/rpc/rpcproxy.dll,,Negotiate,True,tailspin\Wendy,tailspintoys.com,MailboxGuid~ad44b1e0-e44f-4a16-9396-3a437f594f88,MSRPC,192.168.1.77,EXCH1,200,200,,RPC_OUT_DATA,Proxy,exch2.tailspintoys.com,15.00.0775.000,IntraForest,MailboxGuidWithDomain,,,,76,462,1,,1,1,,0,,0,,0,0,16272.3359,0,0,3,0,23,0,25,0,16280,1,16274,16230,16233,16234,16282,?ad44b1e0-e44f-4a16-9396-3a437f594f88@tailspintoys.com:6001,,BeginRequest=2014-02-19T13:30:32.946Z;BeginGetRequestStream=2014-02-19T13:30:32.946Z;OnRequestStreamReady=2014-02-19T13:30:32.946Z;BeginGetResponse=2014-02-19T13:30:32.946Z;OnResponseReady=2014-02-19T13:30:32.977Z;EndGetResponse=2014-02-19T13:30:32.977Z;,PossibleException=IOException;
    
    Se viene visualizzato che il valore **AuthenticationType** è **Negotiate**, il server sta creando correttamente le connessioni autenticate Kerberos.

## Gestire le credenziali ASA

Se è necessario aggiornare la password per la credenziale ASA periodicamente, utilizzare la procedura di configurazione della credenziale ASA illustrata in questo articolo. Prendere in considerazione l'idea di configurare un'attività pianificata per la gestione della password. Controllare l'attività pianificata per garantire il rollover sistematico della password ed evitare possibili interruzioni dell'autenticazione.

## Disattivare l'autenticazione Kerberos

Per configurare il server Accesso client in modo che non utilizzi Kerberos, scollegare o rimuovere i nomi principali del servizio dalla credenziale ASA. Se i nomi principali del servizio vengono rimossi, i client non potranno tentare l'autenticazione Kerberos e i quelli configurati per l'utilizzo dell'autenticazione Negotiate utilizzeranno NTLM. I client configurati per l'utilizzo solo di Kerberos non potranno eseguire la connessione. Una volta rimossi i nomi principali del servizio, è necessario eliminare anche l'account.

**Per rimuovere le credenziali ASA**

1.  Aprire Exchange Management Shell su un server Exchange 2013 ed eseguire il comando seguente:
    
        Set-ClientAccessServer CAS-1 -RemoveAlternateServiceAccountCredentials

2.  Anche se non è necessario eseguire questa operazione immediatamente, occorre riavviare tutti i computer client per cancella re la cache dei ticket Kerberos dal computer.


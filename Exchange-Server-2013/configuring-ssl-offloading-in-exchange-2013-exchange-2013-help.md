---
title: 'Configurazione Offload di SSL in Exchange 2013: Exchange 2013 Help'
TOCTitle: Configurazione Offload di SSL in Exchange 2013
ms:assetid: 654cc2c2-918b-48fc-9532-9c8e3012810d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn635115(v=EXCHG.150)
ms:contentKeyID: 61202269
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione Offload di SSL in Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-08-22_

Di seguito viene illustrato come configurare la ripartizione del carico di lavoro SSL per i protocolli e i servizi correlati sui server Accesso client Exchange 2013 con Service Pack 1 (SP1) installato. Se si dispone di più server Accesso client, è necessario effettuare i passaggi necessari per ogni protocollo o servizio su ogni server Accesso client con SP1 installato nell'organizzazione locale. Le configurazioni di tutti i server Accesso client dell'organizzazione devono essere identiche. Se si passa ad aggiornamenti cumulativi o Service Pack più recenti e si desidera continuare a utilizzare la ripartizione del carico di lavoro SSL, è necessario effettuare di nuovo i seguenti passaggi dopo il passaggio o dopo aver applicato gli aggiornamenti ai server Accesso client di Exchange 2013.

Uno dei principali vantaggi della ripartizione del carico di lavoro SSL è la possibilità di gestire più facilmente i certificati utilizzati. Anziché disporre di certificati SSL separati per ogni server Accesso client con SP1 installato, viene utilizzato un solo certificato SSL, che viene importato in tutti i server Accesso client. Il certificato SSL utilizzato può essere un certificato esistente o un nuovo certificato creato.


> [!WARNING]
> Quando si utilizza Gestione Internet Information Services (IIS), Exchange Management Shell o un'interfaccia della riga di comando per configurare offload SSL, si noti che esiste un sito di <STRONG>Exchange Back-End</STRONG> e un <STRONG>sito Web predefinito</STRONG>. Per offload SSL, solo configurare il <STRONG>sito Web predefinito</STRONG> e non si apportano modifiche al sito di <STRONG>Exchange Back-End</STRONG>.



**Sommario**

Configuring SSL offloading for Outlook Web App

Configuring SSL offloading for the Exchange Admin Center (EAC)

Configuring SSL offloading for Outlook Anywhere

Configuring SSL offloading for the Offline Address Book (OAB)

Configuring SSL offloading for Exchange ActiveSync (EAS)

Configuring SSL offloading for Exchange Web Services (EWS)

Configuring SSL offloading for the Autodiscover service

Configuring SSL offloading for the Mailbox Replication Proxy Service (MRSProxy)

Configurazione della ripartizione del carico di lavoro SSL per client Outlook (directory virtuale MAPI)

Using a Shell script to enable SSL offloading for all protocols and services

Configuring coexistence with Exchange 2007 and Exchange 2010

## Che cosa è necessario sapere prima di iniziare

  - Installare tutti i server Accesso Client e Cassette postali necessari nell'organizzazione.

  - Installare Service Pack 1 (SP1) su ogni server Accesso client e Cassette postati dell'organizzazione. Per scaricare SP1, vedere [Aggiornamenti per Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

  - Determinare le autorizzazioni necessarie per Exchange 2013 visualizzando le [Autorizzazioni funzionalità](feature-permissions-exchange-2013-help.md).

  - Per conoscere le autorizzazioni necessarie per il server Accesso client, vedere "Autorizzazioni del server Accesso client" in [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per conoscere le autorizzazioni necessarie per il server Accesso client, vedere "Autorizzazioni di Outlook Web App" in [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo la Shell per eseguire alcune procedure. Per sapere come aprire Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)).

  - Per utilizzare un certificato esistente sui server Accesso client e sul dispositivo con cui si stanno terminando le comunicazioni SSL, esportare il certificato con la chiave privata su un server Accesso client e importala o installarla sul dispositivo. Per ulteriori informazioni, vedere [Export-ExchangeCertificate](https://technet.microsoft.com/it-it/library/aa996305\(v=exchg.150\)).

  - Per utilizzare un nuovo certificato, è necessario adoperare l'interfaccia di amministrazione Exchange o Shell per creare, importare e abilitare il nuovo certificato. Per ulteriori informazioni, vedere [Interfaccia utente per la gestione dei certificati in Exchange 2013](exchange-2013-certificate-management-ui-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurare la ripartizione del carico di lavoro SSL per Outlook Web App

Per abilitare la ripartizione del carico di lavoro SSL per Outlook Web App, è necessario rimuovere il requisito SSL sulla directory virtuale **owa** sul **Sito Web predefinito**:

  - **Passaggio 1**   È possibile utilizzare Gestione Internet Information Services (IIS) o una riga di comando per disabilitare SSL sulla directory virtuale **owa**:
    
      - Utilizzando Gestione Internet Information Services (IIS), espandere **Siti** \> **Sito Web predefinito**, quindi selezionare la directory virtuale **owa**. Nel riquadro dei risultati, in **IIS**, fare doppio clic su **Impostazioni SSL**. Nel riquadro dei risultati **Impostazioni SSL**, deselezionare la casella di controllo **Richiesta SSL**, quindi fare clic su **Applica** nel riquadro **Azioni**.
    
      - Utilizzando la riga di comando, digitare quanto segue e premere Invio.
        
            appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST

  - **Passaggio 2**   È necessario riavviare il pool di applicazioni corretto o Internet Information Services adottando uno dei metodi seguenti:
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            appcmd Recycle AppPool MSExchangeOWAAppPool
    
      - Utilizzando un cmdlet di Windows PowerShell, digitare quanto segue e premere Invio.
        
            IIS:\>Restart-WebAppPool MSExchangeOWAAppPool
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            iisreset /noforce
    
      - Utilizzo di Gestione Internet Information Services (IIS): In Gestione Internet Information Services (IIS), nel riquadro **Azioni**, fare clic su **Riavvia**.

Torna all'inizio

## Configurare la ripartizione del carico di lavoro SSL per l'interfaccia di amministrazione Exchange (EAC)

Per abilitare la ripartizione del carico di lavoro SSL per EAC, è necessario rimuovere il requisito SSL sulla directory virtuale **ecp** sul **Sito Web predefinito**:

  - **Passaggio 1**   È possibile utilizzare Gestione Internet Information Services (IIS1) o una riga di comando per disabilitare SSL sulla directory virtuale **ecp**:
    
      - Utilizzando Gestione Internet Information Services (IIS), espandere **Siti** \> **Sito Web predefinito**, quindi selezionare la directory virtuale **ecp**. Nel riquadro dei risultati, in **IIS**, fare doppio clic su **Impostazioni SSL**. Nel riquadro dei risultati **Impostazioni SSL**, deselezionare la casella di controllo **Richiesta SSL**, quindi fare clic su **Applica** nel riquadro **Azioni**.
    
      - Utilizzando la riga di comando, digitare quanto segue e premere Invio.
        
            appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
 

  - **Passaggio 2**   È necessario riavviare il pool di applicazioni corretto o Internet Information Services adottando uno dei metodi seguenti:
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            appcmd Recycle AppPool MSExchangeECPAppPool
    
      - Utilizzando un cmdlet di Windows PowerShell, digitare quanto segue e premere Invio.
        
            IIS:\>Restart-WebAppPool MSExchangeECPAppPool
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            iisreset /noforce
    
      - Utilizzo di Gestione Internet Information Services (IIS): In Gestione Internet Information Services (IIS), nel riquadro **Azioni**, fare clic su **Riavvia**.

Torna all'inizio

## Configurazione della ripartizione del carico di lavoro SSL per Outlook Anywhere

SSL Offload di Outlook via Internet è abilitata per impostazione predefinita. Outlook via Internet i client possono usufruire di posta elettronica da una rete pubblica o privata. Per impostazione predefinita, il nome host interno o il nome di dominio completo del server viene utilizzato per consentire ai client interni di Outlook per la connessione. Tuttavia, se Outlook via Internet non viene utilizzata internamente, è necessario rimuovere il nome host interno. Per consentire l'accesso interno ed esterno per i client Outlook, è necessario configurare i nomi host interni ed esterni, impostare il metodo di autenticazione per ogni e impostare entrambi i client interni ed esterni per richiedere la crittografia SSL. Per configurare il metodo di autenticazione per i client esterni, è possibile utilizzare EAC o Shell di gestione di Exchange, ma per i client interni, è necessario utilizzare la Shell:

  - **Passaggio 1**   È possibile utilizzare EAC o Shell se non è stato aggiunto un nome host esterno per Outlook via Internet:
    
      - Utilizzando EAC, andare a **Server**, selezionare il nome del server Accesso client nell'elenco, quindi fare clic su **Modifica**. Nella finestra **Exchange Server**, fare clic su **Outlook Anywhere**, quindi nella casella **Specifica il nome host esterno (ad esempio contoso.com) che gli utenti utilizzeranno per collegarsi all'organizzazione**, inserire il nome host esterno. Verificare che l'opzione **Consenti ripartizione del carico di lavoro SSL** sia selezionata e fare clic su **Salva**.
    
      - Utilizzando Exchange Management Shell, fare clic su **Start**, quindi nel menu **Start** fare clic su **Exchange Management Shell**. Nella finestra, digitare quanto segue e premere Invio:
        
            Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -Externalhostname ClientAccessServer1.contoso.com -ExternalClientsRequireSsl:$True -ExternalClientAuthenticationMethod Basic

  - **Passaggio 2**   Per impostazione predefinita, la ripartizione del carico di lavoro SSL è abilitata. Tuttavia, è possibile utilizzare EAC o Exchange Management Shell se la ripartizione del carico di lavoro SSL è stata disabilitata e si desidera abilitarla:
    
      - Utilizzando EAC, andare a **Server**, selezionare il nome del server Accesso client nell'elenco, quindi fare clic su **Modifica**. Nella finestra **Exchange Server**, fare clic su **Outlook Anywhere**, quindi sull'opzione **Consenti ripartizione del carico di lavoro SSL** e infine su **Salva**.
    
      - Utilizzando Shell, digitare quanto segue e premere Invio:
        
            Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -SSLOffloading $true

  - **Passaggio 3**   Per impostazione predefinita, **Richiesta SSL** non è selezionata sulla directory virtuale **Rpc**, ma se si desidera verificare se SSL è disabilitato, è possibile utilizzare Gestione Internet Information Services (IIS).
    
      - Utilizzando Gestione Internet Information Services (IIS), espandere **Siti** \> **Sito Web predefinito**, quindi selezionare la directory virtuale **Rpc**. Nel riquadro dei risultati, in **IIS**, fare doppio clic su **Impostazioni SSL**. Nel riquadro dei risultati **Impostazioni SSL**, verificare che la casella di controllo **Richiesta SSL** sia deselezionata, quindi fare clic su **Applica** nel riquadro **Azioni**.

  - **Passaggio 4**   È necessario riavviare il pool di applicazioni corretto o Internet Information Services adottando uno dei metodi seguenti:
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            appcmd Recycle AppPool MSExchangeRpcProxyFrontEndAppPool
    
      - Utilizzando un cmdlet di Windows PowerShell, digitare quanto segue e premere Invio.
        
            IIS:\>Restart-WebAppPool MSExchangeRpcProxyFrontEndAppPool
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            iisreset /noforce
    
      - Utilizzo di Gestione Internet Information Services (IIS): In Gestione Internet Information Services (IIS), nel riquadro **Azioni**, fare clic su **Riavvia**.


> [!IMPORTANT]
> È necessario attendere che il processo Service Host applichi le modifiche da Active Directory a Internet Information Services (IIS) ogni 15 minuti anche se si riavvia IIS su un server Accesso client.



Torna all'inizio

## Configurazione della ripartizione del carico di lavoro SSL per Rubrica offline

Per abilitare la ripartizione del carico di lavoro SSL per Rubrica offline, è necessario rimuovere il requisito SSL sulla directory virtuale **OAB** sul **Sito Web predefinito**:

  - **Passaggio 1**   È possibile utilizzare Gestione Internet Information Services (IIS) o una riga di comando per disabilitare SSL sulla directory virtuale **OAB**:
    
      - Utilizzando Gestione Internet Information Services (IIS), espandere **Siti** \> **Sito Web predefinito**, quindi selezionare la directory virtuale **OAB**. Nel riquadro dei risultati, in **IIS**, fare doppio clic su **Impostazioni SSL**. Nel riquadro dei risultati **Impostazioni SSL**, deselezionare la casella di controllo **Richiesta SSL**, quindi fare clic su **Applica** nel riquadro **Azioni**.
    
      - Utilizzando la riga di comando, digitare quanto segue e premere Invio.
        
            appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST

  - **Passaggio 2**   È necessario riavviare il pool di applicazioni corretto o Internet Information Services adottando uno dei metodi seguenti:
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            appcmd Recycle AppPool MSExchangeOABAppPool
    
      - Utilizzando un cmdlet di Windows PowerShell, digitare quanto segue e premere Invio.
        
            IIS:\>Restart-WebAppPool MSExchangeOABAppPool
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            iisreset /noforce
    
      - Utilizzo di Gestione Internet Information Services (IIS): In Gestione Internet Information Services (IIS), nel riquadro **Azioni**, fare clic su **Riavvia**.

Torna all'inizio

## Configurazione della ripartizione del carico di lavoro SSL per Exchange ActiveSync (EAS)

Per abilitare la ripartizione del carico di lavoro SSL per Exchange ActiveSync (EAS), è necessario rimuovere il requisito SSL sulla directory virtuale **Microsoft-Server-ActiveSync** sul **Sito Web predefinito**:

  - **Passaggio 1**   È possibile utilizzare Gestione Internet Information Services (IIS) o una riga di comando per disabilitare SSL sulla directory virtuale **Microsoft-Server-ActiveSync**:
    
      - Utilizzando Gestione Internet Information Services (IIS), espandere **Siti** \> **Sito Web predefinito**, quindi selezionare la directory virtuale **Microsoft-Server-ActiveSync**. Nel riquadro dei risultati, in **IIS**, fare doppio clic su **Impostazioni SSL**. Nel riquadro dei risultati **Impostazioni SSL**, deselezionare la casella di controllo **Richiesta SSL**, quindi fare clic su **Applica** nel riquadro **Azioni**.
    
      - Utilizzando la riga di comando, digitare quanto segue e premere Invio.
        
            appcmd set config "Default Web Site/MSExchangeSyncAppPool" /section:access /sslFlags:None /commit:APPHOST

  - **Passaggio 2**   È necessario riavviare il pool di applicazioni corretto o Internet Information Services adottando uno dei metodi seguenti:
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            appcmd Recycle AppPool MSExchangeSyncAppPool
    
      - Utilizzando un cmdlet di Windows PowerShell, digitare quanto segue e premere Invio.
        
            IIS:\>Restart-WebAppPool MSExchangeSyncAppPool
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            iisreset /noforce
    
      - Utilizzo di Gestione Internet Information Services (IIS): In Gestione Internet Information Services (IIS), nel riquadro **Azioni**, fare clic su **Riavvia**.

Torna all'inizio

## Configurazione della ripartizione del carico di lavoro SSL per Servizi Web Exchange

Per abilitare la ripartizione del carico di lavoro SSL per Servizi Web Exchange, è necessario rimuovere il requisito SSL sulla directory virtuale **owa** su **Sito Web predefinito**:

  - **Passaggio 1**   È possibile utilizzare Gestione Internet Information Services (IIS) o una riga di comando per disabilitare SSL sulla directory virtuale **EWS**:
    
      - Utilizzando Gestione Internet Information Services (IIS), espandere **Siti** \> **Sito Web predefinito**, quindi selezionare la directory virtuale **EWS**. Nel riquadro dei risultati, in **IIS**, fare doppio clic su **Impostazioni SSL**. Nel riquadro dei risultati **Impostazioni SSL**, deselezionare la casella di controllo **Richiesta SSL**, quindi fare clic su **Applica** nel riquadro **Azioni**.
    
      - Utilizzando la riga di comando, digitare quanto segue e premere Invio.
        
            appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST

  - **Passaggio 2**   È necessario riavviare il pool di applicazioni corretto o Internet Information Services adottando uno dei metodi seguenti:
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            appcmd Recycle AppPool MSExchangeServicesAppPool
    
      - Utilizzando un cmdlet di Windows PowerShell, digitare quanto segue e premere Invio.
        
            IIS:\>Restart-WebAppPool MSExchangeServicesAppPool
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            iisreset /noforce
    
      - Utilizzo di Gestione Internet Information Services (IIS): In Gestione Internet Information Services (IIS), nel riquadro **Azioni**, fare clic su **Riavvia**.

Torna all'inizio

## Configurazione della ripartizione del carico di lavoro SSL per il servizio Individuazione automatica

Per abilitare la ripartizione del carico di lavoro SSL per il servizio Individuazione automatica, è necessario rimuovere il requisito SSL sulla directory virtuale **Autodiscover** sul **Sito Web predefinito**:

  - **Passaggio 1**   È possibile utilizzare Gestione Internet Information Services (IIS) o una riga di comando per disabilitare SSL sulla directory virtuale **Autodiscover**:
    
      - Utilizzando Gestione Internet Information Services (IIS), espandere **Siti** \> **Sito Web predefinito**, quindi selezionare la directory virtuale **Autodiscover**. Nel riquadro dei risultati, in **IIS**, fare doppio clic su **Impostazioni SSL**. Nel riquadro dei risultati **Impostazioni SSL**, deselezionare la casella di controllo **Richiesta SSL**, quindi fare clic su **Applica** nel riquadro **Azioni**.
    
      - Utilizzando la riga di comando, digitare quanto segue e premere Invio.
        
            appcmd set config "Default Web Site/autodiscover" /section:access /sslFlags:None /commit:APPHOST

  - **Passaggio 2**   È necessario riavviare il pool di applicazioni corretto o Internet Information Services adottando uno dei metodi seguenti:
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            appcmd Recycle AppPool MSExchangeAutodiscoverAppPool
    
      - Utilizzando un cmdlet di Windows PowerShell, digitare quanto segue e premere Invio.
        
            IIS:\>Restart-WebAppPool MSExchangeAutodiscoverAppPool
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            iisreset /noforce
    
      - Utilizzo di Gestione Internet Information Services (IIS): In Gestione Internet Information Services (IIS), nel riquadro **Azioni**, fare clic su **Riavvia**.

Torna all'inizio

## Configurazione della ripartizione del carico di lavoro SSL per il servizio proxy Replica cassette postali (MRSProxy)

Il servizio Proxy replica delle cassette postali (MRSProxy) viene installato in tutti i server Accesso Client di Exchange 2013. Proxy Mrs consente di rendere spostamento tra foreste richieste locali e su come spostare le cassette postali locali a Office 365. Tuttavia, per impostazione predefinita, proxy Mrs è disabilitata. Se si sta abilitando, è consigliabile abilitare nella foresta di Exchange remota per più foreste, spostamenti delle cassette postali locale o nella foresta di Exchange locale per lo spostamento di una cassetta postale in Office 365. Anche se in servizi Web Exchange (EWS) viene eseguito il servizio proxy Mrs, non è supportato per configurare offload SSL.

Questo perché il servizio MRSProxy si aspetta che il traffico sia firmato o crittografato. Ogni sistema di bilanciamento del carico hardware e ogni firewall devono crittografare il traffico MRSProxy prima di inviarlo ai server Accesso client. In questo caso, per far funzionare la ripartizione del carico di lavoro SSL, si consiglia di configurare il bridging SSL.

**Inverso SSL o Bridging SSL**   Se si abilita inverso SSL o SSL bridging in servizi di bilanciamento del carico hardware, non sarà necessario eseguire la procedura precedente in ogni server accesso client. Abilitazione di SSL inverso nei servizi di bilanciamento del carico hardware, tuttavia, significa che la decrittografia e la crittografia SSL resterà con i server Accesso Client. In questo caso, la crittografia e decrittografia SSL verificherà in servizi di bilanciamento del carico hardware e i server Accesso Client. Se si sceglie di utilizzare Exchange 2013 SSL inverso o offload SSL (bridging SSL) dipende gli obiettivi organizzativi e consigliate per la protezione che devono essere implementati. Nella figura riportata di seguito viene illustrata la connettività dei client con SSL bridging (SSL Secure inverso) abilitato.

![Bridging SSL](images/Dn635115.a08aacc1-0ab4-46b3-bdae-b9518a3f5748(EXCHG.150).jpg "Bridging SSL")

## Configurazione della ripartizione del carico di lavoro SSL per client Outlook (directory virtuale MAPI)

Per abilitare la ripartizione del carico di lavoro SSL per i client Outlook, è necessario rimuovere il requisito SSL sulla directory virtuale **MAPI** sul **Sito Web predefinito**:

  - **Passaggio 1**   È possibile utilizzare Gestione Internet Information Services (IIS) o una riga di comando per disabilitare SSL sulla directory virtuale **MAPI**:
    
      - Utilizzando Gestione Internet Information Services (IIS), espandere **Siti** \> **Sito Web predefinito**, quindi selezionare la directory virtuale **MAPI**. Nel riquadro dei risultati, in **IIS**, fare doppio clic su **Impostazioni SSL**. Nel riquadro dei risultati **Impostazioni SSL**, deselezionare la casella di controllo **Richiesta SSL**, quindi fare clic su **Applica** nel riquadro **Azioni**.
    
      - Utilizzando la riga di comando, digitare quanto segue e premere Invio.
        
            appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST

  - **Passaggio 2**   È necessario riavviare il pool di applicazioni corretto o Internet Information Services adottando uno dei metodi seguenti:
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            appcmd Recycle AppPool MSExchangeMapiFrontEndAppPool
    
      - Utilizzando un cmdlet di Windows PowerShell, digitare quanto segue e premere Invio.
        
            IIS:\>Restart-WebAppPool MSExchangeMapiFrontEndAppPool
    
      - Utilizzo di una riga di comando: Andare a **Start** \> **Esegui**, digitare **cmd** e premere Invio. Nella finestra del prompt dei comandi, digitare quanto segue e premere Invio.
        
            iisreset /noforce
    
      - Utilizzo di Gestione Internet Information Services (IIS): In Gestione Internet Information Services (IIS), nel riquadro **Azioni**, fare clic su **Riavvia**.

Torna all'inizio

## Utilizzo di uno script per abilitare la ripartizione del carico di lavoro SSL per tutti i protocolli e servizi

Se si lavora con una grande organizzazione non più server Accesso client Exchange 2013, può essere utile velocizzare i passaggi precedenti. È possibile copiare e incollare i comandi in uno dei seguenti script in Blocco note, apportare eventuali modiche, salvare il file con estensione .ps1 ed eseguirlo di nuovo da Exchange Management Shell. A seconda della particolari esigenze, entrambi gli script possono essere utilizzati per configurare la ripartizione del carico di lavoro SSL per tutti i protocolli e i servizi per un singolo server o più server Accesso client.


> [!NOTE]
> Le voci di cmdlet <STRONG>Set-OutlookAnywhere</STRONG> , sostituire "MyServer" con il nome del proprio server Accesso Client.



**Utilizzo di Set-WebConfigurationProperty**

    Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
    Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS:  -Location "Default Web Site/OWA"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/ecp"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/EWS"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Autodiscover"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Microsoft-Server-ActiveSync"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/OAB"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/MAPI"
    iisreset /noforce

**Utilizzo di appcmd**


> [!NOTE]
> Le voci di cmdlet <STRONG>Set-OutlookAnywhere</STRONG> , sostituire "MyServer" con il nome del proprio server Accesso Client.



    Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
    Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Autodiscover" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST
    iisreset /noforce

Torna all'inizio

## Configurazione della coesistenza con Exchange 2007 ed Exchange 2010

In uno scenario di coesistenza in cui nell'organizzazione sono presenti server Exchange 2003 ed Exchange 2010, uno dei primi passaggi da eseguire dopo la distribuzione dei server Accesso client di Exchange 2010 è la modifica del DNS in modo che gli utenti di Exchange 2003 possano accedere alle proprie cassette postali da un gruppo di server Accesso client di Exchange 2010. In un tale scenario, è possibile abilitare la ripartizione del carico di lavoro SSL sul sistema di bilanciamento del carico utilizzato per distribuire il traffico client tra i server Accesso client.

**Coesistenza con altre versioni di Outlook Web App**

Con la ripartizione del carico di lavoro SSL configurata sui server Accesso client di Exchange 2013, la coesistenza funziona con Exchange 2007 ed Exchange 2010:

  - Per la coesistenza con Exchange 2007, è necessario uno spazio dei nomi precedente, e il reindirizzamento a tale spazio dei nomi si verifica solo per Outlook Web App e Servizi Web Exchange. Individuazione automatica, Outlook Anywhere ed Exchange ActiveSync saranno passati tramite proxy alle versioni precedenti.

  - Per la coesistenza con Exchange 2010, se sono impostati più URL esterni, verrà utilizzato un reindirizzamento. In caso contrario, sarà utilizzato un proxy.

Torna all'inizio


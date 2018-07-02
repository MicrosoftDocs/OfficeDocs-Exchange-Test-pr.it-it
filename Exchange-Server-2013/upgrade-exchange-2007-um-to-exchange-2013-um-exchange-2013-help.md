---
title: "Eseguire l'aggiornamento alla messaggistica UNIFICATA di Exchange 2007 a messaggistica UNIFICATA di Exchange 2013: Exchange 2013 Help"
TOCTitle: Eseguire l'aggiornamento alla messaggistica UNIFICATA di Exchange 2007 a messaggistica UNIFICATA di Exchange 2013
ms:assetid: 642c922d-7e85-40f0-bb9b-0f20da692be3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn169227(v=EXCHG.150)
ms:contentKeyID: 54652871
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eseguire l'aggiornamento alla messaggistica UNIFICATA di Exchange 2007 a messaggistica UNIFICATA di Exchange 2013

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Quando si esegue l'aggiornamento di un'organizzazione di Microsoft Exchange 2007 tramite la messaggistica unificata alla messaggistica unificata di Exchange 2013, è necessario seguire alcuni passaggi e accertarsi che altri siano già completati come parte della distribuzione di messaggistica unificata di Exchange 2007. A seconda dell'ambiente di telefonia e dei componenti di messaggistica unificata creati e configurati per supportare la messaggistica unificata in Exchange 2007, potrebbe essere necessario distribuire ulteriori apparecchiature telefoniche, inclusi gateway VoIP, IP PBX o classici PBX abilitati per SIP in modo da creare e configurare eventuali componenti di messaggistica unificata richiesti per la messaggistica unificata di Exchange 2013.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 45-90 minuti.

  - Verificare di disporre delle autorizzazioni appropriate per l'organizzazione di Exchange 2007 ed Exchange 2013 per creare e configurare tutti i componenti richiesti.

  - Verificare di aver distribuito e configurato correttamente i componenti telefonici inclusi gateway VoIP, PBX, IP PBX o PBX per SIP.

  - Verificare l'installazione e la configurazione corrette dei server Accesso client in cui è in esecuzione il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange e i server Cassette postali in cui è in esecuzione il servizio di messaggistica unificata di Microsoft Exchange. Per ulteriori informazioni sui servizi di messaggistica unificata, vedere [Servizi di messaggistica unificata](um-services-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Come eseguire l'operazione

## Passaggio 1: Scaricare e installare i Language Pack di messaggistica unificata necessari

I Language Pack di messaggistica unificata consentono ai chiamanti e agli utenti di Outlook Voice Access di interagire con il sistema di caselle vocali in più lingue. Dopo avere installato una lingua supplementare in un server Cassette postali di Exchange 2013, i chiamanti e gli utenti di Outlook Voice Access sono in grado di ascoltare i messaggi di posta elettronica e interagire con il sistema di caselle vocali nella lingua specificata. Tuttavia, per rendere la lingua disponibile per tutte le chiamate in entrata, è necessario installare i necessari Language Pack di messaggistica unificata su tutti i server Cassette postali di Exchange 2013. Ciò consente a tutti i server Cassette postali di Exchange 2013 di rispondere alle chiamate in entrata per la messaggistica unificata.

Per impostazione predefinita, quando si installa un server Cassette postali di Exchange 2013, viene installato il Language Pack per inglese americano (en-US). Questa è l'unica lingua disponibile per il dial plan se non si installa un altro Language Pack di messaggistica unificata. Non è possibile rimuovere la lingua inglese americano (en-US), a meno che non venga rimosso il server Cassette postali dal computer. Una volta installato un Language Pack di messaggistica unificata su un server Cassette postali di Exchange 2013, la lingua associata al Language Pack viene elencata come opzione disponibile durante la configurazione della lingua predefinita per il dial plan. Poiché un operatore automatico di messaggistica unificata è legato a un dial plan di messaggistica unificata quando viene creato l'operatore automatico, per impostazione predefinita utilizza l'impostazione della lingua predefinita del dial plan di messaggistica unificata collegato. Tuttavia, è possibile modificare questa impostazione dopo avere creato l'operatore automatico di messaggistica unificata.


> [!NOTE]
> Se l'inglese americano è l'unica lingua che si desidera sia disponibile per il dial plan, ignorare questo passaggio e procedere al passaggio 2.



È possibile aggiungere i language pack di messaggistica UNIFICATA utilizzando il comando setup.exe oppure eseguendo il programma di installazione .exe *\<UMLanguagePack\>*dopo aver scaricato il language pack di messaggistica UNIFICATA di [Exchange Server 2013 messaggistica UNIFICATA di Language Pack](https://go.microsoft.com/fwlink/p/?linkid=266542). Per ulteriori informazioni, vedere [Installare un Language Pack di messaggistica unificata](install-a-um-language-pack-exchange-2013-help.md).

In questo esempio viene utilizzato il comando setup.exe per installare il Language Pack di messaggistica unificata per il giapponese (ja-JP).

    setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

## Passaggio 2: Spostare i messaggi di saluto, annunci, istruzioni di menu personalizzati di Exchange 2007 nella cassetta postale di sistema di Exchange 2013.

I messaggi di saluto, gli annunci e le istruzioni di menu personalizzati vengono utilizzati dai dial plan e dagli operatori automatici di messaggistica unificata. La cassetta postale di sistema {e0dc1c29-89c3-4034-b678-e6c29d823ed9} viene creata quando si installa Exchange 2007 o Exchange 2013 e viene utilizzata per supportare funzionalità quali Approvazione messaggi e Ricerca in più cassette postali. Questa cassetta postale di sistema è inoltre utilizzata per archiviare i messaggi di saluto, gli annunci e le istruzioni di menu personalizzati dei dial plan e degli operatori automatici. Se la cassetta postale di sistema non esiste, è possibile utilizzare il comando **Setup /PrepareAD** per crearla.

Per impostazione predefinita, le cassette postali di sistema non sono visibili nell'interfaccia di amministrazione di Exchange. È possibile ottenere un elenco delle cassette postali di sistema eseguendo una delle seguenti operazioni:

In questo esempio viene visualizzato un elenco di tutti le cassette postali di sistema.

    Get-Mailbox -Arbitration

Con questo comando viene visualizzato un elenco di cassette postali di sistema e le relative singole proprietà o impostazioni.

    Get-Mailbox -Arbitration |fl

Quando si stanno importando messaggi di saluto, annunci e istruzioni del menu personalizzati da Exchange 2007 su Exchange 2013, è necessario utilizzare lo script MigrateUMCustomPrompts.ps1. Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per importare i saluti, gli annunci e le istruzioni di menu personalizzati. Lo script MigrateUMCustomPrompts.ps1 migra una copia di tutti i saluti, gli annunci e le istruzioni di menu personalizzati della messaggistica unificata di Exchange Server 2007 sulla messaggistica unificata di Exchange 2013. Per impostazione predefinita, lo script MigrateUMCustomPrompts.ps1 si trova nella cartella *\<Program Files\>*\\Microsoft\\Exchange Server\\V15\\Scripts in un server Cassette postali di Exchange 2013 ed è necessario eseguirlo da un server Cassette postali di Exchange 2013. Per eseguire lo script:

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Exchange Server 2013** \> **Exchange Management Shell**.

2.  In Exchange Management Shell, al prompt, digitare il percorso dello script. Ad esempio, digitare **cd "D:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts"**, quindi premere Invio.

3.  Al prompt di Shell digitare **".\\MigrateUMCustomPrompt"**, quindi premere Invio.


> [!NOTE]
> È possibile importare individualmente prompt personalizzati utilizzando il cmdlet <STRONG>Import-UMPrompt</STRONG>. Il cmdlet di messaggistica unificata <STRONG>Copy-UMCustomPrompt</STRONG> di Exchange 2007 non è supportato per copiare prompt personalizzati sulla messaggistica unificata di Exchange 2013.



Quando si utilizza lo script MigrateUMCustomPrompts.ps1 dal server di Exchange 2013, lo script esegue un GUID o un oggetto identificatore di ricerca del dial plan o dell'operatore automatico in Active Directory e li interroga per determinare se esistano messaggi di saluto, annunci, istruzioni del menu personalizzati. Nel caso esistano, saranno importati nella cassetta postale di sistema visualizzata col nome {e0dc1c29-89c3-4034-b678-e6c29d823ed9}.

Utilizzando una cassetta postale di sistema, è possibile effettuare il backup di messaggi di saluto, annunci, istruzioni del menu personalizzati e ripristinarli assieme ad altre cassette postali in un database. Questo riduce la quantità di risorse necessarie. L'archiviazione di messaggi di saluto, annunci, menu e prompt personalizzati in una cassetta postale di sistema elimina eventuali incongruenze che possono verificarsi. Per ulteriori informazioni sugli spostamenti delle cassette postali, vedere [Spostamenti di cassette postali di Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

## Passaggio 3: Esportare e importare i certificati

Se si utilizza SIP o dial plan protetti nell'organizzazione di Exchange 2007, è necessario esportare e importare i certificati che sono stati utilizzati per i server di Accesso client e Cassette postali di Exchange 2013. Mutual Transport Layer Security (protezione livello trasporto reciproca) viene utilizzata per crittografare i dati inviati tra i server di Exchange 2013 e i gateway VoIP, IP PBX e PBX abilitato per SIP. I certificati associano l'identità del proprietario del certificato a una coppia di chiavi elettroniche (pubbliche e private) che vengono utilizzate per la crittografia e la firma digitale. È possibile utilizzare uno dei seguenti certificati per i servizi di routing delle chiamate di messaggistica unificata e per la messaggistica stessa:

  - Un certificato auto-firmato (Exchange)

  - Un certificato di un'infrastruttura a chiave pubblica

  - Un certificato commerciale di terze parti

Per impostazione predefinita, quando si installa Exchange 2013, vengono creati due certificati autofirmati: **Microsoft Exchange Server Auth Certificate** e **Microsoft Exchange**. Il certificato autofirmato **Microsoft Exchange** viene utilizzato per consentire alla messaggistica unificata di crittografare i dati, ma è necessario assegnare il certificato ai servizi di routing per le chiamate di messaggistica unificata e alla messaggistica stessa. Questo certificato autofirmato può essere copiato e poi importato sui gateway VoIP, IP PBX e PBX per SIP. Tuttavia, non è possibile essere utilizzarlo quando è in esecuzione l'integrazione della messaggistica unificata con Microsoft Lync Server.

Per l'abilitazione della messaggistica unificata per crittografare i dati inviati tra i server di Exchange 2013 e i gateway VoIP, IP PBX e PBX per SIP, è necessario effettuare le seguenti operazioni:

  - Utilizzare un certificato di messaggistica unificata autofirmato esistente, creare un nuovo certificato di Exchange autofirmato, inviare una richiesta di certificato a un'autorità di certificazione interna per un certificato di un'infrastruttura a chiave pubblica oppure acquistare un certificato commerciale di terze parti che è possibile utilizzare per la TLS reciproca tra i server Cassette postali e Accesso client di Exchange 2013 e i gateway VoIP, IP PBX e PBX per SIP.
    
    Creare un certificato autofirmato di Exchange utilizzando l'interfaccia di amministrazione di Exchange, come segue:
    
    1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Certificati**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").
    
    2.  Nella pagina **Nuovo certificato di Exchange** scegliere **Crea un certificato autofirmato**, quindi selezionare **Avanti**.
    
    3.  Immettere un nome descrittivo per il certificato, quindi selezionare **Avanti**.
    
    4.  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per selezionare i server di Exchange a cui si intende applicare questo certificato, quindi selezionare **Avanti**.
    
    5.  Specificare i domini che si intendono includere nel certificato, quindi selezionare **Avanti**. Per aggiungere un dominio per un servizio, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    
    6.  Verificare che i domini inclusi siano corrette, quindi selezionare **Fine**.
    

    > [!IMPORTANT]
    > Quando si utilizza l'interfaccia di amministrazione di Exchange per creare un certificato, non viene chiesto di attivare alcun servizio per il certificato stesso. Una volta creato il certificato, è possibile utilizzare l'interfaccia di amministrazione di Exchange per abilitare i servizi. Per ulteriori informazioni su come abilitare un certificato per i servizi, vedere <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Assegnare un certificato per i servizi di messaggistica unificata e routing delle chiamate di messaggistica unificata</A>.

    
    Creazione di un certificato autofirmato di Exchange eseguendo il seguente comando in Shell.
    
        New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true
    

    > [!TIP]
    > Se si specificano i servizi che si intende attivare utilizzando il parametro <EM>Services</EM>, viene richiesto di abilitare i servizi per il certificato creato. In questo esempio viene richiesto di abilitare il certificato per la messaggistica unificata e per i servizi di routing per le chiamate di messaggistica unificata. Per ulteriori informazioni su come abilitare un certificato per i servizi, vedere <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Assegnare un certificato per i servizi di messaggistica unificata e routing delle chiamate di messaggistica unificata</A>.



  - Importare il certificato che viene utilizzato su tutti i server Accesso client e Cassette postali di Exchange 2013 nell'organizzazione. Se si utilizza il certificato autofirmato di Exchange 2013, è necessario copiare il certificato, quindi importarlo sul gateway VoIP, IP PBX o PBX per SIP. Se si utilizza il certificato auto-firmato da Exchange 2007, il nome alternativo del soggetto deve contenere i nomi della macchina di tutti i server di Exchange 2013. Se si dispone di server di messaggistica unificata di Exchange 2007 nell'organizzazione, è possibile utilizzare un certificato autofirmato di Exchange 2013, ma è necessario aggiungere i nomi delle macchine dei server di messaggistica unificata di Exchange 2007 per il nome alternativo del soggetto nel certificato di Exchange 2013.

  - Abilitare o assegnare il certificato da utilizzare per i servizi routing per le chiamate di messaggistica unificata e per la messaggistica unificata su server di Accesso client e Cassette postali nell'organizzazione.
    
    Abilitare i servizi di messaggistica unificata e di routing per le chiamate di messaggistica unificata su tutti i server di Exchange 2013 per utilizzare il certificato autofirmato di Exchange utilizzando l'interfaccia di amministrazione di Exchange, come segue:
    
    1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Certificati**, selezionare il certificato abilitato per i servizi, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    
    2.  Nella pagina **Procedura** selezionare **Servizi**, scegliere **Messaggistica unificata**, quindi selezionare **Routing di chiamata di messaggistica unificata**.
    
    Abilitare un certificato auto-firmato eseguendo il seguente comando in Shell.
    
        Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'

  - Configurare eventuali nuovi o esistenti dial plan di messaggistica unificata come protetti con SIP o protetti.

  - Configurare la modalità di avvio di messaggistica unificata in TLS o Dual su server Accesso client e Cassette postali nell'organizzazione.

  - Creare e configurare nuovi o esistenti gateway IP di messaggistica unificata con un nome di dominio completo.

  - Configurare la porta di attesa sui gateway IP di messaggistica unificata per utilizzare la porta TLS 5061.

  - Riavviare il servizio router di chiamata di messaggistica unificata su tutti i server Accesso client di Exchange 2013 e riavviare il servizio di messaggistica unificata su tutti i server Cassette postali di Exchange 2013. Per ulteriori informazioni sui servizi di messaggistica unificata, vedere [Servizi di messaggistica unificata](um-services-exchange-2013-help.md).

## Passaggio 4: Configurare la modalità di avvio di messaggistica unificata su tutti i server Accesso client di Exchange 2013

Se si utilizzano dial plan protetti o Sip protetto, è necessario configurare la modalità di avvio di messaggistica unificata sui server Accesso client di Exchange 2013. È possibile specificare la modalità di avvio di messaggistica unificata per il servizio router di chiamata di messaggistica unificata su un server Accesso client di Exchange 2013 utilizzando l'interfaccia di amministrazione o Shell. Per impostazione predefinita, il server Accesso client di Exchange 2013 si avvia in modalità TCP, ma se si sta utilizzando Transport Layer Security (TLS) per crittografare il traffico VoIP è necessario configurare il server Accesso client di Exchange 2013 al fine di utilizzare la modalità TLS o Dual. Si consiglia di configurare tutti i server Accesso client di Exchange 2013 al fine di utilizzare Dual in modalità di avvio di messaggistica unificata. Ciò si verifica perché tutti i server Accesso client di Exchange 2013 rispondono alle chiamate in entrata per tutti i dial plan di messaggistica unificata, ma tali dial plan possono avere impostazioni di protezione diverse. Se si modifica la modalità di avvio di messaggistica unificata, è necessario riavviare il servizio router di chiamata di messaggistica unificata affinché le modifiche abbiano effetto. Per ulteriori informazioni sui servizi di messaggistica unificata, vedere [Servizi di messaggistica unificata](um-services-exchange-2013-help.md).

Configurare la modalità di avvio di messaggistica unificata in un server Accesso client di Exchange 2013 utilizzando l'interfaccia di amministrazione di Exchange, come segue:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server di Exchange che si intende modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Server di Exchange**, fare clic su **Messaggistica unificata**.

4.  In **impostazioni del router di chiamata di messaggistica unificata** \> **modalità di avvio di messaggistica unificata**, selezionare una delle seguenti operazione dall'elenco a discesa:
    
      - **TCP**   Utilizzare questa opzione se non si utilizza MTLS ma esclusivamente i dial plan non protetti.
    
      - **TLS**   Utilizzare questa opzione se si utilizza MTLS ed esclusivamente dial plan e SIP protetti.
    
      - **DUAL**   Utilizzare questa opzione se si utilizza MTLS e dial plan protetti, non protetti e SIP protetto.

5.  Dopo aver selezionato la modalità di avvio di messaggistica unificata, fare clic su **Salva**.

Configurare la modalità di avvio di messaggistica unificata su un server Accesso client di Exchange 2013 tramite l'esecuzione del seguente comando in Shell.

    Set-UMCallRouterSettings -Server MyUMCallRouter.northwindtraders.com -UMStartupMode Dual

## Passaggio 5: Configurare la modalità di avvio di messaggistica unificata su tutti i server Cassette postali di Exchange 2013

Se si utilizza SIP o dial plan protetti, è necessario configurare la modalità di avvio di messaggistica unificata sui server Cassette postali di Exchange 2013. È possibile specificare la modalità di avvio di messaggistica unificata per il servizio di messaggistica unificata su un server Cassette postali di Exchange 2013 utilizzando l'interfaccia di amministrazione di Exchange o Shell. Per impostazione predefinita, il server Cassette postali di Exchange 2013 si avvia in modalità TCP, ma se si utilizza Transport Layer Security (TLS) per crittografare il traffico VoIP, è necessario configurare il server Cassette postali per la modalità TLS o Dual. Si consiglia di configurare i server Cassette postali per l'utilizzo di Dual in modalità di avvio di messaggistica unificata. Ciò si verifica perché tutti i server Cassette postali rispondono alle chiamate in entrata per tutti i dial plan di messaggistica unificata, ma tali dial plan possono avere impostazioni di protezione diverse. Se si modifica la modalità di avvio di messaggistica unificata, è necessario riavviare il servizio di messaggistica unificata affinché le modifiche abbiano effetto. Per ulteriori informazioni sui servizi di messaggistica unificata, vedere [Servizi di messaggistica unificata](um-services-exchange-2013-help.md).

Configurare la modalità di avvio di messaggistica unificata su un server Cassette postali di Exchange 2013 tramite l'interfaccia di amministrazione di Exchange, come segue:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server Exchange che si intende modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Server di Exchange**, scegliere **Messaggistica unificata**.

4.  In **Impostazioni del servizio di messaggistica unificata** \> **Modalità di avvio di messaggistica unificata**, selezionare una delle seguenti operazioni dall'elenco a discesa:
    
      - **TCP**   Utilizzare questa opzione se non si utilizza MTLS e si utilizzano esclusivamente i dial plan protetti.
    
      - **TLS**   Utilizzare questa opzione se si utilizza MTLS ed esclusivamente SIP e dial plan protetti.
    
      - **DUAL**   Utilizzare questa opzione se si utilizza MTLS e non dial plan, protetti, non protetti e SIP con protezione.

5.  Dopo aver selezionato la modalità di avvio di messaggistica unificata, fare clic su **Salva**.

Configurare la modalità di avvio di messaggistica unificata su un server Cassette postali di Exchange 2013 tramite l'esecuzione del seguente comando in Shell.

    Set-UMService -Identity MyUMServer -ExternalHostFqdn host.external.contoso.com -IPAddressFamily Any -UMStartupMode Dual

## Passaggio 6: Creare o configurare i dial plan di messaggistica unificata esistenti

A seconda della distribuzione di Exchange 2007 esistente, potrebbe essere necessario creare nuovi dial plan di messaggistica unificata o configurare i dial plan esistenti. I dial plan di messaggistica unificata rappresentano un insieme di sistemi PBX (Private Branch eXchange) per SIP o IP PBX che condividono i numeri di interni comuni dell'utente. Gli interni di tutti gli utenti ospitati su PBX per SIP o IP PBX all'interno di un dial plan contengono lo stesso numero di cifre. Gli utenti possono chiamarsi digitando il numero dell'interno senza aggiungere un numero particolare o digitare un numero di telefono completo.

I dial plan di messaggistica unificata vengono utilizzati nella messaggistica unificata per garantire che i numeri di interno degli utenti siano univoci. In alcune reti di telefonia, esistono diversi sistemi IP PBX, PBX tradizionali o PBX per SIP. In tali reti di telefonia possono essere presenti due utenti il cui numero di interno telefonico è identico. I dial plan di messaggistica unificata consentono di risolvere una situazione simile. L'inserimento di due utenti in due dial plan di messaggistica unificata separati rende univoci i loro numeri di interno. Per ulteriori informazioni, vedere [Dial plan di messaggistica unificata](um-dial-plans-exchange-2013-help.md).

Se necessario, è possibile creare un dial plan di messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange:

1.  Nell'interfaccia di amministrazione di Exchange accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**, quindi fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella pagina **Nuovo dial plan di messaggistica unificata**, completare quanto segue:
    
      - **Nome**°°°Digitare il nome del dial plan. Il nome del dial plan di messaggistica unificata è obbligatorio e deve essere univoco. Tuttavia, il nome digitato viene viene utilizzato esclusivamente per scopi di visualizzazione nell'interfaccia di amministrazione di Exchange e in Shell. La lunghezza massima per il nome di un dial plan di messaggistica unificata è di 64 caratteri e può contenere spazi. Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        Anche se la casella per il nome del dial plan può contenere fino a 64 caratteri, il nome del dial plan non può superare i 49 caratteri. Se si cerca di creare un nome di dial plan che contiene più di 49 caratteri, verrà visualizzato un messaggio di errore. Il messaggio riporta che il criterio della cassetta postale messaggistica unificata non ha potuto essere generato poiché il nome del dial plan di messaggistica unificata è eccessivamente lungo. Infatti, quando viene creato un dial plan, viene creato anche un criterio cassetta postale di messaggistica unificata predefinito con il nome *\<DialPlanName\>***Criterio predefinito**. Quando i 15 caratteri nel criterio predefinito vengono aggiunti al nome del dial plan, i caratteri totali superano il limite. Il parametro *name* può contenere 64 caratteri per il dial plan e il criterio cassetta postale di messaggistica unificata. Tuttavia, se il nome del dial plan è più lungo di 49 caratteri, il nome del criterio cassetta postale di messaggistica unificata predefinito sarà più lungo di 64 caratteri e il sistema non lo consente.
    
      - **Lunghezza numero di interno (cifre)** Immettere il numero di cifre per i numeri di interni nel dial plan. Il numero di cifre dei numeri di interno è basato sul dial plan di telefonia creato su un sistema PBX. Ad esempio, se un utente associato a un dial plan di telefonia compone un numero di interno di quattro cifre per chiamare un altro utente nello stesso dial plan, occorre selezionare 4 come numero di cifre dell'interno.
        
        È una casella obbligatoria il cui intervallo di valori è compreso tra 1 e 20. La lunghezza tipica dell'interno è compresa tra 3 e 7 numeri. Se l'ambiente di telefonia esistente contiene numeri di interni, è necessario specificare un numero di cifre che corrisponda al numero di cifre di quegli interni.
        
        Quando si crea un dial plan per gli interni telefonici, è necessario immettere un numero di interno per l'utente quando è collegato al dial plan dell'interno telefonico. Anche con i dial plan SIP o E.164 è necessario un numero di interno quando un utente abilitato alla messaggistica unificata è collegato a un dial plan URI SIP o E.164. Questo numero di interno viene utilizzato dagli utenti di Outlook Voice Access per accedere alla cassetta postale di Exchange.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Tipo di UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Sicurezza UI\_VoIP)
    
      - **Codice paese**   Utilizzare questa casella per digitare il numero del codice paese utilizzato per le chiamate in uscita. Questo numero verrà anteposto automaticamente al numero di telefono composto. La casella consente di immettere da 1 a 4 cifre. Ad esempio, negli Stati Uniti il codice paese è 1, nel Regno Unito è 44.

3.  Fare clic su **Salva**.

Se necessario, è possibile creare un dial plan di messaggistica unificata tramite l'esecuzione del seguente comando in Shell.

    New-UMDialplan -Name MyUMDialPlan -URIType E164 -NumberOfDigitsInExtension 5 -VoIPSecurity Secured

Se necessario, è possibile configurare un dial plan di messaggistica unificata esistente utilizzando l'interfaccia di amministrazione di Exchange:

1.  Nell'interfaccia di amministrazione di Exchange, passare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera visualizzare o modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Nuovo dial plan di messaggistica unificata** fare clic su **Configura**. Utilizzare le opzioni di configurazione per visualizzare le impostazioni specifiche di dial plan e per abilitare o disabilitare le funzionalità.

Se necessario, è possibile configurare un dial plan di messaggistica unificata esistente tramite l'esecuzione del seguente comando in Shell.

    Set-UMDialplan -Identity MyDialPlan -AccessTelephoneNumbers 4255551234 -AudioCodec Wma -CallAnsweringRulesEnabled $false -OutsideLineAccessCode 9 -VoIPSecurity SIPSecured

Quando veniva distribuita la messaggistica unificata di Exchange 2007, era richiesto di aggiungere un server di messaggistica unificata a un dial plan di messaggistica unificata per rispondere alle chiamate in entrata. Ciò non è più necessario. In Exchange 2013, i server Accesso client e Cassette postali non possono essere collegati a un interno telefonico o un dial plan E.164, ma è necessario collegarli ai dial plan URI SIP. I server Accesso client e Cassette postali risponderanno alle chiamate in arrivo per tutti i tipi di dial plan.

## Passaggio 7: Creare e configurare i gateway IP di messaggistica unificata

A seconda della distribuzione di Exchange 2007 esistente, potrebbe essere necessario creare nuovo gateway IP di messaggistica UNIFICATA o configurare i quelli esistenti. Se si utilizza SIP con protezione o Secured plan di messaggistica unificata, è necessario creare un gateway IP di messaggistica UNIFICATA con un FQDN e utilizzo della Shell per configurarlo per l'ascolto sulla porta 5061. Per i gateway IP di messaggistica UNIFICATA esistente, verificare che è configurati con un nome di dominio COMPLETO e che siano in ascolto sulla porta 5061. Se il gateway IP di messaggistica UNIFICATA non utilizza un nome di dominio COMPLETO, è possibile utilizzare EAC o Shell per modificare l'indirizzo. Se il gateway IP di messaggistica UNIFICATA non utilizza la porta 5061, utilizzare la Shell per modificare la porta. È possibile visualizzare le impostazioni di un gateway IP di messaggistica UNIFICATA utilizzando il cmdlet **Get-UMIPGateway** .

Un gateway IP di messaggistica unificata rappresenta un un gateway fisico VoIP, un PBX o un PBX per SIP. Prima che un gateway VoIP, un IP-PBX o un PBX per SIP possano essere utilizzato per rispondere alle chiamate in entrata e inviare chiamate in uscita per gli utenti della casella vocale, è necessario creare un gateway IP di messaggistica unificata nel servizio directory.

La combinazione del gateway IP di messaggistica unificata e di un gruppo di risposta di messaggistica unificata stabilisce un collegamento tra un gateway VoIP, IP PBX, o PBX abilitato per SIP e un dial plan di messaggistica unificata. Se si creano più gruppi di risposta di messaggistica unificata è possibile associare un singolo gateway IP di messaggistica unificata a più dial plan di messaggistica unificata. Per ulteriori informazioni, vedere [Gateway IP di messaggistica unificata](um-ip-gateways-exchange-2013-help.md).

Se necessario, è possibile creare un gateway IP di messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange, come segue:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella pagina **Nuovo gateway IP di messaggistica unificata** immettere le informazioni seguenti:
    
      - **Nome**   Utilizzare questa casella per specificare un nome univoco per il gateway IP di messaggistica unificata. Si tratta del nome che verrà visualizzato nell'interfaccia di amministrazione di Exchange. Qualora fosse necessario modificare il nome visualizzato del gateway IP di messaggistica unificata dopo la sua creazione, occorre innanzitutto eliminare il gateway IP di messaggistica unificata esistente e, quindi, crearne un altro con il nome corretto. Benché il nome del gateway IP di messaggistica unificata sia obbligatorio viene utilizzato solo ai fini della visualizzazione. Dal momento che l'organizzazione può utilizzare più gateway IP di messaggistica unificata, si consiglia di utilizzare nomi significativi per ognuno di essi. La lunghezza massima per il nome di un gateway IP di messaggistica unificata è di 64 caratteri e può contenere spazi. Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Indirizzo**   È possibile configurare un gateway IP di messaggistica unificata con un indirizzi IPv4 o IPv6 oppure un nome di dominio completo. Utilizzare questa casella per specificare l'indirizzo IP o il nome di dominio completo configurato sul gateway VoIP o su PBX oppure su PBX abilitato per SIP. Questa casella accetta solo FQDN validi immessi nel formato corretto.
        
        È possibile immettere caratteri alfabetici e numerici. Sono supportati indirizzi IPv4, indirizzi IPv6 e nomi di dominio completi (FQDN). Se si desidera utilizzare TLS tra un gateway IP di messaggistica unificata e un dial plan in funzione in modalità protetta o protetta con SIP, è necessario configurare il gateway IP di messaggistica unificata con un nome di dominio completo. È necessario configurarlo anche per rimanere in ascolto sulla porta 5061 e verificare che un gateway VoIP o un IP PBX siano stati configurati per l'ascolto delle richieste MTLS sulla porta 5061. Per configurare un gateway IP di messaggistica unificata, eseguire questo comando in Shell: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`
        
        Se si utilizza un nome di dominio completo, è inoltre necessario verificare che sia stato correttamente configurato un record host DNS per il gateway VoIP, IP PBX o PBX per SIP affinché il nome host venga risolto in un indirizzo IP. Inoltre, se si utilizza un FQDN anziché un indirizzo IP, e la configurazione DNS per il gateway IP di messaggistica unificata è stata modificata, è necessario disabilitare e quindi abilitare di nuovo il gateway IP di messaggistica unificata per avere la certezza che le informazioni di configurazione del gateway IP di messaggistica unificata vengano aggiornate correttamente.
    
      - **Dial plan di messaggistica unificata**   Fare clic su **Sfoglia** per selezionare il dial plan di messaggistica unificata che si intende associare al gateway IP di messaggistica unificata. Selezionando un dial plan di messaggistica unificata da associare a un gateway IP di messaggistica unificata, viene inoltre creato un gruppo di risposta di messaggistica unificata predefinito associato al dial plan di messaggistica unificata selezionato. Se non si seleziona alcun dial plan di messaggistica unificata, sarà necessario creare manualmente un gruppo di risposta di messaggistica unificata e successivamente associarlo al gateway IP di messaggistica unificata creato.

3.  Fare clic su **Salva**.

Se necessario, è possibile creare un gateway IP di messaggistica unificata eseguendo il seguente comando in Shell.

    New-UMIPGateway -Identity MyUMIPGateway -Address "MyUMIPGateway.contoso.com"

Se necessario, è possibile configurare un gateway IP di messaggistica unificata esistente utilizzando l'interfaccia di amministrazione di Exchange:

1.  Nell'interfaccia di amministrazione di Exchange accedere a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Gateway IP di messaggistica unificata** fare clic su **Configura**. Utilizzare le opzioni di configurazione per visualizzare le impostazioni specifiche del gateway IP di messaggistica unificata e per abilitare o disabilitare le funzionalità.

Se necessario, è possibile configurare un gateway IP di messaggistica unificata esistente, eseguendo il seguente comando in Shell.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## Passaggio 8: Creare un gruppo di risposta di messaggistica unificata

A seconda della distribuzione di Exchange 2007 esistente, potrebbe essere necessario creare nuovi gruppi di risposta di messaggistica unificata. Un gruppo di risposta telefonico consente di distribuire le chiamate telefoniche da un singolo numero a più numeri di interno o di telefono. Nella messaggistica unificata, un gruppo di risposta di messaggistica unificata è una rappresentazione logica di un gruppo di risposta telefonico e collega un gateway IP di messaggistica unificata a un dial plan di messaggistica unificata.

È necessario disporre di almeno un gruppo di risposta di messaggistica unificata per ciascun gruppo di risposta PBX o PBX IP. Una volta completata la procedura illustrata di seguito, per impostazione predefinita viene creato un gruppo di risposta di messaggistica unificata. Se si hanno più gruppi di risposta PBX o PBX IP, è necessario creare altri gruppi di risposta di messaggistica unificata. Per ulteriori informazioni sui gruppi di risposta di messaggistica unificata, vedere [Gruppi di risposta di messaggistica unificata](um-hunt-groups-exchange-2013-help.md).

Se necessario, è possibile creare un gruppo di risposta di messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange:

1.  Nell'interfaccia di amministrazione di Exchange, passare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Gruppi di risposta di messaggistica unificata**, fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella pagina **Nuovo gruppi di risposta di messaggistica unificata** immettere le informazioni seguenti:
    
      - **Nome**   Utilizzare questa casella per creare il nome visualizzato per il gruppo di risposta di messaggistica unificata. Il nome di un gruppo di risposta di messaggistica unificata è obbligatorio e deve essere univoco, ma viene utilizzato solo per la visualizzazione in EAC e Shell. Se si desidera modificare il nome visualizzato del gruppo di risposta dopo la creazione, è necessario eliminare il gruppo di risposta esistente e crearne uno con il nome desiderato. Se l'organizzazione utilizza più gruppi di risposta, si consiglia di utilizzare nomi significativi per i gruppi di risposta. La lunghezza massima per il nome di un gruppo di risposta di messaggistica unificata è di 64 caratteri e può contenere spazi, Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Gateway IP di messaggistica unificata**   Utilizzare questa casella per selezionare un gateway IP di messaggistica unificata. In questa casella viene visualizzato il nome del gateway IP di messaggistica unificata collegato con il gruppo di risposta di messaggistica unificata. Per collegare un gateway IP di messaggistica unificata al gruppo di risposta di messaggistica unificata, fare clic su **Sfoglia**.
    
      - **Identificatore pilota**   Utilizzare questa casella per specificare una stringa che identifichi in modo univoco l'identificatore pilota configurato per il sistema PBX o IP PBX. In questa casella è possibile utilizzare un numero di interno o un URI (Uniform Resource Identifier) SIP (Session Initiated Protocol). La casella accetta caratteri alfanumerici. Per PBX legacy, si utilizza un valore numerico come identificatore pilota. Tuttavia, alcuni IP PBX e PBX per SIP possono utilizzare URI SIP.

4.  Fare clic su **Salva**.

Se necessario, è possibile creare un gruppo di risposta di messaggistica unificata eseguendo il seguente comando in Shell.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialPlan MyUMDialPlan -UMIPGateway MyUMIPGateway


> [!TIP]
> Non è possibile configurare o modificare le impostazioni per un gruppo di risposta di messaggistica unificata. Per modificare le impostazioni di configurazione per un gruppo di risposta di messaggistica unificata, è necessario eliminarlo e aggiungere un nuovo gruppo di risposta di messaggistica unificata con le impostazioni corrette.



## Passaggio 9: Creare o configurare operatori automatici di messaggistica unificata

A seconda della distribuzione di Exchange 2007 esistente, potrebbe essere necessario creare nuovi operatori automatici di messaggistica unificata. Gli operatori automatici di messaggistica unificata utilizzati per creare un sistema di menu vocali che consentono ai chiamanti interni ed esterni di utilizzare il sistema dei menu degli operatori automatici di messaggistica unificata in modo da individuare utenti e luoghi o trasferire le chiamate agli utenti dell'azienda o ai dipartimenti di un'organizzazione. Per ulteriori informazioni, vedere [Rispondere automaticamente e il routing delle chiamate in arrivo](automatically-answer-and-route-incoming-calls-exchange-2013-help.md).

Nelle distribuzioni di dimensioni ridotte, è possibile che la messaggistica unificata venga distribuita solo per consentire agli utenti di disporre della casella vocale. In queste distribuzioni, non è necessario creare un operatore automatico. Tuttavia, nella maggior parte dei casi, l'utilizzo degli operatori automatici si rivela molto utile in caso di chiamate all'organizzazione da parte di chiamanti esterni.

Se necessario, è possibile creare un operatore automatico di messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange, come segue:

1.  
    
    Nell'interfaccia di amministrazione di Exchange, passare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Selezionare il dial plan di messaggistica unificata in cui aggiungere l'operatore automatico, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata** fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella pagina **Nuovo operatore automatico di messaggistica unificata** completare i seguenti campi:
    
      - **Nome**   Utilizzare questa casella per creare il nome visualizzato per l'operatore automatico di messaggistica unificata. Il nome dell'operatore automatico di messaggistica unificata è obbligatorio e deve essere univoco. Tuttavia, viene utilizzato solo per la visualizzazione in EAC e Shell. Qualora fosse necessario modificare il nome visualizzato dell'operatore automatico dopo che è stato creato, eliminare in primo luogo l'operatore automatico di messaggistica unificata esistente, quindi creare un altro operatore automatico con il nome desiderato. Se nell'organizzazione vengono utilizzati più operatori automatici di messaggistica unificata, si consiglia di utilizzare nomi significativi per gli operatori automatici di messaggistica unificata. La lunghezza massima del nome di un operatore automatico di messaggistica unificata è di 64 caratteri e può contenere spazi.
        
        Anche se a un nuovo operatore automatico di messaggistica unificata è possibile assegnare un nome contenente spazi, è necessario evitare l'uso degli spazi se la messaggistica unificata viene integrata con Lync Server. Di conseguenza, se è stato creato un operatore automatico il cui nome visualizzato contiene degli spazi e la messaggistica unificata viene integrata con Lync Server, è necessario innanzitutto eliminare l'operatore automatico e poi crearne un altro il cui nome visualizzato non contenga spazi.
    
      - **Crea l'operatore automatico come abilitato**   Selezionare questa casella di controllo per consentire all'operatore automatico di rispondere alle chiamate in arrivo al termine della creazione dell'operatore automatico di messaggistica unificata. Il nuovo operatore automatico è disabilitato e creato per impostazione predefinita. Se si decide di visualizzare l'operatore automatico di messaggistica unificata come disabilitato, è possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell per abilitare l'operatore automatico una volta completata creazione.
    
      - **Imposta operatore automatico per rispondere ai comandi vocali**   Selezionare questa casella di controllo per abilitare l'operatore automatico di messaggistica unificata al servizio di sintesi vocale. In questo modo, i chiamanti possono rispondere mediante toni o input vocali ai prompt di sistema o ai prompt personalizzati utilizzati dall'operatore automatico di messaggistica unificata. Per impostazione predefinita, l'operatore automatico non è abilitato al servizio di sintesi vocale quando viene creato. Affinché i chiamanti utilizzino un operatore automatico abilitato alla sintesi vocale in una lingua diversa dall'inglese americano (en-US), è necessario installare il Language Pack di messaggistica unificata appropriato e configurare le proprietà dell'operatore automatico per utilizzare questa lingua. Il Language Pack di messaggistica unificata per l'inglese americano viene installato per impostazione predefinita quando si installa il server Cassette postali di Exchange 2013.
    
      - **Numeri di accesso**   Immettere il numero di interno o i numeri di telefono che i chiamanti utilizzeranno per raggiungere l'operatore automatico. Digitare un numero di telefono o un numero interno nella casella, quindi fare clic su **Aggiungi** per aggiungere il numero all'elenco. Il numero di cifre per il numero di telefono o il numero interno immesso non deve corrispondere quello di un interno configurato per il dial plan di messaggistica unificata associato. In quanto sono consentite chiamate dirette verso gli operatori automatici di messaggistica unificata.
        
        Il numero di interni o i numeri di accesso che è possibile immettere sono illimitati. Tuttavia, è possibile creare il nuovo operatore automatico senza elencare un numero di interno o di telefono. Non è necessario specificare un numero di telefono o un numero interno. È possibile modificare o rimuovere un numero di interno o un identificatore pilota esistente. Per modificare un numero di telefono o un numero interno esistenti, fare clic su **Modifica**. Per rimuovere dall'elenco un numero di telefono o un numero interno esistente, fare clic su **Rimuovi**.

4.  Fare clic su **Salva**.

Se necessario, è possibile creare un operatore automatico di messaggistica unificata eseguendo il seguente comando in Shell.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true -Status Enabled

Se necessario, è possibile configurare un operatore automatico esistente utilizzando l'interfaccia di amministrazione di Exchange:

1.  Nell'interfaccia di amministrazione di Exchange accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata** in **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata che si intende modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). Utilizzare le opzioni di configurazione per visualizzare le impostazioni specifiche dell'operatore automatico e per abilitare o disabilitare la funzionalità.

Se necessario, è possibile configurare un operatore automatico esistente eseguendo il seguente comando in Shell.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true -StaroutToDialPlanEnabled $true

## Passaggio 10: Creare o configurare criteri cassetta postale di messaggistica unificata

A seconda della distribuzione di Exchange 2007 esistente, potrebbe essere necessario creare nuovi criteri cassetta postale di messaggistica unificata o configurare criteri cassetta postale di messaggistica unificata esistente. I criteri cassetta postale di messaggistica unificata sono necessari quando si abilitano utenti per la messaggistica unificata. La cassetta postale di ogni utente abilitato alla messaggistica unificata deve essere collegata a un singolo criterio cassetta postale di messaggistica unificata. Una volta creato un criterio cassetta postale di messaggistica unificata, è possibile associare una o più cassette postali abilitate alla messaggistica unificata al criterio. In questo modo è possibile controllare le impostazioni di protezione del PIN quali il numero minimo di cifre in un PIN o il numero massimo di tentativi di accesso per gli utenti collegati al criterio cassetta postale di messaggistica unificata. Per ulteriori informazioni, vedere [Criteri cassetta postale di messaggistica unificata](um-mailbox-policies-exchange-2013-help.md).

Se necessario, è possibile creare un criterio cassetta postale di messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange:

1.  Nell'interfaccia di amministrazione di Exchange, passare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Criteri cassetta postale messaggistica unificata** fare clic su **Aggiungi**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Nuovo criterio cassetta postale di messaggistica unificata**, nella casella **Nome**, immettere il nome del nuovo criterio cassetta postale di messaggistica unificata.
    

    > [!NOTE]
    > Questa casella di testo consente di specificare un nome univoco per il criterio cassetta postale di messaggistica unificata. Si tratta del nome che verrà visualizzato nell'interfaccia di amministrazione di Exchange. Qualora fosse necessario modificare il nome visualizzato del criterio cassetta postale di messaggistica unificata dopo la relativa creazione, occorre in primo luogo eliminare il criterio cassetta postale di messaggistica unificata esistente e, quindi, crearne un altro con il nome corretto. Non è possibile eliminare un criterio cassetta postale di messaggistica unificata, se tutti gli utenti abilitati alla messaggistica unificata sono associati ad essa. Il nome del criterio cassetta postale di messaggistica unificata è necessario, ma è utilizzato solo per scopi di visualizzazione. Dal momento che l'organizzazione può utilizzare più criteri cassetta postale di messaggistica unificata, si consiglia di utilizzare nomi significativi per ognuno di essi. La lunghezza massima per il nome di un criterio cassetta postale di messaggistica unificata è di 64 caratteri e può contenere spazi. Non può tuttavia contenere i seguenti caratteri: " / \ [ ] : ; | = , + * ? &lt; &gt;.



4.  Fare clic su **Salva**.
    

    > [!NOTE]
    > Quando viene salvato il criterio cassetta postale di messaggistica unificata, vengono abilitate tutte le impostazioni predefinite inclusi i criteri PIN, le funzionalità della posta vocale e le impostazioni del sistema di caselle vocali protette. Per personalizzare o modificare le impostazioni predefinite, utilizzare il cmdlet <STRONG>Set-UMMailbox</STRONG> o l'interfaccia di amministrazione di Exchange che consente di modificare le impostazioni del criterio cassetta postale di messaggistica unificata appena creato.



Se necessario, è possibile creare un criterio cassetta postale di messaggistica unificata in Shell eseguendo il comando seguente.

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

Se necessario, è possibile configurare un criterio cassetta postale di messaggistica unificata esistente utilizzando l'interfaccia di amministrazione di Exchange:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata** e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si intende modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). Utilizzare le opzioni di configurazione per visualizzare le impostazioni specifiche del criterio cassetta postale di messaggistica unificata e per abilitare o disabilitare la funzionalità.

Se necessario, è possibile configurare un criterio di messaggistica unificata esistente, eseguendo il seguente comando in Shell.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

## Passaggio 11: Spostare le cassette postali esistenti abilitate alla messaggistica unificata in Exchange 2013

Nella messaggistica unificata di Exchange 2007, dopo aver abilitato gli utenti all'interno dell'organizzazione alla casella vocale, un insieme di proprietà di messaggistica unificata predefinito viene applicato all'utente in modo da poter utilizzare le funzionalità di messaggistica unificata. Per ulteriori informazioni, vedere [Segreteria telefonica per gli utenti](voice-mail-for-users-exchange-2013-help.md).

Durante il processo di aggiornamento, esiste un periodo di tempo durante il quale saranno disponibili cassette postali di messaggistica unificata abilitate sia sul server Cassette postali di Exchange 2007 che sul server Cassette postali di Exchange 2013. Tuttavia, se si spostano tutti gli utenti abilitati alla messaggistica unificata oltre ai server Cassette postali di Exchange 2013, è necessario utilizzare l'interfaccia di amministrazione di Exchange o il cmdlet **New-MoveRequest** in Shell da un server Exchange 2013 per conservare tutte le proprietà e le impostazioni, compreso il PIN dell'utente.

Una richiesta di spostamento rappresenta il processo di spostamento di una cassetta postale da un database delle cassette postali ad un altro. Una richiesta di spostamento locale è uno spostamento della cassetta postale all'interno di una singola foresta. Per ulteriori informazioni sugli spostamenti della cassetta postale, vedere:

  - [Spostamenti di cassette postali di Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

  - [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\))

  - [New-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219166\(v=exchg.150\))

  - [Spostamento delle cassette postali](https://go.microsoft.com/fwlink/p/?linkid=296351)

Per spostare una cassetta postale di Exchange 2007 a un server Cassette postali di Exchange 2013 tramite l'interfaccia di amministrazione di Exchange:

1.  Nell'interfaccia di amministrazione di Exchange, fare clic su **Destinatari** \> **Migrazione**, quindi fare clic su **Aggiungi**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella procedura guidata per **Nuovo spostamento cassetta postale locale**, selezionare gli utenti che si intendono spostare, fare clic su **OK**, quindi fare clic su **Avanti**.

3.  Nella pagina **Sposta configurazione** specificare un nome per il nuovo batch. Selezionare le opzioni desiderate per la cassetta postale di archiviazione e il percorso del database delle cassette postali, quindi fare clic su **Nuovo**.

Per spostare una cassetta postale di Exchange 2007 a un server Cassette postali di Exchange 2013 utilizzando la Shell, eseguire il seguente comando.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase "DB01"

## Passaggio 12: Abilitare i nuovi utenti per la messaggistica unificata o configurare le impostazioni per un utente abilitato alla messaggistica unificata esistente

Un utente deve avere una cassetta postale prima di poter essere abilitato alla messaggistica unificata. Per impostazione predefinita, un utente che dispone di una cassetta postale non è abilitato alla messaggistica unificata. Una volta abilitato, l'utente potrà gestire, modificare e configurare le proprietà relative alla messaggistica unificata e le funzionalità del sistema di caselle vocali. È possibile abilitare un utente per la messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange o Shell. Per ulteriori informazioni, vedere [Segreteria telefonica per gli utenti](voice-mail-for-users-exchange-2013-help.md).

Quando si abilita un utente alla messaggistica unificata, è necessario definire almeno un numero di interno che la messaggistica unificata utilizza quando la casella vocale viene inviato alla cassetta postale dell'utente e viene consentito all'utente di utilizzare Outlook Voice Access. Dopo aver abilitato l'utente alla messaggistica unificata, è possibile aggiungere numeri secondari di interno alla cassetta postale dell'utente oppure modificarli o rimuoverli configurando l'indirizzo proxy di messaggistica unificata sulla cassetta postale dell'utente oppure aggiungere o rimuovere estensioni aggiuntive o secondarie per l'utente nell'interfaccia di amministrazione di Exchange. Per aggiungere, modificare o rimuovere numeri di interni, numeri E.164 o indirizzi SIP, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

Per abilitare un utente alla messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange:

1.  In Stima al completamento fare clic su **Destinatari**.

2.  Nella visualizzazione Elenco selezionare l'utente che si intende abilitare per la messaggistica unificata.

3.  Nel riquadro Dettagli sotto **Funzionalità telefono e vocali** fare clic su **Abilita**.

4.  Nella pagina **Abilita cassetta postale di messaggistica unificata**, fare clic sul pulsante **Sfoglia** accanto a **Criteri cassetta postale di messaggistica unificata**, individuare nell'elenco il criterio da assegnare all'utente, quindi fare clic su **OK**.

5.  Nella pagina **Abilita cassetta postale di messaggistica unificata** completare le seguenti caselle:
    
      - **Indirizzo SIP o numero E.164**   Immettere l'indirizzo SIP o il numero E.164 dell'utente. Queste opzioni sono disponibili se l'utente abilitato per la messaggistica unificata è assegnato a un criterio cassetta postale di messaggistica unificata collegato a un URI SIP o a un dial plan E.164. L'aggiunta di un indirizzo SIP o di un numero E.164 per un utente non è disponibile se l'utente è associato al dial plan dell'interno telefonico. Quando si assegna l'utente a un criterio cassetta postale di messaggistica unificata collegato a un dial plan E.164 o URI SIP, è inoltre necessario immettere il numero interno dell'utente. Questo numero di interno viene utilizzato quando gli utenti utilizzano Outlook Voice Access per accedere alla propria cassetta postale. Il numero di cifre configurato in questa casella deve corrispondere al numero di cifre configurato sul dial plan URI SIP o E.164.
    
      - **Numero dell'interno**   Immettere il numero dell'interno per l'utente che si sta abilitando per la messaggistica unificata.
        
        Il numero di intero fornito deve essere valido e contenere lo stesso numero di cifre specificato nel dial plan. È possibile inserire solo caratteri numerici o cifre da 1 a 20. Solitamente la lunghezza del numero di interno va da 3 a 7 cifre. Il numero di cifre nell'interno è impostato nel dial plan collegato al criterio cassetta postale di messaggistica unificata assegnato all'utente.
    
      - Sotto **Impostazioni PIN** completare quanto segue:
        
          - **Genera automaticamente PIN**   Fare clic su questo pulsante per generare automaticamente un PIN per l'utente abilitato alla messaggistica unificata da utilizzare per l'accesso alla casella vocale tramite Outlook Voice Access. Questa impostazione è quella predefinita. Quando si fa clic su questo pulsante, viene generato automaticamente un PIN in base ai criteri del PIN configurati nel criterio cassetta postale di messaggistica unificata associato all'utente. È consigliabile utilizzare questa impostazione per proteggere il PIN dell'utente. Il PIN viene inviato all'utente nel messaggio di benvenuto che riceve quando viene abilitato per la messaggistica unificata. Per impostazione predefinita, dovranno modificare questo PIN la prima volta che accedono alla loro cassetta postale per utilizzare la posta vocale.
        
          - **Digitare il PIN**   Fare clic sul pulsante per specificare manualmente il PIN che l'utente utilizzerà per accedere al sistema di caselle vocali. Il PIN deve soddisfare le impostazioni dei criteri PIN configurate nel criterio cassetta postale di messaggistica unificata associato all'utente abilitato alla messaggistica unificata. Ad esempio, se il criterio cassetta postale di messaggistica unificata è configurato per accettare solo PIN contenenti sette o più cifre, il PIN immesso in questa casella deve contenere almeno sette cifre.
        
          - **Richiedi all'utente di reimpostare il PIN al primo accesso**   Selezionare questa casella di testo per forzare la reimpostazione del PIN della casella vocale dell'utente quando questo accede al sistema di caselle vocali da un telefono utilizzando Outlook Voice Access per la prima volta. Verranno invitati a immettere un PIN che è più significativo per loro. Per motivi di sicurezza, è consigliabile richiedere agli utenti abilitati alla messaggistica unificata di modificare il loro PIN al primo accesso per evitare accessi non autorizzati ai loro dati e alla loro cartella Posta in arrivo. Questa casella di controllo è selezionata per impostazione predefinita.

6.  Esaminare le impostazioni nella pagina **Abilita cassetta postale di messaggistica unificata**. Fare clic su **Fine** per abilitare gli utenti alla messaggistica unificata. Fare clic su **Indietro** per modificare la configurazione.

Per abilitare un utente per la messaggistica unificata in Shell, eseguire il seguente comando.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -NotifyEmail administrator@contoso.com -PINExpired $true

Se necessario, è possibile configurare un utente che è stato abilitato per la messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange:

1.  In EAC, selezionare **Destinatari** \> **Cassette postali**.

2.  Nella visualizzazione Elenco selezionare la cassetta postale per la quale si desidera modificare il criterio cassetta postale di messaggistica unificata.

3.  Nel riquadro dei dettagli, sotto **Funzionalità telefoniche e vocali** \> **Messaggistica unificata** fare clic su **Visualizza dettagli**.

4.  Nella pagina **Cassetta postale di messaggistica unificata**, fare clic su **Impostazioni cassetta postale di messaggistica unificata** per visualizzare o modificare le seguenti proprietà di messaggistica unificata per un utente abilitato alla messaggistica unificata:
    
      - **Stato PIN**   In questo campo di sola visualizzazione è riportato lo stato della cassetta postale dell'utente. Per impostazione predefinita, quando un utente è abilitato alla messaggistica unificata, lo stato del PIN è **Non bloccato**. Tuttavia, se l'utente inserisce più volte un PIN di Outlook Voice Access errato, lo stato viene visualizzato come **Bloccato**.
    
      - **Criteri cassetta postale di messaggistica unificata**   Questa casella mostra il nome dei criteri della cassetta postale di messaggistica unificata associato all'utente abilitato alla messaggistica unificata. È possibile fare clic su **Sfoglia** per individuare e specificare i criteri della cassetta postale di messaggistica unificata da associare a questa cassetta.
    
      - **Interno operatore personale**   Utilizzare questa casella per specificare il numero di interno di un operatore per l'utente. Per impostazione predefinita, il numero di interno non è configurato. Per il numero di interno è possibile inserire da 1 a 20 caratteri. Ciò consente di inoltrare le chiamate in arrivo per l'utente abilitato alla messaggistica unificata al numero specificato nella casella.
        
        È possibile configurare altri tipi di numeri di interno di operatori sui dial plan e per gli operatori automatici. Tuttavia, tali numeri sono in genere utilizzati per centralinisti o altri addetti che operano a livello di azienda globale. È possibile utilizzare l'impostazione interno operatore personale per consentire a un assistente amministrativo o un assistente personale di rispondere alle chiamate in entrata di un utente specifico.

5.  Nella pagina **Cassetta postale di messaggistica unificata**, sotto **Altri interni**, è possibile aggiungere, modificare e visualizzare i numeri interni per l'utente.
    
      - Per aggiungere un numero di interno, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). . Nella pagina **Aggiungi un altro interno**, utilizzare **Sfoglia** per selezionare il dial plan di messaggistica unificata quindi immettere il numero di interno nella casella **Numero interno**.
    
      - Per rimuovere un interno, selezionare il numero che si desidera rimuovere in questa casella e fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

6.  Se si apportano modifiche, fare clic su **Salvai**.

Se necessario, è possibile configurare un utente abilitato per la messaggistica unificata in Shell eseguendo il comando seguente.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringAudioCodec Wma -CallAnsweringRulesEnabled $false -FaxEnabled $false -UMSMSNotificationOption VoiceMail

## Passaggio 13: Configurare i gateway VoIP, IP PBX e PBX per SIP al fine di inviare tutte le chiamate in entrata ai server Accesso client di Exchange 2013

Quando i server Accesso client e Cassette postali di Exchange 2013 vengono installati, sono automaticamente abilitati alla funzione di risposta alle chiamate vocali in entrata e in uscita e all'instradamento dei messaggi di casella vocale verso i destinatari. Quando vengono installati i server Accesso client e Cassette postali di Exchange 2013 e distribuita la messaggistica unificata, non è necessario collegare o aggiungere tali server ai dial plan di messaggistica unificata. I server Accesso client e Cassette postali di Exchange 2013 rispondono a tutte le chiamate in entrata e utilizzano i dial plan di messaggistica unificata per individuare gli utenti.

Il server Accesso client di Exchange 2013 è il punto di ingresso per qualsiasi chiamata in arrivo o richiesta SIP di messaggistica unificata. Il servizio che gestisce le richieste SIP su un server Accesso client di Exchange 2013 è il servizio router di chiamata di messaggistica unificata che viene eseguito su ogni server Accesso client di Exchange 2013 nell'organizzazione.

Quando viene aggiornata la messaggistica unificata di Exchange 2013, è necessario aver già installato e configurato uno o più gateway VoIP per la connessione a PBX nella rete di telefonia oppure installato e configurato i PBX abilitati per SIP o gli IP PBX.

L'ultimo passaggio del processo di aggiornamento della messaggistica unificata di Exchange 2013 consiste nel configurare i gateway VoIP, IP PBX o PBX abilitati a SIP al fine di inviare le chiamate in entrata (tra cui i chiamanti che intendono lasciare un messaggio alla casella vocale di un utente, le chiamate da parte degli utenti abilitati alla messaggistica unificata che chiamano su Outlook Voice Access e le chiamate provenienti da utenti che chiamano un operatore automatico di messaggistica unificata) ai server Accesso client di Exchange 2013. In un primo momento tutte queste chiamate vengono ricevute da un gateway VoIP, IP PBX o PBX abilitato per SIP e poi ritrasmesse ai server Accesso client di Exchange 2013 nell'organizzazione dello stesso. Per ulteriori informazioni, vedere le risorse seguenti:

  -  
    [Servizi di messaggistica unificata](um-services-exchange-2013-help.md)

  -  
    [Note di configurazione per i gateway VoIP, IP PBX e PBX supportati](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  -  
    [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

## Passaggio 14: Disabilitare la risposta alla chiamata in un server di messaggistica unificata di Exchange 2007

È possibile disabilitare la risposta alla chiamata disattivando messaggistica unificata in un server di messaggistica unificata di Exchange 2007 o rimuovendo il server di messaggistica unificata da un dial plan. Quando si disabilita la messaggistica unificata, si impedisce al server di messaggistica unificata di rispondere alle chiamate in entrata. È possibile scegliere di disconnettere tutte le chiamate immediatamente oppure attendere che le chiamate in corso vengano elaborate prima di disabilitare il server di messaggistica unificata. Si consiglia di disabilitare la risposta alle chiamate prima di rimuovere il server da un dial plan in modo che termini di elaborare eventuali chiamate in entrata.

Per disabilitare la messaggistica unificata in un server di messaggistica unificata di Exchange 2007 utilizzando Exchange Management Console:

1.  Nell'albero della console di EMC, accedere a **Configurazione server** \> **Messaggistica unificata**.

2.  Nel riquadro dei risultati selezionare il server Messaggistica unificata da disabilitare.

3.  Nel riquadro azione fare clic su una delle seguenti operazioni:
    
    1.  Quando si seleziona l'opzione **Disabilita immediatamente**, vengono disconnesse tutte le chiamate connesse al server Messaggistica unificata.
    
    2.  Quando si seleziona l'opzione **Disabilita dopo aver completato le chiamate**, non saranno accettate nuove chiamate dal server Messaggistica unificata che sarà disabilitato fino all'elaborazione di tutte le chiamate.

4.  Nella finestra di dialogo di conferma scegliere **Sì** per continuare.

Per disabilitare la messaggistica unificata in un server di messaggistica unificata di Exchange 2007 utilizzando Shell, eseguire il seguente comando.

    Disable-UMServer -Identity MyUMServer -Immediate $true


> [!TIP]
> È possibile utilizzare il cmdlet <STRONG>Disable-UMServer</STRONG> da un server di messaggistica unificata di Exchange 2007 oppure il cmdlet <STRONG>Disable-UMService</STRONG> da un server Cassette postali di Exchange 2013 Mailbox per disabilitare la risposta alle chiamate.



## Passaggio 15: Rimuovere un server di messaggistica unificata di Exchange 2007 da un dial plan

Per elaborare le chiamate, è necessario che un server di messaggistica unificata di Exchange 2007 venga aggiunto a almeno un dial plan di messaggistica unificata. È possibile aggiungere un server di messaggistica unificata a diversi dial plan di messaggistica unificata. È possibile rimuovere un server di messaggistica unificata di Exchange 2007 da un dial plan di messaggistica unificata. Quando si rimuove un server di messaggistica unificata da un dial plan, il server di messaggistica unificata non risponde più alle chiamate e non elabora le chiamate di messaggistica unificata per i destinatari abilitati per la messaggistica unificata.

Per rimuovere un server di messaggistica unificata di Exchange 2007 da un dial plan utilizzando Exchange Management Console:

1.  Nell'albero della console di EMC, accedere a **Configurazione server** \> **Messaggistica unificata**.

2.  Nel riquadro dei risultati selezionare il server Messaggistica unificata.

3.  Nel riquadro azioni, scegliere **Proprietà**.

4.  Nella scheda **Impostazioni della Messaggistica unificata**, nella sezione **Dial plan associati** fare clic su **Rimuovi**.

5.  Nella finestra di dialogo di conferma fare clic su **Sì** per confermare l'eliminazione del server di messaggistica unificata di Exchange 2007 dal dial plan di messaggistica unificata.

6.  Fare clic su **OK** per chiudere la finestra delle proprietà.

Per rimuovere un server di messaggistica unificata di Exchange 2007 da un dial plan utilizzando Shell, eseguire il seguente comando.

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMServer -id MyUMServer
    $s.dialplans-=$dp.identity
    Set-UMServer -id MyUMServer -dialplans:$s.dialplans

In questo esempio vengono mostrati tre dial plan di URI SIP: SipDP1, SipDP2 e SipDP3. Con questo esempio viene rimosso il server di messaggistica unificata denominato `MyUMServer` dal dial plan denominato SipDP3.

    Set-UMServer -id MyUMServer -DialPlans SipDP1,SipDP2

In questo esempio vengono mostrati due dial plan di URI SIP: SipDP1 e SipDP2. Con questo esempio viene rimosso un server di messaggistica unificata denominato `MyUMServer` dal dial plan denominato SipDP2.

    Set-UMServer -id MyUMServer -DialPlans SipDP1


> [!TIP]
> È possibile utilizzare il cmdlet <STRONG>Set-UMServer</STRONG> in Shell in un server di messaggistica unificata di Exchange 2007 o il cmdlet <STRONG>Set-UMService</STRONG> in un server Cassette postali di Exchange 2013 per rimuovere un server di messaggistica unificata di Exchange 2007 da uno o più dial plan. Ad esempio, per rimuovere un server di messaggistica unificata di tutti i dial plan, eseguire il seguente comando: <CODE>Set-UMServer -identity MyUMServer -DialPlan $null</CODE>



## Come verificare se l'operazione ha avuto esito positivo

Dopo aver impostato la messaggistica unificata, verificare quanto segue per assicurarsi che tutto funzioni correttamente:

  - Che un utente abilitato per la casella vocale possa accedere a Outlook Web App o Outlook e visualizzare il messaggio di benvenuto per la messaggistica unificata.

  - Gli utenti di messaggistica unificata possono ricevere messaggi vocali.

  - Gli utenti di messaggistica unificata possono chiamare un numero Outlook Voice Access per ascoltare i messaggi di posta elettronica, gli elementi di calendario e i messaggi vocali.

  - Le messaggistica unificata esegue il routing delle chiamate dall'esterno dell'organizzazione e consente all'utente di effettuare una chiamata.


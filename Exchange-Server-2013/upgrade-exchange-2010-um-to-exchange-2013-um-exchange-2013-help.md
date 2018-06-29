---
title: 'Aggiornamento dalla messaggistica unificata di Exchange 2007 alla messaggistica unificata di Exchange 2010: Exchange 2013 Help'
TOCTitle: Aggiornamento dalla messaggistica unificata di Exchange 2007 alla messaggistica unificata di Exchange 2010
ms:assetid: 01aa5dab-689b-4738-afab-0d2f11a60b39
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn169226(v=EXCHG.150)
ms:contentKeyID: 54652859
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiornamento dalla messaggistica unificata di Exchange 2007 alla messaggistica unificata di Exchange 2010

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

Quando si esegue l'aggiornamento di un'organizzazione di Microsoft Exchange 2010 con messaggistica unificata (UM, Unified Messaging) alla messaggistica unificata di Exchange 2013, è necessario attenersi a una procedura già eseguita come parte della distribuzione della messaggistica unificata di Exchange 2010. A seconda dell'ambiente di telefonia e dei componenti di messaggistica unificata creati e configurati per supportare la messaggistica unificata in Exchange 2010, potrebbe essere necessario distribuire ulteriori apparecchiature telefoniche, inclusi gateway Voice over IP (VoIP), IP PBX (Private Branch eXchange) o PBX abilitato al SIP di tipo tradizionale, quindi creare e configurare eventuali componenti di messaggistica unificata aggiuntivi richiesti per la messaggistica unificata di Exchange 2013.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 45-90 minuti.

  - Assicurarsi di disporre delle autorizzazioni adatte nelle organizzazioni di Exchange 2010 ed Exchange 2013 per poter creare e configurare tutti i componenti necessari.

  - Verificare di aver distribuito e configurato in modo corretto i componenti telefonici, inclusi gateway VoIP e PBX, IP PBX o PBX abilitati al SIP (Session Initiation Protocol).

  - Verificare l'installazione e la configurazione corretta dei server Accesso client su cui è in esecuzione il servizio di routing delle chiamate di messaggistica unificata (UM Call Router) di Microsoft Exchange e i server Cassette postali su cui è in esecuzione il servizio di messaggistica unificata (UM) di Microsoft Exchange. Per ulteriori informazioni sui servizi di messaggistica unificata, vedere [Servizi di messaggistica unificata](um-services-exchange-2013-help.md).
    

    > [!WARNING]
    > È necessario distribuire un server Cassette postali di Exchange 2013 nell'organizzazione prima di configurare i gateway VoIP e gli IP PBX per inviare il traffico SIP messaggistica unificata e RTP ai server Accesso client di Exchange 2013.



  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Come eseguire l'operazione

## Passaggio 1: Scaricare e installare i Language Pack di messaggistica unificata necessari

I Language Pack di messaggistica unificata consentono ai chiamanti e agli utenti di Outlook Voice Access di interagire con il sistema di caselle vocali in più lingue. Dopo avere installato una lingua supplementare in un server Cassette postali di Exchange 2013, i chiamanti e gli utenti di Outlook Voice Access potranno ascoltare i messaggi di posta elettronica e interagire con il sistema di caselle vocali nella lingua specificata. Tuttavia, per rendere disponibile la lingua per tutte le chiamate in arrivo, è necessario installare i Language Pack di messaggistica unificata necessari su tutti i server di cassette postali di Exchange 2013. Questo avviene poiché ogni server Cassette postali di Exchange 2013 è in grado di rispondere alle chiamate in arrivo per il servizio di messaggistica unificata.

Per impostazione predefinita, quando si installa un server Cassette postali di Exchange 2013, viene installato il Language Pack per la lingua inglese americana (en-US). Questa è l'unica lingua disponibile per il dial plan se non si installa un altro Language Pack di messaggistica unificata. Non è possibile rimuovere la lingua inglese americana (en-US), a meno che non si rimuova il server Cassette postali dal computer. Una volta installato un Language Pack di messaggistica unificata su un server Cassette postali di Exchange 2013, anche la lingua associata al Language Pack verrà elencata come opzione disponibile durante la configurazione della lingua predefinita per il dial plan. Dal momento che durante la creazione di un operatore automatico di messaggistica unificata, quest'ultimo viene collegato a un dial plan di messaggistica unificata, si utilizza l'impostazione della lingua del dial pian di messaggistica unificata, per impostazione predefinita. Tuttavia, è possibile modificare questa impostazione dopo avere creato l'operatore automatico di messaggistica unificata.


> [!NOTE]
> Se l'inglese americano è l'unica lingua che si desidera rendere disponibile per il dial plan, ignorare questo passaggio e procedere al passaggio 2.



È possibile aggiungere i language pack di messaggistica UNIFICATA utilizzando il comando setup.exe oppure eseguendo il programma di installazione .exe *\<UMLanguagePack\>*dopo aver scaricato il language pack di messaggistica UNIFICATA di [Exchange Server 2013 messaggistica UNIFICATA di Language Pack](https://go.microsoft.com/fwlink/p/?linkid=266542). Per ulteriori informazioni, vedere [Installare un Language Pack di messaggistica unificata](install-a-um-language-pack-exchange-2013-help.md).

In questo esempio, il comando setup.exe viene utilizzato per installare il Language Pack di messaggistica unificata per il giapponese (ja-JP).

    setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

## Passaggio 2: Spostare su Exchange 2013 la cassetta postale di sistema di Exchange 2010 utilizzata per i messaggi di saluto personalizzati, annunci, menu e prompt di messaggistica unificata

I messaggi di saluto personalizzati, gli annunci, i menu e i prompt vengono usati dai dial plan e dagli operatori automatici di messaggistica unificata. La cassetta postale di sistema denominata {e0dc1c29-89c3-4034-b678-e6c29d823ed9} viene creata quando si installa Exchange 2010 o Exchange 2013 e utilizzata per supportare funzionalità quali Approvazione messaggi e Ricerca in più cassette postali. Questa cassetta postale di sistema viene utilizzata anche per memorizzare i messaggi di saluto personalizzati, gli annunci, i menu e i prompt utilizzata dal dial plan e dall'operatore automatico. Se la cassetta postale di sistema non esiste, è possibile utilizzare il comando **Setup/PrepareAD** per crearne una.

Per impostazione predefinita, le cassette postali di sistema non vengono visualizzate nell'interfaccia di amministrazione di Exchange (EAC). È possibile ottenere un elenco delle cassette postali dei sistema, eseguendo uno dei comandi riportati di seguito:

Questo comando restituisce un elenco di tutte le cassette postali di sistema.

    Get-Mailbox -Arbitration

Questo comando restituisce un elenco delle cassette postali di sistema e delle loro proprietà o impostazioni individuali.

    Get-Mailbox -Arbitration |fl

Utilizzando questa cassetta postale di sistema, è possibile effettuare il backup dei messaggi di saluto personalizzati, menu e prompt e ripristinarli insieme ad altre cassette postali in un database. Questo riduce la quantità di risorse necessarie. La memorizzazione dei messaggi di saluto personalizzati, annunci, menu e prompt in una cassetta postale di sistema rimuove tutte le eventuali incoerenze. Per ulteriori informazioni sulle operazioni di spostamento delle cassette postali, vedere [Spostamenti di cassette postali di Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

## Facoltativo: Esportare e importare manualmente il dial plan e i messaggi di saluto, gli annunci, i menu e i prompt

In alcune situazioni la cassetta postale di sistema di Exchange 2010 potrebbe essere stata rimossa rendendo necessario esportare e importare i saluti personalizzati, gli annunci, i menu e i prompt utilizzati con i dial plan e gli operatori automatici di messaggistica unificata dalla cassetta postale di sistema di Exchange 2010 a quella di Exchange 2013. In entrambe le versioni, la cassetta postale di sistema è denominata {e0dc1c29-89c3-4034-b678-e6c29d823ed9}.

I messaggi di saluto personalizzati, gli annunci, i menu e i prompt consistono in file audio (di formato .waw o .wma) che vengono utilizzati dalla messaggistica unificata per i seguenti scopi:

  - Sui dial plan di messaggistica unificata, tali file audio vengono utilizzati come messaggi di benvenuto e informativi. Vengono riprodotti quando gli utenti di Outlook Voice Access chiamano un numero di Outlook Voice Access.

  - Sugli operatori automatici di messaggistica unificata, i file audio vengono utilizzati per i messaggi di saluto, messaggi informativi, prompt menu e menu di navigazione personalizzati utilizzati per l'orario di ufficio e non di ufficio. Tali file vengono riprodotti quando gli utenti chiamano un operatore automatico di messaggistica unificata.

Durante la procedura di esportazione e importazione dei messaggi di saluto personalizzati, annunci, menu e prompt da Exchange 2010 a Exchange 2013, è necessario utilizzare i cmdlet **Export-UMPrompt** e **Import-UMPrompt**. Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per esportare o importare i prompt personalizzati. Su un server di Exchange 2010, utilizzare il cmdlet **Export-UMPrompt** per esportare i prompt del dial plan e dell'operatore automatico di Exchange 2010. Dopo avere esportato i prompt, è possibile importarli sul server Cassette postali di Exchange 2013. Quando si esegue il cmdlet **Export-UMPrompt** dal server di Exchange 2010, il comando esegue una ricerca del GUID o dell'identificatore di oggetto per il dial plan o l'operatore automatico in Active Directory ed esegue una query per determinare se sono presenti messaggi di saluto personalizzati, annunci, menu o prompt. Se trovati, questi messaggi di saluto personalizzati, annunci, menu o prompt vengono salvati nella directory specificata dall'utente. Dopo aver esportato tutti i messaggi di saluto personalizzati, i menu e i prompt, utilizzare il cmdlet **Import-UMPrompt** per importare i prompt nella cassetta postale di sistema di Exchange 2013.

In questo esempio viene esportata la formula di benvenuto per il dial plan di messaggistica unificata `MyUMDialPlan`; il file viene salvato con il nome `welcomegreeting.wav`.

    $prompt = Export-UMPrompt -PromptFileName "customgreeting.wav" -UMDialPlan MyUMDialPlan
    set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

In questo esempio il file della formula di benvenuto `welcomegreeting.wav` viene importato da d:\\UMPrompts nel dial plan di messaggistica unificata `MyUMDialPlan`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c

In questo esempio viene esportato un messaggio di saluto personalizzato per l'operatore automatico di messaggistica unificata `MyUMAutoAttendant`; il messaggio viene salvato nel file `welcomegreetingbackup.wav`.

    Export-UMPrompt -PromptFileName "welcomegreeting.wav" -UMAutoAttendant MyUMAutoAttendant
    set-content -Path "e:\UMPromptsBackup\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

In questo esempio il file della formula di benvenuto `welcomegreeting.wav` viene importato da d:\\UMPrompts nell'operatore automatico di messaggistica unificata `MyUMAutoAttendant`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c

Per ulteriori informazioni sui prompt personalizzati per la messaggistica unificata, vedere:

  - [Importazione ed esportazione istruzioni, gli annunci, menu e messaggi di saluto personalizzati](import-and-export-custom-greetings-announcements-menus-and-prompts-exchange-2013-help.md)

  - [Import-UMPrompt](https://technet.microsoft.com/it-it/library/dd876899\(v=exchg.150\))

  - [Export-UMPrompt](https://technet.microsoft.com/it-it/library/dd876882\(v=exchg.150\))

  - [Messaggi di saluto, istruzioni e lingue di messaggistica UNIFICATA](um-languages-prompts-and-greetings-exchange-2013-help.md)

## Passaggio 4: Esportare e importare i certificati

Se si utilizzano SIP o dial plan con protezione nell'organizzazione di Exchange 2010, è necessario esportare e importare i certificati utilizzati nei server Accesso client e Cassette postali per Exchange 2013. Mutual Transport Layer Security (MTLS) viene utilizzato per crittografare i dati inviati tra i server di Exchange 2013 e i gateway IP, IP PBX e PBX abilitati al SIP. I certificati associano l'identità del proprietà del certificato a due chiavi elettroniche (pubblica e privata) che vengono utilizzate per crittografare e firmare le informazioni in digitale. È possibile utilizzare uno dei seguenti certificati per i servizi di messaggistica unificata e di routing delle chiamate di messaggistica unificata:

  - Un certificato autofirmato (Exchange)

  - Un certificato interno dell'infrastruttura a chiave pubblica (PKI, Public Key Infrastructure)

  - Un certificato commerciale di terze parti

Per impostazione predefinita, quando si installa Exchange 2013 vengono creati due certificati autofirmati: **Microsoft Exchange Server Auth Certificate** e **Microsoft Exchange**. Il certificato autofirmato **Microsoft Exchange** può essere utilizzato affinché la messaggistica unificata esegua la crittografia dei dati, ma è necessario assegnare il certificato ai servizi di messaggistica unificata o di routing delle chiamate di messaggistica unificata. Questo certificato autofirmato può essere copiato e importato nel gateway VoIP, IP PBX e PBX abilitati al SIP. Tuttavia, è possibile utilizzarlo durante l'integrazione della messaggistica unificata con Microsoft Lync Server.

Per abilitare la messaggistica unificata affinché esegua la crittografia dei dati inviati tra i server Exchange 2013 e i gateway IP, IP PBX e PBX abilitati al SIP, è necessario eseguire una delle seguenti operazioni:

  - Utilizzare un certificato di messaggistica unificata autofirmato, creare un nuovo certificato di Exchange autofirmato, inviare una richiesta di certificato a un'autorità di certificazione interna affinché fornisca un certificato dell'infrastruttura a chiave pubblica o acquistare un certificato commerciale di terze parti da utilizzare per MTLS tra i server di cassetta postale di Exchange 2013 o Accesso client e i gateway IP, IP PBX e PBX abilitati al SIP.
    
    Per creare un certificato di Exchange autofirmato utilizzando l'interfaccia di Exchange, attenersi alla seguente procedura:
    
    1.  In EAC accedere a **Server** \> **Certificati**, quindi selezionare **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").
    
    2.  Nella pagina **Nuovo certificato di Exchange**, scegliere **Crea un certificato autofirmato**, quindi **Avanti**.
    
    3.  Immettere un nome descrittivo per il certificato e fare clic su **Avanti**.
    
    4.  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per selezionare i server di Exchange che si desidera applicare al certificato, quindi selezionare **Avanti**.
    
    5.  Indicare i domini che si desidera includere nel certificato, quindi selezionare **Avanti**. Se si desidera aggiungere un dominio per un servizio, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    
    6.  Verificare che i domini inclusi siano corretti, quindi selezionare **Fine**.
    

    > [!IMPORTANT]
    > Quando si utilizza l'interfaccia di amministrazione di Exchange per creare un certificato, non viene richiesto di abilitare i servizi per il certificato stesso. Tali servizi possono essere abilitati utilizzando l'interfaccia di amministrazione di Exchange, dopo aver creato il certificato. Per ulteriori informazioni su come abilitare i servizi per un certificato, vedere <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Assegnare un certificato per i servizi di messaggistica unificata e routing delle chiamate di messaggistica unificata</A>.

    
    Creare un certificato di Exchange autofirmato eseguendo il seguente comando in Shell.
    
        New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true
    

    > [!NOTE]
    > Se i servizi che si desidera abilitare vengono indicati tramite il parametro <EM>Services</EM>, verrà richiesto di abilitare i servizi per il certificato creato. In questo esempio, viene richiesto all'utente di abilitare il certificato per i servizi di messaggistica unificata e di routing delle chiamate di messaggistica unificata. Per ulteriori informazioni su come abilitare i servizi per un certificato, vedere <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Assegnare un certificato per i servizi di messaggistica unificata e routing delle chiamate di messaggistica unificata</A>.



  - Importare il certificato che verrà utilizzato su tutti i server Accesso client e Cassette postali per Exchange 2013 nell'organizzazione. Se si utilizza il certificato di Exchange 2013 autofirmato, sarà necessario copiare il certificato e importarlo nei gateway VoIP, IP PBX o PBX abilitati al SIP. Se utilizzi il certificato autofirmato di Exchange 2010, è necessario che il nome alternativo del soggetto contenga i nomi dei computer di tutti i server di Exchange 2013. Se nell'organizzazione sono presenti server di messaggistica unificata di Exchange 2010, è possibile utilizzare il certificato di Exchange 2013 autofirmato, ma è necessario aggiungere i nomi dei computer relativi ai server di messaggistica unificata di Exchange 2010 al nome alternativo del soggetto nel certificato di Exchange 2013.

  - Abilitare o assegnare il certificato da utilizzare ai servizi di messaggistica unificata o di routing delle chiamate di messaggistica unificata sui server di Accesso client e Cassette postali.
    
    Per abilitare il servizio di messaggistica unificata e quello di routing delle chiamate di messaggistica unificata su tutti i server Exchange 2013 affinché utilizzino il certificato di Exchange autofirmato tramite l'interfaccia di amministrazione di Exchange, attenersi alla seguente procedura:
    
    1.  In EAC, accedere a **Server** \> **Certificati**, selezionare il servizio per il quale abilitare i servizi, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    
    2.  Nella pagina **Procedura**, selezionare **Servizi**, **Messaggistica unificata**, quindi fare clic su **Routing delle chiamate di messaggistica unificata**.
    
    Abilitare un certificato di Exchange autofirmato eseguendo il seguente comando in Shell.
    
        Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'

  - Configurare eventuali dial plan di messaggistica unificata nuovi o esistenti come SIP con protezione o modalità Protetto.

  - Configurare la modalità di avvio della messaggistica unificata in TLS o Dual sui server Accesso client o di cassette postali dell'organizzazione.

  - Creare e configurare gateway IP di messaggistica unificata nuovi o esistenti con un nome di dominio completo (FQDN, Fully Qualified Domain Name).

  - Configurare la porta di attesa sui gateway IP di messaggistica unificata affinché utilizzi la porta TLS 5061.

  - Riavviare il routing delle chiamate di messaggistica unificata su tutti i server Accesso client di Exchange 2013, quindi riavviare il servizio di messaggistica unificata su tutti i server Cassette postali di Exchange 2013. Per ulteriori informazioni sui servizi di messaggistica unificata, vedere [Servizi di messaggistica unificata](um-services-exchange-2013-help.md).

## Passaggio 5: Configurare la modalità di avvio della messaggistica unificata su tutti i server Accesso client di Exchange 2013

Se si utilizzano dial plan SIP con protezione o protetti, è necessario configurare la modalità di avvio della messaggistica unificata su tutti i server Accesso client di Exchange 2013. È possibile specificare la modalità di avvio della messaggistica unificata relativamente al servizio di routing delle chiamate di messaggistica unificata su un server Accesso client di Exchange 2013 utilizzando l'interfaccia di amministrazione di Exchange o Exchange Management Shell. Per impostazione predefinita, il server Accesso client si avvierà in modalità TCP, ma se si sta utilizzando Transport Layer Security (TLS) per crittografare il traffico VoIP è necessario configurare il server Accesso client di Exchange 2013 per la modalità TLS o Dual. Si consiglia di configurare tutti i server Accesso client di Exchange 2013 per l'utilizzo di Dual in modalità di avvio della messaggistica unificata. Questa situazione si verifica poiché i server Accesso client di Exchange 2013 rispondono alle chiamate in arrivo per tutti i dial plan di messaggistica unificata, ma tali dial plan possono avere impostazioni di protezione diverse. Se si modifica la modalità di avvio della messaggistica unificata, è necessario riavviare il servizio di routing delle chiamate della messaggistica unificata per rendere effettive le modifiche. Per ulteriori informazioni sui servizi di messaggistica unificata, vedere [Servizi di messaggistica unificata](um-services-exchange-2013-help.md).

Configurare la modalità di avvio della modalità di avvio della messaggistica unificata su un server Accesso client di Exchange 2013 utilizzando l'interfaccia di amministrazione di Exchange, nel modo riportato di seguito:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server di Exchange che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Exchange Server** scegliere **Messaggistica unificata**.

4.  In **Impostazioni routing delle chiamate di messaggistica unificata** \> **Modalità di avvio della messaggistica unificata**, selezionare una delle opzioni presenti nell'elenco a discesa:
    
      - **TCP**   Scegliere questa opzione se non si utilizza MTLS, ma soltanto dial plan non protetti.
    
      - **TLS**   Scegliere questa opzione se si utilizza MTLS e soltanto dial plan SIP con protezione o protetti.
    
      - **DUAL**   Scegliere questa opzione se si utilizza MTLS e soltanto dial plan SIP con protezione, protetti o non protetti.

5.  Dopo aver selezionato la modalità di avvio della messaggistica unificata, fare clic su **Salva**.

Configurare la modalità di avvio della messaggistica unificata su un server Accesso client di Exchange 2013 eseguendo in Shell il comando riportato di seguito.

    Set-UMCallRouterSettings -Server MyUMCallRouter.northwindtraders.com -UMStartupMode Dual

## Passaggio 6: Configurare la modalità di avvio della messaggistica unificata su tutti i server Cassette postali di Exchange 2013

Se si utilizzano dial plan SIP con protezione o protetti, è necessario configurare la modalità di avvio della messaggistica unificata su tutti i server Cassette postali di Exchange 2013. È possibile specificare la modalità di avvio della messaggistica unificata relativamente al servizio di messaggistica unificata su un server Cassette postali di Exchange 2013 utilizzando l'interfaccia di amministrazione di Exchange o Shell. Per impostazione predefinita, un server Cassette postali di Exchange 2013 si avvierà in modalità TCP, ma se si sta utilizzando Transport Layer Security (TLS) per crittografare il traffico VoIP, è necessario configurare il server Cassette postali per la modalità TLS o Dual. Si consiglia di configurare tutti i server Cassette postali di Exchange 2013 affinché utilizzino la modalità Dual come quella di avvio della messaggistica unificata. Questa situazione si verifica perché i server Cassette postali di Exchange 2013 rispondono alle chiamate in arrivo per tutti i dial plan di messaggistica unificata, ma tali dial plan possono avere impostazioni di protezione diverse. Se si modifica la modalità di avvio della messaggistica unificata, è necessario riavviare il servizio di messaggistica unificata per rendere effettive le modifiche. Per ulteriori informazioni sui servizi di messaggistica unificata, vedere [Servizi di messaggistica unificata](um-services-exchange-2013-help.md).

Configurare la modalità di avvio della messaggistica unificata su un server Cassette postali di Exchange 2013 utilizzando l'interfaccia di amministrazione di Exchange, nel modo riportato di seguito:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server di Exchange che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Exchange Server** scegliere **Messaggistica unificata**.

4.  In **Impostazioni servizio di messaggistica unificata** \> **Modalità di avvio della messaggistica unificata**, selezionare una delle opzioni presenti nell'elenco a discesa:
    
      - **TCP**   Scegliere questa opzione se non si utilizza MTLS, ma soltanto dial plan non protetti.
    
      - **TLS**   Scegliere questa opzione se si utilizza MTLS e soltanto dial plan SIP con protezione o protetti.
    
      - **DUAL**   Scegliere questa opzione se si utilizza MTLS e soltanto dial plan SIP con protezione, protetti o non protetti.

5.  Dopo aver selezionato la modalità di avvio della messaggistica unificata, fare clic su **Salva**.

Configurare la modalità di avvio della messaggistica unificata su un server Cassette postali di Exchange 2013 eseguendo in Shell il comando riportato di seguito.

    Set-UMService -Identity MyUMServer -ExternalHostFqdn host.external.contoso.com -IPAddressFamily Any -UMStartupMode Dual

## Passaggio 7: Creare o configurare i dial plan di messaggistica unificata esistenti

In base alla distribuzione di Exchange 2010 corrente, è possibile che venga richiesto di creare nuovi dial plan di messaggistica unificata o configurare i dial plan esistenti. Un dial plan di messaggistica unificata rappresenta un insieme di sistemi PBX (Private Branch eXchange) abilitati al SIP tradizionali o IP PBX che condividono i numeri di interni comuni degli utenti. Gli interni di tutti gli utenti ospitati sui PBX abilitati al SIP tradizionali o IP PBX in un dial plan contengono lo stesso numero di cifre. Gli utenti possono chiamarsi digitando l'interno telefonico senza aggiungere un numero particolare o digitare un numero di telefono completo.

I dial plan di messaggistica unificata vengono utilizzati nella messaggistica unificata per garantire che gli interni telefonici degli utenti siano univoci. In alcune reti di telefonia possono esistere più PBX o IP PBX. In tali reti di telefonia possono essere presenti due utenti il cui numero di interno telefonico è identico. I dial plan di messaggistica unificata consentono di risolvere una situazione simile. L'inserimento di due utenti in due dial plan di messaggistica unificata separati rende univoci i loro numeri di interno. Per ulteriori informazioni, vedere [Dial plan di messaggistica unificata](um-dial-plans-exchange-2013-help.md).

Se necessario, è possibile creare un dial plan di messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange:

1.  In EAC accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata** e fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella pagina **Nuovo dial plan di messaggistica unificata**, completare le seguenti caselle:
    
      - **Nome**°°°Digitare il nome del dial plan. Il nome del dial plan di messaggistica unificata è obbligatorio e deve essere univoco. Tuttavia, il nome digitato viene utilizzato soltanto per la visualizzazione nell'interfaccia di amministrazione di Exchange e in Shell. La lunghezza massima per il nome di un dial plan di messaggistica unificata è di 64 caratteri e può contenere spazi. Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        Anche se la casella per il nome del dial plan può contenere fino a 64 caratteri, il nome del dial plan non può superare i 49 caratteri. Se si cerca di creare un nome di dial plan che contiene più di 49 caratteri, verrà visualizzato un messaggio di errore. Nel messaggio viene indicato che i criteri cassetta postale di messaggistica unificata non possono essere generati poiché il nome del dial plan di messaggistica unificata è troppo lungo. Ciò avviene poiché al momento della creazione di un dial plan, viene creato anche un criterio cassetta postale di messaggistica unificata predefinito con il nome *\<DialPlanName\>***Criterio predefinito**. Quando i 15 caratteri del criterio predefinito vengono aggiunti al nome del dial plan, il numero totali dei caratteri supera il limite consentito. Il parametro *name* può contenere 64 caratteri sia per il dial plan che per il criterio cassetta postale di messaggistica unificata. Tuttavia, se il nome del dial plan è più lungo di 49 caratteri, il nome del criterio cassetta postale di messaggistica unificata predefinito sarà più lungo di 64 caratteri e il sistema non lo consente.
    
      - **Lunghezza numero di interno (cifre)** Immettere il numero di cifre per i numeri di interni nel dial plan. Il numero di cifre dei numeri di interno è basato sul dial plan di telefonia creato su un sistema PBX. Ad esempio, se un utente associato a un dial plan di telefonia compone un numero di interno di quattro cifre per chiamare un altro utente nello stesso dial plan, occorre selezionare 4 come numero di cifre dell'interno.
        
        È una casella obbligatoria il cui intervallo di valori è compreso tra 1 e 20. La lunghezza tipica dell'interno è compresa tra 3 e 7 numeri. Se l'ambiente di telefonia esistente contiene numeri di interni, è necessario specificare un numero di cifre che corrisponda al numero di cifre di quegli interni.
        
        Quando si crea un dial plan per gli interni telefonici, è necessario immettere un numero di interno per l'utente nel caso in cui sia collegato al dial plan dell'interno. Anche con i dial plan SIP o E.164 è necessario un numero di interno quando un utente abilitato alla messaggistica unificata è collegato a un dial plan URI SIP o E.164. Il numero di interno viene utilizzato dagli utenti di Outlook Voice Access per accedere alla cassetta postale di Exchange.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Tipo di UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Sicurezza UI\_VoIP)
    
      - **Codice paese**   Utilizzare questa casella per digitare il numero del codice paese utilizzato per le chiamate in uscita. Questo numero verrà anteposto automaticamente al numero di telefono composto. La casella consente di immettere da 1 a 4 cifre. Ad esempio, negli Stati Uniti il codice paese è 1, nel Regno Unito è 44.

3.  Fare clic su **Salva**.

Se necessario, è possibile creare un dial plan di messaggistica unificata eseguendo in Shell il comando riportato di seguito.

    New-UMDialplan -Name MyUMDialPlan -URIType E164 -NumberOfDigitsInExtension 5 -VoIPSecurity Secured

Se necessario, è possibile configurare un dial plan di messaggistica unificata esistente utilizzando l'interfaccia di amministrazione di Exchange, nel modo riportato di seguito:

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera visualizzare o modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Nuovo dial plan di messaggistica unificata** fare clic su **Configura**. Utilizzare le opzioni di configurazione per visualizzare le impostazioni dei dial plan specifiche e per abilitare o disabilitare le funzionalità.

Se necessario, è possibile configurare un dial plan di messaggistica unificata esistente utilizzando Shell:

    Set-UMDialplan -Identity MyDialPlan -AccessTelephoneNumbers 4255551234 -AudioCodec Wma -CallAnsweringRulesEnabled $false -OutsideLineAccessCode 9 -VoIPSecurity SIPSecured

Quando è stata distribuita la funzionalità di messaggistica unificata di Exchange 2010, è stato richiesto di aggiungere un server di messaggistica unificata a un dial plan di messaggistica unificata per rispondere alle chiamate in arrivo. Ciò non è più necessario. In Exchange 2013, i server Accesso client e Cassette postali non possono essere collegati a un numero di telefono interno o a un dial plan E.164, ma possono essere collegati ai dial plan di URI SIP. I server Accesso client e Cassette postali risponderanno alle chiamate in arrivo per tutti i tipi di dial plan.

## Passaggio 8: Creare o configurare i gateway IP di messaggistica unificata esistenti

In base alla distribuzione di Exchange 2010 corrente, è possibile che venga richiesto di creare nuovi gateway IP di messaggistica unificata o di configurare quelli esistenti. Se si utilizzano dial plan SIP con protezione o protetti, è necessario creare un gateway IP di messaggistica unificata con un FQDN e utilizzare Shell per configurarlo all'ascolto sulla porta 5061. Nel caso dei gateway IP di messaggistica unificata esistenti, verificare che siano configurati con un FQDN e siano in ascolto sulla porta 5061. Se il gateway IP di messaggistica unificata non utilizza un FQDN, utilizzare l'interfaccia di amministrazione di Exchange o Shell per modificare l'indirizzo. Nel caso in cui il gateway IP di messaggistica unificata non utilizzi la porta 5061, utilizzare Shell per modificare la porta. È possibile visualizzare le impostazioni relative a un gateway IP di messaggistica unificata utilizzando il cmdlet **Get-UMIPGateway**.

Un gateway IP di messaggistica unificata rappresenta un gateway VoIP fisico, un PBX o un PBX abilitato al SIP. Prima che un gateway VoIP, un IP-PBX o un PBX abilitato al SIP possano essere utilizzati per rispondere alle chiamate in arrivo e inviare chiamate in uscita per gli utenti della casella vocale, è necessario creare un gateway IP di messaggistica unificata per il servizio directory.

La combinazione di gateway IP di messaggistica unificata e di un gruppo di risposta di messaggistica unificata stabilisce un collegamento tra gateway VoIP, IP PBX o PBX abilitato al SIP e un dial plan di messaggistica unificata. Se si creano più gruppi di risposta di messaggistica unificata è possibile associare un singolo gateway IP di messaggistica unificata a più dial plan di messaggistica unificata. Per ulteriori informazioni, vedere [Gateway IP di messaggistica unificata](um-ip-gateways-exchange-2013-help.md).

Se necessario, è possibile creare un gateway IP di messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange, nel modo riportato di seguito:

1.  In EAC accedere a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella pagina **Nuovo gateway IP di messaggistica unificata** immettere le informazioni seguenti:
    
      - **Nome**   Utilizzare questa casella per specificare un nome univoco per il gateway IP di messaggistica unificata. Si tratta del nome che verrà visualizzato nell'interfaccia di amministrazione di Exchange. Qualora fosse necessario modificare il nome visualizzato del gateway IP di messaggistica unificata dopo la sua creazione, occorre innanzitutto eliminare il gateway IP di messaggistica unificata esistente e, quindi, crearne un altro con il nome corretto. Benché il nome del gateway IP di messaggistica unificata sia obbligatorio viene utilizzato solo ai fini della visualizzazione. Dal momento che l'organizzazione può utilizzare più gateway IP di messaggistica unificata, si consiglia di utilizzare nomi significativi per ognuno di essi. La lunghezza massima per il nome di un gateway IP di messaggistica unificata è di 64 caratteri e può contenere spazi. Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Indirizzo**   È possibile configurare un gateway IP di messaggistica unificata con un indirizzo IPv4/IPv6 o un FQDN. Utilizzare questa casella per specificare l'indirizzo IP o nome di dominio completo configurato nel gateway VoIP, IP PBX o nel PBX abilitato per SIP. Questa casella accetta solo FQDN validi immessi nel formato corretto.
        
        È possibile immettere caratteri alfabetici e numerici. Sono supportati indirizzi IPv4, indirizzi IPv6 e nomi di dominio completi (FQDN). Se si desidera utilizzare TLS tra un gateway IP di messaggistica unificata e un dial plan in funzione in modalità protetta o protetta con SIP, è necessario configurare il gateway IP di messaggistica unificata con un nome di dominio completo. È necessario configurarlo anche per rimanere in ascolto sulla porta 5061 e verificare che tutti i gateway VoIP o IP PBX siano stati configurati per l'ascolto delle richieste Mutual TLS sulla porta 5061. Per configurare un gateway IP di messaggistica unificata, eseguire questo comando in Shell: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`
        
        Se si utilizza un FQDN, è inoltre necessario verificare che sia stato correttamente configurato un record host DNS per il gateway VoIP, IP PBX o PBX abilitato al SIP affinché il nome host venga risolto in un indirizzo IP. Inoltre, se si utilizza un FQDN anziché un indirizzo IP, e la configurazione DNS per il gateway IP di messaggistica unificata è stata modificata, è necessario disabilitare e abilitare di nuovo il gateway IP di messaggistica unificata per avere la certezza che le informazioni di configurazione del gateway IP di messaggistica unificata vengano aggiornate correttamente.
    
      - **Dial plan di messaggistica unificata**   Fare clic su **Sfoglia** per selezionare il dial plan di messaggistica unificata che si desidera associare al gateway IP di messaggistica unificata. Selezionando un dial plan di messaggistica unificata da associare a un gateway IP di messaggistica unificata, viene inoltre creato un gruppo di risposta di messaggistica unificata predefinito associato al dial plan di messaggistica unificata selezionato. Se non si seleziona alcun dial plan di messaggistica unificata, sarà necessario creare manualmente un gruppo di risposta di messaggistica unificata e successivamente associarlo al gateway IP di messaggistica unificata creato.

3.  Fare clic su **Salva**.

Se necessario, è possibile creare un gateway IP di messaggistica unificata eseguendo il comando seguente.

    New-UMIPGateway -Identity MyUMIPGateway -Address "MyUMIPGateway.contoso.com"

Per configurare un gateway IP di messaggistica unificata esistente, tramite l'interfaccia di amministrazione di Exchange:

1.  In EAC accedere a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Gateway IP di messaggistica unificata**, fare clic su **Configura**. Utilizzare le opzioni di configurazione per visualizzare le impostazioni dei gateway IP di messaggistica unificata specifiche e per abilitare o disabilitare le funzionalità.

Per configurare in Shell un gateway IP esistente, eseguire il comando seguente nella shell.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## Passaggio 9: Creare un gruppo di risposta di messaggistica unificata

A seconda della distribuzione di Exchange 2010 esistente, potrebbe essere necessario creare nuovi gruppi di risposta di messaggistica unificata. Un gruppo di risposta telefonico consente di distribuire le chiamate telefoniche da un singolo numero a più numeri di interno o di telefono. Nella messaggistica unificata, un gruppo di risposta di messaggistica unificata consiste in una rappresentazione logica di un gruppo di risposta telefonico e consente di collegare un gateway IP di messaggistica unificata a un dial plan di messaggistica unificata.

È necessario disporre di almeno un gruppo di risposta di messaggistica unificata per ciascun gruppo di risposta PBX o IP PBX. Una volta completata la procedura illustrata di seguito, per impostazione predefinita viene creato un gruppo di risposta di messaggistica unificata. Se si hanno più gruppi di risposta PBX o IP PBX, è necessario creare altri gruppi di risposta di messaggistica unificata. Per ulteriori informazioni sui gruppi di risposta di messaggistica unificata, vedere [Gruppi di risposta di messaggistica unificata](um-hunt-groups-exchange-2013-help.md).

Se necessario, è possibile creare un gruppo di risposta di messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange, nel modo riportato di seguito:

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Gruppi di risposta di messaggistica unificata**, fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella pagina **Nuovo gruppo di risposta di messaggistica unificata**, immettere le informazioni seguenti:
    
      - **Nome**   Utilizzare questa casella per creare il nome visualizzato per il gruppo di risposta di messaggistica unificata. Il nome di un gruppo di risposta di messaggistica unificata è obbligatorio e deve essere univoco, ma viene utilizzato solo per la visualizzazione in EAC e Shell. Se si desidera modificare il nome visualizzato del gruppo di risposta dopo averlo creato, è necessario eliminare il gruppo di risposta esistente e crearne uno con il nome desiderato. Se l'organizzazione utilizza più gruppi di risposta, si consiglia di utilizzare nomi significativi per i gruppi di risposta. La lunghezza massima per il nome di un gruppo di risposta di messaggistica unificata è di 64 caratteri e può contenere spazi, Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Gateway IP di messaggistica unificata**   Utilizzare questa casella per selezionare un gateway IP di messaggistica unificata. In questa casella viene visualizzato il nome del gateway IP di messaggistica unificata che verrà collegato al gruppo di risposta di messaggistica unificata. Per collegare un gateway IP di messaggistica unificata al gruppo di risposta di messaggistica unificata, fare clic su **Sfoglia**.
    
      - **Identificatore pilota**   Utilizzare questa casella per specificare una stringa che identifichi in modo univoco l'identificatore pilota configurato per il sistema PBX o IP PBX. In questa casella, è possibile utilizzare un numero di interno o un URI (Uniform Resource Identifier) SIP. La casella accetta caratteri alfanumerici. Per PBX legacy, si utilizza un valore numerico come identificatore pilota. Tuttavia, alcuni IP PBX e PBX abilitati al SIP possono utilizzare URI SIP.

4.  Fare clic su **Salva**.

Se necessario, è possibile creare un gruppo di risposta di messaggistica unificata eseguendo nella shell il comando riportato di seguito.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialPlan MyUMDialPlan -UMIPGateway MyUMIPGateway


> [!TIP]
> Non è possibile configurare o modificare le impostazioni relative a un gruppo di risposta di messaggistica unificata. Se si desidera modificare le impostazioni di configurazione relative a un gruppo di risposta di messaggistica unificata, è necessario eliminare il gruppo di risposta di messaggistica unificata e aggiungerne uno nuovo con le impostazioni corrette.



## Passaggio 10: Creare o configurare gli operatori automatici di messaggistica unificata

A seconda della distribuzione di Exchange 2010 esistente, potrebbe essere necessario creare nuovi operatori automatici di messaggistica unificata. Gli operatori automatici di messaggistica unificata possono essere utilizzati per creare un sistema di menu vocali che consentono ai chiamanti interni ed esterni di utilizzare il sistema dei menu degli operatori automatici di messaggistica unificata per individuare luoghi o persone, nonché per eseguire o trasferire le chiamate agli utenti dell'azienda o ai reparti dell'organizzazione. Per ulteriori informazioni, vedere [Rispondere automaticamente e il routing delle chiamate in arrivo](automatically-answer-and-route-incoming-calls-exchange-2013-help.md).

Nelle distribuzioni di dimensioni ridotte è possibile che la messaggistica unificata venga distribuita solo per consentire agli utenti di lasciare un messaggio vocale ad altri utenti. In queste distribuzioni, non è necessario creare un operatore automatico. Tuttavia, nella maggior parte dei casi, l'utilizzo degli operatori automatici si rivela molto utile in caso di chiamate all'organizzazione da parte di chiamanti esterni.

Se necessario, è possibile creare un operatore automatico di messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange, nel modo riportato di seguito:

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Selezionare il dial plan di messaggistica unificata al quale aggiungere un operatore automatico, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata** fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella pagina **Nuovo operatore automatico di messaggistica unificata** compilare i seguenti campi:
    
      - **Nome**   Utilizzare questa casella per creare il nome visualizzato per l'operatore automatico di messaggistica unificata. Il nome di un operatore automatico di messaggistica unificata è obbligatorio e deve essere univoco. Tuttavia, viene utilizzato solo per la visualizzazione in EAC e nella shell. Qualora fosse necessario modificare il nome visualizzato dell'operatore automatico dopo che è stato creato, eliminare in primo luogo l'operatore automatico di messaggistica unificata esistente, quindi creare un altro operatore automatico con il nome desiderato. Se nell'organizzazione vengono utilizzati più operatori automatici di messaggistica unificata, si consiglia di utilizzare nomi significativi per gli operatori automatici di messaggistica unificata. La lunghezza massima del nome di un operatore automatico di messaggistica unificata è di 64 caratteri e può contenere spazi.
        
        Anche se a un nuovo operatore automatico di messaggistica unificata è possibile assegnare un nome contenente spazi, è necessario evitare l'uso degli spazi se la messaggistica unificata viene integrata con Lync Server. Di conseguenza, se è stato creato un operatore automatico il cui nome visualizzato contiene degli spazi e la messaggistica unificata viene integrata con Lync Server, è necessario innanzitutto eliminare l'operatore automatico e poi crearne un altro il cui nome visualizzato non contenga spazi.
    
      - **Crea l'operatore automatico come abilitato**   Selezionare questa casella di controllo per consentire all'operatore automatico di rispondere alle chiamate in arrivo al termine della creazione dell'operatore automatico di messaggistica unificata. Il nuovo operatore automatico è disabilitato per impostazione predefinita. Se si decide di creare l'operatore automatico di messaggistica unificata come disabilitato, è possibile utilizzare l'interfaccia di amministrazione di Exchange o la shell per abilitare l'operatore automatico una volta completata la procedura di creazione.
    
      - **Imposta operatore automatico per rispondere ai comandi vocali**   Selezionare questa casella di controllo per abilitare l'operatore automatico di messaggistica unificata al servizio di sintesi vocale. In questo modo, i chiamanti possono rispondere mediante toni o input vocali ai prompt di sistema o ai prompt personalizzati utilizzati dall'operatore automatico di messaggistica unificata. Per impostazione predefinita, l'operatore automatico non è abilitato al servizio di sintesi vocale quando viene creato. Affinché i chiamanti utilizzino un operatore automatico abilitato alla sintesi vocale in una lingua diversa dall'inglese americano (en-US), è necessario installare il Language Pack di messaggistica unificata appropriato e configurare le proprietà dell'operatore automatico per utilizzare questa lingua. Il Language Pack di messaggistica unificata per l'inglese americano viene installato per impostazione predefinita quando si installa il server Cassette postali di Exchange 2013.
    
      - **Numeri di accesso**   Immettere il numero di interno o i numeri di telefono che i chiamanti utilizzeranno per raggiungere l'operatore automatico. Digitare un numero di telefono o un numero interno nella casella, quindi fare clic su **Aggiungi** per aggiungere il numero all'elenco. Il numero di cifre per il numero di telefono o il numero interno immesso non deve corrispondere quello di un interno configurato per il dial plan di messaggistica unificata associato, in quanto le chiamate dirette agli operatori automatici di messaggistica unificata sono consentite.
        
        Non c'è limite ai numeri di interno o di accesso che è possibile inserire. Tuttavia, è possibile creare il nuovo operatore automatico senza elencare un numero di interno o di telefono. Non è necessario specificare un numero di telefono o un numero interno. È possibile modificare o rimuovere un numero di interno o un identificatore pilota esistente. Per modificare un numero di telefono o un numero interno esistente, fare clic su **Modifica**. Per rimuovere dall'elenco un numero di telefono o un numero interno esistente, fare clic su **Rimuovi**.

4.  Fare clic su **Salva**.

Se necessario, è possibile creare un operatore automatico di messaggistica unificata eseguendo nella shell il comando riportato di seguito.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true -Status Enabled

Se necessario, è possibile configurare un operatore automatico di messaggistica unificata esistente utilizzando l'interfaccia di amministrazione di Exchange, nel modo riportato di seguito:

1.  In EAC accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata** e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Operatori automatici di messaggistica unificata**, selezionare l'operatore automatico di messaggistica unificata che si desidera visualizzare o configurare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). Utilizzare le opzioni di configurazione per visualizzare le impostazioni degli operatori automatici specifiche e per abilitare o disabilitare le funzionalità.

Se necessario, è possibile configurare un operatore automatico di messaggistica unificata esistente eseguendo nella shell il comando riportato di seguito.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true -StaroutToDialPlanEnabled $true

## Passaggio 11: Creare o configurare criteri cassetta postale di messaggistica unificata

In base alla distribuzione di Exchange 2010 corrente, è possibile che venga richiesto di creare nuovi criteri cassetta postale di messaggistica unificata o configurare quelli esistenti. I criteri cassetta postale di messaggistica unificata sono necessari quando si abilitano utenti per la messaggistica unificata. La cassetta postale di ogni utente abilitato alla messaggistica unificata deve essere collegata a un singolo criterio cassetta postale di messaggistica unificata. Una volta creato un criterio cassetta postale di messaggistica unificata, è possibile associare una o più cassette postali abilitate alla messaggistica unificata al criterio. In questo modo è possibile controllare le impostazioni di protezione del PIN quali il numero minimo di cifre in un PIN o il numero massimo di tentativi di accesso per gli utenti abilitati alla messaggistica unificata collegati al criterio cassette postali di messaggistica unificata. Per ulteriori informazioni, vedere [Criteri cassetta postale di messaggistica unificata](um-mailbox-policies-exchange-2013-help.md).

Se necessario, è possibile creare un criterio cassette postali di messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange:

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Criteri cassetta postale messaggistica unificata** fare clic su **Aggiungi**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Nuovo criterio cassetta postale di messaggistica unificata**, nella casella **Nome** immettere il nome del nuovo criterio cassetta postale di messaggistica unificata.
    

    > [!NOTE]
    > Questa casella consente di specificare un nome univoco per il criterio cassetta postale di messaggistica unificata. Si tratta del nome che verrà visualizzato nell'interfaccia di amministrazione di Exchange. Qualora fosse necessario modificare il nome visualizzato del criterio cassetta postale di messaggistica unificata dopo la relativa creazione, occorre in primo luogo eliminare il criterio cassetta postale di messaggistica unificata esistente e, quindi, crearne un altro con il nome corretto. Non è possibile eliminare un criterio cassetta postale di messaggistica unificata nel caso in cui un utente abilitato alla messaggistica unificata venga associato al criterio. Sebbene sia necessario, il nome del criterio cassetta postale di messaggistica unificata viene utilizzato solo per scopi di visualizzazione. Dal momento che l'organizzazione può utilizzare più criteri cassetta postale di messaggistica unificata, si consiglia di utilizzare nomi significativi per ognuno di essi. La lunghezza massima per il nome di un criterio cassetta postale di messaggistica unificata è di 64 caratteri e può contenere spazi. Non può tuttavia contenere i seguenti caratteri: " / \ [ ] : ; | = , + * ? &lt; &gt;.



4.  Fare clic su **Salva**.
    

    > [!NOTE]
    > Quando viene salvato il criterio cassetta postale di messaggistica unificata, vengono abilitate tutte le impostazioni predefinite inclusi i criteri PIN, le funzionalità della casella vocale e le impostazioni del sistema di caselle vocali protette. Per personalizzare o modificare le impostazioni predefinite relative ai criteri cassetta postale di messaggistica unificata appena creati, utilizzare il cmdlet <STRONG>Set-UMMailbox</STRONG> o l'interfaccia di amministrazione di Exchange.



Se necessario, è possibile creare un criterio cassetta postale di messaggistica unificata eseguendo nella shell il comando riportato di seguito.

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

Se necessario, è possibile configurare un criterio cassetta postale di messaggistica unificata esistente utilizzando la shell:

1.  In EAC accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata** e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera visualizzare o configurare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). Utilizzare le opzioni di configurazione per visualizzare le impostazioni dei criteri cassetta postale di messaggistica unificata specifiche e per abilitare o disabilitare le funzionalità.

Se necessario, è possibile configurare un criterio cassetta postale di messaggistica unificata esistente eseguendo nella shell il comando riportato di seguito.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

## Passaggio 12: Spostare su Exchange 2013 le cassette postali abilitate alla messaggistica unificata

Dopo aver abilitato l'utilizzo della casella vocale per gli utenti all'interno dell'organizzazione, all'utente viene applicato un set predefinito di proprietà di messaggistica unificata per consentirgli di utilizzare le funzionalità di messaggistica unificata di Exchange 2010. Per ulteriori informazioni, vedere [Segreteria telefonica per gli utenti](voice-mail-for-users-exchange-2013-help.md).

Durante la procedura di aggiornamento, è possibile che per un certo periodo di tempo l'utente disponga delle cassette postali abilitate alla messaggistica unificata sia sui server Cassette postali di Exchange 2010 che di Exchange 2013. Tuttavia, se è in corso lo spostamento di tutti gli utenti abilitati alla messaggistica unificata verso i server Cassette postali di Exchange 2013, è necessario utilizzare l'interfaccia di amministrazione di Exchange o il cmdlet **New-MoveRequest** nella shell di un server Exchange 2013, in modo da conservare tutte le proprietà e le impostazioni, quali il PIN dell'utente.

Una richiesta di spostamento rappresenta il processo di spostamento di una cassetta postale da un database delle cassette postali ad un altro. Una richiesta di spostamento locale è uno spostamento della cassetta postale all'interno di una singola foresta. Per ulteriori informazioni sullo spostamento di cassette postali, vedere l'articolo relativo alla

  - [Spostamenti di cassette postali di Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

  - [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\))

  - [New-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219166\(v=exchg.150\))

  - [Gestione delle richieste di spostamento](https://go.microsoft.com/fwlink/p/?linkid=296352)

Per spostare una cassetta postale di Exchange su un server Cassette postali di Exchange 2013 tramite l'interfaccia di amministrazione di Exchange:

1.  In EAC, fare clic su **Destinatari** \> **Migrazione**, quindi scegliere **Aggiungi**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella procedura guidata per **Nuovo spostamento cassetta postale locale**, selezionare l'utente che si desidera spostare, fare clic su **OK**, quindi fare clic su **Avanti**.

3.  Nella pagina **Sposta configurazione** specificare un nome per il nuovo batch. Selezionare le opzioni desiderate per la cassetta postale di archiviazione e il percorso del database delle cassette postali, quindi fare clic su **Nuovo**.

Per spostare una cassetta postale di Exchange 2010 su un server Cassette postali di Exchange 2013 utilizzando la shell, eseguire il comando riportato di seguito.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase "DB01"

## Passaggio 13: Abilitare la funzionalità di messaggistica unificata per nuovi utenti o configurare le impostazioni di un utente esistente abilitato alla messaggistica unificata

Un utente deve avere una cassetta postale prima di poter essere abilitato alla messaggistica unificata. Per impostazione predefinita, un utente che dispone di una cassetta postale non è abilitato alla messaggistica unificata. Una volta abilitato, l'utente potrà gestire, modificare e configurare le proprietà relative alla messaggistica unificata e le funzionalità del sistema di caselle vocali. È possibile abilitare la funzionalità di messaggistica unificata per un utente utilizzando l'interfaccia di amministrazione di Exchange o la shell. Per ulteriori informazioni, vedere [Segreteria telefonica per gli utenti](voice-mail-for-users-exchange-2013-help.md).

Quando si abilita la funzionalità di messaggistica unificata per un utente, è necessario definire almeno un numero interno che la funzionalità utilizza quando viene inviata posta vocale alla cassetta postale dell'utente e per consentire all'utente di utilizzare Outlook Voice Access. Dopo aver abilitato l'utente alla messaggistica unificata, è possibile aggiungere numeri di interno secondari alla cassetta postale dell'utente oppure modificarli o rimuoverli configurando l'indirizzo proxy di messaggistica unificata di Exchange (EUM, Exchange Unified Messaging) per l'utente, nell'interfaccia di amministrazione di Exchange. Per aggiungere, modificare o rimuovere numeri di interno, numeri E.164 o indirizzi SIP, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

Abilitare la funzionalità di messaggistica unificata per un utente utilizzando l'interfaccia di amministrazione di Exchange:

1.  Nell'interfaccia, fare clic su **Destinatari**.

2.  Nella visualizzazione elenco, selezionare l'utente di cui si desidera abilitare la cassetta postale per la messaggistica unificata.

3.  Nel riquadro Dettagli sotto **Funzionalità telefono e vocali** fare clic su **Abilita**.

4.  Nella pagina **Abilita cassetta postale di messaggistica unificata**, fare clic sul pulsante **Sfoglia** accanto a **Criteri cassetta postale di messaggistica unificata**, individuare nell'elenco il criterio da assegnare all'utente, quindi fare clic su **OK**.

5.  Nella pagina **Abilita cassetta postale di messaggistica unificata** completare le seguenti caselle:
    
      - **Indirizzo SIP o numero E.164**   Immettere l'indirizzo SIP o il numero E.164 dell'utente. Queste opzioni sono disponibili se l'utente abilitato per la messaggistica unificata è assegnato a un criterio cassetta postale di messaggistica unificata collegato a un URI SIP o a un dial plan E.164. L'aggiunta di un indirizzo SIP o di un numero E.164 per un utente non è disponibile se l'utente è associato al dial plan dell'interno telefonico. Quando si assegna l'utente a un criterio cassetta postale di messaggistica unificata collegato a un dial plan E.164 o URI SIP, è ancora necessario immettere l'interno dell'utente. Questo numero di interno viene utilizzato quando gli utenti utilizzano Outlook Voice Access per accedere alla propria cassetta postale. Il numero di cifre configurato in questa casella deve corrispondere al numero di cifre configurato sul dial plan URI SIP o E.164.
    
      - **Numero dell'interno**   Immettere il numero dell'interno per l'utente che si sta abilitando per la messaggistica unificata.
        
        Il numero di intero fornito deve essere valido e contenere lo stesso numero di cifre specificato nel dial plan. È possibile inserire solo caratteri numerici o cifre da 1 a 20. Solitamente la lunghezza del numero di interno va da 3 a 7 cifre. Il numero di cifre nell'interno è impostato nel dial plan collegato al criterio cassetta postale di messaggistica unificata assegnato all'utente.
    
      - Sotto **Impostazioni PIN** completare quanto segue:
        
          - **Genera automaticamente PIN**   Fare clic su questo pulsante per generare automaticamente un PIN per l'utente abilitato alla messaggistica unificata da utilizzare per l'accesso alla casella vocale tramite Outlook Voice Access. Questa impostazione è quella predefinita. Quando si fa clic su questo pulsante, viene generato automaticamente un PIN in base ai criteri del PIN configurati nel criterio cassetta postale di messaggistica unificata associato all'utente. È consigliabile utilizzare questa impostazione per proteggere il PIN dell'utente. Il PIN viene inviato all'utente nel messaggio di benvenuto che riceve quando viene abilitato per la messaggistica unificata. Per impostazione predefinita, dovranno modificare questo PIN la prima volta che accedono alla loro cassetta postale per utilizzare la casella vocale.
        
          - **Digitare il PIN**   Fare clic sul pulsante per specificare manualmente il PIN che l'utente utilizzerà per accedere al sistema di caselle vocali. Il PIN deve soddisfare le impostazioni dei criteri PIN configurate nel criterio cassetta postale di messaggistica unificata associato all'utente abilitato alla messaggistica unificata. Ad esempio, se il criterio cassetta postale di messaggistica unificata è configurato per accettare solo PIN contenenti sette o più cifre, il PIN immesso in questa casella deve contenere almeno sette cifre.
        
          - **Richiedi all'utente di reimpostare il PIN al primo accesso**   Selezionare questa casella di testo per forzare la reimpostazione del PIN della casella vocale dell'utente quando questo accede al sistema di caselle vocali da un telefono utilizzando Outlook Voice Access per la prima volta. Verranno invitati a immettere un PIN che è più significativo per loro. Per motivi di sicurezza, è consigliabile richiedere agli utenti abilitati alla messaggistica unificata di modificare il loro PIN al primo accesso per evitare accessi non autorizzati ai loro dati e alla loro cartella Posta in arrivo. Questa casella di controllo è selezionata per impostazione predefinita.

6.  Esaminare le impostazioni nella pagina **Abilita cassetta postale di messaggistica unificata**. Fare clic su **Fine** per abilitare gli utenti alla messaggistica unificata. Fare clic su **Indietro** per modificare la configurazione.

Per abilitare la funzionalità di messaggistica unificata per un utente tramite Shell, eseguire il seguente comando.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -NotifyEmail administrator@contoso.com -PINExpired $true

Se necessario, è possibile configurare un utente abilitato per la messaggistica unificata utilizzando l'interfaccia di amministrazione di Exchange:

1.  Nell'interfaccia di amministrazione di Exchange, selezionare **Destinatari** \> **Cassette postali**.

2.  Nella visualizzazione elenco, selezionare la cassetta postale per la quale si desidera modificare il criterio cassetta postale di messaggistica unificata.

3.  Nel riquadro dei dettagli, sotto **Funzionalità telefoniche e vocali** \> **Messaggistica unificata** fare clic su **Visualizza dettagli**.

4.  Nella pagina **Cassetta postale di messaggistica unificata**, fare clic su **Impostazioni cassetta postale di messaggistica unificata** per visualizzare o modificare le seguenti proprietà di messaggistica unificata per un utente abilitato alla messaggistica unificata:
    
      - **Stato PIN**   In questa casella di sola visualizzazione è riportato lo stato della cassetta postale dell'utente. Per impostazione predefinita, quando un utente è abilitato alla messaggistica unificata, lo stato del PIN è **Non bloccato**. Tuttavia, se l'utente inserisce più volte un PIN di Outlook Voice Access errato, lo stato viene visualizzato come **Bloccato**.
    
      - **Criteri cassetta postale di messaggistica unificata**   Questa casella mostra il nome dei criteri della cassetta postale di messaggistica unificata associato all'utente abilitato alla messaggistica unificata. È possibile fare clic su **Sfoglia** per individuare e specificare i criteri della cassetta postale di messaggistica unificata da associare a questa cassetta.
    
      - **Interno operatore personale**   Utilizzare questa casella per specificare il numero di interno di un operatore per l'utente. Per impostazione predefinita, il numero di interno non è configurato. Per il numero di interno è possibile inserire da 1 a 20 caratteri. Ciò consente di inoltrare le chiamate in arrivo per l'utente abilitato alla messaggistica unificata al numero specificato nella casella.
        
        È possibile configurare altri tipi di numeri di interno di operatori sui dial plan e per gli operatori automatici. Tuttavia, tali numeri sono in genere utilizzati per centralinisti o altri addetti che operano a livello di azienda globale. L'impostazione relativa all'interno dell'operatore personale può essere utilizzata per consentire a un assistente amministrativo o un assistente personale di rispondere alle chiamate in arrivo per un utente specifico.

5.  Nella pagina **Cassetta postale di messaggistica unificata**, sotto **Altri interni**, è possibile aggiungere, modificare e visualizzare i numeri interni per l'utente.
    
      - Per aggiungere un numero di interno, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). . Nella pagina **Aggiungi un altro interno**, utilizzare **Sfoglia** per selezionare il dial plan di messaggistica unificata quindi immettere il numero di interno nella casella **Numero interno**.
    
      - Per rimuovere un interno, selezionare il numero che si desidera rimuovere in questa casella e fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

6.  Se si apportano modifiche, fare clic su **Salvai**.

Se necessario, è possibile configurare un utente abilitato per la messaggistica unificata tramite Shell, eseguendo il comando riportato di seguito.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringAudioCodec Wma -CallAnsweringRulesEnabled $false -FaxEnabled $false -UMSMSNotificationOption VoiceMail

## Passaggio 14: Configurare i gateway VoIP, IP PBX e PBX abilitati al SIP affinché inviino tutte le chiamate in arrivo ai server Accesso client di Exchange 2013

Quando i server Accesso client e Cassette postali di Exchange 2013 vengono installati, sono automaticamente abilitati alla funzione di risposta alle chiamate vocali in arrivo e in uscita e di instradamento dei messaggi della casella vocale ai destinatari appropriati. Quando si installano i server Accesso client e Cassette postali di Exchange 2013 e si distribuisce la messaggistica unificata, non è necessario collegare o aggiungere tali server ai dial plan di messaggistica unificata. I server Accesso client e Cassette postali di Exchange 2013 rispondono a tutte le chiamate in arrivo e utilizzano i dial plan di messaggistica unificata per individuare gli utenti.

Il server Accesso client di Exchange 2013 è il punto di ingresso per qualsiasi chiamata in arrivo o richiesta SIP di messaggistica unificata. Il servizio che gestisce le richieste SIP sul server Accesso client di Exchange 2013 è il servizio di routing delle chiamate di messaggistica unificata e viene eseguito su tutti i server Accesso client di Exchange 2013 della propria organizzazione.

Quando si esegue l'aggiornamento alla funzionalità di messaggistica unificata di Exchange 2013, è necessario che siano già installati e configurati uno o più gateway VoIP per la connessione a PBX nella rete di telefonia. In alternativa, è necessario che siano installati e configurati i PBX abilitati per SIP o IP PBX.

L'ultimo passaggio della procedura di aggiornamento alla funzionalità di messaggistica unificata di Exchange 2013 consiste nella configurazione dei gateway VoIP, IP PBX e PBX abilitati al SIP affinché inviino le chiamate in arrivo ai server Accesso client di Exchange 2013, inclusi i chiamanti che lasciano messaggi vocali per l'utente, le chiamate di utenti abilitati alla messaggistica unificata che chiamano Outlook Voice Access e le chiamate effettuate nell'operatore automatico di messaggistica unificata. Tutte queste chiamate vengono ricevute in prima istanza dal gateway VoIP, IP PBX o PBX abilitato al SIP e successivamente inoltrate ai server Accesso client di Exchange 2013 dell'organizzazione Exchange 2013. Per ulteriori informazioni, vedere le risorse seguenti:

  -  
    [Servizi di messaggistica unificata](um-services-exchange-2013-help.md)

  -  
    [Note di configurazione per i gateway VoIP, IP PBX e PBX supportati](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  -  
    [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

## Passaggio 15: Disabilitare la risposta alle chiamate sul server di messaggistica unificata di Exchange 2010

È possibile disabilitare la risposta alle chiamate disattivando la funzionalità di messaggistica unificata su un server di messaggistica unificata di Exchange 2010 o eliminando il server di messaggistica unificata dal dial plan. Quando si disabilita la funzionalità di messaggistica unificata, si impedisce al server di messaggistica unificata di rispondere alle chiamate in arrivo. È possibile scegliere di disconnettere tutte le chiamate immediatamente oppure attendere che le chiamate in corso vengono elaborate prima di disabilitare il server della messaggistica unificata. È possibile che si desideri disattivare la risposta alle chiamata prima di rimuovere il server dal dial plan, in modo che termini l'elaborazione delle eventuali chiamate in arrivo.

Disabilitare la messaggistica unificata su un server di messaggistica unificata di Exchange 2010 utilizzando Exchange Management Console:

1.  Nell'albero della console di EMC, accedere a **Configurazione server** \> **Messaggistica unificata**.

2.  Nel riquadro dei risultati selezionare il server Messaggistica unificata da disabilitare.

3.  Nel riquadro azione fare clic su una delle seguenti operazioni:
    
      - Quando si seleziona l'opzione **Disabilita immediatamente**, vengono disconnesse tutte le chiamate connesse al server di messaggistica unificata.
    
      - Quando si seleziona l'opzione **Disabilita dopo aver completato le chiamate**, non saranno accettate nuove chiamate dal server di messaggistica unificata che sarà disabilitato fino all'elaborazione di tutte le chiamate.

4.  Nella finestra di dialogo di conferma, scegliere **Sì** per continuare.

Per disabilitare la messaggistica unificata su un server di messaggistica unificata di Exchange 2010 utilizzando la shell, eseguire il seguente comando:

    Disable-UMServer -Identity MyUMServer -Immediate $true


> [!TIP]
> È possibile utilizzare il cmdlet <STRONG>Disable-UMServer</STRONG> di un server di messaggistica unificata di Exchange 2010 o il cmdlet <STRONG>Disable-UMService</STRONG> di un server Cassette postali di Exchange 2013 per la disattivazione della risposta alle chiamate.



## Passaggio 16: Rimuovere un server di messaggistica unificata di Exchange 2010 da un dial plan

Per elaborare le chiamate, è necessario che un server di messaggistica unificata di Exchange 2010 venga aggiunto ad almeno un dial plan di messaggistica unificata. Un server di messaggistica unificata può essere aggiunto a più dial plan di messaggistica unificata. È possibile rimuovere un server di messaggistica unificata di Exchange 2010 da un dial plan di messaggistica unificata. Quando si rimuove un server di messaggistica unificata da un dial plan, il server di messaggistica unificata non risponde più alle chiamate e non elabora le chiamate di messaggistica unificata per i destinatari abilitati per la messaggistica unificata.

Rimuovere un server di messaggistica unificata di Exchange 2010 da un dial plan utilizzando Exchange Management Console:

1.  Nell'albero della console di EMC, accedere a **Configurazione server** \> **Messaggistica unificata**.

2.  Nel riquadro dei risultati selezionare il server di messaggistica unificata.

3.  Nel riquadro azioni, scegliere **Proprietà**.

4.  Nella scheda **Impostazioni della Messaggistica unificata**, nella sezione **Dial plan associati** fare clic su **Rimuovi**.

5.  Nella finestra di dialogo conferma fare clic su **Sì** per confermare l'eliminazione del server Exchange 2010 dal dial plan di messaggistica UNIFICATA.

6.  Fare clic su **OK** per chiudere la finestra delle proprietà.

Per rimuovere un server di messaggistica unificata di Exchange 2010 da un dial plan tramite Shell, eseguire il seguente comando.

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMServer -id MyUMServer
    $s.dialplans-=$dp.identity
    Set-UMServer -id MyUMServer -dialplans:$s.dialplans

In questo esempio, sono presente tre dial plan URI SIP: SipDP1, SipDP2 e SipDP3. In questo esempio viene rimosso un server di messaggistica unificata denominato `MyUMServer` dal dial plan SipDP3.

    Set-UMServer -id MyUMServer -DialPlans SipDP1,SipDP2

In questo esempio, sono presente due dial plan URI SIP: SipDP1 e SipDP2. In questo esempio viene rimosso un server di messaggistica unificata denominato `MyUMServer` dal dial plan SipDP2.

    Set-UMServer -id MyUMServer -DialPlans SipDP1


> [!TIP]
> È possibile utilizzare il cmdlet <STRONG>Set-UMServer</STRONG>in Shell su un server di messaggistica unificata di Exchange 2010 o il cmdlet <STRONG>Set-UMService</STRONG> su un server per cassette postali di Exchange 2013 per l'eliminazione di un server di messaggistica unificata di Exchange 2010 da uno o più dial plan. Ad esempio, per rimuovere il server di messaggistica unificata da tutti i dial plan, eseguire il seguente comando: <CODE>Set-UMServer -identity MyUMServer -DialPlans $null</CODE>



## Come verificare se l'operazione ha avuto esito positivo

Dopo aver configurato la messaggistica unificata, effettuare i seguenti controlli per essere certi che funzioni correttamente:

  - Un utente abilitato per la posta vocale può accedere a Outlook Web App o Outlook e visualizzare il messaggio di benvenuto per la messaggistica unificata.

  - Gli utenti di messaggistica unificata possono ricevere messaggi vocali.

  - Gli utenti di messaggistica unificata possono chiamare un numero Outlook Voice Access per ascoltare i messaggi di posta elettronica, gli elementi di calendario e i messaggi vocali.

  - Le messaggistica unificata esegue il routing delle chiamate dall'esterno dell'organizzazione e consente all'utente di effettuare una chiamata.


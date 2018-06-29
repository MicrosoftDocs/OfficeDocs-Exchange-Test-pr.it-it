---
title: 'Installare Exchange 2013 utilizzando la modalità automatica: Exchange 2013 Help'
TOCTitle: Installare Exchange 2013 utilizzando la modalità automatica
ms:assetid: 386465e9-41da-4e26-9816-b3b69be1f8bf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997281(v=EXCHG.150)
ms:contentKeyID: 50480350
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Installare Exchange 2013 utilizzando la modalità automatica

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-06-19_

Per eseguire un'installazione automatica, è necessario installare Microsoft Exchange Server 2013 dal prompt dei comandi. Per ulteriori informazioni sulla pianificazione e la distribuzione di Exchange 2013, vedere [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md).

Si consiglia di installare il ruolo Trasporto Edge in una rete perimetrale al di fuori della foresta di Active Directory interna dell'organizzazione. Anche se si può installare il ruolo del server Trasporto Edge in un computer appartenente al dominio, in questo modo viene attivata la gestione del dominio solo delle funzioni e impostazioni di Windows. Il ruolo Trasporto Edge stesso non usa Active Directory. Invece usa la funzionalità di WindowsActive Directory Lightweight Directory Services (AD LDS) per archiviare le informazioni su configurazione e destinatario. Per ulteriori informazioni sul ruolo Trasporto Edge, vedere [Server Trasporto Edge](edge-transport-servers-exchange-2013-help.md).


> [!TIP]
> Informazioni sull'Assistente per la distribuzione di Exchange Server Si tratta di uno strumento in linea gratuito che facilita la rapida distribuzione di Exchange 2013 all'interno dell'organizzazione richiedendo alcune domande e creando un elenco di controllo per la distribuzione personalizzato. Per ulteriori informazioni, vedere <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistente per la distribuzione di Exchange Server</A>.




> [!NOTE]
> Dopo aver installato qualsiasi ruolo del server su un computer in cui viene eseguitoExchange 2013, non è possibile utilizzare l'installazione guidata di Exchange 2013 per aggiungere altri ruoli del server sullo stesso computer. Se si desidera aggiungere altri ruoli del server a un computer, è necessario utilizzare Installazione applicazioni nel Pannello di controllo oppure il file Setup.exe da una finestra del prompt dei comandi.<BR>Il ruolo Trasporto Edge non può essere installato nello stesso computer come i ruoli server Cassetta postale o Accesso client.



Per informazioni sulle attività da completare dopo l'installazione, vedere [Attività successive all'installazione di Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

Le informazioni seguenti si applicano a tutti i ruoli server di Exchange 2013.

  - Assicurarsi di aver letto le note di rilascio prima di eseguire l'installazione di Exchange 2013. Per ulteriori informazioni, vedere [Note sulla versione di Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - Il computer su cui si installa Exchange 2013 deve avere un sistema operativo supportato (quale Windows Server 2008 R2 con Service Pack 1 (SP1), Windows Server 2012 R2 o Windows Server 2012), disporre di spazio su disco sufficiente e soddisfare altri requisiti. Per informazioni sui requisiti di sistema, vedere [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Per eseguire l'installazione di Exchange 2013, è necessario installare Microsoft .NET Framework 4.5, Windows Management Framework e altri software richiesti. Per informazioni sui prerequisiti per tutti i ruoli server, vedere [Prerequisiti di Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Dopo aver installato Exchange su un server, non modificare il nome del server. Non è infatti consentito assegnare un nuovo nome a un server dopo l'installazione di un ruolo server Exchange.



Le seguenti informazioni si applicano ai ruoli server Cassette postali e Accesso client di Exchange 2013.

  - Tempo stimato per il completamento: 60 minuti

  - Ciascuna organizzazione deve disporre di almeno un server Accesso client e un server Cassette postali nella foresta di Active Directory. Inoltre, ogni sito di Active Directory che contiene un server Cassette postali deve contenere anche almeno un server Accesso client. Se si separano i ruoli del server, è consigliabile installare per primo il ruolo Cassette postali.

  - Il computer in cui viene installato Exchange 2013 deve essere membro del dominio Active Directory.

  - È necessario utilizzare un account che disponga della delega di appartenenza al gruppo Schema Admins, se non è stato precedentemente preparato lo schema di Active Directory. Se si sta installando il primo server Exchange 2013 nell'organizzazione, l'account utilizzato deve essere membro del gruppo Enterprise Admins. Se lo schema è già stato preparato e non si sta installando il primo server Exchange 2013 nell'organizzazione, è necessario utilizzare un account membro del gruppo di ruoli Gestione organizzazione di Exchange 2013.
    
    Gli amministratori membri del gruppo di ruoli Configurazione delegata possono distribuire i server Exchange 2013 precedentemente sottoposti a provisioning da un membro del gruppo di ruoli Gestione organizzazione.

Le seguenti informazioni si applicano al ruolo server Trasporto Edge di Exchange 2013.

  - Tempo stimato per il completamento: 40 minuti

  - Il ruolo Trasporto Edge è disponibile con Exchange 2013 SP1 o versione successiva.

  - È necessario configurare il suffisso DNS primario del computer. Ad esempio, se il nome di dominio completo del computer è edge.contoso.com, il suffisso DNS del computer è contoso.com. Per ulteriori informazioni, vedere [Suffisso DNS primario manca](primary-dns-suffix-is-missing-exchange-2013-help.md).

  - I server Trasporto Hub di Exchange 2007 e Exchange 2010 devono essere aggiornati prima di poter creare un processo di sottoscrizione EdgeSync tra loro e il server Trasporto Edge di Exchange 2013. Se non si installa questo aggiornamento, è possibile che la sottoscrizione di EdgeSync non funzioni correttamente. Per ulteriori informazioni, vedere la sezione "Scenari di coesistenza supportati" in [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Verificare che l'account utilizzato sia membro del gruppo degli amministratori locali nel computer in cui si sta installando il ruolo Trasporto Edge.

## Installazione di Exchange 2013 in modalità automatica tramite Setup.exe


> [!NOTE]
> Per scaricare l'ultima versione di Exchange 2013, vedere <A href="updates-for-exchange-2013-exchange-2013-help.md">Aggiornamenti per Exchange 2013</A>.



1.  Accedere al computer su cui si desidera installare Exchange 2013.

2.  Andare al percorso di rete dei file di installazione di Exchange 2013.

3.  Nel prompt dei comandi eseguire il comando applicabile per l'organizzazione.
    

    > [!IMPORTANT]
    > Se è attivato un controllo di accesso utente, è necessario eseguire <CODE>Setup.exe</CODE> da un prompt dei comandi elevato.

    
        Setup.exe [/Mode:<setup mode>] [/IAcceptExchangeServerLicenseTerms]
        [/Roles:<server roles to install>] [/InstallWindowsComponents] 
        [/OrganizationName:<name for the new Exchange organization>] 
        [/TargetDir:<target directory>] [/SourceDir:<source directory>]
        [/UpdatesDir:<directory from which to install updates>] 
        [/DomainController:<FQDN of domain controller>] [/DisableAMFiltering]
        [/AnswerFile:<filename>] [/DoNotStartTransport] 
        [/EnableErrorReporting] [/CustomerFeedbackEnabled:<True | False>] 
        [/AddUmLanguagePack:<UM language pack name>] 
        [/RemoveUmLanguagePack:<UM language pack name>] 
        [/NewProvisionedServer:<server>] [/RemoveProvisionedServer:<server>] 
        [/MdbName:<mailbox database name>] [/DbFilePath:<Edb file path>] 
        [/LogFolderPath:<log folder path>] [/ActiveDirectorySplitPermissions:<True | False>]
        [/TenantOrganizationConfig:<path>]

4.  I file di installazione vengono copiati in locale sul computer in cui si sta installando Exchange 2013.

5.  Tutti i prerequisiti, inclusi quelli specifici dei ruoli del server da installare, vengono verificati. Se non sono stati soddisfatti tutti i requisiti, l'installazione non verrà eseguita e verrà visualizzato un messaggio di errore che spiega i motivi della mancata installazione. Se sono stati soddisfatti tutti i requisiti, Exchange 2013 verrà installato.

6.  Riavviare il computer al termine dell'installazione di Exchange 2013.

7.  Completare la distribuzione eseguendo le operazioni descritte in [Attività successive all'installazione di Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Esempi

Di seguito, sono riportati esempi sull'uso di Setup.exe:

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /OrganizationName:MyOrg /IAcceptExchangeServerLicenseTerms**
    
    Questo comando crea un'organizzazione Exchange 2013 in Active Directory denominata MyOrg, installa il ruolo del server Accesso client, il ruolo del server Cassette postali e gli strumenti di gestione e accetta anche i termini di licenza di Exchange 2013.

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /TargetDir:"C:\\Exchange Server" /IAcceptExchangeServerLicenseTerms**
    
    Questo comando installa il ruolo del server Accesso client, il ruolo del server Cassette postali e gli strumenti di gestione nella directory "C:\\Exchange Server". Questo comando presuppone che sia stata già preparata un'organizzazione di Exchange 2013.

  - **Setup.exe /mode:Install /r:CA,MB /IAcceptExchangeServerLicenseTerms**
    
    Questo comando installa il ruolo del server Accesso client, il ruolo del server Cassette postali e gli strumenti di gestione nella posizione di installazione predefinita.

  - **Setup.exe /mode:Install /r:EdgeTransport /IAcceptExchangeServerLicenseTerms**
    
    Questo comando installa il ruolo server Trasporto Edge e gli strumenti di gestione nel percorso di installazione predefinito.

  - **Setup.exe /mode:Install /r:ET /IAcceptExchangeServerLicenseTerms**
    
    Questo comando installa il ruolo server Trasporto Edge e gli strumenti di gestione nel percorso di installazione predefinito.

  - **Setup.exe /mode:Uninstall /IAcceptExchangeServerLicenseTerms**
    
    Questo comando rimuove completamente Exchange 2013 dal server e rimuove la configurazione di Exchange del server da Active Directory.

  - **Setup.exe /PrepareAD /on:"My Org" /IAcceptExchangeServerLicenseTerms**
    
    Questo comando crea un'organizzazione Exchange denominata My Org e prepara Active Directory per Exchange 2013.

  - **C:\\ExchangeServer\\bin\\Setup.exe /m:Install /r:ClientAccess /SourceDir:d:\\amd64 /IAcceptExchangeServerLicenseTerms**
    
    Questo comando aggiunge il ruolo del server Accesso client a un server Exchange 2013 esistente utilizzando D:\\amd64 come directory di origine.

  - **Setup.exe /role:ClientAccess,Mailbox /UpdatesDir:"C:\\ExchangeServer\\New Patches" /IAcceptExchangeServerLicenseTerms**
    
    Questo comando aggiorna ExchangeServer.msi con patch da una directory specificata, quindi installa il ruolo del server Accesso client, il ruolo del server Cassette postali e gli strumenti di gestione. Se questa directory comprende un bundle Language Pack, viene installato anche il Language Pack.

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /DomainController:DC01 /IAcceptExchangeServerLicenseTerms**
    
    Questo comando utilizza il controller di dominio DC01 per inviare una query ed eseguire modifiche a Active Directory durante l'installazione del ruolo del server Accesso client, del ruolo del server Cassette postali e degli strumenti di gestione.

  - **Setup.exe /mode:Install /role:ClientAccess /AnswerFile:c:\\ExchangeConfig.txt /IAcceptExchangeServerLicenseTerms**
    
    Questo comando installa il ruolo del server Accesso client utilizzando le impostazioni contenute nel file ExchangeConfig.txt.

  - **Setup.exe /rprs:Exchange03 /IAcceptExchangeServerLicenseTerms**
    
    Questo comando rimuove l'oggetto Exchange03 da Active Directory.

  - **Setup.exe /AddUmLanguagePack:ko-KR /IAcceptExchangeServerLicenseTerms**
    
    Questo comando installa il Language Pack di messaggistica unificata per la lingua coreana dalla directory %ExchangeSourceDir%\\ServerRoles\\UnifiedMessaging.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che Exchange 2013 sia stato installato correttamente, vedere [Verificare un'installazione di Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.


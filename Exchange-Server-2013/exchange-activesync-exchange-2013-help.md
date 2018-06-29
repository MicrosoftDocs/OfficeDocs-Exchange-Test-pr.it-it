---
title: 'Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync
ms:assetid: 5fafaff3-eb37-4fdb-95f0-e56c45ea5884
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998357(v=EXCHG.150)
ms:contentKeyID: 50480782
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Informazioni sul protocollo client Exchange ActiveSync per Exchange Server 2013. Verranno fornite informazioni sulle funzionalità di Exchange ActiveSync, tra cui le funzionalità di sicurezza, gli elementi che è possibile gestire, come renderlo sicuro e come evitare problemi durante la sincronizzazione con Windows Phone 7.


> [!TIP]
> Questo articolo è rivolto agli amministratori. Si desidera configurare un dispositivo Windows Phone, iOS o Android per l'accesso alla cassetta postale di Office 365 o Exchange Server? Vedere i seguenti argomenti. 
> <UL>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=615415">Set up email on Windows Phone</A></P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=615414">Configurare la posta elettronica nell'app Outlook per dispositivi mobili iOS</A></P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/?linkid=615417">Configurare la posta elettronica in un telefono o tablet Android</A></P></LI></UL>



Exchange ActiveSync è un protocollo client che consente di sincronizzare un dispositivo mobile con la cassetta postale Exchange. Exchange ActiveSync è abilitato per impostazione predefinita quando si installa Microsoft Exchange 2013.

**Sommario**

Cenni preliminari su Exchange ActiveSync

Funzionalità in Exchange ActiveSync

Gestione di Exchange ActiveSync

Sincronizzazione di Windows Phone 7

## Cenni preliminari su Exchange ActiveSync

Exchange ActiveSync è un protocollo di sincronizzazione di Microsoft Exchange ottimizzato per interagire con le reti a latenza elevata e a larghezza di banda ridotta. Questo protocollo, basato su HTTP e XML, consente ai telefoni cellulari di accedere alle informazioni di un'organizzazione su un server con Microsoft Exchange. Exchange ActiveSync consente agli utenti di cellulari di accedere a posta elettronica, calendario, contatti e attività e di continuare a poter accedere a queste informazioni anche quando lavorano offline.


> [!NOTE]
> Exchange ActiveSync non supporta le cassette postali condivise o l'accesso delegato.




> [!IMPORTANT]
> I telefoni cellulari che utilizzano Windows Phone 7 supportano solo un sottoinsieme di tutte le impostazioni dei criteri cassetta postale di Exchange ActiveSync. Per l'elenco completo, vedere Sincronizzazione di Windows Phone 7.



## Funzionalità in Exchange ActiveSync

Exchange ActiveSync fornisce quanto segue:

  - Supporto per i messaggi HTML

  - Supporto per i contrassegni di completamento

  - Raggruppamento dei messaggi di posta elettronica per conversazione

  - Possibilità di sincronizzare o meno un'intera conversazione

  - Sincronizzazione dei messaggi SMS con la cassetta postale di Exchange di un utente

  - Supporto per la visualizzazione dello stato di risposta dei messaggi

  - Supporto per il recupero rapido dei messaggi

  - Informazioni sui partecipanti alla riunione

  - Ricerca avanzata in Exchange

  - Reimpostazione del PIN

  - Protezione avanzata dei dispositivi tramite i criteri di password

  - Servizio di individuazione automatica per il provisioning wireless

  - Supporto per l'impostazione delle risposte automatiche quando gli utenti non sono alla loro postazione, sono in vacanza oppure sono fuori sede

  - Supporto per la sincronizzazione delle attività

  - Direct Push

  - Supporto per le informazioni sulla disponibilità dei contatti

## Gestione di Exchange ActiveSync

Per impostazione predefinita, Exchange ActiveSync è abilitato. Tutti gli utenti che dispongono di una cassetta postale di Exchange possono sincronizzare i propri dispositivi mobili con il server Microsoft Exchange.

È possibile eseguire le seguenti attività di Exchange ActiveSync:

  - Abilitare e disabilitare Exchange ActiveSync per gli utenti

  - Impostare criteri quali la lunghezza minima della password, il blocco del dispositivo e il numero massimo di tentativi di immissione della password non riusciti

  - Avviare la cancellazione remota per cancellare tutti i dati da un telefono cellulare perduto o rubato

  - Eseguire numerosi rapporti per la visualizzazione o l'esportazione in diversi formati

  - Stabilire quali tipi di dispositivi mobili possono sincronizzarsi con l'organizzazione tramite le regole di accesso al dispositivo

## Protezione in Exchange ActiveSync

È possibile configurare Exchange ActiveSync per l'utilizzo della crittografia SSL (Secure Sockets Layer) per le comunicazioni tra il server Exchange e il dispositivo mobile.

## Gestione dell'accesso al dispositivo mobile in Exchange ActiveSync

È possibile controllare quali dispositivi mobili possono sincronizzarsi. Per fare ciò, monitorare i nuovi dispositivi mobili quando si connettono all'organizzazione oppure configurare delle regole per stabilire quali tipi di dispositivi mobili possono connettersi. Indipendentemente dal metodo scelto per specificare quali dispositivi mobili possono sincronizzarsi, è possibile approvare o rifiutare l'accesso a uno specifico dispositivo mobile da parte di uno specifico utente in qualsiasi momento

## Funzionalità di sicurezza del dispositivo in Exchange ActiveSync

Oltre alla possibilità di configurare le opzioni di protezione per le comunicazioni tra il server Exchange e i dispositivi mobili, Exchange ActiveSync offre le seguenti funzionalità per il miglioramento della protezione dei dispositivi mobili:

  - **Cancellazione remota**   Se un cellulare viene perso, rubato o in qualche modo danneggiato, è possibile eseguire un comando di cancellazione remota dei dati dal computer Exchange Server o da un qualsiasi browser utilizzando Outlook Web App. Questo comando cancellerà tutti i dati dal dispositivo mobile.

  - **Criteri di password per il dispositivo**   Exchange ActiveSync consente di configurare diverse opzioni per la password del dispositivo.
    

    > [!WARNING]
    > La tecnologia del lettore di impronta digitale di iOS7 non può essere utilizzata come password del dispositivo. Se si sceglie di utilizzare il lettore di impronta digitale di iOS7, sarà comunque necessario creare e immettere una password per il dispositivo se richiesta dai criteri cassetta postale per i dispositivi mobili dell'organizzazione.

    
    Le opzioni per le password per il dispositivo sono:
    
      - **Lunghezza minima password (caratteri)**   Questa opzione consente di specificare la lunghezza della password per il dispositivo mobile. La lunghezza predefinita è di quattro caratteri, ma la password può contenere fino a 18 caratteri.
    
      - **Numero minimo di set di caratteri**   Utilizzare tale casella di testo per specificare la complessità della password alfanumerica e costringere gli utenti a utilizzare una serie di set di caratteri differenti quali: lettere minuscole, lettere maiuscole, simboli e numeri.
    
      - **Richiedi password alfanumerica**   Questa opzione determina l'affidabilità della password. Oltre ai valori numerici, è possibile imporre l'utilizzo di caratteri o simboli nella password.
    
      - **Tempo di inattività (secondi)**   Questa opzione consente di stabilire per quanto tempo il dispositivo mobile deve rimanere inattivo prima che all'utente venga richiesta la password di sblocco.
    
      - **Applicare la cronologia delle password**   Selezionare tale casella di controllo per impostare il cellulare in modo che l'utente non possa riutilizzare password precedenti. Il numero impostato determina il numero di password già utilizzate che l'utente non potrà riutilizzare.
    
      - **Abilita ripristino password**   Selezionare questa casella di controllo per abilitare il ripristino della password per il dispositivo mobile.  Gli amministratori possono utilizzare il cmdlet **Get-ActiveSyncDeviceStatistics** per cercare la password di ripristino di un utente.
    
      - **Cancellazione dati dispositivo dopo tentativi non riusciti**   Questa opzione consente di specificare se svuotare o meno la memoria del telefono dopo diversi tentativi di immissione password non riusciti.

  - **Criteri di crittografia del dispositivo**   Sono disponibili vari criteri di crittografia dei dispositivi mobili che è possibile applicare a un gruppo di utenti. Tali criteri includono quanto segue:
    
      - **Richiedi crittografia sul dispositivo**   Selezionare questa casella di controllo per richiedere la crittografia sul dispositivo mobile. In questo modo si aumenta il livello di protezione perché tutte le informazioni sul dispositivo mobile vengono crittografate.
    
      - **Richiedi crittografia sulle schede di memoria**   Selezionare questa casella di controllo per richiedere la crittografia della scheda di memoria rimovibile del dispositivo mobile. In questo modo si aumenta il livello di protezione perché tutte le informazioni contenute nelle schede di memoria del dispositivo mobile vengono crittografate.

## Sincronizzazione di Windows Phone 7

Se nell'organizzazione sono presenti dispositivi mobili che utilizzano Windows Phone 7, è possibile che si verifichino dei problemi di sincronizzazione su questi dispositivi se sono configurate determinate proprietà del criterio cassetta postale del dispositivo mobile. Per consentire ai telefoni cellulari con Windows Phone 7 di sincronizzarsi con una cassetta postale di Exchange, impostare la proprietà **AllowNonProvisionableDevices** su true oppure configurare solo le seguenti proprietà del criterio cassetta postale del dispositivo mobile:

  - PasswordRequired

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - DeviceWipeThreshold

  - AllowSimplePassword

  - PasswordExpiration

  - PasswordHistory

  - DisableRemovableStorage

  - DisableIrDA

  - DisableDesktopSync

  - BlockRemoteDesktop

  - BlockInternetSharing


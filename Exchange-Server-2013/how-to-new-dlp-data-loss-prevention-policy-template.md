---
title: 'Create a DLP policy from a template: Exchange 2013 Help'
TOCTitle: Create a DLP policy from a template
ms:assetid: 4432ef8b-6108-48d3-b2af-43ef5b40d2bc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150515(v=EXCHG.150)
ms:contentKeyID: 50479791
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Create a DLP policy from a template

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-01-14_

In Microsoft Exchange Server 2013, è possibile utilizzare i modelli dei criteri di prevenzione della perdita di dati (DLP) per consentire l'applicazione dei criteri di messaggistica e rispondere alle esigenze di conformità dell'organizzazione. Questi modelli contengono gruppi precostituiti di regole che consentono di gestire i dati dei messaggi ai quali sono associati diversi requisiti comuni legali e relativi alle normative. Per visualizzare un elenco di tutti i modelli forniti da Microsoft, vedere [Modelli di criteri DLP forniti di Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md). I modelli DLP forniti come esempio consentono di gestire:

  - I dati relativi al GLBA (Gramm-Leach-Bliley Act)

  - PCI-DSS (Payment Card Industry Data Security Standard)

  - U.S. PII (United States Personally Identifiable Information)

È possibile personalizzare uno di questi modelli DLP o utilizzarli come-è. Modelli di criteri DLP sono basati sulle regole di trasporto che includono nuove condizioni o predicati e azioni. È possibile aggiungere regole aggiuntive quando un criterio DLP è stato stabilito criteri DLP supportano la gamma completa delle regole di trasporto tradizionale. Per ulteriori informazioni sui modelli di criteri, vedere [Modelli di criteri DLP](dlp-policy-templates-exchange-2013-help.md). Per ulteriori informazioni sulle caratteristiche di regola di trasporto, vedere [Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013 ) o [Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) (Exchange Online ). Dopo aver avviato l'applicazione di un criterio, informazioni sulla osservare i risultati esaminare i seguenti argomenti:

Exchange 2013: [Visualizzare i report di rilevamento dei criteri DLP](view-dlp-policy-detection-reports-exchange-2013-help.md)

Exchange Online: [Visualizzare i report di rilevamento dei criteri DLP](https://technet.microsoft.com/it-it/library/dn904484\(v=exchg.150\))


> [!WARNING]
> È opportuno abilitare i criteri DLP in modalità di test prima di eseguirli nell'ambiente di produzione vero e proprio. Durante i test, si consiglia di configurare delle cassette postali campione e di inviare dei messaggi di prova che richiamino i criteri di test in modo da poterne verificare i risultati.



Per altre attività di gestione relative alla creazione di un criterio DLP da un modello, vedere [Procedure DLP](dlp-procedures-exchange-2013-help.md)Exchange Server 2013 o [Procedure DLP](https://technet.microsoft.com/it-it/library/jj938003\(v=exchg.150\))Exchange Online.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 30 minuti

  - Verificare che Exchange 2013 viene impostato come descritto in [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md).

  - Configurare gli account amministratore e utente nell'ambito dell'organizzazione e convalidare il flusso di posta di base.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Prevenzione della perdita di dati (DLP)" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md)

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo dell''interfaccia di amministrazione di Exchange per configurare un criterio di DLP da un modello

1.  Nell'interfaccia di amministrazione di Exchange accedere a **Gestione conformità** \> **Prevenzione della perdita di dati** e quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").
    

    > [!NOTE]
    > È possibile selezionare anche questa azione facendo clic sulla freccia accanto all'icona <STRONG>Aggiungi</STRONG><IMG title="Icona Aggiungi" alt="Icona Aggiungi" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif"> e selezionando <STRONG>Nuovo criterio DLP da modello</STRONG> nel menu a discesa.



2.  Nella pagina **Crea un nuovo criterio DLP da un modello**, completare i seguenti campi:
    
    1.  **Nome**   Aggiungere un nome che consenta di distinguere questo criterio dagli altri.
    
    2.  **Descrizione**   Aggiungere una descrizione facoltativa che riassume il criterio.
    
    3.  **Seleziona un modello**   Selezionare il modello appropriato per iniziare a creare un nuovo criterio.
    
    4.  **Altre opzioni**   Selezionare la modalità o lo stato. Il nuovo criterio non viene abilitato in toto fino a una richiesta specifica. La modalità predefinita per un criterio è il test senza notifiche.
    
    5.  Fare clic su **Salva** per completare la creazione del criterio.


> [!NOTE]
> Oltre alle regole all'interno di un modello specifico, l'organizzazione potrebbe avere altre necessità o criteri aziendali applicabili ai dati sottoposti a regolamentazione nell'ambito dell'ambiente della messaggistica. Exchange 2013 facilita l'operazione di modifica del modello di base per aggiungere azioni in modo che l'ambiente della messaggistica di Exchange risponda alle esigenze dell'utente.



È possibile cambiare i criteri modificando le regole al loro interno una volta che il criterio sarà stato salvato nell'ambiente di Exchange 2013. Un esempio di modifica di una regola potrebbe includere la possibilità di esonerare determinate persone dall'applicazione di un criterio o inviare una notifica e bloccare il recapito del messaggio se si stabilisce che contiene dati sensibili. Per ulteriori informazioni sui criteri di modifica e sulle regole, vedere [Gestire i criteri DLP](manage-dlp-policies-exchange-2013-help.md).

È necessario accedere al gruppo di regole dei criteri specifici nella pagina **Modifica criterio DLP** e utilizzare gli strumenti disponibili su quella pagina per modificare un criterio DLP che è già stato creato in Exchange 2013.

Alcuni criteri consentono l'aggiunta di regole che richiamano RMS per i messaggi. È necessario aver configurato RMS sul server di Exchange prima di aggiungere le azioni per utilizzare questi tipi di regole.

Per qualsiasi criterio DLP è possibile modificare le regole, le azioni, le eccezioni, il periodo di applicazione o stabilire se applicare altre regole nell'ambito del criterio ed è possibile aggiungere condizioni personalizzate per ciascuna di esse.

## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Modelli di criteri DLP](dlp-policy-templates-exchange-2013-help.md)


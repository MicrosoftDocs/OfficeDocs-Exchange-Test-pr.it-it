---
title: 'Creare un criterio DLP personalizzato: Exchange 2013 Help'
TOCTitle: Creare un criterio DLP personalizzato
ms:assetid: b3299a39-9663-41e4-b76e-9d2f7879d486
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150550(v=EXCHG.150)
ms:contentKeyID: 50479863
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un criterio DLP personalizzato

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-03-18_

Un criterio di criterio DLP perdita di dati personalizzati consente di stabilire le condizioni, le regole e le azioni che consentono di soddisfare le esigenze specifiche dell'organizzazione e che potrebbero non essere incluse in uno dei modelli DLP esistenti.

Le condizioni delle regole che sono disponibili in un singolo criterio includono tutte le regole di trasporto tradizionale oltre ai tipi di informazioni riservate presentate in [Cosa cercare i tipi di informazioni riservate in Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md). Per ulteriori informazioni sulle regole di trasporto, vedere [Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013 ) o [Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) (Exchange Online ).


> [!WARNING]
> È consigliabile attivare i criteri DLP in modalità test prima che vengano eseguiti nell'ambiente di produzione. Durante questo tipo di test, è consigliabile configurare cassette postali degli utenti di esempio e inviare messaggi di prova che richiamano i criteri di test per verificare i risultati. Per ulteriori informazioni sull'esecuzione di test, vedere <A href="test-a-mail-flow-rule-exchange-2013-help.md">Testare una regola del flusso di posta elettronica</A>.



Per altre attività di gestione relative alla creazione di criteri DLP personalizzati, vedere [Procedure DLP](dlp-procedures-exchange-2013-help.md)(Exchange 2013 ) o [Procedure DLP](https://technet.microsoft.com/it-it/library/jj938003\(v=exchg.150\)) (Exchange Online ).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 60 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Prevenzione della perdita di dati (DLP)" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per creare un nuovo criterio DLP personalizzato, è necessario seguire le istruzioni di installazione per Exchange 2013. Per ulteriori informazioni sulla distribuzione, vedere [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!NOTE]
> A causa di variazioni in ambienti clienti, Microsoft Customer Support Services (CSS) non possono partecipare lo sviluppo e la verifica di script personalizzati di espressione regolare ("RegEx script"). Per lo sviluppo di script personalizzati RegEX, test e il debug, i clienti di Office 365 saranno necessario basarsi sui risorse IT interne. In alternativa, i clienti di Office 365 possono scegliere di utilizzare una risorsa esterna di consulenza, ad esempio Microsoft Consulting Services (MCS). Indipendentemente dalla risorsa di sviluppo script CSS EXO ed EOP tecnici del supporto non sono disponibili per assistere i clienti con richieste di script personalizzati RegEx.




> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare EAC per creare un criterio DLP personalizzato senza tutte le regole esistenti

1.  In EAC, accedere a **Gestione conformità** \> **prevenzione della perdita di dati**. Vengono visualizzati tutti i criteri esistenti configurate in un elenco.

2.  Fare clic sulla freccia che viene accanto all'icona![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi")**Aggiungi** e selezionare **nuovo criterio personalizzato**.
    

    > [!IMPORTANT]
    > Se si fa clic su <STRONG>Aggiungi</STRONG><IMG title="Icona Aggiungi" alt="Icona Aggiungi" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif"> icona anziché la freccia, si creerà un nuovo criterio basato su un modello. Per ulteriori informazioni sull'utilizzo dei modelli, vedere <A href="how-to-new-dlp-data-loss-prevention-policy-template.md">Create a DLP policy from a template</A>.



3.  Nella pagina **nuovo criterio personalizzato**, completare i seguenti campi:
    
    1.  **Nome**   Aggiungere un nome che consenta di distinguere questo criterio dagli altri.
    
    2.  **Descrizione**   Aggiungere una descrizione facoltativa che riassume il criterio.
    
    3.  **Scelta di uno stato**    Selezionare la modalità o lo stato per questo criterio. Il nuovo criterio non è abilitato completamente fino a quando non si specifica che deve essere. La modalità predefinita per un criterio sia test senza notifiche.

4.  Fare clic su **Salva** per completare la creazione di nuove informazioni di riferimento dei criteri. Il criterio viene aggiunto all'elenco di tutti i criteri che sono state configurate, anche se non vi sono ancora tutte le regole o le azioni associate a questo nuovo criterio personalizzato.

5.  Fare doppio clic sul criterio appena creato oppure selezionarlo e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

6.  Nella pagina **criteri DLP modifica** fare clic su **regole**.
    
    Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere una nuova regola vuota. È possibile stabilire le condizioni utilizzando tutte le regole di trasporto tradizionale oltre ai tipi di informazioni riservate.
    
    Per evitare confusione, specificare un nome univoco per ogni parte del criterio o regola quando è disponibile l'opzione per fornire il proprio stringa di caratteri. Sono disponibili diverse opzioni di ulteriori opzioni per l'utente:
    
    1.  Fare clic sulla freccia che viene accanto all'icona![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi")**Add** per aggiungere una regola su notifica mittente o se consentire le sostituzioni.
    
    2.  Per rimuovere una regola, evidenziare la regola e fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").
    
    3.  Fare clic su **altre opzioni**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni") per aggiungere ulteriori condizioni e azioni per la regola inclusi i limiti specifici di effetti sulle altre regole o l'applicazione di questo criterio.

7.  Fare clic su **Salva** per completare la modifica il criterio e salvare le modifiche.

Modelli di criteri DLP sono un tipo di funzionalità di Microsoft Exchange che consentono di progettare e applicano un sistema di criteri e conformità affidabile per l'ambiente di messaggistica. Per ulteriori informazioni sulle funzionalità di conformità, vedere [Criteri di messaggistica e conformità](messaging-policy-and-compliance-exchange-2013-help.md) (Exchange 2013 ) o [Sicurezza e conformità per Exchange Online](https://technet.microsoft.com/it-it/library/jj200706\(v=exchg.150\)).

## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange 2013

[Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) Exchange Online

[Integrazione di regole di informazioni sensibili con le regole di trasporto](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)


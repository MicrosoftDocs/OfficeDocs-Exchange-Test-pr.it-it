---
title: 'Prevenzione della perdita di dati: Exchange 2013 Help'
TOCTitle: Prevenzione della perdita di dati
ms:assetid: 7c8ed3c1-ca91-4d9b-b16b-0a2b8ac89730
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150527(v=EXCHG.150)
ms:contentKeyID: 50479754
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Prevenzione della perdita di dati

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Informazioni sui criteri DLP, in Exchange Server 2013 ed Exchange Online, ad esempio il tipo di contenuto e come testarli. Sarà inoltre possibile sulle nuove funzionalità di Exchange DLP.

La prevenzione della perdita di dati (DLP) è un importante elemento dei sistemi di messaggistica aziendale a causa del vasto uso di posta elettronica per importanti comunicazioni aziendali che includono anche dati sensibili. Per poter applicare requisiti di conformità a quei dati e gestire il loro utilizzo nella posta elettronica, senza ostacolare la produttività dei lavoratori, le funzionalità di prevenzione della perdita di dati rendono la gestione dei dati sensibili facile come mai prima. Per una panoramica concettuale di DLP, guarda il seguente video.

> [!VIDEO https://www.microsoft.com/it-it/videoplayer/embed/31f2b48e-93ed-4be3-b46d-e7230c0fed8f]

I criteri DLP sono pacchetti semplici contenenti insiemi di condizioni, sono costituite da regole di trasporto, azioni e le eccezioni creati nell'interfaccia di amministrazione di Exchange (EAC) e quindi attivazione per filtrare i messaggi di posta elettronica e allegati. È possibile creare un criterio DLP ma sceglie di non attivare. In questo modo è possibile testare i criteri senza modificare il flusso della posta. I criteri DLP è possono utilizzare le potenzialità delle regole di trasporto esistenti. In realtà, un numero di nuovi tipi di regole di trasporto è stato creato in Microsoft Exchange Server 2013 e Exchange Online per poter eseguire nuove funzionalità DLP. Una nuova funzionalità delle regole di trasporto è un nuovo approccio per la classificazione delle informazioni riservate che possono essere incorporate in elaborazione del flusso della posta. Questa nuova funzionalità DLP consente di eseguire analisi approfondita del contenuto tramite adatta la parola chiave, dizionario corrispondenze, un'espressione regolare valutazione e altro contenuto esame per rilevare contenuti che violino i criteri DLP dell'organizzazione. La versione più recente di Exchange Online e Exchange 2013 SP1 aggiungere [Creazione impronta digitale documenti](overview-of-document-fingerprinting-in-exchange.md), che consente di rileva informazioni riservate nei moduli standard. Per ulteriori informazioni sulle regole di trasporto, vedere [Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013 ) o [Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) (Exchange Online ) e [Integrazione di regole di informazioni sensibili con le regole di trasporto](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md). È inoltre possibile gestire i criteri DLP utilizzando i cmdlet di Exchange Management Shell. Per ulteriori informazioni sui cmdlet di conformità e criteri, vedere [Cmdlet dei criteri e di conformità](https://technet.microsoft.com/it-it/library/dd298082\(v=exchg.150\)).

Oltre ai criteri DLP personalizzabili, è anche possibile informare i mittenti dei messaggi di posta elettronica che stanno per violare uno dei criteri definiti, anche prima che inviino un messaggio non conforme. A tale scopo è possibile configurare dei suggerimenti per i criteri. I suggerimenti sul criterio sono simili ai suggerimenti messaggio e possono essere configurati per presentare una breve nota nel client Microsoft Outlook 2013 che fornisce informazioni relative a possibili violazioni dei criteri alle persone che stanno creando un messaggio. Nella versione più recente di Exchange Online e in Exchange 2013 SP1, i Suggerimenti criteri vengono inoltre visualizzati in Outlook Web App e OWA per i dispositivi. Per ulteriori informazioni, vedere [Suggerimenti per i criteri](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).


> [!NOTE]
> Exchange Online: Prevenzione perdita dati (DLP) è una funzionalità premium che richiede una sottoscrizione Exchange Online Piano 2. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Confronto tra i piani di Exchange Online</A>.<BR>Exchange 2013: Prevenzione perdita dati (DLP) è una funzionalità premium che richiede una licenza di accesso client (CAL, Client Access License) di Enterprise di Exchange. Per ulteriori informazioni sulle licenze CAL e sulla gestione delle licenze server, vedere l'articolo relativo alla <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">gestione delle licenze di Exchange Server</A>.<BR><STRONG>CAL di Exchange Enterprise con servizi:</STRONG> Esiste una distinzione nel comportamento da tenere in considerazione se si è cliente CAL di Exchange Enterprise con servizi con distribuzione ibrida, in cui si dispone di alcune cassette postali in locale e altre in Exchange Online. I criteri DLP sono applicati in Exchange Online. Pertanto, i messaggi inviati da un utente in locale a un altro utente in locale non hanno criteri DLP applicati, poiché il messaggio non lascia l'infrastruttura in locale.



Ricerca di attività di gestione relative a prevenzione della perdita di dati? Vedere [Procedure DLP](dlp-procedures-exchange-2013-help.md) (Exchange 2013 ) o [Procedure DLP](https://technet.microsoft.com/it-it/library/jj938003\(v=exchg.150\)) (Exchange Online ).

**Sommario**

Establish policies to protect sensitive data

Sensitive information types in DLP policies

Detecting sensitive information along with traditional message classification

Detecting sensitive form data with Document Fingerprinting

Policy Tips notify users about sensitive content expectations

Information about DLP-processed messages

Installation prerequisites

For more information

## Stabilire criteri per proteggere i dati sensibili

Le funzionalità di prevenzione perdita dati possono essere d'aiuto per identificare e monitorare molte categorie di informazioni sensibili definite nelle condizioni dei propri criteri, quali ad esempio numeri di identificazione personale o numeri di carte di credito. Si possono definire i propri criteri personalizzati e regole di trasporto o utilizzare i modelli DLP predefiniti forniti da Microsoft per iniziare velocemente. Per ulteriori informazioni sui modelli di criteri inclusi, vedere [Modelli di criteri DLP forniti di Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md). Un *modello di criterio* include una serie di condizioni, regole e azioni che si possono scegliere per creare e salvare un criterio DLP effettivo che aiuta a ispezionare i messaggi. I modelli di criterio sono modelli dai quali è possibile selezionare o costruire le proprie regole specifiche per creare un criterio che corrisponda alle proprie necessità di prevenzione perdita di dati.

Esistono tre diversi metodi per iniziare a utilizzare DLP:

1.  **Applicare un modello pronto all'uso fornito da Microsoft.**   La via più veloce per iniziare a utilizzare i criteri DLP è creare e applicare un nuovo criterio utilizzando un modello. Questo evita lo sforzo di costruire un nuovo gruppo di regole dal nulla. È necessario sapere quale tipo di dati si vogliono controllare o quale regola di conformità si tenta di seguire. È anche necessario conoscere le aspettative aziendali per l'elaborazione di tali dati. Per ulteriori informazioni fare riferimento a [Modelli di criteri DLP forniti di Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md) e [Create a DLP policy from a template](how-to-new-dlp-data-loss-prevention-policy-template.md).

2.  **Importa un file di criteri precostruito proveniente dall'esterno dell'organizzazione.**   È possibile importare criteri provenienti dall'esterno del proprio ambiente di messaggistica creati da fornitori di software indipendenti. È così possibile estendere le soluzioni DLP per adattarle alle proprie esigenze aziendali. Maggiori informazioni su [Modelli di criteri di partner Microsoft](policy-templates-from-microsoft-partners-exchange-2013-help.md), [Definire modelli DLP e tipi di informazione propri](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md), e [Importare un modello di criteri DLP personalizzato da un file](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

3.  **Creare un criterio personalizzato senza alcuna condizione già esistente.**   La propria azienda può avere i propri requisiti per il monitoraggio di determinati dati esistenti nel sistema di messaggistica. È possibile creare un criterio personalizzato completamente proprio per iniziare il controllo e agire sui dati univoci dei messaggi. È necessario conoscere i requisiti e i vincoli dell'ambiente in cui il criterio DLP verrà applicato per poter creare quel criterio personalizzato. Per ulteriori informazioni fare riferimento a [Creare un criterio DLP personalizzato](create-a-custom-dlp-policy-exchange-2013-help.md).

Dopo aver aggiunto un criterio, è possibile revisionare e modificare le sue regole, disattivarlo o rimuoverlo completamente. Le procedure per queste azioni sono previste nell'argomento [Gestire i criteri DLP](manage-dlp-policies-exchange-2013-help.md).

## Tipi di informazioni sensibili nei criteri DLP

Quando si crea o modifica criteri DLP, è possibile includere le regole che includono controlli per le informazioni riservate. I tipi di informazioni riservate elencati nell'argomento [Cosa cercare i tipi di informazioni riservate in Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md) sono disponibili da utilizzare nei criteri. Le condizioni che si stabilisce all'interno di un criterio, ad esempio il numero di volte qualcosa deve trovarsi prima che viene eseguita un'azione o esattamente quali tale azione è può essere personalizzato entro i nuovi criteri personalizzati per soddisfare esigenze specifiche dei criteri. Per ulteriori informazioni sulla creazione DLP criteri, vedere [Creare un criterio DLP personalizzato](create-a-custom-dlp-policy-exchange-2013-help.md). Per ulteriori informazioni sulle regole di trasporto suite completa, vedere [Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013 ) o [Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) (Exchange Online ).

Per facilitare l'utilizzo di regole relative alle informazioni sensibili, Microsoft fornisce modelli di criteri che includono già alcuni tipi di informazioni sensibili. Non è possibile aggiungere tutti i tipi di informazioni sensibili qui elencate ai modelli di criteri poiché i modelli sono stati progettati per aiutare a focalizzare i tipi più comuni di dati relativi alla conformità all'interno dell'organizzazione. Per ulteriori informazioni sui modelli precostruiti, vedere [Modelli di criteri DLP forniti di Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md). È possibile creare numerosi criteri DLP per la proprie organizzazione e abilitarli tutti in modo da esaminare molti tipi diversi di informazioni. È anche possibile creare un criterio DLP che non sia basato su un modello esistente. Per iniziare la creazione di tale criterio, vedere [Creare un criterio DLP personalizzato](create-a-custom-dlp-policy-exchange-2013-help.md). Per ulteriori informazioni sui tipi di informazioni sensibili, vedere [Cosa cercare i tipi di informazioni riservate in Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md).

## Rilevamento di dati riservati con documento Fingerprinting

Con Exchange 2013 SP1 e l'ultima versione di Exchange Online, è possibile utilizzare [Creazione impronta digitale documenti](overview-of-document-fingerprinting-in-exchange.md) per facilitare la creazione di un tipo di informazioni riservate basate su un modulo standard. Per informazioni su come proteggere i dati del modulo, vedere [Proteggere i dati del modulo con documento fingerprinting](protect-form-data-with-document-fingerprinting-exchange-2013-help.md).

## Notifica agli utenti con un suggerimento per il criterio circa le aspettative di contenuti sensibili

È possibile utilizzare i suggerimenti per i criteri dei messaggi di notifica per informare i mittenti dei messaggi sui problemi di conformità possibili durante la creazione di un messaggio di posta elettronica. Quando si configura un suggerimento sul criterio in un criterio DLP, il messaggio di notifica verrà visualizzati solo se un elemento nel messaggio di posta elettronica del mittente soddisfa le condizioni descritte nel criterio. Suggerimenti sui criteri sono simili ai suggerimenti messaggio che sono stati introdotti in Microsoft Exchange 2010. Per ulteriori informazioni, vedere [Suggerimenti per i criteri](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

## Rilevamento di informazioni sensibili con classificazione tradizionale dei messaggi

Exchange 2013 e Exchange Online costituire un nuovo metodo di consentono di gestire i messaggi e allegati dati quando viene confrontato con classificazione tradizionale dei messaggi. Un fattore chiave per la potenza di una soluzione DLP è la possibilità di identificare correttamente contenuti sensibili o riservati che possono essere univoco per l'organizzazione, normativi, geography o altre esigenze aziendali. Exchange 2013 possibile ottenere questo risultato tramite una nuova architettura di analisi approfondita del contenuto associato a criteri di rilevamento definire tramite le regole dei criteri DLP. Come consentire impedire la perdita di dati in Exchange 2013 si basa su come configurare il set di regole di informazioni riservate corretto in modo che forniscono un elevato grado di protezione riducendo un'interruzione del flusso di posta elettronica inappropriate con falsi positivi e negativi. Questi tipi di regole, indicati in tali informazioni DLP sotto forma di rilevamento di informazioni riservate, funzione ambito offerti dalle regole di trasporto per abilitare funzionalità DLP.

Per ulteriori informazioni su queste nuove funzionalità, vedere [Integrazione di regole di informazioni sensibili con le regole di trasporto](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md). I campi di classificazione dei messaggi tradizionale ancora applicabili ai messaggi di Exchange e questi possono essere combinati con il rilevamento di informazioni riservate nuovo sia all'interno di un singolo criterio DLP o in esecuzione contemporaneamente in modo che vengono valutate in modo indipendente all'interno di Exchange. Per ulteriori informazioni sulle classificazioni dei messaggi legacy Exchange 2010, vedere [Informazioni sui messaggi classificazioni](https://go.microsoft.com/fwlink/?linkid=266612) nella libreria TechNet.

## Informazioni sui messaggi elaborati DLP

Per Exchange 2013 ottenere informazioni sui messaggi e i rilevamenti di criteri DLP nell'ambiente in uso, vedere [Visualizzare i report di rilevamento dei criteri DLP](view-dlp-policy-detection-reports-exchange-2013-help.md) e [Creare i rapporti operazioni non consentite per i rilevamenti di criteri DLP](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md). Dati relativi a rilevamenti di DLP è altamente integrato nello strumento di verifica messaggi rapporti di recapito di Exchange 2013.

Per Exchange Online, vedere [Visualizzare i report di rilevamento dei criteri DLP](https://technet.microsoft.com/it-it/library/dn904484\(v=exchg.150\)) e [Creare i rapporti operazioni non consentite per il rilevamento di criteri DLP](https://technet.microsoft.com/it-it/library/dn904486\(v=exchg.150\)).

## Prerequisiti di installazione

Per poter utilizzare le funzionalità DLP, Exchange 2013 o Exchange Online deve essere configurato con almeno una cassetta postale del mittente. Prevenzione perdita dati è una funzionalità premium che richiede una licenza CAL (Client Access License). Per ulteriori informazioni sulla preparazione all'uso di Exchange 2013, vedere [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md). Per ulteriori informazioni sulla preparazione all'uso di Exchange Online, vedere [Exchange Online](https://technet.microsoft.com/it-it/library/jj200580\(v=exchg.150\)).

## Ulteriori informazioni

Exchange 2013

  - [Criteri di messaggistica e conformità](messaging-policy-and-compliance-exchange-2013-help.md)

  - [Procedure DLP](dlp-procedures-exchange-2013-help.md)

  - [Visualizzare i report di rilevamento dei criteri DLP](view-dlp-policy-detection-reports-exchange-2013-help.md)

  - [Creazione impronta digitale documenti](overview-of-document-fingerprinting-in-exchange.md)

  - [Cmdlet dei criteri e di conformità](https://technet.microsoft.com/it-it/library/dd298082\(v=exchg.150\))

Exchange Online

  - [Sicurezza e conformità per Exchange Online](https://technet.microsoft.com/it-it/library/jj200706\(v=exchg.150\))

  - [Procedure DLP](https://technet.microsoft.com/it-it/library/jj938003\(v=exchg.150\))

  - [Visualizzare i report di rilevamento dei criteri DLP](https://technet.microsoft.com/it-it/library/dn904484\(v=exchg.150\))

  - [Creazione impronta digitale documenti](overview-of-document-fingerprinting-in-exchange.md)


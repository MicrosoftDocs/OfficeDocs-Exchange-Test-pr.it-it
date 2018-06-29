---
title: 'Definire modelli DLP e tipi di informazione propri: Exchange 2013 Help'
TOCTitle: Definire modelli DLP e tipi di informazione propri
ms:assetid: f4622dba-3347-4758-b4a2-f01b043c908c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ674310(v=EXCHG.150)
ms:contentKeyID: 50482016
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definire modelli DLP e tipi di informazione propri

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-01-14_

I modelli dei criteri di prevenzione per la perdita di dati (DLP) possono essere sviluppati come file XML indipendenti di Microsoft Exchange Server 2013 e quindi importati utilizzando l'interfaccia di amministrazione di Exchange o Exchange Management Shell. In questa sezione vengono descritti il processo e i dettagli della creazione e ottimizzazione dei file XML DLP da utilizzare in una soluzione DLP. Non è necessario sviluppare autonomamente i file XML DLP poiché l'interfaccia di amministrazione di Exchange consente all'utente di iniziare in modo semplice e rapido con i modelli di criteri DLP e le regole di trasporto esistenti per analizzare i messaggi.

Ricerca di attività di gestione relative ai modelli di criteri DLP? Vedere [Procedure DLP](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013 ) o [Procedure DLP](https://technet.microsoft.com/it-it/library/jj938003\(v=exchg.150\)) (Exchange Online ).


> [!NOTE]
> Exchange 2013: Prevenzione perdita dati (DLP) è una funzionalità premium che richiede una licenza di accesso client (CAL, Client Access License) di Enterprise di Exchange. Per ulteriori informazioni sulle licenze CAL e sulla gestione delle licenze server, vedere l'articolo relativo alla <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">gestione delle licenze di Exchange Server</A>.<BR>Exchange Online: Prevenzione perdita dati (DLP) è una funzionalità premium che richiede una sottoscrizione Exchange Online Piano 2. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Confronto tra i piani di Exchange Online</A>.




> [!IMPORTANT]
> La presente documentazione non ha come obiettivo consigliare un modello aziendale, informazioni sulla creazione di pacchetti di file, linee guida per la distribuzione delle regole per le informazioni riservate né discutere sulle modalità di distribuzione di tali regole. Inoltre, nella presente documentazione non vengono affrontati meccanismi di protezione come la crittografia per le regole distribuite personalizzate, né viene discussa la modalità di utilizzo di tali meccanismi.



## Ampliamento dei tipi di informazioni per soddisfare le esigenze degli utenti

Nelle sezioni successive vengono descritti i concetti e la definizione dello schema XML, che è indispensabile comprendere per iniziare a creare i propri file XML sia per i modelli di criteri DLP che per i pacchetti di regole delle informazioni riservate, che è possibile importare in Exchange 2013 e utilizzare come criteri DLP.

DLP in Microsoft Exchange consente di applicare criteri organizzativi specifici per le informazioni riservate. Un fattore chiave dell'efficacia della soluzione DLP è la possibilità di identificare in modo corretto le informazioni riservate o confidenziali peculiari dell'organizzazione, requisiti normativi, dislocazione geografica o altri aspetti aziendali. Sebbene Microsoft abbia fornito con il prodotto modelli di criteri e tipi di informazioni riservate per le attività iniziali, le esigenze aziendali peculiari potrebbero richiedere una soluzione di prevenzione della perdita dei dati personalizzata. Per questo motivo, Microsoft offre agli utenti un metodo per creare e importare i propri modelli di criteri DLP o le proprie definizioni di informazioni riservate all'interno dei pacchetti di regole di classificazione. Una soluzione DLP accurata si basa sulla configurazione di un insieme di regole appropriato per il motore di rilevamento delle informazioni riservate, in grado di offrire un livello elevato di protezione riducendo al minimo i falsi positivi e negativi.

## Sviluppo di modelli di criteri DLP personalizzati

È possibile scrivere il proprio file XML del modello di criteri DLP e importarlo. Questo approccio all'ampliamento della soluzione DLP fornito in Exchange consentirà di creare criteri DLP in grado di soddisfare nel modo migliore possibile i requisiti DLP.

La gestione dei modelli personalizzati e dei criteri correlati è simile alla gestione dei criteri DLP creati in base ai modelli forniti da Microsoft. In un ciclo di vita tipico DLP, è necessario procedere come segue:

1.  Creare un proprio modello di criteri DLP, un file XML personalizzato. Per ulteriori informazioni, vedere [Sviluppo di file modello per il criterio DLP](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

2.  Importare il modello personalizzato. Per ulteriori informazioni, vedere [Importare un modello di criteri DLP personalizzato da un file](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

3.  Creare un criterio DLP basato sul modello personalizzato. Per ulteriori informazioni, vedere [Create a DLP policy from a template](how-to-new-dlp-data-loss-prevention-policy-template.md).

4.  Aggiornare il modello personalizzato ripetendo i passaggi 1 e 2.

5.  Rimuovere il modello personalizzato. Per ulteriori informazioni, vedere [Remove-DlpPolicyTemplate](https://technet.microsoft.com/it-it/library/jj215739\(v=exchg.150\)).

Per ulteriori informazioni sulla definizione dello schema XML e sui concetti relativi allo sviluppo di modelli personalizzati, vedere [Sviluppo di file modello per il criterio DLP](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

## Sviluppo di tipi di informazioni riservate personalizzate e logica di corrispondenza nei pacchetti di regole di classificazione

È possibile scrivere le proprie definizioni di informazioni riservate in un pacchetto di regole di classificazione, ovvero un file XML, e importarlo come parte della soluzione DLP personalizzata. Il motore di rilevamento delle informazioni riservate offre funzionalità avanzate di analisi del contenuto per l'identificazione di informazioni riservate quali numeri di carte di credito, codici fiscali e proprietà intellettuale della società. Il motore è controllato da un insieme di istruzioni configurabili, o regole, per l'analisi del contenuto. Le regole vengono combinate in un pacchetto di regole di classificazione, un documento XML conforme alla definizione di schema XML per il pacchetto di regole standardizzate. Di seguito è illustrato come sviluppare un pacchetto personalizzato.

1.  Creare tipi di informazioni riservate personalizzate, un file XML personalizzato. Per ulteriori informazioni, vedere [Sviluppo di pacchetti di regole di informazioni riservate](technical-description-of-xml-schema-for-dlp-rule-packages.md).

2.  Importare il tipo di informazioni riservate personalizzato. Per ulteriori informazioni, vedere [New-ClassificationRuleCollection](https://technet.microsoft.com/it-it/library/jj218619\(v=exchg.150\)).

3.  Creare il modello personalizzato in base ai tipi di informazioni personalizzati. Per ulteriori informazioni, vedere [Sviluppo di pacchetti di regole di informazioni riservate](technical-description-of-xml-schema-for-dlp-rule-packages.md).

4.  Aggiornare il modello personalizzato ripetendo i passaggi 1 e 2.

5.  Rimuovere il modello personalizzato. Per ulteriori informazioni, vedere [Remove-ClassificationRuleCollection](https://technet.microsoft.com/it-it/library/jj218670\(v=exchg.150\)).

Per ulteriori informazioni sui pacchetti di regole, vedere [Sviluppo di pacchetti di regole di informazioni riservate](technical-description-of-xml-schema-for-dlp-rule-packages.md) e [Metodi e le tecniche per pacchetti di regole corrispondenti](technical-description-of-xsd-rule-matching-for-dlp-rule-packages.md).

## Informazioni sui tipi di regole nei pacchetti di regole

Le regole di un pacchetto configurano il processo di rilevamento delle caratteristiche di contenuto ben definite; ad esempio, le regole per la ricerca di un numero di patente di guida. Sono disponibili due principali tipi di regole: Entità e affinità.

Le regole *Entità* sono destinate a identificatori ben definiti (e spesso regolamentati) quali i numeri di previdenza sociale negli Stati Uniti. Un'entità è rappresentata da una raccolta di modelli numerabili. Un modello definisce un insieme di corrispondenze con identificatore di corrispondenza primario esplicito. Un esempio di entità è la patente di guida.

Le regole *Affinità* sono destinate a un determinato tipo di documento, ad esempio un rendiconto finanziario aziendale. Un'affinità è rappresentata come un insieme di prove indipendenti. Evidenza è un'aggregazione di corrispondenze necessarie entro una determinata prossimità. Un esempio di affinità è il Sarbanes-Oxley Act statunitense.

## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Importare un modello di criteri DLP personalizzato da un file](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

[New-ClassificationRuleCollection](https://technet.microsoft.com/it-it/library/jj218619\(v=exchg.150\))

[Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange Server 2013

[Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) Exchange Online

[Cosa cercare i tipi di informazioni riservate in Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)


---
title: 'Modelli di criteri DLP: Exchange 2013 Help'
TOCTitle: Modelli di criteri DLP
ms:assetid: c7b1a8e4-30d9-4409-85c5-f85ae023737d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657730(v=EXCHG.150)
ms:contentKeyID: 50481644
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modelli di criteri DLP

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-01-14_

È possibile utilizzare modelli di criteri criterio DLP perdita di dati per acquisire familiarità con la soluzione DLP in Microsoft Exchange 2013. Un modello di criterio DLP è un modello per un criterio. È possibile selezionare un modello per iniziare il processo di creazione dei criteri DLP personalizzati. All'interno dei criteri DLP, è possibile personalizzare le regole per garantire che soddisfi le esigenze aziendali per la prevenzione della perdita di dati. Sono disponibili numerosi modelli di criteri da Microsoft, ma non sono l'unico modo per implementare una soluzione di prevenzione della perdita di dati in Exchange.

Per informazioni sulle attività di gestione relative a modelli di criteri DLP vedere [Procedure DLP](dlp-procedures-exchange-2013-help.md).

**Sommario**

Extend the templates and information types to meet your needs

Create your own new DLP policy template

Include DLP functionality with existing transport rules

Use DLP policies created by Microsoft

For more information

## Estensione dei modelli e dei tipi di informazioni per soddisfare le proprie esigenze

È possibile incorporare i modelli del criterio e le definizioni per il contenuto riservato dai partner Microsoft o dai file sviluppati autonomamente come aggiunta ai modelli del criterio DLP, ai tipi di informazioni e alle regole già forniti in Exchange 2013. In questa sezione vengono presentati diversi modi per aggiungere il proprio contenuto per il criterio DLP ed estenderne la funzionalità. I modelli già forniti da Microsoft costituiscono un metodo conveniente per iniziare a utilizzare una soluzione DLP. Per estendere le funzionalità DLP con i file dei modelli del criterio DLP univoco, è necessario comprendere i requisiti dello schema XML per i modelli del criterio creati indipendentemente da Exchange. Per ulteriori informazioni sui cmdlet di Exchange Management Shell associati ai modelli di criteri DLP, vedere i cmdlet relativi a `Get-DlpPolicyTemplate` in [Cmdlet dei criteri e di conformità](https://technet.microsoft.com/it-it/library/dd298082\(v=exchg.150\)). È inoltre possibile definire i tipi di contenuto riservato dopo aver compreso il formato e la procedura per incorporarli. Per ulteriori informazioni sui cmdlet di Exchange Management Shell associati ai modelli di criteri DLP, vedere i cmdlet relativi a `Get-ClassificationRuleCollection` in [Cmdlet dei criteri e di conformità](https://technet.microsoft.com/it-it/library/dd298082\(v=exchg.150\)).


> [!WARNING]
> È opportuno attivare i criteri DLP in modalità di test prima di applicarli nell'ambiente di produzione vero e proprio. Durante i test, si consiglia di configurare delle cassette postali campione e di inviare dei messaggi di prova che richiamino i criteri di test in modo da poterne verificare i risultati.



## Creazione del proprio modello del criterio DLP o dei tipi di informazioni riservate in un pacchetto di regole di classificazione

È possibile creare un file di modello del criterio DLP indipendentemente da Exchange che soddisfi lo schema XML specifico fornito da Microsoft, quindi impostare il file nel sistema così da creare i criteri DLP partendo da esso. La creazione dei file dei modelli personalizzati consente di definire il proprio modello per i criteri DLP non ancora forniti da Microsoft. Non equivale alla creazione di un criterio DLP utilizzando Interfaccia di amministrazione di Exchange, come accade di solito una volta che i modelli del criterio sono disponibili. Se si crea un modello del criterio indipendente da Exchange, sarà necessario importarlo prima di poterlo utilizzare per analizzare i messaggi. È inoltre possibile creare le definizioni delle informazioni riservate indipendentemente da quelle definite da Microsoft in Exchange. È disponibile una definizione dello schema XML separata per i file del modello del criterio DLP e i pacchetti delle regole di classificazione. Per iniziare, vedere le seguenti informazioni:

  -  [Definire modelli DLP e tipi di informazione propri](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

  -  [Importare un modello di criteri DLP personalizzato da un file](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

## Inclusione della funzionalità DLP nelle regole di trasporto esistenti

Le funzionalità di rilevamento DLP possono essere incorporate nelle regole di trasporto tradizionali senza creare un nuovo criterio DLP. Se è già stato creato un set complesso di regole in una versione precedente di Exchange e si desidera duplicarle o aggiungere il rilevamento di informazioni riservate in Exchange 2013, utilizzare l'editor delle regole di trasporto in Interfaccia di amministrazione di Exchange o Exchange Management Shell per incorporare queste due nuove funzionalità. Per iniziare, vedere le seguenti informazioni:

  -  [Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

  -  [Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) (Exchange Online)

  -  [Gestire le regole di flusso di posta elettronica](manage-mail-flow-rules-exchange-2013-help.md)
    
  -  [Cmdlet dei criteri e di conformità](https://technet.microsoft.com/it-it/library/dd298082\(v=exchg.150\))

## Utilizzo dei criteri DLP creati da Microsoft

Numerosi criteri DLP vengono forniti da Microsoft. Si tratta del modo più semplice per iniziare a utilizzare una soluzione DLP che sia flessibile e facile da implementare. I criteri forniti possono sempre essere utilizzati come punto di partenza e personalizzati ulteriormente per soddisfare i propri requisiti. Per iniziare, vedere le seguenti informazioni:

  - [Modelli di criteri DLP forniti di Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)

  - [Create a DLP policy from a template](how-to-new-dlp-data-loss-prevention-policy-template.md)

## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)


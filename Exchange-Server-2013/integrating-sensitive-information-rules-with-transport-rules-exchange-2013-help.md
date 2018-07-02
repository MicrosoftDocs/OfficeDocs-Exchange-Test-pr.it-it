---
title: 'Integrazione di regole di informazioni sensibili con le regole di trasporto: Exchange 2013 Help'
TOCTitle: Integrazione di regole di informazioni sensibili con le regole di trasporto
ms:assetid: feb014a7-89dd-4f2d-a06d-52806ce435d4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150583(v=EXCHG.150)
ms:contentKeyID: 50479814
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Integrazione di regole di informazioni sensibili con le regole di trasporto

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-01-14_

In Microsoft Exchange, è possibile creare criteri DLP che contengono le regole per le classificazioni di messaggio tradizionale non solo e regole di trasporto esistenti, ma anche associarle con le regole di informazioni riservate rilevate all'interno di messaggi. Il framework di regole di trasporto esistenti offre funzionalità avanzate per definire i criteri di messaggistica, sulle versioni l'intero spettro dei soft ai controlli di disco rigido. Esempi:

  - Limitazione dell'interazione tra destinatari e mittenti, incluse le interazioni tra gruppi legati a un reparto all'interno di un'organizzazione.

  - Applicazione di criteri distinti per le comunicazioni all'interno e all'esterno di un'organizzazione.

  - Blocco di contenuto inappropriato in entrata o in uscita dall'organizzazione.

  - Applicazione di filtri alle informazioni riservate.

  - Verifica o archiviazione di messaggi inviati o ricevuti da determinate persone.

  - Reindirizzamento di messaggi in entrata o in uscita per l'ispezione prima del recapito

  - Applicazione di dichiarazioni di non responsabilità ai messaggi che transitano nell'organizzazione.

Le regole di trasporto consentono di applicare i criteri di messaggistica ai messaggi di posta elettronica che il flusso attraverso la pipeline di trasporto nel servizio di trasporto sui server cassette postali e nei server Trasporto Edge. Queste regole consentono agli amministratori di sistema applicare i criteri di messaggistica, assicurano messaggi Guida più sicura per proteggere i sistemi di messaggistica e impedire la perdita di informazioni accidentali. Per ulteriori informazioni sulle regole di trasporto, vedere [Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) ( Exchange Server 2013 ) o [Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) (Exchange Online ).

## Regole per le informazioni riservate nell'ambito del framework delle regole di trasporto

Le regole di informazioni riservate sono integrate con il framework di regole di trasporto dal Introduzione a una condizione che è possibile personalizzare: **Se il messaggio contiene... Informazioni riservate**. Questa condizione può essere configurata con uno o più tipi di informazioni riservate contenute nei messaggi. Quando vengono configurate più criteri DLP o le regole all'interno di un criterio con tali condizioni, il criterio o regola viene soddisfatta quando corrisponde a una delle condizioni. regole dei criteri Exchange esaminano l'oggetto, corpo e degli allegati del messaggio. Se la regola corrisponde a uno di questi componenti messaggio, verranno applicate le azioni delle regole.

La condizione di informazioni riservate può essere combinata con una qualsiasi delle regole di trasporto già esistenti per definire i criteri di messaggistica. Se combinato, la condizione può essere utilizzato in combinazione con altre regole e fornisce la semantica AND. Due diverse situazioni, ad esempio, vengono aggiunti insieme a un'istruzione AND in modo che sia necessario tenere conto per l'azione da applicare. Una delle azioni delle regole di trasporto possono essere configurata comporta le regole contenenti la corrispondenza del tipo di informazioni riservate. Molti tipi di file diversi possono essere eseguiti da agente delle regole di trasporto, che consente di analizzare i messaggi per applicare le regole di trasporto. Per ulteriori informazioni sui tipi di file supportati, vedere [Utilizzare le regole di trasporto per esaminare messaggi con allegati](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013 ) o [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/it-it/library/jj919236\(v=exchg.150\)) (Exchange Online ).

Le regole possono anche essere utilizzate nella parte dedicata alle eccezioni di una definizione di regola. L'utilizzo delle regole nella definizione delle eccezioni è indipendente dal loro utilizzo come condizione nell'ambito della regola. In questo modo si ottiene la flessibilità necessaria per la definizione di regole dotate di una condizione in grado di specificare più tipi di informazioni da applicare come parte della condizione e in grado anche di distinguere i tipi di informazioni nella condizione. Ciò consentirebbe criteri quali la corrispondenza di regole tradizionali specifiche di classificazione dei messaggi, ma non la corrispondenza di altri tipi di informazioni riservate prima di eseguire azioni che vengono definite in un criterio.

## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Cosa cercare i tipi di informazioni riservate in Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange Server 2013

[Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\)) Exchange Online

[Creare un criterio DLP personalizzato](create-a-custom-dlp-policy-exchange-2013-help.md)


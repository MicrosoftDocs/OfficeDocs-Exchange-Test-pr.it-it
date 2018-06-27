---
title: 'Novità delle regole di trasporto: Exchange 2013 Help'
TOCTitle: Novità delle regole di trasporto
ms:assetid: 0c2fc0b5-3cd2-4d79-aa2b-0c7622ae15a8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150483(v=EXCHG.150)
ms:contentKeyID: 50480012
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Novità delle regole di trasporto

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-10-03_

In Microsoft Exchange Server 2013, molti miglioramenti sono stati fatti per le regole di trasporto. In questo argomento, viene fornita una breve panoramica su alcuni dei miglioramenti e e delle modifiche principali. Per ulteriori informazioni sulle regole di trasporto, vedere [Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

## Supporto per le politiche di prevenzione della perdita dei dati

Le funzionalità di prevenzione della perdita di dati (DLP) in Exchange 2013 consentono alle organizzazioni di ridurre la divulgazione involontaria di dati importanti. Le regole di trasporto sono state aggiornate in modo da supportare le regole di creazione che accompagnano e rafforzano i criteri DLP. Per ulteriori informazioni sul supporto DLP nelle regole di trasporto, vedere i seguenti argomenti:

[Integrazione di regole di informazioni sensibili con le regole di trasporto](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

## Nuovi predicati e azioni

La funzionalità delle regole di trasporto è stata estesa tramite l'aggiunta di nuovi predicati e azioni. È possibile utilizzare ciascun predicato riportato di seguito come una condizione o un'eccezione durante la creazione di regole di trasporto.

Per informazioni dettagliate sull'uso di questi nuovi predicati e azioni, vedere [Condizioni delle regole di trasporto (predicati)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) e [Azioni della regola di trasporto](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md).

## Nuovi predicati

  -  
    **AttachmentExtensionMatchesWords**   Utilizzato per rilevare messaggi che contengono allegati con estensioni specifiche.

  -  
    **AttachmentHasExecutableContent**   Utilizzato per rilevare messaggi che contengono allegati con contenuto eseguibile.

  -  
    **HasSenderOverride** Utilizzato per rilevare messaggi in cui il mittente ha scelto di sostituire una restrizione del criterio DLP.

  -  
    **MessageContainsDataClassifications**   Utilizzato per rilevare informazioni importanti nel corpo del messaggio e in uno qualsiasi degli allegati. Per un elenco delle classificazioni dati disponibili, vedere [Cosa cercare i tipi di informazioni riservate in Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md).

  -  
    **MessageSizeOver**   Utilizzato per rilevare messaggi le cui dimensioni generali sono superiori o uguali al limite specificato.

  -  
    **SenderIPRanges**   Utilizzato per rilevare messaggi inviati da un gruppo specifico di intervalli di indirizzi IP.

## Nuove azioni

  -  
    **GenerateIncidentReport**   Genera un rapporto sulle operazioni non consentite che viene inviato a un determinato indirizzo SMTP. L'azione dispone anche di un parametro chiamato *IncidentReportOriginalMail* che accetta uno di questi due valori: IncludeOriginalMail o DoNotIncludeOriginalMail.

  -  
    **NotifySender**   Controlla la modalità di notifica al mittente di un messaggio che non rispetta un criterio DLP. È possibile scegliere di informare semplicemente il mittente e instradare il messaggio normalmente oppure di rifiutare il messaggio e inviare una notifica al mittente.

  -  
    **StopRuleProcessing**   Interrompe l'elaborazione di tutte le regole successive sul messaggio.

  -  
    **ReportSeverityLevel**   Imposta il livello di gravità specificato nel rapporto sulle operazioni non consentite. I valori per l'azione sono: Informativo, Basso, Medio, Alto e Disattivato.

  -  
    **RouteMessageOutboundRequireTLS**   Richiede la crittografia TLS (Transport Layer Security) durante il routing del messaggio all'esterno dell'organizzazione. Se la crittografia TLS non è supportata, il messaggio viene rifiutato e non consegnato.

## Altre modifiche nelle regole di trasporto

  - **Supporto per la sintassi di espressioni regolari estese**   Le regole di trasporto in Exchange 2013 si basano sulla funzionalità delle espressioni regolari (regex) di Microsoft.NET Framework e supportano, ora, la sintassi di espressioni regolari estese.

  - **Richiamo dell'agente Regole di trasporto**   La principale modifica all'architettura in Exchange 2013 per le regole di trasporto è che l'agente Regole di trasporto viene richiamato su onResolvedMessage. Nelle precedenti versioni di Exchange, l'agente delle regole veniva richiamato su onRoutedMessage. Questa modifica ha consentito di aggiungere nuovi azioni, quali la richiesta della crittografia TLS, che possono cambiare la modalità di routing di un messaggio. Per ulteriori informazioni sull'architettura delle regole di trasporto in Exchange 2013, vedere [Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

  - **Informazioni dettagliate sulle regole di trasporto nei registri di verifica dei messaggi**   Informazioni dettagliate sulle regole di trasporto sono ora incluse nei registri di verifica dei messaggi. Le informazioni includono quali regole sono state attivate per un determinato messaggio e le azioni intraprese come risultato dell'elaborazione di tali regole.

  - **Nuova funzionalità di monitoraggio delle regole**   Exchange 2013 monitora le regole di trasporto configurate e calcola il costo di esecuzione di tali regole sia durante la creazione della regola sia durante il normale utilizzo. Exchange è in grado di rilevare e generare avvisi per le regole che causano ritardi nel recapito della posta.


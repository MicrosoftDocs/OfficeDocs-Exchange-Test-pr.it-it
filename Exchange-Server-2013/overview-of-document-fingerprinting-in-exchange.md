---
title: 'Creazione impronta digitale documenti: Exchange 2013 Help'
TOCTitle: Creazione impronta digitale documenti
ms:assetid: 1e0c579c-26e0-462a-a1b0-d7506dfe05fa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn635176(v=EXCHG.150)
ms:contentKeyID: 61202264
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creazione impronta digitale documenti

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-09-11_

Gli Information Worker dell'organizzazione gestiscono molti tipi di informazioni riservate durante una giornata. *La creazione impronta digitale documenti* rende più semplice proteggere le informazioni identificando moduli standard utilizzati all'interno dell'organizzazione. In questo argomento vengono forniti i concetti dietro la creazione impronta digitale documenti. Se si desidera imparare a creare un'impronta digitale del documento, vedere [Proteggere i dati del modulo con documento fingerprinting](protect-form-data-with-document-fingerprinting-exchange-2013-help.md).

## Scenario di base per la creazione impronta digitale documenti

La creazione impronta digitale documenti è una funzionalità per la prevenzione della perdita di dati che converte un modulo standard in un tipo di informazione sensibile, che può essere usato per definire regole di trasporto e criteri DLP. Ad esempio, è possibile creare l'impronta digitale di un documento basata su un modello di brevetto vuoto e creare quindi un criterio DLP che rileva e blocca tutti i modelli di brevetto in uscita contenenti dati sensibili. In alternativa, è possibile configurare [Suggerimenti per i criteri](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md) per avvertire i mittenti che potrebbero inviare informazioni sensibili e il mittente dovrà verificare che i destinatari sono autorizzati a ricevere brevetti. Questo processo funziona con tutti i moduli basati su testo utilizzati nell'organizzazione. Ulteriori esempi di moduli che è possibile caricare includono:

  - Moduli governativi

  - Moduli di conformità Health Insurance Portability and Accountability Act (HIPAA)

  - Moduli di informazioni dei dipendenti per i reparti delle risorse umane

  - Moduli personalizzati creati specificamente per l'organizzazione

In teoria, l'organizzazione possiede già una pratica aziendale stabilita relativa all'utilizzo di alcuni moduli per la trasmissione di dati sensibili. Dopo aver caricato un modulo vuoto da convertire in un'impronta digitale del documento e aver configurato un criterio corrispondente, l'agente DLP rileverà i documenti nella posta in uscita che corrispondono a tale impronta digitale.

## Funzionamento dell'impronta digitale del documento

Sarà già chiaro che i documenti non hanno impronte digitali nel verso senso della parola, ma il nome consente di spiegare la funzionalità. Come le impronti digitali di una persona presentano criteri univoci, così i documenti presentano modelli di parole univoci. Quando si carica un file, l'agente DLP identifica il modello di parole nel documento, crea un'impronta digitale del documento in base al modello e usa l'impronta digitale del documento per individuare i documenti in uscita contenenti lo stesso modello. Ecco perché il caricamento di un modulo o modello crea il tipo più efficace di impronta digitale del documento. Chiunque compila un modulo usa lo stesso set originale di parole e poi aggiunge proprie parole al documento. Finché il documento in uscita non è protetto da password e contiene tutto il testo del modulo originale, l'agente DLP può determinare se il documento corrisponde all'impronta digitale del documento.

Il seguente esempio mostra cosa accade si crea un'impronta digitale del documento in base al modello di brevetto. È comunque possibile usare qualsiasi modello per la creazione di un'impronta digitale del documento.

**Esempio di un documento di brevetto corrispondente a un'impronta digitale del documento di un modello di brevetto**

![Un documento di licenza corrispondente a un'impronta digitale del documento.](images/Dn635176.9c952770-2cd4-4f62-9735-6d073344be7f(EXCHG.150).png "Un documento di licenza corrispondente a un'impronta digitale del documento.")

Il modello di brevetto contiene i campi bianchi "Titolo del brevetto", "Inventori" e "Descrizione" e le descrizioni per ognuno di questi campi, vale a dire il modello di parole. Quando viene caricato il modello di brevetto originale, è in uno dei tipi di file supportati e in testo normale. L'agente DLP usa un algoritmo per convertire il modello di parole in un'impronta digitale del documento, che è un piccolo file XML Unicode contenente un valore hash univoco che rappresenta il testo originale e l'impronta digitale viene salvata come classificazione di dati in Active Directory. Come misura di sicurezza, il documento originale non viene memorizzato nel servizio; viene memorizzato solo il valore hash e non è possibile ricostruire il modello originale a partire dal valore hash. L'impronta digitale del brevetto diventa poi un tipo di informazione sensibile da associare a un criterio DLP. Dopo aver associato l'impronta digitale a un criterio DLP, l'agente DLP rileva i messaggi di posta elettronica in uscita contenenti documenti che corrispondono all'impronta digitale del brevetto e li tratta in base ai criteri dell'organizzazione. Ad esempio, si potrebbe voler configurare un criterio DLP che impedisce ai normali dipendenti di inviare messaggi in uscita contenenti brevetti. L'agente DLP utilizzerà l'impronta digitale del brevetto per individuare i brevetti e bloccare questi messaggi di posta elettronica. In alternativa, si potrebbe consentire al reparto legare di inviare brevetti ad altre organizzazioni perché deve poterlo fare per lavorare. È possibile consentire a reparti specifici di inviare informazioni sensibili creando eccezioni per tali reparti nel criterio DLP oppure è possibile consentire loro di ignorare un criterio con una giustificazione aziendale. Per informazioni più dettagliate sulla creazione di regole ed eccezioni di criteri DLP, vedere [Procedure DLP](https://technet.microsoft.com/it-it/library/jj938003\(v=exchg.150\)). Per ulteriori informazioni sulla configurazione di suggerimenti di criteri che gli utenti possono ignorare, vedere [Gestire i suggerimenti sui criteri](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).

## Tipi di file supportati

Creazione impronta digitale documenti supporta gli stessi tipi di file supportati nelle regole di trasporto. Per un elenco di tipi di file supportati, vedere [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/it-it/library/jj919236\(v=exchg.150\)). Una nota rapida sui tipi di file: le regole di trasporto né impronta digitale del documento supporta il tipo di file con estensione dotx, che può risultare complessa perché è un file di modello di Word. Quando viene visualizzata la parola "modello" in questo e altri argomenti impronta digitale del documento, fa riferimento a un documento che è stato stabilito come un modulo standard, non il tipo di file di modello.

## Limitazioni della creazione dell'impronta digitale del documento

L'agente DLP della creazione dell'impronta digitale del documento non rileva informazioni riservate nei seguenti casi:

  - File protetti da password

  - File che contengono solo immagini

  - Documenti che non contengono tutto il testo del modulo originale usato per la creazione dell'impronta digitale del documento

## Ulteriori informazioni

[Proteggere i dati del modulo con documento fingerprinting](protect-form-data-with-document-fingerprinting-exchange-2013-help.md)

[Integrazione di regole di informazioni sensibili con le regole di trasporto](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

[Procedure DLP](https://technet.microsoft.com/it-it/library/jj938003\(v=exchg.150\))


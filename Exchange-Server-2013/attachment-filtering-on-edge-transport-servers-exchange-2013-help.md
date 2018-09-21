---
title: 'Filtro degli allegati nei server Trasporto Edge: Exchange 2013 Help'
TOCTitle: Filtro degli allegati nei server Trasporto Edge
ms:assetid: be39a181-c82e-41f5-8846-085bf1f84164
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124399(v=EXCHG.150)
ms:contentKeyID: 60829843
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtro degli allegati nei server Trasporto Edge

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-02-10_

In Microsoft Exchange Server 2013, è possibile utilizzare la funzionalità di filtro degli allegati sui server Trasporto Edge per controllare gli allegati che gli utenti ricevono nei messaggi di posta elettronica. Il filtro degli allegati viene eseguito dall'agente di filtro degli allegati, che è disponibile soltanto sui server Trasporto Edge.

## Tipi di filtro degli allegati

È possibile utilizzare i seguenti tipi di filtro allegati per controllare gli allegati in entrata o in uscita dall'organizzazione attraverso il server Trasporto Edge:

  - **Applicazione del filtro in base al nome file o all'estensione del file**   È possibile specificare il nome file esatto o l'estensione del nome file da filtrare. Un esempio di un filtro del nome file è rappresentato da `BadFileName.exe`. Un esempio di un filtro dell'estensione nome file è rappresentato da `*.exe`.

  - **Applicazione del filtro in base al tipo di contenuto MIME del file**   Specificare un valore relativo al tipo di contenuto MIME da filtrare. Tale valore indica in cosa consiste l'allegato, ad esempio un'immagine JPEG, un file eseguibile o un file di Microsoft Excel. I tipi di contenuto sono rappresentati come `type/subtype`. Ad esempio, un file d'immagine JPEG viene espresso come `image/jpeg`.
    
    Per visualizzare un elenco completo delle estensioni dei nomi dei file e dei tipi di contenuto che possono essere rilevati dal filtro degli allegati, eseguire il comando riportato di seguito sul server Trasporto Edge:
    
    ```powershell
Get-AttachmentFilterEntry | Format-List
```

Dopo aver definito i file da cercare, è possibile configurare l'azione da intraprendere in merito ai messaggi che contengono tali allegati. Non è possibile specificare azioni differenti per tipi differenti di allegati. È possibile configurare una delle seguenti azioni per tutti i messaggi che corrispondono a uno dei filtri degli allegati:

  - **Rifiuta (blocca) il messaggio** Il messaggio viene bloccato. Il mittente riceve un rapporto di mancato recapito in cui viene spiegato che il messaggio non è stato recapitato poiché conteneva un allegato inaccettabile. È possibile personalizzare il testo nel rapporto di mancato recapito. Il testo predefinito è: `Message rejected due to unacceptable attachments`.

  - **Rimuovi allegato ma consenti messaggio**   L'allegato viene rimosso dal messaggio. Tuttavia, il messaggio e altri allegati che non corrispondono al filtro sono consentiti. Se l'allegato viene rimosso, sarà sostituito da un file di testo in cui vengono spiegati i motivi della rimozione. Si tratta dell'azione predefinita.

  - **Elimina in modo silente messaggio**   Il messaggio viene eliminato. Né il mittente né il destinatario ricevono la notifica.

Per ulteriori informazioni, vedere [Gestione di filtro degli allegati nei server Trasporto Edge](manage-attachment-filtering-on-edge-transport-servers-exchange-2013-help.md).


> [!NOTE]
> È possibile recuperare i messaggi che sono stati bloccati o gli allegati che sono stati rimossi. Quando si configura il filtro allegati, esaminare attentamente tutte le possibili corrispondenze dei nomi file e verificare che agli allegati legittimi non venga applicato alcun filtro.<BR>Inoltre, si consiglia di non rimuovere gli allegati dai messaggi di posta elettronica con firma digitale, crittografati o protetti da diritti. Rimuovendo gli allegati da tali messaggi, verranno resi non validi i messaggi con firma digitale e i messaggi crittografati o protetti da diritti risulteranno illeggibili.



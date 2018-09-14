---
title: 'Elementi non ricercabili in Exchange eDiscovery: Exchange 2013 Help'
TOCTitle: Elementi non ricercabili in Exchange eDiscovery
ms:assetid: 32550081-9af9-474b-ae7b-28f1e68cad41
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn602498(v=EXCHG.150)
ms:contentKeyID: 61071986
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Elementi non ricercabili in Exchange eDiscovery

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In eDiscovery In locale per Exchange Server 2013 e Exchange Online, gli elementi non ricercabili sono elementi delle cassette postali che non possono essere indicizzati da ricerca di Exchange o che sono state indicizzate solo parzialmente. Un elemento non ricercabili in genere contiene un file che non possono essere indicizzato, allegato a un messaggio di posta elettronica. Ecco alcuni motivi per cui i file non possono essere indicizzati per la ricerca e vengono restituiti come un elemento non ricercabili quando associato a un messaggio di posta elettronica:

  - Il tipo di file non è supportato per l'indicizzazione perché non è installato un filtro di ricerca (noto anche come *IFilter*) per indicizzare il formato di file.

  - Il tipo di file è disabilitato per l'indicizzazione.

  - Il tipo di file è supportato per l'indicizzazione ma si è verificato un errore di indicizzazione per un file specifico.

  - Un file è crittografato con tecnologie non Microsoft.

  - Un file è protetto da password.

Affinché la ricerca eDiscovery abbia esito positivo, è possibile che l'organizzazione debba rivedere alcuni elementi non ricercabili. È possibile specificare se includere gli elementi non ricercabili quando si copiano i risultati della ricerca di eDiscovery in una cassetta postale di individuazione o si esportano i risultati in un file PST.

## Tipi di file non supportati per la ricerca

Alcuni tipi di file, ad esempio Bitmap o MP3, non contengono contenuto che può essere indicizzato. Di conseguenza, ricerca di Exchange non esegue l'indice full-text su questi tipi di file. Questi tipi di file vengono considerati come tipi di file non supportati. Vi sono inoltre i tipi di file per cui indice full-text è stato disattivato, per impostazione predefinita o da un amministratore. Tipi di file non supportati e disabilitata vengono considerati elementi non ricercabili nelle ricerche eDiscovery. Questi tipi di file che vengono in genere associati a un messaggio di posta elettronica, vengono inclusi nel set di risultati quando si includono gli elementi non ricercabili durante la copia o esportazione dei risultati della ricerca. Per un elenco dei formati di file disabilitati e non supportate, vedere [Formati di file indicizzati da ricerca di Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md). In Exchange Server 2013, gli amministratori possono disattivare l'indicizzazione per un formato di file supportati utilizzando il cmdlet [Set-SearchDocumentFormat](https://technet.microsoft.com/it-it/library/jj873756\(v=exchg.150\)) . Questo cmdlet non è disponibile in Exchange Online.

Per identificare gli elementi non ricercabili in una cassetta postale specifica, è possibile eseguire il cmdlet [Get-FailedContentIndexDocuments](https://technet.microsoft.com/it-it/library/dd351154\(v=exchg.150\)) per ottenere un elenco di elementi da copiare o esportare quando si sceglie di includere elementi non ricercabili nei risultati della ricerca.

## Messaggi con i tipi di file non supportati restituiti nei risultati della ricerca

Non tutti i messaggi con un allegato di file non supportato vengono automaticamente restituiti come un elemento non ricercabile. Questo perché altre proprietà del file, ad esempio il nome del file, sono indicizzate e possono essere cercate. Ad esempio, una ricerca con parola chiave "financial" restituirà un messaggio con un allegato non supportato se la parola chiave è presente nel nome del file. Se la parola chiave è presente solo nel corpo del file allegato, il messaggio verrà restituito come elemento non ricercabile.

Allo stesso modo, i messaggi con allegati file non supportati vengono inclusi nei risultati della ricerca quando altre proprietà di un elemento della cassetta postale, indicizzate e ricercabili, soddisfano i criteri di ricerca. Le proprietà del messaggio che vengono indicizzate per la ricerca includono le date di invio e ricezione, il mittente e il destinatario, il nome del file di un allegato e il testo nel corpo del messaggio. Pertanto, anche se un messaggio con allegato non è ricercabile, il messaggio verrà incluso nei risultati della ricerca normali se il valore di altre proprietà del messaggio corrisponde ai criteri di ricerca. Infatti, è comune che i messaggi con allegati non ricercabili vengano inclusi nei risultati della ricerca normali.

Per un elenco delle proprietà del messaggio di posta elettronica indicizzato per la ricerca, vedere [Proprietà messaggi indicizzati da ricerca di Exchange](message-properties-indexed-by-exchange-search-exchange-2013-help.md).

## Includere gli elementi non ricercabili nei risultati della ricerca

L'organizzazione potrebbe dover identificare ed eseguire un'ulteriore elaborazione degli elementi non ricercabili per determinare cosa contengono e se sono rilevanti. Per includere gli elementi non ricercabili nei risultati della ricerca di eDiscovery, è possibile utilizzare l'opzione relativa agli elementi non ricercabili quando si copiano o esportano i risultati della ricerca. Per includere gli elementi non ricercabili quando si usa In-Place eDiscovery in Exchange o Exchange Online, selezionare l'opzione **Includi elementi senza funzioni di ricerca** quando si copiano i risultati della ricerca in una cassetta postale di individuazione o li si esporta in un file PST. Per includere gli elementi non ricercabili quando si usa eDiscovery Center in SharePoint o SharePoint Online, selezionare l'opzione **Includere gli elementi crittografati o in un formato non riconosciuto**.

Tenere presente durante la copia o l'esportazione di elementi non ricercabili che:

  - Quando si copiano elemento non ricercabili in una cassetta postale di individuazione, gli elementi non ricercabili vengono copiati in una cartella separata denominata **Non ricercabile**, che si trova nella cartella contenente i risultati della ricerca. Quando si esportano i risultati della ricerca e si includono gli elementi non ricercabili, questi vengono esportati in un file PST separato.

  - Quando si includono gli elementi non ricercabili nei risultati della ricerca, verranno restituiti tutti gli elementi non ricercabili nelle cassette postali nelle quali viene eseguita la ricerca, indipendentemente dai criteri di ricerca.

  - Se si sceglie di includere nei risultati della ricerca tutti gli elementi della cassetta postale o se una query di ricerca non specifica parole chiave o specifica solo un intervallo di date, è possibile che gli elementi non ricercabili non vengano copiati nella cartella **Non ricercabile** se si seleziona l'opzione per includere gli elementi non ricercabili. Questo perché tutti gli elementi, compresi gli elementi non ricercabili, vengano inclusi automaticamente nei risultati della ricerca normali.

  - Come affermato in precedenza, poiché le proprietà e i metadati di un messaggio sono indicizzati, la ricerca per parola chiave potrebbe restituire risultati se la parola chiave è presente nelle proprietà o nei metadati di un messaggio al quale è allegato un file non ricercabile. In questo caso, anche due copie dello stesso elemento della cassetta posta verranno incluse nei risultati della ricerca. Per impedire questo tipo di deduplicazione e per includere solo una copia dell'elemento nei risultati della ricerca normali, è possibile selezionare l'opzione **Abilita deduplicazione** quando si copiano o esportano i risultati della ricerca.

  - Se si includono gli elementi non ricercabili nei risultati della ricerca, vengono influenzati anche i risultati della ricerca attesi che sono visualizzati. Se si includono elementi non ricercabili quando si copiano i risultati della ricerca, il numero totale di elementi stimato e le dimensioni totali stimate includeranno gli elementi non ricercabili.

Per ulteriori informazioni sull'inserimento degli elementi non ricercabili nei risultati della ricerca, vedere:

  - [Creazione di una ricerca eDiscovery sul posto](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [Esportazione dei risultati della ricerca eDiscovery in un file PST](https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-ediscovery/export-search-results)

  - [SharePoint: esportazione di contenuto eDiscovery e creazione di report](https://go.microsoft.com/fwlink/p/?linkid=324757)

## Ulteriori informazioni sugli elementi non ricercabili

  - Anche se un tipo di file è supportato dal servizio di ricerca di Exchange ed è indicizzato full-text, possono verificarsi errori di indicizzazione o ricerca che causeranno la restituzione di un file come elemento non ricercabile. Ad esempio, la ricerca di un file molto grande di Excel potrebbe riuscire parzialmente, ma potrebbe poi non riuscire se il limite di dimensioni viene superato. In questo caso, è possibile che lo stesso file venga restituito con i risultati della ricerca e come elemento non ricercabile.

  - I file allegati crittografati con le tecnologie Microsoft vengono indicizzati dalla ricerca di Exchange e ne viene eseguita la ricerca. I file crittografati con tecnologie non Microsoft vengono restituiti come non ricercabili.

  - Messaggi di posta elettronica crittografati con S/MIME non vengono indicizzati e sono considerati elementi non ricercabili. Sono inclusi i messaggi crittografati con o senza allegati.

  - I messaggi protetti con la funzionalità IRM (Information Rights Management) vengono indicizzati dalla ricerca di Exchange e inclusi nei risultati della ricerca se corrispondono ai parametri di query. Per ulteriori informazioni su IRM, vedere [Information Rights Management](information-rights-management-exchange-2013-help.md).

  - Come affermato in precedenza, poiché le proprietà e i metadati di un messaggio sono indicizzati, la ricerca per parola chiave potrebbe restituire risultati se la parola chiave è presente nei metadati indicizzati. Tuttavia, la stessa ricerca per parola chiave potrebbe non restituire lo stesso elemento se la parola chiave è presente solo nel contenuto di un elemento allegato con un tipo di file non supportato. In questo caso, l'elemento verrebbe restituito solo come un elemento non ricercabile.

  - In eDiscovery di Exchange 2010, esiste il concetto di *elenco di indirizzi attendibili*. Sono tipi di file con contenuti non ricercabili e che non vengono quindi indicizzati dalla ricerca di Exchange: ad esempio i file Windows Media Video (.wmv) e Waveform Audio (.wav). Poiché questi tipi di file non presentano contenuti ricercabili, non vengono considerati elementi non ricercabili in Exchange 2010. Gli elementi della cassetta postale contenenti questi tipi di file non vengono restituiti come elementi non ricercabili, né vengono copiati nella cassetta postale di individuazione.
    
    Non esiste più un elenco di indirizzi attendibili in Exchange 2013 o Exchange Online. I tipi di file sono attivati o disattivati per l'indicizzazione o non sono supportati. I tipi di file disabilitati e non supportati sono considerati elementi non ricercabili.


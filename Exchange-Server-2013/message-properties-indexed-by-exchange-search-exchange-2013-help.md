---
title: 'Proprietà messaggi indicizzati da ricerca di Exchange: Exchange 2013 Help'
TOCTitle: Proprietà messaggi indicizzati da ricerca di Exchange
ms:assetid: a9754dc1-44aa-4076-8b59-a5d39246d5b0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ983804(v=EXCHG.150)
ms:contentKeyID: 52063093
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Proprietà messaggi indicizzati da ricerca di Exchange

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-17_

Con il servizio Ricerca di Exchange vengono indicizzate molte proprietà degli elementi, ad esempio mittente, destinatari, corpo del messaggio e allegati dei messaggi di posta elettronica.

## Proprietà indicizzate tramite Ricerca di Exchange

La tabella seguente contiene un elenco di tutte le proprietà degli elementi indicizzate tramite Ricerca di Exchange.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Proprietà</th>
<th>Tipo</th>
<th>Disponibile per query</th>
<th>Disponibile per la ricerca</th>
<th>Recuperabile</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Account</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Assistantname</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Attachment</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Attachmentfilenames</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Attachmentmetaproperties</p></td>
<td><p>Stringa</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Attachmentcount</p></td>
<td><p>Numero intero</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Bcc</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Body</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Businessaddress</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Businessmainphone</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Businessphonenumber</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Carphonenumber</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Categoria</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Cc</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Companyname</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Compositeitemid</p></td>
<td><p>Stringa</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Conversationid</p></td>
<td><p>Numero intero</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Conversationtopic</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Departmentname</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>DisplayName</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Displaynameprefix</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Documentid</p></td>
<td><p>Numero intero</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Emaildisplayname</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Emailoriginaldisplayname</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Errorcode</p></td>
<td><p>Numero intero</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Fileas</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Firstname</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Folderid</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>From</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Homeaddress</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Homephone</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>Numero intero</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Ispartiallyprocessed</p></td>
<td><p>Booleano</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Ispermanentfailure</p></td>
<td><p>Booleano</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Itemclass</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Kind</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Lastattempttime</p></td>
<td><p>DateTime</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Lastname</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Mailboxguid</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Manager</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Meetinglocation</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Middlename</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Mobilephonenumber</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Nickname</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Officelocation</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Otheraddress</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Primarytelephonenumber</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>DateTime</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Receivedby</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Receivedrepresenting</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Recipients</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>DateTime</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Sharinginfo</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>Numero intero</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Tasktitle</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Title</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>To</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Umaudionotes</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Watermark</p></td>
<td><p>Numero intero</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Yomicompanyname</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Yomifirstname</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Yomilastname</p></td>
<td><p>Stringa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


**Note sulle proprietà indicizzate**:

  - **Proprietà sottoponibile a query** possono essere utilizzate nelle query AQS per i client di ricerca, ad esempio Outlook Web App`property:value` coppie, ad esempio `from:bsuneja@cotoso.com`. Un sottoinsieme delle proprietà sottoponibile a query elencate nella tabella precedente è utilizzabile anche nelle query di ricerca di eDiscovery In locale. Per un elenco di queste proprietà, vedere [Proprietà di messaggi e operatori di ricerca per eDiscovery In locale](message-properties-and-search-operators-for-https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery).

  - **Proprietà disponibili per le ricerche** sono proprietà che non è possibile specificare coppie `property:value` , ma una ricerca tramite parola chiave restituisce il valore se disponibili in tutte le proprietà supportano la ricerca. Ad esempio, è possibile utilizzare `body:Contoso` per cercare la stringa `contoso` nel corpo del messaggio solo. Tuttavia, una ricerca per la stringa restituirà tutti gli elementi in cui la proprietà viene rilevata in tutte le proprietà supportano la ricerca.

  - Le **proprietà recuperabili** come `documenteid` e `ispartiallyprocessed` vengono restituite con ogni ricerca.


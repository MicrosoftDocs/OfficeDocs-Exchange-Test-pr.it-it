---
title: 'Contatori delle prestazioni per la gestione dei record di messaggistica: Exchange 2013 Help'
TOCTitle: Contatori delle prestazioni per la gestione dei record di messaggistica
ms:assetid: b59def6f-4249-4e0c-8057-8ae6eb7c5676
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb310790(v=EXCHG.150)
ms:contentKeyID: 51407400
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Contatori delle prestazioni per la gestione dei record di messaggistica

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

I contatori delle prestazioni descritti in questo argomento consentono di monitorare l'implementazione della gestione dei record di messaggistica (MRM) per Microsoft Exchange Server 2010. Siccome l'esecuzione dell'Assistente cartelle gestite è un processo a elevato utilizzo di risorse, è necessario eseguirlo solo quando il server può tollerare il carico aggiuntivo. Quando Assistente cartelle gestite è in esecuzione, è necessario monitorare anche le prestazioni del server. Oltre ai contatori delle prestazioni elencati in questo argomento, è possibile disporre di ulteriori contatori delle prestazioni per il monitoraggio di elementi quali prestazioni del disco e utilizzo della CPU.

Per ulteriori informazioni sul monitoraggio dei computer che eseguono la gestione dei record di messaggistica, vedere [Gestione dei record di messaggistica di monitoraggio](monitoring-messaging-records-management-exchange-2013-help.md).

## Contatori delle prestazioni per la gestione dei record di messaggistica

Nella seguente tabella vengono descritti i contatori delle prestazioni per la gestione dei record di messaggistica.

### Contatori delle prestazioni, oggetti prestazioni e descrizione

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Contatore delle prestazioni</th>
<th>Oggetto prestazione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tempo medio di elaborazione della cassetta postale in secondi</p></td>
<td><p>Assistenti di MSExchange</p></td>
<td><p>Calcola il tempo medio di elaborazione delle cassette postali per gli assistenti basati sul tempo.</p></td>
</tr>
<tr class="even">
<td><p>Cassette postali elaborate</p></td>
<td><p>Assistenti di MSExchange</p></td>
<td><p>Calcola il numero di cassette postali elaborate dagli assistenti basati sul tempo dall'avvio del servizio.</p></td>
</tr>
<tr class="odd">
<td><p>Cassette postali elaborate al secondo</p></td>
<td><p>Assistenti di MSExchange</p></td>
<td><p>Determina la frequenza di cassette postali elaborate al secondo dagli assistenti basati sul tempo.</p></td>
</tr>
<tr class="even">
<td><p>Elementi eliminati ma recuperabili</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Calcola il numero di elementi eliminati dall'Assistente cartelle gestite dall'inizio dell'intervallo di pianificazione più recente. Gli elementi sono comunque recuperabili tramite la cartella degli elementi ripristinabili. Il valore comprende gli elementi delle cassette postali pianificate per l'elaborazione durante l'intervallo di pianificazione e gli elementi di qualsiasi cassetta postale specificata per l'elaborazione. Il contatore viene reimpostato su zero all'inizio di ogni intervallo di pianificazione.</p></td>
</tr>
<tr class="odd">
<td><p>Elementi inseriti nel journal</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Calcola il numero di elementi che l'Assistente cartelle gestite ha inserito nel journal a partire dall'intervallo di pianificazione più recente. Il valore comprende gli elementi delle cassette postali pianificate per l'elaborazione durante il ciclo di lavoro corrente e gli elementi di qualsiasi cassetta postale specificata per l'elaborazione. Il contatore viene azzerato all'inizio di ciascun ciclo di lavoro.</p></td>
</tr>
<tr class="even">
<td><p>Elementi contrassegnati come 'con data di conservazione superata'</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Calcola il numero di elementi che l'Assistente cartelle gestite ha contrassegnato come elementi che hanno superato la data di conservazione a partire dall'intervallo di pianificazione più recente. Il valore comprende gli elementi delle cassette postali pianificate per l'elaborazione durante l'intervallo di pianificazione e gli elementi di qualsiasi cassetta postale specificata per l'elaborazione. Il contatore viene reimpostato su zero all'inizio di ogni intervallo di pianificazione.</p></td>
</tr>
<tr class="odd">
<td><p>Elementi spostati</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Calcola il numero di elementi che l'Assistente cartelle gestite ha spostato a partire dall'intervallo di pianificazione più recente. Il valore comprende gli elementi delle cassette postali pianificate per l'elaborazione durante l'intervallo di pianificazione e gli elementi di qualsiasi cassetta postale specificata per l'elaborazione. Il contatore viene reimpostato su zero all'inizio di ogni intervallo di pianificazione.</p></td>
</tr>
<tr class="even">
<td><p>Elementi eliminati permanentemente</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Calcola il numero di elementi che l'Assistente cartelle gestite ha eliminato permanentemente a partire dall'intervallo di pianificazione più recente. Il valore comprende gli elementi delle cassette postali pianificate per l'elaborazione durante l'intervallo di pianificazione e gli elementi di qualsiasi cassetta postale specificata per l'elaborazione. Il contatore viene azzerato all'inizio di ciascun intervallo di pianificazione.</p></td>
</tr>
<tr class="odd">
<td><p>Elementi soggetti al criterio di conservazione</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Calcola il numero di elementi soggetti al criterio di conservazione da parte dell'Assistente cartelle gestite a partire dall'intervallo di pianificazione più recente. Il valore comprende gli elementi delle cassette postali pianificate per l'elaborazione durante l'intervallo di pianificazione e gli elementi di qualsiasi cassetta postale specificata per l'elaborazione. Il contatore viene azzerato all'inizio di ciascun intervallo di pianificazione. Il contatore è la somma dei quattro contatori relativi alla scadenza riportati di seguito:</p>
<ul>
<li><p>Elementi inseriti nel journal</p></li>
<li><p>Elementi contrassegnati come 'con data di conservazione superata'</p></li>
<li><p>Elementi spostati</p></li>
<li><p>Elementi eliminati permanentemente</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsExpired - Dimensione degli elementi soggetti al criterio di conservazione (in byte)</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Indica la dimensione totale degli elementi fatti scadere dall'Assistente cartelle gestite (SoftDelete, HardDelete, MoveToArchive).</p>
<p>Sono inclusi i seguenti elementi:</p>
<ul>
<li><p>Messaggi soggetti ad eliminazione o a spostamento in una cartella personalizzata gestita da un criterio cassetta postale per cartelle gestite</p></li>
<li><p>Messaggi soggetti ad eliminazione o a spostamento in un archivio da un criterio di conservazione dell'utente</p></li>
<li><p>Messaggi considerati scaduti da un criterio di pulizia</p></li>
<li><p>Messaggi eliminati da tag di pulitura del sistema</p></li>
</ul>
<p>Questo contatore viene azzerato ad ogni checkpoint del ciclo di lavoro dell'Assistente cartelle gestite.</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsSoftDeleted - Dimensione degli elementi eliminati ma recuperabili (in byte)</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Indica la dimensione totale degli elementi eliminati in modo reversibile dall'Assistente cartelle gestite.</p>
<p>Sono inclusi i seguenti elementi:</p>
<ul>
<li><p>Messaggi eliminati in modo reversibile da un criterio cassetta postale di cartella gestita</p></li>
<li><p>Messaggi eliminati in modo reversibile da un criterio di conservazione</p></li>
</ul>
<p>Questo contatore viene azzerato ad ogni checkpoint del ciclo di lavoro dell'Assistente cartelle gestite.</p></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsPermanentlyDeleted - Dimensione degli elementi eliminati in modo permanente (in byte)</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Indica la dimensione totale degli elementi eliminati in modo reversibile dall'Assistente cartelle gestite.</p>
<p>Sono inclusi i seguenti elementi:</p>
<ul>
<li><p>Messaggi eliminati in modo irreversibile da un criterio cassetta postale di cartella gestita</p></li>
<li><p>Messaggi eliminati in modo irreversibile da un criterio di conservazione</p></li>
<li><p>Messaggi eliminati in modo irreversibile da un criterio di elementi ripristinabili</p></li>
</ul>
<p>Questo contatore viene azzerato ad ogni checkpoint del ciclo di lavoro dell'Assistente cartelle gestite.</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsMoved - Dimensione degli elementi spostati a causa di un tag del criterio di archiviazione (in byte)</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Indica la dimensione totale degli elementi spostati in una cartella o spostati in un archivio dall'Assistente cartelle gestite</p>
<p>Sono inclusi i seguenti elementi:</p>
<ul>
<li><p>Messaggi spostati in una cartella personalizzata gestita da un criterio cassetta postale per cartelle gestite</p></li>
<li><p>Messaggi spostati nell'archivio personale da un criterio di conservazione</p></li>
</ul>
<p>Questo contatore viene azzerato ad ogni checkpoint del ciclo di lavoro dell'Assistente cartelle gestite.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsWithPersonalTag - elementi contrassegnati con Tag personali (scadenza o archivio)</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Indica il numero di volte che un utente contrassegna un elemento con un tag personale.</p>
<p>Questo include i tag sia di eliminazione che di archivio.</p>
<p>Ad esempio:</p>
<ul>
<li><p>Un elemento è contrassegnato con un tag personale.</p></li>
<li><p>Un elemento con un tag personale è contrassegnato di nuovo con un altro tag personale.</p></li>
</ul>
<p>Se una cartella viene contrassegnata con un tag personale, il contatore viene incrementato del numero totale di elementi nella cartella.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsWithDefaultTag - Elementi contrassegnati con Tag predefinito (scadenza o archivio)</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Indica il numero di elementi assegnati ad un tag criterio predefinito (DPT) sulla base di un'azione dell'utente come, ad esempio, quando un utente seleziona un messaggio con un tag personalizzato e seleziona <strong>Usa criterio cartella</strong>.</p>
<p>Se ad un nuovo utente viene assegnato un criterio di conservazione con un DPT, il contatore viene incrementato del numero di elementi ai quali verrà assegnato il DTP a causa del criterio di conservazione.</p>

> [!NOTE]
> Se un utente ha un criterio di conservazione con un DPT, i nuovi messaggi che arrivano tramite trasporto riceveranno un tag predefinito e questo non verrà contabilizzato dal contatore.


</td>
</tr>
<tr class="even">
<td><p>TotalItemsWithSystemCleanupTag - Elementi contrassegnati con tag di pulitura del sistema</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Indica il numero di elementi contrassegnati con tag di pulitura del sistema. Include elementi di metadati delle cassette postali che non sono visibili agli utenti.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsExpiredByDefaultExpiryTag - Elementi considerati scaduti a causa di un Tag predefinito di scadenza</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Indica il numero di elementi considerati scaduti (eliminati in modo irreversibile o reversibile) dall'Assistente cartelle gestite a causa di un qualunque tag non personale (predefinito o di sistema) in un criterio di conservazione.</p>
<p>Questo non include gli elementi considerati scaduti dalla pulizia di elementi ripristinabili o da una pulizia di sistema.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsExpiredByPersonalExpiryTag - Elementi considerati scaduti a causa di un Tag personale di scadenza</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Indica il numero di elementi considerati scaduti (eliminati in modo irreversibile o reversibile) dall'Assistente cartelle gestite a causa di un tag personale in un criterio di conservazione.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsMovedByDefaultArchiveTag - Elementi spostati a causa di un tag predefinito di archivio</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Indica il numero di elementi spostati in un archivio dall'Assistente cartelle gestite a causa di un qualunque tag non personale (predefinito o di sistema) in un criterio di conservazione.</p>
<p>Questo non include gli elementi spostati in una cartella elementi recuperabili in archivio da una pulizia degli elementi recuperabili.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsMovedByPersonalArchiveTag - Elementi spostati a causa di un Tag archivio</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Indica il numero di elementi spostati in un archivio dall'Assistente cartelle gestite a causa di un tag personale in un criterio di conservazione.</p></td>
</tr>
<tr class="odd">
<td><p>TotalMovedDumpsterItems - Messaggi spostati per la pulitura della cassetta postale</p></td>
<td><p>Assistente cartelle gestite di MSExchange</p></td>
<td><p>Indica gli elementi spostati in una cartella elementi recuperabili in archivio da una pulizia degli elementi recuperabili.</p></td>
</tr>
</tbody>
</table>


---
title: "Informazioni sull'azzeramento delle pagine in Exchange 2013: Exchange 2013 Help"
TOCTitle: Informazioni sull'azzeramento delle pagine in Exchange 2013
ms:assetid: 0ca7b188-efbc-4c0d-bcfe-5138cffc803c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg549096(v=EXCHG.150)
ms:contentKeyID: 61604697
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Informazioni sull'azzeramento delle pagine in Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

## Azzeramento delle pagine in Exchange 2013

L'*azzeramento* è un meccanismo di sicurezza che scrive zeri o una sequenza binaria sui dati eliminati in modo che tali dati siano più difficili da recuperare. In Exchange Server 2013, un database ESE utilizza *pagine* come unità di archiviazione e, di conseguenza, implementa l'*azzeramento delle pagine*. L'azzeramento delle pagine è abilitato per impostazione predefinita e non può essere disabilitato. Le operazioni di azzeramento delle pagine viene registrato nel file di registro delle transazioni in modo che tutte le copie di un database abbiano le pagine azzerate in modo simile. L'azzeramento di una pagina su un database attivo determina l'azzeramento della pagina su una copia passiva del database.


> [!NOTE]
> Non esiste un meccanismo in Extensible Storage Engine (ESE) per assegnare una priorità nella riutilizzazione delle pagine azzerate per l'allocazione di nuovo spazio. Le tabelle a cui viene assegnata l'allocazione di spazio sequenziale evitano intenzionalmente le pagine azzerate o frammentate favorendo l'utilizzo di pagine sequenziali nuove o libere. Questo approccio riduce gli IOP del database.



In Exchange 2013 l'azzeramento delle pagine attenua l'impatto sulle prestazioni dei server che eseguono tali funzioni. Ciò include:

  - **Capacità di archiviazione e rete ottimizzata**   ESE (Extensible Storage Engine) scrive un record di azzeramento pagina nel file di registro delle transazioni invece di registrare l'intera immagine della pagina. Questo approccio riduce l'I/O di scrittura nel registro e la larghezza di banda necessaria per l'invio dei file di registro.

  - **I/o su disco del database ottimizzata**   In Exchange 2010 RTM in precedenza, azzeramento delle pagine durante solo durante un backup oppure durante la manutenzione pianificata e ha causato i/o su disco del database significativo. Nella pagina successiva (incluso Exchange 2013 ) e Exchange 2010 SP1 azzeramento delle si verifica per impostazione predefinita e viene eseguita al momento della transazione. Nella maggior parte dei casi, azzeramento si verifica subito dopo l'eliminazione una disco rigido. Questo tipo di progetto consente di sfruttare la funzionalità di profondità punto di controllo di modulo, che garantisce che le pagine dirty rimangano nella cache del database per un determinato periodo di tempo in modo che gli aggiornamenti a pagina aggiuntivi che si verificano in chiudono ora prossimità non causare ulteriori database scrittura i/o il database. Per questa ragione azzeramento delle pagine, è associato alcun database significativo impatto dei / o, motivo per cui è abilitata per impostazione predefinita.

## Implementazione dell'azzeramento delle pagine nel database ESE

L'azzeramento delle pagine scrive una sequenza binaria su un record eliminato definitivamente. La sequenza di azzeramento pagine è specifica dell'operazione del motore ESE ed è diversa per le le operazioni di runtime rispetto alle operazioni di manutenzione. La tabella seguente elenca le sequenze di riempimento che corrispondono a specifiche operazioni runtime.

### Sequenza di riempimento per l'azzeramento delle pagine durante le operazioni di runtime di ESE

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Operazione runtime di ESE</th>
<th>Sequenza di riempimento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sostituisce</p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p>Elimina record/valore lungo</p></td>
<td><p>D</p></td>
</tr>
<tr class="odd">
<td><p>Spazio pagina liberato</p></td>
<td><p>H</p></td>
</tr>
</tbody>
</table>


La tabella che segue elenca le sequenze di riempimento che corrispondono alle specifiche operazioni che avvengono durante le operazioni di manutenzione in background di ESE.

### Sequenza di riempimento per l'azzeramento delle pagine durante le operazioni di manutenzione in background di ESE

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Operazioni di manutenzione in background del database ESE</th>
<th>Motivo riempimento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Elimina record</p></td>
<td><p>D</p></td>
</tr>
<tr class="even">
<td><p>Elimina valore lungo</p></td>
<td><p>L</p></td>
</tr>
<tr class="odd">
<td><p>Spazio pagina liberato della pagina parzialmente utilizzata</p></td>
<td><p>Z</p></td>
</tr>
<tr class="even">
<td><p>Spazio pagina liberato della pagina inutilizzata</p></td>
<td><p>U</p></td>
</tr>
</tbody>
</table>


## Manutenzione in background del database

La manutenzione del database in background è un processo che esegue continuamente il checksum e la scansione di ogni database. La sua funzione primaria è l'esecuzione del checksum delle pagine del database, ma gestisce anche la pulitura dello spazio e l'azzeramento dei record e delle pagine non azzerate a causa di un arresto anomalo dell'archivio. La manutenzione in background del database elabora circa 1 MB al secondo per ogni database. Se l'azzeramento delle pagine è una priorità, è possibile ridurre le dimensioni del database per assicurarsi che in caso di arresto improvviso le operazioni di azzeramento durante il ripristino avvengano nel più breve tempo possibile (ad esempio 24 ore).

La manutenzione in background del database è un processo continuo per cui non ci sono eventi associati al suo avvio o al suo completamento. È possibile tenere traccia dell'avanzamento della manutenzione in background del database leggendo il valore di un contatore delle prestazioni:

  - Database MSExchange =\>Istanze-\> Durata manutenzione del database

Questo contatore indica il numero di secondi trascorsi dall'ultimo completamento della manutenzione per un determinato database.

## Processo di azzeramento delle pagine di un database ESE

La tabella seguente illustra gli scenari di eliminazione nel database e quando viene attivata la funzione di azzeramento delle pagine.

### Manutenzione del database in background ESE

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Scenario di eliminazione dal database</th>
<th>Processo di ESE e tempi di azzeramento dei dati del database</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Scenario 1: Il ripristino di singoli elementi è disabilitato e l'utente elimina l'elemento dalla cartella degli elementi ripristinabili.</p></li>
<li><p>Scenario 2: Il ripristino di singoli elementi è disabilitato ed il periodo di mantenimento degli elementi ripristinabili è stato impostato a zero.</p></li>
<li><p>Scenario 3: Il ripristino di singoli elementi è abilitato e l'elemento scade in base la periodo di mantenimento degli elementi eliminati.</p></li>
</ul></td>
<td><p>Un thread asincrono scrive una sequenza binaria sui dati eliminati. Questa azione si verifica entro pochi millisecondi dall'eliminazione del record. Se il processo di archiviazione si arresta in modo anomalo mentre è ancora attiva la funzione di azzeramento asincrono (o se viene annullata la funzione di pulitura dell'archivio versioni a causa di un aumento delle dimensioni), l'azzeramento viene completato quando la manutenzione in background del database elabora quella sezione del database.</p></td>
</tr>
<tr class="even">
<td><p>Scenario di visualizzazione: Scadenza di elementi provenienti dalla visualizzazione delle cartelle di Outlook/Outlook Web App (ad esempio, visualizzazione Conversazione)</p></td>
<td><p>L'azzeramento dei dati avviene quando la manutenzione in background del database elabora questa sezione del database.</p></td>
</tr>
<tr class="odd">
<td><p>Scenario di spostamento/eliminazione delle cassette postali: Cassetta postale di origine eliminata (scadenza della cassetta posta eliminata da dumpster)</p></td>
<td><p>L'azzeramento dei dati avviene quando la manutenzione in background del database elabora questa sezione del database.</p></td>
</tr>
</tbody>
</table>


## Monitoraggio dell'azzeramento delle pagine

È possibile misurare e monitorare la funzionalità di azzeramento delle pagine visualizzando due contatori ESE:

  - Database MSExchange-\>Pagine di manutenzione database azzerate: Indica il numero di pagine azzerate dal motore del database da quando è stato richiamato il contatore delle prestazioni.

  - Database di MSExchange-\>Pagine di manutenzione database azzerate/sec: Indica la frequenza di azzeramento delle pagine.


> [!NOTE]
> Per informazioni su come abilitare questi contatori, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=101194">come abilitare esteso contatori aggiuntivi ESE</A>.



L'azzeramento delle pagine è una funzione della manutenzione del database perciò le informazioni sulle prestazioni relative all'azzeramento delle pagine sia per le transazioni runtime che per la manutenzione in background del database sono incluse in questi contatori.

## Tipo di dati delle cassette postali senza azzeramento delle pagine

I seguenti tipi di dati delle cassette postali non hanno provisioning per l'azzeramento delle pagine:

  - Registri delle transazioni del database delle cassette postali (.log)
    
    Quando vengono eliminati i registri delle transazioni (a causa di un troncamento tramite backup o registrazione circolare), non avviene alcun processo di azzeramento dei blocchi nel file system NTFS che ha archiviato i file di registro. È molto probabile che NTFS riutilizzi rapidamente quello spazio libero per la creazione di nuovi registri ma non è garantito che questo avvenga.

  - File di catalogo di indicizzazione del contenuto
    
    Exchange 2013 utilizza Search Foundation per la funzionalità di indicizzazione della ricerca. Il catalogo di indicizzazione della ricerca è composto da diverse dozzine di file archiviati sullo stesso volume del file di database delle cassette postali. Quando un messaggio viene eliminato in modo definitivo dal database delle cassette postali, il contenuto nel catalogo di ricerca ad esso associato non viene eliminato immediatamente. L'eliminazione del contenuto avviene quando Search Foundation crea un'unione shadow, o master, di numerosi piccoli file di catalogo in un singolo file più grande. Una volta completata l'unione master, i piccoli file del catalogo vengono eliminati. I blocchi in cui erano archiviati i file di catalogo eliminati non vengono azzerati.


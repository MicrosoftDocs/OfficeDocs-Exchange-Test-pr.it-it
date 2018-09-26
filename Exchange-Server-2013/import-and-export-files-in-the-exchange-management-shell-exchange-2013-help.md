---
title: 'Importare ed esportare i file in Exchange Management Shell: Exchange 2013 Help'
TOCTitle: Importare ed esportare i file in Exchange Management Shell
ms:assetid: b4b669e8-a3aa-4b0b-ad34-f1f15d9c9369
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638170(v=EXCHG.150)
ms:contentKeyID: 50555667
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importare ed esportare i file in Exchange Management Shell

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Microsoft Exchange Server 2013 utilizza la modalità remota dell'interfaccia della riga di comando di Windows per stabilire una connessione tra il server o la workstation da cui si amministra Exchange e il server su cui è in esecuzione Exchange 2013 che si sta amministrando. In Exchange 2013 questa funzione viene denominata Exchange Management Shell remota o Shell remota. Anche se si amministra il server Exchange 2013 locale, per effettuare la connessione viene utilizzata la Shell remota. Per ulteriori informazioni sulla Shell locale e remota, vedere [Utilizzo di PowerShell con Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/it-it/library/bb123778\(v=exchg.150\)).

La modalità di importazione ed esportazione dei file da e verso un server Exchange in Exchange 2013 è diversa da quella presente in Exchange Server 2007. Questo cambiamento è dovuto all'uso della Shell remota in Exchange 2013. In questo argomento viene illustrato il motivo per cui è richiesto questo nuovo processo e la modalità di importazione ed esportazione di file tra un server o una workstation locale e un server Exchange 2013.

## Sessioni di Windows PowerShell

Per comprendere il motivo per cui è necessaria una sintassi speciale per importare ed esportare file nella Shell remota, è necessario sapere come la Shell viene implementata in Exchange 2013. La Shell utilizza sessioni di Windows PowerShell, le quali costituiscono gli ambienti in cui variabili cmdlet e così via possono condividere informazioni. Ogni volta che si apre una nuova finestra Shell, si crea una nuova sessione. I cmdlet eseguiti in ogni finestra possono accedere a variabili e ad altre informazioni presenti in tale finestra ma non possono accedere a variabili presenti in altre finestre Shell aperte. Ciò è dovuto al fatto che sono contenuti nella loro propria sessione di Windows PowerShell. Le sessioni di Windows PowerShell possono anche essere definite spazi di esecuzione.

La Shell remota in Exchange 2013 presenta due sessioni: la sessione locale e la sessione remota. La sessione locale è la sessione di Windows PowerShell eseguita nel computer locale. Questa sessione contiene tutti i cmdlet forniti con Windows PowerShell. Ha inoltre accesso al file system locale.

La sessione remota è la sessione di Windows PowerShell eseguita nel server Exchange. Questa sessione viene eseguita dove vengono eseguiti tutti i cmdlet Exchange. Ha accesso al file system del server Exchange.

Quando ci si connette a un server Exchange remoto, viene effettuata una connessione tra la sessione locale nel computer e la sessione remota nel server Exchange. Questa connessione consente di eseguire i cmdlet Exchange del server Exchange remoto nella sessione locale anche se nel computer locale non è installato alcun cmdlet Exchange. Anche se può sembrare che i cmdlet Exchange siano in esecuzione sul computer locale, in realtà vengono eseguiti sul server Exchange.


> [!IMPORTANT]
> Anche se si apre la Shell in un server Exchange 2013, viene effettuato lo stesso processo di connessione e vengono create due sessioni. Pertanto, è necessario utilizzare la stessa nuova sintassi per importare ed esportare file se si apre la Shell in un server Exchange 2013 o da una workstation client remota.



I cmdlet Exchange eseguiti nella sessione remota nel server Exchange remoto non hanno accesso al file system locale. Pertanto non è possibile utilizzare i cmdlet Exchange da soli per importare o esportare da o verso il file system locale. È necessario utilizzare sintassi aggiuntiva per trasferire i file dal e al file system locale affinché i Exchange eseguiti nel server Exchange remoto possano utilizzare i dati. Per ulteriori informazioni sulla sintassi richiesta vedere "Importazione ed esportazione di file nella Shell remota", più avanti in questo argomento.

## Importazione ed esportazione di file nella Shell remota

L'importazione e l'esportazione di file richiedono una sintassi specifica in quanto i server Cassette postali e Accesso client utilizzano la Shell remota e non dispongono dell'accesso al file system del computer locale.

## Importazione di file nella Shell remota

La sintassi per l'importazione di file in Exchange 2013 viene utilizzata ogni volta che si desidera inviare un file a un cmdlet in esecuzione in un server Exchange 2013 dal computer o dal server locale. I cmdlet che accettano dati da un file nel computer locale avranno un parametro denominato *FileData* (o nome simile). Per determinare il parametro corretto da utilizzare, vedere le informazioni della Guida relative al cmdlet che si utilizza.

È necessario comunicare alla Shell quale file si desidera inviare al Exchange 2013 e quale parametro accetterà i dati. A tal fine, utilizzare la sintassi seguente.
```powershell
    <Cmdlet> -FileData ([Byte[]]$(Get-Content -Path <local path to file> -Encoding Byte -ReadCount 0))
```
Il comando seguente, ad esempio, consente di importare il file C:\\MyData.dat nel parametro *FileData* sul cmdlet fittizio **Import-SomeData**.
```powershell
    Import-SomeData -FileData (Byte[]]$(Get-Content -Path "C:\MyData.dat" -Encoding Byte -ReadCount 0))
```
Quando viene eseguito il comando, vengono effettuate le seguenti operazioni:

1.  Il comando viene accettato dalla Shell remota.

2.  La Shell remota valuta il comando e determina che è presente un comando incorporato nel valore fornito al parametro *FileData*.

3.  La Shell remota interrompe la valutazione del comando **Import-SomeData** ed esegue il comando **Get-Content**. Il comando **Get-Content** legge i dati dal file MyData.dat.

4.  La Shell remota archivia temporaneamente i dati dal comando **Get-Content** come oggetto `Byte[]` in modo che possano essere passati al cmdlet **Import-SomeData**.

5.  L'esecuzione del comando **Import-SomeData** riprende. La Shell remota invia la richiesta di esecuzione del cmdlet **Import-SomeData** al server Exchange 2013, insieme all'oggetto creato dal cmdlet **Get-Content**.

6.  Nel server Exchange 2013 remoto, viene eseguito il cmdlet **Import-SomeData** e i dati archiviati nell'oggetto temporaneo creato dal cmdlet **Get-Content** vengono passati al parametro *FileData*. Il cmdlet **Import-SomeData** elabora l'input ed esegue le operazioni richieste.

Alcuni cmdlet utilizzano la seguente sintassi alternativa che consente di effettuare le stesse operazioni della sintassi precedente.
```powershell
    [Byte[]]$Data = Get-Content -Path <local path to file> -Encoding Byte -ReadCount 0
    Import-SomeData -FileData $Data
```
Con questa sintassi alternativa viene effettuato lo stesso processo. L'unica differenza è che, invece di esegue l'intera operazione in una sola volta, i dati recuperati dal file locale vengono archiviati in una variabile a cui è possibile fare riferimento dopo sua la creazione. La variabile viene quindi utilizzata nel comando di importazione per passare il contenuto del file locale al cmdlet **Import-SomeData**. L'utilizzo di questo processo in due passaggi è utile quando si desidera utilizzare i dati dal file locale in più comandi.

Vi sono alcune limitazioni di cui è necessario tenere conto quando si importano file. Per ulteriori informazioni, vedere "Limitazioni sull'importazione di file" più avanti in questo argomento.

Per informazioni specifiche sull'importazione di dati in Exchange 2013, vedere gli argomenti della Guida per la funzionalità che si sta gestendo.

## Limitazioni sull'importazione di file

È necessario impostare dei limiti quando si importano dati nella Shell remota per preservare l'integrità dei dati trasferiti. I trasferimenti in corso non possono essere ripresi se vengono interrotti. Inoltre, poiché i dati trasferiti vengono archiviati nella memoria del server remoto, il server deve essere protetto dall'esaurimento della memoria causata da quantità di dati eccessive.

Per questi motivi, la quantità di dati trasferiti in un server Exchange 2013 remoto da un computer o server locale presenta i seguenti limiti:

  - 500 megabyte (MB) per ogni cmdlet eseguito

  - 75 MB per ogni oggetto passato a un cmdlet

Se si supera uno di questi limiti, l'esecuzione del cmdlet e la pipeline associata verranno arrestate e verrà restituito un errore. Per comprendere il funzionamento di questi limiti, vedere gli esempi riportati nella tabella seguente.

### Esempi di limiti sull'importazione di dati

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Numero di oggetti</th>
<th>Dimensione oggetto (MB)</th>
<th>Dimensione totale (MB)</th>
<th>Risultato dell'operazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10</p></td>
<td><p>40</p></td>
<td><p>400</p></td>
<td><p>L'operazione ha esito positivo poiché la dimensione dei singoli oggetti non supera i 75 MB e la quantità totale di dati passati al cmdlet non supera i 500 MB.</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>80</p></td>
<td><p>400</p></td>
<td><p>L'operazione ha esito negativo poiché, sebbene la quantità totale di dati passati al cmdlet e di soli 400 MB, la dimensione di ogni singolo oggetto supera il limite di 75 MB.</p></td>
</tr>
<tr class="odd">
<td><p>120</p></td>
<td><p>5</p></td>
<td><p>600</p></td>
<td><p>L'operazione ha esito negativo poiché, sebbene la dimensione di ogni singolo oggetto sia di soli 5 MB, la quantità totale di dati passati al cmdlet supera il limite di 500 MB.</p></td>
</tr>
</tbody>
</table>


A causa dei limiti di dimensione fissati per la quantità di dati che è possibile trasferire tra un server Exchange 2013 remoto e un computer locale, non tutti i cmdlet che precedentemente supportavano l'importazione supportano questo metodo di trasferimento di dati. Per determinare sa uno specifico cmdlet supporta questo metodo, vedere le informazioni della Guida relative a tale cmdlet.

Questi limiti dovrebbero soddisfare la maggior parte delle operazioni tipiche che è possibile eseguire su un server Exchange 2013. Se i limiti vengono abbassati, è possibile che alcune operazioni normali non riescano poiché superano i nuovi limiti. Se i limiti vengono alzati, il trasferimento dei dati potrebbe richiedere più tempo ed essere maggiormente esposto al rischio di condizioni temporanee che lo interrompano. Inoltre, è possibile esaurire la memoria nel server remoto se non si è installata memoria sufficiente per consentire al server di archiviare l'intero blocco di dati durante il trasferimento. Ognuna di queste possibilità può causare la perdita di dati, pertanto non è consigliabile modificare i limiti predefiniti.

## Esportazione di file nella Shell remota

La sintassi per l'esportazione di file in Exchange 2013 viene utilizzata ogni volta che si desidera accettare dati da un cmdlet in esecuzione in un server Exchange 2013 remoto e archiviarli nel computer o server locale. I cmdlet che forniscono dati che è possibile salvare in un file locale emetteranno un oggetto contenente la proprietà **FileData** (o proprietà simile). A seconda del cmdlet, la proprietà **FileData** viene popolata esclusivamente sull'oggetto emesso in situazioni specifiche. Per determinare la proprietà corretta da utilizzare e quando è possibile utilizzarla, vedere le informazioni della Guida relative al cmdlet che si utilizza.

È necessario comunicare alla Shell che si intende salvare nel computer locale i dati archiviati nella proprietà **FileData**. A tal fine, utilizzare la sintassi seguente.

```command line
<cmdlet> | ForEach {     <cmdlet> | ForEach { $_.FileData | Add-Content <local path to file> -Encoding Byte }.FileData | Add-Content <local path to file> -Encoding Byte }
```

Il comando seguente, ad esempio, consente di esportare i dati archiviati nella proprietà **FileData** sull'oggetto creato dal cmdlet fittizio **Export-SomeData**. I dati esportati vengono archiviati in un file specificato nel computer locale, in questo caso MyData.dat.


> [!NOTE]
> In questa procedura vengono utilizzati il cmdlet <STRONG>ForEach</STRONG>, oggetti e pipelining. Per ulteriori informazioni su ciascuna funzione, vedere <A href="https://technet.microsoft.com/it-it/library/aa998260(v=exchg.150)">Pipelining</A> e <A href="https://technet.microsoft.com/it-it/library/aa996386(v=exchg.150)">Dati strutturati</A>.



```powershell
Export-SomeData | ForEach {     Export-SomeData | ForEach { $_.FileData | Add-Content C:\MyData.dat -Encoding Byte }.FileData | Add-Content C:\MyData.dat -Encoding Byte }
```

Quando viene eseguito il comando, vengono effettuate le seguenti operazioni:

1.  Il comando viene accettato dalla Shell remota.

2.  La Shell remota chiama il cmdlet **Export-SomeData** sul server Exchange 2013 remoto.

3.  L'oggetto di output creato dal cmdlet **Export-SomeData** viene passato nuovamente alla sessione della Shell locale tramite la pipeline.

4.  L'oggetto di output viene quindi inoltrato tramite pipe al cmdlet **ForEach**, il quale presenta un blocco di script.

5.  All'interno del blocco di script, viene effettuato l'accesso alla proprietà **FileData** sull'oggetto corrente nella pipeline. I dati contenuti nella proprietà **FileData** vengono inoltrati tramite pipe al cmdlet **Add-Content**.

6.  Il cmdlet **Add-Content** salva i dati inoltrati tramite pipe dalla proprietà **FileData** al file MyData.dat nel file system locale.

Per informazioni specifiche sull'esportazione di dati da Exchange 2013, vedere gli argomenti della Guida per la funzionalità che si sta gestendo.


---
title: "Utilizzo dell'output del comando: Exchange 2013 Help"
TOCTitle: Utilizzo dell'output del comando
ms:assetid: 8320e1a5-d3f5-4615-878d-b23e2aaa6b1e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123533(v=EXCHG.150)
ms:contentKeyID: 50481061
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzo dell'output del comando

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Exchange Management Shell offre diversi metodi per formattare l'output di comando. In questa sezione vengono descritti i seguenti argomenti:

  - Formattazione dei dati   Consente di controllare le modalità di formattazione dei dati visualizzati utilizzando i cmdlet **Format-List**, **Format-Table** e **Format-Wide**.

  - Generazione dei dati   Consente di determinare se l'output dei dati viene generato nella finestra della console di Shell o in un file, utilizzando i cmdlet **Out-Host** e **Out-File**. In questo argomento è incluso un esempio di script per la generazione dei dati in MicrosoftInternet Explorer.

  - Filtro dei dati   È possibile filtrare i dati mediante uno dei metodi indicati di seguito:
    
      - Filtro sul lato server, disponibile in alcuni cmdlet.
    
      - Filtro sul lato client, disponibile in tutti i cmdlet eseguendo il piping dei risultati di un comando al cmdlet **Where-Object**.

Per utilizzare la funzionalità descritta in questo argomento, è necessario avere familiarità con i concetti riportati di seguito:

  - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))

  - [Variabili di shell](https://technet.microsoft.com/it-it/library/bb124036\(v=exchg.150\))

  - [Operatori di confronto](https://technet.microsoft.com/it-it/library/bb125229\(v=exchg.150\))

## Formattazione dei dati

Se si utilizzano i cmdlet di formattazione alla fine della pipeline, è possibile ignorare la formattazione predefinita per controllare i dati visualizzati e la relativa modalità di visualizzazione. I cmdlet di formattazione sono **Format-List**, **Format-Table** e **Format-Wide**. A ciascuno è associato uno stile di output distinto e diverso dagli altri cmdlet di formattazione.

## Format-List

Il cmdlet **Format-List** riceve l'input dalla pipeline e genera un elenco in colonna verticale di tutte le proprietà specifiche di ciascun oggetto. È possibile specificare le proprietà che si desidera visualizzare utilizzando il parametro *Property*. Se il cmdlet **Format-List** viene eseguito senza alcun parametro specifico, vengono generate tutte le proprietà. Il cmdlet **Format-List** consente di andare a capo automaticamente, invece di troncare le righe. L'utilizzo del cmdlet **Format-List** si rivela utile per ignorare l'output predefinito di un cmdlet consentendo di recuperare informazioni aggiuntive o più dettagliate.

Ad esempio, quando si esegue il cmdlet **Get-Mailbox**, è possibile visualizzare solo un numero limitato di informazioni nel formato della tabella. Se si esegue il piping dell'output del cmdlet **Get-Mailbox** al cmdlet **Format-List** e si aggiungono i parametri relativi alle informazioni aggiuntive o più dettagliate che si desidera visualizzare, è possibile generare l'output desiderato.

È inoltre possibile specificare un carattere jolly "\*" con un nome parziale della proprietà. Se si include un carattere jolly, è possibile applicare delle corrispondenze tra più proprietà senza che sia necessario digitare singolarmente tutti i nomi delle proprietà. Ad esempio, `Get-Mailbox | Format-List -Property Email* ` restituisce tutte le proprietà che iniziano con `Email`.

Negli esempi seguenti sono illustrate le diverse modalità di visualizzazione degli stessi dati restituiti dal cmdlet **Get-Mailbox**.
```powershell
    Get-Mailbox TestUser1
    
    Name                      Alias                ServerName       ProhibitSendQuo
                                                                    ta
    ----                      -----                ----------       ---------------
    TestUser1                 TestUser1            mbx              unlimited
```
Nel primo esempio, il cmdlet **Get-Mailbox** viene eseguito senza una specifica formattazione, pertanto l'output predefinito è in formato di tabella e contiene un insieme predeterminato di proprietà.
```powershell
    Get-Mailbox TestUser1 | Format-List -Property Name,Alias,EmailAddresses
    
    Name           : TestUser1
    Alias          : TestUser1
    EmailAddresses : {SMTP:TestUser1@contoso.com}
```
Nel secondo esempio, l'output del cmdlet **Get-Mailbox** viene reindirizzato al cmdlet **Format-List** insieme a proprietà specifiche. È evidente che il formato e il contenuto dell'output sono significativamente diversi.
```powershell
    Get-Mailbox TestUser1 | Format-List -Property Name, Alias, Email*
    Name                      : Test User
    Alias                     : TestUser1
    EmailAddresses            : {SMTP:TestUser1@contoso.com}
    EmailAddressPolicyEnabled : True
```
Nell'ultimo esempio, l'output del cmdlet **Get-Mailbox** è reindirizzato al cmdlet **Format-List** come nel secondo esempio, ma viene utilizzato un carattere jolly per applicare corrispondenze tra tutte le proprietà che iniziano con `Email`.

Se più di un oggetto viene trasmesso al cmdlet **Format-List**, tutte le proprietà specificate per un oggetto sono visualizzate e raggruppate per oggetto. L'ordine di visualizzazione dipende dal parametro predefinito per il cmdlet. Il parametro predefinito corrisponde spesso al parametro *Name* o al parametro *Identity*. Ad esempio, quando si esegue il cmdlet **Get-Childitem**, l'ordine di visualizzazione predefinito restituisce i nomi file in ordine alfabetico. Per modificare questo comportamento, è necessario eseguire il cmdlet **Format-List**, insieme al parametro *GroupBy*, e il nome di un valore proprietà in base a cui si desidera raggruppare l'output. Ad esempio, il seguente comando consente di elencare tutti i file in una directory e poi di raggrupparli per estensione.
```powershell
    Get-Childitem | Format-List Name,Length -GroupBy Extension
    
        Extension: .xml
    
    Name   : Config_01.xml
    Length : 5627
    
    Name   : Config_02.xml
    Length : 3901
    
    
        Extension: .bmp
    
    Name   : Image_01.bmp
    Length : 746550
    
    Name   : Image_02.bmp
    Length : 746550
    
    
        Extension: .txt
    
    Name   : Text_01.txt
    Length : 16822
    
    Name   : Text_02.txt
    Length : 9835
```

In questo esempio, il cmdlet **Format-List** ha raggruppato gli elementi in base alla proprietà *Extension* specificata dal parametro *GroupBy*. È possibile utilizzare il parametro *GroupBy* con qualsiasi proprietà valida per gli oggetti nel flusso della pipeline.

## Format-Table

Il cmdlet **Format-Table** consente di visualizzare gli elementi dei dati proprietà in un formato di tabella con intestazioni di etichetta e colonne. Per impostazione predefinita, molti cmdlet, come **Get-Process** e **Get-Service**, utilizzano il formato di tabella per l'output. I parametri per il cmdlet **Format-Table** includono i parametri *Properties* e *GroupBy* e funzionano esattamente come nel cmdlet **Format-List**.

Il cmdlet **Format-Table** usa anche il parametro *Wrap*, che consente la visualizzazione completa di righe lunghe di informazioni sulle proprietà invece di troncarle alla fine di una riga. Per l'utilizzo del parametro *Wrap* per la visualizzazione delle informazioni restituite, confrontare l'output del comando **Get-Command** nei due esempi seguenti.

Nel primo esempio, quando si utilizza il cmdlet **Get-Command** per visualizzare le informazioni di comando sul cmdlet **Get-Process**, le informazioni relative alla proprietà *Definition* risultano troncate.
```powershell
    Get-Command Get-Process | Format-Table Name,Definition
    
    Name                                    Definition
    ----                                    ----------
    get-process                             get-process [[-ProcessName] String[]...
```
Nel secondo esempio, è stato aggiunto il parametro *Wrap* al comando per ottenere la visualizzazione completa dei contenuti della proprietà *Definition*.
```powershell
    Get-Command Get-Process | Format-Table Name,Definition -Wrap
    
    Get-Process                             Get-Process [[-Name] <String[]>] [-Comp
                                            uterName <String[]>] [-Module] [-FileVe
                                            rsionInfo] [-Verbose] [-Debug] [-ErrorA
                                            ction <ActionPreference>] [-WarningActi
                                            on <ActionPreference>] [-ErrorVariable
                                            <String>] [-WarningVariable <String>] [
                                            -OutVariable <String>] [-OutBuffer <Int
                                            32>]
                                            Get-Process -Id <Int32[]> [-ComputerNam
                                            e <String[]>] [-Module] [-FileVersionIn
                                            fo] [-Verbose] [-Debug] [-ErrorAction <
                                            ActionPreference>] [-WarningAction <Act
                                            ionPreference>] [-ErrorVariable <String
                                            >] [-WarningVariable <String>] [-OutVar
                                            iable <String>] [-OutBuffer <Int32>]
                                            Get-Process [-ComputerName <String[]>]
                                            [-Module] [-FileVersionInfo] -InputObje
                                            ct <Process[]> [-Verbose] [-Debug] [-Er
                                            rorAction <ActionPreference>] [-Warning
                                            Action <ActionPreference>] [-ErrorVaria
                                            ble <String>] [-WarningVariable <String
                                            >] [-OutVariable <String>] [-OutBuffer
                                            <Int32>]
```
Come nel cmdlet **Format-List**, è possibile inoltre specificare un carattere jolly "`*`" con un nome proprietà parziale. Se si include un carattere jolly, è possibile applicare delle corrispondenze tra più proprietà senza digitare singolarmente tutti i nomi delle proprietà.

## Format-Wide

Il cmdlet **Format-Wide** consente un controllo più semplice dell'output rispetto agli altri cmdlet di formattazione. Per impostazione predefinita, il cmdlet **Format-Wide** tenta di visualizzare in una riga di output quante più colonne possibili dei valori proprietà. L'aggiunta di parametri consente di controllare il numero di colonne e di stabilire come utilizzare lo spazio di output.

Nell'utilizzo più basilare, l'esecuzione del cmdlet **Format-Wide** senza alcun parametro restituisce l'output in tutte le colonne che la pagina può contenere. Ad esempio, se si esegue il cmdlet **Get-Childitem** e si esegue il piping del relativo output al cmdlet **Format-Wide**, le informazioni verranno visualizzate come segue:
```powershell
    Get-ChildItem | Format-Wide
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml                           Config_02.xml
    Config_03.xml                           Config_04.xml
    Config_05.xml                           Config_06.xml
    Config_07.xml                           Config_08.xml
    Config_09.xml                           Image_01.bmp
    Image_02.bmp                            Image_03.bmp
    Image_04.bmp                            Image_05.bmp
    Image_06.bmp                            Text_01.txt
    Text_02.txt                             Text_03.txt
    Text_04.txt                             Text_05.txt
    Text_06.txt                             Text_07.txt
    Text_08.txt                             Text_09.txt
    Text_10.txt                             Text_11.txt
    Text_12.txt
```
In genere, l'esecuzione del cmdlet **Get-Childitem** senza alcun parametro comporta la visualizzazione dei nomi di tutti i file nella directory in una tabella di proprietà. In questo esempio, eseguendo il piping dell'output del cmdlet**Get-Childitem** al cmdlet **Format-Wide**, l'output viene visualizzato in due colonne di nomi. È importante notare che è possibile visualizzare solo un tipo di proprietà alla volta, specificato da un nome proprietà posto di seguito al cmdlet **Format-Wide**. Se si aggiunge il parametro *Autosize*, l'output viene visualizzato non più in due colonne, ma in tutte le colonne che la larghezza dello schermo può contenere.
```powershell
    Get-ChildItem | Format-Wide -AutoSize
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml   Config_02.xml   Config_03.xml   Config_04.xml   Config_05.xml
    Config_06.xml   Config_07.xml   Config_08.xml   Config_09.xml   Image_01.bmp
    Image_02.bmp    Image_03.bmp    Image_04.bmp    Image_05.bmp    Image_06.bmp
    Text_01.txt     Text_02.txt     Text_03.txt     Text_04.txt     Text_05.txt
    Text_06.txt     Text_07.txt     Text_08.txt     Text_09.txt     Text_10.txt
    Text_11.txt     Text_12.txt
```
In questo esempio, la tabella è ordinata in cinque colonne invece che in due. Il parametro *Column* consente di specificare il numero massimo di colonne in cui visualizzare le informazioni, come illustrato di seguito:
```powershell
    Get-ChildItem | Format-Wide -Column 4
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml       Config_02.xml       Config_03.xml       Config_04.xml
    Config_05.xml       Config_06.xml       Config_07.xml       Config_08.xml
    Config_09.xml       Image_01.bmp        Image_02.bmp        Image_03.bmp
    Image_04.bmp        Image_05.bmp        Image_06.bmp        Text_01.txt
    Text_02.txt         Text_03.txt         Text_04.txt         Text_05.txt
    Text_06.txt         Text_07.txt         Text_08.txt         Text_09.txt
    Text_10.txt         Text_11.txt         Text_12.txt
```
In questo esempio, il numero di colonne è stato impostato su quattro utilizzando il parametro *Column*.

## Generazione dei dati

## Cmdlet Out-Host e Out-File

Il cmdlet **Out-Host** è un cmdlet predefinito non visualizzato alla fine della pipeline. Dopo l'applicazione di tutte le formattazioni, il cmdlet **Out-Host** invia l'output finale alla finestra di console per la visualizzazione. Non è necessario eseguire esplicitamente il cmdlet **Out-Host** poiché rappresenta l'output predefinito. È possibile ignorare l'invio dell'output alla finestra di console eseguendo il cmdlet **Out-File** per ultimo nel comando. Il cmdlet **Out-File**, quindi, scrive l'output nel file specificato nel comando come nell'esempio illustrato di seguito:

```powershell
Get-ChildItem | Format-Wide -Column 4 | Out-File c:\OutputFile.txt
```

In questo esempio, il cmdlet **Out-File** consente di scrivere le informazioni visualizzate nel comando **Get-ChildItem | Format-Wide -Column 4** nel file denominato `OutputFile.txt`. È inoltre possibile reindirizzare l'output della pipeline a un file utilizzando l'operatore di reindirizzamento, rappresentato dalla parentesi angolata verso destra ( `>` ). Per aggiungere l'output della pipeline di un comando ad un file esistente senza sostituire il file originale, utilizzare le doppie parentesi angolate verso destra ( `>>` ), come nell'esempio illustrato di seguito:

```powershell
Get-ChildItem | Format-Wide -Column 4 >> C:\OutputFile.txt
```

In questo esempio, l'output dal cmdlet **Get-Childitem** esegue il piping al cmdlet **Format-Wide** per la formattazione e quindi viene scritto alla fine del file `OutputFile.txt`. È importante notare che se il file `OutputFile.txt` non è disponibile, è possibile crearlo utilizzando le doppie parentesi angolate verso destra ( `>>` ).

Per ulteriori informazioni sulle pipeline, vedere [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\)).

Per ulteriori informazioni sulla sintassi utilizzata nell'esempio precedente, vedere [Sintassi](https://technet.microsoft.com/it-it/library/bb123552\(v=exchg.150\)).

## Visualizzazione dei dati in Internet Explorer

Per la flessibilità e la facilità dell'esecuzione script in Exchange Management Shell, è possibile prelevare i dati restituiti dai comandi e formattarli e generarli in moltissimi modi.

Nell'esempio illustrato di seguito, è descritto come utilizzare uno script semplice per generare i dati restituiti da un comando e visualizzarli in Internet Explorer. Lo script preleva gli oggetti transitati tramite la pipeline, apre una finestra di Internet Explorer e visualizza i dati in Internet Explorer:
```powershell
    $Ie = New-Object -Com InternetExplorer.Application
    $Ie.Navigate("about:blank")
    While ($Ie.Busy) { Sleep 1 }
    $Ie.Visible = $True
    $Ie.Document.Write("$Input")
    # If the previous line doesn't work on your system, uncomment the line below.
    # $Ie.Document.IHtmlDocument2_Write("$Input")
    $Ie
```
Per utilizzare lo script, salvarlo nella directory `C:\Program Files\Microsoft\Exchange Server\V15\Scripts` nel computer in cui eseguire lo script. Assegnare al file il nome `Out-Ie.ps1`. Dopo aver salvato il file, è possibile utilizzare lo script come un cmdlet normale.


> [!NOTE]
> Per essere eseguiti in Exchange 2013, gli script devono essere aggiunti a un ruolo di gestione senza ambito e devono essere assegnati al ruolo direttamente o tramite un gruppo del ruolo di gestione. Per ulteriori informazioni, vedere <A href="understanding-management-roles-exchange-2013-help.md">Informazioni sui ruoli di gestione</A>.



Lo script `Out-Ie` presuppone che i dati ricevuti siano in codice HTML valido. Per convertire in HTML i dati che si desiderano visualizzare, è necessario eseguire il piping dei risultati del comando al cmdlet **ConvertTo-Html**. È possibile, quindi, eseguire il piping dei risultati del comando allo script `Out-Ie`. Nel seguente esempio viene descritto come visualizzare un elenco directory in una finestra di Internet Explorer:

```powershell
Get-ChildItem | Select Name,Length | ConvertTo-Html | Out-Ie
```

## Filtro dei dati

Shell consente l'accesso a un grande numero di informazioni sui server, sulle cassette postali, su Active Directory e su altri oggetti dell'organizzazione. L'accesso a tali informazioni consente una comprensione migliore dell'ambiente, ma le informazioni potrebbero essere eccessive. Shell consente di controllare queste informazioni e di restituire solo i dati che si desidera visualizzare utilizzando un filtro. Sono disponibili i tipi di filtro indicati di seguito:

  - **Filtro sul lato server**   Il filtro sul lato server consente di prelevare il filtro specificato nella riga di comando e di inviarlo al server Exchange in cui viene eseguita la query. Tale server elabora la query e restituisce solo i dati che corrispondono al filtro specificato.
    
    Il filtro sul lato server viene eseguito solo su oggetti che possono restituire decine o centinaia di migliaia di risultati. Di conseguenza, solo i cmdlet della gestione destinatari, ad esempio il cmdlet **Get-Mailbox**, e i cmdlet di gestione delle code, ad esempio il cmdlet **Get-Queue**, supportano il filtro sul lato server. Tali cmdlet supportano il parametro *Filter* che consente di prelevare l'espressione del filtro specificata e di inviarla al server per l'elaborazione.

  - **Filtro sul lato client**   Il filtro sul lato client viene eseguito sugli oggetti nella finestra di console locale in cui si opera. Quando si utilizza il filtro sul lato client, il cmdlet recupera tutti gli oggetti che corrispondono all'attività che si sta eseguendo nella finestra di console locale. Shell preleva tutti i risultati restituiti, vi applica il filtro sul lato client e restituisce solo i risultati che corrispondono al filtro. Tutti i cmdlet supportano il filtro sul lato client che viene richiamato dall'esecuzione del piping sui risultati di un comando al cmdlet **Where-Object**.

## Filtro sul lato server

L'implementazione del filtro sul lato server è specifica del cmdlet in cui è supportata. Il filtro sul lato server è abilitato solo su proprietà specifiche degli oggetti restituiti. Per ulteriori informazioni, vedere la Guida per i seguenti cmdlet:


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-ActiveSyncDevice</p></td>
<td><p>Get-ActiveSyncDeviceClass</p></td>
<td><p>Get-CASMailbox</p></td>
<td><p>Get-Contact</p></td>
<td><p>Get-DistributionGroup</p></td>
</tr>
<tr class="even">
<td><p>Get-DynamicDistributionGroup</p></td>
<td><p>Get-Group</p></td>
<td><p>Get-Mailbox</p></td>
<td><p>Get-MailboxStatistics</p></td>
<td><p>Get-MailContact</p></td>
</tr>
<tr class="odd">
<td><p>Get-MailPublicFolder</p></td>
<td><p>Get-MailUser</p></td>
<td><p>Get-Message</p></td>
<td><p>Get-MobileDevice</p></td>
<td><p>Get-Queue</p></td>
</tr>
<tr class="even">
<td><p>Get-QueueDigest</p></td>
<td><p>Get-Recipient</p></td>
<td><p>Get-RemoteMailbox</p></td>
<td><p>Get-RoleGroup</p></td>
<td><p>Get-SecurityPrincipal</p></td>
</tr>
<tr class="odd">
<td><p>Get-StoreUsageStatistics</p></td>
<td><p>Get-UMMailbox</p></td>
<td><p>Get-User</p></td>
<td><p>Get-UserPhoto</p></td>
<td><p>Remove-Message</p></td>
</tr>
<tr class="even">
<td><p>Resume-Message</p></td>
<td><p>Resume-Queue</p></td>
<td><p>Retry-Queue</p></td>
<td><p>Suspend-Message</p></td>
<td><p>Suspend-Queue</p></td>
</tr>
</tbody>
</table>


## Filtro sul lato client

È possibile utilizzare il filtro sul lato client con qualsiasi cmdlet, inclusi quelli che supportano anche il filtro sul lato server. Come illustrato in precedenza in questo argomento, il filtro sul lato client accetta tutti i dati restituiti da un comando precedente nella pipeline e, a sua volta, restituisce solo i risultati che corrispondono al filtro specificato. Il filtro viene eseguito dal cmdlet **Where-Object**, che è possibile abbreviare in **Where**.

Una volta che i dati passano attraverso la pipeline, il cmdlet **Where** li riceve dall'oggetto precedente, li filtra e li passa su un altro oggetto. Il filtro si basa su un blocco di script definito nel comando **Where**. Il blocco di script filtra i dati in base alle proprietà e ai valori dell'oggetto.

Il cmdlet **Clear-Host** viene utilizzato per cancellare la finestra di console. In questo esempio, è possibile trovare tutti gli alias definiti per il cmdlet **Clear-Host** se si esegue il comando indicato di seguito:
```powershell
    Get-Alias | Where {$_.Definition -eq "Clear-Host"}
    
    CommandType     Name                            Definition
    -----------     ----                            ----------
    Alias           clear                           clear-host
    Alias           cls                             clear-host
```
Il cmdlet **Get-Alias** e il comando **Where** operano insieme per restituire l'elenco di alias definiti solo per il cmdlet **Clear-Host**. Nella seguente tabella vengono descritti tutti gli elementi del comando **Where** utilizzato nell'esempio.

### Elementi del comando Where

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>{ }</code></p></td>
<td><p>Le parentesi graffe racchiudono il blocco di script che definisce il filtro.</p></td>
</tr>
<tr class="even">
<td><p><code>$_</code></p></td>
<td><p>Questa variabile speciale attiva e associa automaticamente gli oggetti nella pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><code>Definition</code></p></td>
<td><p>La proprietà <code>Definition</code> rappresenta la proprietà degli oggetti della pipeline corrente che memorizza il nome della definizione dell'alias. Quando <code>Definition</code> viene utilizzata con la variabile <code>$_</code>, il nome della proprietà viene preceduto da un punto.</p></td>
</tr>
<tr class="even">
<td><p><code>-eq</code></p></td>
<td><p>Questo operatore di confronto, corrispondente a &quot;uguale a&quot;, è utilizzato per specificare che è necessario che i risultati corrispondano esattamente al valore proprietà fornito nell'espressione.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;<strong>Clear-Host</strong>&quot;</p></td>
<td><p>In questo esempio, &quot;<strong>Clear-Host</strong>&quot; indica il valore per il quale il comando sta eseguendo l'analisi.</p></td>
</tr>
</tbody>
</table>


Nell'esempio, gli oggetti restituiti dal cmdlet **Get-Alias** rappresentano tutti gli alias definiti nel sistema. Anche se non è possibile visualizzarli dalla riga di comando, gli alias sono raccolti e passano al cmdlet **Where** attraverso la pipeline. Il cmdlet **Where** utilizza le informazioni nel blocco di script per applicare un filtro agli oggetti alias.

La variabile speciale `$`\_rappresenta gli oggetti in transito. La variabile `$_` viene automaticamente attivata da Shell e viene associata all'oggetto pipeline corrente. Per ulteriori informazioni su questa variabile speciale, vedere [Variabili di shell](https://technet.microsoft.com/it-it/library/bb124036\(v=exchg.150\)).

Utilizzando la notazione "punto" standard (object.property), la proprietà `Definition` viene aggiunta per definire la proprietà esatta dell'oggetto da valutare. L'operatore di confronto `-eq` confronta, quindi, il valore di questa proprietà con `"Clear-Host"`. Solo gli oggetti con la proprietà `Definition` corrispondente a questo criterio vengono trasmessi alla finestra di console per l'output. Per ulteriori informazioni sugli operatori di confronto, vedere [Operatori di confronto](https://technet.microsoft.com/it-it/library/bb125229\(v=exchg.150\)).

Dopo che il comando **Where** ha filtrato gli oggetti restituiti dal cmdlet **Get-Alias**, è possibile eseguire il piping degli oggetti filtrati a un altro comando. Il comando successivo elabora solo gli oggetti filtrati restituiti dal comando Where.


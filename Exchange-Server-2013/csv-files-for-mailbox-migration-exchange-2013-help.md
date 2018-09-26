---
title: 'File CSV per la migrazione delle cassette postali: Exchange 2013 Help'
TOCTitle: File CSV per la migrazione delle cassette postali
ms:assetid: e67b3455-3946-4335-b80c-97823c76ac54
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn170437(v=EXCHG.150)
ms:contentKeyID: 54652855
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# File CSV per la migrazione delle cassette postali

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-11-16_

È possibile utilizzare un file CSV per blocco eseguire la migrazione di un numero elevato di cassette postali degli utenti. Quando si utilizza l'interfaccia di amministrazione di Exchange (EAC) o il cmdlet **New-MigrationBatch** in Exchange Management Shell per creare un batch di migrazione, è possibile specificare un file CSV. Utilizzo di un CSV per specificare più utenti per la migrazione di un batch di migrazione è supportato nei seguenti scenari di migrazione:

  - **Spostamenti in organizzazioni Exchange locali**
    
      - **Spostamento locale:**    indica uno spostamento di cassette postali da un database delle cassette postali all'altro. Uno spostamento locale avviene all'interno di una singola foresta.
    
      - **Spostamento aziendale tra foreste:**    indica lo spostamento delle cassette postali in una foresta diversa. Gli spostamenti tra foreste iniziano dalla foresta di destinazione, ossia la foresta in cui si intende spostare le cassette postali, o dalla foresta di origine, ossia quella in cui si trovano le cassette postali.

  - **Onboarding e offboarding in Exchange Online**
    
      - **Migrazione con spostamento remoto onboarding:**    in una distribuzione ibrida di Exchange è possibile spostare le cassette postali da un'organizzazione Exchange locale a Exchange Online. Tale migrazione viene chiamata anche migrazione con spostamento remoto *onboarding*.
    
      - **Migrazione con spostamento remoto offboarding:**  è anche possibile eseguire una migrazione con spostamento remoto *offboarding*, ossia migrare le cassette postali di Exchange Online nell'organizzazione Exchange locale.
        

        > [!NOTE]
        > Entrambi i tipo di migrazione di spostamento remoto iniziano dall'organizzazione Exchange Online.

    
      - **Migrazione di Exchange a fasi:**    è anche possibile eseguire la migrazione di un sottoinsieme di cassette postali da un'organizzazione Exchange locale a Exchange Online. Si tratta di un altro tipo di migrazione onboarding. È possibile migrare solo cassette postali di Exchange 2003 e Exchange 2007 usando una migrazione a fasi di Exchange. La migrazione delle cassette postali di Exchange 2010 e Exchange 2013 non è supportata in una migrazione in fasi. Prima di eseguire una migrazione in fasi, è necessario utilizzare la sincronizzazione delle directory o un altro metodo di provisioning degli utenti di posta nell'organizzazione Exchange Online.
    
      - **Migrazione IMAP:**    questo tipo di migrazione onboarding consiste nella migrazione dei dati delle cassette postali da un server IMAP (incluso Exchange) a Exchange Online. Per poter migrare i dati delle cassette postali in una migrazione IMAP, è necessario innanzitutto eseguire il provisioning delle cassette postali di Exchange Online.


> [!NOTE]
> Non supporta una migrazione completa Exchange utilizzando un file CSV perché tutte le cassette postali utente locale vengono migrate in Exchange Online in un singolo batch.



## Attributi supportati per i file CSV per gli spostamenti o le migrazioni in blocco

Nella prima riga, o riga di intestazione, di un file CSV utilizzato per la migrazione degli utenti vengono elencati gli attributi, o campi, specificati nella righe successive. Il nome di ciascun attributo è separato da una virgola. Ogni riga sotto la riga di intestazione rappresenta una singolo utente e contiene le informazioni necessarie per la migrazione. Gli attributi di ciascuna singola riga utente devono essere visualizzati nello stesso ordine in cui sono elencati i nomi degli attributi nella riga di intestazione. Il valore di ciascun attributo è separato da una virgola. Se il valore dell'attributo di un record specifico è null, per l'attributo non deve essere specificato nulla. Tuttavia, assicurarsi di includere la virgola per separare il valore null dall'attributo successivo.

I valori di attributo nel file CSV per ignorare il valore del parametro corrispondente quando si utilizza il parametro stesso durante la creazione di un batch di migrazione con l'interfaccia di amministrazione di Exchange o Exchange Management Shell. Per ulteriori informazioni ed esempi, vedere la sezione valori degli attributi nel file CSV ignora i valori per il batch di migrazione.


> [!TIP]
> È possibile utilizzare un editor di testo per creare il file CSV, ma utilizzando un'applicazione come Microsoft Excel sarà più facile importare i dati e configurare e organizzare i file CSV. Salvare i file CSV con estensione .csv o .txt.



Nelle sezioni seguenti vengono descritti gli attributi supportati per la riga di intestazione di un file CSV per ogni tipo di migrazione. Ogni sezione include una tabella che elenca ogni attributo supportato, se necessario, un esempio di un valore da utilizzare per l'attributo e una descrizione.


> [!NOTE]
> Nelle sezioni seguenti <EM>ambiente di origine</EM> denota la posizione corrente di una cassetta postale utente o di un database. <EM>Ambiente di destinazione</EM> denota la posizione in cui sarà migrata la cassetta postale o il database in cui sarà spostata la cassetta postale.



## Spostamenti locali

Nella seguente tabella vengono descritti gli attributi supportati per un file CSV per gli spostamenti locali. Per ulteriori informazioni, vedere [Gestire spostamenti locali](manage-on-premises-moves-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributo</th>
<th>Obbligatorio o facoltativo</th>
<th>Valori accettati</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obbligatorio</p></td>
<td><p>Indirizzo SMTP dell'utente</p></td>
<td><p>Specifica l'utente che sarà spostato.</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>Facoltativo</p></td>
<td><p>Nome del database</p></td>
<td><p>Specifica il database delle cassette postali che verrà spostata nella cassetta postale principale dell'utente. È possibile specificare un altro database nelle diverse righe del file CSV, che consente di spostare le cassette postali nel batch di migrazione stesso database diversi.</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>Facoltativo</p></td>
<td><p>Nome del database</p></td>
<td><p>Specifica il database delle cassette postali che verrà spostata nella cassetta postale di archivio dell'utente (se disponibile). È possibile specificare un altro database nelle diverse righe del file CSV, che consente di spostare cassette postali di archiviazione nel batch di migrazione stesso database diversi.</p>

> [!NOTE]
> Se non si specifica un database di archiviazione, la cassetta postale di archiviazione verrà spostata al database di cassetta postale principale.


</td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>Facoltativo</p></td>
<td><p><code>Unlimited</code> o un intero non negativo da <code>0</code> (valore predefinito) a un valore massimo di <code>2147483647</code></p></td>
<td><p>Specifica il numero di elementi non validi per ignorare se il servizio di migrazione viene rilevato un elemento danneggiato nella cassetta postale. Se si include questo attributo nel file CSV, ignorerà il valore predefinito o un valore specificato se si include il parametro <em>BadItemLimit</em> durante la creazione del batch di migrazione tramite EAC o Exchange Management Shell.</p>

> [!TIP]
> Si consiglia di utilizzare il valore predefinito, 0, e di aumentare il limite di elementi non validi per un particolare utente solo se lo spostamento o la migrazione per tale utente non riesce.


<p></p></td>
</tr>
<tr class="odd">
<td><p>MailboxType</p></td>
<td><p>Facoltativo</p></td>
<td><p>Utilizzare uno dei seguenti valori:</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (il valore predefinito)</p></li>
</ul></td>
<td><p>Specifica se si desidera spostare cassetta postale principale dell'utente, cassetta postale di archivio o entrambi.</p></td>
</tr>
</tbody>
</table>


## Migrazioni di spostamento remoto onboarding in una distribuzione ibrida

In una distribuzione ibrida, è possibile spostare le cassette postali da un'organizzazione Exchange a Exchange Online. Quando si trasferiscono le cassette postali, il batch di migrazione viene creato nell'organizzazione Exchange Online e avviato da un amministratore di Exchange Online. Per ulteriori informazioni, vedere [Spostare le cassette postali tra le organizzazioni locali e di Exchange Online nelle distribuzioni ibride](https://technet.microsoft.com/it-it/library/jj906432\(v=exchg.150\)).

Nella seguente tabella vengono descritti gli attributi supportati per un file CSV per le migrazioni di spostamento remoto onboarding.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributo</th>
<th>Obbligatorio o facoltativo</th>
<th>Valori accettati</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obbligatorio</p></td>
<td><p>Indirizzo SMTP dell'utente</p></td>
<td><p>Specifica l'indirizzo di posta elettronica per l'utente abilitato alla posta nell'organizzazione Exchange Online corrispondente alla cassetta postale utente locale sa migrare.</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>Facoltativo</p></td>
<td><p><code>Unlimited</code> o un intero non negativo da <code>0</code> (valore predefinito) a un valore massimo di <code>2147483647</code></p></td>
<td><p>Specifica il numero di elementi non validi per ignorare se il servizio di migrazione viene rilevato un elemento danneggiato nella cassetta postale. Se si include questo attributo nel file CSV, ignorerà il valore predefinito o il valore specificato se si include il parametro <em>BadItemLimit</em> durante la creazione del batch di migrazione tramite EAC o Exchange Management Shell.</p>

> [!TIP]
> Si consiglia di utilizzare il valore predefinito, 0, e di aumentare il limite di elementi non validi per un particolare utente solo se lo spostamento o la migrazione per tale utente non riesce.


</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>Facoltativo</p></td>
<td><p><code>Unlimited</code> o un intero non negativo da <code>0</code> (valore predefinito) a un valore massimo.</p></td>
<td><p>Specifica il numero di elementi di grandi dimensioni nella cassetta postale dell'utente che verrà ignorata. Quando il numero di elementi di grandi dimensioni supera questo valore, la migrazione della cassetta postale ha esito negativo.</p>
<p>Il valore predefinito è 0, il che significa che la migrazione avrà esito negativo se la cassetta postale contiene elementi di grandi dimensioni.</p>
<p>Nel trasferimento delle cassette postali a Exchange Online, vengono migrati elementi fino a 35 MB.</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>Facoltativo</p></td>
<td><p>Utilizzare uno dei seguenti valori:</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (il valore predefinito)</p></li>
</ul></td>
<td><p>Specifica se si desidera spostare cassetta postale principale dell'utente, cassetta postale di archivio o entrambi.</p></td>
</tr>
</tbody>
</table>


## Spostamenti aziendali tra foreste e migrazioni remote offboarding in una distribuzione ibrida

Come indicato in precedenza, gli spostamenti tra foreste iniziano dalla foresta di destinazione o da quella di origine. Le migrazioni di spostamento remoto offboarding vengono avviate dall'organizzazione Exchange Online. Per ulteriori informazioni, vedere:

  - [Preparare le cassette postali per le richieste di spostamento tra foreste](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Spostare le cassette postali tra le organizzazioni locali e di Exchange Online nelle distribuzioni ibride](https://technet.microsoft.com/it-it/library/jj906432\(v=exchg.150\))

Nella tabella seguente vengono descritti gli attributi supportati per un file CSV per gli spostamenti aziendali tra foreste e per le migrazioni di spostamento remoto offboarding in una distribuzione ibrida Exchange.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributo</th>
<th>Obbligatorio o facoltativo</th>
<th>Valori accettati</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obbligatorio</p></td>
<td><p>Indirizzo SMTP dell'utente</p></td>
<td><p>Per gli spostamenti aziendali tra foreste, specifica la cassetta postale o l'utente abilitato alla posta nella foresta di origine.</p>
<p>Per le migrazioni di spostamento remoto offboarding, specifica la cassetta postale di Exchange Online.</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>Obbligatorio per le migrazioni con spostamenti remoti offboarding e per gli spostamenti tra foreste enterprise avviati dalla foresta di origine. In alternativa, questo attributo può essere specificato durante la creazione del batch di migrazione in EAC o utilizzando Exchange Management Shell.</p>
<p>Questo attributo è facoltativo per gli spostamenti aziendali tra foreste avviati dalla foresta di destinazione.</p></td>
<td><p>Nome del database</p></td>
<td><p>Specifica il database delle cassette postali nella foresta di destinazione che verrà spostata nella cassetta postale principale dell'utente. È possibile specificare un altro database nelle diverse righe del file CSV, che consente di spostare le cassette postali nel batch di migrazione stesso database diversi.</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>Facoltativo</p></td>
<td><p>Nome del database</p></td>
<td><p>Specifica il database delle cassette postali nella foresta di destinazione che verrà spostata nella cassetta postale di archivio dell'utente. È possibile specificare un altro database nelle diverse righe del file CSV, che consente di spostare cassette postali di archiviazione nel batch di migrazione stesso database diversi.</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>Facoltativo</p></td>
<td><p><code>Unlimited</code> o un intero non negativo da <code>0</code> (valore predefinito) a un valore massimo di <code>2147483647</code></p></td>
<td><p>Specifica il numero di elementi non validi per ignorare se il servizio di migrazione viene rilevato un elemento danneggiato nella cassetta postale. Se si include questo attributo nel file CSV, ignorerà il valore predefinito o il valore specificato se si include il parametro <em>BadItemLimit</em> durante la creazione del batch di migrazione tramite EAC o Exchange Management Shell.</p>

> [!TIP]
> Si consiglia di utilizzare il valore predefinito, 0, e di aumentare il limite di elementi non validi per un particolare utente solo se lo spostamento o la migrazione per tale utente non riesce.


</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>Facoltativo</p></td>
<td><p><code>Unlimited</code> o un intero non negativo da <code>0</code> (valore predefinito) a un valore massimo.</p></td>
<td><p>Specifica il numero di elementi di grandi dimensioni nella cassetta postale dell'utente che verrà ignorata. Quando il numero di elementi di grandi dimensioni supera questo valore, la migrazione della cassetta postale ha esito negativo.</p>
<p>Il valore predefinito è 0, il che significa che la migrazione avrà esito negativo se la cassetta postale contiene elementi di grandi dimensioni.</p>
<p>Nel trasferimento delle cassette postali a Exchange Online, vengono migrati elementi fino a 35 MB.</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>Facoltativo</p></td>
<td><p>Utilizzare uno dei seguenti valori:</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (il valore predefinito)</p></li>
</ul></td>
<td><p>Specifica se si desidera spostare cassetta postale principale dell'utente, cassetta postale di archivio o entrambi.</p></td>
</tr>
</tbody>
</table>


## Migrazioni di Exchange in fasi

È necessario utilizzare un file CSV per identificare il gruppo di utenti per un batch di migrazione quando si desidera eseguire una migrazione di Exchange in fasi delle cassette postali locali di Exchange 2003 e Exchange 2007 a Exchange Online. Il numero di cassette postali che è possibile migrare al cloud utilizzando una migrazione di Exchange in fasi è illimitato. Tuttavia, nel file CSV per un batch di migrazione possono essere contenute al massimo 1000 righe. Per migrare più di 1000 cassette postali è necessario creare ulteriori file CSV e utilizzare ciascuno per creare un batch di migrazione. Per ulteriori informazioni sulle migrazioni di Exchange in fasi, vedere [Migrazione in fasi delle cassette postali a Exchange Online](https://technet.microsoft.com/it-it/library/jj874018\(v=exchg.150\)).

Nella seguente tabella vengono descritti gli attributi supportati per un file CSV per la migrazione di Exchange in fasi.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributo</th>
<th>Obbligatorio o facoltativo</th>
<th>Valori accettati</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obbligatorio</p></td>
<td><p>Indirizzo SMTP dell'utente</p></td>
<td><p>Specifica l'indirizzo di posta elettronica per l'utente abilitato alla posta (o una cassetta postale se si sta la ripetizione la migrazione) in Exchange Online corrispondente alla cassetta postale utente locale che verrà migrata. Gli utenti abilitati alla posta elettronica vengono creati in Exchange Online a causa di sincronizzazione della directory o un altro processo di provisioning. L'indirizzo di posta elettronica dell'utente abilitato alla posta deve corrispondere la proprietà <em>WindowsEmailAddress</em> per la cassetta postale locale corrispondente.</p></td>
</tr>
<tr class="even">
<td><p>Password</p></td>
<td><p>Facoltativo</p></td>
<td><p>Una password deve avere una lunghezza minima di otto caratteri e soddisfare eventuali restrizioni password applicate all'organizzazione Office 365.</p></td>
<td><p>Questa password viene impostata sull'account utente quando l'utente abilitato alla posta corrispondente in Exchange Online viene convertito in una cassetta postale durante la migrazione.</p></td>
</tr>
<tr class="odd">
<td><p>ForceChangePassword</p></td>
<td><p>Facoltativo</p></td>
<td><p><code>True</code> oppure <code>False</code></p></td>
<td><p>Specifica se un utente deve cambiare la password al primo accesso alla cassetta postale di Exchange Online.</p>

> [!NOTE]
> Se sono stati implementati una soluzione single sign-on tramite la distribuzione di Active Directory Federation Services 2.0 (AD FS 2.0) nella propria organizzazione locale, è necessario utilizzare <CODE>False</CODE> per il valore di questo attributo.


</td>
</tr>
</tbody>
</table>


## Migrazioni IMAP

Un file CSV per un batch di migrazione IMAP può contenere massimo 50.000 righe. È tuttavia consigliabile eseguire la migrazione degli utenti in diversi batch più piccoli. Per ulteriori informazioni sulle migrazioni IMAP, vedere i seguenti argomenti:

  - [Migrare la posta da un server IMAP alle cassette postali di Exchange Online](https://technet.microsoft.com/it-it/library/jj874015\(v=exchg.150\))

  - [File CSV per il batch di migrazione IMAP](https://technet.microsoft.com/it-it/library/jj200730\(v=exchg.150\))

Nella seguente tabella vengono descritti gli attributi supportati per un file CSV per una migrazione IMAP.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributo</th>
<th>Obbligatorio o facoltativo</th>
<th>Valori accettati</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obbligatorio</p></td>
<td><p>Indirizzo SMTP dell'utente.</p></td>
<td><p>Specifica l'ID utente per la cassetta postale di Exchange Online dell'utente.</p></td>
</tr>
<tr class="even">
<td><p>UserName</p></td>
<td><p>Obbligatorio</p></td>
<td><p>Stringa che identifica l'utente del sistema di messaggistica IMAP in un formato supportato dal server IMAP.</p></td>
<td><p>Specifica il nome di accesso per l'account dell'utente nel sistema di messaggistica IMAP (l'ambiente di origine). Oltre al nome utente, è possibile utilizzare le credenziali di un account assegnato le autorizzazioni necessarie per accedere alle cassette postali nel server IMAP. Per ulteriori informazioni, vedere <a href="https://technet.microsoft.com/it-it/library/jj200730(v=exchg.150)">File CSV per il batch di migrazione IMAP</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Password</p></td>
<td><p>Obbligatorio</p></td>
<td><p>Stringa della password.</p></td>
<td><p>Specifica la password per l'account utente specificato dall'attributo UserName.</p></td>
</tr>
</tbody>
</table>


## I valori degli attributi nel file CSV sovrascrivono i valori per il batch di migrazione.

I valori di attributo nel file CSV per ignorare il valore del parametro corrispondente quando si utilizza il parametro stesso durante la creazione di un batch di migrazione con l'interfaccia di amministrazione di Exchange o Exchange Management Shell. Se si desidera che il valore di batch di migrazione da applicare a un utente, è opportuno lasciare che la cella vuota nel file CSV. Ciò consente di combinare e soddisfano determinati valori degli attributi per gli utenti selezionati in un batch di migrazione.

Ad esempio, aggiungere creiamo un batch in Exchange Management Shell per il primario degli utenti da spostare un'organizzazione tra foreste e cassette postali di archiviazione alla foresta di destinazione utilizzando il seguente comando Exchange Management Shell.

```powershell
    New-MigrationBatch -Name CrossForestBatch1 -SourceEndpoint ForestEndpoint1 -TargetDeliveryDomain forest2.contoso.com -TargetDatabases @(EXCH-MBX-02,EXCH-MBX-03) -TargetArchiveDatabases @(EXCH-MBX-A02,EXCH-MBX-A03) -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\CrossForestBatch1.csv")) -AutoStart
```

> [!NOTE]
> Poiché il valore predefinito è spostare primario e cassette postali di archiviazione, non è necessario specificare in modo esplicito nel comando Exchange Management Shell.



Una parte del file CrossForestBatch1.csv per questo batch di migrazione appare simile alla seguente:

```powershell
    EmailAddress,TargetDatabase,TargetArchiveDatabase
    user1@contoso.com,EXCH-MBX-01,EXCH-MBX-A01
    user2@contoso.com,,
    user3@contoso.com,EXCH-MBX-01,
    ...
```

Poiché i valori del file CSV sovrascrivono i valori per il batch di migrazione, le cassette postali primaria e di archivio per user1 saranno spostate in EXCH-MBX-01 e EXCH-MBX-A01 rispettivamente nella foresta di destinazione. Le cassette postali principale e di archivio per user2 vengono spostate in EXCH-MBX-02 o EXCH-MBX-03. La cassetta postale primaria per user3 viene spostata in EXCH-MBX-01 e la cassetta postale di archivio in EXCH-MBX-A02 o EXCH-MBX-A03

In un altro esempio, si supponga che si crea un batch di una migrazione di spostamento remoto onboarding in una distribuzione ibrida per spostare le cassette postali di archiviazione in Exchange Online con il comando seguente.

```powershell
    New-MigrationBatch -Name OnBoarding1 -SourceEndpoint RemoteEndpoint1 -TargetDeliveryDomain cloud.contoso.com -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\OnBoarding1.csv")) -MailboxType ArchiveOnly -AutoStart
```

Poiché si desidera spostare le cassette postali primarie per utenti selezionati, una parte del file OnBoarding1.csv per questo batch di migrazione apparirà simile alla seguente:

```powershell
    EmailAddress,MailboxType
    user1@contoso.com,
    user2@contoso.com,
    user3@cloud.contoso.com,PrimaryAndArchive
    user4@cloud.contoso.com,PrimaryAndArchive
    ...
```

Poiché il valore del tipo di cassetta postale nel file CSV sovrascrive i valori per il parametro *MailboxType* nel comando per creare il batch, solo la cassetta postale di archivio per user1 e user2 viene migrata a Exchange Online. Le cassette postali primarie e di archivio per user3 e user4 vengono spostate in Exchange Online.


---
title: 'Informazioni sui filtri di ambito di gestione dei ruoli: Exchange 2013 Help'
TOCTitle: Informazioni sui filtri di ambito di gestione dei ruoli
ms:assetid: 6acc2922-ee9c-41f1-8a0f-10a541e8c273
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298043(v=EXCHG.150)
ms:contentKeyID: 50480823
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Informazioni sui filtri di ambito di gestione dei ruoli

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

I filtri di ambito del ruolo di gestione possono essere utilizzati per definire ambiti di gestione altamente personalizzabili. Utilizzando i filtri ambito, è possibile creare un ambito corrispondente alla modalità di segmentazione dei destinatari, dei database e dei server, affinché gli amministratori possano gestire solo quegli oggetti a cui hanno accesso. I filtri ambito possono utilizzare quasi tutte le proprietà dell'oggetto destinatario, database o server.

Per utilizzare i filtri dell'ambito del ruolo di gestione, è necessario conoscere gli ambiti dei ruoli di gestione. Per ulteriori informazioni sugli ambiti dei ruoli di gestione, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

Gli ambiti personalizzati filtrati in Microsoft Exchange Server 2013 vengono creati utilizzando il cmdlet **New-ManagementScope**. I due tipi di ambiti filtrati, per destinatario e per configurazione (che consiste in ambiti di server e database), si dividono in ambiti normali ed esclusivi. Nel seguente elenco sono indicati i parametri da utilizzare nel cmdlet **New-ManagementScope** per creare i diversi tipi di ambito filtrato:

  - **Ambito filtrato normale per destinatario**   Per creare questo tipo di ambito filtrato, utilizzare il parametro *RecipientRestrictionFilter*.

  - **Ambito filtrato esclusivo per destinatario**   Per creare questo tipo di ambito filtrato, utilizzare il parametro *RecipientRestrictionFilter* con l'opzione *Exclusive*.

  - **Ambito filtrato normale per configurazione basata su server**   Per creare questo tipo di ambito filtrato, utilizzare il parametro *ServerRestrictionFilter*.

  - **Ambito filtrato esclusivo per configurazione basata su server**   Per creare questo tipo di ambito filtrato, utilizzare il parametro *ServerRestrictionFilter* con l'opzione *Exclusive*.

  - **Ambito filtrato normale per configurazione basata su database**   Per creare questo tipo di ambito filtrato, utilizzare il parametro *DatabaseRestrictionFilter*.

  - **Ambito filtrato esclusivo per configurazione basata su database**   Per creare questo tipo di ambito filtrato, utilizzare il parametro *DatabaseRestrictionFilter* con l'opzione *Exclusive*.

Quando si crea un ambito personalizzato filtrato, l'ambito cerca di individuare una corrispondenza tra il filtro e qualsiasi oggetto accessibile nell'ambito implicito di lettura del ruolo di gestione. Se trova un oggetto, questo viene incluso tra i risultati restituiti dal filtro e reso disponibile per il ruolo di gestione. Un filtro non può restituire risultati esterni all'ambito implicito di lettura del ruolo di gestione.

Se si specifica un filtro per destinatario usando il parametro *RecipientRestrictionFilter*, è possibile usare il parametro *RecipientRoot* per specificare un'unità organizzativa a cui limitare il filtro. Quando si specifica un'unità organizzativa nel parametro *RecipientRoot*, il filtro per destinatario tenta di individuare i destinatari corrispondenti che si trovano solo nell'unità organizzativa e non entro l'intero ambito implicito di lettura.

Per creare un ambito di gestione utilizzando le proprietà filtrabili incluse in questo argomento, vedere [Creare un ambito normale o esclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

## Sintassi del filtro

I filtri, siano essi per destinatario o per configurazione, utilizzano la stessa sintassi per creare una query. Tutte le query di filtro devono avere almeno i seguenti componenti:

  - **Parentesi di apertura**   La parentesi di apertura ({) indica l'inizio della query del filtro.

  - **Proprietà da esaminare**   La proprietà è il valore di un oggetto che si desidera esaminare. Ad esempio, può trattarsi della città o del reparto di un oggetto destinatario, un nome server o sito di Active Directory su un oggetto di configurazione del server o un nome di database su un oggetto di configurazione del database.

  - **Operatore di confronto**   L'operatore di confronto stabilisce in che modo la query deve valutare il valore specificato rispetto a quello archiviato nella proprietà. Ad esempio, gli operatori di confronto possono essere **Eq** (che significa "uguale a"), **Ne** (che significa "non uguale a"), **Like** (che significa "simile a") e così via. Per l'elenco completo degli operatori che è possibile utilizzare in Exchange Management Shell, vedere [Operatori di confronto](https://technet.microsoft.com/it-it/library/bb125229\(v=exchg.150\)).

  - **Valore da confrontare**   Il valore specificato nella query del filtro verrà confrontato con il valore archiviato nella proprietà specificata. Il valore specificato deve essere racchiuso tra virgolette ("). Se si desidera specificare una stringa parziale, è possibile includerla tra caratteri jolly (\*) e utilizzare un operatore di confronto che supporta i caratteri jolly, quale **Like**. Qualsiasi stringa che contiene la stringa parziale verrà indicata come corrispondente alla query del filtro.

  - **Parentesi di chiusura**   La parentesi di chiusura (}) indica la fine della query del filtro.

I seguenti componenti sono facoltativi e consentono di creare query del filtro più complesse:

  - **Parentesi**   Proprio come in matematica, le parentesi ( ) in una query del filtro consentono di definire l'ordine delle operazioni. Le parentesi più interne vengono valutate per prime e la query del filtro si muove poi verso quelle più esterne.

  - **Operatori logici**   Gli operatori logici uniscono una o più operazioni di confronto e fanno sì che la query del filtro valuti l'intera istruzione. Tra gli operatori logici vi sono **And**, **Or** e **Not**.

Una volta composta, una query semplice sarà simile a questa: `{ City -Eq "Vancouver" }`. Questo filtro individua tutti i destinatari in cui il valore della proprietà **City** è uguale alla stringa "Vancouver".

Un'altra query più complessa è `{ ((City -Eq "Vancouver") -And (Department -Eq "Sales")) -Or (Title -Like "*Manager*") }`. La query del filtro viene valutata nel seguente ordine:

1.  Vengono valutate le proprietà **City** e **Department**. Ognuna di queste è impostata su `True` o `False`, a seconda del valore archiviato in ciascuna proprietà.

2.  Vengono quindi valutati i risultati delle istruzioni **City** e **Department**. Se entrambe sono `True`, l'intera istruzione **And** diventa `True`. Se uno o entrambi sono `False`, l'intera istruzione **And** diventerà `False`. Valgono i seguenti presupposti:
    
      - Se l'istruzione **And** viene valutata come `True`, l'intera query del filtro diventa `True` perché l'operatore **Or** indica che uno dei lati della query deve essere `True`. L'oggetto viene esposto per l'assegnazione del ruolo.
    
      - Se l'istruzione **And** è `False`, la query del filtro continua con la valutazione della proprietà **Title**.

3.  Viene quindi valutata la proprietà **Title**. È impostata su `True` o `False`, a seconda del valore archiviato nella proprietà **Title**. Valgono i seguenti presupposti:
    
      - Se la proprietà **Title** viene valutata come `True`, l'intera query del filtro diventa `True` perché l'operatore **Or** indica che uno dei lati della query deve essere `True`. L'oggetto viene esposto per l'assegnazione del ruolo.
    
      - Se la proprietà **Title** viene valutata come `False`, l'intera query del filtro viene valutata come `False` e l'oggetto non viene esposto per l'assegnazione del ruolo.

Nella seguente tabella è riportato un esempio con valori che mostra quando la query complessa verrebbe valutata come `True` e quando invece come `False`.

### Query complessa

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>City</th>
<th>Department</th>
<th>Title</th>
<th>Risultato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Sales (True)</p></td>
<td><p>CEO (False)</p></td>
<td><p>True perché sia <strong>City</strong> sia <strong>Department</strong> sono valutate come True. <strong>Title</strong> non viene valutata perché le condizioni della query del filtro sono già soddisfatte.</p></td>
</tr>
<tr class="even">
<td><p>Seattle (False)</p></td>
<td><p>Sales (True)</p></td>
<td><p>IT Manager (True)</p></td>
<td><p>True perché <strong>Title</strong> viene valutata come True. I risultati del confronto <strong>City</strong> e <strong>Department</strong> vengono ignorati perché <strong>Title</strong> è stata valutata come True, soddisfando così le condizioni della query del filtro.</p>

> [!NOTE]
> IT Manager soddisfa la query del filtro perché è stato utilizzato l'operatore di confronto <STRONG>Like</STRONG> che consente di individuare le stringhe parziali quando i caratteri jolly (*) vengono utilizzati nella query del filtro.


</td>
</tr>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Marketing (False)</p></td>
<td><p>Writer (False)</p></td>
<td><p>False perché <strong>City</strong> e <strong>Department</strong> non sono state entrambe valutate come True e anche <strong>Title</strong> non è stata valutata come True.</p></td>
</tr>
</tbody>
</table>


## Proprietà destinatario filtrabili

Quando si crea un filtro per destinatario è possibile utilizzare praticamente qualsiasi proprietà su un oggetto destinatario. Per un elenco delle proprietà filtrabili per destinatario, vedere [Proprietà filtrabili per il parametro -RecipientFilter](https://technet.microsoft.com/it-it/library/bb738157\(v=exchg.150\)). Sebbene questo argomento discuta le proprietà che è possibile utilizzare con il parametro *RecipientFilter* su altri cmdlet, la maggior parte di queste proprietà funziona anche con il parametro *RecipientRestrictionFilter* sul cmdlet **New-ManagementScope**.

## Proprietà server filtrabili

È possibile utilizzare le seguenti proprietà del server quando si crea l'ambito di gestione con il parametro *ServerRestrictionFilter*:

  - **CurrentServerRole**

  - **CustomerFeedbackEnabled**

  - **DataPath**

  - **DistinguishedName**

  - **ExchangeLegacyDN**

  - **ExchangeLegacyServerRole**

  - **ExchangeVersion**

  - **Fqdn**

  - **Guid**

  - **InternetWebProxy**

  - **Name**

  - **NetworkAddress**

  - **ObjectCategory**

  - **ObjectClass**

  - **ProductID**

  - **ServerRole**

  - **ServerSite**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

## Proprietà database filtrabili

È possibile utilizzare le seguenti proprietà del database quando si crea un ambito di gestione con il parametro *DatabaseRestrictionFilter*:

  - **AdminDisplayName**

  - **AllowFileRestore**

  - **BackgroundDatabaseMaintenance**

  - **CircularLoggingEnabled**

  - **DatabaseCreated**

  - **DeletedItemRetention**

  - **Description**

  - **DistinguishedName**

  - **EdbFilePath**

  - **EventHistoryRetentionPeriod**

  - **ExchangeLegacyDN**

  - **ExchangeVersion**

  - **Guid**

  - **IssueWarningQuota**

  - **LogFilePrefix**

  - **LogFileSize**

  - **LogFolderPath**

  - **MasterServerOrAvailabilityGroup**

  - **MountAtStartup**

  - **Name**

  - **ObjectCategory**

  - **ObjectClass**

  - **RetainDeletedItemsUntilBackup**

  - **Server**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**


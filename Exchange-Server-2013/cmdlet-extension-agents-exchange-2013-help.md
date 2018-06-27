---
title: 'Agenti di estensione di cmdlet: Exchange 2013 Help'
TOCTitle: Agenti di estensione di cmdlet
ms:assetid: 0257790d-3988-46c3-8882-25ca11559e84
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335054(v=EXCHG.150)
ms:contentKeyID: 50555529
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agenti di estensione di cmdlet

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Gli agenti di estensione cmdlet sono componenti di Microsoft Exchange Server 2013 richiamati dai cmdlet di Exchange 2013 quando vengono eseguiti. Come suggerisce il nome, gli agenti di estensione cmdlet estendono le funzionalità dei cmdlet che li richiamano semplificando l'elaborazione dei dati o eseguendo ulteriori azioni in base ai requisiti del cmdlet. Gli agenti di estensione cmdlet sono disponibili in qualsiasi ruolo del server.

Gli agenti possono modificare, sostituire o estendere le funzionalità dei cmdlet di Exchange Management Shell. Un agente può fornire un valore per un parametro necessario non fornito sul comando, sostituire un valore fornito da un utente, eseguire altre azioni all'esterno del flusso di lavoro del cmdlet durante l'esecuzione di un cmdlet o molto altro.

Ad esempio, il cmdlet **New-Mailbox** accetta il parametro *Database* che specifica il database delle cassette postali in cui creare una nuova cassetta postale. In Microsoft Exchange Server 2007, se non si specifica il parametro *Database* quando si esegue il cmdlet **New-Mailbox**, il comando ha esito negativo. Tuttavia, Exchange 2013, il cmdlet **New-Mailbox** richiama l'agente `Mailbox Resources Management` quando il cmdlet è in esecuzione. Se il parametro *Database* non viene specificato, l'agente `Mailbox Resources Management` determina automaticamente un database delle cassette postali appropriato in cui creare la nuova cassetta postale e inserisce il valore nel parametro *Database*.

Gli agenti di estensione cmdlet possono essere richiamati solo dai cmdlet di Exchange 2013 e Microsoft Exchange Server 2010. I cmdlet di Exchange 2007 e quelli forniti da altri prodotti Microsoft e di terze parti non possono richiamare gli agenti di estensione cmdlet. Anche gli script non possono richiamare direttamente gli agenti di estensione cmdlet. Tuttavia, se gli script contengono i cmdlet di Exchange 2013, tali cmdlet continuano a chiamare gli agenti di estensione cmdlet.

Per informazioni sulle attività di gestione relative agli agenti di estensione cmdlet? vedere [Gestire gli agenti di estensione cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Priorità dell'agente

La priorità dell'agente determina l'ordine in cui gli agenti vengono richiamati durante l'esecuzione di un cmdlet. L'agente con la priorità superiore, più vicina a 0, viene richiamato per primo. La priorità di un agente diventa importante quando due o più agenti tentano di impostare il valore della stessa proprietà. L'agente con la priorità più alta che tenta di impostare un valore della proprietà riesce nell'operazione e tutti i tentativi successivi di impostare la stessa proprietà da parte di agenti con priorità più bassa, vengono ignorati. Ad esempio, se la proprietà **Name** su un oggetto viene modificata da un agente con priorità 3 e un altro agente con priorità 6 modifica lo stesso oggetto, la modifica apportata dall'agente con priorità 6 viene ignorata.

Se si desidera utilizzare `Scripting agent` per impostare il valore delle proprietà che potrebbero essere impostate da altri agenti con priorità più alta, è possibile effettuare quanto segue:

  - Disabilitare l'agente che attualmente imposta la proprietà.

  - Impostare `Scripting agent` su una priorità più alta rispetto all'agente esistente che si desidera sostituire.

  - Mantenere le stesse priorità per gli agenti e verificare che lo script che viene eseguito con `Scripting agent` rispetti il valore fornito da altri agenti.


> [!WARNING]
> La modifica della priorità o la sostituzione della funzionalità di un agente incorporato è un'operazione avanzata. Assicurarsi di essere pienamente consapevoli delle modifiche che verranno apportate.



Per ulteriori informazioni sulla modifica della priorità di un agente, vedere [Gestire gli agenti di estensione cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Agenti incorporati

Exchange 2013 comprende numerosi agenti che possono essere richiamati quando viene eseguito un cmdlet. Nella tabella seguente sono elencati gli agenti nell'ordine esatto ed è indicato se gli agenti sono abilitati per impostazione predefinita. Non è possibile aggiungere agenti o rimuoverli da un server Exchange 2013. È possibile tuttavia utilizzare `Scripting agent` per eseguire script di Windows PowerShell per estendere la funzionalità dei cmdlet che lo utilizzano. Per ulteriori informazioni su `Scripting agent`, vedere la sezione "Agente di script" più avanti in questo argomento.

È possibile abilitare o disabilitare la maggior parte degli agenti o modificarne la priorità se si desidera sostituire la funzionalità di un determinato agente con la funzionalità fornita in uno script personalizzato richiamato dall'utente con `Scripting agent`. Tuttavia, alcuni agenti non possono essere disabilitati. Gli agenti che non possono essere disabilitati sono denominati *agenti di sistema*, la cui proprietà *IsSystem* è impostata su `$True`. Nella tabella seguente vengono fornite informazioni sugli agenti di estensione cmdlet Exchange 2013, inclusi gli agenti di sistema.

La configurazione per gli agenti viene memorizzata a livello di organizzazione. Quando si abilita o si disabilita un agente o si imposta la priorità, è necessario impostare la configurazione dell'agente in ogni server dell'organizzazione. L'eccezione è l'aggiunta di script a `Scripting agent`. È necessario aggiornare gli script in ogni server singolarmente. Per ulteriori informazioni sulla configurazione degli script da utilizzare con `Scripting agent`, vedere la sezione "Agente di script" più avanti in questo argomento.


> [!WARNING]
> La modifica della priorità degli agenti o l'abilitazione o disabilitazione degli agenti, può causare conseguenze indesiderate se non si comprende completamente l'attività di ogni agente e la loro interazione con i cmdlet di Exchange. Prima di modificare la configurazione di ogni agente, assicurarsi di essere completamente consapevoli delle modifiche e dei risultati desiderati e di verificare che lo script personalizzato funzioni correttamente.



### Agenti di estensione cmdlet di Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome agente</th>
<th>Priorità</th>
<th>Abilitato per impostazione predefinita</th>
<th>Agente di sistema</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Admin Audit Log agent</code></p></td>
<td><p>255</p></td>
<td><p>True</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p><code>Scripting agent</code></p></td>
<td><p>6</p></td>
<td><p>False</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Resources Management agent</code></p></td>
<td><p>5</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><code>OAB Resources Management agent</code></p></td>
<td><p>4</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><code>Query Base DN agent</code></p></td>
<td><p>3</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><code>Provisioning Policy agent</code></p></td>
<td><p>2</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><code>Rus agent</code></p></td>
<td><p>1</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Creation Time agent</code></p></td>
<td><p>0</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


## Agente di script

È possibile utilizzare l'agente di estensione cmdlet `Scripting agent` in Exchange 2013 per inserire la propria logica di script nell'esecuzione dei cmdlet di Exchange. Utilizzando l'agente `Scripting agent`, è possibile aggiungere condizioni, sovrascrivere valori e configurare l'attività di report.


> [!WARNING]
> Quando si abilita l'agente di estensione cmdlet <CODE>Scripting agent</CODE>, l'agente viene richiamato ogni volta che un cmdlet viene eseguito su un server Exchange 2013. Ciò include non solo i cmdlet eseguiti direttamente dall'utente in Exchange&nbsp;Management Shell, ma anche i cmdlet eseguiti dai servizi di Exchange&nbsp; e dall'interfaccia di amministrazione di Exchange. Si consiglia vivamente di effettuare dei test sugli script e su qualsiasi modifica apportata al file prima di copiare il file di configurazione aggiornato sui server Exchange 2013&nbsp;e di abilitare l'agente di estensione cmdlet <CODE>Scripting agent</CODE>.



Ogni volta che viene eseguito un cmdlet Exchange, quest'ultimo richiama l'agente di estensione cmdlet `Scripting agent`. Quando questo agente viene richiamato, il cmdlet verifica se nessuno script è configurato per essere richiamato dal cmdlet. Se uno script deve essere eseguito per un cmdlet, il cmdlet tenta di richiamare tutte le API definite nello script. Sono disponibili le seguenti API, che vengono richiamate nell'ordine seguente:

1.  **ProvisionDefaultProperties**   Questo API può essere utilizzato per impostare i valori delle proprietà sugli oggetti quando vengono creati. Quando si imposta un valore, quel valore viene restituito al cmdlet e il cmdlet imposta il valore sulla proprietà. È possibile inserire i valori sulle proprietà se l'utente non ha specificato un valore oppure è possibile sovrascrivere il valore specificato dall'utente. Questo API rispetta i valori impostati dagli agenti di più elevata priorità. L'agente di estensione cmdlet `Scripting agent` non sovrascriverà i valori impostati dagli agenti con priorità più elevata.

2.  **UpdateAffectedIConfigurable**   Si tratta di un'API che può essere utilizzata per impostare i valori delle proprietà sugli oggetti dopo che tutti i processi di elaborazione saranno stati completati, ma l'API `Validate` non ancora richiamata. Questo API rispetta i valori impostati dagli agenti di più elevata priorità. L'agente di estensione cmdlet `Scripting agent` non sovrascriverà i valori impostati dagli agenti con priorità più elevata.

3.  **Validate**   È possibile utilizzare questo API per convalidare i valori sulle proprietà di un oggetto che stanno per essere impostate dal cmdlet. Questo API viene chiamato subito prima che un cmdlet scriva qualsiasi dato. È possibile configurare le verifiche di convalida che consentono ad un cmdlet di riuscire o meno. Se un cmdlet passa le verifiche di convalida in questo API, al cmdlet viene consentito di scrivere i dati. Se il cmdlet non passa le verifiche di convalida, restituisce tutti gli errori definiti in questo API.

4.  **OnComplete**   Questo API viene utilizzato dopo che tutti i processi di elaborazione del cmdlet saranno stati elaborati. Può essere utilizzato per eseguire le attività di postelaborazione come scrivere dati su un database esterno.


> [!NOTE]
> L'agente di estensione cmdlet <CODE>Scripting agent</CODE> non viene richiamato quando vengono eseguiti i cmdlet con il verbo <CODE>Get</CODE>.



## File di configurazione dell'agente di script

Il file di configurazione di `Scripting agent` contiene tutti gli script da eseguire con `Scripting agent`. Gli script nel file di configurazione sono contenuti all'interno dei tag XML che definiscono l'inizio e la fine dello script e i vari parametri di input necessari per passare i dati allo script. Gli script vengono scritti utilizzando la sintassi PowerShell di Windows. Il file di configurazione è un file XML che utilizza gli elementi o gli attributi nella seguente tabella.

### Attributi del file di configurazione dell'agente di script

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Attributo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Configuration</code></p></td>
<td><p>Non applicabile</p></td>
<td><p>Questo elemento contiene tutti gli script che l'agente di estensione cmdlet <code>Scripting agent</code> può eseguire. Il tag <code>Feature</code> è un elemento secondario di questo tag.</p>
<p>È presente un solo tag <code>Configuration</code> in ogni file di configurazione.</p></td>
</tr>
<tr class="even">
<td><p><code>Feature</code></p></td>
<td><p>Non applicabile</p></td>
<td><p>Questo elemento contiene un gruppo di script relativo ad una funzionalità. Ciascuno script, definito nel tag secondario <code>ApiCall</code>, estende una parte specifica della pipeline di esecuzione del cmdlet. Questo tag contiene gli attributi <code>Name</code> e <code>Cmdlets</code>.</p>
<p>Possono esserci più tag <code>Feature</code> per il tag <code>Configuration</code>.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>Questa proprietà contiene il nome della funzionalità. Utilizzare questo attributo per contribuire ad identificare quale funzionalità viene estesa dagli script contenuti all'interno del tag.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Cmdlets</code></p></td>
<td><p>Questo attributo contiene un elenco dei cmdlet Exchange  che verranno utilizzati dal gruppo di script di questa estensione di funzionalità. È possibile specificare più cmdlet separando ciascuno con una virgola.</p></td>
</tr>
<tr class="odd">
<td><p><code>ApiCall</code></p></td>
<td><p>Non applicabile</p></td>
<td><p>Questo elemento contiene gli script che possono estendere una parte della pipeline di esecuzione del cmdlet. Ciascuno script viene definito dal nome di chiamata API nella pipeline di esecuzione del cmdlet in estensione. I nomi API che possono essere estesi sono i seguenti:</p>
<ul>
<li><p><code>ProvisionDefaultProperties</code></p></li>
<li><p><code>UpdateAffectedIConfigurable</code></p></li>
<li><p><code>Validate</code></p></li>
<li><p><code>OnComplete</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>Questo attributo include il nome della chiamata API che sta estendendo la pipeline di esecuzione del cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><code>Common</code></p></td>
<td><p>Non applicabile</p></td>
<td><p>Questo elemento contiene delle funzioni che qualsiasi script del file di configurazione può utilizzare.</p></td>
</tr>
</tbody>
</table>


Ogni server Exchange 2013 include il file ScriptingAgentConfig.xml.sample nella cartella del \<*percorso di installazione* \>\\V14\\Bin\\CmdletExtensionAgents. Questo file deve essere rinominato ScriptingAgentConfig.xml su ogni server Exchange 2013 se si abilita l'agente di estensione del cmdlet Agente di script. Il file di configurazione di esempio contiene script di esempio che è possibile utilizzare per contribuire a comprendere in che modo aggiungere gli script al file di configurazione.

Dopo aver aggiunto uno script al file di configurazione, oppure se si apporta una modifica al file di configurazione, è necessario aggiornarlo su ogni server Exchange 2013 della propria organizzazione. L'operazione è indispensabile per accertarsi che ciascun server contenga una versione aggiornata degli script eseguiti dall'agente di estensione cmdlet `Scripting Agent`.

Alcuni caratteri normalmente utilizzati negli script hanno anche un significato particolare in XML. Per utilizzare questi caratteri nello script, utilizzare le sequenze di escape. Ad esempio, i seguenti caratteri utilizzano una sequenza di escape:

  - Anziché il segno "maggiore di" ( `>` ), utilizzare `&gt;`

  - Anziché il segno "minore di" ( `<` ), utilizzare `$lt;`

  - Anziché il simbolo di "E commerciale" ( `&` ), utilizzare `&amp;`

## Abilitazione dell'agente di script

L'agente di estensione cmdlet `Scripting agent` è disabilitato per impostazione predefinita. Quando si abilita `Scripting agent`, l'agente viene abilitato per l'intera organizzazione di Exchange 2013 . Prima di abilitare `Scripting agent`, verificare che il file di configurazione `Scripting agent` sia stato rinominato correttamente e aggiornato con gli script su ogni server Exchange 2013. Si riceverà un messaggio di errore ogni volta che un cmdlet viene eseguito se il file di configurazione non viene rinominato correttamente o se viene copiato sul computer da un server Exchange 2013 diverso.

Per abilitare `Scripting agent`, è necessario effettuare le seguenti operazioni:

1.  Rinominare il file ScriptingAgentConfig.xml.sample nel **\<percorso di installazione \>\\V15\\Bin\\CmdletExtensionAgents** con ScriptingAgentConfig.xml su ogni server Exchange 2013 dell'organizzazione.
    

    > [!NOTE]
    > È possibile copiare il file di configurazione da un server Exchange 2013 ad altri serverExchange 2013&nbsp;. Accertarsi di aggiornare il file di configurazione che si desidera copiare, prima di copiarlo.



2.  Aggiungere lo script al file di configurazione rinominato su ogni server Exchange 2013 nella propria organizzazione.

3.  Abilitazione dell'agente di estensione cmdlet `Scripting agent`. Per ulteriori informazioni sugli agenti di estensione dei cmdlet, vedere [Gestire gli agenti di estensione cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Priorità dell'agente di script

Per impostazione predefinita, l'agente di estensione cmdlet `Scripting agent` viene eseguito dopo ogni altro agente, ad accezione dell'agente `Scripting agent`. Se si desidera creare uno script per sostituire un agente esistente, è necessario disabilitare l'altro agente o modificare la priorità di entrambi gli agenti in modo che l'agente di estensione cmdlet `Scripting agent` venga eseguito per primo. Per ulteriori informazioni sulla disabiltazione o la modifica della priorità degli agenti, vedere [Gestire gli agenti di estensione cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).


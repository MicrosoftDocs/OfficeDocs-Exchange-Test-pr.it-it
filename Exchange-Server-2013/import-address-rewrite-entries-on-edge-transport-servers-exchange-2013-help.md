---
title: 'Nei server Trasporto Edge voci di riscrittura degli indirizzi di importazione: Exchange 2013 Help'
TOCTitle: Nei server Trasporto Edge voci di riscrittura degli indirizzi di importazione
ms:assetid: bd0942c6-9c66-4b4c-b9bc-2f5f783def76
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb331966(v=EXCHG.150)
ms:contentKeyID: 61060529
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Nei server Trasporto Edge voci di riscrittura degli indirizzi di importazione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile creare in blocco o importare le informazioni sulla riscrittura degli indirizzi in un server Trasporto Edge utilizzando un file CSV. Nell'elenco vengono descritte le situazioni comuni che richiedono all'utente di effettuare le seguenti operazioni:

  - Si sta sostituendo una soluzione di riscrittura degli indirizzi in un server Trasporto Edge.

  - Si conclude un accordo con un fornitore di soluzioni di terze parti che richiede all'utente di riscrivere gli indirizzi di posta elettronica.

  - Si acquisisce un'altra organizzazione ed è necessario riscrivere temporaneamente gli indirizzi di posta elettronica nell'organizzazione acquisita.

Per creare il file CSV, è possibile utilizzare un editor di testo o un'applicazione come Microsoft Excel o il Blocco note. Formattare il file seguendo le istruzioni fornite in questo argomento e salvarlo come file csv.

Nella prima riga o *roga di intestazione* del file CSV vengono elencati i nomi dei parametri. Ciascun parametro è separato da una virgola. I parametri necessari e opzionali sono descritti nella tabella seguente.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio o facoltativo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Nome univoco, descrittivo per la voce di riscrittura degli indirizzi.</p></td>
</tr>
<tr class="even">
<td><p><em>InternalAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>L'indirizzo da modificare. È possibile utilizzare i seguenti valori:</p>
<ul>
<li><p>Un indirizzo di posta elettronica singolo (chris@contoso.com)</p></li>
<li><p>Un singolo dominio o un sottodominio (contoso.com o sales.contoso.com)</p></li>
<li><p>Un dominio e tutti i sottodomini (*.contoso.com)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>ExternalAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>L'indirizzo di posta elettronica finale desiderato. È possibile utilizzare i seguenti valori:</p>
<ul>
<li><p>Un indirizzo di posta elettronica singolo se è stato specificato un singolo indirizzo di posta elettronica per <em>InternalAddress</em></p></li>
<li><p>Un singolo dominio o sottodominio per tutti gli altri valori di <em>InternalAddress</em></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ExceptionList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Disponibile soltanto quando si esegue la riscrittura degli indirizzi di posta elettronica in un dominio o sottodominio (*.contoso.com). Specifica uno o più sottodomini da escludere dalla riscrittura degli indirizzi. Racchiudere il valore tra virgolette doppie e separare più valori con la virgola. Ad esempio, <code>&quot;marketing.contoso.com&quot;</code> o <code>&quot;marketing.contoso.com,legal.contoso.com&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundOnly</em></p></td>
<td><p>Facoltativo</p></td>
<td><p><code>False</code> indica che gli indirizzi vengono scritti nella posta in ingresso e in uscita. <code>True</code> indica che gli indirizzi vengono riscritti soltanto nella posta in uscita ed è necessario configurare manualmente l'indirizzo di posta elettronica riscritto come indirizzi proxy per i destinatari interessati.</p>
<p>Il valore predefinito è <code>False</code>, ma è necessario impostarlo su <code>True</code> se<em>InternalAddress</em> contiene un carattere jolly (*.contoso.com).</p>
<p>Il valore del parametro <em>OutboundOnly</em> nel file CSV è <code>True</code> o <code>False</code>, non <code>$True</code> o <code>$False</code>.</p></td>
</tr>
</tbody>
</table>


Ogni riga al di sotto dell'intestazione rappresenta una voce di riscrittura degli indirizzi singola. I valori di ciascuna riga devono trovarsi nello stesso ordine in cui sono elencati i nomi dei parametri nella riga di intestazione. Ciascun valore è separato da una virgola.

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 30 minuti

  - Assicurarsi di aver compreso le implicazioni relative alla riscrittura degli indirizzi. Ad esempio, l'indirizzo di posta elettronica riscritto deve essere univoco all'interno dell'organizzazione di Exchange e potrebbe essere necessario configurare gli indirizzi proxy per i destinatari interessati. Per ulteriori informazioni, vedere [Indirizzo riscrittura su server Trasporto Edge](address-rewriting-on-edge-transport-servers-exchange-2013-help.md) e [Gestire la riscrittura degli indirizzi nei server Trasporto Edge](manage-address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Agente di riscrittura degli indirizzi" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Se si dispone di più server Trasporto Edge, si consiglia di utilizzare le procedure riportate in questo argomento per importare le voci di riscrittura di indirizzi in un solo server Trasporto Edge, quindi clonare la configurazione di tale server Trasporto Edge in altri server Trasporto Edge dell'organizzazione. Per ulteriori informazioni su come clonare un server Trasporto Edge, vedere [Configurazione clonata del server Trasporto Edge](edge-transport-server-cloned-configuration-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passo 1: Creare il file CSV

Quando si crea il file CSV, è necessario considerare i seguenti aspetti:

  - Se si specificano dei valori per i parametri facoltativi del file CSV, ciascuna riga deve comprendere un valore in quella colonna. Se si desidera creare più voci di riscrittura degli indirizzi in cui solo alcune voci dispongono di parametri facoltativi, è necessario separare queste voci in due file CSV separati, quindi importare singolarmente ogni file CSV.

  - Se il file CSV contiene caratteri non ASCII, assicurarsi di salvare il file CSV utilizzando la codifica UTF-8. A seconda dell'applicazione, il salvataggio del file CSV con codifica UTF-8 o Unicode potrebbe risultare più agevole se le impostazioni locali del sistema del computer corrispondono alla lingua utilizzata nel file CSV.

Nel seguente esempio viene mostrato come popolare un file CSV con i parametri facoltativi *ExceptionList* e *OutboundOnly* compresi:

    Name,InternalAddress,ExternalAddress,ExceptionList,OutboundOnly
    "Wingtip UK",*.wingtiptoys.co.uk,tailspintoys.com,"legal.wingtiptoys.co.uk,finance.wingtiptoys.co.uk,support.wingtiptoys.co.uk",True
    "Wingtip USA",*.wingtiptoys.com,tailspintoys.com,"legal.wingtiptoys.com,finance.wingtiptoys.com,support.wingtiptoys.com,corp.wingtiptoys.com",True
    "Wingtip Canada",*.wingtiptoys.ca,tailspintoys.com,"legal.wingtiptoys.ca,finance.wingtiptoys.ca,support.wingtiptoys.ca",True

## Passo 2: Importare il file di importazione CSV

Per importare il file CSV, utilizzare la seguente sintassi:

    Import-Csv <FileNameAndPath> | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

In questo esempio, vengono importate le voci di riscrittura degli indirizzi da C:\\Documenti\\ImportAddressRewriteEntries.csv.

    Import-Csv "C:\My Documents\ImportAddressRewriteEntries.csv" | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

## Come verificare se l'operazione ha avuto esito positivo?

Per controllare di aver importato correttamente le voci di riscrittura degli indirizzi da un file CSV, effettuare una delle seguenti operazioni:

1.  Per visualizzare tutte le voci di riscrittura degli indirizzi, eseguire il comando `Get-AddressRewriteEntry`.

2.  Per visualizzare i dettagli relativi a una voce di riscrittura degli indirizzi specifica, eseguire il comando `Get-AddressRewriteEntry <AddressRewriteIdentity> | Format-List`


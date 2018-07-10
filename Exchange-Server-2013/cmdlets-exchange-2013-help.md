---
title: 'Cmdlet: Exchange 2013 Help'
TOCTitle: Cmdlet
ms:assetid: 1d741dea-1eb8-4909-850f-63d4efaa1a32
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996589(v=EXCHG.150)
ms:contentKeyID: 50480121
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cmdlet

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Un *cmdlet*, pronunciato "command-let", indica la più piccola unità funzionale in Exchange Management Shell. I cmdlet sono simili ai comandi incorporati in altre shell, ad esempio il comando `dir` presente in `cmd.exe`. Analogamente ai comandi più noti, è possibile chiamare i cmdlet direttamente dalla riga di comando in Shell ed eseguirli nel contesto di Shell e non come processo separato.


> [!NOTE]
> Rispetto a Microsoft Exchange Server 2007, sono state apportate modifiche sull'utilizzo interno dei cmdlet da parte di Exchange 2013 a causa dell'utilizzo della funzionalità di gestione remota di°Windows&nbsp;PowerShell. Queste modifiche non influiscono o influiscono poco sull'utilizzo necessario dei cmdlet, ma possono offrire una maggiore flessibilità nella gestione dei server Exchange.



I cmdlet vengono in genere progettati per attività amministrative ripetitive. In Shell vengono fornite diverse centinaia di cmdlet per attività di gestione specifiche di Exchange. Questi cmdlet sono disponibili in aggiunta ai cmdlet di sistema non correlati a Exchange inclusi nella struttura di base di Windows PowerShell. Per informazioni sull'apertura di Exchange°Management Shell, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)).

Tutti i cmdlet di Shell sono presentati come coppie verbo-nome. La coppia di verbo e nome è sempre separata da un trattino (-) senza spazi e i nomi dei cmdlet sono sempre al singolare. I verbi si riferiscono all'azione eseguita dal cmdlet. I nomi si riferiscono all'oggetto su cui il cmdlet esegue l'azione. Ad esempio, nel cmdlet **Get-SystemMessage**, il verbo è **Get** e il nome è **SystemMessage**. Tutti i cmdlet di Shell che gestiscono una specifica funzionalità condividono lo stesso nome. Nella seguente tabella vengono forniti esempi di alcuni verbi disponibili in Shell.


> [!NOTE]
> Se il verbo viene omesso, Shell presuppone per impostazione predefinita il verbo <STRONG>Get</STRONG>. Ad esempio, quando si chiama <STRONG>Mailbox</STRONG>, vengono recuperati gli stessi risultati della chiamata a <STRONG>Get-Mailbox</STRONG>.



### Esempi di verbi in Exchange Management Shell

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Verbo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Disable</strong></p></td>
<td><p>I cmdlet <strong>Disable</strong> consentono di impostare lo stato <code>Enabled</code> dell'oggetto Exchange specificato su <code>$False</code>. In questo modo, si impedisce all'oggetto di elaborare i dati anche se l'oggetto esiste.</p></td>
</tr>
<tr class="even">
<td><p><strong>Enable</strong></p></td>
<td><p>I cmdlet <strong>Enable</strong> consentono di impostare lo stato Abilitato dell'oggetto Exchange specificato su <code>$True</code>. In questo modo, all'oggetto viene consentita l'elaborazione dei dati.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get</strong></p></td>
<td><p>I cmdlet <strong>Get</strong> consentono il recupero di informazioni su uno specifico oggetto Exchange.</p>

> [!NOTE]
> Quando vengono eseguiti, la maggior parte dei cmdlet <STRONG>Get</STRONG> restituiscono solo informazioni di riepilogo. Per richiedere al cmdlet <STRONG>Get</STRONG> di restituire informazioni dettagliate quando si esegue un comando, eseguire il piping del comando al cmdlet <STRONG>Format-List</STRONG>. Per ulteriori informazioni sul comando <STRONG>Format-List</STRONG>, vedere <A href="working-with-command-output-exchange-2013-help.md">Utilizzo dell'output del comando</A>. Per ulteriori informazioni sul pipelining, vedere <A href="https://technet.microsoft.com/it-it/library/aa998260(v=exchg.150)">Pipelining</A>.


</td>
</tr>
<tr class="even">
<td><p><strong>Install</strong></p></td>
<td><p>I cmdlet <strong>Install</strong> consentono di installare un nuovo oggetto o funzionalità in un server Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Move</strong></p></td>
<td><p>I cmdlet <strong>Move</strong> consentono di spostare l'oggetto Exchange specificato da un contenitore o server a un altro.</p></td>
</tr>
<tr class="even">
<td><p><strong>New</strong></p></td>
<td><p>I cmdlet <strong>New</strong> consentono di creare un nuovo oggetto Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Remove</strong></p></td>
<td><p>I cmdlet <strong>Remove</strong> consentono di eliminare l'oggetto Exchange specificato.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set</strong></p></td>
<td><p>I cmdlet <strong>Set</strong> consentono di modificare le proprietà di un oggetto Exchange esistente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Test</strong></p></td>
<td><p>I cmdlet <strong>Test</strong> consentono di verificare componenti di Exchange specifici e forniscono file di registro che è possibile esaminare.</p></td>
</tr>
<tr class="even">
<td><p><strong>Uninstall</strong></p></td>
<td><p>I cmdlet <strong>Uninstall</strong> consentono di rimuovere un oggetto o funzionalità da un server Exchange.</p></td>
</tr>
</tbody>
</table>


Nell'elenco seguente viene fornito un esempio di insieme completo di cmdlet. Questo insieme di cmdlet viene utilizzato per gestire le funzionalità dei messaggi di notifica sullo stato del recapito (DSN, Delivery Status Notification) e dei messaggi con l'indicazione della quota cassette postali raggiunta in Exchange 2013:

  - **Get-SystemMessage**

  - **New-SystemMessage**

  - **Remove-SystemMessage**

  - **Set-SystemMessage**


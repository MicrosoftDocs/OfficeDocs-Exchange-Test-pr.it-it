---
title: 'Limiti per le cartelle pubbliche: Exchange 2013 Help'
TOCTitle: Limiti per le cartelle pubbliche
ms:assetid: 709b075e-9584-484b-bcaa-e781c26497b4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn594582(v=EXCHG.150)
ms:contentKeyID: 61170932
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Limiti per le cartelle pubbliche

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In Exchange Server 2013, le cartelle pubbliche sono state spostate da un'architettura database tradizionale a una di tipo cassetta postale. Tale cambio consente alle cartelle pubbliche di sfruttare la flessibilità di un gruppo disponibilità database (DAG) e altri miglioramenti della cassetta postale effettuati negli anni. Tuttavia, esistono problemi di prestazioni e nuovi limiti che dovrebbero essere presi in considerazione. Nel presente documento vengono fornite alcune line guida di alto livello per opzioni di configurazione disponibili che potrebbero influire su prestazioni e connettività della cartella pubblica.

## Limiti

Nella tabella seguente sono elencati i limiti per le cartelle pubbliche in locale di Exchange Server 2013. A meno che i limiti sono indicati in modo specifico, come consigliato, i valori elencati nella tabella seguente sono limiti supportati per le cartelle pubbliche.


> [!IMPORTANT]
> Per informazioni sulle limiti Exchange Online per Office 365? Vedere <A href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online Limits</A>.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Limiti</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numero totale di cassette postali di cartelle pubbliche</p></td>
<td><p>100</p></td>
<td><p>Sebbene sia possibile creare più di 100 cassette postali di cartelle pubbliche, questa operazione non è supportata. <a href="https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/create-public-folder-mailbox">Creazione di una cassetta postale di cartelle pubbliche</a></p></td>
</tr>
<tr class="even">
<td><p>Totale cartelle pubbliche nella gerarchia</p></td>
<td><p>1,000,000</p></td>
<td><p>Sebbene sia possibile creare più di 1.000.000 delle cartelle pubbliche, non è supportato. Per qualsiasi distribuzione di cartelle pubbliche più o 100.000, si consiglia di leggere <a href="considerations-when-deploying-public-folders-exchange-2013-help.md">Considerazioni sulla distribuzione delle cartelle pubbliche</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Sottocartelle nella cartella principale</p></td>
<td><p>10,000</p></td>
<td><p>Sebbene sia possibile creare più di 1.000 sottocartelle di una cartella principale, si consiglia di non eseguire questa operazione.</p>
<p>Parametro <em>FolderHierarchyChildrenCountReceiveQuota</em> nel cmdlet <a href="https://technet.microsoft.com/it-it/library/bb123981(v=exchg.150)">Set-Mailbox</a>.</p></td>
</tr>
<tr class="even">
<td><p>Profondità di cartella</p></td>
<td><p>300</p></td>
<td><p>La profondità di cartella è il numero di livelli di cartelle nidificate che possono esistere in un unico ramo di una struttura ad albero di cartelle pubbliche. Parametro <em>FolderHierarchyDepthRecieveQuota</em> nel cmdlet <a href="https://technet.microsoft.com/it-it/library/bb123981(v=exchg.150)">Set-Mailbox</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Numero massimo messaggi per cartella pubblica</p></td>
<td><p>1 milioni</p></td>
<td><p>Parametro <em>MailboxMessagesPerFolderCountRecieveQuota</em> nel cmdlet <a href="https://technet.microsoft.com/it-it/library/bb123981(v=exchg.150)">Set-Mailbox</a>.</p></td>
</tr>
<tr class="even">
<td><p>Dimensione massima della singola cartella pubblica</p></td>
<td><p>10 GB</p></td>
<td><p>Questo limite non tiene conto delle sottocartelle di una singola cartella.</p>
<p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">Configurazione delle quote di archiviazione per una cassetta postale</a></p></td>
</tr>
<tr class="odd">
<td><p>Dimensione delle cassette postali delle cartelle pubbliche</p></td>
<td><p>100 GB</p></td>
<td><p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">Configurazione delle quote di archiviazione per una cassetta postale</a></p></td>
</tr>
<tr class="even">
<td><p>Numero di accessi utente per la cassetta postale della cartella pubblica</p></td>
<td><p>2.000 accessi utente contemporanee</p></td>
<td><p>Si consiglia di configurare la gerarchia in modo tale di disporre di non più di 2.000 utente per casetta postale della cartella pubblica. Ad esempio, se si dispone di 20.000 utenti, è necessario disporre di 10 cassette postali di cartelle pubbliche.</p></td>
</tr>
<tr class="odd">
<td><p>Conservazione elemento spostato</p></td>
<td><p>14 giorni consigliati</p></td>
<td><p>Utilizzare il parametro <em>DefaultPublicFolderMovedItemRetention</em> nel cmdlet <strong>Set-OrganizationConfig</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Limite validità</p></td>
<td><p>Si consiglia di impostare lo stesso valore predefinito utilizzato per le cassette postali regolari.</p></td>
<td><p>Queste impostazioni possono essere impostate ai seguenti livelli:</p>
<ul>
<li><p><strong>Livello di organizzazione:</strong> Parametro <em>DefaultPublicFolderAgeLimit</em> nel cmdlet <strong>Set-OrganizationConfig</strong>.</p></li>
<li><p><strong>Livello cassetta postale:</strong> Parametro <em>AgeLimit</em> nel cmdlet <strong>Set-Mailbox</strong>.</p></li>
<li><p><strong>Livello cartella:</strong> Parametro <em>AgeLimit</em> nel cmdlet <strong>Set-PublicFolder</strong>.</p></li>
</ul>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Mantenimento elementi eliminati</p></td>
<td><p>Si consiglia di impostare lo stesso valore predefinito utilizzato per le cassette postali regolari.</p></td>
<td><p>Queste impostazioni possono essere impostate ai seguenti livelli:</p>
<ul>
<li><p><strong>Livello di organizzazione:Parametro</strong> <em>DefaultPublicFolderMovedItemRetention</em> nel cmdlet <strong>Set-OrganizationConfig</strong>.</p></li>
<li><p><strong>Livello cassetta postale:</strong> Parametro <em>RetainDeletedItemsFor</em> nel cmdlet <strong>Set-Mailbox</strong>.</p></li>
<li><p><strong>Livello cartella:</strong> Parametro <em>RetainDeleteItemsFor</em> nel cmdlet <strong>Set-PublicFolder</strong>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Numero massimo di cartelle pubbliche che può essere eseguita la migrazione a Exchange 2013</p></td>
<td><p>500,000</p></td>
<td><p>Questo è il numero massimo di cartelle pubbliche è possibile spostarsi su Exchange 2013 da una versione legacy di Exchange in una singola migrazione. Per informazioni dettagliate sulla migrazione delle cartelle pubbliche, vedere <a href="use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md">Utilizzare la migrazione seriale per spostare le cartelle pubbliche in Exchange 2013 dalle versioni precedenti</a></p></td>
</tr>
</tbody>
</table>


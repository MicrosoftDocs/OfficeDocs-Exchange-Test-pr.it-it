---
title: 'Checklist della distribuzione di protezione: Exchange 2013 Help'
TOCTitle: Checklist della distribuzione di protezione
ms:assetid: 0cbfad59-f503-48a0-8184-6ca999d89e61
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996026(v=EXCHG.150)
ms:contentKeyID: 50480014
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Checklist della distribuzione di protezione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Le funzionalità di Microsoft Exchange Server 2013 sono state concepite allo scopo di migliorare la protezione dell'ambiente di messaggistica. Generalmente, con Exchange 2013 valgono le seguenti condizioni:

  - Gli account utilizzati da Exchange 2013 dispongono delle autorizzazioni minime necessarie per eseguire determinate serie di attività.

  - Per impostazione predefinita, i servizi vengono avviati solo su richiesta.

  - Le autorizzazioni per l'elenco di controllo di accesso (ACL, Access Control List) per gli oggetti di Exchange sono ridotte al minimo.

  - Le autorizzazioni amministrative vengono impostate in base all'ambito di modifica dell'oggetto per il quale è richiesta la modifica.

  - Per impostazione predefinita, tutti i percorsi dei messaggi predefiniti interni sono crittografati.

In questo argomento vengono descritte alcune procedure che si consiglia di applicare per rafforzare l'ambiente di messaggistica prima di installare Microsoft Exchange. Si consiglia di fare riferimento a questo elenco di controllo ogni volta che si installa un nuovo ruolo del server Exchange.

Prima di installare Exchange 2013, completare le procedure descritte di seguito.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Procedura</th>
<th>Operazioni completate</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Eseguire <a href="https://go.microsoft.com/fwlink/p/?linkid=54836">Microsoft Update</a>.</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Eseguire lo strumento di rimozione malware di Microsoft Windows. Lo strumento di rimozione del software dannoso è incluso in Microsoft Update. Per ulteriori informazioni sullo strumento, vedere <a href="http://go.microsoft.com/fwlink/p/?linkid=73452">Strumento di rimozione malware</a>.</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Eseguire <a href="https://go.microsoft.com/fwlink/p/?linkid=16526">Microsoft Baseline Security Analyzer</a>.</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


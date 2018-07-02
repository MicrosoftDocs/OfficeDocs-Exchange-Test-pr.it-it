---
title: 'Autorizzazioni del connettore di ricezione: Exchange 2013 Help'
TOCTitle: Autorizzazioni del connettore di ricezione
ms:assetid: 31af7139-6823-411b-81b3-e42edd83ee6c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673053(v=EXCHG.150)
ms:contentKeyID: 50480369
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzazioni del connettore di ricezione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Nella seguente tabella sono elencati e descritti i diversi tipi di autorizzazione.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Autorizzazione del connettore di ricezione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-SMTP-Submit</p></td>
<td><p>La sessione deve disporre di questa autorizzazione altrimenti non potrà inviare messaggi a questo connettore di ricezione. Se una sessione non dispone di questa autorizzazione, i comandi MAIL FROM e AUTH non verranno eseguiti.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Any-Recipient</p></td>
<td><p>Questa autorizzazione consente alla sessione di inviare messaggi tramite questo connettore. Se l'autorizzazione non viene concessa, questo connettore accetterà solo i messaggi indirizzati a destinatari in domini accettati.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Any-Sender</p></td>
<td><p>Questa autorizzazione consente alla sessione di ignorare il controllo della contraffazione dell'indirizzo del mittente.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Authoritative-Domain-Sender</p></td>
<td><p>Questa autorizzazione consente ai mittenti con indirizzi di posta elettronica in domini autorevoli di stabilire una sessione in questo connettore di ricezione.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Authentication-Flag</p></td>
<td><p>Questa autorizzazione consente ai server Exchange 2003 inviare messaggi da mittenti interni. Exchange 2010 verrà riconosce i messaggi come interno. Il mittente può dichiarare il messaggio come attendibile. Messaggi che accedono al sistema Exchange tramite invii anonimi verranno inoltrati tramite organizzazione Exchange con questo flag in uno stato non attendibile.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Routing</p></td>
<td><p>Questa autorizzazione consente alla sessione di inviare un messaggio con tutte le intestazioni Ricevuto intatte. Se questa autorizzazione non viene concessa, il server rimuoverà tutte le intestazioni ricevute.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Headers-Organization</p></td>
<td><p>Questa autorizzazione consente alla sessione di inviare un messaggio con tutte le intestazioni dell'organizzazione intatte. Tutte le intestazioni dell'organizzazione iniziano con <strong>X-MS-Exchange-Organization-</strong>. Se questa autorizzazione non viene concessa, il server destinatario rimuoverà tutte le intestazioni dell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Forest</p></td>
<td><p>Questa autorizzazione consente alla sessione di inviare un messaggio con tutte le intestazioni della foresta intatte. Tutte le intestazioni della foresta iniziano con <strong>X-MS-Exchange-Forest-</strong>. Se questa autorizzazione non viene concessa, il server destinatario rimuoverà tutte le intestazioni della foresta.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Exch50</p></td>
<td><p>Questa autorizzazione consente alla sessione di inviare un messaggio contenente il comando XEXCH50, Questo comando è necessario per l'interoperabilità con Exchange 2003. Il comando XEXCH50 fornisce dei dati, quali il livello di probabilità di posta indesiderata (SCL) per il messaggio.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Bypass-Message-Size-Limit</p></td>
<td><p>Questa autorizzazione consente alla sessione di inviare un messaggio di dimensioni superiori alla restrizione configurata per il connettore.</p></td>
</tr>
<tr class="odd">
<td><p>Ms-Exch-Bypass-Anti-Spam</p></td>
<td><p>Questa autorizzazione consente alla sessione di ignorare il filtro di protezione da posta indesiderata.</p></td>
</tr>
</tbody>
</table>


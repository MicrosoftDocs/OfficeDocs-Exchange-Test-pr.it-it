---
title: 'Impostazioni predefinite per directory virtuali Exchange: Exchange 2013 Help'
TOCTitle: Impostazioni predefinite per le directory virtuali di Exchange
ms:assetid: d2d89ce6-4721-4737-a325-fba5ad9422e0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg247612(v=EXCHG.150)
ms:contentKeyID: 52063099
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostazioni predefinite per le directory virtuali di Exchange

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Exchange Server 2013 configura automaticamente più directory virtuali IIS (Internet Information Services) durante l'installazione. Questo argomento contiene informazioni relative alle impostazioni di autenticazione IIS e alle impostazioni predefinite di SSL (Secure Sockets Layer) per i server Accesso client e Cassette postali.

## Server Accesso client

Nella tabella seguente sono elencate le impostazioni predefinite in un server Accesso Client autonomo Exchange 2013.

### Impostazioni predefinite di autenticazione IIS e SSL per server Accesso client

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Directory virtuale</th>
<th>Metodo di autenticazione</th>
<th>Impostazioni SSL</th>
<th>Metodo di gestione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sito Web predefinito</p></td>
<td><ul>
<li><p>Anonimo</p></li>
</ul></td>
<td><ul>
<li><p>Obbligatorio</p></li>
</ul></td>
<td><p>Console di gestione IIS</p></td>
</tr>
<tr class="even">
<td><p>aspnet_client</p></td>
<td><ul>
<li><p>Autenticazione anonima</p></li>
</ul></td>
<td><ul>
<li><p>SSL richiesto</p></li>
<li><p>Richiede crittografia a 128 bit</p></li>
</ul></td>
<td><p>Console di gestione IIS</p></td>
</tr>
<tr class="odd">
<td><p>Individuazione automatica</p></td>
<td><ul>
<li><p>Autenticazione anonima</p></li>
<li><p>Autenticazione di base</p></li>
<li><p>Autenticazione di Windows</p></li>
</ul></td>
<td><ul>
<li><p>SSL richiesto</p></li>
<li><p>Richiede crittografia a 128 bit</p></li>
</ul></td>
<td><p>Exchange Management Shell (Shell)</p></td>
</tr>
<tr class="even">
<td><p>ECP</p></td>
<td><ul>
<li><p>Autenticazione anonima</p></li>
<li><p>Autenticazione di base</p></li>
</ul></td>
<td><ul>
<li><p>SSL richiesto</p></li>
<li><p>Richiede crittografia a 128 bit</p></li>
</ul></td>
<td><p>Interfaccia di amministrazione di Exchange (EAC) o Shell</p></td>
</tr>
<tr class="odd">
<td><p>EWS</p></td>
<td><ul>
<li><p>Autenticazione anonima</p></li>
<li><p>Autenticazione di Windows</p></li>
</ul></td>
<td><ul>
<li><p>SSL richiesto</p></li>
<li><p>Richiede crittografia a 128 bit</p></li>
</ul></td>
<td><p>Shell</p></td>
</tr>
<tr class="even">
<td><p>Microsoft-Server-ActiveSync</p></td>
<td><ul>
<li><p>Autenticazione di base</p></li>
</ul></td>
<td><ul>
<li><p>SSL richiesto</p></li>
<li><p>Richiede crittografia a 128 bit</p></li>
</ul></td>
<td><p>EAC o Shell</p></td>
</tr>
<tr class="odd">
<td><p>OAB</p></td>
<td><ul>
<li><p>Autenticazione di Windows</p></li>
</ul></td>
<td><ul>
<li><p>Non richiesto</p></li>
</ul></td>
<td><p>EAC o Shell</p></td>
</tr>
<tr class="even">
<td><p>owa</p></td>
<td><ul>
<li><p>Autenticazione di base</p></li>
</ul></td>
<td><ul>
<li><p>SSL richiesto</p></li>
<li><p>Richiede crittografia a 128 bit</p></li>
</ul></td>
<td><p>EAC o Shell</p></td>
</tr>
<tr class="odd">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>Autenticazione anonima</p></li>
</ul></td>
<td><ul>
<li><p>Non richiesto</p></li>
</ul></td>
<td><p>Shell</p></td>
</tr>
<tr class="even">
<td><p>RPC</p></td>
<td><ul>
<li><p>Autenticazione di base</p></li>
<li><p>Autenticazione di Windows</p></li>
</ul></td>
<td><ul>
<li><p>SSL richiesto</p></li>
<li><p>Richiede crittografia a 128 bit</p></li>
</ul></td>
<td><p>Shell</p></td>
</tr>
<tr class="odd">
<td><p>RpcWithCert</p></td>
<td><p>Per impostazione predefinita, tutti i metodi di autenticazione sono disabilitati.</p></td>
<td><ul>
<li><p>Obbligatorio</p></li>
</ul></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Server Cassette postali

Nella tabella seguente sono elencate le impostazioni predefinite in un server cassette postali autonomo Exchange 2013.

### Impostazioni predefinite di autenticazione IIS e SSL per server Cassette postali

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Directory virtuale</th>
<th>Metodo di autenticazione</th>
<th>Impostazioni SSL</th>
<th>Metodo di gestione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sito Web predefinito</p></td>
<td><ul>
<li><p>Autenticazione anonima</p></li>
</ul></td>
<td><ul>
<li><p>SSL richiesto</p></li>
<li><p>Richiede crittografia a 128 bit</p></li>
</ul></td>
<td><p>La directory virtuale non può essere configurata dall'utente.</p></td>
</tr>
<tr class="even">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>Autenticazione anonima</p></li>
</ul></td>
<td><ul>
<li><p>Non richiesto</p></li>
</ul></td>
<td><p>Shell</p></td>
</tr>
</tbody>
</table>


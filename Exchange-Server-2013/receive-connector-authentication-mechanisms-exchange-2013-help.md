---
title: 'Meccanismi di autenticazione connettore di ricezione: Exchange 2013 Help'
TOCTitle: Meccanismi di autenticazione connettore di ricezione
ms:assetid: 926424e1-83e3-4c4b-b2dd-bf814d81e877
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657472(v=EXCHG.150)
ms:contentKeyID: 50481182
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Meccanismi di autenticazione connettore di ricezione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_


I meccanismi di autenticazione connettore di ricezione sono i seguenti:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Meccanismo di autenticazione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nessuna</p></td>
<td><p>Nessuna autenticazione.</p></td>
</tr>
<tr class="even">
<td><p>TLS</p></td>
<td><p>Advertise STARTTLS. Richiede la disponibilità di un certificato del server per offrire TLS.</p></td>
</tr>
<tr class="odd">
<td><p>Integrata</p></td>
<td><p>NTLM e Kerberos (autenticazione integrata Windows ).</p></td>
</tr>
<tr class="even">
<td><p>BasicAuth</p></td>
<td><p>Autenticazione di base. Richiede un accesso autenticato.</p></td>
</tr>
<tr class="odd">
<td><p>BasicAuthRequireTLS</p></td>
<td><p>Autenticazione di base su TLS. Richiede un certificato server.</p></td>
</tr>
<tr class="even">
<td><p>ExchangeServer</p></td>
<td><p>Exchange Autenticazione da server (servizi di protezione generico application programming interface (GSSAPI) e GSSAPI reciproca).</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthoritative</p></td>
<td><p>La connessione viene considerata protetta esternamente utilizzando un meccanismo di sicurezza esterna al Exchange. La connessione sia un'associazione di Internet Protocol security (IPsec) o una rete privata virtuale (VPN). In alternativa, il server potrebbe risiedono in una rete fisicamente controllata attendibile. Il metodo di autenticazione <code>ExternalAuthoritative</code> richiede il gruppo di autorizzazioni <code>ExchangeServers</code> . Questa combinazione del gruppo di sicurezza e metodo di autenticazione consente la risoluzione degli indirizzi di posta elettronica mittente anonimo per i messaggi ricevuti tramite il connettore.</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni sui connettori di ricezione meccanismi di autenticazione, vedere [New-ReceiveConnector](https://technet.microsoft.com/it-it/library/bb125139\(v=exchg.150\)).


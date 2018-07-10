---
title: "Autorità di certificazione radice disponibile nell'elenco locale per le relazioni di trust federative: Exchange 2013 Help"
TOCTitle: Autorità di certificazione radice disponibile nell'elenco locale per le relazioni di trust federative
ms:assetid: d4224bf5-69b3-484c-8a70-4f230d3dbdd9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee332350(v=EXCHG.150)
ms:contentKeyID: 50481755
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorità di certificazione radice disponibile nell'elenco locale per le relazioni di trust federative

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-07-26_

Per stabilire una relazione di trust federativa tra l'organizzazione di Exchange Server 2013 Microsoft e il [sistema di autenticazione di Azure Active Directory](https://go.microsoft.com/fwlink/p/?linkid=135986), è necessario un certificato digitale installato nel server Exchange utilizzato per creare la relazione di trust. Si consiglia utilizzando un certificato autofirmato. Un certificato autofirmato creato e installato automaticamente quando si utilizza la procedura guidata **abilitare trust federativo** in Interfaccia di amministrazione di Exchange (EAC).

Se non si desidera utilizzare il certificato autofirmato consigliato, è necessario richiedere e installare un certificato x. 509 Secure Sockets Layer (SSL) da un'autorità di certificazione (CA) attendibile da Microsoft. Sebbene i certificati rilasciati dalle altre autorità di certificazione possono essere utilizzati anche per stabilire una relazione di trust federativa con il sistema di autenticazione Azure AD, non sono certificati da Microsoft fino alla data attuale.

Nella tabella seguente vengono elencate le autorità di certificazione considerate attualmente attendibili da Microsoft. Le autorità di certificazione sono state testate per l'utilizzo con Exchange 2013.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome descrittivo dell'autorità di certificazione</th>
<th>Rilasciato da</th>
<th>Scopi designati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>Autenticazione del server, autenticazione client</p></td>
</tr>
<tr class="even">
<td><p>Comodo</p></td>
<td><p>Autorità di certificazione Comodo</p></td>
<td><p>Autenticazione del server, autenticazione client</p></td>
</tr>
<tr class="odd">
<td><p>CyberTrust</p></td>
<td><p>Autorità di certificazione radice CyberTrust Baltimora</p></td>
<td><p>Autenticazione del server, autenticazione client</p></td>
</tr>
<tr class="even">
<td><p>Digicert</p></td>
<td><p>Autorità di certificazione radice globale Digicert</p></td>
<td><p>Autenticazione del server, autenticazione client</p></td>
</tr>
<tr class="odd">
<td><p>Convalida estesa con garanzia elevata Digicert</p></td>
<td><p>Autorità di certificazione radice globale Digicert</p></td>
<td><p>Autenticazione del server e autenticazione del client</p></td>
</tr>
<tr class="even">
<td><p>Entrust</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>Autenticazione del server, autenticazione client</p></td>
</tr>
<tr class="odd">
<td><p>Entrust (2048)</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>Autenticazione del server, autenticazione client</p></td>
</tr>
<tr class="even">
<td><p>Equifax</p></td>
<td><p>Equifax Secure Certification Authority</p></td>
<td><p>Autenticazione del server, autenticazione client</p></td>
</tr>
<tr class="odd">
<td><p>GlobalSign</p></td>
<td><p>Autorità di certificazione GlobalSign</p></td>
<td><p>Autenticazione del server e autenticazione del client</p></td>
</tr>
<tr class="even">
<td><p>Go Daddy</p></td>
<td><p>Go Daddy Class 2 Certification Authority</p></td>
<td><p>Autenticazione del server e autenticazione del client</p></td>
</tr>
<tr class="odd">
<td><p>Network Solutions</p></td>
<td><p>Autorità di certificazione Network Solutions</p></td>
<td><p>Autenticazione del server, autenticazione client</p></td>
</tr>
<tr class="even">
<td><p>PositiveSSL</p></td>
<td><p>Autorità di certificazione Comodo</p></td>
<td><p>Autenticazione del server e autenticazione del client</p></td>
</tr>
<tr class="odd">
<td><p>SECOM</p></td>
<td><p>Autorità di certificazione SECOM Trust Systems</p></td>
<td><p>Autenticazione del server e autenticazione del client</p></td>
</tr>
<tr class="even">
<td><p>UTN-UserFirst-Hardware</p></td>
<td><p>Autorità di certificazione Comodo</p></td>
<td><p>Autenticazione del server, autenticazione client</p></td>
</tr>
<tr class="odd">
<td><p>VeriSign</p></td>
<td><p>Autorità di certificazione principale pubblica Verisign Class 3</p></td>
<td><p>Autenticazione del server, autenticazione client</p></td>
</tr>
<tr class="even">
<td><p>VeriSign</p></td>
<td><p>VeriSign Trust Network</p></td>
<td><p>Autenticazione del server e autenticazione del client</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni sui requisiti dei certificati per la federazione, vedere [Federazione](federation-exchange-2013-help.md).


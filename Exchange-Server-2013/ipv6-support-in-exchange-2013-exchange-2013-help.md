---
title: 'Supporto IPv6 in Exchange 2013: Exchange 2013 Help'
TOCTitle: Supporto IPv6 in Exchange 2013
ms:assetid: 33543023-eb9a-4102-b990-84a818a52814
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg144561(v=EXCHG.150)
ms:contentKeyID: 50480384
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supporto IPv6 in Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Internet Protocol versione 6 (IPv6) è la versione più recente del protocollo IP. IPv6 ha lo scopo di colmare molte lacune di IPv4, cioè la precedente versione del protocollo.

In Microsoft Exchange Server 2013, IPv6 è supportato solo quando è installato e abilitato anche IPv4. Se Exchange 2013 viene distribuito in questa configurazione, e la rete supporta IPv4 e IPv6, tutti i server Exchange potranno inviare e ricevere dati da dispositivi, server e client che utilizzano gli indirizzi in formato IPv6.

In questo argomento viene descritta l'assegnazione indirizzi IPv6 in Exchange 2013. Per ulteriori informazioni su IPv6, vedere [IPv6](https://go.microsoft.com/fwlink/p/?linkid=92582).

**Sommario**

IPv6 support in Exchange 2013 components

Enable or disable protocols in the operating system

IPv6 address basics

## Supporto IPv6 nei componenti Exchange 2013

Nella tabella seguente vengono descritti i componenti di Exchange 2013 influenzati da IPv6.

### Componenti Exchange 2013 e IPv6

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Supporto IPv6</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Elenco indirizzi IP consentiti e Elenco indirizzi IP bloccati nell'agente filtro connessioni</p></td>
<td><p>Sì</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Provider elenco indirizzi IP consentiti e Provider elenco indirizzi IP bloccati nell'agente filtro connessioni.</p></td>
<td><p>No</p></td>
<td><p>Attualmente non esiste un protocollo standard di settore ampiamente accettato per la ricerca degli indirizzi IPv6. La maggior parte dei provider di elenchi di indirizzi IP bloccati non supporta gli indirizzi IPv6. Se si consentono connessioni anonime da indirizzi IPv6 sconosciuti su un connettore di ricezione, aumenta il rischio che gli spammer ignorino i provider di elenchi di indirizzi IP bloccati riuscendo a inviare la posta indesiderata nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p>Reputazione mittente in agente di analisi protocollo</p></td>
<td><p>No</p></td>
<td><p>L'agente di analisi protocollo non calcola il livello di reputazione del mittente per i messaggi provenienti dai mittenti IPv6. Per ulteriori informazioni sulla reputazione del mittente, vedere <a href="sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md">Reputazione mittente e agente di analisi protocollo</a>.</p></td>
</tr>
<tr class="even">
<td><p>ID mittente</p></td>
<td><p>Sì</p></td>
<td><p>Per ulteriori informazioni, vedere <a href="sender-id-exchange-2013-help.md">ID mittente</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Connettori di ricezione</p></td>
<td><p>Sì</p></td>
<td><p>Gli indirizzi IPv6 sono accettati per i seguenti componenti:</p>
<ul>
<li><p>Binding di indirizzi IP locali</p></li>
<li><p>Indirizzi IP remoti</p></li>
<li><p>Intervalli di indirizzi IP</p></li>
</ul>
<p>Si sconsiglia la configurazione dei connettori di ricezione per accettare le connessioni anonime dagli indirizzi IPv6 sconosciuti. Se l'organizzazione ha la necessità di ricevere posta da mittenti che utilizzano indirizzi IPv6, creare un connettore di ricezione dedicato che limiti gli indirizzi IP remoti consentiti agli indirizzi IPv6 di questi mittenti.</p>
<p>Per ulteriori informazioni, vedere <a href="receive-connectors-exchange-2013-help.md">Connettori di ricezione</a>.</p></td>
</tr>
<tr class="even">
<td><p>Connettori di invio</p></td>
<td><p>Sì</p></td>
<td><p>Gli indirizzi IPv6 sono accettati per i seguenti componenti:</p>
<ul>
<li><p>Indirizzi IP SmartHost</p></li>
<li><p>Il parametro <em>SourceIPAddress</em> per i connettori di invio configurati sui server Trasporto Edge</p></li>
</ul>

> [!NOTE]
> Se si desidera specificare un indirizzo IPv6 per il parametro <EM>SourceIPAddress</EM>, assicurarsi che i record DNS AAAA e MX appropriati siano configurati correttamente. Questo garantisce il recapito dei messaggi se un server di messaggistica remoto tenta un qualsiasi tipo di test di ricerca inverso nell'indirizzo IPv6 specificato.


<p>Per ulteriori informazioni, vedere <a href="send-connectors-exchange-2013-help.md">Connettori di invio</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Limiti di velocità per i messaggi in arrivo</p></td>
<td><p>Parziale</p></td>
<td><p>I limiti di velocità per i messaggi in ingresso che è possibile impostare su un connettore di ricezione, ad esempio i parametri <em>MaxInboundConnectionPercentagePerSource</em>, <em>MaxInboundConnectionPerSource</em> e <em>TarpitInterval</em> sono validi solo per l'indirizzo IPv6 globale. Gli indirizzi IPv6 di collegamento locale e gli indirizzi IPv6 locali rispetto al sito non sono interessati dai limiti di velocità specificati per i messaggi in ingresso.</p></td>
</tr>
<tr class="even">
<td><p>Messaggistica unificata</p></td>
<td><p>Sì</p></td>
<td><p>Per ulteriori informazioni, vedere <a href="ipv6-support-in-unified-messaging-exchange-2013-help.md">Supporto IPv6 in messaggistica unificata</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Membro del gruppo di disponibilità del database (DAG, Database Availability Group)</p></td>
<td><p>Sì</p></td>
<td><p>Gli indirizzi IPv6 statici sono supportati da Windows Server e dal servizio cluster. Tuttavia, l'utilizzo degli indirizzi IPv6 statici non è conforme alle procedure consigliate. Exchange 2013 non supporta la configurazione degli indirizzi IPv6 statici durante l'installazione.</p>
<p>I cluster di failover supportano il protocollo ISATAP (Intra-site Automatic Tunnel Addressing Protocol). e solo gli indirizzi IPv6 che consentono la registrazione dinamica in DNS. Gli indirizzi di collegamento locale non possono essere utilizzati in un cluster.</p>
<p>Per ulteriori informazioni sui requisiti di rete DAG, vedere la sezione &quot;Requisiti di rete&quot; in <a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">Pianificazione della disponibilità elevata e della resilienza del sito</a>.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Attivare o disattivare i protocolli del sistema operativo

I server Exchange 2013 supportano interamente le reti IPv6. Quindi, se non si sta utilizzando IPv6, non è necessario disattivare IPv6 sui server Exchange.

Per il supporto IPv6 in Exchange 2013 è necessario che IPv4 sia installato e abilitato su tutti i server di Exchange 2013. La disinstallazione di IPv4 dal server Exchange 2013 non è supportata.

Per ulteriori informazioni sul supporto IPv6 in Microsoft Windows, vedere [IPv6 per Microsoft Windows: domande frequenti](https://go.microsoft.com/fwlink/p/?linkid=147465).

Inizio pagina

## Nozioni di base sull'indirizzo IPv6

Un indirizzo IPv6 ha una lunghezza di 128 bit. L'indirizzo viene descritto utilizzando la notazione esadecimale con due punti. La notazione esadecimale con due punti descrive l'indirizzo a 128 bit utilizzando otto numeri esadecimali a 4 cifre di 16 bit separate da due punti (:). Un esempio di indirizzo IPv6 in notazione esadecimale con due punti è 2001:0DB8:0000:0000:02AA:00FF:C0A8:640A.

Per rappresentare un indirizzo IPv6, utilizzare i seguenti metodi:

  - **Eliminazione degli zero iniziali**   È possibile omettere gli zero iniziali in uno degli otto numeri esadecimali a 4 cifre in un indirizzo IPv6.

  - **Compressione del doppio segno di due punti**   È possibile utilizzare il doppio segno di due punti (::) per rappresentare cifre esadecimali a 16 bit contigue che contengono solo zeri. Tali cifre composte interamente da zeri possono trovarsi all'inizio, al centro o alla fine dell'indirizzo IPv6. In un indirizzo IPv6 la compressione del doppio segno di due punti può essere utilizzata solo una volta.

  - **Notazione decimale puntata finale**   È possibile rappresentare gli ultimi 32 bit alla fine di un indirizzo IPv6 nella notazione decimale puntata separando le cifre a 8 bit con un punto (.). La notazione decimale puntata finale è utilizzata di frequente con gli indirizzi compatibili con IPv4.

Nella tabella seguente vengono forniti degli esempi di notazione degli indirizzi IPv6 e dell'equivalente sintassi.

### Notazione e sintassi degli indirizzi IPv6

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Notazione dell'indirizzo IPv6</th>
<th>Sintassi indirizzo IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Indirizzo IPv6 completo</p></td>
<td><p>2001:0DB8:0000:0000:02AA:00FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>Indirizzo IPv6 che utilizza l'eliminazione degli zero iniziali</p></td>
<td><p>2001:DB8:0:0:2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="odd">
<td><p>Indirizzo IPv6 che utilizza la compressione del doppio segno di due punti</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>Indirizzo IPv6 che utilizza la notazione decimale puntata finale</p></td>
<td><p>2001:DB8::2AA:FF:192.168.100.10</p></td>
</tr>
</tbody>
</table>


Gli indirizzi IPv6 possono essere classificati nei seguenti tipi:

  - **Indirizzo unicast**   Il pacchetto viene recapitato a un'unica interfaccia.

  - **Indirizzo multicast**   Il pacchetto viene recapitato a più interfacce.

  - **Indirizzo anycast**   Fra più interfacce, il pacchetto viene recapitato all'interfaccia più vicina. La distanza tra le interfacce è definita dal costo di routing.

Gli indirizzi unicast IPv6 dispongono dei seguenti ambiti possibili:

  - **Collegamento locale**   L'ambito dell'indirizzo IPv6 è la subnet locale. Gli indirizzi IPv6 di collegamento locale sono paragonabili agli indirizzi IPv4 di collegamento locale utilizzati in Automatic Private IP Addressing (APIPA).

  - **Sito locale**   L'ambito dell'indirizzo IPv6 è l'organizzazione locale. Gli indirizzi locali rispetto al sito sono stati definiti obsoleti da RFC 3879 e sostituiti dagli indirizzi locali univoci definiti in RFC 4193. Gli indirizzi IPv6 locali rispetto al sito e gli indirizzi IPv6 locali univoci sono paragonabili agli indirizzi IP privati IPv4.

  - **Globale**   L'ambito dell'indirizzo IPv6 è il mondo intero. Gli indirizzi IPv6 globali sono paragonabili agli indirizzi IP pubblici IPv4.

Nella tabella seguente viene fornito un confronto tra gli elementi IPv4 e gli elementi IPv6.

### Confronto tra gli elementi IPv4 e IPv6

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>IPv4</th>
<th>IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Indirizzo IP privato</p></td>
<td><p>10.0.0.0/8</p>
<p>172.16.0.0/12</p>
<p>192.168.0.0/16</p></td>
<td><p>FD00::/8</p></td>
</tr>
<tr class="even">
<td><p>Indirizzo di collegamento locale</p></td>
<td><p>169.254.0.0/16</p></td>
<td><p>FE80::/64</p></td>
</tr>
<tr class="odd">
<td><p>Indirizzo di loopback</p></td>
<td><p>127.0.0.1</p></td>
<td><p>::1</p></td>
</tr>
<tr class="even">
<td><p>Indirizzo non specificato</p></td>
<td><p>0.0.0.0</p></td>
<td><p>::</p></td>
</tr>
<tr class="odd">
<td><p>Risoluzione dell'indirizzo</p></td>
<td><p>Address Resolution Protocol (ARP)</p></td>
<td><p>Individuazione router adiacenti (Neighbor Discovery, ND)</p></td>
</tr>
<tr class="even">
<td><p>Risoluzione del nome host DNS (Domain Name System)</p></td>
<td><p>Record di indirizzo (record A)</p></td>
<td><p>Record &quot;AAAA&quot; o record &quot;A6&quot;</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni sull'assegnazione indirizzi IPv6, vedere [Tipi di indirizzi IPv6](https://go.microsoft.com/fwlink/p/?linkid=98357).

## Formati di input IPv6 supportati

In Exchange 2013 sono supportati i seguenti formati di input per gli indirizzi IPv6:

  - Un indirizzo IPv6 singolo

  - Un intervallo di indirizzi IPv6

  - Un indirizzo IPv6 con una subnet mask

  - Un indirizzo IPv6 con una subnet mask che utilizza la notazione Classless Interdomain Routing (CIDR)

Nella tabella seguente vengono forniti degli esempi dei formati di input accettabili per gli indirizzi IPv6 in Exchange 2013.

### Esempi di indirizzo IPv6

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo</th>
<th>Esempio di indirizzo IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Indirizzo singolo</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>Intervallo di indirizzi</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A-2001:DB8::2AA:FF:C0A8:6414</p></td>
</tr>
<tr class="odd">
<td><p>Indirizzo con subnet mask</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A(FFFF:FFFF:FFFF:FFFF::)</p></td>
</tr>
<tr class="even">
<td><p>Indirizzo con subnet mask che utilizza la notazione CIDR (Classless Inter-Domain Routing)</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A/64</p></td>
</tr>
</tbody>
</table>


Exchange 2013 supporta i seguenti formati di input:

  - Eliminazione degli zeri iniziali

  - Compressione del doppio segno di due punti

  - Notazione decimale puntata finale

Inizio pagina


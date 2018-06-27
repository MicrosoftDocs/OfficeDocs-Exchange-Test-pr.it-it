---
title: 'Requisiti di sistema di Exchange 2013: Exchange 2013 Help'
TOCTitle: Requisiti di sistema di Exchange 2013
ms:assetid: 1e80857c-b870-4a6d-a0f4-ff7b3a7be037
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996719(v=EXCHG.150)
ms:contentKeyID: 50480137
ms.date: 02/20/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Requisiti di sistema di Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Informazioni sui requisiti di Exchange 2013 da conoscere prima di procedere all'installazione. Ad esempio, verranno fornite informazioni sui requisiti per hardware, rete e sistema operativo.

Prima di installare Microsoft Exchange Server 2013, si consiglia di esaminare questo argomento per assicurarsi che la rete, l'hardware, il software, i client e gli altri elementi soddisfino i requisiti per Exchange 2013. Inoltre, verificare di avere compreso gli scenari di coesistenza supportati per Exchange 2013 e le versioni precedenti di Exchange.

## Scenari di coesistenza supportati

Nella seguente tabella sono riportati gli scenari in cui è supportata la coesistenza tra Exchange 2013 e le versioni precedenti di Exchange.

### Coesistenza di Exchange 2013 e versioni precedenti di Exchange Server

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Versione di Exchange</th>
<th>Coesistenza dell'organizzazione di Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 e versioni precedenti</p></td>
<td><p>Non supportata</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>Supportata con le seguenti versioni minime di Exchange:</p>
<ul>
<li><p>1Aggiornamento cumulativo 10 per Exchange 2007 Service Pack 3 (SP3) su tutti i server Exchange 2007 nell'organizzazione, inclusi i server Trasporto Edge.</p></li>
<li><p>Aggiornamento cumulativo 2 (CU2) o versioni successive di Exchange 2013 su tutti i server Exchange 2013 nell'organizzazione.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Supportata con le seguenti versioni minime di Exchange:</p>
<ul>
<li><p>2 Exchange 2010 SP3 su tutti i server Exchange 2010 nell'organizzazione, inclusi i server Trasporto Edge.</p></li>
<li><p>Exchange 2013 CU2 o versioni successive su tutti i server Exchange 2013 nell'organizzazione.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Organizzazione mista di Exchange 2010 e Exchange 2007</p></td>
<td><p>Supportata con le seguenti versioni minime di Exchange:</p>
<ul>
<li><p>1Aggiornamento cumulativo 10 per Exchange 2007 SP3 su tutti i server Exchange 2007 nell'organizzazione, inclusi i server Trasporto Edge.</p></li>
<li><p>2 Exchange 2010 SP3 su tutti i server Exchange 2010 nell'organizzazione, inclusi i server Trasporto Edge.</p></li>
<li><p>Exchange 2013 CU2 o versioni successive su tutti i server Exchange 2013 nell'organizzazione.</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Se si desidera creare una sottoscrizione di EdgeSync tra un server Trasporto Hub Exchange 2007 e un server Trasporto Edge di Exchange 2013 SP1, è necessario installare l'aggiornamento cumulativo 13 o versioni successive per Exchange 2007 SP3 su server Trasporto Hub Exchange 2007.

2   Se si desidera creare una sottoscrizione di EdgeSync tra un server Trasporto Hub Exchange 2010 e un server Trasporto Edge di Exchange 2013 SP1, è necessario installare l'aggiornamento cumulativo 2010 o versioni successive per Exchange 5 SP3 su server Trasporto Hub Exchange 2010.

## Scenari di distribuzione ibrida supportati

Exchange 2013 supporta le distribuzioni ibride con i tenant di Office 365 aggiornati all'ultima versione di Office 365. Per ulteriori informazioni su specifiche distribuzioni ibride, vedere [Prerequisiti per la distribuzione ibrida](https://technet.microsoft.com/it-it/library/hh534377\(v=exchg.150\)).

## Server di rete e di directory

Nella tabella seguente sono elencati i requisiti per i server di rete e di directory nell'organizzazione Exchange 2013.

**Requisiti del server di directory e di rete per Exchange 2013**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Master schema</p></td>
<td><p>Per impostazione predefinita, il master schema viene eseguito sul primo controller di dominio Active Directory installato in una foresta. Sul master schema deve essere installata una delle seguenti versioni:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard o Datacenter1</p></li>
<li><p>Windows Server 2012 Standard o Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard o Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM o versione successiva</p></li>
<li><p>Windows Server 2008 Standard o Enterprise (32 bit o 64 bit)</p></li>
<li><p>Windows Server 2008 Datacenter RTM o versione successiva</p></li>
<li><p>Windows Server 2003 Standard Edition con Service Pack 2 (SP2) o versione successiva (32 bit o 64 bit)</p></li>
<li><p>Windows Server 2003 Enterprise Edition con SP2 o versione successiva (32 bit o 64 bit)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Server di catalogo globale</p></td>
<td><p>In ogni sito di Active Directory dove si intende installare Exchange 2013, è necessario avere almeno un server di catalogo globale su cui sia in esecuzione uno dei sistemi operativi seguenti:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard o Datacenter1</p></li>
<li><p>Windows Server 2012 Standard o Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard o Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM o versione successiva</p></li>
<li><p>Windows Server 2008 Standard o Enterprise (32 bit o 64 bit)</p></li>
<li><p>Windows Server 2008 Datacenter RTM o versione successiva</p></li>
<li><p>Windows Server 2003 Standard Edition con Service Pack 2 (SP2) o versione successiva (32 bit o 64 bit)</p></li>
<li><p>Windows Server 2003 Enterprise Edition con SP2 o versione successiva (32 bit o 64 bit)</p></li>
</ul>
<p>Per ulteriori informazioni sui server di catalogo globale, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=178996">Catalogo globale</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Controller di dominio</p></td>
<td><p>In ogni sito di Active Directory dove si intende installare Exchange 2013, è necessario avere almeno un controller di dominio scrivibile sia in esecuzione una delle seguenti versioni:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard o Datacenter1</p></li>
<li><p>Windows Server 2012 Standard o Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard o Enterprise SP1 o versione successiva</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM o versione successiva</p></li>
<li><p>Windows Server 2008 Standard o Enterprise SP1 o versione successiva (32 bit o 64 bit)</p></li>
<li><p>Windows Server 2008 Datacenter RTM o versione successiva</p></li>
<li><p>Windows Server 2003 Standard Edition con Service Pack 2 (SP2) o versione successiva (32 bit o 64 bit)</p></li>
<li><p>Windows Server 2003 Enterprise Edition con SP2 o versione successiva (32 bit o 64 bit)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Foresta di Active Directory</p></td>
<td><p>Active Directory deve trovarsi nella modalità di funzionalità della foresta di Windows Server 20032.</p></td>
</tr>
<tr class="odd">
<td><p>Supporto dello spazio dei nomi DNS</p></td>
<td><p>Exchange 2013 supporta i seguenti spazi dei nomi DNS (Domain Name System):</p>
<ul>
<li><p>Contigui</p></li>
<li><p>Non contigui</p></li>
<li><p>Domini a etichetta singola</p></li>
<li><p>Indipendente</p></li>
</ul>
<p>Per ulteriori informazioni sugli spazi dei nomi DNS supportati da Exchange, vedere l'articolo 2269838 della Microsoft Knowledge Base, <a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2269838">Compatibilità di Microsoft Exchange con i domini a etichetta singola, spazi dei nomi disgiunti e spazi dei nomi non contigui</a>.</p></td>
</tr>
<tr class="even">
<td><p>Supporto di IPv6</p></td>
<td><p>In Exchange 2013, IPv6 è supportato solo quando è installato e abilitato anche IPv4. Se Exchange 2013 viene distribuito in questa configurazione e la rete supporta IPv4 e IPv6, tutti i server Exchange potranno inviare e ricevere dati da dispositivi, server e client che utilizzano indirizzi IPv6. Per ulteriori informazioni, vedere <a href="ipv6-support-in-exchange-2013-exchange-2013-help.md">Supporto IPv6 in Exchange 2013</a>.</p></td>
</tr>
</tbody>
</table>


1   R2 Windows Server 2012è supportato solo con Exchange 2013 SP1 o versione successiva.

2   La modalità di funzionalità della foresta di Windows Server 2012 R2 è supportata solo con Exchange 2013 SP1 o versione successiva.

## Architettura del server di directory

L'utilizzo di controller di dominio di Active Directory a 64 bit migliora le prestazioni del servizio directory per Exchange 2013.


> [!NOTE]
> In ambienti con più domini, sui controller di dominio di Windows Server 2008 con la lingua di Active Directory impostata su giapponese, è possibile che i server non ricevano alcuni attributi archiviati su un oggetto durante la replica in ingresso. Per ulteriori informazioni, vedere l'articolo 949189 della Microsoft Knowledge Base, <A href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=949189">Un controller di dominio di Windows Server 2008 configurato con la lingua giapponese potrebbe non applicare gli aggiornamenti agli attributi su un oggetto durante la replica in ingresso</A>.



## Installazione di Exchange 2013 sui server di directory

Per motivi di sicurezza e prestazioni, si consiglia di installare Exchange 2013 solo su server membri e non su server di directory di Active Directory. Tuttavia, non è possibile eseguire DCPromo su un computer su cui è installato Exchange 2013. Una volta installato Exchange 2013, non è possibile cambiarne il ruolo da server membro a server di directory o viceversa.

## Hardware

I requisiti hardware consigliati per i server Exchange 2013 dipendono da diversi fattori, compresi i ruoli del server installati e il carico previsto che verrà inviato ai server.

Per informazioni dettagliate su come valutare e configurare la propria distribuzione, vedere [Suggerimenti relativi a ridimensionamento e configurazione di Exchange 2013](exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md).

Per informazioni sulla distribuzione di Exchange in un ambiente virtualizzato, vedere [Virtualizzazione di Exchange 2013](exchange-2013-virtualization-exchange-2013-help.md).

**Requisiti hardware per Exchange 2013**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Requisito</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Processore</p></td>
<td><ul>
<li><p>Computer basato sull'architettura a 64 bit con processore Intel che supporta l'architettura Intel 64 (in precedenza nota come Intel EM64T)</p></li>
<li><p>Processore AMD che supporta la piattaforma AMD64</p></li>
<li><p>I processori Intel Itanium IA64 non sono supportati</p></li>
</ul></td>
<td><p>Vedere la sezione &quot;Sistema operativo&quot; più avanti in questo argomento per informazioni sui sistemi operativi supportati.</p></td>
</tr>
<tr class="even">
<td><p>Memoria</p></td>
<td><p>Varia a seconda dei ruoli di Exchange installati:</p>
<ul>
<li><p><strong>Cassette postali</strong> 8 GB minimo</p></li>
<li><p><strong>Accesso client</strong> 4 GB minimo</p></li>
<li><p><strong>Cassette postali e accesso client combinati</strong> 8 GB minimo</p></li>
<li><p><strong>Trasporto Edge</strong> almeno 4 GB</p></li>
</ul></td>
<td><p>Nessuno.</p></td>
</tr>
<tr class="odd">
<td><p>Dimensione del file di paging</p></td>
<td><p>È necessario impostare la dimensione massima e minima del file di paging nella RAM fisica e aggiungervi 10 MB. Indicare una dimensione massima di 32778 MB se si utilizzano 32 GB di RAM.</p></td>
<td><p>Per suggerimenti avanzati sul file di paging, vedere la sezione &quot;File di paging&quot; in <a href="exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md">Suggerimenti relativi a ridimensionamento e configurazione di Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Spazio su disco</p></td>
<td><ul>
<li><p>Almeno 30 GB nell'unità in cui viene installato Exchange</p></li>
<li><p>500 MB aggiuntivi di spazio disponibile su disco per ogni Language Pack di messaggistica unificata che si intende installare</p></li>
<li><p>200 MB di spazio disponibile su disco nell'unità di sistema</p></li>
<li><p>Un disco rigido su cui archiviare il database delle code di messaggi con almeno 500 MB di spazio disponibile.</p></li>
</ul></td>
<td><p>Per informazioni approfondite sui suggerimenti di archiviazione, vedere <a href="exchange-2013-storage-configuration-options-exchange-2013-help.md">Opzioni di configurazione di archiviazione di Exchange 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Unità</p></td>
<td><p>Unità DVD-ROM, accessibile localmente o in rete</p></td>
<td><p>Nessuno.</p></td>
</tr>
<tr class="even">
<td><p>Risoluzione dello schermo</p></td>
<td><p>1024 x 768 pixel o superiore</p></td>
<td><p>Nessuno.</p></td>
</tr>
<tr class="odd">
<td><p>Formato file</p></td>
<td><p>Partizioni dei dischi formattate come file system NTFS, applicabili alle seguenti partizioni:</p>
<ul>
<li><p>Partizione di sistema</p></li>
<li><p>Partizioni che archiviano i file binari di Exchange o i file creati dalla registrazione diagnostica di Exchange</p></li>
</ul>
<p>Le partizioni del disco che includono i seguenti tipi di file possono essere formattate come ReFS:</p>
<ul>
<li><p>Partizioni contenenti i file di registro delle transazioni</p></li>
<li><p>Partizioni contenenti i file di database</p></li>
<li><p>Partizioni contenenti file di indicizzazione del contenuto</p></li>
</ul></td>
<td><p>Nessuno.</p></td>
</tr>
</tbody>
</table>


## Sistema operativo

Nella tabella seguente sono elencati i sistemi operativi supportati per Exchange 2013.


> [!IMPORTANT]
> Microsoft non supporta l'installazione di Exchange 2013 su un computer in esecuzione in modalità Windows Server Core. Nel computer deve essere eseguita l'installazione completa di Windows Server. Se si desidera installare Exchange 2013 su un computer in esecuzione in modalità Windows Server Core, è necessario convertire il server in un'installazione completa di Windows Server effettuando una delle seguenti operazioni: 
> <UL>
> <LI>
> <P><STRONG>Windows Server 2008 R2</STRONG>&nbsp;&nbsp;&nbsp;Reinstallare Windows Server e selezionare l'opzione <STRONG>Installazione completa</STRONG>.</P>
> <LI>
> <P><STRONG>Windows Server 2012 R2</STRONG> o <STRONG>Windows Server 2012</STRONG>&nbsp;&nbsp;&nbsp;Convertire il server con modalità Windows Server Core in un'installazione completa eseguendo il comando riportato di seguito.</P><PRE><CODE>Install-WindowsFeature Server-Gui-Mgmt-Infra, Server-Gui-Shell -Restart</CODE></PRE></LI></UL>



**Sistemi operativi supportati per Exchange 2013**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ruoli server Cassette postali, Accesso client e Trasporto Hub</p></td>
<td><p>Una delle versioni seguenti:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard o Datacenter1</p></li>
<li><p>Windows Server 2012 Standard o Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard con Service Pack 1 (SP1)</p></li>
<li><p>Windows Server 2008 R2 Enterprise con Service Pack 1 (SP1)</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM o versione successiva</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Strumenti di gestione</p></td>
<td><p>Una delle versioni seguenti:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard o Datacenter1</p></li>
<li><p>Windows Server 2012 Standard o Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard con SP1</p></li>
<li><p>Windows Server 2008 R2 Enterprise con SP1</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM o versione successiva</p></li>
<li><p>Edizione a 64 bit di Windows 8.12</p></li>
<li><p>Edizione a 64 bit di Windows 8</p></li>
<li><p>Edizione a 64 bit di Windows 7 con Service Pack 1</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Windows Server 2012 R2 è supportato solo con Exchange 2013 SP1 o versione successiva.

2   Windows 8.1 è supportato solo con Exchange 2013 SP1 o versione successiva.

**Versioni supportate di Windows Management Framework per Exchange 2013**

Exchange 2013 supporta solo la versione di Windows Management Framework incorporata nella release di Windows la cui installazione su Exchange è in corso. Non installare versioni di Windows Management Framework rese disponibili come download autonomi nei server che eseguono Exchange.

## .NET Framework

Si consiglia di utilizzare l'ultima versione di .NET Framework, compatibile con la versione di Exchange in fase di installazione.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Versione di Exchange</th>
<th>.NET Framework 4.7.1</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU19</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU16 - CU18</p></td>
<td><p></p></td>
<td><p> X</p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## Client supportati

Exchange 2013 supporta le seguenti versioni di Outlook ed Entourage per Mac:

  - Outlook 2016

  - Outlook 2013

  - Outlook 2010

  - Outlook 2007

  - Entourage 2008 per Mac, Web Services Edition

  - Outlook per Mac per Office 365

  - Outlook per Mac 2011

Per un elenco delle versioni di Outlook supportate da Exchange, vedere [Aggiornamenti di Outlook](https://go.microsoft.com/fwlink/p/?linkid=513459).


> [!IMPORTANT]
> Si consiglia di installare i service pack e gli aggiornamenti più recenti per offrire agli utenti la migliore esperienza possibile in caso di connessione a Exchange.



I client Outlook precedenti a Outlook 2007 non sono supportati. I client di posta elettronica su sistemi operativi Mac che richiedono DAV, ad esempio Entourage 2008 per Mac RTM ed Entourage 2004, non sono supportati.

Outlook Web App supporta numerosi browser su vari sistemi operativi e dispositivi. Per informazioni dettagliate, vedere [Novità per Outlook Web App in Exchange 2013](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md).


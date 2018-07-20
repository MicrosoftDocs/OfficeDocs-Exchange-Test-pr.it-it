---
title: 'Note di configurazione per i gateway VoIP, IP PBX e PBX supportati: Exchange 2013 Help'
TOCTitle: Note di configurazione per i gateway VoIP, IP PBX e PBX supportati
ms:assetid: 1583674f-5a57-45fd-8125-087d1624e686
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee681657(v=EXCHG.150)
ms:contentKeyID: 50555544
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Note di configurazione per i gateway VoIP, IP PBX e PBX supportati

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

In questa pagina vengono forniti collegamenti alle note di configurazione che sono stati creati e testate da Microsoft o un partner di gateway VoIP. Quando si Microsoft o un partner consente di distribuire la messaggistica unificata con un nuovo gateway VoIP e PBX o IP PBX configurazione, i prerequisiti e le impostazioni di configurazione sono documentate. Queste informazioni vengono utilizzate per creare una nota di configurazione.

Ogni configurazione PBX sono contenute informazioni su come distribuire la messaggistica unificata con una configurazione di telefonia specifico e include il produttore, modello e versione del firmware per i gateway VoIP, IP PBX o PBX. Inoltre, ciascuna configurazione PBX include altre informazioni, ad esempio:

  - Collaboratori in nota sulla configurazione di creazione e modifica.

  - Prerequisiti dettagliati, inclusi i seguenti:
    
      - Caratteristiche che devono essere abilitata o disabilitata al PBX.
    
      - Hardware specializzata che deve essere installato.
    
      - Indica se un gateway VoIP è obbligatorio.
    
      - Caratteristiche che devono essere presente sul gateway VoIP, se necessario.
    
      - Requisiti specifici di cablaggio tra un gateway IP e un PBX.
    
      - Un elenco di funzionalità di messaggistica unificata che potrebbero non essere disponibili con una configurazione di telefonia specificato.

Per ulteriori informazioni su Microsoft Unified Communications Open Interoperability Program per l'infrastruttura di telefonia aziendale, tra cui la ricerca e di partecipare al programma possono utilizzare completo gateway PSTN SIP e IP PBX e i fornitori dell'infrastruttura di telefonia processo, vedere [Microsoft Unified Communications Open Interoperability Program](https://go.microsoft.com/fwlink/p/?linkid=132071).

## Note di configurazione PBX, IP PBX e gateway VoIP

Microsoft funzioni correttamente con i partner gateway VoIP, AudioCodes e Dialogic, da aggiungere all'elenco dei sistemi PBX che vengono sottoposte a test. Dal momento che attualmente stiamo provando molte combinazioni di componenti di telefonia, in questo argomento viene aggiornato frequentemente. Controllare nuovamente se non è possibile individuare la nota di configurazione appropriato per la distribuzione.

Le note di configurazione seguenti sono disponibili:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Aastra</p></li>
<li><p>Alcatel</p></li>
<li><p>Avaya</p></li>
<li><p>Cisco</p></li>
<li><p>Inter-Tel</p></li>
<li><p>Intecom</p></li>
<li><p>Mitel</p></li>
<li><p>NEC</p></li>
</ul></td>
<td><ul>
<li><p>NeXspan</p></li>
<li><p>Nortel</p></li>
<li><p>Panasonic</p></li>
<li><p>Rolm</p></li>
<li><p>ShoreTel</p></li>
<li><p>Siemens</p></li>
<li><p>Sonus</p></li>
<li><p>Tadiran</p></li>
<li><p>Toshiba</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Aastra


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra MD110 (in precedenza Ericsson MD110)</p></td>
<td><p>MX1 TSW R2A (ovvero BC13)</p></td>
<td><p>Analogico – protocollo MD110 seriale</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="even">
<td><p>Aastra MD110 (in precedenza Ericsson MD110)</p></td>
<td><p>MX1 TSW R2A (ovvero BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>Aastra MX-UNO</p></td>
<td><p>4.0</p></td>
<td><p>Connessione SIP diretta</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Aastra</p></td>
<td><p><a href="http://www.aastra.com/cps/rde/aareddownload?file_id=4384-14746-_p06_xml%26dsproject=aastra%26mtype=pdf">Download</a></p></td>
</tr>
</tbody>
</table>


## Alcatel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello di PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OmniPCX 4400</p></td>
<td><p>R4.2-d2.304-4-h-il-c6s2</p></td>
<td><p>Analogico-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
</tbody>
</table>


## Avaya


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello di PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aura</p></td>
<td><p>Gestione di comunicazioni 5.2.1 con Service Pack 5</p>
<p>Gestione delle sessioni 5.2.</p></td>
<td><p>Connessione SIP diretta</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/downloads/">Download</a></p></td>
</tr>
<tr class="even">
<td><p>CS 2100</p></td>
<td><p>CS 2100 SE13</p></td>
<td><p>Connessione SIP diretta</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/css/p8/documents/100149819">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R009i.05.122.4</p></td>
<td><p>Emulazione Set digitale (DNI7434)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="even">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>Analogico-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 Autorità di certificazione-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>Merlino Magix</p></td>
<td><p>Versione 1.5 versione 6.0</p></td>
<td><p>Analogico-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>Gestione di comunicazione G3xV11 1.3</p></td>
<td><p>Analogico-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>T1 Autorità di certificazione-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>Gestione di comunicazione 3.0 (R013x00.1.346.0)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>S8500</p></td>
<td><p>Gestione di comunicazione 3.0 (R013x00.1.346.0)</p></td>
<td><p>T1 Autorità di certificazione-In-Band DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>Gestione di comunicazione 3.0 (R013x00.1.346.0)</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>S8700</p></td>
<td><p>R011x.02.0.110.4</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
</tbody>
</table>


## Cisco


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione chiamate Cisco 4. x</p></td>
<td><p>4.x</p></td>
<td><p>IP-to-IP</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>Gestione chiamate Cisco 5.1</p></td>
<td><p>5.1.0.9921-12</p></td>
<td><p>Connessione SIP diretta</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco Unified Communications Manager 6.0 e 6.1</p></td>
<td><p>6.x</p></td>
<td><p>Connessione SIP diretta</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">Download</a></p></td>
</tr>
<tr class="even">
<td><p>Cisco Unified Communications Manager 7.0</p></td>
<td><p>7.0.2.20000-5</p></td>
<td><p>Connessione SIP diretta</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=196361">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco Unified Communications Manager 8.0</p></td>
<td><p>8.0.3.20000-5</p></td>
<td><p>Connessione SIP diretta</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=213007">Download</a></p></td>
</tr>
</tbody>
</table>


## Inter-Tel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5000</p></td>
<td><p>Inter-Tel 5000 v 2.1</p></td>
<td><p>T1 Autorità di certificazione-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>Axxess</p></td>
<td><p>Axxess V9.0</p></td>
<td><p>T1 Autorità di certificazione-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
</tbody>
</table>


## Intecom


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PointSpan M6880</p></td>
<td><p>40PS3.5.K.2</p></td>
<td><p>T1 AUTORITÀ DI CERTIFICAZIONE - SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
</tbody>
</table>


## Mitel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>SX2000</p></td>
<td><p>5.0.24</p></td>
<td><p>Emulazione Set digitale (DNISS430)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008MTLDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
</tbody>
</table>


## NEC


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Electra Elite 192</p></td>
<td><p>SP034V4.5</p></td>
<td><p>Analogico-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IMX</p></td>
<td><p>versione 7400</p></td>
<td><p>T1 Autorità di certificazione - MCI seriale</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IMX &amp; IPX</p></td>
<td><p>versione 7400</p></td>
<td><p>Insieme digitale emulazione (DNIDtermIII)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver R18.06.24.000</p></td>
<td><p>T1 Autorità di certificazione – MCI seriale</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IPX</p></td>
<td><p>R18.06.24.000 ver.</p></td>
<td><p>Analogico – MCI seriale</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver.17 Rel.03.46.001</p></td>
<td><p>T1 Q. SIG – MCI seriale</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
</tbody>
</table>


## NeXspan


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>S</p></td>
<td><p>Versione RMS1 R1.3 E1TA</p></td>
<td><p>Analogico-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
</tbody>
</table>


## Nortel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CS1000</p></td>
<td><p>3.0 &amp; 4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>Meridiano 81C</p></td>
<td><p>4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>Meridiano 81C</p></td>
<td><p>4.5</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>Versione 25</p></td>
<td><p>Insieme digitali emulazione (DNI2616)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>Option11c</p></td>
<td><p>Versione 25</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>Versione 25</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>CS - 1000M (successione)</p></td>
<td><p>Versione 25.40</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
</tbody>
</table>


## Panasonic


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KX TDA200</p></td>
<td><p>001-001</p></td>
<td><p>Analogico - In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>KX TDA200</p></td>
<td><p>3</p></td>
<td><p>Analogico - In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>KX TES824</p></td>
<td><p>2.0.2</p></td>
<td><p>Analogico - In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
</tbody>
</table>


## Rolm


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9751</p></td>
<td><p>9005</p></td>
<td><p>Emulazione Set digitale (DNIRP400)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008RLMDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
</tbody>
</table>


## ShoreTel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IP Telephony System</p></td>
<td><p>6.1</p></td>
<td><p>Analogico – SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>IP Telephony System</p></td>
<td><p>7.5</p></td>
<td><p>Analogico – SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
</tbody>
</table>


## Siemens


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HiCom 150E</p></td>
<td><p>2.2 Rel.</p></td>
<td><p>Analogico-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>QSIG BRI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>HiCom 300</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>Insieme digitale emulazione (DNIOptiset)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="even">
<td><p>HiCom 300</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>T1 Autorità di certificazione - In-Band DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 3550</p></td>
<td><p>3 Rel.</p></td>
<td><p>Analogico-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>SMP4 SMR5 ver 3.0</p></td>
<td><p>Analogico-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>QSIG BRI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>SMP4 SMR5 ver 3.0</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>Versione 2.0 SMR9 SMP0</p></td>
<td><p>Analogico - In-Band DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>Versione 2.0 SMR9 SMP0</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
</tbody>
</table>


## Sonus


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
<th>Modello di gateway VoIP</th>
<th>Versione software gateway VoIP</th>
<th>Protocolli supportati</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SBC 1000/2000</p></td>
<td><p>2.2.1 o versione successiva</p></td>
<td><ul>
<li><p>TDM segnali (ISDN): AT &amp; T 4ESS/5ESS, servizio di gestione Directory Nortel 100, in Euro ISDN (ETSI 300 102), QSIG, InsNet NTT (Giappone), ANSI National ISDN-2 (NI-2)</p></li>
<li><p>Segnalazione TDM (CAS): T1 CAS (E &amp; M, avvio Loop); E1 AUTORITÀ DI CERTIFICAZIONE (R2)</p></li>
</ul></td>
<td><p>Sonus</p></td>
<td><p><a href="http://www.sonus.net/sites/default/files/sonussbc1k2kconfigo365.pdf">Download</a></p></td>
</tr>
</tbody>
</table>


## Tadiran


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Flexicom corallo</p></td>
<td><p>14.67.49</p></td>
<td><p>Analogico-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>Flexicom corallo</p></td>
<td><p>14.67.49</p></td>
<td><p>QSIG BRI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>Flexicom corallo</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 Autorità di certificazione - In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>Flexicom corallo</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>IPX corallo</p></td>
<td><p>14.67.49</p></td>
<td><p>Analogico-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP 11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>IPX corallo</p></td>
<td><p>14.67.49</p></td>
<td><p>QSIG BRI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="odd">
<td><p>IPX corallo</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 Autorità di certificazione-In-Band DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
<tr class="even">
<td><p>IPX corallo</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Download</a></p></td>
</tr>
</tbody>
</table>


## Toshiba


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello PBX</th>
<th>Versione software PBX</th>
<th>Protocollo</th>
<th>Fornitori di gateway</th>
<th>Modello di gateway</th>
<th>Autore di configurazione</th>
<th>Download file di configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>Analogico – SMDI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
<tr class="even">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>Analogico-In-Band DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Download</a></p></td>
</tr>
</tbody>
</table>


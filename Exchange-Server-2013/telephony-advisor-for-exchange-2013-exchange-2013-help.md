---
title: 'Sistema di telefonia per Exchange 2013: Exchange 2013 Help'
TOCTitle: Sistema di telefonia per Exchange 2013
ms:assetid: e9f760f2-5901-4ed2-95a5-724555cc700e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee364753(v=EXCHG.150)
ms:contentKeyID: 50555705
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Sistema di telefonia per Exchange 2013

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2017-07-25_

La messaggistica unificata richiede l'integrazione di Microsoft Exchange con il sistema di telefonia esistente per la propria organizzazione. Una distribuzione corretta richiede un'attenta analisi dell'infrastruttura telefonica esistente e l'esecuzione della procedura di pianificazione corretta per distribuire la messaggistica unificata.

La fase di pianificazione può rivelarsi una sfida notevole per gli amministratori di Exchange che hanno un'esperienza minima o inesistente con una rete telefonica. Per risolvere queste problematiche, vedere Resources to Help with Your UM Deployment più avanti in questo argomento.

Per visualizzare i gateway VoIP supportati per la messaggistica unificata, se il proprio sistema PBX è supportato utilizzando un modello o un produttore di gateway VoIP specifico, se il sistema IP PBX è supportato tramite una connessione SIP diretta o per vedere i session border controller (SBC) per la messaggistica unificata di Exchange Online, fare clic su uno dei seguenti collegamenti:

  - Supported VoIP gateways

  - Supported PBXs when using an AudioCodes VoIP gateway

  - Supported PBXs when using a dialogic VoIP gateway
    
      - PBXs supported when using a DMG1000 series Media Gateway
    
      - PBXs supported when using a DMG 2000 series Media Gateway
    
      - PBXs supported when using a DMG3000 series Media Gateway

  - Supported IP PBXs

  - Supported IP PBXs when using SIP media gateways

  - Exchange Unified Messaging, Office Communications Server 2007 R2, and Microsoft Lync Server

## Risorse per facilitare la distribuzione della messaggistica unificata

È difficile creare linee guida per la distribuzione delle reti di telefonia. Sono piuttosto diverse tra loro poiché possono includere gateway VoIP, sistemi IP PBX e PBX con impostazioni di configurazione, firmware e requisiti differenti. Tuttavia, sono disponibili diverse risorse per facilitare la distribuzione corretta della Messaggistica unificata:

  - **Esperti di messaggistica unificata** Esperti di messaggistica unificata sono integratori di sistemi che hanno ricevuto formazione tecnica sulla messaggistica unificata di Exchange eseguito dal team di progettazione Exchange. Per garantire una transizione senza problemi a messaggistica unificata da sistemi di segreteria telefonica legacy, Microsoft è consigliabile che tutti i clienti coinvolgere uno specialista di messaggistica unificata. Per informazioni sui contatti, visitare il sito [Microsoft Exchange Server 2013 Unified Messaging (UM) specialisti](http://go.microsoft.com/fwlink/p/?linkid=262708) o [Individuare Microsoft per la messaggistica unificata](https://go.microsoft.com/fwlink/p/?linkid=261951).

  - **Note sulla configurazione per gateway VoIP, IP PBX e PBX supportati**   Tali note di configurazione contengono le impostazioni e altre informazioni molto utili quando si configurano i gateway VoIP, gli IP PBX e i PBX per la comunicazione con i server Messaggistica unificata presenti nella rete. Per ulteriori informazioni, vedere [Note di configurazione per i gateway VoIP, IP PBX e PBX supportati](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md).

  - **Note di configurazione per gli SBC (Session Border Controllers) supportati**   Queste note di configurazione contengono le impostazioni e altre informazioni utili per configurare gli SBC (Session Border Controllers) per la comunicazione dei server di messaggistica unificata in distribuzione ibride ed Exchange Online della messaggistica unificata. Per ulteriori informazioni, vedere [Note di configurazione per session border controller supportati](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md).
    

    > [!NOTE]
    > Supporto in linea di messaggistica unificata di Exchange per i sistemi PBX di terze parti tramite connessioni dirette dal cliente utilizzati SBCs terminerà in 2018 luglio. Vedere blog del team di Exchange <A href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">cessazione del supporto per i session border controller in Exchange Online della messaggistica unificata</A> per ulteriori informazioni.



Prima di rivolgersi a uno specialista della messaggistica unificata, è necessario essere in grado di rispondere alle principali domande che quest'ultimo porrà. Se si conoscono le risposte alle domande riportate di seguito, la conversazione con lo specialista sarà più produttiva:

  - Quanti utenti di telefonia, del sistema di caselle vocali o di entrambi i tipi di sistema sono presenti nell'organizzazione?

  - A quanti utenti si intende fornire la messaggistica unificata?

  - Quale sistema o sistemi PBX si intendono utilizzare per l'integrazione con la messaggistica unificata?

  - Quanti sistemi PBX comprende l'organizzazione? Specificare fornitore, tipo (basato su circuito o su IP), modello e versione del firmware.

  - I sistemi PBX sono collegati in rete? Sono centralizzati o si trovano in più sedi?

  - Quale sistema o sistemi di caselle vocali sono attualmente utilizzate dall'organizzazione? Specificare il fornitore, il tipo, il modello e la versione del firmware.

  - Come sono integrati i sistemi di caselle vocali nei sistemi PBX (analogico, T1/E1, PRI, emulazione digitale, VoIP, altro)?

  - Sono attualmente in uso connessioni di rete vocali?

  - Quale tipo di sistema fax sono utilizzati nell'organizzazione? Il sistema o i sistemi fax supportano il routing dei fax in ingresso a Exchange?

  - L'organizzazione utilizza gli operatori automatici?

  - È necessario un supporto per utenti solo telefonici, ovvero utenti che non hanno accesso alla posta elettronica?

## Gateway VoIP supportati

L'integrazione della messaggistica unificata con i sistemi PBX richiede l'utilizzo di uno o più gateway VoIP per convertire i protocolli a commutazione di circuito utilizzati da sistemi PBX basati su TDM a protocolli basati su IP a commutazione di pacchetto utilizzati dalla messaggistica unificata. Fornitori di gateway VoIP con diversi modelli di gateway VoIP e multimediali sono stati verificati e sono supportati per la messaggistica unificata.

La verifica di interoperabilità della messaggistica unificata con gateway VoIP, IP PBX e SBC è ora integrata con il programma Microsoft Unified Communications Open Interoperability Program. Per ulteriori informazioni, vedere [Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/p/?linkid=140722).

Il programma di qualificazione per gateway VoIP, IP PBX e gateway VoIP avanzati [Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/p/?linkid=140722) garantisce agli utenti un'installazione e un supporto semplificati quando si utilizzano gateway di telefonia e IP PBX qualificati con il software Microsoft Unified Communications. Solo i prodotti che superano una serie di test rigorosi e sono conformi alle specifiche dei test ricevono la qualificazione.

Per informazioni dettagliate sulla configurazione di gateway, IP PBX, PBX e SBC supportati, vedere una delle seguenti risorse:

  - [Note di configurazione per i gateway VoIP, IP PBX e PBX supportati](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Note di configurazione per session border controller supportati](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

L'interoperabilità è stata verificata per i seguenti fornitori di gateway VoIP:

  - AudioCodes

  - Dialogic

  - Nella seguente tabella sono indicati i fornitori del gateway VoIP, i modelli gateway VoIP e i protocolli supportati da ogni modello.

### Gateway VoIP supportati per la messaggistica unificata

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fornitore</th>
<th>Modello</th>
<th>Protocolli supportati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>MediaPack 114/8 FXO</p></td>
<td><ul>
<li><p>Analogico con DTMF In-Band</p></li>
<li><p>Analogico con SMDI</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><ul>
<li><p>Analogico con DTMF In-Band</p></li>
<li><p>Analogico con SMDI</p></li>
<li><p>BRI Q.SIG</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP-to-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><ul>
<li><p>T1/E1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP-to-IP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG1000PBXDNIW</p></td>
<td><p>Emulazione digitale</p></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG1000LSW</p></td>
<td><ul>
<li><p>Analogico con DTMF In-Band</p></li>
<li><p>Analogico con SMDI</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG2000</p></td>
<td><ul>
<li><p>T1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><ul>
<li><p>BRI Q.SIG</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NET</p></td>
<td><p>VX1200</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Sonus</p></td>
<td><p>SBC 1000/2000 2.2.1 o versione successiva</p></td>
<td><ul>
<li><p>TDM segnali (ISDN): AT &amp; T 4ESS/5ESS, servizio di gestione directory Nortel 100, in Euro ISDN (ETSI 300 102), QSIG, InsNet NTT (Giappone), ANSI National ISDN-2 (NI-2)</p></li>
<li><p>Segnalazione TDM (CAS): T1 CAS (E &amp; M, avvio Loop); E1 AUTORITÀ DI CERTIFICAZIONE (R2)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Quintum</p></td>
<td><p>Serie Tenor DX</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Sistemi PBX supportati quando si utilizza un gateway VoIP AudioCodes

Nella seguente tabella sono presentati i sistemi PBX supportati se si utilizzano gateway VoIP AudioCodes, inclusi MediaPack-114 FXO, MediaPack-118 FXO e Mediant 2000.

### Sistemi PBX supportati con un gateway VoIP AudioCodes

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Produttore del sistema PBX</th>
<th>Tipo/modello del sistema PBX</th>
<th>Modello AudioCodes &quot;x&quot; - sostituire con 4 o 8 se necessario; &quot;y&quot; - sostituire con 1, 2, 4, 8 o 16 se necessario</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>OmniPCX 4400</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Aastra</p></td>
<td><p>M1000, M2000</p></td>
<td><ul>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Magix/Merlin</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8300</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>S8700</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>IP Office</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>CallManager 4.x</p></td>
<td><ul>
<li><p>Mediant1000/IP-to-IP</p></li>
<li><p>Mediant2000/IP-to-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>Electra Elite</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>NEAX2400</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP/RS232</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NeXspan</p></td>
<td><p>S</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Communication Server - 1000M, 1000S, 1000E</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridian 11c, 51c, 61c, 81c</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Panasonic</p></td>
<td><p>KX-TES824, KX-TEA308</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Panasonic</p></td>
<td><p>KX-TDA30, KX-TDA100, KX-TDA200, KX-TDA600</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Shortel</p></td>
<td><p>IP Telephony System</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 150E</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 3550</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Tadiran Telecom</p></td>
<td><p>Coral Flexicom, Coral IPX</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Sistemi PBX supportati quando si utilizza un gateway VoIP Dialogic

Ogni modello di gateway VoIP Dialogic supporta differenti sistemi PBX. Nelle seguenti tabelle sono mostrati il produttore e il modello del sistema PBX e il gateway VoIP Dialogic che è possibile utilizzare. Ogni gateway VoIP utilizza metodi di segnalazione, densità e protocolli differenti.

## Sistemi PBX supportati quando si utilizza un gateway multimediale serie DMG1000

Nella seguente tabella vengono mostrati i sistemi PBX supportati con Dialogic Media Gateway (DMG1000) a bassa densità. Tuttavia, quando viene utilizzato un modello DMG1000 analogico, è necessaria una segnalazione aggiuntiva (protocolli RS232 SMDI, MD110, MCI o segnalazione DTMF In-Band).

### Sistemi PBX supportati quando si utilizza un gateway VoIP Dialogic DMG1000 a bassa densità

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Produttore del sistema PBX</th>
<th>Tipo/modello del sistema PBX</th>
<th>Modello DMG e segnalazioni aggiuntive</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>Aastra MD110 (in precedenza Ericsson MD110)</p></td>
<td><p>DMG1008LSW</p>
<p>Connettività analogica tramite protocollo MD110 RS232</p></td>
</tr>
<tr class="even">
<td><p>Alcatel</p></td>
<td><p>Omni PCX 4400</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3 S8100, S8300, S8700 e S8710 (Communications Mgr SW V2.0 o versioni successive)</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Intercom</p></td>
<td><p></p></td>
<td><p>DMG1008LSW</p>
<p>Connettività analogica tramite protocollo seriale SMDI</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>SX-200D, SX-200 Light, SX-2000 Light, SX-2000 S, SX-2000 VS, SX-200 ICP</p></td>
<td><p>DMG1008MTLDNIW</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2000, 2400, 2400 IPX</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridian 1 - Opzione 11, 21, 21A, 51, 61, 71 e 81</p>
<p>Meridian SL1 - Generic X11, versione 15 o successive</p>
<p>Nortel Communication Server - 1000M, 1000S, 1000E V3.0 o versioni successive</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>SL 100</p></td>
<td><p>DMG1008LSW</p>
<p>Connettività analogica tramite protocollo seriale SMDI</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E (europeo)</p></td>
<td><p>DMG1008LSW</p>
<p>Connettività analogica tramite segnale DTMF In-Band</p></td>
</tr>
<tr class="odd">
<td><p>Siemens/ROLM</p></td>
<td><p>8000 (SW 80003 o versioni successive)<br />
9000 (tutte le versioni)</p>
<p>9751 (tutte le versioni di SW 9005)</p>
<p>9751 (SW 9006.4 o versioni successive)</p></td>
<td><p>DMG1008RLMDNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Toshiba</p></td>
<td><p>CTX (SW versione AR1ME021.00)</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="even">
<td><p>Altri</p></td>
<td><p>Vari</p></td>
<td><p>DMG1008LSW</p>
<p>Connettività analogica tramite DTMF In-Band o SMDI</p></td>
</tr>
</tbody>
</table>


## Sistemi PBX supportati quando si utilizza un gateway multimediale serie DMG 2000

Nella seguente tabella vengono mostrati i sistemi PBX supportati con T1/E1 Dialogic Media Gateway (DMG2000). Il gateway DMG2000, fornito in densità a span singolo (DMG2030DTIQ), doppio (DMG2060DTIQ) o quadruplo (DMG2120DTIQ), supporta i seguenti protocolli:

  - T1 CAS

  - T1 Q.SIG

  - E1 Q.SIG

  - T1 NI-2

  - T1 5ESS

  - T1 DMS100

Se viene utilizzata la segnalazione associata al canale (CAS, Channel Associated Signaling), è necessaria una segnalazione aggiuntiva (protocolli RS232 SMDI, MD110, MCI o segnalazione DTMF In-Band). Se viene utilizzata la segnalazione Q.SIG, è necessario che il sistema PBX supporti i servizi aggiuntivi associati alle informazioni delle parti chiamante e chiamata e le capacità di trasferimento di chiamate richieste dalla messaggistica unificata.

### Sistemi PBX supportati con DMG2000 Media Gateway

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Produttore del sistema PBX</th>
<th>Tipo/modello del sistema PBX</th>
<th>Versione del software richiesta</th>
<th>Protocollo e segnalazione aggiuntiva</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>Omni PCX 4400</p></td>
<td><p>Versione 3.2.712.5</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><p>Versione 3 o successiva</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8500</p></td>
<td><p>Manager SW V2.0 o versioni successive</p></td>
<td><p>T1 CAS</p>
<p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Ericsson</p></td>
<td><p>MD110</p></td>
<td><p>Versione MX1 TSW R2A (BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Intercom</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>CAS (con protocollo seriale SMDI)</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2400 IMX</p></td>
<td><p>Versione 5200 Dic. 92 1b o successive</p></td>
<td><p>CAS (con protocollo seriale MCI)</p></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>2400 IPX</p></td>
<td><p>R17 versione 03.46.001</p></td>
<td><p>T1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Meridian 1 - Opzione 11</p></td>
<td><p>Richiesti le versioni 15 o successive e le opzioni 19 e 46</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Communication Server 1000</p></td>
<td><p>Versione 2121, release 4</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>Versione 9006.4 o successiva (nota: solo caricamento software per il Nord America)</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>V2 SMR 9 SMPO</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Mitel</p></td>
<td><p>SX-2000 S, SX-2000 VS</p></td>
<td><p>LW 34</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>3300</p></td>
<td><p>Versione 5.1.4.8</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
</tbody>
</table>


## Sistemi PBX supportati quando si utilizza un gateway multimediale serie DMG4008BRI

DMG4000 Series Media Gateway viene fornito con varie opzioni di interfaccia TDM. DMG4008BRI supporta densità a 4 porte/8canali e supporta inoltre i protocolli seguenti:

  - ISDN BRI Q.SIG

  - ETSI-DSS1 (Euro ISDN)

  - NET 3 (Belgio)

  - VN3 (Francia)

  - 1TR6 (Germania)

  - INS-64 (Giappone)

  - 5ESS Custom (Nord America - AT\&T)

  - ISDN nazionale (NI1 - Nord America)

Nella tabella seguente vengono riportati i sistemi PBX supportati quando si utilizza un Dialogic 4000 Media Gateway Series (DMG4008).

### Sistemi PBX supportati quando si utilizza un DMG4008BRI Media Gateway

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Produttore del sistema PBX</th>
<th>Tipo/modello del sistema PBX</th>
<th>Versione del software richiesta</th>
<th>Protocollo e segnalazione aggiuntiva</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI-Q.SIG (ECMAV2)</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>S.0 B4400</p></td>
<td><p>BRI-Q.SIG (ECMAV2)</p></td>
</tr>
</tbody>
</table>


## Sistemi IP PBX supportati

Anche i sistemi IP PBX sono supportati dalla messaggistica unificata. Nella seguente tabella vengono indicati i sistemi IP PBX supportati quando si utilizza una connessione SIP diretta alla Messaggistica unificata.

### Sistemi IP PBX supportati quando si utilizza una connessione SIP diretta

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Produttore del sistema PBX</th>
<th>Tipo/modello del sistema PBX</th>
<th>Versione del software richiesta</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>MX-ONE</p></td>
<td><p>4.0</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Aura</p></td>
<td><p>5.2.1 con Service Pack 5 (SP5)</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Communication Server 2100</p></td>
<td><p>CS2100 SE13</p></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>Call Manager, Unified Communications Manager</p></td>
<td><p>5.1, 6.x, 7.0 and8.0</p></td>
</tr>
</tbody>
</table>


## Sistemi IP PBX supportati quando si utilizzano gateway multimediali SIP

Gli IP PBX che utilizzano gateway multimediali SIP sono supportati anche dalla messaggistica unificata. Nella seguente tabella sono indicati i sistemi IP PBX supportati quando si utilizzano le funzionalità IP-to-IP dei gateway multimediali SIP per connettersi alla messaggistica unificata.

### Sistemi IP PBX supportati quando si utilizzano gateway SIP multimediali

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Produttore del sistema PBX</th>
<th>Tipo/modello del sistema PBX</th>
<th>Modello di gateway SIP</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco</p></td>
<td><p>Call Manager 4.x</p></td>
<td><p>AudioCodes Mediant 1000/2000 (IP-to-IP attivo)</p></td>
</tr>
</tbody>
</table>


## Messaggistica unificata di Exchange, Office Communications Server 2007 R2 e Microsoft Lync Server

Per le distribuzioni locali e ibride, la messaggistica unificata di Exchange può essere distribuita insieme a Microsoft Office Communications Server 2007 R2 e Microsoft Lync Server 2010 o 2013 per offrire agli utenti dell'organizzazione funzioni di messaggistica vocale e messaggistica istantanea (IM), disponibilità avanzata, conferenza audio e video, nonché un sistema integrato di gestione della messaggistica e della posta elettronica. Per ulteriori informazioni, vedere:

  - [Distribuzione di panoramica della messaggistica UNIFICATA di Exchange 2013 e Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=202010)

Per ulteriori informazioni sui Microsoft Unified Communications Open Interoperability Program per l'infrastruttura di telefonia aziendale, tra cui la ricerca completo gateway PSTN SIP e IP PBX e sul processo per la telefonia fornitori dell'infrastruttura per partecipare a e partecipare al programma, vedere [Microsoft Unified Communications Open Interoperability Program](https://go.microsoft.com/fwlink/p/?linkid=132071).


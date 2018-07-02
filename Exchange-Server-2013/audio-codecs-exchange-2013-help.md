---
title: 'Codec audio: Exchange 2013 Help'
TOCTitle: Codec audio
ms:assetid: 6c39d65c-c2d3-4128-aae9-8596602819c3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998670(v=EXCHG.150)
ms:contentKeyID: 54652872
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Codec audio

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Nella messaggistica unificata per l'archiviazione dei messaggi vocali viene utilizzato un codec audio. Un altro codec viene utilizzato tra un gateway VoIP o IP PBX (Private Branch eXchange) e il server per cassette postali che esegue il servizio Messaggistica unificata di Microsoft Exchange oppure il server Accesso client che esegue il servizio Router delle chiamate di messaggistica unificata di Microsoft Exchange. Per creare e archiviare i messaggi vocali, la messaggistica unificata può utilizzare uno dei quattro codec audio seguenti:

  - MP3 (predefinito)

  - Windows Media Audio (WMA)

  - Group System Mobile (GSM) 06.10

  - Modulazione PCM (Pulse Code Modulation) lineare G.711


> [!WARNING]
> I codec G.711 (PCMA e PCMU) e G.723.1 sono codec VoIP utilizzati tra un gateway VoIP e i server per cassette postali e Accesso client.



Parte della pianificazione del sistema di Messaggistica unificata consiste nello scegliere il codec audio appropriato in base alle esigenze e ai requisiti dell'organizzazione. In questo argomento vengono fornite informazioni relative ai codec audio utilizzabili da Messaggistica unificata e che possono essere utilizzati per pianificarne correttamente la distribuzione.

## Codec

Il termine *codec* deriva dalla combinazione delle parole "codifica" e "decodifica" riferite ai dati audio digitali. Il codec è un programma che converte i dati digitali nel formato file audio o di flusso audio. I codec vengono utilizzati per convertire un segnale vocale analogico in formato digitale. I codec variano per la qualità dell'audio, per la larghezza di banda necessaria per utilizzarli e per i requisititi di sistema necessari per eseguire la codifica.

In Messaggistica unificata vengono utilizzati due tipi di codec:

  - Il codec utilizzato tra un gateway VoIP, IP PBX o PBX abilitato al SIP e i server per cassette postali e Accesso client oppure tra un gateway VoIP e PBX.

  - Il codec utilizzato per codificare e archiviare i messaggi vocali per gli utenti.

Quando si utilizza un telefono normale su una rete pubblica PSTN (Public Switched Telephone Network), la voce viene trasportata attraverso la linea telefonica in formato analogico. Tuttavia in una rete VoIP (Voice over IP), la voce deve essere convertita in segnali digitali. Questo processo di conversione è noto come codifica. La codifica viene eseguita da un codec. Dopo che la voce digitalizzata ha raggiunto la destinazione, deve essere nuovamente decodificata nel formato analogico originale, in modo che la persona all'altro capo della linea possa ascoltare e comprendere il chiamante.

## Codec VoIP

In Messaggistica unificata, è possibile utilizzare tre tipi di codec tra gateway VoIP o IP PBX e i server per cassette postali e Accesso client.

  - G.711 µ-law

  - G.711 A-law

  - G.723.1

G.711 è uno standard sviluppato per l'utilizzo con i codec audio. Nello standard G.711 sono definiti due algoritmi principali: l'algoritmo µ-law, utilizzato in Nord America e in Giappone e l'algoritmo A-law, utilizzato in Europa e in altri paesi. Il codec audio G.723.1 è utilizzato soprattutto nelle applicazioni VoIP e per l'uso è richiesta una licenza. Il codec G.723.1 è un tipo di codec di elevata qualità e ad alta compressione.

Un server per cassette postali o Accesso client e un gateway VoIP o un sistema IP PBX supportati possono offrire i codec G.711 e G.723.1. Per impostazione predefinita, il primo codec da utilizzare è G.723.1. Se si desidera utilizzare un codec diverso da G.723.1 tra i server per cassette postali e Accesso client e il gateway VoIP o IP PBX, si consiglia di modificare la configurazione del gateway VoIP o di IP PBX. Nella tabella seguente sono elencati alcuni codec VoIP comuni.

### Codec VoIP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Codec VoIP</th>
<th>Larghezza di banda (Kbps)</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>64</p></td>
<td><p>Questo codec richiede un'elaborazione molto bassa. Necessita di un minimo di 128 kb per secondo (Kbps) per la comunicazione a due vie.</p></td>
</tr>
<tr class="even">
<td><p>G.723.1</p></td>
<td><p>5.3/6.3</p></td>
<td><p>Questo codec offre un'elevata compressione con alta qualità audio e richiede una maggiore elaborazione rispetto al codec G.711. Il codec G.723.1. utilizza una larghezza di banda ridotta ma offre una qualità audio più bassa.</p></td>
</tr>
</tbody>
</table>


## Codec di archiviazione dei messaggi vocali di messaggistica unificata

I dial plan di messaggistica unificata sono parte integrante delle operazioni di messaggistica unificata. Per impostazione predefinita, quando si crea un dial plan di messaggistica unificata, questo utilizza il codec audio MP3 per creare e archiviare i messaggi vocali. Tuttavia, dopo averlo creato, è possibile configurare il dial plan di messaggistica unificata per utilizzare i codec audio WMA, GSM 06.10 o PCM lineare G.711.

Ogni codec audio ha i suoi vantaggi e svantaggi. Il codec audio MP3 è stato scelto come codec audio predefinito per la qualità del suono e le proprietà di compressione. I codec audio GSM 06.10 e PCM lineare G.711 sono stati inclusi come opzioni perché supportano altri tipi di sistemi di messaggistica.

Durante la pianificazione della messaggistica unificata, è necessario valutare la dimensione e la qualità relativa del file audio che verrà creato per i messaggi vocali. In genere, quanto più alta è la velocità in bit di un file audio tanto più alta sarà la qualità. È necessario considerare anche l'eventuale compressione del file audio. Nella tabella seguente sono riportati esempi di velocità in bit (bit/sec) e le proprietà di compressione di ciascun codec audio utilizzato nella messaggistica unificata.

### Codec di archiviazione predefiniti dei messaggi vocali di messaggistica unificata

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Codec di archiviazione dei messaggi vocali</th>
<th>Bit</th>
<th>File compresso?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>16 bit</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>WMA</p></td>
<td><p>16 bit</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>PCM G.711</p></td>
<td><p>16 bit</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>GSM 06.10</p></td>
<td><p>8 bit</p></td>
<td><p>Sì</p></td>
</tr>
</tbody>
</table>


Nella messaggistica unificata il tipo di file creato per un messaggio vocale dipende dal codec audio utilizzato per creare il file audio per il messaggio. Il codec audio MP3 crea file audio .mp3, il codec audio WMA crea file audio .wma, mentre i codec audio GSM 06.10 e PCM lineare G.711 generano file audio .wav. Tutti questi tipi di file audio vengono inviati con il messaggio di posta elettronica al destinatario del messaggio vocale.

Spesso ma non sempre, la codifica e decodifica dei dati digitali prevede anche la compressione o decompressione. La compressione audio è un tipo di compressione dei dati che riduce le dimensioni dei file dati audio. L'algoritmo di compressione audio utilizzato dal codec audio comprime i file audio .wma o .wav. Nella messaggistica unificata, il tipo di algoritmo di compressione audio utilizzato dipende dal tipo di codec audio selezionato nelle proprietà del dial plan di messaggistica unificata. Dopo la creazione e la compressione, il file audio viene allegato al messaggio vocale.

Talvolta, durante la compressione e decompressione del file si verifica la perdita dei dati digitali. Più elevato è il grado di compressione utilizzato per comprimere il file audio, maggiore è la perdita di informazioni durante la conversione. Tuttavia, viene utilizzato minore spazio su disco, dal momento che le dimensioni del file audio si riducono. Viceversa, più basso è il grado di compressione, minore è la perdita di informazioni. Tuttavia, è necessario utilizzare maggior spazio su disco, perché le dimensioni del file audio aumentano.

È anche disponibile come un codec audio a banda larga RTAudio o ad alta fedeltà audio per la registrazione di messaggi vocali. Tuttavia, ad alta fedeltà audio mediante RTAudio è disponibile solo dopo che è stata integrata la messaggistica unificata correttamente con [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=202010). Per consentire RTAudio come codec cablato, limitare o a banda larga, il dial plan di messaggistica UNIFICATA deve essere configurato come un dial plan di tipo di URI protocollo SIP (Session Initiation) ed è necessario impostare il codec di ricezione chiamata nel dial plan MP3 o WMA abilitare audio a banda larga (16khz).


> [!IMPORTANT]
> La funzionalità RTAudio non è disponibile in ambienti in cui non è distribuito Lync Server, poiché in ambienti che non hanno Lync Server integrato, il dial plan viene impostato sul numero di interno oppure E.164 e non su URI SIP.



Per ogni chiamata in arrivo si creano due flussi multimediali: in ingresso verso un server Accesso client e in uscita da un server per cassette postali. Quando il tipo di dial plan è impostato su URI SIP e il codec di risposta alle chiamate del dial plan è impostato su MP3 o WMA, il server Accesso client tenta di selezionare il codec VoIP RTAudio per il flusso di messaggi in ingresso. Se la negoziazione riesce, il codec RTAudio per il flusso di messaggi in ingresso viene utilizzato per la risposta alle chiamate normali o a quelle che provengono da un server o client Lync.


> [!NOTE]
> Per le chiamate effettuate utilizzando la funzionalità Ascolta al telefono non viene utilizzato il codec RTAudio. Per il flusso di messaggi in ingresso per le chiamate effettuate utilizzando la funzionalità Ascolta al telefono viene utilizzato il codec G.711 o G.723.1.



Quando viene utilizzato il codec RTAudio, il messaggio vocale viene registrato ad alta fedeltà e viene archiviato come file audio con estensione WMA o MP3 in base alla configurazione del dial plan. Quando il messaggio vocale viene riprodotto per l'utente di Outlook o di Outlook Web App, l'utente può ascoltarlo in alta fedeltà. Se la negoziazione fallisce, viene utilizzato il codec G.711 o G.723.1. Sia il codec G.711 che il codec G.723.1 sono codec a banda stretta. Quando vengono utilizzati come codec VoIP, il messaggio vocale viene registrato e archiviato come file audio a banda stretta con estensione WMA o MP3.

Il flusso di messaggi in uscita viene sempre negoziato utilizzando il codec G.711 o il codec G.723.1. Ciò significa che i chiamanti ascolteranno sempre via telefono un audio a banda stretta. Ciò si applica anche a situazioni nelle quali viene effettuata una chiamata utilizzando Microsoft Lync Server 2010 o versione successiva.

Il formato e codec audio che i server per cassette postali utilizzano per registrare l'audio nei messaggi vocali dipende non solo dal codec audio configurato sul dial plan, ma anche dalla velocità in bit dell'audio che la messaggistica unificata negozia con un peer SIP. Se l'ambiente include Lync Server o gli endpoint SIP, un server per cassette postali negozierà anche il codec audio da utilizzare con un peer SIP. Ad esempio, quando come codec cablato viene negoziato RTAudio a banda larga, un server per cassette postali utilizzerà il formato MP3 32 Kbps o WMA 9.2 per la creazione dei messaggi vocali, a seconda dell'impostazione sul dial plan. La tabella che segue riporta la relazione tra il codec audio per la registrazione del messaggio vocale e il codec audio VoIP o cablato utilizzato.

### Relazione tra codec audio per la registrazione del messaggio vocale e codec audio VoIP o cablato

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Codec audio configurato su un dial plan di messaggistica unificata</th>
<th>Codec VoIP o cablato (banda stretta) - G.723, G.711 o RTAudio (8KHz)</th>
<th>Codec VoIP o cablato (banda larga) - RTAudio (16KHz)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>G.711</p></td>
<td><p>Non applicabile. Un server per cassette postali o Accesso client non negozia l'audio a banda larga se il dial plan è impostato su G.711.</p></td>
</tr>
<tr class="even">
<td><p>WMA</p></td>
<td><p>WMA 9-voice</p></td>
<td><p>WMA 9.2</p></td>
</tr>
<tr class="odd">
<td><p>GSM</p></td>
<td><p>GSM 6.10</p></td>
<td><p>Non applicabile. Cassette postali o Accesso client non negozia l'audio a banda larga se il dial plan è impostato su GSM.</p></td>
</tr>
<tr class="even">
<td><p>MP3</p></td>
<td><p>MP3 (16 Kbps)</p></td>
<td><p>MP3 (32 Kbps)</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Dimensioni dei messaggi di messaggistica unificata

Per la creazione dei messaggi vocali, è possibile configurare la messaggistica unificata per l'utilizzo di uno dei quattro codec audio seguenti: MP3, WMA, GSM 06.10 e PCM lineare G.711. Per impostazione predefinita, è selezionato il formato MP3.

Il codec audio WMA viene sempre salvato nel formato Windows Media e l'allegato consiste in un file con estensione .wma. I file audio configurati con i codec audio GSM o PCM lineare G.711 sono sempre salvati in formato RIFF/WAV format e l'allegato consiste in un file con estensione .wav.

Le dimensioni dei messaggi vocali di messaggistica unificata dipendono dalle dimensioni dell'allegato contenente i dati vocali e le dimensioni dell'allegato dipendono a loro volta dai seguenti fattori:

  - Durata della registrazione del messaggio vocale

  - Codec audio utilizzato

  - Formato di archiviazione del file audio

Nella figura seguente viene illustrata la dipendenza tra le dimensioni del file audio e la durata della registrazione del messaggio vocale per i tre codec audio utilizzabili nella messaggistica unificata.


> [!NOTE]
> Nella figura la durata media di un messaggio vocale di risposta a una chiamata è di circa 30 secondi.



**Dimensioni dei file audio**

![UM\_Message\_Sizing](images/Aa998670.76ca4891-450f-4ffd-9493-aac8d0d23a5d(EXCHG.150).gif "UM_Message_Sizing")

## MP3

Per impostazione predefinita, è selezionato il formato MP3, che costituisce il formato di file audio predefinito per i messaggi vocali. Il formato MP3 è un comune formato di file audio, utilizzato per ridurre notevolmente le dimensioni del file audio ed è il più comunemente utilizzato dai dispositivi audio personali o dai lettori MP3. MP3 è un tipo di codec audio multipiattaforma, utilizzato per la compatibilità con molti telefoni cellulari, dispositivi mobili e diversi sistemi operativi.

## WMA

WMA è il codec audio con la compressione maggiore rispetto ai tre tipi di codec. La compressione è di circa 11.000 byte per 10 secondi di audio. Tuttavia, il formato .wma ha un'intestazione molto più grande rispetto al formato .wav. L'intestazione del file .wma è di circa 7 kilobyte, mentre quella del file .wav file è inferiore a 100 byte. Benché le registrazioni audio WMA non superino i 15 secondi, hanno comunque dimensioni inferiori rispetto alle registrazioni GSM. Pertanto, si utilizza il codec audio WMA per ottenere file piccoli ma di elevata qualità.


> [!NOTE]
> Se si utilizzano notifiche di push dalla distribuzione in locale per OWA per dispositivi, non è possibile utilizzare il formato WMA. OWA per dispositivi supporta solo il formato di file MP3.



## PCM lineare G.711

Il codec audio PCM lineare G.711 crea file audio .wav non compressi. Pertanto, i file audio .wav PCM lineare G.711 occupano molto spazio, indipendentemente dalla durata della registrazione, rispetto ai codec audio GSM e WMA. I file audio .wav creati con il codec audio PCM lineare G.711 occupano poco più di 160.000 byte per 10 secondi di audio. La qualità di questi file audio è la migliore di tutti e tre i codec audio utilizzati dalla messaggistica unificata. Tuttavia, la qualità di file audio analoghi creati con i codec audio WMA e GSM è accettabile per la maggior parte degli utenti che ascoltano messaggi vocali.

## GSM

Il codec audio GSM crea file audio .wav compressi. I file audio .wav creati con il codec audio GSM occupano poco più di 16.000 byte per 10 secondi di audio. Tuttavia, il codec GSM crea file audio più grandi rispetto a quelli creati dal codec audio WMA. Pertanto, valutando qualità del messaggio vocale e dimensioni, il codec GMS potrebbe non rappresentare la scelta migliore.

Inizio pagina


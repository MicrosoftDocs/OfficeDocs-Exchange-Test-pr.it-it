---
title: "Modifiche all'architettura VoIP: Exchange 2013 Help"
TOCTitle: Modifiche all'architettura VoIP
ms:assetid: 55d5ca4a-b0cd-45f1-9f47-e745ef208698
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150516(v=EXCHG.150)
ms:contentKeyID: 50480683
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modifiche all'architettura VoIP

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-03-09_

L'architettura in Microsoft Exchange Server 2013 è diversa dall'architettura in Exchange Server 2007 e Exchange Server 2010. In Exchange 2007 e Exchange 2010, i tipi di server erano separati in più ruoli di server: Accesso client, Cassette postali, Trasporto Hub e Messaggistica unificata. In Exchange 2013, i ruoli dei server sono combinati in due tipi di server e tutti i componenti o servizi di questi ruoli di server vengono eseguiti sullo stesso server fisico o su due server separati chiamati Accesso client e Cassette postali. Nel nuovo modello, il server Accesso client su cui è in esecuzione il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange reindirizza il traffico SIP (Session Initialization Protocol) generato da una chiamata entrante verso un server Cassette postali. Quindi viene stabilito un canale di supporto (Realtime Transport Protocol (RTP) o Secure RTP (SRTP)) tra il gateway VoIP o PBX IP (Private Branch eXchange) al server Cassette postali che ospita la cassetta postale utente. In Exchange 2013, il server Cassette postali dispone degli stessi processi dei ruoli server di messaggistica unificata in Exchange 2007 e Exchange 2010. Il server Cassette postali esegue sia il servizio Messaggistica unificata di Microsoft Exchange che il processo di lavoro di messaggistica unificata. Il server Accesso client esegue il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange che riceve le chiamate in ingresso e le inoltra al server Cassette postali.

**Sommario**

Support for the new Exchange architecture

UM ports

UM dial plans

UM Call Router performance counters

## Supporto per la nuova architettura di Exchange

In Exchange 2013, il server Accesso client è responsabile dell'individuazione automatica, SSL (Secure Sockets Layer), autenticazione, reindirizzamento, e proxy. Il server Accesso client è il punto di ingresso per qualsiasi chiamata in entrata o richiesta SIP di messaggistica unificata (UM). La logica di instradamento e il comando SIP REDIRECT vengono implementati come un servizio incluso automaticamente in un server Accesso client. Questo servizio è noto come servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange. È installato e viene eseguito su ogni server Accesso Client nell'organizzazione. Quando un server Accesso client riceve un SIP INVITE per una chiamata in entrata, il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange reindirizza la chiamata al server Cassette postali. Viene quindi creato un canale di supporto (RTP o SRTP) tra il gateway VoIP, PBX IP o SBC (Session Border Controller) e il server Cassette postali. Sebbene il server Accesso client agisca come un reidirizzatore SIP, gestisce solo le richieste provenienti da gateway VoIP, PBX IP o SBC. Non riceve alcun traffico multimediale. Il traffico multimediale che utilizza RTP o SRTP viene passato solo tra server Cassette postali e peer SIP quali ad esempio gateway VoIP, PBX IP o SBC—non al server Accesso client. Quando si distribuisce Exchange 2013 e messaggistica unificata, è necessari configurare i propri gateway VoIP, PBX IP o SBC per puntare ai server Accesso client installati in modo che le chiamate in entrata vengano correttamente instradate per la messaggistica unificata.

In alcuni casi, distribuire più server Accesso client è un requisito e i server Accesso client vengono distribuiti separatamente su diversi hardware fisici dai server Cassette postali. I server Accesso client possono essere raggruppati in un array utilizzando un bilanciatore di traffico software o hardware L4 o L5. Tuttavia, non esistono array di server Accesso client basati su oggetti Exchange in Active Directory. L'uso di bilanciatori di carico hardware o software per un server Accesso client è pratica accettata nelle distribuzioni di Exchange di grandi dimensioni.

Quando è installato un server di Accesso client, è in esecuzione il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange. Il servizio effettua le seguenti operazioni:

  - Quando viene inizializzato, legge un file di configurazione locale denominato msexchangeumcallrouter.config.

  - Genera la grammatica vocale utilizzando la cassetta postale di arbitraggio per un'organizzazione.

  - Supporta connessioni Transmission Control Protocol (TCP) o il Transport Layer Security (TLS). Tale impostazione è configurabile.

  - Si arresterà solo se si verifica un errore di configurazione e se è impossibile registrare le porte necessarie.

In Exchange 2013, il server Cassette postali non è responsabile di rispondere alle richieste SIP delle chiamate in entrata. È responsabile solo di ricevere il traffico SIP proveniente da in server Accesso client e di stabilire una connessione RTP o SRTP al gateway VoIP, PBX IP o SBC.

Dopo che un server Accesso client ha reindirizzato una chiamata in entrata al server Cassette postali, viene stabilito un canale multimediale tra il gateway VoIP, PBX IP o SBC e il server Cassette postali. Dopo aver stabilito il canale multimediale, il servizio Messaggistica unificata di Microsoft Exchange sul server Cassette postali riproduce il messaggio vocale di saluto dell'utente, elabora le regole risponditore automatico per l'utente ed invita il chiamante a lasciare un messaggio vocale. Il server Cassette postali registra il messaggio vocale, crea una trascrizione del messaggio e la deposita nella cassetta postale dell'utente. Tuttavia, se si sta eseguendo l'integrazione di Exchange con Office Communications Server 2007 R2 o Lync Server, entrambi i canali multimediali SIP e RTP o SRTP per le chiamate in entrata sono gestiti dai server Lync e dai server Cassette postali. In un ambiente integrato Lync, non sono disponibili gateway VoIP, PBX IP PBX o SBC. Lync considera il server Cassette postali su cui è in esecuzione il servizio Messaggistica unificata di Microsoft Exchange come un server di messaggistica unificata di Exchange 2010. Il server Cassette postali e il server Accesso client sui quali è in esecuzione il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange sono considerati peer attendibili poiché entrambi i server devono essere aggiunti a un dial plan SIP. Lync instrada la chiamata in entrata utilizzando il componente Inbound Routing che utilizza SIP per comunicare con il server Accesso client quindi instrada la chiamata al server Cassette postali.

Gli amministratori di messaggistica unificata di Exchange 2010 possono configurare un gruppo di proprietà per la messaggistica unificata su ciascun server Messaggistica unificata. In Exchange 2013, i componenti di messaggistica unificata e le impostazioni di messaggistica unificata si trovano sia sui server Accesso client che sui server Cassette postali. Tutte le impostazioni di configurazione che venivano applicate ad un singolo computer su cui era in esecuzione il ruolo di server Messaggistica unificata in Exchange 2010 sono ancora disponibili. Tuttavia, alcune di queste proprietà e impostazioni di configurazione vengono impostate sul server Accesso client sul quale è in esecuzione il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange e altre sono invece disponibili sul server Cassette postali sul quale è in esecuzione il servizio Messaggistica unificata di Microsoft Exchange. In alcuni casi, la stessa impostazione è disponibile su entrambi. L'elenco seguente mostra i cmdlet e i parametri disponibili sui server Accesso client e Cassette postali e in cui sono state apportate delle modifiche a un cmdlet per supportare gli scenari di distribuzione con le precedenti versioni di messaggistica unificata.

  - **Set-UMService -DialPlans \<MultiValuedProperty\>**    Disponibile sui server Cassette postali di Exchange 2013 e compatibile anche con i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Set-UMCallRouterSettings -DialPlans \<MultiValuedProperty\>**    Disponibile sui server Accesso client di Exchange 2013 ma non disponibile per i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Set-UMService -MaxCallsAllowed \<Int32\>**    Disponibile sui server Cassette postali di Exchange 2013 e compatibile anche con i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Set-UMCallRouterSettings -MaxCallsAllowed \<Int32\>**   Non disponibile sui server Accesso client di Exchange 2013 e non disponibile per i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Set-UMService -SipTcpListeningPort \<Int32\>**   Non configurabile sui server Cassette postali di Exchange 2013 ma è compatibile con i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Set-UMService -SipTlsListeningPort \<Int32\>**   Non configurabile sui server Cassette postali di Exchange 2013 ma è compatibile con i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Set-UMCallRouterSettings -SipTcpListeningPort\<Int32\>**    Disponibile sui server Accesso client di Exchange 2013 ma non compatibile con i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Set-UMCallRouterSettings -SipTlsListeningPort\<Int32\>**    Disponibile sui server Accesso client di Exchange 2013 ma non compatibile con i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Set-UMService - Status \<Enabled | Disabled | NoNewCalls\>**   Non disponibile sui server Cassette postali di Exchange 2013 ma è compatibile con i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Set-UMCallRouterSettings - Status\<Enabled | Disabled | NoNewCalls\>**   Non disponibile sui server Accesso client di Exchange 2013 ma è compatibile con i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Set-UMService -UMStartupMode \<TCP | TLS | Dual\>**    Disponibile sui server Cassette postali di Exchange 2013 e compatibile con i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Set-UMCallRouterSettings - UMStartupMode\<TCP | TLS | Dual\>**    Disponibile sui server Accesso client di Exchange 2013 ma non compatibile con i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Enable-UMService**   Non disponibile sui server Cassette postali di Exchange 2013 ma è compatibile con i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

  - **Disable-UMService**   Non disponibile sui server Cassette postali di Exchange 2013 ma è compatibile con i server di messaggistica unificata di Exchange 2007 e Exchange 2010.

Per il server Cassette postali si utilizzeranno i cmdlet **Set/Get/Enable/Disable-UMService** per visualizzare o configurare le proprietà di messaggistica unificata per il servizio di messaggistica unificata di Microsoft Exchange sui server Cassette postali di Exchange 2013 o sui server di messaggistica unificata di Exchange 2007 o Exchange 2010. Un diverso gruppo di cmdlet, **Set/Get-UMCallRouterSettings**, viene utilizzato per visualizzare e configurare le proprietà del servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange su un server Accesso client. Questo assicura che i cmdlet esistenti **Get-UMServer**, **Set-UMServer**, **Enable-UMServer** e **Disable-UMServer** provenienti da Exchange 2007 e Exchange 2010 possano funzionare in una distribuzione in cui coesistono server Cassette postali di Exchange 2013. Questo assicura che i cmdlet possano funzionare anche se i server Accesso client e i server Cassette postali sono installati o sullo stesso server o su server diversi.

Inizio pagina

## Porte di messaggistica unificata

Il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange che si trova su un server Accesso client utilizza SIP o su TCP ( Transmission Control Protocol) o MTLS (mutual Transport Layer Security ) per comunicare con i server Cassette postali sui quali è in esecuzione il servizio di messaggistica unificata di Microsoft Exchange. Per evitare conflitti tra le porte TCP/UDP (User Datagram Protocol), il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange e il servizio di messaggistica unificata di Microsoft Exchange, per impostazione predefinita vengono impostati e ascoltano su porte TCP differenti. Questi possono accettare connessioni sia protette che non protette, a seconda che MTLS venga utilizzato con traffico SIP e RTP. Per impostazione predefinita un server Accesso client ascolta le richieste SIP sulla porta TCP 5060 in modalità non protetta sulla porta TCP 5061 in modalità protetta SIP quando viene utilizzato MTLS. Queste porte sono configurabili utilizzando il cmdlet **Set-UMCallRouterSettings**. Il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange sul server Accesso client non gestisce il traffico multimediale (RTP o SRTP), perciò vengono utilizzate solo le porte TCP e non vengono utilizzate le porte UDP. Per impostazione predefinita un server Cassette postali ascolta le richieste SIP sulla porta TCP 5062 in modalità non protetta sulla porta TCP 5063 in modalità protetta SIP quando viene utilizzato MTLS. Queste porte non sono configurabili utilizzando i cmdlet di Exchange Management Shell. Su un server Cassette postali si cui è in esecuzione il servizio di messaggistica unificata di Microsoft Exchange, le porte TCP non possono essere configurate sul server Exchange né utilizzando Shell né configurando le impostazioni nel registro. Il servizio di messaggistica unificata di Microsoft Exchange sul server Cassette postali accetterà le connessioni da un server Accesso client sulle porte SIP 5062 e 5063. Dopo che il server Accesso client reindirizza la richiesta SIP al server Cassette postali vengono creati un canale multimediale RTP o SRTP utilizzando un gateway VoIP, PBX IP PBX o SBC, e il processo di lavoro di messaggistica unificata di Microsoft Exchange sul server Cassette postali.

La tabella seguente riassume le porte e i protocolli di Exchange 2013 e se le porte possono essere modificate.

### Porte di ascolto di messaggistica unificata

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocollo</th>
<th>Porta TCP</th>
<th>Porta UDP</th>
<th>È possibile modificare le porte?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SIP (server Accesso Client – servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange)</p></td>
<td><p>5060 (non protetta), 5061 (protetta). Il servizio è in ascolto su entrambe le porte.</p></td>
<td><p>Non applicabile</p></td>
<td><p>Sì, utilizzando il cmdlet <strong>Set-UMCallRouterSettings</strong>.</p></td>
</tr>
<tr class="even">
<td><p>SIP (server Cassette postali – servizio Messaggistica unificata di Microsoft Exchange)</p></td>
<td><p>5062 (non protetta), 5063 (protetta). Il servizio è in ascolto su entrambe le porte.</p></td>
<td><p>Non applicabile</p></td>
<td><p>Le porte non possono essere modificate.</p></td>
</tr>
<tr class="odd">
<td><p>SIP (server Cassette postali - Processo di lavoro di messaggistica unificata)</p></td>
<td><p>5065 e 5067 per TCP (non protette). 5066 and 5068 per Mutual TLS (protette). Questo è il caso quando <em>UMStartupMode</em> è impostato su <em>Dual</em>. Se la modalità <em>UMStartUpMode</em> è impostata su <em>TCP</em> o <em>TLS</em>, vengono utilizzate le porte 5065 e 5066. L'impostazione predefinita di <em>UMStartupMode</em> è <em>TCP</em>.</p></td>
<td><p>Non applicabile</p></td>
<td><p>Le porte non possono essere modificate.</p></td>
</tr>
<tr class="even">
<td><p>RTP (server Cassette postali - Processo di lavoro di messaggistica unificata)</p></td>
<td><p>Non applicabile</p></td>
<td><p>Porte comprese tra 1024 e 65535.</p></td>
<td><p>L'intervallo delle porte può essere modificato tramite il registro (tuttavia, questa non è una configurazione supportata):</p>
<p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMinPort</p>
<p>HKLM\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMaxPort</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Dial plan di messaggistica unificata

La mappatura o associazione di un dial plan di messaggistica unificata ai server Messaggistica unificata non è necessaria in Exchange 2013 come lo era in Exchange 2007 e Exchange 2010. I server Accesso client o Cassette postali sui quali sono in esecuzione servizi di messaggistica unificata non hanno necessità di essere collegati a un dial plan poiché è previsto che ricevano le chiamate in entrata da gateway VoIP, PBX IP o SBC. L'eccezione è che i dial plan SIP utilizzati con Lync 2013, Lync Server 2010, e Office Communications Server 2007 R2 devono essere associati con i server Accesso client e Cassette postali che sono sati distribuiti. Entrambi i tipi di server Exchange devono essere aggiunti a ciascun dial plan SIP per essere inclusi nei peer attendibili da Communications Server 2007 R2 o Lync Server. Altrimenti, Communications Server 2007 R2 o Lync Server rifiuteranno le chiamate in uscita dagli utenti.

La tabella seguente riassume le relazioni tra i server Accesso client e Cassette postali e i dial plan di messaggistica unificata.

### Collegamento di dial plan di messaggistica unificata

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topologia</th>
<th>Dial plan</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accesso client e Cassette postali sullo stesso server (senza dial plan non SIP per Communications Server 2007 R2 o Lync Server 2010)</p></td>
<td><p>Non è più necessario associare i dial plan a server Accesso client o Cassette postali. Non è consentito aggiungere server Accesso client o Cassette postale a un dial plan. Se si esegue il cmdlet <strong>Set-UMService</strong> e si tenta di associare un server Cassette postali a un dial plan non SIP, verrà generato un messaggio di errore.</p></td>
</tr>
<tr class="even">
<td><p>Accesso client e Cassette postali su server (senza dial plan non SIP per Communications Server 2007 R2 o Lync Server 2010)</p></td>
<td><p>Non è più necessario associare i dial plan a server Accesso client o Cassette postali. Non è consentito aggiungere server Accesso client o Cassette postale a un dial plan. Se si esegue il cmdlet <strong>Set-UMService</strong> e si tenta di associare un server Cassette postali a un dial plan non SIP, verrà generato un messaggio di errore.</p></td>
</tr>
<tr class="odd">
<td><p>Accesso client e Cassette postali sullo stesso server (con dial plan SIP per Communications Server 2007 R2 o Lync Server 2010)</p></td>
<td><p>Nel caso di un singolo dial plan SIP, aggiungere tutti i server Accesso client e Cassette postali al dial plan in questione. Nel caso di un più dial plan SIP, aggiungere tutti i server Accesso client e Cassette postali a ciascun dial plan. In questo modo, entrambi i server risulteranno peer attendibili di Office Communications Server 2007 R2 o Lync Server. Nella distribuzione di Office Communications Server 2007 R2 o Lync Server si deve utilizzare lo stesso certificato dei server Accesso client e Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>Accesso client e Cassette postali su server diversi (con dial plan SIP per Communications Server 2007 R2 o Lync Server 2010)</p></td>
<td><p>Nel caso di un singolo dial plan SIP, aggiungere tutti i server Accesso client e Cassette postali al dial plan in questione. Nel caso di un più dial plan SIP, aggiungere tutti i server Accesso client e Cassette postali a ciascun dial plan. In questo modo, entrambi i server risulteranno peer attendibili di Office Communications Server 2007 R2 o Lync Server. Se i certificati da utilizzare sui server Accesso client e Cassette postali sono diversi, nelle distribuzioni di Office Communications Server 2007 R2 o Lync Server si devono utilizzare gli stessi certificati che si usano su ciascun serve Accesso client e Cassette postali nell'organizzazione.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Contatori delle prestazioni del Router delle chiamate di messaggistica unificata

Le versioni precedenti di Exchange includevano il ruolo di server Messaggistica unificata, che eseguiva il servizio Messaggistica unificata di Microsoft Exchange. A causa delle modifiche dell'architettura in Exchange 2013, il server Accesso client esegue il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange e il server Cassette postali esegue il servizio Messaggistica unificata di Microsoft Exchange. Per gli amministratori sono disponibili gli stessi contatori per il servizio Messaggistica unificata di Microsoft Exchange che erano disponibili nelle versioni precedenti messaggistica unificata di Exchange. Tuttavia, esistono anche altri contatori delle prestazioni che possono essere utilizzati sul server Accesso client per verificare lo stato del servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange e per la risoluzione dei problemi.

Per supportare il nuovo servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange in Acceso client in Exchange 2013, sono ora disponibili i seguenti contatori delle prestazioni.

### Contatori delle prestazioni

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Categoria del contatore delle prestazioni</th>
<th>Nome contatore</th>
<th>Descrizione</th>
<th>Soglia</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>% di chiamate in entrata rifiutate dal servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange nell'ultima ora</p></td>
<td><p>Indica la percentuale di chiamate in entrata che sono state respinte dal servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange nel corso dell'ultima ora.</p></td>
<td><p>Deve sempre essere inferiore al 5 percento, ma dovrebbe essere sempre 0.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Chiamate disconnesse a causa di un errore interno non recuperabile nel servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange</p></td>
<td><p>Indica il numero di chiamate disconnesse dopo che si è verificato un errore interno del sistema.</p></td>
<td><p>Il valore deve essere sempre 0.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Numero totale di chiamate in entrata rifiutate dal servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange</p></td>
<td><p>Indica il numero totale delle chiamate in entrata che sono state respinte dal servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange da quanto il servizio è stato avviato.</p></td>
<td><p>Il valore deve essere sempre 0.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Numero totale di chiamate ricevute dal servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange</p></td>
<td><p>Indica il numero totale delle chiamate ricevute dal servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange da quanto il servizio è stato avviato.</p></td>
<td><p>Deve essere 0 o maggiore.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>% di chiamate in entrata rifiutate dal servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange nell'ultima ora</p></td>
<td><p>Indica la percentuale di chiamate in entrata che sono state respinte dal servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange nel corso dell'ultima ora.</p></td>
<td><p>Il valore deve essere inferiore a 5 percento.</p></td>
</tr>
</tbody>
</table>


Inizio pagina


---
title: 'Servizi, porte e protocolli di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Servizi, porte e protocolli di messaggistica unificata
ms:assetid: 5997ce29-1755-48bb-8ff4-b08da549482a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998265(v=EXCHG.150)
ms:contentKeyID: 54652866
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Servizi, porte e protocolli di messaggistica unificata

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-03-09_

Microsoft Exchange 2013 Messaggistica unificata (UM) è necessario che le porte TCP e protocollo UDP (User Datagram) diverse da utilizzare per stabilire la comunicazione tra server che eseguono Exchange 2013 e altri dispositivi. Concessione dell'accesso a queste porte IP, si consente la messaggistica unificata per il corretto funzionamento. In questo argomento vengono illustrate le porte TCP e UDP utilizzate in Exchange 2013 la messaggistica unificata.

## Servizi e i protocolli di messaggistica unificati

Exchange 2013 Servizi e funzionalità di messaggistica unificata si basano sulle porte TCP e UDP statiche e dinamiche per garantire il corretto funzionamento del server Accesso Client che eseguono il servizio Microsoft Exchange Unified Messaging routing delle chiamate e il server cassette postali in esecuzione il servizio messaggistica unificata di Exchange. Durante l'installazione di Exchange 2013, le regole del Firewall in entrata statica Windows vengono aggiunte per Exchange. Se si modificano le porte TCP utilizzate dal server cassette postali e accesso Client, è inoltre necessario riconfigurare le regole di Firewall Windows per consentire la messaggistica unificata per funzionare correttamente.


> [!IMPORTANT]
> On Exchange 2013 accesso Client e cassette postali server che eseguono servizi e i componenti di messaggistica unificata, il programma di installazione di Exchange consente di creare le regole del firewall in entrata che consente le comunicazioni in ingresso senza limitazioni porta TCP. Vengono aggiunte le seguenti regole in entrata per servizi di messaggistica unificata:



1.  **SESWorker (GFW) (TCP-In)**

2.  **UMCallRouter (GFW) (TCP-In)**

3.  **UMCallRouter (TCP-In)**

4.  **UMService (GFW) (TCP-In)**

5.  **UMService (TCP-In)**

6.  **UMWorkerProcess – RPC (TCP-In)**

7.  **UMWorkerProcess (GFW) (TCP-In)**

8.  **UMWorkerProcess (TCP-In)**

## Session Initiation Protocol

Protocollo SIP (Session Initiation) è un protocollo utilizzato per inizializzare la modifica e termina una sessione utente interattiva che interessa gli elementi multimediali, ad esempio video, audio, messaggistica immediata, giochi online e realtà virtuale. Corrisponde a uno dei protocolli di segnalazione di Enterprise Voice over IP (VoIP), insieme a h. 323 iniziali. La maggior parte delle soluzioni basate su standard VoIP utilizzano h. 323 o SIP. Tuttavia, diverse progettazioni di proprietari e protocolli anche. I protocolli VoIP supportano le funzionalità, ad esempio chiamata in attesa, le conferenze telefoniche, in genere e trasferimento di chiamata.

Client SIP, ad esempio gateway VoIP e IP Private Branch PBX () è possibile utilizzare TCP e UDP porta 5060 per la connessione al server SIP, inclusi i server Accesso Client che eseguono il servizio Microsoft Exchange Unified Messaging routing delle chiamate. SIP viene utilizzato solo per la configurazione e all'interruzione di chiamate vocali o video. Tutte le comunicazioni vocali e video si verificano in tempo reale RTP (Transport Protocol).

## Protocollo di trasporto in tempo reale

RTP definisce un formato di pacchetto standard per il recapito di audio e video in una rete specifica, ad esempio Internet. RTP esegue solo i dati audio/video sulla rete. Impostazione delle chiamate e dell'eliminazione della vengono in genere eseguite da SIP.

RTP non richiede una porta TCP o UDP standard o statica per comunicare con. Comunicazioni RTP avvengono su una numero pari UDP porta e il successiva numerica dispari porta superiore viene utilizzata per le comunicazioni TCP. Anche se non le assegnazioni intervallo delle porte standard, RTP viene generalmente configurata per utilizzare porte tra 1024 e 65535 e delle cassette postali in esecuzione di questa convention Segui servizio messaggistica unificata di Exchange. È difficile per RTP di oltrepassare i firewall perché utilizza un intervallo di porte dinamiche.

## Servizi Web di messaggistica unificata

I servizi di messaggistica unificata Web installati sui server cassette postali utilizzano IP per le comunicazioni di rete tra un client, il server cassette postali e i computer che eseguono altri ruoli del server Exchange 2013. Diverse funzionalità clientOutlook Web App e Outlook 2013Exchange 2013 si basa su servizi di messaggistica unificata Web per il corretto funzionamento.

Funzionalità dei client di messaggistica unificata seguenti si basano sui servizi Web di messaggistica unificata:

  - Segreteria telefonica opzioni posta disponibili con Exchange 2013Outlook Web App, tra cui la riproduzione sul feature Phone e la possibilità di reimpostare il PIN.

  - La caratteristica Ascolta al telefono disponibili in un client Outlook.

## Porte di messaggistica unificata

Il servizio Microsoft Exchange Unified Messaging routing delle chiamate trovato in un server Accesso Client utilizza il protocollo SIP su protocollo TCP (Transmission Control) o reciproca Transport Layer Security (mutual TLS) per comunicare con i server cassette postali che eseguono il servizio messaggistica unificata di Exchange. Per evitare conflitti di porta TCP/protocollo UDP (User Datagram), il servizio Microsoft Exchange Unified Messaging routing delle chiamate e il servizio messaggistica unificata di Exchange per impostazione predefinita e in ascolto su porte TCP diverse. È possibile accettare entrambi non protetta e protetta connessioni, a seconda che MTLS viene utilizzato con il traffico SIP e RTP. Per impostazione predefinita, un server Accesso Client è in ascolto per le richieste SIP in entrambi porta TCP 5060 in modalità non protetta e la porta TCP 5061 in modalità SIP protetta quando si utilizza MTLS. Queste porte sono configurabili utilizzando il cmdlet **Set-UMCallRouterSettings** . Il servizio Microsoft Exchange Unified Messaging routing delle chiamate sul server Accesso Client non gestisce (RTP o SRTP) il traffico multimediale, in modo che vengono utilizzate solo le porte TCP e non le porte UDP. Per impostazione predefinita, un server cassette postali è in ascolto per le richieste SIP in entrambi 5062 in modalità non protetta la porta TCP e porta TCP 5063 nella modalità SIP protetta quando si utilizza MTLS. Queste porte non sono configurabili utilizzando i cmdlet di Exchange Management Shell. Il servizio messaggistica unificata di Microsoft Exchange sul server cassette postali accetta connessioni da un server Accesso Client su porte SIP 5062 e 5063. Dopo che il server Accesso Client reindirizza la richiesta SIP a un server cassette postali, viene creato un canale multimediali RTP o SRTP tramite un gateway VoIP, IP PBX o SBC e il processo di lavoro della messaggistica unificata di Microsoft Exchange sul server cassette postali.

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
<td><p>SIP (server Accesso Client: servizio Microsoft Call Router di messaggistica unificata)</p></td>
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
<td><p>5065 e 5067 per TCP (non protetto). 5065 e 5067 per MTLS (protetto). Se è stata impostata su doppia modalità 5066 e 5068 vengono inoltre utilizzati.</p></td>
<td><p>Non applicabile</p></td>
<td><p>Le porte non possono essere modificate.</p></td>
</tr>
<tr class="even">
<td><p>RTP (server Cassette postali - Processo di lavoro di messaggistica unificata)</p></td>
<td><p>Non applicabile</p></td>
<td><p>Porte comprese tra 1024 e 65535.</p></td>
<td><p>Porte possono essere modificate nel file di configurazione msexchangeum.config. Il file msexchangeum.config si trova nella cartella \Program Files\Microsoft\Exchange\V15\bin su un server Messaggistica unificata di Exchange 2013.</p></td>
</tr>
</tbody>
</table>


## Porte di Lync Server e la messaggistica unificata

Exchange 2013 La messaggistica unificata supporta l'attraversamento NAT (Network Address Translation) e consente il supporto RTP da un server cassette postali per essere potenzialmente inviati tramite un firewall NAT. Per il funzionamento, tuttavia, è inoltre necessario disporre Office Microsoft Communications Server 2007 R2 e Microsoft Lync Server 2010 o Microsoft Lync 2013 distribuito nell'ambiente. Se si distribuisce sia Exchange 2013 e Communications Server 2007 R2 o Microsoft Lync Server 2010 o Lync 2013 nella rete, la distribuzione consentirà server cassette postali in esecuzione il servizio messaggistica unificata di Exchange per comunicare con gli endpoint esterno di un firewall NAT. Il server cassette postali è associato a Communications Server 2007 R2, Microsoft Lync Server 2010 o pool Lync 2013 e ottiene i token di autenticazione appropriato da A / servizio di autenticazione V in un computer che funge pool Communications Server 2007 o di Lync Server specifico.

A / V Authentication service viene utilizzato per consentire nel supporto vocale RTP attraversano i dispositivi NAT e firewall. Ciò è necessario perché i gateway multimediali gestiscono solo segnalazione e non sono di trasporto voice in modo sicuro in un dispositivo NAT o firewall. Quando si configura un server Mediation Server di Communications Server 2007 R2, Lync Server 2010 o Lync 2013, si specifica l'A / V Edge server in cui l'A / V autenticazione servizio sia in esecuzione in modo che il server Mediation Server verrà sapere dove inoltrare i pacchetti multimediali in ingresso.

Per ulteriori informazioni su come distribuire Communications Server 2007 R2, Lync Server 2010 o 2013 e Exchange 2013 di messaggistica unificata, vedere le risorse seguenti:

  - [Distribuzione di panoramica della messaggistica UNIFICATA di Exchange 2013 e Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Elenco di controllo: Integrazione di messaggistica UNIFICATA di Exchange 2013 con Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)


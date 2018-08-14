---
title: 'Limiti di dimensione dei messaggi: Exchange 2013 Help'
TOCTitle: Limiti di dimensione dei messaggi
ms:assetid: b6a3840d-b821-4e53-877b-59c16be77206
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124345(v=EXCHG.150)
ms:contentKeyID: 50481491
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Limiti di dimensione dei messaggi

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-08-20_

È possibile applicare dei limiti di dimensioni ai messaggi che transitano attraverso l'organizzazione di Microsoft Exchange Server 2013. È possibile limitare la dimensione complessiva di un messaggio o dei singoli componenti di esso come, ad esempio, l'intestazione, gli allegati e il numero dei destinatari. È possibile applicare i limiti in modo globale per l'intera organizzazione Exchange oppure per un oggetto utente o connettore.

Quando si pianificano i limiti per le dimensioni dei messaggi per l'organizzazione Exchange, è necessario considerare quanto segue:

  - I limiti per le dimensioni che devono essere impostati per i messaggi in arrivo

  - I limiti per le dimensioni che devono essere impostati per i messaggi in uscita

  - La quota della cassetta postale per l'organizzazione di Exchange

  - Rapporto tra i limiti per le dimensioni impostati per i messaggi e la quota applicata per le cassette postali

  - Presenza di utenti speciali nell'organizzazione Exchange che hanno necessità di inviare o ricevere messaggi di dimensioni superiori a quelle consentite

  - Presenza nella topologia di rete di Exchange di altri sistemi di messaggistica o unità aziendali separate con limiti diversi per le dimensioni dei messaggi

Questo argomento fornisce informazioni utili per trovare la risposta giusta a queste domande.

**Sommario**

Tipi di limiti per le dimensioni dei messaggi

Ambito dei limiti

Ordine di precedenza per i limiti per le dimensioni dei messaggi

Messaggi non soggetti ai limiti di dimensioni

## Tipi di limiti per le dimensioni dei messaggi

I limiti per le dimensioni disponibili per i singoli messaggi possono essere divisi nelle seguenti categorie:

  - **Limiti dimensioni intestazione messaggi**   Questi limiti si applicano alle dimensioni complessive dei campi di intestazione presenti nei messaggi. La dimensione del corpo o degli allegati del messaggio non è considerata. Dato che i campi di intestazione sono testo normale, la dimensione dell'intestazione viene determinata dal numero di caratteri in ogni campo di intestazione e dal numero totale di campi di intestazione. Ciascun carattere di testo utilizza 1 byte.
    

    > [!NOTE]
    > Alcuni firewall di terze parti o server proxy applicano limiti di dimensione propri all'intestazione dei messaggi. I firewall di terze parti o server proxy potrebbero riscontrare difficoltà nell'elaborazione dei messaggi che contengono nomi file di allegati di lunghezza superiore ai 50&nbsp;caratteri o nomi file di allegati che contengono caratteri non US-ASCII.



  - **Limite dimensioni messaggi**   Questi limiti si applicano alle dimensioni complessive di un messaggio, inclusi intestazione, corpo del messaggio ed eventuali allegati. I limiti per le dimensioni dei messaggi possono essere impostati per i messaggi in arrivo e in uscita. Per il flusso dei messaggi interni, in Exchange viene utilizzata l'intestazione messaggi personalizzata di `X-MS-Exchange-Organization-OriginalSize:` per registrare la dimensione originale di un messaggio non appena questo entra nell'organizzazione Exchange. Ogni volta che vengono verificati i limiti delle dimensioni per il messaggio specificato, viene utilizzato il valore più basso delle dimensioni correnti per il messaggio o l'intestazione originale delle dimensioni per il messaggio. Le dimensioni del messaggio possono variare a causa della conversione del contenuto, della codifica e dell'elaborazione dell'agente.

  - **Limiti dimensioni allegati**   Questi limiti si applicano alla dimensione massima consentita di un singolo allegato di un messaggio. Il messaggio potrebbe contenere numerosi allegati che ne aumentano notevolmente la dimensione complessiva. Tuttavia, la dimensione massima dell'allegato si riferisce solo alla dimensione di un singolo allegato.

  - **Limiti destinatari**   Questi limiti si applicano al numero totale dei destinatari dei messaggi. Quando un messaggio viene composto, i destinatari sono presenti in `To:`, `Cc:` e nei campi di intestazione `Bcc:`. Quando il messaggio viene inviato per il recapito, i destinatari vengono convertiti in voci `RCPT TO:` nella busta del messaggio. Un gruppo di distribuzione viene considerato come un unico destinatario durante l'invio del messaggio.

Inizio pagina

## Ambito dei limiti

Gli ambiti dei limiti disponibili per i singoli messaggi possono essere divisi nelle seguenti categorie:

  - **Limiti organizzativi**   Questi limiti vengono applicati a tutti i server Cassette postali Exchange 2013 e Trasporto Hub Exchange 2010 e Exchange 2007 presenti nell'organizzazione. Se è installato un server Trasporto Edge nella rete perimetrale, i limiti specificati vengono applicati al server specifico.

  - **Limiti connettore**   Questi limiti si applicano a tutti i messaggi che utilizzano il connettore specifico di invio, di ricezione o esterno per il recapito dei messaggi. I connettori di invio sono definiti nel servizio Trasporto nei server Cassette postali e Trasporto Edge. I connettori di ricezione sono definiti nel servizio Trasporto nei server Cassette postali, nel servizio Trasporto front-end nei server Accesso client e nei server Trasporto Edge.

  - **Collegamenti al sito Active Directory**   Il servizio Trasporto nei server Cassette postali utilizza i siti Active Directory e i costi assegnati ai collegamenti al sito IP Active Directory come uno dei fattori per determinare il percorso di routing meno costoso tra i server Cassette postali nell'organizzazione. È possibile assegnare specifici limiti per le dimensioni dei messaggi ai collegamenti del sito Active Directory nell'ambito della propria organizzazione.

  - **Limiti server**   Questi limiti si applicano a un server Cassette postali o Trasporto Edge specifico. È possibile impostare separatamente i limiti specifici per i messaggi su ciascun server Cassette postali o Trasporto Edge.
    
    In Outlook Web App, l'impostazione del limite massimo per le dimensioni delle richieste HTTP sui server Accesso client controlla anche le dimensioni dei messaggi gli utenti Outlook Web App possono inviare.

  - **Limiti utenti**   Questi limiti si applicano a uno specifico oggetto utente, come ad esempio una cassetta postale, un contatto, un gruppo di distribuzione o una cartella pubblica.

Nelle tabelle seguenti vengono mostrati i limiti dei messaggi, con indicazioni su come configurare i limiti in Exchange Management Shell o nell'interfaccia di amministrazione di Exchange (EAC).

### Limiti dell'organizzazione

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Limite delle dimensioni</th>
<th>Valore predefinito</th>
<th>Configurazione Shell</th>
<th>Configurazione EAC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dimensione massima dei messaggi ricevuti</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>Parametro: <em>MaxReceiveSize</em></p></td>
<td><p><strong>Flusso di posta</strong> &gt; <strong>Connettori di ricezione</strong> &gt; <strong>Altre opzioni</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icona Ulteriori opzioni" alt="Icona Ulteriori opzioni" /> &gt; <strong>Impostazioni di trasporto nell'organizzazione</strong> &gt; <strong>Limiti</strong> &gt; <strong>Dimensione massima messaggio in ingresso</strong></p></td>
</tr>
<tr class="even">
<td><p>Dimensione massima dei messaggi inviati</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>Parametro: <em>MaxSendSize</em></p></td>
<td><p><strong>Flusso di posta</strong> &gt; <strong>Connettori di ricezione</strong> &gt; <strong>Altre opzioni</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icona Ulteriori opzioni" alt="Icona Ulteriori opzioni" /> &gt; <strong>Impostazioni di trasporto nell'organizzazione</strong> &gt; <strong>Limiti</strong> &gt; <strong>Dimensione massima messaggio in uscita</strong></p></td>
</tr>
<tr class="odd">
<td><p>Numero massimo di destinatari per messaggio</p>

> [!NOTE]  
> <p></p>

</td>
<td><p>5000</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>Parametro: <em>MaxRecipientEnvelopeLimit</em></p></td>
<td><p><strong>Flusso di posta</strong> &gt; <strong>Connettori di ricezione</strong> &gt; <strong>Altre opzioni</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icona Ulteriori opzioni" alt="Icona Ulteriori opzioni" /> &gt; <strong>Impostazioni di trasporto nell'organizzazione</strong> &gt; <strong>Limiti</strong> &gt; <strong>Numero massimo di destinatari</strong></p></td>
</tr>
<tr class="even">
<td><p>Dimensione massima degli allegati nelle regole di trasporto applicabili a tutti i server Cassette postali dell'organizzazione</p></td>
<td><p>Non configurato</p></td>
<td><p>Cmdlet: <strong>New-TransportRule</strong>, <strong>Set-TransportRule</strong></p>
<p>Parametro: <em>AttachmentSizeOver</em></p></td>
<td><p><strong>Flusso di posta</strong> &gt; <strong>Regole</strong> &gt; <strong>Aggiungi</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Icona Aggiungi" alt="Icona Aggiungi" /> o <strong>Modifica</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icona Modifica" alt="Icona Modifica" />.</p>
<p>Utilizzare il predicato <strong>Applica questa regola se</strong> &gt; <strong>qualsiasi allegato</strong> &gt; <strong>è maggiore di o uguale a</strong></p>
<p>Utilizzare il predicato <strong>Applica questa regola se</strong> &gt; <strong>le dimensioni</strong> &gt; <strong>del messaggio sono maggiori di o uguali a</strong></p></td>
</tr>
<tr class="odd">
<td><p>Dimensione massima dei messaggi nelle regole di trasporto applicabili a tutti i server Cassette postali dell'organizzazione</p></td>
<td><p></p></td>
<td><p>Cmdlet: <strong>New-TransportRule</strong>, <strong>Set-TransportRule</strong></p>
<p>Parametro: <em>MessageSizeOver</em></p></td>
<td><p><strong>Flusso di posta</strong> &gt; <strong>Regole</strong> &gt; <strong>Aggiungi</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Icona Aggiungi" alt="Icona Aggiungi" /> o <strong>Modifica</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icona Modifica" alt="Icona Modifica" />.</p>
<p>Utilizzare il predicato <strong>Applica questa regola se</strong> &gt; <strong>le dimensioni</strong> &gt; <strong>del messaggio sono maggiori di o uguali a</strong></p></td>
</tr>
</tbody>
</table>


Inizio pagina

### Limiti dei connettori

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Limite delle dimensioni</th>
<th>Valore predefinito</th>
<th>Configurazione Shell</th>
<th>Configurazione EAC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dimensione massima intestazione attraverso un connettore di ricezione</p></td>
<td><p>128 KB</p></td>
<td><p>Cmdlet: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Parametro: <em>MaxHeaderSize</em></p></td>
<td><p>N/D</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Dimensione massima messaggio attraverso un connettore di ricezione</p>

> [!NOTE]
> La dimensione effettiva del messaggio potrebbe essere inferiore a causa della codifica e della conversione del contenuto del messaggio.


</td>
<td><p><strong>Servizio Trasporto sui server Cassette postali</strong></p>
<p>35 MB per i connettori di ricezione predefiniti e proxy client</p>
<p><strong>Servizio di trasporto front-end nei server Accesso client</strong></p>
<p>36 MB per i connettori di ricezione front-end predefiniti e front-end proxy in uscita.</p>
<p>35 MB per il connettore di ricezione front-end client.</p></td>
<td><p>Cmdlet: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Parametro: <em>MaxMessageSize</em></p></td>
<td><p><strong>Flusso di posta</strong> &gt; <strong>Connettori di ricezione</strong> &gt; <strong>Modifica</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icona Modifica" alt="Icona Modifica" /> &gt; <strong>Generale</strong> &gt; <strong>Dimensione massima messaggio in ingresso</strong></p></td>
</tr>
<tr class="odd">
<td><p>Numero massimo di destinatari per messaggio attraverso un connettore di ricezione</p></td>
<td><p><strong>Servizio Trasporto sui server Cassette postali</strong></p>
<p>5.000 per il connettore di ricezione predefinito</p>
<p>200 il connettore di ricezione proxy client</p>
<p><strong>Servizio di trasporto front-end nei server Accesso client</strong></p>
<p>200 per i connettori di ricezione front-end predefiniti, front-end client e front-end proxy client.</p>

> [!NOTE]
> Se per un mittente anonimo viene superato il numero di destinatari, il messaggio viene accettato per i primi 200&nbsp;destinatari. La maggior parte dei server di messaggistica SMTP rileva la presenza del limite relativo ai destinatari. Il server di messaggistica SMTP continua a inviare il messaggio in gruppi di 200 destinatari fino a quando il messaggio non viene inviato a tutti i destinatari.


</td>
<td><p>Cmdlet: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Parametro: <em>MaxRecipientsPerMessage</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>Dimensione massima messaggio attraverso un connettore di invio</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet: <strong>New-SendConnector</strong>, <strong>Set-SendConnector</strong></p>
<p>Parametro: <em>MaxMessageSize</em></p></td>
<td><p><strong>Flusso di posta</strong> &gt; <strong>Connettori di invio</strong> &gt; <strong>Modifica</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icona Modifica" alt="Icona Modifica" /> &gt; <strong>Generale</strong> &gt; <strong>Dimensione massima messaggio in uscita</strong></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Dimensione massima messaggi attraverso un collegamento al sito Active Directory</p></td>
<td><p>Illimitato</p></td>
<td><p>Cmdlet: <strong>Set-AdSiteLink</strong></p>
<p>Parametro: <em>MaxMessageSize</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>Dimensione massima messaggio attraverso un connettore dell'agente di recapito</p></td>
<td><p>Illimitato</p></td>
<td><p>Cmdlet: <strong>New-DeliveryAgentConnector</strong>, <strong>Set-DeliveryAgentConnector</strong></p>
<p>Parametro: <em>MaxMessageSize</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Dimensione massima messaggio attraverso un connettore esterno</p></td>
<td><p>Illimitato</p></td>
<td><p><strong>Cmdlet: Set-ForeignConnector</strong> Parametro: <em>MaxMessageSize</em></p></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>


Inizio pagina

### Limiti dei server

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Limite delle dimensioni</th>
<th>Valore predefinito</th>
<th>Configurazione Shell</th>
<th>Configurazione EAC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dimensione massima intestazione per i messaggi contenuti nella directory di prelievo</p></td>
<td><p>64 KB</p></td>
<td><p>Cmdlet: <strong>Set-TransportService</strong></p>
<p>Parametro: <em>PickupDirectoryMaxHeaderSize</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>Numero massimo di destinatari per messaggio per i messaggi contenuti nella directory di prelievo</p></td>
<td><p>100</p></td>
<td><p>Cmdlet: <strong>Set-TransportService</strong></p>
<p>Parametro: <em>PickupDirectoryMaxRecipientsPerMessage</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Limiti delle dimensioni massime dei messaggi specifici del client per client Outlook Web App, Exchange ActiveSync e Servizi Web Exchange</p></td>
<td><p>Outlook Web App   35 MB</p>
<p>Exchange ActiveSync   10 MB</p>
<p>Servizi Web Exchange   64 MB</p>

> [!NOTE]
> A causa del sovraccarico associato alla codifica Base64, questi valori sono di circa il 33% superiori alla dimensione massima dei messaggi effettiva utilizzabile.


</td>
<td><p>Configurare i valori nel file di configurazione dell'applicazione XML web.config appropriato nei server Accesso client. Per ulteriori informazioni, vedere <a href="configure-client-specific-message-size-limits-exchange-2013-help.md">Configurare la dimensione massima dei messaggi specifici del client</a>.</p></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>


Inizio pagina

### Limiti dell'utente

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Limite delle dimensioni</th>
<th>Valore predefinito</th>
<th>Configurazione Shell</th>
<th>Configurazione EAC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dimensione massima dei messaggi che possono essere inviati a questo destinatario</p></td>
<td><p>Illimitato</p></td>
<td><p>Cmdlet:</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-RemoteMailbox</strong></p>
<p>Parametro: <em>MaxSendSize</em></p></td>
<td><p>Per le cassette postali:</p>
<p><strong>Destinatari</strong> &gt; <strong>Cassette postali</strong> &gt; <strong>Modifica</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icona Modifica" alt="Icona Modifica" /> &gt; <strong>Funzionalità delle cassette postali</strong> &gt; <strong>Flusso di posta</strong> &gt; <strong>Limitazioni nella dimensione del messaggio</strong> &gt; <strong>Visualizza dettagli</strong> &gt; <strong>Messaggi inviati</strong></p>

> [!NOTE]
> Questa impostazione non è configurabile tramite EAC per altri tipi di destinatari.


</td>
</tr>
<tr class="even">
<td><p>Dimensione massima dei messaggi che possono essere inviati a questo destinatario</p></td>
<td><p>Illimitato</p>
<p>Per i criteri di provisioning delle cassette postali del sito: 36 MB</p></td>
<td><p>Cmdlet:</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>New-SiteMailboxProvisioningPolicy</strong></p>
<p><strong>Set-SiteMailboxProvisioningPolicy</strong></p>
<p>Parametro: <em>MaxReceiveSize</em></p></td>
<td><p>Per le cassette postali:</p>
<p><strong>Destinatari</strong> &gt; <strong>Cassette postali</strong> &gt; <strong>Modifica</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icona Modifica" alt="Icona Modifica" /> &gt; <strong>Funzionalità delle cassette postali</strong> &gt; <strong>Flusso di posta</strong> &gt; <strong>Limitazioni nella dimensione del messaggio</strong> &gt; <strong>Visualizza dettagli</strong> &gt; <strong>Messaggi ricevuti</strong></p>

> [!NOTE]
> Questa impostazione non è configurabile tramite EAC per altri tipi di destinatari.


</td>
</tr>
<tr class="odd">
<td><p>Numero massimo di destinatari per messaggio inviato da questo destinatario</p></td>
<td><p>Illimitato</p></td>
<td><p>Cmdlet:</p>
<p><strong>Set-Mailbox</strong>, <strong>Set-MailUser</strong></p>
<p>Parametro: <em>RecipientLimits</em></p>
<p></p></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Ordine di precedenza per i limiti per le dimensioni dei messaggi

È possibile impostare limiti differenti per le dimensioni dei messaggi a livelli differenti dell'organizzazione Exchange. Quando un messaggio viene instradato attraverso l'infrastruttura di trasporto, potrebbe essere sottoposto a varie differenti restrizioni in termini di dimensioni. È consigliabile definire i limiti per le dimensioni dei messaggi in modo tale che i messaggi che transitano nella pipeline di trasporto vengano respinti il più presto possibile, qualora violino i limiti imposti. In generale, è consigliabile impostare limiti più stretti nei punti in cui i messaggi accedono all'infrastruttura. Ad esempio, i limiti per le dimensioni dei messaggi impostati sui connettori di ricezione che ricevono i messaggi da Internet dovrebbero essere minori o uguali ai limiti configurati all'interno dell'organizzazione Exchange. Accettare ed elaborare un messaggio proveniente da Internet e sicuramente destinato a essere rifiutato dal servizio Trasporto nei server Cassette postali costituirebbe infatti un dispendio inutile di risorse di sistema per il server Exchange. Verificare che i limiti per connettori, server e organizzazione siano configurati in modo tale da ridurre al minimo le elaborazioni inutili di messaggi.

In quest'ottica, l'eccezione è rappresentata dai limiti per gli utenti. I limiti a livello di utenti hanno la precedenza su quelli a livello di messaggi. Pertanto, è possibile specificare che un utente è autorizzato a superare i limiti per le dimensioni dei messaggi definiti per l'organizzazione. Ad esempio, è possibile permettere a uno specifico gruppo di cassette postali di determinati utenti di inviare messaggi di dimensioni maggiori rispetto al resto dell'organizzazione configurando limiti di invio e ricezione personalizzati per quelle cassette postali.

Le eccezioni relative ai limiti utente si applicano solo agli scambi di messaggi tra utenti autenticati. Se un utente invia o riceve un messaggio via Internet, verranno applicati i limiti dell'organizzazione. Si supponga ad esempio che per le dimensioni dei messaggi dell'organizzazione sia impostato un limite di 10 MB, ma che gli utenti del reparto marketing siano configurati per inviare e ricevere messaggi fino a 50 MB. Tali utenti saranno in grado di scambiarsi messaggi di grandi dimensioni, ma non potranno ricevere messaggi di grandi dimensioni via Internet, perché questi ultimi provengono da mittenti non autenticati.

Inizio pagina

## Messaggi non soggetti ai limiti di dimensioni

Nel seguente elenco sono indicati i tipi di messaggi generati da un server Cassette postali o Trasporto Edge e che non sono soggetti ai limiti definiti per le dimensioni dei messaggi:

  - Messaggi di sistema

  - Messaggio generato dall'agente

  - Messaggi DSN (Delivery Status Notification)

  - Messaggi rapporto del journal

  - Messaggi in quarantena

Tuttavia, questi messaggi sono comunque soggetti al limite massimo di destinatari per messaggio impostato per l'organizzazione.

Inizio pagina


---
title: 'Consenti messaggio in attesa di indicatore: Exchange 2013 Help'
TOCTitle: Consenti messaggio in attesa di indicatore
ms:assetid: 57fb439e-8208-499f-a20b-814677843a8c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298001(v=EXCHG.150)
ms:contentKeyID: 54652865
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consenti messaggio in attesa di indicatore

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-03-09_

L'indicatore di messaggi in attesa è una funzionalità presente nella maggior parte dei sistemi di casella vocale legacy. Consente agli utenti di essere informati sulla presenza di messaggi di casella vocale nuovi o non ascoltati. Nella modalità più comune, tale funzionalità comporta l'accensione di una spia sul telefono dell'utente che indica la presenza di un messaggio vocale nuovo o non ascoltato.

**Sommario**

Panoramica

The Mailbox server's role in MWI

MWI SIP NOTIFY messages

MWI resilience

MWI administration

Text message (SMS) notifications for voice mail messages and missed calls

## Panoramica

È possibile che le notifiche dell'indicatore di messaggi in attesa includano qualsiasi meccanismo che indichi l'esistenza di un messaggio vocale nuovo o non ascoltato. Il messaggio può essere in un nuovo messaggio di posta elettronica o in un messaggio contrassegnato come non letto. È possibile che le notifiche dell'indicatore di messaggi in attesa si presentino in una delle seguenti forme:

  - Un nuovo messaggio vocale visualizzato da Microsoft Outlook o da Outlook Web App.

  - Un messaggio di testo o SMS (Short Messaging Service) inviati ad un telefono cellulare configurato per ricevere messaggi di testo.

  - Una chiamata in uscita effettuata dal servizio Messaggistica unificata di Exchange.

  - Una spia luminosa sul telefono.

  - Un segnale di chiamata speciale.

  - Icone o pulsanti sul display di un telefono.

  - Una notifica evidenziata all'interno di un'applicazione software.

Nella messaggistica unificata la casella vocale dell'utente è archiviata in una cassetta postale. È possibile accedervi da un telefono utilizzando Outlook Voice Access, da un computer desktop o portatile tramite Outlook o Outlook Web App e, infine, da utenze di telefonia cellulare. Quando un utente riceve un nuovo messaggio vocale, questo viene visualizzato nella relativa cartella di casella vocale. Se si accede al messaggio vocale utilizzando Outlook o Outlook Web App, un messaggio di posta elettronica viene incluso insieme al messaggio vocale.

Poiché le versioni precedenti di Messaggistica unificata erano distribuite in una organizzazione, l'indicatore di messaggi in attesa era supportato in un ambiente tradizionale del gateway VoIP oppure in un ambiente IP PBX grazie ad una soluzione o applicazione di terze parti; poteva anche essere incluso nella messaggistica unificata di Exchange. Nella versione di Exchange 2010 e successive, l'indicatore di messaggi in attesa è supportato anche nel caso in cui la messaggistica unificata sia distribuita con Microsoft Lync Server. Il meccanismo di notifica dell'indicatore di messaggi in attesa, in uso su Lync Server, dipende dal tipo di telefono VoIP utilizzato da un'utenza abilitata su Enterprise Voice e Messaggistica Unificata. È possibile trovare tale meccanismo in uno dei seguenti dispositivi:

  - Un telefono

  - Il display di un telefono

  - Un pulsante della tastiera

Per impostazione predefinita, l'indicatore di messaggi in attesa è attivato per tutti gli utenti abilitati nella messaggistica unificata. È controllato attraverso le impostazioni su un criterio cassetta postale o sui gateway IP di messaggistica unificata, creati e collegati a un dial plan della stessa. L'indicatore di messaggi in attesa funziona anche con messaggi vocali protetti.

Per implementare l'indicatore di messaggi in attesa in un ambiente di telefonia tradizionale con i gateway VoIP, IP PBX o i PBX per SIP, un server Cassette postali che esegue il servizio di messaggistica unificata di Microsoft Exchange invia un messaggio SIP NOTIFY dell'indicatore stesso a un *peer SIP* equivalente a un IP PBX, un gateway VoIP utilizzato con un sistema legacy PBX, un PBX per SIP o, se è stato implementato Lync Server, a un server Lync. IP PBX o PBX accendono la spia sul telefono da scrivania per notificare all'utente la presenza di un messaggio vocale nuovo o non ascoltato.

I chiamanti possono lasciare messaggi vocali in due modi differenti: rispondendo alle chiamate e con Outlook Voice Access. Con la risposta alle chiamate, un server Cassette postali risponde a una chiamata in arrivo e consente al chiamante di lasciare un messaggio vocale a un utente. Con Outlook Voice Access, quando si compone un numero con Outlook Voice Access, è possibile lasciare con il menu di sistema un messaggio vocale a un utente abilitato alla messaggistica unificata.

Inizio pagina

## Il ruolo del server Cassette postali nell'indicatore di messaggi in attesa

Quando viene chiamato un utente abilitato alla messaggistica unificata e lo stesso non risponde al telefono, il servizio di messaggistica unificata di Microsoft Exchange riceve dall'indicatore di messaggi in attesa la segnalazione del cambiamento dello stato e utilizza un messaggio SIP NOTIFY per inviare la richiesta per il cambiamento di notifica a un gateway VoIP, IP PBX o PBX per SIP. Il cambiamento di notifica contiene le seguenti informazioni:

  - Indicatore di messaggi in attesa abilitato (sì o no).

  - Numero di nuovi messaggi vocali o messaggi vocali non ascoltati.

  - Numero dei vecchi messaggi vocali o messaggi contrassegnati come ascoltati.

  - Numero di nuovi messaggi vocali urgenti o messaggi vocali urgenti non ascoltati.

  - Numero di vecchi messaggi vocali urgenti o messaggi vocali urgenti contrassegnati come ascoltati.

  - Il numero di interno principale sul dial plan di messaggistica unificata principale.

  - L'indirizzo IP o il nome di dominio completo (FQDN) del peer SIP che vengono utilizzati per i messaggi SIP NOTIFY.

  - Il tipo di sicurezza del dial plan di messaggistica unificata (non protetto, SIP con protezione o protetto). Tali informazioni verranno utilizzate per stabilire se sia necessario che la connessione al gateway VoIP o a IP PBX sia SIP su TCP o SIP su TLS. TLS (Transport Layer Security) è supportato per SIP NOTIFY dell'indicatore di messaggi in attesa.

Il server Cassette postali utilizza le informazioni sulla deviazione nell'intestazione della chiamata in entrata per stabilire il numero di interno o il numero di telefono dell'utente abilitato alla messaggistica unificata. Stabilito il numero di interno o di telefono, il server Cassette postali invia la richiesta per il SIP peer. Il peer SIP quindi modifica lo stato dell'indicatore di messaggi in attesa e attiva la notifica sul telefono dell'utente.


> [!NOTE]
> Sebbene le interruzioni PBX siano rare, la messaggistica unificata aggiorna automaticamente lo stato dell'indicatore di messaggi in attesa per tutte le cassette postali almeno una volta ogni 12 ore. Non è possibile forzare un aggiornamento ma se il PBX o l'IP PBX vengono disattivati e tutte le spie dell'indicatore di messaggi in attesa si spengono, è necessario un massimo di 6 ore prima che venga ripristinato lo stato corrente per le spie.



Inizio pagina

## Messaggi SIP NOTIFY dell'indicatore di messaggi in attesa

Le notifiche dell'indicatore di messaggi in attesa utilizzano i messaggi SIP NOTIFY per comunicare con i peer SIP. Le informazioni sul cambiamento dello stato dell'indicatore del messaggio in attesa vengono incluse nel messaggio SIP NOTIFY ed indicano l'invio alle utenze delle notifiche dell'indicatore stesso. Ogni volta che viene modificato qualcosa nello stato dell'indicatore dei messaggi in attesa, il servizio di Assistente cassette postali invia queste informazioni al servizio di messaggistica unificata di Microsoft Exchange in esecuzione su un server Cassette postali. Una volta che il server Messaggistica unificata riceve tali informazioni, analizza il messaggio per ottenere il peer SIP o il gateway IP di destinazione e le informazioni sul cambiamento dello stato dell'indicatore dei messaggi in attesa. Viene creato, quindi, un messaggio SIP NOTIFY con le informazioni sul cambiamento dello stato dell'indicatore dei messaggi in attesa nel corpo del messaggio e vengono inviate tali informazioni al peer SIP.

L'indicatore dei messaggi in attesa si basa su RFC 3842 che indica, a sua volta, le notifiche relative all'evento SIP da utilizzare per le notifiche dei messaggi in attesa. L'indicatore dei messaggi in attesa si basa sul modello SIP ed è controllato dagli endpoint presenti in un sistema di messaggistica unificata. Gli endpoint SIP, detti anche peer SIP, che ottengono le informazioni dell'indicatore inviano un messaggio SIP SUBSCRIBE al servizio di messaggistica unificata. Il servizio risponde con un messaggio NOTIFY che indica l'accettazione della sottoscrizione. Tutte le informazioni sul cambiamento dello stato dell'indicatore dei messaggi in attesa verranno trasmesse dal sistema di messaggistica unificata a un endpoint SIP utilizzando i messaggi NOTIFY incorporati all'interno della sottoscrizione precedentemente creata. La sintassi esatta del messaggio SIP NOTIFY da inviare al peer SIP si basa sul formato descritto in RFC 3842.

Quando il servizio di messaggistica unificata su un server Cassette postali invia un messaggio NOTIFY dell'indicatore al peer SIP, l'intestazione dell'evento è impostata sul "riepilogo del messaggio", che indica che si tratta di un messaggio NOTIFY relativo all'indicatore stesso. Il campo di intestazione A indica l'endpoint SIP per cui è necessario fornire il servizio dell'indicatore di messaggi in attesa. È necessario che l'intestazione Sottoscrizione-Stato sia impostata su "terminata" invece che su "attiva". In risposta al messaggio SIP NOTIFY si verificano le seguenti azioni:

1.  Il peer SIP trasmette tali informazioni al PBX utilizzando un protocollo a commutazione di circuiti, quale SMDI.

2.  Il PBX invia un messaggio di operazione riuscita tramite un protocollo a commutazione di circuiti.

3.  È possibile che il peer SIP risponda con uno dei seguenti messaggi: 200 OK (operazione riuscita) o 480 (temporaneamente non disponibile). Un server Messaggistica unificata è in grado di gestire sia tali risposte sia ulteriori risposte di errore.

## L'indicatore dei messaggi in attesa in un ambiente di telefonia tradizionale

In un ambiente di telefonia tradizionale, una chiamata in arrivo viene ricevuta dal PBX e quindi inviata al gateway VoIP oppure viene ricevuta da IP PBX o da un PBX abilitato al SIP. Il server e il servizio Assistente di Cassette postali vengono utilizzati al fine di stabilire lo stato dell'indicatore dei messaggi in attesa per l'utente abilitato alla messaggistica unificata. Ambedue sono funzionali a recapitare la notifica SIP al gateway VoIP, al PBX legacy, a IP PBX o al PBX abilitato al SIP.

In un ambiente di telefonia tradizionale, il flusso di chiamate e la notifica dell'indicatore dei messaggi in attesa sono come indicato di seguito:

1.  La chiamata in arrivo viene ricevuta dal PBX legacy, trasmessa al gateway VoIP oppure a un IP PBX o ad PBX per SIP e, quindi, inoltrata al numero di interno dell'utente abilitato alla messaggistica unificata. L'utente non risponde e viene richiesto al chiamante di lasciare un messaggio vocale.

2.  Il gateway VoIP o un IP PBX inoltrano la chiamata a un server Cassette postali su cui è in esecuzione il servizio Messaggistica unificata di Microsoft Exchange.

3.  Il server Cassette postali esegue una query LDAP per ottenere le informazioni sull'utente abilitato alla messaggistica unificata come il numero di interno e i messaggi di saluto personali. I messaggi di saluto per l'utente di messaggistica unificata vengono riprodotti.

4.  Il messaggio vocale, creato dal servizio di messaggistica unificata, viene inviato al servizio di trasporto di Microsoft Exchange sullo stesso server Cassette postali.

5.  Servizio di trasporto sul server cassette postali invia il messaggio vocale per il server cassette postali contenente cassetta postale dell'utente. L'Assistente per la cassetta postale riceve un evento MAPI per un nuovo messaggio.

6.  Il servizio Assistente cassette postali legge il dial plan di messaggistica unificata e il criterio cassetta postale di messaggistica unificata per stabilire se sia necessario che le notifiche dell'indicatore dei messaggi in attesa vengano inviate all'utente abilitato alla messaggistica unificata. Il servizio Assistente cassette postali interroga tutti i server di Cassette postali associati al dial plan di messaggistica unificata dell'utente abilitato alla stessa. Il servizio Assistente cassette postali tenta di inviare l'evento RPC al primo server di Cassette postali restituito. In caso di errore, il servizio tenta con quello successivo. Il servizio continua a provare per 5 minuti oppure fino a quando non ha tentato su tutti i server Cassette postali. Se tutte le chiamate RPC non riescono, il servizio Assistente cassette postali registra l'errore nel Visualizzatore eventi. Il server Cassette postali interroga tutti i gateway IP di messaggistica unificata associati al dial plan di messaggistica unificata della cassetta postale dell'utente abilitato alla messaggistica unificata.

7.  Il server Messaggistica unificata invia un messaggio SIP NOTIFY ottenuto dalla query al primo gateway IP o a un IP PBX. In caso di errore, il server Cassette postali opta per il successivo gateway IP o IP PBX. Il server Cassette postali continua a provare l'invio per 5 minuti a un gateway VoIP o IP PBX. Se tutti i tentativi di trovare un gateway VoIP o IP PBX non riescono, il server Cassette postali registra un errore. Se viene individuato un gateway VoIP o IP PBX, questo invia la notifica al PBX e il PBX, a sua volta, invia una notifica dell'evento dell'indicatore dei messaggi in attesa al telefono dell'utente affinché venga accesa la spia sul telefono. Se viene utilizzo un IP PBX, la notifica dell'indicatore viene elaborata da IP PBX in modo che la spia sul telefono dell'utente venga accesa. Ulteriori meccanismi di notifica dell'indicatore dei messaggi in attesa sono elencati nella sezione Panoramica. Il tipo di notifica dipende dal fornitore hardware di PBX o IP PBX e dalla scelta di utilizzare Lync Server. Dipende inoltre dalla scelta di utilizzare un telefono analogico, digitale o VoIP.

Inizio pagina

## L'indicatore dei messaggi in attesa in un ambiente Lync Server

In ambienti di telefonia che comprendono Lync Server, una chiamata in arrivo può essere inviata da un telefono esterno verso un Mediation Server, da un client Lync oppure da un telefono basato su VoIP o su comunicazioni unificate (UC, Unified Communications). Una volta ricevuta la chiamata, questa viene inviata al pool di server front-end Lync Server. Il server Cassette postali e il servizio Assistente cassette postali vengono utilizzati per determinare lo stato dell'indicatore dei messaggi in attesa per l'utente abilitato alla messaggistica unificata al fine di recapitare la notifica al client Lync o a un telefono analogico, digitale, VoIP o basato su comunicazioni unificate.

In un ambiente di telefonia con Lync Server, la notifica relativa al flusso di chiamate e all'indicatore dei messaggi in attesa è la seguente:

1.  La chiamata viene inviata da uno dei seguenti dispositivi:
    
      - Da un telefono esterno all'organizzazione (chiamata inviata a Mediation Server)
    
      - Da un client Lync
    
      - Da un telefono VoIP o basato su comunicazioni unificate

2.  La chiamata in entrata viene ricevuta dal pool di server front-end Lync Server e inviata al telefono o all'endpoint SIP dell'utente abilitato alla messaggistica unificata. L'utente non risponde e viene richiesto al chiamante di lasciare un messaggio vocale.

3.  Il pool di server front-end Lync Server inoltra la chiamata al server Cassette postali all'interno della rete locale in modo che la cassetta postale dell'utente venga trovata.

4.  Il server Cassette postali invia una query LDAP per ottenere le informazioni sull'utente abilitato alla messaggistica unificata, quali il relativo numero di interno e i saluti. I saluti vengono riprodotti e viene richiesto al chiamante di lasciare un messaggio vocale.

5.  Il messaggio vocale, creato dal servizio di messaggistica unificata, è trasmesso al servizio di trasporto sullo stesso server Cassette postali all'interno del relativo sito.

6.  Il servizio di trasporto trasmette il messaggio vocale al server Cassette postali che contiene la cassetta postale dell'utente. Il servizio Assistente cassette postali riceve un evento MAPI per un nuovo messaggio vocale.

7.  Il servizio Assistente cassette postali legge il dial plan di messaggistica unificata e il criterio cassetta postale di messaggistica unificata per decidere se le notifiche MWI devono essere inviate all'utente. Il servizio Assistente cassette postali interroga tutti i server Cassette postali associati al dial plan di messaggistica unificata dell'utente. Il servizio Assistente cassette postali tenta di inviare l'evento RPC al primo server di Cassette postali restituito. Se il tentativo non riesce, il servizio Assistente cassette postali tenta con il successivo. Il servizio continua a cercare un server di Cassette postali per 5 minuti o fino a quando non avrà tentato su tutti i server. Se tutte le chiamate RPC falliscono, il servizio Assistente cassette postali registra un errore nel Visualizzatore eventi. Il server Cassette postali interroga Active Directory per tutti i gateway IP di messaggistica unificata associati al dial plan di messaggistica unificata dell'utente abilitato alla messaggistica unificata.

8.  Messaggistica unificata invia un messaggio SIP NOTIFY al primo gateway VoIP o IP PBX ottenuto in seguito alla query. In caso di errore, il server Cassette postali opta per il successivo gateway VoIP o IP PBX. Il server Cassette postali continua a cercare per 5 minuti un gateway VoIP o IP PBX. Se tutti i tentativi di contattare il gateway VoIP o IP PBX non riescono, il server Cassette postali registra un errore. Se il tentativo riesce, il gateway VoIP o IP PBX invia la notifica al pool di server front-end Lync Server che, a sua volta, inoltra una notifica dell'evento dell'indicatore dei messaggi in attesa a un endpoint SIP utilizzato dall'utente, dal telefono dello stesso o dal client Lync.

Inizio pagina

## Resilienza dell'indicatore dei messaggi in attesa

Quando si distribuiscono server Cassette postali, server Accesso client, dial plan di messaggistica unificata e gateway IP di messaggistica unificata e si utilizza l'indicatore di messaggi in attesa per gli utenti abilitati alla messaggistica unificata, è preferibile distribuire più server di Cassette postali e Accesso client e più gateway VoIP e IP PBX per creare la resilienza e la tolleranza all'errore. In questo modo si ottiene anche la resilienza dell'indicatore di messaggi in attesa poiché questo mette a disposizione diversi modi per inviare notifiche dell'indicatore, così come descritto nella sezione precedente.

Per abilitare la tolleranza di errore per l'indicatore dei messaggi in attesa in Messaggistica unificata, è necessario creare e configurare uno o più dei seguenti elementi:

  - Un dial plan di messaggistica unificata collegato all'utente abilitato alla messaggistica unificata che riceve le notifiche dell'indicatore di messaggi in attesa.

  - Un criterio cassetta postale di messaggistica unificata collegato all'utente abilitato alla messaggistica unificata che riceve le notifiche dell'indicatore di messaggi in attesa.

  - Un gateway IP di messaggistica unificata collegato al dial plan di messaggistica unificata, collegato, a sua volta, all'utente abilitato alla messaggistica unificata che riceve le notifiche dell'indicatore di messaggi in attesa.

  - Se viene utilizzato Lync Server, è necessario aggiungere tutti i server Accesso client e Cassette postali al dial plan URI SIP di messaggistica unificata collegato con l'utente abilitato alla messaggistica unificata che riceve le notifiche dell'indicatore di messaggi in attesa.

## Amministrazione dell'indicatore di messaggi in attesa.

È possibile amministrare l'indicatore di messaggi in attesa configurando le impostazioni su due componenti della messaggistica unificata: Criteri cassette postali di messaggistica unificata e gateway IP di messaggistica unificata. Per entrambi i componenti di messaggistica unificata, è possibile abilitare o disabilitare le notifiche dell'indicatore dei messaggi in attesa tramite il cmdlet **Set-UMMailboxPolicy** o il cmdlet **Set-UMIPgateway** in Exchange Management Shell. È inoltre possibile configurare le impostazioni utilizzando l'interfaccia di amministrazione di Exchange. È possibile visualizzare lo stato della notifica dell'indicatore dei messaggi in attesa utilizzando il cmdlet **Get-UMMailboxPolicy** e il cmdlet **Get-UMIPgateway** in Shell oppure visualizzando le impostazioni nell'interfaccia di amministrazione di Exchange.

## I criteri cassetta postale di messaggistica unificata e l'indicatore dei messaggi in attesa

È possibile creare un criterio cassetta postale di messaggistica unificata per applicare un insieme comune di impostazioni dei criteri di messaggistica unificata a un insieme di cassette postali abilitate alla messaggistica unificata. Ad esempio, è possibile utilizzare un criterio cassetta postale di messaggistica unificata per applicare le impostazioni dei criteri PIN, le restrizioni di composizione e le impostazioni delle notifiche nell'indicatore di messaggi in attesa. Se si abilita o disabilita l'indicatore di messaggi in attesa su un criterio cassetta postale di messaggistica unificata, questo viene abilitato o disabilitato per tutti gli utenti della messaggistica unificata associati al criterio cassetta postale di messaggistica unificata. L'impostazione dell'indicatore di messaggi in attesa viene applicato a un sottoinsieme degli utenti associati a un dial plan di messaggistica unificata. Per maggiori informazioni sui criteri cassetta postale di messaggistica unificata, inclusa la modalità di abilitazione o disabilitazione dell'indicatore di messaggi in attesa per un gruppo di utenti abilitati alla messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

È possibile utilizzare l'interfaccia di amministrazione di Exchange o il cmdlet **Set-UMMailboxPolicy** in Shell per configurare l'impostazione dell'indicatore di messaggi in attesa, come illustrato nella tabella seguente.

### L'impostazione dell'indicatore di messaggi in attesa su un criterio cassetta postale di messaggistica unificata

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro Shell</th>
<th>Impostazione disponibile nell'interfaccia di amministrazione di Exchange</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowMessageWaitingIndicator</em></p></td>
<td><p>Sì</p></td>
<td><p>Il parametro <em>AllowMessageWaitingIndicator</em> indica se gli utenti associati al criterio cassetta postale di messaggistica unificata sono in grado di ricevere le notifiche dell'indicatore di messaggi in attesa in caso di ricezione di un nuovo messaggio vocale. Il valore predefinito è <code>$true</code>.</p>
<p>L'abilitazione di tale impostazione consente l'invio di notifiche dell'indicatore di messaggi in attesa agli utenti associati a un singolo criterio cassetta postale di messaggistica unificata per le chiamate ricevute da un gateway IP di messaggistica unificata. Tale impostazione consente al gateway IP di messaggistica unificata di ricevere e inviare messaggi SIP NOTIFY ai telefoni degli utenti abilitati alla messaggistica unificata o agli endpoint SIP.</p>
<p></p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su come gestire le impostazioni dell'indicatore di messaggi in attesa, vedere i seguenti argomenti:

  - [Gestire i criteri cassetta postale di messaggistica unificata](manage-a-um-mailbox-policy-exchange-2013-help.md)

  - [Abilitare i messaggi in attesa indicatore (MWI) per gli utenti](enable-message-waiting-indicator-mwi-for-users-exchange-2013-help.md)

  - [Disattivare i messaggi in attesa indicatore (MWI) per gli utenti](disable-message-waiting-indicator-mwi-for-users-exchange-2013-help.md)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/it-it/library/bb124903\(v=exchg.150\))

## I gateway IP di messaggistica unificata e l'indicatore di messaggi in attesa

Se si disabilita l'indicatore di messaggi in attesa su un gateway IP di messaggistica unificata, verranno disabilitate le notifiche dell'indicatore per tutti gli utenti che effettuano la connessione al gateway VoIP o IP PBX rappresentati dal gateway IP di messaggistica unificata. La disabilitazione dell'indicatore di messaggi in attesa su un singolo gateway IP di messaggistica unificata, collegato a un dial plan di messaggistica unificata, è in grado di disabilitare le notifiche dell'indicatore di messaggi in attesa per tutti gli utenti abilitati alla messaggistica unificata associati a un unico o diversi dial plan di un unico o diversi criteri cassetta postale di messaggistica unificata. Per maggiori informazioni sui criteri cassetta postale di messaggistica unificata, inclusa la modalità di abilitazione o disabilitazione dell'indicatore di messaggi in attesa per un gruppo di utenti abilitati alla messaggistica unificata, vedere [Gestire i criteri cassetta postale di messaggistica unificata](manage-a-um-mailbox-policy-exchange-2013-help.md).

È possibile utilizzare l'interfaccia di amministrazione di Exchange o il cmdlet **Set-UMMailboxPolicy** in Shell per configurare l'impostazione dell'indicatore di messaggi in attesa, come illustrato nella tabella seguente.

### Impostazione dell'indicatore di messaggi in attesa su un gateway IP di messaggistica unificata

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro Shell</th>
<th>Impostazioni disponibili nell'interfaccia di amministrazione di Exchange</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>MessageWaitingIndicatorAllowed</em></p></td>
<td><p>Sì</p></td>
<td><p>Il parametro <em>MessageWaitingIndicatorAllowed</em> consente di specificare se abilitare il gateway IP di messaggistica unificata per inviare i messaggi SIP NOTIFY agli utenti associati a un dial plan di messaggistica unificata. Il valore predefinito è <code>$true</code>.</p>
<p>Quando viene abilitata tale impostazione, è possibile inviare notifiche di caselle vocali agli utenti per le chiamate ricevute dal gateway IP di messaggistica unificata. Tale impostazione consente al gateway IP di messaggistica unificata di inviare notifiche di messaggi in attesa agli utenti abilitati alla messaggistica unificata.</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su come gestire le impostazioni dell'indicatore di messaggi in attesa, vedere i seguenti argomenti:

  - [Gestire un gateway IP di messaggistica unificata](manage-a-um-ip-gateway-exchange-2013-help.md)

  - [Consenti messaggio in attesa indicatore (MWI) su un gateway IP di messaggistica unificata](allow-message-waiting-indicator-mwi-on-a-um-ip-gateway-exchange-2013-help.md)

  - [Impedire a messaggi in attesa indicatore (MWI) su un gateway IP di messaggistica unificata](prevent-message-waiting-indicator-mwi-on-a-um-ip-gateway-exchange-2013-help.md)

  - [Set-UMIPGateway](https://technet.microsoft.com/it-it/library/aa996577\(v=exchg.150\))

Inizio pagina

## Le notifiche SMS per i messaggi vocali e le chiamate senza risposta.

Come accennato in precedenza, una notifica dell'indicatore di messaggi in attesa è un qualsiasi meccanismo che indica la presenza di un nuovo messaggio vocale. Oltre ai meccanismi già discussi, è possibile che agli utenti arrivi una notifica tramite un SMS che indica un messaggio vocale in attesa. Questa notifica dell'indicatore per nuovi messaggi vocali è un modo diverso rispetto a quelli più tradizionali come la spia luminosa o altri meccanismi.

Un SMS inviato a un telefono cellulare quando un chiamante lascia un nuovo messaggio vocale. Gli utenti possono inoltre ricevere una notifica tramite messaggio di testo nel caso in cui non rispondano a una chiamata telefonica o quando non è stato lasciato un messaggio vocale. L'SMS di notifica della chiamata senza risposta può essere inviato all'utente insieme alla notifica del nuovo messaggio vocale.


> [!NOTE]
> L'SMS inviato a un utente include un'anteprima del messaggio vocale.



Le notifiche SMS utilizzano impostazioni diverse rispetto alle impostazioni dell'indicatore di messaggi in attesa sul gateway IP di messaggistica unificata o sul criterio cassette postali di messaggistica unificata. È possibile configurare le notifiche SMS per i nuovi messaggi vocali e le chiamate senza risposta sui criteri cassette postali e sulle cassette postali di messaggistica unificata. È possibile abilitare o disabilitare le notifiche SMS mediante i cmdlet **Set-UMMailboxPolicy** e **Set-UMMailbox** all'interno di Shell. È possibile visualizzare lo stato delle notifiche SMS utilizzando i cmdlet **Get-UMMailboxPolicy** e **Get-UMMailbox**. Non è possibile configurare le notifiche SMS nell'interfaccia di amministrazione di Exchange.

La tabella seguente mostra il parametro da configurare su una cassetta postale di messaggistica unificata per un utente che desidera ricevere gli SMS alla casella vocale e le notifiche di chiamata senza risposta:

### Le impostazioni per le notifiche SMS su una cassetta postale

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><em>UMSMSNotificationOption</em></p></td>
<td><p>No</p></td>
<td><p>Il parametro <em>UMSMSNotificationOption</em> consente di specificare se un utente abilitato alla messaggistica unificata sia in grado di ricevere notifiche SMS esclusivamente per le caselle vocali o per le chiamate alle caselle vocali e quelle senza risposta oppure se non possa ricevere alcuna notifica. I valori di questo parametro sono: <code>VoiceMail</code>, <code>VoiceMailAndMissedCalls</code> e <code>None</code>. Il valore predefinito è <code>None</code>.</p>
<p></p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su come gestire le impostazioni di notifica SMS sulla casetta postale di un utente, vedere di seguito:

  - [Gestire le impostazioni della posta vocale di un utente](manage-voice-mail-settings-for-a-user-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/it-it/library/bb124893\(v=exchg.150\))

La tabella seguente mostra il parametro da configurare su un criterio di messaggistica unificata per un utente che desidera ricevere gli SMS per la casella vocale e le notifiche di chiamata senza risposta:

### Le impostazioni delle notifiche di SMS e delle chiamate senza risposta su un criterio di messaggistica unificata

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro Shell</th>
<th>Impostazioni disponibili nell'interfaccia di amministrazione di Exchange</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowSMSNotification</em></p></td>
<td><p>No</p></td>
<td><p>Il parametro <em>AllowSMSNotification</em> consente di specificare se gli utenti abilitati alla messaggistica unificata le cui cassette postali sono associate al criterio cassetta postale di messaggistica unificata siano in grado di ricevere notifiche SMS sui relativi telefoni cellulari. Se questo parametro è impostato su <code>$true</code>, è necessario utilizzare anche il cmdlet <strong>Set-UMMailbox</strong> e impostare il parametro <em>UMSMSNotificationOption</em> per l'utente abilitato alla messaggistica unificata su <code>voicemail</code> oppure su <code>VoiceMailAndMissedCalls</code>. Il valore predefinito è <code>$true</code>.</p>
<p></p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su come gestire le impostazioni dell'indicatore di messaggi in attesa, vedere di seguito:

  - [Gestire i criteri cassetta postale di messaggistica unificata](manage-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/it-it/library/bb124903\(v=exchg.150\))

Al fine di una corretta ricezione delle notifiche SMS per la casella vocale e le chiamate senza risposta, è necessario eseguire le seguenti operazioni:

1.  Utilizzare l'interfaccia di amministrazione di Exchange o Management Shell per abilitare l'utente alla messaggistica unificata e collegarlo al corretto criterio cassetta postale di messaggistica unificata.

2.  Sul criterio cassetta postale di messaggistica unificata associato all'utente, verificare che il parametro *AllowSMSNotification* sia impostato su `$true`. Per impostare il parametro su `$true`, eseguire il comando seguente: `Set-UMMailboxPolicy -id MyUMMailboxPolicy - AllowSMSNotification $true`.

3.  Sulla cassetta postale dell'utente, abilitare le notifiche SMS impostando il parametro *UMSMSNotificationOption* su `VoiceMailAndMissedCalls` o su `VoiceMail`.

4.  Poiché l'impostazione predefinita è `None`, è necessario eseguire il seguente comando da Shell e impostare l'opzione di notifica del messaggio SMS su `VoiceMailAndMissedCalls` o su `VoiceMail`. Ad esempio: `Set-UMMailbox- -id MyUMMailbox -UMSMSNotificationOption VoiceMailAndMissedCalls`.
    

    > [!IMPORTANT]
    > È necessario che il parametro <EM>AllowSMSNotification</EM> sul criterio cassetta postale della messaggistica unificata e il parametro <EM>UMSMSNotificationOption</EM> sulla cassetta postale dell'utente siano impostati su <CODE>$true</CODE> affinché le notifiche SMS funzionino correttamente.



Oltre alla configurazione del criterio cassetta postale di messaggistica unificata e della cassetta postale dell'utente, funzionali all'abilitazione delle notifiche SMS per il nuovo messaggio vocale e le chiamate senza risposta, è necessario che l'utente abiliti e configuri le notifiche SMS quando si accede a Outlook Web App. Per impostare e configurare le notifiche SMS, è necessario compiere le seguenti operazioni:

1.  Accedere in Outlook Web App e andare a **Opzioni** \> **Cellulare** \> **Casella vocale**.

2.  Nella pagina di **Casella vocale**, in **Notifiche**, fare clic su **Configura notifiche**.

3.  Nella pagina **Invio di SMS**, fare clic sul pulsante **Attiva notifiche**.
    

    > [!WARNING]
    > Non fare clic su <STRONG>Notifiche di casella vocale</STRONG> dal momento che riporta alla pagina <STRONG>Casella Vocale</STRONG>.



4.  Nella pagina **Invio di SMS**, in **Impostazioni locali**, selezionare dall'elenco a discesa le impostazioni locali o la posizione dell'operatore di telefonia mobile per l'invio SMS.

5.  Nella pagina **Invio SMS**, in **Operatore di telefonia mobile**, selezionare dall'elenco a discesa l'operatore di telefonia mobile per l'invio SMS, quindi fare clic su **Avanti**.

6.  Nella pagina **Messaggistica di testo**, alla finestra **Immetti il numero di telefono e fai clic su Avanti**, immettere il numero di telefono cellulare utilizzato per le notifiche dei messaggi, quindi fare clic su **Avanti**. Viene inviato un codice a sei cifre al telefono cellulare. Se il codice a sei a cifre non viene ricevuto, fare clic su **Non ho ricevuto il codice e ho bisogno di un nuovo invio**.

7.  Immettere il codice nella casella **Passcode**, quindi fare clic su **Fine**.

8.  Dopo che l'utente viene abilitato alle notifiche SMS, è possibile fare clic su **Impostare le notifiche della casella vocale** nella pagina **Invio SMS**. Gli utenti sono portati indietro alla pagina di casella vocale, dove sono in grado di scorrere verso il basso fino alla sezione **Notifiche** e impostare le opzioni di notifica dei messaggi di testo per le chiamate senza risposta e la casella vocale.

Inizio pagina


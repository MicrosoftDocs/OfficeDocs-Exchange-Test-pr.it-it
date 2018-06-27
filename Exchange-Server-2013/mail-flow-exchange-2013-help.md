---
title: 'Flusso di posta: Exchange 2013 Help'
TOCTitle: Flusso di posta
ms:assetid: 14df5e1a-a5f7-4b0d-ba97-f53b76f0e7e0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996349(v=EXCHG.150)
ms:contentKeyID: 50480036
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Flusso di posta

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

In Microsoft Exchange Server 2013, il flusso di posta avviene attraverso la pipeline di trasporto. La *pipeline di trasporto* è un insieme di servizi, connessioni, componenti e code che interagiscono per instradare tutti i messaggi al classificatore nel servizio Trasporto di un server Cassette postali all'interno dell'organizzazione.

Ricerca di un elenco di tutti gli argomenti relativi al flusso di posta vedere Documentazione del flusso di posta.

Per informazioni su come configurare il flusso di posta in una nuova organizzazione Exchange 2013, vedere [Configurazione del flusso di posta e di Accesso client](configure-mail-flow-and-client-access-exchange-2013-help.md).

**Sommario**

La pipeline di trasporto

Servizio Trasporto sui server Cassette postali

Documentazione del flusso di posta

## La pipeline di trasporto

La pipeline di trasporto consiste nei seguenti servizi:

  - **Servizio Trasporto front-end nei server Accesso client**   Questo servizio agisce come un proxy senza stato per tutto il traffico SMTP esterno in entrata e (opzionalmente) in uscita nell'organizzazione di Exchange 2013. Il servizio Trasporto front-end non ispeziona il contenuto del messaggio, non comunica con il servizio Trasporto cassette postali nei server Cassette postali né mette in coda i messaggi localmente.

  - **Servizio Trasporto nei server Cassette postali**   Questo servizio è praticamente identico al ruolo del server Trasporto Hub disponibile nelle precedenti versioni di Exchange. Il servizio Trasporto gestisce l'intero flusso di posta SMTP dell'organizzazione ed esegue una classificazione dei messaggi e un controllo del contenuto dei messaggi. A differenza delle precedenti versioni di Exchange, il servizio Trasporto non comunica mai direttamente con i database delle cassette postali. Questa attività è ora gestita dal servizio Trasporto cassette postali. Il servizio di trasporto indirizza i messaggi tra il servizio Trasporto cassette postali, il servizio di trasporto, il servizio Trasporto front end e (a seconda della configurazione) il servizio di trasporto nei server Trasporto Edge. Il servizio di trasporto nei server Cassette postali verrà descritto in modo più dettagliato più avanti in questo argomento.

  - **Servizio Trasporto cassette postali nei server Cassette postali**   Questo servizio è composto da sue servizi separati: il servizio Invio Trasporto cassette postali il servizio Recapito Trasporto cassette postali. Il servizio Recapito Trasporto cassette postali riceve i messaggi SMTP dal servizio Trasporto sul server Cassette postali locale o su altri server Cassette postali ed esegue il collegamento al database di cassette postali locale utilizzando un'istruzione RPC (Remote Procedure Call) di Exchange per recapitare il messaggio. Il servizio Invio Trasporto cassette postali esegue il collegamento al database di cassette postali locale utilizzando l'istruzione RPC per recuperare i messaggi e inoltra i messaggi sull'SMTP al servizio Trasporto del server Cassette postali locali o su altri server Cassette postali. Il servizio Invio Trasporto cassette postali ha accesso alle stesse informazioni sulla topologia di routing del servizio Trasporto. Come nel caso del servizio Trasporto front-end, anche il servizio Trasporto cassette postali non inserisce alcun messaggio nella coda locale.

  - **Servizio di trasporto nei server Trasporto Edge**   Questo servizio è molto simile al servizio di trasporto nei server Cassette postali. Se nella rete perimetrale è installato un server Trasporto Edge, tutte la posta proveniente da Internet o indirizzata a Internet attraversa il server Trasporto Edge del servizio di trasporto. Maggiori dettagli su questo servizio sono disponibili più avanti in questo argomento.

Nella seguente figura vengono illustrate le relazioni tra i componenti nella pipeline di trasporto di Exchange 2013.

**Panoramica sulla pipeline di trasporto in Exchange 2013.**

![Diagramma della panoramica della pipeline di trasporto](images/Aa996349.6f548b64-6ac2-4e98-9098-69ad6cd9f569(EXCHG.150).gif "Diagramma della panoramica della pipeline di trasporto")

## Messaggi provenienti da mittenti esterni

I messaggi provenienti dall'esterno dell'organizzazione vengono immessi nella pipeline di trasporto attraverso un connettore di ricezione nel servizio Trasporto front-end sul server Accesso client e vengono, poi, instradati al servizio Trasporto sul server Cassette postali.

Se nella rete perimetrale è installato un server Trasporto Edge di Exchange 2013, i messaggi provenienti dall'esterno entrano nella pipeline di trasporto attraverso un connettore di ricezione nel servizio di trasporto nel server Trasporto Edge. Dove vanno i messaggi dipende dalla configurazione dei server di Exchange interni.

  - **Server Cassette postali e Accesso client installati nello stesso computer**   In questa configurazione, il server Accesso client viene usato per il flusso di posta in entrata. La posta passa dal servizio di trasporto nel server Trasporto Edge al servizio Trasporto Front End nel server Accesso client, quindi nel servizio di trasporto nel server Cassette postali.

  - **Server Cassette postali e Accesso client installati in computer diversi**   In questa configurazione, il server Accesso client viene ignorato per il flusso di posta in entrata. La posta passa dal servizio di trasporto nel server Trasporto Edge al servizio di trasporto nel server Cassette postali.


> [!NOTE]
> Se si dispone di un server Exchange&nbsp;2010 o Trasporto Edge di Exchange&nbsp;2007 nella rete perimetrale, il flusso di posta si verifica sempre direttamente tra il server Trasporto Edge e il servizio di trasporto nel server Cassette postali. Per ulteriori informazioni, vedere <A href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">Utilizzare un Exchange 2010 o 2007 server Trasporto Edge di Exchange 2013</A>.



## Messaggi provenienti da mittenti interni

I messaggi SMTP provenienti da mittenti interni all'organizzazione entrano nella pipeline di trasporto attraverso il servizio Trasporto su un server Cassette postali in uno dei seguenti modi:

  - Tramite un connettore di ricezione.

  - Dalla directory di prelievo o dalla directory di riproduzione.

  - Dal servizio Trasporto cassette postali.

  - Con invio tramite agente.

Il messaggio viene instradato in base alla destinazione di routing o al gruppo di recapito. Per ulteriori informazioni, vedere [Routing della posta](mail-routing-exchange-2013-help.md).

Se il messaggio ha destinatari esterni, il messaggio viene instradato dal servizio di trasporto nel server Cassette postali a Internet o dal server Cassette postali al servizio Trasporto front end in un server Accesso client e poi a Internet se il connettore di invio è configurato per le connessioni proxy in uscita attraverso il server Accesso client. Per ulteriori informazioni, vedere [Creare un connettore di invio per la posta elettronica inviato a Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md).

Se nella rete perimetrale è installato un server Trasporto Edge, i messaggi con destinatari esterni non vengono mai instradati attraverso il servizio Trasporto front end in un server Accesso clien. Il messaggio viene instradato dal servizio di trasporto in un server Cassette postali al servizio di trasporto nel server Trasporto Edge

## Servizio Trasporto sui server Cassette postali

Ogni messaggio inviato o ricevuto da un'organizzazione di Exchange 2013 deve essere classificato nel servizio Trasporto su un server Cassette postali prima di poter essere instradato e recapitato. Una volta classificato, il messaggio viene inserito in una coda di recapito per il recapito al database di cassette postali di destinazione, al gruppo di disponibilità del database di destinazione (o foresta Active Directory) o al dominio di destinazione esterno all'organizzazione.

Il servizio Trasporto su un server Cassette postali è costituito dai seguenti componenti e processi:

  - **Ricezione SMTP**   Quando si ricevono messaggi dal servizio Trasporto, viene eseguito il controllo del contenuto dei messaggi, vengono applicate le regole di trasporto e viene eseguito il controllo di protezione dalla posta indesiderata e antimalware, se abilitati. La sessione SMTP è costituita da una serie di eventi che interagiscono in un ordine specifico per convalidare il contenuto di un messaggio prima che quest'ultimo venga accettato. Una volta che è transitato completamente tramite il connettore di ricezione SMTP e non è stato rifiutato da eventi di ricezione o da un agente di protezione da posta indesiderata e antimalware, il messaggio viene inserito nella coda di invio.

  - **Invio**   L'invio è il processo che consente di inserire i messaggi nella coda Invio. Il classificatore preleva un messaggio alla volta per la classificazione. L'invio avviene in tre modi:
    
      - Da ricezione SMTP attraverso un connettore di ricezione.
    
      - Tramite la directory di prelievo o la directory di riproduzione. Le directory esistono nei server Cassette postali e nei server Trasporto Edge. I file dei messaggi formattati correttamente che vengono copiati nella directory di prelievo o nella directory di riesecuzione vengono inseriti direttamente nella coda Invio.
    
      - Tramite un agente di trasporto.

  - **Classificatore**   Il classificatore preleva un messaggio alla volta dalla coda Invio. Il classificatore completa la seguente procedura:
    
      - Risoluzione dei destinatari, che include l'indirizzamento di livello superiore, l'espansione e la moltiplicazione.
    
      - Risoluzione del routing.
    
      - Conversione del contenuto.
    
    Vengono inoltre applicate le regole del flusso di posta definite dall'organizzazione. Una volta classificati, i messaggi vengono inseriti in una coda di recapito basata sulla destinazione del messaggio. I messaggi vengono aggiunti alla coda dal database di cassette postali di destinazione, dal gruppo di disponibilità del database, dal sito Active Directory, dalla foresta Active Directory o da un dominio esterno.

  - **Protocollo di invio SMTP**   La modalità di instradamento dei messaggi da parte del servizio Trasporto dipende dalla posizione dei destinatari dei messaggi relativamente al server Cassette postali in cui è avvenuta la classificazione. Il messaggio potrebbe essere instradato in uno dei seguenti percorsi:
    
      - Al servizio Trasporto Cassette postali nello stesso server Cassette postali.
    
      - Al servizio Trasporto Cassette postali in un altro server Cassette postali dello stesso gruppo di disponibilità del database.
    
      - Al servizio di trasporto in un server Cassette postali in un altro gruppo di disponibilità del database, sito Active Directory o foresta Active Directory.
    
      - Per il recapito a Internet attraverso un connettore di invio nello stesso server Cassette postali, attraverso il servizio di trasporto in un altro server Cassette postali, attraverso il servizio Trasporto front end in un server Accesso client o attraverso il servizio di trasporto in un server Trasporto Edge nella rete perimetrale.

## Servizio di trasporto nei server Trasporto Edge

I componenti del servizio di trasporto nei server Trasporto Edge sono identici ai componenti del servizio di trasporto nei server Cassette postali. Tuttavia, quello che effettivamente si verifica durante ogni fase dell'elaborazione nei server Trasporto Edge è diverso. Le differenze vengono descritte nell'elenco seguente.

  - **Ricezione SMTP**   Quando un server Trasporto Edge è sottoscritto in un sito Active Directory interno, il connettore di ricezione predefinito viene automaticamente configurato per accettare posta da server Cassette postali interni e da Internet. Quando i messaggi Internet arrivano nel server Trasporto Edge, gli agenti protezione posta indesiderata filtrano le connessioni e il contenuto dei messaggi e consentono l'identificazione del mittente e del destinatario durante l'accettazione del messaggio all'interno dell'organizzazione. Gli agenti protezione posta indesiderata sono installati e attivati per impostazione predefinita. Funzionalità di filtro di allegati aggiuntivi e delle connessioni sono disponibili, ma il filtro integrato di malware no. Inoltre, le regole di trasporto sono controllate dall'agente regole Edge. Rispetto all'agente Regola di trasporto nei server Cassette postali, solo un piccolo sottogruppo di condizioni delle regole di trasporto è disponibile nei server Trasporto Edge. Tuttavia, esistono azioni delle regole di trasporto univoche correlate alle connessioni SMTP che sono disponibili solo nei server Trasporto Edge.

  - **Invio**   In un server Trasporto Edge, generalmente i messaggi entrano nella coda di invio attraverso un connettore di ricezione. Tuttavia, sono disponibili anche la directory di prelievo e la directory di riesecuzione.

  - **Classificatore**   In un server Trasporto Edge, la classificazione è una breve procedura nella quale il messaggio viene messo direttamente in una coda di recapito per il recapito a destinatari interni o esterni.

  - **Invio SMTP**   Quando un server Trasporto Edge viene sottoscritto in un sito di Active Directory interno, due connettori di invio vengono automaticamente creati e configurati. Uno è responsabile dell'invio della posta in uscita a destinatari in Internet; l'altro è responsabile dell'invio della posta in ingresso da Internet a destinatari interni. La posta in entrata viene inviata al servizio di trasporto in un server Cassette postali disponibile nel sito Active Directory sottoscritto.

## Documentazione del flusso di posta

Nella seguente tabella, sono riportati i collegamenti agli argomenti che offrono maggiori informazioni sul flusso di posta in Exchange 2013 e ne facilitano la gestione.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Argomento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-routing-exchange-2013-help.md">Routing della posta</a></p></td>
<td><p>Il routing della posta descrive il modo in cui i messaggi vengono trasmessi tra i server di messaggistica.</p></td>
</tr>
<tr class="even">
<td><p><a href="connectors-exchange-2013-help.md">Connettori</a></p></td>
<td><p>I connettori definiscono dove e come i messaggi vengono trasmessi a e da server Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="domains-exchange-2013-help.md">Domini</a></p></td>
<td><p>I domini accettati definiscono gli spazi indirizzi SMTP utilizzati nell'organizzazione di Exchange. I domini remoti configurano le impostazioni di formattazione e codifica dei messaggi per i messaggi inviati a domini esterni.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-agents-exchange-2013-help.md">Agenti di trasporto</a></p></td>
<td><p>Gli agenti di trasporto agiscono sui messaggi quando passano attraverso la pipeline di trasporto di Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-high-availability-exchange-2013-help.md">Disponibilità elevata di trasporto</a></p></td>
<td><p>L'elevata disponibilità di trasporto descrive il modo in cui Exchange 2013 conserva copie ridondanti di messaggi durante il passaggio e dopo il recapito.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-logs-exchange-2013-help.md">Registri di trasporto</a></p></td>
<td><p>I registri di trasporto registrano cosa accade ai messaggi quando circolano attraverso la pipeline di trasporto.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-message-approval-exchange-2013-help.md">Gestione approvazione del messaggio</a></p></td>
<td><p>Il trasporto moderato richiede l'approvazione per i messaggi inviati a determinati destinatari.</p></td>
</tr>
<tr class="even">
<td><p><a href="content-conversion-exchange-2013-help.md">Conversione del contenuto</a></p></td>
<td><p>La conversione del contenuto controlla le opzioni per la conversione dei messaggi nel formato di codifica Transport Neutral per i destinatari esterni e le opzioni per la conversione MAPI per i destinatari interni.</p></td>
</tr>
<tr class="odd">
<td><p><a href="dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md">DSN e NDR in Exchange 2013</a></p></td>
<td><p>Le notifiche (DSN) sono i messaggi di sistema inviati ai mittenti dei messaggi; ad esempio, i rapporti di mancato recapito.</p></td>
</tr>
<tr class="even">
<td><p><a href="track-messages-with-delivery-reports-exchange-2013-help.md">Tenere traccia dei messaggi con i rapporti di recapito</a></p></td>
<td><p>I rapporti di recapito sono uno strumento di verifica dei messaggi che è possibile utilizzare per conoscere lo stato di recapito dei messaggi di posta elettronica inviati o ricevuti da utenti presenti nella rubrica dell'organizzazione, con un determinato oggetto. È possibile monitorare le informazioni sul recapito dei messaggi inviati o ricevuti da una specifica cassetta postale dell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><a href="message-size-limits-exchange-2013-help.md">Limiti di dimensione dei messaggi</a></p></td>
<td><p>In questo argomento, vengono descritti i limiti di dimensione e singoli componenti imposti sui messaggi.</p></td>
</tr>
<tr class="even">
<td><p><a href="queue-viewer-exchange-2013-help.md">Visualizzatore code</a></p></td>
<td><p>Utilizzare Visualizzatore code in Casella degli strumenti di Exchange per visualizzare e le code e i messaggi in coda e lavorarci sopra.</p></td>
</tr>
<tr class="odd">
<td><p><a href="pickup-directory-and-replay-directory-exchange-2013-help.md">Directory di prelievo e directory di riesecuzione</a></p></td>
<td><p>Le directory di prelievo e riproduzione vengono utilizzate per inserire file di messaggi nella pipeline di trasporto.</p></td>
</tr>
<tr class="even">
<td><p><a href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">Utilizzare un Exchange 2010 o 2007 server Trasporto Edge di Exchange 2013</a></p></td>
<td><p>In questo argomento, vengono descritte le considerazioni su come utilizzare il server Trasporto Edge ricavato da versioni precedenti di Exchange in Exchange 2013.</p></td>
</tr>
</tbody>
</table>


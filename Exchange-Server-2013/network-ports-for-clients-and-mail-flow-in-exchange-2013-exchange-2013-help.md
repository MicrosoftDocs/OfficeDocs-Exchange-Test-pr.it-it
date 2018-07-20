---
title: 'Porte di rete per client e flusso di posta in Exchange 2013: Exchange 2013 Help'
TOCTitle: Porte di rete per client e flusso di posta in Exchange 2013
ms:assetid: fec09455-e99e-42eb-8b32-1ddc08d9a19e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb331973(v=EXCHG.150)
ms:contentKeyID: 64126830
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Porte di rete per client e flusso di posta in Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In questo argomento vengono fornite informazioni relative alle porte di rete che vengono utilizzate da MicrosoftExchange Server 2013 per le comunicazioni con i client di posta elettronica, server di posta Internet e altri servizi esterni all'organizzazione Exchange locale. Prima di approfondire l'argomento, comprendere le regole di base riportate di seguito:

  - Non è supportato il traffico di rete alterato o limitato tra server Exchange interni, tra server Exchange interni e server Lync o Skype for Business interni oppure tra server Exchange interni e controller di dominio Active Directory interni in qualsiasi tipo di topologia. Se si dispone di firewall o dispositivi di rete che potrebbero potenzialmente limitare o alterare il traffico di rete di questo tipo, è necessario configurare regole che consentono comunicazioni gratuite e senza restrizioni tra questi server (regole che consentano il traffico di rete in ingresso e in uscita su qualsiasi porta, incluse le porte RPC casuali, e su qualsiasi protocollo che non altera mai i bit in rete).

  - In genere, i server Trasporto Edge si trovano in una rete perimetrale; pertanto si presuppone che verrà limitato il traffico di rete tra il server Trasporto Edge e Internet e tra il server Trasporto Edge e l'organizzazione Exchange interna. Le porte di rete sono descritte in questo argomento.

  - Probabilmente verrà limitato il traffico di rete tra i servizi e i client esterni e l'organizzazione Exchange interna. È inoltre consentito limitare il traffico di rete tra client interni e server Exchange interni. Le porte di rete sono descritte in questo argomento.

**Sommario**

Porte di rete necessarie per client e servizi

Porte di rete richieste per il flusso di posta (senza server Trasporto Edge)

Porte di rete richieste per il flusso di posta con i server Trasporto Edge

Porte di rete necessarie per le distribuzioni ibride

Porte di rete necessarie per la Messaggistica unificata

## Porte di rete necessarie per client e servizi

Le porte di rete necessarie ai client di posta elettronica per accedere alle cassette postali e ad altri servizi nell'organizzazione Exchange sono descritte nel diagramma e nella tabella seguenti.

**Note:** 

  - La destinazione per i client e i servizi è un server Accesso client. Può trattarsi di un server Accesso client autonomo o di un server Accesso client e un server Cassette postali installato nello stesso computer.

  - Anche se il diagramma mostra client e servizi da Internet, i concetti sono gli stessi dei client interni (ad esempio, i client di una foresta di account con accesso ai server Exchange in una foresta di risorse). Analogamente, la tabella non dispone di una colonna di origine perché l'origine potrebbe essere qualsiasi percorso esterno all'organizzazione Exchange (ad esempio, Internet o una foresta di account).

  - I server Trasporto Edge non influenzano in alcun modo il traffico di rete associato ai client e servizi.

![Porte di rete necessarie per client e servizi](images/Bb331973.f5ba3439-f001-43c8-848e-0e3fd0fce931(EXCHG.150).png "Porte di rete necessarie per client e servizi")


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Scopo</th>
<th>Porte</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Le connessioni Web crittografate vengono utilizzate dai client e servizi riportati di seguito:</p>
<ul>
<li><p>Servizio di individuazione automatica</p></li>
<li><p>Exchange ActiveSync</p></li>
<li><p>Servizi Web Exchange (EWS)</p></li>
<li><p>Distribuzione della Rubrica offline</p></li>
<li><p>Outlook Anywhere (RPC su HTTP)</p></li>
<li><p>Outlook MAPI su HTTP</p></li>
<li><p>Outlook Web App</p></li>
</ul></td>
<td><p>443/TCP (HTTPS)</p></td>
<td><p>Per ulteriori informazioni su questi client e servizi, vedere i seguenti argomenti:</p>
<ul>
<li><p><a href="autodiscover-service-for-exchange-2013.md">Servizio di individuazione automatica</a></p></li>
<li><p><a href="exchange-activesync-exchange-2013-help.md">Exchange ActiveSync</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/?linkid=529544">Riferimenti di EWS per Exchange</a></p></li>
<li><p><a href="offline-address-books-exchange-2013-help.md">Rubriche offline</a></p></li>
<li><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook via Internet</a></p></li>
<li><p><a href="mapi-over-http-exchange-2013-help.md">MAPI su HTTP</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Novità per Outlook Web App in Exchange 2013</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Le connessioni Web decrittografate vengono utilizzate dai client e servizi riportati di seguito:</p>
<ul>
<li><p>Pubblicazione del calendario Internet</p></li>
<li><p>Outlook Web App (reindirizzato a 443/TCP)</p></li>
<li><p>Individuazione automatica (fallback quando 443/TCP non è disponibile)</p></li>
</ul></td>
<td><p>80/TCP (HTTP)</p></td>
<td><p>Se possibile, è consigliabile utilizzare connessioni Web crittografate su 443/TCP per proteggere i dati e le credenziali. Tuttavia, è possibile che sia necessario configurare alcuni servizi per utilizzare le connessioni Web decrittografate su 80/TCP al server Accesso client.</p>
<p>Per ulteriori informazioni su questi client e servizi, vedere i seguenti argomenti:</p>
<ul>
<li><p><a href="enable-internet-calendar-publishing-exchange-2013-help.md">Abilitare la pubblicazione del calendario Internet</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Novità per Outlook Web App in Exchange 2013</a></p></li>
<li><p><a href="autodiscover-service-for-exchange-2013.md">Servizio di individuazione automatica</a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>client IMAP4</p></td>
<td><p>143/TCP (IMAP), 993/TCP (IMAP protetto)</p></td>
<td><p>IMAP4 è disabilitato per impostazione predefinita. Per ulteriori informazioni, vedere <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">POP3 e IMAP4 in Exchange Server 2013</a>.</p>
<p>Il servizio IMAP4 sul server Accesso client invia le connessioni tramite proxy al servizio back-end IMAP4 su un server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>client POP3</p></td>
<td><p>110/TCP (POP3), 995/TCP (POP3 protetto)</p></td>
<td><p>POP3 è disabilitato per impostazione predefinita. Per ulteriori informazioni, vedere <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">POP3 e IMAP4 in Exchange Server 2013</a>.</p>
<p>Il servizio POP3 sul server Accesso client invia le connessioni tramite proxy al servizio back-end POP3 su un server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>Client SMTP (autenticati)</p></td>
<td><p>587/TCP (SMTP autenticati)</p></td>
<td><p>Il connettore di ricezione predefinito denominato &quot;<em>&lt;Server name&gt;</em> front-end client&quot; è configurato per l'ascolto di invii di client SMTP autenticati sulla porta 587 sul server Accesso client.</p>
<p><strong>Nota:</strong></p>
<p>Se si dispone di client di posta in grado di inviare posta SMTP autenticata solo sulla porta 25, è possibile modificare il valore di binding della scheda di rete del connettore di ricezione per attendere anche invii di posta SMTP autenticata sulla porta 25.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Porte di rete necessarie per il flusso di posta

La modalità di recapito da e verso l'organizzazione Exchange dipende dalla topologia di Exchange. Il fattore più importante è se si dispone di un server Trasporto Edge sottoscritto distribuito nella rete perimetrale.

## Porte di rete richieste per il flusso di posta (senza server Trasporto Edge)

Le porte di rete necessarie per il flusso di posta in un'organizzazione Exchange che dispone solo di server Accesso client e server Cassette postali sono descritte nel diagramma e nella tabella seguenti. Anche se il diagramma mostra server Cassette postali e server Accesso client separati, i concetti sono gli stessi se il server Accesso client e il server Cassette postali sono installati nello stesso computer o in computer separati.

![Porte di rete richieste per il flusso di posta (senza server Trasporto Edge)](images/Bb331973.af54dfd3-fe6b-4b6e-bb8e-b00df94a0be0(EXCHG.150).png "Porte di rete richieste per il flusso di posta (senza server Trasporto Edge)")


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
<th>Scopo</th>
<th>Porte</th>
<th>Origine</th>
<th>Destinazione</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Posta in ingresso</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Internet (qualsiasi)</p></td>
<td><p>Server Accesso client</p></td>
<td><p>Il connettore di ricezione predefinito denominato &quot;<em>&lt;Client Access server name&gt;</em> front-end predefinito&quot; nel server Accesso client è configurato per l'ascolto della posta SMTP in ingresso anonima sulla porta 25.</p>
<p>La posta viene inoltrata dal server Accesso client a un server Cassetta postale utilizzando il connettore di invio implicito e invisibile tra organizzazioni che invia automaticamente la posta tra i server Exchange nella stessa organizzazione.</p></td>
</tr>
<tr class="even">
<td><p>Posta in uscita</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Server Cassette postali</p></td>
<td><p>Internet (qualsiasi)</p></td>
<td><p>Per impostazione predefinita, Exchange non crea connettori di invio che consentono di inviare posta a Internet. È necessario creare manualmente i connettori di invio. Per ulteriori informazioni, vedere <a href="send-connectors-exchange-2013-help.md">Connettori di invio</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Posta in uscita (se inviata attraverso il server Accesso client)</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Server Accesso client</p></td>
<td><p>Internet (qualsiasi)</p></td>
<td><p>La posta in uscita viene inviata tramite un server Accesso client solo quando un connettore di invio è configurato con <strong>Proxy tramite server Accesso client</strong> nell'interfaccia di amministrazione di Exchange o <code>-FrontEndProxyEnabled $true</code> in Exchange Management Shell.</p>
<p>In questo caso, il connettore di ricezione predefinito denominato &quot;<em>&lt;Client Access server name&gt;</em> front-end proxy in uscita&quot; nel server Accesso client è configurato per l'ascolto di posta in uscita dal server Cassette postali. Per ulteriori informazioni, vedere <a href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">Creare un connettore di invio per la posta elettronica inviato a Internet</a>.</p></td>
</tr>
<tr class="even">
<td><p>DNS per la risoluzione dei nomi dell'hop di posta successivo (non raffigurato)</p></td>
<td><p>53/UDP,53/TCP (DNS)</p></td>
<td><p>Server Exchange per Internet (server Accesso client o server Cassette postali)</p></td>
<td><p>Server DNS</p></td>
<td><p>Vedere la sezione Risoluzione dei nomi.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Porte di rete richieste per il flusso di posta con i server Trasporto Edge

Un server Trasporto Edge sottoscritto installato nella rete perimetrale elimina il flusso della posta SMTP tramite il server Accesso client. In particolare:

  - La posta in uscita dall'organizzazione Exchange non passa mai attraverso un server Accesso client. La posta passa sempre da un server Cassette postali nel sito Active Directory sottoscritto al server Trasporto Edge (indipendentemente dalla versione di Exchange sul server Trasporto Edge).

  - La posta in ingresso non passa mai attraverso un server Accesso client autonomo. La posta passa dal server Trasporto Edge a un server Cassette postali nel sito Active Directory sottoscritto. Se il server Cassette postali e il server Accesso client sono installati nello stesso computer, la posta da un server Trasporto Edge Exchange 2013 arriva nel computer del servizio di trasporto front-end (il ruolo del server Accesso client) prima di passare al servizio di trasporto (il ruolo del server Cassette postali). I server Trasporto Edge Exchange 2007 o Exchange 2010 recapitano sempre la posta direttamente al servizio di trasporto, anche quando il server Cassette postali e il server Accesso client sono installati nello stesso computer.

Per ulteriori informazioni, vedere [Flusso di posta](mail-flow-exchange-2013-help.md).

Le porte di rete necessarie per il flusso di posta in organizzazioni Exchange che dispongono di server Trasporto Edge sono descritte nel diagramma e nella tabella seguenti. Se non specificato diversamente, i concetti sono gli stessi se il server Accesso client e il server Cassette postali sono installati nello stesso computer o in computer separati.

![Porte di rete richieste per il flusso di posta con i server Trasporto Edge](images/Bb331973.110c79b3-dbd9-4cb5-bba1-02048363ee1c(EXCHG.150).png "Porte di rete richieste per il flusso di posta con i server Trasporto Edge")


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
<th>Scopo</th>
<th>Porte</th>
<th>Origine</th>
<th>Destinazione</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Posta in ingresso - Da Internet al server Trasporto Edge</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Internet (qualsiasi)</p></td>
<td><p>Server Trasporto Edge</p></td>
<td><p>Il connettore di ricezione predefinito denominato &quot;<em>&lt;Edge Transport server name&gt;</em> connettore di ricezione interno predefinito&quot; nel server Trasporto Edge è configurato per l'ascolto della posta SMTP anonima sulla porta 25.</p></td>
</tr>
<tr class="even">
<td><p>Posta in ingresso - Dal server Trasporto Edge all'organizzazione Exchange interna</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Server Trasporto Edge</p></td>
<td><p>Server Cassette postali nel sito Active Directory sottoscritto</p></td>
<td><p>Il connettore di invio predefinito denominato &quot;EdgeSync - Ingresso in <em>&lt;Active Directory site name&gt;</em>&quot; inoltra la posta in arrivo sulla porta 25 per qualsiasi server Cassette postali nel sito Active Directory sottoscritto. Per ulteriori informazioni, vedere la sezione &quot;Inviare connettori creati durante il processo di sottoscrizione Edge&quot; nell'argomento, <a href="edge-subscriptions-exchange-2013-help.md">Sottoscrizioni Edge</a>.</p>
<p>Il servizio che riceve la posta dipende dal fatto che il server Accesso client e il server Cassette postali sono installati nello stesso computer o in computer separati.</p>
<ul>
<li><p><strong>Server Cassette postali autonomo</strong>   Il connettore di ricezione predefinito denominato &quot;<em>&lt;Mailbox server name&gt;</em> predefinito&quot; è configurato per l'ascolto della posta in ingresso (compresa la posta proveniente dai server Trasporto Edge) sulla porta 25.</p></li>
<li><p><strong>Server Cassette postali e server Accesso client installati sullo stesso computer</strong>   Il connettore di ricezione predefinito denominato &quot;<em>&lt;Server name&gt;</em> front-end predefinito&quot; nel servizio di trasporto front-end (il ruolo del server Accesso client) è configurato per l'ascolto della posta in ingresso (compresa la posta proveniente dai server Trasporto Edge Exchange 2013) sulla porta 25.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Posta in uscita - Dall'organizzazione Exchange interna al server Trasporto Edge</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Server Cassette postali nel sito Active Directory sottoscritto</p></td>
<td><p>Server Trasporto Edge</p></td>
<td><p>La posta in uscita ignora sempre il server Accesso client.</p>
<p>La posta viene inoltrata da qualsiasi server Cassetta postale nel sito Active Directory sottoscritto a un server Trasporto Edge utilizzando il connettore di invio implicito e invisibile tra organizzazioni che invia automaticamente la posta tra i server Exchange nella stessa organizzazione.</p>
<p>Il connettore di ricezione predefinito denominato &quot;<em>&lt;Edge Transport server name&gt;</em> connettore di ricezione interno predefinito&quot; nel server Trasporto Edge è configurato per l'ascolto della posta SMTP sulla porta 25 da qualsiasi server Cassette postali nel sito Active Directory sottoscritto.</p></td>
</tr>
<tr class="even">
<td><p>Posta in uscita - Dal server Trasporto Edge a Internet</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Server Trasporto Edge</p></td>
<td><p>Internet (qualsiasi)</p></td>
<td><p>Il connettore di invio predefinito denominato &quot;EdgeSync -Da <em>&lt;Active Directory site name&gt;</em> a Internet&quot; inoltra la posta in uscita sulla porta 25 dal server Trasporto Edge a Internet.</p></td>
</tr>
<tr class="odd">
<td><p>Sincronizzazione EdgeSync</p></td>
<td><p>50636/TCP (LDAP protetto)</p></td>
<td><p>Server Cassette postali nel sito Active Directory sottoscritto inclusi nel processo di sincronizzazione EdgeSync</p></td>
<td><p>Server Trasporto Edge</p></td>
<td><p>Quando il server Trasporto Edge è sottoscritto nel sito Active Directory, tutti i server Cassette postali esistenti nel sito in quel momento vengono inclusi nel processo di sincronizzazione EdgeSync. Tuttavia, i server Cassette postali aggiunti in un secondo momento non vengono automaticamente inclusi nel processo di sincronizzazione EdgeSync.</p></td>
</tr>
<tr class="even">
<td><p>DNS per la risoluzione dei nomi dell'hop di posta successivo (non raffigurato)</p></td>
<td><p>53/UDP,53/TCP (DNS)</p></td>
<td><p>Server Trasporto Edge</p></td>
<td><p>Server DNS</p></td>
<td><p>Vedere la sezione Risoluzione dei nomi.</p></td>
</tr>
<tr class="odd">
<td><p>Definizione di server proxy per reputazione mittente (non raffigurata)</p></td>
<td><p>definite dall'utente</p></td>
<td><p>Server Trasporto Edge</p></td>
<td><p>Internet</p></td>
<td><p>La reputazione del mittente (agente di analisi del protocollo) consente di analizzare i percorsi dei messaggi in ingresso per ridurre la posta indesiderata. Se l'organizzazione utilizza un server proxy per controllare l'accesso a Internet, è necessario definire i dettagli relativi al server proxy in modo che la reputazione del mittente funzioni correttamente (in particolare, il rilevamento proxy aperto e il blocco del mittente). Utilizzare i parametri <em>ProxyServerName</em>, <em>ProxyServerPort</em> e <em>ProxyServerType</em> sul cmdlet <strong>Set-SenderReputationConfig</strong> per definire il server proxy dell'organizzazione in modo che la reputazione del mittente sia in grado di connettersi a Internet. Per ulteriori informazioni, vedere <a href="manage-sender-reputation-exchange-2013-help.md">Gestione di reputazione mittente</a>.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Risoluzione dei nomi

La risoluzione DNS dell'hop di posta successivo è una parte fondamentale del flusso di posta in qualsiasi organizzazione Exchange. I server Exchange che si occupano della ricezione della posta in ingresso o del recapito della posta in uscita devono essere in grado di risolvere i nomi host interni ed esterni per il routing della posta corretto. Tutti i server Exchange interni devono essere in grado di risolvere i nomi host interni per il routing della posta corretto. Esistono molti modi diversi per progettare un'infrastruttura DNS, ma l'importante è garantire che la risoluzione dei nomi per l'hop di posta successivo funzioni correttamente per tutti i server Exchange.

## Porte di rete necessarie per le distribuzioni ibride

Le porte di rete necessarie per un'organizzazione che utilizza Exchange 2013 e MicrosoftOffice 365 vengono descritte nella sezione "Protocolli, porte ed endpoint per la distribuzione ibrida" in [Prerequisiti per la distribuzione ibrida](https://technet.microsoft.com/it-it/library/hh534377\(v=exchg.150\)).

## Porte di rete necessarie per la Messaggistica unificata

Le porte di rete necessarie per la messaggistica unificata vengono illustrate negli argomenti seguenti:

  - [Servizi, porte e protocolli di messaggistica unificata](um-protocols-ports-and-services-exchange-2013-help.md)

  - [Poster dell'architettura di Exchange Server 2013 SP1](https://go.microsoft.com/fwlink/p/?linkid=518646)

Inizio pagina


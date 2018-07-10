---
title: 'Information Rights Management: Exchange 2013 Help'
TOCTitle: Information Rights Management
ms:assetid: 6ea3a695-3ddd-4d53-b3c6-90041f44ef64
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638140(v=EXCHG.150)
ms:contentKeyID: 50480845
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Information Rights Management

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Ogni giorno, gli informatici utilizzano la posta elettronica per lo scambio di informazioni sensibili come le relazioni finanziarie e dei dati, contratti legali, informazioni sui prodotti riservate, relazioni e proiezioni di vendita, analisi della concorrenza, la ricerca e le informazioni sui brevetti e informazioni su clienti e dipendenti. Perché le persone possono accedere alla propria posta elettronica da qualsiasi luogo, le cassette postali si sono trasformate in depositi contenenti grandi quantità di informazioni potenzialmente sensibili. Di conseguenza, la perdita di informazioni può rappresentare una grave minaccia per le organizzazioni. Per impedire la perdita di informazioni, Microsoft Exchange Server 2013 comprende le funzionalità IRM (Information Rights Management), che forniscono una costante protezione online e offline dei messaggi e degli allegati di posta elettronica.

**Sommario**

What is information leakage?

Traditional solutions to information leakage

IRM in Exchange 2010

Applying IRM protection to messages

Scenarios for IRM protection

Decrypting IRM-protected messages to enforce messaging policies

Prelicensing

IRM agents

IRM requirements

Configuring and testing IRM

Extend Rights Management with the Rights Management connector

## Cosa si intende per perdita di informazioni

La perdita di informazioni potenzialmente riservate può risultare costosa per un'organizzazione: può avere un impatto ad ampio raggio su organizzazione, attività, dipendenti, clienti e partner. Le modalità con cui determinati tipi di informazioni vengono archiviate, trasmesse e protette sono sempre più regolate da normative settoriali e locali. Per non violare le normative vigenti, le organizzazioni devono proteggersi contro la perdita intenzionale, involontaria o accidentale di informazioni.

Di seguito vengono menzionate alcune conseguenze derivanti dalla perdita di informazioni:

  - **Danni finanziari**   A seconda delle dimensioni, del settore e delle normative locali, la perdita di informazioni può comportare conseguenze finanziarie dovute a mancati guadagni o a multe e risarcimenti disposti dai tribunali o dalle autorità competenti. Le società ad azionariato diffuso (public company) potrebbero anche rischiare la perdita di capacità di capitalizzazione sul mercato a causa di una copertura mediatica negativa.

  - **Danni all'immagine e alla credibilità**   La perdita di informazioni può danneggiare l'immagine di un'organizzazione e la sua credibilità nei confronti dei clienti. Inoltre, a seconda della natura della comunicazione, i messaggi di posta elettronica trapelati possono essere una potenziale fonte di imbarazzo per il mittente e l'organizzazione.

  - **Perdita del vantaggio competitivo**   Una delle minacce più gravi legate alla perdita di informazioni è la perdita del vantaggio competitivo sul mercato. La divulgazione dei piani strategici o delle informazioni sulle fusioni e le acquisizioni può comportare la perdita di fatturato o di capitalizzazione. Altre minacce comprendono la perdita di informazioni sulla ricerca, i dati analitici e altre proprietà intellettuali.

Inizio pagina

## Soluzioni standard per affrontare la perdita di informazioni

Anche se le soluzioni standard alla perdita di informazioni possono proteggere l'accesso iniziale ai dati, spesso non offrono una protezione costante. Nella seguente tabella, vengono elencate alcune soluzioni standard e i rispettivi limiti.

### Soluzioni standard

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Soluzione</th>
<th>Descrizione</th>
<th>Limiti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Transport Layer Security (TLS)</p></td>
<td><p>Il TLS è un protocollo Internet standard utilizzato per proteggere le comunicazioni in rete tramite la crittografia. In un ambiente di messaggistica, TLS viene utilizzato per garantire le comunicazioni server-server e client-server.</p>
<p>Per impostazione predefinita, Exchange 2010 utilizza TLS per tutti i trasferimenti di messaggi interni. TLS opportunistico vengono abilitate per impostazione predefinita per le sessioni con host esterno. Exchange tenta di utilizzare la crittografia TLS per la sessione, ma se sul server di destinazione non è possibile stabilire una connessione TLS, Exchange utilizza SMTP. È inoltre possibile configurare la protezione del dominio per applicare mutual TLS con organizzazioni esterne.</p></td>
<td><p>Il TLS protegge solo la sessione SMTP tra due host SMTP. In altre parole, TLS protegge le informazioni in movimento, ma non fornisce protezione a livello di messaggio o per le informazioni statiche. A meno che non vengano crittografati utilizzando un altro metodo, i messaggi nelle cassette postali del mittente e dei destinatari non vengono protetti. Per la posta elettronica inviata al di fuori dell'organizzazione, è possibile richiedere il protocollo TLS solo per il primo hop. Una volta che un host SMTP remoto al di fuori dell'organizzazione ha ricevuto il messaggio, può inoltrarlo ad un altro host SMTP con una sessione in chiaro. Dal momento che il TLS è una tecnologia di trasporto, non è in grado di fornire un controllo su ciò che il destinatario fa con il messaggio.</p></td>
</tr>
<tr class="even">
<td><p>Posta elettronica crittografata</p></td>
<td><p>Gli utenti possono utilizzare tecnologie quali S/MIME per crittografare i messaggi.</p></td>
<td><p>Sono gli utenti a decidere se crittografare un messaggio. Esistono ulteriori costi legati alla distribuzione di una infrastruttura a chiave pubblica (PKI), con il conseguente sovraccarico della gestione dei certificati per gli utenti e la protezione delle chiavi private. Una volta decrittografato un messaggio, non esiste alcun controllo su ciò che il destinatario può fare con le informazioni. Le informazioni decrittografate possono essere tranquillamente copiate, stampante o inviate ad altri. Per impostazione predefinita, gli allegati salvati non sono protetti.</p>
<p>L'organizzazione non può accedere ai messaggi crittografati che utilizzano tecnologie quali S/MIME. L'organizzazione non può controllare il contenuto del messaggio e non può quindi applicare i propri criteri di messaggistica, eseguire la scansione dei messaggi per rilevare l'eventuale presenza di virus o contenuti dannosi oppure effettuare qualsiasi altra azione che richieda l'accesso al contenuto.</p></td>
</tr>
</tbody>
</table>


Infine, le soluzioni standard spesso non dispongono di strumenti in grado di applicare i criteri di messaggistica uniformi per impedire la perdita di informazioni. Ad esempio, un utente invia un messaggio contenente informazioni riservate e lo contrassegna come **Materiale aziendale riservato** e **Non inoltrare**. Una volta recapitato il messaggio al destinatario, il mittente o l'organizzazione non ha più controllo sulle informazioni. Il destinatario può volontariamente o involontariamente inoltrare il messaggio (utilizzando funzionalità quali le regole di inoltro automatico) ad account di posta elettronica esterni, sottoponendo l'organizzazione a sostanziali rischi di perdita delle informazioni.

Inizio pagina

## IRM in Exchange 2013

In Exchange 2013 è possibile utilizzare le funzionalità IRM per applicare una protezione costante ai messaggi e agli allegati. IRM utilizza AD RMS (Active Directory Rights Management Services), una tecnologia di protezione delle informazioni in Windows Server 2008 e versioni successive. Con le funzionalità IRM di Exchange 2013, l'organizzazione e gli utenti possono controllare i diritti di cui dispongono i destinatari per la posta elettronica. IRM consente anche di autorizzare o limitare le azioni del destinatario, quali l'inoltro di un messaggio ad altri destinatari, la stampa di un messaggio o un allegato o l'estrazione del contenuto del messaggio o dell'allegato tramite copia/incolla. La protezione IRM può essere applicata dagli utenti di Microsoft Outlook o Microsoft Office Outlook Web App oppure può essere basata sui criteri di messaggistica dell'organizzazione e applicata utilizzando le regole di protezione del trasporto o le regole di protezione di Outlook. A differenza di altre soluzioni di posta elettronica crittografata, IRM consente anche all'organizzazione di decrittografare il contenuto protetto per verificarne l'aderenza ai criteri di conformità.

AD RMS utilizza licenze e certificati basati sul linguaggio XrML (eXtensible Rights Markup Language) per autenticare i computer e gli utenti e per proteggere i contenuti. Quando i contenuti, come un documento o un messaggio, sono protetto con AD RMS, viene allegata una licenza XrML contenente i diritti di cui dispongono gli utenti autorizzati sui contenuti. Per accedere al contenuto protetto tramite IRM, le applicazioni abilitate ad AD RMS devono procurarsi dal cluster AD RMS una licenza d'uso per l'utente autorizzato.


> [!NOTE]
> In Exchange 2013, l'agente di pre-licenza allega una licenza d'uso ai messaggi protetti utilizzando il cluster AD RMS dell'organizzazione. Per ulteriori dettagli, vedere Prelicensing più avanti in questo argomento.



Le applicazioni utilizzate per creare i contenuti devono essere abilitate a RMS per applicare una protezione costante ai contenuti utilizzando AD RMS. Le applicazioni di Microsoft Office, come Word, Excel, PowerPoint e Outlook sono abilitate per RMS e possono essere utilizzate per creare e utilizzare contenuti protetti.

IRM consente di effettuare le seguenti operazioni:

  - Impedire che un destinatario autorizzato di un contenuto protetto tramite IRM possa inoltrare, modificare, stampare, inviare tramite fax, salvare o tagliare e incollare tale contenuto.

  - Proteggere i formati file degli allegati supportati con lo stesso livello di protezione del messaggio.

  - Impostare una scadenza per i messaggi e gli allegati protetti tramite IRM, in modo che non possano più essere visualizzati dopo il periodo specificato.

  - Impedire che i contenuti protetti tramite IRM vengano copiati utilizzando lo Strumento di cattura in Microsoft Windows.

Tuttavia, IRM non può impedire la copia delle informazioni utilizzando i seguenti metodi:

  - Applicazioni di acquisizione schermate di terzi

  - L'uso di dispositivi di imaging, come le fotocamere, per fotografare il contenuto protetto tramite IRM visualizzato sullo schermo

  - La memorizzazione o la trascrizione manuale delle informazioni da parte degli utenti

Per ulteriori informazioni su AD RMS, vedere [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823).

## Modelli dei criteri per i diritti AD RMS

AD RMS utilizza i modelli di criteri per i diritti basati su XrML che consentono alle applicazioni abilitate a IRM compatibili di applicare i criteri di protezione coerenti. In Windows Server 2008 e versioni successive, il server AD RMS presenta un servizio Web utilizzabile per enumerare e acquisire i modelli. Exchange 2013 viene fornito con il modello Non inoltrare. Quando il modello Non inoltrare viene applicato a un messaggio, solo i destinatari specificati nel messaggio possono decrittografare il messaggio. I destinatari non possono inoltrare, copiare o stampare il messaggio. È possibile creare ulteriori modelli RMS sul server AD RMS dell'organizzazione per soddisfare le esigenze di protezione IRM.

La protezione IRM viene applicata assegnando un modello di criteri per i diritti AD RMS. Utilizzando i modelli dei criteri, è possibile controllare le autorizzazioni che i destinatari hanno su un messaggio. Azioni, come rispondere, rispondere a tutti, inoltrare, estrarre informazioni da un messaggio, salvare o stampare un messaggio, possono essere controllate applicando al messaggio un adeguato modello di criteri per i diritti.

Per ulteriori informazioni sui modelli di criteri per i diritti, vedere [Considerazioni sulla modello dei criteri di AD RMS](https://go.microsoft.com/fwlink/p/?linkid=179455).

Per ulteriori informazioni sulla creazione di modelli di criteri per i diritti AD RMS, vedere [Guida dettagliata AD RMS diritti di criteri di modelli di distribuzione](https://go.microsoft.com/fwlink/p/?linkid=136593).

Inizio pagina

## Applicazione della protezione IRM ai messaggi

In Exchange 2010, la protezione IRM può essere applicata ai messaggi utilizzando i metodi seguenti:

  - **Manuale per gli utenti di Outlook**   Gli utenti Outlook possono protetto con IRM i messaggi con i modelli dei criteri di diritti AD RMS disponibili a loro. Questo processo viene utilizzata la funzionalità IRM in Outlook e non Exchange. Tuttavia, è possibile utilizzare Exchange ai messaggi di accesso che è possibile eseguire le azioni (ad esempio, applicare le regole di trasporto) per applicare la propria organizzazione di messaggistica del criterio. Per ulteriori informazioni sull'utilizzo di IRM in Outlook, vedere [Introduzione a IRM per i messaggi di posta elettronica](https://go.microsoft.com/fwlink/p/?linkid=166897).

  - **Manualmente dagli utenti di Outlook Web App**   Quando si abilita IRM in Outlook Web App, gli utenti possono proteggere tramite IRM i messaggi inviati e visualizzare i messaggi protetti tramite IRM ricevuti. In Exchange 2013 Cumulative Update 1 (CU1) gli utenti di Outlook Web App possono visualizzare anche gli allegati protetti tramite IRM utilizzando la visualizzazione dei documenti WebReady. Per ulteriori informazioni su IRM in Outlook Web App, vedere [Information Rights Management in Outlook Web App](information-rights-management-in-outlook-web-app-exchange-2013-help.md).

  - **Manualmente dagli utenti di dispositivi Exchange ActiveSync e Windows Mobile**   Nella versione a versione di produzione (RTM) di Exchange 2010, gli utenti dei dispositivi mobili Windows possono visualizzare e creare messaggi protetti tramite IRM. Questo richiede agli utenti di dispositivi mobili supportati Windows di connettersi a un computer e attivarli per IRM. In Exchange 2010 SP1, si può abilitare IRM in Microsoft Exchange ActiveSync per consentire agli utenti di dispositivi Exchange ActiveSync (inclusi i dispositivi mobili Windows ) per visualizzare, rispondere per inoltrare e creare messaggi protetti tramite IRM. Per ulteriori informazioni su IRM in Exchange ActiveSync, vedere [Information Rights Management in Exchange ActiveSync](information-rights-management-in-exchange-activesync-exchange-2013-help.md).

  - **Automaticamente in Outlook 2010 e versioni successive**   È possibile creare le regole di protezione di Outlook per proteggere automaticamente tramite IRM i messaggi in Outlook 2010 e versioni successive. Le regole di protezione di Outlook vengono distribuite automaticamente ai client di Outlook 2010 e la protezione tramite IRM viene applicata da Outlook 2010 quando l'utente sta componendo un messaggio. Per ulteriori informazioni sulle regole di protezione di Outlook, vedere [Regole di protezione di Outlook](outlook-protection-rules-exchange-2013-help.md).

  - **Automaticamente sui Server Cassette postali**   È possibile creare le regole di protezione del trasporto per proteggere automaticamente tramite IRM i messaggi sui Server Cassette postali di Exchange 2013. Per ulteriori informazioni sulle regole di protezione del trasporto, vedere [Regole di protezione del trasporto](transport-protection-rules-exchange-2013-help.md).
    

    > [!NOTE]
    > La protezione IRM non viene applicata ai messaggi che sono già protetti tramite IRM. Ad esempio, se un utente protegge tramite IRM un messaggio in Outlook o Outlook Web App, la protezione IRM non viene applicata al messaggio utilizzando una regola di protezione del trasporto.



Inizio pagina

## Scenari per la protezione IRM

Gli scenari per la protezione IRM vengono descritti nella seguente tabella.

### Scenari per la protezione IRM

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Invio dei messaggi protetti tramite IRM</th>
<th>Supportato</th>
<th>Requisiti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>All'interno della stessa distribuzione di Exchange 2013 locale</p></td>
<td><p>Sì</p></td>
<td><p>Per i requisiti, vedere IRM Requirements più avanti in questo argomento.</p></td>
</tr>
<tr class="even">
<td><p>Tra foreste diverse di una distribuzione locale</p></td>
<td><p>Sì</p></td>
<td><p>Per i requisiti, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=199009">configurazione di AD RMS per l'integrazione con Exchange Server 2010 in più foreste diverse</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Tra una distribuzione di Exchange 2013 locale e un'organizzazione di Exchange basata su cloud</p></td>
<td><p>Sì</p></td>
<td><ul>
<li><p>Utilizzare un server AD RMS locale.</p></li>
<li><p>Esportare il dominio di pubblicazione trusted dal server AD RMS locale.</p></li>
<li><p>Importare il dominio di pubblicazione trusted nell'organizzazione basata su cloud.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>A destinatari esterni</p></td>
<td><p>No</p></td>
<td><p>Exchange 2010 non include una soluzione per l'invio di messaggi protetti tramite IRM a destinatari esterni in un'organizzazione non federata. AD RMS offre soluzioni utilizzando i criteri di protezione. È possibile configurare un criterio di attendibilità tra cluster AD RMS e account Microsoft (precedentemente noto come Windows Live ID). Per i messaggi inviati tra due organizzazioni, è possibile creare una relazione di trust federativa tra le due foreste Active Directory utilizzando Active Directory Federation Services (ADFS). Per ulteriori informazioni, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=182909">Understanding AD RMS Trust Policies</a>.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Decrittografia dei messaggi protetti tramite IRM per l'applicazione dei criteri di messaggistica

Per l'applicazione dei criteri di messaggistica e delle regole di conformità, si deve essere in grado di accedere al contenuto del messaggio crittografato. Per soddisfare i requisiti di eDiscovery derivanti da contenziosi, verifiche normative o indagini interne, è necessario anche essere in grado di cercare i messaggi crittografati. Per consentire queste attività, Exchange 2013 include le seguenti funzionalità IRM:

  - **Decrittografia di trasporto**   Per applicare i criteri di messaggistica, gli agenti di trasporto, ad esempio l'agente Regole di trasporto, deve avere accesso al contenuto del messaggio. La decrittografia di trasporto consente agli agenti di trasporto installati sui server Exchange 2013 di accedere ai contenuti del messaggio. Per ulteriori informazioni, vedere [Decrittografia di trasporto](transport-decryption-exchange-2013-help.md).

  - **Decrittografia rapporto del journal**   Per soddisfare i requisiti aziendali o di conformità, le organizzazioni possono utilizzare l'inserimento nel journal per conservare i contenuti di messaggistica. L'agente di journaling crea un rapporto del journal per i messaggi soggetti al journaling e include nel rapporto i metadati relativi al messaggio. Il messaggio originale viene allegato al rapporto del journal. Se il messaggio in un rapporto del journal è protetto tramite IRM, la decrittografia del rapporto del journal allega una copia del testo non crittografato del messaggio al rapporto del journal. Per ulteriori informazioni, vedere [Decrittografia dei rapporti del journal](journal-report-decryption-exchange-2013-help.md).

  - **Decrittografia IRM per il servizio di ricerca di Exchange**   Con la decrittografia IRM per il servizio di ricerca di Exchange, il servizio di ricerca di Exchange può indicizzare i contenuti dei messaggi protetti tramite IRM. Quando un responsabile dell'individuazione utilizza la ricerca eDiscovery sul posto, i messaggi protetti tramite IRM che sono stati indicizzati vengono inclusi nei risultati della ricerca. Per ulteriori informazioni, vedere [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md).
    

    > [!NOTE]
    > In Exchange&nbsp;2010 SP1 e versioni successive, membri del gruppo di ruoli gestione individuazione possono accedere a messaggi protetti tramite IRM restituito da una ricerca di individuazione e che risiede in una cassetta postale di individuazione. Per abilitare questa funzionalità, utilizzare il parametro <EM>EDiscoverySuperUserEnabled</EM> con <A href="https://technet.microsoft.com/it-it/library/dd979792(v=exchg.150)">Set-IRMConfiguration</A> cmdlet. Per ulteriori informazioni, vedere <A href="configure-irm-for-exchange-search-and-in-place-ediscovery-exchange-2013-help.md">Configurare IRM per la ricerca di Exchange e In-Place eDiscovery</A>.



Per abilitare queste funzionalità di decrittografia, i server Exchange devono disporre dell'accesso al messaggio. Questo si ottiene aggiungendo la cassetta postale della federazione, una cassetta postale di sistema creata dal programma di installazione di Exchange, al gruppo degli utenti con privilegi avanzati sul server AD RMS. Per i dettagli, vedere [Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

Inizio pagina

## Pre-licenza

Per visualizzare i messaggi e gli allegati protetti tramite IRM, Exchange 2013 allega automaticamente una pre-licenza ai messaggi protetti. Questa operazione evita al client di doversi collegare ripetutamente al server AD RMS per recuperare una licenza d'uso e permette la visualizzazione offline dei messaggi e degli allegati protetti tramite IRM. La pre-licenza consente anche di visualizzare i messaggi protetti tramite IRM in Outlook Web App. Quando si abilitano le funzionalità IRM, la pre-licenza viene abilitata per impostazione predefinita.

Inizio pagina

## Agenti IRM

In Exchange 2013, la funzionalità IRM viene abilitata utilizzando agenti di trasporto nel servizio di trasporto sui server Cassette postali. Gli agenti IRM vengono installati dal programma di installazione di Exchange su un server Cassette postali. Non è possibile controllare gli agenti IRM utilizzando le attività di gestione per gli agenti di trasporto.


> [!NOTE]
> In Exchange 2013 gli agenti IRM sono incorporati. Gli agenti integrati non sono inclusi nell'elenco degli agenti restituiti dal cmdlet <STRONG>Get-TransportAgent</STRONG>. Per ulteriori informazioni, vedere <A href="transport-agents-exchange-2013-help.md">Agenti di trasporto</A>.



Nella tabella riportata di seguito sono elencati gli agenti IRM implementati sui server Cassette postali.

### Agenti IRM nel servizio di trasporto sui server Cassette postali

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Agente</th>
<th>Evento</th>
<th>Funzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agente di decrittografia RMS</p></td>
<td><p>OnEndOfData (SMTP) e OnSubmittedMessage</p></td>
<td><p>Decrittografa i messaggi per consentire l'accesso agli agenti di trasporto.</p></td>
</tr>
<tr class="even">
<td><p>Agente Regole di trasporto</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>Contrassegna i messaggi che soddisfano le condizioni di una regola di protezione del trasporto per essere protetti tramite IRM dall'agente di crittografia RMS.</p></td>
</tr>
<tr class="odd">
<td><p>Agente di decrittografia RMS</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>Applica la protezione IRM ai messaggi contrassegnati dall'agente Regole di trasporto e crittografa nuovamente i messaggi decrittografati dal trasporto.</p></td>
</tr>
<tr class="even">
<td><p>Agente di pre-licenza</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>Allega una pre-licenza ai messaggi protetti tramite IRM.</p></td>
</tr>
<tr class="odd">
<td><p>Agente di decrittografia dei rapporti del journal</p></td>
<td><p>OnCategorizedMessage</p></td>
<td><p>Esegue la decrittografia dei messaggi protetti tramite IRM allegati ai rapporti del journal e allega le versioni del testo non crittografato, oltre ai messaggi crittografati originali.</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni sugli agenti di trasporto, vedere [Agenti di trasporto](transport-agents-exchange-2013-help.md).

Inizio pagina

## Requisiti IRM

Per implementare IRM nell'organizzazione di Exchange 2013, la distribuzione deve soddisfare i requisiti descritti nella tabella seguente.

### Requisiti IRM

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Server</th>
<th>Requisiti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cluster AD RMS</p></td>
<td><ul>
<li><p><strong>Sistema operativo</strong>   È necessario Windows Server 2012, Windows Server 2008 R2 o Windows Server 2008 SP2 con hotfix <a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=973247">ruolo di Active Directory Rights Management Services in Windows Server 2008</a>.</p></li>
<li><p><strong>Punto di connessione del servizio</strong> Exchange 2010 e applicazioni che supportano AD RMS utilizzano il punto di connessione del servizio registrato in Active Directory per individuare un cluster AD RMS e URL. AD RMS consente di registrare il punto di connessione del servizio dal programma di installazione di AD RMS. Se l'account utilizzato per configurare AD RMS non è un membro del gruppo di protezione Enterprise Admins, è possibile eseguire la registrazione punti di connessione del servizio al termine dell'installazione. Punto di connessione di un solo servizio ad RMS in una foresta Active Directory non esiste.   </p></li>
<li><p><strong>Autorizzazioni</strong>   Le autorizzazioni di lettura e di esecuzione per la pipeline di certificazione dei server AD RMS (file <code>ServerCertification.asmx</code> sui server AD RMS) devono essere assegnate ai seguenti elementi:</p>
<ul>
<li><p>Gruppo di server Exchange o server Exchange singoli</p></li>
<li><p>Gruppo di servizi AD RMS sui server AD RMS</p></li>
</ul>
<p>Per impostazione predefinita, il file ServerCertification asmx si trova nella cartella <code>\inetpub\wwwroot\_wmcs\certification\</code> sui server AD RMS. Per ulteriori informazioni, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=186951">Impostare le autorizzazioni nella Pipeline di certificazione AD RMS Server</a>.</p></li>
<li><p><strong>Utenti con privilegi avanzati di AD RMS</strong>   Per abilitare la decrittografia di trasporto, la decrittografia del report del journal, IRM in Outlook Web App e IRM per il servizio di ricerca di Exchange, è necessario aggiungere la cassetta postale della federazione, una cassetta postale di sistema creata dal programma di installazione di Exchange 2013, al gruppo degli utenti con privilegi avanzati sul cluster AD RMS. Per ulteriori informazioni, vedere <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS</a>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange</p></td>
<td><ul>
<li><p>Exchange 2010 o versione successiva.</p></li>
<li><p>L'hotfix <a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=973136">FIX: ArgumentNullException messaggio di errore di eccezione quando un'applicazione basata su .NET Framework 2.0 SP2 tenta di elaborare una risposta con contenuto di lunghezza zero a una richiesta asincrona del servizio ASP.NET Web: &quot;Valore non può essere null&quot;</a> è consigliato per Microsoft .NET Framework 2.0 SP2.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>Gli utenti possono proteggere tramite IRM i messaggi in Outlook. A partire da Outlook 2003, i modelli AD RMS sono supportati per la protezione dei messaggi tramite IRM.</p></li>
<li><p>regole di protezione Outlook sono una funzionalità Exchange 2010 e Outlook 2010. Le versioni precedenti di Outlook non supportano tale funzionalità.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>I dispositivi che supportano la versione di protocollo 14.1 di Exchange ActiveSync, compresi i dispositivi di Windows Mobile, possono supportare IRM in Exchange ActiveSync. L'applicazione di posta elettronica di un dispositivo mobile deve supportare il tag <strong>RightsManagementInformation</strong> definito nella versione di protocollo 14.1 di Exchange ActiveSync. In Exchange 2013, IRM in Exchange ActiveSync consente agli utenti con i dispositivi supportati di visualizzare, rispondere, inoltrare e creare i messaggi protetti tramite IRM senza richiedere il collegamento del dispositivo a un computer e l'attivazione per IRM. Per ulteriori informazioni, vedere <a href="information-rights-management-in-exchange-activesync-exchange-2013-help.md">Information Rights Management in Exchange ActiveSync</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>



> [!NOTE]
> <EM>ClusterAD RMS</EM> indica il termine utilizzato per una distribuzione di AD RMS in un'organizzazione, tra cui una distribuzione a server singolo. AD RMS indica un servizio Web. Non è necessario installare un cluster di failover di Windows Server. Per l'alta disponibilità e il bilanciamento del carico, è possibile distribuire più server AD RMS nel cluster e utilizzare il bilanciamento del carico di rete.




> [!IMPORTANT]
> In un ambiente di produzione, l'installazione di AD RMS e di Exchange sullo stesso server non è supportata.



Exchange 2013 Le funzionalità IRM supportano i formati di file di Microsoft Office. È possibile estendere la protezione IRM in altri formati di file tramite la distribuzione di programmi di protezione personalizzati. Per ulteriori informazioni sui programmi di protezione personalizzati, vedere la protezione delle informazioni e i partner [Fornitori di Software indipendenti](https://go.microsoft.com/fwlink/p/?linkid=210336)di controllo.

Inizio pagina

## Configurazione e verifica di IRM

È necessario utilizzare Exchange Management Shell per configurare le funzionalità IRM in Exchange 2013. Per configurare le singole funzionalità IRM, utilizzare il cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)). È possibile abilitare o disabilitare IRM per i messaggi interni, la decrittografia di trasporto, la decrittografia del rapporto del journal, il servizio di ricerca di Exchange e Outlook Web App. Per ulteriori informazioni sulla configurazione delle funzionalità IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

Una volta installato un server Exchange 2013, è possibile utilizzare il cmdlet [Test-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979798\(v=exchg.150\)) per eseguire i test end-to-end della distribuzione di IRM. Questi test risultano utili per verificare la funzionalità IRM subito dopo la configurazione di IRM iniziale e successivamente a intervalli regolari. Il cmdlet consente di eseguire i test riportati di seguito:

  - Controlla la configurazione di IRM per l'organizzazione Exchange 2013.

  - Verifica le informazioni sulla versione e l'hotfix del server AD RMS.

  - Verifica se in un server Exchange può essere attivata la funzionalità RMS recuperando un certificato per account con diritti (RAC) e un certificato concessore di licenze client.

  - Acquisisce i modelli di criteri per i diritti AD RMS dal server AD RMS.

  - Verifica che il mittente specificato possa inviare i messaggi protetti tramite IRM.

  - Recupera una licenza d'uso degli utenti con privilegi avanzati per il destinatario specificato.

  - Acquisisce una pre-licenza per il destinatario specificato.

Inizio pagina

## Estensione dei diritti di gestione con il connettore Rights Management

Il connettore Microsoft Rights Management (RMS) è un'applicazione facoltativa che aumenta la protezione dei dati del server Exchange 2013 utilizzando i servizi Microsoft Rights Management basati su cloud. Una volta installato, il connettore RMS assicura una protezione costante per l'intero ciclo di vita dei dati. I servizi sono personalizzabili, in modo da consentire agli utenti di definire il livello di protezione più adatto alle specifiche necessità. È possibile, ad esempio, limitare a specifici utenti l'accesso ai messaggi di posta elettronica o impostare i diritti di sola lettura per particolari messaggi.

Per ulteriori informazioni sulle connettore RMS e su come installarlo, vedere [connettore Rights Management](https://technet.microsoft.com/en-us/library/dn375964.aspx).


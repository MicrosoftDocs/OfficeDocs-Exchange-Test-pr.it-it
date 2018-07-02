---
title: 'Panoramica di servizi di Exchange 2013: Exchange 2013 Help'
TOCTitle: Panoramica di servizi di Exchange 2013
ms:assetid: 2ed45d18-2ff3-4099-b841-050eb16a416b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423542(v=EXCHG.150)
ms:contentKeyID: 74479249
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Panoramica di servizi di Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-10-20_

Durante l'installazione di Exchange Server 2013, il programma di installazione viene eseguita una serie di attività di installazione di nuovi servizi in Microsoft Windows. Un servizio è un processo in background che può essere avviato durante l'avvio del server da Windows Gestione controllo servizi. I servizi sono file eseguibili stati progettati per funzionare in modo indipendente e senza l'intervento amministrativo. Un servizio può essere eseguito tramite una modalità dell'interfaccia utente grafica o una modalità di console.

In tutte le versioni precedenti di Exchange erano inclusi componenti implementati come servizi. In ciascun ruolo del server Exchange sono compresi i servizi che fanno parte del ruolo in questione o che potrebbero essere necessari per l'esecuzione delle funzioni associate al ruolo. Alcuni servizi diventeranno attivi solo quando vengono utilizzate specifiche funzionalità.

Le sezioni in questo argomento vengono descritti i vari servizi installati da Exchange 2013 sul server cassette postali, i server Accesso Client e server Trasporto Edge. Per i servizi che sono contrassegnati come facoltativo, è possibile disattivare il servizio se che l'organizzazione non necessarie le funzionalità fornite dal servizio.

## Exchange servizi nel server cassette postali Exchange 2013

Nella tabella seguente vengono illustrati i servizi Exchange installati nei server Cassette postali.


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
<th>Nome del servizio</th>
<th>Nome breve del servizio</th>
<th>Descrizione e dipendenze</th>
<th>Tipo di avvio predefinito</th>
<th>Contesto di sicurezza</th>
<th>Dipendenze</th>
<th>Obbligatorio o facoltativo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Fornisce informazioni sulla topologia di Active Directory ai servizi di Exchange. Se il servizio viene arrestato, la maggior parte dei servizi di Exchange non potrà essere avviata.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Servizio di condivisione porte Net.Tcp</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Aggiornamento protezione da posta indesiderata di Microsoft Exchange</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Fornisce gli aggiornamenti delle definizioni di posta indesiderata SmartScreen Exchange.</p>

> [!NOTE]
> Dal 1° novembre 2016, Microsoft ha interrotto gli aggiornamenti delle definizioni spam per i filtri SmartScreen in Exchange e Outlook. Le definizioni spam SmartScreen esistenti non verranno eliminate, ma la loro efficacia si ridurrà progressivamente. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange (Eliminazione del supporto per SmartScreen in Outlook ed Exchange)</A>.


</td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Facoltativo</p></td>
</tr>
<tr class="odd">
<td><p>Gestione gruppo di disponibilità dei database di Microsoft Exchange</p></td>
<td><p>MSExchangeDagMgmt</p></td>
<td><p>Fornisce funzionalità di gestione degli archivi e del layout dei database per server Cassette postali nei gruppi di disponibilità dei database (DAG).</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p>
<p>Servizio di condivisione porte Net.Tcp</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Diagnostica di Microsoft Exchange</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Fornisce un agente che consente di monitorare l'integrità del server di Exchange.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Nessuno</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange EdgeSync</p></td>
<td><p>MSExchangeEdgeSync</p></td>
<td><p>Replica i dati del destinatario e di configurazione tra il server Cassette postali e UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) nei server Trasporto Edge sottoscritti in un canale LDAP protetto.</p>
<p>Se non si dispone di un server Trasporto Edge sottoscritto, è possibile disattivare questo servizio.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Facoltativo</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Health Manager</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Parte della disponibilità gestita che monitora l'integrità dei componenti chiave nel server Exchange.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Registro eventi di Windows</p>
<p>Strumentazione gestione Windows</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Backend IMAP4 di Microsoft Exchange</p></td>
<td><p>MSExchangeIMAP4BE</p></td>
<td><p>Per ricevere connessioni client elaborati dal servizio IMAP4 sui server Accesso Client. Per impostazione predefinita, questo servizio non è in esecuzione, in modo che i client IMAP4 non possono connettersi al server Exchange fino a questo servizio viene avviato.</p>
<p>Se non si dispone di client IMAP4, è possibile disabilitare il servizio.</p></td>
<td><p>Manuale</p></td>
<td><p>Servizio di rete</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Facoltativo</p></td>
</tr>
<tr class="even">
<td><p>Archivio informazioni di Microsoft Exchange</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>Gestisce i database delle cassette postali nel server. Se questo servizio viene arrestato, non sono disponibili database delle cassette postali nel server.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p>
<p>Chiamata di procedura remota (RPC)</p>
<p>Server</p>
<p>Registro eventi di Windows</p>
<p>Workstation</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Assistenti cassette postali di Microsoft Exchange</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>Consente l'elaborazione in background delle cassette postali nei database delle cassette postali nel server.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Replica delle cassette postali di Microsoft Exchange</p></td>
<td><p>MSExchangeMailboxReplication</p></td>
<td><p>Elabora gli spostamenti della cassetta postale e le richieste di spostamento.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p>
<p>Servizio di condivisione porte Net.Tcp</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Recapito alle cassette postali di Microsoft Exchange</p></td>
<td><p>MSExchangeDelivery</p></td>
<td><p>Riceve messaggi SMTP dal servizio di trasporto Microsoft Exchange (nei server Cassette postali locali o remoti) e li recapita a un database delle cassette postali locale tramite RPC.</p></td>
<td><p>Automatico</p></td>
<td><p>Servizio di rete</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Invio del trasporto per le cassette postali di Microsoft Exchange</p></td>
<td><p>MSExchangeSubmission</p></td>
<td><p>Riceve messaggi RPC da un database delle cassette postali locale e li invia tramite SMTP al servizio di trasporto Microsoft Exchange (nei server Cassette postali locali o remoti).</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Backend POP3 di Microsoft Exchange</p></td>
<td><p>MSExchangePOP3BE</p></td>
<td><p>Riceve le connessioni client elaborati dal servizio POP3 sui server Accesso Client. Per impostazione predefinita, questo servizio non è in esecuzione, in modo che i client POP3 non possono connettersi al server Exchange fino a questo servizio viene avviato.</p></td>
<td><p>Manuale</p></td>
<td><p>Servizio di rete</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Facoltativo</p></td>
</tr>
<tr class="even">
<td><p>Servizio Replica di Microsoft Exchange</p></td>
<td><p>MSExchangeRepl</p></td>
<td><p>Fornisce la funzionalità di replica per i database delle cassette postali in gruppi di disponibilità del database (DAG).</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Accesso client RPC di Microsoft Exchange</p></td>
<td><p>MSExchangeRPC</p></td>
<td><p>Gestisce le connessioni RPC dei client Exchange.</p></td>
<td><p>Automatico</p></td>
<td><p>Servizio di rete</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Ricerca di Microsoft Exchange</p></td>
<td><p>MSExchangeFastSearch</p></td>
<td><p>Consente di eseguire l'indicizzazione del contenuto della cassetta postale, che ottimizza le prestazioni di ricerca del contenuto.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Controller host di ricerca di Microsoft Exchange</p></td>
<td><p>HostControllerService</p></td>
<td><p>Fornisce servizi di distribuzione e gestione per applicazioni nel server di Exchange locale.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Servizio HTTP</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Estensione server Microsoft Exchange per Windows Server Backup</p></td>
<td><p>WSBExchange</p></td>
<td><p>Consente a Windows Server Backup di eseguire backup e ripristino di dati server di Exchange.</p></td>
<td><p>Manuale</p></td>
<td><p>Sistema locale</p></td>
<td><p>Nessuno</p></td>
<td><p>Facoltativo</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Service Host</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Fornisce un host servizio per i componenti Exchange che non dispongono di servizi.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Servizio di limitazione di Microsoft Exchange</p></td>
<td><p>MSExchangeThrottling</p></td>
<td><p>Consente la gestione dei carichi di lavoro degli utenti che limita la velocità delle operazioni utente (in precedenza noto come Limitazione utenti).</p></td>
<td><p>Automatico</p></td>
<td><p>Servizio di rete</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Trasporto di Microsoft Exchange</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>Fornisce il server SMTP e lo stack di trasporto.</p></td>
<td><p>Automatico</p></td>
<td><p>Servizio di rete</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p>
<p>Servizio Gestione dei filtri di Microsoft</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Ricerca dei registri di trasporto di Microsoft Exchange</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>Fornisce la funzionalità di ricerca remota per i file di registro di trasporto (ad esempio, Verifica messaggi).</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Facoltativo</p></td>
</tr>
<tr class="odd">
<td><p>Messaggistica unificata di Microsoft Exchange</p></td>
<td><p>MSExchangeUM</p></td>
<td><p>Abilita le funzionalità di messaggistica unificata (UM): consente l'archiviazione in Exchange di messaggi vocali e fax e offre agli utenti accesso telefonico a posta elettronica, posta vocale, calendario, contatti o operatore automatico. Se questo servizio viene arrestato, la messaggistica unificata non sarà disponibile.</p>
<p>Se non si usa la messaggistica unificata, è possibile disattivare questo servizio.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Isolamento chiavi CNG</p>
<p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Facoltativo</p></td>
</tr>
</tbody>
</table>


## Exchange servizi nel server Accesso Client Exchange 2013

Nella tabella seguente vengono descritti i servizi Exchange installati nel server Accesso Client.


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
<th>Nome del servizio</th>
<th>Nome breve del servizio</th>
<th>Descrizione e dipendenze</th>
<th>Tipo di avvio predefinito</th>
<th>Contesto di sicurezza</th>
<th>Dipendenze</th>
<th>Obbligatorio o facoltativo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Fornisce informazioni sulla topologia di Active Directory ai servizi di Exchange. Se il servizio viene arrestato, la maggior parte dei servizi di Exchange non potrà essere avviata.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Servizio di condivisione porte Net.Tcp</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Diagnostica di Microsoft Exchange</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Fornisce un agente che consente di monitorare l'integrità del server di Exchange.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Nessuno</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Trasporto front-end Microsoft Exchange</p></td>
<td><p>MSExchangeFrontEndTransport</p></td>
<td><p>Connessioni proxy SMTP da host esterno per il servizio di trasporto sui server cassette postali Microsoft Exchange.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Health Manager</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Parte della disponibilità gestita che monitora l'integrità dei componenti chiave nel server Exchange.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Registro eventi di Windows</p>
<p>Strumentazione gestione Windows</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4</p></td>
<td><p>MSExchangeIMAP4</p></td>
<td><p>Connessioni di client IMAP4 proxy per il servizio IMAP4 sul server cassette postali. Per impostazione predefinita, questo servizio non è in esecuzione, in modo che i client IMAP4 non possono connettersi al server Exchange fino a questo servizio viene avviato.</p>
<p>Se non si dispone di client IMAP4, è possibile disabilitare il servizio.</p></td>
<td><p>Manuale</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Facoltativo</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange POP3</p></td>
<td><p>MSExchangePOP3</p></td>
<td><p>Connessioni client di POP3 proxy per il servizio IMAP4 sul server cassette postali. Per impostazione predefinita, questo servizio non è in esecuzione, in modo che i client POP3 non possono connettersi al server Exchange fino a questo servizio viene avviato.</p></td>
<td><p>Manuale</p></td>
<td><p>Servizio di rete</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Facoltativo</p></td>
</tr>
<tr class="odd">
<td><p>Controller host di ricerca di Microsoft Exchange</p></td>
<td><p>HostControllerService</p></td>
<td><p>Fornisce servizi di distribuzione e gestione per applicazioni nel server di Exchange locale.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Servizio HTTP</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Service Host</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Fornisce un host servizio per i componenti Exchange che non dispongono di servizi.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Router delle chiamate di messaggistica unificata di Microsoft Exchange</p></td>
<td><p>MSExchangeUMCR</p></td>
<td><p>Consente di reindirizzare le connessioni client di messaggistica unificata per il servizio messaggistica unificata sui server cassette postali.</p>
<p>Se non si usa la messaggistica unificata, è possibile disattivare questo servizio.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Isolamento chiavi CNG</p>
<p>Microsoft Exchange Topologia di Active Directory</p></td>
<td><p>Facoltativo</p></td>
</tr>
</tbody>
</table>


## Exchange servizi nei server Trasporto Edge Exchange 2013

Nella tabella seguente vengono illustrati i servizi Exchange installati nei server Trasporto Edge.


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
<th>Nome del servizio</th>
<th>Nome breve del servizio</th>
<th>Descrizione</th>
<th>Tipo di avvio predefinito</th>
<th>Contesto di sicurezza</th>
<th>Dipendenze</th>
<th>Obbligatorio o facoltativo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ADAM di Microsoft Exchange</p></td>
<td><p>ADAM_MSExchange</p></td>
<td><p>Archivia i dati del destinatario e di configurazione nel server Trasporto Edge. Questo servizio rappresenta l'istanza denominata di UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) creata automaticamente dal programma di installazione di Exchange.</p></td>
<td><p>Automatico</p></td>
<td><p>Servizio di rete</p></td>
<td><p>COM+ Event System</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Aggiornamento protezione da posta indesiderata di Microsoft Exchange</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Fornisce gli aggiornamenti delle definizioni di posta indesiderata SmartScreen Exchange.</p>

> [!NOTE]
> Dal 1° novembre 2016, Microsoft ha interrotto gli aggiornamenti delle definizioni spam per i filtri SmartScreen in Exchange e Outlook. Le definizioni spam SmartScreen esistenti non verranno eliminate, ma la loro efficacia si ridurrà progressivamente. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange (Eliminazione del supporto per SmartScreen in Outlook ed Exchange)</A>.


</td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Facoltativo</p></td>
</tr>
<tr class="odd">
<td><p>Servizio credenziali di Microsoft Exchange</p></td>
<td><p>MSExchangeEdgeCredential</p></td>
<td><p>Controlla le modifiche apportate alle credenziali in UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) e le installa nel server Trasporto Edge.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Diagnostica di Microsoft Exchange</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Fornisce un agente che consente di monitorare l'integrità del server di Exchange.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Nessuno</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Health Manager</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Parte della disponibilità gestita che monitora l'integrità dei componenti chiave nel server Exchange.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Registro eventi di Windows</p>
<p>Strumentazione gestione Windows</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Service Host</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Fornisce un host servizio per i componenti Exchange che non dispongono di servizi.</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Trasporto di Microsoft Exchange</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>Fornisce il server SMTP e lo stack di trasporto.</p></td>
<td><p>Automatico</p></td>
<td><p>Servizio di rete</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Obbligatorio</p></td>
</tr>
<tr class="even">
<td><p>Ricerca dei registri di trasporto di Microsoft Exchange</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>Fornisce la funzionalità di ricerca remota per i file di registro di trasporto (ad esempio, Verifica messaggi).</p></td>
<td><p>Automatico</p></td>
<td><p>Sistema locale</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>Facoltativo</p></td>
</tr>
</tbody>
</table>


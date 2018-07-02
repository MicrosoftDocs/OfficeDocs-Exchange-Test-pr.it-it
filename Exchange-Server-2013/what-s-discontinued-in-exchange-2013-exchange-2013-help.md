---
title: 'Funzionalità sospese in Exchange 2013: Exchange 2013 Help'
TOCTitle: Funzionalità sospese in Exchange 2013
ms:assetid: 0ac0001c-b314-4108-b895-d9c0e271b489
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619283(v=EXCHG.150)
ms:contentKeyID: 50479999
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Funzionalità sospese in Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In questo argomento vengono descritti i componenti, le caratteristiche o le funzionalità che sono stati rimossi, sospesi o sostituiti in Microsoft Exchange Server 2013.


> [!NOTE]
> Potrebbero risultare di particolare interesse anche i seguenti argomenti: 
> <UL>
> <LI>
> <P><A href="what-s-new-in-exchange-2013-exchange-2013-help.md">Novità di Exchange 2013</A>&nbsp;&nbsp;&nbsp;Informazioni sulle nuove funzionalità in Exchange Server 2013.</P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=267479">Roadmap per gli sviluppatori di Exchange Server 2013</A>&nbsp;&nbsp;&nbsp;&nbsp;Vedere "tecnologie di sviluppo rimosse da Exchange? Per informazioni sulle caratteristiche di API e sviluppo sospese in Exchange 2013.</P></LI></UL>



## Funzionalità sospese da Exchange 2010 a Exchange 2013

In questa sezione, vengono riportate le funzionalità di Exchange Server 2010 non più disponibili in Exchange 2013.

## Architettura


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ruolo del server Trasporto Hub</p></td>
<td><p>Il ruolo del server Trasporto Hub è stato sostituito dai servizi di trasporto eseguiti nei ruoli server Cassette postali e Accesso client. Il ruolo server Cassette postali include il servizio di trasporto di Microsoft Exchange, il servizio di recapito del trasporto cassette postali di Microsoft Exchange e il servizio Invio del trasporto delle cassette postali di Microsoft Exchange. Il ruolo server Accesso client comprende il servizio Trasporto front-end Microsoft Exchange. Per ulteriori informazioni, vedere <a href="mail-flow-exchange-2013-help.md">Flusso di posta</a>.</p></td>
</tr>
<tr class="even">
<td><p>Ruolo del server Messaggistica unificata</p></td>
<td><p>Il ruolo del server Messaggistica unificata è stato sostituito dai servizi di messaggistica unificata eseguiti nei ruoli server Cassette postali e Accesso client. Il ruolo del server Cassette postali include il servizio Messaggistica unificata di Microsoft Exchange, mentre il ruolo del server Accesso client include il servizio Router delle chiamate di messaggistica unificata di Microsoft Exchange. Per ulteriori informazioni, vedere <a href="voice-architecture-changes-exchange-2013-help.md">Modifiche all'architettura VoIP</a>.</p></td>
</tr>
</tbody>
</table>


## Interfacce di gestione


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Management Console e Pannello di controllo di Exchange</p></td>
<td><p>Exchange Management Console e il Pannello di controllo di Exchange sono stati sostituiti dall'interfaccia di amministrazione di Exchange (EAC). Nell'interfaccia di amministrazione di Exchange viene usata la stessa directory virtuale (/ecp) del Pannello di controllo di Exchange. Per ulteriori informazioni, vedere <a href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Interfaccia di amministrazione di Exchange in Exchange 2013</a>.</p></td>
</tr>
</tbody>
</table>


## Accesso client


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2003 non è supportato</p></td>
<td><p>Per collegare Microsoft Outlook a Exchange 2013, è necessario disporre del servizio di individuazione automatica. Tuttavia, Microsoft Outlook 2003 non supporta l'utilizzo del servizio di individuazione automatica.</p></td>
</tr>
<tr class="even">
<td><p>Accesso RPC/TCP per i client Outlook</p></td>
<td><p>In Exchange 2013, i client di Microsoft Outlook possono connettersi utilizzando Outlook Anywhere (RPC/HTTP) o MAPI su HTTP in Exchange 2013 Service Pack 1, in Outlook 2013 Service Pack 1 e in versioni successive. Se nella propria organizzazione sono presenti client di Outlook, è necessario utilizzare Outlook Anywhere e/o MAPI su HTTP. Per ulteriori informazioni, vedere <a href="outlook-anywhere-exchange-2013-help.md">Outlook via Internet</a> e <a href="mapi-over-http-exchange-2013-help.md">MAPI su HTTP</a>.</p></td>
</tr>
</tbody>
</table>


## Outlook Web App e Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Controllo ortografia</p></td>
<td><p>In Outlook Web App non sono più disponibili i servizi del correttore ortografico integrato. Al contrario, utilizza la funzionalità di controllo ortografico nel browser Web.</p></td>
</tr>
<tr class="even">
<td><p>Filtri personalizzabili</p></td>
<td><p>In Outlook Web App non sono più disponibili né le visualizzazioni filtrate personalizzabili né la possibilità di salvare le visualizzazioni filtrate nei Preferiti. I filtri personalizzabili sono stati sostituiti da filtri fissi che è possibile utilizzare per visualizzare tutti i messaggi, quelli non letti, quelli inviati all'utente o quelli contrassegnati.</p></td>
</tr>
<tr class="odd">
<td><p>Contrassegni dei messaggi</p></td>
<td><p>In Outlook Web App non è disponibile la funzionalità per impostare una data personalizzata su un contrassegno per i messaggi. È possibile utilizzare Outlook per impostare le date personalizzate.</p></td>
</tr>
<tr class="even">
<td><p>Elenco contatti chat</p>
<p></p></td>
<td><p>L'elenco dei contatti chat che veniva visualizzato nell'elenco delle cartelle in Outlook Web App per Exchange 2010 non è più disponibile.</p></td>
</tr>
<tr class="odd">
<td><p>Cartelle di ricerca</p></td>
<td><p>La possibilità per gli utenti di utilizzare le cartelle di ricerca non è attualmente disponibile in Outlook Web App.</p></td>
</tr>
</tbody>
</table>


## Flusso di posta


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Connettori collegati</p></td>
<td><p>La possibilità di collegare un connettore di invio a un connettore di ricezione è stata rimossa. In particolare, è stato rimosso il parametro <em>LinkedReceiveConnector</em> da <a href="https://technet.microsoft.com/it-it/library/aa998936(v=exchg.150)">New-SendConnector</a> e da <a href="https://technet.microsoft.com/it-it/library/aa998294(v=exchg.150)">Set-SendConnector</a>.</p></td>
</tr>
</tbody>
</table>


## Protezione da posta indesiderata e antimalware


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione dell'agente di protezione da posta indesiderata in EMC</p></td>
<td><p>In Exchange 2010, quando si abilitavano gli agenti di protezione da posta indesiderata su un server Trasporto Hub, era possibile gestire tali agenti in Exchange Management Console (EMC). In Exchange 2013, quando vengono attivati gli agenti di protezione dalla posta indesiderata su un server Cassette postali, non è possibile gestire gli agenti utilizzando l'interfaccia di amministrazione di Exchange. È necessario utilizzare Shell. Per informazioni sull’abilitazione degli agenti di protezione dalla posta indesiderata in un server Cassette postali, vedere <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali</a>.</p></td>
</tr>
<tr class="even">
<td><p>Agente Filtro connessioni sui server Trasporto Hub</p></td>
<td><p>In Exchange 2010, quando si abilitavano gli agenti di protezione da posta indesiderata su un server Trasporto Hub, l'agente Filtro degli allegati era l'unico agente di protezione da posta indesiderata non disponibile. In Exchange 2013, quando si abilitano gli agenti di protezione da posta indesiderata su un server Cassette postali, non sono disponibili né l'agente Filtro degli allegati né l'agente Filtro connessioni. L'agente Filtro connessioni offre le funzionalità Elenco indirizzi disponibili ed Elenco indirizzi IP bloccati. Per informazioni sull’abilitazione degli agenti di protezione dalla posta indesiderata in un server Cassette postali, vedere <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali</a>.</p>

> [!NOTE]
> Non è possibile abilitare gli agenti di protezione da posta indesiderata sul server Accesso client di Exchange 2013. Di conseguenza, l'unico sistema per ottenere l'agente Filtro connessioni consiste nell'installazione di un server Trasporto Edge nella rete perimetrale. Per ulteriori informazioni, vedere <A href="edge-transport-servers-exchange-2013-help.md">Server Trasporto Edge</A>.


</td>
</tr>
</tbody>
</table>


## Criteri di messaggistica e conformità


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cartelle gestite</p></td>
<td><p>In Exchange 2010, utilizzare le cartelle gestite per messaggistica (MRM) gestione di conservazione. In Exchange 2013, le cartelle gestite non sono supportate. È necessario utilizzare i criteri di conservazione per la gestione record di Messaggistica.</p>

> [!NOTE]
> I cmdlet relativi alle cartelle gestite sono ancora disponibili. È possibile creare cartelle gestite, impostazioni di contenuto gestito e criteri cassetta postale per cartelle gestite, nonché applicare un criterio cassetta postale per cartelle gestite a un utente, ma l’Assistente MRM ignora l’elaborazione delle cassette postali a cui sono applicati criteri cassetta postale per cartelle gestite.


</td>
</tr>
<tr class="even">
<td><p>Procedura guidata Trasferimento della cartella gestita</p></td>
<td><p>In Exchange 2010, utilizzare la procedura guidata Trasferimento della cartella gestita per creare tag di conservazione in base alle impostazioni della cartella gestita e del contenuto gestito. In Exchange 2013, l'interfaccia di amministrazione di Exchange non comprende questa funzionalità. È possibile utilizzare il cmdlet <strong>New-RetentionPolicyTag</strong> con il parametro <em>ManagedFolderToUpgrade</em> per creare un tag di conservazione in base a una cartella gestita.</p></td>
</tr>
</tbody>
</table>


## Componenti di messaggistica unificata e casella vocale


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ricerche nelle directory tramite il riconoscimento vocale automatico (ASR, Automatic Speech Recognition)</p></td>
<td><p>In Exchange 2010, gli utenti di Outlook Voice Access possono utilizzare gli input vocali del riconoscimento vocale automatico (ASR) per cercare gli utenti elencati nella directory. Gli input vocali possono essere utilizzati in Outlook Voice Access anche per esplorare menu, messaggi e altre opzioni. Anche se un utente di Outlook Voice Access può utilizzare gli input vocali, deve comunque adoperare la tastiera del telefono per inserire il PIN ed esplorare le opzioni personali.</p>
<p>In Exchange 2013, gli utenti di Outlook Voice Access autenticati e non autenticati non possono cercare utenti nella directory utilizzando gli input del riconoscimento vocale automatico (ASR) in alcuna lingua. I chiamanti che chiamano un operatore automatico, però, possono usare gli input vocali in più lingue per esplorare i menu dell'operatore automatico e cercare utenti nella directory.</p></td>
</tr>
</tbody>
</table>


## Strumenti


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Best Practice Analyzer</p></td>
<td><p>Nella Exchange 2010 Exchange l'Analizzatore procedure consigliate esaminata la distribuzione di Exchange e determinato se la configurazione è stato in linea con procedure consigliate da Microsoft. In Exchange 2013 Exchange Best Practice Analyzer sono state sostituite con <a href="https://go.microsoft.com/fwlink/p/?linkid=391077">Office 365 Best Practices Analyzer per Exchange Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Strumento di risoluzione dei problemi del flusso di posta</p></td>
<td><p>In Exchange 2010, lo strumento di risoluzione dei problemi del flusso di posta assisteva l'utente durante la risoluzione di problemi del flusso di posta comuni. In Exchange 2013, la risoluzione dei problemi del flusso di posta è stata eliminata. Ora, è possibile utilizzare la funzionalità di verifica dei messaggi nell'interfaccia di amministrazione di Exchange in Exchange 2013. Per ulteriori informazioni, vedere <a href="track-messages-with-delivery-reports-exchange-2013-help.md">Tenere traccia dei messaggi con i rapporti di recapito</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Performance Monitor</p></td>
<td><p>In Exchange 2010, Performance Monitor era incluso nella casella degli strumenti di Exchange per consentire di raccogliere informazioni sulle prestazioni del sistema di messaggistica. Performance Monitor è in genere utilizzato per visualizzare i parametri chiave durante la risoluzione dei problemi relativi alle prestazioni. In Exchange 2013, Performance Monitor è stato rimosso dalla casella degli strumenti. È ancora possibile trovare Performance Monitor in <strong>Strumenti di amministrazione</strong> di Windows Server 2008.</p></td>
</tr>
<tr class="even">
<td><p>Risoluzione dei problemi di prestazioni</p></td>
<td><p>In Exchange 2013, la risoluzione dei problemi delle prestazioni è stata eliminata.</p></td>
</tr>
<tr class="odd">
<td><p>Visualizzatore registri di routing</p></td>
<td><p>In Exchange 2013, il visualizzatore di registri di routing è stato rimosso.</p></td>
</tr>
</tbody>
</table>


## Copie del database delle cassette postali


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Update-MailboxDatabaseCopy</p></li>
<li><p>Aggiornamento guidato copia del Database delle cassette postali</p></li>
</ul></td>
<td><p>Eseguire il seeding del catalogo dell'indice di contenuto non è più possibile dalla rete di replica. può essere eseguita solo in una rete MAPI. Questo vale anche quando si utilizza il parametro <code>-Network</code> nel cmdlet Update-MailboxDatabaseCopy.</p></td>
</tr>
</tbody>
</table>


## Funzionalità sospese da Exchange 2010 a Exchange 2007

In questa sezione, vengono riportate le funzionalità di Exchange Server 2007 non più disponibili in Exchange 2013.

## API e sviluppo


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange WebDAV</p></td>
<td><p>Utilizzare <a href="https://go.microsoft.com/fwlink/p/?linkid=167197">servizi Web Exchange</a> o <a href="https://go.microsoft.com/fwlink/p/?linkid=157179">API gestita di servizi Web Exchange</a>. In alternativa, è possibile gestire un server Exchange 2007 per le cassette postali gestite dalle applicazioni che utilizzano WebDAV. Per ulteriori informazioni, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=169474">Migrating from WebDAV</a>.</p></td>
</tr>
</tbody>
</table>


## Architettura


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gruppi di archiviazione</p></td>
<td><p>In Exchange 2013 non viene più utilizzata la costruzione del gruppo di archiviazione. Al contrario, è possibile gestire soltanto i database di cassette postali. Per ulteriori informazioni, vedere <a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Gestire il database delle cassette postali in Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>API di backup di flusso ESE (Extensible Storage Engine)</p></td>
<td><p>Exchange 2013 supporta solo backup basati sul VSS compatibili con Exchange. Exchange 2013 include un componente aggiuntivo per Windows Server Backup che consente di eseguire backup e ripristino dei dati. Per ulteriori informazioni, vedere <a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">Backup, ripristino e ripristino di emergenza</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Notifiche UDP (User Datagram Protocol)</p></td>
<td><p>Il supporto per le notifiche User Datagram Protocol (UDP) è stato rimosso da Exchange 2013. Questo influisce sull'esperienza utente quando i client di Outlook 2003 si connettono alle loro cassette postali su un server di Exchange 2013. Per ulteriori informazioni, vedere l'articolo 2009942 della Knowledge Base di Microsoft relativo all'<a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2009942">aggiornamento delle cartelle richiede molto tempo quando un utente di Exchange Server 2010 utilizza Outlook 2003 in modalità in linea</a>.</p></td>
</tr>
</tbody>
</table>


## Disponibilità elevata


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Replica continua cluster (CCR)</p></td>
<td><p>Exchange 2013 utilizza i gruppi di disponibilità del database (DAG) e le copie del database delle cassette postali. Per ulteriori informazioni, vedere <a href="high-availability-and-site-resilience-exchange-2013-help.md">Disponibilità elevata e resilienza del sito</a>.</p></td>
</tr>
<tr class="even">
<td><p>Replica continua locale (LCR)</p></td>
<td><p>Exchange 2013 utilizza i DAG e le copie del database delle cassette postali. Per ulteriori informazioni, vedere <a href="high-availability-and-site-resilience-exchange-2013-help.md">Disponibilità elevata e resilienza del sito</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Replica continua in standby (SCR)</p></td>
<td><p>Exchange 2013 utilizza i DAG e le copie del database delle cassette postali. Per ulteriori informazioni, vedere <a href="high-availability-and-site-resilience-exchange-2013-help.md">Disponibilità elevata e resilienza del sito</a>.</p></td>
</tr>
<tr class="even">
<td><p>Cluster a copia singola (SCC)</p></td>
<td><p>Exchange 2013 utilizza i DAG e le copie del database delle cassette postali. Per ulteriori informazioni, vedere <a href="high-availability-and-site-resilience-exchange-2013-help.md">Disponibilità elevata e resilienza del sito</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Setup /recoverCMS</p></td>
<td><p>Exchange 2013 utilizza Setup /m:recoverServer. Per ulteriori informazioni, vedere <a href="recover-an-exchange-server-exchange-2013-help.md">Ripristino di un server Exchange</a>.</p></td>
</tr>
<tr class="even">
<td><p>Server Cassette postali in cluster</p></td>
<td><p>Exchange 2013 utilizza i DAG e le copie del database delle cassette postali. Per ulteriori informazioni, vedere <a href="high-availability-and-site-resilience-exchange-2013-help.md">Disponibilità elevata e resilienza del sito</a>.</p></td>
</tr>
</tbody>
</table>


## Accesso client


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autenticazione client tramite l'autenticazione Windows integrata (NTLM) per gli utenti POP3 e IMAP4</p></td>
<td><p>NTLM non è supportato per la connettività dei client POP3 o IMAP4 in Exchange 2013. Connessioni da POP3 o IMAP4 programmi client tramite NTLM avrà esito negativo. Se si esegue la versione RTM di Exchange 2013, alternativa consigliata NTLM deve utilizzare l'autenticazione in testo normale con SSL.</p>
<p>Se si utilizza Exchange 2013, per utilizzare NTLM è necessario mantenere un server Exchange 2007 nell'organizzazione di Exchange 2013.</p></td>
</tr>
</tbody>
</table>


## Outlook Web App e Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accesso ai documenti</p></td>
<td><p>Non è possibile utilizzare Outlook Web App per accedere alle librerie di documenti SharePoint di Microsoft e alla condivisione file Windows.</p></td>
</tr>
<tr class="even">
<td><p>Contrassegni dei messaggi</p></td>
<td><p>In Outlook Web App 2013 non è possibile impostare una data personalizzata nei contrassegni dei messaggi. Per impostare date personalizzate, è possibile utilizzare Outlook.</p></td>
</tr>
<tr class="odd">
<td><p>Controllo ortografia</p></td>
<td><p>Outlook Web App utilizza la funzionalità di controllo ortografico nel browser Web.</p></td>
</tr>
<tr class="even">
<td><p>Cartelle di ricerca</p></td>
<td><p>La possibilità per gli utenti di utilizzare le cartelle di ricerca non è attualmente disponibile in Outlook Web App.</p></td>
</tr>
<tr class="odd">
<td><p>Numero massimo di visualizzazioni memorizzate nella cache</p></td>
<td><p>Exchange 2007 è supportata la modifica il numero massimo di visualizzazioni memorizzate nella cache per ogni parametro database (msExchMaxCachedViews) per i client Outlook. Exchange 2013 non vengono più utilizzati in questo parametro.</p></td>
</tr>
</tbody>
</table>


## Funzionalità relative ai destinatari


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cmdlet <strong>Export-Mailbox</strong> e <strong>Import-Mailbox</strong></p></td>
<td><p>In Exchange 2013, utilizzare le richieste di esportazione o importazione. Per ulteriori informazioni, vedere <a href="mailbox-import-and-export-requests-exchange-2013-help.md">Cassetta postale di importare ed esportare le richieste</a>.</p></td>
</tr>
<tr class="even">
<td><p>Gruppo di cmdlet <strong>Move-Mailbox</strong></p></td>
<td><p>In Exchange 2013, utilizzare le richieste di spostamento per spostare le cassette postali. Per ulteriori informazioni, vedere <a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Spostamenti di cassette postali di Exchange 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>ISInteg</p></td>
<td><p>In Exchange 2013, utilizzare <a href="https://technet.microsoft.com/it-it/library/ff625226(v=exchg.150)">New-MailboxRepairRequest</a>.</p></td>
</tr>
</tbody>
</table>


## Criteri di messaggistica e conformità


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cartelle gestite</p></td>
<td><p>In Exchange 2007, utilizzare cartelle gestite per la gestione della conservazione dei messaggi (MRM). In Exchange 2013, le cartelle gestite non sono supportate. È necessario utilizzare criteri di conservazione per la Gestione record di messaggistica (MRM).</p>

> [!NOTE]
> I cmdlet relativi alle cartelle gestite sono ancora disponibili. È possibile creare cartelle gestite, impostazioni di contenuto gestito e criteri cassetta postale per cartelle gestite, nonché applicare un criterio cassetta postale per cartelle gestite a un utente, ma l’Assistente MRM ignora l’elaborazione delle cassette postali a cui sono applicati criteri cassetta postale per cartelle gestite.


</td>
</tr>
</tbody>
</table>


## Componenti di messaggistica unificata e casella vocale


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Commenti e soluzioni alternative</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ricerche nelle directory tramite il riconoscimento vocale automatico (ASR) per Outlook Voice Access</p></td>
<td><p>In Exchange 2007, gli utenti di Outlook Voice Access possono utilizzare gli input vocali del riconoscimento vocale automatico in inglese (Stati Uniti) - (en-US) per cercare gli utenti elencati nella directory. Gli input vocali possono essere utilizzati in Outlook Voice Access anche per esplorare menu, messaggi e altre opzioni. Anche se un utente di Outlook Voice Access può utilizzare gli input vocali, deve comunque adoperare la tastiera del telefono per inserire il PIN ed esplorare le opzioni personali.</p>
<p>In Exchange 2013, gli utenti di Outlook Voice Access autenticati e non autenticati non possono cercare utenti nella directory utilizzando gli input del riconoscimento vocale automatico (ASR) in alcuna lingua. I chiamanti che chiamano un operatore automatico, però, possono usare gli input vocali in più lingue per esplorare i menu dell'operatore automatico e cercare utenti nella directory.</p></td>
</tr>
</tbody>
</table>


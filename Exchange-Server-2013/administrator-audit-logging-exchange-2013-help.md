---
title: "Registrazione controlli dell'amministratore: Exchange 2013 Help"
TOCTitle: Registrazione controlli dell'amministratore
ms:assetid: 22b17eb8-d8ee-4599-b202-d6a7928c20d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335144(v=EXCHG.150)
ms:contentKeyID: 50555556
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registrazione controlli dell'amministratore

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2018-03-05_

Quando un utente o un amministratore apporta una modifica all'organizzazione, per eseguire l'accesso è possibile utilizzare la funzionalità di registrazione controlli di amministrazione disponibile in Microsoft Exchange Server 2013. Grazie ai registri delle modifiche, è possibile associare ciascuna modifica all'utente che l'ha effettivamente effettuata, inserire nei registri stessi informazioni dettagliate sulle modifiche al momento della relativa implementazione, agire in conformità ai requisiti normativi e alle richieste di produzione di documenti, e altro ancora.

Per impostazione predefinita, la registrazione di controllo è abilitata nelle nuove installazioni di Exchange 2013.

**Sommario**

What gets audited

Audit logging configuration

Audit logs

Manual audit log entries

Active Directory replication

Admin Audit Log agent

## Aspetti controllati

Vengono controllati i cmdlet eseguiti direttamente in Exchange Management Shell. Inoltre, vengono registrate anche le operazioni eseguite utilizzando l'interfaccia di amministrazione di Exchange, in quanto eseguono cmdlet in background.

Cmdlet, indipendentemente da dove viene eseguite, siano possibile controllare se un cmdlet nel cmdlet controllo elenco e uno o più parametri su tale cmdlet sono nell'elenco di controllo dei parametri. Registrazione di controllo ha lo scopo di visualizzare le azioni sono state adottate per modificare gli oggetti in un'organizzazione Exchange anziché gli oggetti sono stati visualizzati.


> [!IMPORTANT]
> È possibile che un cmdlet non venga registrato se si verifica un errore prima che il cmdlet richiami l'agente di estensione cmdlet per la registrazione dei controlli dell'amministratore. Se si verifica un errore dopo il richiamo dell'agente per la registrazione dei controlli di amministrazione, il cmdlet viene registrato con l'errore associato. Per ulteriori informazioni, vedere la sezione Admin Audit Log Agent descritta più avanti in questo argomento.<BR>Le modifiche apportate utilizzando gli strumenti di gestione di Microsoft Exchange Server 2010 vengono registrate; tuttavia, le modifiche apportate utilizzando gli strumenti di gestione di Microsoft Exchange Server 2007 non vengono registrate.<BR>Le modifiche alla configurazione del registro di controllo vengono aggiornate ogni 60 minuti sui computer che hanno Shell aperto al momento delle modifiche alla configurazione. Se si desidera applicare immediatamente le modifiche, chiudere e aprire di nuovo Shell su ogni computer.<BR>Potrebbe essere necessario aspettare fino a 15 minuti dopo l'esecuzione di un comando affinché venga visualizzato nei risultati di ricerca del registro di controllo. Questo perché le voci del registro di controllo devono essere indicizzate prima di poter essere ricercate. Se un comando non viene visualizzato nel registro di controllo dell'amministratore, attendere qualche minuto ed eseguire nuovamente la ricerca.



## Configurazione della registrazione di controllo

Per impostazione predefinita, se è abilitata la registrazione di controllo, viene creata una voce di registro ogni volta che viene eseguito alcun cmdlet. Se non si desidera controllare ogni cmdlet in esecuzione, è possibile configurare la registrazione di controllo per controllare solo i cmdlet e parametri che si è interessati. Configurare la registrazione di controllo con il cmdlet **Set-AdminAuditLogConfig** . I parametri di cui viene fatto riferimento nelle sezioni seguenti vengono utilizzati con questo cmdlet.


> [!IMPORTANT]
> Le modifiche apportate alla configurazione dei registri dei controlli di amministrazione vengono sempre registrate, a prescindere che il cmdlet <STRONG>Set-AdministratorAuditLog</STRONG> sia presente nell'elenco dei cmdlet da registrare e che la registrazione dei controlli sia attivata.



Quando viene eseguito un comando, Exchange esamina il cmdlet utilizzato. Se il cmdlet eseguito corrisponde a uno qualsiasi dei cmdlet forniti con il parametro *AdminAuditLogConfigCmdlets*, Exchange controllerà quindi i parametri specificati nel parametro *AdminAuditLogConfigParameters*. Se si verifica la corrispondenza con almeno uno dei parametri presenti nell'elenco, Exchange registra il cmdlet eseguito nella cassetta postale specificata utilizzando il parametro *AdminAuditLogMailbox*. Nelle sezioni seguenti sono disponibili ulteriori informazioni su ogni aspetto della configurazione della registrazione di controllo.

Per ulteriori informazioni sulla gestione della configurazione della registrazione di controllo, vedere [Amministratore di gestire la registrazione di controllo](manage-administrator-audit-logging-exchange-2013-help.md).

Inizio pagina

## Cmdlet

È possibile verificare quali cmdlet vengono controllati fornendo un elenco di cmdlet e dei parametri relativi che si desidera registrare. Quando si configura la registrazione di controllo, è possibile specificare di controllare ogni cmdlet oppure specificare i cmdlet che si desidera controllare utilizzando il parametro *AdminAuditLogConfigCmdlets*. È possibile specificare nomi completi, ad esempio **New-Mailbox** o nomi parziali per i cmdlet e racchiuderli tra caratteri jolly, ad esempio un asterisco (`*`). Ad esempio, se si desidera eseguire la registrazione quando un cmdlet che contiene la stringa `Transport` viene eseguito, è possibile specificare un valore di `*Transport*`. È possibile utilizzare un insieme di nomi completi e parziali per i cmdlet in modo da adattare la configurazione della registrazione di controllo alle proprie esigenze.

## Parametri

Oltre a specificare quali cmdlet si desidera registrare, è possibile indicare anche che i cmdlet devono essere registrati solo se vengono utilizzati determinati parametri su tali cmdlet. Utilizzare il parametro *AdminAuditLogConfigParameters* per specificare quali parametri devono essere registrati. Come con i cmdlet, è possibile specificare per i parametri nomi completi, ad esempio `Database` o nomi parziali racchiusi tra caratteri jolly (`*`), ad esempio `*Address*` o una combinazione di entrambi.

## Periodo di validità del registro di controllo

Per impostazione predefinita, la registrazione dei controlli viene configurata in modo che ciascuna voce del registro di controllo sia memorizzata per un periodo di 90 giorni. Trascorsi 90 giorni, la voce viene eliminata. È possibile modificare il periodo di validità del registro di controllo utilizzando il parametro *AdminAuditLogAgeLimit*. ﻿Il periodo di tempo in cui si desidera che le voci del registro di controllo siano conservate può essere specificato impostando il numero di giorni, ore, minuti e secondi desiderato. Per specificare un valore, utilizzare il formato `dd.hh:mm:ss` ove si applica quanto segue:

  - **dd**   Numero di giorni in cui mantenere la voce del registro di controllo.

  - **hh**   Numero di ore in cui mantenere la voce del registro di controllo.

  - **mm**   Numero di minuti in cui mantenere la voce del registro di controllo.

  - **ss**   Numero di secondi in cui mantenere la voce del registro di controllo.

Per specificare più anni utilizzare il campo `dd`. Ad esempio, 365 giorni corrispondono a un anno, 730 a due anni e 913 a due anni e sei mesi. Per impostare il periodo di validità del registro di controllo su due anni e sei mesi, utilizzare la sintassi `913.00:00:00`.


> [!WARNING]
> ﻿È possibile impostare il periodo di validità del registro di controllo su un valore inferiore a quello corrente. In questo caso, qualsiasi voce del registro di controllo il cui periodo di validità superi il nuovo valore verrà eliminata.<BR>Se si imposta il periodo di validità su 0, Exchange elimina tutte le voci dal registro di controllo.<BR>Si consiglia di fornire l'autorizzazione per configurare il periodo di validità del registro di controllo esclusivamente a utenti estremamente fidati.



## Registrazione elevata

Per impostazione predefinita, il registro di controllo dell'amministratore registra solo il nome del cmdlet, i parametri del cmdlet (e i valori specificati), l'oggetto modificato, l'utente che ha eseguito il cmdlet, quando è stato eseguito il cmdlet e su quale server è stato eseguito. Il registro di controllo dell'amministratore non registra quali proprietà sono state modificate sull'oggetto. Se si desidera che il registro di controllo includa anche le proprietà dell'oggetto modificate, è possibile abilitare la registrazione elevata impostando il parametro *LogLevel* su `Verbose`. Quando si abilita la registrazione elevata, oltre alle informazioni registrate per impostazione predefinita, vengono incluse nel registro di controllo anche le proprietà modificate su un oggetto, inclusi i relativi valori vecchi e nuovi.

## Cmdlet di test

Per impostazione predefinita i cmdlet che iniziano con il verbo **Test** non vengono registrati. ﻿È possibile specificare la registrazione dei cmdlet **Test** impostando il parametro *TestCmdletLoggingEnabled* su `$true`. Sebbene l'attivazione della registrazione dei cmdlet di test sia consentita, si consiglia di avvalersene solo per brevi periodi di tempo, in quanto i cmdlet di test possono produrre una notevole quantità di informazioni.

## Registri di controllo

Ogniqualvolta viene registrato un cmdlet, si crea una voce di registro di controllo. I registri di controllo vengono memorizzati in una cassetta postale di arbitraggio dedicata e nascosta a cui è possibile accedere esclusivamente tramite l'uso dall'interfaccia di amministrazione di Exchange o del cmdlet **Search-AdminAuditLog** o **New-AdminAuditLogSearch**. Non possono essere aperti utilizzando Microsoft Outlook Web App o Microsoft Outlook. Nelle seguenti sezioni è possibile trovare informazioni sui seguenti argomenti:

  - Contenuto dei registri

  - Rapporti disponibili nella pagina di **controllo** dell'interfaccia di amministrazione di Exchange

  - Cmdlet di ricerca dei registri di controllo

## Contenuto dei registri di controllo

Ciascuna voce del registro di controllo contiene le informazioni descritte nella tabella seguente. Il registro di controllo contiene una o più voci. Il numero delle voci del registro di controllo dipende dal periodo di validità del registro di controllo specificato tramite il cmdlet **Set-AdminAuditLogConfig**. Qualsiasi voce di registro che superi il periodo di validità specificato viene eliminata.

### Campi di immissione del registro di controllo

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Campo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>RunspaceId</code></p></td>
<td><p>Questo campo viene utilizzato internamente da Exchange.</p></td>
</tr>
<tr class="even">
<td><p><code>ObjectModified</code></p></td>
<td><p>Questo campo contiene l'oggetto modificato dal cmdlet specificato nel campo <code>CmdletName</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletName</code></p></td>
<td><p>Questo campo contiene il nome del cmdlet eseguito dall'utente indicato nel campo <code>Caller</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletParameters</code></p></td>
<td><p>Questo campo contiene i parametri che sono stati specificati quando è stato eseguito il cmdlet indicato nel campo <code>CmdletName</code>. Sebbene non sia visibile nell'output predefinito, in questo campo viene memorizzato anche il valore specificato con il parametro (se presente). Per ulteriori informazioni su come accedere agli altri dati memorizzati in questo campo, vedere <a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">Ricerca delle modifiche al gruppo di ruoli o i registri di controllo dell'amministratore</a>.</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p>Questo campo contiene le proprietà modificate nell'oggetto indicato nel campo <code>ObjectModified</code>. Sebbene non siano visibili nell'output predefinito, in questo campo sono presenti anche il precedente valore della proprietà e quello nuovo. Per ulteriori informazioni su come accedere agli altri dati memorizzati in questo campo, vedere <a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">Ricerca delle modifiche al gruppo di ruoli o i registri di controllo dell'amministratore</a>.</p>

> [!IMPORTANT]
> Questo campo risulta pieno solo se il parametro <EM>LogLevel</EM> nel cmdlet <STRONG>Set-AdminAuditLogConfig</STRONG> è impostato su <CODE>Verbose</CODE>.


</td>
</tr>
<tr class="even">
<td><p><code>Caller</code></p></td>
<td><p>Questo campo contiene l'account utente di chi ha eseguito il cmdlet indicato nel campo <code>CmdletName</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>Succeeded</code></p></td>
<td><p>Questo campo indica se il cmdlet specificato nel campo <code>CmdletName</code> sia stato eseguito correttamente. Il valore è <code>True</code> o <code>False</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Error</code></p></td>
<td><p>Questo campo contiene il messaggio di errore che viene generato se l'esecuzione del cmdlet indicato nel campo <code>CmdletName</code> non è stata completata correttamente.</p></td>
</tr>
<tr class="odd">
<td><p><code>RunDate</code></p></td>
<td><p>Questo campo indica la data e l'ora di esecuzione del cmdlet specificato nel campo <code>CmdletName</code>. La data e l'ora vengono memorizzati in formato UTC (Coordinated Universal Time).</p></td>
</tr>
<tr class="even">
<td><p><code>OriginatingServer</code></p></td>
<td><p>Questo campo indica il server su cui è in esecuzione il cmdlet specificato nel campo <code>CmdletName</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>Questo campo viene utilizzato internamente da Exchange.</p></td>
</tr>
<tr class="even">
<td><p><code>IsValid</code></p></td>
<td><p>Questo campo viene utilizzato internamente da Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><code>ObjectState</code></p></td>
<td><p>Questo campo viene utilizzato internamente da Exchange.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Rapporti di controllo dell'interfaccia di amministrazione di Exchange

La pagina di **controllo**dell'interfaccia di amministrazione di Exchange comprende diverse rapporti che forniscono informazioni sui vari tipi di modifiche apportate alla configurazione amministrativa e di conformità. I rapporti elencati di seguito contengono informazioni sulle modifiche di configurazione effettuate nell'organizzazione:

  - **Rapporto di un gruppo di ruoli amministratore**   Questo rapporto consente di ricercare le modifiche apportate ai gruppi di ruolo di gestione nell'intervallo di tempo specificato. I risultati restituiti dalla ricerca indicano quali gruppi di ruolo sono stati modificati, da quali utenti, quando e quali modifiche sono state apportate. Il numero massimo di risultati visualizzabili è 3.000. Nel caso siano restituibili più di 3.000 voci, utilizzare il rapporto **Registro di controllo dell'amministratore** o il cmdlet **Search-AdminAuditLog**.

  - **Registro di controllo dell'amministratore**   Questo rapporto consente di esportare le voci del registro di controllo registrate in un intervallo di tempo specificato in un file XML e, quindi, di inviare tale file al destinatario desiderato. Per ulteriori informazioni sul contenuto del file XML, vedere [Struttura del Registro di controllo amministratore](administrator-audit-log-structure-exchange-2013-help.md).

Per informazioni su come utilizzare questi rapporti, vedere [Ricerca delle modifiche al gruppo di ruoli o i registri di controllo dell'amministratore](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

Per informazioni sugli altri rapporti inclusi nella pagina di **controllo**, vedere [Rapporti di controllo di Exchange](exchange-auditing-reports-exchange-2013-help.md).

## Cmdlet Search-AdminAuditLog

Quando si esegue il cmdlet **Search-AdminAuditLog**, vengono restituite tutte le voci del registro di controllo corrispondenti ai criteri di ricerca specificati. È possibile specificare i seguenti criteri:

  - **Cmdlet**   Consente di specificare i cmdlet che si desidera ricercare nel registro dei controlli di amministrazione.

  - **Parametri**   Consente di specificare i parametri, separati da virgole, che si desidera ricercare nel registro di controllo dell'amministratore. ﻿È possibile ricercare dei parametri solo se nella ricerca viene specificato un cmdlet.

  - **Data di fine**   Consente di impostare i risultati della ricerca nel registro controlli di amministrazione in modo da visualizzare solo le voci generate in corrispondenza o prima della data specificata.

  - **Data di inizio**   Consente di impostare i risultati della ricerca nel registro controlli di amministrazione in modo da visualizzare solo le voci generate in corrispondenza o dopo la data specificata.

  - **ID oggetto** Consente di specificare che devono essere restituite solo le voci del registro controlli di amministrazione contenenti gli oggetti modificati desiderati

  - **ID utente**   Consente di specificare che devono essere restituite solo le voci del registro controlli di amministrazione contenenti l'ID utente di chi ha eseguito il cmdlet desiderato.

  - **Operazione completata**   Consente di specificare se devono essere restituite solo le voci del registro controlli di amministrazione che indicano esito positivo o negativo.

Ciascuna voce del registro di controllo restituita dalla ricerca contiene le informazioni descritte nella tabella riportata nella sezione Audit Log Contents. Per impostazione predefinita, vengono restituite solo le prime 1.000 voci di registro corrispondenti ai criteri specificati. Per modificare questo valore e visualizzare un numero maggiore o inferiore di risultati utilizzare il parametro *ResultSize*. Se si desidera che la ricerca restituisca tutte le voci di registro corrispondenti ai criteri immessi, impostare il parametro *ResultSize* su `Unlimited`.

Per ulteriori informazioni sull'utilizzo del cmdlet **Search-AdminAuditLog**, vedere [Ricerca delle modifiche al gruppo di ruoli o i registri di controllo dell'amministratore](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

## Cmdlet New-AdminAuditLogSearch

Il cmdlet **New-AdminAuditLogSearch** esegue la ricerca nel registro di controllo esattamente come il cmdlet **Search-AdminAuditLog**. Tuttavia, dopo aver eseguito la ricerca, anziché mostrare i risultati in Shell, il cmdlet **New-AdminAuditLogSearch** li invia tramite messaggio di posta elettronica al destinatario specificato. I risultati sono disponibili come allegato XML del messaggio di posta elettronica.

﻿Con il cmdlet **New-AdminAuditLogSearch** è possibile utilizzare gli stessi criteri di ricerca validi per il cmdlet **Search-AdminAuditLog**. Per un elenco dettagliato di tali criteri, vedere Search-AdminAuditLog Cmdlet.

Dall'esecuzione del cmdlet **New-AdminAuditLogSearch**, Exchange può impiegare fino a 15 minuti per consegnare il rapporto al destinatario specificato. Il rapporto allegato come file XML può avere le dimensioni massime di 10 megabyte (MB). Il file XML contiene le informazioni descritte nella tabella riportata nella sezione Audit Log Contents. Per ulteriori informazioni sulla struttura del file XML, vedere [Struttura del Registro di controllo amministratore](administrator-audit-log-structure-exchange-2013-help.md).


> [!NOTE]
> Outlook Web App non consente di aprire gli allegati XML per impostazione predefinita. È possibile configurare Exchange per consentire la visualizzazione degli allegati XML con Outlook Web App oppure è possibile usare un altro client di posta elettronica, ad esempio Microsoft Outlook, per visualizzare l'allegato. Per informazioni sulla configurazione di Outlook Web App per consentire la visualizzazione di un allegato XML, vedere <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Consente di visualizzare o configurare le directory virtuali di Outlook Web App</A>.



Per ulteriori informazioni sull'utilizzo del cmdlet **New-AdminAuditLogSearch**, vedere [Ricerca delle modifiche al gruppo di ruoli o i registri di controllo dell'amministratore](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

Inizio pagina

## Voci del registro di controllo manuali

Oltre a registrare i cmdlet di Exchange tutte le volte in cui vengono eseguiti, Exchange 2013 consente di inserire manualmente le voci nel registro di controllo. Exchange 2013 supporta tale operazione tramite l'uso del cmdlet **Write-AdminAuditLog** . I casi in cui può essere necessario l'inserimento manuale di una voce di registro sono i seguenti:

  - Ingresso e uscita per uno script personalizzato

  - Modifica delle informazioni di controllo

  - Orari di inizio e fine della manutenzione

Con il cmdlet **Write-AdminAuditLog** è possibile specificare una stringa di testo da includere nel registro di controllo tramite il parametro *Comment*. Il parametro *Comment* accetta una stringa alfanumerica costituita da massimo 500 caratteri. Nella voce del registro di controllo manuale insieme alla stringa di commento sono incluse tutte le stesse informazioni ottenere quando viene registrato un cmdlet di Exchange. Per una descrizione di ciascun campo incluso nel registro di controllo, vedere la tabella in Audit Log Contents.

È possibile richiamare le voci del registro di controllo manuali esattamente come avviene con qualsiasi altra voce di registro, ovvero utilizzando la pagina di **controllo** dell'interfaccia di amministrazione di Exchange o il cmdlet **Search-AdminAuditLog** o **New-AdminAuditLogSearch**.

Per visualizzare i contenuti del parametro *Comment* del cmdlet **Write-AdminAuditLog** relativamente a una voce di registro di controllo manuale, vedere [Ricerca delle modifiche al gruppo di ruoli o i registri di controllo dell'amministratore](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

## Replica Active Directory

Controllo dell'amministratore registrazione si basa su replica Active Directory per replicare le impostazioni di configurazione specificate per i controller di dominio dell'organizzazione. A seconda delle impostazioni di replica le modifiche apportate potrebbero non essere applicate immediatamente a tutti i server che esegue Exchange 2013 o Exchange 2010 all'interno dell'organizzazione.

## Agente Registro di controllo di amministrazione

L'agente di estensione cmdlet incorporato per la registrazione dei controlli dell'amministratore esegue la registrazione delle operazioni dei cmdlet in Exchange 2013. Questo agente legge la configurazione del registro di controllo ed esegue una valutazione di ogni cmdlet eseguito nell'organizzazione. Se i criteri specificati nella configurazione del registro di controllo corrispondono al cmdlet in esecuzione, l'agente genererà una voce di controllo.

L'agente per la registrazione dei controlli dell'amministratore è abilitato per impostazione predefinita in modo che la registrazione di controllo funzioni correttamente. Non può essere disabilitato né è possibile modificarne la priorità. Per ulteriori informazioni sugli agenti di estensione cmdlet, vedere [Agenti di estensione di cmdlet](cmdlet-extension-agents-exchange-2013-help.md).


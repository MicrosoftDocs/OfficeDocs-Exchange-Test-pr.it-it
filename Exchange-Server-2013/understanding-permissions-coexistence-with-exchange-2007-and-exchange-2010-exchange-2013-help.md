---
title: 'Info. su coesistenza autorizz. Exchange 2007/Exchange 2010: Exchange 2013 Help'
TOCTitle: Informazioni sulla coesistenza delle autorizzazioni con Exchange 2007 ed Exchange 2010
ms:assetid: 28ab1433-23ee-4914-8f21-9a32578792e5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335157(v=EXCHG.150)
ms:contentKeyID: 54915143
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Informazioni sulla coesistenza delle autorizzazioni con Exchange 2007 ed Exchange 2010

 

_**Si applica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Quando si installa Microsoft Exchange Server 2013 in un'organizzazione di Microsoft Exchange Server 2010 o Microsoft Exchange Server 2007 esistente, è necessario sapere come funzioneranno le autorizzazioni nella nuova organizzazione. Leggere di seguito la sezione relativa alla propria organizzazione.

  - Installing Exchange 2013 into an existing Exchange 2010 organization

  - Installing Exchange 2013 into an existing Exchange 2007 organization

## Installazione di Exchange 2013 in un'organizzazione di Exchange 2010 esistente

Exchange 2013 utilizza lo stesso modello di autorizzazioni di ruolo basato su accesso controllo sui ruoli utilizzato in Exchange 2010. Quando si installa Exchange 2013 in un'organizzazione Exchange 2010 esistente, la stessa gruppi di ruoli di gestione, ruoli di gestione e gli ambiti di gestione si applicano a server Exchange 2013 e Exchange 2010 e destinatari. I membri di gruppi di ruoli o gli utenti assegnati a ruoli, è possono amministrare qualsiasi server Exchange 2013 o Exchange 2013 o destinatari inclusi nell'ambito del gruppo di ruoli o ruolo. Se non si utilizzano gli ambiti all'interno dell'organizzazione e si desidera che i membri dei gruppi di ruolo esistente per gestire i destinatari e i server Exchange 2010 ed Exchange 2013, non è necessario eseguire altre operazioni. Gli amministratori saranno in grado di gestire i server Exchange 2013 e i destinatari che vengono aggiunti all'organizzazione. Se è necessario un promemoria sul funzionamento delle autorizzazioni di Exchange 2010 ed Exchange 2013, vedere [Autorizzazioni](permissions-exchange-2013-help.md).

Nella nuova organizzazione, si potrebbe desidera rare di separare la gestione dei server e destinatari di Exchange 2010 e Exchange 2013. Il gruppo di amministratori responsabile della gestione dei server e destinatari di Exchange 2010 potrebbe non avere l'autorizzazione alla gestione dei server e destinatari di Exchange 2013 e viceversa. In questo caso, è possibile utilizzare gli ambiti di gestione per definire i server e destinatari per i quali ogni gruppo di amministratori deve avere l'autorizzazione alla gestione. Dopo aver creato gli ambiti desiderati, è possibile copiare i gruppi di ruoli esistenti, aggiungere gli amministratori che ne devono fare parte, quindi aggiungere gli ambiti a questi gruppi di ruoli. Al termine di queste operazioni, i membri di ogni gruppo di ruoli saranno in grado di gestire solo i server e i destinatari che corrispondono ai propri ambiti.

Per ulteriori informazioni su gruppi di ruoli, ambiti, copia dei gruppi di ruoli e aggiunta degli ambiti ai gruppi di ruoli, vedere i seguenti argomenti:

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Creare un ambito normale o esclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md)

  - [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md)

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

## Installazione di Exchange 2013 in un'organizzazione di Exchange 2010 esistente

Exchange 2013 include autorizzazioni del controllo di accesso basato sui ruoli (RBAC, Role Based Access Control) che sostituiscono il modello di autorizzazioni basato sulla voce di controllo di accesso (ACE) di Active Directory in Microsoft Exchange Server 2007. Le autorizzazioni RBAC costituiscono il meccanismo di autorizzazioni utilizzato per la maggior parte della gestione di Exchange 2013. Questo meccanismo comprende le seguenti aree di gestione:

  - Exchange Management Shell

  - Interfaccia di amministrazione di Exchange (EAC)

  - Servizi Web di Exchange

Per ulteriori informazioni su come pianificare la coesistenza tra Exchange 2013 e Exchange 2007, vedere [Aggiornamento da Exchange 2007 a Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md).

Per informazioni sulle attività di gestione relative alle autorizzazioni, vedere [Autorizzazioni](permissions-exchange-2013-help.md).

## Autorizzazioni in formato Exchange 2013

Il modello delle autorizzazioni RBAC di Exchange 2013 è costituito dai gruppi dei ruoli di gestione a cui viene assegnato uno dei diversi ruoli di gestione. I ruoli di gestione contengono le autorizzazioni che consentono agli amministratori di eseguire le attività nell'organizzazione di Exchange. Gli amministratori vengono aggiunti come membri dei gruppi di ruoli e vengono loro concesse tutte le autorizzazioni previste dai ruoli. Nella tabella seguente viene riportato un esempio dei gruppi di ruoli, di alcuni ruoli assegnati ai gruppi di ruoli e una descrizione del tipo di utente che potrebbe essere membro del gruppo di ruoli.

### Esempi di gruppi di ruolo e di ruoli in Exchange 2013

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Gruppo dei ruoli di gestione</th>
<th>Ruoli di gestione</th>
<th>Membri di questo gruppo di ruoli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>Di seguito vengono riportati alcuni ruoli assegnati a questo gruppo di ruoli:</p>
<ul>
<li><p>Elenchi indirizzi</p></li>
<li><p>Exchange Servers</p></li>
<li><p>Inserimento nel journal</p></li>
<li><p>Destinatari di posta</p></li>
<li><p>Cartelle pubbliche</p></li>
</ul></td>
<td><p>Gli utenti che gestiscono l'intera organizzazione di Exchange 2013 devono essere membri di questo gruppo di ruoli. Con alcune eccezioni, i membri di questo gruppo di ruolo possono gestire quasi ogni aspetto dell'organizzazione di Exchange 2013.</p>
<p>Per impostazione predefinita, l'account utente utilizzato per preparare Active Directory per Exchange 2013 è un membro di questo gruppo di ruolo.</p>
<p>Per ulteriori informazioni su questo gruppo di ruoli e per un elenco completo dei ruoli assegnati al gruppo di ruoli, vedere <a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a>.</p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione in sola visualizzazione</p></td>
<td><p>A questo gruppo vengono assegnati i seguenti ruoli:</p>
<ul>
<li><p>Monitoraggio</p></li>
<li><p>Configurazione di sola lettura</p></li>
<li><p>Destinatari di sola lettura</p></li>
</ul></td>
<td><p>Gli utenti che visualizzano la configurazione dell'intera organizzazione di Exchange 2013 devono essere membri di questo gruppo di ruoli. Gli utenti devono essere in grado di visualizzare la configurazione del server e le informazioni sui destinatari e di eseguire le funzioni di monitoraggio senza poter modificare la configurazione dell'organizzazione o dei destinatari.</p>
<p>Per ulteriori informazioni su questo gruppo di ruoli, vedere <a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Gestione destinatari</p></td>
<td><p>A questo gruppo vengono assegnati i seguenti ruoli:</p>
<ul>
<li><p>Gruppi di distribuzione</p></li>
<li><p>Cartelle pubbliche abilitate alla posta</p></li>
<li><p>Creazione destinatario di posta</p></li>
<li><p>Destinatari di posta</p></li>
<li><p>Verifica messaggi</p></li>
<li><p>Migrazione</p></li>
<li><p>Sposta cassette postali</p></li>
<li><p>Criteri del destinatario</p></li>
</ul></td>
<td><p>Gli utenti che gestiscono i destinatari quali cassette postali, contatti e gruppi di distribuzione nell'organizzazione di Exchange 2013 devono essere membri di questo gruppo di ruoli. Tali utenti possono creare destinatari, modificare o eliminare destinatari esistenti o spostare cassette postali.</p>
<p>Per ulteriori informazioni su questo gruppo di ruoli e per un elenco completo dei ruoli assegnati al gruppo di ruoli, vedere <a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a>.</p></td>
</tr>
<tr class="even">
<td><p>Gestione server</p></td>
<td><p>Di seguito vengono riportati alcuni ruoli assegnati a questo gruppo di ruoli:</p>
<ul>
<li><p>Database</p></li>
<li><p>Connettori di Exchange</p></li>
<li><p>Server Exchange</p></li>
<li><p>Connettori di ricezione</p></li>
<li><p>Code di trasporto</p></li>
</ul></td>
<td><p>Gli utenti che gestiscono la configurazione del server Exchange, come i connettori di ricezione, i certificati, i database e le directory virtuali devono essere membri di questo gruppo di ruoli. Gli utenti possono modificare la configurazione del server Exchange, creare database, riavviare e gestire le code di trasporto.</p>
<p>Per ulteriori informazioni su questo gruppo di ruoli e per un elenco completo dei ruoli assegnati al gruppo di ruoli, vedere <a href="server-management-exchange-2013-help.md">Server Management</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Gestione individuazione</p></td>
<td><p>A questo gruppo vengono assegnati i seguenti ruoli:</p>
<ul>
<li><p>Conservazione legale</p></li>
<li><p>Ricerca cassette postali</p></li>
</ul></td>
<td><p>Gli utenti che eseguono ricerche di cassette postali per supportare i procedimenti legali o per configurare le conservazioni legali devono essere membri di questo gruppo di ruoli.</p>
<p>Di seguito viene riportato l'esempio di un gruppo di ruoli che può contenere amministratori non di Exchange, come il personale dell'ufficio legale. Il personale dell'ufficio legale può eseguire le attività senza l'intervento da parte degli amministratori di Exchange.</p>
<p>Per ulteriori informazioni su questo gruppo di ruoli e per un elenco completo dei ruoli assegnati al gruppo di ruoli, vedere <a href="discovery-management-exchange-2013-help.md">Gestione individuazione</a>.</p></td>
</tr>
</tbody>
</table>


Come mostrato in questa tabella, Exchange 2013 fornisce un controllo preciso sulle autorizzazioni concesse agli amministratori. In Exchange 2013, è possibile scegliere tra 12 gruppi di ruoli. Per un elenco completo dei gruppi di ruoli e delle autorizzazioni fornite, vedere [Gruppi di ruoli incorporati](built-in-role-groups-exchange-2013-help.md).

Poiché Exchange 2013 offre numerosi gruppi di ruoli e perché ulteriormente la personalizzazione è possibile mediante la creazione di gruppi di ruolo contenenti le combinazioni di diversi ruoli, la manipolazione di controllo di accesso (ACL) vengono elencati per gli oggetti Active Directory è più necessario e non produce alcun effetto. Gli elenchi ACL non vengono più utilizzati per applicare le autorizzazioni per gli amministratori o i gruppi in Exchange 2013. Tutte le attività, ad esempio un amministratore quando si crea una cassetta postale o un utente accede a una cassetta postale, vengono gestite da RBAC. RBAC autorizza l'attività e quindi Exchange esegue le attività per conto dell'utente se è consentito. Exchange esegue le attività nel gruppo di protezione universale (USG) sottosistema Trusted Exchange. Con alcune eccezioni, tutti gli elenchi ACL su oggetti in Active Directory che Exchange 2010 deve viene concesso l'accesso a Exchange Trusted Subsystem gruppo di protezione universale. Si tratta di una modifica fondamentale dalla modalità di gestione delle autorizzazioni in Exchange 2007.

Le autorizzazioni concesse a un utente in Active Directory sono separate dalle autorizzazioni concesse all'utente dal controllo dell'accesso basato sui ruoli (RBAC) quando l'utente utilizza gli strumenti di gestione di Exchange 2013.

Per ulteriori informazioni su RBAC, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

## Autorizzazioni in formato Exchange 2007

Per definire i limiti di sicurezza, il modello amministrativo di Exchange 2007 utilizza le foreste di Active Directory. Non esiste alcun isolamento delle autorizzazioni di sicurezza all'interno di una foresta specifica. I proprietari delle foreste e gli amministratori dell'organizzazione possono accedere sempre a tutte le risorse in qualsiasi dominio. In Exchange 2007, può essere necessario concedere solo temporaneamente i diritti agli amministratori dell'organizzazione e agli amministratori del dominio di primo livello.

Exchange 2007 fornisce i seguenti ruoli di amministratore predefiniti:

  - **Ruolo Exchange Organization Administrator**   Questo ruolo concede le autorizzazioni a controllare tutti gli aspetti dell'organizzazione di Exchange 2007. Inoltre, un amministratore che dispone di questo ruolo può concedere le autorizzazioni ad altri amministratori di Exchange. Questo ruolo viene concesso all'account utilizzato per installare Exchange 2007.

  - **Ruolo Amministratore di Exchange solo visualizzazione**   Questo ruolo concede le autorizzazioni a visualizzare la configurazione di Exchange. Tuttavia, un amministratore che dispone di questo ruolo non può modificare gli oggetti nell'organizzazione di Exchange 2007.

  - **Ruolo Amministratore destinatari di Exchange**   Questo ruolo concede le autorizzazioni a gestire i destinatari di posta elettronica. Un amministratore che dispone di questo ruolo può modificare gli elementi correlati a Exchange per utenti, gruppi, contatti e gruppi di distribuzione.

  - **Ruolo Amministratore di Exchange Server**   Questo ruolo concede le autorizzazioni a gestire un server specifico. Tuttavia, questo ruolo non concede le autorizzazioni a eseguire le azioni che comportano un impatto globale sull'organizzazione di Exchange 2007.

  - **Ruolo Amministratore cartelle pubbliche di Exchange**   Questo ruolo è stato aggiunto in Exchange 2007 Service Pack 1**.** Questo ruolo concede le autorizzazioni a gestire le cartelle pubbliche nell'organizzazione di Exchange 2007.

Questo modello di autorizzazione utilizza gruppi USG per tutti i ruoli, ad eccezione del ruolo Exchange Server Administrator. Quando si esegue il comando Exchange 2007**Setup /PrepareAD**, il programma di installazione crea i gruppi USG nel dominio radice e assegna un ambito a livello di foresta ai gruppi USG. Ai gruppi USG vengono assegnati gli elenchi ACL per gestire gli oggetti Exchange in tutto Active Directory.

In Exchange 2007, è possibile separare gli amministratori assegnando loro vari ruoli. Le autorizzazioni vengono assegnate direttamente all'utente o al gruppo USG di cui l'utente è membro. Tutte le azioni eseguite dall'utente si svolgono nel contesto dell'account di Active Directory dell'utente. Nella tabella seguente vengono elencati i ruoli di amministratore di Exchange 2007 con le relative autorizzazioni correlate a Exchange.

### Ruoli di amministratore di Exchange 2007

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo di amministratore</th>
<th>Membri</th>
<th>Membro di</th>
<th>Autorizzazioni di Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Organization Administrator</p></td>
<td><p>L'account amministratore o l'account utilizzato per installare il primo server Exchange 2007</p></td>
<td><p>Amministratore destinatari di Exchange</p>
<p>Gruppo locale Administrators di <em>&lt;nome server&gt;</em></p></td>
<td><p>Controllo completo del contenitore di Microsoft Exchange in Active Directory</p></td>
</tr>
<tr class="even">
<td><p>Amministratore di Exchange solo visualizzazione</p></td>
<td><p>Amministratori destinatari di Exchange</p>
<p>Exchange Server Administrators (<em>&lt;nome server</em>&gt;)</p></td>
<td><p>Amministratori destinatari di Exchange</p>
<p>Exchange Server Administrators</p></td>
<td><p>Accesso in lettura al contenitore di Microsoft Exchange in Active Directory</p>
<p>Accesso in lettura a tutti i domini di Windows che dispongono dei destinatari di Exchange</p></td>
</tr>
<tr class="odd">
<td><p>Amministratore destinatari di Exchange</p></td>
<td><p>Exchange Organization Administrators</p></td>
<td><p>Amministratori di Exchange solo visualizzazione</p></td>
<td><p>Controllo completo delle proprietà di Exchange per gli oggetti utente di Active Directory</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server Administrator</p></td>
<td><p>Exchange Organization Administrators</p></td>
<td><p>Amministratori di Exchange solo visualizzazione</p>
<p>Gruppo locale Administrators di <em>&lt;nome server</em>&gt;</p></td>
<td><p>Controllo completo di <em>&lt;nome server</em>&gt; Exchange</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>Ogni account computer di Exchange 2007</p></td>
<td><p>Amministratori di Exchange solo visualizzazione</p></td>
<td><p>Speciali</p></td>
</tr>
<tr class="even">
<td><p>Amministratore cartelle pubbliche di Exchange</p></td>
<td><p>Exchange Organization Administrators</p></td>
<td><p>Amministratori di Exchange solo visualizzazione</p></td>
<td><p>Controllo completo per gestire tutte le cartelle pubbliche (con il diritto esteso per la creazione della cartella pubblica principale)</p></td>
</tr>
</tbody>
</table>


Se è necessario assegnare più precisamente le autorizzazioni, è possibile modificare gli elenchi ACL per i singoli oggetti Exchange 2007, come gli elenchi di indirizzi o i database. È necessario aggiungere l'utente, o il gruppo di sicurezza a cui appartiene l'utente, direttamente all'elenco ACL. Le azioni vengono quindi eseguite nel contesto dell'utente specifico.

Per ulteriori informazioni riguardo alla gestione delle autorizzazioni in Exchange 2007, vedere l'articolo relativo alla [configurazione delle autorizzazioni in Exchange Server 2007](http://go.microsoft.com/fwlink/p/?linkid=90671).

## Autorizzazioni di coesistenza tra Exchange 2013 ed Exchange 2007

Siccome i modelli delle autorizzazioni per Exchange 2013 e per Exchange 2007 sono diversi, le assegnazioni delle autorizzazioni di Exchange 2013 vengono separate da quelle di Exchange 2007. Ciò accade anche se entrambe le versioni di Exchange sono installate nella stessa foresta. Senza ulteriori attività di configurazione, gli amministratori di Exchange 2013 non dispongono delle autorizzazioni necessarie per gestire server basati su Exchange 2007 e gli amministratori di Exchange 2007 non dispongono delle autorizzazioni necessarie per gestire server basati su Exchange 2013. È necessario considerare le seguenti domande:

  - Si desidera concedere l'accesso agli amministratori di Exchange 2013 per gestire i server Exchange 2007?

  - Si desidera concedere l'accesso agli amministratori di Exchange 2007 per gestire i server Exchange 2013?

  - Si desidera personalizzare le autorizzazioni di Exchange 2013 in modo che corrispondano a tutte le personalizzazioni realizzate per gli elenchi ACL di Exchange 2007?

## Concessione delle autorizzazioni di Exchange 2013 agli amministratori di Exchange 2007

Se si desidera che gli amministratori di Exchange 2007 gestiscano i server Exchange 2013, è necessario aggiungere gli amministratori di Exchange 2007 come membri di uno o più gruppi di ruoli di Exchange 2013. Ai gruppi di ruoli è possibile aggiungere utenti o gruppi USG. Le autorizzazioni concesse ai gruppi di ruoli vengono quindi applicate agli utenti o ai gruppi USG aggiunti come membri.


> [!IMPORTANT]
> Se si utilizzano gruppi di protezione di Active Directory per un dominio locale o globale, è necessario modificarli in gruppi di protezione universali (USG) per aggiungerli come membri di un gruppo di ruolo di Exchange 2013. Exchange 2013 supporta solo i gruppi di protezione universali (USG).



Nella tabella seguente viene descritto il mapping tra i ruoli di amministratore di Exchange 2007 e i gruppi di ruoli di Exchange 2013.

### Ruoli di amministratore di Exchange 2007 e gruppi di ruoli di Exchange 2010

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo di amministratore di Exchange 2007</th>
<th>Gruppo di ruolo di Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Organization Administrator</p></td>
<td><p>Gestione organizzazione</p></td>
</tr>
<tr class="even">
<td><p>Amministratore destinatari di Exchange</p></td>
<td><p>Gestione destinatari</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server Administrator</p></td>
<td><p>Gestione server</p></td>
</tr>
<tr class="even">
<td><p>Amministratore di Exchange solo visualizzazione</p></td>
<td><p>Gestione organizzazione in sola visualizzazione</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>Nessun gruppo di ruoli equivalente in Exchange 2013</p>
<p>Per ulteriori informazioni sulla creazione dei gruppi di ruoli personalizzati, vedere<a href="manage-role-groups-exchange-2013-help.md">Gestire gruppi di ruoli</a>.</p></td>
</tr>
<tr class="even">
<td><p>Amministratore cartelle pubbliche di Exchange</p></td>
<td><p>Gestione cartelle pubbliche</p></td>
</tr>
</tbody>
</table>


Se tutti gli amministratori di Exchange 2007 sono membri di un ruolo amministrativo di Exchange 2007, è possibile aggiungere i membri di ogni gruppo amministrativo al gruppo di ruoli di Exchange 2013 equivalente. Ad esempio, se si desidera concedere a tutti gli amministratori dell'organizzazione di Exchange 2007 l'accesso completo agli oggetti Exchange 2013, aggiungere il gruppo USG Exchange Organization Administrators al gruppo di ruoli Gestione organizzazione.

Per ulteriori informazioni sull'aggiunta degli utenti e dei gruppi USG ai gruppi di ruoli, vedere [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).

Se si modificano gli elenchi ACL per gli oggetti Exchange 2007 per concedere autorizzazioni più precise agli amministratori di Exchange 2007 e si desidera assegnare autorizzazioni simili per i server Exchange 2013 agli amministratori, attenersi alla seguente procedura:

1.  Controllare le personalizzazioni ACL apportate agli oggetti Exchange 2007 e individuare gli amministratori a cui sono state concesse le autorizzazioni per ogni oggetto.

2.  Classificare ogni oggetto Exchange 2007. Ad esempio, stabilire se si tratta di un oggetto database, server o destinatario.

3.  Mappare gli oggetti al gruppo di ruolo di Exchange 2013 corrispondente. Per un elenco dei gruppi di ruoli incorporati, vedere [Gruppi di ruoli incorporati](built-in-role-groups-exchange-2013-help.md).

4.  Aggiungere i gruppi USG o gli utenti per ogni tipo di oggetto ai gruppi di ruoli di Exchange 2013 corrispondenti. Per ulteriori informazioni sull'aggiunta degli utenti e dei gruppi USG ai gruppi di ruoli, vedere [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).

Una volta completata la procedura, gli amministratori di Exchange 2007 saranno membri dello specifico gruppo di ruoli mappato agli oggetti Exchange 2013 appropriati. Gli amministratori di Exchange 2007 possono utilizzare gli strumenti di gestione di Exchange 2013 per gestire i server e i destinatari di Exchange 2013.


> [!IMPORTANT]
> In generale, i server e i destinatari di Exchange&nbsp;2007 devono essere gestiti mediante gli strumenti di gestione di Exchange&nbsp;2007, mentre i server e i destinatari di Exchange 2013 mediante gli strumenti di gestione di Exchange 2013.



Se i gruppi di ruoli incorporati non forniscono lo specifico insieme di autorizzazioni che si desidera concedere ad alcuni amministratori, è possibile creare gruppi di ruoli personalizzati. Quando si crea un gruppo di ruoli personalizzato, è possibile selezionare i ruoli da aggiungere al gruppo. È possibile definire le funzionalità specifiche da rendere membri del gruppo di ruoli da gestire. Ad esempio, per fare in modo che gli amministratori gestiscano solo i gruppi di distribuzione, è possibile creare un gruppo di ruoli personalizzato, quindi selezionare solo il ruolo Gruppi di distribuzione. Al termine dell'operazione, i membri del gruppo di ruoli personalizzato possono gestire solo i gruppi di distribuzione. Per ulteriori informazioni sulla creazione dei gruppi di ruolo personalizzati, vedere[Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

Se si assegnano le autorizzazioni selettive a determinati oggetti Exchange 2007 (ad esempio, consentire agli amministratori di gestire solo specifici database) e se si desidera applicare la stessa configurazione ai server Exchange 2013, vedere "Nuova creazione della personalizzazione ACL di Exchange 2007 utilizzando gli ambiti di gestione in Exchange 2013" più avanti in questo argomento.

## Concessione delle autorizzazioni di Exchange 2007 agli amministratori di Exchange 2013

Se si desidera che gli amministratori di Exchange 2013 gestiscano i server Exchange 2007, aggiungere gli amministratori di Exchange 2013 ai gruppi USG o al gruppo di sicurezza corrispondente allo specifico ruolo di amministratore di Exchange 2007. In alternativa, se si dispone delle impostazioni ACL personalizzate, aggiungere gli amministratori agli elenchi ACL appropriati. Quelli di ruoli sono gruppi USG, quindi possono essere aggiunti direttamente ai gruppi USG dei ruoli di amministratore di Exchange 2007.

Una volta terminata l'operazione, gli amministratori di Exchange 2013 saranno membri del ruolo o dei ruoli di amministratore di Exchange 2007 appropriati. Gli amministratori di Exchange 2013 possono utilizzare gli strumenti di gestione di Exchange 2007 per gestire i server e i destinatari di Exchange 2007.

## Nuova creazione della personalizzazione ACL di Exchange 2007 utilizzando ambiti di gestione di Exchange 2013

In Exchange 2007, quando si desidera limitare il numero di amministratori di un archivio specifico delle cassette postali, degli utenti specifici o per controllare in quale archivio vengono create le cassette postali, è necessario modificare gli elenchi ACL per gli oggetti che si desidera limitare. Exchange 2013 fornisce le stesse capacità, ma senza la necessità di modificare gli elenchi ACL. L'operazione viene eseguita utilizzando gli ambiti di gestione, un componente del controllo dell'accesso basato sui ruoli (RBAC).

Gli ambiti di gestione forniscono ambiti incorporati e personalizzati per definire gli oggetti gestibili dagli amministratori. Applicando gli ambiti di gestione, è possibile definire i destinatari amministrabili, in quali database vengono create le cassette postali e i destinatari o i server amministrati solo da un piccolo gruppo di amministratori.

È possibile creare i seguenti tipi di ambiti di gestione:

  - **Relativi predefiniti**   Gli ambiti relativi predefiniti sono compresi in Exchange 2013. È possibile controllare l'ambito di visualizzazione e le modifiche apportate da un utente. Ad esempio, gli ambiti relativi predefiniti consentono di controllare se gli utenti visualizzano solo le informazioni personali o le informazioni sull'intera organizzazione.

  - **Destinatario**   Gli ambiti dei destinatari determinano i destinatari che un amministratore può creare, modificare o eliminare. Queste selezioni possono essere basate su un'unità organizzativa (OU), un filtro destinatari o entrambi. I filtri destinatari specificano i criteri a cui deve corrispondere un destinatario per essere incluso nell'ambito. Ad esempio, è possibile creare un ambito di filtro destinatari che comprenda tutti gli utenti di una determinata posizione o di un reparto specifico. È possibile anche combinare le unità organizzative (OU) e i filtri destinatari in modo che corrispondano solo agli utenti che si trovano all'interno di una specifica unità organizzativa e che rispondono a un manager specifico.

  - **Server**   Gli ambiti dei server controllano i server gestibili da un amministratore. È possibile specificare gli elenchi o i filtri di server. Per gli elenchi di server, definire un elenco statico di server gestibili. I filtri di server funzionano come i filtri destinatari, in cui è possibile specificare i criteri da soddisfare. Ad esempio, è possibile creare un ambito di server che corrisponda a tutti i server di un sito di Active Directory specifico.

  - **Database**   Gli ambiti dei database consentono di controllare i database gestibili da un amministratore. Consentono di controllare anche i database in cui possono essere create le cassette postali o i database in cui possono essere spostate le cassette postali. Come gli ambiti di server, possono essere definiti come elenchi o filtri. Ad esempio, è possibile creare un elenco o un filtro che consenta agli amministratori di creare o spostare le cassette postali in specifici database delle cassette postali gestiti da una determinata filiale.

  - **Esclusivi**   Gli ambiti di destinatari, server e database possono essere creati anche come ambiti esclusivi. Gli ambiti esclusivi funzionano come le voci ACE di negazione negli elenchi ACL. Se un oggetto corrisponde a un ambito esclusivo, solo gli amministratori assegnati a un ambito esclusivo possono gestire l'oggetto. Questa condizione è vera anche se un altro ambito non esclusivo corrisponde allo stesso oggetto. Questa soluzione risulta particolarmente utile quando si desidera che solo poche persone molto attendibili siano in grado di gestire la cassetta postale di un dirigente. Anche se un altro ambito di destinatari normale è più ampio e comprende la cassetta postale del dirigente, gli amministratori a cui è stato assegnato l'ambito non saranno in grado di gestire la cassetta postale del dirigente, a meno che non sia stato assegnato loro anche l'ambito esclusivo.

Gli ambiti di gestione vengono utilizzati con i ruoli di gestione, le assegnazioni dei ruoli di gestione e i gruppi dei ruoli di gestione per controllare chi può gestire gli oggetti e in che modo è possibile gestirli. Per ulteriori informazioni, vedere i seguenti argomenti:

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

  - [Informazioni sui ambiti esclusivi](understanding-exclusive-scopes-exchange-2013-help.md)

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

  - [Informazioni sui gruppi di ruoli di gestione](understanding-management-role-groups-exchange-2013-help.md)

  - [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md)

Per creare lo stesso modello delle autorizzazioni in Exchange 2013 utilizzando gli ambiti di gestione definiti utilizzando gli elenchi ACL personalizzati, è necessario eseguire l'inventario degli elenchi ACL personalizzati, quindi creare gli ambiti di gestione corrispondenti. È possibile utilizzare le proprietà filtrabili disponibili per gli oggetti destinatario, server e database per creare gli ambiti di gestione che comprendono gli oggetti per i quali controllare l'accesso tramite l'ambito di gestione. Per ulteriori informazioni sulle proprietà utilizzabili con i filtri dell'ambito di gestione, vedere [Informazioni sui filtri di ambito di gestione dei ruoli](understanding-management-role-scope-filters-exchange-2013-help.md).

Per ulteriori informazioni sulla creazione degli ambiti di gestione, vedere [Creare un ambito normale o esclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).


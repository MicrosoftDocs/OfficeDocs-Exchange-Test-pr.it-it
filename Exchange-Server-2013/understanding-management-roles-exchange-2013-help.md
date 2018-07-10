---
title: 'Informazioni sui ruoli di gestione: Exchange 2013 Help'
TOCTitle: Informazioni sui ruoli di gestione
ms:assetid: 887b0a64-84b1-4b8c-9547-e456ea6f5dbd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298116(v=EXCHG.150)
ms:contentKeyID: 50481128
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Informazioni sui ruoli di gestione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

I ruoli di gestione fanno parte del modello di autorizzazioni relativo al controllo dell'accesso basato sui ruoli (RBAC) utilizzato in Microsoft Exchange Server 2013. I ruoli funzionano come un raggruppamento logico di cmdlet, combinati per consentire l'accesso alla configurazione dei componenti di Exchange 2013, quali cassette postali, regole di trasporto e destinatari, per la visualizzazione o la modifica. I ruoli di gestione possono essere ulteriormente combinati in grandi raggruppamenti chiamati gruppi di ruoli di gestione e criteri di assegnazione dei ruoli di gestione, che permettono la gestione delle aree di funzionalità e della configurazione dei destinatari. I gruppi di ruoli e i criteri di assegnazione dei ruoli assegnano le autorizzazioni, rispettivamente, agli amministratori e agli utenti finali. Per ulteriori informazioni sulla gestione dei gruppi di ruoli e dei criteri di assegnazione dei ruoli, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).


> [!NOTE]
> Questo argomento è incentrato sulla funzionalità RBAC avanzata. Se si desidera gestire le autorizzazioni di base di Exchange 2013, quale l'utilizzo dell'interfaccia di amministrazione di Exchange (EAC) per aggiungere membri ai gruppi di ruoli oppure per rimuoverli da tali gruppi, per creare e modificare gruppi di ruoli oppure per creare e modificare i criteri di assegnazione dei ruoli, vedere <A href="permissions-exchange-2013-help.md">Autorizzazioni</A>.



**Sommario**

Built-in management roles

Unscoped top-level management roles

Custom management roles

Management role hierarchy

Management role entries

Unscoped top-level role entries

Management role types

For more information

Gli ambiti del ruolo di gestione e le assegnazioni dei ruoli di gestione sono componenti importanti per il funzionamento dei ruoli di gestione. Per ulteriori informazioni su tali componenti, vedere i seguenti argomenti:

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

  - [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md)

Per informazioni sulle attività di gestione relative ai ruoli di gestione, vedere [Autorizzazioni](permissions-exchange-2013-help.md).

## Ruoli di gestione predefiniti

Exchange 2013 fornisce molti ruoli di gestione incorporati che possono essere utilizzati per amministrare l'organizzazione. Ciascun ruolo include i cmdlet e i parametri necessari agli utenti per la gestione di determinati componenti di Exchange. Di seguito, sono riportati alcuni esempi di alcuni ruoli di gestione incorporati:

  - **Destinatari di posta**   Consente agli amministratori di gestire le cassette postali, i contatti e gli utenti di posta.

  - **Regole di trasporto**   Consente agli amministratori o a utenti esperti assegnati al ruolo di gestire la funzionalità relativa alle regole di trasporto.

  - **Gruppi di distribuzione**   Consente agli amministratori o a utenti esperti assegnati al ruolo di gestire i gruppi di distribuzione e i relativi membri.

  - **MyPersonalInformation**   Consente agli utenti finali di modificare il loro numero telefonico di casa e l'indirizzo del sito Web.

Per un elenco completo dei ruoli di gestione inclusi con Exchange 2013, vedere [Ruoli di gestione predefiniti](built-in-management-roles-exchange-2013-help.md).

È possibile prendere i ruoli incorporati forniti con Exchange 2013 e combinarli in qualsiasi modo per creare un modello di autorizzazioni valido per la propria azienda. Ad esempio, se si desidera che i membri di un gruppo di ruoli gestiscano i destinatari e le cartelle pubbliche, assegnare al gruppo entrambi i ruoli Destinatari di posta e Cartelle pubbliche. Spesso, vengono assegnati i ruoli ai gruppi di ruoli o ai criteri di assegnazione dei ruoli. È, inoltre, possibile assegnare ruoli di gestione direttamente agli utenti se si desidera controllare le autorizzazioni a livello capillare. Si consiglia di utilizzare gruppi di ruoli e criteri di assegnazione dei ruoli piuttosto che un'assegnazione diretta dei ruoli agli utenti per semplificare il modello delle autorizzazioni.


> [!NOTE]
> È possibile assegnare ai criteri di assegnazione dei ruoli solo ruoli di gestione degli utenti finali.



I ruoli di gestione incorporati non possono essere modificati. Tuttavia, è possibile creare ruoli di gestione basati sui ruoli di gestione incorporati e, quindi, assegnare questi nuovi ruoli ai gruppi di ruoli o ai criteri di assegnazione dei ruoli. È, quindi, possibile modificare i nuovi ruoli di gestione in base alle proprie esigenze. Si tratta di un'attività avanzata che un utente standard potrebbe anche non aver mai la necessità di svolgere.

Per ulteriori informazioni sulla creazione di ruoli basati sui ruoli di Exchange incorporati, vedere la sezione Custom Management Roles riportata più avanti in questo argomento.

Affinché diventino effettivi, i ruoli di gestione devono essere assegnati. Spesso, vengono assegnati ruoli di gestione ai gruppi di ruoli e ai criteri di assegnazione dei ruoli. In determinate circostanze, potrebbe anche essere possibile assegnare ruoli direttamente agli utenti, sebbene si tratti di un'attività avanzata che un utente standard potrebbe anche non aver mai la necessità di svolgere.

Per ulteriori informazioni sull'assegnazione dei ruoli di gestione, vedere i seguenti argomenti:

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Gestire i criteri di assegnazione dei ruoli](manage-role-assignment-policies-exchange-2013-help.md)

  - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

Per ulteriori informazioni sulle assegnazioni dei ruoli di gestione, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Inizio pagina

## Ruoli di gestione di primo livello senza ambito

I ruoli di gestione di primo livello senza ambito sono uno speciale tipo di ruolo di gestione che consente di concedere agli utenti l'accesso ai cmdlet non Exchange e agli script personalizzati tramite RBAC. I ruoli di gestione regolari consentono l'accesso solo ai cmdlet di Exchange. Qualora fosse necessario fornire l'accesso a cmdlet non di Exchange in esecuzione su un server di Exchange o pubblicare uno script che possa essere eseguito dagli utenti, è necessario aggiungerli a un ruolo senza ambito. Sono denominati ruoli di primo livello in quanto, se viene creato un ruolo senza ambito che non deriva da un ruolo padre, questo non ha un elemento padre ed è un peer dei ruoli di gestione incorporati forniti con Exchange 2013. Per indicare che si desidera creare una voce di ruolo di primo livello senza ambito, è necessario utilizzare l'opzione *UnscopedTopLevel* con il cmdlet **New-ManagementRole**.

I ruoli senza ambito vengono così denominati in quanto, a differenza dei ruoli di gestione regolari, non possono essere legati a una determinata destinazione. I ruoli senza ambito sono sempre a livello di organizzazione. Ciò significa che gli utenti a cui è assegnato a un ruolo senza ambito possono modificare qualsiasi oggetto all'interno dell'organizzazione Exchange 2013. Per questo motivo, è fondamentale accertarsi che gli script e i cmdlet resi disponibili tramite un ruolo senza ambito siano stati verificati accuratamente in modo che sia chiaro cosa andranno a modificare; è inoltre fondamentale prestare particolare attenzione all'assegnazione dei ruoli senza ambito.

I ruoli senza ambito possono essere assegnati agli assegnatari di ruoli, quali gruppi di ruoli, ruoli di gestione, utenti e gruppi di sicurezza universale. Non possono essere assegnati ai criteri di assegnazione dei ruoli di gestione.

Sebbene i cmdlet di Exchange non possano essere aggiunti come una voce di ruolo di gestione su un ruolo senza ambito, questi possono essere inclusi in script aggiunti come voci di ruolo. Ciò consente di creare script personalizzati che eseguono attività di Exchange che possono poi essere assegnate agli utenti. Uno scenario utile è quello in cui un utente deve eseguire un'attività altamente privilegiata che, normalmente, non rientra nel suo livello amministrativo e in cui la definizione di un nuovo ruolo di gestione o gruppo di ruoli potrebbe risultare problematica. È possibile creare uno script in grado di eseguire questa funzione specifica, aggiungerlo a un ruolo senza ambito e, quindi, assegnare il ruolo senza ambito all'utente. L'utente può, quindi, eseguire solo la funzione specifica fornita dallo script.

Le voci di ruolo aggiunte a un ruolo senza ambito devono anche essere designate come voci di ruolo di primo livello senza ambito. Per ulteriori informazioni sulle voci di ruolo di primo livello senza ambito, vedere Unscoped Top-Level Role Entries.

Per impostazione predefinita, il gruppo di ruoli Gestione organizzazione non dispone delle autorizzazioni per la creazione o la gestione dei gruppi di ruoli senza ambito, onde evitare che i gruppi di ruoli senza ambito vengano creati o modificati erroneamente. Il gruppo di ruoli Gestione organizzazione può delegare il ruolo di gestione Gestione ruoli senza ambito a se stesso e ad altri ruoli assegnati. Per ulteriori informazioni su come creare un ruolo di gestione di primo livello senza ambito, vedere [Creazione di un ruolo senza ambito](create-an-unscoped-role-exchange-2013-help.md).

Inizio pagina

## Ruoli di gestione personalizzati

È possibile creare ruoli di gestione personalizzati che si basano sui ruoli di Exchange incorporati quando i ruoli di gestione incorporati non soddisfano le esigenze dei propri utenti. Quando si crea un ruolo di gestione personalizzato, il nuovo ruolo figlio eredita tutte le voci di ruolo di gestione del ruolo padre. È, quindi, possibile scegliere quali voci di ruolo di gestione si desidera mantenere nel ruolo di gestione personalizzato e rimuovere tutte le voci indesiderate.

I ruoli personalizzati diventano figli del ruolo utilizzato per creare il nuovo ruolo. È possibile utilizzare nel nuovo ruolo figlio solo le voci di ruolo di gestione presenti nel ruolo padre. Per ulteriori informazioni, vedere le seguenti sezioni riportate più avanti in questo argomento:

  - Management Role Hierarchy

  - Management Role Entries

La creazione di ruoli di gestione personalizzati richiede più passi e rappresenta un'attività avanzata che un utente standard potrebbe anche non aver mai la necessità di svolgere. Prima di creare un ruolo di gestione personalizzato, accertarsi che uno dei ruoli di gestione incorporati non fornisca le autorizzazioni necessarie. Per ulteriori informazioni sui ruoli di gestione incorporati o se si desidera creare ruoli di gestione personalizzati, vedere i seguenti argomenti:

  - [Ruoli di gestione predefiniti](built-in-management-roles-exchange-2013-help.md)

  - [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md)

Per ulteriori informazioni sulla creazione di un ruolo di gestione, vedere [Creare un ruolo](create-a-role-exchange-2013-help.md).

Inizio pagina

## Gerarchia dei ruoli di gestione

I ruoli di gestione coesistono in una gerarchia padre e figlio. In cima alla gerarchia ci sono i ruoli di gestione incorporati forniti in Exchange 2013 per impostazione predefinita. Quando si crea un ruolo, in realtà si esegue una copia di un ruolo padre. Il nuovo ruolo è un elemento figlio del ruolo da cui è stato copiato. È, quindi, possibile personalizzare il nuovo ruolo per soddisfare le esigenze degli amministratori o degli utenti a cui si desidera assegnare il ruolo.

È possibile utilizzare i ruoli personalizzati per creare nuovi ruoli. Quando si crea un ruolo da un ruolo personalizzato esistente, quest'ultimo rimane un elemento figlio del relativo ruolo padre, ma diviene anche l'elemento genitore per il nuovo ruolo. Ogni volta che si copia un ruolo, il nuovo ruolo figlio può contenere solo le voci di ruolo presenti nel ruolo padre immediato.

A ciascun ruolo di gestione viene assegnato un tipo di ruolo non modificabile. Il tipo di ruolo definisce il contesto di utilizzo base per il ruolo. Il tipo di ruolo viene copiato dal ruolo padre quando viene creato il ruolo figlio.

**Gerarchia dei ruoli di gestione**

![Diagramma gerarchico dei ruoli di gestione RBAC](images/Dd298116.6851c829-ca8f-40e7-a67c-cc9e85c33953(EXCHG.150).gif "Diagramma gerarchico dei ruoli di gestione RBAC")

Nella figura precedente, viene illustrata la relazione gerarchica dei diversi ruoli di gestione. I ruoli Destinatari di posta e Assistenza tecnica sono ruoli incorporati. Tutti i ruoli figlio derivati da questi ruoli ereditano il tipo di ruolo di ciascun ruolo incorporato. Ad esempio, tutti i ruoli figlio derivati direttamente o indirettamente dal ruolo Destinatari di posta ereditano il tipo di ruolo `MailRecipients`.

Il ruolo personalizzato Amministratori destinatari Seattle è un elemento figlio del ruolo incorporato Destinatari di posta, ma anche l'elemento padre dei ruoli personalizzati Amministratori destinatari ufficio 1 Seattle e Amministratori destinatari ufficio 2 Seattle. Il ruolo personalizzato Amministratori destinatari Seattle contiene solo un sottoinsieme di cmdlet disponibili nel ruolo Destinatari di posta. I ruoli figlio del ruolo personalizzato Amministratori destinatari Seattle possono contenere solo cmdlet presenti anche in quel ruolo. Ad esempio, se un cmdlet è presente nel ruolo Destinatari di posta, ma non nel ruolo personalizzato Amministratori destinatari Seattle, non è possibile aggiungere il cmdlet al ruolo personalizzato Amministratori destinatari ufficio 1 Seattle.

Tutti i ruoli personalizzati seguono lo stesso modello dei ruoli trattati in precedenza. Per ulteriori informazioni su come viene verificato l'accesso ai cmdlet nei ruoli di gestione, vedere la sezione Management Role Entries riportata più avanti in questo argomento.

Inizio pagina

## Voci del ruolo di gestione

Ogni ruolo di gestione, sia che si tratti di un ruolo di Exchange personalizzato o di un ruolo senza ambito, deve disporre di almeno una voce di ruolo di gestione. Una voce consiste in un singolo cmdlet e nei relativi parametri, uno script o un'autorizzazione speciale che si desidera rendere disponibile. Se un cmdlet o o uno script non appare come una voce in un ruolo di gestione, non sarà possibile accedere a tale cmdlet o script tramite quel ruolo. In modo analogo, se un parametro non è presente in una voce, non sarà possibile accedere al parametro su quel cmdlet o script tramite quel ruolo.

Exchange 2013 consente di gestire le voci di ruolo basate sui ruoli di gestione di primo livello di Exchange incorporati e le voci di ruolo basate sui ruoli di gestione di primo livello senza ambito. I ruoli basati sui ruoli di primo livello di Exchange incorporati possono contenere solo le voci di ruolo corrispondenti a cmdlet di Exchange 2013. Per aggiungere script o cmdlet non Exchange personalizzati in modo che gli utenti possano utilizzarli, è necessario aggiungerli come voci di ruolo senza ambito a un ruolo di primo livello senza ambito. Per ulteriori informazioni sulle voci di ruolo senza ambito, vedere la sezione Unscoped Top-Level Role Entries riportata più avanti in questo argomento.

Tutte le voci di ruolo, indipendentemente dal fatto che la voce di ruolo sia un ruolo basato su cmdlet di Exchange o una voce di ruolo senza ambito, rispettano gli stessi principi illustrati nelle sezioni seguenti.

Per ulteriori informazioni sulle voci di ruolo di gestione, vedere [Ruoli di gestione e voci di ruolo](management-roles-and-role-entries-exchange-2013-help.md).

## Relazioni tra i ruoli di gestione padre e figlio

Come indicato in precedenza, una voce di ruolo di gestione, inclusi il cmdlet e i relativi parametri, deve essere presente nel ruolo padre immediato affinché possa essere aggiunta al ruolo figlio. Ad esempio, se il ruolo padre non dispone di una voce per **New-Mailbox**, non sarà possibile assegnare il ruolo figlio a quel cmdlet. Inoltre, se **Set-Mailbox** si trova nel ruolo padre ma il parametro *Database* è stato rimosso dalla voce, non sarò possibile aggiungere il parametro *Database* nel cmdlet **Set-Mailbox** alla voce nel ruolo figlio.

Poiché non è possibile aggiungere le voci di ruolo di gestione ai ruoli figlio se queste non appaiono nei ruoli padre e poiché il ruolo si basa su un tipo di ruolo specifico, è necessario scegliere attentamente il ruolo padre da copiare quando si desidera creare un ruolo personalizzato.

Inizio pagina

## Nomi delle voci dei ruoli di gestione

I nomi delle voci di ruolo di gestione sono una combinazione del ruolo di gestione a cui sono associate e il nome del cmdlet o dello script. Il nome del ruolo e il cmdlet o lo script sono separati da un carattere barra rovesciata (\\). Ad esempio, il nome della voce di ruolo per il cmdlet **Set-Mailbox** nel ruolo Destinatari di posta è `Mail Recipients\Set-Mailbox`. Se il nome di una voce di ruolo contiene spazi, racchiudere l'intero nome tra virgolette (").

Il carattere jolly (\*) può essere utilizzato nel nome della voce di ruolo al fine di restituire tutte le voci di ruolo corrispondenti all'input fornito. Il carattere jolly può essere utilizzato su entrambi i lati del carattere barra rovesciata. La seguente tabella contiene alcune variazioni sulle varie possibilità di utilizzo del carattere jolly in un nome della voce di ruolo.

**Nome della voce di ruolo di gestione con caratteri jolly**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Esempio</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>*\*</code></p></td>
<td><p>Restituisce un elenco di tutte le voci di ruolo per tutti i ruoli.</p></td>
</tr>
<tr class="even">
<td><p><code>*\Set-Mailbox</code></p></td>
<td><p>Restituisce un elenco di tutte le voci di ruolo contenenti il cmdlet <strong>Set-Mailbox</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipients\*</code></p></td>
<td><p>Restituisce un elenco di tutte le voci di ruolo nel ruolo Destinatari di posta.</p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients\*Mailbox</code></p></td>
<td><p>Restituisce un elenco di tutte le voci di ruolo nel ruolo Destinatari di posta che contengono cmdlet che terminano con la parola Mailbox.</p></td>
</tr>
<tr class="odd">
<td><p><code>My*\*Group*</code></p></td>
<td><p>Restituisce un elenco di tutte le voci di ruolo contenenti la stringa Group nel nome del cmdlet per tutti i ruoli che iniziano con My.</p></td>
</tr>
</tbody>
</table>


## Voci di ruolo di primo livello senza ambito

Le voci di ruolo di primo livello senza ambito vengono utilizzate con i ruoli di gestione di primo livello senza ambito per creare ruoli basati su cmdlet non Exchange o script personalizzati. Ciascuna voce di ruolo senza ambito è associata a un singolo cmdlet non di Exchange o script personalizzato. Per indicare che si desidera creare una voce di ruolo senza ambito in un ruolo senza ambito, è necessario specificare il parametro *UnscopedTopLevel* nel cmdlet **Add-ManagementRoleEntry**.

Quando si aggiunge la voce di ruolo senza ambito, è necessario specificare tutti i parametri che possono essere utilizzati con lo script o con il cmdlet non di Exchange. Exchange tenta di verificare i parametri forniti quando si aggiunge la voce di ruolo. Gli utenti assegnati al ruolo senza ambito potranno usufruire solo dei parametri aggiunti alla voce di ruolo al momento della creazione. Se si aggiungono parametri allo script o al cmdlet non di Exchange o se viene rinominato un parametro, è necessario aggiornare la voce di ruolo manualmente. Exchange non verifica se sono state apportate modifiche ai parametri esistenti in una voce di ruolo senza ambito. Se un parametro in una voce di ruolo viene modificato in uno script e si tenta di utilizzare quel parametro, il comando non verrà eseguito.

Gli script aggiunti a una voce di ruolo senza ambito devono trovarsi nella directory degli script di Exchange 2013 su ogni server a cui gli amministratori e gli utenti effettuano la connessione mediante l'uso di Exchange Management Shell. Se si tenta di aggiungere una voce di ruolo senza ambito basata su uno script non presente nella directory degli script di Exchange 2013 sul server utilizzato per aggiungere la voce di ruolo, si verificherà un errore. Il percorso predefinito di installazione della directory contenente gli script di Exchange 2013 è C:\\Program Files\\Microsoft\\Exchange Server\\V15\\RemoteScripts.

I cmdlet non di Exchange aggiunti a una voce di ruolo senza ambito devono essere installati su ciascun server di Exchange 2013 a cui gli amministratori e gli utenti effettuano la connessione mediante l'uso di Shell e su cui desiderano utilizzare i cmdlet. Se si tenta di aggiungere una voce di ruolo senza ambito basata su un cmdlet non di Exchange non installato sul server di Exchange 2013 utilizzato per aggiungere la voce di ruolo, si verificherà un errore. Quando si aggiunge un cmdlet non Exchange, è necessario specificare il nome dello snap-in di Windows PowerShell contenente il cmdlet non Exchange.

Per ulteriori informazioni su come aggiungere una voce di ruolo di gestione senza ambito, vedere [Aggiungere una voce di ruolo a un ruolo](add-a-role-entry-to-a-role-exchange-2013-help.md).

Inizio pagina

## Tipi di ruoli di gestione

I tipi di ruolo di gestione sono alla base di tutti i ruoli di gestione. I tipi stabiliscono gli ambiti impliciti definiti in tutti i ruoli di gestione di un determinato tipo di ruolo e agiscono anche come un raggruppamento logico di ruoli correlati. Tutti i ruoli di gestione derivati dal ruolo di gestione padre incorporato presentano lo stesso tipo di ruolo. Fare riferimento alla figura relativa alla gerarchia dei ruoli di gestione riportata precedentemente in questo argomento per un'illustrazione della relazione. I tipi di ruolo di gestione rappresentano il numero massimo di cmdlet e relativi parametri che è possibile aggiungere a un ruolo associato a uno specifico tipo di ruolo.

I tipi di ruolo di gestione sono suddivisi nelle seguenti categorie:

  - **Amministrativo o specialistico**   I ruoli associati a un tipo di ruolo amministrativo o specialistico hanno un ambito di impatto più vasto all'interno dell'organizzazione di Exchange. I ruoli di questo tipo di ruolo consentono attività, quali gestione del server o dei destinatari, configurazione dell'organizzazione, amministrazione della conformità, controllo e altro ancora.

  - **Orientato all'utente**   I ruoli associati a un tipo di ruolo orientato all'utente hanno un ambito di impatto strettamente legato a un singolo utente. I ruoli di questo tipo di ruolo consentono attività, quali configurazione del profilo utente e gestione personale, gestione dei gruppi di distribuzione di proprietà di un utente e altro ancora.
    
    I nomi dei ruoli associati ai tipi di ruolo orientati all'utente e i nomi dei tipi di ruolo orientati all'utente iniziano con My.

  - **Specializzato**   I ruoli associati a tipi di ruolo specializzati consentono attività che non appartengono ai tipi di ruolo amministrativi o orientati all'utente. I ruoli di questo tipo di ruolo consentono attività quali la rappresentazione delle applicazioni e l'uso di script e cmdlet non di Exchange.

Nella tabella seguente, sono riportati tutti i tipi di ruolo di gestione amministrativi in Exchange 2013 e viene indicato se la configurazione consentita dal tipo di ruolo viene applicata all'intera organizzazione di Exchange oppure solo a un singolo server. Per ulteriori informazioni su ciascuno dei ruoli di gestione associato a questi tipi di ruolo, inclusa una descrizione di ciascun ruolo, che potrebbe trarre vantaggi dall'assegnazione al ruolo e altre informazioni, vedere [Ruoli di gestione predefiniti](built-in-management-roles-exchange-2013-help.md).

**Tipi di ruolo amministrativi**


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di ruolo di gestione</th>
<th>Ruoli di gestione incorporati</th>
<th>Descrizione</th>
<th>Organizzazione o server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ActiveDirectoryPermissions</code></p></td>
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">Ruolo Active Directory le autorizzazioni</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di configurare le autorizzazioni Active Directory in un'organizzazione. Alcune funzionalità che utilizzano le autorizzazioni Active Directory o un elenco di controllo di accesso includono i connettori di invio e ricezione del trasporto e le autorizzazioni di invio per conto di altri per le cassette postali.</p>

> [!NOTE]
> Le autorizzazioni impostate direttamente su oggetti Active Directory potrebbero non essere applicate tramite RBAC.


</td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>AddressLists</code></p></td>
<td><p><a href="address-lists-role-exchange-2013-help.md">Ruolo di elenchi indirizzi</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire elenchi di indirizzi, elenchi di indirizzi globali ed elenchi di indirizzi offline in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">Ruolo ApplicationImpersonation</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono alle applicazioni di impersonare gli utenti in un'organizzazione per eseguire attività per conto di tali utenti.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><a href="archiveapplication-role-exchange-2013-help.md">Ruolo ArchiveApplication</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono alle applicazioni partner di archiviare gli elementi nelle cassette postali utente in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditLogs</code></p></td>
<td><p><a href="audit-logs-role-exchange-2013-help.md">Ruolo registri di controllo</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire la configurazione delle registrazioni di controllo in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletExtensionAgents</code></p></td>
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">Ruolo di agenti di estensione cmdlet</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire gli agenti di estensione dei cmdlet in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>DataLossPrevention</code></p></td>
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">Ruolo di prevenzione della perdita di dati</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono di creare e gestire i criteri di prevenzione della perdita di dati (DLP) e le regole al loro interno in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>DatabaseAvailabilityGroups</code></p></td>
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">Ruolo i gruppi di disponibilità del database</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire i gruppi di disponibilità del database in un'organizzazione. Gli amministratori assegnati a questo ruolo sono direttamente o indirettamente gli amministratori di livello superiore responsabili per la configurazione a elevata disponibilità in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>DatabaseCopies</code></p></td>
<td><p><a href="database-copies-role-exchange-2013-help.md">Ruolo delle copie del database</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire le copie del database sui singoli server.</p></td>
<td><p>Server</p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><a href="databases-role-exchange-2013-help.md">Ruolo del database</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di creare, gestire, montare e smontare i database delle cassette postali sui singoli server.</p></td>
<td><p>Server</p></td>
</tr>
<tr class="odd">
<td><p><code>DisasterRecovery</code></p></td>
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">Ruolo di ripristino di emergenza</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di ripristinare le cassette postali e i database delle cassette postali, creare database delle cassette postali ed eseguire il passaggio e il cambio per compatibilità dei centri dati per i gruppi di disponibilità del database in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>DistributionGroups</code></p></td>
<td><p><a href="distribution-groups-role-exchange-2013-help.md">Ruolo di gruppi di distribuzione</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di creare e gestire gruppi di distribuzione e membri dei gruppi di distribuzione in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>EdgeSubscriptions</code></p></td>
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">Ruolo di sottoscrizioni Edge</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire la configurazione di sincronizzazione e sottoscrizione edge tra i server Trasporto Edge Exchange 2010 e Exchange 2013 server cassette postali in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>EmailAddressPolicies</code></p></td>
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">Ruolo di criteri degli indirizzi di posta elettronica</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire i criteri degli indirizzi di posta elettronica in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeConnectors</code></p></td>
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">Ruolo connettori di Exchange</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di creare, modificare, visualizzare e rimuovere i connettori degli agenti di recapito.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeServerCertificates</code></p></td>
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">Ruolo dei certificati di Exchange Server</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di creare, importare, esportare e gestire i certificati del server di Exchange sui singoli server.</p></td>
<td><p>Server</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeServers</code></p></td>
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Ruolo del server di Exchange</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire la configurazione dei server di Exchange sui singoli server.</p></td>
<td><p>Server</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeVirtualDirectories</code></p></td>
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">Ruolo di directory virtuali di Exchange</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire Outlook Web App, Microsoft ActiveSync, la rubrica offline, l'individuazione automatica, Windows PowerShell e le directory virtuali di Interfaccia di amministrazione di Exchange sui singoli server.</p></td>
<td><p>Server</p></td>
</tr>
<tr class="odd">
<td><p><code>FederatedSharing</code></p></td>
<td><p><a href="federated-sharing-role-exchange-2013-help.md">Ruolo di condivisione federata</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire la condivisione tra foreste e tra organizzazioni in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>InformationRightsManagement</code></p></td>
<td><p><a href="information-rights-management-role-exchange-2013-help.md">Information Rights Management role</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire le funzionalità IRM (Information Rights Management) di Exchange in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><a href="journaling-role-exchange-2013-help.md">Ruolo dell'inserimento nel journal</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire la configurazione del journal in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>LegalHold</code></p></td>
<td><p><a href="legal-hold-role-exchange-2013-help.md">Ruolo di conservazione legale</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di specificare se i dati all'interno di una cassetta postale devono essere conservati per eventuali controversie legali in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxImportExport</code></p></td>
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">Ruolo di importazione\esportazione delle cassette postali</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di importare ed esportare il contenuto delle cassette postali e di eliminare da queste eventuali contenuti non desiderati.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearch</code></p></td>
<td><p><a href="mailbox-search-role-exchange-2013-help.md">Ruolo di ricerca di cassette postali</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di cercare il contenuto di una o più cassette postali in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">Ruolo MailboxSearchApplication</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono alle applicazioni partner di impostare e visualizzare lo stato di conservazione a fini giudiziari di una cassetta postale in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>MailEnabledPublicFolders</code></p></td>
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">Ruolo di cartelle pubbliche abilitate alla posta</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di stabilire se le singole cartelle pubbliche sono abilitate o disabilitate all'utilizzo della posta elettronica in un'organizzazione.</p>
<p>Questo tipo di ruolo consente di gestire le proprietà di posta elettronica delle sole cartelle pubbliche. Non consente di gestire le proprietà delle cartelle pubbliche che non riguardano la posta elettronica. Per gestire le proprietà delle cartelle pubbliche che non riguardano la posta elettronica, è necessario assegnare all'utente un ruolo associato al tipo di ruolo <code>PublicFolders</code>.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>MailRecipientCreation</code></p></td>
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Ruolo di creazione dei destinatari di posta</a></p>
<p></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di creare cassette postali, utenti di posta elettronica, contatti di posta, gruppi di distribuzione e gruppi di distribuzione dinamica in un'organizzazione. I ruoli associati a questo tipo di ruolo possono essere combinati con i ruoli associati al tipo di ruolo <code>MailRecipients</code> per consentire la creazione e gestione dei destinatari.</p>
<p>Questo tipo di ruolo non consente all'utente di abilitare le cartelle pubbliche alla posta. Per abilitare le cartelle pubbliche alla posta, è necessario che all'utente sia assegnato a un ruolo associato al tipo di ruolo <code>MailEnabledPublicFolders</code>.</p>
<p>Se l'organizzazione gestisce un modello di autorizzazioni diviso, in cui la creazione dei destinatari viene eseguita da un gruppo diverso rispetto a quello che esegue la gestione dei destinatari, assegnare il ruolo <code>MailRecipientCreation</code> al gruppo che esegue la creazione dei destinatari e il ruolo <code>MailRecipients</code> al gruppo che esegue la gestione dei destinatari.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>MailRecipients</code></p></td>
<td><p><a href="mail-recipients-role-exchange-2013-help.md">Ruolo destinatari di posta elettronica</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire cassette postali, utenti di posta, contatti di posta, gruppi di distribuzione e gruppi di distribuzione dinamica esistenti in un'organizzazione. I ruoli associati a questo tipo di ruolo non possono creare tali destinatari, ma possono essere combinati con i ruoli associati al tipo di ruolo <code>MailRecipientCreation</code> per consentire la creazione e gestione dei destinatari.</p>
<p>Questo tipo di ruolo non consente all'utente di gestire le cartelle pubbliche abilitate alla posta o i gruppi di distribuzione. Per gestire le cartelle pubbliche abilitate alla posta, è necessario che all'utente sia assegnato un ruolo associato al tipo di ruolo <code>MailEnabledPublicFolders</code>. Per gestire i gruppi di distribuzione, è necessario che all'utente sia assegnato un ruolo associato al tipo di ruolo <code>DistributionGroups</code>.</p>
<p>Se l'organizzazione gestisce un modello di autorizzazioni diviso, in cui la creazione dei destinatari viene eseguita da un gruppo diverso rispetto a quello che esegue la gestione dei destinatari, assegnare il ruolo <code>MailRecipientCreation</code> al gruppo che esegue la creazione dei destinatari e il ruolo <code>MailRecipients</code> al gruppo che esegue la gestione dei destinatari.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>MailTips</code></p></td>
<td><p><a href="mail-tips-role-exchange-2013-help.md">Ruolo di suggerimenti di posta</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire i suggerimenti per i messaggi in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>MessageTracking</code></p></td>
<td><p><a href="message-tracking-role-exchange-2013-help.md">Ruolo di verifica messaggi</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di tenere traccia dei messaggi in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>Migration</code></p></td>
<td><p><a href="migration-role-exchange-2013-help.md">Ruolo di migrazione</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di eseguire la migrazione delle cassette postali e del contenuto delle cassette postali da o verso un server.</p></td>
<td><p>Server</p></td>
</tr>
<tr class="even">
<td><p><code>Monitoring</code></p></td>
<td><p><a href="monitoring-role-exchange-2013-help.md">Ruolo di monitoraggio</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di monitorare i servizi di Microsoft Exchange e la disponibilità dei componenti in un'organizzazione. Oltre che con gli amministratori, è possibile utilizzare i ruoli associati a questo tipo di ruolo con l'account di servizio utilizzato dalle applicazioni di monitoraggio per raccogliere informazioni sullo stato dei server di Exchange.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>MoveMailboxes</code></p></td>
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">Spostare il ruolo cassette postali</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di spostare le cassette postali tra i server di un'organizzazione e tra i server nell'organizzazione locale e in un'altra organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">Ruolo OfficeExtensionApplication</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono alle applicazioni di estensione di Microsoft Office di accedere alle cassette postali utente in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>OrgCustomApps</code></p></td>
<td><p><a href="org-custom-apps-role-exchange-2013-help.md">Ruolo dell'organizzazione personalizzato App</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di visualizzare e modificare le app personalizzate dell'organizzazione in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>OrgMarketplaceApps</code></p></td>
<td><p><a href="org-marketplace-apps-role-exchange-2013-help.md">Ruolo App Marketplace dell'organizzazione</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di visualizzare e modificare le app Marketplace dell'organizzazione in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationClientAccess</code></p></td>
<td><p><a href="organization-client-access-role-exchange-2013-help.md">Ruolo Accesso Client dell'organizzazione</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire le impostazioni del server Accesso client in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>OrganizationConfiguration</code></p></td>
<td><p><a href="organization-configuration-role-exchange-2013-help.md">Ruolo di configurazione dell'organizzazione</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire le impostazioni a livello di organizzazione in un'organizzazione. I tipi di configurazione dell'organizzazione che possono essere controllati con questo tipo di ruolo includono quanto segue e altro ancora:</p>
<ul>
<li><p>Se i suggerimenti per i messaggi sono abilitati o disabilitati per l'organizzazione.</p></li>
<li><p>L'URL della home page della cartella gestita.</p></li>
<li><p>L'indirizzo SMTP del destinatario di Microsoft Exchange e gli indirizzi di posta elettronica alternativi.</p></li>
<li><p>La configurazione dello schema delle proprietà della cassetta postale delle risorse.</p></li>
<li><p>L'URL della Guida per Interfaccia di amministrazione di Exchange e Outlook Web App.</p></li>
</ul>
<p>Questo tipo di ruolo non comprende le autorizzazioni incluse nei tipi di ruolo <code>OrganizationClientAccess</code> o <code>OrganizationTransportSettings</code>.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationTransportSettings</code></p></td>
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">Ruolo di impostazioni di trasporto dell'organizzazione</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire le impostazioni di trasporto a livello di organizzazione, quali i messaggi di sistema, la configurazione del sito Active Directory e altre impostazioni di trasporto a livello di organizzazione in un'organizzazione.</p>
<p>Questo ruolo non consente all'utente di creare o gestire connettori di trasporto di invio o di ricezione, code, elementi Hygiene, agenti, domini accettati e remoti o regole. Per creare o gestire tutte le funzionalità di trasporto, è necessario che all'utente siano assegnati i ruoli associati ai seguenti tipi di ruolo:</p>
<ul>
<li><p><strong>Connettori di ricezione</strong>   <code>ReceiveConnectors</code></p></li>
<li><p><strong>Connettori di invio</strong>   <code>SendConnectors</code></p></li>
<li><p><strong>Code di trasporto</strong>   <code>TransportQueues</code></p></li>
<li><p><strong>Igiene di trasporto</strong>   <code>TransportHygiene</code></p></li>
<li><p><strong>Agenti di trasporto</strong>   <code>TransportAgents</code></p></li>
<li><p><strong>Domini accettati e remoti</strong>   <code>RemoteAndAcceptedDomains</code></p></li>
<li><p><strong>Regole di trasporto</strong>   <code>TransportRules</code></p></li>
</ul></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>POP3AndIMAP4Protocols</code></p></td>
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">Ruolo POP3 e IMAP4 protocolli</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire la configurazione POP3 e IMAP4, quali l'autenticazione e le impostazioni di connessione, sui singoli server.</p></td>
<td><p>Server</p></td>
</tr>
<tr class="odd">
<td><p><code>PublicFolders</code></p></td>
<td><p><a href="public-folders-role-exchange-2013-help.md">Ruolo Cartelle pubbliche</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire le cartelle pubbliche in un'organizzazione.</p>
<p>Questo tipo di ruolo non consente all'utente di gestire l'abilitazione delle cartelle pubbliche alla posta elettronica. Per abilitare o disabilitare una cartella pubblica alla posta, è necessario che all'utente sia assegnato a un ruolo associato al tipo di ruolo <code>MailEnabledPublicFolders</code>.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>ReceiveConnectors</code></p></td>
<td><p><a href="receive-connectors-role-exchange-2013-help.md">Ruolo connettori di ricezione</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire la configurazione del connettore di ricezione del trasporto, quali i limiti di dimensione su un singolo server.</p></td>
<td><p>Server</p></td>
</tr>
<tr class="odd">
<td><p><code>RecipientPolicies</code></p></td>
<td><p><a href="recipient-policies-role-exchange-2013-help.md">Ruolo criteri destinatario</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire i criteri relativi ai destinatari, quali i criteri di provisioning e dei dispositivi mobili, in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>RemoteAndAcceptedDomains</code></p></td>
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">Ruolo di domini accettati e remoti</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire i domini accettati e remoti in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>ResetPassword</code></p></td>
<td><p><a href="reset-password-role-exchange-2013-help.md">Reimpostazione della Password ruolo</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli utenti di reimpostare le proprie password e agli amministratori di reimpostare le password degli utenti in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>RetentionManagement</code></p></td>
<td><p><a href="retention-management-role-exchange-2013-help.md">Ruolo di gestione di conservazione</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire i criteri di conservazione in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>RoleManagement</code></p></td>
<td><p><a href="role-management-role-exchange-2013-help.md">Ruolo di gestione ruoli</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire i gruppi di ruoli di gestione, i criteri di assegnazione dei ruoli, i ruoli di gestione, le voci di ruolo, le assegnazioni e gli ambiti in un'organizzazione.</p>
<p>Gli utenti a cui sono stati assegnati i ruoli associati a questo tipo di ruolo possono sovrascrivere il gruppo di ruoli <strong>role group managed by</strong>, configurare qualsiasi gruppo di ruoli e aggiungere o rimuovere membri da un qualsiasi gruppo di ruoli.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>SecurityGroupCreationAndMembership</code></p></td>
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">La creazione del gruppo di sicurezza e l'appartenenza al ruolo</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di creare e gestire gruppi di protezione universale e le relative appartenenze in un'organizzazione.</p>
<p>Se l'organizzazione gestisce un modello di divisione delle autorizzazioni in cui la creazione dei gruppi di sicurezza universale viene eseguita da un gruppo diverso da quello che gestisce i server Exchange, assegnare a quel gruppo i ruoli associati a questo tipo di ruolo.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>SendConnectors</code></p></td>
<td><p><a href="send-connectors-role-exchange-2013-help.md">Ruolo connettori di invio</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire i connettori di invio del trasporto in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>SupportDiagnostics</code></p></td>
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">Ruolo Support Diagnostics</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di eseguire una diagnostica avanzata seguendo le istruzioni del Servizio Supporto Tecnico Clienti Microsoft in un'organizzazione.</p>

> [!WARNING]
> I ruoli associati a questo tipo di ruolo concedono le autorizzazioni ai cmdlet e script che dovrebbero essere utilizzati sotto la guida del Servizio Supporto Tecnico Clienti Microsoft.


</td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxes</code></p></td>
<td><p><a href="team-mailboxes-role-exchange-2013-help.md">Ruolo cassette postali di team</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di definire uno o più criteri di provisioning delle cassette postali del sito e di gestire le cassette postali del sito in un'organizzazione. Gli amministratori a cui sono assegnati ruoli associati a questo tipo di ruolo possono gestire cassette postali del sito che non sono di loro proprietà.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">Ruolo TeamMailboxLifecycleApplication</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono alle applicazioni partner di aggiornare gli stati del ciclo di vita delle cassette postali del sito in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportAgents</code></p></td>
<td><p><a href="transport-agents-role-exchange-2013-help.md">Ruolo di agenti di trasporto</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire gli agenti di trasporto in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>TransportHygiene</code></p></td>
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">Ruolo igiene di trasporto</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire le funzionalità di protezione dalla posta indesiderata e anti-malware in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportQueues</code></p></td>
<td><p><a href="transport-queues-role-exchange-2013-help.md">Ruolo delle code di trasporto</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire le code di trasporto su un singolo server.</p></td>
<td><p>Server</p></td>
</tr>
<tr class="even">
<td><p><code>TransportRules</code></p></td>
<td><p><a href="transport-rules-role-exchange-2013-help.md">Ruolo di regole di trasporto</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire le regole di trasporto in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>UMMailboxes</code></p></td>
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">Ruolo cassette postali di messaggistica unificata</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire la configurazione di messaggistica unificata delle cassette postali e altri destinatari in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>UMPrompts</code></p></td>
<td><p><a href="um-prompts-role-exchange-2013-help.md">Ruolo di richieste di messaggistica unificata</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di creare e gestire istruzioni vocali di messaggistica unificata personalizzate in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>UnifiedMessaging</code></p></td>
<td><p><a href="unified-messaging-role-exchange-2013-help.md">Ruolo Messaggistica unificata</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire i servizi di messaggistica unificata in un'organizzazione.</p>
<p>Questo ruolo non consente all'utente di gestire la configurazione della cassetta postale specifica di messaggistica unificata o i prompt di messaggistica unificata. Per gestire la configurazione della cassetta postale specifica per la messaggistica unificata, utilizzare ruoli associati al tipo di ruolo <code>UMMailboxes</code>. Per gestire le richieste di messaggistica unificata, utilizzare i ruoli associati al tipo di ruolo <code>UMPrompts</code>.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>UnScopedRoleManagement</code></p></td>
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">Ruolo senza ambito di gestione dei ruoli</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di creare e gestire ruoli di gestione di primo livello senza ambito in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>UserOptions</code></p></td>
<td><p><a href="user-options-role-exchange-2013-help.md">Ruolo di opzioni utente</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di visualizzare le opzioni di Outlook Web App di un utente in un'organizzazione. I ruoli associati a questo tipo di ruolo possono essere utilizzati per aiutare l'utente a risolvere i problemi di diagnostica riscontrati nella configurazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><a href="userapplication-role-exchange-2013-help.md">Ruolo UserApplication</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono alle applicazioni partner di agire per conto degli utenti finali in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyAuditLogs</code></p></td>
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">Ruolo registri di controllo sola visualizzazione</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di eseguire delle ricerche nel registro di controllo in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>ViewOnlyConfiguration</code></p></td>
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">Ruolo di configurazione di sola visualizzazione</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di visualizzare tutte le impostazioni di configurazione di Exchange non relative ai destinatari in un'organizzazione. Esempi di configurazioni visualizzabili sono la configurazione del server, la configurazione di trasporto, la configurazione del database e la configurazione a livello dell'organizzazione.</p>
<p>I ruoli associati a questo tipo di ruolo possono essere combinati con i ruoli associati al tipo di ruolo <code>ViewOnlyRecipients</code> per creare un ruolo in grado di visualizzare tutti gli oggetti in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyRecipients</code></p></td>
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">Ruolo destinatari di sola visualizzazione</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di visualizzare la configurazione dei destinatari, quali cassette postali, utenti di posta, contatti di posta, gruppi di distribuzione e gruppi di distribuzione dinamica.</p>
<p>I ruoli associati a questo tipo di ruolo possono essere combinati con i ruoli associati al tipo di ruolo <code>ViewOnlyConfiguration</code> per creare un ruolo in grado di visualizzare tutti gli oggetti in un'organizzazione.</p></td>
<td><p>Organizzazione</p></td>
</tr>
<tr class="even">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">Ruolo WorkloadManagement</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono agli amministratori di gestire i criteri di gestione del carico di lavoro in un'organizzazione. Gli amministratori possono configurare le definizioni di integrità delle risorse e le classificazioni dei carichi di lavoro, nonché abilitare o disabilitare la gestione dei carichi di lavoro.</p></td>
<td><p>Organizzazione</p></td>
</tr>
</tbody>
</table>


Nella tabella che segue sono elencati tutti i tipi di ruoli di gestione orientati all'utente e i corrispondenti ruoli di gestione incorporati in Exchange 2013.

**Tipi di ruolo orientati all'utente**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di ruolo di gestione</th>
<th>Ruoli orientati all'utente incorporati</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">Ruolo MyBaseOptions</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono ai singoli utenti di visualizzare e modificare la configurazione di base delle relative cassette postali e impostazioni associate.</p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><a href="myaddressinformation-role-exchange-2013-help.md">Ruolo MyAddressInformation</a></p>
<p><a href="mycontactinformation-role-exchange-2013-help.md">Ruolo MyContactInformation</a></p>
<p><a href="mymobileinformation-role-exchange-2013-help.md">Ruolo MyMobileInformation</a></p>
<p><a href="mypersonalinformation-role-exchange-2013-help.md">Ruolo MyPersonalInformation</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono ai singoli utenti di modificare le proprie informazioni di contatto. Queste informazioni includono i relativi indirizzi e numeri di telefono.</p></td>
</tr>
<tr class="odd">
<td><p>MyCustomApps</p></td>
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">Il ruolo personalizzato App</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono ai singoli utenti di visualizzare e modificare le relative app personalizzate.</p></td>
</tr>
<tr class="even">
<td><p>MyDiagnostics</p></td>
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">Ruolo MyDiagnostics</a></p></td>
<td><p>Il tipo di ruolo è associato ai ruoli che consentono ai singoli utenti di eseguire la diagnostica di base sulle cassette postali, ad esempio recuperando le informazioni di diagnostica del calendario.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">Ruolo MyDistributionGroupMembership</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono ai singoli utenti di visualizzare e modificare la propria appartenenza ai gruppi di distribuzione in un'organizzazione, purché tali gruppi di distribuzione consentano la manipolazione dell'appartenenza al gruppo.</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">Ruolo MyDistributionGroups</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono ai singoli utenti di creare, modificare e visualizzare i gruppi di distribuzione e di modificare, visualizzare, rimuovere e aggiungere membri ai gruppi di distribuzione di loro proprietà.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><a href="mydisplayname-role-exchange-2013-help.md">Ruolo MyDisplayName</a></p>
<p><a href="myname-role-exchange-2013-help.md">Ruolo MyName</a></p>
<p><a href="myprofileinformation-role-exchange-2013-help.md">Ruolo MyProfileInformation</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono ai singoli utenti di modificare il proprio nome.</p></td>
</tr>
<tr class="even">
<td><p>MyMarketplaceApps</p></td>
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">Il ruolo App Marketplace</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono ai singoli utenti di visualizzare e modificare le relative app Marketplace.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">Ruolo MyRetentionPolicies</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono ai singoli utenti di visualizzare i relativi tag di conservazione e di visualizzarne e modificarne le impostazioni e i valori predefiniti.</p></td>
</tr>
<tr class="even">
<td><p>MyTeamMailboxes</p></td>
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">Ruolo MyTeamMailboxes</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono ai singoli utenti di creare cassette postali del sito e connetterle ai siti Microsoft SharePoint.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">Ruolo MyTextMessaging</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono ai singoli utenti di creare, visualizzare e modificare le relative impostazioni per la messaggistica di testo.</p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><a href="myvoicemail-role-exchange-2013-help.md">Ruolo MyVoiceMail</a></p></td>
<td><p>Questo tipo di ruolo è associato ai ruoli che consentono ai singoli utenti di visualizzare e modificare le relative impostazioni di posta vocale.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Ulteriori informazioni

[New-ManagementRole](https://technet.microsoft.com/it-it/library/dd298073\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335173\(v=exchg.150\))

[New-ManagementScope](https://technet.microsoft.com/it-it/library/dd335137\(v=exchg.150\))

[Set-ManagementScope](https://technet.microsoft.com/it-it/library/dd297996\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335173\(v=exchg.150\))


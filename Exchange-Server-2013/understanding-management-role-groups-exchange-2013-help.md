---
title: 'Informazioni sui gruppi di ruoli di gestione: Exchange 2013 Help'
TOCTitle: Informazioni sui gruppi di ruoli di gestione
ms:assetid: 2a92e06c-523e-4fd4-a937-152562b7741d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638105(v=EXCHG.150)
ms:contentKeyID: 50480308
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Informazioni sui gruppi di ruoli di gestione

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Un *gruppo di ruoli di gestione* è un gruppo di protezione universale (USG) utilizzato nel modello di autorizzazioni per il controllo di accesso basato sui ruoli (RBAC) in Microsoft Exchange Server 2013. Il gruppo di ruoli di gestione semplifica l'assegnazione dei ruoli di gestione a un gruppo di utenti. A tutti i membri di un gruppo di ruolo viene assegnato lo stesso insieme di ruoli. Ai gruppi di ruolo vengono assegnati ruoli di amministratore ed esperto che definiscono le principali attività amministrative in Exchange 2013, come la gestione dell'organizzazione, la gestione dei destinatari e altre attività. I gruppi di ruolo consentono di assegnare più facilmente una gamma più amplia di autorizzazioni a un gruppo di amministratori o di utenti esperti.


> [!NOTE]
> Questo argomento è incentrato sulla funzionalità RBAC avanzata. Se si desidera gestire le autorizzazioni di base di Exchange 2013, quale l'utilizzo dell'interfaccia di amministrazione di Exchange (EAC) per aggiungere membri ai gruppi di ruoli oppure per rimuoverli da tali gruppi, per creare e modificare gruppi di ruoli oppure per creare e modificare i criteri di assegnazione dei ruoli, vedere <A href="permissions-exchange-2013-help.md">Autorizzazioni</A>.



**Sommario**

Role group layers

Role group management

Built-in role groups

Linked role groups

Role group delegation

Role group membership

Role group creation workflow


> [!NOTE]
> Se si desidera assegnare le autorizzazioni agli utenti per gestire la cassetta postale o i gruppi di distribuzione, vedere <A href="understanding-management-role-assignment-policies-exchange-2013-help.md">Informazioni sui criteri di assegnazione di ruolo di gestione</A>.



## Livelli dei gruppi di ruoli

Di seguito vengono riportati i livelli che costituiscono il modello dei gruppi di ruolo:

  - **Membro del gruppo di ruoli**   Un *membro del gruppo di ruoli* è una cassetta postale, un gruppo di protezione universale (USG) o un altro gruppo di ruoli che può essere aggiunto come membro di un gruppo di ruoli. Quando una cassetta postale, un gruppo di protezione universale o un altro gruppo di ruoli viene aggiunto come membro di un gruppo di ruoli, le assegnazioni stabilite tra ruoli di gestione e il gruppo di ruoli vengono applicate al nuovo membro. Al nuovo membro vengono concesse tutte le autorizzazioni fornite dai ruoli di gestione.

  - **Gruppo di ruoli di gestione**   Il *gruppo di ruoli di gestione* è uno speciale gruppo di protezione universale contenente cassette postali, gruppi di protezione universali e altri gruppi di ruoli che sono membri del gruppo di ruoli. Qui è possibile aggiungere e rimuovere membri e individuare i ruoli di gestione assegnati. La combinazione di tutti i ruoli di un gruppo consente di definire ogni elemento gestibile dai membri aggiunti a un gruppo di ruoli nell'organizzazione di Exchange.

  - **Assegnazione del ruolo di gestione**   Un'*assegnazione del ruolo di gestione* consente di collegare un ruolo di gestione a un gruppo di ruolo. L'assegnazione di un ruolo di gestione a un gruppo consente ai membri del gruppo di utilizzare i cmdlet e i parametri definiti nel ruolo di gestione. Le assegnazioni di ruolo possono utilizzare gli ambiti di gestione per controllare dove può essere utilizzata l'assegnazione. Per ulteriori informazioni, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

  - **Ambito del ruolo di gestione**   Un *ambito del ruolo di gestione* indica l'ambito di influenza o di impatto per un'assegnazione di ruolo. Quando un ruolo viene assegnato con un ambito a un gruppo, l'ambito di gestione fa preciso riferimento agli oggetti che l'assegnazione può gestire. L'assegnazione e l'ambito vengono quindi forniti ai membri del gruppo di ruolo, che limita ciò che i membri possono gestire. Un ambito può essere costituito da un elenco di server o database, unità organizzative o filtri degli oggetti server, database o destinatari. Per ulteriori informazioni, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

  - **Ruolo di gestione**   Un *ruolo di gestione* è un contenitore per un raggruppamento di voci del ruolo di gestione. I ruoli vengono utilizzati per definire le specifiche attività che possono essere eseguite dai membri di un gruppo assegnato al ruolo. Per ulteriori informazioni, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

  - **Voci del ruolo di gestione**   *Voci del ruolo di gestione* indica le singole voci di un ruolo di gestione che forniscono l'accesso a cmdlet, script e altre autorizzazioni speciali che consentono l'accesso a eseguire una specifica attività. Nella maggior parte dei casi, le voci di ruolo sono costituite da un unico cmdlet o script, dai parametri a cui è possibile accedere dal ruolo di gestione e dal gruppo a cui è stato assegnato il ruolo.

Nella seguente figura vengono illustrati tutti i livelli dei gruppi di ruolo dell'elenco precedente e come ogni livello si riferisca agli altri.

**Livelli dei gruppi del ruolo di gestione**

![Layer del gruppo di ruoli gestione](images/Dd638105.a98c237c-7bdb-434b-8c98-22509e46cccf(EXCHG.150).gif "Layer del gruppo di ruoli gestione")

Per ulteriori informazioni su RBAC, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

Inizio pagina

## Gestione dei gruppi di ruoli

Quando si crea un gruppo di ruolo, viene creato il gruppo di protezione universale contenente i membri del gruppo e vengono create le assegnazioni tra il gruppo e i ruoli di gestione specificati. Eventualmente, è possibile specificare anche l'ambito di gestione da applicare alle assegnazioni di ruolo e aggiungere le cassette postali che si desidera far diventare membri del nuovo gruppo.

Dopo aver creato un gruppo di ruolo, ogni livello diventa un oggetto indipendente. Il gruppo di ruolo continua a essere il punto centrale in cui tutti i livelli sono uniti tra loro. Tuttavia, ogni livello viene gestito individualmente. Ad esempio, per modificare l'ambito di gestione applicato al gruppo di ruolo durante la creazione, è necessario modificare l'ambito di ogni singola assegnazione dopo aver creato il gruppo. La gestione del modello dei gruppi di ruolo viene eseguita utilizzando i cmdlet che gestiscono i singoli livelli del modello.

Nella seguente tabella vengono elencati il livello dei gruppi di ruolo e gli argomenti relativi alle procedure utilizzabili per la gestione di ogni livello.

### Argomenti relativi alla gestione dei gruppi di ruolo

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Livello del modello dei gruppi di ruolo</th>
<th>Argomento relativo alla gestione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Membro del gruppo di ruoli</p></td>
<td><p><a href="manage-role-group-members-exchange-2013-help.md">Gestire i membri del gruppo di ruolo</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Gruppo di ruolo</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">Gestire gruppi di ruoli</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Ruoli di gestione e assegnazioni</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">Gestire gruppi di ruoli</a></p></td>
</tr>
<tr class="even">
<td><p>Voci del ruolo di gestione</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">Aggiungere una voce di ruolo a un ruolo</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">Modificare una voce di ruolo</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">Rimuovere una voce di ruolo da un ruolo</a></p>

> [!NOTE]
> La modifica delle voci del ruolo di gestione in ruoli di gestione di un gruppo di ruolo è un'attività avanzata e in genere non è necessaria. È possibile, invece, utilizzare un ruolo di gestione preesistente che si adatta alle esigenze. Per ulteriori informazioni, vedere <A href="built-in-role-groups-exchange-2013-help.md">Gruppi di ruoli incorporati</A>.


</td>
</tr>
</tbody>
</table>


Inizio pagina

## Gruppi di ruoli incorporati

I gruppi di ruolo incorporati sono ruoli forniti con Exchange 2013. Forniscono un insieme di gruppi di ruolo utilizzabili per fornire vari livelli di autorizzazioni amministrative ai gruppi di utenti. È possibile aggiungere o rimuovere utenti da tutti i gruppi di ruolo incorporati. È possibile aggiungere o rimuovere anche assegnazioni di ruolo dalla maggior parte dei gruppi di ruolo. Di seguito vengono riportate le uniche eccezioni:

  - Non è possibile rimuovere alcuna assegnazione del ruolo di delega dal gruppo di ruolo Gestione organizzazione.

  - Non è possibile rimuovere il ruolo Gestione dei ruoli dal gruppo di ruolo Gestione organizzazione.

Nella seguente tabella vengono elencati tutti i gruppi di ruolo incorporati inclusi con Exchange 2013. Per ulteriori informazioni sui gruppi di ruolo incorporati, vedere [Gruppi di ruoli incorporati](built-in-role-groups-exchange-2013-help.md).

### Gruppi di ruoli incorporati

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Gruppo di ruoli</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
<td><p>Gli amministratori membri del gruppo di ruoli Gestione organizzazione dispongono dell'accesso amministrativo all'intera organizzazione di Exchange 2013 e possono eseguire quasi tutte le attività su qualsiasi oggetto di Exchange 2013, con alcune eccezioni. Per impostazione predefinita, i membri di questo gruppo di ruoli non possono eseguire ricerche di cassette postali e la gestione dei ruoli di gestione di primo livello senza ambito.</p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
<td><p>Gli amministratori membri del gruppo di ruolo Gestione organizzazione in sola visualizzazione possono visualizzare le proprietà di tutti gli oggetti nell'organizzazione di Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
<td><p>Gli amministratori membri del gruppo di ruolo Gestione destinatari dispongono dell'accesso amministrativo per creare o modificare i destinatari di Exchange 2013 all'interno dell'organizzazione di Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="um-management-exchange-2013-help.md">Gestione messaggistica unificata</a></p></td>
<td><p>Gli amministratori membri del gruppo di ruolo Gestione messaggistica unificata possono gestire le funzionalità nell'organizzazione di Exchange, ad esempio la configurazione del servizio Messaggistica unificata, le proprietà di messaggistica unificata sulle cassette postali, i prompt di messaggistica unificata e la configurazione dell'operatore automatico di messaggistica unificata.</p></td>
</tr>
<tr class="odd">
<td><p><a href="discovery-management-exchange-2013-help.md">Gestione individuazione</a></p></td>
<td><p>Gli amministratori o gli utenti membri del gruppo di ruolo Gestione individuazione possono effettuare la ricerca dei dati rispondenti a determinati criteri nelle cassette postali dell'organizzazione di Exchange e anche configurare le conservazioni per controversie legali nelle cassette postali.</p></td>
</tr>
<tr class="even">
<td><p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
<td><p>Gli utenti membri del gruppo di ruolo Gestione record possono configurare le funzionalità di conformità, come le tag dei criteri di conservazione, le classificazioni dei messaggi, le regole di trasporto e altro ancora.</p></td>
</tr>
<tr class="odd">
<td><p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
<td><p>Gli amministratori membri di questo gruppo di ruoli possono eseguire la configurazione specifica del server delle funzionalità relative al trasporto, all'accesso client e alla cassetta postale come, ad esempio, copie del database, certificati, code di trasporto, connettori di invio, directory virtuali e protocolli per l'accesso client.</p></td>
</tr>
<tr class="even">
<td><p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
<td><p>Gli utenti membri del gruppo di ruolo Assistenza possono eseguire una gestione limitata dei destinatari di Exchange 2013.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p></td>
<td><p>Gli amministratori che appartengono al gruppo di ruolo per la gestione della sicurezza possono configurare le funzionalità filtro posta indesiderata e antimalware di Exchange 2013. È possibile aggiungere account di servizio a questo gruppo per consentire ai programmi di terzi integrabili con Exchange 2013 di accedere ai cmdlet necessari per recuperare e impostare la configurazione di Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">Gestione della conformità</a></p></td>
<td><p>Gli utenti membri del gruppo di ruoli Gestione della conformità possono effettuare e gestire la configurazione della conformità di Exchange in base ai propri criteri.</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">Gestione cartelle pubbliche</a></p></td>
<td><p>Gli amministratori membri del gruppo di ruolo Gestione di cartelle pubbliche possono gestire le cartelle pubbliche sui server con Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="delegated-setup-exchange-2013-help.md">Installazione delegata</a></p></td>
<td><p>Gli amministratori membri del gruppo di ruolo Configurazione delegata possono distribuire i server Exchange 2013 precedentemente sottoposti a provisioning da un membro del gruppo di ruolo Gestione organizzazione.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Gruppi di ruoli collegati

I gruppi di ruolo collegati vengono utilizzati nelle organizzazioni che installano Exchange 2013 in una specifica foresta delle risorse e collocano gli utenti in altre foreste esterne attendibili. I gruppi di ruolo collegati, come suggerisce il nome, creano un collegamento tra un gruppo della foresta di Exchange e un gruppo di protezione universale di una foresta esterna. Risulta utile quando gli account utente dei Servizi di dominio Active Directory degli amministratori desiderati per amministrare Exchange non si trovano nella stessa foresta delle risorse di Exchange. I gruppi di ruolo collegati possono essere associati solo a un unico gruppo di protezione universale esterno. Inoltre, non è necessario creare un trust bidirezionale tra la foresta di Exchange e la foresta esterna. La foresta di Exchange deve rendere attendibile la foresta esterna, ma quest'ultima non deve rendere attendibile la foresta di Exchange.

Per ulteriori informazioni sulle autorizzazioni in topologie a più foreste, vedere [Informazioni sulle autorizzazioni di più foreste](understanding-multiple-forest-permissions-exchange-2013-help.md).

Un gruppo di ruolo collegato è costituito da due parti:

  - **Gruppo di ruolo collegato**   Il gruppo di ruolo collegato indica un oggetto contenitore che associa il gruppo di protezione universale esterno alle assegnazioni del ruolo di gestione associate al gruppo.

  - **Gruppo di protezione universale esterno**   Il gruppo di protezione universale esterno contiene i membri a cui vengono concesse le autorizzazioni fornite dal gruppo di ruolo collegato.

Quando si crea un gruppo di ruolo collegato, viene fornito un controller di dominio nella foresta esterna contenente gli utenti desiderati per gestire la foresta di Exchange e il gruppo di protezione universale contenente tali utenti come membri, il nome del gruppo di protezione universale esterno e le credenziali necessarie per accedere alla foresta esterna. Exchange consente di aggiungere l'ID di sicurezza (SID) del gruppo di protezione universale esterno al gruppo di ruolo collegato. Siccome il SID del gruppo di protezione universale costituisce l'unica identificazione del gruppo di protezione universale esterno, se si dispone di più foreste esterne, si consiglia vivamente di specificare la foresta esterna nel nome del gruppo di ruolo.

Un gruppo di ruolo collegato non contiene alcun membro. Tutti i membri di tale gruppo vengono gestiti utilizzando il gruppo di protezione universale esterno. In altri termini, non è possibile utilizzare i cmdlet **Update-RoleGroupMember**, **Add-RoleGroupMember** o **Remove-RoleGroupMember** per aggiungere o rimuovere i membri del gruppo di ruolo. Quando si aggiungono membri al gruppo di protezione universale esterno, vengono concesse loro le autorizzazioni fornite dal gruppo di ruolo collegato.

Non è possibile modificare un gruppo di ruolo standard, contenente i propri membri, in un gruppo di ruolo collegato e viceversa. Se si desidera modificare un gruppo di ruolo standard in un gruppo di ruolo collegato, è necessario creare un nuovo gruppo di ruolo collegato e replicare le assegnazioni del ruolo di gestione presenti sul gruppo standard nel gruppo di ruolo collegato. Questo è il caso anche dei gruppi di ruolo incorporati, in quanto gruppi di ruolo standard. Se si desidera eseguire tutta la gestione della foresta di Exchange da una foresta esterna, è necessario creare nuovi gruppi di ruoli collegati e aggiungere i ruoli di gestione esistenti nei gruppi di ruoli incorporati ai nuovi gruppi di ruoli collegati. Per ulteriori informazioni su tale operazione, vedere [Creare gruppi di ruoli collegato il mirroring di gruppi di ruoli incorporati](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md).

Inizio pagina

## Delega dei gruppi di ruoli

Per impostazione predefinita, i membri del gruppo di ruolo Gestione organizzazione possono aggiungere e rimuovere membri dai gruppi. Tuttavia, è possibile abilitare gli utenti non membri del gruppo di ruolo Gestione organizzazione ad aggiungere e rimuovere i membri del gruppo. In tal caso, è possibile utilizzare la delega dei gruppi di ruolo.

La delega dei gruppi di ruolo viene controllata dalla proprietà **ManagedBy** di ogni gruppo. La proprietà **ManagedBy** contiene un elenco di utenti che possono aggiungere e rimuovere membri da tale gruppo di ruolo o modificarne la configurazione. Agli utenti non viene assegnata alcuna autorizzazione fornita dal gruppo di ruolo, a meno che non siano anche membri del gruppo.

Se la proprietà **ManagedBy** è impostata su un gruppo di ruolo, solo gli utenti elencati come gestore dei gruppi di ruolo su tale proprietà possono modificare un gruppo o l'appartenenza di un gruppo per impostazione predefinita. Tuttavia, un parametro facoltativo sui cmdlet, che modificano i gruppi di ruolo o l'appartenenza al gruppo, può ignorare tale restrizione. L'opzione *BypassSecurityGroupManagerCheck* può essere utilizzata dagli utenti membri del ruolo Gestione organizzazione o a cui è assegnato, direttamente o indirettamente, il ruolo Gestione ruoli. Quando questa opzione viene utilizzata, la proprietà **ManagedBy** viene ignorata e l'utente può modificare il gruppo di ruolo o l'appartenenza al gruppo.

Se la proprietà **ManagedBy** non è impostata su un gruppo di ruolo, solo gli utenti membri del ruolo Gestione organizzazione o a cui viene assegnato, direttamente o indirettamente, il ruolo Gestione ruoli possono modificare un gruppo o l'appartenenza al gruppo.


> [!NOTE]
> I ruoli associati a un gruppo potrebbero essere assegnati utilizzando le assegnazioni del ruolo di delega. Con le assegnazioni del ruolo di delega, i membri di un gruppo di ruolo, a cui viene assegnato un ruolo delegato, possono assegnare tale ruolo a un altro gruppo, criterio di assegnazione, utente o gruppo di protezione universale. I membri del gruppo di ruolo possono assegnare solo tale ruolo e non possono delegare il gruppo, a meno che non vengano aggiunti anche alla proprietà <STRONG>ManagedBy</STRONG>. Per ulteriori informazioni sulle assegnazioni del ruolo di delega, vedere <A href="understanding-management-role-assignments-exchange-2013-help.md">Informazioni sulle assegnazioni dei ruoli di gestione</A>.



Per ulteriori informazioni su come gestire la delega dei gruppi di ruolo, vedere [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

Inizio pagina

## Appartenenza ai gruppi di ruolo

Quando un utente diventa membro di un gruppo di ruolo, i ruoli di gestione assegnati al gruppo vengono associati all'utente. Se un utente è membro di più gruppi di ruolo, i ruoli di gestione di ogni gruppo vengono aggregati e assegnati all'utente. Gli utenti, i gruppi di protezione universale e altri gruppi possono essere membri di gruppi di ruolo.

Solo gli utenti membri dei gruppi di ruolo Gestione organizzazione o Gestione ruoli, e gli utenti delegati ad aggiungere e rimuovere utenti dai gruppi, possono gestire l'appartenenza ai gruppi.

Per ulteriori informazioni su come gestire l'appartenenza ai gruppi di ruoli, vedere [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).

## Flusso di lavoro Creazione gruppi di ruoli

Come accennato in precedenza, un gruppo di ruolo è costituito da numerosi livelli. Per comprendere cosa succede quando un gruppo di ruolo viene creato, vedere il seguente esempio, in cui viene creato un nuovo gruppo.

    New-RoleGroup -Name "Seattle Recipient Management" -Roles "Mail Recipients", "Distribution Groups", "Move Mailboxes", "UM Mailboxes" -CustomRecipientWriteScope "Seattle Users", -ManagedBy "Brian", "David", "Katie" -Members "Ray", "Jenn", "Maria", "Chris", "Maija", "Carter", "Jenny", "Sam", "Lukas", "Isabel", "Katie"

Quando viene eseguito il precedente comando, si verifica quanto segue:

1.  Viene creato il nuovo oggetto gruppo di ruolo, che indica uno speciale gruppo di protezione universale, denominato Seattle Recipient Management.

2.  Le cassette postali di Ray, Jens, Maria, Chris, Maija, Carter, Jenny, Sam, Lukas, Isabel e Katie vengono aggiunte come membri del gruppo di ruoli. Tali utenti ricevono le autorizzazioni fornite da questo gruppo di ruolo.

3.  Gli utenti Brian e David vengono aggiunti alla proprietà **ManagedBy** del gruppo di ruolo. Questi utenti possono aggiungere e rimuovere membri dal gruppo di ruolo, ma non verrà concessa loro alcuna autorizzazione fornita dal gruppo, in quanto non membri. Inoltre, Katie viene aggiunta alla proprietà **ManagedBy** del gruppo di ruolo. Siccome è stata aggiunta alla proprietà **ManagedBy** ed è un membro del gruppo di ruolo, può aggiungere o rimuovere membri dal gruppo e le sono concesse le autorizzazioni fornite dal gruppo.

4.  Vengono create le seguenti assegnazioni del ruolo di gestione. Le assegnazioni di ruolo consentono di associare al gruppo di ruolo ogni ruolo di gestione specificato nel comando. L'ambito di gestione Seattle Users viene aggiunto a ogni assegnazione di ruolo. Il nome di ogni assegnazione di ruolo indica una combinazione del ruolo di gestione assegnato e del nome del gruppo.
    
      - `Mail Recipients_Seattle Recipient Management`
    
      - `Distribution Groups_Seattle Recipient Management`
    
      - `Move Mailboxes_Seattle Recipient Management`
    
      - `UM Mailboxes_Seattle Recipient Management`

Se si confrontano i risultati di questo comando con la figura dei livelli del gruppo di ruolo Gestione di questo argomento, è possibile visualizzare dove ogni passo è correlato ai livelli del gruppo. Per gestire ogni livello del gruppo di ruoli, è possibile quindi fare riferimento agli argomenti relativi alla gestione dei gruppi di ruoli Gestione mostrati in "Gestione dei gruppi di ruoli" di questo argomento.

Inizio pagina


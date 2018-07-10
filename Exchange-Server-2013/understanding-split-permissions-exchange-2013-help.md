---
title: 'Informazioni sulle autorizzazioni diviso: Exchange 2013 Help'
TOCTitle: Informazioni sulle autorizzazioni diviso
ms:assetid: 2b709e15-63a2-4841-94bc-b289b71166d0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638106(v=EXCHG.150)
ms:contentKeyID: 50480238
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Informazioni sulle autorizzazioni diviso

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Le organizzazioni che separano la gestione di Microsoft Exchange Server 2013 oggetti e gli oggetti Active Directory utilizzano cosa ha chiamato un modello di *divisione delle autorizzazioni* . Le autorizzazioni diviso consentono alle organizzazioni di assegnare le autorizzazioni necessarie e attività correlate a gruppi specifici all'interno dell'organizzazione. Questa separazione del lavoro consente di mantenere standard e i flussi di lavoro e vengono fornite informazioni utili per controllare la modifica dell'organizzazione.

Il livello massimo di divisione delle autorizzazioni è la separazione della gestione Exchange e Active Directory. Molte organizzazioni hanno due gruppi: amministratori che gestiscono l'infrastruttura dell'organizzazione Exchange, inclusi i server e destinatari e gli amministratori che gestiscono l'infrastruttura Active Directory. In questo modo una separazione importante per molte organizzazioni l'infrastruttura Active Directory spesso include molti percorsi, i domini, servizi, applicazioni e anche gli insiemi di strutture Active Directory. gli amministratori Active Directory devono garantire che le modifiche apportate a Active Directory non influire negativamente sulle altri servizi. Di conseguenza, in genere un piccolo gruppo di amministratori può gestire tale infrastruttura.

Contemporaneamente, l'infrastruttura di Exchange, inclusi i server e destinatari può anche essere complessa e richiede competenze specifiche. Inoltre, Exchange archivia informazioni molto riservate nell'azienda dell'organizzazione. gli amministratori Exchange potrebbe accedere a queste informazioni. Limitando il numero di amministratori Exchange, i limiti dell'organizzazione che possono apportare modifiche alla configurazione Exchange e chi può accedere alle informazioni riservate.

Autorizzazioni diviso in genere esegue distinzione tra la creazione di entità di sicurezza in Active Directory, ad esempio gli utenti e gruppi di sicurezza e la configurazione successiva di tali oggetti. Ciò consente di ridurre le possibilità di accesso non autorizzato alla rete tramite il controllo che consente di creare oggetti di concedono l'accesso a esso. La maggior parte degli amministratori Active Directory spesso l'unico è possibile creare le entità di sicurezza mentre altri amministratori, ad esempio gli amministratori Exchange, possono gestire gli attributi specifici per gli oggetti Active Directory esistente.

Per supportare le diverse esigenze per separare la gestione di Exchange e Active Directory, Exchange 2013 consente di scegliere se si desidera che un modello di autorizzazioni condivise o un modello di autorizzazioni suddivise. Exchange 2013 offre due tipi di modelli di autorizzazioni di divisione: RBAC e Active Directory. Exchange 2013 il valore predefinito è un modello di autorizzazioni condivise.

**Sommario**

Spiegazione dei ruoli basati su Active Directory e il controllo di accesso

Autorizzazioni condivise

Divisione delle autorizzazioni

RBAC divisione delle autorizzazioni

Autorizzazioni suddivise di Active Directory

## Spiegazione dei ruoli basati su Active Directory e il controllo di accesso


Per comprendere le autorizzazioni di divisione, è necessario comprendere il funzionamento del modello di autorizzazioni ruolo basato su accesso controllo (RBAC) Exchange 2013 con Active Directory. È possibile eseguire i controlli del modello di RBAC che è possono eseguire le operazioni, in cui gli oggetti e le azioni. Per ulteriori informazioni sui diversi componenti RBAC illustrate in questo argomento, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

In Exchange 2013, tutte le attività che vengono eseguite per gli oggetti Exchange devono essere eseguite tramite l'interfaccia di amministrazione centrale (EAC) Exchange o Exchange Management Shell. Utilizzano entrambi questi strumenti di gestione RBAC per autorizzare tutte le attività eseguite.

RBAC è un componente esistente in ogni server che esegue Exchange 2013. RBAC controlla se l'utente che esegue un'azione è autorizzato a tale scopo:

  - Se l'utente non è autorizzato a eseguire l'azione, RBAC non è consentita l'azione continuare.

  - Se l'utente è autorizzato a eseguire l'azione, RBAC controlla se l'utente è autorizzato a eseguire l'azione in base all'oggetto specifico richiesto:
    
      - Se l'utente è autorizzato, RBAC consente l'azione continuare.
    
      - Se l'utente non è autorizzato, RBAC non consente l'azione continuare.

Se RBAC consente un'azione continuare, l'azione viene eseguita nel contesto di Exchange sottosistema Trusted e non il contesto dell'utente. Exchange Trusted Subsystem è un gruppo con privilegi elevati di protezione universale (USG) che dispone dell'accesso in lettura/scrittura per ogni Exchange-oggetto correlato all'interno dell'organizzazione Exchange. È anche membro del gruppo di sicurezza locale Administrators e Exchange USG le autorizzazioni di Windows, che consente a Exchange creare e gestire oggetti Active Directory.


> [!WARNING]
> Non si apportano modifiche manuali per l'appartenenza del gruppo di sicurezza Trusted Subsystem Exchange. Inoltre, non viene aggiunta a o rimuoverlo da elenchi di controllo di oggetti accesso (ACL). Se si apportano modifiche a Exchange Trusted Subsystem USG familiarità, si possono causare luogo a danni irreparabile all'organizzazione Exchange.



È importante tenere presente che non ha alcuna importanza autorizzazioni Active Directory dispone di un utente quando si utilizzano gli strumenti di gestione Exchange. Se l'utente è autorizzato tramite RBAC, per eseguire un'azione negli strumenti di gestione Exchange, l'utente può eseguire l'azione indipendentemente dalle autorizzazioni Active Directory il proprio. Al contrario, se un utente è un amministratore dell'organizzazione in Active Directory ma non è autorizzato a eseguire un'azione, ad esempio la creazione di una cassetta postale, in Exchange strumenti di gestione, l'azione non riuscita perché l'utente non dispone delle autorizzazioni necessarie in base alle RBAC.


> [!IMPORTANT]
> Anche se il modello di autorizzazioni RBAC non si applica alle Active Directory gli utenti e dello strumento di Gestione computer, Active Directory utenti e computer non può gestire la configurazione Exchange. Pertanto anche se un utente può avere accesso a modificare alcuni attributi negli oggetti Active Directory, ad esempio il nome visualizzato dell'utente, l'utente deve utilizzare gli strumenti di gestione Exchange e pertanto deve essere autorizzato da RBAC, per gestire gli attributi Exchange.



Inizio pagina

## Autorizzazioni condivise

Il modello di autorizzazioni condivise è il modello predefinito per Exchange 2013. Non è necessario apportare modifiche se si tratta del modello di autorizzazioni che si desidera utilizzare. In questo modello non separare la gestione di oggetti Exchange e Active Directory dall'interno gli strumenti di gestione Exchange. Consente agli amministratori utilizzando gli strumenti di gestione Exchange per creare le entità di sicurezza in Active Directory.

Nella tabella seguente vengono illustrati i ruoli che consentono la creazione di entità di sicurezza in Exchange e i gruppi di ruoli di gestione che sono stati assegnati per impostazione predefinita.

### Ruoli di gestione di entità di sicurezza

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruoli di gestione</th>
<th>Gruppo di ruoli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Ruolo di creazione dei destinatari di posta</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">La creazione del gruppo di sicurezza e l'appartenenza al ruolo</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
</tbody>
</table>


Solo i gruppi di ruoli, utenti o gruppi di protezione universale assegnati al ruolo della creazione dei destinatari possono creare le entità di sicurezza, ad esempio gli utenti Active Directory. Per impostazione predefinita, i gruppi di ruoli Gestione organizzazione e Gestione destinatari sono assegnati al ruolo. Pertanto i membri di questi gruppi di ruolo possono creare le entità di sicurezza.

Solo i gruppi di ruoli, utenti o gruppi di protezione universale assegnati al ruolo la creazione del gruppo di sicurezza e l'appartenenza può creare gruppi di sicurezza o gestire le relative appartenenze. Per impostazione predefinita, solo il gruppo di ruoli Gestione organizzazione viene assegnato al ruolo. Di conseguenza solo i membri del gruppo di ruoli Gestione organizzazione possono creare o gestire l'appartenenza ai gruppi di protezione.

Se si desidera che gli altri utenti di creare le entità di sicurezza, è possibile assegnare il ruolo della creazione dei destinatari e la creazione del gruppo di sicurezza e l'appartenenza al ruolo ad altri gruppi di ruoli, utenti o gruppi di protezione universale.

Per abilitare la gestione delle identità di protezione esistente in Exchange 2013, viene assegnato il ruolo destinatari di posta elettronica per i gruppi di ruoli Gestione organizzazione e Gestione destinatari per impostazione predefinita. Solo i gruppi di ruoli, utenti o gruppi di protezione universale assegnati al ruolo destinatari di posta elettronica possono gestire le entità di sicurezza esistente. Se si desidera che gli altri gruppi di ruoli, utenti o gruppi di protezione universale siano in grado di gestire le entità di sicurezza esistente, è necessario assegnare il ruolo destinatari di posta elettronica a loro.

Per ulteriori informazioni su come aggiungere ruoli a gruppi di ruoli, utenti o gruppi di protezione universali, vedere gli argomenti seguenti:

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

Se è impostato un modello di autorizzazioni suddivise e si desidera modificare un modello di autorizzazioni condivise, vedere [Configurare Exchange 2013 per autorizzazioni condivise](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md).

Inizio pagina

## Divisione delle autorizzazioni

Se l'organizzazione separa Exchange gestione e la gestione Active Directory, è necessario configurare Exchange per supportare il modello di autorizzazioni suddivise. Quando è configurato correttamente, solo gli amministratori che si desidera creare le entità di sicurezza, ad esempio gli amministratori Active Directory, saranno in grado di farlo e solo gli amministratori Exchange saranno in grado di modificare gli attributi Exchange sulle identità di protezione esistente. La divisione di autorizzazioni anche l'opportunità di circa lungo le righe delle partizioni di dominio e la configurazione in Active Directory. Partizioni denominate anche contesti dei nomi. Partizione del dominio vengono archiviati gli utenti, gruppi e gli altri oggetti per un dominio specifico. Partizione di configurazione sono archiviate le informazioni di configurazione a livello di foresta per i servizi utilizzati Active Directory, ad esempio Exchange. I dati memorizzati nella partizione del dominio in genere viene gestiti dagli amministratori Active Directory, anche se gli oggetti possono contenere Exchange-attributi specifici che possono essere gestiti dagli amministratori Exchange. I dati memorizzati nella partizione di configurazione viene gestiti dagli amministratori per ogni servizio rispettivo che archivia i dati nella partizione. Per Exchange, si tratta in genere amministratori Exchange.

Exchange 2013 supporta due tipi seguenti di divisione autorizzazioni:

  - **RBAC divisione delle autorizzazioni**   Autorizzazioni necessarie per creare le entità di sicurezza nella partizione del dominio Active Directory sono controllati dal RBAC. Solo Exchange server, servizi e gli utenti che sono membri dei gruppi di ruolo appropriate possono creare le entità di sicurezza.

  - **Autorizzazioni suddivise Active Directory**   Le autorizzazioni per la creazione delle entità di sicurezza nella partizione di dominio di Active Directory vengono completamente rimosse da qualsiasi utente, servizio o server Exchange. Per creare le entità di sicurezza, non viene fornita alcuna opzione in RBAC. La creazione delle entità di sicurezza in Active Directory deve essere eseguita utilizzando gli strumenti di gestione di Active Directory.
    

    > [!IMPORTANT]
    > Sebbene Active Directory dividere autorizzazioni possono attivate o disabilitate eseguendo il programma di installazione in un computer con Exchange 2013 installato diviso Active Directory configurazione delle autorizzazioni si applica ai server sia Exchange 2013 e Exchange&nbsp;2010. Tuttavia, non ha effetto sulle server Exchange Server 2007 Microsoft.



Se l'organizzazione decide di utilizzare un modello di autorizzazioni suddivise anziché autorizzazioni condivise, è consigliabile utilizzare il modello di autorizzazioni suddivise RBAC. Il modello di autorizzazioni suddivise RBAC fornisce significativamente maggiore flessibilità mantenendo la stessa quasi separazione di amministrazione come Active Directory divisione delle autorizzazioni con l'eccezione che Exchange i server e servizi è possono creare le entità di sicurezza in RBAC modello di autorizzazioni suddivise.

Viene chiesto se si desidera abilitare Active Directory suddividere le autorizzazioni durante l'installazione. Se si sceglie di abilitare Active Directory divisione delle autorizzazioni, è possibile modificare solo alle autorizzazioni condivise o RBAC dividere autorizzazioni eseguendo nuovamente l'installazione e disattivazione Active Directory divisione delle autorizzazioni. Questa opzione applica a tutti i server Exchange 2010 e Exchange 2013 nell'organizzazione.

Nelle sezioni seguenti vengono descritti RBAC e Active Directory divisione delle autorizzazioni in modo più dettagliato.

Inizio pagina

## RBAC divisione delle autorizzazioni

Il modello di sicurezza RBAC consente di modificare le assegnazioni dei ruoli di gestione predefinito per separare gli utenti possono creare le entità di sicurezza nella partizione del dominio Active Directory da chi amministrare i dati dell'organizzazione Exchange nella partizione di configurazione Active Directory. Le entità di sicurezza, ad esempio gli utenti con cassette postali e i gruppi di distribuzione possono essere create dagli amministratori che sono membri della creazione dei destinatari della posta e la creazione del gruppo di sicurezza e appartenenza a ruoli. Queste autorizzazioni restano separate dalle autorizzazioni necessarie per creare le entità di sicurezza di fuori Exchange gli strumenti di gestione. gli amministratori Exchange che non sono assegnati la creazione dei destinatari stampa o la creazione del gruppo di sicurezza e appartenenza a ruoli possono comunque modificare Exchange-attributi correlati alle entità di sicurezza. gli amministratori Active Directory hanno anche la possibilità di utilizzare gli strumenti di gestione Exchange per creare Active Directory le entità di sicurezza.

server Exchange e Exchange sottosistema Trusted disporre delle autorizzazioni per creare le entità di sicurezza in Active Directory per conto di utenti e applicazioni di terze parti che si integrano con RBAC.

RBAC divisione delle autorizzazioni è utile per l'organizzazione se si verifica quanto segue:

  - L'organizzazione non richiede che la creazione di entità di sicurezza essere eseguite utilizzando solo gli strumenti di gestione Active Directory e solo per gli utenti vengono assegnati autorizzazioni specifiche Active Directory.

  - L'organizzazione consente servizi, ad esempio server Exchange, per creare le entità di sicurezza.

  - Si desidera semplificare il processo necessario per creare cassette postali, gli utenti abilitati alla posta elettronica, i gruppi di distribuzione e gruppi di ruoli tramite la loro creazione all'interno di Exchange gli strumenti di gestione.

  - Si desidera gestire l'appartenenza di gruppi di distribuzione e gruppi di ruoli all'interno di strumenti di gestione Exchange.

  - Si dispongono di programmi di terze parti che richiedono che Exchange server siano in grado di creare le entità di sicurezza per loro conto.

Se l'organizzazione richiede una separazione completa di amministrazione Exchange e Active Directory in cui non amministrazione Active Directory può essere eseguita utilizzando gli strumenti di gestione Exchange o Exchange servizi, vedere la sezione Autorizzazioni di Active Directory diviso più avanti in questo argomento.

Il passaggio da autorizzazioni condivise a RBAC divisione delle autorizzazioni è un processo manuale cui rimuovere le autorizzazioni necessarie per creare le entità di sicurezza tra i gruppi di ruoli che vengono concesse per impostazione predefinita. Nella tabella seguente vengono illustrati i ruoli che consentono la creazione di entità di sicurezza in Exchange e i gruppi di ruoli di gestione che sono stati assegnati per impostazione predefinita.

### Ruoli di gestione di entità di sicurezza

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruoli di gestione</th>
<th>Gruppo di ruoli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Ruolo di creazione dei destinatari di posta</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">La creazione del gruppo di sicurezza e l'appartenenza al ruolo</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
</tbody>
</table>


Per impostazione predefinita, i membri dei gruppi di ruolo Gestione organizzazione e Gestione destinatari possono creare le entità di sicurezza. È necessario trasferire la possibilità di creare le entità di sicurezza tra i gruppi di ruoli incorporati e un nuovo gruppo di ruoli creati personalmente.

Per configurare RBAC divisione delle autorizzazioni, è necessario eseguire le operazioni seguenti:

1.  Disattivare le autorizzazioni di divisione Active Directory se è abilitato.

2.  Creare un gruppo di ruoli, che conterrà gli amministratori Active Directory che saranno in grado di creare le entità di sicurezza.

3.  Creare le assegnazioni di ruolo regolare e di delega tra il ruolo della creazione dei destinatari e il nuovo gruppo di ruoli.

4.  Creare le assegnazioni di ruolo regolare e di delega tra la creazione del gruppo di sicurezza e l'appartenenza al ruolo e il nuovo gruppo di ruoli.

5.  Rimuovere i normali e assegnazioni di ruolo Gestione tra il ruolo della creazione dei destinatari e i gruppi di ruoli Gestione organizzazione e Gestione destinatari Delegate.

6.  Rimuovere i normali e assegnazioni di ruolo tra la creazione del gruppo di sicurezza e l'appartenenza al ruolo e gruppo di ruoli Gestione organizzazione Delegate.

Dopo aver in questo modo, solo i membri del nuovo gruppo di ruoli creati personalmente sarà in grado di creare le entità di sicurezza, ad esempio le cassette postali. Il nuovo gruppo solo sarà in grado di creare gli oggetti. Non sarà in grado di configurare gli attributi Exchange sul nuovo oggetto. Un amministratore Active Directory, che è un membro del nuovo gruppo, sarà necessario per creare l'oggetto e un amministratore Exchange sarà necessario configurare gli attributi Exchange sull'oggetto. gli amministratori Exchange non saranno in grado di utilizzare i cmdlet seguenti:

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

gli amministratori Exchange, tuttavia, saranno in grado di creare e gestire Exchange-specifici oggetti, ad esempio le regole di trasporto, i gruppi di distribuzione e così via e gestire Exchange-attributi correlati a tutti gli oggetti.

Inoltre, le caratteristiche associate EAC e Outlook Web App, ad esempio la cassetta postale della procedura guidata nuovo anche non saranno più disponibili o generano un errore se si tenta di utilizzarli.

Se si desidera che il nuovo gruppo di ruoli anche siano in grado di gestire gli attributi Exchange sul nuovo oggetto, il ruolo destinatari di posta elettronica deve anche da assegnare al nuovo gruppo di ruoli.

Per ulteriori informazioni sulla configurazione di un modello di autorizzazioni suddivise, vedere [Configurare Exchange 2013 per le autorizzazioni diviso](configure-exchange-2013-for-split-permissions-exchange-2013-help.md).

Inizio pagina

## Autorizzazioni suddivise di Active Directory

Con Active Directory divisione delle autorizzazioni, è necessario eseguire la creazione di entità di sicurezza nella partizione del dominio Active Directory, ad esempio le cassette postali e i gruppi di distribuzione utilizzando gli strumenti di gestione Active Directory. Vengono apportate diverse modifiche per le autorizzazioni concesse per i server di sottosistema Trusted e ExchangeExchange per limitare le operazioni che possono eseguire Exchange amministratori e i server. Le seguenti modifiche di funzionalità si verificano quando si abilita Active Directory divisione delle autorizzazioni:

  - Creazione di cassette postali, gli utenti abilitati alla posta elettronica, i gruppi di distribuzione e altre entità di sicurezza viene rimosso da strumenti di gestione Exchange.

  - Aggiunta e rimozione di membri del gruppo di distribuzione non può essere eseguite Exchange strumenti di gestione.

  - Vengono rimosse tutte le autorizzazioni concesse per i server di sottosistema Trusted e ExchangeExchange per creare le entità di sicurezza.

  - Exchange server e gli strumenti di gestione Exchange possono solo modificare gli attributi Exchange esistente di entità di sicurezza in Active Directory.

Ad esempio, per creare una cassetta postale con Active Directory autorizzazioni diviso abilitate, un utente deve prima crearlo mediante strumenti Active Directory da un utente con le autorizzazioni necessarie Active Directory. L'utente può quindi essere abilitati alla cassetta postale utilizzando gli strumenti di gestione Exchange. Solo il Exchange-relativi attributi della cassetta postale possono essere modificati dagli amministratori Exchange utilizzando gli strumenti di gestione Exchange.

Active Directory divisione delle autorizzazioni è utile per l'organizzazione se si verifica quanto segue:

  - L'organizzazione richiede che le entità di sicurezza siano creati utilizzando solo gli strumenti di gestione Active Directory o solo da utenti che vengono concesse autorizzazioni specifiche in Active Directory.

  - Si desidera separare completamente la possibilità di creare le entità di sicurezza da quelli che gestiscono l'organizzazione Exchange.

  - Si desidera eseguire tutte le gestione gruppo di distribuzione, incluse la creazione di gruppi di distribuzione e aggiungere e rimuovere i membri dei gruppi, utilizzando gli strumenti di gestione Active Directory.

  - Non si desidera Exchange server o i programmi di terze parti che utilizzano Exchange per loro conto, per creare le entità di sicurezza.


> [!IMPORTANT]
> Passaggio a Active Directory divisione delle autorizzazioni è un'opzione in cui è possibile effettuare quando si installa Exchange 2013 o utilizzando l'installazione guidata utilizzando il parametro <EM>ActiveDirectorySplitPermissions</EM> durante l'esecuzione di <CODE>setup.exe</CODE> dalla riga di comando. È inoltre possibile abilitare o disabilitare Active Directory dividere autorizzazioni dopo aver installato Exchange 2013 rieseguendo <CODE>setup.exe</CODE> dalla riga di comando. Per abilitare Active Directory divisione delle autorizzazioni, impostare il parametro <EM>ActiveDirectorySplitPermissions</EM> su <CODE>true</CODE>. Per disabilitarlo, impostarlo su <CODE>false</CODE>. È sempre necessario specificare l'opzione <EM>PrepareAD</EM> insieme al parametro <EM>ActiveDirectorySplitPermissions</EM> .<BR>Se si dispone di più domini nella stessa foresta, è inoltre necessario specificare l'opzione <EM>PrepareAllDomains</EM> quando si applica Active Directory divisione delle autorizzazioni o eseguita l'installazione con l'opzione <EM>PrepareDomain</EM> in ciascun dominio. Se si sceglie di eseguire il programma di installazione con l'opzione <EM>PrepareDomain</EM> in ciascun dominio anziché utilizzare l'opzione <EM>PrepareAllDomains</EM> , è necessario preparare tutti i domini che contiene Exchange server, gli oggetti abilitati alla posta elettronica o server di catalogo globale che potrebbero essere visualizzati da un server Exchange.




> [!IMPORTANT]
> Non è possibile abilitare Active Directory dividere autorizzazioni se è stato installato Exchange&nbsp;2010 o Exchange 2013 in un controller di dominio.<BR>Dopo aver attivato o disattivato Active Directory divisione delle autorizzazioni, è consigliabile riavviare i server Exchange&nbsp;2010 e Exchange 2013 all'interno dell'organizzazione per imporre la loro sollevare il nuovo token di accesso Active Directory con le autorizzazioni aggiornate.



Exchange 2013 raggiunge Active Directory diviso autorizzazioni rimuovendo le autorizzazioni e appartenenze dal gruppo di protezione ExchangeWindows le autorizzazioni. Questo gruppo di protezione, in autorizzazioni condivise e le autorizzazioni di divisione RBAC, è concesse autorizzazioni a molti oggetti non -Exchange e gli attributi in tutta Active Directory. Per rimuovere le autorizzazioni e l'appartenenza al gruppo di sicurezza, servizi e gli amministratori Exchange vengono impediti creazione o modifica di tali oggettiActive Directory non -Exchange.

Per un elenco delle modifiche che si verificano per il gruppo di sicurezza ExchangeWindows le autorizzazioni e altri componenti Exchange quando si abilita o disabilita Active Directory divisione delle autorizzazioni, vedere la tabella seguente.


> [!NOTE]
> Le assegnazioni di ruolo ai gruppi di ruoli che consentono agli amministratori di Exchange creare le entità di sicurezza vengono rimosse quando è abilitata la Active Directory divisione delle autorizzazioni. Questa operazione viene eseguita per rimuovere l'accesso ai cmdlet che verrebbero altrimenti genererà un errore fase di esecuzione perché non dispone delle autorizzazioni per creare l'oggetto associato Active Directory.



### Modifiche apportate alle autorizzazioni suddivise di Active Directory

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Azione</th>
<th>Modifiche apportate da Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Abilitare Active Directory suddividere le autorizzazioni durante l'installazione di server prima Exchange 2013</p></td>
<td><p>Le seguenti operazioni quando si abilita Active Directory suddividere le autorizzazioni tramite l'installazione guidata oppure eseguendo <code>setup.exe</code> con i parametri <code>/PrepareAD</code> e <code>/ActiveDirectorySplitPermissions:true</code> :</p>
<ul>
<li><p>Viene creata un'unità organizzativa (OU) denominata <strong>Gruppi protetta di Microsoft Exchange</strong>.</p></li>
<li><p>Il gruppo di sicurezza di <strong>Autorizzazioni di Windows Exchange</strong> viene creato in <strong>Microsoft Exchange protetta gruppi</strong> dell'unità Organizzativa.</p></li>
<li><p>Il gruppo di protezione di <strong>Exchange Trusted Subsystem</strong> non viene aggiunto al gruppo di protezione <strong>Exchange le autorizzazioni di Windows</strong>.</p></li>
<li><p>Creazione non delega gestione delle assegnazioni di ruolo ai ruoli di gestione con i seguenti tipi di ruoli di gestione è stata ignorata:</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>Voci di controllo di accesso (ACE) assegnata al gruppo di protezione <strong>Exchange le autorizzazioni di Windows</strong> non vengono aggiunti all'oggetto dominio Active Directory.</p></li>
</ul>
<p>Se si esegue il programma di installazione con l'opzione <em>PrepareAllDomains</em> o <em>PrepareDomain</em> , accade quanto segue in ciascun dominio figlio preparato:</p>
<ul>
<li><p>Tutte le voci assegnate al gruppo di protezione <strong>Exchange le autorizzazioni di Windows</strong> vengono rimossi dall'oggetto di dominio.</p></li>
<li><p>Le voci vengono impostate in ciascun dominio con l'eccezione qualsiasi ACE assegnato al gruppo di protezione <strong>Exchange le autorizzazioni di Windows</strong>.</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>Passaggio da autorizzazioni condivise o RBAC suddividere le autorizzazioni per Active Directory divisione delle autorizzazioni</p></td>
<td><p>Le seguenti operazioni quando si esegue il comando <code>setup.exe</code> con i parametri <code>/PrepareAD</code> e <code>/ActiveDirectorySplitPermissions:true</code> :</p>
<ul>
<li><p>Viene creata un'unità Organizzativa denominata <strong>Gruppi protetta di Microsoft Exchange</strong> .</p></li>
<li><p>Il gruppo di sicurezza di <strong>Autorizzazioni di Windows Exchange</strong> viene spostato all'unità Organizzativa gruppi di <strong>Microsoft Exchange protetto</strong>.</p></li>
<li><p>Il gruppo di protezione di <strong>Exchange Trusted Subsystem</strong> viene rimosso dal gruppo di protezione di <strong>Exchange le autorizzazioni di Windows</strong>.</p></li>
<li><p>Sono stati rimossi non delega assegnazioni di ruolo qualsiasi ai ruoli di gestione con i tipi di ruoli seguenti:</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>Tutte le voci assegnate al gruppo di protezione <strong>Exchange le autorizzazioni di Windows</strong> vengono rimossi dall'oggetto di dominio.</p></li>
</ul>
<p>Se si esegue il programma di installazione con l'opzione <em>PrepareAllDomains</em> o <em>PrepareDomain</em> , accade quanto segue in ciascun dominio figlio preparato:</p>
<ul>
<li><p>Tutte le voci assegnate al gruppo di protezione <strong>Exchange le autorizzazioni di Windows</strong> vengono rimossi dall'oggetto di dominio.</p></li>
<li><p>Le voci vengono impostate in ciascun dominio con l'eccezione qualsiasi ACE assegnato al gruppo di protezione <strong>Exchange le autorizzazioni di Windows</strong>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Passare da Active Directory suddividere le autorizzazioni per autorizzazioni condivise o RBAC diviso</p></td>
<td><p>Le seguenti operazioni quando si esegue il comando <code>setup.exe</code> con i parametri <code>/PrepareAD</code> e <code>/ActiveDirectorySplitPermissions:false</code> :</p>
<ul>
<li><p>Il gruppo di sicurezza di <strong>Autorizzazioni di Windows Exchange</strong> viene spostato a <strong>Microsoft Exchange Security Groups</strong> unità Organizzativa.</p></li>
<li><p>L'unità Organizzativa <strong>Gruppi di protetti da Microsoft Exchange</strong> è stata rimossa.</p></li>
<li><p>Il gruppo di sicurezza <strong>Sottosistemi attendibili di Exchange</strong> viene aggiunto al gruppo di protezione <strong>Exchange le autorizzazioni di Windows</strong>.</p></li>
<li><p>Le voci vengono aggiunte all'oggetto di dominio per il gruppo di protezione di <strong>Exchange le autorizzazioni di Windows</strong>.</p></li>
</ul>
<p>Se si esegue il programma di installazione con l'opzione <em>PrepareAllDomains</em> o <em>PrepareDomain</em> , accade quanto segue in ciascun dominio figlio preparato:</p>
<ul>
<li><p>Le voci vengono aggiunte all'oggetto di dominio per il gruppo di protezione di <strong>Exchange le autorizzazioni di Windows</strong>.</p></li>
<li><p>Le voci vengono impostate in ciascun dominio tra cui le voci assegnate al gruppo di protezione <strong>Exchange le autorizzazioni di Windows</strong>.</p></li>
</ul>
<p>Le assegnazioni di ruolo alla creazione dei destinatari della posta e la creazione del gruppo di sicurezza e ruoli di appartenenza non vengono create automaticamente quando si passa da Active Directory divisi per autorizzazioni condivise. Se le assegnazioni di ruolo delegate sono state personalizzate prima Active Directory suddividere le autorizzazioni che si sta abilitare, tali personalizzazioni vengono lasciate inalterate. Per creare le assegnazioni di ruolo tra questi ruoli e il gruppo di ruoli Gestione organizzazione, vedere <a href="configure-exchange-2013-for-shared-permissions-exchange-2013-help.md">Configurare Exchange 2013 per autorizzazioni condivise</a>.</p></td>
</tr>
</tbody>
</table>


Dopo aver abilitato Active Directory divisione delle autorizzazioni, i cmdlet seguenti non sono più disponibili:

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Dopo aver abilitato Active Directory suddividere le autorizzazioni, i cmdlet seguenti sono accessibili ma non possono essere utilizzati per creare gruppi di distribuzione o modificare l'appartenenza al gruppo di distribuzione:

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Update-DistributionGroupMember**

Alcuni cmdlet, anche se è ancora disponibile, possono offrire solo una funzionalità limitata se utilizzato con Active Directory divisione delle autorizzazioni. Ciò avviene perché potrebbe consentono di configurare gli oggetti destinatario che si trovano nella partizione del dominio Active Directory e Exchange degli oggetti di configurazione presenti nella partizione di configurazione Active Directory. Può inoltre consentono di configurare Exchange-relativi attributi per gli oggetti memorizzati nella partizione del dominio. Tenta di utilizzare i cmdlet per creare oggetti o modificare non -Exchange-relativi attributi negli oggetti nella partizione del dominio, verranno generato un errore. Ad esempio, il cmdlet **Add-ADPermission** restituirà un errore se si tenta di aggiungere autorizzazioni a una cassetta postale. Tuttavia, il cmdlet **Add-ADPermission** avrà esito positivo se si configurano le autorizzazioni su un connettore di ricezione. Ciò avviene perché una cassetta postale viene archiviata nella partizione del dominio mentre connettori di ricezione sono archiviati nella partizione di configurazione.

Inoltre, le caratteristiche associate nell'interfaccia di amministrazione Exchange e Outlook Web App, ad esempio creazione guidata nuova cassetta postale anche non saranno più disponibili o genererà un errore se si tenta di utilizzarli.

gli amministratori Exchange, tuttavia, saranno in grado di creare e gestire Exchange-oggetti specifici, ad esempio le regole di trasporto e così via.

Per ulteriori informazioni sulla configurazione Active Directory un modello di autorizzazioni suddivise, vedere [Configurare Exchange 2013 per le autorizzazioni diviso](configure-exchange-2013-for-split-permissions-exchange-2013-help.md).

Inizio pagina


---
title: 'Autorizzazioni: Exchange 2013 Help'
TOCTitle: Autorizzazioni
ms:assetid: d8dd605e-0af1-4e18-9ce6-e51d04e161ba
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351175(v=EXCHG.150)
ms:contentKeyID: 50481820
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzazioni

 

_**Si applica a:** Exchange Server, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Microsoft Exchange Server 2013 include un gran numero di autorizzazioni predefinite, basate sul modello di autorizzazioni RBAC (Role Based Access Control, Controllo di accesso basato sui ruoli), utilizzabili immediatamente per concedere facilmente le autorizzazioni agli amministratori e agli utenti. È possibile utilizzare le funzionalità delle autorizzazioni di Exchange 2013 che consentono all'organizzazione di diventare rapidamente operativa.


> [!NOTE]
> Alcune funzionalità e nozioni relative al controllo di accesso basato sui ruoli non vengono illustrate nel presente argomento perché rientrano nelle funzionalità avanzate. Se la funzionalità descritta in questo argomento non soddisfa le proprie esigenze e si desidera personalizzare ulteriormente il modello delle autorizzazioni, vedere <A href="understanding-role-based-access-control-exchange-2013-help.md">Controllo di accesso basato sui ruoli</A>.



Per l'elenco di tutti gli argomenti relativi alle autorizzazioni, vedere Permissions documentation.

**Sommario**

Role-based permissions

Role groups and role assignment policies

Work with role groups

Work with role assignment policies

## Autorizzazioni basate sui ruoli

In Exchange 2013, le autorizzazione che vengono concesse agli amministratori e agli utenti sono basate sui ruoli di gestione. Un ruolo definisce l'insieme di attività che un amministratore o un utente sono in grado di eseguire. Ad esempio, il ruolo di gestione denominato `Mail Recipients` definisce le attività che una persona può eseguire per un insieme di cassette postali, contatti e gruppi di distribuzione. Quando viene assegnato un ruolo a un amministratore o a un utente, alla persona vengono concesse le autorizzazioni fornite dal ruolo.

Esistono due tipi di ruoli, ruoli amministrativi e ruoli dell'utente finale:

  - **Ruoli amministrativi**   Tali ruoli contengono le autorizzazioni che possono essere assegnate agli amministratori o a utenti esperti che utilizzano i gruppi di ruoli che si occupano della gestione di una parte dell'organizzazione di Exchange, ad esempio destinatari, server o database.

  - **Ruoli dell'utente finale**   Tali ruoli, assegnati mediante i criteri di assegnazione, consentono agli utenti di gestire vari aspetti della propria cassetta postale e dei gruppi di distribuzione di cui sono proprietari. I ruoli dell'utente finale iniziano con il prefisso `My`.

I ruoli concedono le autorizzazioni che consentono l'esecuzione di attività per amministratori e utenti, rendendo disponibili i cmdlet a coloro a cui sono stati assegnati i ruoli. Poiché in Interfaccia di amministrazione di Exchange e in Exchange Management Shell i cmdlet vengono utilizzati per la gestione di Exchange, la concessione dell'accesso a un cmdlet consente all'amministratore o all'utente di eseguire l'attività in ogni singola interfaccia di gestione di Exchange.

Exchange 2013 include all'incirca 86 ruoli utilizzabili per concedere le autorizzazioni. Per un elenco dei ruoli inclusi in Exchange 2013, vedere [Ruoli di gestione predefiniti](built-in-management-roles-exchange-2013-help.md).

Inizio pagina

## Gruppi di ruoli e criteri dell'assegnazione di ruoli

I ruoli concedono le autorizzazioni per eseguire le attività in Exchange 2013, ma è necessario un metodo semplice per assegnarle ad amministratori e utenti. Exchange 2013 fornisce i seguenti metodi per l'assegnazione delle autorizzazioni:

  - **Gruppi di ruolo**   I gruppi di ruolo consentono di concedere le autorizzazioni agli amministratori e agli utenti esperti.

  - **Criteri dell'assegnazione di ruolo**   Mediante i criteri dell'assegnazione di ruolo è possibile concedere le autorizzazioni agli utenti finali per modificare le impostazioni delle proprie cassette postali o gruppi di distribuzione di cui sono proprietari.

Per ulteriori informazioni sui gruppi di ruoli e sui criteri di assegnazione dei ruoli, vedere le seguenti sezioni.

## Gruppi di ruoli

A ogni amministratore che si occupa della gestione di Exchange 2013 devono essere assegnati almeno uno o più ruoli. Gli amministratori possono disporre di più ruoli perché eseguono mansioni che si estendono su più aree di Exchange. Ad esempio, un amministratore potrebbe gestire sia i destinatari che i server Exchange. In tal caso, all'amministratore potrebbe essere assegnato sia il ruolo `Mail Recipients` che il ruolo `Exchange Servers`.

Per agevolare l'assegnazione di più ruoli a un amministratore, Exchange 2013 include i gruppi di ruoli. I gruppi di ruolo sono gruppi di protezione universale (USG, Universal Security Groups) speciali utilizzati da Exchange 2013 che possono contenere utenti di Active Directory, gruppi di protezione universale e altri gruppi di ruolo. Quando viene assegnato un ruolo a un gruppo di ruolo, le autorizzazioni concesse dal ruolo vengono estese a tutti i membri del gruppo di ruolo. In questo modo è possibile assegnare contemporaneamente molti ruoli a vari membri del gruppo di ruolo. I gruppi di ruolo riguardano in genere aree di gestione più ampie, ad esempio la gestione dei destinatari. Vengono utilizzati solo con i ruoli amministrativi e non con i ruoli dell'utente finale.


> [!NOTE]
> È possibile assegnare un ruolo direttamente a un utente o a un gruppo di protezione universale (USG) senza utilizzare un gruppo di ruolo. Questo metodo di assegnazione di ruolo, tuttavia, è una procedura avanzata che non viene affrontata in questo argomento. Si consiglia di utilizzare i gruppi di ruolo per gestire le autorizzazioni.



Nella figura che segue viene mostrata la relazione tra utenti, gruppi di ruolo e ruoli.

**Ruoli, gruppi di ruolo e membri del gruppo di ruolo**

![Ruolo, gruppo di ruoli e relazione dei membri](images/Dd351175.3fb0b47d-333a-4953-ae38-d710d327bde0(EXCHG.150).gif "Ruolo, gruppo di ruoli e relazione dei membri")

Exchange 2013 comprende alcuni gruppi di ruolo incorporati che forniscono ciascuno le autorizzazioni per la gestione di aree specifiche in Exchange 2013. Alcuni gruppi di ruolo possono sovrapporsi ad altri. Nella tabella seguente i gruppi di ruolo vengono elencati singolarmente con relativa descrizione dell'utilizzo. Per visualizzare i ruoli assegnati a ciascun gruppo di ruoli, fare clic sul nome del gruppo di ruoli nella colonna "Gruppo di ruoli" e aprire la sezione "Ruoli di gestione assegnati a questo gruppo di ruoli".

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
<td><p>Gli amministratori membri del gruppo di ruolo Gestione organizzazione dispongono dell'accesso amministrativo all'intera organizzazione di°Exchange 2013 e possono eseguire quasi tutte le attività su qualsiasi oggetto di°Exchange 2013, con alcune eccezioni quali <code>Discovery Management</code>.</p>

> [!IMPORTANT]
> Poiché il gruppo di ruolo Gestione organizzazione indica un ruolo potente, solo gli utenti o i gruppi di protezione universale, che eseguono attività amministrative a livello di organizzazione che possono potenzialmente influire sull'intera organizzazione di°Exchange, dovrebbero essere membri di questo gruppo.


</td>
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
<td><p>Gli amministratori membri del gruppo di ruoli Gestione della messaggistica unificata possono gestire le funzionalità nell'organizzazione di Exchange, ad esempio la configurazione del servizio Messaggistica unificata, le proprietà di messaggistica unificata nelle cassette postali, le istruzioni vocali di messaggistica unificata e la configurazione dell'operatore automatico di messaggistica unificata.</p></td>
</tr>
<tr class="odd">
<td><p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
<td><p>Per impostazione predefinita, il gruppo di ruoli Help Desk consente ai membri di visualizzare e modificare le opzioni di Microsoft OfficeOutlook Web App per qualsiasi utente nell'organizzazione. Queste opzioni potrebbero includere la modifica del nome visualizzato, dell'indirizzo e del numero telefonico. Non comprendono le opzioni che non sono disponibili in Outlook Web App, ad esempio la modifica delle dimensioni di una cassetta postale o la configurazione del database delle cassette postali in cui si trova una cassetta postale.</p></td>
</tr>
<tr class="even">
<td><p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p></td>
<td><p>Gli amministratori che appartengono al gruppo di ruolo per la gestione della sicurezza possono configurare le funzionalità antivirus e filtro posta indesiderata di Exchange 2013. È possibile aggiungere account di servizio a questo gruppo per consentire ai programmi di terzi integrabili con Exchange 2013 di accedere ai cmdlet necessari per recuperare e impostare la configurazione di Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
<td><p>Gli utenti membri del gruppo di ruolo°Gestione record possono configurare le funzionalità di conformità, come le tag dei criteri di conservazione, le classificazioni dei messaggi e le regole di trasporto.</p></td>
</tr>
<tr class="even">
<td><p><a href="discovery-management-exchange-2013-help.md">Gestione individuazione</a></p></td>
<td><p>Gli amministratori o gli utenti membri del gruppo di ruoli Gestione individuazione possono effettuare la ricerca dei dati rispondenti a determinati criteri nelle cassette postali dell'organizzazione di Exchange e anche configurare le conservazioni a fini giudiziari nelle cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">Gestione cartelle pubbliche</a></p></td>
<td><p>Gli amministratori membri del gruppo di ruolo Gestione di cartelle pubbliche possono gestire le cartelle pubbliche sui server con Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
<td><p>Gli amministratori membri del gruppo di ruolo Gestione server possono eseguire la configurazione specifica del server delle funzionalità relative al trasporto, alla messaggistica unificata, all'accesso client e alle cassette postali come, ad esempio, copie del database, certificati, code di trasporto, connettori di invio, directory virtuali e protocolli per l'accesso client.</p></td>
</tr>
<tr class="odd">
<td><p><a href="delegated-setup-exchange-2013-help.md">Installazione delegata</a></p></td>
<td><p>Gli amministratori membri del gruppo di ruolo Configurazione delegata possono distribuire i server Exchange 2013 precedentemente sottoposti a provisioning da un membro del gruppo di ruolo Gestione organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">Gestione della conformità</a></p></td>
<td><p>Gli utenti membri del gruppo di ruoli Gestione conformità possono configurare e gestire le impostazioni di conformità di Exchange in base ai criteri dell'organizzazione.</p></td>
</tr>
</tbody>
</table>


Se si lavora in un'organizzazione di piccole dimensioni con pochi amministratori, potrebbe essere necessario aggiungere tali amministratori solo al gruppo di ruolo Gestione organizzazione e probabilmente non sarà necessario in alcun caso utilizzare gli altri gruppi di ruolo. Se l'organizzazione è di grandi dimensioni, si avranno probabilmente amministratori che si occupano di attività specifiche nell'ambito dell'amministrazione di Exchange, ad esempio la gestione dei destinatari o del server. In tali casi, potrebbe essere utile aggiungere un amministratore al gruppo di ruolo Gestione destinatari e un altro amministratore al gruppo di ruolo Gestione server. Questi amministratori sono quindi in grado di gestire aree specifiche di Exchange 2013, ma non disporranno delle autorizzazioni necessarie per gestire aree di cui non sono responsabili.

Se i gruppi di ruolo incorporati in Exchange 2013 non corrispondono alla mansione degli amministratori, è possibile creare gruppi di ruolo e aggiungervi i ruoli desiderati. Per ulteriori informazioni, vedere Work with Role Groups più avanti in questo argomento.

Inizio pagina

## Criteri di assegnazione dei ruoli

Exchange 2013 fornisce i criteri dell'assegnazione di ruolo che consentono di controllare le impostazioni che gli utenti sono autorizzati a configurare nelle proprie cassette postali e nei gruppi di distribuzione di cui sono proprietari. Tali impostazioni includono il nome visualizzato, le informazioni di contatto, le impostazioni del sistema di caselle vocali e l'appartenenza a gruppi di distribuzione.

Nell'organizzazione di Exchange 2013 è possibile disporre di più criteri di assegnazione dei ruoli che forniscono livelli di autorizzazioni diversi per differenti tipi di utenti nelle organizzazioni. Ad alcuni utenti può essere consentito modificare il proprio indirizzo o creare gruppi di distribuzione, diversamente da altri, in base al criterio di assegnazione dei ruoli associato alla propria cassetta postale. I criteri dell'assegnazione di ruolo vengono aggiunti direttamente alle cassette postali e ogni cassetta postale può essere associata solo a un criterio dell'assegnazione di ruolo alla volta.

Tra i criteri dell'assegnazione di ruolo dell'organizzazione, uno è contrassegnato come predefinito. Il criterio dell'assegnazione di ruolo predefinito è associato a nuove cassette postali a cui non è stato assegnato esplicitamente un criterio specifico di assegnazione del ruolo al momento della creazione. Il criterio dell'assegnazione di ruolo predefinito deve contenere le autorizzazioni da applicare alla maggior parte delle cassette postali.

Le autorizzazioni vengono aggiunte ai criteri dell'assegnazione di ruolo utilizzando i ruoli dell'utente finale. I ruoli dell'utente finale iniziano con `My` e concedono agli utenti le autorizzazioni per gestire solo la propria cassetta postale o i gruppi di distribuzione di cui sono proprietari. Non possono essere utilizzati per gestire altre cassette postali. Solo i ruoli dell'utente finale possono essere assegnati ai criteri dell'assegnazione di ruolo.

Quando a un utente finale viene assegnato un criterio dell'assegnazione di ruolo, tutte le cassette postali associate a quel ruolo ricevono le autorizzazioni concesse dal ruolo. In questo modo è possibile aggiungere o rimuovere le autorizzazioni a gruppi di utenti senza dover configurare le singole cassette postali. Nella figura successiva viene illustrato quanto segue:

  - I ruoli dell'utente finale vengono assegnati ai criteri dell'assegnazione di ruolo. I criteri dell'assegnazione di ruolo possono condividere gli stessi ruoli dell'utente finale.

  - I criteri dell'assegnazione di ruolo sono associati alle cassette postali. Ogni cassetta postale può essere associata a un solo criterio dell'assegnazione di ruolo.

  - Una volta associata una cassetta postale a un criterio dell'assegnazione di ruolo, i ruoli dell'utente finale vengono applicati alla cassetta postale. Le autorizzazioni concesse dai ruoli vengono concesse all'utente della cassetta postale.

**Ruoli, criteri dell'assegnazione di ruolo e cassette postali**

![Relazioni tra ruolo, criteri di assegnazione dei ruoli e cassetta postale](images/Dd351175.82e07b3d-da59-465b-b349-e0bfde369ace(EXCHG.150).gif "Relazioni tra ruolo, criteri di assegnazione dei ruoli e cassetta postale")

Il criterio di assegnazione dei ruoli Criterio predefinito di assegnazione dei ruoli è incluso in Exchange 2013. Come suggerisce il nome, si tratta del criterio di assegnazione dei ruoli predefinito. Per modificare le autorizzazioni fornite da questo criterio dell'assegnazione di ruolo o per creare criteri dell'assegnazione di ruolo, vedere Work with Role Assignment Policies più avanti in questo argomento.

## Utilizzo dei gruppi di ruoli

Per gestire le autorizzazioni utilizzando i gruppi di ruoli in Exchange 2013, è consigliabile utilizzare Interfaccia di amministrazione di Exchange. Quando si utilizza EAC per gestire i gruppi di ruoli, è possibile aggiungere e rimuovere ruoli e membri, creare gruppi di ruoli e copiare gruppi di ruoli con poche operazioni del mouse. EAC offre finestre di dialogo semplici, come la finestra di dialogo **nuovo gruppo di ruoli**, mostrata nella figura seguente, per eseguire tali attività.

**Finestra di dialogo Nuovo gruppo di ruoli in Stima al completamento**

![Finestra di dialogo Nuovo gruppo di ruoli nell'interfaccia di amministrazione di Exchange](images/Dd351175.e0577090-73e6-4671-ae98-78a8064fde87(EXCHG.150).jpg "Finestra di dialogo Nuovo gruppo di ruoli nell'interfaccia di amministrazione di Exchange")

In Exchange 2013 sono inclusi diversi gruppi di ruoli che separano le autorizzazioni in aree amministrative specifiche. Se questi gruppi di ruolo esistenti forniscono le autorizzazioni necessarie agli amministratori per gestire l'organizzazione di Exchange 2013, è sufficiente aggiungere gli amministratori come membri dei gruppi di ruolo appropriati. Una volta aggiunti a un gruppo di ruolo, gli amministratori saranno in grado di amministrare le funzionalità legate a quel gruppo di ruolo. Per aggiungere o rimuovere membri da un gruppo di ruoli, aprire il gruppo di ruoli in Interfaccia di amministrazione di Exchange (EAC) e aggiungere o rimuovere i membri dall'elenco di appartenenza. Per un elenco dei gruppi di ruoli di gestione incorporati, vedere [Gruppi di ruoli incorporati](built-in-role-groups-exchange-2013-help.md).


> [!IMPORTANT]
> Se un amministratore è membro di più gruppi di ruolo, Exchange 2013 concede all'amministratore tutte le autorizzazioni fornite dai gruppi di ruolo di cui è membro.



Se nessuno dei gruppi di ruoli inclusi in Exchange 2013 dispone delle autorizzazioni necessarie, è possibile utilizzare EAC per creare un gruppo di ruoli e aggiungere i ruoli con le autorizzazioni necessarie. Per il nuovo gruppo di ruolo è necessario procedere come segue:

1.  Scegliere un nome per il gruppo di ruolo.

2.  Selezionare i ruoli che si desidera assegnare al gruppo di ruolo.

3.  Aggiungere i membri al gruppo di ruolo.

4.  Salvare il gruppo di ruolo.

Una volta creato il gruppo di ruolo, è possibile gestirlo come qualsiasi altro gruppo.

Se è presente un gruppo di ruolo che dispone di alcune, ma non di tutte le autorizzazioni necessarie, è possibile copiarlo e modificarlo per creare un gruppo di ruolo. È possibile copiare un gruppo di ruolo esistente e modificarlo, senza coinvolgere il gruppo di ruolo originale. Durante la copia del gruppo di ruolo, è possibile aggiungere un nuovo nome e la descrizione, aggiungere e rimuovere ruoli dal nuovo gruppo di ruolo e aggiungere nuovi membri. Quando si crea o si copia un gruppo di ruolo, viene utilizzata la stessa finestra di dialogo visualizzata nella figura precedente.

È possibile modificare anche gruppi di ruolo esistenti. È possibile aggiungere e rimuovere ruoli da gruppi di ruoli esistenti e aggiungere e rimuovere membri contemporaneamente, utilizzando una finestra di dialogo di EAC simile a quella riportata nella figura precedente. Aggiungendo o rimuovendo ruoli da gruppi di ruolo, vengono attivate e disattivate le funzionalità amministrative dei membri del gruppo di ruolo. Per un elenco dei ruoli che è possibile aggiungere a un gruppo di ruoli, vedere [Ruoli di gestione predefiniti](built-in-management-roles-exchange-2013-help.md).


> [!NOTE]
> Sebbene sia possibile scegliere i ruoli da assegnare ai gruppi di ruolo incorporati, è consigliabile copiare i gruppi di ruolo incorporati, modificare la copia del gruppo di ruolo e aggiungere i membri alla copia del gruppo di ruolo.



Inizio pagina

## Utilizzo dei criteri di assegnazione dei ruoli

Per gestire le autorizzazioni concesse agli utenti finali per la gestione della propria cassetta postale in Exchange 2013, si consiglia di utilizzare Interfaccia di amministrazione di Exchange. Quando si utilizza EAC per la gestione delle autorizzazioni degli utenti finali, è possibile aggiungere, rimuovere i ruoli e creare criteri di assegnazione dei ruoli con poche operazioni del mouse. Interfaccia di amministrazione di Exchange offre finestre di dialogo semplici, come la finestra di dialogo **criterio di assegnazione dei ruoli**, mostrata nella figura seguente, per eseguire tali attività.

**Finestra di dialogo dei criteri di assegnazione dei ruoli in Stima al completamento**

![Finestra di dialogo dei criteri di assegnazione dei ruoli nell'interfaccia di amministrazione di Exchange](images/Dd351175.ecdf3cd4-d50e-4014-95f8-1bd5dafacaff(EXCHG.150).jpg "Finestra di dialogo dei criteri di assegnazione dei ruoli nell'interfaccia di amministrazione di Exchange")

Exchange 2013 include un criterio di assegnazione del ruolo denominato Criteri di assegnazione ruoli predefiniti. Questo criterio di assegnazione del ruolo consente agli utenti con cassette postali associate al criterio di effettuare le seguenti operazioni:

  - Unirsi ai gruppi di distribuzione che consentono ai membri di gestire la propria appartenenza o abbandonarli.

  - Visualizzare e modificare le impostazioni di base della propria cassetta postale, ad esempio le regole di Posta in arrivo, il comportamento ortografico, le impostazioni della posta indesiderata e i dispositivi Microsoft ActiveSync.

  - Modificare le informazioni di contatto, quali indirizzo e numero di telefono dell'ufficio, numero di cellulare e del cercapersone.

  - Creare, modificare o visualizzare le impostazioni dei messaggi di testo.

  - Visualizzare o modificare le impostazioni di posta vocale.

  - Visualizzare e modificare le applicazioni del marketplace.

  - Creare cassette postali di team e collegarle agli elenchi di Microsoft SharePoint.

Per aggiungere o rimuovere le autorizzazioni dal Criterio predefinito di assegnazione dei ruoli o da un qualsiasi altro criterio di assegnazione del ruolo, è possibile utilizzare EAC. La finestra di dialogo utilizzata è simile alla finestra visualizzata nella figura precedente. Quando viene visualizzato il criterio di assegnazione del ruolo in EAC, selezionare la casella di controllo accanto ai ruoli da assegnare o deselezionare la casella di controllo accanto ai ruoli da rimuovere. Le modifiche apportate al criterio di assegnazione del ruolo vengono applicate a ogni cassetta postale associata.

Per assegnare autorizzazioni dell'utente finale diverse ai vari tipi di utenti dell'organizzazione, è possibile creare criteri di assegnazione dei ruoli. Quando si crea un criterio di assegnazione del ruolo, viene visualizzata una finestra di dialogo simile alla finestra mostrata nella figura precedente. È possibile specificare un nuovo nome per il criterio di assegnazione del ruolo, quindi selezionare i ruoli da assegnare al criterio. Una volta creato un criterio di assegnazione del ruolo, è possibile associarlo alle cassette postali utilizzando EAC.

Per scegliere un criterio di assegnazione del ruolo predefinito diverso, è necessario utilizzare la Shell. Quando viene cambiato il criterio di assegnazione del ruolo predefinito, le cassette postali che vengono create saranno associate al nuovo criterio di assegnazione del ruolo predefinito, se esplicitamente specificato. Il criterio di assegnazione del ruolo associato alle cassette postali esistenti non viene modificato quando si seleziona un nuovo criterio di assegnazione del ruolo predefinito.


> [!NOTE]
> Se si seleziona la casella di controllo di un ruolo che include ruoli figlio, verranno selezionate anche le caselle di controllo dei ruoli figlio. Se si deseleziona la casella di controllo di un ruolo con ruoli figlio, verranno deselezionate anche le caselle di controllo dei ruoli figlio.<BR>Per la procedura dettagliata relativa alla creazione dei criteri di assegnazione dei ruoli o alla modifica dei criteri di assegnazione dei ruoli esistenti, vedere gli argomenti indicati di seguito: 
> <UL>
> <LI>
> <P><A href="manage-role-assignment-policies-exchange-2013-help.md">Gestire i criteri di assegnazione dei ruoli</A></P>
> <LI>
> <P><A href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Modificare il criterio di assegnazione di una cassetta postale</A></P></LI></UL>



Inizio pagina

## Documentazione sulle autorizzazioni

Nella tabella seguente sono contenuti i collegamenti agli argomenti che forniscono informazioni relative alle autorizzazioni e alla modalità di gestione in Exchange 2013.


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
<td><p><a href="understanding-role-based-access-control-exchange-2013-help.md">Controllo di accesso basato sui ruoli</a></p></td>
<td><p>Sono disponibili le informazioni su ciascun componente che costituisce RBAC e sulla modalità di creazione dei modelli di autorizzazioni avanzati se i gruppi di ruoli e i ruoli di gestione non sono sufficienti.</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-multiple-forest-permissions-exchange-2013-help.md">Informazioni sulle autorizzazioni di più foreste</a></p></td>
<td><p>Sono disponibili le informazioni sull'implementazione delle autorizzazioni di RBAC nelle organizzazioni con foreste di account e risorse.</p></td>
</tr>
<tr class="odd">
<td><p><a href="understanding-split-permissions-exchange-2013-help.md">Informazioni sulle autorizzazioni diviso</a></p></td>
<td><p>Sono disponibili le informazioni sulla suddivisione di Exchange e la gestione per le entità di sicurezza utilizzando RBAC e le autorizzazioni di suddivisione in Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-permissions-coexistence-with-exchange-2007-and-exchange-2010-exchange-2013-help.md">Informazioni sulla coesistenza delle autorizzazioni con Exchange 2007 ed Exchange 2010</a></p></td>
<td><p>Configurare le autorizzazioni per abilitare l'amministrazione di Exchange 2013 nelle organizzazioni Exchange 2007 ed Exchange 2010 esistenti.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-role-groups-exchange-2013-help.md">Gestire gruppi di ruoli</a></p></td>
<td><p>Configurare le autorizzazioni per gli amministratori di Exchange e gli utenti esperti utilizzando gruppi di ruoli.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-group-members-exchange-2013-help.md">Gestire i membri del gruppo di ruolo</a></p></td>
<td><p>Aggiungere i membri ai gruppi di ruoli. L'aggiunta e la rimozione dei membri ai gruppi di ruoli consentono di configurare gli utenti in grado di gestire le funzionalità di Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-role-groups-exchange-2013-help.md">Gestire i gruppi di ruoli collegato</a></p></td>
<td><p>Configurare le autorizzazioni per gli amministratori di Exchange e gli utenti esperti nelle distribuzioni di Exchange con più foreste.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Gestire i criteri di assegnazione dei ruoli</a></p></td>
<td><p>Configurare le funzionalità a cui gli utenti finali possono accedere dalle cassette postali utilizzando i criteri di assegnazione dei ruoli.</p></td>
</tr>
<tr class="odd">
<td><p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Modificare il criterio di assegnazione di una cassetta postale</a></p></td>
<td><p>Configurare quale criterio di assegnazione del ruolo viene applicato a una o più cassette postali.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md">Creare gruppi di ruoli collegato il mirroring di gruppi di ruoli incorporati</a></p></td>
<td><p>Ricreare i gruppi di ruoli incorporati come gruppi di ruoli collegati nelle distribuzioni di Exchange con più foreste.</p></td>
</tr>
<tr class="odd">
<td><p><a href="view-effective-permissions-exchange-2013-help.md">Visualizzare le autorizzazioni valide</a></p></td>
<td><p>Visualizzare gli utenti con le autorizzazioni per gestire le funzionalità di Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="feature-permissions-exchange-2013-help.md">Autorizzazioni funzionalità</a></p></td>
<td><p>Sono disponibili ulteriori informazioni sulle autorizzazioni necessarie per gestire i servizi e le funzionalità di Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="advanced-permissions-exchange-2013-help.md">Autorizzazioni avanzate</a></p></td>
<td><p>Utilizzare le funzionalità RBAC avanzate per creare i modelli di autorizzazioni altamente personalizzati per adattare le esigenze di qualsiasi organizzazione.</p></td>
</tr>
</tbody>
</table>


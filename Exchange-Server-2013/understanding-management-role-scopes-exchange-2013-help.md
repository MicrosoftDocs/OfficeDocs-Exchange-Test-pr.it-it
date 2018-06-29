---
title: 'Comprensione degli ambiti di gestione dei ruoli: Exchange 2013 Help'
TOCTitle: Comprensione degli ambiti di gestione dei ruoli
ms:assetid: 24ed4a38-438a-4223-9f9c-5d4dea4b046b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335146(v=EXCHG.150)
ms:contentKeyID: 50480186
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Comprensione degli ambiti di gestione dei ruoli

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-07_

Gli *ambiti dei ruoli di gestione* consentono di definire lo specifico ambito di impatto o influenza di un ruolo di gestione quando viene creata un'assegnazione dei ruoli di gestione. Quando si applica un ambito, l'assegnatario dei ruoli può modificare solo gli oggetti contenuti all'interno di quell'ambito. Un assegnatario dei ruoli può indicare un gruppo dei ruoli di gestione, un ruolo di gestione, un criterio di assegnazione dei ruoli di gestione, un utente o un gruppo di protezione universale. Per ulteriori informazioni sui ruoli di gestione, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).


> [!NOTE]
> Questo argomento è incentrato sulla funzionalità RBAC avanzata. Se si desidera gestire le autorizzazioni di base di Exchange 2013, quale l'utilizzo dell'interfaccia di amministrazione di Exchange (EAC) per aggiungere membri ai gruppi di ruoli oppure per rimuoverli da tali gruppi, per creare e modificare gruppi di ruoli oppure per creare e modificare i criteri di assegnazione dei ruoli, vedere <A href="permissions-exchange-2013-help.md">Autorizzazioni</A>.



Ogni ruolo di gestione, se si tratta di un ruolo incorporato o un ruolo personalizzato con ambiti di gestione. Ambiti di gestione possono essere una delle operazioni seguenti:

  - **Normale**   Un *ambito normale* non è esclusivo. Determina se, in Active Directory, gli oggetti possono essere visualizzati o modificati dagli utenti assegnati al ruolo di gestione. In generale, un ruolo di gestione indica gli elementi che è possibile creare o modificare, mentre l'ambito di un ruolo di gestione indica la posizione in cui è possibile eseguire le operazioni di creazione o modifica. Gli ambiti regolari possono essere impliciti o espliciti. Verranno entrambi illustrati più avanti in questo argomento.

  - **Esclusivo**   Un *ambito esclusivo* si comporta quasi come un ambito normale. L'unica differenza è che gli ambiti esclusivi consentono di negare agli utenti l'accesso agli oggetti contenuti all'interno dell'ambito, in quanto quegli utenti non sono assegnati a un ruolo associato all'ambito esclusivo. Tutti gli ambiti esclusivi sono espliciti, descritti più avanti in questo argomento.
    
    Per ulteriori informazioni sugli ambiti esclusivi, vedere [Informazioni sui ambiti esclusivi](understanding-exclusive-scopes-exchange-2013-help.md).

Gli ambiti possono essere ereditati dal ruolo di gestione, specificati come ambito relativo predefinito per un'assegnazione dei ruoli di gestione o creati utilizzando i filtri personalizzati e aggiunti a un'assegnazione dei ruoli di gestione. Gli ambiti ereditati dai ruoli di gestione vengono denominati *ambiti impliciti*, mentre quelli predefiniti e personalizzati vengono denominati *ambiti espliciti*. Nelle sezioni seguenti vengono descritti tutti i tipi di ambito:

  - Implicit Scopes

  - Explicit Scopes

  - Predefined Relative Scopes

  - Custom Scopes
    
      - Recipient Filter Scopes
    
      - Configuration Scopes

Ogni ruolo può disporre dei seguenti tipi di ambiti:

  - **Ambito di lettura del destinatario**   L'ambito implicito di lettura del destinatario determina gli oggetti destinatario che l'utente assegnato al ruolo di gestione può leggere da Active Directory.

  - **Ambito di scrittura del destinatario**   L'ambito implicito di scrittura del destinatario determina gli oggetti destinatario che l'utente assegnato al ruolo di gestione può modificare in Active Directory.

  - **Ambito di lettura della configurazione**   L'ambito implicito di lettura della configurazione determina gli oggetti configurazione che l'utente assegnato al ruolo di gestione può leggere da Active Directory.

  - **Ambito di scrittura della configurazione**    L'ambito implicito di scrittura della configurazione determina gli oggetti dell'organizzazione, dei database e dei server che l'utente assegnato al ruolo di gestione può modificare in Active Directory.

Gli oggetti destinatario includono le cassette postali, gruppi di distribuzione, gli utenti abilitato alla posta e altri oggetti. Gli oggetti configurazione includono server che eseguono Microsoft Exchange Server 2013 e che si trovano in server che eseguono Exchange. Ogni tipo di ambito può essere un ambito implicito o esplicito ambito.

## Ambiti impliciti

Gli ambiti impliciti indicano gli ambiti predefiniti che si applicano a un tipo di ruolo di gestione. Siccome gli ambiti impliciti vengono associati a un tipo di ruolo di gestione, tutti i ruoli di gestione padre e figlio con lo stesso tipo di ruolo dispongono anche degli stessi ambiti impliciti. Gli ambiti impliciti si applicano ai ruoli di gestione incorporati e a quelli personalizzati. Per ulteriori informazioni sui ruoli di gestione e sui tipi di ruolo di gestione, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

Nelle tabelle seguenti vengono elencati tutti gli ambiti impliciti definibili per i ruoli di gestione.

### Ambiti impliciti definiti per i ruoli di gestione

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Ambiti impliciti</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p>Se <code>Organization</code> è presente nell'ambito di scrittura del destinatario, il ruolo può creare o modificare gli oggetti destinatario in tutta l'organizzazione Exchange.</p>
<p>Se <code>Organization</code> è presente nell'ambito di lettura del destinatario, i ruoli possono visualizzare qualsiasi oggetto destinatario in tutta l'organizzazione Exchange.</p>
<p>Questo ambito viene utilizzato solo con gli ambiti di scrittura e lettura del destinatario.</p></td>
</tr>
<tr class="even">
<td><p><code>MyGAL</code></p></td>
<td><p>Se <code>MyGAL</code> è presente nell'ambito di scrittura del destinatario, il ruolo può visualizzare le proprietà di qualsiasi destinatario all'interno dell'elenco indirizzi globale dell'utente corrente.</p>
<p>Se <code>MyGAL</code> è presente nell'ambito di lettura del destinatario, il ruolo può visualizzare le proprietà di qualsiasi destinatario all'interno dell'elenco indirizzi globale corrente.</p>
<p>Questo ambito viene utilizzato solo con gli ambiti di lettura del destinatario.</p></td>
</tr>
<tr class="odd">
<td><p><code>Self</code></p></td>
<td><p>Se <code>Self</code> è presente nell'ambito di scrittura del destinatario, il ruolo può modificare solo le proprietà della cassetta postale dell'utente corrente.</p>
<p>Se <code>Self</code> è presente nell'ambito di lettura del destinatario, il ruolo può visualizzare solo le proprietà della cassetta postale dell'utente corrente.</p>
<p>Questo ambito viene utilizzato solo con gli ambiti di scrittura e lettura del destinatario.</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p>Se <code>MyDistributionGroups</code> è presente nell'ambito di scrittura del destinatario, il ruolo può creare o modificare gli oggetti lista di distribuzione che appartengono all'utente corrente.</p>
<p>Se <code>MyDistributionGroups</code> è presente nell'ambito di lettura del destinatario, il ruolo può visualizzare gli oggetti lista di distribuzione che appartengono all'utente corrente.</p>
<p>Questo ambito viene utilizzato solo con gli ambiti di scrittura e lettura del destinatario.</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationConfig</code></p></td>
<td><p>Se <code>OrganizationConfig</code> è presente nell'ambito di scrittura della configurazione, il ruolo può creare o modificare qualsiasi oggetto di configurazione del server o del database in tutta l'organizzazione di Exchange.</p>
<p>Se <code>OrganizationConfig</code> è presente nell'ambito di lettura della configurazione, il ruolo può visualizzare qualsiasi oggetto di configurazione del server o del database in tutta l'organizzazione di Exchange.</p>
<p>Questo ambito viene utilizzato solo con gli ambiti di scrittura e lettura della configurazione.</p></td>
</tr>
<tr class="even">
<td><p><code>None</code></p></td>
<td><p>Se <code>None</code> si trova in un ambito, quell'ambito non è disponibile per il ruolo. Ad esempio, un ruolo che presenta <code>None</code> nell'ambito di scrittura del destinatario non può modificare gli oggetti destinatario nell'organizzazione Exchange.</p></td>
</tr>
</tbody>
</table>


Se un ruolo viene associato a un assegnatario e nessun ambito predefinito o personalizzato viene specificato, gli ambiti impliciti definiti per il ruolo vengono utilizzati per controllare gli oggetti organizzazione o destinatario che l'utente può visualizzare o modificare.

L'ambito di scrittura implicito di un ruolo è sempre uguale o inferiore all'ambito di lettura implicito. Ciò significa che un ruolo non può mai modificare gli oggetti non visualizzabili dall'ambito.

Non è possibile modificare gli ambiti impliciti definiti per i ruoli di gestione. Tuttavia, è possibile sostituire l'ambito di scrittura implicito e l'ambito di configurazione per un ruolo di gestione. Quando un ambito relativo predefinito o un ambito personalizzato viene utilizzato per un'assegnazione di ruolo, l'ambito di scrittura implicito del ruolo viene sostituito, dando precedenza al nuovo ambito. L'ambito di lettura implicito di un ruolo non può essere sostituito e viene sempre applicato. Per ulteriori informazioni, vedere Predefined Relative Scopes e Custom Scopes.

Espandere la tabella seguente per visualizzare un elenco di tutti i ruoli di gestione incorporati e i relativi ambiti impliciti. Per ulteriori informazioni su ogni ruolo incorporato, vedere [Ruoli di gestione predefiniti](built-in-management-roles-exchange-2013-help.md).

## Ambiti impliciti dei ruoli di gestione incorporati


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
<th>Ruolo di gestione</th>
<th>Ambito di lettura del destinatario</th>
<th>Ambito di scrittura del destinatario</th>
<th>Ambito di lettura della configurazione</th>
<th>Ambito di scrittura della configurazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Active Directory Permissions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Address Lists</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Cmdlet Extension Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Data Loss Prevention</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Database Availability Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Database Copies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Disaster Recovery</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Distribution Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Edge Subscriptions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>E-Mail Address Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Server Certificates</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Servers</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Virtual Directories</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Federated Sharing</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Information Rights Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Legal Hold</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>LegalHoldApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Enabled Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipient Creation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Tips</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Import Export</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Search</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Message Tracking</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Migration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Monitoring</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Move Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>My Custom Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>My Marketplace Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyAddressInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDiagnostics</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDisplayName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyMobileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyPersonalInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyTeamMailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Client Access</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Organization Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Transport Settings</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>POP3 And IMAP4 Protocols</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Receive Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Recipient Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Remote and Accepted Domains</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Reset Password</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Retention Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Security Group Creation and Membership</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Send Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Support Diagnostics</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Hygiene</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Queues</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Rules</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UM Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UM Prompts</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Unified Messaging</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UnScoped Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>User Options</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>View-Only Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## Ambiti espliciti

Gli ambiti espliciti sono ambiti che controllano gli oggetti modificabili da un ruolo di gestione. Mentre gli ambiti impliciti vengono definiti per un ruolo di gestione, gli ambiti espliciti vengono definiti per un'assegnazione del ruolo di gestione. Ciò consente agli ambiti impliciti di essere applicati in modo coerente in tutti i ruoli di gestione, se non si stabilisce di utilizzare un altro ambito esplicito. Per ulteriori informazioni sulle assegnazioni del ruolo di gestione, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Gli ambiti espliciti sostituiscono gli ambiti impliciti di configurazione e di scrittura di un ruolo di gestione. Non sostituiscono l'ambito di lettura implicito di un ruolo di gestione. L'ambito di lettura implicito continua a definire gli oggetti che il ruolo di gestione può leggere.

Gli ambiti espliciti risultano utili quando l'ambito di scrittura implicito di un ruolo di gestione non soddisfa le esigenze dell'azienda. È possibile aggiungere un ambito esplicito per comprendere quasi tutto ciò che si desidera, fino a quando il nuovo ambito non supera i limiti dell'ambito di lettura implicito. I cmdlet che fanno parte di un ruolo di gestione devono essere in grado di leggere le informazioni sugli oggetti o i contenitori che comprendono gli oggetti per i cmdlet per creare o modificare gli oggetti. Ad esempio, se l'ambito di lettura implicito per un ruolo di gestione è impostato su `Self`, non è possibile aggiungere un ambito di scrittura esplicito di `Organization`, perché l'ambito di scrittura esplicito supera i limiti dell'ambito di lettura implicito.

Per ulteriori informazioni, vedere le seguenti sezioni:

  - Predefined Relative Scopes

  - Custom Scopes

## Ambiti relativi predefiniti

Exchange 2013 offre diversi relativa predefiniti scrivere gli ambiti che è possibile utilizzare per modificare l'ambito di un ruolo di gestione. Ambito predefinito relativo offrono un modo semplice da maggiormente soddisfare le esigenze dell'azienda senza dover creare manualmente gli ambiti personalizzati. Vengono chiamati ambiti relativi perché è relativa all'assegnatario di ruolo a cui è assegnato l'assegnazione di ruolo associate. Ad esempio, l'ambito relativo `Self` predefiniti limita tale ambito di scrittura solo l'utente corrente. L'ambito relativo `MyDistributionGroups` predefinito consente di limitare l'ambito di scrittura al gruppo di distribuzione che proprietario solo l'utente corrente. Ambito predefinito relativo solo utilizzabile per definire l'ambito degli oggetti destinatario. Ambito predefinito relativo non può essere utilizzato a oggetti di configurazione di ambito. Nella tabella seguente sono elencati gli ambiti relativi predefiniti che è possibile utilizzare.

### Ambiti relativi predefiniti

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Ambiti impliciti</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p>Se <code>Organization</code> è presente nell'ambito di scrittura del destinatario, il ruolo può creare o modificare gli oggetti destinatario in tutta l'organizzazione Exchange.</p>
<p>Se <code>Organization</code> è presente nell'ambito di lettura del destinatario, i ruoli possono visualizzare qualsiasi oggetto destinatario in tutta l'organizzazione Exchange.</p>
<p>Questo ambito viene utilizzato solo con gli ambiti di scrittura e lettura del destinatario.</p></td>
</tr>
<tr class="even">
<td><p><code>Self</code></p></td>
<td><p>Se <code>Self</code> è presente nell'ambito di scrittura del destinatario, il ruolo può modificare solo le proprietà della cassetta postale dell'utente corrente.</p>
<p>Se <code>Self</code> è presente nell'ambito di lettura del destinatario, il ruolo può visualizzare solo le proprietà della cassetta postale dell'utente corrente.</p>
<p>Questo ambito viene utilizzato solo con gli ambiti di scrittura e lettura del destinatario.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p>Se <code>MyDistributionGroups</code> è presente nell'ambito di scrittura del destinatario, il ruolo può creare o modificare gli oggetti lista di distribuzione che appartengono all'utente corrente.</p>
<p>Se <code>MyDistributionGroups</code> è presente nell'ambito di lettura del destinatario, il ruolo può visualizzare gli oggetti lista di distribuzione che appartengono all'utente corrente.</p>
<p>Questo ambito viene utilizzato solo con gli ambiti di scrittura e lettura del destinatario.</p></td>
</tr>
</tbody>
</table>


Gli ambiti relativi predefiniti vengono applicati quando si crea una nuova assegnazione dei ruoli di gestione. Durante la creazione dell'assegnazione di ruolo, utilizzando il cmdlet **New-ManagementRoleAssignment**, è possibile specificare un ambito relativo predefinito utilizzando il parametro *RecipientRelativeWriteScope*. Una volta creata la nuova assegnazione di ruolo, il nuovo ruolo predefinito sostituisce l'ambito di scrittura implicito del ruolo di gestione. Non è possibile specificare un ambito dei destinatari personalizzato quando si crea un'assegnazione di ruolo con un ambito relativo predefinito. Se necessario, è comunque possibile specificare un ambito di configurazione personalizzato.

Per ulteriori informazioni sull'aggiunta di un'assegnazione dei ruoli di gestione a un ambito relativo predefinito, vedere [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

## Ambiti personalizzati

Gli ambiti personalizzati necessari per l'ambito di scrittura implicita e il relativo ambito predefinito non soddisfa le esigenze dell'azienda. Gli ambiti personalizzati consentono di definire un livello di granularità, l'ambito a cui verrà applicato il ruolo di gestione. È possibile ad esempio, assegnare una specifica unità organizzativa (OU), un tipo specifico di destinatari o entrambi. In alternativa, è possibile solo consentire a un gruppo di amministratori siano in grado di gestire un set specifico di database delle cassette postali.

Come con gli ambiti relativi predefiniti, gli ambiti personalizzati sostituiscono gli ambiti impliciti di scrittura e di configurazione dell'organizzazione definiti per i ruoli di gestione. L'ambito di lettura implicito per i ruoli di gestione continua a essere applicato e l'ambito personalizzato risultante non deve superare i limiti dell'ambito di lettura implicito. È possibile creare i seguenti tre tipi di ambiti personalizzati:

  - **Ambito di unità organizzativa**   Un ambito di unità organizzativa, che indica l'ambito personalizzato più semplice, viene creato utilizzando il parametro *RecipientOrganizationalUnitScope* del cmdlet **New-ManagementRoleAssignment** . Specificando un ambito di unità organizzativa quando viene assegnato un ruolo, l'assegnatario del ruolo può modificare solo gli oggetti destinatario all'interno di tale unità organizzativa. Per ulteriori informazioni sull'aggiunta di un'assegnazione dei ruoli di gestione a un ambito di unità organizzativa, vedere [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

  - **Ambito di filtro dei destinatari**   Gli ambiti di filtro dei destinatari utilizzano i filtri per indirizzare specifici destinatari in base al tipo o ad altre proprietà dei destinatari, come il reparto, il gestore, il percorso e altro ancora. Per ulteriori informazioni, vedere la sezione Recipient Filter Scopes.

  - **Ambito di configurazione**   Gli ambiti di configurazione utilizzano filtri o gli elenchi di server di destinazione specifici basato su elenchi di server o proprietà filtrabili che possono essere definite in server, ad esempio un sito Active Directory o un ruolo del server. Gli ambiti di configurazione possono inoltre utilizzare gli ambiti dei database per specifici database basati su elenchi di database o proprietà filtrabili del database di destinazione. Per ulteriori informazioni, vedere la sezione Configurazione ambiti .

Utilizzando il cmdlet **New-ManagementScope**, è possibile creare ambiti personalizzati di configurazione e del destinatario semplici e ampi o complessi e precisi. Quando si crea un ambito di configurazione o del destinatario, vengono restituiti solo gli oggetti destinatario, server o database che corrispondono ai rispettivi ambiti. Quando questi ambiti vengono applicati a un'assegnazione di ruolo utilizzando i cmdlet **New-ManagementRoleAssignment** o **Set-ManagementRoleAssignment**, solo gli oggetti che corrispondono agli ambiti possono essere modificati dagli assegnatari del ruolo. Una volta creato un ambito personalizzato, non è possibile modificare il tipo di ambito. Un ambito per il destinatario è sempre un ambito per il destinatario e un ambito per la configurazione è sempre un ambito per la configurazione.

Per impostazione predefinita, un ambito personalizzato consente a un assegnatario di ruolo di accedere a un insieme di oggetti che soddisfano gli ambiti definite. Tuttavia, essi non escludere attivamente accesso alle altri assegnatari ruolo che non sono inoltre assegnato l'ambito stesso o equivalente. Qualsiasi ambito personalizzato può accedere agli oggetti stessi se degli elenchi o filtri in tali ambiti soddisfano gli stessi oggetti. Potrebbero verificarsi gli oggetti di cui non si desidera questo comportamento, ad esempio come nel caso dei dirigenti. Per questi oggetti, è possibile definire ambiti esclusivi. Ambiti esclusivi utilizzare filtri o gli elenchi allo stesso modo degli ambiti normali ma a differenza di ambiti normali, negare l'accesso agli oggetti inclusi nell'ambito di tutti gli utenti che non fanno parte dell'ambito esclusivo uguale o equivalente. Per ulteriori informazioni sugli ambiti esclusivi, vedere [Informazioni sui ambiti esclusivi](understanding-exclusive-scopes-exchange-2013-help.md).

## Ambiti di filtro destinatario

Gli ambiti di filtro dei destinatari consentono di controllare gli oggetti destinatario gestibili dagli assegnatari del ruolo valutando una o più proprietà di un oggetto destinatario rispetto al valore specificato in un'istruzione per il filtro. I destinatari compresi negli ambiti dei destinatari sono le cassette postali, gli utenti abilitati alla posta, i gruppi di distribuzione e i contatti di posta. Solo i destinatari corrispondenti al filtro specificato possono essere gestiti dagli assegnatari del ruolo. Un esempio di istruzione per il filtro è `{ Name -Eq "David" }` dove**Name** è la proprietà dell'oggetto destinatario valutato e **David** è il valore che si desidera valutare rispetto alla proprietà. L'operatore di confronto **-Eq** indica che il valore archiviato nella proprietà deve essere pari al valore specificato per il filtro affinché sia true. Se il filtro è true, il destinatario è compreso nell'ambito.

Gli ambiti di filtro dei destinatari vengono creati specificando il filtro destinatario da utilizzare con il parametro *RecipientRestrictionFilter* nel cmdlet **New-ManagementScope**. Per impostazione predefinita, il cmdlet **New-ManagementScope** crea ambiti normali. Se si desidera creare un ambito esclusivo, includere l'opzione *Exclusive* al parametro *RecipientRestrictionFilter*.

Quando si crea un filtro di restrizione dei destinatari, Exchange valuta per impostazione predefinita il filtro fornito rispetto a ogni oggetto destinatario dell'organizzazione. Se si desidera limitare i destinatari valutati dall'ambito, è possibile utilizzare il parametro *RecipientRoot* insieme al parametro *RecipientRestrictionFilter*. Il parametro *RecipientRoot* accetta un'unità organizzativa. Quando si utilizza il parametro *RecipientRoot*, Exchange valuta solo i destinatari compresi nell'unità organizzativa specificata rispetto al filtro fornito.

Quando si aggiunge un ambito di filtro dei destinatari a un'assegnazione di ruolo, specificare il nome dell'ambito dei destinatari nel parametro *CustomRecipientWriteScope* di **New-ManagementRoleAssignment**, se si sta creando una nuova assegnazione di ruolo, oppure il cmdlet **Set-ManagementRoleAssignment** se si sta aggiornando un'assegnazione di ruolo esistente. Ogni assegnazione di ruolo può disporre di un unico ambito dei destinatari, compresi gli ambiti relativi predefiniti. È possibile aggiungere un unico ambito di configurazione alla stessa assegnazione di ruolo a cui è stato aggiunto un ambito dei destinatari.

Per ulteriori informazioni sulla sintassi dei filtri e per un elenco completo delle proprietà filtrabili dei destinatari, vedere [Informazioni sui filtri di ambito di gestione dei ruoli](understanding-management-role-scope-filters-exchange-2013-help.md).

## Ambiti di configurazione

Di seguito sono due tipi di ambiti configurazione offerti in Exchange 2013:

  - **Ambiti di server**   Esistono due tipi di ambiti di server, server filtro ambiti e gli ambiti di elenco di server. Configurazione di server, compresi connettori di ricezione, code di trasporto, certificati del server, le directory virtuali e così via, può essere gestiti se un oggetto server è incluso in un ambito server.
    
      - **Ambiti di filtro dei server**   Gli ambiti di filtro dei server consentono di controllare gli oggetti server gestibili dagli assegnatari del ruolo valutando una o più proprietà di un oggetto server rispetto al valore specificato in un'istruzione per il filtro. Per creare un ambito di filtro dei server, utilizzare il parametro *ServerRestrictionFilter* nel cmdlet **New-ManagementScope**.
    
      - **Ambiti di elenco dei server**   Gli ambiti di elenco dei server consentono di controllare gli oggetti server gestibili dagli assegnatari del ruolo definendo un elenco di server accessibili da un assegnatario del ruolo. Per creare un ambito di elenco dei server, utilizzare il parametro *ServerList* nel cmdlet **New-ManagementScope**.

  - **Ambiti dei database**   Esistono due tipi di ambiti di database, gli ambiti filtro dei database e gli ambiti elenco database. Configurazione del database che può essere gestite se un oggetto di database è incluso in un ambito di database includono i limiti di quota del database, manutenzione del database, la replica delle cartelle pubbliche, se viene installato un database, e così via. Oltre alla configurazione del database, gli ambiti dei database anche utilizzabile per stabilire quali destinatari database possono essere creati in. Se sono presenti server di pre-Exchange 2010 SP1 all'interno dell'organizzazione, vedere la sezione ambiti del Database e le versioni precedenti di Exchange più avanti in questo argomento.
    
      - **Ambiti di filtro dei database**   Gli ambiti di filtro dei database consentono di controllare gli oggetti database gestibili dagli assegnatari del ruolo valutando una o più proprietà di un oggetto database rispetto al valore specificato in un'istruzione per il filtro. Per creare un ambito di filtro dei database, utilizzare il parametro *DatabaseRestrictionFilter* nel cmdlet **New-ManagementScope**.
    
      - **Ambiti di elenco dei database**   Gli ambiti di elenco dei database consentono di controllare gli oggetti database gestibili dagli assegnatari del ruolo definendo un elenco di database accessibili da un assegnatario del ruolo. Per creare un ambito di elenco dei database, utilizzare il parametro *DatabaseList* nel cmdlet **New-ManagementScope**.

Per ulteriori informazioni sulla sintassi dei filtri e per un elenco completo delle proprietà filtrabili dei server e dei database, vedere [Informazioni sui filtri di ambito di gestione dei ruoli](understanding-management-role-scope-filters-exchange-2013-help.md).

Gli elenchi dei server e dei database possono essere definiti specificando ogni server e ogni database che si desidera includere nei rispettivi ambiti. Nei rispettivi ambiti possono essere specificati più server o database, separando i nomi con una virgola.

Quando si aggiunge un ambito di configurazione dei server o dei database a un'assegnazione di ruolo, specificare il nome dell'ambito nel parametro *CustomConfigWriteScope* del cmdlet **New-ManagementRoleAssignment**, se si sta creando una nuova assegnazione di ruolo, oppure il cmdlet **Set-ManagementRoleAssignment** se si sta aggiornando un'assegnazione di ruolo esistente. Ogni assegnazione di ruolo può disporre di un unico ambito di configurazione.

Oltre al controllo dei database gestibili dagli assegnatari del ruolo, gli ambiti dei database consentono anche di controllare i database in cui gli assegnatari del ruolo possono creare le cassette postali. Si tratta di un'operazione diversa dal controllo dei destinatari gestibili da un assegnatario del ruolo. Se un assegnatario del ruolo dispone delle autorizzazioni per creare una nuova cassetta postale, abilitare alla posta un utente esistente o spostare le cassette postali, è possibile definire ulteriormente le autorizzazioni utilizzando gli ambiti dei database per controllare il database in cui viene creata la cassetta postale o in quale database viene spostata una cassetta postale. Il controllo dei destinatari gestibili da un assegnatario del ruolo viene eseguito utilizzando l'ambito dei destinatari specificato nel parametro *CustomRecipientWriteScope* del cmdlet **New-ManagementRoleAssignment** o **Set-ManagementRoleAssignment**. Il controllo dei database in cui può essere creata o spostata una cassetta postale viene eseguito utilizzando l'ambito dei database specificato nel parametro *CustomConfigurationWriteScope* degli stessi cmdlet.


> [!NOTE]
> Distribuzione automatica delle cassette postali può essere controllata tramite gli ambiti dei database.



Exchange caratteristiche potrebbero richiedere gli ambiti di server, gli ambiti dei database o entrambi, da gestire. Se una funzionalità richiede che sia il server che gli ambiti dei database da gestire, due le assegnazioni di ruolo devono essere create e assegnate all'assegnatario di ruolo che deve avere accesso a gestire la funzionalità. Un'assegnazione di ruolo deve essere associata all'ambito del server e un'assegnazione di ruolo deve essere associata all'ambito di database.

Alcuni cmdlet può utilizzare gli ambiti di configurazione non immediatamente evidenti. La tabella seguente contiene un elenco dei cmdlet e degli ambiti di configurazione utilizzabile per controllarne l'applicazione. Per i cmdlet compresi nell'area funzionale dei destinatari, gli ambiti di configurazione consentono di controllare in quali database possono essere creati i destinatari. Non controllano quali destinatari possono essere gestiti. La colonna **Ambiti necessari** può contenere i seguenti elementi:

  - **Database**   Per eseguire il cmdlet, all'assegnatario del ruolo deve essere associata un'assegnazione di ruolo con l'ambito dei database che comprende il database da gestire oppure l'ambito implicito di scrittura della configurazione del ruolo deve comprendere il database da gestire.

  - **Server**   Per eseguire il cmdlet, all'assegnatario del ruolo deve essere associata un'assegnazione di ruolo con l'ambito dei server che comprende il server da gestire oppure l'ambito implicito di scrittura della configurazione del ruolo deve comprendere il server da gestire.

  - **Server o database**   Per eseguire il cmdlet, all'assegnatario del ruolo deve essere associata un'assegnazione di ruolo in cui l'ambito dei database comprende il database gestito oppure in cui l'ambito dei server comprende il server in cui si trova il database. Oppure, l'ambito implicito di scrittura della configurazione del ruolo deve contenere il database da gestire o contenere il server in cui si trova il database e l'assegnazione di ruolo non può disporre di un ambito di scrittura personalizzato.

  - **Server e database**   Per eseguire questo cmdlet, all'assegnatario del ruolo devono essere associate due assegnazioni di ruolo. La prima assegnazione di ruolo deve comprendere l'ambito dei database che comprende il database da gestire. La seconda assegnazione di ruolo deve comprendere l'ambito dei server che comprende il server da gestire. Le assegnazioni di ruolo possono disporre di ambiti di configurazione personalizzati definiti o possono ereditare l'ambito implicito di scrittura della configurazione dal ruolo. Per ereditare l'ambito implicito di scrittura dal ruolo, l'assegnazione di ruolo non può disporre di un ambito di scrittura personalizzato.

### Aree funzionali e ambiti di server e database applicabili

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Area funzionale</th>
<th>Cmdlet</th>
<th>Ambiti necessari</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Database</p></td>
<td><p><strong>Dismount-Database</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>Database</p></td>
<td><p><strong>Mount-Database</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="odd">
<td><p>Database</p></td>
<td><p><strong>Move-DatabasePath</strong></p></td>
<td><p>Server e database</p></td>
</tr>
<tr class="even">
<td><p>Database</p></td>
<td><p><strong>Remove-MailboxDatabase</strong></p></td>
<td><p>Server o database</p></td>
</tr>
<tr class="odd">
<td><p>Database</p></td>
<td><p><strong>Set-MailboxDatabase</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>Disponibilità elevata</p></td>
<td><p><strong>Add-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>Server</p></td>
</tr>
<tr class="odd">
<td><p>Disponibilità elevata</p></td>
<td><p><strong>Add-MailboxDatabaseCopy</strong></p></td>
<td><p>Server</p></td>
</tr>
<tr class="even">
<td><p>Disponibilità elevata</p></td>
<td><p><strong>Move-ActiveMailboxDatabase</strong></p></td>
<td><p>Server</p></td>
</tr>
<tr class="odd">
<td><p>Disponibilità elevata</p></td>
<td><p><strong>Remove-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>Server</p></td>
</tr>
<tr class="even">
<td><p>Disponibilità elevata</p></td>
<td><p><strong>Remove-MailboxDatabaseCopy</strong></p></td>
<td><p>Server o database</p></td>
</tr>
<tr class="odd">
<td><p>Disponibilità elevata</p></td>
<td><p><strong>Resume-MailboxDatabaseCopy</strong></p></td>
<td><p>Server o database</p></td>
</tr>
<tr class="even">
<td><p>Disponibilità elevata</p></td>
<td><p><strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>Server o database</p></td>
</tr>
<tr class="odd">
<td><p>Disponibilità elevata</p></td>
<td><p><strong>Suspend-MailboxDatabaseCopy</strong></p></td>
<td><p>Server o database</p></td>
</tr>
<tr class="even">
<td><p>Disponibilità elevata</p></td>
<td><p><strong>Update-MailboxDatabaseCopy</strong></p></td>
<td><p>Server o database</p></td>
</tr>
<tr class="odd">
<td><p>Destinatari</p></td>
<td><p><strong>Connect-Mailbox</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>Destinatari</p></td>
<td><p><strong>Enable-Mailbox</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="odd">
<td><p>Destinatari</p></td>
<td><p><strong>New-Mailbox</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>Destinatari</p></td>
<td><p><strong>New-MoveRequest</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="odd">
<td><p>Risoluzione dei problemi</p></td>
<td><p><strong>Test-MapiConnectivity</strong></p></td>
<td><p>Database</p></td>
</tr>
</tbody>
</table>


## Gli ambiti dei database e le versioni precedenti di Exchange

Gli ambiti dei database prima introdotti in Microsoft Exchange 2010 Service Pack 1 (SP1) e continuano a essere supportato in Exchange 2013. Versioni di Exchange prima Exchange 2010 SP1 supportano solo gli ambiti dei destinatari e gli ambiti di configurazione di server. Quando si crea un nuovo ambito di database in un Exchange 2010 SP1 o versione successiva, si riceverà il messaggio di avviso seguente:

    WARNING: Database management scopes will only be applied when a user connects to a server running Exchange 2010 SP1 or later. Servers running a version of Exchange prior to Exchange 2010 SP1 won't apply any roles from a role assignment linked to a database scope. Database management scopes also won't be visible to the Get-ManagementScope cmdlet when it's run from a pre-Exchange 2010 SP1 server.

Quando si crea un ambito di database, viene applicata solo agli utenti che si connettono al server che eseguono Exchange 2010 SP1 o versione successiva. Gli utenti che si connettono al server di pre-Exchange 2010 SP1 non dispongono di tutte le assegnazioni di ruolo associate applicati a tali ambiti di database. Ciò significa che le autorizzazioni fornite da queste assegnazioni di ruolo non vengono concesse agli utenti quando si connettono al server di pre-Exchange 2010 SP1. Impossibile creare, rimuovere, modificare o visualizzati dai server di pre-Exchange 2010 SP1 gli ambiti dei database.

Un ambito di database può includere tutti i database nella propria organizzazione Exchange. Includono server Exchange Server 2007, Exchange 2010 e Exchange 2013. In questo modo è possibile controllare quali database, indipendentemente dalla versione Exchange, che gli utenti possono gestire. Come con altri ambiti del database, le assegnazioni di ruolo associate agli ambiti dei database che contengono database Exchange 2007 e Exchange 2010 vengono applicate solo agli utenti quando si connettono a un Exchange 2010 SP1 o versione successiva.

Gli utenti che si connettono a una pre-Exchange 2010 server SP1 possono visualizzare e modificare le assegnazioni di ruolo associate agli ambiti dei database. Include la modifica dell'ambito di configurazione per un'assegnazione di ruolo esistente a un ambito server se è attualmente associato a un ambito di database. Tuttavia, se l'ambito della configurazione in un'assegnazione di ruolo viene modificato in un ambito di server e successivamente si desidera ripristinare un ambito di database o se l'utente desidera modificare l'ambito della configurazione a un altro ambito di database, l'utente necessario apportare le modifiche durante la connessione a un Exchange 2010 SP1 o versione successiva. Gli utenti possono specificare solo gli ambiti di server quando si modifica l'ambito della configurazione in un'assegnazione di ruolo se sono connessi a una pre-Exchange 2010 server SP1.


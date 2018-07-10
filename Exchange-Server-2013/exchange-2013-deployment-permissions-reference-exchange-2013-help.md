---
title: 'Riferimenti per le autorizzazioni di distribuzione di Exchange 2013: Exchange 2013 Help'
TOCTitle: Riferimenti per le autorizzazioni di distribuzione di Exchange 2013
ms:assetid: b13412d0-0cc4-4c1d-bf31-cae3d3e211a9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee681663(v=EXCHG.150)
ms:contentKeyID: 59634753
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Riferimenti per le autorizzazioni di distribuzione di Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In questo argomento vengono descritte le autorizzazioni necessarie per configurare un'organizzazione di Microsoft Exchange Server 2013. I gruppi di protezione universali (USG) associati ai gruppi del ruolo di gestione e altre entità di sicurezza e gruppi di protezione di Windows vengono aggiunti agli elenchi di controllo degli accessi (ACL) di diversi oggetti Active Directory. Gli ACL controllano le operazioni che possono essere eseguite su ciascun oggetto. Venendo a conoscenza delle autorizzazioni concesse a ogni gruppo di ruoli, gruppo di protezione o entità di sicurezza, è possibile determinare le autorizzazioni minime necessarie per installare Exchange 2013.

In alcuni casi, l'elenco di controllo degli accessi non viene applicato alla proprietà standard, **ntSecurityDescriptor**, ma a un'altra proprietà, ad esempio **msExchMailboxSecurityDescriptor**. Il servizio directory non è in grado di applicare una protezione non specificata nel descrittore di protezione di Windows. Nella maggior parte dei casi, gli elenchi di controllo degli accessi vengono replicati per essere archiviati in oggetti appropriati dal servizio Archivio informazioni. Sfortunatamente, non esiste alcuno strumento per visualizzare gli elenchi di controllo degli accessi in modo diverso da dati binari non elaborati.

Le colonne di ciascuna tabella delle autorizzazioni includono le seguenti informazioni:

  - **Account**   L'entità di sicurezza a cui sono concesse o negate le autorizzazioni.

  - **Tipo ACE**   Tipo di voce di controllo di accesso (ACE)
    
      - **ACE consentita**   Consente all'utente o al gruppo associato all'ACE di accedere a un elemento.
    
      - **ACE negata**   Impedisce all'utente o al gruppo associato all'ACE di accedere a un elemento.

  - **Ereditarietà**   Tipo di ereditarietà utilizzata per oggetti figlio.
    
      - **Tutte** indica che le autorizzazioni si applicano all'oggetto e ai sottoggetti.
    
      - **Desc** indica le autorizzazioni che si applicano alla classe di oggetti elencata nella riga Sulla proprietà/Si applica a.
    
      - **Nessuna** indica le autorizzazioni da applicare all'oggetto.

  - **Autorizzazioni**   Le autorizzazioni concesse all'account.

  - **Sulla proprietà/Si applica a**   In alcuni casi, le autorizzazioni si applicano solo a una proprietà specificata, a un insieme di proprietà o a una classe di oggetti. Queste autorizzazioni limitate sono specificate di seguito.

  - **Commenti**   Nei casi in cui è possibile, questa colonna spiega perché le autorizzazioni sono necessarie oppure fornisce altre informazioni sulle autorizzazioni.

Le autorizzazioni in genere vengono elencate nella tabella in base ai nomi utilizzati nella scheda **Visualizza/Modifica** della finestra **Avanzate** della pagina delle proprietà **Sicurezza** di Active Directory Service Interfaces (ADSI) Edit (AdsiEdit.msc). La pagina delle proprietà di ADSI Edit **Sicurezza** riporta una visualizzazione molto più ridotta delle autorizzazioni. Lo strumento LDP (Ldp.exe) visualizza la maschera di accesso direttamente come valore numerico. Il codice di installazione si riferisce alle autorizzazioni mediante costanti predefinite.

La seguente tabella mostra il rapporto tra tali valori.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Pagina di riepilogo di ADSI Edit</th>
<th>Finestra Avanzate di ADSI Edit, scheda Visualizza/Modifica</th>
<th>Voci di elenco di controllo di accesso applicate a un oggetto specificato</th>
<th>Valore binario (maschera di accesso in LDP)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>controllo completo</p></td>
<td><p>controllo completo</p></td>
<td><p><code>WRITE_OWNER | WRITE_DAC | READ_CONTROL | DELETE | ACTRL_DS_CONTROL_ACCESS | ACTRL_DS_LIST_OBJECT | ACTRL_DS_DELETE_TREE | ACTRL_DS_WRITE_PROP | ACTRL_DS_READ_PROP | ACTRL_DS_SELF | ACTRL_DS_LIST | ACTRL_DS_DELETE_CHILD | ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x000F01FF</code></p></td>
</tr>
<tr class="even">
<td><p>Lettura</p></td>
<td><p>Visualizzazione contenuto + Lettura di tutte le proprietà + Autorizzazioni di lettura</p></td>
<td><p><code>ACTRL_DS_LIST | ACTRL_DS_READ_PROP | READ_CONTROL</code></p></td>
<td><p><code>0x00020014</code></p></td>
</tr>
<tr class="odd">
<td><p>Scrittura</p></td>
<td><p>Scrivi tutte le proprietà + Tutte le scritture convalidate</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP | ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000028</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Visualizzazione contenuto</p></td>
<td><p><code>ACTRL_DS_LIST</code></p></td>
<td><p><code>0x00000004</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Lettura di tutte le proprietà</p></td>
<td><p><code>ACTRL_DS_READ_PROP</code></p></td>
<td><p><code>0x00000010</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Scrivi tutte le proprietà</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP</code></p></td>
<td><p><code>0x00000020</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Elimina</p></td>
<td><p><code>DELETE</code></p></td>
<td><p><code>0x00010000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Elimina sottoalbero</p></td>
<td><p><code>ACTRL_DS_DELETE_TREE</code></p></td>
<td><p><code>0x00000040</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Autorizzazioni di lettura</p></td>
<td><p><code>READ_CONTROL</code></p></td>
<td><p><code>0x00020000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Autorizzazioni di modifica</p></td>
<td><p><code>WRITE_DAC</code></p></td>
<td><p><code>0x00040000</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Modifica proprietario</p></td>
<td><p><code>WRITE_OWNER</code></p></td>
<td><p><code>0x00080000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Tutte le scritture convalidate</p></td>
<td><p><code>ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000008</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Tutti i diritti estesi</p></td>
<td><p><code>ACTRL_DS_CONTROL_ACCESS</code></p></td>
<td><p><code>0x00000100</code></p></td>
</tr>
<tr class="even">
<td><p>Crea tutti gli oggetti figlio</p></td>
<td><p>Crea tutti gli oggetti figlio</p></td>
<td><p><code>ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x00000001</code></p></td>
</tr>
<tr class="odd">
<td><p>Elimina tutti gli oggetti figlio</p></td>
<td><p>Elimina tutti gli oggetti figlio</p></td>
<td><p><code>ACTRL_DS_DELETE_CHILD</code></p></td>
<td><p><code>0x00000002</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
<td><p><code>ACTRL_DS_LIST_OBJECT</code></p></td>
<td><p><code>0x00000080</code></p></td>
</tr>
</tbody>
</table>


I diritti estesi sono diritti personalizzati specificati da singole applicazioni, nell'elenco di controllo degli accessi. Tuttavia, non sono utilizzati in Active Directory. L'applicazione specifica applica qualsiasi diritto esteso. Esempi di diritti estesi di Exchange sono "Crea cartella pubblica" o "Crea proprietà con nome nell'archivio informazioni".

Per informazioni sulle autorizzazioni impostate durante un'installazione di Exchange Server 2010 Microsoft, vedere [Riferimento le autorizzazioni di distribuzione di Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=402924).

## Preparazione delle autorizzazioni di Active Directory

Nelle tabelle delle autorizzazioni di questa sezione vengono riportate le autorizzazioni impostate quando si esegue il comando `Setup /PrepareAD`.


> [!NOTE]
> Le autorizzazioni descritte in questa sezione sono le autorizzazioni predefinite che sono configurate quando si esegue la distribuzione di Exchange 2013 tramite il modello di autorizzazioni di condivisione. In caso di distribuzione di Exchange 2013 tramite il modello di divisione delle autorizzazioni di Active Directory, le autorizzazioni predefinite sono diverse. Per ulteriori informazioni sulle modifiche delle autorizzazioni predefinite utilizzando le autorizzazioni condivise di Active Directory e i modelli di autorizzazioni di divisione e condivisione in generale, vedere <A href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</A> in <A href="understanding-split-permissions-exchange-2013-help.md">Informazioni sulle autorizzazioni diviso</A>. Se si preferisce non utilizzare le autorizzazioni di divisione di Active Directory durante l'installazione di Exchange, Exchange utilizzerà le autorizzazioni condivise.



## Autorizzazioni del contenitore di Microsoft Exchange

Nella seguente tabella vengono riportate le autorizzazioni impostate nel contenitore di Microsoft Exchange nella partizione di configurazione.

### Nome distinto dell'oggetto: CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<domain\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Account di installazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p></p></td>
<td><p>Si tratta dell'account utilizzato per eseguire <code>/PrepareAD</code>.</p></td>
</tr>
<tr class="even">
<td><p>Gestione dell'organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Nessuna</p></td>
<td><p>Proprietà di lettura</p>
<p>Contenuto elenco</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazioni di modifica</p></td>
<td><p>msExchSmtpRceiveConnector</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Configurazione delegata</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni del contenitore di individuazione automatica di Microsoft Exchange

Nella seguente tabella vengono riportate le autorizzazioni impostate nel contenitore di individuazione automatica di Microsoft Exchange nella partizione di configurazione.

### Nome distinto dell'oggetto: CN=Microsoft Exchange Autodiscover,CN=Services,CN=Configuration,DC=\<domain\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni del contenitore dell'organizzazione di Microsoft Exchange

Nelle tabelle delle autorizzazioni di questa sezione vengono riportate le autorizzazioni impostate nell'organizzazione di Microsoft Exchange e nei sottocontenitori all'interno della partizione di configurazione.

### Nome distinto dell'oggetto: CN=\<organization\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<domain\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Enterprise Admins</p>
<p>Gruppo radice Domain Admins</p>
<p>Account di installazione</p>
<p>Gestione organizzazione</p></td>
<td><p>ACE negata</p></td>
<td><p>Tutte</p></td>
<td><p>Invia come</p>
<p>Ricevi come</p></td>
<td><p></p></td>
<td><p>Gli amministratori di Windows non possono aprire le cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>Enterprise Admins</p>
<p>Schema Admins</p>
<p>Gruppo radice Domain Admins</p>
<p>Account di installazione</p>
<p>Gestione organizzazione</p></td>
<td><p>ACE negata</p></td>
<td><p>Tutte</p></td>
<td><p>Rappresentazione dei Servizi Web Exchange</p>
<p>Serializzazione dei token dei Servizi Web Exchange</p></td>
<td><p></p></td>
<td><p>Diritto esteso</p></td>
</tr>
<tr class="odd">
<td><p>Enterprise Admins</p>
<p>Schema Admins</p>
<p>Gruppo radice Domain Admins</p>
<p>Account di installazione</p></td>
<td><p>ACE negata</p></td>
<td><p>Tutte</p></td>
<td><p>Accesso al trasporto dell'archivio</p>
<p>Delega vincolata dell'archivio</p>
<p>Accesso in lettura all'archivio</p>
<p>Accesso in lettura e scrittura all'archivio</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sistema locale</p></td>
<td><p>Consenti</p></td>
<td><p>Tutte</p></td>
<td><p>Tutti i diritti estesi</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE negata</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpace</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utenti autenticati</p></td>
<td><p>Consenti</p></td>
<td><p>Nessuna</p></td>
<td><p>Lettura</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>NT Authority\servizio di rete</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Server disponibilità gestita</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Tutti i diritti estesi</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchOwningServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchDatabaseCreated</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUserCulture</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>siteFolderGUID</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>siteFolderServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchEDBOffline</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchPatchMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>publicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea cartella pubblica principale</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea cartella pubblica principale</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Visualizza stato dell'Archivio informazioni</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Visualizza stato dell'Archivio informazioni</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Amministra l'Archivio informazioni</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Amministra l'Archivio informazioni</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea proprietà con nome nell'Archivio informazioni</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea proprietà con nome nell'Archivio informazioni</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Modifica l'elenco di controllo degli accessi delle cartelle pubbliche</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Modifica l'elenco di controllo degli accessi delle cartelle pubbliche</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Modifica le quote delle cartelle pubbliche</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Modifica le quote delle cartelle pubbliche</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Modifica l'elenco di controllo di accesso amministrativo delle cartelle pubbliche</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Modifica l'elenco di controllo di accesso amministrativo delle cartelle pubbliche</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Modifica la scadenza delle cartelle pubbliche</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Modifica la scadenza delle cartelle pubbliche</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Modifica l'elenco delle repliche della cartella pubblica</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Modifica l'elenco delle repliche della cartella pubblica</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Modifica il mantenimento degli elementi eliminati di una cartella pubblica</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Modifica il mantenimento degli elementi eliminati di una cartella pubblica</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea cartella pubblica</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea cartella pubblica</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Cartella pubblica abilitata all'utilizzo della posta</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Tutti</p>
<p>NT Authority\accesso anonimo</p>
<p></p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea proprietà con nome nell'Archivio informazioni</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Tutti</p>
<p>NT Authority\accesso anonimo</p>
<p></p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea cartella pubblica</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Tutti</p>
<p>NT Authority\accesso anonimo</p>
<p></p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p><code>/ msExchPrivateMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Tutti</p>
<p>NT Authority\accesso anonimo</p>
<p></p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p><code>/ siteAddressing</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=All Address Lists,CN=Address Lists Container,CN=\<organization\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Contenuto elenco</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Offline Address Lists,CN=Address Lists Container, CN=\<organization\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Download della Rubrica offline</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Addressing,CN=\<organization\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Recipient Policies,CN=\<organization\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni del contenitore nella partizione di configurazione

Nelle tabelle delle autorizzazioni di questa sezione vengono riportate le autorizzazioni impostate dal comando `Setup /PrepareAD` in diversi contenitori all'interno della partizione di configurazione.

### Nome distinto dell'oggetto: CN=Sites,CN=Configuration,DC=\<domain\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchVersion / site</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchVersion / site-link</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchPartnerId / site</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchMinorPartnerId / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchResponsibleforSites / site</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p></p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchTransportSiteFlags / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchCost / site-link</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p>
<p>Sistema locale</p>
<p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p><code>/ msExchEdgeSyncEHFConnector</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p>
<p>Sistema locale</p>
<p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p><code>/ msExchEdgeSyncMservConnector</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Figli</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p>
<p>Elimina albero</p></td>
<td><p><code>msExchEdgeSyncServiceConfig / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p>
<p>Sistema locale</p>
<p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p><code>/ msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Figli</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p>
<p>Elimina albero</p></td>
<td><p><code>msExchEdgeSyncMservConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Figli</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p>
<p>Elimina albero</p></td>
<td><p><code>msExchEdgeSyncEHFConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Deleted Objects,CN=Configuration,DC=\<domain\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Contenuto elenco</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Amministrazione dell'organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Account di installazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazione di lettura</p>
<p>Autorizzazione di scrittura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p>Si tratta dell'account utilizzato per eseguire <code>/PrepareAD</code>.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servizio di rete</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Contenuto elenco</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni del gruppo amministrativo di Exchange

Il comando `Setup /PrepareAD` configura anche le seguenti autorizzazioni nei gruppi amministrativi all'interno dell'organizzazione.

### Nome distinto dell'oggetto: CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Accesso al Servizio aggiornamento destinatari</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Consente agli amministratori destinatari di Exchange di apporre ai destinatari un indicatore con informazioni sull'indirizzo proxy.</p></td>
</tr>
<tr class="even">
<td><p>Sistema locale</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Accesso al Servizio aggiornamento destinatari</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Consente ai server di apporre ai destinatari un indicatore con informazioni sull'indirizzo proxy.</p></td>
</tr>
<tr class="odd">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Accesso al Servizio aggiornamento destinatari</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Consente agli amministratori delle cartelle pubbliche di Exchange di apporre ai destinatari un indicatore con informazioni sull'indirizzo proxy.</p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Advanced Security Settings,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Nessuna</p></td>
<td><p>Contenuto elenco</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Encryption,CN=Advanced Security Settings,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Nessuna</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Arrays,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Nessuna</p></td>
<td><p>Contenuto elenco</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Database Availability Groups,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Nessuna</p></td>
<td><p>Contenuto elenco</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Databases,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Nessuna</p></td>
<td><p>Contenuto elenco</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Servers,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE negata</p></td>
<td><p>Tutte</p></td>
<td><p>Ricevi come</p></td>
<td><p></p></td>
<td><p>I server di Exchange non possono aprire le cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Nessuna</p></td>
<td><p>Contenuto elenco</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni del contenitore dei gruppi di protezione di Microsoft Exchange

Nelle tabelle delle autorizzazioni di questa sezione vengono riportate le autorizzazioni impostate nel contenitore dei gruppi di protezione di Microsoft Exchange nella partizione del dominio radice.

### Nome distinto dell'oggetto: OU=Microsoft Exchange Security Groups,DC=\<root domain\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p></td>
<td><p><code>/ Group</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Elimina</p></td>
<td><p><code>/ group</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Member / group</code></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Organization Management,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Public Folder Management,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=ExchangeLegacyInterop,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Exchange Servers,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Amministratori del dominio radice</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura membri</p>
<p>Scrittura membri</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Amministratori del dominio figlio</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura membri</p>
<p>Scrittura membri</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Preparazione di un dominio

Nella seguente tabella vengono riportate le autorizzazioni impostate quando si esegue il comando `Setup /PrepareDomain`.


> [!NOTE]
> Le autorizzazioni descritte in questa sezione sono le autorizzazioni predefinite che vengono configurate quando si esegue la distribuzione di Exchange 2013 tramite il modello di autorizzazioni condivise. Se è stata effettuata la distribuzione di Exchange 2013 utilizzando il modello di autorizzazioni condivise di Active Directory, le autorizzazioni predefinite sono diverse. Per ulteriori informazioni sulle modifiche alle autorizzazioni predefinite quando si utilizzano modelli Active Directory di suddivisione delle autorizzazioni e di condivisione e divisione di autorizzazioni in generale, vedere <A href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</A> in <A href="understanding-split-permissions-exchange-2013-help.md">Informazioni sulle autorizzazioni diviso</A>. Se si preferisce non utilizzare le autorizzazioni suddivise di Active Directory durante l'installazione di Exchange, Exchange utilizzerà le autorizzazioni di condivisione.



### Nome distinto dell'oggetto: DC=\<domain\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>Concede le autorizzazioni di lettura per il servizio di trasporto.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Sincronizzazione replica</p></td>
<td><p></p></td>
<td><p>Diritto esteso</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p>
<p>Elenco elementi figlio</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p>
<p>Elenco elementi figlio</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>WriteDACL</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>WriteDACL</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Elimina albero</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Elimina albero</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina</p></td>
<td><p><code>/ contact</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina</p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina</p></td>
<td><p><code>/ organizationUnit</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina</p></td>
<td><p><code>/ group</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p></td>
<td><p><code>/ computer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Reimposta password al successivo accesso</p></td>
<td><p></p></td>
<td><p>Diritto esteso</p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Cambia password</p></td>
<td><p><code> / user</code></p></td>
<td><p>Diritto esteso</p></td>
</tr>
<tr class="odd">
<td><p>Installazione delegata</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=AdminSDHolder,CN=System,DC=\<domain\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>Concede le autorizzazioni di lettura per il servizio di trasporto.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Sincronizzazione replica</p></td>
<td><p></p></td>
<td><p>Diritto esteso</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p>
<p>Elenco elementi figlio</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p>
<p>Elenco elementi figlio</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di Windows Exchange</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Installazione delegata</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Deleted Objects,DC=\<domain\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Contenuto elenco</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Microsoft Exchange System Objects,DC=\<domain\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p>
<p>Contenuto elenco</p>
<p>Autorizzazioni di lettura</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazioni di lettura</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
</tr>
<tr class="even">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>adminDisplayName</code></p></td>
</tr>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>modifyTimeStamp</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE negata</p></td>
<td><p>Tutte</p></td>
<td><p>Elimina albero</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura Elimina albero</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Elimina elemento figlio</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Elimina elemento figlio</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Cambia password</p>
<p>Reimposta password al successivo accesso</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p>legacyExchangeDN / publicFolder</p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gestione cartelle pubbliche</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p>
<p>Proprietà di scrittura</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Exchange Install Domain Servers,CN=Microsoft Exchange System Objects,DC=\<domain\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione organizzazione</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Installazione del ruolo del server

Durante l'installazione dei ruoli del server Cassette postali e Accesso client, il programma di installazione aggiunge il gruppo di protezione universale Gestione dell'organizzazione al gruppo di protezione Administrators sul computer locale in modo che i membri del gruppo del ruolo di gestione denominato Gestione dell'organizzazione possano gestire il server.

Nella tabella delle autorizzazioni seguente vengono riportate le autorizzazioni impostate quando si installano i ruoli del server Cassette postali e Accesso client.

### Nome distinto dell'oggetto: CN=\<server\>,CN=Servers,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MACHINE$</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>MACHINE$</p></td>
<td><p>ACE consentita</p></td>
<td><p>Nessuna</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p><code>msExchServerSite</code></p>
<p><code>msExchEdgeSyncCredential</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accesso al trasporto dell'archivio</p>
<p>Delega vincolata dell'archivio</p>
<p>Accesso in lettura all'archivio</p>
<p>Accesso in lettura e scrittura all'archivio</p></td>
<td><p></p></td>
<td><p>Diritti estesi</p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Serializzazione dei token dei Servizi Web Exchange</p></td>
<td><p></p></td>
<td><p>Diritto esteso</p>
<p>Concesso solo sugli oggetti del ruolo server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sistema locale</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Autorizzazioni di lettura</p>
<p>Contenuto elenco</p>
<p>Proprietà di lettura</p>
<p>Elencazione oggetti</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Installazione delegata</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Controllo completo</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Installazione delegata</p></td>
<td><p>ACE negata</p></td>
<td><p>Tutte</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Installazione delegata</p></td>
<td><p>ACE negata</p></td>
<td><p>Tutte</p></td>
<td><p>Ricevi come</p>
<p>Invia come</p></td>
<td><p></p></td>
<td><p>Diritto esteso</p></td>
</tr>
</tbody>
</table>


## Gruppi di disponibilità del database

Nelle tabelle delle autorizzazioni di questa sezione vengono riportate le autorizzazioni impostate in relazione ai gruppi di disponibilità del database e ai relativi membri.

### Nome distinto dell'oggetto: CN=\<DAGName\>,CN=Database Availability Groups,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

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
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Nessuna</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Trasporto Edge

Se si installa un server Trasporto Edge e si stabilisce una sottoscrizione Edge con l'organizzazione di Exchange, le autorizzazioni riportate nella seguente tabella delle autorizzazioni vengono impostate quando il server Trasporto Edge crea un'istanza nell'organizzazione.

### Nome distinto dell'oggetto: CN=\<server\>,CN=Servers,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Proprietà di scrittura</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Nessuna</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p></p></td>
<td><p>ACE viene definita nello schema per gli oggetti di classe <code>msExchExchangeServer</code><code>defaultSecurityDescriptor</code>.</p></td>
</tr>
</tbody>
</table>


## Installazione del server Cassette postali

Nel corso dell'installazione del primo server Cassette postali, vengono creati i contenitori seguenti, qualora non fossero già esistenti. Nella seguente tabella delle autorizzazioni vengono riportate le autorizzazioni applicate.

### Nome distinto dell'oggetto: CN=Availability Configuration,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Desc</p></td>
<td><p>Proprietà di lettura</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpaceObjects</code></p></td>
<td><p>Diritto esteso</p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Default \<Server\>,CN=SMTP Receive Connectors,CN=Protocols,CN=\<Server\>,CN=Servers,CN=\<admin group\>,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE negata</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni della foresta</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE negata</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni dell'organizzazione</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta qualsiasi mittente</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta qualsiasi mittente</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta qualsiasi mittente</p></td>
<td><p></p></td>
<td><p>Si tratta dell'ID di sicurezza (SID) conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta qualsiasi mittente</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta qualsiasi mittente</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta EXCH50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta EXCH50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta EXCH50</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta EXCH50</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta EXCH50</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi a qualsiasi destinatario</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi a qualsiasi destinatario</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi a qualsiasi destinatario</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi a qualsiasi destinatario</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi a qualsiasi destinatario</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XShadow</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta intestazioni di routing</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta intestazioni di routing</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta intestazioni di routing</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta intestazioni di routing</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta intestazioni di routing</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XSessionParams</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XSessionParams</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XSessionParams</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni della foresta</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta xAttr</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta xAttr</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta xAttr</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XProxyFrom</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XProxyFrom della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XProxyFrom della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XSysProbe</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XSysProbe della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XSysProbe della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia proprietà estese XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia proprietà estese XMessageContext</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia proprietà estese XMessageContext</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia indice Fast XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia indice Fast XMessageContext</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia indice Fast XMessageContext</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia la cache del destinatario di Active Directory di Exchange XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia la cache del destinatario di Active Directory di Exchange XMessageContext</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia la cache del destinatario di Active Directory di Exchange XMessageContext</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta contrassegno di autenticazione</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta contrassegno di autenticazione</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta contrassegno di autenticazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta contrassegno di autenticazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta contrassegno di autenticazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora la protezione da posta indesiderata</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora la protezione da posta indesiderata</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora la protezione da posta indesiderata</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora la protezione da posta indesiderata</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora la protezione da posta indesiderata</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora limite dimensione dei messaggi</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora limite dimensione dei messaggi</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora limite dimensione dei messaggi</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora limite dimensione dei messaggi</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora limite dimensione dei messaggi</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni dell'organizzazione</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni dell'organizzazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni dell'organizzazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi al server</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi al server</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi al server</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi al server</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi al server</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta il mittente del dominio autorevole</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta il mittente del dominio autorevole</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta il mittente del dominio autorevole</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta il mittente del dominio autorevole</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta il mittente del dominio autorevole</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi a qualsiasi destinatario</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta intestazioni di routing</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora la protezione da posta indesiderata</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi al server</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto dell'oggetto: CN=Client \<Server\>,CN=SMTP Receive Connectors,CN=Protocols,CN=\<Server\>,CN=Servers,CN=\<admin group\>,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi a qualsiasi destinatario</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta intestazioni di routing</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora la protezione da posta indesiderata</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utenti autenticati</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi al server</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XSessionParams</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XSessionParams</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XSessionParams</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta qualsiasi mittente</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta qualsiasi mittente</p></td>
<td><p></p></td>
<td><p>Si tratta dell'ID di sicurezza (SID) conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta qualsiasi mittente</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta qualsiasi mittente</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta Exch50</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta Exch50</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta Exch50</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta Exch50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi a qualsiasi destinatario</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi a qualsiasi destinatario</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi a qualsiasi destinatario</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi a qualsiasi destinatario</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi a qualsiasi destinatario</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XShadow</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta intestazioni di routing</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta intestazioni di routing</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta intestazioni di routing</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta intestazioni di routing</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta intestazioni di routing</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni della foresta</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta xAttr</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta xAttr</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta xAttr</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XProxyFrom</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XProxyFrom della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XProxyFrom della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta contrassegno di autenticazione</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta contrassegno di autenticazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta contrassegno di autenticazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta contrassegno di autenticazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XSysProbe</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XSysProbe della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta XSysProbe della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta contrassegno di autenticazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora la protezione da posta indesiderata</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora la protezione da posta indesiderata</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora la protezione da posta indesiderata</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora la protezione da posta indesiderata</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia proprietà estese XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia proprietà estese XMessageContext</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia proprietà estese XMessageContext</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia indice Fast XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia indice Fast XMessageContext</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia indice Fast XMessageContext</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora limite dimensione dei messaggi</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora limite dimensione dei messaggi</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora limite dimensione dei messaggi</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Ignora limite dimensione dei messaggi</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni dell'organizzazione</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni dell'organizzazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta le intestazioni dell'organizzazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia la cache del destinatario di Active Directory di Exchange XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia la cache del destinatario di Active Directory di Exchange XMessageContext</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia la cache del destinatario di Active Directory di Exchange XMessageContext</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi al server</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi al server</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi al server</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Inoltra i messaggi al server</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta il mittente del dominio autorevole</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta il mittente del dominio autorevole</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta il mittente del dominio autorevole</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Accetta il mittente del dominio autorevole</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Creazione di connettori di invio SMTP

Nella seguente tabella vengono riportate le autorizzazioni impostate quando si creano i connettori di invio.

### Nome distinto dell'oggetto: CN=\<Connector Name\>,CN=Connections,CN=\<routing group\>,CN=Routing Groups, CN=\<admin group\>,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Account</th>
<th>Tipo ACE</th>
<th>Ereditarietà</th>
<th>Autorizzazioni</th>
<th>Sulla proprietà/ Si applica a</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NT AUTHORITY\ACCESSO ANONIMO</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni di routing</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni dell'organizzazione</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni dell'organizzazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni dell'organizzazione</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni della foresta</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia XShadow</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia XShadow</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni di routing</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-10</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni di routing</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server partner.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni di routing</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni di routing</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni di routing</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia le intestazioni di routing</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i Server Exchange legacy.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia Exch50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia Exch50</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia Exch50</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia Exch50</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i server protetti esternamente.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>ACE consentita</p></td>
<td><p>Tutte</p></td>
<td><p>Invia Exch50</p></td>
<td><p></p></td>
<td><p>Si tratta del SID conosciuto per i Server Exchange legacy.</p></td>
</tr>
</tbody>
</table>


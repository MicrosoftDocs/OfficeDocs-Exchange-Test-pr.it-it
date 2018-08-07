---
title: 'Riferimento rapido Exchange Management Shell-Exchange 2013: Exchange 2013 Help'
TOCTitle: Riferimento rapido a Exchange Management Shell per Exchange 2013
ms:assetid: 3ea4a105-a93c-48ba-96ce-6170125354e1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619302(v=EXCHG.150)
ms:contentKeyID: 50480439
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Riferimento rapido a Exchange Management Shell per Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

In questo argomento sono illustrati i cmdlet maggiormente utilizzati per la versione RTM (Release To Manufacturing) e successive di Microsoft Exchange Server 2013 e vengono forniti alcuni esempi di utilizzo.


> [!NOTE]
> Presto verranno aggiunti ulteriori contenuti su altre aree di Exchange 2013.



Per ulteriori informazioni su Exchange Management Shell in Exchange 2013 e su tutti i cmdlet disponibili, vedere gli argomenti seguenti:

  - [Utilizzo di PowerShell con Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/it-it/library/bb123778\(v=exchg.150\))

  - [Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))

## Argomenti su cui si desiderano informazioni

## Cmdlet per azioni comuni

I verbi seguenti sono supportati dalla maggioranza dei cmdlet e sono associati a un'azione specifica.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>New</p></td>
<td><p>Il verbo New consente di creare un'istanza di un elemento, ad esempio una nuova impostazione di configurazione, un nuovo database o un nuovo connettore SMTP.</p></td>
</tr>
<tr class="even">
<td><p>Remove</p></td>
<td><p>Il verbo Remove consente di rimuovere un'istanza di un elemento, ad esempio una cassetta postale o una regola di trasporto.</p>
<p>Tutti i cmdlet Remove supportano i parametri <em>WhatIf</em> e <em>Confirm</em>. Per ulteriori informazioni su questi parametri, vedere Important Parameters.</p></td>
</tr>
<tr class="odd">
<td><p>Enable</p></td>
<td><p>Il verbo Enable consente di abilitare un'impostazione o la ricezione di posta per un destinatario.</p></td>
</tr>
<tr class="even">
<td><p>Disable</p></td>
<td><p>Il verbo Disable consente di disabilitare un'impostazione o la ricezione di posta per un destinatario.</p>
<p>Tutti i cmdlet Disable supportano i parametri <em>WhatIf</em> e <em>Confirm</em>. Per ulteriori informazioni su questi parametri, vedere Important Parameters.</p></td>
</tr>
<tr class="odd">
<td><p>Set</p></td>
<td><p>Il verbo Set consente di modificare impostazioni specifiche di un oggetto, ad esempio l'alias di un contatto o il mantenimento di elementi eliminati di un database di cassette postali.</p></td>
</tr>
<tr class="even">
<td><p>Get</p></td>
<td><p>Il verbo Get consente di eseguire una query su un oggetto specifico o un sottoinsieme di un tipo di oggetto, ad esempio una cassetta postale specifica, tutti gli utenti di cassette postali o gli utenti di cassette postali in un dominio.</p></td>
</tr>
</tbody>
</table>


## Parametri importanti

I parametri seguenti consentono di controllare la modalità di esecuzione dei comandi e indicano esattamente quali operazioni verranno eseguite da un comando prima che influenzi i dati.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Identity</p></td>
<td><p>Il parametro <em>Identity</em> identifica l'oggetto univoco per l'attività. Esso è in genere utilizzato con i cmdlet Enalbe, Disable, Remove, Set e Get. <em>Identity</em> è inoltre un parametro di posizione, ovvero non è necessario specificare <em>Identity</em> quando si specifica il valore del parametro sulla riga di comando.</p>
<p>Ad esempio, <em>Get-Mailbox-Identity user1</em> esegue una query sulla cassetta postale di <em>user1</em>. <em>Get-Mailbox user1</em> è equivalente a <em>Get-Mailbox -Identity user1</em>.</p></td>
</tr>
<tr class="even">
<td><p>WhatIf</p></td>
<td><p>Il parametro <em>WhatIf</em> indica al cmdlet di simulare le azioni da eseguire sull'oggetto. Utilizzando il parametro <em>WhatIf</em>, è possibile visualizzare quali modifiche verrebbero apportate senza effettivamente applicarle. Il valore predefinito è <em>$true</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Confirm</p></td>
<td><p>Il parametro <em>Confirm</em> determina l'interruzione dell'elaborazione del cmdlet e richiede che l'amministratore sia a conoscenza dell'operazione che verrà eseguita dal cmdlet prima che l'elaborazione continui. Il valore predefinito è <em>$true</em>.</p></td>
</tr>
<tr class="even">
<td><p>Validate</p></td>
<td><p>Il parametro <em>Validate</em> determina la verifica, da parte del cmdlet, che siano soddisfatti tutti i prerequisiti per l'esecuzione dell'operazione e che l'operazione venga completata correttamente.</p></td>
</tr>
</tbody>
</table>


## Suggerimenti pratici

I comandi seguenti sono associati a varie attività che è possibile utilizzare per l'amministrazione di Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-Command</p></td>
<td><p>Questo cmdlet recupera tutte le attività che possono essere eseguite in Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p>Get-Command *<em>parola chiave</em>*</p></td>
<td><p>Questo cmdlet recupera le attività con <em>parola chiave</em> nel cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p>Get-<em>attività</em> | Get-Member</p></td>
<td><p>Questo cmdlet recupera tutte le proprietà e i metodi di <em>attività</em>.</p></td>
</tr>
<tr class="even">
<td><p>Get-<em>attività</em> | Format-List</p></td>
<td><p>Questo cmdlet visualizza l'output della query in un elenco formattato. È possibile eseguire il piping dell'output di qualsiasi cmdlet Get in Format-List per visualizzare l'intero set di proprietà presenti nell'oggetto restituito dal comando oppure è possibile specificare singole proprietà che si desidera visualizzare, separate da virgole, come nell'esempio seguente: <em>Get-Mailbox *john* | Format-List alias,*quota</em></p></td>
</tr>
<tr class="odd">
<td><p>Help <em>attività</em></p></td>
<td><p>Questo cmdlet recupera informazioni nella Guida di Exchange Management Shell su qualsiasi attività di Exchange 2013, come nell'esempio seguente: <em>Help Get-Mailbox</em></p></td>
</tr>
<tr class="even">
<td><p>Get-<em>attività</em> | Format-List &gt; <em>file.txt</em></p></td>
<td><p>Questo cmdlet esporta l'output di <em>attività</em> in un file di testo: <em>file.txt</em></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-RoleGroupMember &quot;<em>Organization Management</em>&quot;</p></td>
<td><p>Questo comando recupera i membri del gruppo di ruoli di gestione <em>Organization Management</em>.</p></td>
</tr>
<tr class="even">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Mail Recipient Creation</em>&quot; -GetEffectiveUsers</p></td>
<td><p>Questo comando recupera l'elenco di tutti gli utenti a cui sono state concesse le autorizzazioni fornite dal ruolo di gestione <em>Mail Recipient Creation</em>. Sono inclusi gli utenti membri dei gruppi di ruoli o dei gruppi di sicurezza universali a cui è stato assegnato il ruolo Mail Recipient Creation. Non sono inclusi gli utenti membri dei gruppi di ruoli collegati in un'altra foresta.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -RoleAssignee <em>Administrator</em> | Get-ManagementRole | Get-ManagementRoleEntry</p></td>
<td><p>Questo comando recupera un elenco di cmdlet che possono essere eseguiti dall'utente <em>Administrator</em>.</p></td>
</tr>
<tr class="even">
<td><p>ForEach ($RoleEntry in Get-ManagementRoleEntry *\<em>Remove-Mailbox</em> -parameters Identity) {Get-ManagementRoleAssignment -Role $RoleEntry.Role -GetEffectiveUsers -Delegating $False | Where-Object {$_.EffectiveUserName -Ne &quot;All Group Members&quot;} | FL Role, EffectiveUserName, AssignmentChain}</p></td>
<td><p>Questo comando recupera l'elenco di tutti gli utenti che possono eseguire il cmdlet <em>Remove-Mailbox</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -WritableRecipient <em>kima</em> -GetEffectiveUsers | FT RoleAssigneeName, EffectiveUserName, Role, AssignmentChain</p></td>
<td><p>Questo comando recupera l'elenco di tutti gli utenti che possono modificare la cassetta postale di <em>kima</em>.</p></td>
</tr>
<tr class="even">
<td><p>New-ManagementScope &quot;<em>Seattle Users</em>&quot; -RecipientRestrictionFilter { <em>City</em> -Eq &quot;<em>Seattle</em>&quot; }</p>
<p>New-RoleGroup &quot;<em>Seattle Admins</em>&quot; -Roles &quot;<em>Mail Recipients</em>&quot;, &quot;<em>Mail Recipient Creation</em>&quot;, &quot;<em>Mailbox Import Export</em>&quot;, -CustomRecipientWriteScope &quot;<em>Seattle Users</em>&quot;</p></td>
<td><p>Questo comando crea un nuovo ambito di gestione e un nuovo gruppo di ruoli di gestione per consentire ai membri di tale gruppo di gestire i destinatari di Seattle.</p>
<p>Viene creato innanzitutto l'ambito di gestione <em>Seattle Users</em>, che include solo i destinatari per cui l'attributo <em>City</em> del relativo oggetto utente è impostato su <em>Seattle</em>.</p>
<p>Viene quindi creato un nuovo gruppo di ruoli denominato <em>Seattle Admins</em>, dopodiché vengono assegnati i ruoli <em>Mail Recipients</em>, <em>Mail Recipient Creation</em> e <em>Mailbox Import Export</em>. L'ambito del gruppo di ruoli viene definito in modo che i relativi membri possano gestire solo gli utenti che rientrano nell'ambito del filtro dei destinatari <em>Seattle Users</em>.</p></td>
</tr>
<tr class="odd">
<td><p>New-ManagementScope &quot;<em>Vancouver Servers</em>&quot; -ServerRestrictionFilter { <em>ServerSite</em> -Eq &quot;<em>Vancouver</em>&quot; }</p>
<p>$RoleGroup = Get-RoleGroup &quot;<em>Server Management</em>&quot;</p>
<p>New-RoleGroup &quot;<em>Vancouver Server Management</em>&quot; -Roles $RoleGroup.Roles -CustomConfigWriteScope &quot;<em>Vancouver Servers</em>&quot;</p></td>
<td><p>Questo comando crea un nuovo ambito di gestione e copia un gruppo di ruoli esistente per consentire ai membri del nuovo gruppo di gestire solo i server del sito di Active Directory Vancouver.</p>
<p>Viene creato innanzitutto l'ambito di gestione <em>Vancouver Servers</em>, che include solo i server disponibili nel sito Active Directory <em>Vancouver</em>. Tale sito Active Directory è memorizzato nell'attributo <em>ServerSite</em> degli oggetti server.</p>
<p>Viene quindi creato un nuovo gruppo di ruoli di nome <em>Vancouver Server Management</em>, costituito da una copia del gruppo di ruoli <em>Server Management</em>. Per il nuovo gruppo di ruoli viene tuttavia definito un ambito che consente ai membri di gestire solo i server che rientrano nell'ambito del filtro di configurazione <em>Vancouver Servers</em>.</p></td>
</tr>
<tr class="even">
<td><p>Add-RoleGroupMember &quot;<em>Organization Management</em>&quot; -Member <em>davids</em></p></td>
<td><p>Questo comando aggiunge l'utente <em>davids</em> al gruppo di ruoli <em>Organization Management</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Mail Recipient Creation</em>&quot; -RoleAssignee &quot;<em>Seattle Admins</em>&quot; | Remove-ManagementRoleAssignment</p></td>
<td><p>Questo comando rimuove il ruolo <em>Mail Recipient Creation</em> dal gruppo di ruoli <em>Seattle Admins</em>. Questo comando è utile perché non è necessario conoscere il nome dell'assegnazione del ruolo di gestione che associa il ruolo al gruppo di ruoli.</p></td>
</tr>
</tbody>
</table>


## Remote Shell


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos</p>
<p>Import-PSSession $Session</p></td>
<td><p>Questi comandi aprono una sessione shell remota tra un computer locale aggiunto al dominio e un server Exchange 2013 remoto con nome di dominio completo <em>ExServer.contoso.com</em>. Utilizzare questo comando se si desidera gestire un server Exchange 2013 remoto e si dispone solo di Windows Management Framework, che include l'interfaccia della riga di comando Windows PowerShell, installata nel computer locale. Questo comando utilizza le credenziali di accesso correnti per l'autenticazione sul server Exchange 2013 remoto.</p></td>
</tr>
<tr class="even">
<td><p>$UserCredential = Get-Credential</p>
<p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos -Credential $UserCredential</p>
<p>Import-PSSession $Session</p></td>
<td><p>Questi comandi aprono una sessione shell remota tra un computer locale aggiunto al dominio e un server Exchange 2013 remoto con nome di dominio completo <em>ExServer.contoso.com</em>. Utilizzare questo comando se si desidera gestire un server Exchange 2013 remoto e si dispone solo di Windows Management Framework, che include Windows PowerShell, installato nel computer locale. Questo comando utilizza le credenziali specificate esplicitamente per l'autenticazione sul server Exchange 2013 remoto.</p></td>
</tr>
<tr class="odd">
<td><p>Remove-PSSession $Session</p></td>
<td><p>Questo comando chiude la sessione shell remota tra un computer locale e il server Exchange 2013 remoto.</p></td>
</tr>
<tr class="even">
<td><p>Import-RecipientDataProperty -Identity &quot;Tony Smith&quot; -SpokenName -FileData <em>([Byte[]]$(Get-Content -Path &quot;M:\AudioFiles\TonySmith.wma&quot; -Encoding Byte -ReadCount 0))</em></p></td>
<td><p>Questo comando mostra un esempio, in corsivo, della sintassi richiesta per importare un file in un server Exchange 2013 remoto utilizzando il paramero FileData su un cmdlet. La sintassi comprende i dati contenuti nel file <em>M:\AudioFiles\TonySmith.wma</em> e invia tramite flusso i dati alla proprietà FileData sul cmdlet Import-RecipientDataProperty.</p>
<p>Il parametro FileData accetta dati da un file sul computer locale utilizzando questa sintassi sulla maggior parte dei cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p>Export-RecipientDataProperty -Identity tony@contoso.com -SpokenName <em>| ForEach { $_.FileData | Add-Content C:\tonysmith.wma -Encoding Byte}</em></p></td>
<td><p>Questo comando mostra un esempio, in corsivo, della sintassi richiesta per esportare un file da un server Exchange 2013 remoto. La sintassi comprende i dati archiviati nella proprietà FileData sull'oggetto restituito dal cmdlet e quindi invia tramite flusso i dati al computer locale. I dati vengono quindi archiviati nel file <em>C:\tonysmith.wma</em>.</p>
<p>La maggior parte dei cmdlet che emette oggetti con una proprietà FileData utilizza questa sintassi per esportare dati in un file sul computer locale.</p></td>
</tr>
</tbody>
</table>


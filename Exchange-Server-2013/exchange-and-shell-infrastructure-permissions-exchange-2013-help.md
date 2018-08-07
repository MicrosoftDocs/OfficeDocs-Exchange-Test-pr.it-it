---
title: 'Autorizzaz. infrastr. Exchange/Exchange Management Shell: Exchange 2013 Help'
TOCTitle: Autorizzazioni infrastruttura Exchange ed Exchange Management Shell
ms:assetid: 3646a4e8-36b2-41fb-89a4-79b0963fcb11
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638114(v=EXCHG.150)
ms:contentKeyID: 50480336
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzazioni infrastruttura Exchange ed Exchange Management Shell

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Le autorizzazioni necessarie per eseguire attività che consentono la configurazione dei vari componenti di Microsoft Exchange Server 2013 dipendono dalla procedura eseguita o dal cmdlet che si desidera eseguire. Vedere ciascuna delle sezioni in questo argomento per ulteriori informazioni sulle loro rispettive funzionalità.

Per individuare le autorizzazioni necessarie per eseguire la procedura o il cmdlet, procedere come segue:

1.  Nella tabella seguente individuare la funzionalità più pertinente alla procedura o al cmdlet che si vuole eseguire.

2.  Esaminare quindi le autorizzazioni necessarie per la funzionalità. È necessario ricevere l'assegnazione di uno di questi gruppi di ruoli, di un gruppo di ruoli personalizzato equivalente o di un ruolo di gestione equivalente. È inoltre possibile fare clic su un gruppo di ruoli per visualizzarne i ruoli di gestione. Se per una determinata funzionalità sono elencati più gruppi di ruoli, per usarla è necessario essere assegnati a uno di questi gruppi. Per altre informazioni sui gruppi di ruoli e sui ruoli di gestione, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

3.  A questo punto, eseguire il cmdlet **Get-ManagementRoleAssignment** per individuare i gruppi di ruoli o i ruoli di gestione a cui si è assegnati e verificare se si dispone delle autorizzazioni necessarie per gestire la funzionalità.
    

    > [!NOTE]
    > Per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG> è necessario ricevere l'assegnazione del ruolo di gestione dei ruoli. Se non si hanno le autorizzazioni per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, chiedere all'amministratore di Exchange di recuperare i gruppi di ruoli o i ruoli di gestione assegnati.



Se si desidera delegare la gestione di una funzionalità a un altro utente, vedere [Delegare le assegnazioni di ruolo](delegate-role-assignments-exchange-2013-help.md).


> [!NOTE]
> È possibile che per alcune funzionalità siano necessarie le autorizzazioni dell'amministratore locale sul server che si vuole gestire. Per gestire queste funzionalità, è necessario essere membro del gruppo Administrators locale su quel server.



## Autorizzazioni per l'infrastruttura di Exchange

Nella tabella seguente sono elencate le autorizzazioni necessarie per eseguire attività che consentono la configurazione generale delle impostazioni di Exchange 2013.

Gli utenti a cui viene assegnato il gruppo di ruoli di gestione in sola visualizzazione possono visualizzare la configurazione delle funzionalità nella tabella seguente. Per altre informazioni, vedere Gestione dell'organizzazione in sola visualizzazione[Gestione organizzazione sola visualizzazione](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Autorizzazioni necessarie</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Registrazione controlli dell'amministratore</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni di configurazione dell'interfaccia di amministrazione di Exchange</p></td>
<td><p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Connettività dell'interfaccia di amministrazione di Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni di configurazione del server di Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Impostazioni della Guida</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Categorie dei messaggi</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="odd">
<td><p>Codice &quot;Product Key&quot;</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Integrità del sistema di verifica</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Registrazione di controllo dell'amministratore in sola visualizzazione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p>

> [!NOTE]
> È anche possibile assegnare manualmente il ruolo di gestione Registri di controllo di sola visualizzazione a un gruppo di ruoli di gestione. Per ulteriori informazioni, vedere <A href="view-only-audit-logs-role-exchange-2013-help.md">Ruolo registri di controllo sola visualizzazione</A>.


</td>
</tr>
<tr class="even">
<td><p>Scrittura nel registro di controllo</p></td>
<td><p>Gli utenti membri di un qualsiasi gruppo di ruoli o assegnati a un qualsiasi ruolo di gestione possono scrivere nel registro di controllo dell'amministratore.</p></td>
</tr>
</tbody>
</table>


## Autorizzazioni per l'infrastruttura di Shell

Nella tabella seguente sono elencate le autorizzazioni necessarie per eseguire attività che consentono di configurare le funzionalità che controllano l'esecuzione di Exchange Management Shell.

Gli utenti a cui viene assegnato il gruppo di ruoli di gestione in sola visualizzazione possono visualizzare la configurazione delle funzionalità nella tabella seguente. Per altre informazioni, vedere Gestione dell'organizzazione in sola visualizzazione[Gestione organizzazione sola visualizzazione](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Autorizzazioni necessarie</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Impostazioni del server Servizi di dominio Active Directory</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestione messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p>Agenti di estensione di cmdlet</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Directory virtuali di PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Installazione di PowerShell e Gestione remota Windows</p></td>
<td><p>Amministratore del server locale</p></td>
</tr>
<tr class="odd">
<td><p>Remote Shell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni per certificati e federazione

Nella seguente tabella sono elencate le autorizzazioni necessarie per eseguire attività correlate alle relazioni di trust federative, alla configurazione OAuth, alla gestione dei certificati e alla configurazione della distribuzione ibrida.

Gli utenti a cui viene assegnato il gruppo di ruoli di gestione in sola visualizzazione possono visualizzare la configurazione delle funzionalità nella tabella seguente. Per altre informazioni, vedere Gestione dell'organizzazione in sola visualizzazione[Gestione organizzazione sola visualizzazione](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Autorizzazioni necessarie</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione dei certificati</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Relazioni di trust federative, OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Relazioni di trust federative di prova, OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Configurazione della distribuzione ibrida</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Connettori tra organizzazioni</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
</tbody>
</table>


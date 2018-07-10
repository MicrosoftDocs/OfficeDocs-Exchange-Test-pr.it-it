---
title: 'Autorizzazioni di integrità e prestazioni del server: Exchange 2013 Help'
TOCTitle: Autorizzazioni di integrità e prestazioni del server
ms:assetid: 00b23fd3-6679-4b06-a3d4-51df3112b9cd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150479(v=EXCHG.150)
ms:contentKeyID: 50479891
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzazioni di integrità e prestazioni del server

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

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



## Autorizzazioni di gestione del carico di lavoro di Exchange

Nella tabella seguente sono elencate le autorizzazioni necessarie per eseguire attività che gestiscono l'integrità e prestazioni dell'organizzazione Exchange 2013. Per ulteriori informazioni, vedere [Gestione del carico di lavoro di Exchange](exchange-workload-management-exchange-2013-help.md).

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
<td><p>Limitazione utente</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Limitazione del carico di lavoro di Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni del registro eventi di Exchange

Nella tabella seguente sono elencate le autorizzazioni necessarie per eseguire attività che consentono di gestire le impostazioni del registro eventi di Exchange.

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
<td><p>Gestione dei registri eventi di Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestione messaggistica unificata</a></p></td>
</tr>
</tbody>
</table>


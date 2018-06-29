---
title: 'Autorizzazioni per la gestione del ruolo: Exchange 2013 Help'
TOCTitle: Autorizzazioni per la gestione del ruolo
ms:assetid: cb9591c4-fbb3-4199-8007-6bbfdfd5a2e9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638186(v=EXCHG.150)
ms:contentKeyID: 50481696
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzazioni per la gestione del ruolo

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Le autorizzazioni richieste per eseguire le operazioni di configurazione dei ruoli di gestione dipendono dalla procedura eseguita o dal cmdlet che si intende eseguire. Per ulteriori informazioni sui ruoli di gestione, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

Per individuare le autorizzazioni necessarie per eseguire la procedura o il cmdlet, procedere come segue:

1.  Nella tabella seguente individuare la funzionalità più pertinente alla procedura o al cmdlet che si vuole eseguire.

2.  Esaminare quindi le autorizzazioni necessarie per la funzionalità. È necessario ricevere l'assegnazione di uno di questi gruppi di ruoli, di un gruppo di ruoli personalizzato equivalente o di un ruolo di gestione equivalente. È inoltre possibile fare clic su un gruppo di ruoli per visualizzarne i ruoli di gestione. Se per una determinata funzionalità sono elencati più gruppi di ruoli, per usarla è necessario essere assegnati a uno di questi gruppi. Per altre informazioni sui gruppi di ruoli e sui ruoli di gestione, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

3.  A questo punto, eseguire il cmdlet **Get-ManagementRoleAssignment** per individuare i gruppi di ruoli o i ruoli di gestione a cui si è assegnati e verificare se si dispone delle autorizzazioni necessarie per gestire la funzionalità.
    

    > [!NOTE]
    > Per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG> è necessario ricevere l'assegnazione del ruolo di gestione dei ruoli. Se non si hanno le autorizzazioni per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, chiedere all'amministratore di Exchange di recuperare i gruppi di ruoli o i ruoli di gestione assegnati.



Se si desidera delegare la gestione di una funzionalità a un altro utente, vedere [Delegare le assegnazioni di ruolo](delegate-role-assignments-exchange-2013-help.md).

## Autorizzazioni per la gestione del ruolo

È possibile utilizzare le funzionalità indicate nella seguente tabella per gestire i gruppi di ruoli di gestione, i ruoli, i criteri di assegnazione, le assegnazioni e gli ambiti che definiscono le autorizzazioni applicabili ad amministratori e utenti finali. Gli utenti a cui viene assegnato il gruppo di ruoli di gestione in sola visualizzazione possono visualizzare la configurazione delle funzionalità nella tabella seguente. Per altre informazioni, vedere Gestione dell'organizzazione in sola visualizzazione[Gestione organizzazione sola visualizzazione](view-only-organization-management-exchange-2013-help.md).


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
<td><p>Ruoli di gestione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Ruoli di gestione privi di ambito</p></td>
<td><p>Ruolo di gestione <a href="unscoped-role-management-role-exchange-2013-help.md">Ruolo senza ambito di gestione dei ruoli</a></p></td>
</tr>
<tr class="odd">
<td><p>Gruppi di ruoli</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Criteri di assegnazione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Assegnazioni di ruolo</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Ambiti di gestione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Voci del ruolo di gestione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni legacy</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Divisione delle autorizzazioni di Active Directory</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>

> [!IMPORTANT]
> Per eseguire il comando <CODE>setup.exe</CODE> con i parametri <EM>PrepareAD</EM> e <EM>ActiveDirectorySplitPermissions</EM>, l'account utilizzato deve essere membro dei gruppi Schema Admins ed Enterprise Administrators.


</td>
</tr>
</tbody>
</table>


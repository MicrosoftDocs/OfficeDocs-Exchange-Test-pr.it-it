---
title: 'Criteri di messaggistica e autorizzazioni di conformità: Exchange 2013 Help'
TOCTitle: Criteri di messaggistica e autorizzazioni di conformità
ms:assetid: ec4d3b9f-b85a-4cb9-95f5-6fc149c3899b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638205(v=EXCHG.150)
ms:contentKeyID: 50481935
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criteri di messaggistica e autorizzazioni di conformità

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Le autorizzazioni richieste per configurare i criteri di messaggistica e la conformità dipendono dalla procedura in esecuzione o dal cmdlet che si intende eseguire. Per ulteriori informazioni sui criteri di messaggistica e sulla conformità, vedere [Criteri di messaggistica e conformità](messaging-policy-and-compliance-exchange-2013-help.md).

Per individuare le autorizzazioni necessarie per eseguire la procedura o il cmdlet, procedere come segue:

1.  Nella tabella seguente individuare la funzionalità più pertinente alla procedura o al cmdlet che si vuole eseguire.

2.  Esaminare quindi le autorizzazioni necessarie per la funzionalità. È necessario ricevere l'assegnazione di uno di questi gruppi di ruoli, di un gruppo di ruoli personalizzato equivalente o di un ruolo di gestione equivalente. È inoltre possibile fare clic su un gruppo di ruoli per visualizzarne i ruoli di gestione. Se per una determinata funzionalità sono elencati più gruppi di ruoli, per usarla è necessario essere assegnati a uno di questi gruppi. Per altre informazioni sui gruppi di ruoli e sui ruoli di gestione, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

3.  A questo punto, eseguire il cmdlet **Get-ManagementRoleAssignment** per individuare i gruppi di ruoli o i ruoli di gestione a cui si è assegnati e verificare se si dispone delle autorizzazioni necessarie per gestire la funzionalità.
    

    > [!NOTE]
    > Per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG> è necessario ricevere l'assegnazione del ruolo di gestione dei ruoli. Se non si hanno le autorizzazioni per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, chiedere all'amministratore di Exchange di recuperare i gruppi di ruoli o i ruoli di gestione assegnati.



Se si desidera delegare la gestione di una funzionalità a un altro utente, vedere [Delegare le assegnazioni di ruolo](delegate-role-assignments-exchange-2013-help.md).


> [!NOTE]
> È possibile che alcune delle funzionalità che si desidera gestire esistano sui server Trasporto Edge. Per gestire le funzionalità sui server Trasporto Edge, è necessario diventare membro del gruppo Administrators locale sul server Trasporto Edge che si desidera gestire. I server Trasporto Edge non usano il controllo di accesso basato sui ruoli (RBAC). Le funzionalità che è possibile gestire sui server Trasporto Edge hanno l'amministratore locale di Trasporto Edge nella colonna "Autorizzazioni necessarie" nella tabella sotto riportata.



## Criteri di messaggistica e autorizzazioni di conformità

È possibile utilizzare le funzionalità nella tabella seguente per configurare le funzionalità dei criteri di messaggistica e della conformità. Sono elencati i gruppi di ruolo necessari per configurare ciascuna funzionalità.

Gli utenti a cui è assegnato il gruppo di ruoli View-Only Management possono visualizzare la configurazione delle funzionalità nella tabella seguente. Per ulteriori informazioni, vedere [Gestione organizzazione sola visualizzazione](view-only-organization-management-exchange-2013-help.md).


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
<td><p>Prevenzione della perdita di dati (DLP)</p></td>
<td><p>Se si utilizza Office 365:</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Amministratore globale di office 365</a>, che include automaticamente Exchange <a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Amministrazione del servizio Office 365</a>, oltre a gruppo di ruoli amministratore <a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a> in Exchange</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Amministratore password di Office 365</a></p></li>
</ul>
<p>Se si utilizza solo Exchange Server 2013 o Exchange Online:</p>
<ul>
<li><p><a href="compliance-management-exchange-2013-help.md">Gestione della conformità</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Eliminazione del contenuto delle cassette postali tramite il cmdlet <a href="https://technet.microsoft.com/it-it/library/dd298173(v=exchg.150)">Search-Mailbox</a> con l'opzione <em>DeleteContent</em></p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">Gestione individuazione</a> <strong>e</strong></p>
<p><a href="mailbox-import-export-role-exchange-2013-help.md">Ruolo di importazione\esportazione delle cassette postali</a></p>

> [!NOTE]
> Per impostazione predefinita, il ruolo di esportazione e importazione delle cassette postali non viene assegnato ad alcun gruppo di ruoli. È possibile assegnare un ruolo di gestione a un gruppo di ruoli predefinito o personalizzato, un utente o un gruppo di sicurezza universale. È consigliabile assegnare un ruolo a un gruppo di ruoli. Per ulteriori informazioni, vedere <A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">Aggiungere un ruolo di un utente o gruppo di protezione universale</A>.


</td>
</tr>
<tr class="odd">
<td><p>Creazione di cassette postali di individuazione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Inserimento nel journal</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
<tr class="odd">
<td><p>Registrazione di controllo delle cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
<tr class="even">
<td><p>Classificazioni dei messaggi</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Gestione record di messaggistica</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">Gestione della conformità</a></p>
<p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
<tr class="even">
<td><p>eDiscovery in locale</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">Gestione individuazione</a></p>

> [!NOTE]
> Per impostazione predefinita, il gruppo di ruoli Discovery Management è inizialmente vuoto. Nessun utente, inclusi gli amministratori, dispone delle autorizzazioni necessarie per eseguire ricerche nelle cassette postali. Per ulteriori informazioni, vedere <A href="https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-ediscovery/assign-ediscovery-permissions">Assegnare le autorizzazioni di eDiscovery di Exchange</A>.


</td>
</tr>
<tr class="odd">
<td><p>Conservazione in locale</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">Gestione individuazione</a></p>
<p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>

> [!IMPORTANT]
> Per creare un'archiviazione sul posto basata su query, l'utente richiede l'assegnazione dei ruoli Ricerca nella cassetta postale e Conservazione per controversia legale direttamente o tramite l'appartenenza a un gruppo di ruoli a cui sono stati assegnati entrambi i ruoli. Per creare un'archiviazione sul posto senza utilizzare la query, che mette in attesa tutti gli elementi della cassetta postale, deve essere stato assegnato il ruolo Conservazione per controversia legale. Il gruppo di ruoli Gestione individuazione viene assegnato a entrambi i ruoli.<BR>Il gruppo di ruoli Gestione organizzazione viene assegnato al ruolo Conservazione per controversia legale. I membri del gruppo di ruoli Gestione organizzazione possono archiviare sul posto tutti gli elementi di una cassetta postale, ma non creare un'archiviazione sul posto basata su query.


</td>
</tr>
<tr class="even">
<td><p>Archivio locale</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Archivio locale – Test connettività</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Information Rights Management (IRM), configurazione</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">Gestione della conformità</a></p>
<p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Criteri di conservazione – Applicazione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
<tr class="even">
<td><p>Criteri di conservazione - Creazione</p></td>
<td><p>Vedere Gestione record di messaggistica</p></td>
</tr>
<tr class="odd">
<td><p>Regole di trasporto</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
</tbody>
</table>


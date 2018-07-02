---
title: 'Autorizzazioni per il flusso di posta: Exchange 2013 Help'
TOCTitle: Autorizzazioni per il flusso di posta
ms:assetid: f49f4fb5-af75-43cb-900f-c5f7b8cfa143
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638213(v=EXCHG.150)
ms:contentKeyID: 50482019
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzazioni per il flusso di posta

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Le autorizzazioni necessarie per eseguire le attività correlate al flusso di posta dipendono dalla procedura eseguita o dal cmdlet che si intende eseguire. Per ulteriori informazioni sulle funzionalità di trasporto, vedere [Flusso di posta](mail-flow-exchange-2013-help.md).

In questo argomento sono elencate le autorizzazioni necessarie per gestire le caratteristiche di flusso di posta elettronica in Microsoft Exchange Server 2013. Per informazioni sulla correlazione tra le autorizzazioni di Office 365 per le autorizzazioni di Exchange, vedere [autorizzazioni in Office 365](https://go.microsoft.com/fwlink/p/?linkid=335814).

Per individuare le autorizzazioni necessarie per eseguire la procedura o il cmdlet, procedere come segue:

1.  Nella tabella seguente individuare la funzionalità più pertinente alla procedura o al cmdlet che si vuole eseguire.

2.  Esaminare quindi le autorizzazioni necessarie per la funzionalità. È necessario ricevere l'assegnazione di uno di questi gruppi di ruoli, di un gruppo di ruoli personalizzato equivalente o di un ruolo di gestione equivalente. È inoltre possibile fare clic su un gruppo di ruoli per visualizzarne i ruoli di gestione. Se per una determinata funzionalità sono elencati più gruppi di ruoli, per usarla è necessario essere assegnati a uno di questi gruppi. Per altre informazioni sui gruppi di ruoli e sui ruoli di gestione, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

3.  A questo punto, eseguire il cmdlet **Get-ManagementRoleAssignment** per individuare i gruppi di ruoli o i ruoli di gestione a cui si è assegnati e verificare se si dispone delle autorizzazioni necessarie per gestire la funzionalità.
    

    > [!NOTE]
    > Per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG> è necessario ricevere l'assegnazione del ruolo di gestione dei ruoli. Se non si hanno le autorizzazioni per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, chiedere all'amministratore di Exchange di recuperare i gruppi di ruoli o i ruoli di gestione assegnati.



Se si desidera delegare la gestione di una funzionalità a un altro utente, vedere [Delegare le assegnazioni di ruolo](delegate-role-assignments-exchange-2013-help.md).


> [!NOTE]
> È possibile che alcune delle funzionalità che si desidera gestire esistano sui server Trasporto Edge. Per gestire le funzionalità sui server Trasporto Edge, è necessario diventare membro del gruppo Administrators locale sul server Trasporto Edge che si desidera gestire. I server Trasporto Edge non usano il controllo di accesso basato sui ruoli (RBAC). Le funzionalità che è possibile gestire sui server Trasporto Edge hanno l'amministratore locale di Trasporto Edge nella colonna "Autorizzazioni necessarie" nella tabella sotto riportata.




> [!NOTE]
> È possibile che per alcune funzionalità siano necessarie le autorizzazioni dell'amministratore locale sul server che si vuole gestire. Per gestire queste funzionalità, è necessario essere membro del gruppo Administrators locale su quel server.



## Autorizzazioni per il flusso di posta

È possibile utilizzare le funzionalità indicate nelle tabelle seguenti per configurare il flusso di posta nel servizio di trasporto front-end sui server Accesso client, nel servizio di trasporto sui server Cassette postali, nel servizio di trasporto alle cassette postali sui server Cassette postali e Trasporto Edge. Sono elencate le autorizzazioni necessarie per configurare ciascuna funzionalità.

Gli utenti a cui è assegnato il gruppo di ruolo View-Only Management possono visualizzare la configurazione delle funzionalità nella tabella seguente. Per ulteriori informazioni, vedere [Gestione organizzazione sola visualizzazione](view-only-organization-management-exchange-2013-help.md).

**Server Cassette postali e server Accesso client**


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
<td><p>Domini accettati</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Gestione del sito e del collegamento al sito Active Directory</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Funzionalità di protezione da posta indesiderata</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p></td>
</tr>
<tr class="even">
<td><p>Aggiornamenti protezione da posta indesiderata</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p></td>
</tr>
<tr class="odd">
<td><p>Gestione dei certificati</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Connettori dell'agente di recapito</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>DSN</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>EdgeSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Connettori esterni</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Servizio Trasporto front-end</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p></td>
</tr>
<tr class="odd">
<td><p>Inserimento nel journal</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
<tr class="even">
<td><p>Accesso alle cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurazione della posta indesiderata delle cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="even">
<td><p>Servizio Trasporto cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p></td>
</tr>
<tr class="odd">
<td><p>Suggerimenti messaggio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Classificazioni dei messaggi</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
<tr class="odd">
<td><p>Verifica messaggi</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Trasporto con moderatore</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Code</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Connettori di ricezione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p></td>
</tr>
<tr class="odd">
<td><p>Domini remoti</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Aggregazione dell'elenco indirizzi attendibili</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
<tr class="odd">
<td><p>Connettori di invio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Ridondanza shadow</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Test del flusso di posta</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Test dell'elaborazione delle regole di trasporto</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Agenti di trasporto</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
<tr class="even">
<td><p>Configurazione del trasporto</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Registri di trasporto</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Regole di trasporto</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
<tr class="odd">
<td><p>Servizio di trasporto</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p></td>
</tr>
<tr class="even">
<td><p>Domini X.400</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
</tbody>
</table>


**Server Trasporto Edge**


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
<td><p>Domini accettati - Trasporto Edge</p></td>
<td><p>Trasporto Edge - Amministratore locale</p></td>
</tr>
<tr class="even">
<td><p>Riscrittura indirizzo - Trasporto Edge</p></td>
<td><p>Amministratore locale di Trasporto Edge</p></td>
</tr>
<tr class="odd">
<td><p>Server Trasporto Edge</p></td>
<td><p>Amministratore locale di Trasporto Edge</p></td>
</tr>
<tr class="even">
<td><p>EdgeSync - Trasporto Edge</p></td>
<td><p>Amministratore locale di Trasporto Edge</p></td>
</tr>
<tr class="odd">
<td><p>Code - Trasporto Edge</p></td>
<td><p>Amministratore locale di Trasporto Edge</p></td>
</tr>
<tr class="even">
<td><p>Connettori di ricezione - Trasporto Edge</p></td>
<td><p>Amministratore locale di Trasporto Edge</p></td>
</tr>
<tr class="odd">
<td><p>Connettori di invio - Trasporto Edge</p></td>
<td><p>Amministratore locale di Trasporto Edge</p></td>
</tr>
<tr class="even">
<td><p>Configurazione del trasporto - Trasporto Edge</p></td>
<td><p>Amministratore locale di Trasporto Edge</p></td>
</tr>
<tr class="odd">
<td><p>Registri di trasporto - Trasporto Edge</p></td>
<td><p>Amministratore locale di Trasporto Edge</p></td>
</tr>
<tr class="even">
<td><p>Regole di trasporto - Trasporto Edge</p></td>
<td><p>Amministratore locale di Trasporto Edge</p></td>
</tr>
</tbody>
</table>


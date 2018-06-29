---
title: 'Elevata disponibilità e sito le autorizzazioni resilienza: Exchange 2013 Help'
TOCTitle: Elevata disponibilità e sito le autorizzazioni resilienza
ms:assetid: 66085107-4d4d-41c3-a425-82314acd9eee
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638136(v=EXCHG.150)
ms:contentKeyID: 50480832
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Elevata disponibilità e sito le autorizzazioni resilienza

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-11-12_

Le autorizzazioni richieste per configurare l'alta disponibilità dipendono dalla procedura eseguita o dal cmdlet che si intende eseguire. Per ulteriori informazioni sull'alta disponibilità, vedere [Disponibilità elevata e resilienza del sito](high-availability-and-site-resilience-exchange-2013-help.md).

Per individuare le autorizzazioni necessarie per eseguire la procedura o il cmdlet, procedere come segue:

1.  Nella tabella seguente individuare la funzionalità più pertinente alla procedura o al cmdlet che si vuole eseguire.

2.  Esaminare quindi le autorizzazioni necessarie per la funzionalità. È necessario ricevere l'assegnazione di uno di questi gruppi di ruoli, di un gruppo di ruoli personalizzato equivalente o di un ruolo di gestione equivalente. È inoltre possibile fare clic su un gruppo di ruoli per visualizzarne i ruoli di gestione. Se per una determinata funzionalità sono elencati più gruppi di ruoli, per usarla è necessario essere assegnati a uno di questi gruppi. Per altre informazioni sui gruppi di ruoli e sui ruoli di gestione, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

3.  A questo punto, eseguire il cmdlet **Get-ManagementRoleAssignment** per individuare i gruppi di ruoli o i ruoli di gestione a cui si è assegnati e verificare se si dispone delle autorizzazioni necessarie per gestire la funzionalità.
    

    > [!NOTE]
    > Per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG> è necessario ricevere l'assegnazione del ruolo di gestione dei ruoli. Se non si hanno le autorizzazioni per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, chiedere all'amministratore di Exchange di recuperare i gruppi di ruoli o i ruoli di gestione assegnati.



Se si desidera delegare la gestione di una funzionalità a un altro utente, vedere [Delegare le assegnazioni di ruolo](delegate-role-assignments-exchange-2013-help.md).

## Autorizzazioni per i gruppi di disponibilità del database

È possibile utilizzare le funzionalità nella tabella seguente per aggiungere, rimuovere e configurare le impostazioni per i gruppi di disponibilità del database (DAG).

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
<td><p>Appartenenza al gruppo di disponibilità del database</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Ruolo i gruppi di disponibilità del database</a></p></td>
</tr>
<tr class="even">
<td><p>Proprietà del gruppo di disponibilità del database</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Ruolo i gruppi di disponibilità del database</a></p></td>
</tr>
<tr class="odd">
<td><p>Gruppi di disponibilità del database</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Ruolo i gruppi di disponibilità del database</a></p></td>
</tr>
<tr class="even">
<td><p>Reti di disponibilità del database</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Ruolo i gruppi di disponibilità del database</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni per la copia del database delle cassette postali

È possibile utilizzare le funzionalità nella tabella seguente per aggiungere, rimuovere, aggiornare e attivare le copie del database delle cassette postali.


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
<td><p>Passaggio di database</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="databases-role-exchange-2013-help.md">Ruolo del database</a></p></td>
</tr>
<tr class="even">
<td><p>Copie del database delle cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">Ruolo delle copie del database</a></p></td>
</tr>
<tr class="odd">
<td><p>Passaggio di server</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="databases-role-exchange-2013-help.md">Ruolo del database</a></p></td>
</tr>
<tr class="even">
<td><p>Aggiornamento di una copia del database delle cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">Ruolo delle copie del database</a></p></td>
</tr>
</tbody>
</table>


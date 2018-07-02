---
title: 'Autorizzazioni dei destinatari: Exchange 2013 Help'
TOCTitle: Autorizzazioni dei destinatari
ms:assetid: 5b690bcb-c6df-4511-90e1-08ca91f43b37
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638132(v=EXCHG.150)
ms:contentKeyID: 50480759
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autorizzazioni dei destinatari

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Le autorizzazioni richieste per eseguire le attività di gestione dei destinatari dipendono dalla procedura utilizzata o dal cmdlet che si intende eseguire.

Per individuare le autorizzazioni necessarie per eseguire la procedura o il cmdlet, procedere come segue:

1.  Nella tabella seguente individuare la funzionalità più pertinente alla procedura o al cmdlet che si vuole eseguire.

2.  Esaminare quindi le autorizzazioni necessarie per la funzionalità. È necessario ricevere l'assegnazione di uno di questi gruppi di ruoli, di un gruppo di ruoli personalizzato equivalente o di un ruolo di gestione equivalente. È inoltre possibile fare clic su un gruppo di ruoli per visualizzarne i ruoli di gestione. Se per una determinata funzionalità sono elencati più gruppi di ruoli, per usarla è necessario essere assegnati a uno di questi gruppi. Per altre informazioni sui gruppi di ruoli e sui ruoli di gestione, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

3.  A questo punto, eseguire il cmdlet **Get-ManagementRoleAssignment** per individuare i gruppi di ruoli o i ruoli di gestione a cui si è assegnati e verificare se si dispone delle autorizzazioni necessarie per gestire la funzionalità.
    

    > [!NOTE]
    > Per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG> è necessario ricevere l'assegnazione del ruolo di gestione dei ruoli. Se non si hanno le autorizzazioni per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, chiedere all'amministratore di Exchange di recuperare i gruppi di ruoli o i ruoli di gestione assegnati.



Se si desidera delegare la gestione di una funzionalità a un altro utente, vedere [Delegare le assegnazioni di ruolo](delegate-role-assignments-exchange-2013-help.md).

## Autorizzazioni per il server Cassette postali

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
<td><p>Ripristino del calendario, configurazione del server</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Delega dei server Cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Criteri degli indirizzi di posta elettronica</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Ricerca di Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Ricerca – diagnostica</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p>
<p>Ruolo Support Diagnostics</p>

> [!NOTE]
> Il ruolo Support Diagnostics non viene assegnato a un gruppo di ruoli. Per ulteriori informazioni, vedere <A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">Aggiungere un ruolo di un utente o gruppo di protezione universale</A>.


</td>
</tr>
<tr class="even">
<td><p>Metrica del gruppo</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Importazione/esportazione</p></td>
<td><p>Ruolo di importazione\esportazione delle cassette postali</p>

> [!NOTE]
> Il ruolo di importazione\esportazione delle cassette postali non viene assegnato a un gruppo di ruoli. Per ulteriori informazioni, vedere <A href="mailbox-import-export-role-exchange-2013-help.md">Ruolo di importazione\esportazione delle cassette postali</A>.


</td>
</tr>
<tr class="even">
<td><p>Assistenti cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Spostamenti delle cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Ripristino della cassetta postale</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Richiesta di riparazione delle cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Richiesta di ripristino delle cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurazione del server Cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Gestione del servizio di indicizzazione ricerca di Exchange su un server delle cassette postali</p></td>
<td><p>Amministratore locale sul server delle cassette postali</p></td>
</tr>
<tr class="odd">
<td><p>Connettività MAPI</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Directory virtuali della rubrica offline</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Rimozione delle cassette postali di archiviazione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni per la condivisione e il calendario

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
<td><p>Configurazione del calendario</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="even">
<td><p>Diagnostica del calendario</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p>
<p><a href="compliance-management-exchange-2013-help.md">Gestione della conformità</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="odd">
<td><p>Elaborazione del calendario</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="even">
<td><p>Notifiche</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Relazioni dell'organizzazione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Criteri di condivisione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni per la configurazione della cassetta postale delle risorse

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
<td><p>Criteri di prenotazione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="even">
<td><p>Delega</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurazione dello schema delle cassette postali per la risorsa</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni per il database delle cassette postali

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
<td><p>Database delle cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni di provisioning dei destinatari

Questa tabella contiene le varie autorizzazioni necessarie per gestire i destinatari.

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
<td><p>Elenco di indirizzi, elenco indirizzi globale</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Protezione da posta indesiderata</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>App per Outlook</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="even">
<td><p>Applicazione dei criteri di condivisione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Arbitraggio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Connessione dell'archivio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Assegnazione delle rubriche offline</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Risposte automatiche</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurazione del calendario</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Ripristino del calendario</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Impostazioni di aggregazione contatti</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Cassette postali disconnesse</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="odd">
<td><p>Gruppi di distribuzione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Gruppi di distribuzione dinamici</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Indirizzi di posta elettronica</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestione messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p>Regole di Posta in arrivo</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="odd">
<td><p>Contatti di posta</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Suggerimenti per la posta</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Utente di posta</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni per le cartelle delle cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="odd">
<td><p>Cartelle delle cassette postali</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Connettività MAPI</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Configurazione dei messaggi</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="even">
<td><p>Quote dei messaggi</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Moderazione</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni e delega</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Cassette postali di archivio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Proprietà dei dati del destinatario</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Cassette postali remote</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Conservazione e conservazione legale</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="records-management-exchange-2013-help.md">Gestione record</a></p></td>
</tr>
<tr class="odd">
<td><p>Invia come</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Configurazione del controllo ortografia</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
<tr class="odd">
<td><p>Messaggistica unificata</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="um-management-exchange-2013-help.md">Gestione messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p>Cassette postali degli utenti</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Foto utente</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="help-desk-exchange-2013-help.md">Assistenza</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni per lo spostamento e la migrazione delle cassette postali

La tabella contiene le autorizzazioni necessarie per spostare le cassette postali locali in domini o foreste diversi e per effettuare le migrazione delle cassette postali locali da e verso l'organizzazione basata su cloud.


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
<td><p>Spostamento delle cassette postali (locale o tra foreste)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Spostamento delle cassette postali (distribuzione ibrida)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Migrazione (on-boarding e off-boarding dal cloud)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
</tbody>
</table>


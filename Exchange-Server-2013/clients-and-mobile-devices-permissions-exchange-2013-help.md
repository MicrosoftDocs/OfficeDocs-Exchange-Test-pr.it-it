---
title: 'Autorizzazioni per client e dispositivi mobili: Exchange 2013 Help'
TOCTitle: Autorizzazioni per client e dispositivi mobili
ms:assetid: 57eca42a-5a7f-4c65-89f0-7a84f2dbea19
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638131(v=EXCHG.150)
ms:contentKeyID: 50480702
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autorizzazioni per client e dispositivi mobili

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-11-10_

Le autorizzazioni richieste per eseguire attività su client e dispositivi mobili dipendono dalla procedura in esecuzione o dal cmdlet che si intende eseguire. Per ulteriori informazioni sulle funzionalità per client e dispositivi mobili, vedere [Client e dispositivi mobili](clients-and-mobile-exchange-2013-help.md).

Per individuare le autorizzazioni necessarie per eseguire la procedura o il cmdlet, procedere come segue:

1.  Nella tabella seguente individuare la funzionalità più pertinente alla procedura o al cmdlet che si vuole eseguire.

2.  Esaminare quindi le autorizzazioni necessarie per la funzionalità. È necessario ricevere l'assegnazione di uno di questi gruppi di ruoli, di un gruppo di ruoli personalizzato equivalente o di un ruolo di gestione equivalente. È inoltre possibile fare clic su un gruppo di ruoli per visualizzarne i ruoli di gestione. Se per una determinata funzionalità sono elencati più gruppi di ruoli, per usarla è necessario essere assegnati a uno di questi gruppi. Per altre informazioni sui gruppi di ruoli e sui ruoli di gestione, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

3.  A questo punto, eseguire il cmdlet **Get-ManagementRoleAssignment** per individuare i gruppi di ruoli o i ruoli di gestione a cui si è assegnati e verificare se si dispone delle autorizzazioni necessarie per gestire la funzionalità.
    

    > [!NOTE]
    > Per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG> è necessario ricevere l'assegnazione del ruolo di gestione dei ruoli. Se non si hanno le autorizzazioni per eseguire il cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, chiedere all'amministratore di Exchange di recuperare i gruppi di ruoli o i ruoli di gestione assegnati.



Se si desidera delegare la gestione di una funzionalità a un altro utente, vedere [Delegare le assegnazioni di ruolo](delegate-role-assignments-exchange-2013-help.md).


> [!NOTE]
> È possibile che per alcune funzionalità siano necessarie le autorizzazioni dell'amministratore locale sul server che si vuole gestire. Per gestire queste funzionalità, è necessario essere membro del gruppo Administrators locale su quel server.



## Autorizzazioni del server Accesso client

È possibile configurare le seguenti funzionalità per il server Accesso client.

Gli utenti a cui viene assegnato il gruppo di ruoli di gestione in sola visualizzazione possono visualizzare la configurazione delle funzionalità nella tabella seguente. Per altre informazioni, vedere Gestione dell'organizzazione in sola visualizzazione[Gestione organizzazione sola visualizzazione](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Autorizzazioni richieste</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Impostazioni di array del server Accesso client</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni del server Accesso client</p></td>
<td><p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Impostazioni del canale di posta elettronica del servizio Accesso client</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni utente di Accesso client</p></td>
<td><p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Impostazioni della directory virtuale accesso client</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni di Accesso client RPC</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Le impostazioni del proxy di notifiche di push</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni di reindirizzamento dell'autenticazione OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni di Exchange ActiveSync

È possibile configurare quanto segue per Exchange ActiveSync.

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
<td><p>Exchange ActiveSync Impostazioni di blocco automatico</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni del criterio cassetta postale di Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Impostazioni del server Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni di Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Impostazioni utente di Exchange ActiveSync</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni della directory virtuale di Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Impostazioni dei criteri cassetta postale per i dispositivi mobili</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni utente per dispositivi mobili</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni del servizio di individuazione automatica

È possibile configurare quanto segue per il servizio di individuazione automatica.

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
<td><p>Impostazioni di configurazione del servizio di individuazione automatica</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Installazione delegata</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni della directory virtuale del servizio di individuazione automatica</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni del servizio Disponibilità

È possibile configurare quanto segue per il servizio Disponibilità.

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
<td><p>Impostazioni dello spazio degli indirizzi del servizio Disponibilità</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni di configurazione del servizio Disponibilità</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni della limitazione delle richieste client

È possibile configurare quanto segue per la limitazione delle richieste client.

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
<td><p>Impostazioni della limitazione delle richieste client</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni di Servizi Web Exchange

È possibile configurare quanto segue per le directory virtuali di Servizi Web.

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
<td><p>Impostazioni della directory virtuale di Servizi Web Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Verifica di Servizi Web Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Verifica di Servizi Web di Outlook</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni di Outlook Anywhere

È possibile configurare e gestire le seguenti impostazioni per Outlook Anywhere.

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
<td><p>Configurazione di Outlook Anywhere (abilitazione, disabilitazione, modifica, visualizzazione)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Installazione delegata</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p></td>
</tr>
<tr class="even">
<td><p>Componente proxy RPC su HTTP</p></td>
<td><p>Amministratore del server locale</p></td>
</tr>
<tr class="odd">
<td><p>Verifica della connettività di Outlook Anywhere</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni di Outlook Web App

È possibile utilizzare le funzionalità seguenti per visualizzare le impostazioni di Outlook Web App, controllare la sicurezza e l'accesso utente a Outlook Web App e verificare la connettività di Outlook Web App.

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
<td><p>Editor di grafica</p></td>
<td><p>Amministratore del server locale</p></td>
</tr>
<tr class="even">
<td><p>Gestione IIS</p></td>
<td><p>Amministratore del server locale</p></td>
</tr>
<tr class="odd">
<td><p>ISA Server 2006</p></td>
<td><p>Amministratore di ISA Server Enterprise</p></td>
</tr>
<tr class="even">
<td><p>Criteri cassetta postale di Outlook Web App</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Directory virtuali di Outlook Web App</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p></td>
</tr>
<tr class="even">
<td><p>Editor del Registro di sistema</p></td>
<td><p>Amministratore del server locale</p></td>
</tr>
<tr class="odd">
<td><p>Configurazione S/MIME</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Editor di testo</p></td>
<td><p>Amministratore del server locale</p></td>
</tr>
<tr class="odd">
<td><p>Visualizzazione dei criteri cassetta postale di Outlook Web App</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Installazione delegata</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gestione di Hygiene</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni POP3 e IMAP4

È possibile configurare quanto segue per POP3 e IMAP4.

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
<td><p>Impostazioni IMAP4</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni POP3</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
</tr>
<tr class="odd">
<td><p>Verifica delle impostazioni IMAP4</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Verifica delle impostazioni POP3</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p>
<p><a href="server-management-exchange-2013-help.md">Server Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gestione organizzazione sola visualizzazione</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni della directory virtuale di Windows PowerShell

È possibile configurare quanto segue per Windows PowerShell.

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
<td><p>Prova di Windows PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni di Windows PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gestione organizzazione</a></p></td>
</tr>
</tbody>
</table>


## Autorizzazioni della messaggistica di testo

È possibile configurare quanto segue per la messaggistica di testo.

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
<td><p>Impostazioni di notifica della messaggistica di testo</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="even">
<td><p>Impostazioni della messaggistica di testo</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Gestione destinatari</a></p></td>
</tr>
<tr class="odd">
<td><p>Impostazioni utente della messaggistica di testo</p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">Ruolo MyTextMessaging</a></p>
<p>Gli utenti possono configurare le impostazioni di messaggistica di testo nella propria cassetta postale. Gli amministratori non possono configurare le impostazioni di messaggistica di testo nella cassetta postale di un altro utente.</p></td>
</tr>
</tbody>
</table>


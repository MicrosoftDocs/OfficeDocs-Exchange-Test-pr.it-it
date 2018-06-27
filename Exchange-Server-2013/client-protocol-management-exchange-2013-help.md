---
title: 'Gestione dei protocolli client: Exchange 2013 Help'
TOCTitle: Gestione dei protocolli client
ms:assetid: 89ba6d24-d1d3-46d5-a0ae-61f0d4c6df21
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657727(v=EXCHG.150)
ms:contentKeyID: 50481104
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione dei protocolli client

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Gestione dei protocolli client Exchange ActiveSync, Outlook Web App, POP3, IMAP4, il servizio di individuazione automatica, servizi Web Exchange e il servizio disponibilità viene generato in tre aree diverse: l'interfaccia di amministrazione di Exchange (EAC), Exchange Management Shell e Gestione Internet Information Services (IIS). Le impostazioni che vengono gestite in ogni punto variano per ogni protocollo client.

## Gestione delle impostazioni di Outlook Web App

La maggior parte delle impostazioni da applicare le caratteristiche di Outlook Web App sono disponibili per gli utenti possono essere impostata nella directory virtuale di Outlook Web App o possono essere configurata in un criterio cassetta postale di Outlook Web App. Utilizzando i criteri cassetta postale di Outlook Web App, è possibile definire le caratteristiche disponibili per singoli utenti. Impostazioni dei criteri cassetta postale per ignorare le impostazioni della directory virtuale. Per ulteriori informazioni sulla gestione di Outlook Web App, vedere [Outlook Web App](outlook-web-app-exchange-2013-help.md).

## Gestione delle impostazioni di Exchange ActiveSync

In Exchange 2010, tutti i protocolli di accesso client sono stati implementati e gestiti in un singolo server role, il ruolo del server Accesso Client. Gestione dei protocolli è stata eseguita su una singola istanza di IIS, si è verificato un oggetto unica directory virtuali in Active Directory per ogni protocollo client e un singolo set di cmdlet utilizzati per configurare la directory virtuale.

In Exchange 2013, la gestione dei protocolli client di Exchange ActiveSync è suddivisa tra il server Accesso Client e il server cassette postali. Questa modifica architettura, è possibile eseguire le attività di gestione delle diverse directory virtuali nel server Accesso Client e il server cassette postali. Se questi due server non sono installati nello stesso computer fisico, i parametri utilizzati con la directory virtuale cmdlet verranno modificato basato sul ruolo del server in cui vengono eseguiti.

Per ulteriori informazioni sulle modifiche all'architettura in Exchange 2013, vedere [Novità di Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).

Esistono due tipi di impostazioni che possono essere applicate alla directory virtuale di Exchange ActiveSync:

  - Impostazioni disponibili per la sessione di cassette postali

  - Impostazioni disponibili per il server e la directory virtuale

Le impostazioni che si applicano alla sessione di cassette postali sono le impostazioni della sessione utente. Quando un utente si connette a un server Accesso Client, la connessione è inoltrata al server cassette postali contenente cassetta postale dell'utente. Un identificatore univoco della directory virtuale è incluso nella richiesta tramite proxy. Quindi, il server cassette postali consente di recuperare le impostazioni della directory virtuale da Active Directory e li applica alla sessione. Le impostazioni della directory virtuale sono memorizzate nella cache nel server cassette postali per migliorare le prestazioni.

Se la connessione è inoltrata a un altro sito Active Directory, le impostazioni della directory virtuale verranno caricate dal server Accesso Client nello stesso sito del server cassette postali, non dal server Accesso Client in cui la connessione ha avuto origine.

Nelle tabelle seguenti indicano le impostazioni della directory virtuale possono essere gestite nei diversi server. Se si tenta di gestire un'impostazione specifica in un server per cui non è applicabile, si riceverà un messaggio di errore che indica che la proprietà che si desidera impostare è di sola lettura per il server che si opera in.

**Impostazioni della directory virtuale sul server Accesso Client Exchange ActiveSync**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione</th>
<th>Server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BadItemReportingEnabled</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>BasicAuthEnabled</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>ClientCertAuth</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>CompressionEnabled</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthenticationMethods</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>ExternalURL</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>InternalAuthenticationMethods</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>InternalURL</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertificateAuthorityURL</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>MobileClientCertificateProvisioningEnabled</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertTemplateName</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsActionForUnknownServers</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsAllowedServers</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsBlockedServers</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsInternalDomainSuffixList</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>SendWatsonReport</p></td>
<td><p>Accesso client</p></td>
</tr>
</tbody>
</table>


**Impostazioni della directory virtuale di Exchange ActiveSync sul server Accesso Client e cassette postali**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione</th>
<th>Server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ApplicationRoot</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="even">
<td><p>AppPoolID</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="odd">
<td><p>MetabasePath</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="even">
<td><p>Nome</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="odd">
<td><p>Percorso</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="even">
<td><p>ProxySubVdir</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="odd">
<td><p>VirtualDirectoryName</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="even">
<td><p>WebsiteName</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
</tbody>
</table>


## Gestione delle impostazioni POP3 e IMAP4

In Exchange 2013, l'implementazione dei protocolli POP3 e IMAP4 è stata segmentata anche tra l'accesso Client e ruoli del server cassette postali. Per la nuova implementazione connettività POP3 e IMAP4 ogni gestiti da un servizio sul server Accesso Client, nonché da un servizio sul server cassette postali. I nomi dei servizi in esecuzione sul server Accesso Client sono gli stessi nomi esistente in Exchange 2010: servizio IMAP4 di Microsoft Exchange e servizi POP3. I nomi dei due nuovi servizi in esecuzione nel server cassette postali sono il servizio Microsoft Exchange IMAP4 back-end e il servizio Microsoft Exchange POP3 back-end.

Per la gestione di connettività POP3 e IMAP4 all'interno dell'organizzazione, considerare quanto segue:

  - Se si esegue il ruolo del server Accesso Client e il ruolo del server cassette postali nello stesso computer, le modifiche apportate alle impostazioni POP3 o IMAP4 vengono applicate automaticamente ai servizi POP3 e IMAP4 corretti.

  - Se si esegue il ruolo del server Accesso Client e il ruolo del server cassette postali in computer distinti, è necessario gestire le impostazioni nel computer utilizzato per gestire l'impostazione che si desidera modificare.

Utilizzare che le tabelle seguenti indicano quali impostazioni POP/IMAP ogni ruolo del server.

**Impostazioni POP3 e IMAP4 sul server Accesso Client**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione</th>
<th>Server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AuthenticatedConnectionTimeout</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>Banner</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>ExternalConnectionSettings</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>InternalConnectionSettings</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>MaxCommandSize</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionFromSingleIP</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>MaxConnections</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionsPerUser</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="odd">
<td><p>PreAuthenticatedConnectionTimeout</p></td>
<td><p>Accesso client</p></td>
</tr>
<tr class="even">
<td><p>UnencryptedOrTLSBindings</p></td>
<td><p>Accesso client</p></td>
</tr>
</tbody>
</table>


**Impostazioni POP3 e IMAP4 sul server cassette postali**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione</th>
<th>Server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CalendarItemRetrivalOption</p></td>
<td><p>Mailbox</p></td>
</tr>
<tr class="even">
<td><p>EnableExactRFC822Size</p></td>
<td><p>Mailbox</p></td>
</tr>
<tr class="odd">
<td><p>MessageRetrievalSortOrder</p></td>
<td><p>Mailbox</p></td>
</tr>
<tr class="even">
<td><p>OWAServerURL</p></td>
<td><p>Mailbox</p></td>
</tr>
<tr class="odd">
<td><p>ProxyTargetPort</p></td>
<td><p>Mailbox</p></td>
</tr>
<tr class="even">
<td><p>ShowHiddenFoldersEnabled</p></td>
<td><p>Mailbox</p></td>
</tr>
<tr class="odd">
<td><p>SuppressReadReceipt</p></td>
<td><p>Mailbox</p></td>
</tr>
</tbody>
</table>


**Impostazioni POP3 e IMAP4 sul server Accesso Client e cassette postali**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione</th>
<th>Server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="even">
<td><p>EnforceCertificateErrors</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="odd">
<td><p>LogFileLocation</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="even">
<td><p>LogFileRolloverSettings</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="odd">
<td><p>LoginType</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="even">
<td><p>LogPerFileSizeQuota</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="odd">
<td><p>ProotocolLogEnabled</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="even">
<td><p>Server</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>Cassette postali e accesso client</p></td>
</tr>
</tbody>
</table>


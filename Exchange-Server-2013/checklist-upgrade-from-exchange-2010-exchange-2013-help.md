---
title: 'Elenco di controllo: aggiornamento da Exchange 2010: Exchange 2013 Help'
TOCTitle: 'Elenco di controllo: aggiornamento da Exchange 2010'
ms:assetid: 06c1045a-5fcf-4e24-a901-1a979302fb8d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee332309(v=EXCHG.150)
ms:contentKeyID: 51407333
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Elenco di controllo: aggiornamento da Exchange 2010

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-07_

Utilizzare questo elenco di controllo per l'aggiornamento da Microsoft Exchange 2010 a Exchange 2013. Prima di iniziare a utilizzare questo elenco di controllo, assicurarsi che si ha familiarità con i concetti illustrati in:

  - [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Novità di Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md)

Questo elenco di controllo è generico e fornisce le istruzioni per un tipico scenario di aggiornamento.


> [!NOTE]
> L'Assistente per la distribuzione di Exchange fornisce una guida personalizzata dettagliata alla distribuzione di Exchange Server. L'Assistente per la distribuzione facilita la distribuzione di una nuova installazione di Exchange Server 2013, l'aggiornamento da una versione precedente a Exchange 2013 o la configurazione di una distribuzione ibrida di Exchange 2013 ed Exchange Online. Per ulteriori informazioni, vedere <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistente per la distribuzione di Exchange Server</A>.



## Elenco di controllo per l'aggiornamento da Exchange 2010 a Exchange 2013


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Operazioni completate</p></td>
<td><p>Attività</p></td>
<td><p>Argomenti</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. Leggere le note sulla versione.</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Note sulla versione di Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>2. Verificare i requisiti di sistema</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisiti di sistema di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>3. Verificare che siano stati eseguiti i passaggi preliminari richiesti</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Prerequisiti di Exchange 2013</a></p>
<p><a href="deployment-security-checklist-exchange-2013-help.md">Checklist della distribuzione di protezione</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>4. Configurare lo spazio dei nomi non contiguo</p>

> [!NOTE]
> Questo passaggio è facoltativo. È necessario effettuarlo soltanto se l'organizzazione sta eseguendo uno spazio nomi non contiguo.


</td>
<td><p><a href="configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md">Configurare l'elenco ricerca suffissi DNS per un spazio dei nomi disgiunto</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5. Selezionare una rubrica offline per tutti i database delle cassette postali di Exchange 2010</p></td>
<td><p><a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Set mailbox database properties</a> in <a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Gestire il database delle cassette postali in Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>6. Installare Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installazione di Exchange 2013 utilizzando l'installazione guidata</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Installazione del ruolo Trasporto Edge di Exchange 2013 tramite l'installazione guidata</a></p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Verificare un'installazione di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. Creare una cassetta postale di Exchange 2013</p></td>
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">Creazione di cassette postali utente</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Configurare le directory virtuali di Exchange</p>

> [!NOTE]
> Questo passaggio è necessario se si desidera utilizzare Exchange Web Services, Outlook via Internet oppure la rubrica offline. Inoltre, potrebbe essere necessario se si deve modificare una delle impostazioni predefinite per il Pannello di controllo di Exchange, Microsoft Office&nbsp;Outlook Web App oppure Exchange ActiveSync.<BR>


</td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configurazione del server Accesso client di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Aggiungere certificati digitali al server Accesso client</p></td>
<td><p><a href="digital-certificates-and-ssl-exchange-2013-help.md">Certificati digitali e SSL</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. Spostare la cassetta postale di arbitraggio</p></td>
<td><p><a href="move-the-exchange-2010-system-mailbox-to-exchange-2013-exchange-2013-help.md">Spostare la cassetta postale di sistema di Exchange 2010 in Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Configurare la messaggistica unificata</p>

> [!NOTE]
> Questo passaggio è facoltativo. È necessario effettuarlo soltanto se si desidera utilizzare la funzionalità di messaggistica unificata nella propria organizzazione.


</td>
<td><p><a href="upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md">Aggiornamento dalla messaggistica unificata di Exchange 2007 alla messaggistica unificata di Exchange 2010</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>12. Configurare server Trasporto Edge</p>

> [!NOTE]
> Questo passaggio è facoltativo. È necessario solo se l'organizzazione utilizza un server Trasporto Edge.


</td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">Configurazione del flusso della posta Internet tramite un server Trasporto Edge sottoscritto</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>13. Abilitare e configurare Outlook via Internet</p></td>
<td><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook via Internet</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>14. Configurare il punto di connessione del servizio</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configurazione del server Accesso client di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. Configurare i record DNS</p></td>
<td><p><a href="https://technet.microsoft.com/it-it/library/dn307232(v=exchg.150)">Configurare i record DNS per l'installazione di Exchange 2010 su più server</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>16. spostare le cassette postali da Exchange 2010 a Exchange 2013</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Spostamenti di cassette postali di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>17. Spostare i dati delle cartelle pubbliche da Exchange 2013 a Exchange 2013</p></td>
<td><p><a href="public-folders-exchange-2013-help.md">Cartelle pubbliche</a></p>
<p><a href="https://technet.microsoft.com/it-it/library/jj150486(v=exchg.150)">Utilizzo della migrazione seriale per spostare le cartelle pubbliche in Exchange 2013 dalle versioni precedenti</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>18. Attività di post-installazione</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Attività successive all'installazione di Exchange 2013</a></p></td>
</tr>
</tbody>
</table>


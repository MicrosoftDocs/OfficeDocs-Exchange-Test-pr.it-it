---
title: 'Elenco di controllo: Aggiornamento da Exchange 2007: Exchange 2013 Help'
TOCTitle: 'Elenco di controllo: Aggiornamento da Exchange 2007'
ms:assetid: 53aaa370-4562-43e4-9b75-7a705400c5a5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff805032(v=EXCHG.150)
ms:contentKeyID: 51407373
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Elenco di controllo: Aggiornamento da Exchange 2007

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Utilizzare questo elenco di controllo per un aggiornamento da Microsoft Exchange Server 2007 a Exchange Server 2013. Prima di iniziare a lavorare con questo elenco di controllo, verificare di disporre delle nozioni di base illustrate in:

  - [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Novità di Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md)

Questo elenco di controllo è generico e fornisce le istruzioni per un tipico scenario di aggiornamento.


> [!NOTE]
> L'Assistente per la distribuzione di Exchange fornisce una guida personalizzata dettagliata alla distribuzione di Exchange Server. L'Assistente per la distribuzione facilita la distribuzione di una nuova installazione di Exchange Server 2013, l'aggiornamento da una versione precedente a Exchange 2013 o la configurazione di una distribuzione ibrida di Exchange 2013 ed Exchange Online. Per ulteriori informazioni, vedere <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistente per la distribuzione di Exchange Server</A>.



## Elenco di controllo per l'aggiornamento da Exchange 2007 a Exchange 2013


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
<td><p>Argomento/i</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. Leggere le note di rilascio.</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Note sulla versione di Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>2. Verificare i requisiti del sistema</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisiti di sistema di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. Verificare che siano stati eseguiti i passaggi preliminari richiesti</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Prerequisiti di Exchange 2013</a></p>
<p><a href="deployment-security-checklist-exchange-2013-help.md">Checklist della distribuzione di protezione</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. Configurare lo spazio dei nomi non contiguo</p>

> [!NOTE]
> Questo passaggio è facoltativo. È necessario solo se l'organizzazione sta eseguendo uno spazio nomi non contiguo.


</td>
<td><p><a href="configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md">Configurare l'elenco ricerca suffissi DNS per un spazio dei nomi disgiunto</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5. Selezionare una rubrica offline per tutti i database delle cassette postali di Exchange 2007</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/?linkid=320546">Download come effettuare il provisioning dei destinatari per la Rubrica Offline</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>6. Creare il nome host Exchange legacy</p></td>
<td><p><a href="https://technet.microsoft.com/it-it/library/dn130105(v=exchg.150)">Creazione di un nome host Exchange legacy</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>7. Installare Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installazione di Exchange 2013 utilizzando l'installazione guidata</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Installazione del ruolo Trasporto Edge di Exchange 2013 tramite l'installazione guidata</a></p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Verificare un'installazione di Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Creare una cassetta postale di Exchange 2013</p></td>
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">Creazione di cassette postali utente</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Configurare le directory virtuali di Exchange</p>

> [!NOTE]
> Questo passaggio è necessario se si desidera utilizzare Exchange Web Services, Outlook tramite Internet oppure la Rubrica offline. Inoltre, potrebbe essere necessario se si deve modificare una delle impostazioni predefinite per il Pannello di controllo di Exchange, Microsoft OfficeOutlook Web App oppure Exchange ActiveSync.<BR>


<p></p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configurazione del server Accesso client di Exchange 2013</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>10. Configurare i certificati di Exchange 2013</p></td>
<td><p><a href="digital-certificates-and-ssl-exchange-2013-help.md">Certificati digitali e SSL</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Configurare i certificati di Exchange 2007</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/?linkid=320553">Gestione di SSL per un Server accesso Client</a></p></td>
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
<td> </td>
<td><p>13. Configurare la messaggistica unificata</p>

> [!NOTE]
> Questo passaggio è facoltativo. È necessario solo se si desidera utilizzare Messaggistica Unificata nella propria organizzazione.


</td>
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">Pianificazione per la messaggistica unificata</a></p>
<p><a href="deploy-exchange-2013-um-exchange-2013-help.md">Distribuzione della messaggistica unificata di Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>14. Abilitare e configurare Outlook via Internet</p></td>
<td><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook via Internet</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. Configurare il punto di connessione del servizio</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configurazione del server Accesso client di Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>16. Configurare gli URL di Exchange 2007</p></td>
<td><p><a href="https://technet.microsoft.com/it-it/library/dn282262(v=exchg.150)">Configurare gli URL esterni di Exchange 2007</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>17. Configurare i record DNS</p></td>
<td><p><a href="https://technet.microsoft.com/it-it/library/dn283988(v=exchg.150)">Configurare i record DNS per l'installazione di Exchange 2007 su più server</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>18. Spostare le cassette postali da Exchange 2007 a Exchange 2013</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Spostamenti di cassette postali di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>19. Spostare i dati delle cartelle pubbliche da Exchange 2013 a Exchange 2013</p>

> [!NOTE]
> Questo passaggio è facoltativo. È necessario solo se l'organizzazione utilizza cartelle pubbliche.


</td>
<td><p><a href="public-folders-exchange-2013-help.md">Cartelle pubbliche</a></p>
<p><a href="https://technet.microsoft.com/it-it/library/jj150486(v=exchg.150)">Utilizzo della migrazione seriale per spostare le cartelle pubbliche in Exchange 2013 dalle versioni precedenti</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>20. Attività di post-installazione</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Attività successive all'installazione di Exchange 2013</a></p></td>
</tr>
</tbody>
</table>


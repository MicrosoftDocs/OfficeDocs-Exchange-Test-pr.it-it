---
title: 'Elenco di controllo: Eseguire una nuova installazione di Exchange 2013: Exchange 2013 Help'
TOCTitle: 'Elenco di controllo: Eseguire una nuova installazione di Exchange 2013'
ms:assetid: f70d9dd3-7370-472e-b05e-1ea1671272b2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff805042(v=EXCHG.150)
ms:contentKeyID: 50482052
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Elenco di controllo: Eseguire una nuova installazione di Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Utilizzare questo elenco di controllo per la distribuzione di Microsoft Exchange Server 2013. Prima di iniziare a utilizzare l'elenco di controllo, è necessario acquisire una certa familiarità con i concetti generali illustrati negli argomenti seguenti:

  - [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Checklist della distribuzione di protezione](deployment-security-checklist-exchange-2013-help.md)

Questo elenco di controllo è generico in quanto fornisce istruzioni riguardanti uno scenario tipico.


> [!NOTE]
> L'Assistente per la distribuzione di Exchange fornisce una guida personalizzata dettagliata alla distribuzione di Exchange Server. L'Assistente per la distribuzione facilita la distribuzione di una nuova installazione di Exchange Server 2013, l'aggiornamento da una versione precedente a Exchange 2013 o la configurazione di una distribuzione ibrida di Exchange 2013 ed Exchange Online. Per ulteriori informazioni, vedere <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistente per la distribuzione di Exchange Server</A>.



## Elenco di controllo per una nuova installazione di Exchange 2013


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
<td><p>Argomento</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. Leggere le note di rilascio.</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Note sulla versione di Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>2. Verificare i requisiti di sistema.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisiti di sistema di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. Verificare che siano stati eseguiti i passaggi preliminari richiesti.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Prerequisiti di Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. Configurare lo spazio dei nomi non contiguo.</p>

> [!NOTE]
> Questo passaggio è facoltativo. È necessario solo se sull'organizzazione è in esecuzione uno spazio dei nomi non contiguo.


</td>
<td><p><a href="disjoint-namespace-scenarios-exchange-2013-help.md">Scenari di spazio dei nomi disgiunto</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>5. Installare il ruolo del server Cassette postali.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installazione di Exchange 2013 utilizzando l'installazione guidata</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>6. Installare il ruolo del server Accesso client.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installazione di Exchange 2013 utilizzando l'installazione guidata</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. Installare il ruolo del server Trasporto Edge.</p>

> [!NOTE]
> Questo passaggio è facoltativo. È necessario soltanto se si desidera installare un server Trasporto Edge. Per ulteriori informazioni, vedere <A href="edge-transport-servers-exchange-2013-help.md">Server Trasporto Edge</A>.


</td>
<td><p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Installazione del ruolo Trasporto Edge di Exchange 2013 tramite l'installazione guidata</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Creare una sottoscrizione di EdgeSync</p>
<p>Questo passaggio è facoltativo. È necessario soltanto se è stato installato un server Trasporto Edge e si desidera configurare una sottoscrizione di EdgeSync tra il server Trasporto Edge e il server Trasporto Hub. Per ulteriori informazioni, vedere <a href="edge-subscriptions-exchange-2013-help.md">Sottoscrizioni Edge</a>.</p></td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">Configurazione del flusso della posta Internet tramite un server Trasporto Edge sottoscritto</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Configurare il trasporto.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 1: Create a Send connector</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. Aggiungere domini accettati aggiuntivi.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 2: Add additional accepted domains</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Configurare i criteri degli indirizzi di posta elettronica.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 3: Configure the default email address policy</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>12. Configurare le impostazioni delle directory virtuali, inclusa la rubrica offline, i servizi Web di Exchange, l'interfaccia di amministrazione di Exchange (EAC), Outlook Web App e le directory virtuali di Exchange ActiveSync.</p>

> [!NOTE]
> Questo passaggio è necessario per utilizzare Servizi Web Exchange, Outlook via Internet o la rubrica offline. Può anche essere necessario per modificare una delle impostazioni predefinite dell'interfaccia di amministrazione di Exchange, Outlook Web App o Exchange ActiveSync.


</td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 4: Configure external URLs</a></p>
<p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 5: Configure internal URLs</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>13. Aggiungere certificati digitali al server Accesso client.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 6: Configure an SSL certificate</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>14. Configurare la messaggistica unificata</p>

> [!NOTE]
> Questo passaggio è facoltativo. È necessario solo se si desidera utilizzare la messaggistica unificata nell'organizzazione.


</td>
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Distribuzione di segreteria telefonica e messaggistica UNIFICATA</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. Configurare ulteriori impostazioni di messaggistica unificata e Lync Server.</p>

> [!NOTE]
> Questo passaggio è facoltativo. È necessario eseguirlo solo se è stata configurata la messaggistica unificata nell'organizzazione e si desidera integrarla con Lync Server.


</td>
<td><p><a href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">Distribuzione di panoramica della messaggistica UNIFICATA di Exchange 2013 e Lync Server</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>16. Attività di post-installazione.</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Attività successive all'installazione di Exchange 2013</a></p></td>
</tr>
</tbody>
</table>


---
title: 'Elenco contr.: Aggiorna mess. unif. Exchange 2010 a 2013.: Exchange 2013 Help'
TOCTitle: "Elenco di controllo: Effettuare l'aggiornamento della Messaggistica unificata di Exchange 2010 alla Messaggistica unificata di Exchange 2013."
ms:assetid: 799bd1b1-a918-4bd8-911e-e6ca08bd7b52
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn169228(v=EXCHG.150)
ms:contentKeyID: 54652876
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Elenco di controllo: Effettuare l'aggiornamento della Messaggistica unificata di Exchange 2010 alla Messaggistica unificata di Exchange 2013.

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Utilizzare questo elenco di controllo per effettuare l'aggiornamento da Messaggistica unificata di Exchange a Messaggistica unificata di Exchange 2010. Assicurarsi di fare riferimento a queste informazioni quando si esegue l'aggiornamento dell'organizzazione Exchange 2010 e della distribuzione di messaggistica unificata a Exchange 2013. Per istruzioni dettagliate relative all'aggiornamento a Messaggistica unificata di Exchange 2013, vedere [Aggiornamento dalla messaggistica unificata di Exchange 2007 alla messaggistica unificata di Exchange 2010](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md).

Prima di iniziare a lavorare sull'elenco di controllo, è fondamentale conoscere i concetti presentati nelle sezioni:

  - [Pianificazione per la messaggistica unificata](planning-for-unified-messaging-exchange-2013-help.md)

  - [Integrazione del telefono sistema con la messaggistica UNIFICATA](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephone-system-integration-with-um)

  - [Connettere il sistema di segreteria telefonica alla rete telefonica](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/connect-voice-mail-system)

Per istruzioni dettagliate sull'aggiornamento da Messaggistica unificata di Exchange 2010 a Messaggistica unificata di Exchange 2007, vedere [Eseguire l'aggiornamento alla messaggistica UNIFICATA di Exchange 2007 a messaggistica UNIFICATA di Exchange 2013](upgrade-exchange-2007-um-to-exchange-2013-um-exchange-2013-help.md).

## Elenco di controllo per l'aggiornamento da Messaggistica unificata di Exchange 2007 a Messaggistica unificata di Exchange 2010


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Operazioni completate</th>
<th>Attività</th>
<th>Argomento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Distribuzione e configurazione dei componenti di telefonia.</p></td>
<td><p><a href="connect-um-to-your-telephone-system-exchange-2013-help.md">Connettersi alla messaggistica unificata al sistema telefonico in uso</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Prima di eseguire l'installazione di Exchange 2013, rivedere i requisiti di sistema.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisiti di sistema di Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Verificare di disporre dei prerequisiti di installazione.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Prerequisiti di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Installare i server Accesso client e Cassette postali necessari.</p>

> [!WARNING]
> È necessario distribuire un server Cassette postali di Exchange 2013 nell'organizzazione prima di configurare i gateway VoIP e gli IP PBX per inviare il traffico SIP messaggistica unificata e RTP ai server Accesso client di Exchange 2013.


</td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installazione di Exchange 2013 utilizzando l'installazione guidata</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Verificare l'installazione e rivedere i file di registro dell'installazione dei server.</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Verificare un'installazione di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Se necessario, installare i language pack di messaggistica unificata.</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">Installare un Language Pack di messaggistica unificata</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Spostare la cassetta postale di sistema di Exchange 2010 utilizzata per i prompt personalizzati di messaggistica unificata in Exchange 2013.</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Spostamenti di cassette postali di Exchange 2013</a></p>

> [!NOTE]
> Se la cassetta postale di sistema è già stata spostata, è comunque possibile importare/esportare manualmente i prompt personalizzati da Exchange 2010 utilizzando <A href="import-and-export-custom-greetings-announcements-menus-and-prompts-exchange-2013-help.md">Importazione ed esportazione istruzioni, gli annunci, menu e messaggi di saluto personalizzati</A>.


</td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Esportare e importare certificati.</p></td>
<td><p><a href="deploying-certificates-for-um-exchange-2013-help.md">Distribuzione dei certificati per la messaggistica unificata</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configurare la modalità di avvio di messaggistica unificata su tutti i server Accesso client di Exchange 2013.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configurare la modalità di avvio in un server Accesso Client</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurare la modalità di avvio di messaggistica unificata su tutti i server Cassette postali di Exchange 2013.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configurare la modalità di avvio in un server cassette postali</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Creare o configurare i dial plan di messaggistica unificata esistenti.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan">Creazione di un dial plan di messaggistica unificata</a></p>
<p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/manage-um-dial-plan">Gestire un dial plan di messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Creare o configurare i gateway IP di messaggistica unificata esistenti.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway">Creare un gateway IP di messaggistica unificata</a></p>
<p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/manage-um-ip-gateway">Gestire un gateway IP di messaggistica unificata</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Creare un gruppo di risposta di messaggistica unificata.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-hunt-group">Creazione di un gruppo di risposta di messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Creare o configurare gli operatori automatici di messaggistica unificata.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/create-a-um-auto-attendant">Creazione di un operatore automatico di messaggistica unificata</a></p>
<p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/manage-um-auto-attendant">Gestire un operatore automatico di messaggistica unificata</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Creare o configurare i criteri cassetta postale di messaggistica unificata.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy">Creazione di un criterio cassetta postale di messaggistica unificata</a></p>
<p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy">Gestire i criteri cassetta postale di messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Spostare le cassette postali abilitate alla messaggistica unificata esistenti in Exchange 2013.</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Spostamenti di cassette postali di Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Abilitare nuovi utenti alla Messaggistica unificata o configurare le impostazioni per un utente esistente abilitato alla messaggistica unificata.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail">Consentire a un utente per la segreteria telefonica</a></p>
<p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-voice-mail-settings">Gestire le impostazioni della posta vocale di un utente</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurare gateway VoIP, IP PBX e IP-PBX abilitati a SIP all'invio di tutte le chiamate in arrivo ai server Accesso client di Exchange 2013.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways">Note di configurazione per i gateway VoIP, IP PBX e PBX supportati</a> <a href="connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md">Connettere un controller dei confini VoIP gateway, IP PBX o della sessione di messaggistica UNIFICATA</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Disabilitare il risponditore automatico sui server di messaggistica unificata di Exchange 2010.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296335">Disabilitazione della messaggistica unificata di Exchange 2010</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Rimuovere un server di messaggistica unificata Exchange 2010 da un dial plan.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296336">Rimuovere un Server di messaggistica UNIFICATA da un Dial Plan</a></p></td>
</tr>
</tbody>
</table>


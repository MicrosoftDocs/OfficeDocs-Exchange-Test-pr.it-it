---
title: 'Elenco di controllo: Implementare la messaggistica unificata di Exchange 2013: Exchange 2013 Help'
TOCTitle: 'Elenco di controllo: Implementare la messaggistica unificata di Exchange 2013'
ms:assetid: 41b666a2-0d0d-471f-90a3-07c3c562af85
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673520(v=EXCHG.150)
ms:contentKeyID: 52063063
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Elenco di controllo: Implementare la messaggistica unificata di Exchange 2013

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-03-09_

Utilizzare questo elenco di controllo per installare e distribuire la Messaggistica unificata nell'organizzazione.

Prima di iniziare a lavorare sull'elenco di controllo, è fondamentale conoscere i concetti presentati nelle sezioni:

  - [\[ONP\] di messaggistica unificata](unified-messaging-exchange-2013-help.md)

  - [Nuove funzionalità di posta vocale](new-voice-mail-features-exchange-2013-help.md)

  - [Pianificazione per la messaggistica unificata](planning-for-unified-messaging-exchange-2013-help.md)

Per istruzioni dettagliate sulla distribuzione della Messaggistica unificata e di Microsoft Lync Server, vedere [Elenco di controllo: Integrazione di messaggistica UNIFICATA di Exchange 2013 con Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md).

## Elenco di controllo per la distribuzione della Messaggistica Unificata


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
<td><p> </p></td>
<td><p>Verificare di disporre dei prerequisiti di installazione.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Prerequisiti di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
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
<td><p> </p></td>
<td><p>Se necessario, installare i language pack di messaggistica unificata.</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">Installare un Language Pack di messaggistica unificata</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Creare il numero di dial plan richiesto per l'organizzazione.</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">Creazione di un dial plan di messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurare l'impostazione di protezione del dial plan.</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">Configurare le impostazioni di protezione VoIP</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Configurare la modalità di avvio per la messaggistica unificata sul server Accesso client e Cassette postali.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configurare la modalità di avvio in un server cassette postali</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configurare la modalità di avvio in un server Accesso Client</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurare il numero di chiamate simultanee sui server Cassette postali.</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">Configurare il numero di chiamate in arrivo in un server cassette postali</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configurare i numeri di Outlook Voice Access e di altre impostazioni.</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">Gestire un dial plan di messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurare la composizione in uscita per la Messaggistica unificata.</p></td>
<td><p><a href="authorize-calls-using-dialing-rules-exchange-2013-help.md">Autorizzare chiamate utilizzando le regole di composizione</a></p>
<p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">Autorizzare chiamate per gli utenti in un dial plan</a></p>
<p><a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">Autorizzare le chiamate per un gruppo di utenti</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Creare il numero richiesto di operatori automatici.</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">Creazione di un operatore automatico di messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Impostare e configurare ogni operatore automatico di messaggistica unificata.</p></td>
<td><p><a href="set-up-a-um-auto-attendant-exchange-2013-help.md">Configurare un operatore automatico di messaggistica unificata</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Creare, importare e abilitare un nuovo certificato di Exchange per la messaggistica unificata o abilitare un certificato di terze parti affidabile reciprocamente. Inoltre, importare il certificato su tutti i gateway VoIP, IP PBX e SBC.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Aggiungere server cassette postali e accesso Client a un dial plan URI SIP</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Riavviare il servizio Messaggistica unificata di Microsoft Exchange e il servizio Call Router di Messaggistica unificata su tutti i server di Exchange per caricare i certificati necessari.</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Arrestare il servizio di messaggistica unificata di Exchange</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Avviare il servizio di messaggistica unificata di Exchange</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Arrestare il servizio Microsoft Exchange Unified Messaging routing delle chiamate</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Avviare il servizio Microsoft Exchange Unified Messaging routing delle chiamate</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Creare un criterio cassetta postale di messaggistica unificata o configurare il criterio cassetta postale di messaggistica unificata predefinito.</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">Creazione di un criterio cassetta postale di messaggistica unificata</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">Gestire i criteri cassetta postale di messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Abilitare gli utenti alla Messaggistica unificata con un numero di estensione e un numero E.164, se necessario.</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">Consentire a un utente per la segreteria telefonica</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Abilita ricezione fax (facoltativo).</p></td>
<td><p><a href="enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md">Consentire agli utenti di posta vocale di ricevere fax</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configura sistema di posta vocale protetto (facoltativo).</p></td>
<td><p><a href="protect-voice-mail-exchange-2013-help.md">Sistema di caselle vocali protette</a></p></td>
</tr>
</tbody>
</table>


Inizio pagina


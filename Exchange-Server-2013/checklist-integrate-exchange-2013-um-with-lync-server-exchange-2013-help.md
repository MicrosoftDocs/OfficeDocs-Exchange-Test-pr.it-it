---
title: 'Elenco contr.: Int. mess. UNIF. Exchange 2013 Lync Server: Exchange 2013 Help'
TOCTitle: 'Elenco di controllo: Integrazione di messaggistica UNIFICATA di Exchange 2013 con Lync Server'
ms:assetid: 3b82e86f-9f30-4445-96ad-744082abeaeb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638120(v=EXCHG.150)
ms:contentKeyID: 52063062
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Elenco di controllo: Integrazione di messaggistica UNIFICATA di Exchange 2013 con Lync Server

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Utilizzare questo elenco di controllo per installare e distribuire la messaggistica unificata di Microsoft Lync Server 2013. In questo argomento, "Lync Server" si riferisce anche a Lync Server 2010. Tuttavia, Microsoft Office Communications Server 2007 R2 può essere distribuita insieme a Messaggistica unificata.


Prima di iniziare a lavorare sull'elenco di controllo, è fondamentale conoscere i concetti presentati nelle sezioni:

  - [Distribuzione di panoramica della messaggistica UNIFICATA di Exchange 2013 e Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Coesistenza con Office Communications Server 2007 R2 e Lync Server](coexistence-with-office-communications-server-2007-r2-and-lync-server-exchange-2013-help.md)

Per ulteriori informazioni su come eseguire le attività da completare per Lync Server, vedere [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=265752).

## Elenco di controllo per la distribuzione di Microsoft Lync Server e di Messaggistica unificata


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
<td><p>Prima di eseguire l'installazione di Exchange Server 2013, rivedere i requisiti di sistema.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisiti di sistema di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Verificare di disporre dei prerequisiti di installazione.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Prerequisiti di Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Rivedere i prerequisiti per l'integrazione di Microsoft Lync Server 2013 e Microsoft Exchange Server 2013.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282082">Prerequisiti per l'integrazione di Microsoft Lync Server 2013 e Microsoft Exchange Server 2013</a></p>

> [!TIP]
> Il Unified Communications Managed API (UCMA) 4.0 Runtime è necessario per Exchange 2013 e Lync Server 2010 e 2013 e viene installato durante l'installazione. Per scaricare e leggere informazioni relative ai UCMA 4.0, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=258269">Unified Communications Managed API 4.0 Runtime</A>


</td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Installare i server Accesso client e Cassette postali necessari.</p></td>
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
<td><p>Creare il numero di dial plan URI SIP necessari per l'organizzazione.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan">Creazione di un dial plan di messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurare l'impostazione di sicurezza del dial plan.</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">Configurare le impostazioni di protezione VoIP</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configurare il numero di chiamate simultanee nei server Cassette postali.</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">Configurare il numero di chiamate in arrivo in un server cassette postali</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurare i numeri di Outlook Voice Access e di altre impostazioni.</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">Gestire un dial plan di messaggistica unificata</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Aggiungere tutti i server Accesso client e Cassette postali a ogni dial plan URI SIP.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Aggiungere server cassette postali e accesso Client a un dial plan URI SIP</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurare la composizione in uscita per la Messaggistica unificata. Consentire tutte le chiamate sui dial plan URI SIP e sui criteri cassette postali di messaggistica unificata associati ai dial plan.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/authorize-calls-for-users-in-a-dial-plan">Autorizzare chiamate per gli utenti in un dial plan</a></p>
<p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/authorize-calls-for-a-group-of-users">Autorizzare le chiamate per un gruppo di utenti</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Creare il numero richiesto di operatori automatici.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/create-a-um-auto-attendant">Creazione di un operatore automatico di messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Impostare e configurare ogni operatore automatico di messaggistica unificata.</p></td>
<td><p><a href="set-up-a-um-auto-attendant-exchange-2013-help.md">Configurare un operatore automatico di messaggistica unificata</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Creare, importare e abilitare un nuovo certificato di Exchange per la messaggistica unificata o abilitare un certificato di terze parti affidabile reciprocamente.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Aggiungere server cassette postali e accesso Client a un dial plan URI SIP</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Configurare la modalità di avvio per la messaggistica unificata su Dual o TLS per ogni Accesso client o server Cassette postali.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configurare la modalità di avvio in un server cassette postali</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configurare la modalità di avvio in un server Accesso Client</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Riavviare il servizio Messaggistica unificata di Microsoft Exchange e il servizio Call Router di Messaggistica unificata su tutti i server di Exchange per caricare i certificati necessari.</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Arrestare il servizio di messaggistica unificata di Exchange</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Avviare il servizio di messaggistica unificata di Exchange</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Arrestare il servizio Microsoft Exchange Unified Messaging routing delle chiamate</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Avviare il servizio Microsoft Exchange Unified Messaging routing delle chiamate</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Creare un criterio cassetta postale di messaggistica unificata o configurare il criterio cassetta postale di messaggistica unificata predefinito.</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">Creazione di un criterio cassetta postale di messaggistica unificata</a></p>
<p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy">Gestire i criteri cassetta postale di messaggistica unificata</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Abilitare gli utenti alla Messaggistica unificata con un indirizzo SIP e associarli a un dial plan URI SIP.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail">Consentire a un utente per la segreteria telefonica</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Consultare la documentazione di Lync Server 2013.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282081">Pianificazione</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Installare e distribuire Lync Server 2013.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282051">Distribuzione di Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Importare il PKI interno affidabile reciprocamente o il certificato di terze parti importato sui server Messaggistica unificata di Exchange.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281863">Configurare i certificati per i server</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281865">Configurare i certificati nel Server che esegue Microsoft Exchange Server messaggistica unificata</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Se necessario, avviare i servizi Lync sui server per caricare i certificati.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282084">Avviare i servizi nei server</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Aprire Exchange Management Shell ed eseguire lo script exchucutil.ps1 dalla cartella %Programmi%\Microsoft\Exchange Server\V15\Scripts.</p>
<p></p></td>
<td><p><a href="configure-um-to-work-with-lync-server-exchange-2013-help.md">Configurare la messaggistica unificata per l'utilizzo con Lync Server</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Rivedere i requisiti per VoIP aziendale.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281876">Prerequisiti software per Enterprise Voice</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281875">Sicurezza e prerequisiti per la configurazione di Enterprise Voice</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Distribuire e configurare i gateway multimediali o i server Mediation Server e definire i peer.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281872">Distribuzione di Mediation Server e definizione di peer</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configurare un trunk tra un server Mediation Server e uno o più peer per garantire la connettività PSTN (Public Switched Telephone Network).</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281868">Configurazione di trunk</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Creare e configurare un dial plan Lync e creare, definire e associare le regole di normalizzazione.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281867">Configurazione di Dial plan</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configurare i criteri vocali e definire l'utilizzo del telefono e il routing delle chiamata in uscita.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281869">Configurazione dei criteri vocali, record utilizzo PSTN e route vocali</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Eseguire l'utilità di integrazione ocsumutil.exe di Exchange, che crea gli oggetti contatto per Outlook Voice Access e per gli operatori automatici.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281866">Configurare Lync Server 2013 per l'utilizzo della messaggistica unificata in Microsoft Exchange Server</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Definire, configurare e distribuire le funzionalità avanzate necessarie per VoIP aziendale.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281871">Distribuzione avanzate funzionalità VoIP aziendale</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Abilitare gli utenti per VoIP aziendale. Immettere un URI linea, assegnare un criterio vocale e un dial plan Lync.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281873">Consentire agli utenti per Enterprise Voice</a></p></td>
</tr>
</tbody>
</table>


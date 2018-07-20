---
title: 'Aggiornamento da Exchange 2007 a Exchange 2013: Exchange 2013 Help'
TOCTitle: Aggiornamento da Exchange 2007 a Exchange 2013
ms:assetid: a604b96d-2a51-480f-937f-45ad753c2cad
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ898581(v=EXCHG.150)
ms:contentKeyID: 51407399
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiornamento da Exchange 2007 a Exchange 2013

 

_**Si applica a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Microsoft Exchange Server 2010 e Exchange Server 2007 dispongono di diversi ruoli del server: Accesso client, cassetta postale, Trasporto Hub, messaggistica unificata e Trasporto Edge. Con Exchange Server 2013, il numero di ruoli del server è stato ridotto da cinque a tre: Accesso client, cassetta postale e Trasporto Edge. La messaggistica unificata viene ora considerata un componente o funzionalità secondaria delle funzionalità vocali offerte in Exchange 2013. (Per ulteriori dettagli sulle modifiche, vedere "Architettura di Exchange 2013" in [Novità di Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).)

Quando si aggiorna un'organizzazione Exchange 2007 esistente a Exchange 2013, per un determinato periodo di tempo i server Exchange 2007 e Exchange 2013 coesistono nell'organizzazione. È possibile mantenere questa modalità per un periodo di tempo indefinito o è possibile completare immediatamente l'aggiornamento a Exchange 2013 spostando tutte le risorse da Exchange 2007 a Exchange 2013, quindi rimuovendo le autorizzazioni dei server Exchange 2007. Per ottenere un scenario di coesistenza, è necessario che si verifichino le seguenti condizioni:

  - Exchange 2013 deve essere distribuito in un'organizzazione Exchange esistente.

  - Devono essere disponibili più versioni di Microsoft Exchange che forniscono i servizi di messaggistica all'organizzazione.

Non è possibile aggiornare un'organizzazione Exchange 2003 esistente direttamente a Exchange 2013. È necessario eseguire prima l'aggiornamento dell'organizzazione Exchange 2003 a Exchange 2007 o Exchange 2010 e quindi aggiornare l'organizzazione Exchange 2007 o Exchange 2010 a Exchange 2013. È consigliabile aggiornare l'organizzazione da Exchange 2003 a Exchange 2010 e quindi da Exchange 2010 a Exchange 2013.


> [!WARNING]
> Prima di eseguire l'aggiornamento a Exchange 2013 è necessario rimuovere tutte le istanze di Exchange 2003 dall'organizzazione.



È possibile migrare tutte le cassette postali di Exchange 2003 a Exchange Online. Per ulteriori informazioni su questo approccio, vedere [Modalità di migrazione della posta elettronica a Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).

Nella seguente tabella sono riportati gli scenari in cui è supportata la coesistenza tra Exchange 2013 e le versioni precedenti di Exchange.

### Coesistenza di Exchange 2013 e versioni precedenti di Exchange Server

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Versione di Exchange</th>
<th>Coesistenza dell'organizzazione di Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 e versioni precedenti</p></td>
<td><p>Non supportata</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>Supportata con le seguenti versioni minime di Exchange:</p>
<ul>
<li><p>1Aggiornamento cumulativo 10 per Exchange 2007 Service Pack 3 (SP3) su tutti i server Exchange 2007 nell'organizzazione, inclusi i server Trasporto Edge.</p></li>
<li><p>Aggiornamento cumulativo 2 (CU2) o versioni successive di Exchange 2013 su tutti i server Exchange 2013 nell'organizzazione.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Supportata con le seguenti versioni minime di Exchange:</p>
<ul>
<li><p>2 Exchange 2010 SP3 su tutti i server Exchange 2010 nell'organizzazione, inclusi i server Trasporto Edge.</p></li>
<li><p>Exchange 2013 CU2 o versioni successive su tutti i server Exchange 2013 nell'organizzazione.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Organizzazione mista di Exchange 2010 e Exchange 2007</p></td>
<td><p>Supportata con le seguenti versioni minime di Exchange:</p>
<ul>
<li><p>1Aggiornamento cumulativo 10 per Exchange 2007 SP3 su tutti i server Exchange 2007 nell'organizzazione, inclusi i server Trasporto Edge.</p></li>
<li><p>2 Exchange 2010 SP3 su tutti i server Exchange 2010 nell'organizzazione, inclusi i server Trasporto Edge.</p></li>
<li><p>Exchange 2013 CU2 o versioni successive su tutti i server Exchange 2013 nell'organizzazione.</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Se si desidera creare una sottoscrizione di EdgeSync tra un server Trasporto Hub Exchange 2007 e un server Trasporto Edge di Exchange 2013 SP1, è necessario installare l'aggiornamento cumulativo 13 o versioni successive per Exchange 2007 SP3 su server Trasporto Hub Exchange 2007.

2   Se si desidera creare una sottoscrizione di EdgeSync tra un server Trasporto Hub Exchange 2010 e un server Trasporto Edge di Exchange 2013 SP1, è necessario installare l'aggiornamento cumulativo 2010 o versioni successive per Exchange 5 SP3 su server Trasporto Hub Exchange 2010.

## Coesistenza in modalità mista di Exchange 2013 ed Exchange 2007 con Exchange 2010

Se sono presenti siti di Active Directory con entrambi Exchange 2010 e Exchange 2007 installati, attenersi alle istruzioni di aggiornamento per entrambi Exchange 2010 e Exchange 2007 ed eseguire i passaggi di aggiornamento richiesti per entrambi.

## Panoramica del processo di aggiornamento

Per offrire una panoramica del processo di aggiornamento da Exchange 2007 a Exchange 2013, nella tabella seguente sono state raccolte risorse correlate a ogni attività chiave. Per specifiche istruzioni dettagliate, vedere [Elenco di controllo: Aggiornamento da Exchange 2007](checklist-upgrade-from-exchange-2007-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attività</th>
<th>Argomento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Informazioni su ruoli e componenti di Exchange 2013</p></td>
<td><p><a href="what-s-new-in-exchange-2013-exchange-2013-help.md">Novità di Exchange 2013</a></p>
<p><a href="client-access-server-exchange-2013-help.md">Server Accesso client</a></p>
<p><a href="mailbox-server-exchange-2013-help.md">Server Cassette postali</a></p>
<p><a href="mail-flow-exchange-2013-help.md">Flusso di posta</a></p>
<p><a href="unified-messaging-exchange-2013-help.md">[ONP] di messaggistica unificata</a></p></td>
</tr>
<tr class="even">
<td><p>Installazione di Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Installazione di Exchange 2013 utilizzando l'installazione guidata</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Installazione del ruolo Trasporto Edge di Exchange 2013 tramite l'installazione guidata</a> (facoltativo)</p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Verificare un'installazione di Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Aggiunta di certificati digitali sul server Accesso client</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configurazione del server Accesso client di Exchange 2013</a></p>
<p><a href="digital-certificates-and-ssl-exchange-2013-help.md">Certificati digitali e SSL</a></p>
<p><a href="create-a-digital-certificate-request-exchange-2013-help.md">Creare una richiesta di certificato digitale</a></p></td>
</tr>
<tr class="even">
<td><p>Configurazione di directory virtuali correlate a Exchange</p></td>
<td><p><a href="default-settings-for-exchange-virtual-directories-exchange-2013-help.md">Impostazioni predefinite per le directory virtuali di Exchange</a></p></td>
</tr>
<tr class="odd">
<td><p>Spostamento di cassette postali da Exchange 2010</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Spostamenti di cassette postali di Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Configurazione dei componenti di trasporto</p></td>
<td><p><a href="edge-subscriptions-exchange-2013-help.md">Sottoscrizioni Edge</a> (necessario solo se è stato installato un server Trasporto Edge)</p>
<p><a href="mail-routing-exchange-2013-help.md">Routing della posta</a></p>
<p><a href="shadow-redundancy-exchange-2013-help.md">Ridondanza shadow</a></p>
<p><a href="delivery-reports-for-administrators-exchange-2013-help.md">Rapporti di recapito per gli amministratori</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurazione e distribuzione della messaggistica unificata</p></td>
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">Pianificazione per la messaggistica unificata</a></p>
<p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Distribuzione di segreteria telefonica e messaggistica UNIFICATA</a></p></td>
</tr>
</tbody>
</table>


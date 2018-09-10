---
title: 'Accesso alle cartelle pubbliche con Outlook 2016 per Mac: Exchange 2013 Help'
TOCTitle: Accesso alle cartelle pubbliche con Outlook 2016 per Mac
ms:assetid: bc9b8226-bd8b-4edc-882b-4f19cfe118eb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt788631(v=EXCHG.150)
ms:contentKeyID: 74115361
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Accesso alle cartelle pubbliche con Outlook 2016 per Mac

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016, Office 365_

_**Ultima modifica dell'argomento:** 2017-05-19_

**Riepilogo:**  Le topologie supportate di Exchange più recenti che consentono agli utenti di accedere alle cartelle pubbliche con Outlook 2016 per Mac.

Con le versioni dell'[aggiornamento di aprile 2016](https://go.microsoft.com/fwlink/?linkid=829202) per i client di Outlook 2016 per Mac, l'[aggiornamento cumulativo 14 (CU14)](https://go.microsoft.com/fwlink/p/?linkid=849432) per Exchange 2013 e l'[aggiornamento cumulativo 2 (CU 2)](https://go.microsoft.com/fwlink/p/?linkid=849793) per Exchange 2016, gli utenti di Outlook 2016 per Mac possono ora accedere alle cartelle pubbliche in più tipi di topologie rispetto a prima.

## Limitazioni di Outlook per Mac

Tutte le versioni di Outlook per Mac consentono di accedere alle cartelle pubbliche di Exchange, ma fino a poco tempo fa questi client non potevano accedere alle cartelle pubbliche negli scenari di distribuzione seguenti:

  - **Coesistenza con cartelle pubbliche legacy.** Quando una cassetta postale di un utente è abilitata in un server Exchange 2013 o Exchange 2016, l'utente non può utilizzare Outlook per Mac per accedere alle cartelle pubbliche distribuite nei server che eseguono Exchange 2010 SP3 o versioni successive. Altri client possono accedere a tali cartelle pubbliche legacy in questo scenario.

  - **Topologie ibride.** Gli utenti locali con una cassetta postale in Exchange Online non possono usare Outlook per Mac per accedere alle cartelle pubbliche moderne locali. Allo stesso modo, gli utenti con una cassetta postale di Exchange 2013 o Exchange 2016 locale non possono usare Outlook per Mac per accedere alle cartelle pubbliche distribuite in Exchange Online.

## Outlook 2016 per Mac

Con l'aggiornamento di aprile 2016 per Outlook 2016 per Mac, oltre all'aggiornamento cumulativo CU14 per Exchange 2013 e CU2 per Exchange 2016, gli scenari descritti in precedenza non sono compatibili per i client di Outlook 2016 per Mac.

Nella tabella seguente vengono riepilogate le topologie supportate per gli utenti con i client di Outlook 2016 per Mac che tentano di accedere alle cartelle pubbliche in Exchange 2013, Exchange 2016 ed Exchange Online.


> [!NOTE]
> Gli scenari illustrati nella tabella seguente presuppongono che l'aggiornamento di aprile 2016 per Outlook 2016 per Mac sia stato applicato a tutti i client.




<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Le cartelle pubbliche sono distribuite su...</th>
<th>La cassetta postale utente è su Exchange 2010 SP3 o versione successiva</th>
<th>La cassetta postale utente è su Exchange 2013 CU13 o versione successiva</th>
<th>La cassetta postale utente è su Exchange 2016 CU2 o versione successiva</th>
<th>La cassetta postale utente è su Office 365/Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2010 SP3 o versione successiva</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportata</p></td>
<td><p>Non supportata</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server 2013 CU13 o versione successiva</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 2016 CU2 o versione successiva</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
</tr>
<tr class="even">
<td><p>Office 365/Exchange Online</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
</tr>
</tbody>
</table>


Negli articoli seguenti viene descritto come distribuire le cartelle pubbliche dell'organizzazione di Exchange in caso di coesistenza o topologia ibrida. Purché i client di Outlook 2016 per Mac abbiano installato l'aggiornamento di aprile 2016, sono in grado di accedere alle cartelle pubbliche nelle configurazioni descritte nei seguenti articoli:

  - [Configurazione delle cartelle pubbliche legacy in cui si trovano le cassette postali degli utenti su server Exchange 2013](configure-legacy-public-folders-where-user-mailboxes-are-on-exchange-2013-servers-exchange-2013-help.md)

  - [Configurare le cartelle pubbliche di Exchange 2013 per una distribuzione ibrida](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

  - [Configurare le cartelle pubbliche di Exchange Online per una distribuzione ibrida](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/set-up-exo-hybrid-public-folders)


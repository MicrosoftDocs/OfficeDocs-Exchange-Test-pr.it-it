---
title: 'Impossibile installare Exchange 2013 in una foresta di Exchange 2003 o Exchange 2000 Server.: Exchange 2013 Help'
TOCTitle: Impossibile installare Exchange 2013 in una foresta di Exchange 2003 o Exchange 2000 Server.
ms:assetid: a115b182-cbd2-4d31-aa0e-375240939301
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.exchange2000or2003presentinorg(v=EXCHG.150)
ms:contentKeyID: 50481339
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impossibile installare Exchange 2013 in una foresta di Exchange 2003 o Exchange 2000 Server.

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-09_

Microsoft Exchange Server 2013 non è in grado di continuare l'operazione poiché uno o più computer eseguono Exchange 2000 Server o Exchange Server 2003 se disponibili nella foresta Active Directory. Prima di poter installare Exchange 2013, tutti i server Exchange 2000 e Exchange 2003 devono essere rimossi dalla foresta. È necessario eseguire l'upgrade di cassette postali, cartelle pubbliche e di tutti gli altri i componenti o oggetti Exchange a Exchange Server 2007 o Exchange Server 2010. Non è possibile eseguire l'upgrade da Exchange 2000 o Exchange 2003 direttamente a Exchange 2013.

Il percorso che è necessario seguire per installare Exchange 2013 nell'organizzazione dipende dalla versione di Exchange attualmente installato nella foresta. Per ulteriori informazioni, vedere la tabella seguente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Se quanto riportato è installato nell'organizzazione</th>
<th>È necessario seguire questo percorso per eseguire l'upgrade a Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2000</p></td>
<td><ol>
<li><p>Installare Exchange 2007 nell'organizzazione Exchange 2000.</p></li>
<li><p>Configurare la coesistenza di Exchange 2007 ed Exchange 2000.</p></li>
<li><p>Migrare cassette postali, cartelle pubbliche e altri componenti di Exchange 2000 a Exchange 2007.</p></li>
<li><p>Non concedere l'autorizzazione e rimuovere tutti i server Exchange 2000.</p></li>
<li><p>Installare Exchange 2013 nell'organizzazione Exchange 2007.</p></li>
<li><p>Configurare la coesistenza di Exchange 2013 ed Exchange 2007.</p></li>
<li><p>Migrare cassette postali, cartelle pubbliche e altri componenti di Exchange 2007 a Exchange 2013.</p></li>
<li><p>Non concedere l'autorizzazione e rimuovere tutti i server Exchange 2007.</p></li>
</ol>
<p>Per ulteriori informazioni, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=103281">aggiornamento a Exchange 2007</a> e <a href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">Aggiornamento da Exchange 2007 a Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2003</p></td>
<td><ol>
<li><p>Installare Exchange 2010 nell'organizzazione Exchange 2003.</p></li>
<li><p>Configurare la coesistenza di Exchange 2010 ed Exchange 2003.</p></li>
<li><p>Migrare cassette postali, cartelle pubbliche e altri componenti di Exchange 2003 a Exchange 2010.</p></li>
<li><p>Non concedere l'autorizzazione e rimuovere tutti i server Exchange 2003.</p></li>
<li><p>Installare Exchange 2013 nell'organizzazione Exchange 2010.</p></li>
<li><p>Configurare la coesistenza di Exchange 2013 ed Exchange 2010.</p></li>
<li><p>Migrare cassette postali, cartelle pubbliche e altri componenti di Exchange 2007 a Exchange 2010.</p></li>
<li><p>Non concedere l'autorizzazione e rimuovere tutti i server Exchange 2010.</p></li>
</ol>
<p>Per ulteriori informazioni, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=268414">Exchange 2003 - Roadmap di pianificazione per l'aggiornamento e la coesistenza</a> and <a href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">Aggiornamento da Exchange 2007 a Exchange 2010</a>.</p></td>
</tr>
</tbody>
</table>


Durante l'aggiornamento a Exchange 2010 o Exchange 2013, è possibile utilizzare Exchange Deployment Assistant per semplificare il completamento della distribuzione. Per ulteriori informazioni, vedere i seguenti collegamenti:

  - [Assistente per la distribuzione di Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=171086)

  - [Assistente per la distribuzione di Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=277105)

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.


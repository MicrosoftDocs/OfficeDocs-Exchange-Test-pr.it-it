---
title: 'Elenco di controllo: Distribuzione criteri conservazione: Exchange 2013 Help'
TOCTitle: 'Elenco di controllo: Distribuzione di criteri di conservazione'
ms:assetid: 59e299fd-b6a8-48f5-88ae-dc20dbe32e90
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee364743(v=EXCHG.150)
ms:contentKeyID: 50480723
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Elenco di controllo: Distribuzione di criteri di conservazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Utilizzare questo elenco di controllo per la distribuzione dei criteri nell'organizzazione Microsoft Exchange Server 2013. Prima di iniziare a lavorare con questo elenco di controllo, però, verificare di disporre delle nozioni di base sui seguenti argomenti:

  - [Gestione record di messaggistica](messaging-records-management-exchange-2013-help.md)

  - [Tag di conservazione e criteri di conservazione](retention-tags-and-retention-policies-exchange-2013-help.md)

## Elenco di controllo per la distribuzione dei criteri di archiviazione


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
<th>Risorse</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p> </p></td>
<td><p>Valutare i requisiti per la gestione dei record di messaggistica per diversi gruppi di utenti.</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">Gestione record di messaggistica</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Stabilire qual è la versione del client Microsoft Outlook in uso.</p></td>
<td><p>Analizzare i file di registro di accesso Client RPC al <code>%ExchangeInstallPath%Logging\RPC Client Access</code>.</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Creare i tag di conservazione.</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">Creare un criterio di conservazione</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Creare i criteri di conservazione.</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">Creare un criterio di conservazione</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Aggiungere tag di conservazione ai criteri di conservazione.</p></td>
<td><p><a href="add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md">I tag di conservazione per aggiungere o rimuovere i tag di conservazione da un criterio di conservazione</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Impostare i criteri di conservazione per le cassette postali.</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">Archiviazione sul posto una cassetta postale di conservazione</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Applicare un criterio di conservazione a una singola cassetta postale a scopo di test.</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">Applicazione dei criteri di conservazione alle cassette postali</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Facoltativo: Implementare il blocco dei client per bloccare i client Outlook legacy.</p></td>
<td><p><a href="configure-outlook-client-blocking-exchange-2013-help.md">Configurare i Client di Outlook per la gestione dei record di messaggistica di blocco</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Iniziare le attività di formazione e comunicazione utente. Includere una scadenza per l'elaborazione dei criteri di conservazione e lo spostamento o l'eliminazione degli elementi.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Applicare i criteri di conservazione ad altre cassette postali.</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">Applicazione dei criteri di conservazione alle cassette postali</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Ricordare agli utenti la scadenza con qualche giorno di anticipo.</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Alla scadenza, rimuovere il criterio di conservazione dalle cassette postali.</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">Archiviazione sul posto una cassetta postale di conservazione</a></p></td>
</tr>
</tbody>
</table>


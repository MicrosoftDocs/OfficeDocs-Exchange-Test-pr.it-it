---
title: 'Identificare i problemi verifiche automatiche - Active Directory: Exchange 2013 Help'
TOCTitle: Identificare i problemi verifiche automatiche - Active Directory
ms:assetid: af08e7a1-775a-4e56-a6fe-4ffc10460514
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn793979(v=EXCHG.150)
ms:contentKeyID: 62632439
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Identificare i problemi verifiche automatiche - Active Directory

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Assegni in questa pagina consente di identificare alcune delle problematiche correlate alla configurazione più comuni. È possibile utilizzare gli assegni automatici riportata di seguito per convalidare la configurazione e la Guida aggiornare l'ambiente in uso..

Se si dispone già di un account utente di Office 365, selezionare **Accedi**. Non è necessario un account di ID di Azure. Potrebbe essere richiesto per un account utente nuovamente quando eseguire le verifiche. In tal caso, l'account utente è nel formato username@youroffice365login.domain e la password.

## Prerequisiti

Controllerà per vedere se sono Assistente per l'accesso di Azure Active Directory e Azure Active Directory Module per Windows PowerShell installato.

Assistente per l'accesso di Azure Active Directory è disponibile in due versioni: [a 32 bit](https://go.microsoft.com/fwlink/?linkid=286261) e [a 64 bit](https://go.microsoft.com/fwlink/?linkid=286262).

Azure Active Directory Module per Windows PowerShell è disponibile in due versioni: [a 32 bit](https://go.microsoft.com/fwlink/?linkid=286258) e [a 64 bit](https://go.microsoft.com/fwlink/?linkid=286259).

## Controlli di Active Directory


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Applicazione</p></td>
<td><p>Sintomo</p></td>
<td><p>Controllo</p></td>
</tr>
<tr class="even">
<td><p>Versione di Exchange</p></td>
<td><p>Si desidera verificare se dispone di Exchange Server installato in locale e se si desidera versione disponibile.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834879">Eseguire questo controllo</a></p></td>
</tr>
<tr class="odd">
<td><p>Credentials</p></td>
<td><p>Non perché è possibile disporre di credenziali corrette per spostare in Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834880">Eseguire questo controllo</a></p></td>
</tr>
<tr class="even">
<td><p>Strumenti di terze parti 3</p></td>
<td><p>Desidera verificare quali 3a integrazioni/applicazioni di terze parti è stato installato nell'ambiente di messaggistica.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834907">Eseguire questo controllo</a></p></td>
</tr>
<tr class="odd">
<td><p>Cassette postali condivise</p></td>
<td><p>Desidera determinare che gestisce le cassette postali di altri utenti (delegati).</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834917">Eseguire questo controllo</a></p></td>
</tr>
</tbody>
</table>


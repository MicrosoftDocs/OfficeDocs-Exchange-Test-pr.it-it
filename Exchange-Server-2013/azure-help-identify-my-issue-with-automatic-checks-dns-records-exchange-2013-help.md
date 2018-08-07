---
title: 'Azure: identificare problemi - verifica autom - record DNS: Exchange 2013 Help'
TOCTitle: 'Azure: Consentono di identificare il problema con verifica automatica - record DNS'
ms:assetid: 1ef42cde-4df4-401a-b8f2-494630996ca8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn793619(v=EXCHG.150)
ms:contentKeyID: 62629993
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Azure: Consentono di identificare il problema con verifica automatica - record DNS

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Uno dei problemi relativi all'installazione di configurazione più comuni in modo non corretto è rappresentata dalla configurazione record DNS. È possibile utilizzare le verifiche automatiche elencate di seguito per convalidare la configurazione e la Guida aggiornare l'ambiente in uso.

Se si dispone già di un account utente di Office 365, selezionare Accedi. Non è necessario un account di ID di Azure. Potrebbe essere richiesto per un account utente nuovamente quando eseguire le verifiche. In tal caso, l'account utente è nel formato username@youroffice365login.domain e la password.

## Prerequisiti

Controllerà per vedere se sono Assistente per l'accesso di Azure Active Directory e Azure Active Directory Module per Windows PowerShell installato.

Assistente per l'accesso di Azure Active Directory è disponibile in due versioni: [a 32 bit](https://go.microsoft.com/fwlink/?linkid=286261) e [a 64 bit](https://go.microsoft.com/fwlink/?linkid=286262).

Azure Active Directory Module per Windows PowerShell è disponibile in due versioni: [a 32 bit](https://go.microsoft.com/fwlink/?linkid=286258) e [a 64 bit](https://go.microsoft.com/fwlink/?linkid=286259).

## Controlli dei record DNS


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
<td><p>Domini</p></td>
<td><p>Il dominio personalizzato (ad esempio contoso.com) non sembra essere configurato con Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Eseguire questo controllo</a></p></td>
</tr>
<tr class="odd">
<td><p>Domini</p></td>
<td><p>Dominio (ad esempio contoso.com) personalizzato non sembra essere configurato con Office 365 (è possibile utilizzare un record CNAME)</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Eseguire questo controllo</a></p></td>
</tr>
<tr class="even">
<td><p>Domini</p></td>
<td><p>Dominio (ad esempio contoso.com) personalizzato non sembra essere configurato con Office 365 (è possibile utilizzare un record TXT)</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Eseguire questo controllo</a></p></td>
</tr>
<tr class="odd">
<td><p>Messaggistica immediata</p></td>
<td><p>Gli utenti riscontrano dei problemi per il funzionamento del client Lync</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834901">Eseguire questo controllo</a></p></td>
</tr>
<tr class="even">
<td><p>Messaggistica immediata</p></td>
<td><p>Gli utenti hanno dei problemi per i client Lync per l'utilizzo con altre organizzazioni</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834902">Eseguire questo controllo</a></p></td>
</tr>
<tr class="odd">
<td><p>Posta elettronica</p></td>
<td><p>Non è possibile ottenere Outlook per la configurazione automatica con Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834897">Eseguire questo controllo</a></p></td>
</tr>
<tr class="even">
<td><p>Posta elettronica</p></td>
<td><p>Non sembra della posta elettronica di routing per Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834898">Eseguire questo controllo</a></p></td>
</tr>
<tr class="odd">
<td><p>Posta elettronica</p></td>
<td><p>Organizzazione otterrà molto posta INDESIDERATA</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834903">Eseguire questo controllo</a></p></td>
</tr>
<tr class="even">
<td><p>Posta elettronica</p></td>
<td><p>Non sembra funzionare ibrida di Exchange</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834904">Eseguire questo controllo</a></p></td>
</tr>
</tbody>
</table>


---
title: 'Identifica problemi verifiche autom.-sincronizz. Directory: Exchange 2013 Help'
TOCTitle: Identificare i problemi verifiche automatiche - sincronizzazione della Directory
ms:assetid: e6ea900a-c382-444c-a8ce-54d392bfeca3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn793977(v=EXCHG.150)
ms:contentKeyID: 62632443
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Identificare i problemi verifiche automatiche - sincronizzazione della Directory

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile utilizzare le verifiche automatiche riportata di seguito per convalidare la configurazione e la Guida aggiornare l'ambiente in uso.

Se si dispone già di un account utente di Office 365, selezionare Accedi. Non è necessario un account di ID di Azure. Potrebbe essere richiesto per un account utente nuovamente quando eseguire le verifiche. In tal caso, l'account utente è nel formato username@youroffice365login.domain e la password.


> [!NOTE]
> Se vengono visualizzati messaggi di avviso sincronizzazione nel portale di Office 365, gli errori nei registri eventi di server di sincronizzazione, o non integri directory synchronization notifiche tramite posta elettronica di Microsoft Online Services, si potrebbe avere un tipo di problema di sincronizzazione della directory. <A href="https://aka.ms/dsup">Risoluzione dei problemi di sincronizzazione della Directory</A> è uno strumento di diagnostico basato su Web progettato per individuare tipi comuni di errori di sincronizzazione e prevedere soluzioni mirate a eventuali problemi rilevati. Risoluzione dei problemi di sincronizzazione della Directory deve essere eseguito sul server DirSync.



## Prerequisiti

Controllerà per vedere se sono Assistente per l'accesso di Azure Active Directory e Azure Active Directory Module per Windows PowerShell installato.

Assistente per l'accesso di Azure Active Directory è disponibile in due versioni: [a 32 bit](https://go.microsoft.com/fwlink/?linkid=286261) e [a 64 bit](https://go.microsoft.com/fwlink/?linkid=286262).

Azure Active Directory Module per Windows PowerShell è disponibile in due versioni: [a 32 bit](https://go.microsoft.com/fwlink/?linkid=286258) e [a 64 bit](https://go.microsoft.com/fwlink/?linkid=286259).

## Controlli di sincronizzazione della directory


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
<td><p>Sincronizzazione delle directory</p></td>
<td><p>Desidera verificare se tutti i account utente di Active Directory soddisfino i requisiti per la sincronizzazione delle directory.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834884">Eseguire questo controllo</a></p></td>
</tr>
<tr class="odd">
<td><p>Sincronizzazione delle directory</p></td>
<td><p>Desidera verificare se i livelli funzionali di dominio Active Directory siano correttamente impostati a Windows Server 2003 o versioni successive.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Eseguire questo controllo</a></p></td>
</tr>
<tr class="even">
<td><p>Sincronizzazione delle directory</p></td>
<td><p>Desidera verificare se si è verificato durante la sincronizzazione delle directory nelle ultime tre ore.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">Eseguire questo controllo</a></p></td>
</tr>
<tr class="odd">
<td><p>Sincronizzazione delle directory</p></td>
<td><p>Desidera verificare se Active Directory dispone di attributi utente duplicati in cui verranno bloccato la sincronizzazione delle directory.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834883">Eseguire questo controllo</a></p></td>
</tr>
<tr class="even">
<td><p>Sincronizzazione delle directory</p></td>
<td><p>Desidera verificare se la sincronizzazione delle directory è abilitata in Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">Eseguire questo controllo</a></p></td>
</tr>
<tr class="odd">
<td><p>Sincronizzazione delle directory</p></td>
<td><p>Desidera verificare se è possibile distribuire le limitazioni offerta di Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834920">Eseguire questo controllo</a></p></td>
</tr>
<tr class="even">
<td><p>Sincronizzazione delle directory</p></td>
<td><p>Desidera verificare se è possibile distribuire Office 365 e utilizzare le impostazioni di sincronizzazione della directory predefinita.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Eseguire questo controllo</a></p></td>
</tr>
<tr class="odd">
<td><p>Sincronizzazione delle directory</p></td>
<td><p>Desidera verificare se si utilizza Active Directory e può supportare la sincronizzazione delle directory.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834886">Eseguire questo controllo</a></p></td>
</tr>
<tr class="even">
<td><p>Sincronizzazione delle directory</p></td>
<td><p>Desidera verificare se tutti i gruppi di Active Directory soddisfino i requisiti per la sincronizzazione delle directory.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834913">Eseguire questo controllo</a></p></td>
</tr>
</tbody>
</table>


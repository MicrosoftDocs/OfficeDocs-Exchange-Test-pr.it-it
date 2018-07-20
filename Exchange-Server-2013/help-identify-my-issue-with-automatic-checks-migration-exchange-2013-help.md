﻿---
title: 'Identificare i problemi verifiche automatiche - migrazione: Exchange 2013 Help'
TOCTitle: Identificare i problemi verifiche automatiche - migrazione
ms:assetid: c1cd235d-8e8b-44a8-862d-9d36dc3a44c3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn793980(v=EXCHG.150)
ms:contentKeyID: 62632441
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Identificare i problemi verifiche automatiche - migrazione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Assegni in questa pagina consente di identificare alcune delle problematiche correlate alla configurazione più comuni. È possibile utilizzare gli assegni automatici riportata di seguito per convalidare la configurazione e la Guida aggiornare l'ambiente in uso.

Se si dispone già di un account utente di Office 365, selezionare **Accedi**. Non è necessario un account di ID di Azure. Potrebbe essere richiesto per un account utente nuovamente quando eseguire le verifiche. In tal caso, l'account utente è nel formato username@youroffice365login.domain e la password.

## Prerequisiti

Controllerà per vedere se sono Assistente per l'accesso di Azure Active Directory e Azure Active Directory Module per Windows PowerShell installato.

Assistente per l'accesso di Azure Active Directory è disponibile in due versioni: [a 32 bit](https://go.microsoft.com/fwlink/?linkid=286261) e [a 64 bit](https://go.microsoft.com/fwlink/?linkid=286262).

Azure Active Directory Module per Windows PowerShell è disponibile in due versioni: [a 32 bit](https://go.microsoft.com/fwlink/?linkid=286258) e [a 64 bit](https://go.microsoft.com/fwlink/?linkid=286259).

## Aggiunta di controlli di domini


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
<td><p>Dimensioni della cassetta postale</p></td>
<td><p>Desidera determinare se gli utenti stanno utilizzando dimensioni della cassetta postale predefinito dell'organizzazione in modo ottimale posso pianificare la migrazione.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834877">Eseguire questo controllo</a></p></td>
</tr>
<tr class="odd">
<td><p>Foresta singola</p></td>
<td><p>Sto cercando di valutare se sono la migrazione degli account personali degli utenti alla sincronizzazione della Directory.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834875">Eseguire questo controllo</a></p></td>
</tr>
<tr class="even">
<td><p>Modalità funzionale di dominio</p></td>
<td><p>Si desidera verificare se si è pronto per integrare ADFS 2.0/Single Sign-in</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Eseguire questo controllo</a></p></td>
</tr>
<tr class="odd">
<td><p>Cartelle pubbliche</p></td>
<td><p>Desidera verificare se dispone di cartelle pubbliche per eseguire la migrazione a Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834896">Eseguire questo controllo</a></p></td>
</tr>
</tbody>
</table>


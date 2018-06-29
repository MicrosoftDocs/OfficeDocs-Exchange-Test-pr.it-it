---
title: 'Preparare le cassette postali per le richieste di spostamento tra foreste: Exchange 2013 Help'
TOCTitle: Preparare le cassette postali per le richieste di spostamento tra foreste
ms:assetid: fdbed4fc-a77e-40d5-a211-863b05d74784
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633491(v=EXCHG.150)
ms:contentKeyID: 50482096
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Preparare le cassette postali per le richieste di spostamento tra foreste

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2017-11-22_

**Riepilogo:** informazioni sulla preparazione di cassette postali per più foreste sposta Exchange 2013.

Microsoft Exchange 2013 supporta spostamenti e migrazioni utilizzando Exchange Management Shell in modo specifico i cmdlet **New-MoveRequest** e **New-MigrationBatch** . È inoltre possibile spostare la cassetta postale tramite interfaccia di amministrazione di Exchange (EAC). Si noti che è possibile spostare le cassette postali di Exchange 2010 ed Exchange 2013 in una foresta di Exchange 2013.

Per spostare una cassetta postale da un insieme di strutture Exchange in una foresta Exchange 2013, la foresta di destinazione Exchange 2013 deve contenere un utente abilitato alla posta valido con un insieme di attributi Active Directory specificato. Se è presente almeno un server Accesso Client di Exchange 2013 distribuito nella foresta, la foresta è considerata un insieme di strutture Exchange 2013.

Per preparare la foresta per lo spostamento delle cassette postali, è necessario creare nella foresta di destinazione utenti abilitati all'uso della posta con gli attributi richiesti. Di seguito vengono illustrati due approcci consigliati per la creazione di utenti abilitati all'uso della posta con gli attributi necessari:

  - Se è stato distribuito Microsoft Identity Lifecycle Manager (ILM) per la sincronizzazione degli elenchi indirizzi globali tra foreste, per creare l'utente abilitato all'uso della posta è consigliabile utilizzare Service Pack 1 (SP1) per ILM 2007 Feature Pack 1 (FP1). È disponibile codice di esempio che può essere utilizzato per imparare a personalizzare ILM per la sinconizzazione dell'utente della cassetta postale di origine con quello di destinazione.
    
    Per ulteriori informazioni, incluso il download del codice di esempio, vedere [Preparare le cassette postali per gli spostamenti tra foreste con codice di esempio](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md).

  - Se l'utente di posta elettronica di destinazione viene creato utilizzando uno strumento di Active Directory diverso da ILM/MIIS, utilizzare il cmdlet **Update-Recipient** con il parametro *Identity* per eseguire il servizio Elenco indirizzi e generare **LegacyExchangeDN** per l'utente di posta elettronica di destinazione. È stato creato uno script di Windows PowerShell di esempio in grado di leggere e scrivere in Active Directory e di eseguire il cmdlet **Update-Recipient**.
    
    Per ulteriori informazioni sull'utilizzo dello script di esempio, vedere [Prepara le cassette postali per gli spostamenti tra foreste utilizzando lo script Prepare MoveRequest.ps1 in Shell](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md).

Dopo aver creato l'utente di posta elettronica di destinazione, è possibile eseguire i cmdlet **New-MoveRequest** o **New-MigrationBatch** per spostare la cassetta postale nella foresta Exchange 2013 di destinazione.

Per ulteriori informazioni sulle richieste di spostamento remote, vedere gli argomenti seguenti:

  - [New-MigrationBatch](https://technet.microsoft.com/it-it/library/jj219166\(v=exchg.150\))

  - [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\))

Per ulteriori informazioni sullo spostamento di cassette postali remote e legacy, vedere [Spostamenti di cassette postali di Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

Nella parte restante di questo argomento vengono descritti gli attributi degli utenti di posta elettronica di Active Directory necessari allo spostamento di una cassetta postale. Tali attributi vengono configurati automaticamente quando si utilizza il codice o lo script per preparare lo spostamento della cassetta postale. È tuttavia possibile copiare manualmente tali attributi tramite un editor Active Directory.

## Attributi degli utenti di Active Directory necessari allo spostamento di una cassetta postale

Per supportare lo spostamento di una cassetta postale remota, l'oggetto utente di posta nella foresta di Exchange 2013 di destinazione deve disporre degli attributi di Active Directory illustrati in questa sezione:

  - Attributi obbligatori

  - Attributi facoltativi

  - Attributi collegati

  - Attributi degli utenti collegati

  - Attributi delle cassette postali delle risorse

  - Attributi aggiuntivi

## Attributi obbligatori

Nella tabella seguente è riportato l'insieme di attributi minimo che è necessario configurare in ILM per l'utente di posta elettronica di destinazione affinché il cmdlet **New-MoveRequest** funzioni correttamente.

### Attributi dell'utente di posta

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributi di Active Directory dell'utente di posta</th>
<th>Azione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>displayName</strong></p></td>
<td><p>Copiare l'attributo corrispondente della cassetta postale di origine o generare un nuovo valore.</p></td>
</tr>
<tr class="even">
<td><p><strong>Mail</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>mailNickname</strong></p></td>
<td><p>Copiare l'attributo corrispondente della cassetta postale di origine o generare un nuovo valore.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchArchiveGUID and msExchArchiveName</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine. Gli attributi sono disponibili solo se la cassetta postale di origine è Exchange 2010.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMailboxGUID</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>-2147483642 (decimale) //equivale a 0x80000006 (esadecimale).</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientTypeDetails</strong></p></td>
<td><p>128 (decimale) /0x80 (esadecimale).</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUserCulture</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchVersion</strong></p></td>
<td><p>44220983382016 (decimale).</p></td>
</tr>
<tr class="even">
<td><p><strong>cn</strong></p></td>
<td><p>Copiare l'attributo corrispondente della cassetta postale di origine o generare un nuovo valore.</p></td>
</tr>
<tr class="odd">
<td><p><strong>proxyAddresses</strong></p></td>
<td><p>Copiare l'attributo <strong>proxyAddresses</strong> della cassetta postale di origine. Copiare inoltre l'attributo <strong>LegacyExchangeDN</strong> della cassetta postale di origine come indirizzo X500 nell'attributo <strong>proxyAddresses</strong> dell'utente di posta di destinazione.</p>

> [!NOTE]
> L'attributo <STRONG>proxyAddresses</STRONG> dell'utente della cassetta postale di origine deve contenere un indirizzo SMTP che corrisponde al dominio autorevole della foresta di destinazione. Ciò consente al cmdlet <STRONG>New-MoveRequest</STRONG> di selezionare correttamente l'attributo <STRONG>targetAddress</STRONG> dell'utente abilitato alla posta di origine (convertito dall'utente della cassetta postale di origine dopo il completamento della richiesta di spostamento della cassetta postale) per assicurare che il routing dei messaggi di posta elettronica continui a essere eseguito correttamente.


</td>
</tr>
<tr class="even">
<td><p><strong>sAMAccountName</strong></p></td>
<td><p>Copiare l'attributo corrispondente della cassetta postale di origine o generare un nuovo valore.</p>
<p>Verificare che il valore sia univoco nel dominio della foresta di destinazione a cui appartiene l'utente di posta di destinazione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>targetAddress</strong></p></td>
<td><p>Impostare un indirizzo SMTP nell'attributo <strong>proxyAddresses</strong> della cassetta postale di origine.</p>
<p>Tale indirizzo SMTP deve appartenere al dominio autorevole della foresta di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>userAccountControl</strong></p></td>
<td><p>Costante: 514 //equivale a 0x202, ACCOUNTDISABLE | NORMAL_ACCOUNT.</p></td>
</tr>
<tr class="odd">
<td><p><strong>userPrincipalName</strong></p></td>
<td><p>Copiare l'attributo corrispondente della cassetta postale di origine o generare un nuovo valore. Poiché l'account di accesso dell'utente di posta è disabilitato, questo attributo <strong>userPrincipalName</strong> non viene utilizzato.</p></td>
</tr>
</tbody>
</table>


## Attributi facoltativi

La configurazione degli attributi seguenti non è obbligatoria per il corretto funzionamento del cmdlet **New-MoveRequest**. Sincronizzando tali attributi è tuttavia possibile assicurare una migliore esperienza utente end-to-end dopo lo spostamento della cassetta postale. Poiché l'utente di posta di destinazione viene visualizzato nell'elenco indirizzi globale della foresta di destinazione, è consigliabile impostare i seguenti attributi correlati all'elenco indirizzi globale.

### Attributi correlati all'elenco indirizzi globale

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributi di Active Directory dell'utente di posta</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>c</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>co</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>countryCode</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>company</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>department</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>facsimileTelephoneNumber</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>givenName</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>homePhone</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>info</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>initials</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>l</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>mobile</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchAssistantName</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchHideFromAddressLists</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherHomePhone</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherTelephone</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>pager</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>physicalDeliveryOfficeName</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalCode</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>sn</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>st</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>streetAddress</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>telephoneAssistant</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>telephoneNumber</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>title</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
</tbody>
</table>


## Attributi collegati

Un attributo collegato è un attributo di Active Directory che fa riferimento ad altri oggetti di Active Directory nella foresta locale. Non è possibile copiare direttamente i valori degli attributi collagati da una cassetta postale nella foresta di origine a un utente di posta nella foresta di destinazione. È innanzitutto necessario trovare nella foresta di origine gli oggetti di Active Directory a cui fa riferimento l'attributo della cassetta postale di origine, quindi occorre trovare nella foresta di destinazione gli oggetti di Active Directory corrispondenti agli oggetti di Active Directory della foresta di origine menzionati in precedenza. Infine, è necessario impostare l'attributo dell'utente di posta di destinazione in modo che faccia riferimento agli oggetti di Active Directory nella foresta di destinazione.

### Attributi collegati

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributi di Active Directory dell'utente di posta</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>altRecipient</strong></p></td>
<td><p>Corrisponde all'attributo <strong>altRecipient</strong> della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>deliverAndRedirect</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine. Questo attributo è un valore booleano che dovrebbe essere impostato insieme a <strong>altRecipient</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Manager</strong> (e i relativi backlink)</p></td>
<td><p>Corrisponde all'attributo manager della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>MemberOf</strong> (backlink)</p></td>
<td><p>Si tratta del backlink dell'attributo di appartenenza a un gruppo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>publicDelegates</strong> (e relativi backlink)</p></td>
<td><p>Corrisponde all'attributo <strong>publicDelegates</strong> della cassetta postale di origine.</p></td>
</tr>
</tbody>
</table>


## Attributi degli utenti collegati

Quando si sposta una cassetta postale in una foresta di risorse di Exchange 2013, la cassetta postale nella foresta di risorse viene considerata una *cassetta postale collegata*. In questo scenario, è necessario creare un utente di posta collegato nella foresta di risorse di destinazione. Per creare un utente di posta collegato, è necessario impostare gli attributi indicati nella tabella seguente.

### Attributi degli utenti collegati

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributi di Active Directory dell'utente di posta</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchMasterAccountHistory</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMasterAccountSid</strong></p></td>
<td><p>Se per la cassetta postale di origine è disponibile l'attributo <strong>msExchMasterAccountSid</strong>, copiarlo. In caso contrario, copiare l'attributo <strong>objectSid</strong> della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>Costante:-1073741818 (decimale) //equivale a 0xC0000006 *senza segno*.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> È possibile creare una cassetta postale esclusivamente se tra la foresta di origine e quella di destinazione esiste una relazione di trust tra foreste.



Se l'oggetto di origine è disabilitato e l'attributo **msExchMasterAccountSid** è impostato su self (cassetta postale per una risorsa o cassetta postale condivisa), non viene imposto alcun contrassegnlo per l'utente di destinazione.

Se l'oggetto è disabilitato e l'attributo **msExchMasterAccountSid** non è impostato, la cassetta postale non è valida.

Se l'oggetto è abilitato e l'attributo **msExchMasterAccountSid** è impostato, la cassetta postale non è valida.

## Attributi delle cassette postali delle risorse

Se si desidera spostare una cassetta postale di risorsa in una foresta di Exchange 2013, è necessario impostare gli attributi indicati nella tabella seguente per l'utente di posta di destinazione.

### Attributi delle cassette postali delle risorse

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributi di Active Directory dell'utente di posta</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>Se la cassetta postale di origine è una sala riunioni:</p>
<ul>
<li><p><strong>Costante</strong>   -2147481850 (decimale) //equivale a 0x80000706 *senza segno*.</p></li>
</ul>
<p>Se la cassetta postale di origine è una cassetta postale attrezzatura:</p>
<ul>
<li><p><strong>Costante</strong>   -2147481594 (decimale) //equivale a 0x80000806 *senza segno*.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceCapacity</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceDisplay</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceMetaData</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceSearchProperties</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
</tbody>
</table>


## Attributi aggiuntivi

In Exchange 2007, durante lo spostamento di una cassetta postale il cmdlet **Move-Mailbox** copia anche gli attributi indicati nella tabella seguente. È facoltativamente possibile copiare tali attributi se richiesto dall'organizzazione.

### Attributi delle cassette postali delle risorse

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributi di Active Directory dell'utente di posta</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>comment</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>deletedItemFlags</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>delivContLength</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>departmentNumber</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>description</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>division</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeID</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>employeeNumber</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeType</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>extensionAttribute1-15</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>homePostalAddress</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>internationalISDNNumber</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ipPhone</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>language</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>lmPwdHistory</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>localeID</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>mAPIRecipient</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>middleName</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticCompanyName</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticDepartment</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticDisplayName</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticFirstName</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticLastName</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchBlockedSendersHash</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCExpirySuspensionEnd</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchELCExpirySuspensionStart</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCMailboxFlags</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchExternalOOFOptions</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneFlags</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLDeleteThreshold</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLJunkThreshold</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLQuarantineThreshold</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLRejectThreshold</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMDBRulesQuota</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchPoliciesExcluded</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchSafeRecipientsHash</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchSafeSendersHash</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUMSpokenName</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherFacsimileTelephoneNumber</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherIpPhone</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherMobile</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherPager</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>preferredDeliveryMethod</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>personalPager</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>personalTitle</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>photo</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>pOPCharacterSet</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>pOPContentFormat</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalAddress</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>postOfficeBox</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>primaryInternationalISDNNumber</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>primaryTelexNumber</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>showInAdvancedViewOnly</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>street</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>terminalServer</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>textEncodedORAddress</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>thumbnailLogo</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>thumbnailPhoto</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>url</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>userCert</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>userCertificate</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="even">
<td><p><strong>userSMIMECertificate</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
<tr class="odd">
<td><p><strong>wWWHomePage</strong></p></td>
<td><p>Copiare direttamente l'attributo corrispondente della cassetta postale di origine.</p></td>
</tr>
</tbody>
</table>


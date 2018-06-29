---
title: 'Elimina e ricrea la cassetta postale di individuazione predefinita in Exchange: Exchange 2013 Help'
TOCTitle: Elimina e ricrea la cassetta postale di individuazione predefinita in Exchange
ms:assetid: 4bde0b00-bdf7-44b4-ba64-aa062bc10ca2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn750894(v=EXCHG.150)
ms:contentKeyID: 62371316
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Elimina e ricrea la cassetta postale di individuazione predefinita in Exchange

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-05-04_

Puoi utilizzare Exchange Management Shell per eliminare la cassetta postale di individuazione predefinita, ricrearla e assegnarle autorizzazioni.

## Quando eseguire questa operazione

In Exchange Server 2013 e Exchange Online, la dimensione massima della cassetta postale di individuazione predefinita è 50 GB. Viene utilizzato per memorizzare i risultati della ricerca eDiscovery sul posto. Prima che è stato modificato il limite delle dimensioni, le organizzazioni potrebbero aumentare la quota di archiviazione a più di 50 GB. Di conseguenza, le cassette postali di individuazione diventi più di 50 GB. Esistono tre tipi di problemi con una cassetta postale di individuazione superiori a 50 GB:

  - Non è supportato.

  - Impossibile eseguire la migrazione di Office 365.

  - Se la cassetta postale di individuazione in Exchange Server 2010, non può essere aggiornata a Exchange Server 2013.

La risoluzione del problema dipende nel caso in cui si desideri salvare i risultati della ricerca da una cassetta postale di individuazione predefinita che superi i 50 GB.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Salvare i risultati della ricerca?</th>
<th>Esegui questa operazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>No</p></td>
<td><p>Seguire i passaggi in questo argomento per eliminare e quindi ricreare la cassetta postale di individuazione predefinita.</p></td>
</tr>
<tr class="even">
<td><p>Sì</p></td>
<td><p>Segui le istruzioni riportate in <a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">Ridurre le dimensioni di una cassetta postale di individuazione in Exchange</a>.</p></td>
</tr>
</tbody>
</table>


## Utilizzare Exchange Management Shell per eliminare e ricreare la cassetta postale di individuazione


> [!NOTE]
> È possibile utilizzare Interfaccia di amministrazione di Exchange (EAC) perché le cassette postali di individuazione sono sono visualizzate nell'EAC.



1.  Eseguire il comando seguente per eliminare la cassetta postale di individuazione predefinita.
    
        Remove-Mailbox "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}"

2.  Nel messaggio di richiesta di conferma per eliminare la cassetta postale e l'oggetto utente di Active Directory corrispondente, digita **Y**, quindi premi Invio.
    
    Un nuovo oggetto utente viene viene creato nella Active Directory quando si crea la cassetta postale di individuazione nel passaggio successivo.

3.  Eseguire il comando seguente per ricreare la cassetta postale di individuazione predefinita.
    
        New-Mailbox -Name "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -Alias "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -DisplayName "Discovery Search Mailbox" -Discovery

4.  Eseguire il seguente comando per assegnare a un gruppo di ruoli di Gestione individuazione le autorizzazioni per aprire una cassetta postale di individuazione e visualizzare i risultati di ricerca.
    
        Add-MailboxPermission "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User "Discovery Management" -AccessRights FullAccess -InheritanceType all


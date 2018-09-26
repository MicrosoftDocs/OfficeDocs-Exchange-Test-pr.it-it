---
title: 'Disabilitazione o eliminazione di una cassetta postale: Exchange 2013 Help'
TOCTitle: Disabilitazione o eliminazione di una cassetta postale
ms:assetid: 31ad25d6-2942-4fd9-aecb-cdf9654163d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ863434(v=EXCHG.150)
ms:contentKeyID: 50555563
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Disabilitazione o eliminazione di una cassetta postale

 

_**Si applica a:** Exchange Server 2013 SP1_

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile utilizzare EAC o un'istanza di Shell per disabilitare o eliminare una cassetta postale in Exchange 2013. Quando si disabilita o elimina una cassetta postale, Exchange la conserva nel database delle cassette postali imposta lo stato disabilitato per la cassetta postale. Le cassette postali disabilitate ed eliminate vengono mantenute nel relativo database fino alla scadenza del periodo di conservazione, che equivale a 30 giorni per impostazione predefinita. Una volta trascorso il periodo di conservazione, la cassetta postale viene *eliminata* definitivamente.

Nel caso in cui fosse necessario eliminare una cassetta postale in Exchange Online, vedere [Eliminare o ripristinare le cassette postali utente in Exchange Online](https://technet.microsoft.com/it-it/library/dn186233\(v=exchg.150\)).


> [!NOTE]
> Le cassette postali disabilitate o eliminate vengono definite <EM>cassette postali disconnesse</EM>.



La principale differenza tra l'eliminazione e la disabilitazione di una cassetta postale è che quando si disabilita una cassetta postale, gli attributi di Exchange vengono rimossi dal corrispondente account utente in Active Directory, ma l'account utente viene mantenuto. Quando si elimina una cassetta postale, vengono eliminati sia gli attributi di Exchange sia l'account utente in Active Directory. La differenza determina anche le opzioni per la riconnessione o il ripristino delle cassette postali disabilitate ed eliminate.

Nella tabella seguente, sono riportati i tipi di cassette postali di Exchange che è possibile disabilitare ed eliminare.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di cassetta postale</th>
<th>Disattivare?</th>
<th>Eliminare?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cassetta postale di archiviazione</p></td>
<td><p>Sì</p></td>
<td><p>No *</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale collegata</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale delle risorse (Sala o Attrezzatura)</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale condivisa</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale utente</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
</tbody>
</table>


\* Se una cassetta postale di archiviazione è abilitata, questa verrà eliminata quando viene eliminata la cassetta postale principale. Per informazioni sulla disattivazione delle cassette postali di archiviazione, vedere [Gestione degli archivi In Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md).

Se un amministratore elimina un account utente che dispone di una cassetta postale, l'archivio informazioni di Exchange rileva che la cassetta postale non è più collegata all'account utente e la contrassegna come da eliminare, anche se è bloccata. Se si desidera conservare la cassetta postale, eseguire queste operazioni:

1.  Disattivare l'account utente invece di eliminarlo.

2.  Modificare le proprietà della cassetta postale al fine di limitarne uso e accesso. Ad esempio, impostare la quota di invio e ricezione su 1, bloccare gli utenti che possono inviare messaggi alla cassetta postale e limitare gli utenti che possono accedere alla cassetta postale.

3.  Conservare la cassetta postale fino a quando tutti i dati sono stati rimossi o fino a quando il blocco non è più necessario.

Per le attività di gestione aggiuntive relative alle cassette postali disconnesse, vedere i seguenti argomenti:

  - [Cassette postali disconnesse](disconnected-mailboxes-exchange-2013-help.md)

  - [Connettere una cassetta postale disabilitata](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [La connessione o il ripristino di una cassetta postale eliminata](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [Eliminare definitivamente una cassetta postale](permanently-delete-a-mailbox-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Disabilitare una cassetta postale

Come indicato in precedenza, quando si disabilita una cassetta postale, gli attributi di Exchange vengono rimossi dal corrispondente account utente in Active Directory, ma l'account utente viene mantenuto.

## Disabilitazione di una cassetta postale tramite l'interfaccia di amministrazione di Exchange

Nella procedura seguente, viene illustrato come disabilitare una cassetta postale utente. Utilizzare la stessa procedura per disabilitare altri tipi di cassetta postale una volta visualizzata la pagina appropriata nell'interfaccia di amministrazione di Exchange.

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale utente che si desidera disabilitare.

3.  Fare clic su **Altro**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni"), quindi su **Disabilita**.

4.  Verrà visualizzato il messaggio di avviso che richiede se si desidera disattivare la cassetta postale. Fare clic su **Sì** per confermare l'operazione.

La cassetta postale viene rimossa dall'elenco delle cassette postali.

## Disabilitazione di una cassetta postale tramite Shell

Utilizzare il seguente comando per disabilitare le cassette postali utente, le cassette postali collegate, le cassette postali per le risorse e le cassette postali condivise.

```powershell
Disable-Mailbox <identity>
```

Quando si esegue questo comando, viene visualizzato un messaggio per la conferma della disattivazione della cassetta postale.

Di seguito, sono riportati alcuni esempi di comandi per la disattivazione delle cassette postali.


```powershell
Disable-Mailbox danj
```

```powershell
    Disable-Mailbox "Conf Room 31/1234 (12)"
```

```powershell
Disable-Mailbox sharedmbx@contoso.com
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta disattivazione di una cassetta postale, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, fare clic su **Destinatari**, andare alla pagina appropriata per il tipo di cassetta postale disabilitata, quindi verificare che la cassetta postale non sia più presente nell'elenco.

  - In Utenti e computer di Active Directory fare clic con il pulsante destro del mouse sull'account utente di cui è stata disabilitata la cassetta postale, quindi scegliere **Proprietà**. Nella scheda **Generale**, notare che il campo **Posta elettronica** è vuoto. Ciò indica che la cassetta postale è disabilitata, ma che l'account utente esiste ancora.

  - In Shell, utilizzare il seguente comando.
    ```powershell
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    ```

    Il valore `Disabled` nella proprietà *DisconnectReason* indica che la cassetta postale è disabilitata.
    

    > [!NOTE]
    > Quando si elimina una cassetta postale, il valore nella proprietà <EM>DisconnectReason</EM> è anche <CODE>Disabled</CODE>. Tuttavia, il corrispondente account utente in Active Directory viene eliminato.



  - In Shell, utilizzare il seguente comando.
    
    ```powershell
        Get-User <identity>
    ```
    
    Notare che il valore per la proprietà *RecipientType* è `User` invece di `UserMailbox`, che è il valore per gli utenti con cassette postali abilitate. Ciò indica anche che la cassetta postale è disabilitata, ma che l'account utente viene mantenuto.

## Eliminazione di una cassetta postale

Come indicato in precedenza, quando si elimina una cassetta postale, vengono eliminati sia gli attributi di Exchange sia l'account utente in Active Directory. La cassetta postale (e la cassetta postale di archiviazione, se abilitata) verrà eliminata in modo definitivo dal database delle cassette postali una volta scaduto il relativo periodo di conservazione.

## Eliminazione di una cassetta postale tramite l'interfaccia di amministrazione di Exchange

Nelle seguente procedura, viene illustrato come eliminare una cassetta postale utente. Utilizzare la stessa procedura per eliminare altri tipi di cassetta postale una volta visualizzata la pagina appropriata nell'interfaccia di amministrazione di Exchange.

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale che si desidera eliminare, quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

3.  Viene visualizzato un avviso di conferma per l'eliminazione della cassetta postale. Fare clic su **Sì** per eliminare la cassetta postale.

La cassetta postale viene rimossa dall'elenco delle cassette postali.

## Eliminazione di una cassetta postale tramite Shell

Utilizzare il seguente comando per eliminare le cassette postali utente, le cassette postali collegate, le cassette postali per le risorse e le cassette postali condivise.

```powershell
Remove-Mailbox <identity>
```

Quando si esegue questo comando, viene visualizzato un messaggio per la conferma dell'eliminazione della cassetta postale.

Di seguito, sono riportati alcuni esempi di comandi per l'eliminazione delle cassette postali.


```powershell
Remove-Mailbox pilarp@contoso.com
```

```powershell
Remove-Mailbox "Fleet Van (16)"
```

```powershell
Remove-Mailbox corpprint
```


## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta eliminazione di una cassetta postale, effettuare una delle seguenti operazioni.

1.  Nell'interfaccia di amministrazione di Exchange, fare clic su **Destinatari**, andare alla pagina appropriata per il tipo di cassetta postale eliminata, quindi verificare che la cassetta postale non sia più presente nell'elenco.

2.  In Utenti e computer di Active Directory, verificare che l'account utente corrispondente non sia più presente nell'elenco.

Oppure

1.  Eseguire il seguente comando per verificare la corretta eliminazione della cassetta postale.
    ```powershell
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    ```
    Il valore `Disabled` nella proprietà *DisconnectReason* indica che la cassetta postale è stata disabilitata.
    

    > [!NOTE]
    > Quando si elimina una cassetta postale, il valore nella proprietà <EM>DisconnectReason</EM> è anche <CODE>Disabled</CODE>. Tuttavia, il corrispondente account utente in Active Directory viene mantenuto.



2.  Utilizzare il seguente comando per verificare la corretta eliminazione dell'account utente in Active Directory.
    
    ```powershell
    Get-User <identity>
    ```
    
    Il comando restituirà un errore indicante l'impossibilità di rintracciare l'utente, confermando, in questo modo, l'eliminazione dell'account.


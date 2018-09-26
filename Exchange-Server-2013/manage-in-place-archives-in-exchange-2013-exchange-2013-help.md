---
title: 'Gestione degli archivi In Exchange 2013: Exchange 2013 Help'
TOCTitle: Gestione degli archivi In Exchange 2013
ms:assetid: 49ef4a3e-d209-4fb2-80a3-6132b0f69bd0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ651146(v=EXCHG.150)
ms:contentKeyID: 50480533
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione degli archivi In Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-02-01_

Archiviazione sul posto consente di riprendere il controllo dei dati di messaggistica dell'organizzazione eliminando la necessità di file di archivio personale (con estensione pst) e consentendo di soddisfare requisiti di conservazione ed eDiscovery messaggi dell'organizzazione. Con l'archiviazione abilitato, gli utenti possono archiviare i messaggi in una cassetta postale di archiviazione, è possibile accedere tramite MicrosoftOutlook e Outlook Web App.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Archiviazione in locale" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Non è supportato per disporre della cassetta postale principale dell'utente si trovano in una versione precedente di Exchange di archivio dell'utente. Se non è ancora in Exchange 2010 cassetta postale principale dell'utente, è necessario spostare su Exchange 2013 allo stesso tempo che si sposta nell'archivio in Exchange 2013.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Creazione di una cassetta postale e abilitazione di un archivio locale

## Utilizzo dell'interfaccia di amministrazione di Exchange

1.  Accedere a **Destinatari** \> **Cassette postali**.

2.  Fare clic su **Nuovo** \> **Cassetta postale utente**.

3.  Nella pagina **Nuova cassetta postale utente**, nella casella **Alias**, digitare l'alias per l'utente.
    

    > [!NOTE]
    > Se questa casella resta vuota, il valore digitato nella casella <STRONG>Nome accesso utente</STRONG> viene utilizzato per l'alias.



4.  Selezionare una delle seguenti opzioni:
    
      - **Utente esistente**   Fare clic su questo pulsante e scegliere **Sfoglia** per aprire la finestra di dialogo **Seleziona utente - Intera foresta**. Questa finestra di dialogo consente di visualizzare nella foresta un elenco di account utente di Active Directory che non sono abilitati alla posta o che non dispongono di cassette postali di Exchange. Selezionare gli account utente che si desidera abilitare alla posta e fare clic su **OK**. Se si seleziona questa opzione, non è necessario fornire le informazioni sull'account utente perché esistono già in Active Directory.
    
      - **Nuovo utente**   Fare clic su questo pulsante per creare un nuovo account utente in Active Directory e creare una cassetta postale per l'utente. Se si seleziona questa opzione, sarà necessario fornire le informazioni richieste sull'account utente.
    

    > [!NOTE]
    > L'account di Active Directory associato alle cassette postali utente deve essere ubicato nella stessa foresta del server Exchange. Per creare una cassetta postale per un account utente che si trova in una foresta trusted, è necessario creare una cassetta postale collegata. Per ulteriori informazioni, vedere <A href="manage-linked-mailboxes-exchange-2013-help.md">Gestire le cassette postali collegate</A>.



5.  Fare clic su **Altre opzioni** per configurare le seguenti impostazioni.
    
      - **Database cassette postali**   Fare clic su **Sfoglia** per selezionare il database nel quale memorizzare la cassetta postale. Se non viene selezionato alcun database, Exchange ne assegnerà automaticamente uno.
    
      - **Archivio**   Selezionare questa casella di controllo per creare un archivio per la cassetta postale. Se viene creata una cassetta postale di archiviazione, gli elementi della cassetta postale verranno spostati automaticamente dalla cassetta postale principale all'archivio, in base alle impostazioni predefinite dei criteri di conservazione o a quelle definite.
        
        Fare clic su **Sfoglia** per selezionare nella foresta locale un database dove salvare la cassetta postale di archiviazione.
        
        Per ulteriori informazioni, vedere [Archiviazione sul posto di Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Criterio rubrica**   Utilizzare questo elenco per selezionare un criterio per la rubrica per la cassetta postale. I criteri rubrica contengono un elenco di indirizzi globale, una rubrica offline , un elenco di sale e un set di elenchi di indirizzi. Quando un ABP viene assegnato agli utenti di cassette postali, fornisce loro un accesso ad un GAL personalizzato in Outlook e Outlook Web App. Per ulteriori informazioni, vedere [Criteri delle rubriche](https://docs.microsoft.com/it-it/exchange/address-books/address-book-policies/address-book-policies).

6.  Al termine, scegliere **Salva** per creare la cassetta postale.

## Utilizzo di Shell

In questo esempio, vengono creati l'utente Chris Ashton in Active Directory e una cassetta postale nel database di cassette postali DB01 e viene abilitato un archivio. La password deve essere reimpostata all'accesso successivo. In questo esempio, viene creata una variabile ($password), viene richiesta l'immissione della password che viene poi assegnata alla variabile come un oggetto SecureString per l'impostazione del valore iniziale della password.

```powershell
    $password = Read-Host "Enter password" -AsSecureString
    New-Mailbox -UserPrincipalName chris@contoso.com -Alias chris -Archive -Database "DB01" -Name ChrisAshton -OrganizationalUnit Users -Password $password -FirstName Chris -LastName Ashton -DisplayName "Chris Ashton" 
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-Mailbox](https://technet.microsoft.com/it-it/library/aa997663\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione della cassetta postale utente con un archivio locale, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**, quindi selezionare la nuova cassetta postale utente nell'elenco. Nel riquadro dei dettagli, in **Archiviazione in locale**, confermare che sia impostato su **Abilitato**. Fare clic su **Visualizza dettagli** per visualizzare le proprietà dell'archivio, incluso il suo stato e il database delle cassette postali in cui è stato creato.

  - In Shell, eseguire il comando riportato di seguito per visualizzare le informazioni sulla nuova cassetta postale utente e sul nuovo archivio.
    ```powershell
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress,*Archive*
    ```
  - In Shell, utilizzare il cmdlet **Test-ArchiveConnectivity** per verificare la connessione dell'archivio. Per un esempio di come verificare la connessione dell'archivio, vedere la sezione relativa agli esempi in [Test-ArchiveConnectivity](https://technet.microsoft.com/it-it/library/hh529914\(v=exchg.150\)).

## Abilitazione di un archivio locale per la cassetta postale esistente

È anche possibile creare archivi per utenti esistenti che dispongono già di una cassetta postale ma che non sono abilitati per l'archivio. Questa operazione è conosciuta come *abilitazione di un archivio* per una cassetta postale esistente.

## Utilizzo dell'interfaccia di amministrazione di Exchange

1.  Accedere a **Destinatari** \> **Cassette postale**.

2.  Scegliere una cassetta postale.

3.  Nel riquadro dei dettagli, in **Archiviazione in locale**, fare clic **Abilita**.
    

    > [!TIP]
    > Inoltre, è possibile abilitare archivi in blocco selezionando più cassette postali utilizzando i tasti Maiusc e Ctrl. Dopo aver selezionato più cassette postali, nel riquadro dei dettagli, fare clic su <STRONG>Altre opzioni</STRONG>. Quindi, in <STRONG>Archivio</STRONG> scegliere <STRONG>Abilita</STRONG>.



4.  Nella pagina **Crea archiviazione in locale**, fare clic su **OK** affinché Exchange selezioni automaticamente un database di cassette postali per l'archivio oppure **Sfoglia** per specificarne uno.

## Utilizzo di Shell

In questo esempio, viene abilitato l'archivio per la cassetta postale di Tony Smith.

```powershell
Enable-Mailbox "Tony Smith" -Archive
```

In questo esempio vengono recuperate le cassette postali nel database DB01 che non dispone di un archivio locale o basato su cloud abilitato e di un nome che inizia per DiscoverySearchMailbox. Viene eseguito il piping dei risultati nel cmdlet **Enable-Mailbox** per abilitare l'archivio per tutte le cassette postali sul database di cassette postali DB01.
```powershell
    Get-Mailbox -Database DB01 -Filter {ArchiveGuid -Eq $null -AND ArchiveDomain -eq $null -AND Name -NotLike "DiscoverySearchMailbox*"} | Enable-Mailbox -Archive
```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Enable-Mailbox](https://technet.microsoft.com/it-it/library/aa998251\(v=exchg.150\)) e [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare l'avvenuta abilitazione di un archivio locale per una cassetta postale esistente, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**, quindi selezionare la cassetta postale nell'elenco. Nel riquadro dei dettagli, in **Archiviazione in locale**, confermare che sia impostato su **Abilitato**. Fare clic su **Visualizza dettagli** per visualizzare le proprietà dell'archivio, incluso il suo stato e il database delle cassette postali in cui è stato creato.

  - In Shell, eseguire il comando riportato di seguito per visualizzare le informazioni sul nuovo archivio.
    ```powershell
        Get-Mailbox <Name> | FL Name,*Archive*
    ```
  - In Shell, utilizzare il cmdlet **Test-ArchiveConnectivity** per verificare la connessione dell'archivio. Per un esempio di come verificare la connessione dell'archivio, vedere gli esempi in [Test-ArchiveConnectivity](https://technet.microsoft.com/it-it/library/hh529914\(v=exchg.150\)).

## Disabilitazione di un archivio locale

È possibile che si desideri disabilitare un archivio utente per consentire la risoluzione dei problemi o se si sposta la cassetta postale in una versione di Exchange che non supporta Archiviazione in locale. Se si disabilita un archivio locale, tutte le informazioni nell'archivio verranno mantenute nel database delle cassette postali fino al termine del periodo di conservazione delle cassette postali, dopo il quale l'archivio locale verrà eliminato definitivamente (per impostazione predefinita Exchange conserva le cassette postali disconnesse, incluse quelle di archiviazione, per 30 giorni.)


> [!IMPORTANT]
> La disabilitazione dell'archivio locale rimuoverà l'archivio dalla cassetta postale e lo contrassegnerà nel database delle cassette postali per l'eliminazione.



Se si desidera riconnettere l'archivio locale alla cassetta postale, è possibile utilizzare il cmdlet [Connect-Mailbox](https://technet.microsoft.com/it-it/library/aa997878\(v=exchg.150\)) con il parametro *Archive*.

## Utilizzo dell'interfaccia di amministrazione di Exchange

1.  Accedere a **Destinatari** \> **Cassette postale**.

2.  Scegliere una cassetta postale.

3.  Nel riquadro dei dettagli, in **Archiviazione in locale**, fare clic su **Disabilita**.
    

    > [!TIP]
    > Inoltre, è possibile disabilitare archivi in blocco selezionando più cassette postali utilizzando i tasti Maiusc e CTRL. Dopo aver selezionato più cassette postali, nel riquadro dei dettagli, fare clic su <STRONG>Altre opzioni</STRONG>. Quindi, in <STRONG>Archivio</STRONG> scegliere <STRONG>Disabilita</STRONG>.



## Utilizzo di Shell

In questo esempio, viene disabilitato l'archivio per la cassetta postale di Chris Ashton. La cassetta postale non viene disabilitata.

```powershell
Disable-Mailbox -Identity "Chris Ashton" -Archive
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Disable-Mailbox](https://technet.microsoft.com/it-it/library/aa997210\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare l'avvenuta disabilitazione di un archivio, procedere come segue:

  - Nell'interfaccia di amministrazione di Exchange, selezionare la cassetta postale. Nel riquadro dei dettagli verificare lo stato dell'archivio in **Archiviazione in locale**.

  - In Shell, eseguire il comando seguente per verificare le proprietà dell'archivio per l'utente della cassetta postale.
    ```powershell
        Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*
    ```
    Se l'archivio è disabilitato, vengono restituiti i seguenti valori per le proprietà relative all'archivio.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Proprietà</th>
    <th>Valore</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ArchiveDatabase (per archivi locali)</p></td>
    <td><p>&lt;vuoto&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>ArchiveState</p></td>
    <td><p><code>None</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>DisabledArchiveDatabase (per archivi locali)</p></td>
    <td><p>&lt;nome del database delle cassette postali&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>DisabledArchiveGuid</p></td>
    <td><p>&lt;GUID dell'archivio disabilitato&gt;</p></td>
    </tr>
    </tbody>
    </table>


## Connessione di un archivio locale

Quando si disabilita una cassetta postale di archiviazione, questa viene disconnessa. Una cassetta postale di archiviazione disconnessa viene conservata nel database di cassette postali per un determinato periodo di tempo. Per impostazione predefinita, Exchange conserva gli archivi disconnessi per 30 giorni. Durante questo periodo, è possibile ripristinare l'archivio associandolo a una cassetta postale esistente. Per conservare una cassetta postale o un archivio eliminato per un periodo di tempo inferiore o superiore, è possibile modificare il periodo di conservazione delle cassette postali eliminate.


> [!WARNING]
> Se si disabilita un archivio per un utente e poi si abilità un archivio per quello stesso utente, l'utente otterrà un nuovo archivio. Il nuovo archivio creato non contiene i dati presenti nell'archivio disconnesso dell'utente. Se si desidera riconnettere un utente al proprio archivio disconnesso, è necessario utilizzare questa procedura.




> [!NOTE]
> Non è possibile utilizzare l'Interfaccia di amministrazione di Exchange per collegare un archivio disconnesso per un utente della cassetta postale.



## Utilizzo di Shell

1.  Se non si conosce il nome dell'archivio, è possibile visualizzarlo in Shell utilizzando il comando riportato di seguito. In questo esempio viene recuperato il database delle cassette postali DB01; ne viene eseguito il piping al cmdlet **Get-MailboxStatistics** per recuperare le statistiche sulle cassette postali per tutte le cassette postali del database, quindi, viene utilizzato il cmdle **Where-Object** per filtrare i risultati e recuperare un elenco di archivi disconnessi. Il comando visualizza ulteriori informazioni sugli archivi, quali il GUID e il conteggio degli elementi.
    ```powershell
        Get-MailboxDatabase "DB01" | Get-MailboxStatistics | Where {($_.DisconnectDate -ne $null) -and ($_.IsArchiveMailbox -eq $true)} | Format-List
    ```
2.  Connettere l'archivio alla cassetta postale principale. In questo esempio, l'archivio di Chris Ashton viene connesso alla cassetta postale principale di Chris Ashton e viene utilizzato il GUID come identità dell'archivio.
    ```powershell
        Enable-Mailbox -ArchiveGuid "8734c04e-981e-4ccf-a547-1c1ac7ebf3e2" -ArchiveDatabase "DB01" -Identity "Chris Ashton"
    ```
Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [Get-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb124924\(v=exchg.150\))

  - [Get-MailboxStatistics](https://technet.microsoft.com/it-it/library/bb124612\(v=exchg.150\))

  - [Enable-Mailbox](https://technet.microsoft.com/it-it/library/aa998251\(v=exchg.150\))

## Come verificare se l'operazione ha avuto esito positivo

Per verificare l'avvenuta disconnessione di un archivio per un utente della cassetta postale, eseguire il seguente comando Shell per recuperare le proprietà dell'archivio dell'utente della cassetta postale e verificare i valori restituiti per le proprietà *ArchiveGuid* e *ArchiveDatabase*.
```powershell
    Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*
```

---
title: 'La connessione o il ripristino di una cassetta postale eliminata: Exchange 2013 Help'
TOCTitle: La connessione o il ripristino di una cassetta postale eliminata
ms:assetid: a5e6ac44-5901-4eab-9017-c6fae80a0f83
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ863438(v=EXCHG.150)
ms:contentKeyID: 50555651
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# La connessione o il ripristino di una cassetta postale eliminata

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-05-04_

È possibile utilizzare EAC o Shell per connettere una cassetta postale eliminata a un account utente di Active Directory. Quando si elimina una cassetta postale, Exchange la conserva nel database relativo e la imposta sullo stato di disabilitato. Viene eliminato anche l'account utente di Active Directory associato. La cassetta postale viene conservata fino alla scadenza del periodo di conservazione delle cassette postali eliminate, che, per impostazione predefinita, equivale a 30 giorni, quindi viene rimossa permanentemente (o *eliminata definitivamente*) dal database delle cassette postali.

Fino a quando una cassetta postale eliminata non viene eliminata definitivamente dal database delle cassette postali di Exchange, è possibile utilizzare EAC o Shell per connetterla a un account utente di Active Directory. È inoltre possibile utilizzare Shell per ripristinare il contenuto della cassetta postale eliminata in una cassetta postale esistente.

Per ulteriori informazioni sulle cassette postali disconnesse e per eseguire altre attività di gestione correlate, vedere gli argomenti seguenti:

  - [Cassette postali disconnesse](disconnected-mailboxes-exchange-2013-help.md)

  - [Disabilitazione o eliminazione di una cassetta postale](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [Connettere una cassetta postale disabilitata](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [Eliminare definitivamente una cassetta postale](permanently-delete-a-mailbox-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Creare un nuovo account utente in Active Directory a cui connettere la cassetta postale eliminata. In alternativa, utilizzare il cmdlet **Get-User** in Shell per verificare che l'account utente di Active Directory a cui connettere la cassetta postale eliminata esista e che non sia già associato a un'altra cassetta postale. Per connettere una cassetta postale eliminata a un account utente, è necessario che l'account esista e che il valore per la proprietà *RecipientType* sia pari a `User`, che indica che l'account non è ancora abilitato alla cassetta postale.
    
    Per le organizzazioni Exchange locali è possibile verificare queste informazioni anche in Utenti e computer di Active Directory.
    

    > [!IMPORTANT]
    > Quando si connettono le cassette postali collegate eliminate, delle risorse o condivise, l'account utente di Active Directory al quale si sta connettendo la cassetta postale deve essere disabilitato.



  - Per verificare che la cassetta postale eliminata che si desidera connettere a un account utente esista nel database delle cassette postali e che non sia una cassetta postale eliminata in maniera reversibile, eseguire il comando seguente.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    La cassetta postale eliminata deve essere presente nel database delle cassette postali e il valore della proprietà *DisconnectReason* deve essere `Disabled`. Se la cassetta postale è stata eliminata definitivamente dal database, il comando non restituirà alcun risultato.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## Operazione desiderata

## Connettere una cassetta postale eliminata

Quando si connette una cassetta postale eliminata, la si associa a un account utente non abilitato alla posta, ossia che non dispone di una cassetta postale esistente. Per connettere una cassetta postale eliminata a un account utente che dispone di una cassetta postale, è necessario ripristinare la cassetta postale eliminata. Per ulteriori informazioni, vedere Restore a deleted mailbox più avanti in questo argomento.

## Connessione di una cassetta postale eliminata tramite EAC

Nella procedura seguente viene descritto come connettere una cassetta postale utente eliminata a un account utente. È inoltre possibile utilizzare questa procedura per connettere le cassette postali collegate, le cassette postali delle risorse e le cassette postali condivise eliminate in un account utente.

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Fare clic su **Altro**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni"), quindi su **Connessione ad una cassetta postale**.
    
    Verrà visualizzato l'elenco delle cassette postali disconnesse sul server Exchange selezionato nell'organizzazione Exchange.
    

    > [!NOTE]
    > Nell'elenco sono incluse le cassette postali disabilitate, le cassette postali eliminate e quelle eliminate in maniera reversibile.



3.  Fare clic sulla cassetta postale eliminata che si desidera connettere a un utente, quindi su **Connetti**.

4.  Nella finestra in cui viene chiesto se si è sicuri di voler connettere la cassetta postale, fare clic su **Sì**.
    
    Viene visualizzato un elenco di account utente che non sono abilitati alla posta elettronica.

5.  Fare clic sull'utente a cui si desidera connettere la cassetta postale eliminata e selezionare **OK**.
    
    Exchange connetterà la cassetta postale eliminata all'account utente selezionato.

## Connessione di una cassetta postale eliminata tramite Shell

Utilizzare il cmdlet **Connect-Mailbox** in Shell per connettere una cassetta postale eliminata a un account utente non abilitato alla posta. È necessario specificare il tipo di cassetta postale che si sta connettendo. Negli esempi seguenti viene illustrata la sintassi per riconnettere cassette postali utente, collegate, sala, dispositivo e condivise. In tutti gli esempi il parametro *Alias* facoltativo viene utilizzato per specificare l'alias di posta elettronica, che è la parte dell'indirizzo di posta elettronica sul lato sinistro del simbolo di chiocciola (@). Se non viene incluso il parametro *Alias*, il valore specificato nel parametro *User* o *LinkedMasterAccount* viene utilizzato per creare l'alias per l'indirizzo di posta elettronica per la cassetta postale riconnessa.


> [!NOTE]
> Come affermato in precedenza, quando si connettono le cassette postali collegate, delle risorse o condivise, l'account utente di Active Directory al quale si sta connettendo la cassetta postale deve essere disabilitato.



Con questo esempio viene connessa una cassetta postale utente. Il parametro *Identity* consente di specificare il nome visualizzato della cassetta postale eliminata conservata nel database delle cassette postali denominato MBXDB01. Il parametro *User* consente di specificare l'account utente di Active Directory a cui connettere la cassetta postale.

    Connect-Mailbox -Identity "Paul Cannon" -Database MBXDB01 -User "Robin Wood" -Alias robinw


> [!NOTE]
> È inoltre possibile utilizzare i valori per le proprietà <CODE>LegacyDN</CODE> o <CODE>MailboxGuid</CODE> per identificare la cassetta postale eliminata.



In questo esempio viene connessa una cassetta postale collegata. Il parametro *Identity* consente di specificare la cassetta postale eliminata sul database delle cassette postali denominato MBXDB02. Il parametro *LinkedMasterAccount* consente di specificare l'account utente di Active Directory nella foresta di account a cui si desidera connettere la cassetta postale. Il parametro *LinkedDomainController* consente di specificare un controller di dominio nella foresta di account.

    Connect-Mailbox -Identity "Temp User" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount danpark@fabrikam.com -Alias dpark

In questo esempio viene connessa una cassetta postale sala.

    Connect-Mailbox -Identity "rm2121" -Database "MBXResourceDB" -User "Conference Room 2121" -Alias ConfRm2121 -Room

In questo esempio viene connessa una cassetta postale per apparecchiatura.

    Connect-Mailbox -Identity "MotorPool01" -Database "MBXResourceDB" -User "Van01 (12 passengers)" -Alias van01 -Equipment

Con questo esempio viene connessa una cassetta postale condivisa.

    Connect-Mailbox -Identity "Printer Support" -Database MBXDB01 -User "Corp Printer Support" -Alias corpprint -Shared


> [!NOTE]
> È inoltre possibile utilizzare i valori di <CODE>LegacyDN</CODE> o <CODE>MailboxGuid</CODE> per identificare la cassetta postale eliminata.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Connect-Mailbox](https://technet.microsoft.com/it-it/library/aa997878\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta connessione della cassetta postale eliminata a un account utente, effettuare una delle seguenti operazioni:

  - In EAC, fare clic su **Destinatari**, accedere alla pagina corretta per il tipo di cassetta postale connessa, fare clic su **Aggiorna**![Icona Aggiorna](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icona Aggiorna") e verificare che la cassetta postale sia presente nell'elenco.

  - In Utenti e computer di Active Directory fare clic con il pulsante destro del mouse sull'account utente connesso alla cassetta postale, quindi scegliere **Proprietà**. La casella **Posta elettronica** della scheda **Generale** contiene l'indirizzo di posta elettronica della cassetta postale connessa.

  - In Shell, utilizzare il seguente comando.
    
        Get-User <identity>
    
    Il valore **UserMailbox** per la proprietà *RecipientType* indica che l'account utente e la cassetta postale sono connessi. È inoltre possibile eseguire il comando **Get-Mailbox \<identity\>** per verificare che la cassetta postale sia stata connessa.

## Ripristinare una cassetta postale eliminata

È inoltre possibile utilizzare Shell per ripristinare una cassetta postale eliminata in una cassetta postale esistente utilizzando il cmdlet **New-MailboxRestoreRequest**. Quando si ripristina una cassetta postale eliminata, il contenuto viene copiato in una cassetta postale esistente, indicata come *cassetta postale di destinazione*. Una volta ripristinata, una cassetta postale eliminata continua a essere conservata nel database delle cassette postali fino a quando non viene rimossa permanentemente da un amministratore o eliminata definitivamente alla scadenza del periodo di conservazione.

Una volta completata la richiesta di ripristino della cassetta postale, per impostazione predefinita essa viene conservata per 30 giorni prima di essere rimossa. È possibile rimuoverla prima utilizzando il cmdlet **Remove-StoreMailbox**.


> [!NOTE]
> Non è possibile utilizzare EAC per ripristinare una cassetta postale eliminata.



## Ripristino di una cassetta postale eliminata tramite Shell

Per creare una richiesta di ripristino delle cassette postali, è necessario utilizzare il nome visualizzato, il nome distinto legacy (DN) oppure il GUID della cassetta postale eliminata. Utilizzare il cmdlet **Get-MailboxStatistics** per visualizzare i valori delle proprietà `DisplayName`, `MailboxGuid` e `LegacyDN` per la cassetta postale eliminata che si desidera ripristinare. Ad esempio, utilizzare il comando seguente per restituire le informazioni di tutte le cassette postali disabilitate ed eliminate nell'organizzazione.

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "Disabled"} | fl DisplayName,MailboxGuid,LegacyDN,Database

Con questo esempio viene ripristinata la cassetta postale eliminata, identificata dal parametro *SourceStoreMailbox* e viene posizionata nel database delle cassette postali MBXDB01, nella cassetta postale di destinazione Debra Garcia. Il parametro *AllowLegacyDNMismatch* viene utilizzato in modo che la cassetta postale di origine possa essere ripristinata in un'altra cassetta postale che non abbia lo stesso valore DN legacy.

    New-MailboxRestoreRequest -SourceStoreMailbox e4890ee7-79a2-4f94-9569-91e61eac372b -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

Con questo esempio viene ripristinata la cassetta postale archivio eliminata di Pilar Pinilla nella cassetta postale archivio corrente. Il parametro *AllowLegacyDNMismatch* non è necessario poiché una cassetta postale principale e la cassetta postale archivio corrispondente dispongono dello stesso DN legacy.

    New-MailboxRestoreRequest -SourceStoreMailbox "Personal Archive - Pilar Pinilla" -SourceDatabase "MDB01" -TargetMailbox pilarp@contoso.com -TargetIsArchive

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829875\(v=exchg.150\)).

## Utilizzo della Shell per ripristinare una cassetta postale eliminata cartelle pubbliche

Se viene eliminata una cassetta postale di cartelle pubbliche che si desidera ripristinare e la cassetta postale è entro il limite di mantenimento elementi eliminati (vedere [Configurare il periodo di mantenimento degli elementi eliminati e delle quote di elementi ripristinabili](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)) è possibile utilizzare il cmdlet `Connect-Mailbox` , seguito dal cmdlet `Update-StoreMailboxState` . Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Connect-Mailbox](https://technet.microsoft.com/it-it/library/aa997878\(v=exchg.150\)) e [Update-StoreMailboxState](https://technet.microsoft.com/it-it/library/jj860462\(v=exchg.150\)).

È necessario il GUID della cassetta postale eliminata cartelle pubbliche, nonché il GUID o il nome del database delle cassette postali che contiene la cassetta postale di cartelle pubbliche. Se non si dispone di queste informazioni, è possibile eseguire le operazioni seguenti:

1.  Ottenere il nome di dominio completo (FQDN) del controller di dominio e foresta di Active Directory eseguendo il cmdlet seguente:
    
        Get-OrganizationConfig | fl OriginatingServer

2.  Con le informazioni restituite dal passaggio 1, ricerca contenitore degli oggetti eliminati in Active Directory per il GUID della cassetta postale di cartelle pubbliche e il GUID o il nome del database delle cassette postali in cui era contenuta la cassetta postale eliminata cartelle pubbliche.
    

    > [!TIP]
    > È possibile cercare Deleted Objects utilizzando uno script personalizzato o utilizzando l'utilità Ldp, che può essere aperto digitando <STRONG>ldp.exe</STRONG> prompt di Powershell.



Quando si conosce il GUID cassetta postale di cartelle pubbliche eliminata e il nome o il GUID della cassetta postale di database che contenuta la cassetta postale di cartelle pubbliche, eseguita i comandi seguenti per ripristinare la cassetta postale di cartelle pubbliche.

1.  Creare un nuovo oggetto Active Directory eseguendo i comandi seguenti (è richiesto per fornire le credenziali appropriate):
    
        New-MailUser <mailUserName> -ExternalEmailAddress <emailAddress> 
        
        Get-MailUser <mailUserName> | Disable-MailUser
    
    Dove `<mailUserName>`, `<emailAddress>`e `<mailUserName>` sono valori scegliere. È necessario utilizzare lo stesso valore `<mailUserName>` nel passaggio successivo.

2.  Connettersi alla cassetta postale eliminata cartelle pubbliche per l'oggetto di Active Directory che appena creato eseguendo il comando seguente:
    
        Connect-Mailbox -Identity <public folder mailbox GUID> -Database <database name or GUID> -User <mailUserName>
    

    > [!NOTE]
    > Il parametro <CODE>Identity</CODE> specifica l'oggetto cassetta postale nel database di Exchange per la connessione a un oggetto utente di Active Directory. Nell'esempio precedente consente di specificare il GUID della cassetta postale di cartelle pubbliche, ma è inoltre possibile utilizzare il valore del nome visualizzato o il valore LegacyExchangeDN.



3.  Eseguire `Update-StoreMailboxState` sulla cassetta postale di cartelle pubbliche, in base all'esempio seguente:
    
        Update-StoreMailboxState -Identity <public folder mailbox GUID> -Database <database name or GUID>
    
    In passo 2, il parametro `Identity` accetta GUID, nome visualizzato o valori LegacyExchangeDN per la cassetta postale di cartelle pubbliche.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che è stato ripristinato correttamente una cassetta postale eliminata cartelle pubbliche, eseguire il cmdlet **Get-PublicFolder -GetChildren -\<public folder mailbox GUID\>** . Se il ripristino ha esito positivo, questo cmdlet funziona.

Per ulteriori informazioni, vedere:

  - [Connect-Mailbox](https://technet.microsoft.com/it-it/library/aa997878\(v=exchg.150\))

  - [Update-StoreMailboxState](https://technet.microsoft.com/it-it/library/jj860462\(v=exchg.150\))


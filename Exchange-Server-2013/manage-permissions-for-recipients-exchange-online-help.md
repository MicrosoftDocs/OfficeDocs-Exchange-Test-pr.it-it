---
title: 'Gestione delle autorizzazioni per i destinatari: Exchange 2013 Help'
TOCTitle: Gestione delle autorizzazioni per i destinatari
ms:assetid: 749cdfe3-496b-453f-96eb-20a0bf28fd52
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ919240(v=EXCHG.150)
ms:contentKeyID: 51407303
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione delle autorizzazioni per i destinatari

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2018-04-20_

È possibile utilizzare EAC o Shell per assegnare autorizzazioni a utenti o gruppi (denominati *delegati*) per consentire loro di aprire o inviare messaggi da altre cassette postali. Le autorizzazioni possono essere assegnate a cassette postali utente, cassette postali collegate, cassette postali per le risorse e cassette postali condivise. È inoltre possibile assegnare autorizzazioni a gruppi di distribuzione, gruppi di distribuzione dinamici e gruppi di protezione abilitati alla posta, in modo da consentire ai delegati di inviare messaggi per conto del gruppo. È possibile assegnare ai delegati le seguenti autorizzazioni per accedere alle cassette postali o per inviare messaggi per conto di gruppi o cassette postali:

  - **Accesso completo**   Questa autorizzazione consente a un delegato di aprire la cassetta postale dell'utente e di accedere al relativo contenuto. Tuttavia, l'assegnazione dell'autorizzazione Accesso completo non permette al delegato di inviare posta dalla cassetta postale. Per inviare la posta è necessario assegnare al delegato l'autorizzazione Invia come oppure Invia per conto di.
    
    L'autorizzazione Accesso completo non è disponibile durante la configurazione delle autorizzazioni per i gruppi.

  - **Invia come**   Questa autorizzazione consente ai delegati di utilizzare la cassetta postale per inviare messaggi. Dopo aver assegnato questa autorizzazione a un delegato, qualunque messaggio inviato da un delegato utilizzando la cassetta postale apparirà come se fosse stato inviato dal proprietario della cassetta postale. Tuttavia, questa autorizzazione non consente a un delegato di accedere alla cassetta postale dell'utente. Consente agli utenti solamente di aprire la cassetta postale. Se l'autorizzazione viene assegnata a un gruppo, un eventuale messaggio inviato da un delegato verrà visualizzato come messaggio inviato dal gruppo.

  - **Invia per conto di**   Anche questa autorizzazione consente a un delegato di utilizzare la cassetta postale per inviare messaggi. Una volta assegnata questa autorizzazione a un delegato, l'indirizzo **Da** di qualunque messaggio inviato dal delegato indicherà che il messaggio è stato inviato dal delegato per conto del proprietario della cassetta postale.


> [!NOTE]
> Se si assegna l'accesso completo, Invia come o invia l'autorizzazione per conto dell'utente per accedere a una cassetta postale nascosta dagli elenchi di indirizzi, il delegato non sarà in grado di aprire la cassetta postale o inviare messaggi.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 2 minuti.

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Assegnazione delle autorizzazioni a una cassetta postale

Come precedentemente affermato, le autorizzazioni possono essere assegnate a cassette postali utente, cassette postali collegate, cassette postali per le risorse e cassette postali condivise. È anche possibile utilizzare Shell per assegnare ai delegati le autorizzazioni per accedere a una cassetta postale di individuazione.

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni e delega" nella sezione "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

## Utilizzare EAC per assegnare autorizzazioni

Nella procedura seguente, viene illustrato come assegnare autorizzazioni a una cassetta postale utente. Una procedura analoga consente di assegnare autorizzazioni a cassette postali per le risorse o condivise, accedendo alla pagina **Risorse** o **Condivise** in EAC e selezionando la cassetta postale cui assegnare le autorizzazioni.

1.  In EAC, accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali, fare clic sulla cassetta postale cui si desidera assegnare autorizzazioni, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina delle proprietà della cassetta postale, fare clic su **Delega cassette postali**.

4.  Per assegnare le autorizzazioni ai delegati, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") sotto l'autorizzazione desiderata per visualizzare una pagina contenente un elenco di destinatari nell'organizzazione di Exchange a cui può essere assegnata l'autorizzazione. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").
    
    Per rimuovere un'autorizzazione per un destinatario, nell'autorizzazione approvata, selezionare il destinatario e scegliere **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

5.  Fare clic su **Salva** per salvare le modifiche.

## Utilizzare EAC per blocco assegnare le autorizzazioni

Utilizzare la procedura seguente per assegnare autorizzazioni in blocco.

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Selezionare le cassette postali che si desiderano assegnare le autorizzazioni per.

3.  Clic o toccare **altre opzioni** nel riquadro a destra e, in **Delega cassette postali** scegliere **Aggiungi**.

4.  Nella pagina **delega Aggiungi in blocco**, fare clic o toccare **Aggiungi** ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") nell'autorizzazione approvata per visualizzare una pagina in cui sono elencati tutti i destinatari dell'organizzazione di Exchange che può essere assegnata l'autorizzazione. Selezionare i destinatari a cui si desidera, aggiungerli all'elenco e quindi fare clic su **OK**.
    
    Per rimuovere un'autorizzazione per i destinatari, nell'autorizzazione approvata, selezionare i destinatari e quindi fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

## Utilizzare l'interfaccia di amministrazione di Exchange per assegnare a un utente l'autorizzazione ad inviare messaggi di posta elettronica dalla cassetta postale di un altro utente.

Nella procedura riportata di seguito viene illustrato come assegnare a un utente l'autorizzazione ad inviare messaggi di posta elettronica dalla cassetta postale di un altro utente.

1.  Nell'interfaccia di amministrazione di Exchange selezionare **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali fare clic sulla cassetta postale per cui si desidera assegnare autorizzazioni Invia come, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà della cassetta postale fare clic su **Delega cassette postali**.

4.  Per assegnare le autorizzazioni ai delegati, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") in **Invia come** o **Invia per conto di** per visualizzare una pagina in cui sono elencati tutti i destinatari dell'organizzazione di Exchange ai quali è possibile assegnare l'autorizzazione. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È possibile anche cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").
    
    L'autorizzazione **Invia come** consente al delegato di inviare messaggi di posta elettronica dalla cassetta postale.
    
    L'autorizzazione **Invia per conto di** consente al delegato di inviare messaggi di posta elettronica per conto della cassetta postale. La riga **Da** di ogni messaggio inviato da un delegato indica che tale messaggio è stato inviato dal delegato per conto del proprietario della cassetta postale.
    

    > [!NOTE]
    > Se l'utente deve anche poter aprire e visualizzare il contenuto della cassetta postale, è necessario che gli venga assegnata l'autorizzazione <STRONG>Accesso completo</STRONG>.



5.  Fare clic su **Salva** per salvare le modifiche.

## Utilizzo dell'interfaccia di amministrazione di Exchange per assegnare a un'utente l'autorizzazione a inviare posta elettronica da un gruppo

Nella procedura riportata di seguito viene illustrato come assegnare a un utente l'autorizzazione ad inviare messaggi di posta elettronica da un gruppo.

1.  Nell'interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Gruppi**.

2.  Nell'elenco dei gruppi fare clic su quello per cui si desidera assegnare autorizzazioni Invia come, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del gruppo fare clic su **Delega gruppi**.

4.  Per assegnare le autorizzazioni ai delegati, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") in **Invia come** o **Invia per conto di** per visualizzare una pagina in cui sono elencati tutti i destinatari dell'organizzazione di Exchange ai quali è possibile assegnare l'autorizzazione. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È possibile anche cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").
    
    L'autorizzazione **Invia come** consente al delegato di inviare messaggi di posta elettronica dal gruppo.
    
    L'autorizzazione **Invia per conto di** consente al delegato di inviare messaggi di posta elettronica per conto del gruppo. La riga **Da** di ogni messaggio inviato da un delegato indica che tale messaggio è stato inviato dal delegato per conto del gruppo.

5.  Fare clic su **Salva** per salvare le modifiche.

## Utilizzo dell'interfaccia di amministrazione di Exchange per assegnare autorizzazioni di accesso completo

Nella procedura riportata di seguito viene illustrato come assegnare autorizzazioni di accesso completo alla cassetta postale di un utente.

1.  Nell'interfaccia di amministrazione di Exchange selezionare **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali, fare clic sulla cassetta postale per cui si desidera assegnare autorizzazioni di accesso completo, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà della cassetta postale fare clic su **Delega cassette postali**.

4.  Per assegnare le autorizzazioni ai delegati, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") in **Accesso completo** per visualizzare una pagina contenente l'elenco di tutti i destinatari dell'organizzazione di Exchange ai quali è possibile assegnare l'autorizzazione. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È possibile anche cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").
    
    L'autorizzazione **Accesso completo** consente a un delegato di aprire la cassetta postale dell'utente e di accedere al relativo contenuto.
    

    > [!NOTE]
    > L'assegnazione dell'autorizzazione <STRONG>Accesso completo</STRONG>, tuttavia, non permette al delegato di inviare posta dalla cassetta postale. Per consentire l'invio di posta, è necessario assegnare al delegato l'autorizzazione <STRONG>Invia come</STRONG> o <STRONG>Invia per conto di</STRONG>.



5.  Fare clic su **Salva** per salvare le modifiche.

## Utilizzare Shell per assegnare autorizzazioni

Nelle sezioni riportate viene illustrato come utilizzare Shell per gestire le autorizzazioni Accesso completo, Invia come e Invia per conto di per le cassette postali.

## Gestire l'autorizzazione Accesso completo

Negli esempi riportati viene illustrato come utilizzare i cmdlet **Add-MailboxPermission** e **Remove-MailboxPermission** per gestire le autorizzazioni Accesso completo.

In questo esempio al delegato Raymond Sam viene assegnata l'autorizzazione Accesso completo alla cassetta postale di Terry Adams.

    Add-MailboxPermission -Identity "Terry Adams" -User raymonds -AccessRights FullAccess -InheritanceType all

Nell'esempio riportato, a Esther Valle viene assegnata l'autorizzazione Accesso completo alla cassetta postale di individuazione predefinita dell'organizzazione.

    Add-MailboxPermission -Identity "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User estherv -AccessRights FullAccess -InheritanceType all

Nell'esempio seguente, ai membri del gruppo di distribuzione del supporto tecnico viene concessa l'autorizzazione Accesso completo alla cassetta postale condivisa Ticket del supporto tecnico.

    Add-MailboxPermission "HelpdeskTickets" -User helpdesk -AccessRights FullAccess -InheritanceType all

In questo esempio viene rimossa dall'utente Jim Hance l'autorizzazione di accesso completo alla cassetta postale di Ayla Kol.

    Remove-MailboxPermission -Identity ayla -User "Jim Hance" -AccessRights FullAccess -Inheritance

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [Add-MailboxPermission](https://technet.microsoft.com/it-it/library/bb124097\(v=exchg.150\))

  - [Remove-MailboxPermission](https://technet.microsoft.com/it-it/library/bb125153\(v=exchg.150\))

## Gestire l'autorizzazione Invia come

Negli esempi seguenti viene illustrato come gestire le autorizzazioni Invia come in Exchange Server 2013 e in Exchange Online. In Exchange 2013, è necessario utilizzare i cmdlet **Add-ADPermission** e **Remove-ADPermission**; in Exchange Online, è necessario utilizzare i cmdlet **Add-RecipientPermission** e **Remove-RecipientPermission**. In entrambi i casi, viene utilizzato il parametro *Identity* per specificare il nome della cassetta postale per l'aggiunta o la rimozione dell'autorizzazione Invia come e il parametro *User* o *Trustee* per specificare il delegato (ad esempio, un utente o gruppo) cui verrà assegnato o verrà annullata l'assegnazione dell'autorizzazione Invia come.


> [!TIP]
> Utilizzare il cmdlet <STRONG>Get-Recipient</STRONG> per recuperare la proprietà <EM>Name</EM> per la cassetta postale e il delegato. Utilizzare questi valori per assegnare l'autorizzazione Invia come.



## Exchange Server 2013

In questo esempio viene assegnata l'autorizzazione Invia come al gruppo del supporto tecnico sulla cassetta postale condivisa del team di supporto tecnico.

    Add-ADPermission -Identity helpdesksupport -User helpdeskgroup -ExtendedRights "Send As"

In questo esempio viene rimossa l'autorizzazione Invia come per l'utente Pilar Pinilla sulla cassetta postale di James Alvord.

    Remove-ADPermission -Identity "James Alvord" -User pilarp -ExtendedRights "Send As"

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [Add-ADPermission](https://technet.microsoft.com/it-it/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/it-it/library/aa996048\(v=exchg.150\))

## Exchange Online

In questo esempio viene assegnata l'autorizzazione Invia come al gruppo di supporto stampanti sulla cassetta postale condivisa denominata Contoso Printer Support.

    Add-RecipientPermission -Identity "Contoso Printer Support" -Trustee "Printer Support" -AccessRights SendAs

In questo esempio viene rimossa l'autorizzazione Invia come per l'utente Karen Toh sulla cassetta postale per Yan Li.

    Remove-RecipientPermission -Identity "Yan Li" -Trustee "Karen Toh" -ExtendedRights SendAs

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [Add-RecipientPermission](https://technet.microsoft.com/it-it/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/it-it/library/ff945794\(v=exchg.150\))

## Gestire l'autorizzazione Invia per conto di

Negli esempi riportati viene illustrato come utilizzare il cmdlet **Set-Mailbox** per gestire le autorizzazioni Invia per conto di.

In questo esempio, al delegato Holly Holt viene assegnata l'autorizzazione Invia per conto di alla cassetta postale di Sean Chai.

    Set-Mailbox -Identity seanc@contoso.com -GrantSendOnBehalfTo hollyh

In questo esempio viene rimossa l'autorizzazione Invia per conto di sulla cassetta postale condivisa dei dirigenti Contoso assegnata al gruppo Assistenti di direzione temporanei.

    Set-Mailbox "Contoso Executives" -GrantSendOnBehalfTo @{remove="tempassistants@contoso.com"}

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare l'assegnazione corretta delle autorizzazioni a cassette postali o a cassette postali condivise, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange:
    
    1.  Accedere a **Destinatari** \> **Cassette postali** o **Condivise**, fare clic sulla cassetta postale, quindi su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    
    2.  Dalla pagina delle proprietà della cassetta postale, fare clic su **Delega cassette postali**.
    
    3.  Se sono state assegnate autorizzazioni a un destinatario, verificare che l'utente o il gruppo sia presente nell'elenco in corrispondenza dell'autorizzazione appropriata. Se sono state rimosse autorizzazioni, verificare che il destinatario non sia presente nell'elenco in corrispondenza dell'autorizzazione appropriata.

Oppure

  - In Shell, eseguire uno dei comandi seguenti, in base all'autorizzazione gestita.
    
      - **Accesso completo**
        
            Get-MailboxPermission -Identity <mailbox>
        
        Per verificare se a un delegato specifico sia stata assegnata l'autorizzazione Accesso completo, eseguire il comando riportato.
        
            Get-MailboxPermission -Identity <mailbox> -User <delegate>
    
      - **Invia come**
        
        In Exchange Server 2013, eseguire il seguente comando.
        
            Get-ADPermission -Identity <name of mailbox> -User <delegate>
        
        In Exchange Online, eseguire il seguente comando.
        
            Get-RecipientPermission -Identity <mailbox> -Trustee <delegate>
    
      - **Invia per conto di**
        
            Get-Mailbox -Identity <mailbox> | FL GrantSendOnBehalfTo

## Assegnazione delle autorizzazioni a un gruppo

Come precedentemente riportato, è possibile assegnare le autorizzazioni Invia come e Invia per conto di a gruppi di distribuzione, gruppi di distribuzione dinamici e gruppi di protezione abilitati alla posta, in modo da consentire ai delegati di inviare messaggi come gruppo o per conto del gruppo.

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di distribuzione" e "Gruppi di distribuzione dinamici" nella sezione "Autorizzazioni di provisioning dei destinatari" dell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

## Utilizzare EAC per assegnare autorizzazioni

1.  In Interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Gruppi**.

2.  Nell'elenco dei gruppi, fare clic sul gruppo cui si desidera assegnare autorizzazioni, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina delle proprietà del gruppo, fare clic su **Delega gruppi**.

4.  Per assegnare le autorizzazioni ai delegati, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") sotto l'autorizzazione desiderata per visualizzare una pagina contenente un elenco di destinatari nell'organizzazione di Exchange a cui può essere assegnata l'autorizzazione. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").
    
    Per rimuovere un'autorizzazione per un destinatario, nell'autorizzazione approvata, selezionare il destinatario e scegliere **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

5.  Fare clic su **Salva** per salvare le modifiche.

## Utilizzare Shell per assegnare autorizzazioni

Nelle sezioni riportate viene illustrato come utilizzare Shell per gestire le autorizzazioni Invia come e Invia per conto di per i gruppi.

## Gestire l'autorizzazione Invia come

Negli esempi seguenti viene illustrato come gestire le autorizzazioni Invia come per i gruppi in Exchange Server 2013 e in Exchange Online. In Exchange 2013, è necessario utilizzare i cmdlet **Add-ADPermission** e **Remove-ADPermission**. In Exchange Online, è necessario utilizzare i cmdlet **Add-RecipientPermission** e **Remove-RecipientPermission**. In entrambi i casi, viene utilizzato il parametro *Identity* per specificare il nome del gruppo per l'aggiunta o la rimozione dell'autorizzazione Invia come e il parametro *User* o *Trustee* per specificare il delegato (ad esempio, un utente o gruppo) cui verrà assegnato o verrà annullata l'assegnazione dell'autorizzazione Invia come.


> [!TIP]
> Utilizzare il cmdlet <STRONG>Get-Recipient</STRONG> per recuperare la proprietà <EM>Name</EM> per il gruppo e il delegato. Utilizzare questi valori per assegnare l'autorizzazione Invia come.



## Exchange Server 2013

In questo esempio viene assegnata l'autorizzazione Invia come al gruppo Sales Admins per il gruppo denominato Contoso Sales Info. Ciò consente ai membri del gruppo di amministratori vendite di inviare messaggi come il gruppo Contoso Sales Information.

    Add-ADPermission -Identity "Contoso Sales Info" -User "Sales Admins" -ExtendedRights "Send As"

In questo esempio viene rimossa l'autorizzazione Invia come per l'utente Alan Shen sul gruppo Corporate IT Admins.

    Remove-ADPermission -Identity "Corporate IT Admins" -User contoso\alans -ExtendedRights "Send As"

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [Add-ADPermission](https://technet.microsoft.com/it-it/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/it-it/library/aa996048\(v=exchg.150\))

## Exchange Online

In questo esempio viene assegnata l'autorizzazione Invia come al gruppo Contoso Admins per il gruppo per trasmettere i messaggi di emergenza.

    Add-RecipientPermission -Identity emergencybroadcast@contoso.com -Trustee "Contoso Admins" -AccessRights SendAs

In questo esempio viene rimossa l'autorizzazione Invia come per l'utente Walter Harp sul gruppo di protezione Printer Resources.

    Remove-RecipientPermission -Identity "Printer Resources" -Trustee walterh@contoso.com ExtendedRights SendAs

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [Add-RecipientPermission](https://technet.microsoft.com/it-it/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/it-it/library/ff945794\(v=exchg.150\))

## Gestire l'autorizzazione Invia per conto di

Negli esempi riportati viene illustrato come utilizzare il cmdlet **Set-DistributionGroup** e **Set-DynamicDistributionGroup** per gestire le autorizzazioni Invia per conto di per i gruppi.

In questo esempio, al delegato Sara Davis viene assegnata l'autorizzazione Invia per conto di al gruppo di distribuzione di supporto stampanti.

    Set-DistributionGroup -Identity printersupport@contoso.com -GrantSendOnBehalfTo sarad

In questo esempio, al delegato amministratore viene assegnata l'autorizzazione Invia per conto di al gruppo di distribuzione dinamico Tutti i dipendenti.

    Set-DynamicDistributionGroup -Identity "All Employees" -GrantSendOnBehalfTo administrator

In questo esempio viene rimossa l'autorizzazione Invia per conto di sul gruppo di distribuzione dinamico Tutti i dipendenti assegnata all'amministratore.

    Set-DynamicDistributionGroup "All Employees" -GrantSendOnBehalfTo @{remove="administrator"}

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

  - [Set-DistributionGroup](https://technet.microsoft.com/it-it/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/it-it/library/bb123796\(v=exchg.150\))

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta assegnazione di autorizzazioni a un gruppo, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange:
    
    1.  Accedere a **Destinatari** \> **Gruppi**, fare clic sul gruppo, quindi su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    
    2.  Dalla pagina delle proprietà del gruppo, fare clic su **Delega gruppi**.
    
    3.  Se sono state assegnate autorizzazioni a un destinatario, verificare che l'utente o il gruppo sia presente nell'elenco in corrispondenza dell'autorizzazione appropriata. Se sono state rimosse autorizzazioni, verificare che il destinatario non sia presente nell'elenco in corrispondenza dell'autorizzazione appropriata.

Oppure

  - In Shell, eseguire uno dei comandi seguenti, in base all'autorizzazione gestita.
    
      - **Invia come**
        
        In Exchange Server 2013, eseguire il seguente comando.
        
            Get-ADPermission -Identity <name of group> -User <delegate>
        
        In Exchange Online, eseguire il seguente comando.
        
            Get-RecipientPermission -Identity <group> -Trustee <delegate>
    
      - **Invia per conto di**
        
            Get-DistributionGroup -Identity <group> | FL GrantSendOnBehalfTo
        
        Oppure
        
            Get-DynamicDistributionGroup -Identity <group> | FL GrantSendOnBehalfTo


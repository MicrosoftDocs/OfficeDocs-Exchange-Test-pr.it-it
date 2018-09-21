---
title: 'Creazione di cassette postali utente: Exchange 2013 Help'
TOCTitle: Creazione di cassette postali utente
ms:assetid: 51a8b4c6-a53e-41c5-8bb1-ea4c0eaa0174
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ991919(v=EXCHG.150)
ms:contentKeyID: 52063069
ms.date: 04/05/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Creazione di cassette postali utente

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-04-12_

Le cassette postali costituiscono il tipo di destinatario più comune utilizzato dagli Information Worker in un'organizzazione di Exchange. Ciascuna cassetta postale è associata a un account utente di Active Directory. L'utente può utilizzare la cassetta postale per inviare e ricevere messaggi, nonché per archiviare messaggi, appuntamenti, attività, note e documenti. Creazione di cassette postali utente tramite EAC o Shell.

È inoltre possibile creare cassette postali per gli utenti esistenti che dispongono di un account utente di Active Directory ma non di una cassetta postale corrispondente. In questo caso si parla di *abilitare alle cassette postali* gli utenti esistenti.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ogni attività per la cassetta postale utente: 2-5 minuti.

  - Quando si crea un nuova cassetta postale utente, l'utilizzo dell'apostrofo (') e delle virgolette (") nell'alias o nel nome di acceso utente non è consentito. Anche se non si riceve un messaggio di errore durante la creazione della cassetta postale utente, l'utilizzo di questi caratteri può causare problemi in futuro. Ad esempio, gli utenti con autorizzazioni di accesso a una cassetta postale creata con i caratteri non supportati, potrebbero riscontrare problemi o comportamenti inaspettati.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Creare una cassetta postale utente

## Utilizzare EAC per creare una cassetta postale utente

1.  In EAC, selezionare **Destinatari** \> **Cassette postali**.

2.  Fare clic su **Nuovo** \> **Cassetta postale utente**.

3.  Nella pagina **Nuova cassetta postale utente**, nella casella **Alias** digitare l'alias dell'utente, cioè il suo alias di posta elettronica. L'alias dell'utente è la parte dell'indirizzo di posta elettronica a sinistra del simbolo di chiocciola (@). Deve essere univoco nella foresta.
    

    > [!NOTE]
    > Sei si lascia vuota questa casella, come alias di posta elettronica dell'utente viene utilizzata la parte del nome utente ricavata da <STRONG>Nome di accesso utente</STRONG>.



4.      
    Selezionare una delle seguenti opzioni:
    
      - **Utente esistente**   Selezionare questa opzione per abilitare un utente esistente alla posta e creare una cassetta postale.
        
        Fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona utente - Intera foresta**. Questa finestra di dialogo consente di visualizzare nella foresta un elenco di account utente di Active Directory che non sono abilitati alla posta o che non dispongono di cassette postali di Exchange. Selezionare gli account utente che si desidera abilitare alla posta e fare clic su **OK**. Se si seleziona questa opzione, non è necessario fornire le informazioni sull'account utente perché esistono già in Active Directory.
    
      - **Nuovo utente**   Selezionare questa opzione per creare un nuovo account utente in Active Directory e creare una cassetta postale per l'utente. Se si seleziona questa opzione, sarà necessario fornire le informazioni richieste sull'account utente.
    

    > [!NOTE]
    > L'account di Active Directory associato alle cassette postali utente deve essere ubicato nella stessa foresta del server Exchange. Per creare una cassetta postale per un account utente che si trova in una foresta trusted, è necessario creare una cassetta postale collegata. Vedere <A href="manage-linked-mailboxes-exchange-2013-help.md">Gestire le cassette postali collegate</A>.



5.      
    Se è stata selezionata l'opzione **Nuovo utente** nel passo 4, riempire le seguenti caselle nella pagina **Nuova cassetta postale utente**. Altrimenti, andare al passo 7.
    
      - **Nome**   Utilizzare questa casella per digitare il nome dell'utente.
    
      - **Iniziali**   Utilizzare questa casella per digitare le iniziali dell'utente.
    
      - **Cognome**   Utilizzare questa casella per digitare il cognome dell'utente.
    
      - **\* Nome visualizzato**   Utilizzare questa casella per digitare un nome visualizzato per l'utente. Questo è il nome che compare nell'elenco delle cassette postali nell'interfaccia di amministrazione di Exchange e nella rubrica condivisa. Per impostazione predefinita, questa casella contiene i nomi immessi nelle caselle **Nome di battesimo**, **Iniziali** e **Cognome**. Se queste caselle non sono state utilizzate, è necessario digitare un nome in questa casella perché è obbligatoria. Il nome non può superare i 64 caratteri.
    
      - **\* Nome**   Utilizzare questa casella per digitare un nome da assegnare all'utente. Questo è il nome elencato in Active Directory. Questa casella contiene i nomi immessi nelle caselle **Nome**, **Iniziali** e **Cognome**. Se queste caselle non sono state utilizzate, è necessario digitare un nome in questa casella perché è obbligatoria. Il nome non può superare i 64 caratteri.
    
      - **Unità organizzativa**   È possibile selezionare un'unità organizzativa diversa da quella predefinita (che corrisponde all'ambito dei destinatari). Se l'ambito dei destinatari è impostato a livello di foresta, il valore predefinito è impostato sul contenitore di utenti nel dominio di Active Directory contenente il computer su cui è in esecuzione l'interfaccia di amministrazione di Exchange. Se l'ambito dei destinatari viene impostato su un dominio specifico, per impostazione predefinita verrà selezionato il contenitore di utenti del dominio in questione. Se infine come ambito dei destinatari si sceglie una specifica unità organizzativa, per impostazione predefinita verrà selezionata l'unità organizzativa specificata.
        
        Per selezionare un'unità organizzativa diversa, scegliere il pulsante **Sfoglia**. La finestra di dialogo visualizzerà tutte le unità organizzative presenti nella foresta all'interno dell'ambito specificato. Selezionare l'unità organizzativa desiderata e quindi fare clic su **OK**.
    
      - **\* Nome accesso utente**   Utilizzare questa casella per digitare il nome utilizzato dall'utente per accedere alla cassetta postale e al dominio. Il nome di accesso dell'utente è costituito da un nome utente a sinistra del simbolo @ e da un suffisso a destra del simbolo. In genere, il suffisso è costituito dal nome di dominio in cui risiede l'account utente. Tenere presente che l'utilizzo dell'apostrofo (') e delle virgolette (") nel nome di acceso utente non è consentito.
        

        > [!NOTE]
        > Se il nome utente è diverso da quello utilizzato nella casella <STRONG>Alias</STRONG>, l'indirizzo di posta elettronica e il nome di accesso dell'utente saranno diversi.

    
      - **\* Nuova password**   Utilizzare questa casella per digitare la password da utilizzare per accedere alla cassetta postale.
        

        > [!NOTE]
        > Verificare che la password immessa sia conforme ai requisiti di lunghezza, complessità e cronologia del dominio in cui viene creato l'account utente.

    
      - **\* Conferma password**   Utilizzare questa casella per confermare la password digitata nella casella **Password**.
    
      - **Richiedi modifica della password al successivo accesso**   Selezionare questa casella di controllo se si desidera che l'utente reimposti la password al primo accesso alla cassetta postale.
        
        Se si seleziona questa casella di controllo, al primo accesso l'utente visualizzerà una finestra di dialogo in cui potrà modificare la password. L'utente non potrà eseguire alcuna operazione finché la password non viene modificata.

6.      
    Fare clic su **Altre opzioni** per configurare le seguenti caselle. Altrimenti, passare direttamente al passo 7 per salvare la nuova cassetta postale utente.
    
      - **Specifica database delle cassette postali**   Utilizzare questa opzione per specificare un database delle cassette postali invece che permettere a Exchange di selezionarlo automaticamente. Fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona database delle cassette postali**. In questa finestra di dialogo vengono elencati tutti i database delle cassette postali nell'organizzazione di Exchange. Per impostazione predefinita, i database delle cassette postali sono ordinati per nome. È inoltre possibile fare clic sul titolo della colonna corrispondente per ordinare i database in base al nome o alla versione del server. Selezionare il database delle cassette postali desiderato e fare clic su **OK**.
    
      - **Crea l'archivio locale per l'utente**   Selezionare questa casella di controllo per creare un archivio per la cassetta postale. Se viene creata una cassetta postale di archiviazione, gli elementi della cassetta postale verranno spostati automaticamente dalla cassetta postale principale all'archivio, in base alle impostazioni predefinite dei criteri di conservazione o a quelle definite.
        
        Fare clic su **Sfoglia** per selezionare nella foresta locale un database dove salvare la cassetta postale di archiviazione.
        
        Per ulteriori informazioni, vedere [Archiviazione sul posto di Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Criterio rubrica**   Utilizzare questa opzione per specificare un criterio per la rubrica per la cassetta postale. I criteri rubrica contengono un elenco di indirizzi globale, una rubrica offline , un elenco di sale e un set di elenchi di indirizzi. Quando un ABP viene assegnato agli utenti di cassette postali, fornisce loro un accesso ad un GAL personalizzato in Outlook e Outlook Web App. Per ulteriori informazioni, vedere [Criteri delle rubriche](https://docs.microsoft.com/it-it/exchange/address-books/address-book-policies/address-book-policies).
        
        Nell'elenco a discesa, selezionare il criterio da associare a questa cassetta postale.

7.      
    Al termine, scegliere **Salva** per creare la cassetta postale.

## Utilizzare Shell per creare una cassetta postale utente

In questo esempio vengono creati un account utente e una cassetta postale per l'utente Pilar Pinilla con i seguenti dettagli:

  - L'alias è pilarp

  - Il nome è Pilar e il cognome è Pinilla

  - Il nome e il nome visualizzato corrispondono a Pilar Pinilla

  - Il nome di accesso utente è pilarp@contoso.com

  - La password è Pa$$word1

  - La cassetta postale sarà creata nell'unità organizzativa predefinita. Per specificare un'unità organizzativa diversa, è possibile utilizzare il parametro *OrganizationalUnit*.

<!-- end list -->

    New-Mailbox -Alias pilarp -Name "Pilar Pinilla" -FirstName Pilar -LastName Pinilla -DisplayName "Pilar Pinilla" -UserPrincipalName pilarp@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)

Per informazioni sulla sintassi e sui parametri, vedere [New-Mailbox](https://technet.microsoft.com/it-it/library/aa997663\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione della cassetta postale utente, effettuare una delle seguenti operazioni:

  - In EAC, selezionare **Destinatari** \> **Cassette postali**. La nuova cassetta postale utente viene visualizzata nell'elenco delle cassette postali. In **Tipo di cassetta postale**, il tipo è **Utente**.

  - In Shell, eseguire il comando riportato di seguito per visualizzare informazioni sulla nuova cassetta postale utente.
    
    ```powershell
Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress
```

## Creare una cassetta postale per un utente esistente

È inoltre possibile creare cassette postali per gli utenti esistenti che dispongono di un account utente di Active Directory ma non di una cassetta postale corrispondente. In questo caso si parla di *abilitare alle cassette postali* gli utenti esistenti. Dopo aver abilitato alle cassette postali un utente esistente, l'utente può inviare e ricevere messaggi di posta elettronica.

## Utilizzare EAC per creare una cassetta postale per un utente esistente

1.  In EAC, selezionare **Destinatari** \> **Cassette postali**.

2.  Fare clic su **Nuovo** \> **Cassetta postale utente**.

3.  Nella pagina **Nuova cassetta postale utente**, nella casella **Alias** digitare l'alias dell'utente, cioè il suo alias di posta elettronica. L'alias dell'utente è la parte dell'indirizzo di posta elettronica a sinistra del simbolo di chiocciola (@). Deve essere univoco nella foresta.
    

    > [!NOTE]
    > Sei si lascia vuota questa casella, come alias di posta elettronica dell'utente viene utilizzata la parte del nome utente ricavata da <STRONG>Nome di accesso utente</STRONG>.



4.  Fare clic su **Utente esistente**.

5.  Fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona utente - Intera foresta**. Questa finestra di dialogo consente di visualizzare nella foresta un elenco di account utente di Active Directory che non sono abilitati alla posta o che non dispongono di cassette postali di Exchange. Selezionare gli account utente che si desidera abilitare alla posta e fare clic su **OK**.
    
    Quando si crea una cassetta postale per un utente esistente, non è necessario fornire le informazioni sull'account perché esistono già in Active Directory.
    

    > [!NOTE]
    > L'account di Active Directory associato alle cassette postali utente deve essere ubicato nella stessa foresta del server Exchange. Per creare una cassetta postale per un account utente che si trova in una foresta trusted, è necessario creare una cassetta postale collegata. Vedere <A href="manage-linked-mailboxes-exchange-2013-help.md">Gestire le cassette postali collegate</A>.



6.  Fare clic su **Altre opzioni** per configurare le seguenti caselle. Altrimenti, passare direttamente al passo 7 per salvare la nuova cassetta postale utente.
    
      - **Specifica database delle cassette postali**   Utilizzare questa opzione per specificare un database delle cassette postali invece che permettere a Exchange di selezionarlo automaticamente. Fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona database delle cassette postali**. In questa finestra di dialogo vengono elencati tutti i database delle cassette postali nell'organizzazione di Exchange. Per impostazione predefinita, i database delle cassette postali sono ordinati per nome. È inoltre possibile fare clic sul titolo della colonna corrispondente per ordinare i database in base al nome o alla versione del server. Selezionare il database delle cassette postali desiderato e fare clic su **OK**.
    
      - **Crea l'archivio locale per l'utente**   Selezionare questa casella di controllo per creare un archivio per la cassetta postale. Se viene creata una cassetta postale di archiviazione, gli elementi della cassetta postale verranno spostati automaticamente dalla cassetta postale principale all'archivio, in base alle impostazioni predefinite dei criteri di conservazione o a quelle definite.
        
        Fare clic su **Sfoglia** per selezionare nella foresta locale un database dove salvare la cassetta postale di archiviazione.
        
        Per ulteriori informazioni, vedere [Archiviazione sul posto di Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Criterio rubrica**   Utilizzare questa opzione per specificare un criterio per la rubrica per la cassetta postale. I criteri rubrica contengono un elenco di indirizzi globale, una rubrica offline , un elenco di sale e un set di elenchi di indirizzi. Quando un ABP viene assegnato agli utenti di cassette postali, fornisce loro un accesso ad un GAL personalizzato in Outlook e Outlook Web App. Per ulteriori informazioni, vedere [Criteri delle rubriche](https://docs.microsoft.com/it-it/exchange/address-books/address-book-policies/address-book-policies).
        
        Nell'elenco a discesa, selezionare il criterio da associare a questa cassetta postale.

7.  Al termine, scegliere **Salva** per creare la cassetta postale.

## Utilizzare Shell per creare una cassetta postale per un utente esistente

In questo esempio viene creata una cassetta postale per l'utente estherv@contoso.com nel database di Exchange denominato UsersMailboxDatabase.

```powershell
Enable-Mailbox estherv@contoso.com -Database UsersMailboxDatabase
```

Inoltre, è possibile utilizzare il cmdlet **Enable-Mailbox** per abilitare più utenti alla posta. È possibile eseguire questa operazione inviando i risultati del cmdlet **Get-User** al cmdlet **Enable-Mailbox**. Quando viene eseguito il cmdlet **Get-User**, è necessario restituire solo utenti non ancora abilitati alla posta. Per eseguire l'operazione, è necessario specificare il valore User con il parametro *RecipientTypeDetails*. Inoltre, è possibile limitare i risultati restituiti utilizzando il parametro *Filter* per richiedere solo utenti che soddisfino i criteri specificati. Quindi eseguire il piping dei risultati al cmdlet **Enable-Mailbox**.

Ad esempio, il comando di seguito abilita alle cassette postali gli utenti che non sono già abilitati alla posta elettronica e che dispongono di un valore nella proprietà **UserPrincipalName**, che aiuta a garantire che non si converta inavvertitamente un account di sistema in una cassetta postale.

```powershell
Get-User -RecipientTypeDetails User -Filter { UserPrincipalName -ne $Null } | Enable-Mailbox
```

Per informazioni sulla sintassi e sui parametri, vedere [Enable-Mailbox](https://technet.microsoft.com/it-it/library/aa998251\(v=exchg.150\)) e [Get-User](https://technet.microsoft.com/it-it/library/aa996896\(v=exchg.150\)).

Per ulteriori informazioni sull'esecuzione del piping, vedere [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione di una cassetta postale per un utente esistente, effettuare una delle seguenti operazioni:

  - In EAC, selezionare **Destinatari** \> **Cassette postali**. Il nuovo utente abilitato alle cassette postali utente viene visualizzato nell'elenco delle cassette postali. In **Tipo di cassetta postale**, il tipo è **Utente**.

  - In Shell, eseguire il comando riportato di seguito per visualizzare informazioni sul nuovo utente abilitato alle cassette postali.
    
    ```powershell
Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress
```
    
    Il valore per la proprietà *RecipientTypeDetails* è `UserMailbox`.


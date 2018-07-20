---
title: 'Creazione di un ambito di gestione personalizzato per le ricerche di eDiscovery sul posto: Exchange 2013 Help'
TOCTitle: Creazione di un ambito di gestione personalizzato per le ricerche di eDiscovery sul posto
ms:assetid: 1543aefe-3709-402c-b9cd-c11fe898aad1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn741464(v=EXCHG.150)
ms:contentKeyID: 62219744
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creazione di un ambito di gestione personalizzato per le ricerche di eDiscovery sul posto

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-01-21_

È possibile utilizzare un ambito di gestione personalizzato per consentire a particolari persone o gruppi di utilizzare eDiscovery sul posto per eseguire ricerche in un sottoinsieme di cassette postali nell'organizzazione Exchange 2013 o Exchange Online. Ad esempio, è possibile consentire a un responsabile dell'individuazione di cercare solo nelle cassette postali di utenti di una specifica sede o reparto. A tale scopo è possibile creare un ambito di gestione personalizzato. L'ambito di gestione personalizzato utilizza un filtro destinatario per controllare le cassette postali in cui eseguire la ricerca. Gli ambiti del filtro destinatario utilizzano filtri per mirare a specifici destinatari in base al tipo o altre proprietà.

Per eDiscovery sul posto la sola proprietà di una cassetta postale utente che può essere utilizzata per creare un filtro destinatario per un ambito personalizzato è l'appartenenza al gruppo di distribuzione (il nome proprietà effettivo è *MemberOfGroup*). Se si utilizzano altre proprietà, ad esempio *CustomAttributeN*, *Department* o *PostalCode*, la ricerca non riesce quando viene eseguita da un membro del gruppo di ruoli a cui è assegnato l'ambito personalizzato.

Per ulteriori informazioni sugli ambiti personalizzati, vedere:

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

  - [Informazioni sui filtri di ambito di gestione dei ruoli](understanding-management-role-scope-filters-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Come giù detto, è possibile utilizzare solo l'appartenenza al gruppo come filtro destinatario per creare un ambito di filtro destinatario personalizzato da usare per eDiscovery. Qualsiasi altra proprietà del destinatario non può essere utilizzata per creare un ambito personalizzato per le ricerche di eDiscovery. Tenere presente che non è possibile utilizzare neppure l'appartenenza in un gruppo di distribuzione dinamico.

  - Eseguire i passaggi da 1 e 3 per consentire a un responsabile dell'individuazione di esportare i risultati della ricerca per una ricerca eDiscovery che utilizza un ambito di gestione personalizzato.

  - Se il responsabile dell'individuazione non ha necessità di visualizzare l'anteprima dei risultati della ricerca, è possibile ignorare il passaggio 4.

  - Se il responsabile dell'individuazione non ha necessità di copiare i risultati della ricerca, è possibile ignorare il passaggio 5.

## Passaggio 1: Organizzazione degli utenti in gruppi di distribuzione per eDiscovery

Per cercare in un sottoinsieme di cassette postali in un'organizzazione o per restringere l'ambito delle cassette postali di origine in cui un risposabile dell'individuazione può eseguire ricerche, è necessario raggruppare un sottoinsieme di cassette postali in uno o più gruppi di distribuzione. Quando si crea un ambito di gestione personalizzato nel passaggio 2, è necessario utilizzare tali gruppi di distribuzione come filtro destinatario per creare un ambito di gestione personalizzato. In tal modo un responsabile dell'individuazione può cercare solo nelle cassette postali degli utenti che sono membri di un determinato gruppo.

È possibile utilizzare i gruppi di distribuzione esistenti per gli scopi di eDiscovery oppure crearne di nuovi. Vedere Ulteriori informazioni alla fine di questo argomento per suggerimenti e istruzioni per la creazione di gruppi di distribuzione che è possibile utilizzare per definire l'ambito delle ricerche di eDiscovery.

## Passaggio 2: Creazione di un ambito di gestione personalizzato

A questo punto è possibile creare un ambito di gestione personalizzato definito dall'appartenenza di un gruppo di distribuzione (utilizzando il filtro destinatario *MemberOfGroup*). Una volta applicato tale ambito a un gruppo di ruoli utilizzato per eDiscovery, i membri di tale gruppo possono eseguire ricerche nelle cassette postali degli utenti che sono membri del gruppo di distribuzione utilizzato per creare l'ambito di gestione personalizzato.

Questa procedura utilizza i comandi di Exchange Management Shell per creare un ambito di gestione personalizzato denominato Ottawa Users eDiscovery Scope. Viene specificato il gruppo di distribuzione denominato Ottawa Users per il filtro destinatario dell'ambito personalizzato.

1.  Eseguire questo comando per visualizzare e salvare le proprietà del gruppo Ottawa Users in una variabile, che sarà utilizzata nel comando successivo.
    
        $DG = Get-DistributionGroup -Identity "Ottawa Users"

2.  Eseguire questo comando per creare un ambito di gestione personalizzato in base all'appartenenza del gruppo di distribuzione Ottawa Users.
    
        New-ManagementScope "Ottawa Users eDiscovery Scope" -RecipientRestrictionFilter "MemberOfGroup -eq '$($DG.DistinguishedName)'"
    
    Il nome distinto del gruppo di distribuzione, contenuto nella variabile **$DG**, viene utilizzato per creare il filtro destinatario per il nuovo ambito di gestione.

## Passaggio 3: Creazione di un gruppo di ruoli di gestione

In questo passaggio viene creato un nuovo gruppo di ruoli di gestione e viene assegnato l'ambito personalizzato creato al passaggio 2. Aggiungere i ruoli Conservazione ai fini giudiziari e Ricerca cassette postali in modo che i membri del gruppo di ruoli possano eseguire ricerche di eDiscovery sul posto e collocare le cassette postali in Archiviazione sul posto o Conservazione per controversia legale. È possibile, inoltre, aggiungere membri a questo gruppo di ruoli per consentire loro di eseguire ricerche nelle cassette postali dei membri del gruppo di distribuzione utilizzato per creare l'ambito personalizzato al passaggio 2.

Negli esempi seguenti, il gruppo di protezione Ottawa Users eDiscovery Managers sarà aggiunto come membro di questo gruppo di ruoli. È possibile utilizzare Shell o EAC per questo passaggio.

## Utilizzare Shell per creare un gruppo di ruoli di gestione

Eseguire questo comando per creare un nuovo gruppo di ruoli di gestione che utilizza l'ambito personalizzato creato al passaggio 2. Il comando, inoltre, aggiunge i ruoli Conservazione ai fini giudiziari e Ricerca cassette postali e il gruppo di protezione Ottawa Users eDiscovery Managers come membri del nuovo gruppo di ruoli.

    New-RoleGroup "Ottawa Discovery Management" -Roles "Mailbox Search","Legal Hold" -CustomRecipientWriteScope "Ottawa Users eDiscovery Scope" -Members "Ottawa Users eDiscovery Managers"

## Utilizzare EAC per creare un gruppo di ruoli di gestione

1.  In EAC, accedere ad **Autorizzazioni** \> **Ruoli amministratore**, quindi fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  In **Nuovo gruppo di ruoli**, fornire le seguenti informazioni:
    
      - **Nome**   Immettere un nome descrittivo per il nuovo gruppo di ruoli. Per questo esempio sarà utilizzato **Ottawa Discovery Management**.
    
      - **Ambito di scrittura**   Selezionare l'ambito di gestione personalizzato creato al passaggio 2. Questo ambito sarà applicato al nuovo gruppo di ruoli.
    
      - **Ruoli**   Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e aggiungere i ruoli **Conservazione ai fini giudiziari** e **Ricerca cassette postali** al nuovo gruppo di ruoli.
    
      - **Membri**   Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e selezionare gli utenti, il gruppo di protezione o i gruppi di ruoli da aggiungere come membri del nuovo gruppo di ruoli. Per questo esempio, i membri del gruppo di protezione **Ottawa Users eDiscovery Managers** potranno eseguire ricerche solo nelle cassette postali degli utenti che sono membri del gruppo di distribuzione **Ottawa Users**.

3.  Fare clic su **Salva** per creare il gruppo di ruoli.
    
    Di seguito viene riportato un esempio che mostra come appare la finestra **Nuovo gruppo di ruoli** al termine delle operazioni.
    
    ![Creazione di un nuovo gruppo di ruoli per un ambito personalizzato](images/Dn741464.a6e3419f-d5d9-404f-890d-ad35f499756f(EXCHG.150).gif "Creazione di un nuovo gruppo di ruoli per un ambito personalizzato")  

## (Facoltativo) Passaggio 4: Aggiunta di responsabili dell'individuazione come membri del gruppo di distribuzione utilizzato per creare l'ambito di gestione personalizzato

È necessario eseguire questo passaggio solo se si desidera consentire a un responsabile dell'individuazione di visualizzare l'anteprima dei risultati della ricerca di eDiscovery.

Eseguire questo comando per aggiungere il gruppo di protezione Ottawa Users eDiscovery Managers come membro del gruppo di distribuzione Ottawa Users.

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Users eDiscovery Managers"

È inoltre possibile utilizzare EAC per aggiungere membri a un gruppo di distribuzione. Per ulteriori informazioni, vedere [Creazione e gestione dei gruppi di distribuzione](create-and-manage-distribution-groups-exchange-2013-help.md).

## (Facoltativo) Passaggio 5: Aggiunta di una cassetta postale di individuazione come membro del gruppo di distribuzione utilizzato per creare l'ambito di gestione personalizzato

È necessario eseguire questo passaggio solo se si desidera consentire a un responsabile dell'individuazione di copiare i risultati della ricerca di eDiscovery.

Eseguire questo comando per aggiungere la cassetta postale di individuazione Ottawa Users eDiscovery Managers come membro del gruppo di distribuzione Ottawa Users.

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Discovery Mailbox"


> [!NOTE]
> Per aprire una cassetta postale di individuazione e visualizzare i risultati della ricerca, è necessario assegnare ai responsabili dell'individuazione autorizzazioni di accesso completo per la cassetta postale di individuazione. Per ulteriori informazioni, vedere <A href="create-a-discovery-mailbox-exchange-2013-help.md">Creazione di una cassetta postale di individuazione</A>.



## Come verificare se l'operazione ha avuto esito positivo

Di seguito sono indicati alcuni modi per verificare se gli ambiti di gestione personalizzati per eDiscovery sono stati implementati correttamente. Al momento della verifica, accertarsi che l'utente che esegue le ricerche di eDiscovery sia un membro del gruppo di ruoli che utilizza l'ambito di gestione personalizzato.

  - Creare una ricerca di eDiscovery e selezionare il gruppo di distribuzione utilizzato per creare l'ambito di gestione personalizzato come origine delle cassette postali in cui eseguire ricerche. La ricerca deve poter essere eseguita in tutte le cassette postali.

  - Creare una ricerca di eDiscovery e cercare nelle cassette postali di un utente non membro del gruppo di distribuzione utilizzato per creare l'ambito di gestione personalizzato. La ricerca non dovrebbe riuscire perché il responsabile dell'individuazione può eseguire ricerche solo nelle cassette postali per gli utenti membri del gruppo di distribuzione utilizzato per creare l'ambito di gestione personalizzato. In tal caso, viene restituito un errore simile al seguente: "Impossibile eseguire la ricerca nella cassetta postale \<*nome della cassetta postale*\> in quanto l'utente corrente non dispone dell'autorizzazione per accedere alla cassetta postale".

  - Creare una ricerca di eDiscovery e cercare nelle cassette postali degli utenti membri del gruppo di distribuzione utilizzato per creare l'ambito di gestione personalizzato. Nella stessa ricerca, includere le cassette postali degli utenti non membri. La ricerca dovrebbe riuscire parzialmente, ossia dovrebbe poter essere eseguita nelle cassette postali dei membri del gruppo di distribuzione utilizzato per creare l'ambito di gestione personalizzato e fallire nelle cassette postali per gli utenti che non sono membri di quel gruppo.

## Ulteriori informazioni

  - Poiché in questo scenario i gruppi di distribuzione sono utilizzati per definire l'ambito delle ricerche di eDiscovery e non per il recapito dei messaggi, durante la creazione e configurazione dei gruppi di distribuzione per eDiscovery è opportuno tenere presenti le seguenti indicazioni:
    
      - Creare gruppi di distribuzione con un'appartenenza chiusa in modo che solo i proprietario di un gruppo possano aggiungere o rimuovere membri dal gruppo. Se si crea il gruppo Shell, utilizzare la sintassi `MemberJoinRestriction closed` e `MemberDepartRestriction closed`.
    
      - Abilitare la moderazione del gruppo in modo che i messaggi inviati al gruppo vengano inviati prima ai moderatori del gruppo che possono approvarli o rifiutarli. Se si crea il gruppo in Shell, utilizzare la sintassi `ModerationEnabled $true`. Se si utilizza EAC, è possibile abilitare la moderazione dopo la creazione del gruppo.
    
      - Nascondere il gruppo di distribuzione dalla rubrica condivisa dell'organizzazione. Utilizzare EAC o il cmdlet **Set-DistributionGroup** dopo aver creato il gruppo. Se si utilizza Shell, utilizzare la sintassi `HiddenFromAddressListsEnabled $true`.
    
    Nell'esempio seguente, il primo comando crea un gruppo di distribuzione con appartenenza chiusa e moderazione abilitata. Il secondo comando nasconde il gruppo dalla rubrica condivisa.
    ```
    New-DistributionGroup -Name "Vancouver Users eDiscovery Scope" -Alias VancouverUserseDiscovery -MemberJoinRestriction closed -MemberDepartRestriction closed -ModerationEnabled $true
    ```
    ```
    Set-DistributionGroup "Vancouver Users eDiscovery Scope" -HiddenFromAddressListsEnabled $true
    ```

    Per ulteriori informazioni sulla creazione e sulla gestione dei gruppi di distribuzione, vedere [Creazione e gestione dei gruppi di distribuzione](create-and-manage-distribution-groups-exchange-2013-help.md).

  - Anche se è possibile utilizzare solo l'appartenenza al gruppo di distribuzione come filtro destinatario per un ambito di gestione personalizzato per eDiscovery, è possibile utilizzare altre proprietà del destinatario per aggiungere membri a tale gruppo di distribuzione. Di seguito sono forniti alcuni esempi di utilizzo dei cmdlet **Get-Mailbox** e**Get-Recipient** per restituire uno specifico gruppo di utenti in base all'utente comune o agli attributi della cassetta postale.
    ```
    Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    ```
    ```
    Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "VancouverSubsidiary"'
    ```
    ```
    Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    ```
    ```
    Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    ```
    ```
    Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -OrganizationalUnit "namsr01a002.sdf.exchangelabs.com/Microsoft Exchange Hosted Organizations/contoso.onmicrosoft.com"
    ```

  - È possibile utilizzare gli esempi del punto precedente per creare una variabile da usare con il cmdlet **Add-DistributionGroupMember** per aggiungere un gruppo di utenti a un gruppo di distribuzione. Nell'esempio seguente, il primo comando crea una variabile che contiene tutte le cassette postali degli utenti con il valore **Vancouver** per la proprietà *Department* nell'account utente. Il secondo comando aggiunge tali utenti al gruppo di distribuzione Vancouver Users.
    ```
    $members = Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "Vancouver"'
    ```
    ```
    $members | ForEach {Add-DistributionGroupMember "Ottawa Users" -Member $_.Name}
    ```

  - È possibile utilizzare il cmdlet **Add-RoleGroupMember** per aggiungere un membro a un gruppo di ruoli esistente utilizzato per definire l'ambito delle ricerche di eDiscovery. Ad esempio, il comando seguente aggiunge l'utente admin@ottawa.contoso.com al gruppo di ruoli Ottawa Discovery Management.
    
        Add-RoleGroupMember "Vancouver Discovery Management" -Member paralegal@vancouver.contoso.com
    
    È inoltre possibile utilizzare EAC per aggiungere membri a un gruppo di ruoli. Per ulteriori informazioni, vedere la sezione "Aggiungere membri a un gruppo di ruoli" in [Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md).

  - In Exchange Online un ambito di gestione personalizzato utilizzato per eDiscovery non può essere utilizzato per la ricerca delle cassette postali inattive. Ciò avviene perché una cassetta postale inattiva non può essere un membro di un gruppo di distribuzione. Ad esempio, si supponga che un utente sia membro del gruppo di distribuzione che è stato utilizzato per creare un ambito di gestione personalizzata per eDiscovery. Quindi quell'utente lascia l'organizzazione e delle relative cassette postali sono rese inattive (da inserire una conservazione per controversia legale o sul posto legale della cassetta postale e quindi eliminare l'account utente di Office 365 corrispondente). Il risultato è che l'utente viene rimosso come membro di qualsiasi gruppo di distribuzione, tra cui il gruppo è stato utilizzato per creare l'ambito di gestione personalizzato utilizzato per eDiscovery. Se un responsabile dell'individuazione (che è un membro del gruppo di ruoli a cui è assegnato l'ambito di gestione personalizzato) tenta di cercare la cassetta postale inattiva, la ricerca avrà esito negativo. Per eseguire la ricerca delle cassette postali inattive, un responsabile dell'individuazione deve essere un membro del gruppo di ruoli gestione individuazione o un gruppo di ruolo disponga delle autorizzazioni per l'intera organizzazione di ricerca.
    
    Per ulteriori informazioni sulle cassette postali inattive, vedere [Cassette postali inattive in Exchange Online](https://technet.microsoft.com/it-it/library/dn798632\(v=exchg.150\)).


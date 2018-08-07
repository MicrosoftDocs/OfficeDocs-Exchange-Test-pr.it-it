---
title: 'Ridurre dimens. cassetta postale individuaz. in Exchange: Exchange 2013 Help'
TOCTitle: Ridurre le dimensioni di una cassetta postale di individuazione in Exchange
ms:assetid: fa762d14-f942-4728-8813-887d11441a68
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn750895(v=EXCHG.150)
ms:contentKeyID: 62371317
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ridurre le dimensioni di una cassetta postale di individuazione in Exchange

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Cassetta postale di individuazione che supera il limite di 50 GB Questo problema può essere risolto creando nuove cassette di individuazione e copiando i risultati della ricerca dalla cassetta di individuazione grande alle nuove.

## Motivo per l'esecuzione di questa operazione

In Exchange Server 2013 e Exchange Online, la dimensione massima delle cassette postali di individuazione, che vengono utilizzate per memorizzare i risultati della ricerca eDiscovery sul posto, è 50 GB. Prima del limite delle dimensioni correnti, sono stati in grado di aumentare la quota di archiviazione a più di 50 GB, che ha comportato con cassette postali di individuazione molto dimensioni superiori a 50 GB. Esistono tre tipi di problemi con le cassette postali di individuazione che sono superiori a 50 GB:

  - Non sono supportate.

  - Non possono essere migrate a Office 365.

  - Se le cassette postali di individuazione in Exchange Server 2010, non possono essere aggiornate a Exchange Server 2013.

## Il processo in breve

Di seguito vengono descritte in breve le operazioni necessarie per ridurre le dimensioni di una cassetta postale di individuazione che supera il limite di 50 GB:

1.  Create cassette postali di individuazione aggiuntive in cui distribuire i risultati della ricerca.

2.  Copy i risultati della ricerca dalla cassetta postale di individuazione esistente in una o più delle nuove cassette postali di individuazione.

3.  Delete le ricerche eDiscovery dalla cassetta postale di individuazione originale per ridurne le dimensioni.

La strategia presentata qui consente di raggruppare i risultati della ricerca della cassetta postale di individuazione originale in ricerche eDiscovery distinte in base agli intervalli di data. Si tratta di un modo rapido per copiare un gran numero di risultati della ricerca una nuova cassetta postale di individuazione. Nell'immagine seguente viene illustrato questo approccio.

![Riduzione delle dimensioni di una cassetta postale di individuazione](images/Dn750895.4400df18-c7ed-4c62-b304-f9060ffbdba5(EXCHG.150).gif "Riduzione delle dimensioni di una cassetta postale di individuazione")

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: Il tempo necessario varia in base al numero e alle dimensioni dei risultati della ricerca che saranno copiati nelle diverse cassette postali di individuazione.

  - Eseguire il comando seguente per determinare le dimensioni delle cassette postali di individuazione all'interno dell'organizzazione.
    
        Get-Mailbox -RecipientTypeDetails DiscoveryMailbox | Get-MailboxStatistics | FL DisplayName,TotalItemSize

  - Stabilire se è necessario conservare tutti o alcuni dei risultati della ricerca della cassetta postale di individuazione che supera il limite di 50 GB. Attenersi ai passaggi in questo argomento per conservare i risultati della ricerca copiandoli in un'altra cassetta postale di individuazione. Se non è necessario conservare i risultati di una specifica ricerca eDiscovery, è possibile eliminare la ricerca, come spiegato nel passaggio 3. Eliminando una ricerca, saranno eliminati i risultati della ricerca dalla cassetta postale di individuazione.

  - Se non si ha bisogno dei risultati della ricerca di una cassetta postale di individuazione che supera il limite di 50 GB, è possibile eliminarli. Se si tratta della cassetta postale di individuazione predefinita creata al momento del provisioning dell'organizzazione Exchange, è possibile ricrearla. Per ulteriori informazioni, vedere [Elimina e ricrea la cassetta postale di individuazione predefinita in Exchange](delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md).

  - Per le azioni legali correnti, è possibile decidere di esportare i risultati di determinate ricerche eDiscovery in file .pst. In tal modo, i risultati di una specifica richiesta vengono conservati. Oltre ai file .pst contenenti i risultati della ricerca, viene esportato anche un registro dei risultati della ricerca (formato .csv) contenente una voce per ciascun messaggio restituito nei risultati della ricerca. Ogni voce di questo file identifica la cassetta postale di origine in cui si trova il messaggio. Per ulteriori informazioni, vedere [Esportazione dei risultati della ricerca eDiscovery in un file PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md).
    
    Dopo aver esportato i risultati della ricerca nei file .pst, per importarli in una nuova cassetta postale di individuazione sarà necessario utilizzare Outlook.

## Passaggio 1: Creare cassette postali di individuazione

Il primo passaggio consiste nel creare cassette postali di individuazione aggiuntive in modo da poter copiare i risultati della ricerca dalla cassetta postale di individuazione che ha superato le dimensioni limite. Sulla base del limite di 50 GB per le cassette postali di individuazione, stabilire il numero di cassette postali di individuazione necessarie e crearle. Sarà quindi necessario assegnare a utenti o gruppi le autorizzazioni necessarie per aprire queste nuove cassette postali di individuazione.

1.  Eseguire il comando seguente per creare una nuova cassetta postale di individuazione.
    
        New-Mailbox -Name <discovery mailbox name> -Discovery

2.  Eseguire il seguente comando per assegnare a un utente o a un gruppo le autorizzazioni per aprire la cassetta postale di individuazione e visualizzare i risultati della ricerca.
    
        Add-MailboxPermission <discovery mailbox name> -User <name of user or group> -AccessRights FullAccess -InheritanceType all

## Passaggio 2: Copiare i risultati della ricerca in una cassetta postale di individuazione

Il passaggio successivo consiste nell'utilizzare il cmdlet **New-MailboxSearch** per copiare i risultati della ricerca dalla cassetta postale di individuazione esistente a una nuova cassetta postale di individuazione creata nel passaggio precedente. Questa procedura utilizza i parametri *StartDate* e *EndDate* per definire gli ambiti della ricerca come batch non superiori a 50 GB. Tale operazione potrebbe richiedere una fase di test (con la stima dei risultati della ricerca) per definire con esattezza le dimensioni dei risultati della ricerca.

1.  Eseguire il comando seguente per creare una nuova ricerca eDiscovery.
    
        New-MailboxSearch -Name "Search results from 2010" -SourceMailboxes "Discovery Search Mailbox" -StartDate "01/01/2010" -EndDate "12/31/2010" -TargetMailbox "Discovery Mailbox Backup 01" -EstimateOnly -StatusMailRecipients admin@contoso.com
    
    In questo esempio vengono utilizzati i seguenti parametri:
    
      - *Name*   Questo parametro consente di specificare il nome della nuova ricerca eDiscovery. Poiché l'ambito della ricerca viene definito tramite le date di invio e ricezione, è utile che il nome della ricerca includa l'intervallo di date.
    
      - *SourceMailboxes*   Questo parametro consente di specificare la cassetta postale di individuazione predefinita. È inoltre possibile specificare il nome di un'altra cassetta postale di individuazione che ha superato il limite di dimensione.
    
      - *StartDate* e *EndDate*   Questi parametri consentono di specificare l'intervallo di date dei risultati della ricerca nella cassetta postale di individuazione predefinita che è necessario includere nei risultati della ricerca.
        

        > [!NOTE]
        > Per le date, utilizzare il formato breve mm/gg/aaaa, anche se le impostazioni Opzioni internazionali del computer locale sono configurate con un formato differente, ad esempio gg/mm/aaaa. Ad esempio, utilizzare <STRONG>01/03/2014</STRONG> per specificare 1 marzo 2014.

    
      - *TargetMailbox*   Questo parametro consente di specificare che i risultati della ricerca devono essere copiati nella cassetta postale di individuazione denominata "Discovery Mailbox Backup 01".
    
      - *EstimateOnly*   Questo parametro consente di specificare che sarà fornita solo una stima del numero di elementi che saranno restituiti una volta avviata la ricerca. Se non si include questo parametro, una volta iniziata la ricerca, i messaggi vengono copiati nella cassetta postale di destinazione. Se si utilizza questo parametro, è possibile regolare gli intervalli di date per aumentare o ridurre il numero dei risultati della ricerca.
    
      - *StatusMailRecipients*   Questo parametro consente di specificare che il messaggio di stato deve essere inviato al destinatario specificato.

2.  Una volta creata la ricerca, avviarla utilizzando la Shell oppure l'interfaccia di amministrazione di Exchange (EAC).
    
      - **Utilizzo della Shell:**  Eseguire il seguente comando per avviare la ricerca creata nel passaggio precedente. Poiché al momento della creazione della ricerca è stato incluso il parametro *EstimateOnly*, i risultati della ricerca non saranno copiati nella cassetta postale di individuazione di destinazione.
        
            Start-MailboxSearch "Search results from 2010"
    
      - **Utilizzo di EAC:**  Accedere a **Gestione conformità** \> **In-Place eDiscovery e In-Place Hold**. Selezionare la ricerca creata nel passaggio precedente, fare clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca"), quindi fare clic su **Stima dei risultati della ricerca**.

3.  Se necessario, regolare l'intervallo di date in modo da aumentare o ridurre la quantità di risultati della ricerca restituiti. Se si modifica l'intervallo di date, eseguire nuovamente la ricerca per ottenere una nuova stima dei risultati. Provare a modificare il nome della ricerca in modo da riflettere il nuovo intervallo di date.

4.  Una volta terminato il test della ricerca, utilizzare la Shell o EAC per copiare i risultati della ricerca nella cassetta postale di individuazione di destinazione.
    
      - **Utilizzo della Shell:**  Eseguire i seguenti comandi per copiare i risultati della ricerca. È necessario rimuovere il parametro *EstimateOnly* prima di poter copiare i risultati della ricerca.
      ```
      Set-MailboxSearch "Search results from 2010" -EstimateOnly $false
      ```
      ```
      Start-MailboxSearch "Search results from 2010"
      ```
      - **Utilizzo di EAC:**  Accedere a **Gestione conformità** \> **In-Place eDiscovery e In-Place Hold**. Selezionare la ricerca, fare clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca"), quindi fare clic su **Copiare i risultati della ricerca**.
    
    Per ulteriori informazioni, vedere [Copiare i risultati della ricerca eDiscovery in una cassetta postale di individuazione](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md).

5.  Ripetere i passaggi da 1 a 4 per creare nuove ricerche per intervalli di date aggiuntive. Includere l'intervallo di date nel nome della nuova ricerca per indicare l'intervallo dei risultati. Per accertarsi che nessuna delle cassette postali di individuazione superi il limite di 50 GB, utilizzare cassette postali di individuazione diverse come cassetta postale di destinazione.

## Passaggio 3: Eliminare ricerche eDiscovery

Dopo aver copiato i risultati della ricerca dalla cassetta postale di individuazione originale a un'altra cassetta postale di individuazione, è possibile eliminare le ricerche eDiscovery originali. Eliminando una ricerca eDiscovery, i risultati della ricerca verranno eliminati dalla cassetta postale di individuazione in cui sono archiviati.

Prima di eliminare una ricerca, è necessario eseguire il seguente comando per identificare le dimensioni dei risultati della ricerca che sono stati copiati in una cassetta postale di individuazione per tutte le ricerche dell'organizzazione.

    Get-MailboxSearch | FL Name,TargetMailbox,ResultSizeCopied

È possibile utilizzare la Shell o EAC per eliminare una ricerca di eDiscovery.

  - **Utilizzo della Shell:**  Eseguire il comando riportato di seguito.
    
        Remove-MailboxSearch -Identity <name of search>

  - **Utilizzo di EAC:**  Accedere a **Gestione conformità** \> **In-Place eDiscovery e In-Place Hold**. Selezionare la ricerca che si desidera eliminare e fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

## Come verificare se l'operazione ha avuto esito positivo

Una volta eliminate le ricerche di eDiscovery, per rimuovere i risultati dalla cassetta postale di individuazione in cui erano archiviati, eseguire il seguente comando per visualizzare le dimensioni di una determinata cassetta postale di individuazione.

    Get-Mailbox <name of discovery mailbox> | Get-MailboxStatistics | FL TotalItemSize


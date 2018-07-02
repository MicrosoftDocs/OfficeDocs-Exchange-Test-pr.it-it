---
title: 'Copiare i risultati della ricerca eDiscovery in una cassetta postale di individuazione: Exchange 2013 Help'
TOCTitle: Copiare i risultati della ricerca eDiscovery in una cassetta postale di individuazione
ms:assetid: bff2ce89-9e6f-494a-bd6a-2f2011507845
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn624163(v=EXCHG.150)
ms:contentKeyID: 61183416
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Copiare i risultati della ricerca eDiscovery in una cassetta postale di individuazione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-02-24_

Dopo aver creato una ricerca eDiscovery In locale, è possibile utilizzare EAC per copiare i risultati di una cassetta postale di individuazione. È inoltre possibile utilizzare Shell per avviare una ricerca eDiscovery che è stata creata utilizzando il cmdlet **New-MailboxSearch** , che verrà copiato i risultati per la cassetta postale di individuazione che è stata specificata al momento della creazione della ricerca.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti o più tempo in base al numero di elementi delle cassette postali restituiti nei risultati della ricerca

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "eDiscovery locale" nell'argomento[Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Una ricerca eDiscovery deve essere creato tramite EAC o Shell, prima di copiare i risultati della ricerca. Per ulteriori informazioni, vedere [Creazione di una ricerca eDiscovery sul posto](create-an-in-place-ediscovery-search-exchange-2013-help.md).

  - Exchange 2013 Il programma di installazione consente di creare una cassetta postale di individuazione denominata una **Cassetta postale di individuazione** per copiare i risultati della ricerca. La cassetta postale di individuazione viene creata anche in Exchange Online per impostazione predefinita. È possibile creare cassette postali di individuazione aggiuntive. Per ulteriori informazioni, vedere [Creazione di una cassetta postale di individuazione](create-a-discovery-mailbox-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzare EAC per copiare i risultati della ricerca

1.  In EAC, andare a **Gestione conformità** \> **eDiscovery sul posto e conservazione**.

2.  Nella visualizzazione elenco, selezionare una ricerca eDiscovery.

3.  Fare clic su **Ricerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca"), quindi su **Copia risultati della ricerca** dall'elenco a discesa.

4.  In **Copia risultati della ricerca**, scegliere una delle seguenti opzioni:
    
      - **Includi elementi non ricercabili**    Selezionare questa casella di controllo per includere gli elementi delle cassette postali che non eseguire la ricerca (ad esempio, i messaggi con allegati tipi di file che risulta impossibile indicizzare attraverso Exchange ricerca). Per ulteriori informazioni, vedere [Elementi non ricercabili in Exchange eDiscovery](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).
    
      - **Abilita la deduplicazione**   Selezionare questa casella di controllo per escludere i messaggi duplicati. Nella cassetta postale di individuazione verrà copiata una sola istanza del messaggio.
    
      - **Abilita la registrazione completa**   Selezionare questa casella di controllo per includere un registro completo nei risultati della ricerca.
    
      - **Inviami una e-mail quando la copia è stata completata**   Selezionare questa casella di controllo per ricevere una notifica tramite posta elettronica al termine della ricerca.
    
      - **Copia i risultati in questa cassetta postale di individuazione**   Fare clic su **Sfoglia** per selezionare la cassetta postale di individuazione in cui si desidera copiare i risultati della ricerca.
        
        ![Copia risultati ricerca](images/Dn624163.875e25ed-8308-408c-92c4-8c76fc9d9bfc(EXCHG.150).gif "Copia risultati ricerca")  

5.  Fare clic su **Copia** per avviare il processo per copiare i risultati della ricerca nella cassetta postale di individuazione specificata.

6.  Fare clic su **Aggiorna**![Icona Aggiorna](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icona Aggiorna") per aggiornare le informazioni sullo stato della copia visualizzate nel riquadro dei dettagli.

7.  Al termine della copia, fare clic su **Apri** per aprire la cassetta postale di individuazione e visualizzare i risultati della ricerca.

## Utilizzo della Shell per copiare i risultati di ricerca

Dopo aver utilizzato il cmdlet **New-MailboxSearch** per creare una ricerca eDiscovery In locale, è necessario avviare la ricerca per copiare i messaggi per la cassetta postale di individuazione specificato nel parametro *TargetMailbox* . Per informazioni sulla creazione di ricerche eDiscovery utilizzando Shell, vedere:

  - [Use the Shell to create an In-Place eDiscovery search](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [New-MailboxSearch](https://technet.microsoft.com/it-it/library/dd298064\(v=exchg.150\))

Ad esempio, eseguire il comando seguente per avviare una ricerca eDiscovery denominata *Fabrikam indagini* per copiare i risultati della ricerca per la cassetta postale di individuazione specificato.

    Start-MailboxSearch "Fabrikam Investigation"

Se si utilizza l'opzione *EstimateOnly* per ottenere una stima dei risultati della ricerca, è necessario rimuovere il commutatore prima di copiare i risultati della ricerca. È inoltre necessario specificare una cassetta postale di individuazione di copiare per eseguire la ricerca dei risultati. Si supponga ad esempio che una ricerca solo stima creata utilizzando il comando seguente:

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeUnsearchableItems

Per copiare i risultati della ricerca in una cassetta postale di individuazione, eseguire i comandi seguenti:

    Set-MailboxSearch "FY13 Q2 Financial Results" -EstimateOnly $false -TargetMailbox "Discovery Search Mailbox"

    Start-MailboxSearch "FY13 Q2 Financial Results"

## Ulteriori informazioni sulla copia dei risultati di ricerca

  - Dopo aver copiato i risultati della ricerca per la cassetta postale di individuazione, è possibile esportare i risultati della ricerca in un file PST. Per ulteriori informazioni, vedere [Esportazione dei risultati della ricerca eDiscovery in un file PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md).

  - Per ulteriori informazioni sugli elementi non ricercabili, vedere [Elementi non ricercabili in Exchange eDiscovery](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

  - Se si sta copiando tutto il contenuto delle cassette postali all'interno di un intervallo di date specifiche (se non viene specificata una qualsiasi parola chiave nei criteri di ricerca), quindi tutti gli elementi non ricercabili in tale intervallo di date verranno automaticamente inclusi nei risultati della ricerca. Pertanto, non selezionare la casella di controllo **Includi gli elementi non ricercabili** durante la copia dei risultati di ricerca. In caso contrario, una copia di tutti gli elementi non ricercabili verrà copiata nella cassetta postale di individuazione.

  - Oltre a copiare i risultati della ricerca per una cassetta postale di individuazione, si può stimare o visualizzare in anteprima i risultati della ricerca per una ricerca selezionata.
    
      - **Risultati della ricerca Estimate**   Questa opzione consente di ottenere una stima delle dimensioni totali e numero di elementi che verranno restituiti dalla ricerca in base ai criteri specificati. Stime vengono visualizzate nel riquadro dei dettagli in EAC.
    
      - **Risultati della ricerca di anteprima**   Questa opzione consente di visualizzare in anteprima i risultati di ricerca restituiti dalla ricerca invece di copiarli in una cassetta postale di individuazione per visualizzare. Consente di determinare rapidamente se i risultati della ricerca sono pertinenti. Dopo che visualizzare in anteprima i risultati, è possibile modificare le query di ricerca per limitare i risultati di ricerca e rieseguire la ricerca. Gli elementi nella pagina anteprima sono di sola lettura versioni dei risultati della ricerca effettivo, in modo che non è possibile spostare, modificare, eliminare o inoltrare nella pagina di anteprima.
    
    Per ulteriori informazioni, vedere [stima o anteprima dei risultati di ricerca](create-an-in-place-ediscovery-search-exchange-2013-help.md).


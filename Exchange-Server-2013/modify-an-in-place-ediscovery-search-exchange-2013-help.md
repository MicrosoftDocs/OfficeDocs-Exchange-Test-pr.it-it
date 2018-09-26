---
title: 'Modificare una ricerca eDiscovery In locale: Exchange 2013 Help'
TOCTitle: Modificare una ricerca eDiscovery In locale
ms:assetid: 3162743c-cc12-4997-91e0-bcbfea8bcb17
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335182(v=EXCHG.150)
ms:contentKeyID: 50480273
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare una ricerca eDiscovery In locale

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-08-27_

Dopo aver creato una ricerca eDiscovery In locale, è possibile modificare in modo da modificare i parametri di ricerca. Ad esempio, è possibile modificare le cassette postali di cui viene eseguita la ricerca, gli intervalli di date, parole chiave, le opzioni di registrazione o è possibile specificare una cassetta postale di individuazione diversa per l'archiviazione dei risultati della ricerca. Le modifiche apportate alle proprietà di ricerca da utilizzare quando si riavvia la ricerca.


> [!WARNING]
> Se si esegue una ricerca eDiscovery In locale, è necessario arrestare prima di apportare modifiche. Quando si riavvia la ricerca, i risultati di ricerca è stata eseguita l'ultima volta vengono rimossi dalla cassetta postale di individuazione. Tuttavia, vengono salvati i registri delle ricerche precedenti.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2-5 minuti.

  - Una ricerca eDiscovery In locale è stata creata e non è in esecuzione.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "eDiscovery locale" nell'argomento[Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Operazione desiderata

## Utilizzare EAC per modificare una ricerca eDiscovery In locale

1.  Accedere a **Gestione conformità** \> **eDiscovery e conservazione in locale**.

2.  Nella visualizzazione elenco, selezionare la ricerca di eDiscovery In locale che si desidera modificare e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  **In-Place eDiscovery e archiviazione**, è possibile modificare le impostazioni seguenti:
    
      - Nella pagina **nome** modificare il nome per la ricerca e una descrizione facoltativa.
    
      - Nella pagina delle **cassette postali**, modificare le cassette postali per la ricerca. È possibile eseguire una ricerca tutte le cassette postali o selezionare quelle specifiche per la ricerca.
        

        > [!IMPORTANT]
        > È possibile utilizzare l'opzione <STRONG>di ricerca tutte le cassette postali</STRONG> per effettuare tutte le cassette postali sui server cassette postali Exchange 2013 in attesa. Per creare un'archiviazione sul posto, è necessario selezionare <STRONG>le cassette postali specificare la ricerca</STRONG>. Per ulteriori informazioni, vedere <A href="https://docs.microsoft.com/it-it/exchange/security-and-compliance/create-or-remove-in-place-holds">Creare o rimuovere un'archiviazione sul posto</A>.

    
      - Nella pagina **query di ricerca**, modificare i campi seguenti:
        
          - **Includono tutto il contenuto delle cassette postali utente**    Selezionare questa opzione per archiviare tutto il contenuto nelle cassette postali selezionate in attesa.
        
          - **Filtro basato su criteri**   Selezionare questa opzione per specificare i criteri di ricerca, inclusi parole chiave, data di inizio e fine, indirizzo di mittente e destinatario e tipi di messaggi.
    
      - Nella pagina **Conservazione In locale**, selezionare la casella di controllo **contenuto locale che corrispondono alla query di ricerca di cassette postali selezionate in attesa** e quindi selezionare una delle opzioni seguenti per inserire gli elementi nella conservazione In locale:
        
          - **In mantenimento illimitato**   Selezionare questa opzione per impostare gli elementi restituiti su un mantenimento illimitato. Gli elementi conservati verranno mantenuti fino a quando la cassetta postale non sarà stata rimossa dalla ricerca o non sarà stata eliminata la ricerca.
        
          - **Specifica numero di giorni di archiviazione degli elementi in relazione alla data di ricezione** Utilizzare questa opzione per conservare gli elementi per un periodo determinato. Ad esempio, è possibile utilizzare questa opzione se l'organizzazione richiede che tutti i messaggi vengano conservati per almeno sette anni. È possibile utilizzare una conservazione in locale *basata sul tempo* insieme al criterio di conservazione per essere certi che gli elementi vengano eliminati dopo sette anni.
            

            > [!IMPORTANT]
            > Quando le cassette postali o gli elementi vengono messi nell'archiviazione sul posto per motivi legali, si consiglia in genere di conservarli in modo illimitato e rimuovere la conservazione una volta terminati la causa o l'indagine.



4.  Fare clic su **Salva**.

## Utilizzo della Shell per modificare una ricerca eDiscovery In locale

Questo esempio viene modificata la ricerca di eDiscovery In locale ricerca Project Contoso per la ricerca di cassette postali appartenenti ai membri del gruppo di distribuzione DG-mondo.

```powershell
Set-MailboxSearch -Identity "Search-Project Contoso" -SourceMailboxes "DG-ProjectManagers"
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che sia stata modificata correttamente una ricerca eDiscovery In locale, effettuare una delle operazioni seguenti:

  - Utilizzare EAC per controllare le proprietà della ricerca.

  - Utilizzare il cmdlet **Get-MailboxSearch** dalla Shell per verificare le proprietà della ricerca. Per esempi di come controllare le proprietà di una cassetta postale di ricerca, vedere la sezione "Esempi" in [Get-MailboxSearch](https://technet.microsoft.com/it-it/library/dd351021\(v=exchg.150\)).


> [!NOTE]
> Se si utilizza <STRONG>Get-MailboxSearch</STRONG> in Exchange Online per recuperare informazioni su una ricerca eDiscovery, è necessario specificare il nome di una ricerca per restituire un elenco completo delle proprietà di ricerca. ad esempio, <CODE>Get-MailboxSearch "Contoso Legal Case"</CODE>. Se si esegue il cmdlet <STRONG>Get-MailboxSearch</STRONG> senza alcun parametro, non vengono restituite le proprietà seguenti: 
> <UL>
> <LI>
> <P>SourceMailboxes</P>
> <LI>
> <P>Sources</P>
> <LI>
> <P>SearchQuery</P>
> <LI>
> <P>ResultsLink</P>
> <LI>
> <P>PreviewResultsLink</P>
> <LI>
> <P>Errors</P></LI></UL>Il motivo è che richiede molte risorse per restituire le proprietà per tutte le ricerche di eDiscovery nell'organizzazione.



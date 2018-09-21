---
title: 'Cerca/elimina messaggi - Guida di Amministrazione: Exchange 2013 Help'
TOCTitle: Ricerca ed eliminazione di messaggi - Guida di Amministrazione
ms:assetid: 8c36bb03-e716-4fdd-9958-4aa7a2a1db42
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff459253(v=EXCHG.150)
ms:contentKeyID: 52057288
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ricerca ed eliminazione di messaggi - Guida di Amministrazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-12-20_

Gli amministratori possono utilizzare il cmdlet **Search-Mailbox** per cercare cassette postali utente ed eliminare messaggi da una cassetta postale.

Per cercare ed eliminare i messaggi in un solo passaggio, eseguire il cmdlet **Search-Mailbox** con l'opzione *DeleteContent*. Tuttavia, durante questa operazione non è possibile visualizzare in anteprima i risultati di ricerca o creare un registro dei messaggi che verrà restituito dalla ricerca e si potrebbero inavvertitamente eliminare messaggi. Per visualizzare in anteprima un registro dei messaggi trovati nella ricerca prima che vengano eliminati, eseguire il cmdlet **Search-Mailbox** con l'opzione *LogOnly*.

Come ulteriore salvaguardia, è possibile prima copiare i messaggi su un'altra cassetta postale utilizzando i parametri *TargetMailbox* e *TargetFolder*. Nell'effettuare questa operazione, mantenere una copia dei messaggi eliminati nel caso sia necessario accedervi di nuovo.

## Informazioni necessarie per iniziare

  - Tempo stimato per il completamento: 10 minuti. Il tempo effettivo potrebbe variare in base alla dimensione della cassetta postale e della query di ricerca.

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per eseguire tali procedure. È necessario utilizzare la shell.

  - Per cercare ed eliminare messaggi nelle cassette postali degli utenti, è necessario ricoprire entrambi i seguenti ruoli di gestione:
    
      - **Ricerca cassetta postale**   Questo ruolo consente la ricerca dei messaggi in più cassette postali nell'organizzazione. Agli amministratori non viene assegnato questo ruolo per impostazione predefinita. Per assegnare a se stessi questo ruolo per poter effettuare ricerche nelle cassette postali, aggiungersi come membro del gruppo di ruoli Gestione individuazione. Vedere [Assegnare le autorizzazioni di eDiscovery di Exchange](https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-ediscovery/assign-ediscovery-permissions).
    
      - **Esportazione/importazione cassette postali**   Questo ruolo consente all'utente di eliminare messaggi dalla cassetta postale dell'utente. Per impostazione predefinita, questo ruolo non è assegnato ad alcun gruppo di ruoli. Per eliminare i messaggi dalle cassette postali degli utenti, è possibile aggiungere il ruolo Esportazione/importazione delle cassette postali al gruppo di ruoli Gestione organizzazione. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" in [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - Se la cassetta postale dalla quale si desidera eliminare i messaggi ha la funzione di individuazione di singoli elementi, è necessario prima disabilitare la funzione. Per ulteriori informazioni, vedere [Abilitare o disabilitare il ripristino di un singolo elemento per una cassetta postale](https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-user-mailboxes/enable-or-disable-single-item-recovery).

  - Se la cassetta postale dalla quale si desidera eliminare i messaggi è stata bloccata, si consiglia di verificare con i responsabili della gestione dei record o con il dipartimento legale prima di rimuovere l'opzione di conservazione ed eliminare il contenuto delle cassette postali. Dopo aver ottenuto l'approvazione, seguire i passaggi elencati nell'argomento [Pulire la cartella elementi ripristinabili](clean-up-the-recoverable-items-folder-exchange-2013-help.md).

  - Una singola ricerca può essere eseguita su un massimo di 10.000 cassette postali con il cmdlet **Search-Mailbox**. Se si è un'organizzazione Exchange Online con più di 10.000 cassette postali, è possibile utilizzare la funzionalità Ricerca di conformità (o il corrispondente cmdlet **New-ComplianceSearch**) per cercare un numero illimitato di cassette postali. È possibile utilizzare il cmdlet **New-ComplianceSearchAction** per eliminare i messaggi restituiti da una ricerca di conformità. Per ulteriori informazioni, vedere [Cercare ed eliminare messaggi dall'organizzazione di Office 365](https://go.microsoft.com/fwlink/p/?linkid=786856).

  - Se si include una query di ricerca (usando il parametro *SearchQuery*), il cmdlet **Search-Mailbox** restituirà un massimo di 10.000 elementi nei risultati della ricerca. Pertanto se si include una query di ricerca, potrebbe essere necessario eseguire il comando **Search-Mailbox** più volte per eliminare più di 10.000 elementi.

  - Cassetta postale di archivio dell'utente verrà cercata anche quando si esegue il cmdlet **Search-Mailbox** . Allo stesso modo, verranno eliminati gli elementi nella cassetta postale di archivio principale quando si utilizza il cmdlet **Search-Mailbox** con l'opzione *DeleteContent* . Per evitare questo problema, è possibile includere l'opzione *DoNotIncludeArchive* . Inoltre, è consigliabile non utilizzare l'opzione *DeleteContent* per eliminare i messaggi nelle cassette postali Exchange Online con l'espansione automatica archiviazione abilitata poiché potrebbe verificarsi una perdita di dati imprevisti.

## Ricerca di messaggi e registrazione dei risultati della ricerca

Con questo esempio viene effettuata una ricerca nella cassetta postale di April Stewart per individuare i messaggi contenenti la frase "Your bank statement" nell'oggetto e il risultato viene registrato nella cartella SearchAndDeleteLog della cassetta postale dell'amministratore. I messaggi non vengono copiati né eliminati nella cassetta postale di destinazione.

    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full

Nell'esempio seguente in tutte le cassette postali dell'organizzazione si cercano i messaggi con qualsiasi tipo di file allegato contenente la parola "Trojan" nel nome file e viene inviato un messaggio del registro alla cassetta postale dell'amministratore.

    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery attachment:trojan* -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Search-Mailbox](https://technet.microsoft.com/it-it/library/dd298173\(v=exchg.150\)).

Torna su

## Ricerca ed eliminazione dei messaggi

Con questo esempio viene effettuata una ricerca nella cassetta postale di April Stewart per individuare i messaggi contenenti la frase "Your bank statement" nell'oggetto; tali messaggi vengono eliminati dalla cassetta postale di origine senza che vengano copiati i risultati di ricerca su un'altra cartella. Come spiegato precedentemente, è necessario avere il ruolo di gestione Esportazione/Importazione delle cassette postali per eliminare messaggi dalla cassetta postale di un utente.


> [!IMPORTANT]
> Quando si utilizza il cmdlet <STRONG>Search-Mailbox</STRONG> con l'opzione <EM>DeleteContent</EM>, i messaggi vengono eliminati permanentemente dalla cassetta postale di origine. Prima di eliminare permanentemente i messaggi, si consiglia di utilizzare l'opzione <EM>LogOnly</EM> per creare un registro dei messaggi trovati nella ricerca prima che vengano eliminati oppure copiare i messaggi su un'altra cassetta postale prima di eliminarli dalla cassetta postale di origine.



```powershell
Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -DeleteContent
```

Con questo esempio viene effettuata una ricerca nella cassetta postale di April Stewart per individuare i messaggi contenenti la frase "Your bank statement" nell'oggetto. Il risultato viene copiato nella cartella AprilStewart-DeletedMessages nella cassetta postale BackupMailbox e i messaggi vengono eliminati dalla cassetta postale di April.

    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox "BackupMailbox" -TargetFolder "AprilStewart-DeletedMessages" -LogLevel Full -DeleteContent

In questo esempio si cercano in tutte le cassette postali dell'organizzazione i messaggi con la riga di oggetto "Download this file" e quindi li si elimina in modo definitivo.

    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery 'Subject:"Download this file"' -DeleteContent

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Search-Mailbox](https://technet.microsoft.com/it-it/library/dd298173\(v=exchg.150\)).

Torna su

## Usando il parametro -LogLevel Full

In alcuni degli esempi precedenti, il parametro *LogLevel* con valore `Full` viene utilizzato per registrare informazioni dettagliate sui risultati restituiti dal cmdlet **Search-Mailbox**. Quando si include questo parametro, un messaggio di posta elettronica viene creato e inviato alla cassetta postale specificata dal parametro *TargetMailbox*. Il file di registro (che è un file in formato CSV denominato Search Results.csv) è allegato a questo messaggio di posta elettronica e si trova nella cartella specificata dal parametro *TargetFolder*. Il file di registro contiene una riga per ogni messaggio incluso nei risultati della ricerca quando si esegue il cmdlet **Search-Mailbox**.


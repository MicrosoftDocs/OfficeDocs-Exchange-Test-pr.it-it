---
title: 'Recupera messaggi eliminati nella cassetta postale utente: Exchange 2013 Help'
TOCTitle: Recuperare i messaggi eliminati nella cassetta postale dell'utente
ms:assetid: 9e0e34ce-efc5-454e-8d15-57b4da867f12
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff660637(v=EXCHG.150)
ms:contentKeyID: 50555644
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recuperare i messaggi eliminati nella cassetta postale dell'utente

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

(Questo argomento è destinato agli amministratori di Exchange.)

Gli amministratori possono cercare e recuperare i messaggi di posta elettronica eliminato nella cassetta postale dell'utente. Includono gli elementi che verranno eliminati definitivamente (cancellati) da una persona (utilizzando la caratteristica Recupera elementi eliminati in Outlook o Outlook Web App ) o gli elementi eliminati da un processo automatizzato, ad esempio il criterio di conservazione assegnato a cassette postali degli utenti. In questi casi, gli elementi eliminati non possono essere recuperati da un utente. Tuttavia, gli amministratori possono recuperare i messaggi eliminati se il periodo di mantenimento elementi eliminati per l'elemento non è scaduto.


> [!NOTE]
> Oltre a utilizzare questa procedura per cercare e recuperare gli elementi eliminati (che sono stati spostati nella cartella Elementi ripristinabili\Eliminazioni se è abilitato il ripristino di un singolo elemento o la conservazione in caso di dispute), è possibile utilizzare questa procedura anche per cercare gli elementi che risiedono in altre cartelle della cassetta postale e per eliminare gli elementi dalla cassetta postale di origine (nota anche come <EM>ricerca ed eliminazione</EM>).



## Cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 15-30 minuti.

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - Ripristino di singoli elementi deve essere abilitato per una cassetta postale prima dell'eliminazione dell'elemento che si desidera ripristinare. In Exchange Online, ripristino di singoli elementi è attivato per impostazione predefinita, quando viene creata una nuova cassetta postale. In Exchange 2013, ripristino di singoli elementi è disabilitato quando viene creata una cassetta postale. Per ulteriori informazioni, vedere [Abilitare o disabilitare il ripristino di un singolo elemento per una cassetta postale](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md).

  - Per cercare e recuperare gli elementi, è necessario disporre delle seguenti informazioni:
    
      - **Cassetta postale di origine**   Si tratta della cassetta postale da cercare.
    
      - **Cassetta postale di destinazione**   Questa è la cassetta postale di individuazione in cui verranno ripristinati i messaggi. Exchange Il programma di installazione consente di creare una cassetta postale di individuazione. In Exchange Online cassette postali di individuazione viene inoltre creata per impostazione predefinita. Se necessario, è possibile creare cassette postali di individuazione aggiuntive. Per ulteriori informazioni, vedere [Creazione di una cassetta postale di individuazione](create-a-discovery-mailbox-exchange-2013-help.md).
        

        > [!NOTE]
        > Quando si utilizza il cmdlet <STRONG>Search-Mailbox</STRONG>, è anche possibile specificare una cassetta postale di destinazione che non sia una cassetta postale di individuazione. Tuttavia, non è possibile specificare la stessa cassetta postale come cassetta postale di origine e di destinazione.

    
      - **Criteri di ricerca**   I criteri comprendono il mittente, il destinatario o le parole chiave (termini o frasi) del messaggio.

  - In questo argomento viene illustrato l'utilizzo di PowerShell per recuperare elementi eliminati in postale una cassetta. È inoltre possibile utilizzare lo strumento di basati sull'interfaccia In-Place eDiscovery per trovare ed esportare gli elementi eliminati in un file PST. L'utente verrà utilizzato il file PST per ripristinare i messaggi eliminati alle cassette postali. Per istruzioni dettagliate, vedere [Recover degli elementi eliminati nella cassetta postale dell'utente, la Guida di amministrazione](https://go.microsoft.com/fwlink/p/?linkid=722928).

## (Facoltativo) Passaggio 1: Connessione a Exchange Online tramite remote PowerShell

È sufficiente eseguire questo passaggio se si dispone di un'organizzazione Exchange Online o Office 365. Se si dispone di un'organizzazione Exchange 2013, eseguire il comando in Exchange Management Shell andare al passaggio successivo.

1.  Nel computer locale, aprire Windows PowerShell ed eseguire il seguente comando.
    
        $UserCredential = Get-Credential
    
    Nella finestra di dialogo **Richiesta credenziali di Windows PowerShell**, digitare il nome utente e la password per l'account dell'amministratore globale Office 365 e fare clic su **OK**.

2.  Eseguire il comando riportato di seguito.
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  Eseguire il comando riportato di seguito.
    
        Import-PSSession $Session

4.  Per verificare di essere connessi alla propria organizzazione Exchange Online, eseguire il seguente comando per visualizzare un elenco di tutte le cassette postali dell'organizzazione:
    
        Get-Mailbox

Per ulteriori informazioni o nel caso di problemi di connessione all'organizzazione Exchange Online, vedere [Connect a Exchange Online tramite remote PowerShell](https://go.microsoft.com/fwlink/p/?linkid=517283).

## Passaggio 2: Cercare e recuperare elementi mancanti

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "eDiscovery locale" nell'argomento[Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!NOTE]
> È possibile utilizzare eDiscovery In locale nell'interfaccia di amministrazione di Exchange (EAC) per cercare gli elementi mancanti. Quando si utilizza l'interfaccia di amministrazione di Exchange, è tuttavia non possono limitare la ricerca per la cartella elementi ripristinabili. Anche se non si è eliminati, verranno restituiti messaggi che soddisfano i parametri di ricerca. Dopo che si sta di ripristino per la cassetta postale di individuazione specificato, potrebbe essere necessario esaminare i risultati della ricerca e rimuovere i messaggi non necessari prima di recupero dei messaggi rimanenti cassetta postale dell'utente o di esportazione in un file pst.<BR>Per ulteriori informazioni sull'utilizzo dell'interfaccia di amministrazione di Exchange per eseguire una ricerca eDiscovery in locale, vedere <A href="create-an-in-place-ediscovery-search-exchange-2013-help.md">Creazione di una ricerca eDiscovery sul posto</A>.



Il primo passo nel processo di ripristino è la ricerca dei messaggi nella cassetta postale di origine. Utilizzare uno dei seguenti metodi per cercare una cassetta postale dell'utente e copiare i messaggi in una cassetta postale di individuazione.

In questo esempio vengono cercati i messaggi nella cassetta postale di April Stewart che soddisfano i seguenti criteri:

  - Mittente: Ken Kwok

  - Parola chiave: Seattle

<!-- end list -->

    Search-Mailbox "April Stewart" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "Discovery Search Mailbox" -TargetFolder "April Stewart Recovery" -LogLevel Full


> [!NOTE]
> Quando si utilizza il cmdlet <STRONG>Search-Mailbox</STRONG>, è possibile esaminare la ricerca utilizzando il parametro <EM>SearchQuery</EM> per specificare una query formattata con il linguaggio KQL (Keyword Query Language). È possibile anche utilizzare l'opzione <EM>SearchDumpsterOnly</EM> per effettuare la ricerca solo negli elementi della cartella Elementi ripristinabili.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Search-Mailbox](https://technet.microsoft.com/it-it/library/dd298173\(v=exchg.150\)).

**Come verificare se l'operazione ha avuto esito positivo?**

Per verificare che la ricerca dei messaggi da recuperare sia stata effettuata in modo corretto, accedere alla cassetta postale di individuazione selezionata come cassetta postale di destinazione ed esaminare i risultati della ricerca.

## Passaggio 3: Ripristinare gli elementi recuperati

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "eDiscovery locale" nell'argomento[Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!NOTE]
> Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per ripristinare gli elementi recuperati.



Dopo che sono stati ripristinati i messaggi in una cassetta postale di individuazione, è possibile ripristinare loro cassetta postale dell'utente utilizzando il cmdlet **Search-Mailbox** . In Exchange 2013, è anche possibile utilizzare i cmdlet **New-MailboxExportRequest** e **New-MailboxImportRequest** per i messaggi per esportare o importare i messaggi da un file con estensione pst.

## Ripristino dei messaggi tramite Shell

In questo esempio, i messaggi vengono ripristinati nella cassetta postale di April Stewart ed eliminati da Discovery Search Mailbox.

    Search-Mailbox "Discovery Search Mailbox" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "April Stewart" -TargetFolder "Recovered Messages" -LogLevel Full -DeleteContent

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Search-Mailbox](https://technet.microsoft.com/it-it/library/dd298173\(v=exchg.150\)).

**Come verificare se l'operazione ha avuto esito positivo?**

Per verificare il corretto ripristino dei messaggi nella cassetta postale dell'utente, chiedere all'utente di esaminare i messaggi presenti nella cartella di destinazione specificata nel comando indicato in precedenza.

## (Exchange 2013) Utilizzo della Shell per esportare e importare i messaggi da un file con estensione pst

In Exchange 2013, è possibile esportare contenuto da una cassetta postale in un file con estensione pst e importare il contenuto di un file pst in una cassetta postale. Per ulteriori informazioni sull'esportazione e importazione delle cassette postali, vedere [Cassetta postale di importare ed esportare le richieste](mailbox-import-and-export-requests-exchange-2013-help.md). È possibile eseguire questa operazione in Exchange Online.

In questo esempio vengono utilizzate le impostazioni seguenti per esportare i messaggi dalla cartella April Stewart Recovery di Discovery Search Mailbox in un file .pst:

  - **Cassetta postale**   Discovery Search Mailbox

  - **Cartella di origine**   April Stewart Recovery

  - **ContentFilter**   April travel plans

  - **Percorso per il file PST**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxExportRequest -Mailbox "Discovery Search Mailbox" -SourceRootFolder "April Stewart Recovery" -ContentFilter {Subject -eq "April travel plans"} -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MailboxExportRequest](https://technet.microsoft.com/it-it/library/ff607299\(v=exchg.150\)).

In questo esempio vengono utilizzate le impostazioni seguenti per importare i messaggi da un file .pst alla cartella Recovered By Helpdesk nella cassetta postale di April Stewart:

  - **Cassetta postale**   April Stewart

  - **Cartella di destinazione**   Recovered By Helpdesk

  - **Percorso per il file PST**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxImportRequest -Mailbox "April Stewart" -TargetRootFolder "Recovered By Helpdesk" -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst 

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-MailboxImportRequest](https://technet.microsoft.com/it-it/library/ff607310\(v=exchg.150\)).

**Come verificare se l'operazione ha avuto esito positivo?**

Per verificare la corretta esportazione dei messaggi in un file PST, utilizzare Outlook per aprire il file PST e ispezionarne il contenuto. Per verificare la corretta importazione dei messaggi dal file PST, chiedere all'utente di ispezionare il contenuto della cartella di destinazione specificata nel comando indicato in precedenza.

## Ulteriori informazioni

  - La capacità di recupero degli elementi eliminati è abilitata per il *ripristino di un singolo elemento*, che consente a un amministratore di recuperare un messaggio che viene eliminato da un utente o dal criterio di conservazione, purché non ha scadenza del periodo di mantenimento elementi eliminati per l'elemento. Per ulteriori informazioni sul ripristino di un singolo elemento, vedere [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md).

  - Una cassetta postale Exchange Online è configurata per conservare gli elementi eliminati 14 giorni, per impostazione predefinita. È possibile modificare questa impostazione per un massimo di 30 giorni. In Exchange 2013, un database delle cassette postali è configurato per conservare gli elementi eliminati 14 giorni, per impostazione predefinita. È possibile configurare le impostazioni di mantenimento elementi eliminati per una cassetta postale o i database delle cassette postali. Per ulteriori informazioni, vedere:
    
      - [Vengono conservati gli elementi eliminato in modo permanente il tempo di modifica per una cassetta postale di Exchange Online](https://technet.microsoft.com/it-it/library/dn163584\(v=exchg.150\))
    
      - [Configurare il periodo di mantenimento degli elementi eliminati e delle quote di elementi ripristinabili](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)

  - Come indicato in precedenza, è possibile utilizzare anche lo strumento di eDiscovery In locale per cercare ed esportare gli elementi eliminati in un file PST. L'utente verrà utilizzato il file PST per ripristinare i messaggi eliminati alle cassette postali. Per istruzioni dettagliate, vedere [Recover degli elementi eliminati nella cassetta postale dell'utente, la Guida di amministrazione](https://go.microsoft.com/fwlink/p/?linkid=722928).

  - Gli utenti possono recuperare un elemento eliminato se non è stato eliminato e se il periodo di mantenimento elementi eliminati per l'elemento non è scaduto. Se gli utenti devono recuperare elementi eliminati dalla cartella elementi ripristinabili, puntino agli argomenti seguenti:
    
      - [Recupera posta eliminata in Outlook 2010](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [Recupera posta eliminata in Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=624829)
    
      - [Recuperare elementi o messaggi di posta elettronica eliminati in Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

  - In questo argomento viene illustrato come utilizzare il cmdlet **Search-Mailbox** per cercare e recuperare elementi mancanti. Se si utilizza questo cmdlet, è possibile cercare solo una cassetta postale alla volta. Se si desidera eseguire la ricerca più cassette postali contemporaneamente, è possibile utilizzare il cmdlet [New-MailboxSearch](https://technet.microsoft.com/it-it/library/dd298064\(v=exchg.150\)) in Windows PowerShell o [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md) nell'interfaccia di amministrazione di Exchange (EAC).

  - Oltre a utilizzare la procedura seguente per cercare e recuperare elementi eliminati, è inoltre possibile utilizzare una procedura analoga per cercare gli elementi nelle cassette postali utente e quindi eliminarli dalla cassetta postale di origine. Per ulteriori informazioni, vedere [Ricerca ed eliminazione di messaggi - Guida di Amministrazione](search-for-and-delete-messages-admin-help-exchange-2013-help.md).


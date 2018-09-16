---
title: 'Eseguire la migrazione dalle cartelle gestite: Exchange 2013 Help'
TOCTitle: Eseguire la migrazione dalle cartelle gestite
ms:assetid: 6796a79d-501e-4216-9370-77965bc5835d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298032(v=EXCHG.150)
ms:contentKeyID: 52063103
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eseguire la migrazione dalle cartelle gestite

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

In Microsoft Exchange Server 2013, la gestione record di messaggistica viene eseguita utilizzando i tag e i criteri di conservazione. Il criterio di conservazione è un gruppo di tag di conservazione che può essere applicato a una cassetta postale. Per ulteriori dettagli, vedere [Tag di conservazione e criteri di conservazione](https://docs.microsoft.com/it-it/exchange/security-and-compliance/messaging-records-management/retention-tags-and-policies). Le cartelle gestite, ovvero la tecnologia per gestire i record di messaggistica introdotta in Exchange Server 2007, non sono ancora supportate.

È possibile eseguire la migrazione di una cassetta postale a cui è applicato un criterio per cartelle gestite per utilizzare un criterio di conservazione. A questo scopo, è necessario creare dei tag di conservazione equivalenti alle cartelle gestite collegate al criterio cassette postali per cartelle gestite dell'utente.


> [!IMPORTANT]
> Prima di eseguire la migrazione dalle cartelle gestite ai criteri di conservazione nell'ambiente di produzione, è opportuno verificare il processo in un ambiente di prova.




> [!TIP]
> È possibile posizionare le cassette postali nel mantenimento per interrompere l'elaborazione dei criteri di conservazione o dei criteri cassette postali per cartelle gestite. La disposizione del blocco di conservazione delle casette postali può essere utile in scenari di migrazione al fine di evitare di cancellare i messaggi o spostarli in archivio fino a nuove impostazioni dei criteri stati testate su cassette postali di prova o su un esiguo numero di cassette postali di produzione. Per ulteriori informazioni, vedere <A href="https://docs.microsoft.com/it-it/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold">Archiviazione sul posto una cassetta postale di conservazione</A>.



Per le altre attività di gestione relative a Gestione record di messaggistica, vedere [Messaggistica Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

## Confronto dei tag di conservazione con le cartelle gestite

A differenza delle cartelle gestite, dove lo spostamento degli elementi deve essere eseguito dagli utenti sulla base delle impostazioni di conservazione, i tag di conservazione possono essere applicati a una cartella o a un singolo elemento nella cassetta postale. Questo processo ha un impatto minimo sul flusso di lavoro dell'utente e sui metodi di organizzazione di posta elettronica. Quando a una cartella vengono applicati dei tag di conservazione, tutti gli elementi che si trovano in quella cartella ereditano le impostazioni di conservazione. Gli utenti possono specificare ulteriori impostazioni di conservazione applicando altri tag di conservazione ai singoli elementi nella cartella.

Le cartelle gestite supportano diverse impostazioni del contenuto gestito per una cartella, ciascuna con una classe di messaggio diverso (ad esempio elementi di posta elettronica o del calendario). I tag di conservazione non necessitano di impostazioni separate per i contenuti gestiti perché le impostazioni di conservazione sono specificate nelle proprietà del tag. Non è supportato per creare i tag di conservazione per particolari classi di messaggio, con l'eccezione di un tag dei criteri predefiniti per i messaggi di casella vocale. I tag di conservazione, inoltre, non consentono di utilizzare l'inserimento nel journal eseguito dall'Assistente cartelle gestite.


> [!NOTE]
> Le regole del journal, utilizzate per inviare copie di messaggi con un rapporto del journal da annotare in una cassetta postale, vengono applicate nella pipeline di trasporto dall'agente di journaling e sono indipendenti dalla gestione dei record di messaggistica. Per ulteriori dettagli, vedere <A href="journaling-exchange-2013-help.md">Inserimento nel journal</A>.



Nella seguente tabella sono messe a confronto le funzionalità di gestione dei record di messaggistica disponibili quando si utilizzano i tag di conservazione o le cartelle gestite.

### Tag di conservazione e cartelle gestite

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Tag di conservazione</th>
<th>Cartelle gestite</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Specificare le impostazioni di conservazione per le cartelle predefinite (ad esempio, Posta in arrivo)</p></td>
<td><p>Utilizzare i tag del criterio di conservazione</p></td>
<td><p>Utilizzare le cartelle gestite predefinite</p></td>
</tr>
<tr class="even">
<td><p>Specificare le impostazioni di conservazione per l'intera cassetta postale</p></td>
<td><p>Utilizzare un tag del criterio predefinito</p></td>
<td><p>Utilizzare cartelle gestite predefinite</p></td>
</tr>
<tr class="odd">
<td><p>Utilizzare le impostazioni di conservazione per le cartelle personalizzate</p></td>
<td><p>Utilizzare i tag personali</p></td>
<td><p>Utilizzare le cartelle gestite personalizzate</p></td>
</tr>
<tr class="even">
<td><p>Richiedere le impostazioni del contenuto gestito</p></td>
<td><p>No (impostazioni di conservazione incluse in un tag di conservazione)</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Utilizzare le impostazioni di conservazione per diverse classi di messaggio (ad esempio, messaggi di posta elettronica, casella vocale o elementi di calendario)</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Supportare l'azione MoveToArchive che sposta gli elementi nella cassetta postale di archivio dell'utente</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Supportare l'azione MoveToManagedFolder</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Consentire l'inserimento nel journal tramite Assistente cartelle gestite</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Criterio applicato all'utente</p></td>
<td><p>Criterio di conservazione</p></td>
<td><p>Criteri cassetta postale per cartella gestita</p></td>
</tr>
<tr class="even">
<td><p>Numero massimo di criteri che è possibile applicare a un utente della cassetta postale</p></td>
<td><p>1</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>Elaborazione eseguita dall'Assistente cartelle gestite</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Supporto client</p></td>
<td><p>Microsoft Outlook 2010 e OfficeOutlook Web App</p></td>
<td><p>Outlook 2010, Office Outlook 2007 e Outlook Web App</p></td>
</tr>
</tbody>
</table>


## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 20 minuti.

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per creare i tag di conservazione basati sui criteri di conservazione.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Eseguire la migrazione di utenti di cassette postali da cartelle gestite

Di seguito sono indicati alcuni passaggi generali per eseguire la migrazione degli utenti da questo criterio cassetta postale per cartelle gestite verso un criterio di conservazione. Di seguito, ogni passaggio viene ampiamente descritto in questo argomento:

1.  Raccogliere informazioni sui criteri cassetta postale di cartelle gestite applicato a tutte le cassette postali Exchange 2010 e Exchange 2007, in ogni criterio cartelle gestite e gestite le impostazioni del contenuto per ogni cartella gestita. È possibile utilizzare EMC o Shell su un server Exchange 2010 o Exchange 2007 per ottenere queste informazioni.

2.  Creare i tag di conservazione per la migrazione.

3.  Creare un criterio di conservazione e collegare i tag di conservazione appena creati al criterio.

4.  Rimuovere il criterio cassetta postale per cartella gestita, quindi applicare i criteri di conservazione alle cassette postali degli utenti.
    

    > [!IMPORTANT]
    > Dopo aver applicato il criterio di conservazione a un utente ed eseguito l'Assistente cartelle gestite, le cartelle gestite nella cassetta postale dell'utente non vengono più gestite.



Per le seguenti procedure, alle cassette postali di Contoso è stato applicato un criterio cassetta postale per cartelle gestite che contiene le seguenti cartelle gestite.

### Cartelle gestite per Contoso

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cartella gestita</th>
<th>Impostazioni contenuto gestito</th>
<th>Conservazione attivata</th>
<th>Periodo di conservazione</th>
<th>Azione di conservazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Corp-DeletedItems</p></td>
<td><p>CS-Corp-DeletedItems</p></td>
<td><p>Sì</p></td>
<td><p>30 giorni</p></td>
<td><p>Elimina e consenti ripristino</p></td>
</tr>
<tr class="even">
<td><p>Corp-SentItems</p></td>
<td><p>CS-Corp-SentItems</p></td>
<td><p>Sì</p></td>
<td><p>1.825 giorni</p></td>
<td><p>Sposta negli elementi eliminati</p></td>
</tr>
<tr class="odd">
<td><p>Corp-JunkMail</p></td>
<td><p>CS-Corp-JunkMail</p></td>
<td><p>Sì</p></td>
<td><p>30 giorni</p></td>
<td><p>Elimina definitivamente</p></td>
</tr>
<tr class="even">
<td><p>Corp-EntireMailbox</p></td>
<td><p>CS-Corp-EntireMailbox</p></td>
<td><p>Sì</p></td>
<td><p>365 giorni</p></td>
<td><p>Sposta negli elementi eliminati</p></td>
</tr>
<tr class="odd">
<td><p>30 giorni</p></td>
<td><p>CS-30Days</p></td>
<td><p>Sì</p></td>
<td><p>30 giorni</p></td>
<td><p>Sposta negli elementi eliminati</p></td>
</tr>
<tr class="even">
<td><p>5 anni</p></td>
<td><p>CS-5Years</p></td>
<td><p>Sì</p></td>
<td><p>1.825 giorni</p></td>
<td><p>Sposta negli elementi eliminati</p></td>
</tr>
<tr class="odd">
<td><p>Nessuna scadenza</p></td>
<td><p>CS-NeverExpire</p></td>
<td><p>No</p></td>
<td><p>365 giorni</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


## Come eseguire l'operazione

## Passaggio 1: Creare i tag di conservazione per la migrazione

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione record di messaggistica" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Per completare questo passaggio esistono due metodi:

  - **Creare tag di conservazione basati sulle cartelle gestite e le relative impostazioni del contenuto gestito**   Per questo metodo, si utilizza il cmdlet **New-RetentionPolicyTag** con il parametro *ManagedFolderToUpgrade*. Quando si specifica questo parametro, il tag di conservazione corrispondente viene automaticamente applicato alla cartella gestita.
    

    > [!IMPORTANT]
    > Se nella cartella gestita da trasferire sono presenti più impostazioni del contenuto gestito per diverse classi di messaggi, viene creato un tag di conservazione e viene utilizzato il periodo di validità della conservazione più elevato di tutte le impostazioni del contenuto gestito come periodo di validità della conservazione per il tag trasferito, indipendentemente dalla classe del messaggio delle impostazioni del contenuto gestito.<BR>Esaminare ad esempio le impostazioni seguenti del contenuto gestito per la cartella gestita Corp-DeletedItems.



  - **Creare i tag di conservazione specificando manualmente le impostazioni di conservazione**   Per questo metodo, si utilizza il cmdlet **New-RetentionPolicyTag** senza il parametro *ManagedFolderToUpgrade*. Quando non si specifica questo parametro, qualsiasi tag del criterio di conservazione aggiunto al criterio viene applicato alle cartelle predefinite e il tag del criterio predefinito viene applicato all'intera cassetta postale. Tuttavia, gli eventuali tag personali aggiunti al criterio non vengono automaticamente applicati alle cartelle gestite.


> [!NOTE]
> Se si è in un ambiente misto con server Exchange 2013 e Exchange&nbsp;2010, è possibile utilizzare la procedura guidata <STRONG>Cartella gestita porta</STRONG> in Exchange Management Console (EMC) su un server Exchange&nbsp;2010 facilmente cartella gestita di porta e impostazione del contenuto per i tag di conservazione corrispondente gestito.



**Creazione dei tag di conservazione sulla base delle cartelle gestite**

In questo esempio, i tag di conservazione vengono creati sulla base delle impostazioni dei corrispondenti contenuti gestiti che compaiono nel criterio per le cartelle gestite Contoso.

    New-RetentionPolicyTag Corp-DeletedItems -ManagedFolderToUpgrade Corp-DeletedItems
    New-RetentionPolicyTag Corp-SentItems -ManagedFolderToUpgrade Corp-SentItems
    New-RetentionPolicyTag Corp-JunkMail -ManagedFolderToUpgrade Corp-JunkMail
    New-RetentionPolicyTag Corp-EntireMailbox -ManagedFolderToUpgrade Corp-EntireMailbox
    New-RetentionPolicyTag 30Days -ManagedFolderToUpgrade 30Days
    New-RetentionPolicyTag 5Years -ManagedFolderToUpgrade 5Years
    New-RetentionPolicyTag NeverExpire -ManagedFolderToUpgrade NeverExpire

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-RetentionPolicyTag](https://technet.microsoft.com/it-it/library/dd335226\(v=exchg.150\)).

**Creazione manuale dei tag di conservazione**


> [!NOTE]
> È possibile utilizzare l'interfaccia di amministrazione di Exchange per creare manualmente i tag di conservazione (non basati sulle impostazioni nelle cartelle gestite). Per ulteriori informazioni, vedere <A href="https://docs.microsoft.com/it-it/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">Creare un criterio di conservazione</A>.



In questo esempio, i tag di conservazione vengono creati sulla base delle cartelle gestite e delle impostazioni dei corrispondenti contenuti gestiti che compaiono nel criterio per le cartelle gestite Contoso. Le impostazioni di conservazione vengono specificate manualmente senza utilizzare il parametro *ManagedFolderToUpgrade*.

    New-RetentionPolicyTag Corp-DeletedItems -Type DeletedItems -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction DeleteAndAllowRecovery
    New-RetentionPolicyTag Corp-SentItems -Type SentItems -RetentionEnabled $true -AgeLimitforRetention 1825 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag Corp-JunkMail -Type JunkMail -RetentionEnabled $true -AgeLimitforRetention 30 -RetentionAction PermanentlyDelete
    New-RetentionPolicyTag Corp-EntireMailbox -Type All -RetentionEnabled $true -AgeLimitForRetention 365 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag 30Days -Type Personal -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag 5Years -Type Personal -RetentionEnabled $true -AgeLimitForRetention 1825 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag NeverExpire -Type Personal -RetentionEnabled $false

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-RetentionPolicyTag](https://technet.microsoft.com/it-it/library/dd335226\(v=exchg.150\)).

## Passaggio 2: Creare un criterio di conservazione

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione record di messaggistica" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!NOTE]
> È inoltre possibile utilizzare l'interfaccia di amministrazione di Exchange per creare un criterio di conservazione e per aggiungere tag di conservazione al criterio. Per ulteriori informazioni, vedere <A href="https://docs.microsoft.com/it-it/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">Creare un criterio di conservazione</A>.



In questo esempio, viene creato il criterio di conservazione RP-Corp e i tag di conservazione appena creati vengono collegati al criterio stesso.

    New-RetentionPolicy RP-Corp -RetentionPolicyTagLinks Corp-DeletedItems,Corp-SentItems,Corp-JunkMail,Corp-EntireMailbox,30Days,NeverExpire

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-RetentionPolicy](https://technet.microsoft.com/it-it/library/dd297970\(v=exchg.150\)).

## Passaggio 3: Rimuovere i criteri cassetta postale per cartelle gestite dalle cassette postali dell'utente

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Applicazione criteri di conservazione" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

In questo esempio viene rimosso il criterio cassetta postale per cartelle gestite e qualsiasi cartella gestite dalla cassetta postale di Ken Kwok. Le cartelle gestite che dispongono di eventuali messaggi non vengono rimosse.

    Set-Mailbox -Identity Kwok -RemoveManagedFolderAndPolicy RP-Corp

## Passaggio 4: Applicare il criterio di conservazione alle cassette postali degli utenti

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Applicazione criteri di conservazione" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!NOTE]
> È inoltre possibile utilizzare l'interfaccia di amministrazione di Exchange per applicare un criterio di conservazione agli utenti. Per ulteriori informazioni, vedere <A href="https://docs.microsoft.com/it-it/exchange/security-and-compliance/messaging-records-management/apply-retention-policy">Applicazione dei criteri di conservazione alle cassette postali</A>.



In questo esempio, il criterio di conservazione RP-Corp appena creato viene applicato alla cassetta postale dell'utente Ken Kwok.

    Set-Mailbox -Identity Kwok -RetentionPolicy RP-Corp

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che sia stata eseguita la migrazione dalle cartelle gestite verso i criteri di conservazione, effettuare le seguenti operazioni:

  - Generare un report di tutte le cassette postali dell'utente e il criterio di conservazione applicato alle stesse.
    
    Tramite tale comando viene recuperato il criterio di conservazione applicato a tutte le cassette postali in un'organizzazione e il relativo stato di conservazione.
    
        Get-Mailbox -ResultSize unlimited -Filter {Name -NotLike "DiscoverySearch*�?} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto

  - Dopo che l'Assistente cartelle gestite ha elaborato una casetta postale con un criterio di conservazione, utilizzare il cmdlet [Get-RetentionPolicyTag](https://technet.microsoft.com/it-it/library/dd298009\(v=exchg.150\)) per recuperare i tag di conservazione disposti nella casetta postale dell'utente
    
    Tramite tale comando vengono recuperati i tag di conservazione effettivamente applicati alla cassetta postale dell'utente April Stewart.
    
        Get-RetentionPolicyTag -Mailbox astewart


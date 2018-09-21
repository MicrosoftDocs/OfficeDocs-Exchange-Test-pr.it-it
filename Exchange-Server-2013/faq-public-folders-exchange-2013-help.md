---
title: 'Domande frequenti: Cartelle pubbliche: Exchange 2013 Help'
TOCTitle: 'Domande frequenti: Cartelle pubbliche'
ms:assetid: 1cdcdcb7-f11b-45ca-ad23-7c38f640208c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ552408(v=EXCHG.150)
ms:contentKeyID: 50480116
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Domande frequenti: Cartelle pubbliche

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-03-27_

In questo argomento, viene fornito un elenco di domande frequenti sulle cartelle pubbliche in Exchange Server 2013. Per ulteriori informazioni sulle cartelle pubbliche, vedere [Cartelle pubbliche](public-folders-exchange-2013-help.md).

Ci sono domande sulle cartelle pubbliche per cui non esiste una risposta in questa sezione? Inviare un messaggio di posta elettronica a [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com).

## Domande frequenti sulla migrazione delle cartelle pubbliche

In questa sezione contiene le domande frequenti sulla migrazione delle cartelle pubbliche. Per ulteriori informazioni, vedere [Utilizzare la migrazione seriale per spostare le cartelle pubbliche in Exchange 2013 dalle versioni precedenti](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md), [Utilizzare la migrazione batch delle cartelle pubbliche legacy a Office 365 ed Exchange Online](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/batch-migration-of-legacy-public-folders)o [Utilizzare la migrazione batch per migrare le cartelle pubbliche di Exchange 2013 a Exchange Online](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/batch-migration-of-exchange-2013-public-folders).

## Che cosa sono gli scenari di migrazione supportati cartelle pubbliche?

Di seguito sono descritte le opzioni disponibili per la migrazione delle cartelle pubblica a Exchange 2013 o Exchange Online.

  - Le cartelle pubbliche di Exchange 2007 (RU15 SP3 o versione successiva) è possibile migrare a Exchange 2013 o Exchange Online.

  - Le cartelle pubbliche di Exchange 2010 (RU8 SP3 o versione successiva) è possibile migrare a Exchange 2013 o Exchange Online.

  - Le cartelle pubbliche di Exchange 2013 (CU15 o versione successiva) può essere eseguita la migrazione a Exchange Online.

Sono supportate le migrazioni attualmente sola a Exchange 2013 nella stessa foresta di Active Directory. Le migrazioni tra foreste saranno supportate in futuro.

## Una volta eseguita la migrazione, cosa succede alla gerarchia sui server di Exchange 2010 di origine?

Durante la fase di finalizzazione della migrazione, viene posizionato un blocco sul server di origine in modo da renderlo inaccessibile all'utente. Questo blocco viene mantenuto per evitare che gli utenti accedano alle cartelle pubbliche di origine anche una volta completata la migrazione. Sebbene sia possibile rilasciare tale blocco, si consiglia di non farlo in quanto non è possibile sincronizzare le modifiche in Exchange 2013.

## Cosa succede alle regole sulle cartelle pubbliche durante la migrazione di cartelle pubbliche?

Le regole sulle cartelle pubbliche vengono migrate insieme ai dati e mantenute come tali. Non vengono convertite in regole delle cassette postali.

## Cosa succede se vengono apportate modifiche alla gerarchia sull'origine una volta generato il file .csv iniziale? In che modo tali modifiche si riflettono sulla destinazione?

Il file .csv viene utilizzato per stabilire il mapping tra la gerarchia di origine e la cassetta postale di destinazione. Contiene solo le cartelle di livello superiore. Le cartelle figlio al di sotto delle cartelle di livello superiore vengono migrate automaticamente. Pertanto, se si aggiunge una nuova cartella figlio, questa viene migrata durante il processo. Se si crea una nuova cartella di livello superiore, questa verrà creata nella cassetta postale contenente la copia scrivibile della gerarchia.

## Durante la migrazione alle cartelle pubbliche di Exchange 2013, se trascorre un lungo periodo di tempo tra la sospensione e la finalizzazione, come si può forzare una sincronizzazione delta affinché gli utenti possano accedere alle cartelle pubbliche durante la sincronizzazione finale?

È possibile far sì che una sincronizzazione delta venga sincronizzata prima della finalizzazione (prima del blocco dell'origine) utilizzando il seguente comando Shell:

```powershell
Resume-PublicFolderMigrationRequest \PublicFolderMigration
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Resume-PublicFolderMigrationRequest](https://technet.microsoft.com/it-it/library/jj218689\(v=exchg.150\)).

## Per la migrazione di una gerarchia distribuita a livello geografico, come si può verificare che le cartelle pubbliche vengano create nella posizione più vicina agli utenti di destinazione?

Come parte del processo di migrazione, viene generato un file .csv (utilizzando lo script `publicfoldertomailboxmapgenerator.ps1`). Questo file contiene il mapping da cartella a cassetta postale per la nuova gerarchia. È possibile utilizzare il file .csv per creare cassette postali di cartelle pubbliche nella posizione geografica appropriata e modificare il file in modo da inserire le cartelle richieste nella cassetta postale appropriata affinché siano vicino agli utenti di destinazione.

È possibile generare Il file .csv di input eseguendo lo script `AggregatePFData.ps1`, situato nella directory \<*Percorso di installazione di Exchange*\>\\V15\\Scripts. Eseguire lo script come segue:

    .\AggregatePFData.ps1 | Select-Object -property @{Name="FolderName"; Expression = {$_.Identity}}, @{Name="FolderSize"; Expression = {$_.TotalItemSize.Value.ToBytes()}} | Export-CSV -Path <Path followed by the name of the CSV>

## Le autorizzazioni per le cartelle pubbliche esistenti migrano?

Sì, le autorizzazioni verranno fatte migrare automaticamente al livello di cartella con i dati. Non è necessario eseguire questo passaggio separatamente.

## Le cartelle pubbliche stanno per essere abbandonate?

No. Le cartelle pubbliche rappresentano un'utile risorsa per l'integrazione di Outlook, offrono semplici scenari di condivisione e consentono ad ampi gruppi di destinatari di accedere agli stessi dati.

## Quali client supportano le cartelle pubbliche?

Gli utenti di Outlook 2007, Outlook 2010, Outlook 2013 e Outlook 2011 per Mac possono accedere alle cartelle pubbliche. Tuttavia, gli utenti che dispongono di cassette postali nei server di Exchange 2013 non potranno connettersi alle cartelle pubbliche di Exchange 2007 o di Exchange 2010 da client che utilizzano i Servizi Web Exchange (EWS), ad esempio Outlook per Mac. Si consiglia di effettuare la migrazione delle cartelle pubbliche legacy su Exchange 2013 al fine di garantire l'accesso a quegli utenti.

## Esistono limiti nei client?

Outlook Web App è supportato, ma con alcune limitazioni. È possibile aggiungere e rimuovere le cartelle pubbliche preferite (se si tratta di posta elettronica, Post, calendario, contatti e le cartelle pubbliche) ed eseguire operazioni a livello di elemento, ad esempio la creazione, modifica, eliminazione dei post e risposte ai messaggi inviati. Tuttavia, non possono eseguire le operazioni seguenti in Outlook Web App:

  - Creare o eliminare cartelle pubbliche

  - Trascinare contenuti

  - Accedere alle cartelle pubbliche che si trovano nei server che eseguono versioni precedenti di Exchange


> [!NOTE]
> È possibile creare solo le regole di cartelle pubbliche che contengono l' elemento <STRONG>Rispondi utilizzando un modello specifico</STRONG> nelle cartelle pubbliche abilitate alla posta. È possibile preesistente regole contenenti <STRONG>Rispondi utilizzando un modello specifico</STRONG> continuerà a funzionare in cartelle pubbliche non abilitati alla posta, ma tali cartelle è Impossibile creare nuove regole a questo elemento modello o modificare le regole esistenti con questo elemento.



In uno scenario ibrido, Outlook sul web e Outlook 2011 per Mac non sono supportati per le cartelle pubbliche tra locali. Gli utenti devono essere nello stesso percorso le cartelle pubbliche per accedervi con Outlook 2011 per Mac o Outlook sul web. Gli utenti di 2016 Outlook per Mac possono accedere alle cartelle pubbliche in uno scenario ibrido, se vengono seguite alle procedure descritte in [procedure di distribuzione ibrida](https://technet.microsoft.com/en-us/library/jj200788\(v=exchg.150\).aspx) e l'aggiornamento di aprile 2016 di 2016 Outlook per Mac è stato installato in tutti i client.

## Come posso archiviare una gerarchia di dimensioni notevoli in una cassetta postale di cartelle pubbliche?

Per ulteriori informazioni sui limiti di archiviazione delle cartelle pubbliche, vedere [Limiti per le cartelle pubbliche](limits-for-public-folders-exchange-2013-help.md).

## Come posso visualizzare la cassetta postale di cartelle pubbliche della gerarchia?

Eseguire il comando indicato di seguito:

```powershell
Get-OrganizationConfig | Format-List RootPublicFolderMailbox
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997571\(v=exchg.150\)).

## Come posso creare cassette postali con un contenuto per le cartelle pubbliche utilizzando i cmdlet di Exchange Management Shell?

Utilizzare i seguenti comandi per creare la prima cassetta postale di cartelle pubbliche della gerarchia master e le cassette postali della gerarchia secondaria.

```powershell
New-Mailbox -PublicFolder -Name <name of public folder>
```

Per ulteriori dettagli, vedere [Creare una cartella pubblica](https://docs.microsoft.com/it-it/exchange/collaboration-exo/public-folders/create-public-folder).

## Nelle versioni precedenti di Exchange, ogni database delle cassette postali disponeva di un'opzione per la definizione del proprio database di cartelle pubbliche. Cosa succederà ora in Exchange 2013?

Exchange 2013 non presenta impostazioni a livello di database. Exchange 2013 dispone della possibilità a livello di cassette postali di specificare la cassetta postale di cartelle pubbliche, ma, per impostazione predefinita, Exchange calcola automaticamente la cassetta postale della gerarchia per utente.

## Come vengono utilizzati gli strumenti metrici delle cartelle pubbliche in Exchange 2013?

In Exchange 2013, è possibile utilizzare i cmdlet [Get-PublicFolderStatistics](https://technet.microsoft.com/it-it/library/aa998663\(v=exchg.150\)) e [Get-PublicFolderItemStatistics](https://technet.microsoft.com/it-it/library/ee332344\(v=exchg.150\)) per ottenere dati metrici sulle cartelle pubbliche. Si tratta della stessa soluzione presente in Exchange 2010 e, pertanto, nulla è cambiato qui. Le cartelle pubbliche non richiedono ulteriori componenti aggiuntivi di segnalazione.

## Le cartelle pubbliche sono in grado di distinguere tra accesso interno alle cartelle pubbliche e accesso per conto di terzi?

In Exchange 2013, le autorizzazioni delle cartelle pubbliche vengono gestite tramite Controllo di accesso basato sui ruoli (RBAC). Gli elenchi di controllo di accesso (ACL) non vengono utilizzati in Exchange 2013. È possibile utilizzare i cmdlet [Get-PublicFolderStatistics](https://technet.microsoft.com/it-it/library/aa998663\(v=exchg.150\)) e [Get-PublicFolderItemStatistics](https://technet.microsoft.com/it-it/library/ee332344\(v=exchg.150\)) per tenere traccia degli account che eseguono attività amministrative e, quindi, controllare l'accesso di conseguenza. Per ulteriori informazioni su RBAC, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md).

## La registrazione di controllo delle cassette postali funziona con le cartelle pubbliche?

No. Non in questo momento.

## Quali sono i limiti per le cartelle pubbliche? Quali sono le raccomandazioni?

Per ulteriori informazioni sui limiti delle cartelle pubbliche, vedere [Limiti per le cartelle pubbliche](limits-for-public-folders-exchange-2013-help.md).

## Quali sono le raccomandazioni per suddividere le cassette postali di cartelle pubbliche? Devono rimanere sullo stesso database?

Nelle versioni precedenti di Exchange, era possibile dividere le cartelle pubbliche tra più database. L'utente può decidere se dividere il contenuto di una cassetta postale di cartelle pubbliche con una cassetta postale sullo stesso database o su un database differente. In genere, è opportuno dividere il contenuto con una cassetta su un database differente, in modo da equilibrare l'archivio e l'I\\O.

## Si possono impostare criteri di conservazione sulle cartelle pubbliche?

Proprio come nelle versioni precedenti di Exchange, è possibile impostare limiti di conservazione sugli elementi. Per ulteriori informazioni, vedere [Limiti per le cartelle pubbliche](limits-for-public-folders-exchange-2013-help.md).

## È possibile specificare quali utenti possono utilizzare una determinata cassetta postale di cartelle pubbliche?

In Exchange 2007 ed Exchange 2010, era possibile specificare quali utenti avrebbero avuto accesso a determinate cartelle pubbliche. In Exchange 2013, è possibile impostare la cassetta postale di cartelle pubbliche per utente. A tale scopo, utilizzare il cmdlet [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)) con il parametro *DefaultPublicFolderMailbox*.

```powershell
Set-Mailbox -Identity kweku@contoso.com -DefaultPublicFolderMailbox "PF_Administration"
```

## Se la gerarchia master subisce un calo, qual è l'impatto dell'utente?

Se la cassetta postale di cartelle pubbliche della gerarchia master subisce un calo, gli utenti possono visualizzare le cartelle pubbliche ma non scriverci. Per evitare un calo della gerarchia, si consiglia di includere le cartelle pubbliche in un gruppo di disponibilità del database. Per informazioni sui gruppi di disponibilità del database, vedere [Gruppi di disponibilità dei database (DAG)](database-availability-groups-dags-exchange-2013-help.md).

## Si può decidere quale cassetta postale di cartelle pubbliche sarà la cassetta postale della gerarchia master?

No. Se si tenta di modificare la cassetta postale della gerarchia master, si riceverà un messaggio di errore.

## Le cartelle pubbliche dispongono di funzionalità di ricerca full-text?

Sì. In Exchange 2013 è disponibile la funzionalità di ricerca full-text per le cartelle pubbliche. Non è tuttavia possibile eseguire la ricerca in più cartelle pubbliche.


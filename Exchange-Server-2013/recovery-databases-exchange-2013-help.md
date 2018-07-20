---
title: 'Database di ripristino: Exchange 2013 Help'
TOCTitle: Database di ripristino
ms:assetid: f3c6fd0b-2e25-442e-a0fc-46f663130c3e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876954(v=EXCHG.150)
ms:contentKeyID: 50482039
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Database di ripristino

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-02_

Un database di ripristino (RDB) è un tipo speciale di database delle cassette postali che consente di montare un database delle cassette postali ripristinato e di estrarre i dati dal database ripristinato durante un'operazione di ripristino. Per estrarre i dati da un database di ripristino è possibile utilizzare il cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829875\(v=exchg.150\)). Dopo l'estrazione, i dati possono essere esportati in una cartella o uniti in una cassetta postale esistente. I database di ripristino consentono di ripristinare i dati da un backup o dalla copia di un database senza interferire con l'accesso dell'utente ai dati correnti.

Microsoft Exchange Server 2013 supporta la possibilità di ripristinare i dati direttamente in un database di ripristino. L'installazione dei dati recuperati come database di ripristino consente all'amministratore di ripristinare le singole cassette postali o i singoli elementi di una cassetta postale. Il recupero di un database di ripristino può essere effettuato in due modi:

  - Se esiste già un database di ripristino, l'applicazione può smontare il database, ripristinare i dati nel database di ripristino e i file di registro e quindi montare nuovamente il database.

  - È possibile ripristinare il database e i file di registro in qualsiasi percorso su disco. Exchange analizza i dati ripristinati e riesegue i registri delle transazioni per aggiornare il database; successivamente è possibile configurare un database di ripristino affinché faccia riferimento a file di database già ripristinati.

## Differenza tra un database delle cassette postali e un database di ripristino

I database di ripristino differiscono per diversi aspetti dai database delle cassette postali standard:

  - Un database di ripristino viene creato utilizzando Exchange Management Shell.

  - Non è possibile inviare messaggi di posta da o verso un database di ripristino. L'accesso di tutti i protocolli client (compresi SMTP, POP3 e IMAP4) a un database di ripristino è bloccato. Questa struttura impedisce l'uso di un database di ripristino per inserire o rimuovere messaggi di posta dal sistema di messaggistica.

  - L'accesso MAPI client tramite Microsoft Office Outlook o Outlook Web App è bloccato. L'accesso MAPI è supportato per un database di ripristino, ma solo attraverso applicazioni e strumenti di ripristino. Quando si utilizza MAPI per accedere a una cassetta postale in un database di ripristino è necessario specificare sia il GUID della cassetta postale sia il GUID del database.

  - Le cassette postali in un database di ripristino non possono essere connesse agli account utente. Per consentire a un utente di accedere ai dati in una cassetta postale di un database di ripristino, è necessario unire la cassetta postale a una cassetta postale esistente o esportata in una cartella.

  - I criteri di gestione del sistema e delle cassette postali non vengono applicati. Questa struttura impedisce l'eliminazione degli elementi in un database di ripristino durante il processo di ripristino eseguito dal sistema.

  - La manutenzione in linea non viene eseguita per i database di ripristino.

  - La registrazione circolare non può essere abilitata per i database di ripristino.

  - Su un server Cassette postali è possibile montare un solo database di ripristino per volta. L'uso di un database di ripristino non viene conteggiato nel limite di database per server Cassette postali.

  - Non è possibile creare copie dei database delle cassette postali di un database di ripristino.

  - Un database di ripristino può essere utilizzato come destinazione per le operazioni di ripristino, ma non per le operazioni di backup.

  - Un database ripristinato montato come database di ripristino non è in alcun modo associato alla cassetta postale originale.

## Utilizzo di un database di ripristino

Prima di utilizzare un database di ripristino è necessario rispettare alcuni requisiti. Un database di ripristino può essere utilizzato solo per i database delle cassette postali di Exchange 2013. I database delle cassette postali di versioni precedenti di Exchange non sono supportati. Inoltre, la cassetta postale di destinazione utilizzata per l'unione e l'estrazione dei dati deve trovarsi nella stessa foresta di Active Directory del database montato nel database di ripristino.

Un database di ripristino non può essere utilizzato per ripristinare dati in diverse situazioni, ad esempio:

  - **Ripristino temporaneo dallo stesso server**   È possibile eseguire un ripristino da un database di ripristino dopo aver ripristinato il database originale da un backup durante un'operazione di ripristino temporaneo.

  - **Ripristino temporaneo da un server alternativo**   È possibile utilizzare un server alternativo per ospitare il database temporaneo e successivamente eseguire un ripristino dei dati da un database di ripristino dopo aver ripristinato il database originale dal backup.

  - **Ripristino della cassetta postale**   È possibile ripristinare dal backup una singola cassetta postale una volta trascorso il periodo di conservazione della cassetta postale eliminata. Successivamente è possibile estrarre i dati dalla cassetta postale ripristinata e copiarli in una cartella di destinazione o unirli a un'altra cassetta postale.

  - **Ripristino di elementi specifici**   È possibile ripristinare dal backup i dati che sono stati eliminati da una cassetta postale.


> [!NOTE]
> Gli elenchi di controllo di accesso alle cartelle non vengono conservati durante il ripristino del contenuto in una cassetta postale attiva. Poiché il processo di ripristino implica in genere il ripristino dei dati delle cassette postali e l'unione del contenuto nel database originale, la copia o il ripristino degli elenchi di controllo di accesso non è necessario.



Un database di ripristino è progettato per ripristinare un database delle cassette postali nei seguenti casi e condizioni:

  - Le informazioni logiche relative al database originale e alle cassette postali presenti nel database rimangono intatte e inalterate in Active Directory.

  - È necessario ripristinare una singola cassetta postale o un singolo database. Gli scenari di ripristino includono:
    
      - Ripristino o riparazione di un database mentre è in uso un database temporaneo, con l'obiettivo di unire i due database.
    
      - Ripristino di un database su un server diverso dal server originale per tale database. Se necessario, è possibile unire nuovamente i dati ripristinati nel server originale.
    
      - Ripristino di elementi eliminati in precedenza dalle cassette postali degli utenti una volta trascorso il periodo di conservazione degli elementi eliminati.

I database di ripristino non sono in genere progettati per scenari che richiedono il ripristino di interi server o in cui è necessario ripristinare più database, né per le situazioni di emergenza in cui è necessario modificare o ricostruire la topologia di Active Directory.

Per la procedura dettagliata sulla creazione di un database di ripristino, vedere [Creare un database di ripristino](create-a-recovery-database-exchange-2013-help.md). Per la procedura dettagliata sull'uso di un database di ripristino, vedere [Recupero dei dati utilizzando un database di ripristino](restore-data-using-a-recovery-database-exchange-2013-help.md).


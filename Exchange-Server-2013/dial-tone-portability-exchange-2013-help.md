---
title: 'Portabilità temporanea: Exchange 2013 Help'
TOCTitle: Portabilità temporanea
ms:assetid: ea62fae0-5e0a-460c-beb6-52532c8c8dbc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876950(v=EXCHG.150)
ms:contentKeyID: 51407438
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Portabilità temporanea

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-01-28_

La portabilità temporanea è una caratteristica di Microsoft Exchange Server 2013 che fornisce una soluzione di continuità aziendale limitata in caso di errori relativi a un database delle cassette postali, a un server o a un intero sito. La portabilità temporanea consente agli utenti di disporre di una cassetta postale temporanea per l'invio e la ricezione di posta elettronica durante il ripristino o la riparazione della cassetta postale originale. La cassette postale temporanea può trovarsi sullo stesso server Cassette postali di Exchange 2013 o su un altro server Cassette postali di Exchange 2013 dell'organizzazione che ha i database con la stessa versione dello schema del database. In questo modo un server alternativo può ospitare le cassette postali di utenti precedentemente su un server non più disponibile. I client che supportano l'individuazione automatica vengono automaticamente reindirizzati al nuovo server senza dover aggiornare manualmente il profilo desktop dell'utente. Una volta ripristinati i dati della cassetta postale originale dell'utente, un amministratore può unire la cassetta postale ripristinata e la cassetta postale temporanea dell'utente in una singola cassetta postale aggiornata.

Questo processo di utilizzo della portabilità temporanea è definito *ripristino temporaneo*. Un ripristino temporaneo presuppone la creazione di un database vuoto su un server Cassette postali per sostituire il database danneggiato. Il database vuoto, definito *database temporaneo*, consente agli utenti di inviare e ricevere messaggi di posta elettronica durante il ripristino del database danneggiato.

Sono disponibili tre opzioni per l'esecuzione di un ripristino temporaneo:

  - **Ripristino temporaneo sul server con il database che presenta errori**   Se il server che ospita il database con errori è ancora funzionante, si consiglia di eseguire il ripristino temporaneo su tale server. Il tempo di inattività risulterà inferiore perché non sarà necessario spostare i file di database tra i server. Inoltre, non sarà necessario riconfigurare i profili di messaggistica per i client che non supportano l'individuazione automatica.

  - **Ripristino temporaneo mediante un server alternativo per il database temporaneo**   Se un server si danneggia e necessita di una ricostruzione, il metodo più efficace per fornire agli utenti funzionalità base di posta è di creare un database temporaneo su un altro server e utilizzare la portabilità temporanea per trasferire la configurazione della cassetta postale degli utenti sul nuovo server. Questo processo richiede di spostare il database temporaneo di nuovo sul server originale (ripristinato), pertanto è necessario più tempo per il processo di ripristino complessivo. Inoltre, questo processo è più complesso dell'esecuzione di un ripristino temporaneo sul server originale. Quando si esegue questo processo, il server che ospita il database dei segnali di linea deve avere risorse sufficienti per supportare il carico aggiuntivo di utenti supplementari. Inoltre, se il client dell'utente non supporta l'individuazione automatica, il profilo di messaggistica dovrà essere riconfigurato per fare riferimento al server dei segnali di linea.

  - **Ripristino temporaneo utilizzando e mantenendo un server alternativo per il database temporaneo**   L'opzione è simile alla precedente, tranne per il fatto che non viene eseguito il ritorno al server originale. Questa opzione è consigliata nelle situazioni in cui non è possibile ripristinare il server danneggiato. In questo scenario, in genere gli utenti rimangono sul server alternativo anche al termine dell'operazione di ripristino. Quando si esegue questo processo, il server che ospita il database dei segnali di linea deve avere risorse sufficienti per supportare il carico aggiuntivo di utenti supplementari. Inoltre, se il client dell'utente non supporta l'individuazione automatica, il profilo di messaggistica dovrà essere riconfigurato per fare riferimento al server dei segnali di linea.

Tutte le tre opzioni richiedono le stesse procedure di base:

1.  **Creare un database temporaneo vuoto per sostituire il database con errori.**
    
    Questo nuovo database permetterà agli utenti in possesso di cassette postali sul database danneggiato di inviare e ricevere nuovi messaggi. La portabilità temporanea consente di trasferire un utente su un database differente senza spostare la cassetta postale. Se si crea il database temporaneo su un server diverso rispetto a quello che ospita il database danneggiato, è necessario spostare la configurazione della cassetta postale sul nuovo server.

2.  **Ripristinare il vecchio database.**
    
    Utilizzare il software di backup e ripristino utilizzato comunemente per ripristinare il database danneggiato. Se non è disponibile un backup del database danneggiato, procedere con il ripristino adottando altri mezzi. Se si utilizza lo stesso server per il ripristino temporaneo, è necessario ripristinare il database in un database di ripristino (RDB).

3.  **Scambiare il database temporaneo con il database ripristinato.**
    
    Dopo il ripristino del database danneggiato è possibile scambiarlo con il database temporaneo. Questa operazione consente agli utenti di inviare e ricevere messaggi di posta elettronica e di accedere a tutti i dati contenuti nel database ripristinato. Se gli utenti erano stati trasferiti a un database temporaneo su un altro server, è necessario trasferire la configurazione della cassetta postale sul server di partenza.

4.  **Unire i database.**
    
    Per recuperare i dati dal database temporaneo e importarli nel database ripristinato, utilizzare il cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/it-it/library/ff829875\(v=exchg.150\)).

Per la procedura dettagliata di esecuzione del ripristino temporaneo, vedere [Esecuzione di un ripristino del segnale](perform-a-dial-tone-recovery-exchange-2013-help.md).


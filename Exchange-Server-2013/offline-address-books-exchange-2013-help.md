---
title: 'Rubriche offline: Exchange 2013 Help'
TOCTitle: Rubriche offline
ms:assetid: a6bcb072-4ab9-400e-a5d0-c05264629097
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232155(v=EXCHG.150)
ms:contentKeyID: 50481363
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rubriche offline

 

_**Si applica a:** Exchange Server 2010, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-11-16_

Una rubrica offline è la copia di una raccolta di indirizzi di posta elettronica scaricata in modo tale da consentire a un utente di Microsoft Outlook di accedere alla rubrica quando è disconnesso dal server. Microsoft Exchange genera i nuovi file della rubrica offline, li comprime e li archivia in una condivisione locale. È possibile scegliere quali elenchi di indirizzi rendere disponibili agli utenti che lavorano offline e configurare il metodo di distribuzione di tali rubriche.

Per ulteriori informazioni sugli elenchi di indirizzi, vedere [Elenchi indirizzi](address-lists-exchange-2013-help.md).


> [!IMPORTANT]
> I dati OAB sono prodotti dal servizio OABGen di Microsoft Exchange, un assistente cassette postali. Se si utilizza il descrittore di protezione per impedire agli utenti di visualizzare destinatari specifici in Active Directory, gli utenti che scaricano la rubrica offline potranno visualizzare tali destinatari nascosti. Per nascondere un destinatario da un elenco di indirizzi, impostare quindi il parametro <EM>HiddenFromAddressListsEnabled</EM> sui cmdlet <A href="https://technet.microsoft.com/it-it/library/aa998596(v=exchg.150)">Set-PublicFolder</A>, <A href="https://technet.microsoft.com/it-it/library/aa995950(v=exchg.150)">Set-MailContact</A>, <A href="https://technet.microsoft.com/it-it/library/aa995971(v=exchg.150)">Set-MailUser</A>, <A href="https://technet.microsoft.com/it-it/library/bb123796(v=exchg.150)">Set-DynamicDistributionGroup</A>, <A href="https://technet.microsoft.com/it-it/library/bb123981(v=exchg.150)">Set-Mailbox</A> e <A href="https://technet.microsoft.com/it-it/library/bb124955(v=exchg.150)">Set-DistributionGroup</A>. In alternativa, è possibile creare una nuova Rubrica offline predefinita che non contiene i destinatari nascosti. Per informazioni dettagliate su come aggiungere o rimuovere elenchi di indirizzi da una rubrica offline, vedere <A href="add-an-address-list-to-or-remove-an-address-list-from-an-offline-address-book-exchange-2013-help.md">Aggiungere un elenco di indirizzi o rimuovere un elenco di indirizzi di una Rubrica fuori rete</A>.



Per informazioni sulle attività di gestione relative alle rubriche offline? vedere [Procedure della Rubrica fuori rete](offline-address-book-procedures-exchange-2013-help.md).

**Sommario**

Moving OABs between Exchange versions

OAB version 4 and Outlook clients

Web-based distribution

OAB considerations

## Spostamento di rubriche offline tra versioni di Exchange

In Exchange 2007 ed Exchange 2010 viene utilizzato il cmdlet **Move-OfflineAddressBook** per spostare la generazione della rubrica offline su un altro server Cassette postali. Exchange 2013 supporta solamente la rubrica offline (versione 4). È la stessa versione della rubrica offline predefinita in Exchange 2010. Non è possibile configurare Exchange 2013 per generare altre versioni della rubrica offline; la generazione della rubrica offline avviene sul server Cassette postali su cui risiede la cassetta postale dell'organizzazione. Di conseguenza, per spostare la generazione della rubrica offline in Exchange 2013, occorre spostare la cassetta postale dell'organizzazione. È possibile spostare la generazione della rubrica offline solo in un altro database delle cassette postali di Exchange 2013. Non è possibile spostare la generazione della rubrica offline in una versione precedente di Exchange. Per trovare la cassetta postale dell'organizzazione per la rubrica offline di Exchange 2013, eseguire il seguente comando Shell:

    Get-Mailbox -Arbitration | where {$_.PersistedCapabilities -like "*oab*"}

È quindi possibile utilizzare i cmdlet **MoveRequest** per spostare la cassetta postale.

## Rubrica offline versione 4 e client Outlook

Exchange 2013 supporta solo la versione 4 della rubrica offline, introdotta in Exchange 2003 Service Pack 2 (SP2) e supportata da Outlook 2007, Outlook 2010 e Outlook 2013. La rubrica offline Unicode consente ai computer client di ricevere aggiornamenti differenziali invece che i download completi della rubrica offline e dimensioni di file ridotte.

## Client Outlook che utilizzano la rubrica offline versione 4

Per Outlook 2013, Outlook 2010, Outlook 2007 e i client che utilizzano la versione 4 della rubrica offline, se la dimensione dei file changes.oab è pari o superiore alla metà della dimensione di tutti i file della rubrica offline, Outlook avvia il download completo della rubrica offline.

## Distribuzione basata su Web

La *distribuzione basata sul Web* è il metodo di distribuzione con cui i client Outlook 2013, Outlook 2010 o Outlook 2007 che lavorano offline possono accedere alla rubrica offline.

L'utilizzo della distribuzione basata su Web presenta molti vantaggi, tra i quali:

  - Supporto di più computer client simultaneamente.

  - Riduzione dell'utilizzo della larghezza di banda.

  - Maggior controllo dei punti di distribuzione della Rubrica offline. Con la distribuzione basata su Web, il punto di distribuzione è l'indirizzo Web HTTPS in cui i computer client possono scaricare la rubrica offline.

Per un miglior utilizzo della distribuzione basata su Web, i computer client devono eseguire Outlook 2013, Outlook 2010 o Outlook 2007.

Per funzionare correttamente, la distribuzione basata su Web dipende dai seguenti componenti:

  - **Processo di generazione della Rubrica offline**   Processo con cui viene creata e aggiornata la Rubrica offline in Exchange. Per creare e aggiornare la rubrica offline, il servizio OABGen viene eseguito sul server Cassette postali su cui si trova la cassetta postale dell'organizzazione. Per supportare la distribuzione della rubrica offline, questo server deve essere un server Cassette postali di Exchange.

  - **Distribuzione della rubrica offline**   Se un client avvia la richiesta di distribuzione della rubrica offline, la richiesta verrà indirizzata attraverso un server Accesso client. Il server Accesso client inoltra la richiesta al server Cassette postali che ospita i file della rubrica offline. I file della rubrica offline vengono distribuiti direttamente dal server Cassette postali al client.

  - **Directory virtuale della Rubrica offline**   La directory virtuale della Rubrica offline è il punto di distribuzione utilizzato dal metodo di distribuzione basata su Web. Per impostazione predefinita, quando si installa Exchange, viene creata una nuova directory virtuale denominata **OAB** nel sito Web interno predefinito in IIS (Internet Information Services). Se esistono utenti sul lato client che si connettono a Outlook esternamente al firewall dell'organizzazione, è possibile aggiungere un sito Web esterno. In alternativa, quando viene eseguito il cmdlet **New-OABVirtualDirectory** in Shell, viene creata una nuova directory virtuale denominata OAB nel sito Web IIS predefinito sul server Accesso client Exchange locale. Per informazioni, vedere [Creare una directory virtuale della Rubrica offline](create-an-offline-address-book-virtual-directory-exchange-2013-help.md).

  - **Servizio di individuazione automatica**   È una funzionalità disponibile in Outlook 2013, Outlook 2010 o Outlook 2007 e in alcuni dispositivi mobili che configura automaticamente i client per l'accesso a Exchange. Il servizio è in esecuzione su un server Accesso client e restituisce l'URL corretto della Rubrica fuori rete per una specifica connessione del client.

## Considerazioni relative alla rubrica offline

Per la pianificazione e l'implementazione della strategia relativa alle Rubriche offline è consigliabile valutare i fattori seguenti:

  - Dimensione della Rubrica offline dell'organizzazione. Per ulteriori informazioni, vedere OAB size considerations più avanti in questo argomento.

  - Numero di download della Rubrica offline.

  - Numero e frequenza delle modifiche del nome distinto principale.

  - Mancate corrispondenze dell'indirizzo SMTP.

  - Numero complessivo di modifiche apportate alla directory.

## Considerazioni relative alla dimensione delle rubriche offline

In alcune organizzazioni, la Rubrica offline è un file di piccole dimensioni, il cui download viene richiesto dagli utenti solo occasionalmente. In questo caso, il download di una Rubrica offline non rappresenta un problema. Tuttavia, nel caso di organizzazioni complesse con directory di grandi dimensioni o di organizzazioni che hanno distribuito Outlook 2003 in modalità cache di Exchange, questa operazione può rappresentare un problema, in particolare se i server Exchange dell'organizzazione sono consolidati in un centro dati regionale.

La dimensione di una Rubrica offline può variare da pochi megabyte ad alcune centinaia di megabyte. La dimensione di una Rubrica offline dipende dai seguenti fattori:

  - Uso dei certificati nell'azienda. Maggiore è il numero dei certificati PKI (Public Key Infrastructure), maggiore è la dimensione della Rubrica offline. La dimensione dei certificati PKI varia da 1 KB a 3 KB. Tali certificati PKI contribuiscono in modo determinante alla dimensione di una Rubrica offline.

  - Numero di destinatari di posta in Active Directory.

  - Numero di gruppi di distribuzione in Active Directory.

  - Informazioni aggiunte in Active Directory dalle aziende, relative a ciascun oggetto abilitato all'utilizzo delle cassette postali o all'utilizzo della posta. Ad esempio, alcune organizzazioni compilano le proprietà degli indirizzi per ogni utente, a differenza di altre.


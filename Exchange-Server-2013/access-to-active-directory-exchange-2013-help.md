---
title: 'Accesso ad Active Directory: Exchange 2013 Help'
TOCTitle: Accesso ad Active Directory
ms:assetid: 61080b45-8bce-4c23-b744-ed264d5f0b7d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998561(v=EXCHG.150)
ms:contentKeyID: 50480736
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Accesso ad Active Directory

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In Microsoft Exchange Server 2013 tutte le informazioni relative alla configurazione e ai destinatari vengono archiviate nel database del servizio di directory di Active Directory. Quando un computer che utilizza Exchange 2013 richiede le informazioni sui destinatari e sulla configurazione dell'organizzazione di Exchange, è necessario che esegua una query in Active Directory per accedere alle informazioni. I server Active Directory devono essere disponibili affinché Exchange 2013 funzioni correttamente.

In questo argomento viene spiegato come Exchange 2013 archivia e recupera le informazioni in Active Directory per consentire la pianificazione degli accessi ad Active Directory. In questo argomento vengono inoltre fornite informazioni necessarie per il ripristino di oggetti Exchange 2013 di Active Directory eliminati.

## Informazioni su Exchange archiviate in Active Directory

Le informazioni vengono archiviate nei tre tipi di partizioni logiche del database Active Directory descritte nelle seguenti sezioni:

  - Partizione dello schema

  - Partizione di configurazione

  - Partizione di dominio

## Partizione dello schema

Nella partizione di schema vengono archiviati i due tipi di informazioni riportati di seguito:

  - **Classi di schema**, che definiscono tutti i tipi di oggetto che possono essere creati e archiviati inActive Directory.

  - **Attributi di schema**, che definiscono tutte le proprietà che possono essere utilizzate per descrivere gli oggetti archiviati in Active Directory.

Quando si esegue il processo di preparazione di Exchange 2013 o si installa il primo ruolo server Active Directory nella foresta, il processo di preparazione di Active Directory aggiunge numerosi attributi e classi allo schema di Active Directory. Le classi aggiunte allo schema vengono utilizzate per creare oggetti specifici per Exchange, ad esempio agenti e connettori. Gli attributi aggiunti allo schema consentono invece di configurare gli oggetti specifici per Exchange, nonché i gruppi e gli utenti abilitati all'utilizzo della posta. Negli attributi sono incluse proprietà quali le impostazioni di Microsoft Office Outlook Web Access e le impostazioni della messaggistica unificata di Microsoft Exchange. In ciascun controller di dominio e server di catalogo globale presente nella foresta è contenuta una replica completa della partizione di schema.

Per ulteriori informazioni sulle modifiche dello schema in Exchange 2013, vedere [Modifiche allo schema di Active Directory in Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

## Partizione di configurazione

Nella partizione di configurazione vengono archiviate informazioni sulla configurazione a livello di foresta, incluse quelle sulla configurazione dei siti Active Directory, sulle impostazioni globali di Exchange, sulle impostazioni di trasporto e sui criteri delle cassette postali. Ogni tipo di informazione di configurazione viene archiviata in un contenitore della partizione. Le informazioni sulla configurazione di Exchange vengono incluse in una sottocartella del contenitore relativo ai servizi della partizione. Tra le informazioni archiviate in questo contenitore sono presenti le seguenti:

  - Elenchi di indirizzi

  - Criteri delle cassette postali delle rubriche

  - Gruppi amministrativi

  - Impostazione dell'accesso client

  - Connessioni

  - Impostazioni delle cassette postali mobili

  - Impostazioni globali

  - Impostazioni di monitoraggio

  - Criteri di sistema

  - Contenitore criteri di conservazione

  - Impostazioni di trasporto

In ciascun controller di dominio e server di catalogo globale presente nella foresta è contenuta una replica completa della partizione di configurazione.

## Partizione di dominio

Nella partizione di dominio vengono archiviate informazioni all'interno di contenitori e unità organizzative predefiniti creati dall'amministratore di Active Directory. In questi contenitori sono presenti gli oggetti specifici per il dominio. I dati in questione includono gli oggetti di sistema di Exchange e informazioni sui computer, gli utenti e i gruppi presenti nel dominio. Una volta installato Exchange 2013, Exchange aggiorna gli oggetti archiviati nella partizione per supportare la funzionalità di Exchange, che influisce sulle modalità di archiviazione e di accesso alle informazioni relative ai destinatari.

In ogni controller di dominio è contenuta una replica completa della partizione di dominio per la quale quest'ultimo è autorevole. In ogni server di catalogo globale presente nella foresta è contenuto un sottoinsieme delle informazioni archiviate in ciascuna partizione di dominio della foresta.

## Modalità di accesso alle informazioni presenti in Active Directory da parte di Exchange 2013

Exchange 2013 accede alle informazioni archiviate in Active Directory mediante un'API di Active Directory. Il servizio Topologia di Microsoft ExchangeActive Directory viene eseguito su tutti i ruoli server di Exchange 2013. Si tratta di un servizio in grado di leggere le informazioni presenti in tutte le partizioni di Active Directory. I dati recuperati vengono memorizzati nella cache e utilizzati dai server Exchange 2013 per individuare la posizione del sito di Active Directory di tutti i servizi di Exchange installati nell'organizzazione.

Per ulteriori informazioni sul rilevamento della topologia e dei servizi, vedere [Pianificazione dell'utilizzo di siti di Active Directory per il routing della posta](planning-to-use-active-directory-sites-for-routing-mail-exchange-2013-help.md).

Exchange 2013 è un'applicazione compatibile con il sito di Active Directory che, comunicando con i server di directory disponibili nello stesso sito del server Exchange, consente di ottimizzare il traffico di rete. Per recuperare informazioni relative ai destinatari e ad altri ruoli di server Exchange 2013, ogni ruolo di server nell'organizzazione Active Directory deve comunicare con Exchange 2013. Nelle sezioni che seguono vengono descritti i dati recuperati da ciascun ruolo del server.

Per impostazione predefinita, ogni volta che un server Exchange 2013 viene avviato, esegue il binding a un controller di dominio e a un server di catalogo globale selezionati in modo casuale nel suo sito. È possibile visualizzare i server di directory selezionati utilizzando il cmdlet **Get-ExchangeServer** in Exchange Management Shell. È inoltre possibile utilizzare il cmdlet **Set-ExchangeServer** per configurare un elenco statico di controller di dominio a cui un server Exchange 2013 deve eseguire il binding oppure un elenco di controller di dominio da escludere.


> [!IMPORTANT]
> È possibile configurare un controller di dominio di Windows Server 2008 come server di directory di sola lettura. Questa configurazione è utile quando si desidera distribuire un controller di dominio o un server di catalogo globale in un sito remoto per scopi di autenticazione e autorizzazione, ma non si desidera consentire agli amministratori in quel sito di apportare delle modifiche ad Active Directory. Tuttavia, non è possibile distribuire un server Exchange 2013 in un sito che contiene solo server di directory di sola lettura.



## Ruolo del server Cassette postali

Il ruolo del server Cassetta Postale recupera le informazioni sulla configurazione relative agli utenti delle cassette postali e le archivia in Active Directory. Inoltre, per Exchange 2013, il server Cassette postali include tutti i componenti server tradizionali presenti in Exchange 2010: protocolli di Accesso client, servizi di trasporto, database delle cassette postali e messaggistica unificata. Il server Cassette postali gestisce tutta l'attività per le cassette postali attive su quel server.

## Ruolo del server Accesso client

In Exchange 2013, il server Accesso client fornisce l'autenticazione, il reindirizzamento limitato e i servizi proxy. Il server Accesso Client non esegue alcun rendering dei dati. Il server Accesso Client è un thin server senza stato. Non vi sono mai oggetti in coda o archiviati sul server Accesso client. Il server Accesso client include tutti i protocolli di accesso client normalmente disponibili: HTTP, POP e IMAP, SMTP.

## Ripristino degli oggetti di Exchange eliminati

Il Cestino di Active Directory consente di ridurre i tempi di inattività del servizio di directory perché permette di conservare e ripristinare gli oggetti Active Directory eliminati per errore senza dover ripristinare i dati di Active Directory dai backup oppure riavviare Servizi di dominio Active Directory (AD DS) o i controller di dominio.

Quando si ripristinano oggetti Active Directory correlati a Exchange che sono stati eliminati è fondamentale ricordare che gli oggetti Exchange non esistono separatamente. Ad esempio, quando si abilitata un utente alla posta elettronica, per quell'utente vengono stabiliti diversi criteri e collegamenti che si basano sulla configurazione corrente di Exchange. Quando si ripristina un oggetto destinatario o configurazione di Exchange eliminato possono verificarsi due problemi:

  - **Conflitti**   Alcuni attributi Exchange devono essere univoci all'interno di una foresta. Ad esempio, due utenti differenti non possono avere lo stesso indirizzo proxy (di posta elettronica). Active Directory non impone l'unicità degli indirizzi proxy; sono gli strumenti amministrativi di Exchange che ne verificano l'univocità. Inoltre, i criteri per gli indirizzi di posta elettronica di Exchange risolvono automaticamente eventuali conflitti nelle assegnazioni degli indirizzi proxy sulla base di regole deterministiche. Pertanto, è possibile ripristinare un oggetto utente Exchange e di conseguenza creare un conflitto con indirizzi proxy o altri attributi che dovrebbero essere univoci.

  - **Configurazioni errate**   Exchange ha una serie di regole automatizzate che assegnano diversi criteri e impostazioni. Se si elimina un destinatario e poi si modificano le regole o i criteri, il ripristino di un oggetto utente Exchange potrebbe portare all'assegnazione di un utente a un criterio sbagliato (o perfino non più disponibile).

Le seguenti linee guida sono utili per limitare i problemi che possono verificarsi quando si ripristinano oggetti correlati a Exchange già eliminati:

  - Se un oggetto di configurazione Exchange è stato eliminato utilizzando gli strumenti di gestione di Exchange, non è possibile ripristinarlo. Al contrario, ricreare l'oggetto utilizzando gli strumenti di gestione di Exchange (Exchange Admin Center o Exchange Management Shell).

  - Se si è eliminato un oggetto di configurazione di Exchange senza utilizzare gli strumenti di gestione di Exchange, è necessario ripristinarlo appena possibile. Quanto più numerose sono le modifiche apportate al sistema a livello di amministrazione e configurazione dopo l'eliminazione, tanto più frequenti saranno gli errori di configurazione quando si ripristineranno gli oggetti.

  - Se si ripristinano i destinatari Exchange (contatti, utenti o gruppi di distribuzione) eliminati, verificare con attenzione la presenza di eventuali conflitti ed errori legati agli oggetti ripristinati. Se sussiste la possibilità che i criteri o altri elementi di configurazione di Exchange relativi ai destinatari siano stati modificati dopo l'eliminazione, riapplicare i criteri correnti ai destinatari ripristinati in modo che siano configurati correttamente.

## Ulteriori informazioni

[Active Directory Recycle Bin Guida dettagliata](https://go.microsoft.com/fwlink/p/?linkid=178720)

[Introduzione ai miglioramenti centro di amministrazione di Active Directory (livello 100)](https://go.microsoft.com/fwlink/p/?linkid=267641)

[Gestione di Active Directory di dominio Active Directory utilizzando Centro di amministrazione di Active Directory (livello 200) avanzata](https://go.microsoft.com/fwlink/p/?linkid=267642)


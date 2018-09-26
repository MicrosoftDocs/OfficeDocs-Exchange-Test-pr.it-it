---
title: 'Gestione delle copie del database delle cassette postali: Exchange 2013 Help'
TOCTitle: Gestione delle copie del database delle cassette postali
ms:assetid: 28cedf1d-365a-4e36-b2ba-6bf81af8684f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335158(v=EXCHG.150)
ms:contentKeyID: 50480209
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione delle copie del database delle cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-08-26_

Dopo la creazione, la configurazione e l'inserimento dei membri del server cassette postali nel gruppo di disponibilità del database, è possibile utilizzare l'interfaccia di amministrazione di Exchange o Exchange Management Shell per aggiungere copie di database delle cassette postali in modo flessibile e granulare.

## Gestione delle copie del database

Dopo aver creato più copie di un database, è possibile utilizzare l'interfaccia di amministrazione di Exchange o Management Shell per monitorare l'integrità e lo stato di ogni copia ed eseguire altre attività di gestione associate alle copie del database. Alcune attività di gestione che potrebbe essere necessario eseguire comprendono la sospensione o la ripresa, il seeding, il monitoraggio, la configurazione delle impostazioni e la rimozione di una copia del database.

## Sospensione e ripresa delle copie del database

Per molte ragioni quali l'esecuzione della manutenzione pianificata, potrebbe essere necessario sospendere e riprendere l'attività di replica continua per una copia del database. Inoltre, alcune attività amministrative, quali il seeding, richiedono innanzitutto la sospensione di una copia del database. Si consiglia di sospendere tutte le attività di replica durante la modifica del percorso del database o dei relativi file di registro. È possibile sospendere e riprendere l'attività di copia del database utilizzando l'interfaccia di amministrazione di Exchange o eseguendo i cmdlet **Suspend-MailboxDatabaseCopy** e **Resume-MailboxDatabaseCopy** in Shell. Per la procedura dettagliata su come sospendere o riprendere l'attività di replica continua per una copia del database, vedere [Sospendere o riprendere una copia del database delle cassette postali](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md).

## Seeding di una copia del database

Il *seeding*, denominato anche *aggiornamento*, indica il processo in cui un database, vuoto o una copia del database di produzione, viene aggiunto al percorso della copia di destinazione su un altro server Cassette postali nello stesso gruppo di disponibilità del database (DAG) del database attivo. Questo diventa il database di riferimento per la copia gestita da quel server.

In base alla situazione, il seeding può indicare un processo avviato automaticamente o manualmente. Quando viene aggiunta una copia del database, viene effettuato il seeding automatico della copia, a condizione che il server di destinazione e la relativa archiviazione siano configurati correttamente. Se si desidera il seeding manuale di una copia del database e non il seeding automatico durante la creazione della copia, è possibile utilizzare il parametro *SeedingPostponed* quando si esegue il cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd298105\(v=exchg.150\)).

Raramente le copie del database necessitano di un nuovo seeding dopo quello iniziale. Ma se fosse necessario eseguire il reseeding o si desidera effettuare il seeding di un database manualmente invece che consentire al sistema di effettuarlo automaticamente, queste attività possono essere eseguite utilizzando la procedura guidata di aggiornamento della copia database delle cassette postali nell'interfaccia di amministrazione di Exchange o utilizzando il cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)) in Shell. Prima di effettuare il seeding di una copia del database, è necessario prima sospendere la copia del database delle cassette postali. Per la procedura dettagliata di esecuzione del seeding di una copia di database, vedere [Aggiornamento di una copia del database delle cassette postali](update-a-mailbox-database-copy-exchange-2013-help.md).

Una volta completata una operazione di seeding automatico, la replica per la copia del database delle cassette postali viene ripresa automaticamente. Se non si desidera la ripresa automatica della replica, è possibile utilizzare il parametro *ManualResume* durante l'esecuzione del cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)).

## Scelta di cosa sottoporre a seeding

Quando si esegue un'operazione di seeding, è possibile scegliere di eseguire il seeding la copia del database delle cassette postali, il catalogo di indicizzazione del contenuto per la copia del database delle cassette postali, o la copia del database e la copia del catalogo dell'indice di contenuto.

Il comportamento predefinito della procedura guidata aggiornamento copia del Database delle cassette postali e il cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)) deve eseguire il seeding della copia del database delle cassette postali sia la copia del catalogo dell'indice di contenuto. Per eseguire il seeding solo la copia del database delle cassette postali senza eseguire il seeding del catalogo di indicizzazione del contenuto, utilizzare il parametro *DatabaseOnly* quando si esegue il cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)) . Per eseguire il seeding solo la copia del catalogo dell'indice di contenuto, utilizzare il parametro *CatalogOnly* quando si esegue il cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)) .

## Selezione dell'origine del seeding

Qualsiasi copia integra del database può essere utilizzata come origine del seeding per un'altra copia di quel database. Tutto questo risulta particolarmente utile quando è presente un gruppo di disponibilità del database esteso su più ubicazioni fisiche. Ad esempio, si consideri una distribuzione del gruppo di disponibilità del database con quattro membri, in cui due (MBX1 e MBX2) si trovano a Portland (Oregon) e due (MBX3 e MBX4) si trovano a New York (New York). Il database delle cassette postali denominato DB1 è attivo su MBX1 e copie passive di DB1 sono presenti su MBX2 e MBX3. Quando si aggiunge una copia di DB1 a MBX4, è disponibile l'opzione di utilizzare la copia su MBX3 come origine del seeding. Nel fare ciò, si evita di effettuare il seeding attraverso il collegamento WAN (wide area network) tra Portland e New York.

Per utilizzare una copia specifica come origine per il seeding durante l'aggiunta di una nuova copia del database, eseguire quanto segue:

  - Utilizzare il parametro *SeedingPostponed* durante l'esecuzione del cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd298105\(v=exchg.150\)) per aggiungere la copia del database. Se non si utilizza il parametro *SeedingPostponed*, sulla copia del database verrà esplicitamente effettuato il seeding utilizzando la copia attiva del database come origine.

  - È possibile specificare il server di origine che si vuole utilizzare come parte della procedura guidata di aggiornamento della copia database delle cassette postali nell'interfaccia di amministrazione di Exchange oppure utilizzare il parametro *SourceServer* durante l'esecuzione del cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)) per specificare il server di origine desiderato per il seeding. Nell'esempio precedente, è necessario specificare MBX3 come server di origine. Se non si utilizza il parametro *SourceServer*, verrà esplicitamente effettuato il seeding utilizzando la copia attiva del database come origine.

## Seeding e reti

Oltre alla selezione di uno specifico server di origine per il seeding di una copia del database delle cassette postali, è anche possibile usare Shell per specificare le reti DAG da utilizzare ed eventualmente ignorare le impostazioni di compressione e crittografia della rete DAG durante l'operazione di seeding.


> [!NOTE]
> Eseguire il seeding del catalogo di indicizzazione un contesto è possibile solo tramite una rete MAPI. Ciò avviene anche se si utilizza il parametro <CODE>-Network</CODE> nel cmdlet Update-MailboxDatabaseCopy.



Per specificare le reti da utilizzare per il seeding, utilizzare il parametro *Network* quando durante l'esecuzione del cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)) e specificare le reti DAG che si desidera utilizzare. Se non si utilizza il parametro *Network*, il sistema si comporta nel modo seguente per la selezione di una rete da utilizzare per l'operazione di seeding:

  - Se i server di origine e di destinazione si trovano nella stessa subnet ed è stata configurata una rete di replica che comprende la subnet, verrà utilizzata la rete di replica.

  - Se i server di origine e di destinazione si trovano in subnet diverse, anche se è stata configurata una rete di replica contenente queste subnet, per il seeding verrà utilizzata la rete client (MAPI).

  - Se i server di origine e di destinazione si trovano in datacenter diversi, per il seeding verrà utilizzata la rete client (MAPI).

A livello di DAG, le reti DAG sono configurate per la crittografia e compressione. Per impostazione predefinita, la crittografia e la compressione vengono utilizzate solo per le comunicazioni su diverse subnet. Se l'origine e la destinazione si trovano in subnet diverse e il DAG è configurato con i valori predefiniti per *NetworkCompression* e *NetworkEncryption*, è possibile sostituire questi valori utilizzando rispettivamente i parametri *NetworkCompressionOverride* e *NetworkEncryptionOverride*, durante l'esecuzione del cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)).

## Processo di seeding

Quando si avvia un processo di seeding utilizzando i cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd298105\(v=exchg.150\)) o [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)), si effettuano le seguenti attività:

1.  Le proprietà del database da Active Directory vengono lette per convalidare il database e i server specificati e per verificare l'esecuzione di Exchange 2013 da parte dei server di origine e di destinazione, entrambi membri dello stesso DAG, e che il database specificato non sia un database di ripristino. Vengono letti anche i percorsi dei file del database.

2.  Le attività di preparazione ai controlli del seeding vengono effettuate dal servizio Replica di Microsoft Exchange sul server di destinazione.

3.  Il servizio Replica di Microsoft Exchange sul server di destinazione consente di controllare la presenza del database e dei file di registro delle transazioni nelle directory dei file lette dai controlli di Active Directory nel passo 1.

4.  Il servizio Replica di Microsoft Exchange consente di restituire le informazioni sullo stato dal server di destinazione all'interfaccia amministrativa da cui è stato eseguito il cmdlet.

5.  Se sono stati superati tutti i controlli preliminari, viene richiesto di confermare l'operazione prima di continuare. Se si conferma l'operazione, il processo continua. Se si verifica un errore durante i controlli preliminari, viene riportato l'errore e l'operazione si interrompe.

6.  L'operazione di seeding viene avviata dal servizio Replica di Microsoft Exchange sul server di destinazione.

7.  Il servizio Replica di Microsoft Exchange consente di sospendere la replica del database per la copia attiva del database.

8.  Le informazioni sullo stato del database vengono aggiornate dal servizio Replica di Microsoft Exchange per riflettere uno stato di seeding.

9.  Se sul server di destinazione ancora non esistono le directory per i database di destinazione e i file di registro, queste vengono create.

10. Viene inoltrata una richiesta di seeding del database dal servizio Replica di Microsoft Exchange sul server di destinazione al servizio Replica di Microsoft Exchange sul server di origine utilizzando TCP. Questa richiesta e le successive comunicazioni per il seeding del database si verificano su una rete DAG configurata come rete di replica.

11. Il servizio Replica di Microsoft Exchange sul server di origine avvia un backup di flusso ESE (Extensible Storage Engine) tramite l'interfaccia del servizio Archivio informazioni di Microsoft Exchange.

12. Il servizio Archivio informazioni di Microsoft Exchange invia un flusso di dati del database al servizio Replica di Microsoft Exchange.

13. I dati del database vengono spostati dal servizio Replica di Microsoft Exchange del server di origine al servizio Replica di Microsoft Exchange del server di destinazione.

14. Il servizio Replica di Microsoft Exchange sul server di destinazione scrive la copia del database in una directory temporanea che si trova nella directory del database principale denominata *temp-seeding*.

15. L'operazione di backup del flusso sul server di origine termina quando viene raggiunta la fine del database.

16. L'operazione di scrittura sul server di destinazione viene completata e il database viene spostato dalla directory temp-seeding al percorso finale. La directory temp-seeding viene eliminata.

17. Sul server di destinazione, il servizio Replica di Microsoft Exchange inoltra una richiesta al servizio Ricerca di Microsoft Exchange per installare il catalogo di indicizzazione del contenuto per la copia del database, se esiste. Se esistono file di catalogo non aggiornati provenienti da un'istanza precedente della copia del database, l'operazione di installazione non andrà a buon fine, provocando la replica del catalogo dal server di origine. Allo stesso modo, se il catalogo non esiste in una una nuova istanza della copia del database sul server di destinazione, è necessaria una copia del catalogo. Il servizio Replica di Microsoft Exchange indica al servizio Ricerca di Microsoft Exchange di sospendere le'indicizzazione per la copia del database mentre un nuovo catalogo viene copiato dall'origine.

18. Il servizio Replica di Microsoft Exchange sul server di destinazione invia una richiesta di seeding del catalogo al servizio Replica di Microsoft Exchange sul server di origine.

19. Sul server di origine, il servizio Replica di Microsoft Exchange richiede le informazioni sulla directory dal servizio Ricerca di Microsoft Exchange e richiede di sospendere l'indicizzazione.

20. Il servizio Ricerca di Microsoft Exchange sul server di origine restituisce le informazioni sulla directory del catalogo di ricerca al servizio Replica di Microsoft Exchange.

21. Il servizio Replica di Microsoft Exchange sul server di origine legge i file di catalogo dalla directory.

22. Il servizio Replica di Microsoft Exchange sul server di origine sposta i dati del catalogo al servizio Replica di Microsoft Exchange sul server di destinazione utilizzando una connessione su una rete di replica. Una volta completata l'operazione di lettura, il servizio Replica di Microsoft Exchange invia una richiesta al servizio Ricerca di Microsoft Exchange per riprendere l'indicizzazione del database di origine.

23. Se nella directory sono presenti file di catalogo sul server di destinazione, il servizio Replica di Microsoft Exchange sul server di destinazione li elimina.

24. Il servizio Replica di Microsoft Exchange sul server di destinazione scrive i dati del catalogo in una directory temporanea denominata *CiSeed.Temp* fino al completo trasferimento dei dati.

25. Il servizio Replica di Microsoft Exchange sposta tutti i dati del catalogo nel percorso finale.

26. Il servizio Replica di Microsoft Exchange sul server di destinazione riprende l'indicizzazione di ricerca sul database di destinazione.

27. Il servizio Replica di Microsoft Exchange sul server di destinazione restituisce lo stato di completamento.

28. Il risultato finale dell'operazione viene inviato all'interfaccia amministrativa da cui è stato chiamato il cmdlet.

## Configurazione delle copie del database

Dopo aver creato una copia del database, è possibile visualizzare e modificare le impostazioni di configurazione, se necessario. È possibile visualizzare alcune informazioni di configurazione esaminando la pagina **Proprietà** di una copia del database nell'interfaccia di amministrazione di Exchange. Si possono anche utilizzare i cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb124924\(v=exchg.150\)) e [Set-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd298104\(v=exchg.150\)) in Shell per visualizzare e configurare le impostazioni di copia del database, quali l'intervallo di riesecuzione, il tempo di ritardo di troncamento e l'ordine di preferenza dell'attivazione. Per la procedura dettagliata su come visualizzare e configurare le impostazioni di copia del database, vedere [Configurazione delle proprietà della copia del database delle cassette postali](configure-mailbox-database-copy-properties-exchange-2013-help.md).

## Utilizzo delle opzioni Intervallo di riesecuzione e Tempo di ritardo di troncamento

Le copie del database delle cassette postali supportano l'utilizzo dei valori *Intervallo di riesecuzione* e *Tempo di ritardo di troncamento*, entrambi espressi in minuti. Impostando un intervallo di riesecuzione, è possibile riportare una copia del database indietro a uno specifico momento. Impostando un tempo di ritardo di troncamento, è possibile utilizzare i registri su una copia passiva del database per eseguire il ripristino dei file di registro sulla copia attiva del database. Siccome entrambe le funzionalità comportano l'aumento temporaneo dei file di registro, il relativo utilizzo influenzerà la progettazione di archiviazione.

## Intervallo di riesecuzione

L'intervallo di riesecuzione indica una proprietà della copia del database delle cassette postali che specifica il tempo, in minuti, del ritardo nella riesecuzione dei file di registro per la copia del database. L'intervallo di riesecuzione inizia da quando un file di registro è stato replicato sulla copia passiva e ha superato il controllo. Ritardando la riesecuzione dei registri sulla copia del database, si ha la possibilità di ripristinare il database a uno specifico momento nel passato. Una copia del database delle cassette postali, configurata con un intervallo di riesecuzione maggiore a 0, viene denominata *copia ritardata del database delle cassette postali* o semplicemente *copia ritardata*.

Una strategia che utilizza le copie del database e le funzionalità di conservazione in caso di dispute in Exchange 2013 può fornire protezione rispetto a una serie di errori che di solito causano la perdita di dati. Tuttavia, queste funzionalità non possono fornire sistemi di sicurezza contro la perdita dei dati in caso di danneggiamento della partizione logica che, sebbene raro, può causare la perdita di dati. Le copie ritardate sono pensate per prevenire la perdita dei dati in caso di danneggiamento della partizione logica. Generalmente, esistono due tipi di danneggiamento della partizione logica:

  - **Danneggiamento della partizione logica del database**   Il checksum delle pagine del database corrisponde, ma i dati delle pagine sono errati logicamente. Questo può verificarsi se ESE tenta di scrivere una pagina del database e, sebbene il sistema operativo indichi che l'operazione è riuscita, i dati non siano stati scritti sul disco o siano stati scritti nel posto sbagliato. Questo viene definito *rilevamento flush*. Per prevenire la perdita dei dati a causa dei rilevamenti flush, ESE comprende un meccanismo di rilevazione flush nel database insieme a una funzionalità di correzione della pagina (ripristino pagina singola).

  - **Danneggiamento della partizione logica di archiviazione**   I dati vengono aggiunti, eliminati o manipolati in modo imprevisto. Questi casi sono generalmente causati da applicazioni di terze parti. Generalmente, questa situazione viene percepita dall'utente come un danneggiamento. L'archivio di Exchange considera la transazione che ha causato il danneggiamento della partizione logica come una serie di operazioni MAPI valide. La funzionalità Conservazione per controversia legale in Exchange 2013 fornisce una protezione contro il danneggiamento della partizione logica (poichè previene l'eliminazione permanente del contenuto da parte di una applicazione utente). Tuttavia, esistono scenari per cui una cassetta postale utente raggiunge uno stato di danneggiamento tale che risulta più semplice ripristinare il database ad un momento precedente del danneggiamento e quindi esportare la cassetta postale utente per recuperare i dati corretti.

La combinazione delle copie del database, dei criteri di conservazione e del ripristino di singole pagine tramite ESE non offre sistemi di sicurezza nel caso di un danno gravissimo alla partizione logica dell'archivio, anche se raro. La decisione di utilizzare una copia del database con un intervallo di riesecuzione (copia ritardata) dipende dalle applicazioni di terze parti che si utilizzano e dalla cronologia dell'organizzazione con il danneggiamento della partizione logica dell'archivio.

Le copie ritardate possono autoripristinare in Exchange 2013 quando si richiama la riproduzione automatica del registro per riprodurre i file di registro in determinati scenari:

  - Raggiungimento di una soglia di spazio insufficiente su disco

  - Quando la copia ritardata ha un danneggiamento fisico è necessaria un'applicazione di patch alla pagina

  - Quando sono presenti meno di tre copie integre disponibili (solo attivo o passivo; copie del database ritardate non sono conteggiate) per più di 24 ore

Pagina applicazione di patch è disponibile per le copie ritardate tramite questa funzionalità di riproduzione automatica. Se il sistema rileva che è necessaria per una copia ritardata applicate patch per pagina, i registri vengono riprodotti automaticamente nella copia ritardata per eseguire l'applicazione di patch di pagina. Le copie ritardate anche richiamare questa funzionalità di riproduzione automatico quando viene raggiunta una soglia di spazio su disco insufficiente e quando la copia ritardata è stata rilevata come copia disponibile solo per un determinato periodo di tempo.

Il comportamento di riproduzione delle copie ritardate è disabilitato per impostazione predefinita e può essere abilitato utilizzando il comando seguente.

```powershell
Set-DatabaseAvailabilityGroup <DAGName> -ReplayLagManagerEnabled $true
```

Una volta abilitata, la riproduzione avviene quando ci sono meno di tre copie. È possibile modificare il valore predefinito di 3, modificando il seguente valore di registro DWORD.

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagManagerNumAvailableCopies**

Per abilitare la riproduzione per il raggiungimento della soglia di spazio insufficiente su disco, è necessario configurare la seguente voce di registro.

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagLowSpacePlaydownThresholdInMB**

Dopo aver configurato tutte le impostazioni di registro, riavviare il servizio Microsoft Exchange DAG Management per rendere effettive le modifiche.

Come esempio, considerare un ambiente dove un dato database dispone di 4 copie (3 copie ad elevata disponibilità ed 1 copia ritardata) e l'impostazione predefinita è utilizzata per ReplayLagManagerNumAvailableCopies. Se una copia non ritardata non è in grado di funzionare per qualsiasi motivo (ad esempio è sospeso) la copia ritardata riprodurrà automaticamente i rispettivi file di registro in 24 ore.

Se si sceglie di utilizzare ritardate copie senza abilitare il parametro `ReplayLagManagerEnabled` , tenere presente le implicazioni seguenti:

  - L'intervallo di riesecuzione indica un valore configurato dall'amministratore e per impostazione predefinita è disabilitato.

  - L'impostazione dell'intervallo di riesecuzione ha un valore predefinito pari a 0 giorni e un valore massimo di 14 giorni.

  - Le copie ritardate non sono considerate copie altamente disponibili. Al contrario, sono progettate per eseguire un ripristino di emergenza, per proteggere da danneggiamenti logici dell'archivio.

  - Maggiore è l'impostazione dell'intervallo di riesecuzione, più lungo sarà il processo di ripristino del database. In base al numero di file di registro che è necessario riprodurre durante il ripristino e della velocità a cui l'hardware può riprodurli, possono essere necessarie diverse ore per ripristinare un database.

  - Si consiglia di determinare se le copie ritardate sono fondamentali per la strategia globale del ripristino di emergenza. Se sono fondamentali per la strategia, si consiglia l'utilizzo di più copie ritardate o l'impiego di un array ridondante di dischi indipendenti (RAID) per proteggere un'unica copia ritardata, se non si dispone di più copie ritardate. Se si smarrisce un disco o viene danneggiato, non si perde il punto di ripristino.

  - Le copie ritardate non sono riparabili con la funzionalità di ripristino di singole pagine tramite ESE. Se in una copia ritardata viene riscontrato il danneggiamento di una pagina del database (ad esempio, un errore -1018), sarà necessario sottoporla a reseeding (operazione che le farà perdere l'aspetto di copia ritardata).

L'attivazione e il ripristino di una copia ritardata del database delle cassette postali è un processo semplice se si desidera che il database esegua di nuovo tutti i file di registro e renda corrente la copia del database. Se si desidera eseguire nuovamente i file di registro fino a un determinato momento, l'operazione può rivelarsi più complicata, in quanto è necessario manipolare manualmente i file di registro ed eseguire Exchange Server Utilità database (Eseutil.exe).

Per la procedura dettagliata su come sospendere una copia del database delle cassette postali, vedere [Attivare una copia del database delle cassette postali ritardata](activate-a-lagged-mailbox-database-copy-exchange-2013-help.md).

## Intervallo di troncamento

Il tempo di ritardo di troncamento indica una proprietà della copia del database delle cassette postali che specifica la quantità di tempo, in minuti, per ritardare l'eliminazione dei registri per la copia del database dopo la riesecuzione dei file di registro nella copia del database. Il tempo di ritardo di troncamento inizia quando un file di registro è stato replicato nella copia passiva, ha superato il controllo ed è stato correttamente rieseguito nella copia del database. Ritardando il troncamento dei file di registro dalla copia del database, si ha la possibilità di correggere gli errori che riguardano i file di registro per la copia attiva del database.

## Copie del database e troncamento dei registri

Il troncamento del registro funziona in Exchange 2013 come Exchange 2010. Comportamento di troncamento dipende dal ritardo tempi e troncamento ritardo tempo le impostazioni di riproduzione per la copia.

Per ottenere il troncamento dei file di registro di una copia del database quando le impostazioni di intervallo vengono lasciate al valore predefinito di 0 (disabilitato), è necessario soddisfare i seguenti criteri:

  - Deve essere disponibile una copia di backup del file di registro o deve essere abilitata la registrazione circolare.

  - Il file di registro deve essere al di sotto del checkpoint (il file di registro minimo richiesto per il ripristino) del database.

  - Tutte le altre copie ritardate devono avere ispezionato il file di registro.

  - Tutte le altre copie (non ritardate) devono aver eseguito di nuovo il file di registro.

Per ottenere il troncamento di una copia ritardata del database, è necessario soddisfare i seguenti criteri:

  - Il file di registro deve essere al di sotto del checkpoint per il database.

  - Il file di registro deve essere precedente a ReplayLagTime + TruncationLagTime.

  - Il file di registro deve essere stato troncato nella copia attiva.

In Exchange 2013 il troncamento dei registri non si verifica per la copia attiva del database delle cassette postali quando vengono sospese una o più copie passive. Se le attività di manutenzione pianificata richiedono un lungo periodo di tempo (ad esempio, diversi giorni), potrebbe verificarsi un notevole accumulo di file di registro. Per evitare che l'unità di registro si riempi di registri di transazioni, è possibile rimuovere la copia passiva del database interessata, invece di sospenderla. Una volta completata la manutenzione pianificata, è possibile aggiungere di nuovo la copia passiva del database.

In Exchange 2013 Service Pack 1 (SP1) viene introdotta una nuova funzionalità denominata *troncamento espanso*, disabilitata per impostazione predefinita. Durante le operazioni comuni, tutte le copie del database conservano i registri da inviare ad altre copie del database, finché tutte le copie di un database confermano di aver eseguito di nuovo (copie passive) o di aver ricevuto (copie ritardate) i file di registro. Si tratta del comportamento di troncamento dei registri predefinito. Se la copia di un database passa in modalità non in linea, i file di registro iniziano ad accumulare sui dischi utilizzati dalle altre copie del database. Se la copia del database interessata resta in modalità non in linea per un lungo periodo, è possibile che le altre copie del database esauriscano lo spazio sul disco disponibile.

Quando è attivato il troncamento espanso, il comportamento di troncamento è diverso. Ogni copia del database tiene traccia dello spazio libero sul disco e applica il comportamento di troncamento espanso se lo spazio è insufficiente. Per la copia attiva, lo straggler meno recente (la copia del database passiva meno recente nella riesecuzione del registro) viene ignorato e il troncamento rispetta le rimanenti copie passive meno recenti. La copia del database attiva è dove viene calcolato il troncamento globale. Le copie passive tenteranno di rispettare la decisione di troncamento presa nella copia attiva. Nonostante l'implicazione del nome MinCopiesToProtect, Exchange ignorerà solo lo straggler noto meno recente al momento in cui viene eseguito il troncamento. Se in una copia passiva lo spazio è insufficiente, i file di registro verranno troncati indipendentemente usando i parametri di configurazione descritti di seguito.

Quando il database non in linea passa alla modalità in linea, non saranno presenti i file dei registri eliminati dalle altre copie integre. Inoltre, lo stato della copia del database corrisponderà a FailedAndSuspended. In questo caso, se la funzione Autoreseed è configurata, per tutte le copie interessate verrà eseguito il reseeding in modo automatico. Se la funzione Autoreseed non è configurata, è necessario che un amministratore esegua il seeding manuale della copia del database.

I parametri relativi al numero necessario di copie integre, la soglia relativa allo spazio libero su disco e il numero di registri da conservare, sono configurabili. Per impostazione predefinita, la soglia di spazio libero su disco è pari a 204800 MB (200 GB) e il numero di registri da conservare è pari a 100.000 (100 GB) per le copie passive e 10.000 (10 GB) per le copie attive.

Se si abilita il troncamento espanso, la configurazione dei relativi parametri viene eseguita tramite modifica del Registro di sistema di Windows in ogni membro DAG. È possibile configurare 3 valori del Registro di sistema, memorizzati in HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\BackupInformation. Per impostazione predefinita, la chiave BackupInformation con i seguenti valori DWORD non esiste e deve essere creata manualmente. Nella tabella riportata di seguito, sono indicati i valori del Registro di sistema DWORD in BackupInformation:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Valore del Registro di sistema</th>
<th>Descrizione</th>
<th>Valore predefinito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LooseTruncation_MinCopiesToProtect</p></td>
<td><p>Questa chiave viene utilizzata per consentire il troncamento espanso. Rappresenta il numero di copie passive da proteggere dal troncamento espanso nella copia attiva di un database. L'impostazione del valore della chiave su 0 consente di disabilitare il troncamento espanso.</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p>LooseTruncation_MinDiskFreeSpaceThresholdInMB</p></td>
<td><p>La soglia relativa allo spazio libero su disco (in MB) per l'attivazione del troncamento espanso. Se lo spazio libero sul disco supera questo valore, viene attivato il troncamento espanso.</p></td>
<td><p>Se il valore del Registro di sistema non è configurato, il valore predefinito usato dal troncamento espanso è 200 GB.</p></td>
</tr>
<tr class="odd">
<td><p>LooseTruncation_MinLogsToProtect</p></td>
<td><p>Il numero minimo di file di registri da mantenere nelle copie integre per le quali si sta eseguendo il troncamento dei registri. Se il valore del Registro di sistema è configurato, il valore configurato viene applicato alle copie attive e passive.</p></td>
<td><p>Se il valore del Registro di sistema non è configurato, vengono usati i valori predefiniti di 100.000 per le copie di database passive e di 10.000 per le copie di database attive.</p></td>
</tr>
</tbody>
</table>


Quando si usa il valore del Registro di sistema LooseTruncation\_MinLogsToProtect registry, tenere presente che il comportamento è diverso per le copie del database attive e passive. Nella copia del database attiva, questo è il numero di file di registro in più che vengono conservati prima di quelli che vengono richiesti dalle copie passive protette e dall'intervallo richiesto della copia attiva. In una copia di database passiva, questo è il numero di registri conservati dal registro disponibile più recente. Un decimo di questo numero viene usato anche per conservare i registri prima dell'intervallo richiesto della copia passiva. I due limiti sono presenti per garantire che le copie di database ritardate non occupino troppo spazio, dal momento che il loro intervallo necessario è generalmente molto grande.

## Criterio di attivazione del database

Esistono scenari in cui si può creare un database delle cassette postali e impedire al sistema di attivare automaticamente quella copia nel caso si verifichi un errore; ad esempio:

  - Se si distribuiscono una o più copie del database delle cassette postali a un datacenter alternativo o a un datacenter in standby.

  - Se si configura una copia del database come copia ritardata per il ripristino.

  - Se si stanno eseguendo operazioni di manutenzione o di aggiornamento di un server.

In ciascuno degli scenari precedenti, esistono copie del database che il sistema non deve attivare automaticamente. Per impedire l'attivazione automatica di una copia del database delle cassette postali da parte del sistema, è possibile configurare la copia come bloccata (sospesa) per l'attivazione. In questo modo, il sistema può mantenere aggiornato il database tramite la distribuzione e la riesecuzione dei file di registro, ma non può attivare automaticamente e utilizzare la copia. Le copie bloccate per l'attivazione devono essere attivate manualmente da un amministratore. È possibile configurare il criterio di attivazione del database per l'intero server utilizzando il cmdlet [Set-MailboxServer](https://technet.microsoft.com/it-it/library/aa998651\(v=exchg.150\)) o una copia di un database individuale utilizzando il cmdlet [Set-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd298104\(v=exchg.150\)) per impostare il parametro *DatabaseCopyAutoActivationPolicy* su Blocked.

Per ulteriori informazioni sulla configurazione del criterio di attivazione del database, vedere [Configurare i criteri di attivazione per una copia del database delle cassette postali](configure-activation-policy-for-a-mailbox-database-copy-exchange-2013-help.md).

## Effetto degli spostamenti della cassetta postale sulla replica continua

In un database delle cassette postali molto occupato con una alta frequenza di generazione di registri, esiste una grande probabilità di perdita di dati se le repliche nelle copie del database passivo non sono allineate alla generazione dei registri. Uno scenario che può provocare una alta frequenza di generazione di registri è lo spostamento delle cassette postali. Exchange 2013 include un servizio API di garanzia dei dati utilizzato da servizi quali il servizio di replica delle cassette postali di Microsoft Exchange (MRS) per controllare l'integrità dell'architettura della copia del database basato sul valore del parametro *DataMoveReplicationConstraint* impostato dal sistema o da un amministratore. In particolare, il servizio API di garanzia dei dati può essere utilizzato per:

  - **Controllo integrità replica**   Conferma che sia disponibile il numero prerequisito di copie del database.

  - **Controllo scaricamento replica**   Conferma che i file di registro richiesti sono stati duplicati per il numero prerequisito di copie del database.

Quando viene eseguito, il servizio API restituisce all'applicazione chiamante le seguenti informazioni di stato:

  - **Retry**   Significa che si è verificato un errore temporaneo che impedisce di controllare una condizione sul database.

  - **Satisfied**   Significa che il database soddisfa le condizioni richieste o che il database non è stato replicato.

  - **NotSatisfied**   Significa che il database non soddisfa le condizioni richieste. Inoltre, all'applicazione chiamante viene fornita l'informazione relativa al motivo per cui è stata fornita la risposta **NotSatisfied**.

Il valore del parametro *DataMoveReplicationConstraint* per il database delle cassette postali determina quante copie si dovrebbero valutare come parte della richiesta. I valori consentiti per il parametro *DataMoveReplicationConstraint* sono i seguenti:

  - `None`   Quando si crea un database delle cassette postali questo valore viene assegnato per impostazione predefinita. Quando è impostato questo valore, le condizioni del servizio API di garanzia dei dati vengono ignorate. Questa impostazione deve essere utilizzata solo per i database delle cassette postali che non sono replicati.

  - `SecondCopy`   Questo è il valore predefinito quando si aggiunge la seconda copia di un database di cassette postali. Quando è impostato questo valore, almeno una copia passiva del database deve soddisfare le condizioni del servizio API di garanzia dei dati.

  - `SecondDatacenter`   Quando è impostato questo valore, almeno una copia passiva del database in un altro sito Active Directory deve soddisfare le condizioni del servizio API di garanzia dei dati.

  - `AllDatacenters`   Quando è impostato questo valore, almeno una copia passiva del database in ciascun sito Active Directory deve soddisfare le condizioni del servizio API di garanzia dei dati.

  - `AllCopies`   Quando è impostato questo valore, tutte le copie passive del database devono soddisfare le condizioni del servizio API di garanzia dei dati.

**Controllo integrità replica**

Quando viene eseguito il servizio API di garanzia dei dati per valutare l'integrità dell'infrastruttura della copia del database, vengono valutati vari elementi.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Se il parametro <em>DataMoveReplicationConstraint</em> è impostato su…</th>
<th>Quindi, per un determinato database…</th>
<th>Condizioni</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SecondCopy</code></p></td>
<td><p>Almeno una copia passiva di un database replicato deve soddisfare le condizioni nella prossima colonna.</p></td>
<td><p>La copia passiva del database deve:</p>
<ul>
<li><p>Essere integra.</p></li>
<li><p>Avere una coda di riesecuzione entro 10 minuti dell'intervallo di riesecuzione.</p></li>
<li><p>Avere una lunghezza della coda di copia inferiore a 10 registri.</p></li>
<li><p>Avere una lunghezza media della coda di copia inferiore a 10 registri. La lunghezza media della coda di copia viene calcolata sulla base del numero di volte che l'applicazione ha interrogato lo stato del database.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SecondDatacenter</code></p></td>
<td><p>Almeno una copia passiva di un database replicato in un altro sito Active Directory deve soddisfare le condizioni nella prossima colonna.</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>AllDatacenters</code></p></td>
<td><p>La copia attiva deve essere montata e una copia passiva in ciascun sito Active Directory deve soddisfare le condizioni nella prossima colonna.</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>AllCopies</code></p></td>
<td><p>La copia attiva deve essere montata e tutte le copie passive del database devono soddisfare le condizioni nella prossima colonna.</p></td>
<td></td>
</tr>
</tbody>
</table>


**Controllo scaricamento replica**

Il servizio API di garanzia dei dati può essere utilizzato per convalidare che un numero prerequisito di copie del database hanno replicato i registri delle transazioni richiesti. Questo viene verificato confrontando il timestamp dell'ultimo registro replicato con il commit timestamp del servizio chiamante (in molti casi questo è il timestamp dell'ultimo file di registro che contiene i dati richiesti) più cinque secondi aggiuntivi (per compensare le differenze tra gli orari di sistema). Se il timestamp di riproduzione è superiore al commit timestamp, il parametro *DataMoveReplicationConstraint* è soddisfatto. Se il timestamp di riproduzione è inferiore al commit timestamp, il parametro *DataMoveReplicationConstraint* non è soddisfatto.

Prima di spostare un grande numero di cassette postali verso e da database di replica in un gruppo di disponibilità del database (DAG) si raccomando di configurare il parametro *DataMoveReplicationConstraint* su ciascun database delle cassette postali in accordo a quanto segue:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Se si sta distribuendo…</th>
<th>Impostare DataMoveReplicationConstraint su...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Database delle cassette postali che non hanno alcuna delle copie del database</p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p>Un gruppo di disponibilità del database (DAG) all'interno di un singolo sito di Active Directory</p></td>
<td><p><code>SecondCopy</code></p></td>
</tr>
<tr class="odd">
<td><p>Un gruppo di disponibilità del database (DAG) in più datacenter utilizzando un sito di Active Directory esteso</p></td>
<td><p><code>SecondCopy</code></p></td>
</tr>
<tr class="even">
<td><p>Un gruppo di disponibilità del database (DAG) che si espande su due siti Active Directory, e si avranno molte copie del database disponibili in ciascun sito</p></td>
<td><p><code>SecondDatacenter</code></p></td>
</tr>
<tr class="odd">
<td><p>Un gruppo di disponibilità del database che si espande su due siti Active Directory e si avranno solo copie del database ritardate sul sito SecondCopy</p></td>
<td><p><code>SecondCopy</code></p>
<p>Questo è dovuto al fatto che il servizio API di garanzia dei dati non garantisce che i dati vengano impegnati fino a che il file di registro sia replicato nella copia del database e a causa della natura della copia del database che deve essere ritardata questo vincolo non consentirà lo spostamento richiesto, a meno che il valore di ReplayLagTime della copia ritardata del database sia inferiore a 30 minuti.</p></td>
</tr>
<tr class="even">
<td><p>Un gruppo di disponibilità del database (DAG) che si estende su tre o più siti Active Directory e ciascun sito conterrà un elevato numero di copie del database disponibili</p></td>
<td><p><code>AllDatacenters</code></p></td>
</tr>
</tbody>
</table>


## Bilanciamento delle copie del database

A causa della natura intrinseca dei gruppi DAG, come conseguenza dei switchover e dei failover del database, le copie attive del database delle cassette postali modificheranno gli host più volte durante il ciclo di vita di un gruppo DAG. Di conseguenza, i gruppi DAG possono diventare non bilanciati in termini di distribuzione delle copie attive del database delle cassette postali. Nella tabella seguente viene illustrato un esempio di un gruppo DAG che dispone di quattro database con quattro copie di ogni database (per un totale di 16 database su ogni server) con una distribuzione non uniforme delle copie attive del database.

### Gruppo DAG con una distribuzione non bilanciata delle copie attive

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Server</th>
<th>Numero di database attivi</th>
<th>Numero di database passivi</th>
<th>Numero di database installati</th>
<th>Numero di database disinstallati</th>
<th>Elenco conteggio delle preferenze</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1</p></td>
<td><p>5</p></td>
<td><p>11</p></td>
<td><p>5</p></td>
<td><p>0</p></td>
<td><p>4, 4, 3, 5</p></td>
</tr>
<tr class="even">
<td><p>EX2</p></td>
<td><p>1</p></td>
<td><p>15</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>1, 8, 6, 1</p></td>
</tr>
<tr class="odd">
<td><p>EX3</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>0</p></td>
<td><p>13, 2, 1, 0</p></td>
</tr>
<tr class="even">
<td><p>EX4</p></td>
<td><p>1</p></td>
<td><p>15</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>1, 1, 5, 9</p></td>
</tr>
</tbody>
</table>


Nell'esempio precedente, esistono quattro copie di ogni database, quindi solo quattro valori possibili per la preferenza di attivazione (1, 2, 3 o 4). Nella colonna **Elenco conteggio delle preferenze** viene visualizzato il conteggio del numero di database con ogni valore. Ad esempio, in EX3 esistono 13 copie del database con la preferenza di attivazione 1, due copie con la preferenza di attivazione 2, una copia con la preferenza di attivazione 3 e nessuna copia con la preferenza di attivazione 4.

Come si può vedere, questo gruppo di disponibilità del database non è bilanciato in termini di numero dei database attivi e passivi ospitati da ogni membro del gruppo di disponibilità del database o in termini di conteggio delle preferenze di attivazione dei database ospitati.

È possibile utilizzare lo script RedistributeActiveDatabases.ps1 per bilanciare le copie del database delle cassette postali attivo attraverso il gruppo di disponibilità del database (DAG). Questo script sposta i database tra le copie per cercare di avere un numero uguale di database installati su ogni server del gruppo DAG. Se necessario, lo script tenta di bilanciare anche i database attivi tra i siti.

Lo script fornisce due opzioni per il bilanciamento delle copie attive del database all'interno di un gruppo DAG:

  - **BalanceDbsByActivationPreference**   Quando questa opzione viene specificata, lo script tenta di spostare i database nella copia preferita (in base alla preferenza di attivazione) indipendentemente dal sito di Active Directory.

  - **BalanceDbsByActivationPreference**   Quando questa opzione viene specificata, lo script tenta di spostare i database attivi nella copia preferita, mentre tenta di bilanciare anche i database attivi all'interno di ogni sito di Active Directory.

Dopo l'esecuzione dello script con la prima opzione, il precedente gruppo DAG non bilanciato diventa bilanciato, come mostrato nella tabella seguente.

### Gruppo DAG con una distribuzione bilanciata delle copie attive

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Server</th>
<th>Numero di database attivi</th>
<th>Numero di database passivi</th>
<th>Numero di database installati</th>
<th>Numero di database disinstallati</th>
<th>Elenco conteggio delle preferenze</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="even">
<td><p>EX2</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="odd">
<td><p>EX3</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="even">
<td><p>EX4</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
</tbody>
</table>


Come mostrato nella tabella precedente, il gruppo DAG è ora bilanciato in termini di numero dei database attivi e passivi su ogni server e di preferenza di attivazione tra i server.

La seguente tabella elenca i parametri disponibili per lo script RedistributeActiveDatabases.ps1.

### Parametri dello script RedistributeActiveDatabases.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>Specifica il nome del gruppo DAG che si desidera bilanciare di nuovo. Se questo parametro viene omesso, viene utilizzato il gruppo DAG di cui è membro il server locale.</p></td>
</tr>
<tr class="even">
<td><p><em>BalanceDbsByActivationPreference</em></p></td>
<td><p>Specifica che lo script deve spostare i database nella copia preferita indipendentemente dal sito di Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><em>BalanceDbsBySiteAndActivationPreference</em></p></td>
<td><p>Specifica che lo script deve tentare di spostare i database attivi nella copia preferita, mentre tenta di bilanciare anche i database attivi all'interno di ogni sito di Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowFinalDatabaseDistribution</em></p></td>
<td><p>Specifica la visualizzazione di un rapporto sulla distribuzione corrente del database dopo il completamento della ridistribuzione.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowedDeviationFromMeanPercentage</em></p></td>
<td><p>Specifica la variante consentita dei database attivi tra i siti, espressa in percentuale. L'impostazione predefinita è 20%. Ad esempio, se esistevano 99 database distribuiti tra tre siti, la distribuzione ideale era di 33 database in ogni sito. Se la discrepanza consentita è del 20%, lo script tenta di bilanciare i database in modo che ogni sito non abbia più del 10% in più o in meno del numero. Il 10% di 33 è 3,3, arrotondato a 4. Pertanto, lo script tenta di disporre di 29-37 database in ogni sito.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowDatabaseCurrentActives</em></p></td>
<td><p>Specifica che lo script produce un rapporto per ogni database che descrive lo spostamento del database e se ora è attivo sulla copia preferita.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowDatabaseDistributionByServer</em></p></td>
<td><p>Specifica che lo script produce un rapporto per ogni server che mostra la distribuzione di database.</p></td>
</tr>
<tr class="even">
<td><p><em>RunOnlyOnPAM</em></p></td>
<td><p>Specifica che lo script viene eseguito solo sul membro DAG che attualmente dispone del ruolo PAM. Lo script verifica l'esecuzione dal ruolo PAM. Se non viene eseguito dal ruolo PAM, lo script viene chiuso.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogEvents</em></p></td>
<td><p>Specifica che lo script registra un evento (evento MsExchangeRepl 4115) contenente un riepilogo delle azioni.</p></td>
</tr>
<tr class="even">
<td><p><em>IncludeNonReplicatedDatabases</em></p></td>
<td><p>Specifica che lo script deve comprendere i database non replicati (database senza copie) nel determinare come ridistribuire i database attivi. Anche se i database non replicati non possono essere spostati, possono influenzare la distribuzione dei database replicati.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>L'opzione Confirm può essere utilizzata per sopprimere il prompt di conferma visualizzato per impostazione predefinita quando viene eseguito questo script. Per sopprimere il prompt di conferma, utilizzare la sintassi -Confirm:$False. È necessario includere i due punti ( : ) nella sintassi.</p></td>
</tr>
</tbody>
</table>


## Esempi di RedistributeActiveDatabases.ps1

In questo esempio, viene mostrata la distribuzione corrente del database per un gruppo DAG, compreso l'elenco conteggio delle preferenze.

```powershell
RedistributeActiveDatabases.ps1 -DagName DAG1 -ShowDatabaseDistributionByServer | Format-Table
```

In questo esempio, le copie attive del database delle cassette postali in un gruppo DAG vengono ridistribuite e bilanciate utilizzando la preferenza di attivazione senza chiedere conferma.

```powershell
RedistributeActiveDatabases.ps1 -DagName DAG1 -BalanceDbsByActivationPreference -Confirm:$False
```

In questo esempio, le copie attive del database delle cassette postali in un gruppo DAG vengono ridistribuite e bilanciate utilizzando la preferenza di attivazione e viene prodotto un riepilogo della distribuzione.
```powershell
    RedistributeActiveDatabases.ps1 -DagName DAG1 -BalanceDbsByActivationPreference -ShowFinalDatabaseDistribution
```

## Monitoraggio delle copie del database

Una copia del database costituisce la prima difesa contro gli errori che si verificano nella copia attiva del database. Comunque, è molto importante monitorare l'integrità e lo stato delle copie del database per assicurarne la disponibilità quando necessario. È possibile vedere una grande varietà di informazioni, incluso la lunghezza della coda di copia, lunghezza della coda di replica, informazioni di stato e stato dell'indice dei contenuti esaminando i dettagli di una copia del database nell'interfaccia di amministrazione di Exchange. È possibile utilizzare anche il cmdlet **Get-MailboxDatabaseCopyStatus** in Shell per visualizzare una serie di informazioni sullo stato di una copia del database.

Per ulteriori informazioni sul monitoraggio delle copie del database, vedere [Gruppi di disponibilità del database di monitoraggio](monitoring-database-availability-groups-exchange-2013-help.md).

## Eliminazione di una copia del database

Una copia del database può essere rimossa in qualunque momento utilizzando l'interfaccia di amministrazione di Exchange o il cmdlet **Remove-MailboxDatabaseCopy** in Shell. Una volta rimossa una copia del database, è necessario eliminare manualmente tutti i file di registro del database e delle transazioni dal server da cui viene rimossa la copia del database. Per la procedura dettagliata su come eseguire il seeding di una copia di database, vedere [Rimuovere una copia del database delle cassette postali](remove-a-mailbox-database-copy-exchange-2013-help.md).

## Switchover del database

Il server Cassette postali che ospita la copia attiva di un database viene denominato master del database delle cassette postali. Il processo di attivazione di una copia passiva del database modifica il master per il database delle cassette postali e converte la copia passiva nella nuova copia attiva. Questo processo viene denominato switchover del database. In uno switchover del database, la copia attiva di un database viene disinstallata da un server Cassette postali e una copia passiva di quel database viene installata come nuova copia attiva del database delle cassette postali su un altro server Cassette postali. Quando si esegue uno switchover, è possibile sostituire l'impostazione dial di installazione del database per il nuovo master del database delle cassette postali.

È possibile individuare rapidamente quale server Cassette postali è il master del database delle cassette postali corrente consultando la colonna a destra nella scheda **Copie database** nell'interfaccia di amministrazione di Exchange. È possibile eseguire uno switchover utilizzando il collegamento **Activate** nell'interfaccia di amministrazione di Exchange o utilizzando il cmdlet **Move-ActiveMailboxDatabase** in Shell.

Esistono molti controlli interni che verranno eseguiti prima di attivare una copia passiva:

  - Viene controllato lo stato della copia del database. Se la copia del database ha lo stato non riuscito, lo switchover viene bloccato. È possibile modificare questo comportamento e non eseguire il controllo di integrità utilizzando il parametro *SkipHealthChecks* del cmdlet **Move-ActiveMailboxDatabase**. Questo parametro consente di spostare la copia attiva in una copia del database con lo stato non riuscito.

  - La copia attiva del database viene controllata per vedere se questa rappresenta attualmente l'origine di un seeding per qualsiasi copia passiva del database. Se la copia attiva è attualmente utilizzata come origine del seeding, lo switchover viene bloccato. È possibile modificare questo comportamento e non eseguire il controllo di origine seeding utilizzando il parametro *SkipActiveCopyChecks* del cmdlet **Move-ActiveMailboxDatabase**. Questo parametro consente di spostare una copia attiva mentre viene usata come origine di un seeding. Utilizzando questo parametro l'operazione di seeding verrà cancellata e considerata non riuscita.

  - Viene controllata la lunghezza della coda di copia e la lunghezza della coda di riesecuzione per la copia del database per assicurarsi che i valori rientrino nei criteri configurati. Inoltre, la copia del database viene controllata per assicurarsi che non sia attualmente in uso come origine per il seeding. Se i valori di lunghezza delle code non rientrano nei criteri configurati o se il database è attualmente utilizzato come origine per il seeding, lo switchover viene bloccato. È possibile ignorare questo comportamento e non eseguire questi controlli utilizzando il parametro *SkipLagChecks* del cmdlet **Move-ActiveMailboxDatabase**. Questo parametro consente l'attivazione di una copia con code di copia e di riesecuzione che non rientrano nei criteri configurati.

  - Viene controllato lo stato del catalogo di ricerca (indice dei contenuti) per la copia del database. Se il catalogo di ricerca non è aggiornato, non è integro o è danneggiato, lo switchover viene bloccato. È possibile ignorare questo comportamento e non eseguire il controllo del catalogo di ricerca utilizzando il parametro *SkipClientExperienceChecks* del cmdlet **Move-ActiveMailboxDatabase**. Questo parametro fa sì che questo tipo di ricerca ignori il controllo di integrità del catalogo. Se il catalogo di ricerca per la copia del database che si sta attivando non è integro o non è utilizzabile e viene utilizzato questo parametro per ignorare il controllo di integrità del catalogo e viene attivata la copia del database, sarà necessario sottoporre di nuovo il catalogo a indicizzazione o seeding.

Quando si esegue uno switchover del database, è possibile anche sostituire le impostazioni dial di installazione configurate per il server che ospita la copia passiva del database attivato. L'utilizzando del parametro *MountDialOverride* del cmdlet **Move-ActiveMailboxDatabase** indica al server di destinazione di ignorare le impostazioni dial di installazione e di utilizzare quelle specificate dal parametro *MountDialOverride*.

Per la procedura dettagliata relativa all'esecuzione dello switchover di una copia del database, vedere [Attivare una copia del database delle cassette postali](activate-a-mailbox-database-copy-exchange-2013-help.md).


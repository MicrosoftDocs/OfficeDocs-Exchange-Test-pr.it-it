---
title: 'Diagnostica dei problemi di ricerca di Exchange: Exchange 2013 Help'
TOCTitle: Diagnostica dei problemi di ricerca di Exchange
ms:assetid: 8cfa26f4-ccf0-42dd-8570-67018188b4e8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123701(v=EXCHG.150)
ms:contentKeyID: 52063124
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Diagnostica dei problemi di ricerca di Exchange

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Exchange Ricerca indicizza cassette postali e gli allegati è supportato nelle cassette postali Exchange. Con l'aumento volumi di posta elettronica, l'aumento delle dimensioni della cassetta postale e le quote di archiviazione, il provisioning di cassette postali di archiviazione per gli utenti e In-Place eDiscovery per l'esecuzione di ricerche di individuazione, Exchange ricerca è essenziale dei server cassette postali nell'organizzazione Microsoft Exchange Server 2013. Problemi con Exchange ricerca possono influire sulla produttività degli utenti e influire sulle funzionalità eDiscovery sul posto.

Per ulteriori informazioni sulla funzionalità Ricerca di Exchange, vedere [Ricerca di Exchange](exchange-search-exchange-2013-help.md).

Per informazioni sulle altre attività relative alla gestione di Ricerche di Exchange, vedere [Exchange Search procedures](exchange-search-procedures-exchange-2013-help.md).

## Utilizzo del cmdlet Test-ExchangeSearch

Il passo 5 della procedura in questo argomento descrive l'esecuzione del cmdlet **Test-ExchangeSearch** nella diagnostica dei problemi nella funzionalità Ricerca di Exchange. È possibile usare il cmdlet **Test-ExchangeSearch** per verificare la funzionalità Ricerca di Exchange su un server Cassette postali, un database di cassette postali o una specifica cassetta postale. Il cmdlet invia un messaggio di prova alla cassetta postale specificata (o a un database di cassette postali, se non ne è stata specificata alcuna cassetta), poi esegue una ricerca per stabilire se quel messaggio è stato indicizzato, incluso il tempo necessario per l'indicizzazione. In condizioni normali, Ricerca di Exchange indicizza un messaggio al massimo 10 secondi dopo che questo è stato creato o spedito alla cassetta postale. Il messaggio di prova viene eliminato automaticamente dopo il test.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Test-ExchangeSearch](https://technet.microsoft.com/it-it/library/bb124733\(v=exchg.150\)).

## Recupero di elementi non ricercabili

È possibile utilizzare il cmdlet [Get-FailedContentIndexDocuments](https://technet.microsoft.com/it-it/library/dd351154\(v=exchg.150\)) per recuperare un elenco di elementi non ricercabili delle cassette postali che non è possibile indicizzare correttamente dal Exchange ricerca. È possibile eseguire il cmdlet in un server cassette postali, un database delle cassette postali o una cassetta postale specifica. Il cmdlet restituisce informazioni dettagliate su ogni elemento che non viene eseguita la ricerca. Sono diversi i motivi per cui non è possibile cercare un elemento della cassetta postale; ad esempio, un messaggio di posta elettronica può contenere un tipo di file degli allegati che non può essere indicizzato per la ricerca o perché un filtro di ricerca non è installato o è disabilitato. Se un filtro di ricerca per il tipo file è disponibile, è possibile installare sui server Exchange.


> [!IMPORTANT]
> I filtri di ricerca forniti da Microsoft sono testati e supportati da Microsoft. Si consiglia di provare qualsiasi filtro di ricerca di terze parti in un ambiente di prova prima di installarlo sui server Exchange in ambiente di produzione.



Per ulteriori informazioni sugli elementi non ricercabili, vedere:

  - [Formati di file indicizzati da ricerca di Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [Elementi non ricercabili in Exchange eDiscovery](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

## Diagnostica dei problemi di ricerca di Exchange

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ricerca di Exchange" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

1.  **Verificare lo stato del servizio**   Sul server Cassette postali è stato avviato il servizio di Ricerca di Microsoft Exchange (MSExchangeFastSearch)? Se sì, andare al passo 2. Altrimenti, utilizzare lo snap-in MMC Servizi per verificare se il servizio MSExchangeFastSearch è in esecuzione:
    
    1.  Fare clic su **Start**, scegliere **Strumenti di amministrazione**, quindi selezionare **Servizi**.
    
    2.  In **Servizi**, verificare che lo **Stato** del servizio **Ricerca di Microsoft Exchange** risulti **Avviato**.

2.  **Controllare la configurazione del database di cassette postali**   Il parametro *IndexEnabled* è impostato su true per il database di cassette postali dell'utente? Se sì, andare al passo 3. Altrimenti, verificare che il flag *IndexEnabled* sia impostato su True utilizzando il seguente comando in Shell.
    
        Get-MailboxDatabase | Format-Table Name,IndexEnabled
    
    Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Get-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb124924\(v=exchg.150\)).

3.  **Verificare lo stato della ricerca per indicizzazione del database di cassette postali**   Nel database Exchange è stata eseguita una ricerca per indicizzazione? Se sì, andare al passaggio 4. In caso contrario, utilizzare Monitoraggio affidabilità e prestazioni per verificare il **crawler: cassette postali rimanenti** contatore dell'oggetto prestazioni **Indicizzatore di ricerca di MSExchange**. Fare quanto segue:
    
    1.  Aprire **Performance Monitor** (perfmon.exe).
    
    2.  Nell'albero della console in **Strumenti di monitoraggio**, fare clic su **Performance Monitor**.
    
    3.  Nel riquadro di Performance Monitor, fare clic su **Aggiungi** (segno più verde).
    
    4.  In **Aggiungi contatori**, nell'elenco **Seleziona contatori dal computer**, selezionare il server sul quale è presente il database che si vuole controllare.
    
    5.  Nella casella priva di etichetta nell'elenco **Seleziona contatori dal computer**, selezionare l'oggetto prestazioni **Indicizzatore di ricerca di MSExchange**.
    
    6.  Nella casella **Istanze di oggetti selezionati**, selezionare l'istanza del database delle cassette postali dell'utente.
    
    7.  Scegliere **Aggiungi**, quindi **OK**.
        
        Nel riquadro Performance Monitor, l'oggetto prestazioni **Indicizzatore di ricerca di MSExchange** compare nella colonna **Oggetto** e i suoi contatori sono elencati nella colonna **Contatore**.
    
    8.  Visualizza il **crawler: Contatore** cassette postali rimanenti. Ogni valore di 1 o superiore indica che nelle cassette postali nel database è ancora in esecuzione la ricerca per indicizzazione. Una volta completata la ricerca per indicizzazione, il valore sarà **0**.
    
    Per informazioni sull'utilizzo di Performance Monitor, vedere [delle prestazioni e affidabilità Monitoring Guida introduttiva Guida di Windows Server 2008](https://go.microsoft.com/fwlink/p/?linkid=178005)

4.  **Controllare l'integrità dell'indicizzazione della copia del database**   L'indice di contenuto è integro? Usare il cmdlet **Get-MailboxDatabaseCopyStatus** per controllare l'integrità dell'indicizzazione del contenuto per una copia del database.
    
        Get-MailboxDatabaseCopyStatus -Server $env:ComputerName | Format-Table Name,Status,ContentIndex* -Auto
    
    Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/it-it/library/dd298044\(v=exchg.150\)).

5.  **Eseguire il cmdlet Test-ExchangeSearch**   Se è già stata eseguita la ricerca per indicizzazione del database delle cassette postali è possibile eseguire il cmdlet **Test-ExchangeSearch** per l'intero database o per una specifica cassetta posatale.
    
        Test-ExchangeSearch -Identity AlanBrewer@contoso.com
    
    Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Test-ExchangeSearch](https://technet.microsoft.com/it-it/library/bb124733\(v=exchg.150\)).

6.  **Controllare il registro eventi di applicazione**   Utilizzando il Visualizzatore eventi o la Shell, controllare il registro eventi di applicazione per i messaggi di errore relativi alla ricerca. Controllare i seguenti origini eventi.
    
      - **MSExchangeFastSearch**
    
      - **MSExchangeIS**
    
    Per ulteriori informazioni, seguire il collegamento nella voce del registro eventi.

7.  **Riavviare il servizio Ricerca di Microsoft Exchange**   Usare lo snap-in Servizi MMC o Shell per arrestare e quindi riavviare il servizio Ricerca di MicrosoftExchange (MSExchangeFastSearch):
    
    1.  Fare clic su **Start**, scegliere **Strumenti di amministrazione**, quindi selezionare **Servizi**.
    
    2.  Nel riquadro **Servizi**, fare clic con il pulsante destro del mouse su **Ricerca di Microsoft Exchange**, quindi fare clic su **Arresta**. Dopo aver interrotto il servizio, fare nuovamente clic con il pulsante destro del mouse sul servizio e quindi scegliere **Avvia**.

8.  **Eseguire il reseeding del catalogo di ricerca**   In alcuni casi (ad esempio, se il catalogo di ricerca è danneggiato) può essere necessario eseguire il reseeding del catalogo stesso. Quando è necessario effettuare una operazione di reseeding di un catalogo di ricerca, il servizio di ricerca di Exchange lo notifica registrando delle voci nel registro eventi dell'applicazione. Per ulteriori informazioni sul reseeding del catalogo di ricerca, vedere [Reseeding del catalogo di ricerca](reseed-the-search-catalog-exchange-2013-help.md).


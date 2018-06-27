---
title: 'Filtro contenuto: Exchange 2013 Help'
TOCTitle: Filtro contenuto
ms:assetid: d660ffbf-de05-46c2-940b-5200eca94e0a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124739(v=EXCHG.150)
ms:contentKeyID: 50481781
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtro contenuto

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_


> [!NOTE]
> Dal 1° novembre 2016, Microsoft ha interrotto gli aggiornamenti delle definizioni spam per i filtri SmartScreen in Exchange e Outlook. Le definizioni spam SmartScreen esistenti non verranno eliminate, ma la loro efficacia si ridurrà progressivamente. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange (Eliminazione del supporto per SmartScreen in Outlook ed Exchange)</A>.



L'agente filtro contenuti restituisce i messaggi di posta elettronica in ingresso e valuta la probabilità che un messaggio in ingresso è valido o la posta indesiderata. A differenza di molte altre tecnologie di filtro, l'agente filtro contenuto utilizza le caratteristiche di un campione significativo forma statistica di messaggi di posta elettronica. L'inclusione dei messaggi legittimi in questo esempio consente di ridurre le possibilità di errori. Dal momento che l'agente filtro contenuti riconosce le caratteristiche della posta indesiderata e messaggi legittimi, viene aumentata la precisione. Sono disponibili periodicamente tramite [Microsoft Update](https://go.microsoft.com/fwlink/p/?linkid=54836)aggiornamenti per l'agente filtro contenuto.

**Sommario**

Using the Content Filter agent

Configuring the Content Filter agent

## Utilizzo dell'agente filtro contenuto

L'agente filtro contenuto è uno dei molti agenti di protezione dalla posta indesiderata di Exchange. Quando vengono configurati su un server Exchange, gli agenti di protezione dalla posta indesiderata agiscono sui messaggi in modo cumulativo per ridurre il numero di messaggi indesiderati ricevuti dall'organizzazione. Per ulteriori informazioni su come pianificare e distribuire gli agenti di protezione dalla posta indesiderata, vedere [Protezione anti-spam](anti-spam-protection-exchange-2013-help.md).

L'agente filtro contenuto assegna un livello di probabilità di posta indesiderata (SCL) a ciascun messaggio. La valutazione del livello di probabilità di posta indesiderata è un numero compreso tra 0 e 9. Un valore alto indica una maggiore probabilità che il messaggio sia indesiderato.

È possibile configurare l'agente filtro contenuto in modo che intraprenda le seguenti azioni sui messaggi in base al livello SCL:

  - Elimina messaggio

  - Rifiuta messaggio

  - Metti in quarantena messaggio

Ad esempio, è possibile stabilire che i messaggi il cui livello SCL è 7 o superiore devono essere eliminati, i messaggi il cui livello SCL è 6 devono essere rifiutati e i messaggi il cui livello SCL è 5 devono essere messi in quarantena.

È possibile regolare il comportamento della soglia SCL assegnando diversi livelli SCL a ciascuna di queste azioni. Per ulteriori informazioni sulla regolazione della soglia SCL per soddisfare le esigenze dell'organizzazione e sulle soglie SCL per ciascun destinatario, vedere [Soglia del livello di probabilità di posta indesiderata](spam-confidence-level-threshold-exchange-2013-help.md).


> [!NOTE]
> I messaggi con dimensione superiore a 11 MB non vengono analizzati da Filtro messaggi intelligente. Vengono infatti filtrati dal filtro contenuto senza alcuna scansione.



## Espressioni consentite ed espressioni non consentite

È possibile personalizzare il modo in cui l'agente filtro contenuto assegna il livello di probabilità di posta indesiderata configurando parole personalizzate. Le parole personalizzate sono singole parole o frasi che l'agente filtro contenuto utilizza per applicare l'elaborazione del filtro appropriata. Le parole o le frasi approvate vengono configurate come espressioni consentite, mentre le parole o le frasi non approvate vengono configurate come espressioni non consentite. Quando l'agente filtro contenuto rileva un'espressione consentita preconfigurata in un messaggio in arrivo, l'agente filtro contenuto assegna automaticamente un livello 0 di probabilità di posta indesiderata al messaggio. In alternativa, quando viene individuata un'espressione non consentita configurata in un messaggio in arrivo, l'agente filtro contenuto assegna un livello 9 di probabilità di posta indesiderata.

È possibile immettere parole o frasi personalizzate con qualsiasi combinazione di lettere maiuscole e minuscole. Tuttavia, quando valuta il contenuto del messaggio, l'agente filtro contenuto ignora le maiuscole e le minuscole. Il numero massimo di parole o frasi personalizzate che è possibile creare è 800.

## Convalida del timbro posta elettronica Outlook

L'agente filtro contenuto include anche la convalida del Timbro posta elettronica Outlook, una prova di calcolo che Outlook applica ai messaggi in uscita per consentire ai sistemi di messaggistica dei destinatari di distinguere i messaggi di posta elettronica legittimi dalla posta indesiderata. Questa funzionalità consente di ridurre la probabilità di falsi positivi. Nell'ambito dei filtri di protezione dalla posta indesiderata, un *falso positivo* esiste quando un filtro di protezione dalla posta indesiderata identifica erroneamente un messaggio proveniente da un mittente legittimo come posta indesiderata. Quando la convalida Timbro posta elettronica Outlook è abilitata, l'agente Filtro contenuto analizza il messaggio in arrivo alla ricerca di un'intestazione di timbro elettronico di calcolo. La presenza di un'intestazione del timbro di calcolo valida e risolta nel messaggio indica che il computer client che ha generato il messaggio ha risolto il timbro di calcolo.

I computer non richiedono un tempo di elaborazione significativo per risolvere i singoli timbri di calcolo. Tuttavia, l'elaborazione dei timbri in molti messaggi può risultare proibitiva per un mittente malintenzionato. È improbabile che chiunque invii milioni di messaggi di posta indesiderata sia disposto a investire nella capacità di elaborazione necessaria a risolvere i timbri di calcolo per tutti i messaggi di posta indesiderata in uscita. Se la posta elettronica di un mittente contiene un timbro di calcolo valido e risolto, è improbabile che si tratti di un mittente malintenzionato. In questo caso, l'agente filtro contenuto ridurrà il livello di probabilità di posta indesiderata. Se la funzionalità di convalida del timbro è abilitata e il messaggio in arrivo non contiene un'intestazione del timbro di calcolo o se tale intestazione non è valida, l'agente filtro contenuto non modificherà il livello SCL.

## Esclusione del destinatario, del mittente e del dominio del mittente

In alcune organizzazioni, è necessario accettare interamente la posta elettronica inviata a determinati alias. Questo scenario può causare dei problemi se l'organizzazione è una società che gestisce volumi significativi di posta indesiderata.

Ad esempio, una società denominata Woodgrove Bank ha un alias denominato customerloans@woodgrovebank.com che fornisce supporto basato sulla posta elettronica ai clienti esterni. Gli amministratori di Exchange configurano l'agente filtro contenuto per l'impostazione delle espressioni non consentite che escludono dal filtro parole o frasi in genere utilizzate nella posta indesiderata inviata da agenzie prive di scrupoli. Per evitare che messaggi potenzialmente legittimi vengano rifiutati, gli amministratori impostano delle eccezioni all'applicazione del filtro contenuto specificando un elenco di indirizzi di posta elettronica SMTP di destinatari nella configurazione dell'agente filtro contenuto.

È anche possibile specificare mittenti e domini di mittenti che non si desidera siano bloccati dall'agente filtro contenuto.

## Aggregazione dell'elenco indirizzi attendibili

In Exchange 2013, l'agente filtro contenuto del server Trasporto Edge utilizza gli elenchi Mittenti attendibili, gli elenchi Mittenti bloccati, gli elenchi Destinatari attendibili e i contatti attendibili di Outlook per ottimizzare l'applicazione dei filtri per la posta indesiderata. L'*aggregazione dell'elenco indirizzi attendibili* è un insieme di funzionalità di protezione da posta indesiderata condiviso da Outlook ed Exchange. Come suggerisce il nome, questa funzione consente di raccogliere i dati dagli elenchi di indirizzi protetti dalla posta indesiderata che gli utenti di Outlook configurano e quindi rendere tali dati disponibili per gli agenti protezione posta indesiderata nel server Exchange. I messaggi di posta elettronica che gli utenti di Outlook ricevono dai contatti aggiunti ai propri elenchi Destinatari attendibili, Mittenti attendibili di Outlook o all'elenco dei contatti attendibili vengono identificati come sicuri dall'agente filtro contenuto. L'agente filtro mittente applica inoltre un filtro dei mittenti per destinatario utilizzando l'elenco Mittenti bloccati configurato dagli utenti. Per ulteriori informazioni, vedere [Aggregazione dell'elenco indirizzi attendibili](safelist-aggregation-exchange-2013-help.md).

## Configurazione dell'agente filtro contenuto

L'agente filtro contenuto viene configurato utilizzando Exchange Management Shell.


> [!IMPORTANT]
> Le modifiche apportate alla configurazione dell'agente filtro contenuto in Exchange Management Shell sono valide solo sul computer locale. Se l'agente filtro contenuto viene eseguito su più server Exchange dell'organizzazione, è necessario che le modifiche alla configurazione del filtro contenuto vengano apportate su ogni singolo computer.



L'agente filtro contenuto si basa sugli aggiornamenti per stabilire il livello di probabilità in base al quale il messaggio non viene considerato posta indesiderata e può essere quindi recapitato. Tra questi sono inclusi dati aggiornati relativi al phishing dei siti Web, l'euristica della posta indesiderata di Microsoft SmartScreen e altri aggiornamenti del filtro messaggi intelligente. Gli aggiornamenti del filtro contenuto includono in genere 6 MB di dati utili per periodi di tempo più lunghi rispetto ad altri dati relativi all'aggiornamento della protezione da posta indesiderata.

Gli aggiornamenti del filtro contenuto sono messe a disposizione da [Microsoft Update](https://go.microsoft.com/fwlink/p/?linkid=54836). I dati di aggiornamento del filtro contenuto viene aggiornato e disponibile per il download ogni due settimane.

Per ulteriori informazioni su come configurare il filtro contenuto, vedere [Gestire il filtro contenuto](manage-content-filtering-exchange-2013-help.md).


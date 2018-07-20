---
title: 'Riservatezza errori di query DNS: Exchange 2013 Help'
TOCTitle: Riservatezza errori di query DNS
ms:assetid: a3c3980c-20ca-4b54-a2e6-76d49af620b4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb676467(v=EXCHG.150)
ms:contentKeyID: 52063091
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Riservatezza errori di query DNS

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-12-02_

In Microsoft Exchange Server 2013, è possibile modificare la riservatezza query DNS per il recapito dei messaggi leggermente più veloce quando si verificano errori DNS per il dominio di destinazione. Tuttavia, a seconda degli errori DNS questa modifica può causare errori di recapito in determinate circostanze.

## Query DNS e il recapito dei messaggi remoti

Exchange server responsabile per il recapito dei messaggi a destinatari esterni devono essere in grado di trovare un server di messaggistica di destinazione che accetta la posta per i destinatari esterni. A seconda di destinazione, i messaggi vengono messi in uno o più code di recapito remoto sono in attesa il recapito a destinatari remoti. Per ulteriori informazioni sulle code di recapito, vedere [Code](queues-exchange-2013-help.md).

Exchange server esegue una query ai server DNS configurati per trovare i record DNS necessari per il recapito del messaggio. I server DNS vengono sottoposti a query in ordine in cui sono elencate. Se uno dei server DNS non è disponibile, la query viene inoltrata al server DNS successivo nell'elenco. I server DNS vengono sottoposti a query per le informazioni seguenti:

  - **Record di Mail Exchanger (MX) per la parte del dominio del destinatario esterno**   Il record MX contiene il nome di dominio completo (FQDN) del server di messaggistica responsabile dell'accettazione di messaggi per il dominio e un valore di preferenza per il server messaggistica. Il valore di preferenza minore indica un server di messaggistica preferito. Il valore della preferenza è importante se il dominio include uno o più record MX. Per ottimizzare la tolleranza di errore, la maggior parte delle organizzazioni utilizzano più server di messaggistica e più record MX con i valori delle preferenze diverse.

  - **Indirizzo (A) record per i server di messaggistica di destinazione**   Ogni server di messaggistica che viene utilizzata in un record MX deve avere un record corrispondente. Il record viene utilizzato per trovare l'indirizzo IP del server di messaggistica di destinazione. Il server Trasporto Edge sottoscritto utilizza l'indirizzo IP per aprire una connessione SMTP con il server di messaggistica di destinazione. Sebbene tecnicamente, è possibile utilizzare il nome di dominio completo di un nome canonico (CNAME) record in un record MX, questa operazione viola 974 RFC, RFC 1034, RFC 1912 e RFC 2181 e pertanto non è supportata dai server più messaggistica.
    
    La combinazione necessaria delle query DNS iterativa e le query DNS ricorsiva che iniziano con un server DNS principale viene utilizzata per risolvere il nome FQDN del server di messaggistica che viene trovato nel record MX in un indirizzo IP.

In Exchange 2013, non esiste un limite di query DNS che non è configurabile pari a 5 secondi per ogni server DNS e un limite di un minuto per l'intera query DNS.

## Possibili problemi di DNS

Anche se le impostazioni DNS nel server di Exchange siano configurate correttamente, problemi con i record DNS per un dominio specifico o eventuali problemi relativi ai server DNS che consentono di trovare il server DNS autorevole per un dominio specifico possono verificarsi. In generale, questi problemi sono sotto il controllo e devono essere risolto dai partecipanti che dispongono di tali server DNS. Questi errori relativi a DNS possono dipendere da uno o più delle condizioni seguenti:

  - Record DNS non valido per il dominio di destinazione

  - Problemi di utilizzo dei server DNS

  - Problemi durante la replica di server DNS

In Exchange 2013, quando una query DNS restituisce errori, la query continua a successivo server DNS solo se che server DNS non è già ha restituito un errore della query corrente.

È possibile controllare la riservatezza di errore di query DNS modificando il file di configurazione dell'applicazione XML `%ExchangeInstallPath%bin\EdgeTransport.exe.config` . Questo file è associato il servizio di trasporto di Microsoft Exchange. Dopo aver riavviato il servizio di trasporto di Microsoft Exchange, vengono applicate le modifiche salvate a questo file. Quando viene riavviato il servizio, il flusso della posta nel server è temporaneamente interrotto. La riservatezza di errore di query DNS è controllata dalla chiave *DnsFaultTolerance* nel file EdgeTransport.exe.config. Questa chiave vengono utilizzati i valori seguenti:

  - **Flessibile**   Quando la query DNS rileva una combinazione di record MX validi e i record MX non validi, la query DNS continua finché non viene raggiunto il valore di timeout query DNS di un minuto. Vengono eliminati i record MX non validi e viene utilizzato il record MX valido con il valore della preferenza più basso di recapitare il messaggio al server di messaggistica di destinazione. Questo è il valore predefinito.

  - **Normale**   Quando la query DNS rileva innanzitutto un record MX non valido, vengono eliminati immediatamente qualsiasi risolto i record MX con un valore di preferenza è maggiore di o uguale ai record MX non validi. Il record MX rimanente con il valore della preferenza più basso viene utilizzato per recapitare il messaggio al server di messaggistica di destinazione senza dover attendere l'intera query DNS per il timeout. Sebbene questo comportamento potrebbe causare il recapito dei messaggi più veloce, potenziale svantaggio di questo comportamento è che la query DNS non potrebbe essere Nessun record MX validi se si verificano le condizioni seguenti:
    
      - Il record MX non valido è il primo record MX per il dominio di destinazione.
    
      - Il record MX validi hanno lo stesso valore di priorità come il record MX non valido.

In modalità `Normal` e modalità `Lenient` , i risultati della query DNS per un record MX non valido non sono mai memorizzate nella cache. La volta successiva che esegue una query DNS, la funzione tenterà di risolvere i record MX per il dominio di destinazione.


> [!NOTE]
> Qualsiasi impostazione personalizzata per singolo server apportata nei file di configurazione dell'applicazione XML di Exchange, ad esempio, i file web.config sui server Accesso client oppure il file EdgeTransport.exe.config sui server Cassette postali, verrà sovrascritta quando si installa un aggiornamento cumulativo di Exchange. Salvare queste informazioni in modo da poter facilmente riconfigurare il server dopo l'installazione. È necessario riconfigurare queste impostazioni dopo aver installato un aggiornamento cumulativo di Exchange.



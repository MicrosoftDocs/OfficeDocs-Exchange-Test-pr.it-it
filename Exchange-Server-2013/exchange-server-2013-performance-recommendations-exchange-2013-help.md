---
title: 'Suggerimenti relativi alle prestazioni di Exchange Server 2013: Exchange 2013 Help'
TOCTitle: Suggerimenti relativi alle prestazioni di Exchange Server 2013
ms:assetid: 6d0aea68-10d5-4a18-b632-a814ce3daa43
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn879084(v=EXCHG.150)
ms:contentKeyID: 63763760
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Suggerimenti relativi alle prestazioni di Exchange Server 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

risoluzione dei problemi e ottimizzazione delle prestazioni Exchange Server 2013 sono particolarmente efficace quando l'ambiente è stati correttamente ridimensionata e pianificato. Mentre Exchange 2013 sono stati progettati per semplificare l'infrastruttura delle risorse sottostanti, può utilizzare comunque una grande quantità di risorse di sistema, ad esempio memoria, capacità di archiviazione e capacità della CPU.

Negli articoli di questa sezione sono stato creati da team delle prestazioni di Exchange. Contengono competenze del team del prodotto Exchange anche come best practices maturate dal casi di supporto tecnico clienti. L'obiettivo di questi articoli è utili per comprendere l'impatto delle modifiche introdotte in Exchange 2013 e l'importanza del dimensionamento correttamente l'infrastruttura di Exchange 2013. È stato incluso anche le ottimizzazioni consigliate e indicazioni sull'identificazione dei problemi di prestazioni.

## Modifiche dell'architettura in Exchange 2013 e altre risorse

Le modifiche dell'architettura di Exchange 2013 sono già documentate su TechNet e in [Exchange Team Blog](https://go.microsoft.com/fwlink/p/?linkid=35786). Si verrà innanzitutto touch in caso di modifiche di alto livello pochi considerare la possibilità per comprendere meglio le prestazioni dei costi e dimensioni. Di seguito, quindi è stata inclusa un elenco di riferimenti consigliati per fornire ulteriori contesto e dello sfondo nelle seguenti aree importanti.


> [!NOTE]
> Vedere <A href="exchange-2013-virtualization-exchange-2013-help.md">Virtualizzazione di Exchange 2013</A> per indicazioni di ottimizzazione delle prestazioni relative alla distribuzione di Exchange Server 2013 in un ambiente virtualizzato.



In Exchange 2013, il ruolo del server Accesso Client è un server proxy senza informazioni sullo stato. Dopo la responsabilità principale del ruolo del server Accesso Client è per l'autenticazione proxy e quindi le richieste in arrivo ogni richiesta al server cassette postali appropriato, quello che ospita la copia attiva della cassetta postale utente. Ciò significa che non è più necessario per configurare l'affinità tra il server Accesso Client e bilanciamento del carico per i protocolli specifici.

Un'altra modifica degne di nota in Exchange 2013 sia disponibile nell'archivio informazioni. Il servizio Archivio informazioni ora costituito da due tipi di processi: host e lavoratori. Ogni istanza del database è associato il proprio processo Microsoft.Exchange.Store.Worker.exe. Consente un migliore isolamento di problemi relativi al database problematica e può ridurre l'impatto sulle prestazioni di un problema del database solo all'istanza di un lavoro per il database.

Il servizio replica di Microsoft Exchange è responsabile per tutti i servizi di disponibilità elevata relativi al ruolo Server cassette postali. Questo servizio di replica ospita il componente Active Manager, responsabile per il monitoraggio errori e utilizzo di azioni correttive.

Un ottimo post su modifiche dell'architettura, tra cui l'impatto di modifica delle dimensioni un ambiente di Exchange 2013 dalle versioni precedenti, sono disponibili in [Exchange 2013 Server Role Architecture](https://go.microsoft.com/fwlink/p/?linkid=523735).

Informazioni sulle modifiche dell'architettura di Exchange 2013 e informazioni di carattere generale su altre aree rilevanti, sono disponibili negli articoli seguenti:

[Exchange Server 2013 Architecture](https://go.microsoft.com/fwlink/p/?linkid=523769)

[Pianificare il modo più appropriato: Exchange Server 2013 dimensionamento scenari](https://go.microsoft.com/fwlink/p/?linkid=523773)

[Monitoraggio e ottimizzazione di Microsoft Exchange Server 2013 Performance](https://go.microsoft.com/fwlink/p/?linkid=523774)

[L'implementazione di Exchange Server 2013: (01) eseguire l'aggiornamento e distribuzione di Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523775)

[L'implementazione di Exchange Server 2013: (02) pianificare il modo in cui destra: Exchange Server 2013 dimensioni](https://go.microsoft.com/fwlink/p/?linkid=523776)

[L'implementazione di Exchange Server 2013: (03) Exchange Server 2013 Virtualization Best Practices](https://go.microsoft.com/fwlink/p/?linkid=523777)

[L'implementazione di Exchange Server 2013: architettura di Exchange (04): disponibilità elevata e resilienza del sito](https://go.microsoft.com/fwlink/p/?linkid=523779)

[L'implementazione di Exchange Server 2013: connettività Outlook (05)](https://go.microsoft.com/fwlink/p/?linkid=523781)

[Architettura di preferita](https://go.microsoft.com/fwlink/p/?linkid=523782)

[Ruolo del Server accesso Client Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=386373)

[Exchange Server 2013 Virtualization Best Practices](https://go.microsoft.com/fwlink/p/?linkid=523783)

[Bilanciamento del carico](load-balancing-exchange-2013-help.md)

[Aggiornamenti di Exchange Server: numeri di build e date di rilascio](https://technet.microsoft.com/it-it/library/hh135098\(v=exchg.150\))

[Note sulla versione di Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md)

[Aggiornamenti per Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md)

[Utilizzo dei Thread di ASP.NET in IIS 7.5, IIS 7.0 e IIS 6.0](https://go.microsoft.com/fwlink/p/?linkid=169626)


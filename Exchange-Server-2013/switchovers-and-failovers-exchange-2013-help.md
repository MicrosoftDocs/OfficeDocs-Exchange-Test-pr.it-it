---
title: 'Passaggi e failover: Exchange 2013 Help'
TOCTitle: Passaggi e failover
ms:assetid: 75388645-cae1-402e-bf02-c4949d3e2c31
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298067(v=EXCHG.150)
ms:contentKeyID: 62523891
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Passaggi e failover

 

_**Si applica a:** Exchange Server 2013 SP1_

_**Ultima modifica dell'argomento:** 2015-12-02_

Switchover e procedure di failover sono le due forme di interruzioni di Microsoft Exchange Server 2013:

  - Un *passaggio* è un'interruzione di un database o server che viene avviato in modo esplicito da un cmdlet o dal sistema di disponibilità gestita in Exchange 2013 pianificata. Switchover vengono in genere eseguita per prepararsi per l'esecuzione di un'operazione di manutenzione. Switchover comportano lo spostamento della copia del database delle cassette postali attivo in un altro server nel gruppo di disponibilità del database (DAG). Se non viene trovata alcuna destinazione integro durante un passaggio, amministratori genererà un errore e il database delle cassette postali rimarrà backup o installato.

  - Un *failover* fa riferimento a eventi imprevisti che genera la non disponibilità dei servizi, dati o entrambi. Un failover comporta il sistema automaticamente risolto l'errore attivando una copia del database delle cassette postali passiva per effettuare la copia del database delle cassette postali attivi. Se non viene trovata alcuna destinazione integro durante un failover, il database delle cassette postali viene disinstallato.

Exchange 2013 è stato appositamente progettato per gestire switchover e failover.

Per informazioni sulle attività di gestione relative alla resilienza del sito e all'elevata disponibilità, vedere [Gestione di elevata disponibilità e resilienza del sito](managing-high-availability-and-site-resilience-exchange-2013-help.md).

## Switchover

In Exchange 2013 sono disponibili tre tipi di autenticazione:

  - Switchover del database

  - Switchover del server

  - Switchover del datacenter

## Switchover del database

Un *switchover di database* è la procedura mediante la quale un singolo database attivo viene trasferito su un'altra copia di database (copia passiva) che diventa la nuova copia attiva di database. I switchover possono avvenire sia all'interno dei datacenter che tra l'uno e l'altro. È possibile eseguire un switchover di database utilizzando l'interfaccia di amministrazione di Exchange o Shell. Indipendentemente da quale interfaccia viene utilizzata, la procedura di switchover è analoga alla seguente:

1.  L'amministratore avvia un switchover del database per spostare la copia attiva corrente di database delle cassette postali su un altro server.

2.  Il client utilizzato per questa attività esegue una chiamata RPC al servizio Replica di Microsoft Exchange su un membro del gruppo di disponibilità.

3.  Se non detiene il ruolo di PAM (Manager primario attivo), il membro del gruppo DAG assegna l'attività al server che contiene il ruolo PAM.

4.  Viene effettuata una chiamata RPC al servizio Replica di Microsoft Exchange sul server che contiene il ruolo PAM.

5.  Il PAM legge e aggiorna le informazioni sulla posizione del database che è memorizzata nel database cluster per il DAG.

6.  Il PAM contatta il servizio Replica di Microsoft Exchange sul membro DAG la cui copia passiva è stata attivata come nuova copia attiva del database delle cassette postali.

7.  Il servizio Replica di Microsoft Exchange sul server di destinazione esegue una query sui servizi Replica di Microsoft Exchange su tutti gli altri membri DAG per determinare il miglior file di registro di origine per la copia del database.

8.  Il database viene disinstallato dal server corrente e il servizio Replica di Microsoft Exchange copia i registri rimanenti sul server di destinazione.

9.  Il servizio replica di Microsoft Exchange sul server di destinazione richiede un'installazione del database.

10. ll servizio Archivio informazioni di Microsoft Exchange sul server di destinazione riesegue i file di registro e installa il database.

11. Qualsiasi codice di errore viene riportato al servizio Replica di Microsoft Exchange sul server di destinazione.

12. Il PAM (Manager primario attivo) aggiorna le informazioni sullo stato della copia del database nel database cluster per il gruppo di disponibilità del database (DAG).

13. Tutti gli errori di codice vengono restituiti dal servizio Replica di Microsoft Exchange sul server di destinazione al servizio Replica di Microsoft Exchange sul PAM (Manager primario attivo).

14. Il servizio Replica di Microsoft Exchange sul PAM restituisce tutti gli errori all'interfaccia amministrativa da cui è stata richiamata l'attività.

15. Remote PowerShell restituisce i risultati dell'operazione all'interfaccia amministrativa richiedente.

Per ulteriori informazioni sull'esecuzione di uno switchover del database, vedere [Attivare una copia del database delle cassette postali](activate-a-mailbox-database-copy-exchange-2013-help.md).

## Switchover del server

Un switchover del server è la procedura mediante la quale tutti i database attivi su un membro DAG sono attivati su uno o più altri membri DAG. Come i switchover dei database, un switchover di un server può avvenire sia nell'ambito di un datacenter che tra un datacenter e l'altro e può essere avviato utilizzando EAC o Shell. Indipendentemente da quale interfaccia viene utilizzata, la procedura di switchover del server è analoga alla seguente:

1.  L'amministratore avvia un switchover di un server per spostare tutte le copie attive del database delle cassette postali su uno o più server.

2.  Per questa attività si eseguono gli stessi passi già descritti in questo argomento per i switchover dei database (Passi 2 - 4) per ciascuno dei database attivi sul server corrente.

3.  Il PAM legge e aggiorna le informazioni sulla posizione del database che è memorizzata nel database cluster per il DAG.

4.  Il PAM (Manager primario attivo) contatta il servizio Replica di Microsoft Exchange su ciascun membro del DAG con una copia passiva in corso di attivazione.

5.  Il servizio Replica di Microsoft Exchange sui server di destinazione esegue una query sui servizi Replica di Microsoft Exchange su tutti gli altri membri DAG per determinare la miglior origine di registro per la copia del database.

6.  Il database viene disinstallato dal server corrente e il servizio Replica di Microsoft Exchange copia i registri rimanenti su ciascun server di destinazione.

7.  Il servizio Replica di Microsoft Exchange su ciascun server di destinazione richiede un'installazione del database.

8.  ll servizio Archivio informazioni di Microsoft Exchange su ciascun server di destinazione riesegue i file di registro e installa il database.

9.  Qualsiasi codice di errore viene riportato al servizio Replica di Microsoft Exchange sul server di destinazione.

10. Il PAM (Manager primario attivo) aggiorna le informazioni sullo stato della copia del database nel database cluster per il gruppo di disponibilità del database (DAG).

11. Tutti gli errori di codice vengono restituiti dal servizio Replica di Microsoft Exchange sul server di destinazione al servizio Replica di Microsoft Exchange sul PAM (Manager primario attivo).

12. Il servizio Replica di Microsoft Exchange sul PAM restituisce tutti gli errori all'interfaccia amministrativa da cui è stata richiamata l'attività.

13. Remote PowerShell restituisce i risultati dell'operazione all'interfaccia amministrativa richiedente.

Per ulteriori informazioni sull'esecuzione di uno switchover del server, vedere [Esecuzione del passaggio di un server](perform-a-server-switchover-exchange-2013-help.md).

## Switchover dei datacenter

In una configurazione con resilienza del sito, può verificarsi all'interno di un DAG il ripristino automatico in risposta a un errore a livello di sito, consentendo al sistema di messaggistica di rimanere in uno stato funzionale. Questa configurazione richiede almeno tre posizioni, poiché richiede la distribuzione dei membri DAG in due posizioni e quella del server di controllo del DAG in una terza posizione.

Se non si dispone di tre posizioni, oppure se si hanno tre posizioni ma si desidera controllare le azioni di ripristino a livello di datacenter, è possibile configurare un DAG per il ripristino manuale nel caso di errore a livello di sito. In tal caso, la procedura da eseguire viene denominata *switchover del datacenter*. Come per molti scenari di ripristino di emergenza, la pianificazione e preparazione anticipata di uno switchover del datacenter può semplificare il processo e ridurre la durata dell'interruzione.

A causa delle numerose modifiche all'architettura di Exchange 2013, incluso il consolidamento dei ruoli del server, l'esecuzione di switchover del datacenter in Exchange 2013 è significativamente più facile di quanto non lo fosse per Exchange 2010. Per una procedura dettagliata sull'esecuzione di switchover del datacenter, vedere [Passaggi centro dati](datacenter-switchovers-exchange-2013-help.md).

## Failover

Un failover è un processo di attivazione automatico che può verificarsi a livello del database, del server o del datacenter. I failover si verificano in risposta ad un errore in un singolo database (ad esempio, una perdita di dati isolata) o in un intero servizio (ad esempio, un errore nella scheda madre o un'interruzione nell'alimentazione) oppure in un intero sito (ad esempio, la perdita di tutti i membri DAG in un sito).

I DAG e le copie del database delle cassette postali forniscono una ridondanza completa e un rapido ripristino sia dei dati che dei servizi che forniscono l'accesso ai dati. Nella seguente tabella vengono descritte le azioni di ripristino previste per diversi tipi di errore. Alcuni errori richiedono l'avvio del ripristino da parte dell'amministratore, mentre altri vengono gestiti automaticamente dal sistema.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Descrizione</th>
<th>Attivazione automatica</th>
<th>Azione di ripristino automatico</th>
<th>Stato nel corso di ripristino: Attivo</th>
<th>Stato nel corso di ripristino: Passivo</th>
<th>Azioni di ripristino</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Errore del database di Extensible Storage Engine (ESE): Le unità sulle quali è archiviato il database restituiscono gli errori su alcune letture (ad esempio, un errore -1018 error).</p></td>
<td><p>Possibile breve interruzione.</p>
<p>Possibile failover automatico.</p></td>
<td><p>Correzione automatica di pagina non valida.</p></td>
<td><p>Switchover manuale, failover automatico o ripristino in linea.</p></td>
<td><p>Non riuscita</p></td>
<td><p>Ricostruzione RAID, ripristino di database e copia database, ripristino ed esecuzione, quindi installazione delle patch sulla pagina o installazione delle patch sulla pagina dalla copia.</p></td>
<td><p>Potrebbero esserci altri codici di errore di database trasferibili.</p>
<p>Non include errori di blocco di sistema per file NTFS.</p>
<p>Se viene eseguito il failover o switchover, il server host viene aggiornato.</p></td>
</tr>
<tr class="even">
<td><p>Errore del database ESE &quot;<em>semi-soft&quot;</em>: Le unità in cui è archiviato il database restituiscono gli errori in alcune operazioni di scrittura.</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Ricostruzione automatica volume/disco dopo possibile sostituzione unità.</p></td>
<td><p>Disinstallazione se non è possibile il ripristino.</p></td>
<td><p>Operazione non riuscita</p></td>
<td><p>La rigenerazione RAID può risolvere il problema.</p>
<p>Copia e ripristino, ripristino ed esecuzione del recupero o ricostruzione volume/disco dopo possibile sostituzione.</p></td>
<td><p>Un errore di scrittura semi-soft ESE indica che alcune operazioni di scrittura vengono completate correttamente.</p>
<p>Non include un errore di blocco NTFS.</p></td>
</tr>
<tr class="odd">
<td><p>Errore di registro ESE &quot;semi-soft&quot;: Le unità su cui sono archiviati i dati di registrazione stanno restituendo errori non ripristinati su alcune operazioni di lettura o scrittura.</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Ricostruzione automatica volume/disco dopo possibile sostituzione unità.</p></td>
<td><p>Disinstallazione, se non è possibile il ripristino.</p></td>
<td><p>Operazione non riuscita</p></td>
<td><p>La rigenerazione RAID può risolvere il problema.</p>
<p>Copia e ripristino, ripristino ed esecuzione del recupero o ricostruzione volume/disco dopo possibile sostituzione.</p></td>
<td><p>Un errore di lettura/scrittura semi-soft ESE significa che alcune operazioni di lettura/scrittura vengono completate correttamente.</p>
<p>Se si verifica un errore sul database, si verificherà il ripristino automatico prima che inizi la procedura del ripristino dei dati di registrazione.</p></td>
</tr>
<tr class="even">
<td><p>Errore software ESE o esaurimento risorse: Un errore in cui ESE termina l'istanza (ad esempio, ID Evento 1022, profondità punto di arresto troppo alta).</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Nessuno.</p></td>
<td><p>Disinstallazione, se non è possibile il ripristino.</p></td>
<td><p>Operazione non riuscita</p></td>
<td><p>Correzione del problema delle risorse sottostanti.</p></td>
<td><p>Questo errore potrebbe essere l'errore emerso in altri casi.</p></td>
</tr>
<tr class="odd">
<td><p>Errori di blocco NTFS: Nelle unità su cui è archiviato il database o nei registri si è verificato un errore di lettura o scrittura su una struttura di controllo NTFS.</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Volume completamente ricostruito dopo possibile sostituzione delle unità.</p></td>
<td><p>Disinstallazione, se non è possibile il ripristino.</p></td>
<td><p>Operazione non riuscita</p></td>
<td><p>La rigenerazione RAID può risolvere il problema. Le utilità NTFS potrebbero risolvere i problemi NTFS. Potrebbe essere necessario il ripristino di Exchange.</p></td>
<td><p>Ciò si verifica con maggior probabilità quando RAID non è in uso. Se ci sono degli effetti sul volume di registro attivo, alcuni file di registro andranno perduti.</p>
<p>Non include gli errori corretti automaticamente da NTFS o dal software o hardware sottostante.</p></td>
</tr>
<tr class="even">
<td><p>Errore dell'unità di database o di registro: Su un'unità su cui è archiviato il database o i registri si è verificato un errore grave ed è totalmente inaccessibile.</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Sostituzione o riformattazione dell'unità, seguita dalla ricostruzione completa del volume.</p></td>
<td><p>Disinstallazione, se non è possibile il ripristino.</p></td>
<td><p>Operazione non riuscita</p></td>
<td><p>Sostituzione di unità seguita da una possibile rigenerazione RAID.</p>
<p>Sostituzione di unità seguita da una completa rigenerazione del volume.</p>
<p>Ricostruzione completa del volume.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="odd">
<td><p>Errore del volume di database o di registro: Errore nel volume a causa di NTFS o problemi di volume di livello inferiore.</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Unità riformattata o sostituita.</p></td>
<td><p>Disinstallazione, se non è possibile il ripristino.</p></td>
<td><p>Operazione non riuscita</p></td>
<td><p>Sostituzione di unità seguita da una possibile rigenerazione RAID.</p>
<p>Sostituzione di unità seguita da una completa rigenerazione del volume.</p>
<p>Ricostruzione completa del volume.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="even">
<td><p>Spazio esaurito sul database o sul volume di registro: Spazio esaurito nel sistema dei file NTFS con il database o i file di registro.</p></td>
<td><p>Failover automatico se un'altra copia non si trova in uno stato simile.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Operazione non riuscita</p></td>
<td><p>Eseguire backup completi o progressivi, cancellare manualmente i registri, lasciar passare del tempo, riprendere la copia del database oppure ripristinare una copia del database con errore.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="odd">
<td><p>Disinstallazione da parte dell'amministratore del database non corretto.</p></td>
<td><p>Se il failover automatico non è bloccato dall'amministratore, ci sarà una breve interruzione.</p>
<p>Se viene impedito il failover automatico, ci sarà un'interruzione finché non verrà installato il database.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Non applicabile</p></td>
<td><p>Correzione dell'errore da parte dell'amministratore.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="even">
<td><p>Sospensione da parte dell'amministratore della copia del database errato.</p></td>
<td><p>A seconda della configurazione e della copia con errore, è possibile impedire il ripristino automatico.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Non applicabile.</p></td>
<td><p>Sospeso</p></td>
<td><p>Correzione dell'errore da parte dell'amministratore.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="odd">
<td><p>Disinstallazione da parte dell'amministratore di un database per archiviazione, NTFS o manutenzione del volume.</p></td>
<td><p>Se il failover automatico non è bloccato dall'amministratore, ci sarà una breve interruzione.</p>
<p>Se il failover automatico viene bloccato, ci sarà un'interruzione finché l'amministratore non completerà l'attività.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Non applicabile</p></td>
<td><p>Completamento dell'attività da parte dell'amministratore.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="even">
<td><p>Sospensione da parte dell'amministratore di una copia del database per archiviazione, NTFS o manutenzione del volume.</p></td>
<td><p>A seconda della configurazione e della copia con errore, è possibile impedire il ripristino automatico.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Non applicabile.</p></td>
<td><p>Sospeso</p></td>
<td><p>Completamento delle azioni da parte dell'amministratore.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="odd">
<td><p>Disinstallazione di un database da parte dell'amministratore per la manutenzione offline del database.</p></td>
<td><p>Interruzione fino all'intervento di correzione.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Sospeso</p></td>
<td><p>Completamento delle azioni da parte dell'amministratore.</p></td>
<td><p>Le copie del database attiva e passiva sono diverse.</p>
<p>L'Amministratore deve sospendere le copie.</p></td>
</tr>
<tr class="even">
<td><p>Rete di archiviazione (SAN), disco o errore del controller di archiviazione.</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Ripristino dell'hardware.</p></td>
<td><p>Una copia passiva del database si troverà nello stato in cui si trovava al momento in cui si è verificato l'errore del sistema.</p></td>
</tr>
<tr class="odd">
<td><p>Manutenzione dell'hardware del server.</p></td>
<td><p>Brevi intervalli di interruzione durante il failover automatico (a meno che non venga bloccato da un amministratore).</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Completamento delle azioni.</p></td>
<td><p>Una copia passiva del database si troverà nello stato in cui si trovava al momento in cui il sistema è stato chiuso.</p></td>
</tr>
<tr class="even">
<td><p>Manutenzione del software del server.</p></td>
<td><p>Brevi intervalli di interruzione durante il failover automatico (a meno che non venga bloccato da un amministratore).</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Completamento delle azioni.</p></td>
<td><p>Una copia passiva del database si troverà nello stato in cui si trovava al momento in cui il sistema è stato chiuso.</p></td>
</tr>
<tr class="odd">
<td><p>Il servizio Archivio informazioni di Microsoft Exchange viene interrotto o sospeso da un amministratore.</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Riavviare il servizio Archivio informazioni di Microsoft Exchange.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="even">
<td><p>Errore del servizio Archivio informazioni di Microsoft Exchange ; il sistema operativo è ancora in esecuzione.</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Gestione controllo servizi riavvia il servizio Archivio informazioni di Microsoft Exchange.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Riavvio automatico o manuale del servizio Archivio informazioni di Microsoft Exchange.</p></td>
<td><p>Una copia passiva del database si troverà nello stato in cui si trovava al momento in cui si è verificato l'errore del servizio Archivio informazioni di Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>Errore parziale del servizio Archivio informazioni di Microsoft Exchange; in alcune parti dell'archivio di Exchange si è verificato un errore, ma l'errore non viene identificato come irreversibile.</p></td>
<td><p>Possibile breve interruzione durante il failover automatico.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Montata e parzialmente funzionante.</p></td>
<td><p>Qualsiasi, ma potrebbe essere solo parzialmente funzionale</p></td>
<td><p>Riavviare il server, il sistema operativo o il servizio Archivio informazioni di Microsoft Exchange .</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="even">
<td><p>Errore del server: Si è verificato un errore sul server per uno dei seguenti motivi:</p>
<ul>
<li><p>Interruzione dell'alimentazione</p></li>
<li><p>Errore irreversibile del chip del processore, della scheda madre o del backplane</p></li>
<li><p>Errore di arresto del sistema operativo</p></li>
<li><p>Il sistema operativo non risponde</p></li>
<li><p>Errore di comunicazione irreversibile</p></li>
</ul></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Riavviare il computer.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Ripristinare l'alimentazione, modificare le impostazioni del sistema operativo, modificare le impostazioni dell'hardware, sostituire l'hardware, riavviare il sistema operativo, il sistema operativo del servizio, l'hardware del servizio o correggere i problemi di comunicazione.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="odd">
<td><p>Nel gruppo di disponibilità del database (DAG) si è verificato un errore di quorum.</p></td>
<td><p>Interruzione fino all'intervento di correzione.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Correggere il quorum non corretto, assegnare un nuovo quorum o ripristinare la rete che ha provocato l'errore del quorum.</p></td>
<td><p>Una copia passiva del database si troverà nello stato in cui si trovava al momento in cui si è verificato l'errore del sistema.</p></td>
</tr>
<tr class="even">
<td><p>Errore di comunicazione su rete MAPI: Il server non è più disponibile in rete MAPI.</p></td>
<td><p>Breve interruzione durante il failover automatico; non ci dovrebbe essere perdita di dati.</p></td>
<td><p>Nessuna. Altri tentativi di comunicazione.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Correggere il problema di comunicazione correggendo i problemi di hardware o di software.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="odd">
<td><p>Errore di comunicazione sulla rete per la replica: Il server non riceve heartbeat, copie di registro né seeding sulla rete per la replica non funzionante.</p></td>
<td><p>Possibile esaurimento copie o del seeding mentre il carico di lavoro viene trasferito su un'altra rete.</p></td>
<td><p>Nessuna. Altri tentativi di comunicazione.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Correggere il problema di comunicazione correggendo i problemi di hardware o di software.</p></td>
<td><p>Effetti dell'errore sulla resilienza.</p></td>
</tr>
<tr class="even">
<td><p>Errore di comunicazione su più reti: Il server non è in grado di ricevere heartbeat, copie di registri o seeding attraverso più reti.</p></td>
<td><p>Breve interruzione durante il failover automatico; non ci dovrebbe essere perdita di dati.</p></td>
<td><p>Nessuna. Altri tentativi di comunicazione.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Correggere il problema di comunicazione correggendo i problemi di hardware o di software.</p></td>
<td><p>Almeno una rete è ancora funzionante.</p></td>
</tr>
<tr class="odd">
<td><p>Errore parziale di una o più reti: Nelle reti si verifica una percentuale di errori più elevata.</p></td>
<td><p>Errore non rilevato, nessuna azione.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Installazione eseguita, possibili problemi di prestazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Correggere il problema di comunicazione correggendo i problemi di hardware o di software.</p></td>
<td><p>Sulla rete si sta verificando una percentuale di errori più elevata del normale.</p></td>
</tr>
<tr class="even">
<td><p>Blocco sistema operativo non rilevato: Il sistema operativo smette di rispondere, ma ciò non viene rilevato dal monitoraggio o dal clustering.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Qualsiasi.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Riavviare o interrompere le risorse che non rispondono.</p></td>
<td><p>Il blocco non è stato rilevato, quindi non viene intrapresa alcuna azione.</p>
<p>Alcune funzionalità potrebbero non essere operative.</p></td>
</tr>
<tr class="odd">
<td><p>Si è verificato un errore nell'unità del sistema operativo.</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Sostituire l'unità e ricostruire il server oppure ricreare il volume mediante RAID.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="even">
<td><p>Spazio insufficiente sull'unità del sistema operativo.</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Liberare manualmente lo spazio sul volume.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="odd">
<td><p>Nell'unità che contiene i file binari di Exchange si è verificato un errore di unità o di volume.</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Sostituire l'unità e reinstallare l'applicazione oppure ricreare il volume mediante RAID.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="even">
<td><p>Spazio insufficiente nell'unità contenente i file binari di Exchange.</p></td>
<td><p>Breve interruzione durante il failover automatico.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Liberare manualmente lo spazio sul volume.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
<tr class="odd">
<td><p>Rilevato registro nuovo non valido: La sequenza di registro viene interrotta da un file esistente.</p></td>
<td><p>Breve interruzione durante il failover automatico, considerare che le altre copie non abbiano lo stesso problema.</p></td>
<td><p>Nessuna.</p></td>
<td><p>Disinstallazione.</p></td>
<td><p>Operazione non riuscita</p></td>
<td><p>Rimuovere i registri in eccesso dopo averne determinato l'origine.</p></td>
<td><p>I registri in eccesso non dovrebbero eseguire la replica.</p></td>
</tr>
<tr class="even">
<td><p>Nella replica continua è stato rilevato un registro non valido: Nella riesecuzione è stato rilevato un registro non corretto durante la copia o la riesecuzione.</p></td>
<td><p>Non applicabile.</p></td>
<td><p>Eliminare il registro.</p></td>
<td><p>Non applicabile.</p></td>
<td><p>Operazione non riuscita</p></td>
<td><p>Eliminare il registro non valido, spostare il flusso di registri non corretti.</p></td>
<td><p>Non applicabile.</p></td>
</tr>
</tbody>
</table>


## Failover del database

Un failover del database si verifica quando una copia del database che era attiva non è più in grado di rimanere attiva. Gli eventi qui di seguito riportati si verificano come parte del failover di un database:

1.  L'errore del database è stato rilevato dal servizio Archivio informazioni di Microsoft Exchange.

2.  Il servizio Archivio informazioni di Microsoft Exchange riporta gli errori sul registro eventi del canale color porpora.

3.  Active Manager sul server che contiene il database non corretto ha rilevato gli errori.

4.  Active Manager richiede lo stato della copia del database dagli altri server che hanno una copia del database.

5.  Gli altri server restituiscono lo stato della copia del database all'Active Manager richiedente.

6.  Il PAM avvia uno spostamento del database attivo su un altro server nel gruppo di disponibilità del database (DAG) utilizzando l'algoritmo di selezione della copia migliore.

7.  Il PAM aggiorna la posizione dell'installazione del database nel database cluster per utilizzare il server selezionato.

8.  Il Il PAM (Manager primario attivo) invia una richiesta al manager attivo sul server selezionato per renderlo master del database.

9.  Active Manager sul server selezionato richiede che il servizio Replica di Microsoft Exchange tenti di copiare gli ultimi registri dal server precedente e imposti il contrassegno installabile per il database.

10. Il servizio Replica di Microsoft Exchange copia i registri dal server che aveva in precedenza la copia attiva del database.

11. Active Manager legge il numero massimo di generazione dei registi dal database cluster.

12. Il servizio Archivio informazioni di Microsoft Exchange installa la nuova copia di database attivo.

## Failover del server

Un failover del server si verifica quando il membro del gruppo di disponibilità del database non è più in grado di operare con la rete MAPI oppure quando il servizio cluster di un membro del gruppo di disponibilità non è più in grado di contattare i rimanenti membri del DAG. Gli eventi qui di seguito riportati si verificano come parte del failover di un database:

1.  Il servizio Cluster sul PAM invia una notifica al PAM per una delle due condizioni:
    
    1.  **Nodo disattivo**   Il server è raggiungibile ma non in grado di partecipare alle operazioni del DAG.
    
    2.  **Rete MAPI chiusa**   Il server non può essere contattato sulla rete MAPI, quindi non è in grado di partecipare alle operazioni DAG.

2.  Se il server è raggiungibile, il PAM contatta Active Manager sul server con errore e richiede che tutti i database vengano disinstallati immediatamente.

3.  Per ciascuna copia del database con errore:
    
    1.  Il PAM richiede lo stato della copia del database da tutti i server del gruppo di disponibilità del database (DAG).
    
    2.  Il PAM riceve una risposta da tutti i membri raggiungibili e attivi del DAG.
    
    3.  PAM tenta di determinare la migliore origine del registro tra tutti i server rispondenti effettuando la query sul numero dell'ultima generazione dei registri da ciascuno dei risponditori.
    
    4.  Ogni server risponde con il numero di generazione del registro.

4.  Il PAM recupera lo stato corrente del catalogo di indicizzazione della ricerca dal database cluster.

5.  Sulla base del numero di generazione dei registri e dell'integrità del catalogo di ciascuna copia del database, il PAM seleziona le migliori copie da attivare.

6.  Il PAM aggiorna la posizione di installazione del database nel database cluster.

7.  Il Manager primario attivo (PAM) avvia il failover del database comunicando con Active Manager su uno o più server.

8.  Active Manager sui server selezionati richiede che il servizio Replica di Microsoft Exchange tenti di copiare gli ultimi registri dal server precedente e imposti il contrassegno installabile.

9.  Quando il database è installabile, Active Manager sui server installa i database.

Per ulteriori informazioni sulla miglior procedura di selezione di Active Manager, vedere [Active Manager](active-manager-exchange-2013-help.md).

## Failover del datacenter

Sono state apportate modifiche significative in Exchange 2013 che affrontano le difficoltà di configurazione della resilienza del sito in Exchange 2010. Con la semplificazione dello spazio dei nomi, il consolidamento dei ruoli del server, la separazione del ripristino del DAG e del server Accesso client (in Exchange 2013, lo spazio dei nomi non ha bisogno di spostarsi con il DAG) e le modifiche al bilanciamento del carico, Exchange 2013 fornisce nuove opzioni di resilienza del sito, quali ad esempio la possibilità di utilizzare un solo spazio dei nomi. Inoltre, se si dispone di più di due posizioni in cui distribuire i componenti del servizio di messaggistica, Exchange 2013 consente anche di configurare il servizio di messaggistica per failover automatico in risposta agli errori che richiedono un intervento manuale in Exchange 2010.

La resilienza del sito è stata semplificata da un punto di vista operativo in Exchange 2013. Exchange sfrutta la tolleranza di errore incorporata nello spazio dei nomi attraverso più indirizzi IP e il bilanciamento del carico (e, se necessario, la possibilità di attivare e disattivare i server). Una delle modifiche più significative apportata in Exchange 2013 consiste nell'utilizzare la capacità dei client di memorizzare nella cache più indirizzi IP restituiti da un server DNS in risposta alla richiesta di risoluzione di un nome. Presupponendo che il client abbia la capacità di memorizzare nella cache più indirizzi IP (come in quasi tutti i client HTTP e quasi tutti i protocolli di accesso del client in Exchange 2013 basati su HTTP (Outlook, Outlook via Internet, Exchange ActiveSync (EAS), EWS, OWA, Interfaccia di amministrazione di Exchange, RPS e così via), tutti i client HTTP hanno la capacità di utilizzare più indirizzi IP fornendo in tal modo il failover da parte del client. È possibile configurare il DNS per gestire più indirizzi IP per un client durante la risoluzione dei nomi. Ad esempio, il client richiede mail.contoso.com e ottiene due indirizzi IP o quattro indirizzi IP. Tuttavia, il client utilizzerà in maniera affidabile molti degli indirizzi IP che ottiene. Ciò migliora notevolmente la condizione del client, poiché se si verifica un errore su uno degli indirizzi IP, il client può disporre di uno o più indirizzi per tentare di connettersi. Se un client ne prova uno e si verifica un errore, attende circa 20 secondi e prova quello successivo nell'elenco. Pertanto, se si perde la connettività alla matrice CAS primaria e si dispone di un secondo indirizzo IP pubblicato per una seconda matrice CAS, il ripristino per i client avviene automaticamente (in circa 21 secondi).

I client HTTP moderni (sistemi operativi e browser di dieci anni o meno) lavorano automaticamente con questa ridondanza. Lo stack HTTP può accettare più indirizzi IP per un nome di dominio completo (FQDN) e, se si verifica un errore con il primo indirizzo IP (ovvero, non riesce a connettersi), passerà al successivo indirizzo IP dell'elenco. In caso di errore non grave (la connessione è andata perduta una volta stabilita la sessione, forse a causa di un errore saltuario nel servizio in cui, ad esempio, un dispositivo sta interrompendo i pacchetti e deve essere disattivato), potrebbe essere necessario aggiornare il browser.

Con la corretta configurazione, il failover si verifica a livello del client e i client vengono automaticamente reindirizzati a un secondo datacenter che dispone di server Accesso client operativi e questi server comunicano tramite proxy con il server Cassette postali dell'utente, che non subisce gli effetti dell'interruzione (poiché non si effettua un switchover). Poiché il servizio viene ripristinato automaticamente, invece di effettuare le operazioni di recupero del servizio, l'utente può dedicarsi alla risoluzione del problema (ad esempio, sostituendo il dispositivo di bilanciamento del carico in errore).

Poiché è possibile eseguire il failover dello spazio dei nomi tra i datacenter, per ottenere il failover di un datacenter è sufficiente disporre di un meccanismo per failover del ruolo del server Cassette postali nei datacenter. Per ottenere un failover automatico per il gruppo di disponibilità del database, è sufficiente architettare una soluzione in cui il gruppo di disponibilità del database è equamente suddiviso tra i due datacenter e, quindi, posizionare il server di controllo in una terza posizione affinché possa essere gestito dai membri del gruppo di disponibilità del database in uno dei datacenter, indipendentemente dallo stato della rete tra i datacenter che contengono i membri del gruppo di disponibilità del database. La soluzione risiede nella terza posizione isolata dagli errori di rete che influenzano le posizioni contenenti i membri DAG.

Se si solo sono due datacenter e si desidera poter configurare il failover automatico, è possibile utilizzare Microsoft Azure come posizione di terzi. È necessario creare una rete virtuale Azure e connettersi ai due datacenter utilizzando una connessione VPN multipunto. Sarà quindi possibile collocare il server di controllo in una macchina virtuale Microsoft Azure. Per ulteriori informazioni, vedere [Utilizzo di una macchina virtuale Azure Microsoft come server di controllo del DAG](using-a-microsoft-azure-vm-as-a-dag-witness-server-exchange-2013-help.md).


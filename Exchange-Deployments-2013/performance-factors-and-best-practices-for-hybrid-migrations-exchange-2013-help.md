---
title: 'Fattori relativi alle prestazioni e procedure consigliate per le migrazioni ibride: Exchange 2013 Help'
TOCTitle: Fattori relativi alle prestazioni e procedure consigliate per le migrazioni ibride
ms:assetid: 120a7832-d2d3-47d7-b305-918360c2ef66
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt483789(v=EXCHG.150)
ms:contentKeyID: 70117980
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Fattori relativi alle prestazioni e procedure consigliate per le migrazioni ibride

 

_**Si applica a:** Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Esistono varie possibilità per la migrazione di dati da un'organizzazione di posta elettronica locale a Office 365. Una domanda frequente quando si pianifica una migrazione a Office 365 è come migliorare le prestazioni della migrazione di dati e ottimizzare la velocità della migrazione. In questo articolo vengono descritte le prestazioni di migrazione per distribuzioni ibride di Exchange. Per informazioni sulle prestazioni relative ad altri metodi di migrazione, vedere [Prestazioni e procedure consigliate per la migrazione a Office 365](http://go.microsoft.com/fwlink/p/?linkid=623651).

## Fattori relativi alle prestazioni e procedure consigliate per le migrazioni ibride

La migrazione di distribuzione ibrida supporta il passaggio lineare tra i server Exchange e Exchange Online in Office 365.

La migrazione di distribuzione ibrida è di gran lunga il metodo più rapido per migrare i dati della cassetta postale su Office 365. Nel corso di distribuzioni reali dei clienti è stata osservata una velocità effettiva fino a 100 GB/ora. Nella tabella che segue è riportato un elenco di fattori che influiscono sugli scenari di migrazione ibrida nativa di Office 365.

Se l'ambiente locale contiene più siti in aree geograficamente distanti, è possibile migliorare le prestazioni di migrazione creando endpoint di migrazione geograficamente vicini. Infatti, in uno scenario simile la migrazione sfrutta la rete Microsoft anziché utilizzare un endpoint di migrazione centralizzato che usa la rete locale.

## Fattore 1: origine dati (Exchange Server)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elenco di controllo</th>
<th>Descrizione</th>
<th>Procedure consigliate</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Prestazioni del sistema</p></td>
<td><p>L'estrazione dei dati è un'attività a elevato utilizzo di risorse. Di conseguenza, il sistema di origine deve disporre di risorse sufficienti, quali tempo di CPU e memoria, per garantire prestazioni di migrazione ottimali. Durante la migrazione, il sistema di origine è spesso vicino a raggiungere la capacità massima in presenza di un carico di lavoro normale degli utenti finali. Un carico di lavoro aggiuntivo dovuto alla migrazione può talvolta impedire l'accesso degli utenti finali a causa della mancanza di risorse di sistema.</p></td>
<td><p>Monitorare le prestazioni del sistema durante un test di migrazione pilota. Se il sistema è impegnato, evitare una pianificazione di migrazione aggressiva per il sistema in questione a causa di potenziali rallentamenti della migrazione e problemi di disponibilità dei servizi. Se possibile, migliorare le prestazioni del sistema di origine aggiungendo risorse hardware e riducendo il carico del sistema tramite lo spostamento di attività e utenti su altri server che non sono coinvolti nella migrazione.</p>
<p>Per ulteriori informazioni, vedere:</p>
<ul>
<li><p><a href="http://go.microsoft.com/fwlink/?linkid=723566">Chiedere Perf Guy: Sizing Exchange 2016 Deployments</a></p></li>
<li><p><a href="https://technet.microsoft.com/it-it/library/jj150551(v=exchg.150)">Prestazioni e lo stato dei server</a></p></li>
<li><p><a href="http://technet.microsoft.com/it-it/library/dd351192.aspx">Informazioni sulle prestazioni di Exchange 2010</a></p></li>
</ul>
<p>Quando si esegue la migrazione da un'organizzazione di Exchange locale in cui sono presenti più server Cassette postali e più database, è consigliabile creare un elenco di utenti coinvolti nella migrazione che sia equamente distribuito tra più server Cassette postali e database. In base alle prestazioni dei singoli server, l'elenco può essere ulteriormente perfezionato per ottimizzare la velocità effettiva.</p>
<p>Ad esempio, se il server A ha il 50% in più di disponibilità di risorse rispetto al server B, è ragionevole avere il 50% in più di utenti dal server A nello stesso batch di migrazione. Procedure analoghe possono essere applicate ad altri sistemi di origine.</p>
<p>Eseguire le migrazioni quando la disponibilità di risorse nei server è massima, ad esempio dopo l'orario di lavoro oppure nei fine settimana e in giorni festivi.</p></td>
</tr>
<tr class="even">
<td><p>Attività di back-end</p></td>
<td><p>Altre attività di back-end in esecuzione durante la migrazione. Poiché le procedure consigliate prevedono di eseguire la migrazione dopo l'orario di lavoro, non è raro che le migrazioni entrino in conflitto con altre attività di manutenzione eseguite nei server locali, come il backup dei dati.</p></td>
<td><p>Valutare altre attività di sistema che potrebbero essere eseguite durante la migrazione. È consigliabile eseguire la migrazione dei dati quando non sono in esecuzione altre attività a elevato utilizzo di risorse.</p>
<p><strong>Nota</strong>   Per i clienti che utilizzano Microsoft Exchange locale, attività di back-end comuni sono le soluzioni di backup e la <a href="http://technet.microsoft.com/it-it/library/aa996226(exchg.65).aspx">manutenzione dell'archivio di Exchange</a>.</p></td>
</tr>
</tbody>
</table>


## Fattore 2: server di migrazione

La migrazione i distribuzione ibrida è un metodo di migrazione con pull/push di dati avviato sul cloud e il server ibrido di Exchange funge da server di migrazione. Questa situazione è spesso sottovalutata e i clienti utilizzano una macchina virtuale su bassa scala come server ibrido. Ciò determina prestazioni di migrazione insoddisfacenti

**Procedura consigliata**

Oltre ad applicare le procedure consigliate descritte in precedenza, sono state sottoposte a test le seguenti procedure consigliate che hanno determinato un miglioramento delle prestazioni in scenari reali di migrazione dei clienti:

  - Utilizzare potenti computer fisici di livello server anziché macchine virtuali per i server ibridi di Exchange.

  - Utilizzare più server ibridi alle spalle del servizio di bilanciamento del carico di rete del cliente.

Ad esempio, in migrazioni di clienti reali è stata registrata una velocità effettiva costante di 30 GB/ora utilizzando la seguente configurazione:

  - **Rete**  Pipe in uscita di 500 MB verso Internet, rete interna su 1 GB con backbone fiber da 10 GB.

  - **Hardware**   Le specifiche relative ai due server Accesso client/HUB (fisici) sono:
    
      - CPU: CPU Intel® Xeon® E5520 da 2,27 GHz e 2,26 GHz (due processori).
    
      - RAM: 24 GB.
    
      - Dischi: otto a 146 GB per disco. Configurazione RAID 5 = spazio raw totale 960 GB.

  - **Proxy MRS**   Configurato con un valore di concorrenza pari a 100.

## Fattore 3: modulo di migrazione

La migrazione di distribuzione ibrida utilizza strumenti nativi di Office 365. È soggetta a limitazioni di Office 365 migrazione servizio.

**Exchange 2003 e versioni successive di Exchange**

Quando si esegue la migrazione da Exchange 2003, esiste una differenza sostanziale per l'esperienza dell'utente finale. A differenza delle ultime versioni di Exchange, gli utenti finali di Exchange 2003 non possono accedere alle cassette postali mentre è in corso la migrazione dei dati. Di conseguenza, i clienti che dispongono di Exchange 2003 sono in genere più preoccupati riguardo al momento in cui pianificare le migrazioni e al tempo necessario per completarle, in particolare quando le prestazioni di migrazione sono basse a causa di elevate dimensioni delle cassette postali o una rete lenta.

La migrazione da Exchange 2003 è anche soggetta a interruzioni. Ad esempio, in una migrazione di un cliente reale, durante la migrazione di una cassetta postale di 10 GB, si è verificato un errore del servizio quando il processo era stato completato al 50%. È stato quindi necessario riavviare il server Accesso client di Office 365, che stava elaborando la migrazione dei dati, per risolvere il problema. Il riavvio della migrazione della cassetta postale ha comportato una ripetizione della migrazione di tutti i dati pari a 10 GB. Non è infatti stato possibile riprendere la migrazione dal punto in cui si era interrotta. Per Exchange 2010, e le ultime versioni di Exchange, è invece possibile riprendere le migrazioni in seguito alle interruzioni.

**Procedura consigliata**

Alcuni clienti scelgono di eseguire migrazioni in due passaggi per le cassette postali più estese e importanti di Exchange 2003:

  - **Primo passaggio**   Eseguire la migrazione delle cassette postali da Exchange 2003 a un server Exchange 2010 o versioni successive, che in genere rappresenta il server ibrido. Il primo passaggio è uno spostamento offline, ma in genere si tratta di una migrazione molto veloce su una rete locale.

  - **Secondo passaggio**   Eseguire la migrazione delle cassette postali da Exchange 2010 o versioni successive a Office 365.

Il secondo passaggio consiste in uno spostamento online, che garantisce un miglioramento dell'esperienza utente e della tolleranza d'errore. Questo approccio in due passaggi richiede una licenza di Exchange per la cassetta postale temporanea locale.

**Proxy di servizio di replica delle cassette postali (MRSProxy)**

Il proxy MRS è la caratteristica di migrazione locale che interagisce con il servizio di replica delle cassette postali in esecuzione su Office 365. Per ulteriori informazioni, vedere [Informazioni sulle richieste di spostamento](http://technet.microsoft.com/it-it/library/dd298174.aspx).

**Procedura consigliata**

È possibile configurare il numero massimo di connessioni al proxy MRS per l'istanza locale del server ibrido di Exchange. Eseguire il comando di Windows PowerShell riportato di seguito.

    Set-WebServicesVirtualDirectory -Identity "EWS (Default Web Site)" -MRSMaxConnections <number between 0 and unlimited; default is 100>


> [!NOTE]
> Per la maggior parte delle migrazioni dei clienti non è necessario modificare il valore MRSMaxConnections predefinito. Se è necessario proteggere il server di origine affinché non venga sovraccaricato dalle operazioni di migrazione, i clienti possono ridurre il numero di connessioni. Questa impostazione è specifica per ogni server MRSProxy. Se un cliente dispone di due server MRSProxy, ognuno impostato su 10 connessioni, il numero totale di connessioni proxy MRS sarà 20 (2x10). Per ulteriori informazioni sulla configurazione del servizio proxy MRS nell'organizzazione di Exchange 2010 locale, vedere <A href="http://technet.microsoft.com/it-it/library/ee732395.aspx">Avvio del servizio di MRSProxy su un server Accesso client remoto</A>.



## Fattore 4: rete

**Test di verifica**

Per i clienti di Exchange 2010 o versioni successive il testing delle prestazioni di rete per le migrazioni ibride può essere eseguito esaminando più migrazioni di cassette postali. In alternativa, è possibile eseguire la migrazione delle effettive cassette postali degli utenti con l'opzione -SuspendWhenReadyToComplete per ottenere un'indicazione delle prestazioni di migrazione. Al termine del test, rimuovere la richiesta di spostamento per evitare conseguenze per gli utenti finali.

Per ulteriori informazioni sulle richieste di spostamento, vedere [New-MoveRequest](https://technet.microsoft.com/it-it/library/dd351123\(v=exchg.150\)).

## Fattore 5: Servizio Office 365

La limitazione basata sull'integrità delle risorse di Office 365 incide sulle migrazioni utilizzando la migrazione di distribuzione ibrida di Office 365. Per ulteriori dettagli, vedere la sezione Limitazione basata sull'integrità delle risorse di Office 365.


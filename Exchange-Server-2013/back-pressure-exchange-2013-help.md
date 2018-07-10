---
title: 'Funzionalità di congestione: Exchange 2013 Help'
TOCTitle: Funzionalità di congestione
ms:assetid: 03003544-e802-4988-9427-5fc4da64dcb8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201658(v=EXCHG.150)
ms:contentKeyID: 52063039
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Funzionalità di congestione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

La funzionalità di congestione è una funzionalità di monitoraggio delle risorse di sistema del servizio di trasporto di Microsoft Exchange presente sui server Cassette postali e sui server Trasporto Edge di Exchange 2013.

Exchange può rilevare la congestione di risorse essenziali, quali spazio disponibile sul disco rigido e memoria, e intervenire per evitare l'interruzione del servizio. La funzione di congestione impedisce che le risorse di sistema vengano completamente occupate e si consente al server Exchange di elaborare i messaggi esistente prima di accettarne di nuovi. Se l'utilizzo delle risorse di sistema torna a un livello normale, il server Exchange riprenderà gradualmente il funzionamento normale e accetta di nuovi messaggi.

In Exchange 2013, quando il servizio di trasporto su un server Cassette postali o un server Trasporto Edge sono in stato di congestione delle risorse, vengono accettate le connessioni in ingresso, ma i messaggi in arrivo su tali connessioni vengono accettati a una velocità inferiore o vengono rifiutati. Quando un host SMTP tenta di effettuare una connessione a un server Exchange in stato di congestione, la connessione ha esito positivo. Tuttavia, quando l'host emette il comando **MAIL FROM** per inviare un messaggio, a seconda della risorsa che si trova in stato di congestione, il servizio di trasporto ritarda il riconoscimento del comando **MAIL FROM** o rifiuta la connessione.

**Sommario**

Resources monitored

Actions taken by Exchange Transport when under resource pressure

Back pressure configuration options in the EdgeTransport.exe.config file

Back pressure logging information

## Risorse monitorate

Le risorse di sistema riportate di seguito vengono monitorate come parte della funzionalità di controllo dell'utilizzo delle risorse:

  - Spazio libero sul disco rigido in cui viene archiviato il database delle code dei messaggi.

  - Spazio libero sul disco rigido in cui vengono archiviati i registri delle transazioni del database delle code dei messaggi.

  - Numero di transazioni del database delle code dei messaggi senza commit presenti in memoria.

  - Memoria utilizzata dal processo EdgeTransport.exe.

  - Memoria utilizzata da tutti gli altri processi.

  - Indica il numero di messaggi contenuti nella coda di invio.

Per ogni risorsa di sistema monitorata su un server Cassette postali o Trasporto Edge vengono applicati i tre livelli di utilizzo delle risorse riportati di seguito:

  - **Normale**   La risorsa non viene sovrautilizzata. Il server accetta le nuove connessioni e i nuovi messaggi.

  - **Medio**   La risorsa viene leggermente sovrautilizzata. La funzionalità di congestione viene applicata al server in modo limitato. È consentito il flusso della posta proveniente dai mittenti nel dominio autorevole. Tuttavia, a seconda della risorsa specifica in stato di congestione, il server utilizza il tarpitting per ritardare la risposta o rifiuta i comandi **MAIL FROM** in ingresso da altre risorse.

  - **Alto**   La risorsa viene fortemente sovrautilizzata. Viene applicata la funzione completa di congestione. L'intero flusso di messaggi viene interrotto e il server rifiuta tutti i nuovi comandi **MAIL FROM** in ingresso.

Nelle sezioni seguenti viene illustrato come Exchange gestisce i casi in cui una risorsa specifica è in stato di congestione.

## Spazio libero sul disco rigido per il database delle code dei messaggi

Per impostazione predefinita il database delle code dei messaggi viene memorizzato in %ExchangeInstallPath%TransportRoles\\data\\Queue. Exchange consente di monitorare l'utilizzo di spazio su disco rigido di questo percorso. Il livello alto di utilizzo dello spazio sul disco rigido viene calcolato con la formula seguente:

100 \* (*dimensione disco rigido* - *costante fissa*) / *dimensione disco rigido*

Il valore della *costante fissa* è 500 megabyte (MB).

I risultati di questa formula vengono espressi in forma di percentuale dello spazio totale utilizzato sul disco rigido. I risultati della formula sono sempre arrotondati al numero intero più vicino. Per impostazione predefinita, il livello medio di utilizzo del disco rigido è inferiore del 2% al livello alto. Per impostazione predefinita, il livello normale di utilizzo del disco rigido è inferiore del 4% al livello alto.

Inizio pagina

## Spazio libero sul disco rigido per i registri delle transazioni del database delle code dei messaggi

Per impostazione predefinita i registri delle transazioni del database delle code dei messaggi vengono memorizzati in %ExchangeInstallPath%TransportRoles\\data\\Queue. Exchange consente di monitorare l'utilizzo di spazio su disco rigido di questo percorso. Il file di configurazione dell'applicazione %ExchangeInstallPath%Bin\\EdgeTransport.exe.config contiene una chiave *DatabaseCheckPointDepthMax* con un valore predefinito pari a 384 MB. Questa chiave controlla la dimensione totale consentita per tutti i registri delle transazioni senza commit presenti nel disco rigido. Questa chiave è utilizzata nella formula per il calcolo dell'utilizzo del disco rigido.


> [!NOTE]
> Il valore della chiave <EM>DatabaseCheckPointDepthMax</EM> si applica a tutti database ESE (Extensible Storage Engine) relativi al trasporto presenti sul server Cassette postali o Trasporto Edge. In tal modo sono inclusi il database delle code dei messaggi e il database del filtro IP.



Per impostazione predefinita, l'alto livello di utilizzo dell'unità disco rigido viene calcolato utilizzando la formula seguente:

100 \* (*dimensione del disco rigido* - Min (5 GB, 3\**DatabaseCheckPointDepthMax*)) / *dimensione del disco rigido*

I risultati della formula sono sempre arrotondati al numero intero più vicino. Per impostazione predefinita, il livello medio di utilizzo del disco rigido è inferiore del 2% al livello alto. Il livello normale di utilizzo dello spazio sul disco rigido è inferiore del 4% al livello alto.

Inizio pagina

## Numero di transazioni del database delle code dei messaggi senza commit presenti in memoria

Viene mantenuto in memoria un elenco delle modifiche apportate al database delle code dei messaggi fino al momento in cui sarà possibile eseguire il commit di modifiche in un registro delle transazioni. Quindi viene eseguito il commit dell'elenco nel database delle code dei messaggi stesso. Le transazioni in sospeso del database delle code dei messaggi che vengono mantenute in memoria sono note come *bucket versione*. Il numero di bucket versione può aumentare a livelli inaccettabili a causa un volume di messaggi in arrivo eccezionalmente alto, ad attacchi di spam, problemi di integrità del database delle code di messaggi o delle prestazioni del disco rigido.

Quando Exchange inizia a ricevere messaggi, tali messaggi vengono raggruppati insieme in batch e quindi preparati come bucket versione. Se un messaggio in arrivo presenta un allegato di grandi dimensioni, può essere suddiviso in più batch. Questi batch elaborati sono denominati *punti batch*. Il numero di punti batch in sospeso può superare le soglie impostate, in particolare quando è presente un volume imprevedibilmente elevato di messaggi in arrivo con allegati di grandi dimensioni.

Quando i bucket versione o i punti batch sono in stato di congestione, il server di Exchange inizia a limitare la larghezza di banda delle connessioni in ingresso ritardando il riconoscimento dei messaggi in arrivo. Exchange riduce la frequenza del flusso dei messaggi in entrata mediante il tarpitting che causa un ritardo nei comandi **MAIL FROM**. Se la condizione di congestione delle risorse continua, Exchange aumenta gradualmente il ritardo di tarpitting. Quando l'utilizzo delle risorse torna ad essere normale, Exchnage inizia a ridurre gradualmente il ritardo di riconoscimento e torna al funzionamento normale. Per impostazione predefinita, Exchange inizia a ritardare di 10 secondi il riconoscimento dei messaggi in caso di congestione delle risorse. Se le risorse continuano ad essere in stato di congestione, il ritardo viene aumentato a incrementi di 5 secondi fino a 55 secondi.

Exchange mantiene una cronologia di utilizzo delle risorse per il bucket versione e il punto batch. Se l'utilizzo delle risorse non torna al livello normale per un numero specifico di intervalli di polling, denominato profondità della cronologica, Exchange arresta il ritardo di tarpitting e inizia a rifiutare i messaggi in arrivo finché l'utilizzo delle risorse non torna al livello normale. Per impostazione predefinita, le profondità della cronologia per bucket versione e punti batch sono rispettivamente di 10 e 300 intervalli di polling.

Inizio pagina

## Memoria utilizzata dal processo EdgeTransport.exe

Per impostazione predefinita, il livello alto di utilizzo della memoria da parte del processo EdgeTransport.exe viene calcolato utilizzando la formula seguente:

il 75% della memoria fisica totale o 1 terabyte, a seconda di quale valore è più basso

Questo calcolo non include la memoria virtuale disponibile nel disco rigido nel file di paging né la memoria utilizzata da altri processi. I risultati di questa formula vengono espressi in forma di percentuale della memoria totale utilizzata dal processo EdgeTransport.exe. I risultati della formula sono sempre arrotondati al numero intero più vicino.

Per impostazione predefinita, il livello medio di utilizzo della memoria da parte del file EdgeTransport.exe viene calcolato come il valore più basso tra il 73% della memoria fisica totale e un valore inferiore del 2% al valore del livello alto. Per impostazione predefinita, il livello normale di utilizzo della memoria da parte del file EdgeTransport.exe viene calcolato come il valore più basso tra il 71% della memoria fisica totale e un valore inferiore del 4% al valore del livello alto.

Se l'utilizzo della memoria da parte del processo EdgeTransport.exe è superiore al livello normale specificato, viene imposta la funzione di *Garbage Collection*. Garbage Collection è un processo che consente di verificare la presenza di oggetti non utilizzati in memoria e recuperare la memoria utilizzata da essi.

Exchange mantiene una cronologia di utilizzo memoria del processo EdgeTransport.exe. Se l'utilizzo delle risorse non torna al livello normale per un numero specifico di intervalli di polling, denominato profondità della cronologia, Exchange inizia a rifiutare i messaggi in arrivo finché l'utilizzo delle risorse non torna al livello normale. Per impostazione predefinita, la profondità della cronologia per l'utilizzo della memoria di EdgeTransport.exe è di 30 intervalli di polling.

Inizio pagina

## Memoria utilizzata da tutti i processi

Per impostazione predefinita, il livello alto di utilizzo della memoria da parte di tutti i processi è il 94% della memoria fisica totale. Questo valore non include la memoria virtuale disponibile sull'unità disco rigido nel file di paging.

Quando viene raggiunto il livello di utilizzo della memoria specificato, si verifica una *disidratazione dei messaggi*. La disidratazione dei messaggi è l'azione di rimozione degli elementi non necessari di messaggi in coda memorizzati nella cache. I messaggi completi vengono memorizzati nella cache per migliorare le prestazioni. La rimozione dalla memoria del contenuto MIME dei messaggi in coda riduce la quantità di memoria utilizzata a spese di una maggiore latenza, perché i messaggi vengono letti direttamente dal database della coda dei messaggi. Per impostazione predefinita, la disidratazione dei messaggi è abilitata.

Inizio pagina

## Indica il numero di messaggi contenuti nella coda di invio

La coda di invio viene associata al servizio di trasporto sui server Cassette postali e Trasporto Edge di Exchange 2013. Il classificatore elabora ogni messaggio della coda di invio. La classificazione comporta la collocazione dei messaggi in una coda di recapito. Per ulteriori informazioni, vedere [Flusso di posta](mail-flow-exchange-2013-help.md) e [Code](queues-exchange-2013-help.md). Un numero elevato di messaggi nella coda di invio indica che il classificatore sta riscontrando problemi durante l'elaborazione dei messaggi.

Quando la coda di invio è in stato di congestione, il server di Exchange inizia a limitare la larghezza di banda delle connessioni in ingresso ritardando il riconoscimento dei messaggi in arrivo. Exchange riduce la frequenza del flusso dei messaggi in entrata mediante il tarpitting che causa un ritardo nei comandi **MAIL FROM**. Se la condizione di congestione della coda di invio continua, Exchange aumenta gradualmente il ritardo di tarpitting. Quando l'utilizzo della coda di invio torna ad essere normale, Exchnage inizia a ridurre gradualmente il ritardo di riconoscimento e torna al funzionamento normale. Per impostazione predefinita, Exchange inizia a ritardare di 10 secondi il riconoscimento dei messaggi in caso di congestione della coda di invio. Se la coda di invio continua ad essere in stato di congestione, il ritardo viene aumentato a incrementi di 5 secondi fino a 55 secondi.

Exchange mantiene una cronologia relativa all'utilizzo della coda di invio. Se l'utilizzo della coda di invio non torna al livello normale per un numero specifico di intervalli di polling, denominato profondità della cronologica, Exchange arresta il ritardo di tarpitting e inizia a rifiutare i messaggi in arrivo finché l'utilizzo della coda di invio non torna al livello normale. Per impostazione predefinita, la profondità della cronologia per la coda di invio è di 300 intervalli di polling.

## Azioni effettuate dal trasporto di Exchange quando una risorsa è in stato di congestione

Nella tabella seguente sono riportate le azioni effettuate dal trasporto di Exchange quando una risorsa specifica è in stato di congestione.

### Azioni della funzione di congestione effettuate dai server di cassette postali e Trasporto Edge in risposta a uno stato di congestione

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Risorsa in stato di congestione</th>
<th>Livello di utilizzo</th>
<th>Azioni intraprese</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Spazio su disco rigido per database della coda messaggi</p></td>
<td><p>Medio</p></td>
<td><ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Spazio su disco rigido per database della coda messaggi</p></td>
<td><p>Alto</p></td>
<td><ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da altri server di Exchange</p></li>
<li><p>Rifiuto dell'invio dei messaggi dai database delle cassette postali da parte del servizio di invio del trasporto alla cassetta postale sui server Cassette postali</p></li>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Spazio su disco rigido per registri delle transazioni del database della coda messaggi</p></td>
<td><p>Medio</p></td>
<td><ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Spazio su disco rigido per registri delle transazioni del database della coda messaggi</p></td>
<td><p>Alto</p></td>
<td><ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da altri server di Exchange</p></li>
<li><p>Rifiuto dell'invio dei messaggi dai database delle cassette postali da parte del servizio di invio del trasporto alla cassetta postale sui server Cassette postali</p></li>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Bucket versione</p></td>
<td><p>Medio</p></td>
<td><p>Introduzione o aumento del ritardo di tarpitting per i messaggi in arrivo. Se viene raggiunto il livello normale per l'intera profondità della cronologia dei bucket versione, effettuare le azioni seguenti:</p>
<ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Bucket versione</p></td>
<td><p>Alto</p></td>
<td><p>Introduzione o aumento del ritardo di tarpitting per i messaggi in arrivo. Se viene raggiunto il livello normale per l'intera profondità della cronologia dei bucket versione, effettuare le azioni seguenti:</p>
<ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da altri server di Exchange</p></li>
<li><p>Rifiuto dell'invio dei messaggi dai database delle cassette postali da parte del servizio di invio del trasporto alla cassetta postale sui server Cassette postali</p></li>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Punto batch</p></td>
<td><p>Medio</p></td>
<td><p>Introduzione o aumento del ritardo di tarpitting per i messaggi in arrivo. Se viene raggiunto il livello normale per l'intera profondità della cronologia dei punti versione, effettuare le azioni seguenti:</p>
<ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Punto batch</p></td>
<td><p>Alto</p></td>
<td><p>Introduzione o aumento del ritardo di tarpitting per i messaggi in arrivo. Se viene raggiunto il livello normale per l'intera profondità della cronologia dei punti versione, effettuare le azioni seguenti:</p>
<ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da altri server di Exchange</p></li>
<li><p>Rifiuto dell'invio dei messaggi dai database delle cassette postali da parte del servizio di invio del trasporto alla cassetta postale sui server Cassette postali</p></li>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Memoria utilizzata dal processo EdgeTransport.exe</p></td>
<td><p>Medio</p></td>
<td><ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
<li><p>Imposizione della garbage collection</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Memoria utilizzata dal processo EdgeTransport.exe</p></td>
<td><p>Alto</p></td>
<td><ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da altri server di Exchange</p></li>
<li><p>Rifiuto dell'invio dei messaggi dai database delle cassette postali da parte del servizio di invio del trasporto alla cassetta postale sui server Cassette postali</p></li>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Memoria utilizzata da tutti i processi</p></td>
<td><p>Medio</p></td>
<td><ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
<li><p>Imposizione della garbage collection</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Memoria utilizzata da tutti i processi</p></td>
<td><p>Alto</p></td>
<td><ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da altri server di Exchange</p></li>
<li><p>Rifiuto dell'invio dei messaggi dai database delle cassette postali da parte del servizio di invio del trasporto alla cassetta postale sui server Cassette postali</p></li>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
<li><p>Eliminazione della cache DNS dalla memoria</p></li>
<li><p>Avvio disidratazione dei messaggi</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Indica il numero di messaggi contenuti nella coda di invio</p></td>
<td><p>Medio</p></td>
<td><p>Introduzione o aumento del ritardo di tarpitting per i messaggi in arrivo. Se viene raggiunto il livello normale per l'intera profondità della cronologia della coda di invio, effettuare le azioni seguenti:</p>
<ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
<li><p>Imposizione della garbage collection</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Indica il numero di messaggi contenuti nella coda di invio</p></td>
<td><p>Alto</p></td>
<td><p>Introduzione o aumento del ritardo di tarpitting per i messaggi in arrivo. Se viene raggiunto il livello normale per l'intera profondità della cronologia della coda di invio, effettuare le azioni seguenti:</p>
<ul>
<li><p>Rifiuto dei messaggi in arrivo provenienti da altri server di Exchange</p></li>
<li><p>Rifiuto dell'invio dei messaggi dai database delle cassette postali da parte del servizio di invio del trasporto alla cassetta postale sui server Cassette postali</p></li>
<li><p>Rifiuto dei messaggi in arrivo provenienti da server non Exchange</p></li>
<li><p>Rifiuto dell'invio di messaggi dalle directory di prelievo e riproduzione</p></li>
<li><p>Eliminazione della cache DNS dalla memoria</p></li>
<li><p>Avvio disidratazione dei messaggi</p></li>
</ul></td>
</tr>
</tbody>
</table>


Inizio pagina

## Opzioni di configurazione della funzione di congestione nel file EdgeTransport.exe.config

Tutte le opzioni di configurazione per la funzione di congestione sono disponibili nel file di configurazione dell'applicazione XML %ExchangeInstallPath%Bin\\EdgeTransport.exe.config.


> [!WARNING]
> Queste impostazioni sono elencate solo a titolo di riferimento. Si sconsiglia qualsiasi modifica alle impostazioni della funzione di congestione nel file EdgeTransport.exe.config. Eventuali modifiche apportate alle impostazioni della funzione di congestione possono compromettere le prestazioni o risultare in una perdita di dati. Si consiglia di ricercare e correggere la causa di qualsiasi condizione di congestione che può verificarsi.



### Opzioni di configurazione dell'opzione di congestione

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome chiave</th>
<th>Valore predefinito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>EnableResourceMonitoring</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>ResourceMonitoringInterval</em></p></td>
<td><p><code>00:00:02</code> (2 secondi)</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. Questo valore indica che verrà utilizzata la formula predefinita.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. Questo valore indica che il valore effettivo è inferiore del 2% al valore di <em>PercentageDatabaseDiskSpaceUsedHighThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. Questo valore indica che il valore effettivo è inferiore del 2% al valore di <em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. Questo valore indica che verrà utilizzata la formula predefinita.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. Questo valore indica che il valore effettivo è inferiore del 2% al valore di <em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. Questo valore indica che il valore effettivo è inferiore del 2% al valore di <em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedHighThreshold</em></p></td>
<td><p>0. Questo valore indica che verrà utilizzato il calcolo predefinito.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePrivateBytesUsedMediumThreshold</em></p></td>
<td><p>0. Questo valore indica che il valore effettivo è inferiore del 2% al valore di <em>PercentagePrivateBytesUsedHighThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedNormalThreshold</em></p></td>
<td><p>0. Questo valore indica che il valore effettivo è inferiore del 2% al valore di <em>PercentagePrivateBytesUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsHighThreshold</em></p></td>
<td><p>200</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsMediumThreshold</em></p></td>
<td><p>120</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsNormalThreshold</em></p></td>
<td><p>80</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsHistoryDepth</em></p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointHighThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointMediumThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointNormalThreshold</em></p></td>
<td><p>1000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointUseCostForPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointBatchSize</em></p></td>
<td><p>40</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointBatchTimeout</em></p></td>
<td><p><code>00:00:00.100</code> (0,1 secondi)</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointItemExpiryInterval</em></p></td>
<td><p><code>00:05:00</code> (5 minuti)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPBaseThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:00</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPMaxThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:55</code> (55 secondi)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPStepThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:05</code> (5 secondi)</p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPStartThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:10</code> (10 secondi)</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePhysicalMemoryUsedLimit</em></p></td>
<td><p>94</p></td>
</tr>
<tr class="odd">
<td><p><em>DehydrateMessagesUnderMemoryPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateBytesHistoryDepth</em></p></td>
<td><p>30</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueHighThreshold</em></p></td>
<td><p>10000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueMediumThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueNormalThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Informazioni sulla registrazione della funzione di congestione

Nell'elenco seguente vengono descritte le voci del registro eventi generate da eventi specifici della funzione di congestione in Exchange:

  - **Voce del registro eventi relativa a un aumento del livello di utilizzo delle risorse**
    
    Tipo evento: Errore
    
    Origine evento: MSExchangeTransport
    
    Categoria evento: Gestione risorse
    
    ID evento: 15004
    
    Descrizione: Pressione risorsa aumentata da *Livello di utilizzo precedente* a *Livello di utilizzo corrente*.

  - **Voce del registro eventi relativa a una diminuzione del livello di utilizzo delle risorse**
    
    Tipo evento: Informazioni
    
    Origine evento: MSExchangeTransport
    
    Categoria evento: Gestione risorse
    
    ID evento: 15005
    
    Descrizione: Pressione risorsa diminuita da *Livello di utilizzo precedente* a *Livello di utilizzo corrente*.

  - **Voce del registro eventi per spazio su disco insufficiente**
    
    Tipo evento: Errore
    
    Origine evento: MSExchangeTransport
    
    Categoria evento: Gestione risorse
    
    ID evento: 15006
    
    Descrizione: Messaggi rifiutati dal servizio di trasporto di Microsoft Exchange poiché lo spazio su disco è inferiore alla soglia configurata. È probabile che sia richiesta un'azione amministrativa per liberare spazio per consentire al servizio di continuare a funzionare.

  - **Voce del registro eventi per memoria insufficiente**
    
    Tipo evento: Errore
    
    Origine evento: MSExchangeTransport
    
    Categoria evento: Gestione risorse
    
    ID evento: 15007
    
    Descrizione: Il servizio di trasporto di Microsoft Exchange rifiuta l'invio di messaggi. Il servizio continua a consumare una quantità di memoria superiore alla soglia configurata. È probabile che sia necessario riavviare il servizio per consentirne il normale funzionamento.

Inizio pagina


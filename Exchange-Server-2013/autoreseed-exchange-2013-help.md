---
title: 'AutoReseed: Exchange 2013 Help'
TOCTitle: AutoReseed
ms:assetid: 61f9a8be-070e-4c62-b505-52644fcff0c5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn789209(v=EXCHG.150)
ms:contentKeyID: 62523890
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# AutoReseed

 

_**Si applica a:** Exchange Server 2013 SP1_

_**Ultima modifica dell'argomento:** 2015-03-09_

Reseeding automatico o reseeding automatico, è una funzionalità che è la sostituzione per le quali è normalmente gestito dall'amministratore di azione in risposta a un errore del disco, evento danneggiamento dei database o altro problema che richiede un reseeding di una copia del database. Reseeding automatico è progettato per il ripristino automatico ridondanza del database dopo un errore del disco con dischi di riserva sottoposti a provisioning nel sistema.

## Panoramica di Autoreseed

Nella configurazione del reseeding automatico, viene utilizzata una struttura di presentazione dell'archiviazione standardizzata e l'amministratore stabilisce il punto di partenza. Il reseeding automatico consiste nel ripristinare la ridondanza il più presto possibile in seguito ad un errore di un'unità. Per questo è necessaria la pre-associazione di un gruppo di volumi (inclusi i volumi di riserva) e i database che utilizzano punti di montaggio. Nel caso di un errore del disco in cui il disco non è più disponibile per il sistema operativo, o non è più accessibile in scrittura, il sistema assegna un volume di riserva e viene effettuato il reseeding automatico delle copie del database danneggiate.

1.  Microsoft Exchange di servizio di replica scannerizza periodicamente le copie che hanno lo stato di FailedAndSuspended. Se tutte le copie del database in un volume configurato per AutoReseed sono in uno stato di FailedandSuspended per 15 minuti consecutive, viene avviato il flusso di lavoro di reseeding automatico.

2.  Reseeding automatico tenterà di riprendere la copia non riuscita e sospesa fino a tre volte con una sospensione di 5 minuti tra ogni tentativo. In alcuni casi, dopo la ripresa di una copia del database FailedandSuspended, la copia rimane nello stato Failed. Questo problema può verificarsi per diversi motivi, in modo che questo passaggio è progettato per gestire i casi. Reseeding automatico verrà automaticamente sospendere una copia del database che è stata eseguita per 10 minuti consecutivi mantenere il flusso di lavoro in esecuzione. Se le azioni di sospensione e ripresa non genera una copia del database integro, il flusso di lavoro prosegue.

3.  Quando viene rilevato una copia con tale stato, vengono eseguiti alcuni controlli dei prerequisiti. Ad esempio, verifica che un copia di riserva disco sia disponibile e che il database e i relativi file di registro sono configurati nello stesso volume e nelle posizioni appropriate che soddisfano le convenzioni di denominazione necessari.

4.  Se i controlli dei prerequisiti hanno esito positivo, il Reclaimer disco funzione all'interno del servizio di replica di Microsoft Exchange assegna, riassocia e formatta un copia di riserva disco in base alla sequenza temporale nella tabella seguente. Reseeding automatico tenterà di assegnare un volume di riserva fino a 5 volte, con 1 ora inattivo tra ogni prova.

5.  Dopo che è stata assegnata una copia di riserva, reseeding automatico eseguirà un'operazione InPlaceSeed utilizzando SafeDeleteExistingFiles seeding switch. Tutti i database che sono stati sul disco interessato vengono nuovamente eseguito il seeding utilizzando la copia attiva del database come dell'origine del seeding.

6.  Una volta completato il seeding, il servizio di replica di Microsoft Exchange verifica che la nuova copia per cui è stato effettuato il seeding sia integra.

Dopo che tutti i tentativi sono esauriti, interrompe il flusso di lavoro. Se dopo 3 giorni, la copia del database non è ancora FailedandSuspended, lo stato del flusso di lavoro viene reimpostato e riavvia dal passaggio 1. Questo comportamento reset/resume è utile (e intenzionale) poiché potrebbero essere necessari alcuni giorni per sostituire un disco, controller e così via.

A questo punto, se l'errore è stato un errore del disco, sarebbe necessario un intervento manuale di un operatore o amministratore per rimuovere e sostituire il disco danneggiato e riconfigurarlo come riserva.

Il reseeding automatico viene configurato utilizzando tre proprietà del DAG. Due delle proprietà riguardano i due punti di montaggio in uso. Exchange 2013 sfrutta il fatto che Windows Server consente più punti di montaggio per volume. La proprietà *AutoDagVolumesRootFolderPath* riguarda il punto di montaggio contenente tutti i volumi disponibili. Include anche i volumi che ospitano i database e i volumi di riserva. La proprietà *AutoDagDatabasesRootFolderPath* riguarda il punto di montaggio contenente i database. Una terza proprietà del DAG, *AutoDagDatabaseCopiesPerVolume*, viene utilizzata per configurare il numero di copie del database per volume.

Qui di seguito è illustrato un esempio di configurazione di reseeding automatico.

**Esempio di configurazione del reseeding automatico**

![Configurazione automatica di reseeding di esempio](images/Dn789209.e3af7306-f5b4-4ec4-9ccf-222ec452699b(EXCHG.150).gif "Configurazione automatica di reseeding di esempio")

In questo esempio, ci sono tre volumi, due dei quali contengono i database (VOL1 e VOL2) e uno dei quali è un volume di riserva vuoto, formattato (VOL3).

Per configurare il reseeding automatico:

1.  Tutti e tre i volumi sono montati sotto un singolo punto di montaggio. In questo esempio, viene utilizzato un punto punto di montaggio di C:\\ExchVols. Questo punto rappresenta la directory utilizzata per ottenere l'archiviazione per i database di Exchange.

2.  La directory principale dei database delle cassette postali viene montata come un altro punto di montaggio. In questo esempio, viene utilizzato un punto di montaggio di C:\\ExchDBs. Quindi, viene creata una struttura della directory affinché venga creata una directory principale per il database e due sottodirectory sotto la directory principale: un file di database e uno per i file di registro.

3.  Vengono creati i database. L'esempio sopra riportato illustra una struttura semplice che utilizza un singolo database per volume. Pertanto, VOL1 dispone di tre directory: la directory principale e due sottodirectory (una per il file di database di MDB1 e una per i relativi registri). Sebbene non vengano descritti nell'immagine di esempio, ci sarebbero altre tre directory su VOL2: la directory principale e, sotto di essa, una directory per il file di database di MDB2 e una per i relativi file di registro.

In questa configurazione, se MDB1 o MDB2 registrano un errore, viene automaticamente eseguito il reseeding di una copia del database danneggiato su VOL3.

## Disk Reclaimer

Il componente AutoReseed che alloca e formatta dischi di ricambio viene chiamato *Disk Reclaimer*. Il componente Disk Reclaimer formatta automaticamente dischi di ricambio in preparazione per il reseeding automatico a diversi livelli, a seconda dello stato del disco. Affinché Disk Reclaimer formatti un disco, devono essere soddisfatte determinate condizioni:

  - Disk Reclaimer deve essere attivato. È attivato per impostazione predefinita, ma può essere disattivato utilizzando [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/it-it/library/dd297934\(v=exchg.150\)).

  - Il volume deve avere un punto di installazione nel percorso dei volumi radice (per impostazione predefinita, C:\\ExchangeVolumes).

  - Il volume non deve avere punti di installazione nel percorso dei volumi del database (per impostazione predefinita, C:\\ExchangeDatabases).

  - Se il volume contiene file, nessuno dei file deve essere toccato per 24 ore.

Oltre alle precedenti condizioni, Disk Reclaimer proverà a formattare un dato volume solo una volta al giorno. Nella tabella seguente viene descritto il comportamento di formattazione di Disk Reclaimer.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Stato del disco e copia del database</th>
<th>Intervallo di formattazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Disco non formattato o formattato ma vuoto oppure formattato ma contenente file che sono stati toccati durante le 24 ore e ci sono copie del database attive integre nel sito di Active Directory locale che possono essere usate come origine di seeding.</p></td>
<td><p>1 giorno</p></td>
</tr>
<tr class="even">
<td><p>Disco non formattato o formattato ma vuoto oppure formattato ma contenente file che sono stati toccati durante le 24 ore, ma non ci sono copie del database attive integre nel sito di Active Directory locale che possono essere usate come origine di seeding.</p></td>
<td><p>2 giorni</p></td>
</tr>
<tr class="odd">
<td><p>Disco non formattato o formattato ma vuoto oppure formattato ma contenente file che sono stati toccati durante le 24 ore e ci sono copie del database attive integre nel sito di Active Directory locale che possono essere usate come origine di seeding, ma non ci sono file sconosciuti fuori dal file del database (file EDB) e file di registro.</p></td>
<td><p>2 settimane</p></td>
</tr>
<tr class="even">
<td><p>Disco non formattato o formattato ma vuoto oppure formattato ma contenente file che sono stati toccati durante le 24 ore e ci sono copie del database attive integre nel sito di Active Directory locale che possono essere usate come origine di seeding, ma ci sono uno o più file del database (file EDB) per i database non presenti in Active Directory.</p></td>
<td><p>2 settimane</p></td>
</tr>
</tbody>
</table>


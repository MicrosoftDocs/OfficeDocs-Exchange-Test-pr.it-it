---
title: 'Messaging records management errori ed eventi: Exchange 2013 Help'
TOCTitle: Messaging records management errori ed eventi
ms:assetid: 8bc3f5ae-403b-45af-86c1-b2fccab34e63
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb310783(v=EXCHG.150)
ms:contentKeyID: 51407391
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Messaging records management errori ed eventi

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Gestione record di messaggistica genera eventi che è possibile visualizzare nel Visualizzatore eventi. Questa operazione consente di risolvere i problemi e di verificare le prestazioni dell'Assistente cartelle gestite. Il Visualizzatore eventi registra i seguenti tipi di eventi, nell'ordine di importanza specificato:

1.  Eventi di errore

2.  Eventi di avviso

3.  Eventi informativi

## Errori ed eventi di Gestione record di messaggistica

Le seguenti tabelle forniscono un elenco di eventi che è possibile utilizzare per risolvere i problemi di Gestione record di messaggistica. I tipi di registrazione comprendono:

  - Eventi contrassegnati come **LogAlways** che vengono sempre registrati singolarmente.

  - Eventi contrassegnati come **LogPeriodic** che vengono registrati solo una volta ogni cinque minuti e non ogni volta che si verificano. Ciò consente di evitare un numero di voci di registro eccessivo.

### Eventi di Gestione record di messaggistica della categoria Assistente cartelle gestite

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>ID evento</strong></th>
<th><strong>Categoria</strong></th>
<th><strong>Tipo evento</strong></th>
<th><strong>Registrazione</strong></th>
<th><strong>Valore o descrizione</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10003</p></td>
<td><p>Assistente cartelle gestite</p></td>
<td><p>Errore</p></td>
<td><p>LogPeriodic</p></td>
<td><p>Impossibile ottenere l'oggetto di configurazione server da Active Directory. &lt;<em>Dettagli eccezione</em>&gt;. Verificare che non siano presenti problemi di connettività di rete del controller di dominio e che la configurazione DNS sia corretta.</p></td>
</tr>
<tr class="even">
<td><p>10004</p></td>
<td><p>Assistente cartelle gestite</p></td>
<td><p>Errore</p></td>
<td><p>LogAlways</p></td>
<td><p>Il criterio di conservazione non verrà applicato alla cartella &lt;<em>cartella</em>&gt; nella cassetta postale &lt;<em>cassetta postale</em>&gt;. Impossibile elaborare l'impostazione del contenuto gestito &lt;<em>impostazioni del contenuto</em>&gt; per la cartella gestita &lt;<em>cartella gestita</em>&gt;. Il valore di RetentionAction è MoveToFolder ma non è stata specificata una cartella di destinazione. Specificare una cartella di destinazione.</p></td>
</tr>
<tr class="odd">
<td><p>10005</p></td>
<td><p>Assistente cartelle gestite</p></td>
<td><p>Errore</p></td>
<td><p>LogAlways</p></td>
<td><p>Il criterio di conservazione non verrà applicato alla cartella &lt;<em>cartella</em>&gt; nella cassetta postale &lt;<em>cassetta postale</em>&gt;. Impossibile elaborare le impostazioni del contenuto gestito &lt;<em>impostazioni relative al contenuto</em>&gt; per la cartella gestita &lt;<em>cartella gestita</em>&gt;. Il valore di RetentionAction è MoveToFolder ma la cartella di destinazione &lt;<em>cartella</em>&gt; è identica alla cartella di origine &lt;<em>cartella</em>&gt;. Specificare una cartella di destinazione diversa dalla cartella di origine.</p></td>
</tr>
<tr class="even">
<td><p>10009</p></td>
<td><p>Assistente cartelle gestite</p></td>
<td><p>Errore</p></td>
<td><p>LogAlways</p></td>
<td><p>Elaborazione di tutti i database ignorata nel server locale. Impossibile leggere i parametri del registro di controllo da Active Directory. L'operazione verrà ripetuta in seguito nella finestra della pianificazione. Database corrente: &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10010</p></td>
<td><p>Assistente cartelle gestite</p></td>
<td><p>Errore</p></td>
<td><p>LogAlways</p></td>
<td><p>Elaborazione di tutti i database ignorata nel server locale. Il registro di controllo è abilitato, ma manca il percorso del registro di controllo in Active Directory. L'operazione verrà ripetuta in seguito nella finestra della pianificazione. Database corrente: &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10011</p></td>
<td><p>Assistente cartelle gestite</p></td>
<td><p>Errore</p></td>
<td><p>LogAlways</p></td>
<td><p>Impossibile configurare il registro di controllo. L'elaborazione del database corrente verrà interrotta: '%1'. L'operazione verrà ripetuta in seguito nella finestra della pianificazione. Dettagli eccezione: &lt;<em>dettagli</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10012</p></td>
<td><p>Assistente cartelle gestite</p></td>
<td><p>Errore</p></td>
<td><p>LogAlways</p></td>
<td><p>Impossibile scrivere nel registro di controllo. L'elaborazione del database corrente verrà interrotta: &lt;<em>database</em>&gt;. L'operazione di scrittura nel registro di controllo verrà ripetuta in seguito nella finestra della pianificazione. Dettagli eccezione: &lt;<em>dettagli</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10017</p></td>
<td><p>Assistente cartelle gestite</p></td>
<td><p>Errore</p></td>
<td><p>LogAlways</p></td>
<td><p>Si è verificata un'eccezione dell'Assistente cartelle gestite durante l'elaborazione della cassetta postale: &lt;<em>cassetta postale</em>&gt; Cartella: Nome: &lt;<em>nome cartella</em>&gt; ID: &lt;<em>ID cartella</em>&gt; Elemento: ID: &lt;<em>ID</em>&gt;. Eccezione: &lt;<em>eccezione</em>&gt;.</p></td>
</tr>
</tbody>
</table>


### Eventi di MRM nella categoria Assistenti

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>ID evento</strong></th>
<th><strong>Categoria</strong></th>
<th><strong>Tipo evento</strong></th>
<th><strong>Registrazione</strong></th>
<th><strong>Valore o descrizione</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9004</p></td>
<td><p>Assistenti</p></td>
<td><p>Avviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. &lt;<em>servizio</em>&gt; non è stato in grado di elaborare la cassetta postale &lt;<em>cassetta postale</em>&gt;. L'errore è stato causato dalla seguente eccezione: &lt;<em>eccezione</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9014</p></td>
<td><p>Assistenti</p></td>
<td><p>Avviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. Impossibile elaborare le modifiche alla pianificazione. L'errore è stato causato dalla seguente eccezione: &lt;<em>eccezione</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9017</p></td>
<td><p>Assistenti</p></td>
<td><p>Informazioni</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. Inserimento in corso di un intervallo di tempo pianificato da parte di &lt;<em>servizio</em>&gt; per il database &lt;<em>database</em>&gt;. Sono presenti &lt;<em>numero</em>&gt; cassette postali da elaborare.</p></td>
</tr>
<tr class="even">
<td><p>9018</p></td>
<td><p>Assistenti</p></td>
<td><p>Informazioni</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. Chiusura in corso di un intervallo di tempo pianificato da parte di &lt;<em>servizio</em>&gt; per il database &lt;<em>database</em>&gt;. Sono state elaborate correttamente &lt;<em>numero</em>&gt; di &lt;<em>numero</em>&gt; cassette postali. &lt;<em>numero</em>&gt; cassette postali sono state ignorate a causa di errori. &lt;<em>numero</em>&gt; sono state elaborate separatamente. &lt;<em>numero</em>&gt; non sono state elaborate a causa di tempo insufficiente.</p>

> [!NOTE]
> Alla prossima esecuzione, l'Assistente cartelle gestite riprenderà l'operazione da dove era stata interrotta.


</td>
</tr>
<tr class="odd">
<td><p>9019</p></td>
<td><p>Assistenti</p></td>
<td><p>Avviso</p></td>
<td><p>LogPeriodic</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. Impossibile salvare l'avanzamento per &lt;<em>servizio</em>&gt; nel database &lt;<em>database</em>&gt;. (L'assistente non è stato in grado di eseguire il salvataggio nel punto in cui si è interrotto in modo da poter riprendere l'operazione da quel punto al suo successivo riavvio). L'errore è stato causato dalla seguente eccezione: &lt;<em>eccezione</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9020</p></td>
<td><p>Assistenti</p></td>
<td><p>Avviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. Impossibile avviare &lt;<em>nome assistente</em>&gt; per il database &lt;<em>database</em>&gt;. L'errore è stato causato dalla seguente eccezione: &lt;<em>eccezione</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9021</p></td>
<td><p>Assistenti</p></td>
<td><p>Informazioni</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. Elaborazione in corso di una richiesta su richiesta da parte di &lt;<em>servizio</em>&gt; per il database &lt;<em>database</em>&gt;. Sono presenti &lt;<em>numero</em>&gt; cassette postali da elaborare.</p></td>
</tr>
<tr class="even">
<td><p>9022</p></td>
<td><p>Assistenti</p></td>
<td><p>Informazioni</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. Richiesta su richiesta da parte di &lt;<em>servizio</em>&gt; per il database &lt;<em>database</em>&gt; completata. Sono state elaborate correttamente &lt;<em>numero</em>&gt; di &lt;<em>numero</em>&gt; cassette postali. &lt;<em>numero</em>&gt; cassette postali sono state ignorate a causa di errori.</p></td>
</tr>
<tr class="odd">
<td><p>9023</p></td>
<td><p>Assistenti</p></td>
<td><p>Avviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. &lt;<em>servizio</em>&gt; non è riuscito ad avviare l'elaborazione dell'intervallo di tempo nel database &lt;<em>database</em>&gt;. L'errore è stato causato dalla seguente eccezione: &lt;<em>eccezione</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9025</p></td>
<td><p>Assistenti</p></td>
<td><p>Informazioni</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. &lt;<em>servizio</em>&gt; ha ignorato &lt;<em>numero</em>&gt; cassette postali nel database &lt;<em>database</em>&gt;. Cassette postali: &lt;<em>cassette postali</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9026</p></td>
<td><p>Assistenti</p></td>
<td><p>Avviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. &lt;<em>servizio</em>&gt; non è riuscito ad avviare l'elaborazione a richiesta nel database &lt;<em>database</em>&gt;. L'errore è stato causato dalla seguente eccezione: &lt;<em>eccezione</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9027</p></td>
<td><p>Assistenti</p></td>
<td><p>Errore</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. &lt;<em>servizio</em>&gt; ha causato per &lt;<em>numero</em>&gt; volte l'arresto del processo durante l'elaborazione della cassetta postale &lt;<em>cassetta postale</em>&gt; nel database &lt;<em>database</em>&gt;. Questa cassetta postale non verrà più elaborata nell'intervallo di tempo richiesto o nella richiesta su richiesta. L'errore è stato causato dalla seguente eccezione: &lt;<em>eccezione</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9028</p></td>
<td><p>Assistenti</p></td>
<td><p>Avviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. &lt;<em>servizio</em>&gt; ha causato per &lt;<em>numero</em>&gt; volte l'arresto del processo durante l'elaborazione della cassetta postale &lt;<em>cassetta postale</em>&gt; nel database &lt;<em>database</em>&gt;. L'errore è stato causato dalla seguente eccezione: &lt;<em>eccezione</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9033</p></td>
<td><p>Assistenti</p></td>
<td><p>Avviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. Richiesta su richiesta di &lt;<em>servizio</em>&gt; per il database &lt;<em>database</em>&gt; ricevuta. Tuttavia non sono presenti cassette postali da elaborare.</p></td>
</tr>
<tr class="odd">
<td><p>9034</p></td>
<td><p>Assistenti</p></td>
<td><p>Informazioni</p></td>
<td><p>LogAlways</p></td>
<td><p>Il servizio &lt;<em>servizio</em>&gt; ha interrotto le operazioni basate sull'ora per l'Assistente cartelle gestite nel database &lt;<em>database</em>&gt;.</p></td>
</tr>
<tr class="even">
<td><p>9035</p></td>
<td><p>Assistenti</p></td>
<td><p>Avviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Il servizio &lt;<em>servizio</em>&gt;. &lt;<em>nome assistente</em>&gt; non è stato in grado di elaborare &lt;<em>numero</em>&gt; cassette postali a causa di tempo insufficiente.</p></td>
</tr>
<tr class="odd">
<td><p>9037</p></td>
<td><p>Assistenti</p></td>
<td><p>Errore</p></td>
<td><p>LogAlways</p></td>
<td><p>Servizio &lt;<em>servizio</em>&gt;. Si è verificata un'eccezione durante l'elaborazione di una RPC. Metodo: &lt;<em>metodo</em>&gt;, Eccezione: &lt;<em>eccezione</em>&gt;</p></td>
</tr>
</tbody>
</table>


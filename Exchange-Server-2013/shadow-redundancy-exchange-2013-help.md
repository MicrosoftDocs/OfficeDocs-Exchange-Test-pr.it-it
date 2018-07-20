---
title: 'Ridondanza shadow: Exchange 2013 Help'
TOCTitle: Ridondanza shadow
ms:assetid: a40dbe61-2a18-48a8-b2e0-4e81a6678d11
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351027(v=EXCHG.150)
ms:contentKeyID: 50481319
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ridondanza shadow

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

La ridondanza shadow è stata introdotta in Microsoft Exchange Server 2010 per fornire copie ridondanti dei messaggi prima che siano recapitati alle cassette postali. In Exchange 2010, la ridondanza shadow ritardava l'eliminazione di un messaggio dal database di trasporto su un server di trasporto fino a quando il server non aveva verificato che l'hop successivo avesse completato il percorso di recapito del messaggio. Se l'hop successivo restituiva un errore prima di segnalare l'effettivo recapito al server di trasporto, quest'ultimo rinviava il messaggio a tale hop successivo. I server Exchange 2010 utilizzavano il verbo XSHADOW per annunciare il loro supporto per la ridondanza shadow. Se un server SMTP non supportava la ridondanza shadow, Exchange 2010 utilizzava una conferma ritardata basata su un intervallo di tempo configurato sul connettore di ricezione per creare una copia ridondante del messaggio.

Il principale miglioramento alla ridondanza shadow in Microsoft Exchange Server 2013 riguarda il server di trasporto, che ora crea una copia ridondante di qualunque messaggio ricevuto prima di dare atto della ricezione corretta del messaggio al server di invio. Il supporto o la mancanza di supporto del server di invio per la ridondanza shadow non è importante. Questo aiuta a garantire che tutti i messaggi nella pipeline di trasporto di Exchange 2013 siano resi ridondanti durante il transito. Se Exchange 2013 determina che il messaggio originale è andato perso nel transito, viene recapitata la copia ridondante del messaggio.

**Sommario**

Shadow redundancy components

Requirements for shadow redundancy

Shadow redundancy is enabled by default

How shadow messages are created

SMTP timeouts

How shadow messages are maintained

Message processing after an outage

## Componenti della ridondanza shadow

Nella tabella seguente sono descritti i componenti della ridondanza shadow. In questo argomento vengono utilizzati i seguenti termini:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Termine</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Server di trasporto</p></td>
<td><p>Un server di Exchange con code dei messaggi, responsabile del routing dei messaggi. In Exchange 2013, un server di trasporto è un server Cassette postali (il servizio Trasporto sul server Cassette postali).</p></td>
</tr>
<tr class="even">
<td><p>Database di trasporto</p></td>
<td><p>Il database della coda dei messaggi su un server di trasporto di Exchange 2013. Anche le code shadow e Safety Net sono archiviate nel database di trasporto.</p></td>
</tr>
<tr class="odd">
<td><p>Limite di disponibilità elevata del trasporto</p></td>
<td><p>Un gruppo di disponibilità del database (DAG) in ambienti DAG, oppure un sito Active Directory in ambienti non DAG. Quando sul server trasporto arriva un messaggio nel limite di disponibilità elevata del trasporto, Exchange prova a mantenere due copie ridondanti del messaggio sui server di trasporto interni al limite. Quando un messaggio lascia il limite di disponibilità elevata del trasporto, Exchange interrompe la gestione delle copie ridondanti del messaggio.</p></td>
</tr>
<tr class="even">
<td><p>Messaggio principale</p></td>
<td><p>Il messaggio inviato alla pipeline di trasporto per il recapito.</p></td>
</tr>
<tr class="odd">
<td><p>Messaggio shadow</p></td>
<td><p>La copia ridondante del messaggio che il server shadow gestisce fino alla conferma che il messaggio primario è stato correttamente elaborato dal server primario.</p></td>
</tr>
<tr class="even">
<td><p>Server primario</p></td>
<td><p>Il server di trasporto che sta attualmente elaborando il messaggio primario.</p></td>
</tr>
<tr class="odd">
<td><p>Server shadow</p></td>
<td><p>Il server di trasporto contenente il messaggio shadow per il server primario. Un server di trasporto potrebbe essere il server primario per alcuni messaggi e il server shadow per altri messaggi.</p></td>
</tr>
<tr class="even">
<td><p>Coda shadow</p></td>
<td><p>La coda di recapito dove il server shadow archivia i messaggi shadow. Per i messaggi con più destinatari, ogni hop successivo per il messaggio primario richiede code shadow separate.</p></td>
</tr>
<tr class="odd">
<td><p>Stato di eliminazione</p></td>
<td><p>Le informazioni mantenute da un server di trasporto per i messaggi shadow che indicano che il messaggio primario è stato elaborato correttamente.</p></td>
</tr>
<tr class="even">
<td><p>Notifica di eliminazione</p></td>
<td><p>La risposta che un server shadow riceve da un server primario che indica che un messaggio shadow è pronto per la rimozione.</p></td>
</tr>
<tr class="odd">
<td><p>Rete sicura</p></td>
<td><p>La versione migliorata di Exchange 2013 del dumpster di trasporto. I messaggi correttamente elaborati o recapitati a un destinatario di cassette postali dal servizio Trasporto su un server Cassette postali sono trasferiti in Safety Net. Per ulteriori informazioni, vedere <a href="safety-net-exchange-2013-help.md">Rete sicura</a>.</p></td>
</tr>
<tr class="even">
<td><p>Shadow Redundancy Manager</p></td>
<td><p>Componente di trasporto che gestisce la ridondanza shadow.</p></td>
</tr>
<tr class="odd">
<td><p>Heartbeat</p></td>
<td><p>Il processo che consente ai server primari e ai server shadow di verificare reciprocamente la disponibilità.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Requisiti per la ridondanza shadow

Anche se può sembrare ovvio, la ridondanza shadow richiede più server Cassette postali di Exchange 2013. Il server Cassette postali può essere autonomo oppure può essere installato insieme al server Accesso client sullo stesso computer.

  - Se il server Cassette postali non è membro di un gruppo di disponibilità del database, gli altri server Cassette postali devono trovarsi nel sito Active Directory locale.

  - Se il server Cassette postali è membro di un gruppo di disponibilità del database, gli altri server Cassette postali devono appartenere allo stesso gruppo. Gli altri server Cassette postali appartenenti al gruppo di disponibilità del database possono trovarsi nel sito Active Directory locale o in un sito Active Directory remoto. Se il gruppo di disponibilità del database si estende su più siti Active Directory, la ridondanza shadow preferisce creare una copia ridondante del messaggio in un sito Active Directory remoto per la resilienza del sito.

Di seguito sono riportate le situazioni in cui la ridondanza shadow non può proteggere i messaggi in transito:

  - Negli ambienti con server di Exchange singolo.

  - Nei gruppi di disponibilità del database con provisioning.

  - Durante l'errore simultaneo di due server di trasporto coinvolti nella ridondanza shadow di un messaggio.

Inizio pagina

## La ridondanza shadow è abilitata per impostazione predefinita

Per impostazione predefinita, la ridondanza shadow è abilitata a livello globale nel servizio Trasporto su tutti i server Cassette postali per mezzo del parametro *ShadowRedundancyEnabled* del cmdlet **Set-TransportConfig**. Per impostazione predefinita, se il servizio Trasporto su un server Cassette postali non può creare una copia ridondante di un messaggio, il messaggio non viene rifiutato. Tuttavia, è possibile configurare Exchange 2013 per rifiutare un messaggio se non viene creata una copia ridondante del messaggio utilizzando il parametro *RejectMessageOnShadowFailure* del cmdlet **Set-TransportConfig**. Il messaggio viene rifiutato con un errore temporaneo, ma il server di invio non può ritrasmettere il messaggio. Il codice di risposta SMTP è `451 4.4.0 Message failed to be made redundant.`. È opportuno configurare Exchange 2013 per rifiutare i messaggi che non possono essere resi ridondanti solo quando l'organizzazione ha a disposizione più server Cassette postali di Exchange 2013.

Nella tabella seguente sono descritti i parametri che consentono la ridondanza shadow.

### Parametri che consentono la ridondanza shadow

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Valore predefinito</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowRedundancyEnabled</em> in <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> consente la ridondanza shadow su tutti i server di trasporto nell'organizzazione.</p></li>
<li><p><code>$false</code> disabilita la ridondanza shadow su tutti i server di trasporto nell'organizzazione.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RejectMessageOnShadowFailure</em> in <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$false</code></p></td>
<td><ul>
<li><p><code>$false</code>   Quando non è possibile creare una copia shadow del messaggio, il messaggio primario viene accettato comunque dai server di trasporto nell'organizzazione. Questi messaggi non sono persistenti in maniera ridondante durante il transito.</p></li>
<li><p><code>$true</code>   Nessun messaggio viene accettato o confermato dai server di trasporto nell'organizzazione finché non è stata correttamente creata una copia shadow del messaggio. Se non è possibile creare una copia shadow del messaggio, il messaggio primario viene rifiutato con un errore temporaneo. Tutti i messaggi nell'organizzazione sono persistenti in maniera ridondante durante il transito.</p>
<p>Questo valore dovrebbe essere impostato su <code>$true</code> solo se sono presenti più server Cassette postali di Exchange 2013 in un gruppo di disponibilità del database o in un sito Active Directory in cui può essere creata una copia shadow del messaggio.</p></li>
</ul>
<p>Questo parametro è significativo solo se <em>ShadowRedundancyEnabled</em> è impostato su <code>$true</code>.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Modalità di creazione dei messaggi shadow

L'obiettivo principale della ridondanza shadow è sempre quello di avere due copie di un messaggio entro un limite di disponibilità elevata del trasporto mentre il messaggio è in transito. Il momento e la posizione di creazione della copia ridondante del messaggio dipendono dalla provenienza e dalla destinazione del messaggio. Esistono tre fattori determinanti principali:

  - Messaggi ricevuti esternamente a un limite di disponibilità elevata del trasporto.

  - Messaggi inviati esternamente a un limite di disponibilità elevata del trasporto.

  - Messaggi ricevuti dal servizio Invio Trasporto cassette postali da un server Cassette postali nel limite di disponibilità elevata del trasporto.

Un *limite di disponibilità elevata del trasporto* corrisponde a uno dei seguenti elementi:

  - Un gruppo di disponibilità del database per i server Cassette postali membri del gruppo. Include un gruppo di disponibilità del database che si estende su più siti di Active Directory.

  - Un sito Active Directory per i server Cassette postali che non appartengono a un gruppo di disponibilità del database.

La ridondanza shadow non tiene mai traccia dei messaggi shadow attraverso un limite di disponibilità elevata del trasporto. Quando un messaggio supera il limite di disponibilità elevata del trasporto, la ridondanza shadow viene avviata o riavviata. In questo modo si riduce il traffico di gestione dei messaggi shadow e si impedisce il rinvio dei messaggi shadow attraverso il limite di disponibilità elevata del trasporto. I server Trasporto Hub di Exchange 2010 rappresentano un caso speciale e sono affrontati più avanti in questo argomento.

## Messaggi ricevuti esternamente a un limite di disponibilità elevata del trasporto

Quando il servizio Trasporto su un server Cassette postali di Exchange 2013 riceve un messaggio esternamente al limite di disponibilità elevata del trasporto, il server Cassette postali non è interessato al supporto della ridondanza shadow da parte del server di invio. Finché la ridondanza shadow è abilitata, il server Cassette postali che riceve il messaggio crea una copia ridondante del messaggio su un altro server Cassette postali nel limite di disponibilità elevata del trasporto prima di dare atto della ricezione del messaggio al server di invio. Ecco un esempio di funzionamento del processo:

![Creazione di messaggi shadow](images/Dd351027.a97d383b-6ae4-458d-af3a-1ac0a41cd52b(EXCHG.150).gif "Creazione di messaggi shadow")

1.  Un server SMTP trasmette un messaggio al servizio Trasporto su un server Cassette postali. Il server Cassette postali è il server primario e il messaggio è il messaggio primario.

2.  Mentre la sessione SMTP originale con il server SMTP è ancora attiva, il servizio Trasporto sul server primario apre una nuova sessione SMTP simultanea con il servizio Trasporto su un server Cassette postali diverso nell'organizzazione per creare una copia ridondante del messaggio.
    
      - Se il server primario è membro di un gruppo di disponibilità del database, si connette a un server Cassette postali diverso nello stesso gruppo. Se il gruppo di disponibilità del database si estende su più siti Active Directory, per impostazione predefinita viene preferito un server Cassette postali in un sito Active Directory diverso. Questa impostazione è controllata dal parametro *ShadowMessagePreference* del cmdlet **Set-TransportService**. Il valore predefinito è `PreferRemote`, ma è possibile cambiarlo in `RemoteOnly` o `LocalOnly`.
    
      - Se il server primario non è membro di un gruppo di disponibilità del database, si connette a un server Cassette postali diverso nello stesso sito Active Directory, indipendentemente dal valore del parametro *ShadowMessagePreference*.

3.  Il server primario trasmette una copia del messaggio al servizio di trasporto sull'altro server Cassette postali, mentre il servizio di trasporto sull'altro server Cassette postali conferma che la copia del messaggio sia stata creata correttamente. La copia del messaggio è il messaggio shadow e il server Cassette postali che lo gestisce è il server shadow per il server primario. Il messaggio esiste in una coda shadow sul server shadow.

4.  Dopo aver ricevuto la conferma dal server shadow, il server primario conferma la ricezione del messaggio primario al server SMTP originale nella sessione SMTP originale e la sessione SMTP viene chiusa.

## Messaggi inviati esternamente a un limite di disponibilità elevata del trasporto

Quando un server di trasporto di Exchange 2013 trasmette un messaggio all'esterno del limite di disponibilità elevata del trasporto e il server SMTP all'altro capo conferma la corretta ricezione del messaggio, il server di trasporto sposta il messaggio in Rete sicura. Non può verificarsi alcun rinvio del messaggio da Safety Net dopo che il messaggio primario è stato trasmesso attraverso il limite di disponibilità elevata del trasporto. Per ulteriori informazioni su Safety Net, vedere [Rete sicura](safety-net-exchange-2013-help.md).

## Messaggi trasmessi all'interno di un limite di disponibilità elevata del trasporto

Il routing dei messaggi è stato ottimizzato in Exchange 2013 in modo che, se la destinazione finale è in un gruppo di disponibilità del database o un sito Active Directory, non siano generalmente richiesti più hop tra il servizio di trasporto sui server Cassette postali nel gruppo di disponibilità del database o nel sito Active Directory. Dopo che il messaggio è stato accettato dal servizio Trasporto su un server Cassette postali nel gruppo di disponibilità del database o nel sito Active Directory che contiene la destinazione finale del messaggio, l'hop successivo del messaggio è generalmente la destinazione finale stessa. L'obiettivo della ridondanza shadow di mantenere due copie di un messaggio in transito viene raggiunto quando una copia shadow del messaggio esiste ovunque all'interno del gruppo di disponibilità del database o del sito Active Directory. In generale, solo gli scenari di failover in un gruppo di disponibilità del database che richiede il cmdlet **Redirect-Message** per svuotare le code attive su un server Cassette postali richiedono più hop nello stesso limite di disponibilità elevata del trasporto.

## Ridondanza shadow con server Trasporto Hub di Exchange 2010 nello stesso sito Active Directory

Se un server Trasporto Hub di Exchange 2010 trasmette un messaggio a un server Cassette postali di Exchange 2013 nello stesso sito Active Directory, il server Trasporto Hub di Exchange 2010 annuncia il supporto per la ridondanza shadow utilizzando il comando XSHADOW, mentre il server Cassette postali non annuncia il supporto per la ridondanza shadow. Questo impedisce al server Trasporto Hub di Exchange 2010 di creare una copia shadow del messaggio su un server Cassette postali di Exchange 2013.

Quando il servizio Trasporto su un server Cassette postali di Exchange 2013 trasmette un messaggio a un server Trasporto Hub di Exchange 2010 nello stesso sito Active Directory, il server Cassette postali di Exchange 2013 crea una copia shadow del messaggio per il server Trasporto Hub di Exchange 2010. Dopo che il server Cassette postali di Exchange 2013 riceve conferma dal server Trasporto Hub di Exchange 2010 che il messaggio è stato correttamente ricevuto, il server Cassette postali di Exchange 2013 sposta il messaggio correttamente elaborato in Safety Net. Tuttavia, i messaggi elaborati correttamente in Safety Net dal server Cassette postali di Exchange 2013 non vengono mai rinviati ai server Trasporto Hub di Exchange 2010.

Inizio pagina

## Timeout SMTP

Durante il tentativo di creare una copia ridondante del messaggio, potrebbe verificarsi un timeout della connessione SMTP tra il server SMTP di invio e il server primario o della sessione SMTP tra il server primario e il server shadow. I connettori di invio e ricezione dispongono entrambi di un parametro *ConnectionInactivityTimeOut* relativo all'effettiva trasmissione dei dati sul connettore. Anche i connettori di ricezione hanno un parametro *ConnectionTimeOut*.

Se una delle sessioni SMTP subisce un timeout prima della creazione e della conferma della copia shadow del messaggio, il risultato viene controllato dal parametro *RejectMessageOnShadowFailure* del cmdlet **Set-TransportConfig**. Per impostazione predefinita, il valore di questo parametro è `$false`, che implica che il messaggio primario viene accettato senza la creazione di una copia shadow. Se il valore di questo parametro è `$true`, il messaggio primario viene rifiutato con l'errore temporaneo `451 4.4.0`.

Se la copia shadow di un messaggio viene creata correttamente, ma la sessione SMTP tra il server SMTP di invio e il server primario subisce un timeout, il server primario accetta ed elabora il messaggio primario. Il server SMTP di invio recapiterà di nuovo il messaggio non confermato, ma il rilevamento dei messaggi duplicati impedirà agli utenti delle cassette postali di Exchange di vedere i messaggi duplicati. Quando il server SMTP di invio ripete l'invio del messaggio, il server primario crea un'altra copia shadow del messaggio. Non c'è alcuna relazione tra i messaggi shadow creati durante il rinvio dei messaggi da parte del server SMTP di invio.

Nella tabella seguente sono descritti i parametri che controllano la creazione dei messaggi shadow

### Parametri di creazione del messaggio shadow

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origine</th>
<th>Valore predefinito</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowMessagePreferenceSetting</em> in <strong>Set-TransportConfig</strong></p></td>
<td><p><code>PreferRemote</code></p></td>
<td><ul>
<li><p><code>PreferRemote</code>   Tenta di creare una copia shadow del messaggio su un server Cassette postali in un sito Active Directory diverso. Se l'operazione non riesce, tenta di creare una copia shadow del messaggio su un server nel sito Active Directory locale.</p></li>
<li><p><code>LocalOnly</code>   Una copia shadow del messaggio dovrebbe essere creata solo su un server di trasporto nel sito Active Directory locale.</p></li>
<li><p><code>RemoteOnly</code>: una copia shadow del messaggio dovrebbe essere creata solo su un server di trasporto in un sito Active Directory diverso.</p></li>
</ul>
<p>Questo parametro ha senso solo quando il server primario che sta tentando di creare una copia shadow del messaggio è un server Cassette postali membro di un gruppo di disponibilità del database che si estende su più siti Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxRetriesForRemoteSiteShadow</em> in <strong>Set-TransportConfig</strong></p></td>
<td><p>4</p></td>
<td><p>Questo parametro è utilizzato quando il server Cassette postali è membro di un gruppo di disponibilità del database che si estende su più siti Active Directory.</p>
<ul>
<li><p>Se <em>ShadowMessagePreferenceSetting</em> è impostato su <code>PreferRemote</code>, il server Cassette postali tenta innanzitutto di creare una copia shadow del messaggio su un altro server Cassette postali in un sito remoto di Active Directory fino a raggiungere il numero di volte specificato da <em>MaxRetriesForRemoteSiteShadow</em>. Se questa operazione ha esito negativo, il server Cassette postali tenta di creare una copia shadow del messaggio in un altro server Cassette postali nel sito locale Active Directory fino a raggiungere il numero di volte specificato da <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
<li><p>Se <em>ShadowMessagePreferenceSetting</em> è impostato su <code>RemoteOnly</code>, il server Cassette postali tenta innanzitutto di creare una copia shadow del messaggio su un server Cassette postali in un sito Active Directory remoto fino a raggiungere il numero di tentativi specificato da <em>MaxRetriesForRemoteSiteShadow</em>.</p></li>
<li><p>Il</p></li>
</ul>
<p>Quando si verificano errori nella creazione di una copia shadow del messaggio:</p>
<ul>
<li><p>Se <em>RejectMessageOnShadowFailure</em> è <code>$true</code>, il messaggio principale viene rifiutato con un errore transitorio.</p></li>
<li><p>Se <em>RejectMessageOnShadowFailure</em> è <code>$false</code>, il messaggio principale viene accettato ma non è persistente in modo ridondante.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MaxRetriesForLocalSiteShadow</em> in <strong>Set-TransportConfig</strong></p></td>
<td><p>2</p></td>
<td><p>Questo parametro viene utilizzato nelle seguenti circostanze:</p>
<ul>
<li><p>Se il server Cassette postali è membro di un gruppo di disponibilità del database che si estende su più siti Active Directory.</p>
<ol>
<li><p>Se <em>ShadowMessagePreferenceSetting</em> è impostato su <code>PreferRemote</code>, il server Cassette postali tenta innanzitutto di creare una copia shadow del messaggio su un altro server Cassette postali in un sito remoto di Active Directory fino a raggiungere il numero di volte specificato da <em>MaxRetriesForRemoteSiteShadow</em>. Se questa operazione ha esito negativo, il server Cassette postali tenta di creare una copia shadow del messaggio in un altro server Cassette postali nel sito locale Active Directory fino a raggiungere il numero di volte specificato da <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
<li><p>Se <em>ShadowMessagePreferenceSetting</em> è impostato su <code>LocalOnly</code>, il server Cassette postali tenta innanzitutto di creare una copia shadow del messaggio su un server Cassette postali diverso nel sito Active Directory locale fino a raggiungere il numero di tentativi specificato da <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
</ol></li>
<li><p>Se il server Cassette postali non è membro di un gruppo di disponibilità del database, o se il server Cassette postali è membro di un gruppo di disponibilità del database in un sito Active Directory, il server Cassette postali tenta unicamente di creare una copia shadow del messaggio su un server Cassette postali diverso nel sito Active Directory locale fino a raggiungere il numero di tentativi specificato da <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
</ul>
<p>Quando si verificano errori nella creazione di una copia shadow del messaggio:</p>
<ul>
<li><p>Se <em>RejectMessageOnShadowFailure</em> è <code>$true</code>, il messaggio principale viene rifiutato con un errore transitorio.</p></li>
<li><p>Se <em>RejectMessageOnShadowFailure</em> è <code>$false</code>, il messaggio principale viene accettato ma non è persistente in modo ridondante.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ConnectionInactivityTimeout</em> in <strong>Set-ReceiveConnector</strong></p></td>
<td><p>5 minuti nel servizio di trasporto sui server Cassette postali</p>
<p>5 minuti nel servizio di trasporto front-end sui server Accesso client.</p>
<p>1 minuto sui server Trasporto Edge.</p></td>
<td><p>Questo parametro consente di specificare il tempo massimo per il quale una connessione SMTP aperta con un server di messaggistica di origine può restare inattiva prima che venga chiusa. Il valore del parametro deve essere inferiore al valore specificato dal parametro <em>ConnectionTimeout</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>ConnectionTimeout</em> in <strong>Set-ReceiveConnector</strong></p></td>
<td><p>10 minuti nel servizio di trasporto sui server Cassette postali</p>
<p>10 minuti nel servizio di trasporto front-end sui server Accesso client.</p>
<p>5 minuti sui server Trasporto Edge.</p></td>
<td><p>Questo parametro consente di specificare il tempo massimo per il quale una connessione SMTP con un server di messaggistica di origine può restare aperta anche se è in corso la trasmissione di dati dal server di messaggistica di origine. Il valore del parametro deve essere superiore al valore specificato dal parametro <em>ConnectionInactivityTimeout</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>ConnectionInactivityTimeOut</em> in <strong>Set-SendConnector</strong></p></td>
<td><p>10 minuti</p></td>
<td><p>Questo parametro consente di specificare il tempo massimo per il quale una connessione SMTP aperta con un server di messaggistica di destinazione può restare inattiva prima che venga chiusa.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Modalità di manutenzione dei messaggi shadow

Dopo aver creato correttamente un messaggio shadow, il lavoro della ridondanza shadow è appena cominciato. Il server primario e il server shadow devono rimanere in contatto per tenere traccia dell'avanzamento del messaggio.

Quando il server primario trasmette correttamente il messaggio all'hop successivo e l'hop successivo conferma la ricezione del messaggio, il server primario aggiorna lo *stato di rimozione* del messaggio impostandolo come recapito completato. Lo stato di rimozione è fondamentalmente un messaggio che contiene un elenco di messaggi monitorati. Un messaggio recapitato correttamente non deve essere mantenuto in una coda shadow; nel momento in cui il server shadow sa che il server primario ha trasmesso correttamente il messaggio all'hop successivo, il server shadow sposta il messaggio shadow dalla coda shadow a Safety Net.

Il server shadow determina lo stato di rimozione dei messaggi shadow nelle code shadow interrogando il server primario. Se il server shadow apre una sessione SMTP con il server primario per un qualunque motivo, compresa la trasmissione di altri messaggi non correlati, il server shadow invia il comando **XQDISCARD** per determinare lo stato di rimozione dei messaggi primari. Se il server shadow non ha aperto una sessione SMTP con il server primario dopo un intervallo di tempo configurato, il server shadow apre una sessione SMTP con il server primario e invia il comando **XQDISCARD**. L'intervallo di tempo è controllato dal parametro *ShadowHeartbeatFrequentcy* nel cmdlet **Set-TransportConfig**. Il valore predefinito è 2 minuti. Dopo che il server shadow ha aperto una sessione SMTP con il server primario, questo risponde con le *notifiche di rimozione* per i messaggi corrispondenti al server shadow che esegue la query. In Exchange 2013, le notifiche di rimozione sono archiviate su disco, non in memoria. Pertanto, se il servizio Trasporto di Microsoft Exchange viene riavviato, le notifiche di rimozione vengono mantenute. Dopo l'avvio del servizio, il server primario conosce ancora i messaggi elaborati correttamente e tali informazioni sono disponibili per il server shadow.

La comunicazione SMTP tra il server shadow e il server primario è utilizzata come *heartbeat* che determina la disponibilità dei server. Se il server shadow non può aprire una sessione SMTP con il server primario dopo un intervallo di tempo configurato, o se il database di trasporto del server primario utilizza un ID database diverso, il server shadow alza il suo livello a quello di server primario, alza di livello i messaggi shadow trasformandoli in messaggi primari e trasmette i messaggi all'hop successivo. L'intervallo di tempo è controllato dal parametro *ShadowResubmitTimeSpan* nel cmdlet **Set-TransportConfig**. Il valore predefinito è 3 ore.

*Shadow Redundancy Manager* è il componente principale di un server di trasporto Exchange 2013, responsabile della gestione della ridondanza shadow. Shadow Redundancy Manager è responsabile del mantenimento delle informazioni seguenti per tutti i messaggi principali che un server sta attualmente elaborando:

  - Server shadow per ogni messaggio principale in fase di elaborazione.

  - Stato di eliminazione da inviare al server shadow.

Shadow Redundancy Manager è responsabile di quanto segue per tutti i messaggi shadow presenti nelle code shadow di un server shadow:

  - Mantenimento dell'elenco di server primari per ogni messaggio shadow.

  - Confronto tra l'ID database originale e l'ID database corrente del database delle code in cui è archiviata la copia primaria del messaggio.

  - Controllo della disponibilità di ogni server primario per cui viene messo in coda un messaggio shadow.

  - Elaborazione delle notifiche di eliminazione provenienti dai server primari.

  - Rimozione dei messaggi shadow provenienti dalle code shadow dopo la ricezione di tutte le notifiche di rimozione previste.

  - Decisione del momento in cui il server shadow deve assumere la proprietà dei messaggi shadow, divenendo server primario.

  - Verifica delle biforcazioni dei messaggi e di altri messaggi con effetto collaterale, quali notifiche sullo stato del recapito (DSN) e rapporti del journal, per verificare che la copia ridondante del messaggio non venga rilasciata finché non sono state elaborate tutte le biforcazioni del messaggio.

Nella tabella seguente sono descritti i parametri che controllano la gestione dei messaggi shadow.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Valore predefinito</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowHeartbeatFrequency</em> in <strong>Set-TransportConfig</strong></p></td>
<td><p>2 minuti</p></td>
<td><p>Il tempo massimo atteso da un server shadow prima di aprire una connessione SMTP al server primario per verificare lo stato di rimozione dei messaggi.</p></td>
</tr>
<tr class="even">
<td><p><em>ShadowResubmitTimeSpan</em> in <strong>Set-TransportConfig</strong></p></td>
<td><p>3 ore</p></td>
<td><p>Il tempo che un server attende prima di decidere che si è verificato un errore in un server primario e di acquisire la proprietà dei messaggi shadow nella coda shadow per il server primario che non è raggiungibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShadowMessageAutoDiscardInterval</em> in <strong>Set-TransportConfig</strong></p></td>
<td><p>2 giorni</p></td>
<td><p>Il tempo per cui un server conserva gli eventi di rimozione per i messaggi recapitati correttamente. Un server principale mette in coda gli eventi di eliminazione fino all'interrogazione da parte di un server shadow. Tuttavia, se il server shadow non interroga il server primario per la durata specificata in questo parametro, il server primario elimina gli eventi in coda.</p></td>
</tr>
<tr class="even">
<td><p><em>SafetyNetHoldTime</em> in <strong>Set-TransportConfig</strong></p></td>
<td><p>2 giorni</p></td>
<td><p>Il tempo di conservazione in Safety Net dei messaggi elaborati correttamente. I messaggi shadow non confermati scadono da Safety Net dopo la somma dei valori <em>SafetyNetHoldTime</em> e <em>MessageExpirationTimeout</em> in <strong>Set-TransportService</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageExpirationTimeout</em> in <strong>Set-TransportService</strong></p></td>
<td><p>2 giorni</p></td>
<td><p>Quanto tempo un messaggio può rimanere in coda prima della scadenza.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Elaborazione del messaggio dopo un'interruzione

La ridondanza shadow consente di ridurre al minimo la perdita di messaggi a causa di interruzioni del server. Quando un server di trasporto torna in linea dopo un'interruzione, si possono presentare due scenari:

  - **Il server torna in linea con un nuovo database di trasporto**   In questo scenario, il database di trasporto non può essere recuperato a causa del danneggiamento dei dati o di un errore hardware. In questo caso, poiché il server di trasporto avrà un nuovo ID database, sarà riconosciuto come nuova route dagli altri server di trasporto dell'organizzazione. Ciò si applica anche alla situazione in cui non è possibile recuperare un server e viene fornito un nuovo server in sostituzione.

  - **Il server torna in linea con lo stesso database di trasporto**   In questo scenario, non si verifica un errore del server di trasporto, ma tale server è rimasto offline per un tempo sufficiente a far sì che il server shadow assuma la proprietà dei messaggi e li rinvii. Questo scenario può essere causato, ad esempio, da un errore della scheda di rete o da una manutenzione prolungata sul server.

Nella tabella seguente sono riepilogate le reazioni della ridondanza shadow a questi due scenari. Per ragioni di chiarezza, si presume che il server che ha subito un'interruzione sia denominato Mailbox01.

### Elaborazione dei messaggi negli scenari di ripristino

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Scenario di ripristino</th>
<th>Azioni intraprese</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mailbox01 torna online con un nuovo database.</p></td>
<td><p>Quando Mailbox01 diventa non disponibile, ogni server che presenta messaggi shadow in coda per Mailbox01 assume la proprietà di tali messaggi e li invia nuovamente. I messaggi vengono poi recapitati alle loro destinazioni.</p>
<p>Il ritardo massimo per i messaggi è il valore del parametro <em>ShadowHeartbeatFrequency</em> nel cmdlet <strong>Set-TransportConfig</strong>. Il valore predefinito è 2 minuti.</p></td>
</tr>
<tr class="even">
<td><p>Mailbox01 torna online con lo stesso database.</p></td>
<td><p>Dopo il ritorno online di Mailbox01, vengono recapitati i messaggi nelle relative code, che potrebbero già essere stati recapitati dai server che possiedono le copie shadow dei messaggi per Mailbox01. Ciò causerà il recapito duplicato di tali messaggi. Gli utenti delle cassette postali di Exchange non vedranno i messaggi duplicati grazie al rilevamento dei messaggi duplicati. Tuttavia, i destinatari su sistemi di messaggistica diversi da Exchange potranno ricevere copie duplicate dei messaggi.</p>
<p>Il ritardo massimo per i messaggi è il valore del parametro <em>ShadowResubmitTimeSpan</em> nel cmdlet <strong>Set-TransportConfig</strong>. Il valore predefinito è 3 ore.</p></td>
</tr>
</tbody>
</table>


Inizio pagina


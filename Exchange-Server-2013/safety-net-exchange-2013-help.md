---
title: 'Rete sicura: Exchange 2013 Help'
TOCTitle: Rete sicura
ms:assetid: d0abb807-3b12-4c7d-bc7e-769b87c84ccb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657495(v=EXCHG.150)
ms:contentKeyID: 50481711
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rete sicura

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

In Microsoft Exchange Server 2013 il meccanismo principale della disponibilità elevata della cassetta postale è il gruppo di disponibilità del database (DAG). Per ulteriori informazioni sui gruppi di disponibilità del database, vedere [Gestione dei gruppi di disponibilità del database](managing-database-availability-groups-exchange-2013-help.md). Il *dumpster di trasporto* è stato introdotto per la prima volta in Exchange 2007 e ulteriormente migliorato in Exchange 2010 per fornire copie ridondanti dei messaggi, una volta recapitati alle cassette postali nei DAG. In Exchange 2010 il dumpster di trasporto offriva una protezione dalla perdita di dati mantenendo una coda di messaggi recapitati correttamente che non erano stati replicati nelle copie passive del database delle cassette postali nel DAG. Quando un errore del database delle cassette postali o del server richiedeva la promozione di una copia obsoleta del database delle cassette postali, i messaggi nel dumpster di trasporto venivano reinviati automaticamente alla nuova copia attiva del database delle cassette postali.

Il dumpster di trasporto è stato migliorato in Exchange 2013 e viene adesso denominato *Rete sicura*.

Di seguito vengono descritte le analogie tra Rete sicura e il dumpster di trasporto in Exchange 2010:

  - Rete sicura è una coda associata al servizio di trasporto su un server Cassette postali, che memorizza le copie dei messaggi elaborati correttamente dal server.

  - È possibile specificare la permanenza delle copie dei messaggi elaborati correttamente in Rete sicura prima che scadano e vengano eliminati automaticamente. Il valore predefinito è 2 giorni.

Di seguito vengono riportate le differenze di Rete sicura in Exchange 2013:

  - Rete sicura non richiede gruppi di disponibilità del database. Per i server Cassette postali che non appartengono ai DAG, Rete sicura memorizza le copie dei messaggi recapitati sugli altri server Cassette postali nel sito Active Directory locale.

  - Anche Rete sicura è adesso caratterizzata da ridondanza, non essendo più un singolo punto di errore. Si introduce così il concetto di *Rete sicura primaria* e *Rete sicura shadow*. Se la Rete sicura primaria non è disponibile per oltre 12 ore, le richieste di reinvio diventano richieste di reinvio shadow e i messaggi vengono recapitati di nuovo dalla Rete sicura shadow.

  - Rete sicura si assume alcuni compiti della ridondanza shadow negli ambienti DAG. La ridondanza shadow non deve mantenere un'altra copia del messaggio recapitato in una coda shadow mentre attende che il messaggio recapitato venga replicato nelle copie passive del database delle cassette postali sugli altri server Cassette postali nel DAG. La copia del messaggio recapitato è già memorizzata in Rete sicura, così il messaggio può essere inviato di nuovo da Rete sicura, se necessario.

  - In Exchange 2013 la disponibilità elevata di trasporto è più del massimo sforzo possibile per la ridondanza dei messaggi. Exchange 2013 tenta di garantire la ridondanza dei messaggi. Di conseguenza non è possibile specificare un limite di dimensione massimo per Rete sicura. È possibile specificare solo per quanto tempo Rete sicura deve conservare i messaggi prima che vengano eliminati automaticamente.

**Sommario**

How Safety Net works

Message resubmission from Safety Net

Message resubmission from Shadow Safety Net

## Funzionamento di Rete sicura

La ridondanza shadow mantiene una copia ridondante del messaggio mentre questo è in transito. Rete sicura mantiene una copia ridondante di un messaggio dopo che questo è stato elaborato correttamente. In tal modo entra in funzione dove la ridondanza shadow finisce. Gli stessi concetti sulla ridondanza shadow, incluso il limite di disponibilità elevata del trasporto, i messaggi primari, i server primari, i messaggi shadow e i server shadow si applicano anche a Rete sicura. Per ulteriori informazioni, vedere [Ridondanza shadow](shadow-redundancy-exchange-2013-help.md).

La Rete sicura primaria è presente nel server Cassette postali che ha conservato il messaggio primario prima che venisse elaborato correttamente dal servizio di trasporto. Ne potrebbe risultare che il messaggio sia stato recapitato al servizio Trasporto delle cassette postali sul server di destinazione Cassette postali. Oppure che il messaggio sia stato inoltrato tramite il server Cassette postali in un sito Active Directory designato come sito hub nel percorso verso il DAG o il sito Active Directory di destinazione. Dopo che il server primario ha elaborato il messaggio primario, il messaggio viene spostato dalla coda attiva alla Rete sicura primaria sullo stesso server.

La Rete sicura shadow si trova sul server Cassette postali che ha conservato il messaggio shadow. Dopo che aver determinato che il server primario ha elaborato correttamente il messaggio primario, il server shadow sposta il messaggio shadow dalla coda shadow alla Rete sicura shadow sullo stesso server. Sebbene possa sembrare ovvio, l'esistenza della Rete sicura shadow richiede l'abilitazione della ridondanza shadow, che in Exchange 2013 è abilitata per impostazione predefinita.

Nella tabella seguente sono descritti i parametri utilizzati da Rete sicura.


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
<td><p><em>SafetyNetHoldTime</em> in <strong>Set-TransportConfig</strong></p></td>
<td><p>2 giorni</p></td>
<td><p>I messaggi primari elaborati correttamente entro il periodo di tempo previsto vengono conservati nella Rete sicura primaria mentre i messaggi shadow riconosciuti vengono memorizzati nella Rete sicura shadow.</p>
<p>È inoltre possibile specificare questo valore nell'interfaccia di amministrazione di Exchange (EAC) tramite <strong>Flusso di posta</strong> &gt; <strong>Connettori di ricezione</strong> &gt; <strong>Altre opzioni</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icona Ulteriori opzioni" alt="Icona Ulteriori opzioni" /> &gt; <strong>Impostazioni trasporto organizzazione</strong> &gt; <strong>Rete sicura</strong> &gt; <strong>Tempo permanenza nella rete sicura</strong>.</p>
<p>La scadenza dei messaggi shadow non riconosciuti da Rete sicura shadow è determinata dalla somma di <em>SafetyNetHoldTime</em> e <em>MessageExpirationTimeout</em> in <strong>Set-TransportService</strong>.</p>
<p>Per evitare la perdita di data durante i reinvii di Rete sicura, il valore di <em>SafetyNetHoldTime</em> deve essere superiore o uguale al valore di <em>ReplayLagTime</em> in <strong>Set-MailboxDatabaseCopy</strong> per la copia ritardata del database delle cassette postali.</p></td>
</tr>
<tr class="even">
<td><p><em>ReplayLagTime</em> in <strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>Non configurato</p></td>
<td><p>La quantità di tempo di attesa del servizio Replica di Microsoft Exchange prima di riprodurre i file di registro copiati nella copia passiva del database. Impostando questo parametro su un valore maggiore di 0, si crea una copia del database delle cassette postali ritardata. Il valore massimo è 14 giorni.</p>
<p>Per evitare la perdita di dati durante i reinvii di Rete sicura, il valore di <em>ReplayLagTime</em> deve essere minore o uguale al valore di <em>SafetyNetHoldTime</em> in <strong>Set-TransportConfig</strong> per la copia ritardata del database delle cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageExpirationTimeout</em> in <strong>Set-TransportService</strong></p></td>
<td><p>2 giorni</p></td>
<td><p>Quanto tempo un messaggio può rimanere in coda prima della scadenza.</p></td>
</tr>
<tr class="even">
<td><p><em>ShadowRedundancyEnabled</em> in <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> consente la ridondanza shadow su tutti i server di trasporto nell'organizzazione.</p></li>
<li><p><code>$false</code> disabilita la ridondanza shadow su tutti i server di trasporto nell'organizzazione.</p></li>
</ul>
<p>Una Rete sicura ridondante richiede che la ridondanza shadow sia abilitata.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Reinvio di messaggi da Rete sicura

I reinvii dei messaggi da Rete sicura vengono inizializzati dal componente Active Manager del servizio Replica di Microsoft Exchange che gestisce i DAG e le copie del database delle cassette postali. Nessuna azione manuale è necessaria per il reinvio dei messaggi da Rete sicura. Per ulteriori informazioni su Active Manager, vedere [Active Manager](active-manager-exchange-2013-help.md).

Esistono due scenari di base di reinvio di messaggi di Rete sicura:

  - In seguito a failover automatico o manuale di un database delle cassette postali in un DAG.

  - In seguito all'attivazione di una copia ritardata di un database delle cassette postali.

Una *copia del database delle cassette postali ritardata* o *copia ritardata* è una copia passiva di un database delle cassette postali in cui gli aggiornamenti al database vengono ritardati di proposito per proteggere il database da danneggiamenti logici. Per ulteriori informazioni, vedere [Gestione delle copie del database delle cassette postali](managing-mailbox-database-copies-exchange-2013-help.md).

L'unica differenza significativa tra i due scenari è quanto è necessario andare indietro nel tempo per reinviare i messaggi da Rete sicura. Per il failover in un DAG, la nuova copia attiva del database delle cassette postali è in genere da diversi minuti a diverse ore antecedente alla vecchia copia attiva. Una copia ritardata del database delle cassette postali è in genere di diverse ore antecedente alla vecchia copia attiva.

Il requisito principale per un reinvio corretto da Rete sicura per una copia ritardata è che la permanenza dei messaggi in Rete sicura deve essere superiore o uguale al ritardo della copia ritardata del database delle cassette postali. In altre parole, il valore di *SafetyNetHoldTime* in **Set-TransportConfig** deve essere maggiore o uguale al valore di *ReplayLagTime* in **Set-MailboxDatabaseCopy** per la copia ritardata.

Inizio pagina

## Reinvio di messaggi dalla Rete sicura shadow

Analogamente al reinvio dei messaggi dalla Rete sicura primaria, i reinvii dalla Rete sicura shadow sono completamente automatizzati e non richiedono interventi manuali.

Quando Active Manager richiede il reinvio di messaggi da Rete sicura per un periodo di tempo specifico, la richiesta passa al servizio di trasporto sui server Cassette postali dove la Rete sicura primaria conserva le copie dei messaggi per il periodo di tempo necessario. Nelle organizzazioni Exchange di grandi dimensioni, è probabile che i messaggi richiesti siano presenti in Rete sicura in più server Cassette postali, in particolare se il periodo di tempo richiesto è lungo.

Senza ottimizzazione, il reinvio di messaggi da Rete sicura avrebbe come conseguenza una quantità potenzialmente notevole di recapiti duplicati. I recapiti duplicati all'interno dell'organizzazione Exchange non rappresentano un problema poiché il rilevamento dei messaggi duplicati impedisce agli utenti delle cassette postali di vedere le copie duplicate di un messaggio. Il recapito dei messaggi duplicati ai destinatari esterni all'organizzazione di Exchange darebbe tuttavia luogo a copie duplicate dei messaggi. Fortunatamente in Exchange 2013 è stato ottimizzato il reinvio dei messaggi da Rete sicura per ridurre il recapito dei messaggi duplicati.

Se la Rete sicura inizialmente non risponde o se smette di rispondete durante il reinvio del messaggio, Active Manager continua a tentare di contattarla per altre 12 ore. Dopo 12 ore viene inviata una trasmissione al servizio di trasporto su tutti i server Cassette postali entro il limite di disponibilità elevata del trasporto con la richiesta di reinvio del messaggio da Rete sicura per l'intervallo di tempo richiesto per il database delle cassette postali richiesto. Quando una Rete sicura shadow risponde, reinvia i messaggi per il database delle cassette postali richiesto solo durante l'intervallo di tempo richiesto.

È necessario tenere presenti alcune considerazioni importanti per i messaggi shadow archiviati nella Rete sicura shadow:

  - La Rete sicura shadow non conosce il punto in cui il server primario ha trasmesso il messaggio primario.

  - I messaggi shadow nella Rete sicura shadow contengono soltanto i destinatari della busta del messaggio originale e non i destinatari effettivi a cui è stato recapitato il messaggio primario. Il destinatario di una busta del messaggio potrebbe ad esempio essere un gruppo di distribuzione che richiede espansione.

  - I messaggi nella Rete sicura shadow non presentano gli aggiornamenti dei messaggi avvenuti dopo l'elaborazione del messaggio da parte del server primario, ad esempio la codifica del messaggio o la conversione del contenuto.

Il messaggio shadow reinviato dalla Rete sicura shadow richiede classificazione ed elaborazione complete tramite il servizio di trasporto sul server Cassette postali. Il reinvio di quantità notevoli di messaggi shadow dalla Rete sicura shadow può essere dispendioso in termini di impiego di risorse per il server Cassette postali. Fortunatamente anche il reinvio dei messaggi shadow dalla Rete sicura shadow è stato ottimizzato, di conseguenza vengono reinviati solo i messaggi nella Rete sicura shadow per l'intervallo di tempo richiesto e il database delle cassette postali richiesto.

L'interazione tra la Rete sicura primaria e la Rete sicura shadow durante il reinvio dei messaggi è descritta nello scenario seguente.

1.  Active Manager richiede un reinvio dei messaggi dalla Rete sicura per un database delle cassette postali per l'intervallo di tempo 05:00-9:00. Il server Cassette postali su cui si trova la Rete sicura primaria ha tuttavia subito un arresto anomalo a causa di un errore dell'hardware. Active Manager tenta ripetutamente di contattare la Rete sicura primaria per 12 ore.

2.  Trascorse le 12 ore, Active Manger invia un messaggio di trasmissione al servizio di trasporto su tutti i server Cassette postali entro il limite di disponibilità elevata del trasporto alla ricerca di altre reti sicure che contengano i messaggi per il database delle cassette postali di destinazione per l'intervallo di tempo compreso tra le 5:00 e le 9:00. Le risposte della Rete sicura Net shadow sono i reinvii dei messaggi per il database delle cassette postali per l'intervallo di tempo compreso tra le 5:00 e le 9:00.

Un'interazione interessante si verifica quando la Rete sicura primaria è offline durante parte dell'intervallo di reinvio richiesto come descritto nello scenario seguente.

1.  Il database delle code sul server Cassette postali su cui si trova la Rete sicura primaria è danneggiato. Ne viene creato uno nuovo alle 7:00. Tutti i messaggi primari memorizzati nella Rete sicura primaria dalle 1:00 alle 7:00 vengono persi ma il server è in grado di memorizzare le copie dei messaggi recapitati correttamente in Rete sicura a partire dalle 7:00.

2.  Active Manager richiede un reinvio dei messaggi da Rete sicura per un database delle cassette postali per l'intervallo di tempo tra l'1:00 e le 9:00.

3.  La Rete sicura primaria reinvia i messaggi per l'intervallo di tempo tra le 7:00 e le 9:00.

4.  La Rete sicura primaria invia un messaggio di trasmissione al servizio di trasporto su tutti i server Cassette postali entro il limite di disponibilità elevata del trasporto alla ricerca di altre reti sicure che contengano i messaggi per il database delle cassette postali di destinazione per l'intervallo di tempo 1:00-7:00 per cui la Rete sicura primaria non contiene messaggi. La Rete sicura shadow genera una seconda richiesta di reinvio per conto della Rete sicura primaria per reinviare i messaggi shadow per il database delle cassette postali di destinazione per l'intervallo di tempo 1:00-7:00.

Ci sono altre questioni da considerare quando i messaggi vengono reinviati da Rete sicura.

1.  Tutte le notifiche sullo stato del recapito (DSN) e i rapporti di mancato recapito (NDR) vengono rimossi per i reinvii di Rete sicura. Ad esempio, se il messaggio primario ha dato come risultato un rapporto NDR, questo non verrà recapitato per il messaggio reinviato.

2.  Gli utenti rimossi da un gruppo di distribuzione potrebbero non ricevere un messaggio reinviato quando Rete sicura shadow reinvia il messaggio. Ad esempio, un messaggio viene inviato a un gruppo contenente l'utente A e l'utente B ed entrambi i destinatari ricevono il messaggio. L'utente B viene successivamente rimosso dal gruppo. In seguito viene inoltrata una richiesta di reinvio dalla Rete sicura primaria per il database delle cassette postali in cui si trova la cassetta postale dell'utente B. La Rete sicura primaria non è tuttavia disponibile per oltre 12 ore quindi il server della Rete sicura shadow risponde e reinvia il messaggio in questione. Durante il reinvio, quando il gruppo di distribuzione viene espanso, l'utente B non è un membro del gruppo e non riceverà una copia del messaggio reinviato.

3.  I nuovi utenti aggiunti a un gruppo di distribuzione potrebbero ricevere un vecchio messaggio reinviato quando la Rete sicura shadow reinvia il messaggio. Ad esempio, un messaggio viene inviato a un gruppo contenente l'utente A e l'utente B ed entrambi i destinatari ricevono il messaggio. L'utente C viene successivamente aggiunto al gruppo. In seguito viene inoltrata una richiesta di reinvio dalla Rete sicura primaria per il database delle cassette postali in cui si trova la cassetta postale dell'utente C. Il server della Rete sicura primaria non è tuttavia disponibile per oltre 12 ore quindi il server della Rete sicura shadow risponde e reinvia i messaggi in questione. Durante il reinvio, quando il gruppo di distribuzione viene espanso, l'utente C è un membro del gruppo e riceverà una copia del messaggio reinviato.

Inizio pagina


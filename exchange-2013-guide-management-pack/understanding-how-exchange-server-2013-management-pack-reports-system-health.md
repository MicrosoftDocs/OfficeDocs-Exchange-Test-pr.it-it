---
title: Informazioni sulla segnalazione relativa all'integrità del sistema da parte di Exchange Server 2013 Management Pack
TOCTitle: Informazioni sulla segnalazione relativa all'integrità del sistema da parte di Exchange Server 2013 Management Pack
ms:assetid: 6ca8847f-93fe-458d-bd43-7afad7fdd2f4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn195910(v=EXCHG.150)
ms:contentKeyID: 53275565
ms.date: 08/30/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Informazioni sulla segnalazione relativa all'integrità del sistema da parte di Exchange Server 2013 Management Pack

 

_**Ultima modifica dell'argomento:**  2013-04-17_

In questo argomento vengono fornite informazioni sul monitoraggio e sulla segnalazione relativa all'integrità del sistema Exchange da parte di Exchange Server 2013 Management Pack. In Exchange 2013 Management Pack, le informazioni sullo stato di integrità vengono riportate semplicemente. Ogni volta che l'integrità risulta danneggiata e che viene attivato il risponditore di inoltro, il seguente evento viene registrato nel registro eventi di Windows:

## Disponibilità gestita

In Exchange Server 2013, vengono apportate alcune modifiche all'architettura. Una delle modifiche chiave è la funzionalità *Disponibilità gestita* in cui tutti i componenti di Exchange 2013 dispongono di monitor integrati in grado di rilevare problemi e di tentare di ripristinare la disponibilità del servizio. Exchange 2013 Management Pack si basa su questa funzionalità. I problemi che non possono essere ripristinati automaticamente vengono inoltrati a Exchange 2013 Management Pack come avviso. Ogni componente in Exchange 2013 monitora sé stesso tramite tre componenti di base denominati probe, monitor e risponditori.

![Disponibilità gestita](images/Dn195910.dd5febae-d05e-4089-a3f5-1691b2d9a3d7(EXCHG.150).png "Disponibilità gestita")

  - **Probe**   Sono insiemi di agenti di raccolta dati che misurano vari componenti. Sono disponibili tre tipi diversi di probe:
    
      - Transazioni sintetiche che misurano operazioni utente end-to-end sintetiche e controlli che misurano il traffico effettivo.
    
      - Controlli che misurano il traffico clienti effettivo.
    
      - Notifiche che consentono a Exchange di intervenire immediatamente. Un buon esempio ne è la notifica che viene attivata alla scadenza del certificato.

  - **Monitor**   I dati raccolti tramite probe vengono trasferiti ai monitor che analizzano i dati per condizioni specifiche e in base a tali condizioni stabiliscono se un determinato componente è integro o danneggiato.

  - **Risponditori**   Se un monitor stabilisce che un componente è danneggiato attiverà un risponditore. Se il problema è reversibile, il risponditore tenta di ripristinare il componente tramite la logica incorporata. Sono disponibili alcuni risponditori per ciascun componente, ma quello rilevante per Exchange 2013 Management Pack è il *risponditore di inoltro*. Quando viene attivato il risponditore di inoltro, questo genera un evento che Exchange 2013 Management Pack riconosce e di cui fornisce agli amministratori le informazioni appropriate e necessarie per risolvere il problema.

Ciascun componente in Exchange 2013 utilizza un insieme specifico di probe, monitor e risponditori per monitorare sé stesso. Si fa riferimento a queste raccolte di probe e monitor come *impostazioni di integrità*. Ad esempio, esiste un numero di probe che raccoglie dati su vari aspetti del servizio ActiveSync. Tali dati vengono elaborati da un insieme di monitor dedicato che attiva i risponditori appropriati per correggere i problemi rilevati nel servizio ActiveSync. Considerati collettivamente, tali componenti costituiscono l'impostazione di integrità di ActiveSync.

Le impostazioni di integrità in Exchange sono organizzate secondo le quattro categorie seguenti che corrispondono al dashboard del Management Pack:

  - Punti tocco del cliente

  - Componenti del servizio

  - Risorse del server

  - Dipendenze fondamentali

Per un elenco completo delle impostazioni di integrità di Exchange, vedere [Appendix A: Exchange health sets](appendix-a-exchange-health-sets.md).

Per ulteriori informazioni sulla Disponibilità gestita, vedere [Integrità del server e prestazioni](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Rollup dell'integrità

In questo argomento vengono fornite informazioni sul monitoraggio e sulla segnalazione relativa all'integrità del sistema Exchange da parte di Exchange Server 2013 Management Pack. In Exchange 2013 Management Pack, le informazioni sullo stato di integrità vengono riportate semplicemente. Ogni volta che l'impostazione di integrità risulta danneggiata e che viene attivato il risponditore di inoltro, il seguente evento viene registrato nel registro eventi di Windows:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Nome registro</p></td>
<td><p>Monitoraggio/ManagedAvailability di Microsoft Exchange</p></td>
</tr>
<tr class="even">
<td><p>Origine</p></td>
<td><p>ManagedAvailability</p></td>
</tr>
<tr class="odd">
<td><p>Data</p></td>
<td><p>&lt;<em>data e ora dell'evento di protocollo</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>ID evento</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>Categoria attività</p></td>
<td><p>Monitoraggio</p></td>
</tr>
<tr class="even">
<td><p>Livello</p></td>
<td><p>Errore</p></td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><p>&lt;<em>nessuna</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Utente</p></td>
<td><p>SYSTEM</p></td>
</tr>
<tr class="odd">
<td><p>Computer</p></td>
<td><p>&lt;<em>Nome di dominio completo del server Exchange</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Descrizione</p></td>
<td><p>&lt;<em>generato dinamicamente dal risponditore di inoltro</em>&gt;</p></td>
</tr>
</tbody>
</table>


L'agente Management Pack rileva ed elabora l'evento. Tramite l'evento, Disponibilità gestita è in grado di generare avvisi in SCOM. Quando viene risolto il problema corrispondente e l'impostazione di integrità torna allo stato di integrità, il seguente evento viene registrato nel registro eventi di Windows:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Nome registro</p></td>
<td><p>Monitoraggio/ManagedAvailability di Microsoft Exchange</p></td>
</tr>
<tr class="even">
<td><p>Origine</p></td>
<td><p>ManagedAvailability</p></td>
</tr>
<tr class="odd">
<td><p>Data</p></td>
<td><p>&lt;<em>data e ora dell'evento di protocollo</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>ID evento</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>Categoria attività</p></td>
<td><p>Monitoraggio</p></td>
</tr>
<tr class="even">
<td><p>Livello</p></td>
<td><p>Informazioni</p></td>
</tr>
<tr class="odd">
<td><p>Parole chiave</p></td>
<td><p>&lt;<em>nessuna</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Utente</p></td>
<td><p>SYSTEM</p></td>
</tr>
<tr class="odd">
<td><p>Computer</p></td>
<td><p>&lt;<em>Nome di dominio completo del server Exchange</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Descrizione</p></td>
<td><p>&lt;<em>generato dinamicamente dal risponditore di inoltro</em>&gt;</p></td>
</tr>
</tbody>
</table>


I Management Pack che hanno monitorato le versioni precedenti di Exchange erano completamente centralizzati. Gli agenti su ciascun server Exchange raccoglievano i dati e un motore di correlazione centrale confrontava e valutava tutti i dati riportati dagli agenti per stabilire l'integrità di tutto il servizio. In ambienti di grandi dimensioni, il processo risultava in correlazioni complesse, che causavano ritardi nella generazione di avvisi. In Exchange 2013, la correlazione degli avvisi non è più utilizzata. Al contrario, ogni server esegue monitoraggio e avvisa SCOM se necessario, permettendo un'architettura altamente scalabile.

In base all'impatto dell'evento, e all'impostazione di integrità che lo attiva, il problema viene visualizzato nella console SCOM nella categoria corrispondente. Se l'evento ha un impatto sull'utente, l'indicatore dei punti tocco del cliente viene visualizzato come danneggiato. Se causa la mancanza di disponibilità di un intero componente come OWA, l'indicatore relativo al componente del servizio viene visualizzato come danneggiato. Se si tratta di un problema con un server specifico, l'indicatore relativo all'integrità del server corrispondente viene visualizzato come danneggiato. Infine, se il problema è relativo a una risorsa da cui dipende Exchange, l'indicatore relativo alle dipendenze fondamentali viene visualizzato come danneggiato. Per ulteriori informazioni su queste categorie, vedere [Guida introduttiva a Exchange Server 2013 Management Pack](getting-started-with-exchange-server-2013-management-pack.md).


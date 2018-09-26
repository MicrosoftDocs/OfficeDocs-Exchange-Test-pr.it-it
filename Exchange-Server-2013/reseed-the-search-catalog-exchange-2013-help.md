---
title: 'Reseeding del catalogo di ricerca: Exchange 2013 Help'
TOCTitle: Reseeding del catalogo di ricerca
ms:assetid: 9d873bd4-0422-4975-b5e2-82a347479115
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633475(v=EXCHG.150)
ms:contentKeyID: 52063089
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Reseeding del catalogo di ricerca

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Se il catalogo di indicizzazione del contenuto per una copia del database delle cassette postali risulta danneggiato, potrebbe essere necessario eseguire il reseeding del catalogo. Gli indici dei contenuti danneggiati vengono indicati nel registro eventi dell'applicazione dal seguente evento.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ID evento</th>
<th>Livello</th>
<th>Origine</th>
<th>Dettagli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>123</p></td>
<td><p>Errore</p></td>
<td><p>ExchangeStoreDB</p></td>
<td><p>In corrispondenza del &lt;<em>timestamp</em>&gt;, la copia dell'&lt;<em>identità</em>&gt; del database dell'archivio informazioni di Microsoft Exchange su questo server ha riscontrato un catalogo di ricerca danneggiato. Consultare il registro eventi sul server per altri eventi &quot;ExchangeStoreDb&quot; e &quot;MSExchange Search Indexer&quot; per informazioni più specifiche sugli errori. Si consiglia di effettuare il reseeding del catalogo tramite l'attività 'Update-MailboxDatabaseCopy'.</p></td>
</tr>
</tbody>
</table>


Se la copia del database delle cassette postali si trova su un server che è parte di un gruppo di disponibilità del database (DAG), è possibile effettuare il reseeding del catalogo di indicizzazione del contenuto da un altro membro DAG.

Se la copia del database delle cassette postali è l'unica copia, è necessario creare manualmente un nuovo catalogo di indicizzazione del contenuto.

Per altre attività di gestione relative al servizio di ricerca Exchange, vedere [Exchange Search procedures](exchange-search-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti. Il tempo di reseeding effettivo potrebbe variare in base alla dimensione del catalogo di indicizzazione del contenuto sottoposto a reseeding.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ricerca di Exchange" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Effettuare il reseeding del contenuto del catalogo di indicizzazione del contenuto, se il database delle cassette postali fa parte di un DAG

Utilizzare una delle procedure seguenti se il database delle cassette postali si trova su un server che è parte di un DAG.

## Esecuzione del reseeding del catalogo di indicizzazione del contenuto da qualsiasi origine

In questo esempio viene eseguito il reseeding del catalogo di indicizzazione del contenuto per la copia del database DB1 sul server Cassette postali MBX1 da qualsiasi server di origine in un gruppo di disponibilità del database (DAG) con una copia del database.

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly
```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)).

## Esecuzione dei reseeding del catalogo di indicizzazione del contenuto da una determinata origine

In questo esempio, viene eseguito il reseeding del catalogo di indicizzazione del contenuto per la copia del database DB1 sul server Cassette postali MBX1 dal server Cassette postali MBX2 contenente anche una copia del database.

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2 -CatalogOnly
```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Update-MailboxDatabaseCopy](https://technet.microsoft.com/it-it/library/dd335201\(v=exchg.150\)).

## Effettuare il reseeding del contenuto del catalogo di indicizzazione del contenuto, se è presente solo una copia del database delle cassette postali

Se è presente solo una copia del database delle cassette postali, è necessario effettuare il reseeding manuale del catalogo di ricerca tramite la ricreazione del catalogo di indicizzazione del contenuto.

1.  Eseguire i seguenti comandi per arrestare i servizi Microsoft Exchange Search e Microsoft Exchange Search Host Controller.
   
```powershell
Stop-Service MSExchangeFastSearch
```
   
   
```powershell
Stop-Service HostControllerService
```
   

2.  Eliminare, spostare o rinominare la cartella che contiene il catalogo di indicizzazione del contenuto di Exchange. La cartella è denominata `%ExchangeInstallPath\Mailbox\<name of mailbox database>_Catalog\<GUID>12.1.Single`. Ad esempio, è possibile rinominare la cartella `C:\Program Files\Microsoft\Exchange Server\V15\Mailbox\Mailbox Database 0657134726_Catalog\F0627A72-9F1D-494A-839A-D7C915C279DB12.1.Single_OLD`.
    

    > [!NOTE]
    > L'eliminazione della cartella renderà disponibile ulteriore spazio su disco. In alternativa, si potrebbe rinominare o spostare la cartella per tenerla per la risoluzione dei problemi.



3.  Eseguire i seguenti comandi per riavviare i servizi Microsoft Exchange Search e Microsoft Exchange Search Host Controller.
    
```powershell
Start-Service MSExchangeFastSearch
```
    
```powershell
Start-Service HostControllerService
```
  ```powershell 
    Dopo il riavvio di questi servizi, Exchange Search eseguirà la ricostruzione del catalogo di indicizzazione del contenuto.
```

## Come verificare se l'operazione ha avuto esito positivo

Potrebbe richiedere del tempo ad Exchange Search per effettuare il reseeding del catalogo di indicizzazione del contenuto. Eseguire questo comando per visualizzare lo stato del processo di reseeding.
```powershell
    Get-MailboxDatabaseCopyStatus | FL Name,*Index*
```
Quando il reseeding del catalogo di ricerca è in corso, il valore della proprietà *ContentIndexState* è **Ricerca per indicizzazione in corso**. Quando il reseeding è completo, questo valore viene modificato in **Integro**.


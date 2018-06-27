---
title: 'Spostamenti di cassette postali di Exchange 2013: Exchange 2013 Help'
TOCTitle: Spostamenti di cassette postali di Exchange 2013
ms:assetid: 9c0a0bc9-2a39-4cf0-aa6e-6e5ef3fd38b5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150543(v=EXCHG.150)
ms:contentKeyID: 50481274
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Spostamenti di cassette postali di Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-07_

Quando si sposta una cassetta postale, la si sposta da un *database delle cassette postali di origine* a un *database delle cassette postali di destinazione*. Il database delle cassette postali di destinazione può trovarsi sullo stesso server, su un server diverso, in un dominio diverso, in un sito diverso di Active Directory o in un'altra foresta.

## Motivi per lo spostamento delle cassette postali

Potrebbe essere necessario spostare le cassette postali nei seguenti scenari:

  - **Aggiornamento**   Quando si esegue l'aggiornamento di un'organizzazione di Microsoft Exchange Server 2007 o Exchange Server 2010 esistente a Exchange Server 2013, le cassette postali vengono spostate dai server di Exchange esistenti a un server Cassette postali di Exchange 2013.

  - **Riallineamento**   È possibile spostare le cassette postali per il riallineamento. Ad esempio, è possibile spostare una cassetta postale da un database a un altro in cui il limite di dimensioni delle cassette postali è maggiore.

  - **Analisi di un problema**   Per analizzare un problema che si è verificato in una cassetta postale, è possibile spostarla in un server diverso. Ad esempio, è possibile spostare tutte le cassette postali con un'elevata attività in un altro server.

  - **Cassette postali danneggiate**   In caso di cassette postali danneggiate, è possibile spostarle in un server o un database diverso. I messaggi danneggiati non verranno spostati.

  - **Modifiche alle posizioni fisiche**   È possibile spostare le cassette postali in un server di un sito diverso di Active Directory. Ad esempio, se un utente si sposta in una posizione fisica diversa, è possibile spostare la cassetta postale dell'utente in un server più vicino alla nuova posizione.

  - **Separazione dei ruoli amministrativi**   È possibile separare l'amministrazione di Exchange dall'amministrazione account del sistema operativo Windows. A tale scopo, è possibile spostare le cassette postali da una singola foresta a uno scenario di foreste delle risorse. In questo scenario, le cassette postali di Exchange risiedono in un'unica foresta, mentre gli account utente associati di Windows risiedono in un'altra foresta.

  - **Amministrazione esterna della posta elettronica**   È possibile decidere di affidare esternamente l'amministrazione della posta elettronica mantenendo l'amministrazione degli account utente di Windows. A tale scopo, è possibile spostare le cassette postali da una singola foresta a uno scenario di foreste delle risorse.

  - **Integrazione tra l'amministrazione della posta elettronica e degli account utente**   È possibile decidere di passare da un modello di amministrazione della posta elettronica separato o affidato a terzi a un modello in cui la posta elettronica e gli account utente possono essere gestiti nell'ambito della stessa foresta. A tale scopo, è possibile spostare le cassette postali da uno scenario di foreste delle risorse a una singola foresta. In questo scenario, le cassette postali di Exchange e gli account utente di Windows risiedono nella stessa foresta.

## Spostamenti di Exchange 2013

Microsoft Exchange Server 2013 introduce il concetto di *spostamenti in batch* ed *endpoint di migrazione*. Gli endpoint di migrazione sono oggetti di gestione che descrivono il server remoto e le connessioni che è possibile associare a uno o più batch. Inoltre, la nuova architettura di spostamento in batch migliora gli spostamenti del servizio di replica delle cassette postali (MRS) con capacità di gestione avanzate. L'architettura di spostamento in batch in Exchange 2013 dispone delle seguenti capacità:

  - Capacità di spostare più cassette postali in grandi batch.

  - Notifica di posta elettronica durante lo spostamento con creazione di un rapporto.

  - Ripetizione e prioritizzazione automatiche degli spostamenti.

  - Le cassette postali di archiviazione primarie e personali possono essere spostate insieme o separatamente.

  - Opzione per la finalizzazione della richiesta di spostamento manuale, che consente di rivedere lo spostamento prima di completarlo.

  - Sincronizzazioni incrementali periodiche per aggiornare i cambiamenti di migrazione.

In Exchange 2013 è necessario spostare le cassette postali tra Exchange 2007, Exchange 2010 e Exchange 2013 dall'interfaccia di amministrazione di Exchange 2013 ed Exchange Management Shell.


> [!NOTE]
> In Exchange 2013 è ancora possibile eseguire singoli spostamenti di cassette postali in maniera analoga a Exchange Server 2010 utilizzando Interfaccia di amministrazione di Exchange (EAC) oppure i cmdlet per le richieste di spostamento o i batch di migrazione.




> [!NOTE]
> Non è possibile spostare le cassette postali locali da Exchange Server 2003 a Exchange 2013.



Per ulteriori informazioni sulla gestione degli spostamenti nuovi ed esistenti, vedere [Gestire spostamenti locali](manage-on-premises-moves-exchange-2013-help.md).

## Endpoint di migrazione

Gli endpoint di migrazione acquisiscono le informazioni sul server remoto e mantengono le credenziali richieste per la migrazione dei dati e le impostazioni di limitazione delle richieste dell'origine. È possibile utilizzare gli endpoint di migrazione per configurare le impostazioni per gli spostamenti remoti e tra foreste. Gli spostamenti locali non richiedono l'utilizzo di un endpoint. (Gli spostamenti locali provocano lo spostamento delle cassette postali tra due diversi database di Exchange locali.)

Nell'elenco seguente sono riportati i tipi di spostamento che supportano gli endpoint di migrazione:

  - **Spostamento tra foreste**   Consente di spostare le cassette postali tra due diverse foreste di Exchange locali. Gli spostamenti tra foreste richiedono l'utilizzo di un endpoint RemoteMove di Exchange.

  - **Spostamento remoto**   In una distribuzione ibrida, uno spostamento remoto implica una migrazione *onboarding* o *offboarding*. Gli spostamenti remoti richiedono l'utilizzo di un endpoint RemoteMove. La modalità onboarding consente di spostare le cassette postali da un'organizzazione di Exchange locale a Exchange Online in Microsoft Office 365, utilizzando un endpoint RemoteMove come endpoint di origine del batch di migrazione. La modalità offboarding consente di spostare le cassette postali da Exchange Online in Office 365 a un'organizzazione di Exchange locale, utilizzando un endpoint RemoteMove di Exchange come endpoint di destinazione del batch di migrazione.

Nella tabella di seguito sono mostrati i tipi di endpoint di migrazione e i valori che è possibile gestire in Exchange 2013.

### Valori dei tipi di endpoint di migrazione

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange RemoteMove</th>
<th>Exchange LocalMove</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MaxConcurrentMigrations</p></td>
<td><p>MaxConcurrentMigrations</p></td>
</tr>
<tr class="even">
<td><p>RemoteServer</p></td>
<td><p>Sito</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDomain</p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>BadItemLimit</p></td>
</tr>
<tr class="even">
<td><p>Database</p></td>
<td><p>LargeItemLimit</p></td>
</tr>
<tr class="odd">
<td><p>TargetDeliveryDomain</p></td>
<td><p>PrimaryOnly</p></td>
</tr>
<tr class="even">
<td><p>PrimaryOnly</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDatabase</p></td>
<td><p>DAG</p></td>
</tr>
<tr class="even">
<td><p>ArchiveOnly</p></td>
<td><p>Forest</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni sugli endpoint di migrazione, vedere l'interfaccia utente **Migrazione** in Interfaccia di amministrazione di Exchange (EAC) e [New-MigrationEndpoint](https://technet.microsoft.com/it-it/library/jj218611\(v=exchg.150\)).

Per ulteriori informazioni sulla gestione degli spostamenti nuovi ed esistenti, vedere [Gestire spostamenti locali](manage-on-premises-moves-exchange-2013-help.md).


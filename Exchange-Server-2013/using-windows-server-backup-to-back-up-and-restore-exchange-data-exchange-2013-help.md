---
title: 'Windows Server Backup esegue backup/recupero dati Exchange: Exchange 2013 Help'
TOCTitle: Utilizzo di Windows Server Backup per eseguire il backup e il recupero dei dati di Exchange
ms:assetid: 0fac891a-5713-42b6-afd5-c91b2b88f966
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876851(v=EXCHG.150)
ms:contentKeyID: 50479997
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzo di Windows Server Backup per eseguire il backup e il recupero dei dati di Exchange

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Microsoft [architettura preferito](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx) per Exchange Server 2013 utilizza il concetto di Exchange Native Data Protection. Exchange Protezione dei dati nativi basato sulle funzionalità native Exchange per proteggere i dati delle cassette postali, senza l'utilizzo dei backup tradizionale. Ma se si desidera creare i backup, Exchange include un plug-in per Windows Server Backup (WSB) che consente di creare i backup compatibile con Exchange basate sul Volume del servizio Copia shadow del Exchange dati. Per sfruttare i backup compatibile con Exchange, è necessario disporre della funzionalità WSB installata.

Il componente aggiuntivo, WSBExchange.exe, viene eseguito come un servizio denominato Microsoft Exchange Server Extension per Windows Server Backup (il nome breve di questo servizio corrisponde a WSBExchange). Il servizio viene installato e configurato automaticamente e viene avviato manualmente su tutti i server Cassette postali. Il plug-in consente a WSB di creare backup compatibili con Exchange.

Prima di utilizzare WSB per eseguire il backup dei dati di Exchange, si consiglia di acquisire familiarità con le seguenti funzionalità e opzioni per il plug-in:

  - I backup eseguiti con WSB si verificano al livello del volume e l'unico modo per eseguire un backup o un ripristino a livello di applicazione consiste nel selezionare un volume intero. Per eseguire il backup di un database e del relativo flusso di registrazione, è necessario eseguire il backup dell'intero volume contenente i registri e il database, non soltanto le singole cartelle. Non è possibile eseguire il backup dei dati senza prima aver eseguito il backup dell'intero volume contenente i dati.

  - Il backup deve essere eseguito localmente sul server e non è possibile utilizzare il plug-in per effettuare backup VSS remoti. Non esiste un'amministrazione remota di WSB o del plug-in. Tuttavia, è possibile utilizzare Servizi Desktop remoto o Servizi terminal per gestire in remoto i backup.

  - Il backup può essere creato su un'unità locale o su una condivisione di rete remota.

  - È possibile eseguire solo backup completi. Il troncamento del registro si verifica solo dopo l'esecuzione di un backup VSS completo di un volume o di cartelle contenenti un database di Exchange.

  - Quando si ripristinano i dati, è possibile ripristinare solo i dati di Exchange. Tali dati possono essere ripristinati nella loro posizione originale o in una posizione alternativa. Se si ripristinano i dati nella posizione originaria, WSB e il plug-in gestiranno automaticamente il processo di ripristino, che comprende la disinstallazione di qualsiasi database esistente e la riproduzione dei registri nel database recuperato.

  - Il processo di ripristino non supporta direttamente il database di ripristino (RDB) di Exchange. Per utilizzare un RDB, è necessario ripristinare i dati in un percorso alternativo, quindi copiare o spostare i dati ripristinati da quel percorso alla struttura della cartella RDB.

  - Quando si esegue il ripristino dei dati di Exchange, tutti i database sottoposti a backup devono essere ripristinati insieme. Non è possibile ripristinare un singolo database.

  - I ripristini bare metal sono supportati quando si utilizza WSB; tuttavia, l'approccio di ripristino consigliato in relazione ai server di Exchange consiste nel recupero del server di Exchange e nel successivo ripristino dei dati. Se l'utente utilizza un'applicazione di terze parti per eseguire il backup (non Microsoft), il supporto relativo ai ripristini bare metal di Exchange viene fornito dal produttore di tale applicazione.

Nella seguente tabella viene descritta la supportabilità delle opzione di backup e ripristini disponibili per Exchange 2013 con WSB.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Se l'utente...</th>
<th>Quindi...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Eseguire il backup completo del server...</p></td>
<td><p>Viene eseguita una copia VSS del backup, quindi i registri della transazione per i database del server non vengono troncati.</p></td>
</tr>
<tr class="even">
<td><p>Eseguire un backup personalizzato e selezionare uno o più volumi per i quali eseguire il backup...</p></td>
<td><p>È possibile selezionare un backup VSS completo, che consente di troncare i registri relativi alle transazioni dei database nei volumi selezionai quando viene completato un backup.</p></td>
</tr>
<tr class="odd">
<td><p>Eseguire un backup personalizzato e selezionare una o più cartelle per i quali eseguire il backup...</p></td>
<td><p>È possibile selezionare un backup VSS completo al fine di troncare i file di registro. Tuttavia, il recupero del backup è limitato al ripristino dei file, dal momento che un ripristino a livello di applicazione non è disponibile.</p></td>
</tr>
</tbody>
</table>


Per visualizzare una procedura dettagliata per eseguire il backup di Exchange utilizzando WSB, vedere [Utilizzare Windows Server Backup per eseguire il backup di Exchange](use-windows-server-backup-to-back-up-exchange-exchange-2013-help.md).

Per la procedura dettagliata su come ripristinare i dati da un backup eseguito con WSB, vedere [Ripristino di un backup di Exchange tramite Windows Server Backup](use-windows-server-backup-to-restore-a-backup-of-exchange-exchange-2013-help.md).


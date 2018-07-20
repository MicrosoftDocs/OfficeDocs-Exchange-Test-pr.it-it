---
title: 'Prestazioni e lo stato dei server: Exchange 2013 Help'
TOCTitle: Prestazioni e lo stato dei server
ms:assetid: 9d1fdec8-8273-4c71-88f1-b4edfd542c4f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150551(v=EXCHG.150)
ms:contentKeyID: 50481299
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Prestazioni e lo stato dei server

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Informazioni sui server integrità e prestazioni è importante per la progettazione e la gestione di un'infrastruttura di messaggistica ad alte prestazioni. Microsoft Exchange Server 2013 introduce miglioramenti all'integrità del server e delle prestazioni.

Trovare un elenco di tutti gli argomenti relativi all'integrità e prestazioni server? Vedere la documentazione di integrità e alle prestazioni di Server.

## Disponibilità gestita

Exchange 2013 introduce il concetto di *disponibilità gestita*. Managed availability viene eseguito su ogni server Exchange 2013. Si è costituito dai due processi, il servizio di Exchange Health Manager (MSExchangeHMHost.exe) e il processo Exchange Health Manager Worker (MSExchangeHMWorker.exe) e i componenti asincroni seguenti:

  - **Motore di probe**   Il *motore di probe* accetta le misure nel server.

  - **Motore di probe di monitoraggio**   Il *motore di probe di monitoraggio* archivia la regola business su cosa si intende uno stato integro. Il risultato è analogo a un modulo di riconoscimento motivo, ricercare i modelli e le misure da che differiscono da uno stato integro e quindi valutare un componente o caratteristica non è integro.

  - **Motore di risponditore**   Quando il *motore di risponditore* viene generato un avviso per un componente non integro, la prima azione è provare a ripristinare tale componente. Azioni di ripristino in più fasi consente di disponibilità gestita. Il primo tentativo potrebbe essere necessario riavviare il pool di applicazioni, il secondo tentativo potrebbe essere necessario riavviare il servizio corrispondente e il tentativo di terzo potrebbe essere necessario riavviare il server. E l'ultimo tentativo potrebbe essere per mettere il server non in linea, in modo che non vengono più accettati traffico. Se tutte queste azioni hanno esito negativo, verrà inviato un avviso per il supporto tecnico.

Per ulteriori informazioni sulla disponibilità gestita, vedere [Disponibilità gestita](managed-availability-exchange-2013-help.md).

## Gestione del carico di lavoro

gestione del carico di lavoro Exchange 2013 include i componenti seguenti:

  - *Gestione del carico di lavoro* è il nuovo nome per l'utente la limitazione della funzionalità di Exchange Server 2010. È possibile personalizzare queste impostazioni in base alle esigenze del proprio ambiente.

  - *Gestione del carico di lavoro del sistema* è stata introdotta Exchange 2013 e viene utilizzato per limitare automaticamente specifici carichi di lavoro di Exchange per il monitoraggio dell'integrità delle risorse chiave del server. Queste impostazioni devono essere personalizzate solo seguendo le istruzioni del cliente servizio supporto tecnico Microsoft.

Per ulteriori informazioni, vedere [Gestione del carico di lavoro di Exchange](exchange-workload-management-exchange-2013-help.md).

## Documentazione relativa all'integrità e prestazioni di server

Nella tabella seguente contiene collegamenti ad argomenti che consentono di conoscere e gestire lo stato dei server e le prestazioni in Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Argomento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="exchange-workload-management-exchange-2013-help.md">Gestione del carico di lavoro di Exchange</a></p></td>
<td><p>Informazioni sulla gestione dei carichi di lavoro di Exchange tramite il controllo risorse impiegate da singoli utenti.</p></td>
</tr>
<tr class="even">
<td><p><a href="managed-availability-exchange-2013-help.md">Disponibilità gestita</a></p></td>
<td><p>Per conoscere le azioni di monitoraggio e il ripristino di risorse predefiniti disponibili in Exchange 2013.</p></td>
</tr>
</tbody>
</table>


---
title: 'Failover Cluster comando interfaccia Windows non installato:Exchange 2013 Help'
TOCTitle: Funzionalità di failover Cluster comando interfaccia Windows non è installato
ms:assetid: 0d839514-5ab7-497d-8945-41392b4c3980
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.rsatclusteringcmdinterfaceinstalled(v=EXCHG.150)
ms:contentKeyID: 51407337
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Funzionalità di failover Cluster comando interfaccia Windows non è installato

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2014-12-03_

L'installazione di Microsoft Exchange Server 2013 non può procedere perché nel computer locale non è presente una funzionalità di Windows necessaria. È necessario installare questa funzionalità di Windows prima che Exchange 2013 possa procedere.

Exchange 2013 Installazione richiede che la funzionalità di **Interfaccia di comando Cluster di Failover** Windows vengano installati nel computer prima di continuare.

Effettuare le operazioni seguenti per installare la funzionalità di Windows nel computer in uso. Se è necessario riavviare il computer per completare l'installazione della funzionalità, uscire dal programma di installazione di Exchange 2013, riavviare ed eseguire nuovamente l'installazione.


> [!NOTE]
> Potrebbe essere necessario installare ulteriori funzionalità o aggiornamenti di Windows prima che l'installazione di Exchange 2013 possa procedere. Per un elenco completo delle funzionalità e degli aggiornamenti di Windows richiesti, vedere <A href="exchange-2013-prerequisites-exchange-2013-help.md">Prerequisiti di Exchange 2013</A>.



1.  Aprire Windows PowerShell nel computer locale.

2.  Eseguire il comando seguente per installare la caratteristica di Windows necessaria.
    
        Install-WindowsFeature RSAT-Clustering-CmdInterface

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.


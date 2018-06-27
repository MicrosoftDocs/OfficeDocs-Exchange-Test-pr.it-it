---
title: "Eseguire l'Override Controller di dominio è impostato nel Registry_ConfigDCHostNameMismatch: Exchange 2013 Help"
TOCTitle: Eseguire l'Override Controller di dominio è impostato nel Registry_ConfigDCHostNameMismatch
ms:assetid: 3aef5470-d510-4b59-a4b6-36d274a984ae
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.configdchostnamemismatch(v=EXCHG.150)
ms:contentKeyID: 50480443
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eseguire l'Override Controller di dominio è impostato nel Registry\_ConfigDCHostNameMismatch

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2016-12-15_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Il programma di installazione di Microsoft Exchange Server 2007 non può continuare il tentativo di utilizzare controller di dominio specificato. Un controller di dominio in modo statico mappato nel Registro di sistema.

Installazione di Exchange 2007 è necessario che il controller di dominio specificato nel comando il programma di installazione deve corrispondere il controller di dominio in modo statico mappata tramite una sostituzione del Registro di sistema.

Per risolvere questo problema, eseguire l'installazione, specificando il controller di dominio mappato in modo statico per il **/DomainController: \<***FQDN of thestatically mapped domain controller***\>** parametro.

Per ulteriori informazioni su DSAccess e rilevamento servizi directory, vedere l'articolo della Microsoft Knowledge Base 250570 "Directory Service Server Detection and DSAccess Usage" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=250570](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=250570)).


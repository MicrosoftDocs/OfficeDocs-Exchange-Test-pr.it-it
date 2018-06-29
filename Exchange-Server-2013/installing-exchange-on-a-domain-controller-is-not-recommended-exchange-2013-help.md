---
title: 'Installazione di Exchange in un controller di dominio non è consigliabile: Exchange 2013 Help'
TOCTitle: Installazione di Exchange in un controller di dominio non è consigliabile
ms:assetid: 48922de2-a68c-4092-96a5-d38c8e5f49f5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.warninginstallexchangerolesondomaincontroller(v=EXCHG.150)
ms:contentKeyID: 50480512
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Installazione di Exchange in un controller di dominio non è consigliabile

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2013-03-22_

Il programma di installazione di Microsoft Exchange Server 2013 ha rilevato che il computer in cui si sta tentando di installare Exchange 2013 è un controller di dominio Active Directory. L'installazione di Exchange 2013 in un controller di dominio non è consigliabile.

Se si installa Exchange 2013 in un controller di dominio, tenere presenti i seguenti problemi:

  - La configurazione di Exchange 2013 per la suddivisione delle autorizzazioni di Active Directory non è supportata.

  - Quando si installa Exchange in un controller di dominio, il gruppo di protezione universale (USG, Universal Security Group ) Exchange Trusted Subsystem viene aggiunto al gruppo Domain Admins. In tal caso, a tutti i server Exchange del dominio vengono concessi i diritti di amministratore di dominio per quel dominio.

  - Exchange Server e Active Directory sono entrambe applicazioni che richiedono un utilizzo intensivo delle risorse. Quando vengono eseguite entrambe sullo stesso computer, le prestazioni ne verranno influenzate.

  - Assicurarsi che il controller di dominio in cui è installato Exchange 2013 sia un server di catalogo globale.

  - I servizi di Exchange potrebbero non essere avviati correttamente se il controller di dominio è anche un server di catalogo globale.

  - L'arresto del sistema richiederà molto più tempo se i servizi di Exchange non vengono arrestati prima di arrestare o riavviare il server.

  - L'abbassamento di livello di un controller di dominio a un server membro non è supportato.

  - L'esecuzione di Exchange 2013 su un nodo di cluster che è anche un controller di dominio Active Directory non è supportata.

Si consiglia di installare Exchange 2013 su un server membro.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.


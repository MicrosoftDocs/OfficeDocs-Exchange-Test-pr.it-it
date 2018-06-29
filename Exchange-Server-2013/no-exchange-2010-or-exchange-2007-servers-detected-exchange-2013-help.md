---
title: 'Nessun server Exchange 2010 o Exchange 2007 rilevato: Exchange 2013 Help'
TOCTitle: Nessun server Exchange 2010 o Exchange 2007 rilevato
ms:assetid: 789cabab-c769-4a16-a6c8-3db82cff8861
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.noe14serverwarning(v=EXCHG.150)
ms:contentKeyID: 50481005
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Nessun server Exchange 2010 o Exchange 2007 rilevato

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2012-11-08_

Questo messaggio è stato visualizzato dal programma di installazione di Microsoft Exchange Server 2013 in quanto non esistono ruoli del server Exchange Server 2010 o Exchange Server 2007 nell'organizzazione.


> [!WARNING]
> Continuando con l'installazione di Exchange Server 2013, in futuro non sarà possibile aggiungere server Exchange&nbsp;2010 o Exchange&nbsp;2007 all'organizzazione.



Prima di distribuire Exchange 2013, prendere in considerazione i seguenti fattori che potrebbero richiedere la distribuzione di server Exchange 2010 o Exchange 2007 prima di distribuire Exchange 2013:

  - **Applicazioni di terze parti o sviluppate internamente**   Le applicazioni sviluppate per versioni precedenti di Exchange possono non essere compatibili con Exchange 2013. Potrebbe essere opportuno continuare a utilizzare server Exchange 2010 o Exchange 2007 in grado di supportare tali applicazioni.

  - **Requisiti di coesistenza o migrazione**   Se si intende eseguire la migrazione delle cassette postali nell'organizzazione, alcune soluzioni possono richiedere l'utilizzo di server Exchange 2010 o Exchange 2007.

Se è necessario distribuire server Exchange 2010 o Exchange 2007, effettuare l'operazione prima di distribuire Exchange 2013. È indispensabile preparare Active Directory per ogni versione di Exchange nel seguente ordine:

1.  Exchange 2007

2.  Exchange 2010

3.  Exchange 2013

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.


---
title: 'ExecutionPolicy GPO è definita: Exchange 2013 Help'
TOCTitle: ExecutionPolicy GPO è definita
ms:assetid: 63de83e2-9a6b-4f57-85b9-df445bea18dd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.powershellexecutionpolicycheckset(v=EXCHG.150)
ms:contentKeyID: 61202267
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ExecutionPolicy GPO è definita

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2016-12-15_

Impossibile proseguire con la configurazione di Microsoft Exchange Server 2013 perché è stato rilevato che l'oggetto criteri di gruppo (GPO) **ExecutionPolicy** definisce uno o entrambi i seguenti criteri:

  - **MachinePolicy**

  - **UserPolicy**

Non importa come sono stati definiti i criteri. È importante solo che essi sono stati definiti.

Quando si esegue la configurazione di Exchange 2013, Exchange si arresta e disabilita il servizio WMI (Strumentazione gestione Windows). Quando sono definiti entrambi i criteri, il servizio WMI deve essere abilitato per eseguire uno script di Windows PowerShell. Se i criteri sono definiti e il servizio WMI viene interrotto, il setup non viene completato e il server viene lasciato in uno stato incoerente.

Per poter proseguire con la configurazione, è necessario rimuovere temporaneamente tutte le definizioni di **MachinePolicy** o **UserPolicy** nel GPO **ExecutionPolicy**.

Per informazioni su come rimuovere tutte le definizioni di **MachinePolicy** o **UserPolicy** nel GPO **ExecutionPolicy**, vedere [l'articolo della Knowledge Base KB981474](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=981474).


> [!NOTE]
> Anche se l'articolo è stato scritto per Exchange 2010, viene applicato anche agli aggiornamenti cumulativi e ai service pack di Exchange 2013.



Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.


---
title: 'Utilizzare un Exchange 2010 o 2007 server Trasporto Edge di Exchange 2013: Exchange 2013 Help'
TOCTitle: Utilizzare un Exchange 2010 o 2007 server Trasporto Edge di Exchange 2013
ms:assetid: ce99b4bd-868c-4767-9009-e22c17ac0ac7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150569(v=EXCHG.150)
ms:contentKeyID: 50481698
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzare un Exchange 2010 o 2007 server Trasporto Edge di Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Il server Trasporto Edge è disponibile in Microsoft Exchange Server 2013 Service Pack 1 (SP1). È tuttavia possibile continuare a utilizzare i server Trasporto Edge Exchange Server 2007 o Exchange Server 2010 esistenti distribuiti nella rete perimetrale. In alternativa è possibile installare un nuovo server Trasporto Edge Exchange 2007 o Exchange 2010 nella rete perimetrale per una nuova organizzazione di Exchange 2013 aggiornata.

Saranno necessarie le nozioni seguenti:

  - Per un server Trasporto Edge Exchange 2007 o Exchange 2010 è prevista una connessione a un server Trasporto Hub. In Exchange 2013 esiste il servizio di trasporto sul server Cassette postali. Pertanto il flusso di posta in Internet transita tra il servizio di trasporto sul server Cassette postali e il server Trasporto Edge, che ignora il server Accesso client Exchange 2013.

  - È possibile sottoscrivere un server Trasporto Edge di Exchange 2007 o Exchange 2010 per un sito di Active Directory che contiene solo server Exchange 2013. È possibile importare il file di sottoscrizione Edge ed eseguire EdgeSync su un server Cassette postali di Exchange 2013 autonomo o su un server in cui il server Cassette postali e il server Accesso client sono installati nello stesso computer. Non è possibile importare il file di sottoscrizione Edge o eseguire EdgeSync su un server Accesso client di Exchange 2013 autonomo.

  - Le procedure per la distribuzione di un nuovo server Trasporto Edge Exchange 2007 o Exchange 2010 nell'organizzazione Exchange 2013 sono fondamentalmente le stesse delle versioni precedenti di Exchange. Tuttavia le procedure eseguite sul server Trasporto Hub sono eseguite sul server Cassette postali in Exchange 2013. Le procedure includono:
    
      - [Configurare il flusso della posta Internet tramite un Server Trasporto Edge sottoscritto](https://go.microsoft.com/fwlink/p/?linkid=275859)
    
      - [Configurare il flusso della posta tra un Server Trasporto Edge e i server Trasporto Hub senza utilizzare EdgeSync](https://go.microsoft.com/fwlink/p/?linkid=276661)


---
title: 'Domande frequenti sulla procedura guidata di configurazione ibrida: Exchange 2013 Help'
TOCTitle: Domande frequenti sulla procedura guidata di configurazione ibrida
ms:assetid: e911e6e0-e36e-4430-ac36-c745a10d6c26
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt488940(v=EXCHG.150)
ms:contentKeyID: 72045781
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Domande frequenti sulla procedura guidata di configurazione ibrida

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

Microsoft ha rilasciato una nuova procedura guidata per la configurazione ibrida che semplifica la configurazione di una distribuzione ibrida, consente una maggiore flessibilità e offre le versioni più aggiornate. Questa versione della procedura guidata ibrida è incorporata in Exchange 2016 e versioni di Exchange 2013 iniziando dall'aggiornamento cumulativo 10. Tuttavia, è possibile scaricare la nuova procedura guidata anche se si esegue una versione dell'aggiornamento cumulativo di Exchange 2013 meno recente o di Exchange 2010 Service Pack 3 (SP3).

Per ulteriori informazioni sulla procedura guidata per la configurazione ibrida di Office 365, vedere [Introducing the Microsoft Office 365 Hybrid Configuration Wizard](http://go.microsoft.com/fwlink/?linkid=717122) e [Office 365 Hybrid Configuration Wizard for Exchange 2010](http://go.microsoft.com/fwlink/?linkid=730687) nel blog del team di Exchange.

Per scaricare la procedura guidata per la configurazione ibrida di Office 365, andare a [http://aka.ms/HybridWizard](http://aka.ms/hybridwizard).

## Domande frequenti dai clienti

  - D: Quali versioni di Exchange supportano la nuova procedura guidata per la configurazione ibrida?  
    R: È necessario disporre di almeno un server che soddisfi i requisiti seguenti:
    
      - **Exchange 2010**Exchange 2010 Service Pack 3 deve essere installato su almeno un server che esegue i ruoli del server Cassetta postale, Trasporto Hub e Accesso client. È inoltre consigliabile installare l’aggiornamento cumulativo più recente disponibile per Exchange 2010 SP3.
    
      - **Exchange 2013** L’aggiornamento cumulativo più recente di Exchange 2013 deve essere installato su almeno un server che esegue i ruoli del server Cassetta postale e Accesso client. Se non è possibile installare l'aggiornamento cumulativo più recente, è supportata anche la versione immediatamente precedente. Aggiornamenti cumulativi precedenti non sono supportati.
    
      - **Exchange 2016** L’aggiornamento cumulativo più recente di Exchange 2016 deve essere installato su almeno un server che esegue il ruolo del server Cassetta postale.
    
    Si supponga, ad esempio, di aver installato Exchange 2013 CU8 nell'organizzazione locale e che la versione più recente di Exchange 2013 disponibile sia CU10. Per rimanere in una configurazione ibrida supportata, è necessario aggiornare i server di Exchange 2013 almeno all'aggiornamento cumulativo CU9. Tuttavia, si consiglia vivamente di eseguire l'aggiornamento cumulativo CU10.
    
    Gli aggiornamenti cumulativi vengono rilasciati ogni 3 mesi. Pertanto, aggiornare i server all'aggiornamento cumulativo più recente garantisce un'ulteriore flessibilità qualora fosse necessario più tempo per completare gli aggiornamenti.

<!-- end list -->

  - D: La procedura guidata di configurazione ibrida funzionerà con Exchange 2007?  
    R: È possibile configurare una distribuzione ibrida con Exchange 2007 nell'organizzazione. Tuttavia, a tale scopo è necessario distribuire almeno un server che esegue Exchange 2013 che soddisfi i requisiti riportati sopra.

<!-- end list -->

  - D: È possibile scegliere la nuova procedura guidata di configurazione ibrida?  
    R: No. La procedura guidata di configurazione ibrida è l’unica attualmente supportata in Exchange 2010, Exchange 2013 e Exchange 2016.

<!-- end list -->

  - D: È possibile aggiornare la configurazione ibrida di Exchange 2010 attuale per Exchange 2013 o Exchange 2016 utilizzando la nuova procedura guidata di configurazione ibrida?  
    R: Sì. Assicurarsi di disporre di almeno un server che soddisfi i requisiti per la procedura guidata di configurazione ibrida corrente, quindi eseguirla. La procedura guidata verificherà lo stato corrente della configurazione ibrida e illustrerà facilmente il processo di aggiornamento.


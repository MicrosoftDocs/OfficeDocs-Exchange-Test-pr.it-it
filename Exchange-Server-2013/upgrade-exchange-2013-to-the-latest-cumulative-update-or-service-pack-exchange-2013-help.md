---
title: "Upgrade di Exchange 2013 all'aggiornamento cumulativo o Service Pack più recente: Exchange 2013 Help"
TOCTitle: Upgrade di Exchange 2013 all'aggiornamento cumulativo o Service Pack più recente
ms:assetid: 928a4a0b-0082-4d50-a696-bfaf2782f42d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ983803(v=EXCHG.150)
ms:contentKeyID: 52063127
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Upgrade di Exchange 2013 all'aggiornamento cumulativo o Service Pack più recente

 

_**Si applica a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-09-04_

Se Microsoft Exchange Server 2013 è installato, è possibile eseguire l'aggiornamento all'aggiornamento cumulativo o service pack di Exchange 2013 più recente. È possibile usare l'installazione guidata di Exchange 2013 per aggiornare la versione corrente di Exchange 2013. Per ulteriori informazioni sull'aggiornamento cumulativo o service pack più recente di Exchange 2013, vedere [Aggiornamenti per Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md). Per ulteriori informazioni su Exchange 2013, vedere [Novità di Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).


> [!WARNING]
> Dopo aver eseguito l'aggiornamento di Exchange 2013 ad un nuovo aggiornamento o service pack cumulativo, non è più possibile disinstallare la nuova versione per tornare alla versione precedente. Se si disinstalla la nuova versione, Exchange verrà rimosso dal server.



## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 60 minuti

  - Leggere le note sulla versione prima di iniziare l'installazione di Exchange 2013. Per ulteriori informazioni, vedere [Note sulla versione di Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - Accertarsi che per i server in cui si pianifica di installare l'aggiornamento cumulativo o service pack vengano soddisfatti i requisiti e i prerequisiti di sistema. Per ulteriori informazioni, vedere [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md) e [Prerequisiti di Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).
    

    > [!WARNING]
    > Qualsiasi impostazione personalizzata per singolo server apportata nei file di configurazione dell'applicazione XML di Exchange, ad esempio, i file web.config sui server Accesso client oppure il file EdgeTransport.exe.config sui server Cassette postali, verrà sovrascritta quando si installa un aggiornamento cumulativo di Exchange. Salvare queste informazioni in modo da poter facilmente riconfigurare il server dopo l'installazione. È necessario riconfigurare queste impostazioni dopo aver installato un aggiornamento cumulativo di Exchange.



  - Dopo l'installazione di un aggiornamento cumulativo o service pack, è necessario riavviare il computer per applicare le modifiche al registro e al sistema operativo.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Installare service pack o aggiornamento cumulativo Exchange 2013

È possibile installare l'aggiornamento cumulativo o service pack per Exchange 2013 tramite l'installazione guidata o in modalità automatica. Per istruzioni specifiche, vedere i seguenti argomenti:

  - [Installazione di Exchange 2013 utilizzando l'installazione guidata](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

  - [Installare Exchange 2013 utilizzando la modalità automatica](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)

Se il computer su cui è stato installato un service pack o un aggiornamento cumulativo fa parte di un gruppo di disponibilità dei database, seguire la procedura nella sezione [Gestione dei gruppi di disponibilità del database](managing-database-availability-groups-exchange-2013-help.md) dell'argomento [Gestione dei gruppi di disponibilità del database](managing-database-availability-groups-exchange-2013-help.md).


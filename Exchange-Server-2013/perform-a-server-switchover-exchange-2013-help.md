---
title: 'Esecuzione del passaggio di un server: Exchange 2013 Help'
TOCTitle: Esecuzione del passaggio di un server
ms:assetid: ffcefd56-b0a0-4229-9011-fff4197b7c74
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298187(v=EXCHG.150)
ms:contentKeyID: 62523894
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Esecuzione del passaggio di un server

 

_**Si applica a:** Exchange Server 2013 SP1_

_**Ultima modifica dell'argomento:** 2014-06-23_

L'esecuzione del passaggio server è un'attività che consente di spostare tutte le copie del database delle cassette postali attive dal server Cassette postali corrente a uno o più server Cassette postali in un gruppo di disponibilità del database (DAG, database availability group). Questa attività viene eseguita come parte della preparazione per un'interruzione pianificata del server Cassette postali selezionato.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 30 secondi per database

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di disponibilità del database" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Esecuzione del passaggio di un server tramite EAC

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere"Copie del database cassette postali" nell'argomento [Elevata disponibilità e sito le autorizzazioni resilienza](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **server**.

2.  Selezionare il server Cassette postali di cui si desidera eseguire il passaggio.

3.  Nel riquadro dei dettagli, selezionare **Passaggio del server**.

4.  Nella pagina **Passaggio del server**, effettuare una delle seguenti operazioni:
    
    1.  Accettare l'impostazione predefinita **Scegli automaticamente un server destinazione** (in questo caso il sistema sceglie automaticamente il miglior server di cassette postali per ciascun database da passare), quindi scegliere **Salva**.
    
    2.  Selezionare **Utilizzare il server specificato come destinazione per il passaggio**, fare clic su **Sfoglia** per selezionare un server di cassette postali, quindi scegliere **Salva**.

5.  Al termine del passaggio, fare clic su **Chiudi** per uscire dalla pagina **Passaggio del server**.

## Esecuzione del passaggio del server tramite Shell

In questo esempio viene eseguito un passaggio di server per il server MBX1. Il sistema seleziona automaticamente il server Cassette postali migliore per ogni database attivo su MBX1.

```powershell
Move-ActiveMailboxDatabase -Server MBX1
```

In questo esempio viene eseguito un passaggio di server per il server Cassette postali MBX4. Al termine dell'operazione, il server MBX5 ospita la copia attiva dei database precedentemente attivi sul server MBX4.

```powershell
Move-ActiveMailboxDatabase -Server MBX4 -ActivateOnServer MBX5
```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Move-ActiveMailboxDatabase](https://technet.microsoft.com/it-it/library/dd298068\(v=exchg.150\)).


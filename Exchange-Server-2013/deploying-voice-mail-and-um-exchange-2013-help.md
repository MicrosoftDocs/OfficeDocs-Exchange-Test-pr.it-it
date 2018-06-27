---
title: 'Distribuzione di segreteria telefonica e messaggistica UNIFICATA: Exchange 2013 Help'
TOCTitle: Distribuzione di segreteria telefonica e messaggistica UNIFICATA
ms:assetid: 3df61b62-a1e4-41fb-969c-319189ae4e42
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673519(v=EXCHG.150)
ms:contentKeyID: 50480464
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Distribuzione di segreteria telefonica e messaggistica UNIFICATA

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

La messaggistica unificata di Exchange consente di fornite servizi di posta vocale agli utenti nell'organizzazione. Quando si distribuisce la messaggistica unificata, è necessario integrare la distribuzione di Exchange Server con il sistema di telefonia esistente nell'organizzazione o con Microsoft Lync Server. Una distribuzione corretta richiede un'attenta analisi dell'infrastruttura telefonica esistente e l'esecuzione della procedura di pianificazione corretta per distribuire e gestire la posta vocale in Messaggistica unificata. Se si sta eseguendo l'integrazione di Exchange con Lync Server, è necessario acquisire familiarità con quel prodotto.

Quando si distribuisce la messaggistica unificata, è possibile scegliere tra diverse opzioni in base all'hardware telefonico disponibile nell'organizzazione. Se si connette la messaggistica unificata alla rete telefonica, è possibile che nell'organizzazione sia presente una delle seguenti configurazioni telefoniche:

  - Uno o più gateway VoIP con uno o più sistemi PBX

  - Uno o più IP PBX

  - Uno o più sistemi PBX abilitati per SIP

  - Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server 2010 o 2013


> [!WARNING]
> Quando si distribuisce la messaggistica unificata di Exchange in un ambiente ospitato o ibrido, è necessario distribuire dei session border controller. I session border controller non permettono alla messaggistica unificata di connettersi a una rete telefonica né forniscono un segnale di linea per un'organizzazione. Tuttavia, connettono la distribuzione della messaggistica unificata locale a un datacenter utilizzando il protocollo IP su una WAN pubblica o privata.



**Hardware telefonico**   Scegliere il gateway VoIP, IP PBX o SBC corretto è solo il primo passo nella procedura di integrazione della rete telefonica con la messaggistica unificata. È necessario configurare questi dispositivi per l'utilizzo con la messaggistica unificata, distribuire i ruoli Accesso client e Cassette postali necessari e creare e configurare tutti i componenti della messaggistica unificata richiesti. Questi componenti consentono di connettere la rete con protocollo basato su circuiti alla rete di dati IP e abilitare la posta vocale per gli utenti nell'organizzazione. Per ulteriori informazioni, vedere [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

**Microsoft Lync Server**   La messaggistica unificata può utilizzare Microsoft Lync Server per combinare funzionalità di messaggistica vocale, messaggistica istantanea, presenza avanzata, conferenza audio/video e posta elettronica in un ambiente di comunicazione integrato e intuitivo. L'integrazione della messaggistica unificata e di Lync Server offre i seguenti vantaggi:

  - Notifiche di presenza avanzate, disponibili per numerose applicazioni, che consentono di informare gli utenti sulla disponibilità dei contatti.

  - L'integrazione di messaggistica istantanea, messaggistica vocale, conferenze, posta elettronica e altri metodi di comunicazione che consentono agli utenti di selezionare la modalità più appropriata alla loro attività. Gli utenti possono anche passare da una modalità all'altra.

  - Disponibilità di metodi di comunicazione alternativi da qualsiasi postazione dotata di una connessione Internet.

  - Un client intelligente (Microsoft Lync) per telefonia, messaggistica istantanea e conferenze.

  - Modalità di utilizzo coerenti tra dispositivi diversi.

Per ulteriori informazioni su Lync Server, vedere [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

## Fasi di distribuzione

Per la messaggistica unificata sono disponibili molte opzioni di distribuzione. Le singole opzioni hanno in comune diversi passi che sono necessari per creare un sistema modulare e ad alta disponibilità per un gran numero di utenti. Questi passaggi sono i seguenti:

1.  Distribuire e configurare i componenti di telefonia o Microsoft Lync Server con la messaggistica unificata.

2.  Verificare che siano stati installati correttamente i ruoli del server Accesso client e Cassette postali necessari per la messaggistica unificata.
    

    > [!WARNING]
    > È necessario distribuire un server Cassette postali di Exchange 2013 nell'organizzazione prima di configurare i gateway VoIP e gli IP PBX per inviare il traffico SIP messaggistica unificata e RTP ai server Accesso client di Exchange 2013.



3.  Creare e configurare i componenti richiesti per la messaggistica unificata, tra cui dial plan, gateway IP, gruppi di risposta e criteri cassetta postale di messaggistica unificata.

4.  Eseguire le attività successive alla distribuzione, come la distribuzione dei certificati per MTLS, la creazione di operatori automatici di messaggistica unificata e le funzionalità client.

Per ulteriori informazioni sulla distribuzione di messaggistica unificata, vedere [Distribuzione della messaggistica unificata di Exchange 2013](deploy-exchange-2013-um-exchange-2013-help.md).

Se si integra l'ambiente di messaggistica unificata con Microsoft Lync Server, è necessario tenere presenti altre considerazioni di pianificazione. Per ulteriori informazioni, vedere [Distribuzione di panoramica della messaggistica UNIFICATA di Exchange 2013 e Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md).


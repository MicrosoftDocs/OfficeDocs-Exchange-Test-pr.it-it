---
title: 'Impostazioni dispositivo Exchange ActiveSync con distribuzioni ibride di Exchange: Exchange 2013 Help'
TOCTitle: Impostazioni dispositivo Exchange ActiveSync con distribuzioni ibride di Exchange
ms:assetid: 77f7cd72-2a8a-467e-9ffd-b93f5eeb2f69
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn931281(v=EXCHG.150)
ms:contentKeyID: 64361797
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Impostazioni dispositivo Exchange ActiveSync con distribuzioni ibride di Exchange

 

_**Si applica a:**Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-01-27_

I dispositivi Exchange ActiveSync vengono riconfigurati automaticamente quando una cassetta postale viene spostata da un'organizzazione di Exchange locale in Office 365. Exchange ActiveSync troverà il nuovo percorso della cassetta postale in Office 365 e aggiornerà la sua configurazione per rivolgersi direttamente a Office 365. Il dispositivo Exchange ActiveSync non effettuerà tentativi e contatterà il server Exchange locale dopo che è stato reindirizzato a Office 365. Salvo alcune eccezioni (descritte di seguito), l'utente non ha più bisogno di configurare manualmente il dispositivo affinché la posta continui a funzionare.

Se si desidera spostare una cassetta postale in Office 365, vedere [Spostare le cassette postali tra le organizzazioni locali e di Exchange Online nelle distribuzioni ibride](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md).

Per ulteriori informazioni sulle distribuzioni ibride, vedere [Distribuzioni ibride di Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

Per utilizzare il reindirizzamento automatico, i server locali devono eseguire le versioni più recenti di Exchange 2010, Exchange 2013, Exchange 2016 o versioni successive. È inoltre necessario aver già utilizzato [Procedura guidata di configurazione ibrida](hybrid-configuration-wizard-exchange-2013-help.md) per configurare la distribuzione ibrida. La funzionalità di reindirizzamento di Exchange ActiveSync utilizza l'URL di destinazione di Outlook sul Web configurato nell'oggetto relazione dell'organizzazione. L'oggetto viene configurato quando viene eseguita la procedura guidata per la configurazione ibrida.

Se l'organizzazione soddisfa i requisiti elencati sopra, i dispositivi mobili dovrebbero essere reindirizzati automaticamente a Office 365 quando una cassetta postale dell'utente viene spostata, senza ulteriore configurazione. Per ottenere i migliori risultati, verificare che i dispositivi mobili degli utenti eseguano le versioni più recenti dei sistemi operativi e dei client di posta elettronica. Per alcuni dispositivi mobili, ad esempio quelli che eseguono il sistema operativo Android, il reindirizzamento potrebbe richiedere più tempo del previsto. Inoltre, alcuni dispositivi potrebbero non interpretare correttamente le istruzioni di reindirizzamento di Exchange ActiveSync 451 inviate da Exchange. Per questi dispositivi, gli utenti dovranno comunque riconfigurarli manualmente o ricreare l'account di posta elettronica sul dispositivo. Per sapere se un dispositivo supporta il reindirizzamento di Exchange ActiveSync 451, contattare il produttore del dispositivo.

Il reindirizzamento automatico di Exchange ActiveSync non è supportato negli scenari seguenti:

  - Spostamento delle cassette postali da Office 365 a un'organizzazione di Exchange locale.

  - Spostamento delle cassette postali tra organizzazioni di Exchange locali.

  - Spostamento delle cassette postali dai server Exchange 2007 a Office 365.


---
title: 'Registri di trasporto: Exchange 2013 Help'
TOCTitle: Registri di trasporto
ms:assetid: f8cf635d-60c2-4aa3-9c06-244c29942cba
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd302434(v=EXCHG.150)
ms:contentKeyID: 50482109
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registri di trasporto

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-01-28_

I registri di trasporto forniscono informazioni su ciò che accade nella pipeline di trasporto. In Microsoft Exchange Server 2013 sono disponibili i seguenti registri di trasporto:

**Registri degli agenti** Nei registri degli agenti vengono registrate le azioni eseguite su un messaggio da specifici agenti di protezione dalla posta indesiderata. La registrazione agente è disponibile nel servizio di trasporto su un server Cassette postali. Per ulteriori informazioni, vedere [Registrazione agente di protezione da posta indesiderata](anti-spam-agent-logging-exchange-2013-help.md).

**Registrazione connettività** La registrazione connettività registra i servizi di trasporto di attività di connessione in uscita. La registrazione della connettività è disponibile nel servizio di trasporto front-end dei server Accesso client, nel servizio di trasporto dei server Cassette postali e nel servizio di trasporto delle cassette postali nei server Cassette postali. Per ulteriori informazioni, vedere [Registrazione di integrazione applicativa](connectivity-logging-exchange-2013-help.md).

**Verifica messaggi e rapporti di recapito**   Nei registri di verifica messaggi viene registrata tutta l'attività relativa ai messaggi trasferiti a/da un server Cassette postali di Exchange 2013. La verifica dei messaggi è disponibile nel servizio di trasporto e nel servizio di trasporto cassette postali sui server Cassette postali. Per ulteriori informazioni, vedere [Verifica messaggi](message-tracking-exchange-2013-help.md).

I rapporti di recapito utilizzano le informazioni archiviate nel registro di verifica messaggi per cercare informazioni sui messaggi inviati a/da una specifica cassetta postale. Per ulteriori informazioni, vedere [Rapporti di recapito per gli amministratori](delivery-reports-for-administrators-exchange-2013-help.md).

**Analisi della pipeline**   L'analisi della pipeline registra snapshot dei messaggi prima e dopo l'intervento degli agenti di trasporto nel servizio di trasporto sui server Cassette postali e nel servizio Recapito alle cassette postali nei server Cassette postali. Per ulteriori informazioni, vedere [Analisi della pipeline](pipeline-tracing-exchange-2013-help.md).

**Registri di protocollo**   Con la registrazione protocollo vengono registrate le conversazioni SMTP tra i connettori di invio e ricezione nell'ambito del recapito dei messaggi. La registrazione del protocollo è disponibile nel servizio di trasporto front-end dei server Accesso client, nel servizio di trasporto dei server Cassette postali e nel servizio di trasporto delle cassette postali sui server Cassette postali. Per ulteriori informazioni, vedere [Registrazione del protocollo](protocol-logging-exchange-2013-help.md).

**Registri della tabella di routing**   Con registrazione della tabella di routing viene periodicamente registrata una snapshot della tabella di routing utilizzata da Exchange 2013 per instradare i messaggi alle rispettive destinazioni. La registrazione della tabella di routing è disponibile nel servizio di trasporto sui server Cassette postali.


---
title: 'Connettori esterni: Exchange 2013 Help'
TOCTitle: Connettori esterni
ms:assetid: 21c6a7a9-f4d2-4359-9ac9-930701b63a4e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996779(v=EXCHG.150)
ms:contentKeyID: 50480154
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Connettori esterni

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-09-25_

Un connettore esterno recapita i messaggi a un server o a un sistema esterno che non utilizza SMTP come meccanismo di trasporto principale. Un esempio può essere un server gateway fax. Un connettore esterno utilizza una directory di destinazione locale o condivisa per l'invio, tramite trasferimento file, dei messaggi in uscita al sistema esterno. I connettori esterni vengono creati nel servizio di trasporto di un server Cassette postali di Microsoft Exchange Server 2013.

I server con gateway esterno inviano i messaggi all'organizzazione Exchange 2013 utilizzando la directory di prelievo o riproduzione presente nel servizio di trasporto del server Cassette postali. Dopo essere stati formattati correttamente, i file dei messaggi di posta elettronica copiati in ciascuna directory vengono inviati per il recapito a una cassetta postale di Exchange.


> [!TIP]
> Nella maggior parte dei casi in cui è necessario recapitare i messaggi in uscita a un sistema non SMTP, è consigliabile utilizzare i connettori agente di recapito perché, tra l'altro, consentono di gestire le code di messaggi e non è necessario scrivere i messaggi nel file system. Per ulteriori dettagli, vedere l'argomento <A href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">Agenti di recapito e connettori agente di recapito</A>.



## Ulteriori informazioni

[Creare un connettore esterno per il recapito di messaggi a un gateway fax non SMTP](create-a-foreign-connector-to-deliver-messages-to-a-non-smtp-fax-gateway-exchange-2013-help.md)

[Agenti di recapito e connettori agente di recapito](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

[New-ForeignConnector](https://technet.microsoft.com/it-it/library/aa996310\(v=exchg.150\))

[Set-ForeignConnector](https://technet.microsoft.com/it-it/library/bb123789\(v=exchg.150\))


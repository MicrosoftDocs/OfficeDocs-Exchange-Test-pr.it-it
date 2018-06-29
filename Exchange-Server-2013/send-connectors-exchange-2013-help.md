---
title: 'Connettori di invio: Exchange 2013 Help'
TOCTitle: Connettori di invio
ms:assetid: 6aa19a12-c7b2-4eac-a8dc-9a4d26919ac5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998662(v=EXCHG.150)
ms:contentKeyID: 50480902
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Connettori di invio

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-15_

In Microsoft Exchange Server 2013, un connettore di invio controlla il flusso dei messaggi in uscita verso il server di ricezione. Questi connettori vengono configurati sui server Cassette postali su cui è in esecuzione il servizio di trasporto. Generalmente, si configura un connettore di invio per l'invio dei messaggi in uscita a uno smart host o direttamente al destinatario tramite DNS.

I server Cassette postali di Exchange 2013 su cui è in esecuzione il servizio di trasporto necessitano di connettori di invio per recapitare i messaggi all'hop successivo lungo il percorso che conduce a destinazione. I connettori di invio creati sui server Cassette postali vengono archiviati in Active Directory e sono disponibili per tutti i server Cassette postali su cui è in esecuzione il servizio di trasporto nell'organizzazione.


> [!IMPORTANT]
> Quando si distribuisce Exchange 2013, il flusso della posta in uscita non può iniziare fino a quando non viene configurato un connettore di invio per l'instradamento della posta in uscita a Internet. Per ulteriori informazioni, vedere <A href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">Creare un connettore di invio per la posta elettronica inviato a Internet</A>.



## Selezione del tipo di connettore di invio

Generalmente il connettore di invio viene creato nella sezione **Flusso di posta** dell'interfaccia di amministrazione di Exchange. Quando si crea un nuovo connettore di invio, si sceglie un **Tipo** disponibile adatto allo scenario di connessione. Il tipo determina le impostazioni di autorizzazioni predefinite assegnate al connettore e concede tali autorizzazioni a entità di sicurezza attendibili. Le identità di sicurezza includono utenti, computer e gruppi di protezione.

Tra le procedure in cui sono illustrate specifiche selezioni per il **Tipo** vi sono [Creare un connettore di invio per instradare la posta elettronica in uscita tramite uno Smart Host](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md) e [Creare un connettore di invio per l'invio di posta elettronica a un partner con sicurezza TLS (Transport Layer) applicate](create-a-send-connector-to-send-email-to-a-partner-with-transport-layer-security-tls-applied-exchange-2013-help.md).

Se si preferisce utilizzare Exchange Management Shell piuttosto che l'interfaccia di amministrazione di Exchange, è possibile creare un connettore di invio e specificare un tipo utilizzando il cmdlet [New-SendConnector](https://technet.microsoft.com/it-it/library/aa998936\(v=exchg.150\)).

## Nuove funzionalità dei connettori di invio in Exchange 2013

La relazione tra il servizio di trasporto Front End sui server Accesso client e il servizio di trasporto sui server Cassette postali in Exchange 2013 introduce un nuovo comportamento dei connettori di invio. In primo luogo, è possibile impostare un connettore di invio nel servizio di trasporto di un server Cassette postali affinché instradi la posta in uscita attraverso un server di trasporto Front End nel sito Active Directory locale utilizzando il parametro *FrontEndProxyEnabled* del cmdlet [Set-SendConnector](https://technet.microsoft.com/it-it/library/aa998294\(v=exchg.150\)), consolidando così la modalità di instradamento della posta elettronica dal servizio di trasporto. Per ulteriori informazioni sui servizi di trasporto, il comportamento di instradamento e le destinazioni in Exchange 2013, vedere [Routing della posta](mail-routing-exchange-2013-help.md). Per una panoramica sulla pipeline di trasporto e una descrizione di ciascun servizio di trasporto, vedere [Flusso di posta](mail-flow-exchange-2013-help.md).

Il parametro *IsCoexistenceConnector* è stato deprecato. Nella maggior parte dei casi, quando si desidera configurare un ambiente ibrido in cui una parte delle cassette postali sono ospitate in locale e una parte su cloud, è consigliabile utilizzare la procedura guidata per la configurazione ibrida.

*LinkedReceiveConnector* è stato deprecato. Questo parametro veniva utilizzato per creare, ad esempio, i connettori per l'instradamento dei messaggi a un servizio di protezione da posta indesiderata di terzi. Ora, nella maggior parte dei casi, l'indirizzamento della posta al servizio di protezione da posta indesiderata viene eseguito tramite il record MX e il comportamento del connettore associato non è rilevante.

La dimensione massima predefinita del messaggio, specificata dal parametro *MaxMessageSize*, è stata portata da 10 MB a 25 MB. Per informazioni su come impostare i parametri su un connettore di invio, vedere [Set-SendConnector](https://technet.microsoft.com/it-it/library/aa998294\(v=exchg.150\)).

*TlsCertificateName* è stato aggiunto. Viene utilizzato per autenticare il certificato locale per l'utilizzo nelle connessioni in uscita e ridurre al minimo il rischio di certificati fraudolenti.


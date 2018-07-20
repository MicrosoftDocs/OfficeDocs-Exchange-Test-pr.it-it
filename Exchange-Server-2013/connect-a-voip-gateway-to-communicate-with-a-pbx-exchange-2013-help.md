---
title: 'Connettere un gateway VoIP per comunicare con un PBX: Exchange 2013 Help'
TOCTitle: Connettere un gateway VoIP per comunicare con un PBX
ms:assetid: 76bcdc54-3ec2-408a-bdbe-37826580dd62
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998872(v=EXCHG.150)
ms:contentKeyID: 50555611
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Connettere un gateway VoIP per comunicare con un PBX

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-15_

Quando si configurano le reti di telefonia e dati per la messaggistica unificata in Microsoft Exchange Server 2013, è necessario configurare i gateway VoIP in modo che comunichino con i server Accesso client su cui è in esecuzione il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange e con i server Cassette postali su cui è in esecuzione il servizio Messaggistica unificata di Microsoft Exchange. È necessario anche configurare i gateway VoIP per la comunicazione con i sistemi PBX (Private Branch eXchanges) dell'organizzazione. Per configurare un gateway VoIP affinché comunichi con un centralino, è possibile utilizzare le informazioni e i collegamenti descritti in questo argomento.

## Configurazione di un gateway VoIP

Quando si configura un gateway VoIP, è necessario considerare se il dispositivo gateway VoIP è di tipo analogico, digitale o analogico e digitale. Se l'interfaccia del gateway VoIP per la connessione a un sistema PBX è analogica, è necessario configurare correttamente le impostazioni appropriate per abilitare il gateway VoIP alla comunicazione con tale sistema. Se l'interfaccia del gateway VoIP per la connessione a un sistema PBX è digitale, potrebbe non essere necessaria alcuna configurazione aggiuntiva per abilitare l'interfaccia digitale alla comunicazione con il sistema PBX.

Di seguito vengono indicate le risorse consigliate in Exchange TechCenter che forniscono informazioni utili per la corretta configurazione dei gateway VoIP e dei sistemi PBX:

  - **Documentazione sui gateway VoIP e sui sistemi IP PBX e PBX supportati**   [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md) Sono inclusi i file di configurazione e le informazioni di installazione utilizzabili per la configurazione dei gateway VoIP e dei sistemi PBX.

  - **Note tecniche e di configurazione**   [Note di configurazione per i gateway VoIP, IP PBX e PBX supportati](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md) Sono inclusi i file di configurazione e le informazioni di installazione utilizzabili per la configurazione dei gateway VoIP e dei sistemi PBX.

  - **Configurazione di un gateway VoIP basata su AudioCodes**  [Risorse di Microsoft Exchange Server pagina](https://www.audiocodes.com/solutions/microsoft/exchange-server) fornisce le informazioni di configurazione e di supporto più recente che consentono di configurare i gateway VoIP basato su AudioCodes per l'utilizzo con la messaggistica unificata.

  - **Configurazione di un gateway VoIP basato su Dialogic**   Il [sito Web Dialogic](https://www.dialogic.com/) vengono fornite le informazioni di configurazione e di supporto più aggiornate per i gateway VoIP basato su Dialogic.

È consigliabile che tutti i clienti che prevedono di distribuire la messaggistica unificata ottengano l'assistenza di un esperto di messaggistica unificata. Un tecnico esperto nella messaggistica unificata di Exchange consente di verificare che non esiste un aggiornamento senza problemi a messaggistica unificata da un legacy o audio di terze parti del sistema di posta e consentono di pianificare e distribuire un nuovo sistema di segreteria telefonica messaggistica unificata di Exchange. Distribuzione di un nuovo sistema di segreteria telefonica o l'aggiornamento di una voce legacy uno richiede conoscenza significativa VoIP gateway, sistemi PBX e la messaggistica unificata. Per ulteriori informazioni su come contattare un tecnico esperto nella messaggistica unificata, vedere [Microsoft Exchange Server 2013 Unified Messaging (UM) specialisti](http://go.microsoft.com/fwlink/p/?linkid=262708) o certified partner di messaggistica UNIFICATA in [Microsoft individuare](https://go.microsoft.com/fwlink/p/?linkid=261951).

## Ulteriori informazioni

[Note di configurazione per i gateway VoIP, IP PBX e PBX supportati](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

[Connettersi alla messaggistica unificata a un gateway VoIP supportato](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md)


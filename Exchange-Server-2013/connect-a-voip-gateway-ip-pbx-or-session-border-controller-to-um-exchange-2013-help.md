---
title: 'Connettere un controller dei confini VoIP gateway, IP PBX o della sessione di messaggistica UNIFICATA: Exchange 2013 Help'
TOCTitle: Connettere un controller dei confini VoIP gateway, IP PBX o della sessione di messaggistica UNIFICATA
ms:assetid: a7cecf59-b93a-413b-bb88-29f2669ef2cf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124084(v=EXCHG.150)
ms:contentKeyID: 50555653
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Connettere un controller dei confini VoIP gateway, IP PBX o della sessione di messaggistica UNIFICATA

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

È necessario configurare vocale nel gateway IP (VoIP) e IP Private Branch Scambia (PBX) correttamente durante la distribuzione di messaggistica unificata (UM) per l'organizzazione. Se si distribuisce alla messaggistica UNIFICATA in un ambiente ibrido, sarà inoltre necessario configurare correttamente i session border controller (sbc). A tale scopo, è necessario configurare le interfacce del gateway VoIP, IP PBX e SBC per comunicare con i server Accesso Client che eseguono il servizio Microsoft Exchange Unified Messaging routing delle chiamate e il server cassette postali in esecuzione il servizio messaggistica unificata di Exchange o interfaccia.


> [!IMPORTANT]
> Quando si eseguono attività amministrative per un gateway VoIP, IP PBX o SBC utilizzando un web browser, non vengono crittografate le richieste HTTP inviate in rete. Per aumentare il livello di sicurezza per i gateway VoIP, IP PBX o SBC sulla rete, utilizzare Secure Sockets Layer (SSL) o Internet Protocol security (IPsec) per proteggere i dati trasmessi sulla rete e le credenziali amministrative. È inoltre consigliabile utilizzare un meccanismo di autenticazione avanzata e utilizzo di password complesse amministrativo per proteggere le credenziali amministrative per il dispositivo.



## Interfacce di dispositivo di telefonia IP

Esistono diversi tipi di porte o interfacce che è necessario configurare per consentire la comunicazione tra un PBX, VoIP gateway, IP PBX o SBC e il server Accesso Client e cassette postali nella rete. Quando si configura un gateway VoIP, IP PBX o SBC, è necessario considerare se il dispositivo analogico, digitali, o analogici e digitali.

Se l'interfaccia gateway VoIP che si connette a un sistema PBX analogico, è necessario configurare correttamente le impostazioni appropriate per abilitare il gateway VoIP comunicare con i server Accesso Client e cassette postali. Per IP PBX e SBC, è necessario configurare anche correttamente le interfacce IP per abilitare questi dispositivi comunicare con i server Accesso Client e cassette postali. Tutti questi dispositivi sono diversi tipi di connessioni o le porte che sono disponibili a seconda del modello di dispositivo e fornitori.

Per consentire le comunicazioni con i server Accesso Client e cassette postali nella rete:

  - Per i gateway VoIP, è necessario configurare le interfacce di telefonia per comunicare con i sistemi PBX ed è necessario configurare le interfacce IP per il dispositivo.

  - Per IP PBX, è necessario configurare in base a commutazione di circuito e di rete o connessioni basate su IP.

  - Per SBCs, è necessario configurare entrambe le interfacce IP, una per la rete e l'altra interfaccia che si connette tramite Internet o una connessione WAN dedicata.

Questo è un elenco delle risorse disponibili nel TechCenter di Exchange che forniscono informazioni che consentono di configurare correttamente i gateway VoIP, IP PBX e SBC:

  - **Gateway IP di supportati, IP PBX e PBX documentazione** [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md) include i file di configurazione e informazioni sulle impostazioni che è possibile utilizzare quando si configurano i gateway VoIP, IP PBX, PBX e SBC.   

  - **Configurazione e le note tecniche** [Note di configurazione per i gateway VoIP, IP PBX e PBX supportati](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md) include i file di configurazione e informazioni sulle impostazioni che è possibile utilizzare quando si configurano i gateway VoIP, IP PBX e PBX.   

  - **Note di configurazione per la messaggistica UNIFICATA di Exchange online** [Note di configurazione per session border controller supportati](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md) include i file di configurazione e informazioni sulle impostazioni che è possibile utilizzare quando si configura SBCs.   

Esperti di messaggistica unificate sono disponibili per agevolare la configurazione di dispositivi di rete basato su IP e di telefonia. Specialista la messaggistica unificata può consentono di assicurarsi che non esiste una transizione senza problemi a messaggistica unificata da un legacy o vocale di terze parti del sistema di posta o consentono di pianificare e distribuire un nuovo sistema di segreteria telefonica messaggistica unificata di Exchange. Distribuzione di un nuovo sistema di segreteria telefonica o l'aggiornamento di uno legacy richiede conoscenza significativa VoIP gateway, IP PBX, sistemi PBX e la messaggistica unificata. Per ulteriori informazioni su come contattare un tecnico esperto nella messaggistica unificata, vedere [Microsoft Exchange Server 2013 Unified Messaging (UM) specialisti](http://go.microsoft.com/fwlink/p/?linkid=262708) o certified partner di messaggistica UNIFICATA in [Microsoft individuare](https://go.microsoft.com/fwlink/p/?linkid=261951).

Dopo aver configurato un gateway VoIP, IP PBX o SBC IP interfaccia, è necessario creare e configurare un gateway IP di messaggistica UNIFICATA per rappresentare ogni dispositivo su cui è distribuito. Per ulteriori informazioni su come creare un gateway IP di messaggistica UNIFICATA, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).

Dopo aver creato un gateway IP di messaggistica UNIFICATA, i server Accesso Client e cassette postali associati al gateway IP di messaggistica UNIFICATA inviare una richiesta SIP OPTIONS al gateway VoIP, IP PBX o SBC per assicurarsi che sia reattiva. Se il gateway VoIP, IP PBX o SBC non risponde, il server cassette postali verrà registrato un evento con ID 1088 che indica che la richiesta non riuscita. Per risolvere questo problema, verificare che il gateway VoIP, IP PBX o SBC è disponibile e online e la configurazione di messaggistica unificata sia corretta.

Un server Accesso Client e un server cassette postali dovranno comunicare solo con un gateway VoIP, IP PBX o SBC è elencato come attendibile peer Session Initiation Protocol (SIP). Verrà registrato un evento con ID 1175 quando più host DNS condividono lo stesso indirizzo IP. Questo evento può verificarsi se è configurato le zone DNS con nomi di dominio completi per i gateway VoIP della rete. Messaggistica unificata protegge la richieste non autorizzate recuperando l'URL interno della directory virtuale di servizi Web di messaggistica unificata che si trova sul server cassette postali e quindi utilizzando l'URL per creare l'elenco dei nomi di dominio completo per il SIP attendibile peer. Dopo aver risolto nell'indirizzo IP stesso due FQDN, questo evento verrà registrato.


> [!NOTE]
> È necessario riavviare il MicrosoftExchange servizio messaggistica unificata se un gateway VoIP, IP PBX o SBC è configurato per disporre di un nome di dominio COMPLETO e il record DNS del gateway VoIP, IP PBX o SBC viene modificato dopo aver avviato il servizio. Se non riavviare il servizio, il server cassette postali non sarà in grado di individuare il gateway VoIP, IP PBX o SBC. Si verifica perché una cache per tutti i gateway VoIP, IP PBX o SBC è presente un server cassette postali e la risoluzione DNS viene eseguita solo quando viene riavviato il servizio o quando viene modificata la configurazione di un gateway VoIP, IP PBX o SBC.



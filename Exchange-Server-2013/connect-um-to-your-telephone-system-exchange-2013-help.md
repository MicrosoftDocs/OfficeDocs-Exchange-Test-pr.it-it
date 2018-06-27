---
title: 'Connettersi alla messaggistica unificata al sistema telefonico in uso: Exchange 2013 Help'
TOCTitle: Connettersi alla messaggistica unificata al sistema telefonico in uso
ms:assetid: 92c3e029-f732-4d6d-b147-2b3006d5f088
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673544(v=EXCHG.150)
ms:contentKeyID: 50555640
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Connettersi alla messaggistica unificata al sistema telefonico in uso

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-30_

La messaggistica unificata combina la messaggistica vocale e di posta elettronica in una sola cassetta postale accessibile da diversi dispositivi. Gli utenti possono ascoltare i messaggi della segreteria telefonica dalla Posta in arrivo o tramite Outlook Voice Access da qualsiasi telefono.

Quando si distribuisce la messaggistica unificata in un'organizzazione di Microsoft Exchange, è necessario installare, distribuire e configurare uno o più gateway VoIP (Voice over IP) per connettersi ai sistemi PBX (Private Branch eXchanges) della rete di telefonia oppure installare, distribuire e configurare i sistemi PBX o IP PBX abilitati per SIP (Session Initiation Protocol). Se si sta aggiornando il sistema di caselle vocali corrente, sarà necessario distribuire i dispositivi che si connettono alla rete di telefonia, installare i server Accesso client e Cassette postali di Exchange, quindi creare i componenti di messaggistica unificata necessari che consentono alla rete di telefonia di connettersi alla rete dati. In questo modo, le chiamate in arrivo dalla rete di telefonia si connetteranno ai gateway VoIP, ai sistemi IP PBX o PBX abilitati per SIP e i dispositivi si connetteranno all'organizzazione di Exchange.

Se si sta installando, distribuendo e configurando Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server, non verranno utilizzati i gateway VoIP, i sistemi IP PBX, o PBX abilitati per SIP per la connessione diretta alla messaggistica unificata di Exchange. Saranno invece Lync Mediation Server e un gateway VoIP o un gateway VoIP avanzato con funzionalità di Mediation Server e un gateway VoIP a rendere possibile la connessione alla messaggistica unificata di Exchange. Gli utenti di messaggistica unificata abilitati per il VoIP aziendale possono recuperare, ascoltare e rispondere ai messaggi vocali ed effettuare chiamate in uscita. Possono anche accedere ad altre funzionalità di Lync, tra cui la presenza e la messaggistica istantanea (IM) utilizzando Office Communicator o un client Lync.

Le informazioni seguenti consentiranno di impostare e distribuire la messaggistica unificata e di abilitare le funzionalità di segreteria telefonica per gli utenti nell'organizzazione:

  - [Connettere un controller dei confini VoIP gateway, IP PBX o della sessione di messaggistica UNIFICATA](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md) Informazioni sulla connessione alla messaggistica unificata dei gateway VoIP o dei sistemi IP PBX.

  - [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md) Informazioni sui gateway VoIP e sui sistemi IP PBX e PBX supportati.

  - [Note di configurazione per i gateway VoIP, IP PBX e PBX supportati](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)  Informazioni sulla configurazione dei gatway VoIP e dei sistemi IP PBX e PBX.


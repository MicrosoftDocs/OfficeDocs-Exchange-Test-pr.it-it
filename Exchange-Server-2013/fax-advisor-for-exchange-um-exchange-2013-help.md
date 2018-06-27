---
title: 'Fax advisor per la messaggistica UNIFICATA di Exchange: Exchange 2013 Help'
TOCTitle: Fax advisor per la messaggistica UNIFICATA di Exchange
ms:assetid: 928a466d-cc0c-4160-bd4c-f0fc76b038d4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee364747(v=EXCHG.150)
ms:contentKeyID: 52057302
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Fax advisor per la messaggistica UNIFICATA di Exchange

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

Messaggistica unificata (UM) di Microsoft si basa su soluzioni partner fax certificate per funzionalità avanzate, come i fax in uscita o il routing dei fax. Per impostazione predefinita, gli utenti non vengono configurati per il recapito di messaggi fax a utenti abilitati alla messaggistica unificata. I server Exchange inviano richieste fax a una soluzione partner fax certificata. Il server del partner fax riceve i dati e li invia alla cassetta postale del destinatario tramite un messaggio di posta elettronica con allegato il fax in formato TIFF. Per dettagli, vedere [Consentire agli utenti di posta vocale di ricevere fax](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md).


> [!IMPORTANT]
> È consigliabile che tutti i clienti che prevedono di distribuire la messaggistica unificata ottengano l'assistenza di un esperto di messaggistica unificata. Specialista la messaggistica unificata consente di verificare che esista una transizione senza problemi a messaggistica unificata da un sistema di caselle vocali legacy. Esecuzione di una nuova distribuzione o aggiornamento di un sistema di caselle vocali legacy richiede la conoscenza significativo sui sistemi PBX e la messaggistica unificata. Per ulteriori informazioni su come contattare un tecnico esperto nella messaggistica unificata, vedere il <A href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 Unified Messaging (UM) specialisti</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=261951">Individuare Microsoft per la messaggistica unificata</A>.



## Programma Partner fax per la messaggistica unificata di Exchange

Al fine di diventare un partner fax certificato per l'interoperabilità con Messaggistica unificata, il partner deve eseguire le richieste contenute nel documento Fax Partner Interoperability Specification e la soluzione fax deve essere certificata da un fornitore indipendente. Per ulteriori informazioni sulla certificazione di un prodotto fax in modo che possa essere utilizzato con la messaggistica unificata di, inviare una richiesta a [Partner fax per la messaggistica unificata](mailto:fax-part@microsoft.com).

## Soluzioni partner fax certificate come interoperabili con la messaggistica unificata

Se è già stato distribuito la messaggistica unificata di Exchange e si cerca un partner fax che consentono i fax in ingresso per l'organizzazione, vedere [Individuare Microsoft per i partner Fax](https://go.microsoft.com/fwlink/p/?linkid=190238). Tali fornitori di software certificati come interagire con Exchange Server e includono soluzioni software certificati per la messaggistica unificata.

## VoIP, media gateway e supporto IP PBX

La corretta configurazione dei gateway VoIP per l'organizzazione è un'attività di distribuzione complessa che deve essere completata per distribuire correttamente Messaggistica unificata di Exchange con i fax in arrivo. Per trovare risposte a eventuali dubbi e ottenere le informazioni di configurazione più aggiornate sui gateway, vedere [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md). Nell'argomento [Note di configurazione per i gateway VoIP, IP PBX e PBX supportati](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md) vengono forniti file e note di configurazione dei gateway VoIP necessari per configurare correttamente i gateway VoIP dell'organizzazione, IP PBX e SBC in modo che funzionino con la messaggistica unificata di Exchange.

La verifica di interoperabilità della Messaggistica unificata di Exchange con gateway VoIP è ora integrata con il programma Microsoft Unified Communications Open Interoperability Program. Per ulteriori informazioni, vedere [Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/p/?linkid=140722).

Il programma di qualificazione per gateway VoIP e PBX IP [Programma interoperabilità aperta Microsoft Unified Communications](http://go.microsoft.com/fwlink/p/?linkid=140722) garantisce agli utenti un'installazione e un supporto semplificati quando si utilizzano gateway di telefonia e IP PBX qualificati con il software Microsoft Unified Communications.


> [!IMPORTANT]
> L'invio e la ricezione dei fax tramite T.38 o G.711 non sono supportati in un ambiente in cui la messaggistica unificata e Communications Server 2007 R2 o Microsoft Lync Server sono integrati.



## Distribuzione e configurazione dei fax

La messaggistica unificata consente di inoltrare le chiamate fax in arrivo a una soluzione partner fax dedicata, che riconosce la chiamata fax del mittente e riceve il fax per conto dell'utente abilitato alla messaggistica unificata. Tuttavia, per consentire la ricezione dei messaggi fax nella cassetta postale degli utenti abilitati alla messaggistica unificata, è necessario configurare il server Partner fax, quindi configurare i dial plan e i criteri cassetta postale di messaggistica unificata e abilitare la ricezione dei fax per gli utenti abilitati alla messaggistica unificata. Per dettagli, vedere [Impostazione di fax in arrivo](setting-up-incoming-faxing-exchange-2013-help.md).


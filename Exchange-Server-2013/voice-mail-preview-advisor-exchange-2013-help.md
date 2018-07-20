---
title: 'Advisor Anteprima messaggio vocale: Exchange 2013 Help'
TOCTitle: Advisor Anteprima messaggio vocale
ms:assetid: 0957dd54-df6d-4b50-9db5-4757f548b899
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee364730(v=EXCHG.150)
ms:contentKeyID: 51407335
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Advisor Anteprima messaggio vocale

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

La messaggistica unificata di Exchange Microsoft fornisce una funzionalità denominata Anteprima casella vocale che utilizza il riconoscimento vocale automatico (ASR) per aggiungere ai messaggi vocali una versione di testo del file audio relativo al sistema di caselle vocali. Il riconoscimento vocale automatico non è del tutto preciso, soprattutto quando viene utilizzato per registrare un messaggio audio con voci sconosciute e rumori. Alcune organizzazioni richiedono costantemente trascrizioni di messaggi vocali prive di errori (o quasi). Il programma partner Anteprima casella vocale consente alle organizzazioni di questo tipo di soddisfare tali requisiti.

Anteprima casella vocale utilizza le [tecnologie di riconoscimento vocale Microsoft](http://go.microsoft.com/fwlink/p/?linkid=187348) per fornire una versione di testo delle registrazioni audio. Il testo del messaggio vocale viene visualizzato nei messaggi di posta elettronica all'interno di MicrosoftOutlook Web App, Outlook 2010 o versioni successive, nonché in altri programmi di posta elettronica.

Per impostazione predefinita, quando si abilita un utente alla messaggistica unificata in una distribuzione locale o ibrida, le anteprime delle caselle vocali vengono inviate soltanto se è stato installato un Language Pack di messaggistica unificata supportato. Quando si abilita un utente alla messaggistica unificata in Exchange Online, vengono installati tutti i Language Pack di messaggistica unificata. Tuttavia, la funzionalità Anteprima casella vocale non è supportata per tutte le lingue installate.

Sono disponibili i partner di Anteprima casella vocale, i quali offrono servizi e un supporto di trascrizione avanzato per la funzionalità corrispondente. Tali partner utilizzano persone che correggono le trascrizioni della posta vocale create utilizzando il riconoscimento vocale automatico. Ogni partner di Anteprima casella vocale deve soddisfare una serie di requisiti per ottenere la certificazione e interagire con la messaggistica unificata di Exchange.

Se ritiene che le anteprime posta vocali inviati a utenti non sono abbastanza accurati, è possibile contattare uno dei partner certificati Anteprima messaggio vocale elencati nella [Individuare Microsoft](https://go.microsoft.com/fwlink/p/?linkid=281966) e accesso backup con loro un costo aggiuntivo.

**Sommario**

Panoramica

Exchange Unified Messaging Voice Mail Partner program

Voice Mail Preview partners certified for Exchange Unified Messaging

Configuring Voice Mail Preview partners

VoIP or media gateways and IP PBX support

## Panoramica

Quando la messaggistica unificata registra l'audio di un messaggio vocale, utilizza ASR per creare un testo dell'anteprima della casella vocale dal file audio, quindi inoltra l'intero messaggio vocale per il recapito all'utente. Per ciascun messaggio vocale creato, la messaggistica unificata determina un livello di probabilità per l'anteprima della casella vocale inclusa con il messaggio. Determina il grado di corrispondenza tra l'audio della registrazione e le parole, i numeri e le frasi contenute nel messaggio. Se il sistema rileva facilmente corrispondenze, il livello di probabilità sarà elevato. Un livello di probabilità maggiore viene generalmente associato a una precisione maggiore.

La precisione del testo dell'anteprima casella vocale dipende da molti fattori e, a volte, non è possibile controllare tali fattori. Tuttavia, il testo potrebbe essere più preciso quando:

  - Viene lasciato un messaggio vocale semplice e il chiamante non utilizza gergo, termini tecnici o parole o frasi insolite.

  - Il chiamante utilizza una lingua facilmente riconosciuta tradotta dal sistema di caselle vocali. Generalmente, i messaggi vocali lasciati dai chiamanti che non parlano troppo rapidamente o troppo piano e che non hanno forti accenti produrranno frasi e sentenze più precise.

  - Il messaggio vocale non presenta echi e rumori in sottofondo e l'audio non ha subito interruzioni.

La maggior parte dei clienti che usufruiscono della messaggistica unificata trovano che le anteprime delle caselle vocali siano sufficientemente accurate per i propri utenti. Tuttavia, quando ASR viene applicato alle registrazioni fatte sul telefono da voci e rumori di sottofondo sconosciuti, il testo dell'anteprima della casella vocale non è del tutto preciso. Se il livello di probabilità è piuttosto basso o le anteprime delle caselle vocali ricevute non sono molto precise, è possibile aumentare la precisione delle anteprime delle caselle vocali ricevute dagli utenti come segue:

  - Effettuare la registrazione per un servizio di trascrizione dei messaggi vocali da un partner Anteprima casella vocale.

  - Dopo aver effettuato la registrazione a un partner Anteprima casella vocale, impostarlo affinché collabori con la messaggistica unificata. Per ulteriori informazioni su come configurare la messaggistica unificata per un partner Anteprima casella vocale, vedere [Configurare i servizi partner Anteprima messaggio vocale per gli utenti](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md).

Una volta effettuata la registrazione a un partner di Anteprima casella vocale, i server Exchange dell'organizzazione reindirizzano i messaggi vocali con il file audio allegato al partner di Anteprima casella vocale invece di generare un testo di anteprima della casella vocale per i messaggi vocali e inoltrare tali messaggi alla cassetta postale dell'utente. In seguito, il messaggio di posta elettronica contenente il testo dell'anteprima della casella postale creato dal partner di Anteprima casella vocale viene inviato ai server Exchange dell'organizzazione per il recapito alla cassetta postale del destinatario.


> [!IMPORTANT]
> È consigliabile che tutti i clienti che prevedono di distribuire la messaggistica unificata ottengano l'assistenza di un esperto di messaggistica UNIFICATA. Specialista alla messaggistica UNIFICATA consente di verificare che esista una transizione senza problemi di messaggistica UNIFICATA da un sistema di caselle vocali legacy. Esegue una nuova distribuzione o aggiornamento di un sistema di caselle vocali legacy richiede la conoscenza significativa gateway VoIP, IP PBX, sistemi PBX, session border controller (sbc) e la messaggistica unificata. Per ulteriori informazioni su come contattare un tecnico esperto nella messaggistica UNIFICATA, vedere il <A href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 Unified Messaging (UM) specialisti</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=261951">Individuare Microsoft per la messaggistica unificata</A>.



Inizio pagina

## Programma partner di Anteprima casella vocale per la messaggistica unificata di Exchange

Per diventare un partner certificato di Anteprima casella vocale che interagisce con la messaggistica unificata di Exchange, il partner deve implementare i requisiti contenuti nel documento Voice Mail Preview Interoperability Specification e la soluzione partner deve essere certificata da un fornitore indipendente. Se si è interessati a certificare il proprio servizio di trascrizione per l'utilizzo con la messaggistica unificata di Exchange, inviare una richiesta al [partner di Anteprima casella vocale per la messaggistica unificata di Exchange](mailto:vmppp@microsoft.com).

## Partner di Anteprima casella vocale certificati per la messaggistica unificata di Exchange

Se già stato distribuito la messaggistica unificata nell'organizzazione e si sta cercando un certified partner Anteprima messaggio vocale fornire servizi di supporto trascrizione, vedere [Microsoft individuare](https://go.microsoft.com/fwlink/p/?linkid=281966). Questi fornitori di software certificati come interagire con messaggistica UNIFICATA di Exchange.

## Configurazione dei partner di Anteprima casella vocale

Dopo aver configurato la funzionalità di messaggistica unificata, quest'ultima inoltra i messaggi vocali con l'audio a un partner di Anteprima casella vocale dedicato, il quale recupera il file audio e crea il testo di anteprima della casella vocale. Tuttavia, per consentire agli utenti di ricevere l'anteprima della casella vocale con il relativo messaggio vocale nella propria cassetta postale, è necessario configurare un criterio cassetta postale di messaggistica unificata, quindi verificare che gli utenti siano in grado di ricevere le anteprime delle caselle vocali nei proprio messaggi vocali in Outlook 2010 o in una versione successiva di Outlook Web App. Per ulteriori informazioni su come configurare la messaggistica unificata per un partner di Anteprima casella vocale, vedere [Configurare i servizi partner Anteprima messaggio vocale per gli utenti](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md).

## Supporto IP PBX e gateway multimediali o VoIP

La configurazione dei gateway VoIP e dei sistemi IP PBX per l'organizzazione è un'attività di distribuzione difficile che deve essere portata a termine correttamente per garantire la distribuzione della messaggistica unificata con un partner di Anteprima casella vocale. Per informazioni in grado di agevolare la configurazione dei gateway VoIP e dei sistemi IP PBX e per informazioni più aggiornate su come configurarli, vedere [Sistema di telefonia per Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md) o [Note di configurazione per i gateway VoIP, IP PBX e PBX supportati](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md).

Testing interoperabilità della messaggistica UNIFICATA di Exchange a VoIP gateway è stato integrato con Microsoft Unified Communications Open Interoperability Program. Per ulteriori informazioni, vedere [Microsoft Unified Communications Open Interoperability Program](https://go.microsoft.com/fwlink/p/?linkid=132071).

Inizio pagina


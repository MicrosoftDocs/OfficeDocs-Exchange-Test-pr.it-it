---
title: 'Codici di chiamata, prefissi e formati dei numeri: Exchange 2013 Help'
TOCTitle: Codici di chiamata, prefissi e formati dei numeri
ms:assetid: 26d61e55-f8dd-4d25-81f1-78a87cf88bad
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb266967(v=EXCHG.150)
ms:contentKeyID: 51407355
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Codici di chiamata, prefissi e formati dei numeri

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-05-04_

È possibile configurare diversi codici di chiamata utilizzati da un server Messaggistica unificata per effettuare chiamate interne ed esterne per utenti abilitati alla messaggistica unificata. Spesso, è necessario configurare un dial plan con codici di accesso o di chiamata, un prefisso nazionale o formati di numeri nazionali e internazionali in modo da poter controllare le chiamate esterne per gli utenti nell'organizzazione. In questo argomento vengono descritti i codici di chiamata, i prefissi e i formati di numeri e viene illustrato come utilizzarli per controllare le chiamate esterne per l'organizzazione.

**Sommario**

Panoramica

Outside line access code

National number prefix

In-country/region access code

International access code

In-country/region and international number formats

## Panoramica

*L'esecuzione delle chiamate esterne* è il processo utilizzato dagli utenti che chiamano un dial plan o un operatore automatico di messaggistica unificata ed effettuano, quindi, una chiamata a un numero di telefono interno o esterno. Quando un utente chiama un dial plan o un operatore automatico di messaggistica unificata, quindi effettua una chiamata, Messaggistica unificata utilizza le impostazioni configurate nel dial plan o nell'operatore automatico e i criteri cassetta postale di messaggistica unificata impostati per l'esecuzione della chiamata. Messaggistica unificata effettua una chiamata in uscita nei casi seguenti:

  - Quando viene effettuata una chiamata a un numero di telefono esterno di un chiamante

  - Quando una chiamata viene trasferita a un operatore automatico

  - Quando una chiamata viene trasferita a un utente (abilitato o meno alla messaggistica unificata) nell'organizzazione

  - Quando un utente abilitato alla messaggistica unificata utilizza la funzionalità Ascolta al telefono

Esistono due tipi di utenti che effettuano chiamate esterne: utenti autenticati e utenti non autenticati. Gli utenti non autenticati chiamano il numero di Outlook Voice Access configurato su un dial plan di messaggistica unificata ma non accedono alla propria cassetta postale. Chiamano anche un numero configurato su un operatore automatico di messaggistica unificata. Gli utenti autenticati chiamano il numero di Outlook Voice Access e accedono correttamente alla propria cassetta postale. Quando un utente chiama il numero di Outlook Voice Access, viene inizialmente considerato non autenticato poiché non ha fornito il proprio numero di interno e il PIN e non ha effettuato l'accesso alla propria cassetta postale. Gli utenti verranno autenticati dopo aver fornito il proprio numero di interno e il PIN e dopo aver correttamente effettuato l'accesso alla propria cassetta postale.

Quando un utente non autenticato chiama un operatore automatico di messaggistica unificata ed effettua una chiamata utilizzando la funzionalità di esecuzione delle chiamate esterne, vengono utilizzate le impostazioni per le chiamate esterne configurate nel dial plan e nell'operatore automatico di messaggistica unificata. Quando un utente non autenticato chiama il numero di Outlook Voice Access configurato in un dial plan, vengono utilizzate soltanto le impostazioni configurate nel dial plan. Quando gli utenti effettuano correttamente l'accesso alla propria cassetta postale, vengono applicati le impostazioni di configurazione del dial plan e il criterio di messaggistica unificata associati all'utente autenticato.

È necessario configurare diverse impostazioni per controllare le chiamate in uscita della propria organizzazione. Per controllare l'esecuzione delle chiamate esterne, è necessario configurare i dial plan di messaggistica unificata, gli operatori automatici e i criteri cassetta postale di messaggistica unificata di Messaggistica unificata. Per controllare l'esecuzione delle chiamate esterne, è possibile configurare nei dial plan, negli operatori automatici e nei criteri cassetta postale di messaggistica unificata le seguenti impostazioni:

  - Linea esterna, codici di accesso nazionali e internazionali

  - Prefissi numeri nazionali

  - Formati numeri nazionali e internazionali

  - Gruppi di regole di composizione nazionali e internazionali

  - Gruppi di regole di composizione nazionali e internazionali consentiti

  - Voci delle regole di composizione

Configurare i codici di accesso, prefissi, e formati dei numeri nella messaggistica unificata dial plan nella pagina **Dial codici**Interfaccia di amministrazione di Exchange (EAC). È inoltre possibile configurare le impostazioni tramite il cmdlet **Set-UMDialPlan** in Exchange Management Shell. È possibile scegliere di tutte le impostazioni, nessuna delle impostazioni o solo alcune delle impostazioni di configurazione. Ogni impostazione controlla una parte del processo di outdialing specifica.

Messaggistica unificata utilizza codici di accesso, prefissi e formati di numeri per determinare il numero corretto da chiamare. Possono essere configurati per limitare le chiamate in uscita di utente che accedono a un operatore automatico di Messaggistica unificata associato a un dial plan di Messaggistica unificata o che chiamano un numero di Outlook Voice Access configurato nel dial plan.

Per ulteriori informazioni sulle chiamate esterne in Messaggistica unificata, vedere [Codici di chiamata, prefissi e formati dei numeri](dial-codes-number-prefixes-and-number-formats-exchange-2013-help.md).

Inizio pagina

## Codice di accesso per linee esterne

È possibile configurare un numero di accesso alla linea esterna, anche noto come *codice di accesso a linea interurbana*, in ogni dial plan creato. Questo è il numero che viene utilizzato per accedere a una linea telefonica esterna. Questo numero è configurato anche nei PBX (Private Branch eXchange) o IP PBX nell'organizzazione. Nella maggior parte delle reti telefoniche gli utenti compongono il numero 9 per accedere a una linea esterna ed effettuare una chiamata a un numero di telefono esterno.

È necessario configurare un codice di accesso alla linea esterna in ogni dial plan creato. Il codice di chiamata configurato sarà valido per tutti gli utenti associati a un criterio cassetta postale di messaggistica unificata a sua volta associato al dial plan di messaggistica unificata. Quando un chiamante collegato al dial plan effettua una chiamata e il dial plan effettua la chiamata esterna, Messaggistica unificata aggiunge il codice di accesso alla linea esterna (di solito 9) di fronte alla stringa del numero composto in modo che PBX o IP PBX possano comporre correttamente il numero. Se non viene configurato il codice di accesso alla linea esterna, PBX o IP PBX potrebbero non riconoscere il numero inviato. Ad esempio, come indicato in precedenza, in molte organizzazioni il codice di accesso composto dagli utenti per accedere alla linea esterna è 9 e tale impostazione è configurata in un PBX o IP PBX. È necessario configurare Messaggistica unificata in modo che venga anteposto il codice di accesso alla linea esterna (9) alla stringa del numero di telefono affinché il PBX o IP PBX sia in grado di comporre correttamente il numero per la chiamata in uscita. Se si configura il codice di chiamata in modo tale che venga anteposto il codice di accesso alla linea esterna, Messaggistica unificata sarà in grado di utilizzare il codice di accesso alla linea esterna per accedere a una linea esterna prima che venga composta la stringa del numero di telefono esterno. Il codice di chiamata configurato sarà valido per tutti gli utenti associati a un criterio cassetta postale di messaggistica unificata a sua volta associato al dial plan di messaggistica unificata.

## Prefisso nazionale

È anche possibile configurare il prefisso nazionale e il codice paese in un dial plan di messaggistica unificata. Il numero immesso viene utilizzato da Messaggistica unificata per comporre il codice paese o il prefisso nazionale corretto quando un utente effettua una chiamata in uscita nazionale o internazionale. Ad esempio, quando un utente del Nord America effettua una chiamata in uscita internazionale verso l'Europa, Messaggistica unificata aggiungerà il prefisso nazionale prima della stringa del numero di telefono inviata al PBX o IP PBX per l'esecuzione della chiamata in uscita. Il numero 1 viene utilizzato come prefisso nazionale per il Nord America.

## Codice di accesso nel paese/regione

È possibile configurare un codice paese in un dial plan di messaggistica unificata. Il codice di accesso paese è costituito dalle cifre associate a un paese specifico. Il codice paese viene utilizzato da Messaggistica unificata per comporre il numero di telefono corretto quando viene effettuata una chiamata verso un numero di telefono nello stesso paese. Questo numero verrà aggiunto alla stringa del numero inviata a PBX o a IP PBX quando viene effettuata la chiamata in uscita. Ad esempio, Messaggistica unificata aggiungerà il numero 1 ad una chiamata effettuata dagli Stati Uniti e destinata agli Stati Uniti. Il codice paese per il Regno Unito è 44.

## Codice di accesso internazionale

È possibile configurare un codice di accesso internazionale in un dial plan di messaggistica unificata. Il codice di accesso internazionale è costituito dalle cifre utilizzate per accedere ai numeri di telefono internazionali. Il codice di accesso internazionale viene utilizzato da Messaggistica unificata per comporre il codice di accesso internazionale corretto quando viene effettuata una chiamata da un numero di telefono di un paese verso il numero di telefono di un altro paese. Questo numero verrà aggiunto alla stringa del numero inviata a PBX o a IP PBX quando viene effettuata la chiamata in uscita. Ad esempio, Messaggistica unificata utilizzerà 011 come codice di accesso internazionale per gli Stati Uniti. Il codice di accesso internazionale per l'Europa è 00.

Inizio pagina

## Formati numeri nazionali e internazionali

È possibile effettuare la configurazione delle chiamate in arrivo per i formati di numeri nazionali e internazionali in un dial plan di messaggistica unificata. Dopo che sono state configurate queste impostazioni, Messaggistica unificata sarà in grado di riconoscere le chiamate in arrivo nazionali e internazionali tra dial plan di messaggistica unificata all'interno della medesima organizzazione. È inoltre possibile aggiungere formati di numeri per chiamate in arrivo effettuate in un unico dial plan. La configurazione di tali opzioni consente all'organizzazione di risparmiare denaro impedendo l'esecuzione di chiamate in uscita che non possono essere effettuate da utenti all'interno dell'organizzazione e contribuisce a evitare le frodi telefoniche. Le informazioni configurate verranno utilizzate da Messaggistica unificata per esaminare il formato del numero della chiamata in arrivo e per verificare che il formato numero corrisponda prima che la chiamata venga accettata. Ad esempio, potrebbero esistere più dial plan all'interno dell'organizzazione. Se si dispone di un dial plan per gli Stati Uniti e di un altro dial plan per il Regno Unito, sarà possibile consentire agli utenti nel dial plan degli Stati Uniti di disporre della Messaggistica unificata in grado di effettuare chiamate verso gli utenti nel dial plan del Regno Unito, ma sarà anche possibile non consentire loro di chiamare direttamente altri numeri nazionali o internazionali.


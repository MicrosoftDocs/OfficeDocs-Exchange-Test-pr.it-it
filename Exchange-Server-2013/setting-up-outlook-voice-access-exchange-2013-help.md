---
title: 'Configurazione di Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurazione di Outlook Voice Access
ms:assetid: 5ce8c877-35f3-4e55-a65e-5ca469aeae99
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298010(v=EXCHG.150)
ms:contentKeyID: 50555595
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione di Outlook Voice Access

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-03-09_

Microsoft Outlook Voice Access consente agli utenti abilitati alla messaggistica unificata di Exchange di accedere alle proprie cassette postali utilizzando telefoni analogici, digitali o cellulari.

Un utente di Outlook Voice Access (denominato anche *sottoscrittore*), è un utente di un'organizzazione abilitato alla messaggistica unificata. I sottoscrittori utilizzano Outlook Voice Access per accedere alle proprie cassette postali via telefono per recuperare messaggi di posta elettronica, messaggi vocali, contatti personali e informazioni sul calendario.

**Sommario**

Outlook Voice Access overview

Outlook Voice Access interfaces

Outlook Voice Access scenarios

Distribution groups and contact groups

Choosing a language

Controlling Outlook Voice Access features

## Panoramica di Outlook Voice Access

In Messaggistica unificata di Microsoft Exchange, un utente abilitato alla messaggistica unificata può eseguire una chiamata a un numero telefonico interno o esterno configurato su un dial plan di messaggistica unificata per accedere alla sua cassetta postale e utilizzare il sistema di menu disponibile in Outlook Voice Access. Utilizzando questo menu, gli utenti abilitati alla messaggistica unificata possono leggere messaggi di posta elettronica, ascoltare messaggi vocali, interagire con il proprio calendario di Outlook, accedere ai contatti personali ed eseguire attività quali la configurazione del PIN di Outlook Voice Access o la registrazione dei messaggi di saluto.

Due tipi di utenti autenticati e non autenticati, possono chiamare un numero Outlook Voice Access. Quando un utente non autenticato chiama in un numero Outlook Voice Access che è impostato su un dial plan di messaggistica unificata, sono solo in grado di eseguire ricerche di directory per gli utenti. Gli utenti autenticati, quelli immettere il proprio PIN possono eseguire ricerche di directory e accedere alle cassette postali per ascoltare la posta elettronica, gli elementi del calendario e segreteria telefonica e cercare contatti personali dell'utente. Quando si esegue la ricerca per un utente nella directory o di contatti personali, dopo aver individuato l'utente, possono trasferire le chiamate a un utente o chiamare l'interno dell'utente.

## Interfacce di Outlook Voice Access

Sono disponibili due interfacce utente di messaggistica unificata per gli utenti di Outlook Voice Access: l'interfaccia telefonica e l'interfaccia utente vocale che utilizza il riconoscimento vocale automatico.

Prima che gli utenti possono utilizzare l'interfaccia vocale in Outlook Voice Access, che deve essere abilitato per il dial plan di messaggistica unificata e per il criterio cassetta postale di messaggistica unificata e inoltre essere abilitato per l'utente. Per impostazione predefinita, quando si crea un dial plan e un criterio cassetta postale di messaggistica unificata e Abilita segreteria telefonica per un utente, l'utente può utilizzare ASR o l'interfaccia vocale di Outlook Voice Access per esplorare i menu, i messaggi e altre opzioni. Tuttavia, anche se l'utente è in grado di utilizzare l'interfaccia vocale, si sarà necessario utilizzare il tastierino telefono per immettere il proprio PIN, selezionare le opzioni personali ed eseguire una ricerca nella directory. Nella tabella seguente sono elencate le impostazioni predefinite.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente di messaggistica unificata</th>
<th>Impostazione predefinita</th>
<th>Esempio di Exchange Management Shell per consentire l'accesso dell'interfaccia utente vocale</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dial plan di messaggistica unificata</p></td>
<td><p>Abilitato</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -AutomaticSpeechRecognitionEnabled  $true</code></p></td>
</tr>
<tr class="even">
<td><p>Criterio cassetta postale di messaggistica unificata</p></td>
<td><p>Abilitato</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyUMPolicy -AllowAutomaticSpeechRecognition  $true</code></p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale dell'utente</p></td>
<td><p>Abilitato</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -AutomaticSpeechRecognitionEnabled $true</code></p></td>
</tr>
</tbody>
</table>


La sezione seguente comprende gli scenari che descrivono la funzionalità di interfaccia utente vocale.

Inizio pagina

## Scenari di Outlook Voice Access

Di seguito, sono riportati esempi su come utilizzare Outlook Voice Access da un telefono:

  - **Accesso alla posta elettronica**   Un utente di Outlook Voice Access effettua una chiamata a un numero di Outlook Voice Access da un telefono e desidera accedere alla propria posta elettronica. Il prompt vocale scandisce "Benvenuti. È stata eseguita la connessione a Microsoft Exchange. Per accedere alla cassetta postale, inserire il proprio numero di interno. Per contattare qualcuno, premere il tasto cancelletto." Dopo aver immesso il numero di interno della propria cassetta postale, il prompt vocale richiede di immettere il PIN e di premere il tasto cancelletto. Una volta immesso il PIN, il prompt vocale recita "Sono presenti 2 nuovi messaggi vocali, 10 nuovi messaggi di posta elettronica e la prossima riunione è alle 10.00. Dire segreteria telefonica, posta elettronica, calendario, contatti personali, directory od opzioni personali." Quando l'utente pronuncia "Posta elettronica", il sistema di caselle vocali legge l'intestazione dei messaggi, quindi il nome, l'oggetto, l'ora e la priorità dei messaggi presenti nella cassetta postale dell'utente.

  - **Accesso al calendario**   Un utente di Outlook Voice Access effettua una chiamata a un numero di Outlook Voice Access da un telefono e desidera accedere al proprio calendario. Viene riprodotto il prompt vocale, "Benvenuti. È stata eseguita la connessione a Microsoft Exchange. Per accedere alla cassetta postale, immettere il proprio interno. Per contattare qualcuno, premere il tasto cancelletto." Dopo aver immesso il numero di interno della propria cassetta postale, il prompt vocale richiede di immettere il PIN e di premere il tasto cancelletto. Una volta immesso il PIN, il prompt vocale recita "Sono presenti 2 nuovi messaggi vocali, 10 nuovi messaggi di posta elettronica e la prossima riunione è alle 10.00. Dire segreteria telefonica, posta elettronica, calendario, contatti personali, directory od opzioni personali." Quando l'utente pronuncia "Calendario", il sistema di caselle vocali richiede di indicare il giorno specifico da visualizzare. Se l'utente sceglie il calendario odierno, il sistema di caselle vocali risponde aprendo il calendario relativo al giorno specificato. e quindi leggerà gli appuntamenti dell'utente per quel giorno.
    

    > [!NOTE]
    > Se un server Cassette postali su cui è in esecuzione il servizio di messaggistica unificata di Microsoft Exchange riscontra un elemento di calendario danneggiato nella cassetta postale di un utente, l'elemento non verrà letto e l'utente verrà inviato al menu principale di Outlook Voice Access, ignorando la lettura di eventuali riunioni aggiuntive pianificate per il resto del giorno.



  - **Accesso al sistema di caselle vocali**   Un utente di Outlook Voice Access effettua una chiamata a un numero di Outlook Voice Access da un telefono e desidera accedere alla proprio sistema di caselle vocali. Viene riprodotto il prompt vocale, "Benvenuti. È stata eseguita la connessione a Microsoft Exchange. Per accedere alla cassetta postale, immettere il proprio interno. Per contattare qualcuno, premere il tasto cancelletto." Dopo aver immesso il numero di interno della propria cassetta postale, il prompt vocale richiede di immettere il PIN e di premere il tasto cancelletto. Una volta immesso il PIN, il prompt vocale recita "Sono presenti 2 nuovi messaggi vocali, 10 nuovi messaggi di posta elettronica e la prossima riunione è alle 10.00. Dire segreteria telefonica, posta elettronica, calendario, contatti personali, directory od opzioni personali." Quando l'utente pronuncia "Segreteria telefonica", il sistema di caselle vocali legge l'intestazione dei messaggi, quindi il nome, l'oggetto, l'ora e la priorità dei messaggi vocali presenti nella cassetta postale del sottoscrittore.
    

    > [!NOTE]
    > Se è abilitato il riconoscimento vocale, gli utenti possono accedere cassetta postale abilitata alla messaggistica unificata tramite input vocale. I sottoscrittori possono inoltre utilizzare composizione a toni, noto anche come dual tone di segnali multifrequenza (DTMF) premendo 0. Riconoscimento vocale non è abilitato per l'input PIN.



  - **Individua un utente nella directory**   Un utente di Outlook Voice Access effettua una chiamata a un numero di Outlook Voice Access da un telefono e desidera individuare una persona nella directory pronunciandone l'alias di posta posta elettronica. Viene riprodotto il prompt vocale, "Benvenuti. È stata eseguita la connessione a Microsoft Exchange. Per contattare qualcuno, premere il tasto cancelletto." L'utente preme il tasto cancelletto, quindi utilizza gli input a toni per specificare l'indirizzo SMTP della persona.
    

    > [!NOTE]
    > La funzionalità di ricerca nella directory con un numero di Outlook Voice Access non è abilitata per i comandi vocali. L'utente può specificare il nome della persona che desidera contattare soltanto mediante input a toni.

    

    > [!IMPORTANT]
    > Presso alcune società (in particolare nell'Asia orientale), è possibile che i telefoni negli uffici non abbiano le lettere sui tasti. Ciò rende praticamente impossibile utilizzare la funzionalità di digitazione del nome mediante interfaccia a toni, se non si dispone di una conoscenza approfondita del mapping dei tasti. Per impostazione predefinita, la messaggistica unificata utilizza il mapping dei tasti E.161. Ad esempio, 2=ABC, 3=DEF, 4=GHI, 5=JKL, 6=MNO, 7=PQRS, 8=TUV, 9=WXYZ.

    
    Durante l'immissione di una combinazione di lettere e numeri, ad esempio Mike1092, le cifre numeriche sono associate ai tasti corrispondenti. Per immettere correttamente l'alias di posta elettronica di Mike1092, l'utente dovrà premere i numeri 64531092. Inoltre, per i caratteri diversi da A-Z e 0-9, non è disponibile un equivalente nei tasti del telefono. Quindi, questi caratteri non devono essere immessi. Ad esempio, l'alias di posta elettronica jim.wilson verrebbe immesso come 546945766. Benché i caratteri da immettere siano 10, l'utente immetterà soltanto 9 cifre, dal momento che il punto (.) non ha un equivalente sui tasti.

Inizio pagina

## Gruppi di distribuzione e di contatti

Gli utenti possono utilizzare Outlook Voice Access per inviare o inoltrare un messaggio vocale, un messaggio di posta elettronica o una convocazione di riunione. Possono inviare o inoltrare il messaggio o la convocazione di riunione a uno qualsiasi dei seguenti utenti:

  - Una persona presente nella cartella personale Contatti

  - Una persona presente nella rubrica condivisa dell'organizzazione

  - Un gruppo di contatti creato nella cartella Contatti

  - Un gruppo di distribuzione incluso nella rubrica condivisa dell'organizzazione

Possono inviare messaggi e convocazioni di riunioni utilizzando l'interfaccia utente vocale (se è stato attivato il riconoscimento vocale automatico) o utilizzando gli input a toni sul tastierino del telefono. Possono, inoltre, utilizzare Outlook Voice Access anche per ascoltare informazioni dettagliate su un gruppo, compresi i membri appartenenti al gruppo.


> [!NOTE]
> Se un utente tenta di inviare un messaggio a un gruppo (un gruppo di distribuzione nella rubrica condivisa o un gruppo di contatti nella propria cartella personale Contatti) privo di membri, il sistema di caselle vocali non consentirà l'invio o l'inoltro del messaggio o della convocazione di riunione. Se si tenta di aggiungere un gruppo senza membri come uno dei destinatari di un messaggio o di una convocazione di riunione creata sul telefono, il sistema di caselle vocali non aggiungerà il gruppo al messaggio e riporterà: "Impossibile inviare il messaggio, in quanto il contatto non dispone di un indirizzo di posta elettronica valido."



## Selezione di una lingua

Gli utenti non possono modificare la lingua utilizzata da Outlook Voice Access per comunicare con essi e quella utilizzata dagli utenti stessi per la risposta. Il sistema di caselle vocali tenta di individuare e utilizzare la corrispondenza migliore per la lingua scelta dall'utente al momento dell'accesso a MicrosoftOutlook Web App o quella scelta nelle impostazioni regionali in Outlook Web App. Se la lingua selezionata non è supportata da Outlook Voice Access, il sistema di caselle vocali utilizzerà la stessa lingua ascoltata dai chiamanti quando viene richiesto loro di lasciare un messaggio vocale.

Inizio pagina

## Controllo delle funzionalità di Outlook Voice Access

Per impostazione predefinita, quando gli utenti accedono a Outlook Voice Access, è possibile utilizzare il telefono per accedere alle loro calendario, posta elettronica e contatti personali e di eseguire ricerche nella directory. È possibile utilizzare la Shell per impedire agli utenti di accedere a uno o più di queste funzionalità, mentre utilizzano Outlook Voice Access per accedere alla cassetta postale. Quando si modificano le funzionalità di Outlook Voice Access in un criterio cassetta postale di messaggistica unificata, le modifiche influiscono sulla tutti gli utenti che sono associati al criterio cassetta postale di messaggistica unificata. È inoltre possibile disattivare alcune caratteristiche in postale una singola cassetta, anche se le altre funzionalità possono essere disattivati solo su un criterio cassetta postale di messaggistica unificata e non sono disponibili in una singola cassetta postale.


> [!NOTE]
> Le impostazioni dell'interfaccia telefonica di Outlook Voice Access per gli utenti abilitati alla messaggistica unificata o i criteri cassetta postale di messaggistica unificata possono essere modificate solo utilizzando Shell.



**Impostazioni dei criteri cassetta postale di messaggistica unificata**   È possibile disabilitare l'accesso degli utenti per le caratteristiche di Outlook Voice Access seguenti in un criterio cassetta postale di messaggistica unificata:

  - Riconoscimento vocale automatico

  - Accesso senza PIN alla posta vocale

  - Risposte vocali ad altri messaggi

  - Accesso dell'interfaccia telefonica al calendario

  - Accesso dell'interfaccia telefonica alla directory

  - Accesso dell'interfaccia telefonica alla posta elettronica

  - Accesso dell'interfaccia telefonica ai contatti personali

**Impostazioni delle cassette postali abilitate alla messaggistica unificata**   È possibile disabilitare l'accesso di un utente alle seguenti funzionalità di Outlook Voice Access nella cassetta postale dell'utente:

  - Accesso dell'interfaccia telefonica al calendario

  - Accesso dell'interfaccia telefonica alla posta elettronica

  - Riconoscimento vocale automatico

È possibile evitare che gli utenti ricevano messaggi vocali, ma nel contempo lasciare loro la possibilità di accedere alla propria cassetta postale utilizzando Outlook Voice Access. È possibile abilitare un utente alla messaggistica unificata e configurarne la cassetta postale con un numero di interno non utilizzato da altri utenti nell'organizzazione.

Inizio pagina


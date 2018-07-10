---
title: 'Rispondere automaticamente e il routing delle chiamate in arrivo: Exchange 2013 Help'
TOCTitle: Rispondere automaticamente e il routing delle chiamate in arrivo
ms:assetid: d3dcd488-bd57-44cc-bdd4-ddee42a69dde
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124724(v=EXCHG.150)
ms:contentKeyID: 50481754
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rispondere automaticamente e il routing delle chiamate in arrivo

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-08-26_

La messaggistica unificata di Microsoft consente di creare uno o più operatori automatici di messaggistica unificata, in base alle esigenze dell'organizzazione. Diversamente dagli altri componenti di messaggistica unificata, quali dial plan e gateway IP, non è necessario creare gli operatori automatici di messaggistica unificata. Tuttavia, gli operatori automatici consentono ai chiamanti interni ed esterni di individuare gli utenti o i reparti presenti in un'organizzazione e di trasferire loro le chiamate. In questo argomento viene descritta la funzionalità degli operatori automatici di messaggistica unificata.

**Sommario**

Auto attendants

UM auto attendants

Auto attendants with multiple languages

Non-business and business hours custom greetings

Menu navigation entries

Auto attendant examples

## Operatori automatici

In ambienti di telefonia o di messaggistica unificata, un operatore automatico o un sistema di menu con operatori automatici trasferisce i chiamanti al numero di interno di un utente o di un reparto senza l'intervento di un centralinista o di un operatore. In molti sistemi con operatore automatico il centralinista o l'operatore può essere raggiunto premendo o pronunciando lo zero. L'operatore automatico è una funzionalità disponibile nella maggior parte delle moderne soluzioni PBX (Private Branch eXchange), IP PBX e di messaggistica unificata.

Alcuni sistemi con operatori automatici utilizzano menu informativi di soli messaggi e menu vocali che consentono all'organizzazione di fornire informazioni sugli orari di ufficio, sul raggiungimento delle sedi dell'azienda, sulle opportunità di lavoro e risposte ad altre domande frequenti. Dopo la riproduzione del messaggio, i chiamanti vengono inoltrati al centralinista o all'operatore oppure possono tornare al menu principale.

Nei sistemi con operatori automatici più complessi, il sistema di menu può essere utilizzato per passare ad altri menu con operatori automatici, per individuare un utente nel sistema o per il trasferimento a un'altra linea telefonica esterna. Il sistema di menu può inoltre essere utilizzato per consentire al chiamante di interagire con il sistema in determinate situazioni, ad esempio quando uno studente si iscrive a un corso universitario o quando controlla i voti ottenuti, oppure quando viene attivata una carta di credito tramite telefono.

Gli operatori automatici sono indubbiamente di grande utilità, tuttavia se non vengono progettati e configurati correttamente possono disorientare e ostacolare i chiamanti. Ad esempio, in particolare nelle organizzazioni di grandi dimensioni, se gli operatori automatici non sono progettati correttamente i chiamanti passano in genere attraverso una lunga serie di domande e di prompt di menu prima di essere finalmente trasferiti alla persona in grado di rispondere alle loro domande.

## Operatori automatici di messaggistica unificata

La messaggistica unificata consente di creare uno o più operatori automatici di messaggistica unificata, in base alle esigenze dell'organizzazione. Gli operatori automatici di messaggistica unificata possono essere utilizzati per creare un sistema di menu vocali per un'organizzazione che consenta ai chiamanti interni ed esterni di spostarsi all'interno del sistema dei menu degli operatori automatici di messaggistica unificata, allo scopo di individuare ed eseguire o trasferire le chiamate agli utenti dell'azienda o ai reparti dell'organizzazione.

Quando utenti anonimi o non autenticati chiamano un numero di telefono aziendale esterno oppure quando chiamanti interni chiamano un numero di interno definito, ricevono una serie di istruzioni vocali volte ad agevolare l'esecuzione della chiamata o l'individuazione di un utente nell'organizzazione e quindi l'esecuzione della chiamata verso l'utente. L'operatore automatico di messaggistica unificata è costituito dall'insieme di istruzioni vocali o file WAV che i chiamanti ascoltano in luogo di un operatore umano quando chiamano un'organizzazione che dispone del servizio Messaggistica unificata. L'operatore automatico di messaggistica unificata consente ai chiamanti di spostarsi all'interno del sistema di menu, di eseguire chiamate o di individuare gli utenti utilizzando gli input del segnale multifrequenza DTMF (Dual tone multi-frequency) o gli input vocali. Tuttavia, per utilizzare il riconoscimento vocale automatico (ASR, Automatic Speech Recognition) o gli input vocali, è necessario abilitare la funzionalità ASR dell'operatore automatico di messaggistica unificata.

Un operatore automatico di messaggistica unificata dispone delle seguenti funzionalità:

  - Fornisce messaggi aziendali o messaggi di saluto informativi.

  - Fornisce menu aziendali personalizzati. È possibile personalizzare tali menu in modo da creare più livelli.

  - Fornisce una funzione di ricerca nella directory che consente a un chiamante di cercare un nome nella directory dell'organizzazione.

  - Consente a un chiamante di collegarsi al telefono di membri dell'organizzazione o di lasciare loro un messaggio.

Non vi è alcun limite al numero di operatori automatici di messaggistica unificata che è possibile creare. Ogni operatore automatico della messaggistica unificata è in grado di supportare un numero illimitato di numeri di interni. Un operatore automatico di messaggistica unificata può fare riferimento a un solo dial plan di messaggistica unificata, e può fare riferimento o collegarsi ad altri operatori automatici.

Una chiamata in ingresso ricevuta da un numero di telefono esterno o da un numero di interno viene trasferita tra i server Exchange e quindi inviata a un operatore automatico di messaggistica unificata. L'operatore automatico di messaggistica unificata viene configurato dall'amministratore per l'utilizzo di file vocali preregistrati (WAV) che vengono quindi riprodotti tramite telefono per il chiamate consentendogli di spostarsi attraverso il sistema dei menu della messaggistica unificata. I file .wav utilizzati per configurare un operatore automatico di messaggistica unificata possono essere personalizzati in base alle esigenze dell'organizzazione.

Inizio pagina

## Operatori automatici in più lingue

Esistono delle situazioni in cui è possibile fornire ai chiamanti operatori automatici con diverse lingue. L'impostazione della lingua disponibile per un operatore automatico di messaggistica unificata consentono di configurare la lingua predefinita dell'operatore automatico. Quando si utilizzano le istruzioni vocali predefinite di sistema per l'operatore automatico, la lingua configurata verrà utilizzata dall'operatore automatico per rispondere alle chiamate in arrivo. Questa impostazione della lingua influisce solo sulle istruzioni di sistema predefinite. L'impostazione della lingue non influisce sui prompt personalizzati configurati su un operatore automatico.

Per le distribuzioni locali o ibride, quando si installa la versione inglese (USA), questa è la sola lingua disponibile per la configurazione degli operatori automatici di messaggistica unificata. Se tuttavia si installa una versione localizzata, ad esempio il giapponese, è possibile configurare l'operatore automatico creato per utilizzare il giapponese o l'inglese (USA) come lingua predefinita. Per consentire l'utilizzo di altre lingue predefinite in un operatore automatico, è possibile installare pacchetti di lingue aggiuntive per la messaggistica unificata.

Ad esempio, se l'attività ha la propria sede negli Stati Uniti ma richiede un sistema di menu che fornisca ai chiamanti le opzioni Inglese (Stati Uniti), Spagnolo e Francese, è necessario anzitutto installare i supporti lingua di messaggistica unificata richiesti. In questo caso, se è stata installata la versione inglese (USA), dovrebbe essere installato il supporto lingua di messaggistica unificata per lo spagnolo e il francese. Tuttavia, poiché un operatore automatico di messaggistica unificata può disporre di una sola lingua configurata alla volta, è possibile creare quattro operatori automatici: un operatore automatico principale configurato per l'utilizzo dell'inglese (USA) e un operatore automatico per ciascuna lingua inglese (USA), spagnolo e francese. Dopo di che sarebbe necessario configurare l'operatore automatico principale in modo che disponga delle associazioni di tasti appropriate e sia in grado di spostarsi tra i menu per accedere agli altri operatori automatici creati per ciascuna lingua. In questo esempio, l'operatore automatico principale risponde a una chiamata in arrivo e il chiamante sente il seguente messaggio: "Benvenuti alla Contoso, Ltd. Per l'inglese, premere o pronunciare 1. Per lo spagnolo, premere o pronunciare 2. Per il francese, premere o pronunciare 3."


> [!TIP]
> Nella messaggistica unificata di Exchange, gli utenti di Outlook Voice Access autenticati e non autenticati non possono cercare utenti nella directory adoperando gli input del riconoscimento vocale automatico (ASR) in alcuna lingua. I chiamanti che chiamano un operatore automatico, però, possono utilizzare gli input vocali in più lingue per esplorare i menu dell'operatore automatico e cercare utenti nella directory.



Inizio pagina

## Messaggi di saluto personalizzati per l'orario di ufficio e non di ufficio

Una volta creato un operatore automatico di messaggistica unificata, verrà utilizzato un prompt di sistema predefinito per il messaggio di saluto Istruzione vocale menu principale Orario non di ufficio riprodotto per il chiamante dopo la formula di benvenuto Orario non di ufficio. Anche se i prompt di sistema non devono essere sostituiti o modificati, è probabile che si desideri personalizzare i messaggi di saluto e le istruzioni vocali del menu utilizzate con gli operatori automatici di messaggistica unificata. Spesso, oltre alla configurazione della formula di benvenuto personalizzata Orario non di ufficio, sarà possibile creare e configurare un messaggio personalizzato di saluto Istruzione vocale menu principale Orario non di ufficio. Una volta configurato il messaggio di saluto personalizzato, è necessario abilitare il mapping dei tasti per l'operatore automatico di messaggistica unificata per l'orario non di ufficio.

Il messaggio di saluto personalizzato per l'istruzione del menu principale dell'orario non di ufficio è un elenco di opzioni che i chiamanti ascoltano al di fuori dell'orario di ufficio. Per abilitare i chiamanti all'ascolto del messaggio di saluto del menu principale Orario non di ufficio, è necessario configurare prima la pianificazione dell'orario di ufficio e di quello al di fuori dell'orario di ufficio utilizzando EAC oppure il cmdlet **Set-UMAutoAttendant** in Shell. Ad esempio, "In questo momento gli uffici della Trey Research sono chiusi. Per una richiesta di pronto soccorso, riagganciare e comporre il 911. Per lasciare un messaggio a uno dei nostri medici, premere 1. Per lasciare un messaggio a uno dei nostri fisioterapisti, premere 2. Per lasciare un messaggio generico a uno dei nostri coordinatori di direzione, premere 3. Per parlare con un operatore, premere 0."

Per impostazione predefinita, quando si crea un operatore automatico di messaggistica unificata le istruzioni vocali o i messaggi di saluto per l'orario di ufficio e non di ufficio non sono configurati e non sono state definite le voci di spostamento nei menu principali per l'orario di ufficio o non di ufficio. Per configurare in modo corretto i messaggi di saluto e le istruzioni vocali personalizzate del menu principale per l'orario non di ufficio, è necessario:

1.  Configurare l'orario di ufficio e non di ufficio dalla pagina **Orario di ufficio**.

2.  Creare il file del messaggio di saluto che verrà utilizzato per la formula di benvenuto durante gli orari non di ufficio.

3.  Configurare la formula di benvenuto per gli orari non di ufficio nella pagina **Messaggi di saluto**.

4.  Creare il file del messaggio di saluto che verrà utilizzato per il messaggio di saluto per l'istruzione del menu principale dell'orario non di ufficio.

5.  Configurare il messaggio di saluto per l'istruzione vocale del menu principale dell'orario non di ufficio nella pagina **Messaggi di saluto**.

6.  Abilitare lo spostamento tra menu e aggiungere le voci relative dalla pagina **Navigazione nei menu**.

Inizio pagina

## Voci di spostamento tra menu

Se si utilizza il messaggio di saluto predefinito dell'istruzione vocale del menu principale e si definiscono una o più voci di spostamento tra menu, il motore di sintesi vocale (TTS, Text-to-Speech) di messaggistica unificata sintetizzerà un'istruzione vocale del menu principale. Tuttavia, il motore di sintesi vocale sintetizzerà solo l'istruzione vocale del menu principale se è configurato il messaggio di saluto predefinito ed è stata definita almeno una voce di spostamento tra menu. Il motore di sintesi vocale non sintetizzerà l'istruzione vocale del menu principale se si utilizza un'istruzione vocale personalizzata, ad esempio, "Per il reparto vendite, premere 1. Per il reparto assistenza, premere 2." Per creare l'istruzione vocale del menu principale, è necessario creare due voci di spostamento tra menu: uno denominato "Reparto vendite" e un altro "Reparto assistenza", quindi configurare la voce di mapping dei tasti per riprodurre un file audio, eseguire il trasferimento a un numero di interno oppure inviare il chiamante a un altro operatore automatico.

Quando vengono configurate le voci di spostamento tra menu, vengono definite le opzioni e le operazioni che verranno eseguite se un chiamante pronuncia una frase mentre sta utilizzando un operatore automatico abilitato al servizio di sintesi vocale o se preme un tasto sulla tastiera del telefono mentre sta utilizzando un operatore automatico non abilitato al servizio di sintesi vocale. Per configurare le voci di spostamento tra menu per operatore automatico, è necessario:

  - Abilitare la navigazione nei menu in orario non di ufficio.

  - Aggiungere le voci di spostamento tra menu.

  - Digitare il nome della voce di navigazione nei menu.

  - Selezionare un'opzione dall'elenco **Quando viene premuto questo tasto** e utilizzare la casella **Riproduci il seguente file audio** per caricare il file audio da riprodurre.

  - Configurare l'azione che si desidera eseguire:
    
      - Trasferisci a questo numero di interno
    
      - Trasferisci a questo operatore automatico di messaggistica unificata
    
      - Lascia un messaggio vocale per questo utente
    
      - Notifica sede aziendale
    
      - Notifica orario di ufficio

Inizio pagina

## Esempi di operatori automatici

Nei seguenti esempi viene illustrato come utilizzare gli operatori automatici di messaggistica unificata con la messaggistica unificata:

  - **Esempio 1**   Nel caso di una società denominata Contoso, Ltd., i clienti esterni possono utilizzare tre numeri di telefono esterni: 425-555-0111 (Uffici aziendali), 425-555-0122 (Supporto tecnico) e 425-555-0133 (Vendite). I reparti Risorse umane, Amministrazione e Contabilità dispongono di numeri di telefono interni a cui si accede solo tramite l'operatore automatico di messaggistica unificata degli uffici aziendali.
    
    Per creare una struttura di operatori automatici che supporti questo scenario, vengono creati e configurati tre operatori automatici di messaggistica unificata, ciascuno con il numero di telefono esterno appropriato. Vengono creati altri tre operatori di messaggistica unificata per ciascun reparto degli uffici aziendali. Ciascun operatore automatico viene configurato in base alle proprie esigenze, ad esempio scegliendo il tipo di messaggio di saluto o altre informazioni sull'esplorazione dei menu.

  - **Esempio 2**   Nel caso della società denominata Contoso, Ltd., i clienti esterni chiamano il numero principale della società, 425-555-0100. Quando un chiamante esterno chiama il numero esterno, risponderà l'operatore automatico di messaggistica unificata con un messaggio di benvenuto e quindi inviterà l'utente a premere o a pronunciare "Uno" per essere trasferito all'amministrazione, a premere o a pronunciare "Due" per essere trasferito al supporto tecnico, a premere o a pronunciare "Tre" per essere trasferito al servizio informazioni dell'azienda. e infine a premere o a pronunciare "Zero" per essere trasferito all'operatore." Per creare una struttura di operatori automatici di messaggistica unificata che supporti questo scenario, viene creato un operatore automatico di messaggistica unificata che dispone di estensioni personalizzate in grado di instradare la chiamata al numero di interno appropriato.

Inizio pagina


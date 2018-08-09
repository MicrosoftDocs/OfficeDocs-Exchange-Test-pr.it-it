---
title: 'Consente di visualizzare trascrizione posta vocale: Exchange 2013 Help'
TOCTitle: Consentire agli utenti di visualizzare una trascrizione di posta vocale
ms:assetid: c5192e05-905c-440f-beec-1f697edc15b3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff629381(v=EXCHG.150)
ms:contentKeyID: 51407418
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consentire agli utenti di visualizzare una trascrizione di posta vocale

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Anteprima casella vocale è una funzionalità disponibile per gli utenti che utilizzano la messaggistica unificata per ricevere i messaggi vocali. L'anteprima della casella vocale migliora le funzionalità esistenti della casella vocale di messaggistica unificata offrendo una versione di testo delle registrazioni audio. Il testo del messaggio vocale viene visualizzato nei messaggi di posta elettronica in MicrosoftOutlook Web App, Outlook 2010 e versioni successive, nonché un altri programmi di posta elettronica supportati. Per ulteriori informazioni, vedere [Microsoft Speech Technologies](http://go.microsoft.com/fwlink/p/?linkid=187348).

## È necessario utilizzare un programma di posta elettronica specifico?

No. La funzionalità Anteprima casella vocale è inclusa nel testo del corpo del messaggio di qualsiasi programma di posta elettronica, compresi i programmi per cellulare. Sebbene gli utenti possano utilizzare altri programmi di posta elettronica per ricevere i messaggi vocali, Outlook e Outlook Web App offrono prestazioni migliori. Ad esempio, quando si seleziona una parola specifica nel testo di Anteprima casella vocale in Outlook 2010 e versioni successive, la riproduzione audio del messaggio vocale inizierà dalla parola selezionata. Questa opzione è utile per l'ascolto di una parte specifica del messaggio vocale.

## È possibile cercare messaggi vocali specifici?

Sì. Le parole e le frasi del testo di anteprima dei messaggi vocali sono indicizzate automaticamente, quindi i messaggi vocali verranno visualizzati nei risultati della ricerca. In Outlook 2010 o versioni successive oppure in Outlook Web App, gli utenti possono anche utilizzare la casella **Note audio** per aggiungere testo relativo a un messaggio vocale. Per facilitare l'individuazione di un messaggio, le note sono incluse anche nelle ricerche.

## Perché questa funzionalità viene chiamata "Anteprima casella vocale"?

È importante indirizzare nel modo giusto le aspettative degli utenti. L'anteprima della casella vocale non genera necessariamente un testo esattamente corrispondente a quello pronunciato dai chiamanti nei messaggi vocali. In realtà, in genere è alquanto impreciso. Il termine trascrizione suggerisce un risultato migliore a quello che è generalmente possibile ottenere. Il termine anteprima suggerisce che il lettore sarà in grado di cogliere l'idea generale del contenuto del messaggio vocale, un risultato più vicino alle reali potenzialità della funzionalità.

## Che cosa rende più o meno accurato il testo di anteprima della casella vocale?

L'accuratezza del testo di Anteprima casella vocale dipende da diversi fattori che a volte è impossibile controllare. Il testo di anteprima della casella vocale ha maggiori probabilità di essere accurato quando:

  - Il chiamante lascia un messaggio vocale semplice che non contiene termini appartenenti a slang, gergo tecnico o parole o frasi non comuni.

  - Il chiamante utilizza una lingua facilmente riconoscibile e traducibile dal sistema di caselle vocali. In genere, i messaggi vocali lasciati dai chiamanti che non parlano troppo velocemente o troppo piano e che non presentano accenti marcati genereranno proposizioni e frasi più precise.

  - Il messaggio vocale è privo di rumori di fondo, echi e interruzioni audio.

## Quali lingue è possibile utilizzare con Anteprima casella vocale?

Il testo di anteprima delle caselle vocali è disponibile nelle seguenti lingue:

  - Inglese (Stati Uniti) (en-US)

  - Inglese (Canada) (en-CA)

  - Francese (Francia) (fr-FR)

  - Italiano (it-IT)

  - Polacco (pl-PL)

  - Portoghese (Portogallo) (pt-PT)

  - Spagnolo (Spagna) (es-ES)

Se si dispongono di un locale o la distribuzione ibrida di messaggistica UNIFICATA, è possibile scaricare i language pack di messaggistica UNIFICATA dall' [Area Download Microsoft](https://go.microsoft.com/fwlink/?linkid=266542).

Se si dispone di una distribuzione locale o ibrida, dopo aver installato un Language Pack di messaggistica unificata, il dial plan e gli operatori automatici possono essere configurati per l'uso della lingua scelta. Per gli utenti online, non è necessario installare Language Pack di messaggistica unificata. Molte aziende dispongono di un solo dial plan di messaggistica unificata. La messaggistica unificata tenterà di creare un'anteprima casella vocale nella lingua del dial plan predefinita, ma tale lingua deve supportare Anteprima casella vocale. Un dial plan di messaggistica unificata può essere configurato per la creazione di anteprime delle caselle vocali in una sola lingua alla volta.

Per configurare la messaggistica unificata in modo che le anteprime delle caselle vocali siano disponibili in una lingua diversa dall'inglese (en-US), procedere come segue:

1.  Verificare che l'anteprima della casella vocale sia supportata nella lingua che si desidera utilizzare.

2.  In caso di distribuzione locale o ibrida, scaricare e installare il Language Pack di messaggistica unificata appropriato. Tale operazione non comporta la configurazione della lingua predefinita del dial plan.

3.  Configurare il dial plan con la lingua che sarà utilizzata per Anteprima casella vocale. Per ulteriori informazioni, vedere [Impostare la lingua predefinita per un dial plan](set-the-default-language-on-a-dial-plan-exchange-2013-help.md).

Le modalità di visualizzazione del testo di anteprima della casella vocale nelle lingue supportate dipende dal tipo di messaggio vocale inviato. Esistono due tipi:

  - **Messaggi vocali registrati quando un utente non risponde al telefono**
    
    Per questi messaggi, la lingua utilizzata per Anteprima casella vocale è determinata dalla lingua parlata dal chiamante e dall'eventuale supporto di tale lingua. Ad esempio, se un chiamante lascia un messaggio vocale in italiano, il testo di anteprima della casella vocale verrà visualizzato in italiano se l'italiano è stato configurato nel dial plan. Tuttavia, se un chiamante lascia un messaggio in giapponese, nel messaggio non sarà incluso alcun testo di anteprima della casella vocale perché il giapponese non è disponibile.

  - **Messaggi vocali inviati da un utente di Outlook Voice Access**
    
    Per i messaggi inviati da un utente di Outlook Voice Access, la lingua utilizzata da Anteprima casella vocale è controllata dall'amministratore della posta vocale. Di conseguenza, il testo di Anteprima casella vocale sarà la stessa del sistema di caselle vocali. Tuttavia, se un chiamante la cui lingua non è supportata per Anteprima casella vocale utilizza Outlook Voice Access per lasciare un messaggio, nel messaggio non sarà incluso alcun testo di anteprima del messaggio vocale. Per ulteriori informazioni su Outlook Voice Access, vedere [Configurazione di Outlook Voice Access](setting-up-outlook-voice-access-exchange-2013-help.md).

## La messaggistica unificata rileva se l'anteprima di un messaggio vocale non è precisa?

Il livello di sicurezza è determinato per ogni anteprima inclusa in un messaggio vocale. Il sistema di caselle vocali calcola il livello di perfezione con cui i suoni delle registrazioni corrispondono alle parole, ai numeri e alle frasi. Se le corrispondenze vengono trovate facilmente, il livello di sicurezza è alto. Un livello di probabilità alto è in genere associato a una precisione maggiore.

Se il livello di sicurezza è inferiore a un determinato valore, la frase **Anteprima casella vocale (confidenza bassa)** appare sopra il testo dell'anteprima del messaggio vocale. Se il livello di probabilità è alto, probabilmente l'anteprima del testo risulterà inaccurata.

La messaggistica unificata utilizza il riconoscimento vocale automatico (ASR, Automatic Speech Recognition) per calcolare il livello di sicurezza nell'anteprima, ma non è possibile stabilire quali parole siano corrette e quali errate.

Il sistema cerca tuttavia di migliorare la precisione delle anteprima dei messaggi vocali. Ad esempio, cerca la corrispondenza tra il numero del chiamante (se fornito) e i contatti personali dell'utente, la rubrica dell'organizzazione o i contatti dei social network. Se la corrispondenza viene rilevata, includerà il nome del chiamante, insieme agli elenchi standard di nomi e parole, quando viene eseguito il riconoscimento vocale automatico (ASR) per la registrazione vocale.

## È possibile utilizzare Anteprima casella vocale se il risultato non è del tutto soddisfacente?

Gli utenti possono trarre vantaggio dalla funzionalità di anteprima della casella vocale purché cerchino di non interpretare l'anteprima alla lettera. Al contrario, è preferibile cercare nomi, numeri di telefono e frasi quali "Richiamami" o "Devo parlarti" che possono fornire indicazioni sullo scopo della chiamata.

Anteprima casella vocale non prevede la dettatura esatta dei messaggi, ma consente agli utenti di rispondere, ad esempio, alle domande riportate di seguito:

  - Questo messaggio vocale è legato al mio lavoro?

  - Questo messaggio vocale è importante per me?

  - Il chiamante ha lasciato un numero di telefono? È un numero diverso da quelli che nell'elenco corrispondono al chiamante?

  - Il chiamante considera urgente questo messaggio vocale?

  - Devo assentarmi temporaneamente dalla riunione per richiamare questa persona?

  - Era prevista una chiamata per confermare la richiesta. È la chiamata di conferma?

## La funzionalità Anteprima casella vocale può essere attivata o disattivata?

Sì. Se la funzionalità Anteprima casella vocale è abilitata, gli utenti possono attivarla o disattivarla utilizzando Outlook 2010 o versione successiva o Outlook Web App. Per installare la lingua desiderata, tuttavia, la lingua del dial plan deve supportare Anteprima casella vocale e il Language Pack di messaggistica unificata.

Sebbene le impostazioni di Anteprima casella vocale coincidano se un utente utilizza Outlook 2010 o versione successiva o Outlook Web App, le modalità di accesso tuttavia saranno diverse:

**Outlook Web App**

Per accedere alle impostazioni di Anteprima casella vocale in Outlook Web App, gli utenti possono fare clic su **Impostazioni** \> **telefono** \> **Posta vocale**. Nella pagina **Posta vocale**, le impostazioni sono disponibili sotto **anteprima casella vocale**.

Per impostazione predefinita, le opzioni della funzionalità Anteprima casella vocale sono disponibili quando l'utente è abilitato alla messaggistica unificata. Se il dial plan di messaggistica unificata è configurato per l'utilizzo di un Language Pack di messaggistica unificata in grado di supportare Anteprima casella vocale, le anteprime della casella vocale verranno create per gli utenti nei seguenti casi:

  - Un chiamante lascia un messaggio vocale perché l'utente non risponde al telefono.

  - Un utente abilitato alla messaggistica unificata accede a Outlook Voice Access e registra un messaggio vocale per uno o più destinatari.

Quando un chiamante lascia un messaggio vocale e l'opzione **Includi anteprima del testo nei messaggi vocali ricevuti** è abilitata, verrà creata un'anteprima del messaggio vocale nel messaggio di posta elettronica, il file audio verrà allegato e inviato alla cassetta postale del destinatario. Ci sono casi in cui può essere necessario disabilitare questa opzione se la lingua configurata nel dial plan non include il supporto per Anteprima casella vocale e se non si desidera includere le anteprime nei messaggi vocali.

Quando gli utenti accedono a Outlook Voice Access e inviano un messaggio vocale a un altro utente, possono deselezionare la casella di controllo **Includi testo di anteprima nei messaggi vocali inviati tramite Outlook Voice Access**. Ad esempio, potrebbe essere opportuno deselezionare questa casella se inviano messaggi vocali in una lingua non supportata da Anteprima casella vocale o se non desiderano includere l'anteprima casella vocale con il messaggio perché è troppo lungo.


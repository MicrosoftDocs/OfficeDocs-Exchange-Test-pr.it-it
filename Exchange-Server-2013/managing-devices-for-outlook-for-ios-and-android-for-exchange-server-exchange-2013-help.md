---
title: 'Gestione dei dispositivo per Outlook per iOS e Android in Exchange Server: Exchange 2013 Help'
TOCTitle: Gestione dei dispositivo per Outlook per iOS e Android in Exchange Server
ms:assetid: 16ce7d24-be74-4466-b126-828a67f69b6e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt465748(v=EXCHG.150)
ms:contentKeyID: 70076147
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione dei dispositivo per Outlook per iOS e Android in Exchange Server

 

_**Si applica a:**Exchange Server 2010, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2018-04-01_

**Riepilogo:** in questo articolo viene illustrato come Exchange Active Sync consente di gestire i dispositivi mobili con Outlook per iOS e Android in Exchange l'organizzazione locale.

Microsoft consiglia Exchange ActiveSync per la gestione dei dispositivi mobili utilizzati per accedere alle cassette postali di Exchange nell'ambiente locale. Exchange ActiveSync è un protocollo di sincronizzazione di Microsoft Exchange che consenta ai telefoni cellulari di accedere alle informazioni di un'organizzazione in un server che esegue Microsoft Exchange.

In questo articolo vengono descritte le funzionalità specifiche di Exchange ActiveSync e gli scenari relativi ai dispositivi mobili che eseguono Outlook per Android e iOS. Informazioni complete sul protocollo di sincronizzazione di Microsoft Exchange sono disponibili n [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md). Inoltre, sono disponibili informazioni sul [blog di Office](https://go.microsoft.com/fwlink/p/?linkid=62392) in cui vengono descritti in dettaglio l'applicazione delle password e altri vantaggi dell'uso di Exchange ActiveSync con dispositivi che eseguono Outlook per iOS e Android.

## Blocco PIN e crittografia dispositivo

Se i criteri dell'organizzazione Exchange ActiveSync richiedono una password nei dispositivi mobili per consentire agli utenti di sincronizzare la posta elettronica, Outlook impone il criterio a livello di dispositivo. Questo metodo funziona in modo diverso tra i dispositivi iOS e dispositivi Android, in base ai controlli disponibili forniti da Apple e Google.

Nei dispositivi iOS, Outlook controlla per assicurarsi che un passcode o PIN sia correttamente impostato. Nel caso in cui un passcode non sia impostato, verrà richiesto agli utenti di creare un passcode nelle impostazioni di iOS. Fino alla configurazione del passcode, l'utente non sarà in grado di accedere a Outlook per iOS.

Outlook per iOS viene eseguito solo in IOS 8.0 o versione successiva. Questi dispositivi vengono forniti con la crittografia incorporata che Outlook usa dopo aver abilitato il passcode per crittografare tutti i dati che Outlook memorizza localmente nel dispositivo iOS. Di conseguenza, i dispositivi iOS con un PIN verranno crittografati sia che questo sia richiesto o meno da un criterio ActiveSync.

Nei dispositivi Android, Outlook applicherà regole di blocco dello schermo. Inoltre, Google offre controlli che consentono a Outlook per Android di rispettare i criteri di Exchange relativi lunghezza e complessità della password e il numero di tentativi di sblocco schermo consentiti prima di eliminare il telefono. Outlook per Android incoraggerà inoltre la crittografia di archiviazione se non è abilitata, guidando gli utenti attraverso questa procedura con istruzioni dettagliate.

I dispositivi iOS e Android che non supportano queste impostazioni di sicurezza della password non saranno in grado di connettersi a una cassetta postale di Exchange.

## Cancellazione remota con Exchange ActiveSync

Exchange ActiveSync consente agli amministratori di cancellare in remoto i dispositivi, come se fossero compromessi. Con Outlook per iOS e Android, una cancellazione in remoto viene eseguita nell'app di Outlook, non una cancellazione completa del dispositivo.

Dopo che il comando di cancellazione in remoto viene richiesto dall'amministratore, la cancellazione si verifica entro alcuni secondi dalla connessione successiva dell'app di Outlook a Exchange. L'app di Outlook verrà reimpostata e verranno rimossi dal dispositivo tutti i file, i contatti, il calendario e la posta di Outlook, oltre che dal servizio di Outlook. La cancellazione non influirà su nessuna app e informazione personale dell'utente al di fuori di Outlook.

Poiché Outlook per iOS e Android viene visualizzato come associazione singola al dispositivo mobile in Exchange, un comando di cancellazione in remoto rimuoverà dati ed eliminerà le relazioni di sincronizzazione da tutti i dispositivi che eseguono Outlook (iPhone, iPad, Android) associati all'utente.


> [!NOTE]
> Grazie all'architettura cloud dietro Outlook per iOS e Android, il risultato di una cancellazione in remoto del dispositivo non viene registrata nuovamente in Exchange. Anche quando la cancellazione viene eseguita correttamente, verrà visualizzato lo stato <STRONG>In sospeso</STRONG>. Si tratta di un problema noto e una soluzione è in fase di sviluppo.



## Identificatori e controllo di accesso dei dispositivi

Data l'architettura basata sul cloud di Outlook per iOS e Android, le connessioni di Outlook vengono visualizzate come un singolo identificatore (ID) dispositivo mobile per ogni utente in Exchange. Ciò significa che i controlli di accesso dei dispositivi mobili per ogni utente vengono applicati a tutti i dispositivi associati a questo ID dispositivo. L'implementazione crea due condizioni diverse da come funziona il dispositivo Exchange ActiveSync tradizionale.

  - **Blocco:** una regola di blocco blocca Outlook su tutti i dispositivi e sistemi operativi supportati. Non è possibile bloccare i sistemi operativi o dispositivi singoli.

  - **Quarantena:** il processo di quarantena funziona in base ai singoli utenti, invece che in base ai singoli dispositivi. Dopo che un utente ha rilasciato un dispositivo dalla quarantena, può installare e configurare Outlook in tanti quanti dispositivi desiderati. Poiché l'utente è stato rilasciato dalla quarantena, tutti i nuovi dispositivi associati a quell'utente non verranno messi in quarantena.

Quando i criteri delle cassette postali del dispositivo mobile sono disponibili, vengono applicati a tutti i dispositivi associati. Pertanto, se si applica un blocco PIN per una cassetta postale specifica, tutti i dispositivi che si connettono a tale cassetta postale richiederanno un PIN.


> [!NOTE]
> Poiché gli ID dispositivo non sono determinati da alcun ID di <EM>dispositivo fisico</EM>, possono cambiare senza preavviso. In questo caso, è possibile che le conseguenze impreviste quando gli ID dispositivo vengono utilizzati per la gestione di dispositivi utente, come dispositivi "consentiti" esistenti potrebbero essere bloccati o messi in quarantena da Exchange in modo imprevisto. È consigliabile pertanto che gli amministratori impostino solo criteri di dispositivi mobili che consentono e bloccano i dispositivi in base al tipo di dispositivo o modello del dispositivo.



## Domande frequenti sulla gestione dei dispositivi con Exchange ActiveSync

Di seguito sono riportare le domande frequenti su password, PIN e criteri di crittografia per i dispositivi che eseguono Outlook per iOS e Android.

## L'applicazione posta nativa in iOS applica i criteri di Exchange ActiveSync relativi ai requisiti di complessità e lunghezza delle password. Perché non Outlook?

Outlook consente di sfruttare i controlli per sviluppatori delle applicazioni di terze parti che sono disponibili in Microsoft. Microsoft continuerà a migliorare questa funzionalità man mano che Apple renderà disponibili per gli sviluppatori altri controlli.

## Perché Outlook per iOS e Android applicano PIN a livello del dispositivo invece che a livello di app?

Dopo aver valutato le funzionalità disponibili in iOS e Android, Microsoft ritiene che un PIN a livello di dispositivo offra un'esperienza ottimale per i clienti in termini di comodità e sicurezza. Un PIN a livello di app indica che gli utenti devono immettere due diversi PIN per accedere alla posta elettronica, il che potrebbe non essere desiderabile. Inoltre, un PIN a livello di dispositivo, significa che è possibile usufruire delle nuove funzionalità come la crittografia nativa dei dispositivi, TouchID in IOS e Smart Lock su Android. La cancellazione in remoto viene comunque applicata a livello di app, il che significa che le applicazioni e i dati personali degli utenti non verranno interessati dalla cancellazione di Outlook.

## Se Outlook per la crittografia dei dispositivi Android supporto.

Sì, Outlook per Android supporta la crittografia del dispositivo tramite criteri cassetta postale di Exchange dispositivo mobile. Tuttavia, prima di Android 7.0, la disponibilità e l'implementazione di questo processo varia in base produttori di dispositivi e versione del sistema operativo Android, che consentono all'utente di annullare durante il processo di crittografia. Con le modifiche introdotte Google Android 7.0, Outlook per Android è ora in grado di applicare la crittografia per i dispositivi che eseguono Android 7.0 o versione successiva. Gli utenti con i dispositivi che eseguono i sistemi operativi non saranno in grado di annullare il processo di crittografia.

Anche se il dispositivo Android è crittografato e autore di un attacco è in possesso del dispositivo, purché un dispositivo PIN viene abilitato, il database di Outlook rimane inaccessibile. Ciò è valido anche con il debug USB attivato e Android SDK installato. Se un utente malintenzionato tenta radice il dispositivo per ignorare il PIN per l'accesso a queste informazioni, il processo di radice verrà annullata archiviazione di tutti i dispositivi e rimuove tutti i dati di Outlook. Se il dispositivo è in formato non crittografato e directory principale dell'utente prima di furto, è possibile che un utente malintenzionato accedere al database di Outlook, consentendo di debug nel dispositivo USB e collegare il dispositivo a un computer con SDK Android installato.


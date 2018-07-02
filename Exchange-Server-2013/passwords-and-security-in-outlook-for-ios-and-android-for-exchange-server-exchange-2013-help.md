---
title: 'Passwords and Security in Outlook for iOS and Android for Exchange Server: Exchange 2013 Help'
TOCTitle: Passwords and Security in Outlook for iOS and Android for Exchange Server
ms:assetid: e5565beb-7ef3-47c4-8daf-6d8f1d22dceb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt465750(v=EXCHG.150)
ms:contentKeyID: 70076152
ms.date: 04/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Passwords and Security in Outlook for iOS and Android for Exchange Server

 

_**Si applica a:** Exchange Server 2010, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2018-04-01_

**Sintesi:**  in questo articolo viene descritto il modo in cui password e sicurezza funzionano in Outlook per iOS e Android con Exchange Server.

La prima volta che l'app Outlook per iOS e Android viene eseguita in un ambiente Exchange locale, Outlook genera una chiave AES-128 casuale. Questa chiave è nota come la *chiave dispositivo* e viene archiviata solo nel dispositivo dell'utente.

## Creazione di un account e protezione password

Quando un utente accede a Exchange, il nome utente e la password e una chiave dispositivo AES-128 univoca vengono inviati dal dispositivo dell'utente al servizio Outlook tramite una connessione TLS, in cui la chiave del dispositivo viene conservata in una memoria di calcolo runtime. Dopo aver verificato la password con il server Exchange, il servizio Outlook usa la chiave del dispositivo per crittografare la password, quindi la password crittografata viene archiviata nel servizio. La chiave del dispositivo, nel frattempo, viene cancellata dalla memoria e non è mai archiviata nel servizio Outlook (la chiave viene archiviata solo nel dispositivo dell'utente).

Successivamente, quando un utente tenta di connettersi a Exchange per recuperare i dati della cassetta postale, la chiave del dispositivo viene nuovamente passata dal dispositivo al servizio Outlook tramite una connessione TLS protetta, dove viene utilizzata per decrittografare la password nella memoria di calcolo runtime. Una volta decrittografata, la password non viene mai archiviata nel servizio o scritta in un disco di archiviazione locale e la chiave del dispositivo viene di nuovo cancellata dalla memoria.

Dopo che il servizio Outlook ha decrittografato la password in fase di esecuzione, il servizio può quindi connettersi al server Exchange per sincronizzare posta, calendario e altri dati della cassetta postale. Finché l'utente continua ad aprire e usare Outlook periodicamente, il servizio Outlook conserverà in memoria una copia della password decrittografata dell'utente per mantenere attiva la connessione al server Exchange.

## Inattività account ed eliminazione password dalla memoria

Dopo tre giorni di inattività, il servizio Outlook eliminerà la password decrittografata dalla memoria. Avendo eliminatola password decrittografata, il servizio Outlook non è in grado di accedere alla cassetta postale dell'utente. La password crittografata rimane memorizzata nel servizio di Outlook, ma decrittografarla nuovamente non è possibile senza la chiave del dispositivo, che è disponibile solo nel dispositivo dell'utente.

Esistono tre modi in cui un account utente può diventare inattivo:

  - Outlook per iOS e Android vengono disinstallati dall'utente.

  - L'aggiornamento app in background viene disabilitato nelle opzioni Impostazioni, quindi viene applicata una chiusura forzata in Outlook.

  - Il dispositivo non è connesso a Internet, impedendo a Outlook di sincronizzarsi con Exchange.


> [!NOTE]
> Outlook non diventa inattivo solo perché l'utente non apre l'app per un periodo di tempo, ad esempio nel fine settimana o in vacanza. Finché l'aggiornamento dell'app in background è abilitato (impostazione predefinita per Outlook per iOS e Android), funzioni come le notifiche pus e la sincronizzazione in background della posta elettronica vengono considerata attività.



**Cancellazione delle password crittografate e della cache dei messaggi dal disco rigido**

Il servizio Outlook svuota o elimina gli account inattivi con cadenza settimanale. Dopo la disattivazione di un account utente, il servizio Outlook elimina dal servizio sia la password decrittografata sia il contenuto della cassetta postale memorizzata nella cache dell'utente.

**Combinazione di sicurezza dispositivo e servizio**

Ogni chiave del dispositivo unica dell'utente non viene mai archiviata nel servizio Outlook e la password di Exchange dell'utente non viene mai archiviata nel dispositivo. Questa architettura significa che affinché una parte non autorizzata possa accedere a una password utente, dovrebbe disporre dell'accesso non autorizzato al servizio Outlook e dell'accesso fisico al dispositivo dell'utente.

Implementando criteri PIN e la crittografia su dispositivi nell'organizzazione, la parte dannosa dovrebbe anche superare la crittografia del dispositivo solo per accedere alla chiave del dispositivo. Tutto ciò dovrebbe avvenire prima che all'utente venga inviata la notifica sulla compromissione del dispositivo e che possa richiedere la cancellazione remota del dispositivo.

## Domande frequenti sulla sicurezza del dispositivo

Di seguito sono riportate delle domande frequenti sulla progettazione della sicurezza e sulle impostazioni di Outlook per iOS e Android.

## Le credenziali utente rimangono archiviate nel servizio Outlook se blocco l'accesso di Outlook al server Exchange?

Se si sceglie di bloccare l'accesso di Outlook per iOS e Android ai server Exchange locali, la connessione iniziale verrà rifiutata da Exchange. Le credenziali utente non verranno archiviate dal servizio Outlook e le credenziali presentate nel tentativo di connessione non riuscito vengono immediatamente rimosse dalla memoria.

## In che modo la chiave del dispositivo univoca e la password utente crittografata vengono trasferite al servizio Outlook?

Tutte le comunicazioni tra l'app di Outlook e il servizio Outlook avvengono tramite una connessione crittografata TLS. Outlook per iOS e Android è in grado di connettersi con il servizio di Outlook e nient'altro.

## Come è possibile rimuovere le credenziali e le informazioni sulla cassetta postale utente dal servizio Outlook?

Esistono tre modi per rimuovere le informazioni dal servizio Outlook:

  - Opzione 1: avviare una cancellazione remota per ogni utente che ha utilizzato l'app per connettersi a Exchange.

  - Opzione 2: tutti gli utenti eliminano Outlook per iOS e Android. Tutti i dati verranno rimossi entro circa 3-7 giorni dal servizio Outlook.

  - Opzione 3: invitare ogni utente a rimuovere l'account dall'app Outlook, quindi eliminare l'app dai dispositivi mobili. Nell'app, chiedere agli utenti di andare a **Impostazioni**, quindi toccare **Impostazioni account**, quindi **Seleziona un account** ed **Elimina account**.

## L'app viene chiusa o disinstallata, ma continua a connettersi al server Exchange. Perché succede?

Il servizio Outlook esegue la decrittografia delle password nella memoria di calcolo runtime e le utilizza per connettersi a Exchange. Poiché il servizio Outlook si connette a Exchange per conto del dispositivo per recuperare e memorizzare nella cache i dati della cassetta postale, è possibile continuare per un breve periodo di tempo finché il servizio non rileva che Outlook non richiede più dati.

Se un utente disinstalla l'app del dispositivo senza prima usare l'opzione **Elimina account**, il servizio Outlook rimarrà connesso al server Exchange finché l'account non diventa inattivo, come descritto nella sezione sopra "Inattività account ed eliminazione password dalla memoria". Per interrompere l'attività, seguire semplicemente l'opzione 1 o 3 delle domande frequenti oppure bloccare l'app, come descritto in [Bloccare Outlook per iOS e Android](https://technet.microsoft.com/it-it/library/mt759239\(v=exchg.150\)).

## Una password è meno sicura in Outlook per iOS e Android che quando si utilizzano altri client Exchange ActiveSync?

No. I client EAS in genere salvano le credenziali utente localmente nel dispositivo dell'utente. Ciò significa che se un dispositivo viene rubato o compromesso, una parte malintenzionata potrebbe riuscire ad accedere alla password dell'utente. Con la progettazione di sicurezza di Outlook per iOS e Android, una parte non autorizzata ha bisogno dell'accesso non autorizzato al servizio cloud Outlook **e** dell'accesso fisico al dispositivo dell'utente.

## Cosa succede se un utente tenta di usare Outlook per iOS e Android dopo che i suoi dati sono stati eliminati dal servizio di Outlook?

Se un account utente diventa inattivo (ad esempio disattivando l'aggiornamento app in background sul dispositivo o se il dispositivo si disconnette da Internet per un periodo di tempo), l'app Outlook si riconnetterà al servizio Outlook al successivo riavvio dell'app e il processo di crittografia della password e di memorizzazione nella cache della posta elettronica verrà riavviato. Questa operazione è trasparente per l'utente.

## Come vengono memorizzati temporaneamente nella cache i dati della cassetta postale protetti mentre sono archiviati nel servizio Outlook?

Sono disponibili ulteriori informazioni su come sono attualmente protetti i dati nel [Centro protezione di Azure](https://azure.microsoft.com/support/trust-center/). Come indicato in precedenza, stiamo provvedendo allo spostamento di Azure in Office 365. La sicurezza di questi servizi è trattata nel [Centro protezione di Office 365](https://go.microsoft.com/fwlink/p/?linkid=525776).


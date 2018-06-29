---
title: 'Outlook for iOS and Android: Exchange 2013 Help'
TOCTitle: Outlook for iOS and Android
ms:assetid: 3a66817c-30da-4965-a6db-2955b5365b0f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt465744(v=EXCHG.150)
ms:contentKeyID: 70061458
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook for iOS and Android

 

_**Si applica a:**Exchange Server 2010, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2018-04-02_

**Riepilogo:** in questo articolo sono dell'architettura e informazioni sulla sicurezza per gli amministratori su Outlook per iOS e Android in un Exchange 2013 locale ambiente.

L'app Outlook per iOS e Android è progettata per raggruppare e-mail, calendario, contatti e altri file. In questo modo, gli utenti dell'organizzazione possono effettuare più operazioni direttamente dai dispositivi mobili. In questo articolo è riportata una panoramica sull'architettura e sulla struttura di archiviazione dell'app, in modo che gli amministratori di Exchange possano implementare e gestire Outlook per iOS e Android nelle proprie organizzazioni di Exchange.


> [!NOTE]
> The <A href="https://support.office.com/it-it/article/outlook-for-ios-and-android-help-center-cd84214e-a5ac-4e95-9ea3-e07f78d0cde">Centro assistenza di Outlook per iOS e Android</A> è disponibili per utenti e include una guida all'utilizzo dell'app su determinati dispositivi, nonché informazioni sulla risoluzione dei problemi.



## Architettura di Outlook per iOS e Android

Outlook per iOS e Android è costituita da un'app front-end installata su dispositivi mobili e da un servizio cloud sicuro e scalabile back-end, noto come *servizio Outlook*. L'elaborazione delle informazioni nel servizio Outlook abilita caratteristiche e funzionalità avanzate che migliorano l'esperienza di Outlook, offrendo anche stabilità e prestazioni ottimizzate. Questa architettura si basa sul servizio Outlook per l'elaborazione intensiva, riducendo al minimo le risorse richieste dai dispositivi degli utenti.

Esempi di cosa servire Outlook sono disponibili per gli utenti:

  - Categorizzazione della Posta in arrivo evidenziata.

  - Funzionalità di annullamento della sottoscrizione con un clic dalle liste di distribuzione.

  - Efficacia e velocità della ricerca migliorate.

  - Possibilità di inoltrare e inviare file di grandi dimensioni senza doverli prima scaricare in un dispositivo mobile.

## Memorizzazione dei dati nella cache

Per migliorare le prestazioni, un sottoinsieme di posta elettronica, calendario e dati di file dalla cassetta postale di ogni utente viene memorizzato nella cache nel servizio di Outlook. Questo servizio viene attualmente eseguito su Microsoft Azure. Si sta spostando il servizio di Outlook in Office 365 e prevede di disporre di spostamento completata non appena.

Le informazioni nel servizio di Outlook attualmente archiviate negli Stati Uniti o in Europa, in base all'indirizzo IP del client. Mentre si sposta il servizio di Outlook in Office 365, si consente di allineare i principi di interfaccia di protezione di Office 365 con una strategia di centro dati localizzato. In Office 365 paese o regione, amministratore del cliente ingressi durante l'installazione iniziale dei servizi, un cliente determina la posizione di archiviazione principale per i dati del cliente. Per ulteriori informazioni, vedere [Office 365 Trust Center](https://go.microsoft.com/fwlink/p/?linkid=525776).

## Domande frequenti sulla memorizzazione dei dati nella cache

Di seguito sono riportate delle domande frequenti sull'archiviazione dei dati in Outlook per iOS e Android.

## Quanti dati della cassetta postale di un utente vengono memorizzati nella cache del servizio Outlook?

Circa un mese di dati relativi a posta elettronica, calendario e contatti. Il processo di memorizzazione nella cache è determinato da un algoritmo che prende in considerazione, tra l'altro, le dimensioni di una cassetta postale, l'importanza relativa di una determinata cartella all'interno della cassetta postale (ad esempio, la cartella Posta in arrivo predefinita rispetto a una cartella precedentemente creata dall'utente) e la frequenza con cui un utente accede a una determinata cartella.

Il servizio Outlook consente di archiviare i dati degli allegati nel modo seguente: Quando un utente richiede di aprire un allegato di posta elettronica in Outlook dal server di Exchange e lo archivia temporaneamente. A questo punto l'allegato viene recapitato all'app nel dispositivo mobile dell'utente. I dati con più di un mese vengono periodicamente scaricati dal servizio, finché l'allegato sarà disponibile solo nel server di Exchange.

## Come è possibile rimuovere le informazioni personali dal servizio Outlook?

Sono disponibili tre opzioni per rimuovere le informazioni personali dal servizio Outlook.

  - Opzione 1: Avviare una cancellazione remota per ogni utente che ha utilizzato l'app Outlook per iOS e Android per connettersi a Office 365 o Exchange.

  - Opzione 2: Invitare tutti gli utenti a eliminare l'app Outlook. Tutti i dati verranno rimossi entro circa 3-7 giorni.

  - Opzione 3: Invitare ogni utente a rimuovere l'account dall'app Outlook ed eliminare quindi l'app dai dispositivi mobili. Per rimuovere un account, chiedere agli utenti di eseguire la procedura seguente:
    
    1.  Nell'app Outlook, in **Impostazioni** toccare **Impostazioni account**.
    
    2.  Toccare **Seleziona un account**, quindi con l'account selezionato toccare **Rimuovi account**.
    
    3.  Toccare **Dati remoti e dispositivo**.

## Come vengono memorizzati temporaneamente nella cache i dati della cassetta postale protetti mentre sono archiviati nel servizio Outlook?

Per ulteriori informazioni come i dati attualmente è protetto in [Centro protezione Azure](https://azure.microsoft.com/support/trust-center/). Come osservato in precedenza, passiamo ora da Azure per Office 365. Viene descritto come effettuare la sicurezza di questi servizi in [Office 365 Trust Center](https://go.microsoft.com/fwlink/p/?linkid=525776).


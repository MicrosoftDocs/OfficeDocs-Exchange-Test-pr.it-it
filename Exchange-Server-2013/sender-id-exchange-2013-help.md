---
title: 'ID mittente: Exchange 2013 Help'
TOCTitle: ID mittente
ms:assetid: 0f628f83-df8c-43fb-bf49-7aaa9ec69ab1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996295(v=EXCHG.150)
ms:contentKeyID: 50479994
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ID mittente

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

L'agente ID mittente è un agente di protezione da posta indesiderata disponibile in Microsoft Exchange Server 2013. L'agente ID mittente si basa sull'intestazione RECEIVED SMTP e su una query al servizio DNS del sistema mittente per stabilire l'eventuale azione da intraprendere su un messaggio in ingresso.

L'ID mittente ha lo scopo di contrastare la rappresentazione di un mittente e di un dominio, una pratica che viene spesso denominata *spoofing*, ovvero la falsificazione delle identità. La *posta falsificata* è un messaggio di posta elettronica in cui l'indirizzo del mittente è stato modificato in modo tale che sembra essere stato inviato da un mittente diverso dal mittente effettivo del messaggio.

I messaggi falsificati generalmente contengono un indirizzo del mittente di una determinata organizzazione. In passato era relativamente semplice effettuare lo spoofing dall'indirizzo del mittente, sia nella sessione SMTP, ad esempio l'intestazione MAIL FROM:, sia nei dati del messaggio RFC 2822, ad esempio Da: "Masato Kawai" masato@contoso.com, perché le intestazioni non venivano convalidate.

**Sommario**

Utilizzo dell'ID mittente per contrastare la falsificazione delle identità

Aggiornamento dei server DNS per l'accesso a Internet dell'organizzazione per il supporto dell'ID mittente

Identificazione dei destinatari e dei domini mittente da escludere dal filtro dell'ID mittente

## Utilizzo dell'ID mittente per contrastare la falsificazione delle identità

ID mittente rende più difficile la falsificazione dell'identità. Quando si abilita l'ID mittente, ciascun messaggio contiene uno stato dell'ID mittente nei metadati del messaggio. Quando si riceve un messaggio di posta elettronica, il server di Exchange interroga il server DNS del mittente per verificare che l'indirizzo IP da cui è stato ricevuto il messaggio sia autorizzato a inviare messaggi per il dominio specificato nelle intestazioni del messaggio. L'indirizzo IP del server mittente autorizzato viene definito PRA (Purported Responsible Address).

Gli amministratori dei domini pubblicano i record SPF (Sender Policy Framework) sui server DNS amministrati I record SPF identificano i server di posta elettronica in uscita autorizzati. Se un record SPF viene configurato sul server DNS del mittente, il server di Exchange analizza il record SPF e determina se l'indirizzo IP da cui è stato ricevuto il messaggio è autorizzato a inviare la posta elettronica per conto del dominio specificato nel messaggio. Per ulteriori informazioni sul contenuto di un record SPF e su come crearne uno, vedere [ID mittente](https://go.microsoft.com/fwlink/p/?linkid=50977).

Il server di Exchange aggiorna i metadati del messaggio con lo stato dell'ID mittente basato sul record SPF. Una volta che il server di Exchange ha aggiornato i metadati del messaggio, il recapito del messaggio procede come al solito.

## Valori dello stato dell'ID mittente

Il processo di valutazione dell'ID mittente genera uno stato ID mittente per il messaggio. Lo stato dell'ID mittente viene utilizzato per valutare il livello di probabilità di posta indesiderata (SCL) del messaggio. È possibile impostare lo stato su uno dei seguenti valori:

  - **Pass   **Sia l'indirizzo IP che il PRA (Purported Responsible Address) hanno superato il controllo di verifica dell'ID mittente.

  - **Neutral   **I dati relativi all'ID mittente pubblicato non consentono di arrivare a conclusioni esplicite.

  - **Soft fail**   L'indirizzo IP del PRA potrebbe trovarsi nel set non consentito.

  - **Fail   **L'indirizzo IP non è consentito; non viene trovato alcun indirizzo PRA nella posta in arrivo o il dominio di invio non esiste.

  - **None**   Non esistono dati pubblicati sull'SFP nel DNS del mittente.

  - **TempError**   Si è verificato un errore DNS temporaneo, ad esempio il server DNS non è disponibile.

  - **PermError**   Il record DNS non è valido, ad esempio un errore nel formato del record.

Lo stato dell'ID mittente viene aggiunto ai metadati del messaggio e viene quindi convertito in una proprietà MAPI. Il filtro della posta elettronica indesiderata in Microsoft Outlook utilizza la proprietà MAPI durante la generazione del valore del livello di probabilità di posta indesiderata.

Outlook né visualizza lo stato dell'ID mittente né contrassegna necessariamente un messaggio come indesiderato a determinati valori dell'ID mittente. Outlook utilizza il valore dello stato dell'ID mittente solo durante il calcolo del valore del livello di probabilità di posta indesiderata.

Oltre ai sette scenari che generano gli stati dell'ID mittente, il processo di valutazione dell'ID mittente può rivelare delle istanze in cui manca l'intestazione Da: relativa all'indirizzo IP. In questo caso Indirizzo IP mancante, non è possibile impostare lo stato dell'ID mittente. ed Exchange continuerà a elaborare il messaggio senza includere lo stato dell'ID mittente nel messaggio. Il messaggio non verrà eliminato né rifiutato. In questo scenario, lo stato dell'ID mittente non viene impostato e viene inserita una voce nel registro eventi applicazioni.

Per ulteriori informazioni sulla visualizzazione dello stato dell'ID mittente nei messaggi, vedere [Contrassegni filtro posta indesiderata](anti-spam-stamps-exchange-2013-help.md).

## Opzioni dell'ID mittente per la gestione dei messaggi contraffatti e dei server DNS non raggiungibili

È, inoltre, possibile definire in che modo il server di Exchange gestisce i messaggi identificati come contraffatti e come si comporta questo server quando non è possibile raggiungere il server DNS. Le opzioni per la modalità di gestione dei messaggi contraffatti e dei server DNS non raggiungibili da parte di Exchange includono le seguenti azioni:

  - **Contrassegna lo stato**   Questa opzione è l'azione predefinita. In tutti i messaggi in ingresso nell'organizzazione lo stato dell'ID mittente è incluso nei metadati del messaggio.

  - **Rifiuta**   Se l'azione dell'ID mittente viene impostata su Rifiuta messaggio, exExchangeNoVersion rifiuta il messaggio e invia una risposta di errore SMTP al server di invio. La risposta di errore SMTP è una risposta di protocollo di livello 5*xx* in cui il testo è lo stato dell'ID mittente.

  - **Elimina**   Questa opzione elimina il messaggio senza informare il server di invio del sistema dell'eliminazione. Infatti il server Exchange invia un comando SMTP "OK" fittizio al server di invio ed elimina il messaggio. Poiché il server di invio presuppone che il messaggio sia stato inviato, non ripete l'invio del messaggio nella stessa sessione.

Per ulteriori informazioni su come configurare l'agente ID mittente, vedere [Gestione dell'ID mittente](manage-sender-id-exchange-2013-help.md).

Torna su

## Aggiornamento dei server DNS per l'accesso a Internet dell'organizzazione per il supporto dell'ID mittente

L'efficacia dell'ID mittente dipende da specifici dati DNS. Tanto più numerose sono le organizzazioni che aggiornano i server DNS per l'accesso a Internet utilizzando un record SPF, tanto più efficace è l'identificazione dei messaggi di posta elettronica contraffatti da parte dell'ID mittente.

Per supportare l'infrastruttura dell'ID mittente, è necessario aggiornare i dati DNS per l'accesso a Internet creando un record SPF e ospitandolo sui server DNS pubblici. Per ulteriori informazioni su come creare e distribuire i record SPF, vedere [ID mittente](https://go.microsoft.com/fwlink/p/?linkid=50977).

Torna su

## Identificazione dei destinatari e dei domini mittente da escludere dal filtro dell'ID mittente

In alcuni casi, può essere necessario escludere determinati destinatari e domini mittente dal filtro dell'ID mittente. Per eseguire tale operazione, specificare i destinatari e i domini del mittente utilizzando il cmdlet **Set-SenderIdConfig** in Exchange Management Shell. Per ulteriori informazioni, vedere [Set-SenderIdConfig](https://technet.microsoft.com/it-it/library/aa998859\(v=exchg.150\)).

Inizio pagina


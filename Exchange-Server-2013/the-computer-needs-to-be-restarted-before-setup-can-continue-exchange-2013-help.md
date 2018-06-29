---
title: "Per poter proseguire con l'installazione, è necessario riavviare il computer: Exchange 2013 Help"
TOCTitle: Per poter proseguire con l'installazione, è necessario riavviare il computer
ms:assetid: d5c73280-4e54-473a-b328-9673af11e2c0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.rebootpending(v=EXCHG.150)
ms:contentKeyID: 50481776
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Per poter proseguire con l'installazione, è necessario riavviare il computer

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2016-12-09_

Microsoft Exchange Server 2013 non può continuare l'installazione perché è stato rilevato che nel computer locale deve essere riavviato per completare l'installazione di altri programmi o gli aggiornamenti di Windows.

## Perché succede?

Quando i programmi e gli aggiornamenti di Windows vengono installati, apportano modifiche ai file memorizzati sul computer. Talvolta, nel corso dell'installazione, un programma o un aggiornamento di Windows deve apportare modifiche a un file in uso. In questo caso, è necessario riavviare il computer prima che altri programmi, ad esempio, Exchange 2013, possano essere installati. L'installazione di Exchange richiede che tutte le altre procedure di installazione siano terminate. In questo modo, può verificare che siano stati installati tutti i prerequisiti necessari al corretto funzionamento.

In alcuni casi, l'installazione della versione precedente di un programma o di un aggiornamento di Windows potrebbe non essere completata correttamente. In questa situazione, alcune modifiche non vengono applicate, facendo sì che Windows e altri programmi ritengano necessario un riavvio. Purtroppo, dal momento che l'installazione non riuscita non rimuove mai le modifiche, è possibile che l'applicazione degli aggiornamenti di Windows e l'installazione di altri programmi vengano bloccate. A ogni avvio dell'installazione di Exchange, verrà visualizzato questo errore.

## Come si risolve il problema?

Nella maggior parte dei casi, è sufficiente riavviare il computer. In alcuni casi, tuttavia, l'errore viene visualizzato anche dopo il riavvio del computer. Ciò accade quando l'installazione di un programma o di un aggiornamento di Windows deve apportare ulteriori modifiche, che necessitano di un riavvio del computer. Se l'errore viene visualizzato dopo il riavvio del computer, provare a ripetere l'operazione.

Se il computer è stato riavviato per più di un paio di volte e l'errore viene comunque visualizzato, provare a reinstallare i programmi o gli aggiornamenti di Windows appena installati. Questa situazione fa sì che un'installazione con errore venga completata correttamente.

Se dopo il riavvio del computer e la reinstallazione di programmi recenti o Windows aggiornamenti, è *ancora* visualizzato questo errore, si consiglia di contattare il supporto Microsoft. Verrà consentono di determinare il motivo per cui Windows e altre applicazioni possono essere inviati che computer deve essere riavviato. Per contattare il supporto tecnico Microsoft, passare al [supporto per Microsoft Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=525940).


> [!WARNING]
> Non provare a risolvere il problema eliminando oppure modificando manualmente chiavi o valori nel Registro di sistema di Windows. Infatti, questa operazione risolve il problema solo temporaneamente. Ciò è particolarmente importante nel caso in cui l'installazione non riuscita fa riferimento a un aggiornamento di Windows.


